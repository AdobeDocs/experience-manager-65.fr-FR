---
title: Étendre la fonctionnalité de recherche des ressources d’Adobe Experience Manager
description: Étendez les fonctionnalités de recherche des ressources Adobe Experience Manager au-delà des valeurs par défaut.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 566add37d6dd7efe22a99fc234ca42878f050aee
workflow-type: tm+mt
source-wordcount: '859'
ht-degree: 75%

---


# Étendre la recherche de ressources{#extending-assets-search}

Vous pouvez étendre les fonctionnalités [!DNL Adobe Experience Manager Assets] de recherche. Out of the box, [!DNL Experience Manager Assets] searches for assets by strings.

La recherche est effectuée par le biais de l’interface QueryBuilder, de sorte qu’elle puisse être personnalisée avec plusieurs prédicats. Vous pouvez remplacer l’ensemble des prédicats par défaut dans le répertoire suivant : `/apps/dam/content/search/searchpanel/facets`.

You can also add additional tabs to the [!DNL Assets] admin panel.

>[!CAUTION]
>
>As of [!DNL Experience Manager] 6.4, Classic UI is deprecated. For announcement, see [deprecated and removed features](https://docs.adobe.com/content/help/en/experience-manager-64/release-notes/deprecated-removed-features.html). Adobe recommande l’utilisation de l’interface utilisateur tactile. For customization, see [search facets](/help/assets/search-facets.md).

## Incrustation {#overlaying}

To overlay the pre-configured predicates, copy the `facets` node from `/libs/dam/content/search/searchpanel` to `/apps/dam/content/search/searchpanel/` or specify another `facetURL` property in the `searchpanel` configuration (the default is to `/libs/dam/content/search/searchpanel/facets.overlay.infinity.json`).

![screen_shot_2012-06-05at113619am](assets/screen_shot_2012-06-05at113619am.png)

>[!NOTE]
>
>Par défaut, la structure de répertoire sous /`apps` n’existe pas et doit être créée. Assurez-vous que les types de nœuds correspondent à ceux existant sous / `libs`.

## Ajouter des onglets {#adding-tabs}

Vous pouvez ajouter d’autres onglets de recherche en les configurant dans l’interface d’administration Ressources. Pour créer des onglets supplémentaires, procédez comme suit :

1. Créez la structure de dossiers `/apps/wcm/core/content/damadmin/tabs,`si elle n’existe pas encore, puis copiez le nœud `tabs` dans le répertoire `/libs/wcm/core/content/damadmin` et collez-le.
1. Créez et configurez le second onglet, le cas échéant.

   >[!NOTE]
   >
   >Lorsque vous créez un second nœud `siteadminsearchpanel`, assurez-vous de définir une propriété `id` afin d’éviter tout conflit de formulaire.

## Création de prédicats personnalisés {#creating-custom-predicates}

[!DNL Assets] est fourni avec un ensemble de prédicats prédéfinis qui peuvent être utilisés pour personnaliser une page de partage de ressources. Customizing an Asset Share in this way is covered in [create and configure an Asset Share page](/help/assets/assets-finder-editor.md#creating-and-configuring-an-asset-share-page).

In addition to using pre-existing predicates, Experience Manager developers can also create their own predicates using the [Query Builder API](/help/sites-developing/querybuilder-api.md).

La création de prédicats personnalisés nécessite des connaissances de base sur la [structure des widgets](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html).

La pratique recommandée consiste à copier un prédicat existant, puis à le modifier. Des exemples de prédicats sont disponibles dans le répertoire **/libs/cq/search/components/predicates**.

### Exemple : création d’un prédicat de propriété simple   {#example-build-a-simple-property-predicate}

Pour créer un prédicat de propriété, procédez comme suit :

1. Créez un dossier de composant dans votre répertoire de projets, par exemple **/apps/geometrixx/components/titlepredicate**.
1. Ajoutez **content.xml** :

   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <jcr:root xmlns:sling="https://sling.apache.org/jcr/sling/1.0" xmlns:cq="https://www.day.com/jcr/cq/1.0" xmlns:jcr="https://www.jcp.org/jcr/1.0"
       jcr:primaryType="cq:Component"
       jcr:title="Title Predicate"
       sling:resourceSuperType="foundation/components/parbase"
       allowedParents="[*/parsys]"
       componentGroup="Search"/>
   ```

1. Ajoutez `titlepredicate.jsp`.

   ```java
   <%--
   
     Sample title predicate component
   
   --%><%@ page import="java.util.Calendar" %><%
   %><%@include file="/libs/foundation/global.jsp"%><%
   
       // A unique id is necessary in case this predicate is inserted multiple times on the same page
       String elemId = "cq-predicate-" +  Long.toString(Calendar.getInstance().getTimeInMillis());
   
   %><div class="predicatebox">
   
       <div class="title">Title</div>
   
       <%-- The wrapper for the form elements. All items will be append to this wrapper. --%>
       <div id="<%= elemId %>" class="content"></div>
   
   </div><script type="text/javascript">
   
       CQ.Ext.onLoad(function() {
   
           var predicateName = "property";
           var propertyName = "jcr:content/metadata/dc:title";
           var elemId = "<%= elemId %>";
   
           // Get the page wide available QueryBuilder.
           var qb = CQ.search.Util.getQueryBuilder();
   
           // createId adds a counter to the predicate name - useful in case this predicate
           // is inserted multiple times on the same page.
           var id = qb.createId(predicateName);
   
           // Hidden field that defines the property to search for; in our case this
           // is the "dc:title" metadata. The name "property" (or "1_property", "2_property" etc.)
           // indicates the server to use the property predicate
           // (com.day.cq.search.eval.JcrPropertyPredicateEvaluator).
           qb.addField({
               "xtype": "hidden",
               "renderTo": elemId,
               "name": id,
               "value": propertyName
           });
   
           // The visible text field. The name has to be like the one of the hidden field above
           // plus the ".value" suffix.
           qb.addField({
               "xtype": "textfield",
               "renderTo": elemId,
               "name": id + ".value"
           });
   
           // Depending on the predicate additional parameters allow to configure the
           // predicate. Here we add an operation parameter to create a "like" query.
           // Again note the name set to the id and a suffix.
           qb.addField({
               "xtype": "hidden",
               "renderTo": elemId,
               "name": id + ".operation",
               "value": "like"
           });
       });
   </script>
   ```

1. Pour rendre le composant accessible, vous devez être en mesure de le modifier. Pour rendre un composant modifiable, dans CRXDE, ajoutez un nœud **cq:editConfig** de type principal **cq:EditConfig**. Pour pouvoir supprimer des paragraphes, ajoutez une propriété **cq:actions** à plusieurs valeurs avec une seule valeur de **DELETE**.
1. Accédez à votre navigateur puis, sur votre exemple de page (par exemple **press.html**), basculez en mode de conception et activez votre nouveau composant pour le système de paragraphes de prédicats (par exemple **left**).

1. En mode d’**édition**, le nouveau composant est désormais disponible dans le sidekick (accessible dans le groupe **Recherche**). Insérez le composant dans la colonne **Prédicats** et saisissez un mot de recherche, par exemple **Diamant**, puis cliquez sur la loupe pour lancer la recherche.

   >[!NOTE]
   >
   >Lors de la recherche, assurez-vous de saisir le terme exact en respectant la casse.

### Exemple : création d’un prédicat de groupe simple {#example-build-a-simple-group-predicate}

Pour créer un prédicat de groupe, procédez comme suit :

1. Créez un dossier de composant dans votre répertoire de projets, par exemple **/apps/geometrixx/components/picspredicate**.
1. Ajoutez **content.xml** :

   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <jcr:root xmlns:sling="https://sling.apache.org/jcr/sling/1.0" xmlns:cq="https://www.day.com/jcr/cq/1.0" xmlns:jcr="https://www.jcp.org/jcr/1.0"
       jcr:primaryType="cq:Component"
       jcr:title="Image Formats"
       sling:resourceSuperType="foundation/components/parbase"
       allowedParents="[*/parsys]"
       componentGroup="Search"/>
   ```

1. Ajoutez **titlepredicate.jsp** :

   ```java
   <%--
   
     Sample group predicate component
   
   --%><%@ page import="java.util.Calendar" %><%
   %><%@include file="/libs/foundation/global.jsp"%><%
   
       // A unique id is necessary in case this predicate is inserted multiple times on the same page.
       String elemId = "cq-predicate-" +  Long.toString(Calendar.getInstance().getTimeInMillis());
   
   %><div class="predicatebox">
   
       <div class="title">Image Formats</div>
   
       <%-- The wrapper for the form elements. All items will be append to this wrapper. --%>
       <div id="<%= elemId %>" class="content"></div>
   
   </div><script type="text/javascript">
   
       CQ.Ext.onLoad(function() {
   
           var predicateName = "property";
           var propertyName = "jcr:content/metadata/dc:format";
           var elemId = "<%= elemId %>";
   
           // Get the page wide available QueryBuilder.
           var qb = CQ.search.Util.getQueryBuilder();
   
           // Create a unique group ID; will return e.g. "1_group".
           var groupId = qb.createGroupId();
   
           // Hidden field that defines the property to search for  - in our case "dc:format" -
           // and declares the group of predicates. "property" in the name ("1_group.property")
           // indicates to the server to use the "property predicate"
           // (com.day.cq.search.eval.JcrPropertyPredicateEvaluator).
           qb.addField({
               "xtype": "hidden",
               "renderTo": "<%= elemId %>",
               "name": groupId + "." + predicateName, // 1_group.property
               "value": propertyName
           });
   
           // Declare to combine the multiple values using OR.
           qb.add(new CQ.Ext.form.Hidden({
               "name": groupId + ".p.or",  // 1_group.p.or
               "value": "true"
           }));
   
           // The options
           var options = [
               { "label":"JPEG", "value":"image/jpeg"},
               { "label":"PNG",  "value":"image/png" },
               { "label":"GIF",  "value":"image/gif" }
           ];
   
           // Build a checkbox for each option.
           for (var i = 0; i < options.length; i++) {
               qb.addField({
                   "xtype": "checkbox",
                   "renderTo": "<%= elemId %>",
                   // 1_group.property.0_value, 1_group.property.1_value etc.
                   "name": groupId + "." +  predicateName + "." + i + "_value",
                   "inputValue": options[i].value,
                   "boxLabel": options[i].label,
                   "listeners": {
                       "check": function() {
                           // Submit the search form when checking/unchecking a checkbox.
                           qb.submit();
                       }
                   }
               });
           }
       });
   ```

1. Pour rendre le composant accessible, vous devez être en mesure de le modifier. Pour rendre un composant modifiable, dans CRXDE, ajoutez un nœud **cq:editConfig** de type principal **cq:EditConfig**. Pour pouvoir supprimer des paragraphes, ajoutez une propriété **cq:actions** à plusieurs valeurs avec une seule valeur de **DELETE**.
1. Accédez à votre navigateur puis, sur votre exemple de page (par exemple **press.html**), basculez en mode de conception et activez votre nouveau composant pour le système de paragraphes de prédicats (par exemple **left**).
1. En mode d’**édition**, le nouveau composant est désormais disponible dans le sidekick (accessible dans le groupe **Recherche**). Insérez le composant dans la colonne **Prédicats**.

## Widgets de prédicats installés {#installed-predicate-widgets}

Les prédicats suivants sont disponibles sous forme de widgets ExtJS préconfigurés.

### FulltextPredicate   {#fulltextpredicate}

| Propriétés | Type | Description |
|---|---|---|
| predicateName | Chaîne | Nom du prédicat. La valeur par défaut est `fulltext` |
| searchCallback | Fonction | Callback for triggering search on event `keyup`. La valeur par défaut est `CQ.wcm.SiteAdmin.doSearch` |

### PropertyPredicate {#propertypredicate}

| Propriétés | Type | Description |
|---|---|---|
| predicateName | Chaîne | Nom du prédicat. La valeur par défaut est `property` |
| propertyName | Chaîne | Nom de la propriété JCR. La valeur par défaut est `jcr:title` |
| defaultValue | Chaîne | Valeur par défaut préremplie. |

### PathPredicate {#pathpredicate}

| Propriétés | Type | Description |
|---|---|---|
| predicateName | Chaîne | Nom du prédicat. La valeur par défaut est `path` |
| rootPath | Chaîne | Chemin racine du prédicat. La valeur par défaut est `/content/dam` |
| pathFieldPredicateName | Chaîne | La valeur par défaut est `folder` |
| showFlatOption | Booléen | Indicateur pour afficher la case à cocher `search in subfolders`. La valeur par défaut est « true ». |

### DatePredicate {#datepredicate}

| Propriétés | Type | Description |
|---|---|---|
| predicateName | Chaîne | Nom du prédicat. La valeur par défaut est `daterange` |
| propertyName | Chaîne | Nom de la propriété JCR. La valeur par défaut est `jcr:content/jcr:lastModified` |
| defaultValue | Chaîne | Valeur par défaut préremplie |

### OptionsPredicate {#optionspredicate}

| Propriétés | Type | Description |
|---|---|---|
| titre | Chaîne | Ajoute un titre supérieur supplémentaire |
| predicateName | Chaîne | Nom du prédicat. La valeur par défaut est `daterange` |
| propertyName | Chaîne | Nom de la propriété JCR. La valeur par défaut est `jcr:content/metadata/cq:tags` |
| collapse | Chaîne | Réduire par niveau. La valeur par défaut est `level1` |
| triggerSearch | Booléen | Indicateur de déclenchement de la recherche lors de la vérification. Par défaut : « false » |
| searchCallback | Fonction | Rappel pour déclencher la recherche. La valeur par défaut est `CQ.wcm.SiteAdmin.doSearch` |
| searchTimeoutTime | Nombre | Délai d’expiration avant le déclenchement de searchCallback. Valeur par défaut : 800 ms |

## Personnalisation des résultats de la recherche {#customizing-search-results}

La présentation des résultats de la recherche sur une page de partage des ressources est régie par la loupe sélectionnée. Experience Manager Assets est fourni avec un ensemble d’objectifs prédéfinis qui peuvent être utilisés pour personnaliser une page de partage de ressources. Ce processus de personnalisation d’un partage de ressources est abordé dans la section [Création et configuration d’une page de partage de ressources](/help/assets/assets-finder-editor.md#creating-and-configuring-an-asset-share-page).

Outre l’utilisation d’objectifs préexistants, les développeurs d’Experience Manager peuvent également créer leurs propres objectifs.
