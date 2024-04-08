---
title: Créer le balisage dans une application AEM
description: Utilisation ou extension de balises par programmation dans une application AEM personnalisée
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
feature: Tagging
exl-id: d885520d-d0ed-45fa-8511-faa2495d667a
solution: Experience Manager, Experience Manager Sites
source-git-commit: f22f51b4d65abf4cf1f6e04952f873eca5119727
workflow-type: tm+mt
source-wordcount: '868'
ht-degree: 95%

---

# Créer le balisage dans une application AEM{#building-tagging-into-an-aem-application}

Dans un contexte de programmation par balises ou d’extension de balises dans une application AEM personnalisée, ce document décrit l’utilisation de

* [l’API de balisage](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/tagging/package-summary.html)

qui interagit avec le

* [framework de balisage](/help/sites-developing/framework.md)

Pour plus d’informations sur le balisage, consultez :

* La section [Administration des balises](/help/sites-administering/tags.md) pour plus d’informations sur la manière de créer et gérer des balises et déterminer à quel contenu elles ont été appliquées.
* La section [Utilisation de balises](/help/sites-authoring/tags.md) pour plus d’informations sur le balisage de contenu.

## Vue d’ensemble de l’API de balisage {#overview-of-the-tagging-api}

L’implémentation du [cadre de balisage](/help/sites-developing/framework.md) dans AEM permet la gestion des balises et du contenu des balises à l’aide de l’API JCR. TagManager garantit que les balises saisies en tant que valeurs dans la propriété de tableau de chaîne de caractères `cq:tags` ne sont pas dupliquées, supprime les TagID pointant vers des balises non existantes et met à jour les TagID pour les balises déplacées ou fusionnées. TagManager utilise un écouteur d’observation JCR qui annule les modifications incorrectes. Les principales classes sont stockées dans le package [com.day.cq.tagging](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/index.html?com/day/cq/tagging/package-summary.html) :

* JcrTagManagerFactory - Renvoie une implémentation JCR d’un `TagManager`. C’est l’implémentation de référence de l’API de balisage.
* `TagManager` – permet de résoudre et de créer des balises par chemins et noms.
* `Tag` – définit l’objet de balise.

### Récupération d’un TagManager basé sur JCR {#getting-a-jcr-based-tagmanager}

Pour récupérer une instance de TagManager, vous devez disposer d’une `Session` JCR et appeler `getTagManager(Session)` :

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

Une `Tag` peut être récupérée à l’aide du `TagManager`, en résolvant une balise existante ou en en créant une nouvelle :

```java
Tag tag = tagManager.resolve("my/tag"); // for existing tags

Tag tag = tagManager.createTag("my/tag"); // for new tags
```

Pour l’implémentation basée sur JCR, qui mappe les `Tags` à des `Nodes` JCR, vous pouvez directement utiliser le mécanisme `adaptTo` de Sling si vous disposez de la ressource (par exemple, `/content/cq:tags/default/my/tag`) :

```java
Tag tag = resource.adaptTo(Tag.class);
```

Même si une balise peut seulement être convertie à partir d’une ressource (et non d’un nœud), une balise peut être convertie à la fois en un nœud et une ressource :

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

Le widget de formulaire `CQ.tagging.TagInputField` est destiné à la saisie de balises. Il dispose d’un menu contextuel permettant de faire une sélection parmi les balises existantes, et inclut la saisie semi-automatique, ainsi que bien d’autres fonctions. Son xtype est `tags`.

## Tag Garbage Collector {#the-tag-garbage-collector}

Tag Garbage Collector est un service d’arrière-plan qui nettoie les balises masquées et inutilisées. Les balises masquées et non utilisées sont des balises `/content/cq:tags` qui ont une propriété `cq:movedTo` et ne sont pas appliquées à un nœud de contenu. Leur nombre est nul. Avec ce processus de suppression à l’arrière-plan, le nœud de contenu (c’est-à-dire la propriété `cq:tags`) n’a pas besoin d’être mis à jour lors du déplacement ou de la fusion. Les références de la propriété `cq:tags` sont automatiquement mises à jour lorsque la propriété `cq:tags` est mise à jour, par exemple via la boîte de dialogue des propriétés de la page.

