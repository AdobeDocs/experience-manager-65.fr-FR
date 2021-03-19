---
title: Création du balisage dans une application AEM
seo-title: Création du balisage dans une application AEM
description: Utiliser des balises ou étendre des balises par programmation dans une application AEM personnalisée
seo-description: Utiliser des balises ou étendre des balises par programmation dans une application AEM personnalisée
uuid: 0549552e-0d51-4162-b418-babf4ceee046
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: 032aea1f-0105-4299-8d32-ba6bee78437f
feature: Balisage
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '894'
ht-degree: 77%

---


# Création du balisage dans une application AEM{#building-tagging-into-an-aem-application}

Dans un contexte de programmation par balises ou d’extension de balises dans une application AEM personnalisée, cette page décrit l’utilisation de

* [l’API de balisage ](https://helpx.adobe.com/fr/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/tagging/package-summary.html)

qui interagit avec le

* [cadre de balisage](/help/sites-developing/framework.md)

Pour plus d’informations sur le balisage, voir :

* [Administration des ](/help/sites-administering/tags.md) balises pour en savoir plus sur la création et la gestion des balises, ainsi que sur les balises de contenu qui ont été appliquées.
* [Utilisation des balises](/help/sites-authoring/tags.md) pour plus d’informations sur le balisage du contenu.

## Vue d’ensemble de l’API de balisage {#overview-of-the-tagging-api}

L’implémentation du [cadre de balisage](/help/sites-developing/framework.md) dans AEM permet la gestion des balises et du contenu des balises à l’aide de l’API JCR . TagManager garantit que les balises entrées en tant que valeurs sur la propriété de tableau de chaînes `cq:tags` ne sont pas dupliquées. Il supprime les TagID pointant vers des balises non existantes et met à jour les TagID pour les balises déplacées ou fusionnées. TagManager utilise un écouteur d’observation JCR qui annule les modifications incorrectes. Les principales classes sont stockées dans le module [com.day.cq.tagging](https://helpx.adobe.com/fr/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/index.html?com/day/cq/tagging/package-summary.html) :

* JcrTagManagerFactory - renvoie une implémentation JCR d’un `TagManager`. C’est l’implémentation de référence de l’API de balisage.
* `TagManager` – permet de résoudre et de créer des balises par chemins et noms.
* `Tag` – définit l’objet de balise.

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

Un objet `Tag` peut être récupéré à l’aide du `TagManager`, en résolvant une balise existante ou en en créant une autre :

```java
Tag tag = tagManager.resolve("my/tag"); // for existing tags

Tag tag = tagManager.createTag("my/tag"); // for new tags
```

Pour l’implémentation basée sur JCR, qui mappe les `Tags` à des `Nodes` JCR, vous pouvez directement utiliser le mécanisme `adaptTo` de Sling si vous disposez de la ressource (par exemple, `/content/cq:tags/default/my/tag`) :

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
>L’adaptation directe de `Node` à `Tag` n’est pas possible, car la fonction `Node` n’implémente pas la méthode Sling `Adaptable.adaptTo(Class)`.

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

`CQ.tagging.TagInputField` est un widget de formulaire qui permet de saisir des balises. Il dispose d’un menu contextuel permettant de faire une sélection parmi les balises existantes, et inclut la saisie semi-automatique, ainsi que bien d’autres fonctions. Son xtype est `tags`.

## Tag Garbage Collector {#the-tag-garbage-collector}

Tag Garbage Collector est un service d’arrière-plan qui nettoie les balises masquées et inutilisées. Les balises masquées et inutilisées sont des balises inférieures à `/content/cq:tags` qui possèdent une propriété `cq:movedTo` et ne sont pas utilisées sur un noeud de contenu ; elles ont un nombre égal à zéro. Avec ce processus de suppression à l’arrière-plan, le nœud de contenu (c’est-à-dire la propriété `cq:tags`) n’a pas besoin d’être mis à jour lors du déplacement ou de la fusion. Les références de la propriété `cq:tags` sont automatiquement mises à jour lorsque la propriété `cq:tags` est mise à jour, par ex. via la boîte de dialogue des propriétés de la page.

Tag Garbage Collector s’exécute par défaut une fois par jour. Cette fréquence peut être configurée sur : 

```xml
http://localhost:4502/system/console/configMgr/com.day.cq.tagging.impl.TagGarbageCollector
```

## Recherche de balises et obtention de la liste des balises {#tag-search-and-tag-listing}

La recherche de balises et l’obtention de la liste des balises fonctionnent comme suit :

* La recherche de TagID recherche les balises pour lesquelles la propriété `cq:movedTo` est définie sur TagID et suit l&#39;ensemble des balises `cq:movedTo` TagID.

* La recherche du titre de la balise recherche uniquement les balises qui ne possèdent pas de propriété `cq:movedTo`.

## Balises dans différentes langues {#tags-in-different-languages}

Comme décrit dans la documentation relative à l’administration des balises, dans la section [Gestion des balises dans différentes langues](/help/sites-administering/tags.md#managing-tags-in-different-languages), une balise `title`peut être définie dans différentes langues. Une propriété sensible à la langue est ensuite ajoutée au nœud de la balise. Cette propriété a le format `jcr:title.<locale>`, par ex. `jcr:title.fr` pour la traduction en français. `<locale>` doit être une chaîne de paramètres régionaux ISO en minuscules et utiliser &quot;_&quot; au lieu de &quot;-&quot;, par exemple :  `de_ch`.

Lorsque la balise **Animaux** est ajoutée à la page **Produits**, la valeur `stockphotography:animals` est ajoutée à la propriété `cq:tags` du noeud /content/geometrixx/fr/products/jcr:content. La traduction est référencée à partir du nœud de balise.

L’API côté serveur dispose de méthodes liées à `title` localisées :

* [com.day.cq.tagging.Tag](https://helpx.adobe.com/fr/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/index.html?com/day/cq/tagging/Tag.html)

   * getLocalizedTitle(Locale locale)
   * getLocalizedTitlePaths()
   * getLocalizedTitles()
   * getTitle(Locale locale)
   * getTitlePath(Locale locale)

* [com.day.cq.tagging.TagManager](https://helpx.adobe.com/fr/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/index.html?com/day/cq/tagging/TagManager.html)

   * canCreateTagByTitle(String tagTitlePath, Locale locale)
   * createTagByTitle(String tagTitlePath, Locale locale)
   * resolveByTitle(String tagTitlePath, Locale locale)

Dans AEM, la langue peut être identifiée à partir de la langue de la page ou de l’utilisateur:

* pour récupérer la langue de la page dans une JSP :

   * `currentPage.getLanguage(false)`

* pour récupérer la langue de l’utilisateur dans une JSP :

   * `slingRequest.getLocale()`

`currentPage` et `slingRequest` sont disponibles dans une JSP via la balise [&lt;cq:definedObjects>](/help/sites-developing/taglib.md).

Pour le balisage, la localisation dépend du contexte, car la balise `titles` peut être affichée dans la langue de la page, dans la langue de l’utilisateur ou dans toute autre langue.

### Ajout d’une langue à la boîte de dialogue Modifier la balise {#adding-a-new-language-to-the-edit-tag-dialog}

La procédure suivante décrit comment ajouter une langue (finnois) à la boîte de dialogue **Modifier la balise** :

1. Dans **CRXDE**, modifiez la propriété multi-valeur `languages` du nœud `/content/cq:tags`.

1. Ajoutez `fi_fi` (code langue pour le finlandais) et enregistrez les modifications.

La nouvelle langue (finnois) est désormais disponible dans la boîte de dialogue des propriétés de la page et dans la boîte de dialogue **Modifier la balise** lors de la modification d’une balise dans la console **Balisage**.

>[!NOTE]
>
>La nouvelle langue doit faire partie de celles reconnues par AEM, c’est-à-dire qu’elle doit être disponible sous `/libs/wcm/core/resources/languages`.

