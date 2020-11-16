---
title: Utilisation et extension de widgets (IU classique)
seo-title: Utilisation et extension de widgets (IU classique)
description: L’interface web d’AEM utilise AJAX et d’autres technologies modernes intégrées dans les navigateurs pour activer l’édition tel écran tel écrit (WYSIWYG) et permettre aux auteurs de mettre en forme le contenu directement sur la page web.
seo-description: L’interface web d’AEM utilise AJAX et d’autres technologies modernes intégrées dans les navigateurs pour activer l’édition tel écran tel écrit (WYSIWYG) et permettre aux auteurs de mettre en forme le contenu directement sur la page web.
uuid: eb3da415-cbef-4766-a28e-837e238a4156
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: components
content-type: reference
discoiquuid: 7b234f1f-4470-4de1-a3c3-ab19e5e001ad
docset: aem65
translation-type: tm+mt
source-git-commit: ec528e115f3e050e4124b5c232063721eaed8df5
workflow-type: tm+mt
source-wordcount: '4965'
ht-degree: 58%

---


# Utilisation et extension de widgets (IU classique){#using-and-extending-widgets-classic-ui}

>[!NOTE]
>
>Cette page décrit l’utilisation de widgets dans l’interface utilisateur classique, qui a été abandonnée dans AEM 6.4.
>
>Adobe vous recommande d’utiliser l’[IU tactile](/help/sites-developing/touch-ui-concepts.md) moderne basée sur l’[IU Coral](/help/sites-developing/touch-ui-concepts.md#coral-ui) et l’[IU Granite](/help/sites-developing/touch-ui-concepts.md#granite-ui-foundation-components).

L’interface web d’Adobe Experience Manager utilise AJAX et d’autres technologies modernes intégrées dans les navigateurs pour activer l’édition tel écran tel écrit (WYSIWYG) et permettre aux auteurs de mettre en forme le contenu directement sur la page web.

Adobe Experience Manager (AEM) utilise la bibliothèque de widgets [ExtJS](https://www.sencha.com/), laquelle fournit des éléments d’interface utilisateur particulièrement soignés compatibles avec les principaux navigateurs du marché et permettent de créer des interfaces utilisateur dignes des ordinateurs de bureau.

Ces widgets sont inclus dans AEM et, en plus d’être utilisés par AEM, ils peuvent l’être par tout site web créé à l’aide de cette solution.

Pour consulter la liste complète de tous les widgets disponibles dans AEM, vous pouvez vous reporter à la [documentation API des widgets](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html) ou à la [liste des xtypes existants](/help/sites-developing/xtypes.md). En outre, de nombreux exemples montrant comment utiliser la structure ExtJS sont disponibles sur le site de [Sencha](https://www.sencha.com/products/extjs/examples/), le propriétaire de la structure.

Cette page vous livre quelques pistes concernant l’utilisation et l’extension des widgets. Elle vous explique, tout d’abord, comment [inclure du code côté client dans une page](#including-the-client-sided-code-in-a-page). Elle présente ensuite quelques exemples de composants qui ont été créés pour illustrer des scénarios d’utilisation et d’extension de base. Ces composants sont disponibles dans le module **Utilisation de widgets ExtJS** sur **Package Share**.

Ce module contient des exemples des éléments suivants :

* [Boîtes de dialogue de base](#basic-dialogs) constituées de widgets prêts à l’emploi.
* [Boîtes de dialogue dynamiques](#dynamic-dialogs) créées avec des widgets prêts à l’emploi et la logique JavaScript personnalisée.
* Boîtes de dialogue basées sur des [widgets personnalisés](#custom-widgets).
* Un [panneau Arborescence](#tree-overview) qui affiche une arborescence JCR sous un chemin d’accès donné.
* Un [panneau Grille](#grid-overview) qui affiche des données sous la forme d’un tableau.

>[!NOTE]
>
>L’IU classique d’Adobe Experience Manager repose sur [ExtJS 3.4.0](https://extjs.cachefly.net/ext-3.4.0/docs/).

## Insertion du code côté client dans une page {#including-the-client-sided-code-in-a-page}

Le code javascript et la feuille de style côté client doivent être placés dans une bibliothèque cliente.

Pour créer une bibliothèque cliente, procédez comme suit :

1. Create a node below `/apps/<project>` with the following properties:

   * name=&quot;clientlib&quot;
   * jcr:mixinTypes=&quot;[mix:lockable]&quot;
   * jcr:primaryType=&quot;cq:ClientLibraryFolder&quot;
   * sling:resourceType=&quot;widgets/clientlib&quot;
   * categories=&quot;[&lt;category-name>]&quot;
   * dependencies=&quot;[cq.widgets]&quot;

   `Note: <category-name> is the name of the custom library (e.g. "cq.extjstraining") and is used to include the library on the page.`

1. Below `clientlib` create the `css` and `js` folders (nt:folder).

1. Below `clientlib` create the `css.txt` and `js.txt` files (nt:files). Ces fichiers .txt répertorient les fichiers qui sont inclus dans la bibliothèque.

1. Edit `js.txt`: it needs to start with &#39; `#base=js`&#39; followed by the list of the files that will be aggregated by the CQ client library service, eg:

   ```
   #base=js
    components.js
    exercises.js
    CustomWidget.js
    CustomBrowseField.js
    InsertTextPlugin.js
   ```

1. Edit `css.txt`: it needs to start with &#39; `#base=css`&#39; followed by the list of the files that will be aggregated by the CQ client library service, eg:

   ```
   #base=css
    components.css
   ```

1. Sous le dossier `js`, placez les fichiers JavaScript appartenant à la bibliothèque.

1. Below the `css` folder, place the `.css` files and the resources used by the css files (e.g. `my_icon.png`).

>[!NOTE]
>
>La gestion des feuilles de style décrites précédemment est facultative.

Pour inclure la bibliothèque cliente dans le fichier jsp du composant de page :

* pour inclure à la fois le code javascript et les feuilles de style :
   `<ui:includeClientLib categories="<category-name1>, <category-name2>, ..."/>`
où 
`<category-nameX>` est le nom de la bibliothèque côté client.

* pour inclure uniquement le code javascript :
   `<ui:includeClientLib js="<category-name>"/>`

Pour plus d’informations, consultez la description de la balise [&lt;ui:includeClientLib>](/help/sites-developing/taglib.md#lt-ui-includeclientlib).

Dans certains cas, une bibliothèque cliente ne doit être disponible que dans le mode de création et doit être exclue du mode de publication. Vous pouvez y parvenir comme suit :

```xml
    if (WCMMode.fromRequest(request) != WCMMode.DISABLED) {
        %><ui:includeClientLib categories="cq.collab.blog"/><%
    }
```

### Prise en main des exemples {#getting-started-with-the-samples}

To follow the tutorials on this page, install the package called **Using ExtJS Widgets** in a local AEM instance and create a sample page in which the components will be included. Pour ce faire :

1. In your AEM instance download the package called **Using ExtJS Widgets (v01)** from Package Share and install the package. It creates the project `extjstraining` below `/apps` in the repository.
1. Include the client library containing the scripts (js) and the stylesheet (css) in the head tag of the geometrixx page jsp, as you will include the sample components in a new page of the **Geometrixx** branch:
in **CRXDE Lite** open the file `/apps/geometrixx/components/page/headlibs.jsp` and add the `cq.extjstraining` category to the existing `<ui:includeClientLib>` tag as follows:
   `%><ui:includeClientLib categories="apps.geometrixx-main, cq.extjstraining"/><%`
1. Create a new page in the **Geometrixx** branch below `/content/geometrixx/en/products` and call it **Using ExtJS Widgets**.
1. Passez en mode Création et ajoutez tous les composants du groupe appelé **Utilisation des widgets ExtJS** à la conception de Geometrixx.
1. Go back in edit mode: the components of the group **Using ExtJS Widgets** are available in the Sidekick.

>[!NOTE]
>
>Les exemples de cette page sont basés sur l’échantillon de contenu Geometrixx. Celui-ci n’est plus fourni avec AEM et a été remplacé par We.Retail. See the document [We.Retail Reference Implementation](/help/sites-developing/we-retail.md#we-retail-geometrixx) for how to download and install Geometrixx.

### Boîtes de dialogue de base {#basic-dialogs}

Les boîtes de dialogue sont généralement utilisées pour modifier du contenu. Cependant, elles peuvent également afficher simplement des informations. Pour afficher une boîte de dialogue complète, une méthode simple consiste à accéder à sa représentation au format json. Pour ce faire, faites pointer le navigateur vers :

`https://localhost:4502/<path-to-dialog>.-1.json`

Le premier composant du groupe **Utilisation des widgets ExtJS** dans le sidekick se nomme **1. Éléments de base de boîte de dialogue**. Il comprend quatre boîtes de dialogue de base qui sont constituées de widgets prêts à l’emploi, sans logique JavaScript personnalisée. The dialogs are stored below `/apps/extjstraining/components/dialogbasics`. Les boîtes de dialogue de base sont les suivantes :

* Boîte de dialogue complète (nœud `full`) : elle affiche une fenêtre avec 3 onglets ayant chacun 2 champs de texte.
* Boîte de dialogue à un seul panneau (nœud `singlepanel`) : elle affiche une fenêtre avec 1 seul onglet comprenant 2 champs de texte.
* Boîte de dialogue à plusieurs panneaux (nœud `multipanel`) : l’affichage est identique à celui de la boîte de dialogue complète, mais la construction est différente.
* Boîte de dialogue de conception (nœud `design`) : elle affiche une fenêtre avec 2 onglets. Le premier onglet contient un champ de texte, un menu déroulant et une zone de texte réductible. Le deuxième onglet comprend un jeu de champs avec 4 champs de texte et un jeu de champs réductible avec 2 champs de texte.

Insérez le composant **1. Éléments de base de boîte de dialogue** dans l’exemple de page :

1. Ajoutez le composant **1. Dialog Basics** component to the sample page from the **Using ExtJS Widgets** tab in the **Sidekick**.
1. Le composant affiche un titre, du texte et un lien **PROPRIÉTÉS** : cliquez sur le lien pour afficher les propriétés du paragraphe qui sont stockées dans le référentiel. Cliquez à nouveau sur le lien pour masquer les propriétés.

Le composant se présente sous la forme suivante :

![chlimage_1-60](assets/chlimage_1-60.png)

#### Exemple 1 : Boîte de dialogue complète {#example-full-dialog}

La boîte de dialogue **Complète** affiche une fenêtre avec trois onglets ayant chacun deux champs de texte. Il s’agit de la boîte de dialogue par défaut du composant **Éléments de base de boîte de dialogue**. Ses caractéristiques sont les suivantes :

* Is defined by a node: node type = `cq:Dialog`, xtype = ` [dialog](/help/sites-developing/xtypes.md#dialog)`.
* Displays 3 tabs (node type = `cq:Panel`).
* Each tab has 2 textfields (node type = `cq:Widget`, xtype = ` [textfield](/help/sites-developing/xtypes.md#textfield)`).
* Est défini par le noeud :
   `/apps/extjstraining/components/dialogbasics/full`
* Est rendu au format JSON en demandant :
   `https://localhost:4502/apps/extjstraining/components/dialogbasics/full.-1.json`

La boîte de dialogue se présente comme suit :

![screen_shot_2012-01-31at45411pm](assets/screen_shot_2012-01-31at45411pm.png)

#### Exemple 2 : Boîte de dialogue à un seul panneau {#example-single-panel-dialog}

La boîte de dialogue **à un seul panneau** affiche une fenêtre avec un seul onglet comprenant deux champs de texte. Ses caractéristiques sont les suivantes :

* Displays 1 tab (node type = `cq:Dialog`, xtype = ` [panel](/help/sites-developing/xtypes.md#panel)`)
* The tab has 2 textfields (node type = `cq:Widget`, xtype = ` [textfield](/help/sites-developing/xtypes.md#textfield)`)
* Est défini par le noeud :
   `/apps/extjstraining/components/dialogbasics/singlepanel`
* Est rendu au format json en demandant :
   `https://localhost:4502/apps/extjstraining/components/dialogbasics/singlepanel.-1.json`
* L’avantage de cette boîte de dialogue est de nécessiter moins de configuration que la **Boîte de dialogue complète**.
* Utilisation recommandée : boîtes de dialogue simples affichant des informations ou ne comportant que quelques champs.

Pour utiliser la boîte de dialogue à un seul panneau, procédez comme suit :

1. Remplacez la boîte de dialogue du composant **Éléments de base de boîte de dialogue** par la boîte de dialogue **à un seul panneau** :
   1. In **CRXDE Lite**, delete the node: `/apps/extjstraining/components/dialogbasics/dialog`
   1. Cliquez sur **Enregistrer tout** pour enregistrer les modifications.
   1. Copy the node: `/apps/extjstraining/components/dialogbasics/singlepanel`
   1. Paste the copied node below: `/apps/extjstraining/components/dialogbasics`
   1. Sélectionnez le noeud : `/apps/extjstraining/components/dialogbasics/Copy of singlepanel`et renommez-la `dialog`.
1. Modifiez le composant. La boîte de dialogue s’affiche alors comme suit :

![screen_shot_2012-01-31at45952pm](assets/screen_shot_2012-01-31at45952pm.png)

#### Exemple 3 : Boîte de dialogue à plusieurs panneaux {#example-multi-panel-dialog}

Dans le cas de la boîte de dialogue **à plusieurs panneaux**, l’affichage est identique à celui de la boîte de dialogue **complète**, mais la construction est différente. Ses caractéristiques sont les suivantes :

* Is defined by a node (node type = `cq:Dialog`, xtype = ` [tabpanel](/help/sites-developing/xtypes.md#tabpanel)`).
* Displays 3 tabs (node type = `cq:Panel`).
* Each tab has 2 textfields (node type = `cq:Widget`, xtype = ` [textfield](/help/sites-developing/xtypes.md#textfield)`).
* Est défini par le noeud :
   `/apps/extjstraining/components/dialogbasics/multipanel`
* Est rendu au format json en demandant :
   `https://localhost:4502/apps/extjstraining/components/dialogbasics/multipanel.-1.json`
* Par rapport à la **Boîte de dialogue complète**, elle présente une structure simplifiée.
* Utilisation recommandée : boîtes de dialogues à plusieurs onglets.

Pour utiliser la boîte de dialogue Panneau multiple :

1. Replace the dialog of the **Dialog Basics** component with the **Multi Panel** dialog:
follow the steps described for the [Example 2: Single Panel Dialog](#example-single-panel-dialog)
1. Modifiez le composant. La boîte de dialogue s’affiche alors comme suit :

![screen_shot_2012-01-31at50119pm](assets/screen_shot_2012-01-31at50119pm.png)

#### Exemple 4 : Format Riche {#example-rich-dialog}

La boîte de dialogue **Riche** affiche une fenêtre avec deux onglets. Le premier onglet contient un champ de texte, un menu déroulant et une zone de texte réductible. Le deuxième onglet comprend un jeu de champs avec quatre champs de texte et un jeu de champs réductible avec deux champs de texte. Ses caractéristiques sont les suivantes :

* Is defined by a node (node type = `cq:Dialog`, xtype = ` [dialog](/help/sites-developing/xtypes.md#dialog)`).
* Displays 2 tabs (node type = `cq:Panel`).
* The first tab has a ` [dialogfieldset](/help/sites-developing/xtypes.md#dialogfieldset)` widget with a ` [textfield](/help/sites-developing/xtypes.md#textfield)` and a ` [selection](/help/sites-developing/xtypes.md#selection)` widget with 3 options, and a collapsible ` [dialogfieldset](/help/sites-developing/xtypes.md#dialogfieldset)` with a ` [textarea](/help/sites-developing/xtypes.md#textarea)` widget.
* The second tab has a ` [dialogfieldset](/help/sites-developing/xtypes.md#dialogfieldset)` widget with 4 ` [textfield](/help/sites-developing/xtypes.md#textfield)` widgets, and a collapsible `dialogfieldset` with 2 ` [textfield](/help/sites-developing/xtypes.md#textfield)` widgets.
* Est défini par le noeud :
   `/apps/extjstraining/components/dialogbasics/rich`
* Est rendu au format json en demandant :
   `https://localhost:4502/apps/extjstraining/components/dialogbasics/rich.-1.json`

Pour utiliser la boîte de dialogue **Riche**, procédez comme suit :

1. Replace the dialog of the **Dialog Basics** component with the **Rich** dialog:
follow the steps described for the [Example 2: Single Panel Dialog](#example-single-panel-dialog)
1. Modifiez le composant. La boîte de dialogue s’affiche alors comme suit :

![screen_shot_2012-01-31at50429pm](assets/screen_shot_2012-01-31at50429pm.png) ![screen_shot_2012-01-31at50519pm](assets/screen_shot_2012-01-31at50519pm.png)

### Boîtes de dialogue dynamiques {#dynamic-dialogs}

Le deuxième composant du groupe **Utilisation des widgets ExtJS** dans le sidekick se nomme **2. Boîtes de dialogue dynamiques**. Il comprend trois boîtes de dialogue dynamiques qui sont constituées de widgets prêts à l’emploi, **avec une logique JavaScript personnalisée**. The dialogs are stored below `/apps/extjstraining/components/dynamicdialogs`. Les boîtes de dialogue dynamiques sont les suivantes :

* Boîte de dialogue Switch Tabs (nœud `switchtabs`) : elle affiche une fenêtre avec deux onglets. Le premier onglet comprend trois cases d’option : lorsqu’une option est sélectionnée, l’onglet correspondant est affiché. Le deuxième onglet comprend deux champs de texte.
* Boîte de dialogue  (nœud (`arbitrary`arbitrary) : elle affiche une fenêtre avec un seul onglet. Cet onglet se compose d’une zone permettant de déposer ou de télécharger une ressource, ainsi que d’une section affichant des informations sur la page et sur la ressource, le cas échéant.
* the Toggle Fields dialog ( `togglefield` node): it displays a window with one tab. Cet onglet comprend une case à cocher : lorsque cette case est cochée, un jeu de champs composé de deux champs de texte est affiché.

To include the **2. Boîtes de dialogue dynamiques** dans l’exemple de page :

1. Ajoutez le composant **2. Boîtes de dialogue dynamiques** à l’exemple de page à partir de l’onglet **Utilisation des widgets ExtJS** dans le **sidekick**.
1. Le composant affiche un titre, du texte et un lien **PROPRIÉTÉS** : cliquez sur ce lien pour afficher les propriétés du paragraphe qui sont stockées dans le référentiel. Cliquez à nouveau pour masquer les propriétés.

Le composant se présente sous la forme suivante :

![chlimage_1-61](assets/chlimage_1-61.png)

#### Exemple 1 : Boîte de dialogue Switch Tabs {#example-switch-tabs-dialog}

La boîte de dialogue **Switch Tabs** affiche une fenêtre avec deux onglets. Le premier onglet comprend trois cases d’option : lorsqu’une option est sélectionnée, l’onglet correspondant est affiché. Le deuxième onglet comprend deux champs de texte.

Ses caractéristiques principales sont les suivantes :

* Is defined by a node (node type = `cq:Dialog`, xtype = ` [dialog](/help/sites-developing/xtypes.md#dialog)`).
* Elle affiche 2 onglets (type de nœud = `cq:Panel`) : 1 onglet de sélection, le deuxième onglet dépend de la sélection effectuée dans le premier onglet (3 options).
* Has 3 optional tabs (node type = `cq:Panel`), each one has 2 textfields (node type = `cq:Widget`, xtype = ` [textfield](/help/sites-developing/xtypes.md#textfield)`). Un seul onglet facultatif est affiché à la fois.
* Est défini par le `switchtabs` noeud à :
   `/apps/extjstraining/components/dynamicdialogs/switchtabs`
* Est rendu au format json en demandant :
   `https://localhost:4502/apps/extjstraining/components/dynamicdialogs/switchtabs.-1.json`

Cette logique est implémentée par le biais d’écouteurs d’événements et de code JavaScript comme suit :

* Le noeud dialog dispose d’un module d’écoute &quot; `beforeshow`&quot; qui masque tous les onglets facultatifs avant que la boîte de dialogue ne s’affiche :
   `beforeshow="function(dialog){Ejst.x2.manageTabs(dialog.items.get(0));}"`

   `dialog.items.get(0)` obtient le panneau de tabulation qui contient le panneau de sélection et les 3 panneaux facultatifs.
* The `Ejst.x2` object is defined in the `exercises.js` file at:
   `/apps/extjstraining/clientlib/js/exercises.js`
* In the `Ejst.x2.manageTabs()` method, as the value of `index` is -1, all the optional tabs are hidden (i goes from 1 to 3).
* The selection tab has 2 listeners: one that shows the selected tab when the dialog is loaded (&quot; `loadcontent`&quot; event) and one that shows the selected tab when the selection is changed (&quot; `selectionchanged`&quot; event):
   `loadcontent="function(field,rec,path){Ejst.x2.showTab(field);}"`

   `selectionchanged="function(field,value){Ejst.x2.showTab(field);}"`
* Dans la `Ejst.x2.showTab()` méthode :
   `field.findParentByType('tabpanel')` obtient le panneau d’onglets contenant tous les onglets ( `field` représente le widget de sélection).
   `field.getValue()` obtient la valeur de la sélection, par exemple : tab2
   `Ejst.x2.manageTabs()` affiche l’onglet sélectionné.
* Each optional tab has a listener that hides the tab on &quot; `render`&quot; event:
   `render="function(tab){Ejst.x2.hideTab(tab);}"`
* Dans la `Ejst.x2.hideTab()` méthode :
   `tabPanel` est le panneau de tabulation qui contient tous les onglets.
   `index` est l’index de l’onglet facultatif.
   `tabPanel.hideTabStripItem(index)` masque l’onglet

Elle se présente comme suit :

![screen_shot_2012-02-01at114745am](assets/screen_shot_2012-02-01at114745am.png)

#### Exemple 2 : Boîte de dialogue Arbitrary {#example-arbitrary-dialog}

Très souvent, une boîte de dialogue affiche du contenu provenant d’un composant sous-jacent. La boîte de dialogue décrite ici, baptisée **Arbitrary**, extrait le contenu d’un autre composant.

La boîte de dialogue **Arbitrary** affiche une fenêtre avec un seul onglet. Cet onglet comprend deux zones : l’une permettant de déposer ou de télécharger une ressource, et une autre affichant des informations sur la page et sur la ressource, le cas échéant.

Ses caractéristiques principales sont les suivantes :

* Is defined by a node (node type = `cq:Dialog`, xtype = ` [dialog](/help/sites-developing/xtypes.md#dialog)`).
* Displays 1 tabpanel widget (node type = `cq:Widget`, xtype = ` [tabpanel](/help/sites-developing/xtypes.md#tabpanel)`) with 1 panel (node type = `cq:Panel`)
* The panel has a smartfile widget (node type = `cq:Widget`, xtype = ` [smartfile](/help/sites-developing/xtypes.md#smartfile)`) and an ownerdraw widget (node type = `cq:Widget`, xtype = ` [ownerdraw](/help/sites-developing/xtypes.md#ownerdraw)`)
* Est défini par le `arbitrary` noeud à :
   `/apps/extjstraining/components/dynamicdialogs/arbitrary`
* Est rendu au format json en demandant :
   `https://localhost:4502/apps/extjstraining/components/dynamicdialogs/arbitrary.-1.json`

Cette logique est implémentée par le biais d’écouteurs d’événements et de code JavaScript comme suit :

* Le widget de dessin de propriétés comporte un écouteur &quot; `loadcontent`&quot; qui affiche des informations sur la page contenant le composant et la ressource référencée par le widget de fichier intelligent lors du chargement du contenu :
   `loadcontent="function(field,rec,path){Ejst.x2.showInfo(field,rec,path);}"`

   `field` est défini avec l’objet ownerdraw
   `path` est défini avec le chemin de contenu du composant (par ex. : /content/geometrixx/fr/products/triangle/ui-tutorial/jcr:content/par/dynamicdialogs)
* The `Ejst.x2` object is defined in the `exercises.js` file at:
   `/apps/extjstraining/clientlib/js/exercises.js`
* Dans la `Ejst.x2.showInfo()` méthode :
   `pagePath` est le chemin d’accès de la page contenant le composant
   `pageInfo` représente les propriétés de la page au format json.
   `reference` est le chemin d’accès de l’actif référencé
   `metadata` représente les métadonnées du fichier au format json.
   `ownerdraw.getEl().update(html);` affiche le code html créé dans la boîte de dialogue.

Pour utiliser la boîte de dialogue **Arbitrary**, procédez comme suit :

1. Replace the dialog of the **Dynamic Dialog** component with the **Arbitrary** dialog:
follow the steps described for the [Example 2: Single Panel Dialog](#example-single-panel-dialog)
1. Modifiez le composant. La boîte de dialogue s’affiche alors comme suit :

![screen_shot_2012-02-01at115300am](assets/screen_shot_2012-02-01at115300am.png)

#### Exemple 3 : Boîte de dialogue Toggle Fields {#example-toggle-fields-dialog}

La boîte de dialogue **Toggle Fields**) affiche une fenêtre avec un seul onglet. Cet onglet comprend une case à cocher : lorsque cette case est cochée, un jeu de champs composé de deux champs de texte est affiché.

Ses caractéristiques principales sont les suivantes :

* Is defined by a node (node type = `cq:Dialog`, xtype = ` [dialog](/help/sites-developing/xtypes.md#dialog)`).
* Displays 1 tabpanel widget (node type = `cq:Widget`, xtype = ` [tabpanel](/help/sites-developing/xtypes.md#textpanel)`) with 1 panel (node type = `cq:Panel`).
* The panel has a selection/checkbox widget (node type = `cq:Widget`, xtype = ` [selection](/help/sites-developing/xtypes.md#selection)`, type = ` [checkbox](/help/sites-developing/xtypes.md#checkbox)`) and a collapsible dialogfieldset widget (node type = `cq:Widget`, xtype = ` [dialogfieldset](/help/sites-developing/xtypes.md#dialogfieldset)`) that is hidden by default, with 2 textfield widgets (node type = `cq:Widget`, xtype = ` [textfield](/help/sites-developing/xtypes.md#textfield)`).
* Est défini par le `togglefields` noeud à :
   `/apps/extjstraining/components/dynamicdialogs/togglefields`
* Est rendu au format json en demandant :
   `https://localhost:4502/apps/extjstraining/components/dynamicdialogs/togglefields.-1.json`

Cette logique est implémentée par le biais d’écouteurs d’événements et de code JavaScript comme suit :

* the selection tab has 2 listeners: one that shows the dialogfieldset when the content is loaded (&quot; `loadcontent`&quot; event) and one that shows the dialogfieldset when the selection is changed (&quot; `selectionchanged`&quot; event):
   `loadcontent="function(field,rec,path){Ejst.x2.toggleFieldSet(field);}"`

   `selectionchanged="function(field,value){Ejst.x2.toggleFieldSet(field);}"`
* The `Ejst.x2` object is defined in the `exercises.js` file at:
   `/apps/extjstraining/clientlib/js/exercises.js`
* Dans la `Ejst.x2.toggleFieldSet()` méthode :
   `box` est l’objet de sélection
   `panel` est le panneau contenant la sélection et les widgets d&#39;ensemble de champs de dialogue
   `fieldSet` est l’objet dialogfieldset
   `show` est la valeur de la sélection (true ou false) basée sur &#39; `show`&#39; le jeu de champs de dialogue est affiché ou non.

To use the **Toggle Fields** dialog:

1. Replace the dialog of the **Dynamic Dialog** component with the **Toggle Fields** dialog:
follow the steps described for the [Example 2: Single Panel Dialog](#example-single-panel-dialog)
1. Modifiez le composant. La boîte de dialogue s’affiche alors comme suit :

![screen_shot_2012-02-01at115518am](assets/screen_shot_2012-02-01at115518am.png)

### Widgets personnalisés {#custom-widgets}

Les widgets prêts à l’emploi fournis avec AEM couvrent normalement la plupart des scénarios d’utilisation. Cependant, il peut être parfois nécessaire de créer un widget personnalisé pour couvrir une exigence spécifique à un projet. Des widgets personnalisés peuvent être créés en étendant des widgets existants. Pour vous aider à débuter avec ce type de personnalisation, le module **Utilisation des widgets ExtJS** comprend trois boîtes de dialogue qui utilisent trois widgets personnalisés différents :

* La boîte de dialogue Multi Field (nœud `multifield`) affiche une fenêtre avec un seul onglet. Cet onglet comprend un widget multifield personnalisé qui comporte deux zones : un menu déroulant avec deux options et un champ de texte. As it is based on the out-of-the-box `multifield` widget (that only has a text field), it has all the features of the `multifield` widget.
* La boîte de dialogue Tree Browse (nœud `treebrowse`) affiche une fenêtre avec un seul onglet contenant un widget d’exploration du chemin : lorsque vous cliquez sur la flèche, une fenêtre s’ouvre dans laquelle vous pouvez parcourir une hiérarchie et sélectionner un élément. Le chemin d’accès de l’élément est ensuite ajouté au champ du chemin et conservé lorsque la boîte de dialogue est fermée.
* Une boîte de dialogue basée sur le module Éditeur de texte enrichi (nœud `rteplugin`) qui ajoute un bouton personnalisé à l’Éditeur de texte enrichi pour insérer du texte personnalisé dans le texte principal. Elle comprend un widget `richtext` (RTE) et une fonctionnalité personnalisée qui est ajoutée par le biais du module externe RTE.

Les widgets personnalisés et le module externe sont inclus dans le composant appelé **3. Widgets personnalisés** du module **Utilisation des widgets ExtJS**. Pour inclure ce composant dans l’exemple de page, procédez comme suit :

1. Ajoutez le composant **3. Widgets personnalisés** à l’exemple de page à partir de l’onglet **Utilisation des widgets ExtJS** dans le **sidekick**.
1. Le composant affiche un titre, du texte et, lorsque vous cliquez sur le lien **PROPRIÉTÉS**, les propriétés du paragraphe stocké dans le référentiel. Cliquez à nouveau pour masquer les propriétés.
Le composant se présente sous la forme suivante :

![chlimage_1-62](assets/chlimage_1-62.png)

#### Exemple 1 : Widget Custom Multifield {#example-custom-multifield-widget}

La boîte de dialogue basée sur le widget **Custom Multifield** affiche une fenêtre avec un seul onglet. Cet onglet comprend un widget à plusieurs champs (multi-field) personnalisé qui, contrairement à l’onglet standard avec son champ unique, comporte deux zones : un menu déroulant avec deux options et un champ de texte.

Boîte de dialogue basée sur le widget **Custom Multifield** :

* Is defined by a node (node type = `cq:Dialog`, xtype = ` [dialog](/help/sites-developing/xtypes.md#dialog)`).
* Displays 1 tabpanel widget (node type = `cq:Widget`, xtype = ` [tabpanel](/help/sites-developing/xtypes.md#tabpanel)`) containing a panel (node type = `cq:Widget`, xtype = ` [panel](/help/sites-developing/xtypes.md#panel)`).
* The panel has a `multifield` widget (node type = `cq:Widget`, xtype = ` [multifield](/help/sites-developing/xtypes.md#multifield)`).
* The `multifield` widget has a fieldconfig (node type = `nt:unstructured`, xtype = `ejstcustom`, optionsProvider = `Ejst.x3.provideOptions`) that is based on the custom xtype &#39; `ejstcustom`&#39;:
   * &#39; `fieldconfig`&#39; is a config option of the ` [CQ.form.MultiField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.MultiField)` object.
   * &#39; `optionsProvider`&#39; is a configuration of the `ejstcustom` widget. Il est défini avec la `Ejst.x3.provideOptions` méthode définie dans `exercises.js` :
      `/apps/extjstraining/clientlib/js/exercises.js`
et renvoie 2 options.
* Est défini par le `multifield` noeud à :
   `/apps/extjstraining/components/customwidgets/multifield`
* Est rendu au format json en demandant :
   `https://localhost:4502/apps/extjstraining/components/customwidgets/multifield.-1.json`

Widget à plusieurs champs (multifield) personnalisé (xtype = `ejstcustom`) :

* Il s’agit d’un objet JavaScript appelé `Ejst.CustomWidget`.
* Is defined in the `CustomWidget.js` javascript file at:
   `/apps/extjstraining/clientlib/js/CustomWidget.js`
* Extends the ` [CQ.form.CompositeField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.CompositeField)` widget.
* Has 3 fields: `hiddenField` (Textfield), `allowField` (ComboBox) and `otherField` (Textfield)
* Overrides `CQ.Ext.Component#initComponent` to add the 3 fields:
   * `allowField` est un objet [CQ.form.Selection](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.Selection) de type « select ». optionsProvider est une configuration de l’objet Selection qui est instancié avec la configuration optionsProvider du CustomWidget défini dans la boîte de dialogue.
   * `otherField` est un objet [CQ.Ext.form.TextField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.TextField).
* Overrides the methods `setValue`, `getValue` and `getRawValue` of [CQ.form.CompositeField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.CompositeField) in order to set and retrieve the value of CustomWidget with the format:
   `<allowField value>/<otherField value>, e.g.: 'Bla1/hello'`.
* S&#39;enregistre comme &quot; `ejstcustom`&quot; xtype :
   `CQ.Ext.reg('ejstcustom', Ejst.CustomWidget);`

La boîte de dialogue basée sur le widget **Custom Multifield** se présente comme suit :

![screen_shot_2012-02-01at115840am](assets/screen_shot_2012-02-01at115840am.png)

#### Exemple 2 : Widget treebrowse personnalisé {#example-custom-treebrowse-widget}

La boîte de dialogue basée sur le widget **Treebrowse** personnalisé affiche une fenêtre avec un seul onglet contenant un widget d’exploration de chemin personnalisé : lorsque vous cliquez sur la flèche, une fenêtre s’ouvre dans laquelle vous pouvez parcourir une hiérarchie et sélectionner un élément. Le chemin d’accès de l’élément est ensuite ajouté au champ du chemin et conservé lorsque la boîte de dialogue est fermée.

Boîte de dialogue treebrowse personnalisée :

* Is defined by a node (node type = `cq:Dialog`, xtype = ` [dialog](/help/sites-developing/xtypes.md#dialog)`).
* Displays 1 tabpanel widget (node type = `cq:Widget`, xtype = ` [tabpanel](/help/sites-developing/xtypes.md#tabpanel)`) containing a panel (node type = `cq:Widget`, xtype = ` [panel](/help/sites-developing/xtypes.md#panel)`).
* The panel has a custom widget (node type = `cq:Widget`, xtype = `ejstbrowse`)
* Est défini par le `treebrowse` noeud à :
   `/apps/extjstraining/components/customwidgets/treebrowse`
* Est rendu au format json en demandant :
   `https://localhost:4502/apps/extjstraining/components/customwidgets/treebrowse.-1.json`

Widget treebrowse personnalisé (xtype = `ejstbrowse`) :

* Il s’agit d’un objet JavaScript appelé `Ejst.CustomWidget`.
* Is defined in the `CustomBrowseField.js` javascript file at:
   `/apps/extjstraining/clientlib/js/CustomBrowseField.js`
* Extends ` [CQ.Ext.form.TriggerField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.TriggerField)`.
* Il définit une fenêtre de navigation appelée `browseWindow`.
* Overrides ` [CQ.Ext.form.TriggerField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.TriggerField)#onTriggerClick` to show the browse window when the arrow is clicked.
* Il définit un objet [CQ.Ext.tree.TreePanel](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.tree.TreePanel) :
   * It gets its data by calling the servlet registered at `/bin/wcm/siteadmin/tree.json`.
   * Its root is &quot; `apps/extjstraining`&quot;.
* Defines a `window` object ( ` [CQ.Ext.Window](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Window)`):
   * Il est basé sur le panneau prédéfini.
   * Il comprend un bouton **OK** qui définit la valeur du chemin d’accès sélectionné et masque le panneau.
* La fenêtre est ancrée sous le champ **Chemin d’accès**.
* Le chemin d’accès est transmis du champ de navigation à la fenêtre lorsque l’événement `show` se produit.
* S&#39;enregistre comme &quot; `ejstbrowse`&quot; xtype :
   `CQ.Ext.reg('ejstbrowse', Ejst.CustomBrowseField);`

To use the **Custom Treebrowse** widget based dialog:

1. Replace the dialog of the **Custom Widgets** component with the **Custom Treebrowse** dialog:
follow the steps described for the [Example 2: Single Panel Dialog](#example-single-panel-dialog)
1. Modifiez le composant. La boîte de dialogue s’affiche alors comme suit :

![screen_shot_2012-02-01at120104pm](assets/screen_shot_2012-02-01at120104pm.png)

#### Exemple 3 : Module externe Éditeur de texte enrichi (RTE){#example-rich-text-editor-rte-plug-in}

La boîte de dialogue basée sur le **module externe Éditeur de Texte Enrichi (RTE)** comprend un bouton personnalisé pour insérer du texte personnalisé entre crochets. Le texte personnalisé peut être analysé par une logique côté serveur (non implémentée dans cet exemple), par exemple pour ajouter du texte défini à l’emplacement donné :

Boîte de dialogue basée sur le **module externe RTE** :

* Est défini par le noeud rteplugin dans :
   `/apps/extjstraining/components/customwidgets/rteplugin`
* Est rendu au format json en demandant :
   `https://localhost:4502/apps/extjstraining/components/customwidgets/rteplugin.-1.json`
* The `rtePlugins` node has a child node `inserttext` (node type = `nt:unstructured`) that is named after the plugin. Elle possède une propriété appelée `features`, qui définit les fonctionnalités du module externe disponibles pour l’éditeur de texte enrichi.

Module externe RTE :

* Il s’agit d’un objet JavaScript appelé `Ejst.InsertTextPlugin`.
* Is defined in the `InsertTextPlugin.js` javascript file at:
   `/apps/extjstraining/clientlib/js/InsertTextPlugin.js`
* Extends the ` [CQ.form.rte.plugins.Plugin](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.rte.plugins.Plugin)` object.
* Les méthodes suivantes définissent l’objet ` [CQ.form.rte.plugins.Plugin](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.form.rte.plugins.Plugin)` et sont remplacées dans le module externe d’implémentation :
   * `getFeatures()` renvoie un tableau de toutes les fonctionnalités rendues disponibles par le module externe.
   * `initializeUI()` ajoute le nouveau bouton à la barre d’outils de l’Éditeur de texte enrichi.
   * `notifyPluginConfig()` affiche le titre et le texte lorsque le bouton est survolé.
   * `execute()` est appelé lorsque l’utilisateur clique sur le bouton et exécute l’action du module externe : il affiche une fenêtre qui est utilisée pour définir le texte à inclure.
* `insertText()` insère un texte à l’aide de l’objet de boîte de dialogue correspondant `Ejst.InsertTextPlugin.Dialog` (voir plus loin).
* `executeInsertText()` est appelée par la `apply()` méthode de la boîte de dialogue, qui est déclenchée lorsque l’utilisateur clique sur le bouton **OK** .
* S&#39;enregistre comme module externe &quot; `inserttext`&quot; :
   `CQ.form.rte.plugins.PluginRegistry.register("inserttext", Ejst.InsertTextPlugin);`
* L’objet `Ejst.InsertTextPlugin.Dialog` définit la boîte de dialogue qui s’ouvre lorsque l’utilisateur clique sur le bouton du module externe. La boîte de dialogue se compose d’un panneau, d’un formulaire, d’un champ de texte et de 2 boutons (**OK** et **Annuler**).

Pour utiliser la boîte de dialogue basée sur le **module externe Éditeur de Texte Enrichi (RTE)**, procédez comme suit :

1. Remplacez la boîte de dialogue du composant **Widgets personnalisés** par la boîte de dialogue basée sur le **module externe Éditeur de Texte Enrichi (RTE)** : Suivez la procédure décrite pour [Exemple 2 : Boîte de dialogue à un seul panneau](#example-single-panel-dialog).
1. Modifiez le composant.
1. Cliquez sur la dernière icône à droite (celle avec quatre flèches). Enter a path and click **OK**:
The path is displayed within brackets ([ ]).
1. Cliquez sur **OK** pour fermer l’Éditeur de texte enrichi.

La boîte de dialogue basée sur le **module externe Éditeur de Texte Enrichi (RTE)** se présente sous la forme suivante :

![screen_shot_2012-02-01at120254pm](assets/screen_shot_2012-02-01at120254pm.png)

>[!NOTE]
>
>This example only shows how to implement the client-side part of the logic: the placeholders (*[text]*) have then to be parsed on the server-side explicitly (e.g. in the component JSP).

### Tree Overview {#tree-overview}

L’objet` [CQ.Ext.tree.TreePanel](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.tree.TreePanel)` prêt à l’emploi représente les données d’interface utilisateur sous la forme d’une arborescence. Le composant Tree Overview inclus dans le module **Utilisation des widgets ExtJS** montre comment utiliser l’objet `TreePanel` pour afficher une arborescence JCR sous un chemin d’accès donné. La fenêtre proprement dite peut être ancrée/détachée. Dans cet exemple, la logique de fenêtre est incorporée dans le fichier JSP du composant entre les balises &lt;script>&lt;/script>.

Pour inclure le composant **Tree Overview** dans l’exemple de page :

1. Ajoutez le composant **4. Tree Overview** à l’exemple de page à partir de l’onglet **Utilisation des widgets ExtJS** dans le **sidekick**.
1. Le composant affiche les éléments suivants :
   * Un titre, accompagné de texte.
   * Un lien **PROPRIÉTÉS** : cliquez sur ce lien pour afficher les propriétés du paragraphe qui sont stockées dans le référentiel. Cliquez à nouveau pour masquer les propriétés.
   * Une fenêtre flottante avec une représentation arborescente du référentiel, qui peut être développée.

Le composant se présente sous la forme suivante :

![screen_shot_2012-02-01at120639pm](assets/screen_shot_2012-02-01at120639pm.png)

Composant Tree Overview :

* Est défini à :
   `/apps/extjstraining/components/treeoverview`

* Sa boîte de dialogue permet de définir la taille de la fenêtre et d’ancrer/de détacher cette dernière (voir les détails ci-dessous).

Le jsp du composant :

* récupère la largeur, la hauteur et les propriétés d’ancrage à partir du référentiel ;
* affiche du texte sur le format des données d’aperçu de l’arborescence ;
* incorpore la logique de fenêtre dans le fichier JSP du composant entre des balises JavaScript ;
* Est défini à :
   `apps/extjstraining/components/treeoverview/content.jsp`

Le code JavaScript incorporé dans le jsp du composant :

* Définit un objet `tree` en essayant de récupérer une fenêtre arborescente de la page.
* If the window displaying the tree does not exist, `treePanel` ([CQ.Ext.tree.TreePanel](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.tree.TreePanel)) is created:
   * `treePanel` contient les données utilisées pour créer la fenêtre.
   * Les données sont récupérées en appelant la servlet enregistrée à l&#39;adresse suivante :
      `/bin/wcm/siteadmin/tree.json`
* The `beforeload` listener makes sure the clicked node is loaded.
* The `root` object sets the path `apps/extjstraining` as the tree root.
* `tree` ( ` [CQ.Ext.Window](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Window)`) est défini en fonction de la valeur prédéfinie `treePanel`et s’affiche avec :
   `tree.show();`
* Si la fenêtre existe déjà, elle est affichée en fonction de la largeur, de la hauteur et des propriétés d’ancrage extraites du référentiel.

Boîte de dialogue du composant :

* Elle affiche 1 onglet avec 2 champs pour définir la taille (largeur et hauteur) de la fenêtre d’aperçu d’arborescence et 1 champ pour ancrer/détacher la fenêtre.
* Is defined by a node (node type = `cq:Dialog`, xtype = ` [panel](/help/sites-developing/xtypes.md#panel)`).
* The panel has a sizefield widget (node type = `cq:Widget`, xtype = ` [sizefield](/help/sites-developing/xtypes.md#sizefield)`) and a selection widget (node type = `cq:Widget`, xtype = ` [selection](/help/sites-developing/xtypes.md#selection)`, type = `radio`) with 2 options (true/false)
* Est défini par le noeud dialog à :
   `/apps/extjstraining/components/treeoverview/dialog`
* Est rendu au format json en demandant :
   `https://localhost:4502/apps/extjstraining/components/treeoverview/dialog.-1.json`
* Elle se présente comme suit :

![screen_shot_2012-02-01at120745pm](assets/screen_shot_2012-02-01at120745pm.png)

### Grid Overview {#grid-overview}

Un panneau Grille représente les données sous la forme d’un tableau de lignes et de colonnes. Il se compose des éléments suivants :

* Magasin : modèle contenant les enregistrements de données (lignes).
* Modèle de colonne : mise en page de colonne.
* Affichage : encapsule l’interface utilisateur.
* Modèle de sélection : comportement de la sélection.

The Grid Overview component included in the **Using ExtJS Widgets** package shows how to display data in a tabular format:

* L’exemple 1 utilise des données statiques.
* L&#39;exemple 2 utilise les données récupérées du référentiel.

Pour inclure le composant Aperçu de la grille dans l’exemple de page :

1. Ajoutez le composant **5. Grid Overview** à l’exemple de page à partir de l’onglet **Utilisation des widgets ExtJS** dans le **sidekick**.
1. Le composant affiche les éléments suivants :
   * un titre avec du texte
   * Un lien **PROPRIÉTÉS** : cliquez sur ce lien pour afficher les propriétés du paragraphe qui sont stockées dans le référentiel. Cliquez à nouveau pour masquer les propriétés.
   * Une fenêtre flottante contenant des données sous la forme d’un tableau.

Le composant se présente sous la forme suivante :

![screen_shot_2012-02-01at121109pm](assets/screen_shot_2012-02-01at121109pm.png)

#### Exemple 1 : Grille par défaut {#example-default-grid}

Dans sa version prête à l’emploi, le composant **Grid Overview** affiche une fenêtre avec des données statiques sous forme de tableau. Dans cet exemple, la logique est incorporée dans le fichier JSP du composant de deux manières différentes :

* La logique générique est définie entre les balises &lt;script>&lt;/script>.
* La logique spécifique est disponible dans un fichier .js distinct et un lien vers celle-ci est créé dans le fichier jsp. Cette configuration permet de basculer facilement entre les deux logiques (statique/dynamique) en commentant les balises &lt;script> souhaitées.

Composant Grid Overview :

* Est défini à :
   `/apps/extjstraining/components/gridoverview`
* Sa boîte de dialogue permet de définir la taille de la fenêtre et d’ancrer/de détacher cette dernière.

Le jsp du composant :

* récupère la largeur, la hauteur et les propriétés d’ancrage à partir du référentiel ;
* affiche du texte en guise d’introduction pour le format de données d’aperçu de grille ;
* Référence le code javascript qui définit l’objet GridPanel :
   `<script type="text/javascript" src="/apps/extjstraining/components/gridoverview/defaultgrid.js"></script>`

   `defaultgrid.js` définit certaines données statiques en tant que base de l’objet GridPanel.
* incorpore, entre des balises JavaScript, du code JavaScript qui définit l’objet Window utilisant l’objet GridPanel ;
* Est défini à :
   `apps/extjstraining/components/gridoverview/content.jsp`

Le code JavaScript incorporé dans le jsp du composant :

* Defines the `grid` object by trying to retrieve the window component from the page:
   `var grid = CQ.Ext.getCmp("<%= node.getName() %>-grid");`
* If `grid` does not exist, a [CQ.Ext.grid.GridPanel](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.grid.GridPanel) object ( `gridPanel`) is defined by calling the `getGridPanel()` method (see below). Cette méthode est définie dans `defaultgrid.js`.
* `grid` est un ` [CQ.Ext.Window](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.Window)` objet, basé sur le GridPanel prédéfini, et s’affiche : `grid.show();`
* Si l’objet `grid` existe déjà, il est affiché en fonction de la largeur, de la hauteur et des propriétés d’ancrage extraites du référentiel.

The javascript file ( `defaultgrid.js`) referenced in the component jsp defines the `getGridPanel()` method which is called by the script embedded in the JSP and returns a ` [CQ.Ext.grid.GridPanel](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.grid.GridPanel)` object, based on static data. La logique est la suivante :

* `myData` est un tableau de données statiques, composé de 5 colonnes et de 4 lignes.
* `store` est un `CQ.Ext.data.Store` objet consommé `myData`.
* `store` est chargé en mémoire :
   `store.load();`
* `gridPanel` est un ` [CQ.Ext.grid.GridPanel](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.grid.GridPanel)` objet qui consomme `store`:
   * les largeurs de colonne sont redimensionnées en tout temps :
      `forceFit: true`
   * seule une ligne à la fois peut être sélectionnée :
      `singleSelect:true`

#### Exemple 2 : Grille de recherche de référence {#example-reference-search-grid}

When you install the package, the `content.jsp` of the **Grid Overview** component displays a grid that is based on static data. Il est possible de modifier le composant pour afficher une grille présentant les caractéristiques suivantes :

* Trois colonnes.
* Contenu basé sur les données extraites du référentiel en appelant un servlet.
* Les cellules de la dernière colonne peuvent être modifiées. La valeur est conservée dans une propriété `test` sous le nœud défini par le chemin d’accès qui est affiché dans la première colonne.

As explained in the section before, the window object gets its ` [CQ.Ext.grid.GridPanel](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.grid.GridPanel)` object by calling the `getGridPanel()` method defined in the `defaultgrid.js` file at `/apps/extjstraining/components/gridoverview/defaultgrid.js`. The **Grid Overview **component provides a different implementation for the `getGridPanel()` method, defined in the `referencesearch.js` file at `/apps/extjstraining/components/gridoverview/referencesearch.js`. En changeant le fichier .js qui est référencé dans le jsp du composant, la grille sera basée sur les données extraites du référentiel.

Changez le fichier .js qui est référencé dans le jsp du composant :

1. In **CRXDE Lite**, in the `content.jsp` file of the component, comment the line that includes the `defaultgrid.js` file, so that it looks as follows:
   `<!-- script type="text/javascript" src="/apps/extjstraining/components/gridoverview/defaultgrid.js"></script-->`
1. Remove the comment from the line that includes the `referencesearch.js` file, so that it looks as follows:
   `<script type="text/javascript" src="/apps/extjstraining/components/gridoverview/referencesearch.js"></script>`
1. Enregistrez les modifications.
1. Actualisez l’exemple de page.

Le composant se présente sous la forme suivante :

![screen_shot_2012-02-01at121429pm](assets/screen_shot_2012-02-01at121429pm.png)

The javascript code referenced in the component jsp ( `referencesearch.js`) defines the `getGridPanel()` method called from the component jsp and returns a ` [CQ.Ext.grid.GridPanel](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.grid.GridPanel)` object, based on data that are dynamically retrieved from the repository. La logique contenue dans le fichier `referencesearch.js` définit des données dynamiques comme base de l’objet GridPanel :

* `reader` est un objet ` [CQ.Ext.data.JsonReader](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.data.JsonReader)`qui lit la réponse du servlet au format JSON pour 3 colonnes.
* `cm` est un ` [CQ.Ext.grid.ColumnModel](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.grid.ColumnModel)` objet de 3 colonnes.
Les cellules de colonne &quot;Test&quot; peuvent être modifiées à mesure qu’elles sont définies avec un éditeur :
   `editor: new [CQ.Ext.form.TextField](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.form.TextField)({})`
* les colonnes peuvent être triées :
   `cm.defaultSortable = true;`
* `store` est un ` [CQ.Ext.data.GroupingStore](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.data.GroupingStore)` objet :
   * it gets its data by calling the servlet registered at &quot; `/bin/querybuilder.json`&quot; with a few parameters used to filter the query
   * Il repose sur l’objet `reader` défini précédemment.
   * Le tableau est trié selon la colonne **jcr:path** dans l’ordre croissant.
* `gridPanel` est un ` [CQ.Ext.grid.EditorGridPanel](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.grid.EditorGridPanel)` objet qui peut être modifié :
   * Il repose sur l’objet `store` prédéfini et sur le modèle de colonne `cm`.
   * seule une ligne à la fois peut être sélectionnée :
      `sm: new [CQ.Ext.grid.RowSelectionModel](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/widgets-api/index.html?class=CQ.Ext.grid.RowSelectionModel)({singleSelect:true})`
   * L’écouteur `afteredit` vérifie les éléments suivants après la modification d’une cellule de la colonne « **Test** » :
      * the property &#39; `test`&#39; of the node at the path defined by the &quot;**jcr:path**&quot; column is set in the repository with the value of the cell
      * Si l’opération POST est réussie, la valeur est ajoutée à l’objet `store` ; dans le cas contraire, elle est rejetée.
