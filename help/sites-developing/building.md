---
title: Création du balisage dans une application AEM
seo-title: Création du balisage dans une application AEM
description: Travailler par programmation avec des balises ou étendre des balises dans une application AEM personnalisée
seo-description: Travailler par programmation avec des balises ou étendre des balises dans une application AEM personnalisée
uuid: 0549552e-0d51-4162-b418-babf4ceee046
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: 032aea1f-0105-4299-8d32-ba6bee78437f
translation-type: tm+mt
source-git-commit: 1493b301ecf4c25f785495e11ead352de600ddb7
workflow-type: tm+mt
source-wordcount: '893'
ht-degree: 59%

---


# Création du balisage dans une application AEM{#building-tagging-into-an-aem-application}

Dans un contexte de programmation par balises ou d’extension de balises dans une application AEM personnalisée, cette page décrit l’utilisation de

* [l’API de balisage ](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/tagging/package-summary.html)

qui interagit avec le

* [framework de balisage](/help/sites-developing/framework.md)

Pour plus d’informations sur le balisage, voir :

* [Administration des balises](/help/sites-administering/tags.md) pour en savoir plus sur la création et la gestion des balises, ainsi que sur les balises de contenu qui ont été appliquées.
* [Utilisation des balises](/help/sites-authoring/tags.md) pour plus d’informations sur le balisage du contenu.

## Vue d’ensemble de l’API de balisage {#overview-of-the-tagging-api}

L’implémentation du [framework de balisage](/help/sites-developing/framework.md) dans AEM permet la gestion des balises et du contenu des balises à l’aide de l’API JCR. The TagManager ensures that tags entered as values on the `cq:tags` string array property are not duplicated, it removes TagIDs pointing to non-existing tags and updates TagIDs for moved or merged tags. TagManager utilise un écouteur d’observation JCR qui annule les modifications incorrectes. Les principales classes sont stockées dans le modules [com.day.cq.tagging](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/index.html?com/day/cq/tagging/package-summary.html) :

* JcrTagManagerFactory - renvoie une implémentation JCR d’un `TagManager`. C’est l’implémentation de référence de l’API de balisage.
* `TagManager` - permet de résoudre et de créer des balises par chemins et noms.
* `Tag` - définit l’objet tag.

### Récupération d’un TagManager basé sur JCR {#getting-a-jcr-based-tagmanager}

Pour récupérer une instance de TagManager, vous devez disposer d’une `Session` JRC et appeler `getTagManager(Session)` :

```java
@Reference
JcrTagManagerFactory jcrTagManagerFactory;

TagManager tagManager = jcrTagManagerFactory.getTagManager(session);
```

Dans le contexte standard de Sling, vous pouvez également effectuer une adaptation à un `TagManager` à partir du `ResourceResolver` : 

```java
TagManager tagManager = resourceResolver.adaptTo(TagManager.class);
```

### Récupération d’un objet Tag {#retrieving-a-tag-object}

A `Tag` can be retrieved through the `TagManager`, by either resolving an existing tag or creating a new one:

```java
Tag tag = tagManager.resolve("my/tag"); // for existing tags

Tag tag = tagManager.createTag("my/tag"); // for new tags
```

For the JCR-based implementation, which maps `Tags` onto JCR `Nodes`, you can directly use Sling&#39;s `adaptTo` mechanism if you have the resource (e.g. such as `/content/cq:tags/default/my/tag`):

```java
Tag tag = resource.adaptTo(Tag.class);
```

Bien qu’une balise ne puisse être convertie que *à partir d’une ressource (et non d’un noeud), une balise peut être convertie *en *à la fois un noeud et une ressource :

```java
Node node = tag.adaptTo(Node.class);
Resource node = tag.adaptTo(Resource.class);
```

>[!NOTE]
>
>Directly adapting from `Node` to `Tag` is not possible, because `Node` does not implement the Sling `Adaptable.adaptTo(Class)` method.

### Récupération et définition des balises {#getting-and-setting-tags}

```java
// Getting the tags of a Resource:
Tag[] tags = tagManager.getTags(resource);

// Setting tags to a Resource:
tagManager.setTags(resource, tags);
```

### Recherche de balises {#searching-for-tags}

```java
// Searching for the Resource objects that are tagged with the tag object:
Iterator<Resource> it = tag.find();

// Retrieving the usage count of the tag object:
long count = tag.getCount();

// Searching for the Resource objects that are tagged with the tagID String:
 RangeIterator<Resource> it = tagManager.find(tagID);
```

>[!NOTE]
>
>`RangeIterator` valide à utiliser :
>
>`com.day.cq.commons.RangeIterator`

### Suppression des balises {#deleting-tags}

```java
tagManager.deleteTag(tag);
```

### Réplication de balises {#replicating-tags}