Tag Garbage Collector s’exécute par défaut une fois par jour. Vous pouvez le configurer à partir des éléments suivants :

```xml
http://localhost:4502/system/console/configMgr/com.day.cq.tagging.impl.TagGarbageCollector
```

## Recherche de balises et obtention de la liste des balises {#tag-search-and-tag-listing}

La recherche de balises et l’obtention de la liste des balises fonctionnent comme suit :

* La recherche de TagID recherche les balises dont la propriété `cq:movedTo` est définie sur TagID et suit les balises `cq:movedTo`.

* La recherche de titre de balise recherche uniquement les balises qui n’ont pas de propriété `cq:movedTo`.

## Balises dans différentes langues {#tags-in-different-languages}

Comme le décrit la documentation relative à la gestion des balises, dans la section [Gestion des balises dans différentes langues](/help/sites-administering/tags.md#managing-tags-in-different-languages), une balise `title` peut être définie dans différentes langues. Une propriété sensible à la langue est ensuite ajoutée au nœud de la balise. Cette propriété a le format `jcr:title.<locale>`, par ex. `jcr:title.fr` pour la traduction en français. `<locale>` doit être une chaîne en langue locale ISO en minuscules et utiliser « _ » au lieu de « - », par exemple : `de_ch`.

Lorsque la balise **Animals** est ajoutée à la page **Produits**, la valeur `stockphotography:animals` est ajoutée à la propriété `cq:tags` du nœud /content/geometrixx/fr/products/jcr:content. La traduction est référencée à partir du nœud de balise.

L’API côté serveur dispose de méthodes liées à `title` localisées :

* [com.day.cq.tagging.Tag](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/index.html?com/day/cq/tagging/Tag.html)

   * getLocalizedTitle(Locale locale)
   * getLocalizedTitlePaths()
   * getLocalizedTitles()
   * getTitle(Locale locale)
   * getTitlePath(Locale locale)

* [com.day.cq.tagging.TagManager](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/index.html?com/day/cq/tagging/TagManager.html)

   * canCreateTagByTitle(String tagTitlePath, Locale locale)
   * createTagByTitle(String tagTitlePath, Locale locale)
   * resolveByTitle(String tagTitlePath, Locale locale)

Dans AEM, la langue peut être identifiée à partir de la langue de la page ou de l’utilisateur :

* pour récupérer la langue de la page dans un JSP :

   * `currentPage.getLanguage(false)`

* pour récupérer la langue de l’utilisateur dans un JSP :

   * `slingRequest.getLocale()`

`currentPage` et `slingRequest` sont disponibles dans un JSP via la balise [&lt;cq:definedObjects>](/help/sites-developing/taglib.md).

Pour le balisage, la localisation dépend du contexte, car la balise `titles` peut être affichée dans la langue de la page, dans la langue de l’utilisateur ou de l’utilisatrice ou dans toute autre langue.

### Ajout d’une langue à la boîte de dialogue Modifier la balise {#adding-a-new-language-to-the-edit-tag-dialog}

La procédure suivante décrit comment ajouter une langue (par exemple, finnois) à la boîte de dialogue **Modifier la balise** :

1. Dans **CRXDE**, modifiez la propriété multi-valeur `languages` du nœud `/content/cq:tags`.

1. Ajoutez `fi_fi` (code langue pour le finnois) et enregistrez les modifications.

La nouvelle langue (finnois) est désormais disponible dans la boîte de dialogue des propriétés de la page et dans la boîte de dialogue **Modifier la balise** lors de la modification d’une balise dans la console **Balisage**.

>[!NOTE]
>
>La nouvelle langue doit être une des langues reconnues par AEM. En d’autres termes, elle doit être disponible sous forme de nœud sous `/libs/wcm/core/resources/languages`.

>[!CAUTION]
>
>L’installation du balisage du contenu prêt à l’emploi par le biais d’un module de mise à jour officiel (y compris les Service Packs, les Service Packs de sécurité, les Feature Packs étendus, les Cumulative Feature Packs, les correctifs etc.) réinitialise la propriété languages de la propriété `/content/cq:tags` par défaut. Il est donc nécessaire de l’ajouter à partir des propriétés avant l’installation.