Il est possible d’utiliser le service de réplication (`Replicator`) avec des balises dans la mesure où elles sont de type `nt:hierarchyNode` : 

```java
replicator.replicate(session, replicationActionType, tagPath);
```

## Balisage du côté client {#tagging-on-the-client-side}

`CQ.tagging.TagInputField` est un widget de formulaire qui permet de saisir des balises. Il dispose d’un menu contextuel permettant de faire une sélection parmi les balises existantes, et inclut la saisie semi-automatique, ainsi que bien d’autres fonctions. Its xtype is `tags`.

## Le Tag Garbage Collector {#the-tag-garbage-collector}

Le récupérateur de balises est un service d’arrière-plan qui nettoie les balises qui sont masquées et inutilisées. Hidden and unused tags are tags below `/content/cq:tags` that have a `cq:movedTo` property and are not used on a content node - they have a count of zero. Avec ce processus de suppression à l’arrière-plan, le nœud de contenu (c’est-à-dire la propriété `cq:tags`) n’a pas besoin d’être mis à jour lors du déplacement ou de la fusion. Les références de la propriété `cq:tags` sont automatiquement mises à jour lorsque la propriété `cq:tags` est mise à jour, par ex. via la boîte de dialogue des propriétés de la page.

Le Tag Garbage Collector s’exécute par défaut une fois par jour. Cette fréquence peut être configurée sur : 

```xml
http://localhost:4502/system/console/configMgr/com.day.cq.tagging.impl.TagGarbageCollector
```

## Recherche de balises et listing des balises {#tag-search-and-tag-listing}

La recherche de balises et le listing des balises fonctionnent comme suit :

* The search for TagID searches for the tags that have the property `cq:movedTo` set to TagID and follows through the `cq:movedTo` TagIDs.

* The search for tag Title only searches the tags that do not have a `cq:movedTo` property.

## Balises dans différentes langues {#tags-in-different-languages}

As described in the documentation for administering tags, in the section [Managing Tags in Different Languages](/help/sites-administering/tags.md#managing-tags-in-different-languages), a tag `title`can be defined in different languages. Une propriété sensible à la langue est ensuite ajoutée au nœud de la balise. Cette propriété a le format `jcr:title.<locale>`, par exemple `jcr:title.fr` pour la traduction française. `<locale>` doit être une chaîne de paramètres régionaux ISO en minuscules et utiliser &quot;_&quot; au lieu de &quot;-&quot;, par exemple : `de_ch`.

When the **Animals** tag is added to the **Products** page, the value `stockphotography:animals` is added to the property `cq:tags` of the node /content/geometrixx/en/products/jcr:content. La traduction est référencée à partir du nœud de balise.

L’API côté serveur a localisé des méthodes liées à `title` :

* [com.day.cq.tagging.Tag](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/index.html?com/day/cq/tagging/Tag.html)

   * getLocalizedTitle(Locale locale)
   * getLocalizedTitlePaths()
   * getLocalizedTitles()
   * getTitle(Locale locale)
   * getTitlePath(Locale locale)

* [com.day.cq.tagging.TagManager](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/index.html?com/day/cq/tagging/TagManager.html)

   * canCreateTagByTitle(String tagTitlePath, Locale locale)
   * createTagByTitle(String tagTitlePath, Locale locale)
   * resolveByTitle(String tagTitlePath, Locale locale)

Dans AEM, la langue peut être identifiée à partir de la langue de la page ou de la langue de l’utilisateur :

* pour récupérer la langue de la page dans une JSP :

   * `currentPage.getLanguage(false)`

* pour récupérer la langue de l’utilisateur dans une JSP :

   * `slingRequest.getLocale()`

`currentPage` et `slingRequest` sont disponibles dans une JSP via la balise [&lt;cq:definedObjects>](/help/sites-developing/taglib.md).

Pour le balisage, la localisation dépend du contexte, car la balise `titles` peut être affichée dans la langue de la page, dans la langue de l’utilisateur ou dans toute autre langue.

### Ajout d’une langue à la boîte de dialogue Modifier la balise {#adding-a-new-language-to-the-edit-tag-dialog}

La procédure suivante décrit comment ajouter une langue (finnois) à la boîte de dialogue **Modifier la balise** :

1. In **CRXDE**, edit the multi-value property `languages` of the node `/content/cq:tags`.

1. Ajoutez `fi_fi` (code langue pour le finlandais) et enregistrez les modifications.

La nouvelle langue (finnois) est désormais disponible dans la boîte de dialogue des propriétés de la page et dans la boîte de dialogue **Modifier la balise** lors de la modification d’une balise dans la console **Balisage**.

>[!NOTE]
>
>La nouvelle langue doit faire partie de celles reconnues par AEM, c’est-à-dire qu’elle doit être disponible sous `/libs/wcm/core/resources/languages`.

