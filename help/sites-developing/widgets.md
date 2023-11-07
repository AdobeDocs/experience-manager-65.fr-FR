---
title: Utiliser et optimiser les widgets (IU classique)
description: L’interface web d’Adobe Experience Manager utilise AJAX et d’autres technologies modernes intégrées dans les navigateurs pour activer l’édition tel écran tel écrit (WYSIWYG) et permettre aux auteurs et autrices de mettre en forme le contenu directement sur la page web.
uuid: eb3da415-cbef-4766-a28e-837e238a4156
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: components
content-type: reference
discoiquuid: 7b234f1f-4470-4de1-a3c3-ab19e5e001ad
docset: aem65
exl-id: 56a9591c-cd78-42e8-a5d7-6b48581d6af6
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '4925'
ht-degree: 99%

---

# Utilisation et extension de widgets (IU classique){#using-and-extending-widgets-classic-ui}

>[!NOTE]
>
>Cette page décrit l’utilisation des widgets dans l’IU classique, qui était obsolète dans AEM 6.4.
>
>Adobe vous recommande d’utiliser l’[IU tactile](/help/sites-developing/touch-ui-concepts.md) moderne, basée sur l’[IU Coral](/help/sites-developing/touch-ui-concepts.md#coral-ui) et l’[IU Granite](/help/sites-developing/touch-ui-concepts.md#granite-ui-foundation-components).

L’interface web d’Adobe Experience Manager utilise AJAX et d’autres technologies modernes intégrées dans les navigateurs pour activer l’édition tel écran tel écrit (WYSIWYG) et permettre aux auteurs et autrices de mettre en forme le contenu directement sur la page web.

AEM utilise la bibliothèque de widgets [ExtJS](https://www.sencha.com/), qui fournit des éléments d’interface utilisateur très soignés qui fonctionnent sur tous les navigateurs les plus importants et permettent de créer des expériences d’interface utilisateur de niveau bureau.

Ces widgets sont inclus dans AEM et, en plus d’être utilisés par AEM lui-même, peuvent être utilisés par n’importe quel site web créé à l’aide d’AEM.

Pour consulter la liste complète de tous les widgets disponibles dans AEM, vous pouvez vous reporter à la [documentation sur les API des widgets](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html) ou à la [liste des xtypes existants](/help/sites-developing/xtypes.md). En outre, de nombreux exemples montrant comment utiliser le framework ExtJS sont disponibles sur le site de [Sencha](https://examples.sencha.com/extjs/7.6.0/), le propriétaire du framework.

Cette page donne quelques informations sur l’utilisation et l’optimisation des widgets. Elle décrit d’abord comment [inclure un code côté client dans une page](#including-the-client-sided-code-in-a-page). Elle décrit ensuite quelques exemples de composants qui ont été créés pour illustrer une utilisation et une extension de base. Ces composants sont disponibles dans le module **Utilisation des widgets ExtJS** dans **Partage de packages**.

Le package comprend des exemples de :

* Des [Boîtes de dialogue de base](#basic-dialogs) créées grâce à des widgets prêts à l’emploi.
* Des [Boîtes de dialogue dynamiques](#dynamic-dialogs) créées grâce à des widgets prêts à l’emploi et à une logique JavaScript personnalisée.
* Des boîtes de dialogue basées sur des [widgets personnalisés](#custom-widgets).
* Un [panneau d’arborescence](#tree-overview) affichant une arborescence JCR sous un chemin d’accès donné.
* Un [panneau grille](#grid-overview) affichant des données sous la forme d’un tableau.

>[!NOTE]
>
>L’IU classique d’Adobe Experience Manager repose sur [ExtJS 3.4.0](https://extjs.cachefly.net/ext-3.4.0/docs/).

## Insertion du code côté client dans une page {#including-the-client-sided-code-in-a-page}

Le code JavaScript côté client et de feuille de style doit être placé dans une bibliothèque cliente.

Pour créer une bibliothèque cliente, procédez comme suit :

1. Créez un nœud sous `/apps/<project>` avec les propriétés suivantes :

   * name=&quot;clientlib&quot;
   * jcr:mixinTypes=&quot;[mix:lockable]&quot;
   * jcr:primaryType=&quot;cq:ClientLibraryFolder&quot;
   * sling:resourceType=&quot;widgets/clientlib&quot;
   * categories=&quot;[&lt;category-name>]&quot;
   * dependencies=&quot;[cq.widgets]&quot;

   `Note: <category-name> is the name of the custom library (for example, "cq.extjstraining") and is used to include the library on the page.`

1. Sous `clientlib`, créez les dossiers `css` et `js` (nt:folder).

1. Sous `clientlib`, créez les fichiers `css.txt` et `js.txt` (nt:files). Ces fichiers .txt répertorient les fichiers qui sont inclus dans la bibliothèque.

1. Modifier`js.txt` : il doit commencer par « `#base=js` », suivi de la liste des fichiers qui seront agrégés par le service de bibliothèque cliente CQ, par exemple :

   ```
   #base=js
    components.js
    exercises.js
    CustomWidget.js
    CustomBrowseField.js
    InsertTextPlugin.js
   ```

1. Modifier`css.txt` : il doit commencer par « `#base=css` », suivi de la liste des fichiers qui seront agrégés par le service de bibliothèque cliente CQ, par exemple :

   ```
   #base=css
    components.css
   ```

1. Sous le dossier `js`, placez les fichiers JavaScript appartenant à la bibliothèque.

1. Sous le dossier `css`, placez les fichiers `.css` et les ressources utilisées par les fichiers css (par exemple, `my_icon.png`).

>[!NOTE]
>
>La gestion des feuilles de style décrite précédemment est facultative.

Pour inclure la bibliothèque cliente dans le fichier jsp du composant de page, procédez comme suit :

* pour inclure le code JavaScript et les feuilles de style :
  `<ui:includeClientLib categories="<category-name1>, <category-name2>, ..."/>`
where `<category-nameX>` est le nom de la bibliothèque côté client.

* pour inclure uniquement le code JavaScript :
  `<ui:includeClientLib js="<category-name>"/>`

Pour plus d’informations, voir la description de la variable [&lt;ui:includeclientlib>](/help/sites-developing/taglib.md#lt-ui-includeclientlib) balise .

Parfois, une bibliothèque cliente ne doit être disponible qu’en mode création et doit être exclue du mode publication. Cela peut se faire comme suit :

```xml
    if (WCMMode.fromRequest(request) != WCMMode.DISABLED) {
        %><ui:includeClientLib categories="cq.collab.blog"/><%
    }
```

### Prise en main des exemples {#getting-started-with-the-samples}

Pour suivre les tutoriels sur cette page, installez le package **Utilisation des widgets ExtJS** dans une instance locale d’AEM, puis créez un une page d’exemple dans laquelle les composants seront inclus. Pour ce faire, procédez comme suit :

1. Dans votre instance d’AEM, téléchargez le package nommé **Utilisation des widgets ExtJS (v01)** dans le partage de packages, puis installez le package. Il crée le projet `extjstraining` sous `/apps` dans le référentiel.
1. Incluez la bibliothèque cliente contenant les scripts (js) et la feuille de style (css) dans la balise head du jsp de la page Geometrixx. Vous allez inclure les exemples de composants dans une nouvelle page de la branche **Geometrixx** :
dans **CRXDE Lite** ouvrez le fichier `/apps/geometrixx/components/page/headlibs.jsp` et ajoutez la catégorie `cq.extjstraining` à la balise `<ui:includeClientLib>` existante de la façon suivante :
   `%><ui:includeClientLib categories="apps.geometrixx-main, cq.extjstraining"/><%`
1. Créez une page dans la branche **Geometrixx** sous `/content/geometrixx/en/products` et nommez-la **Utilisation des widgets ExtJS**.
1. Passez en mode Création et ajoutez tous les composants du groupe appelé **Utilisation des widgets ExtJS** à la conception de Geometrixx.
1. Revenez au mode d’édition : les composants du groupe **Utilisation des widgets ExtJS** sont disponibles dans le sidekick.

>[!NOTE]
>
>Les exemples de cette page sont basés sur l’échantillon de contenu Geometrixx. Celui-ci n’est plus fourni avec AEM et a été remplacé par We.Retail. Pour savoir comment télécharger et installer Geometrixx, consultez l’[implémentation de référence We.Retail](/help/sites-developing/we-retail.md#we-retail-geometrixx).

### Boîtes de dialogue de base {#basic-dialogs}

Les boîtes de dialogue sont généralement utilisées pour modifier le contenu, mais elles peuvent également afficher des informations. Pour afficher facilement une boîte de dialogue complète, accédez à sa représentation au format json. Pour ce faire, pointez votre navigateur vers :

`https://localhost:4502/<path-to-dialog>.-1.json`

Le premier composant du groupe **Utilisation des widgets ExtJS** du sidekick est appelé **1. Principes de base de la boîte de dialogue** et comprend quatre boîtes de dialogue de base qui sont créées avec des widgets prêts à l’emploi et sans logique JavaScript personnalisée. Les boîtes de dialogue sont stockées sous `/apps/extjstraining/components/dialogbasics`. Les boîtes de dialogue de base sont les suivantes :

* la boîte de dialogue complète (nœud `full`) : elle affiche une fenêtre avec trois onglets ayant chacun deux champs de texte.
* la boîte de dialogue à panneau unique (nœud `singlepanel`) : elle affiche une fenêtre avec un seul onglet comprenant deux champs de texte.
* la boîte de dialogue à plusieurs panneaux (nœud `multipanel`) : l’affichage est identique à celui de la boîte de dialogue complète, mais la construction est différente.
* la boîte de dialogue de conception (nœud `design`) : elle affiche une fenêtre avec deux onglets. Le premier onglet comprend un champ de texte, un menu déroulant et une zone de texte réductible. Le deuxième onglet comporte un ensemble de champs avec quatre champs de texte et un ensemble de champs réductible avec deux champs de texte.

Inclure le composant **1. Principes de base de la boîte de dialogue** dans l’exemple de page :

1. Ajoutez le composant **1. Composant de base de boîte de dialogue** à l’exemple de page à partir de l’onglet **Utilisation des widgets ExtJS** dans le **sidekick**.
1. Le composant affiche un titre, du texte et un lien **PROPRIÉTÉS**. La sélection du lien affiche les propriétés du paragraphe stocké dans le référentiel. Sélectionnez à nouveau le lien pour masquer les propriétés.

Le composant se présente sous la forme suivante :

![chlimage_1-60](assets/chlimage_1-60.png)

#### Exemple 1 : boîte de dialogue complète {#example-full-dialog}

La boîte de dialogue **complète** affiche une fenêtre avec trois onglets, chacun d’eux comportant deux champs de texte. Il s’agit de la boîte de dialogue par défaut du composant **Principes de base de la boîte de dialogue**. Ses caractéristiques sont les suivantes :

* Elle est définie par un nœud : type de nœud = `cq:Dialog`, xtype = ` [dialog](/help/sites-developing/xtypes.md#dialog)`.
* Affiche trois onglets (type de nœud = `cq:Panel`).
* Chaque onglet comporte deux champs de texte (type de nœud = `cq:Widget`, xtype = ` [textfield](/help/sites-developing/xtypes.md#textfield)`).
* Est défini par le nœud :
  `/apps/extjstraining/components/dialogbasics/full`
* Son rendu est effectué au format JSON en demandant :
  `https://localhost:4502/apps/extjstraining/components/dialogbasics/full.-1.json`

La boîte de dialogue se présente comme suit :

![screen_shot_2012-01-31at45411pm](assets/screen_shot_2012-01-31at45411pm.png)

#### Exemple 2 : Boîte de dialogue à un seul panneau {#example-single-panel-dialog}

La boîte de dialogue **à panneau unique** affiche une fenêtre avec un onglet contenant deux champs de texte. Ses caractéristiques sont les suivantes :

* Affiche un onglet (type de nœud = `cq:Dialog`, xtype = ` [panel](/help/sites-developing/xtypes.md#panel)`).
* L’onglet comporte deux champs de texte (type de nœud = `cq:Widget`, xtype = ` [textfield](/help/sites-developing/xtypes.md#textfield)`).
* Est défini par le nœud :
  `/apps/extjstraining/components/dialogbasics/singlepanel`
* Son rendu est effectué au format json en demandant :
  `https://localhost:4502/apps/extjstraining/components/dialogbasics/singlepanel.-1.json`
* Un avantage par rapport à la **Boîte de dialogue complète** est qu’une configuration moindre est nécessaire.
* Utilisation recommandée : pour les boîtes de dialogue simples qui affichent des informations ou qui ne comportent que quelques champs.

Pour utiliser la boîte de dialogue à panneau unique, procédez comme suit :

1. Remplacez la boîte de dialogue du composant **Principes de base de la boîte de dialogue** par la boîte de dialogue à **panneau unique** :
   1. Dans **CRXDE Lite**, supprimez le nœud suivant : `/apps/extjstraining/components/dialogbasics/dialog`.
   1. Cliquez sur **Enregistrer tout** pour enregistrer les modifications.
   1. Copiez le nœud : `/apps/extjstraining/components/dialogbasics/singlepanel`.
   1. Collez ci-dessous le nœud que vous avez copié : `/apps/extjstraining/components/dialogbasics`.
   1. Sélectionnez le nœud `/apps/extjstraining/components/dialogbasics/Copy of singlepanel` et renommez-le `dialog`.
1. Modifiez le composant. La boîte de dialogue s’affiche alors comme suit :

![screen_shot_2012-01-31at45952pm](assets/screen_shot_2012-01-31at45952pm.png)

#### Exemple 3 : boîte de dialogue à plusieurs panneaux {#example-multi-panel-dialog}

La boîte de dialogue à **plusieurs panneaux** présente le même affichage que la boîte de dialogue **complète**, mais sa conception est différente. Ses caractéristiques sont les suivantes :

* Elle est définie par un nœud (type de nœud = `cq:Dialog`, xtype = ` [tabpanel](/help/sites-developing/xtypes.md#tabpanel)`).
* Affiche trois onglets (type de nœud = `cq:Panel`).
* Chaque onglet comporte deux champs de texte (type de nœud = `cq:Widget`, xtype = ` [textfield](/help/sites-developing/xtypes.md#textfield)`).
* Est défini par le nœud :
  `/apps/extjstraining/components/dialogbasics/multipanel`
* Son rendu est effectué au format json en demandant :
  `https://localhost:4502/apps/extjstraining/components/dialogbasics/multipanel.-1.json`
* Par rapport à la **Boîte de dialogue complète**, elle présente une structure simplifiée.
* Utilisation recommandée : pour les boîtes de dialogues à plusieurs onglets.

Pour utiliser la boîte de dialogue à plusieurs panneaux, procédez comme suit :

1. Remplacez la boîte de dialogue du composant **Éléments de base de la boîte de dialogue** par la boîte de dialogue **à plusieurs panneaux** :
Suivez la procédure décrite à la section [Exemple 2 : boîte de dialogue à un seul panneau](#example-single-panel-dialog).
1. Modifiez le composant. La boîte de dialogue s’affiche alors comme suit :

![screen_shot_2012-01-31at50119pm](assets/screen_shot_2012-01-31at50119pm.png)

#### Exemple 4 : Format Riche {#example-rich-dialog}

La boîte de dialogue **enrichie** affiche une fenêtre avec deux onglets. Le premier onglet comprend un champ de texte, un menu déroulant et une zone de texte réductible. Le deuxième onglet comporte un ensemble de champs avec quatre champs de texte et un ensemble de champs réductible avec deux champs de texte. Ses caractéristiques sont les suivantes :

* Elle est définie par un nœud (type de nœud = `cq:Dialog`, xtype = ` [dialog](/help/sites-developing/xtypes.md#dialog)`).
* Affiche deux onglets (type de nœud = `cq:Panel`).
* Le premier onglet comporte un widget ` [dialogfieldset](/help/sites-developing/xtypes.md#dialogfieldset)` avec un ` [textfield](/help/sites-developing/xtypes.md#textfield)` et un widget ` [selection](/help/sites-developing/xtypes.md#selection)` avec trois options, ainsi qu’un ` [dialogfieldset](/help/sites-developing/xtypes.md#dialogfieldset)` réductible avec un widget ` [textarea](/help/sites-developing/xtypes.md#textarea)`.
* Le deuxième onglet comprend un widget ` [dialogfieldset](/help/sites-developing/xtypes.md#dialogfieldset)` avec quatre widgets ` [textfield](/help/sites-developing/xtypes.md#textfield)`, ainsi qu’un `dialogfieldset` réductible avec deux widgets ` [textfield](/help/sites-developing/xtypes.md#textfield)`.
* Est défini par le nœud :
  `/apps/extjstraining/components/dialogbasics/rich`
* Son rendu est effectué au format json en demandant :
  `https://localhost:4502/apps/extjstraining/components/dialogbasics/rich.-1.json`

Pour utiliser la boîte de dialogue **Riche**, procédez comme suit :

1. Remplacez la boîte de dialogue du composant **Éléments de base de boîte de dialogue** par la boîte de dialogue **Riche** :
Suivez la procédure décrite pour [Exemple 2 : boîte de dialogue à un seul panneau](#example-single-panel-dialog).
1. Modifiez le composant. La boîte de dialogue s’affiche alors comme suit :

![screen_shot_2012-01-31at50429pm](assets/screen_shot_2012-01-31at50429pm.png) ![screen_shot_2012-01-31at50519pm](assets/screen_shot_2012-01-31at50519pm.png)

### Boîtes de dialogue dynamiques {#dynamic-dialogs}

Le deuxième composant du groupe **Utilisation des widgets ExtJS** dans le sidekick est appelé **2. Boîtes de dialogue dynamiques** et comprend trois boîtes de dialogue dynamiques conçues avec des widgets prêts à l’emploi et **avec une logique JavaScript personnalisée**. Les boîtes de dialogue sont stockées sous `/apps/extjstraining/components/dynamicdialogs`. Les boîtes de dialogue dynamiques sont les suivantes :

* Boîte de dialogue Switch Tabs (nœud `switchtabs`) : elle affiche une fenêtre avec deux onglets. Le premier onglet comporte une sélection radio avec trois options : lorsqu’une option est sélectionnée, un onglet correspondant à l’option s’affiche. Le deuxième onglet comporte deux champs de texte.
* Boîte de dialogue Arbitrary (nœud `arbitrary`) : elle affiche une fenêtre avec un seul onglet. Cet onglet se compose d’une zone permettant de déposer ou de charger une ressource, ainsi que d’une section affichant des informations sur la page et sur la ressource, le cas échéant.
* Boîte de dialogue Toggle Fields (nœud `togglefield`) : elle affiche une fenêtre avec un seul onglet. Cet onglet comprend une case à cocher : lorsque cette case est cochée, un jeu de champs composé de deux champs de texte est affiché.

Pour inclure le composant **2. Boîtes de dialogue dynamiques** dans l’exemple de page, procédez comme suit :

1. Ajoutez le composant **2. Boîtes de dialogue dynamiques** à l’exemple de page à partir de l’onglet **Utilisation des widgets ExtJS** dans le **sidekick**.
1. Le composant affiche un titre, du texte et un lien **PROPRIÉTÉS**. La sélection du lien affiche les propriétés du paragraphe stocké dans le référentiel. Sélectionnez à nouveau le lien pour masquer les propriétés.

Le composant se présente sous la forme suivante :

![chlimage_1-61](assets/chlimage_1-61.png)

#### Exemple 1 : boîte de dialogue Switch Tabs {#example-switch-tabs-dialog}

La boîte de dialogue **Switch Tabs** affiche une fenêtre avec deux onglets. Le premier onglet comporte une sélection radio avec trois options : lorsqu’une option est sélectionnée, un onglet correspondant à l’option s’affiche. Le deuxième onglet comporte deux champs de texte.

Ses caractéristiques principales sont les suivantes :

* Elle est définie par un nœud (type de nœud = `cq:Dialog`, xtype = ` [dialog](/help/sites-developing/xtypes.md#dialog)`).
* Affiche deux onglets (type de nœud = `cq:Panel`) : un onglet de sélection, le deuxième onglet dépend de la sélection effectuée dans le premier onglet (trois options).
* Elle comprend trois onglets facultatifs (type de nœud = `cq:Panel`) ayant chacun deux champs de texte (type de nœud = `cq:Widget`, xtype = ` [textfield](/help/sites-developing/xtypes.md#textfield)`). Un seul onglet facultatif est affiché à la fois.
* Est défini par le nœud `switchtabs` à l’adresse :
  `/apps/extjstraining/components/dynamicdialogs/switchtabs`
* Son rendu est effectué au format json en demandant :
  `https://localhost:4502/apps/extjstraining/components/dynamicdialogs/switchtabs.-1.json`

Cette logique est implémentée par le biais de listeners d’événements et de code JavaScript comme suit :

* Le nœud de la boîte de dialogue comporte un listener « `beforeshow` » qui masque tous les onglets facultatifs avant l’affichage de la boîte de dialogue :
  `beforeshow="function(dialog){Ejst.x2.manageTabs(dialog.items.get(0));}"`
  `dialog.items.get(0)` obtient le `tabpanel` qui contient le panneau de sélection et les trois panneaux facultatifs.
* L’objet `Ejst.x2` est défini dans le fichier `exercises.js` à l’emplacement suivant :
  `/apps/extjstraining/clientlib/js/exercises.js`
* Dans la méthode `Ejst.x2.manageTabs()`, étant donné que la valeur `index` est -1, tous les onglets facultatifs sont masqués (i passe de 1 à 3).
* L’onglet de sélection comprend deux listeners : l’un affiche l’onglet sélectionné lors du chargement de la boîte de dialogue (événement « `loadcontent` ») et l’autre affiche l’onglet sélectionné lors du changement de la sélection (événement « `selectionchanged` ») :
  `loadcontent="function(field,rec,path){Ejst.x2.showTab(field);}"`
  `selectionchanged="function(field,value){Ejst.x2.showTab(field);}"`
* Pour la méthode `Ejst.x2.showTab()`,
  `field.findParentByType('tabpanel')` obtient le `tabpanel` qui contient tous les onglets (`field` représente le widget de sélection) ;
  `field.getValue()` obtient la valeur de la sélection, par exemple : tab2 ;
  `Ejst.x2.manageTabs()` affiche l’onglet sélectionné.
* Chaque onglet facultatif comprend un listener qui le masque lorsque l’événement « `render` » se produit :
  `render="function(tab){Ejst.x2.hideTab(tab);}"`
* Pour la méthode `Ejst.x2.hideTab()`,
  `tabPanel` est le `tabpanel` qui contient tous les onglets ;
  `index` est l’index de l’onglet facultatif.
  `tabPanel.hideTabStripItem(index)` masque l’onglet.

Il se présente comme suit :

![screen_shot_2012-02-01at114745am](assets/screen_shot_2012-02-01at114745am.png)

#### Exemple 2 : boîte de dialogue Arbitrary {#example-arbitrary-dialog}

Très souvent, une boîte de dialogue affiche du contenu provenant d’un composant sous-jacent. La boîte de dialogue décrite ici, baptisée **Arbitrary**, extrait le contenu d’un autre composant.

La boîte de dialogue **Arbitrary** affiche une fenêtre avec un seul onglet. L’onglet comporte deux champs : l’un pour télécharger ou télécharger en amont une ressource et l’autre pour afficher des informations sur la page qui la contient et sur la ressource si elle a été référencée.

Ses caractéristiques principales sont les suivantes :

* Elle est définie par un nœud (type de nœud = `cq:Dialog`, xtype = ` [dialog](/help/sites-developing/xtypes.md#dialog)`).
* Affiche un widget `tabpanel` (type de nœud = `cq:Widget`, xtype = ` [tabpanel](/help/sites-developing/xtypes.md#tabpanel)`) avec un panneau (type de nœud = `cq:Panel`).
* Le panneau comprend un widget smartfile (type de nœud = `cq:Widget`, xtype = ` [smartfile](/help/sites-developing/xtypes.md#smartfile)`) et un widget ownerdraw (type de nœud = `cq:Widget`, xtype = ` [ownerdraw](/help/sites-developing/xtypes.md#ownerdraw)`).
* Est défini par le nœud `arbitrary` à l’adresse :
  `/apps/extjstraining/components/dynamicdialogs/arbitrary`
* Son rendu est effectué au format json en demandant :
  `https://localhost:4502/apps/extjstraining/components/dynamicdialogs/arbitrary.-1.json`

Cette logique est implémentée par le biais de listeners d’événements et de code JavaScript comme suit :

* Le widget `ownerdraw` comporte un listener « `loadcontent` » qui affiche des informations sur la page contenant le composant. En d’autres termes, la ressource référencée par le widget de fichier intelligent lors du chargement du contenu :
  `loadcontent="function(field,rec,path){Ejst.x2.showInfo(field,rec,path);}"`
  `field` est défini avec l’objet `ownerdraw` ;
  `path` est défini avec le chemin d’accès au contenu du composant (par exemple, `/content/geometrixx/en/products/triangle/ui-tutorial/jcr:content/par/dynamicdialogs`).
* L’objet `Ejst.x2` est défini dans le fichier `exercises.js` à l’emplacement suivant :
  `/apps/extjstraining/clientlib/js/exercises.js`
* Pour la méthode `Ejst.x2.showInfo()`,
  `pagePath` est le chemin d’accès de la page contenant le composant ;
  `pageInfo` représente les propriétés de page au format json ;
  `reference` est le chemin d’accès de la ressource référencée ;
  `metadata` représente les métadonnées de la ressource au format json ;
  `ownerdraw.getEl().update(html);` affiche le code HTML créé dans la boîte de dialogue.

Pour utiliser la boîte de dialogue **Arbitrary**, procédez comme suit :

1. Remplacez la boîte de dialogue du composant **Boîte de dialogue dynamique** par la boîte de dialogue **Arbitraire** :
Suivez la procédure décrite pour [Exemple 2 : boîte de dialogue à un seul panneau](#example-single-panel-dialog).
1. Modifiez le composant. La boîte de dialogue s’affiche alors comme suit :

![screen_shot_2012-02-01at115300am](assets/screen_shot_2012-02-01at115300am.png)

#### Exemple 3 : Boîte de dialogue Toggle Fields {#example-toggle-fields-dialog}

La boîte de dialogue **Toggle Fields** affiche une fenêtre avec un seul onglet. Cet onglet comprend une case à cocher : lorsque cette case est cochée, un jeu de champs composé de deux champs de texte est affiché.

Ses caractéristiques principales sont les suivantes :

* Elle est définie par un nœud (type de nœud = `cq:Dialog`, xtype = ` [dialog](/help/sites-developing/xtypes.md#dialog)`).
* Affiche un widget `tabpanel` (type de nœud = `cq:Widget`, xtype = ` [tabpanel](/help/sites-developing/xtypes.md#textpanel)`) avec un panneau (type de nœud = `cq:Panel`).
* Le panneau comprend un widget de sélection/case à cocher (type de nœud = `cq:Widget`, xtype = ` [selection](/help/sites-developing/xtypes.md#selection)`, type = ` [checkbox](/help/sites-developing/xtypes.md#checkbox)`) et un widget dialogfieldset réductible (type de nœud = `cq:Widget`, xtype = ` [dialogfieldset](/help/sites-developing/xtypes.md#dialogfieldset)`), qui est masqué par défaut, avec deux widgets textfield (type de nœud = `cq:Widget`, xtype = ` [textfield](/help/sites-developing/xtypes.md#textfield)`).
* Est défini par le nœud `togglefields` à l’adresse :
  `/apps/extjstraining/components/dynamicdialogs/togglefields`
* Son rendu est effectué au format json en demandant :
  `https://localhost:4502/apps/extjstraining/components/dynamicdialogs/togglefields.-1.json`

Cette logique est implémentée par le biais de listeners d’événements et de code JavaScript comme suit :

* la sélection comprend deux listeners : l’un affiche le widget dialogfieldset lors du chargement du contenu (événement « `loadcontent` ») et l’autre affiche le widget dialogfieldset lors du changement de la sélection (événement « `selectionchanged` ») :
  `loadcontent="function(field,rec,path){Ejst.x2.toggleFieldSet(field);}"`
  `selectionchanged="function(field,value){Ejst.x2.toggleFieldSet(field);}"`
* L’objet `Ejst.x2` est défini dans le fichier `exercises.js` à l’emplacement suivant :
  `/apps/extjstraining/clientlib/js/exercises.js`
* Pour la méthode `Ejst.x2.toggleFieldSet()`,
  `box` est l’objet de sélection ;
  `panel` est le panneau contenant la sélection et les widgets dialogfieldset ;
  `fieldSet` est l’objet dialogfieldset ;
  `show` est la valeur de la sélection (true ou false) ;
basée sur « `show` » si dialogfieldset s’affiche ou non.

Pour utiliser la boîte de dialogue **Toggle Fields**, procédez comme suit :

1. Remplacez la boîte de dialogue du composant **Boîte de dialogue dynamique** par la boîte de dialogue **Champs de bouton bascule** :
Suivez la procédure décrite pour [Exemple 2 : boîte de dialogue à un seul panneau](#example-single-panel-dialog).
1. Modifiez le composant. La boîte de dialogue s’affiche alors comme suit :

![screen_shot_2012-02-01at115518am](assets/screen_shot_2012-02-01at115518am.png)

### Widgets personnalisés {#custom-widgets}

Les widgets prêts à l’emploi fournis avec AEM doivent couvrir la plupart des cas d’utilisation. Cependant, il peut, dans certaines situations, s’avérer nécessaire de créer un widget personnalisé pour traiter un cas spécifique à un projet. Les widgets personnalisés peuvent être créés en optimisant les widgets existants. Pour faciliter la prise en main de cette personnalisation, le package **`Using ExtJS Widgets`** comprend trois boîtes de dialogue qui utilisent trois widgets personnalisés différents :

* La boîte de dialogue Multi Field (nœud `multifield`) affiche une fenêtre avec un seul onglet. Cet onglet comprend un widget multifield personnalisé qui comporte deux zones : un menu déroulant avec deux options et un champ de texte. Étant donné qu’il est basé sur le widget `multifield` prêt à l’emploi (qui comprend uniquement un champ de texte), il possède toutes les fonctionnalités du widget `multifield`.
* La boîte de dialogue Tree Browse (nœud `treebrowse`) affiche une fenêtre avec un seul onglet contenant un widget d’exploration du chemin : lorsque vous cliquez sur la flèche, une fenêtre s’ouvre dans laquelle vous pouvez parcourir une hiérarchie et sélectionner un élément. Le chemin d’accès de l’élément est ensuite ajouté au champ du chemin et conservé lorsque la boîte de dialogue est fermée.
* Une boîte de dialogue basée sur le module Éditeur de texte enrichi (nœud `rteplugin`) qui ajoute un bouton personnalisé à l’Éditeur de texte enrichi pour insérer du texte personnalisé dans le texte principal. Elle comprend un widget `richtext` (RTE) et une fonctionnalité personnalisée, ajoutée par le biais du module externe RTE.

Les widgets personnalisés et le module externe sont inclus dans le composant appelé **3. Widgets personnalisés** du package **Utilisation des widgets ExtJS**. Pour inclure ce composant dans l’exemple de page :

1. Ajoutez le composant **3. Widgets personnalisés** à l’exemple de page à partir de l’onglet **Utilisation des widgets ExtJS** dans le **sidekick**.
1. Le composant affiche un titre, du texte et, lorsque vous cliquez sur le lien **PROPRIÉTÉS**, les propriétés du paragraphe stocké dans le référentiel. Cliquez à nouveau pour masquer les propriétés.
Le composant se présente sous la forme suivante :

![chlimage_1-62](assets/chlimage_1-62.png)

#### Exemple 1 : Widget Custom Multifield {#example-custom-multifield-widget}

La boîte de dialogue basée sur le widget **Custom Multifield** affiche une fenêtre avec un seul onglet. L’onglet comporte un widget champ personnalisé à choix multiples qui, contrairement au widget standard qui comporte un champ, a deux champs : un menu déroulant avec deux options et un champ de texte.

La boîte de dialogue basée sur le widget **Custom Multifield** :

* est définie par un nœud (type de nœud = `cq:Dialog`, xtype = ` [dialog](/help/sites-developing/xtypes.md#dialog)`) ;
* affiche un widget `tabpanel` (type de nœud = `cq:Widget`, xtype = ` [tabpanel](/help/sites-developing/xtypes.md#tabpanel)`) contenant un panneau (type de nœud = `cq:Widget`, xtype = ` [panel](/help/sites-developing/xtypes.md#panel)`).
* Le panneau comprend un widget `multifield` (type de nœud = `cq:Widget`, xtype = ` [multifield](/help/sites-developing/xtypes.md#multifield)`).
* Le widget `multifield` comprend une option fieldconfig (type de nœud = `nt:unstructured`, xtype = `ejstcustom`, optionsProvider = `Ejst.x3.provideOptions`) basée sur le xtype personnalisé « `ejstcustom` » :
   * « `fieldconfig` » est une option de configuration de l’objet ` [CQ.form.MultiField](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.form.MultiField)`.
   * « `optionsProvider` » est une configuration du widget `ejstcustom`. Elle est définie avec la méthode `Ejst.x3.provideOptions` qui est définie dans `exercises.js` dans :
     `/apps/extjstraining/clientlib/js/exercises.js`
et renvoie deux options.
* Est défini par le nœud `multifield` à l’adresse :
  `/apps/extjstraining/components/customwidgets/multifield`
* Son rendu est effectué au format json en demandant :
  `https://localhost:4502/apps/extjstraining/components/customwidgets/multifield.-1.json`

Le widget `multifield` personnalisé (xtype = `ejstcustom`) :

* est un objet JavaScript appelé `Ejst.CustomWidget` ;
* est défini dans le fichier JavaScript `CustomWidget.js` à l’emplacement suivant :
  `/apps/extjstraining/clientlib/js/CustomWidget.js`
* étend le widget ` [CQ.form.CompositeField](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.form.CompositeField)` ;
* comporte trois champs : `hiddenField` (Textfield), `allowField` (ComboBox) et `otherField` (Textfield) ;
* remplace `CQ.Ext.Component#initComponent` pour ajouter les trois champs :
   * `allowField` est un objet [CQ.form.Selection](https://developer.adobe.com/fr/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.form.Selection) de type « select ». optionsProvider est une configuration de l’objet Selection qui est instanciée avec la configuration optionsProvider du widget personnalisé (CustomWidget) défini dans la boîte de dialogue.
   * `otherField` est un objet [CQ.Ext.form.TextField](https://developer.adobe.com/fr/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.form.TextField).
* remplace les méthodes `setValue`, `getValue` et `getRawValue` de [CQ.form.CompositeField](https://developer.adobe.com/fr/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.form.CompositeField) afin de définir et de récupérer la valeur de CustomWidget au format :
  `<allowField value>/<otherField value>, for example: 'Bla1/hello'`.
* S’enregistre lui-même en tant que xtype « `ejstcustom` » :
  `CQ.Ext.reg('ejstcustom', Ejst.CustomWidget);`

La boîte de dialogue basée sur le widget **Custom Multifield** se présente comme suit :

![screen_shot_2012-02-01at115840am](assets/screen_shot_2012-02-01at115840am.png)

#### Exemple 2 : widget `Treebrowse` personnalisé {#example-custom-treebrowse-widget}

La boîte de dialogue basée sur le widget **`Treebrowse`** affiche une fenêtre avec un onglet contenant un widget de navigation de chemin personnalisé. Lorsque vous sélectionnez la flèche, une fenêtre s’ouvre dans laquelle vous pouvez parcourir une hiérarchie et sélectionner un élément. Le chemin d’accès de l’élément est ensuite ajouté au champ du chemin et conservé lorsque la boîte de dialogue est fermée.

La boîte de dialogue `treebrowse` personnalisée :

* est définie par un nœud (type de nœud = `cq:Dialog`, xtype = ` [dialog](/help/sites-developing/xtypes.md#dialog)`) ;
* affiche un widget `tabpanel` (type de nœud = `cq:Widget`, xtype = ` [tabpanel](/help/sites-developing/xtypes.md#tabpanel)`) contenant un panneau (type de nœud = `cq:Widget`, xtype = ` [panel](/help/sites-developing/xtypes.md#panel)`).
* Le panneau comprend un widget personnalisé (type de nœud = `cq:Widget`, xtype = `ejstbrowse`).
* Est défini par le nœud `treebrowse` à l’adresse :
  `/apps/extjstraining/components/customwidgets/treebrowse`
* Son rendu est effectué au format json en demandant :
  `https://localhost:4502/apps/extjstraining/components/customwidgets/treebrowse.-1.json`

Widget treebrowse personnalisé (xtype = `ejstbrowse`) :

* est un objet JavaScript appelé `Ejst.CustomWidget` ;
* est défini dans le fichier JavaScript `CustomBrowseField.js` à l’emplacement suivant :
  `/apps/extjstraining/clientlib/js/CustomBrowseField.js`
* Il étend ` [CQ.Ext.form.TriggerField](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.form.TriggerField)`.
* Il définit une fenêtre de navigation appelée `browseWindow`.
* Il remplace ` [CQ.Ext.form.TriggerField](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.form.TriggerField)#onTriggerClick` pour afficher la fenêtre de navigation lorsque l’utilisateur clique sur la flèche.
* Il définit un objet [CQ.Ext.tree.TreePanel](https://developer.adobe.com/fr/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.tree.TreePanel) :
   * Il récupère ses données en appelant le servlet enregistré à l’emplacement `/bin/wcm/siteadmin/tree.json`.
   * Sa racine est « `apps/extjstraining` ».
* Il définit un objet `window` (` [CQ.Ext.Window](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.Window)`) :
   * Il est basé sur le panneau prédéfini.
   * Il comprend un bouton **OK** qui définit la valeur du chemin d’accès sélectionné et masque le panneau.
* La fenêtre est ancrée sous le champ **Chemin d’accès**.
* Le chemin d’accès est transmis du champ de navigation à la fenêtre lorsque l’événement `show` se produit.
* S’enregistre lui-même en tant que xtype « `ejstbrowse` » :
  `CQ.Ext.reg('ejstbrowse', Ejst.CustomBrowseField);`

Pour utiliser la boîte de dialogue basée sur le widget **Custom Treebrowse**, procédez comme suit :

1. Remplacez la boîte de dialogue du composant **Widgets personnalisés** par la boîte de dialogue **Exploration d’arborescence personnalisée** :
Suivez la procédure décrite pour [Exemple 2 : boîte de dialogue à un seul panneau](#example-single-panel-dialog).
1. Modifiez le composant. La boîte de dialogue s’affiche alors comme suit :

![screen_shot_2012-02-01at120104pm](assets/screen_shot_2012-02-01at120104pm.png)

#### Exemple 3 : module externe Éditeur de texte enrichi (RTE) {#example-rich-text-editor-rte-plug-in}

La boîte de dialogue basée sur le **module externe Éditeur de texte enrichi (RTE)** dispose d’un bouton personnalisé permettant d’insérer du texte personnalisé entre crochets. Le texte personnalisé peut être analysé par une logique côté serveur (non implémentée dans cet exemple), par exemple, pour ajouter du texte défini au chemin donné :

Boîte de dialogue basée sur le **module externe de RTE** :

* Elle est définie par le nœud rteplugin à l’emplacement suivant :
  `/apps/extjstraining/components/customwidgets/rteplugin`
* Son rendu est effectué au format json en demandant :
  `https://localhost:4502/apps/extjstraining/components/customwidgets/rteplugin.-1.json`
* Le nœud `rtePlugins` comprend un nœud enfant `inserttext` (type de nœud = `nt:unstructured`) dont le nom provient du module externe. Elle dispose d’une propriété appelée `features`, qui définit les fonctionnalités du module externe disponibles pour l’éditeur de texte enrichi.

Module externe de RTE :

* est un objet JavaScript appelé `Ejst.InsertTextPlugin` ;
* est défini dans le fichier JavaScript `InsertTextPlugin.js` à l’emplacement suivant :
  `/apps/extjstraining/clientlib/js/InsertTextPlugin.js`
* Il étend l’objet ` [CQ.form.rte.plugins.Plugin](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.form.rte.plugins.Plugin)`.
* Les méthodes suivantes définissent l’objet ` [CQ.form.rte.plugins.Plugin](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.form.rte.plugins.Plugin)` et sont remplacées dans le module externe d’implémentation :
   * `getFeatures()` renvoie un tableau de toutes les fonctionnalités rendues disponibles par le module externe.
   * `initializeUI()` ajoute le nouveau bouton à la barre d’outils de l’Éditeur de texte enrichi.
   * `notifyPluginConfig()` affiche le titre et le texte lorsque l’utilisateur survole le bouton avec le pointeur de la souris.
   * `execute()` est appelé lorsque l’utilisateur clique sur le bouton et exécute l’action du module externe : il affiche une fenêtre qui est utilisée pour définir le texte à inclure.
* `insertText()` insère un texte à l’aide de l’objet de boîte de dialogue correspondant `Ejst.InsertTextPlugin.Dialog` (voir plus loin).
* `executeInsertText()` est appelé par la méthode `apply()` de la boîte de dialogue, qui est déclenchée lorsque l’utilisateur clique sur le bouton **OK**.
* S’enregistre lui-même en tant que plug-in « `inserttext` » :
  `CQ.form.rte.plugins.PluginRegistry.register("inserttext", Ejst.InsertTextPlugin);`
* L’objet `Ejst.InsertTextPlugin.Dialog` définit la boîte de dialogue qui s’ouvre lorsque l’utilisateur clique sur le bouton du module externe. La boîte de dialogue comprend un panneau, un formulaire, un champ de texte et deux boutons (**OK** et **Annuler**).

Pour utiliser la boîte de dialogue basée sur le **module externe Éditeur de Texte Enrichi (RTE)**, procédez comme suit :

1. Remplacez la boîte de dialogue du composant **Widgets personnalisés** par la boîte de dialogue basée sur le **module externe Éditeur de Texte Enrichi (RTE)** :
Suivez la procédure décrite pour [Exemple 2 : boîte de dialogue à un seul panneau](#example-single-panel-dialog).
1. Modifiez le composant.
1. Cliquez sur la dernière icône sur la droite (celle qui comporte quatre flèches). Saisissez un chemin d’accès et cliquez ensuite sur **OK** :
Le chemin d’accès est affiché entre crochets ([ ]).
1. Cliquez sur **OK** pour fermer l’éditeur de texte enrichi.

La boîte de dialogue basée sur le **module externe Éditeur de texte enrichi (RTE)** se présente comme suit :

![screen_shot_2012-02-01at120254pm](assets/screen_shot_2012-02-01at120254pm.png)

>[!NOTE]
>
>Cet exemple montre uniquement comment implémenter la partie côté client de la logique : les espaces réservés (*[texte]*) doivent ensuite être analysés explicitement du côté serveur (dans le JSP du composant, par exemple).

### Tree Overview {#tree-overview}

L’objet` [CQ.Ext.tree.TreePanel](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.tree.TreePanel)` prêt à l’emploi représente les données d’interface utilisateur sous la forme d’une arborescence. Le composant Tree Overview inclus dans le package **Utilisation des widgets ExtJS** montre comment utiliser l’objet `TreePanel` pour afficher une arborescence JCR sous un chemin d’accès donné. La fenêtre proprement dite peut être ancrée/détachée. Dans cet exemple, la logique de fenêtre est incorporée dans le fichier JSP du composant entre les balises &lt;script>&lt;/script>.

Pour inclure le composant **Tree Overview** dans l’exemple de page :

1. Ajoutez le composant **4. Tree Overview** à l’exemple de page à partir de l’onglet **Utilisation des widgets ExtJS** dans le **sidekick**.
1. Le composant affiche les éléments suivants :
   * un titre, avec du texte ;
   * un lien **PROPRIÉTÉS** : cliquez sur le lien pour afficher les propriétés du paragraphe stocké dans le référentiel. Cliquez à nouveau pour masquer les propriétés.
   * une fenêtre flottante avec une représentation arborescente du référentiel qui peut être développée.

Le composant se présente sous la forme suivante :

![screen_shot_2012-02-01at120639pm](assets/screen_shot_2012-02-01at120639pm.png)

Composant Tree Overview :

* Il est défini à l’emplacement suivant :
  `/apps/extjstraining/components/treeoverview`

* La boîte de dialogue vous permet de définir la taille de la fenêtre et d’ancrer ou de désancrer la fenêtre (voir les détails ci-dessous).

Le jsp du composant :

* Récupère la largeur, la hauteur et les propriétés ancrées du référentiel.
* Affiche du texte sur le format de données de vue d’ensemble de l’arborescence.
* Incorpore la logique de fenêtre dans le jsp du composant entre les balises JavaScript.
* Il est défini à l’emplacement suivant :
  `apps/extjstraining/components/treeoverview/content.jsp`

Le code JavaScript incorporé dans le jsp du composant :

* Définit un objet `tree` en essayant de récupérer une fenêtre d’arborescence de la page.
* Si la fenêtre qui affiche l’arborescence n’existe pas, `treePanel` ([CQ.Ext.tree.TreePanel](https://developer.adobe.com/fr/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.tree.TreePanel)) est créé :
   * `treePanel` contient les données utilisées pour créer la fenêtre.
   * Les données sont récupérées en appelant le servlet enregistré à l’emplacement suivant :
     `/bin/wcm/siteadmin/tree.json`
* Le listener `beforeload` s’assure que le nœud sélectionné est chargé.
* L’objet `root` définit le chemin d’accès `apps/extjstraining` en tant que racine de l’arborescence.
* `tree` (` [CQ.Ext.Window](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.Window)`) est défini sur la base du `treePanel` prédéfini et est affiché avec :
  `tree.show();`
* Si la fenêtre existe déjà, elle est affichée en fonction de la largeur, de la hauteur et des propriétés d’ancrage extraites du référentiel.

Boîte de dialogue du composant :

* Affiche un onglet avec deux champs pour définir la taille (largeur et hauteur) de la fenêtre de vue d’ensemble de l’arborescence et un champ pour ancrer/désancrer la fenêtre.
* Elle est définie par un nœud (type de nœud = `cq:Dialog`, xtype = ` [panel](/help/sites-developing/xtypes.md#panel)`).
* Le panneau comprend un widget sizefield (type de nœud = `cq:Widget`, xtype = ` [sizefield](/help/sites-developing/xtypes.md#sizefield)`) et un widget de sélection (type de nœud = `cq:Widget`, xtype = ` [selection](/help/sites-developing/xtypes.md#selection)`, type = `radio`) avec deux options (true/false).
* Elle est définie par le nœud dialog à l’emplacement suivant :
  `/apps/extjstraining/components/treeoverview/dialog`
* Son rendu est effectué au format json en demandant :
  `https://localhost:4502/apps/extjstraining/components/treeoverview/dialog.-1.json`
* Elle se présente comme suit :

![screen_shot_2012-02-01at120745pm](assets/screen_shot_2012-02-01at120745pm.png)

### Vue d’ensemble de grille {#grid-overview}

Un panneau Grille représente les données sous la forme d’un tableau comprenant des lignes et des colonnes. Il se compose des éléments suivants :

* Magasin : modèle contenant les enregistrements de données (lignes).
* Modèle de colonne : mise en page de colonne.
* Affichage : encapsule l’interface utilisateur.
* Modèle de sélection : comportement de la sélection.

Le composant Grid Overview inclus dans le package **Utilisation des widgets ExtJS** montre comment afficher les données sous la forme d’un tableau :

* L’exemple 1 utilise des données statiques.
* L’exemple 2 utilise les données extraites du référentiel.

Pour inclure le composant Grid Overview dans l’exemple de page :

1. Ajoutez le composant **5. Grid Overview** à l’exemple de page à partir de l’onglet **Utilisation des widgets ExtJS** dans le **sidekick**.
1. Le composant affiche les éléments suivants :
   * Un titre, accompagné de texte
   * un lien **PROPRIÉTÉS** : cliquez sur le lien pour afficher les propriétés du paragraphe stocké dans le référentiel ; Cliquez à nouveau pour masquer les propriétés.
   * une fenêtre flottante contenant des données sous forme de tableau.

Le composant se présente sous la forme suivante :

![screen_shot_2012-02-01at121109pm](assets/screen_shot_2012-02-01at121109pm.png)

#### Exemple 1 : grille par défaut {#example-default-grid}

Dans sa version prête à l’emploi, le composant **Vue d’ensemble de grille** affiche une fenêtre avec des données statiques sous la forme d’un tableau. Dans cet exemple, la logique est incorporée dans le fichier jsp du composant, de deux manières :

* la logique générique est définie entre les balises &lt;script>&lt;/script> ;
* la logique spécifique est disponible dans un fichier .js distinct et est liée au fichier jsp. Cette configuration permet de passer facilement d’une logique à l’autre (statique/dynamique) en commentant les balises &lt;script> souhaitées.

Composant Grid Overview :

* Il est défini à l’emplacement suivant :
  `/apps/extjstraining/components/gridoverview`
* La boîte de dialogue vous permet de définir la taille de la fenêtre et d’ancrer ou de désancrer la fenêtre.

Le jsp du composant :

* Récupère la largeur, la hauteur et les propriétés ancrées du référentiel.
* Affiche du texte en guise d’introduction pour le format de données de vue d’ensemble de grille.
* Fait référence au code JavaScript qui définit l’objet GridPanel :
  `<script type="text/javascript" src="/apps/extjstraining/components/gridoverview/defaultgrid.js"></script>`
  `defaultgrid.js` définit certaines données statiques comme base de l’objet GridPanel.
* Incorpore entre des balises JavaScript, le code JavaScript qui définit l’objet Window utilisant l’objet GridPanel.
* Il est défini à l’emplacement suivant :
  `apps/extjstraining/components/gridoverview/content.jsp`

Le code JavaScript incorporé dans le jsp du composant :

* Définit l’objet `grid` en essayant de récupérer le composant window de la page :
  `var grid = CQ.Ext.getCmp("<%= node.getName() %>-grid");`
* Si `grid` n’existe pas, un objet [CQ.Ext.grid.GridPanel](https://developer.adobe.com/fr/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.grid.GridPanel) ( `gridPanel`) est défini en appelant la méthode `getGridPanel()` (voir ci-après). Cette méthode est définie dans `defaultgrid.js`.
* `grid` est un objet ` [CQ.Ext.Window](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.Window)` basé sur l’objet GridPanel prédéfini et affiché sous la forme : `grid.show();`.
* Si `grid` existe déjà, il est affiché en fonction de la largeur, de la hauteur et des propriétés d’ancrage extraites du référentiel.

Le fichier JavaScript (`defaultgrid.js`) référencé dans le jsp du composant définit la méthode `getGridPanel()` qui est appelée par le script incorporé dans le fichier JSP et renvoie un objet ` [CQ.Ext.grid.GridPanel](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.grid.GridPanel)` sur la base de données statiques. La logique est la suivante :

* `myData` est un tableau de données statiques, composé de cinq colonnes et de quatre lignes.
* `store` est un objet `CQ.Ext.data.Store` qui utilise `myData`.
* `store` est chargé en mémoire :
  `store.load();`
* `gridPanel` est un objet ` [CQ.Ext.grid.GridPanel](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.grid.GridPanel)` qui utilise `store` :
   * Les largeurs de colonnes sont toujours reproportionnées :
     `forceFit: true`
   * Une seule ligne peut être sélectionnée à la fois :
     `singleSelect:true`

#### Exemple 2 : grille de recherche de référence {#example-reference-search-grid}

Lorsque vous installez le package, le fichier `content.jsp` du composant **Grid Overview** affiche une grille sur la base des données statiques. Il est possible de modifier le composant pour afficher une grille avec les caractéristiques suivantes :

* A trois colonnes.
* Est basé sur les données récupérées du référentiel en appelant une servlet.
* Les cellules de la dernière colonne peuvent être modifiées. La valeur est conservée dans une propriété `test` sous le nœud défini par le chemin d’accès qui est affiché dans la première colonne.

Comme indiqué à la section précédente, l’objet window obtient son objet ` [CQ.Ext.grid.GridPanel](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.grid.GridPanel)` en appelant la méthode `getGridPanel()` définie dans le fichier `defaultgrid.js` à l’emplacement suivant : `/apps/extjstraining/components/gridoverview/defaultgrid.js`. Le composant **Grid Overview** fournit une implémentation différente pour la méthode `getGridPanel()` ; elle est définie dans le fichier `referencesearch.js` sous `/apps/extjstraining/components/gridoverview/referencesearch.js`. En changeant le fichier .js qui est référencé dans le jsp du composant, la grille sera basée sur les données extraites du référentiel.

Changez le fichier .js qui est référencé dans le jsp du composant :

1. Dans **CRXDE Lite**, dans le fichier `content.jsp` du composant, mettez en commentaire la ligne qui contient le fichier `defaultgrid.js`, de sorte qu’elle se présente comme suit :
   `<!-- script type="text/javascript" src="/apps/extjstraining/components/gridoverview/defaultgrid.js"></script-->`
1. Supprimez le commentaire de la ligne qui contient le fichier `referencesearch.js` afin qu’elle se présente comme suit :
   `<script type="text/javascript" src="/apps/extjstraining/components/gridoverview/referencesearch.js"></script>`
1. Enregistrez les modifications.
1. Actualisez l’exemple de page.

Le composant se présente sous la forme suivante :

![screen_shot_2012-02-01at121429pm](assets/screen_shot_2012-02-01at121429pm.png)

Le code JavaScript référencé dans le jsp du composant (`referencesearch.js`) définit la méthode `getGridPanel()` qui est appelée par le jsp du composant et renvoie un objet ` [CQ.Ext.grid.GridPanel](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.grid.GridPanel)` sur la base des données qui sont extraites de manière dynamique du référentiel. La logique contenue dans le fichier `referencesearch.js` définit des données dynamiques comme base de l’objet GridPanel :

* `reader` est un objet ` [CQ.Ext.data.JsonReader](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.data.JsonReader)` qui lit la réponse du servlet au format JSON pour trois colonnes.
* `cm` est un objet ` [CQ.Ext.grid.ColumnModel](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.grid.ColumnModel)` pour trois colonnes.
Les cellules de la colonne « Test » peuvent être modifiées, étant donné qu’elles sont définies avec un éditeur :
  `editor: new [CQ.Ext.form.TextField](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.form.TextField)({})`
* Les colonnes peuvent faire l’objet d’un tri :
  `cm.defaultSortable = true;`
* `store` est un objet ` [CQ.Ext.data.GroupingStore](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.data.GroupingStore)` :
   * Il récupère ses données en appelant le servlet enregistré à l’emplacement « `/bin/querybuilder.json` » ; quelques paramètres sont utilisés pour filtrer la requête.
   * Il repose sur l’objet `reader` défini précédemment.
   * Le tableau est trié selon la colonne **jcr:path** dans l’ordre croissant.
* `gridPanel` est un objet ` [CQ.Ext.grid.EditorGridPanel](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.grid.EditorGridPanel)` qui peut être modifié :
   * Il repose sur l’objet `store` prédéfini et sur le modèle de colonne `cm`. 
   * Une seule ligne peut être sélectionnée à la fois :
     `sm: new [CQ.Ext.grid.RowSelectionModel](https://developer.adobe.com/experience-manager/reference-materials/6-5/widgets-api/index.html?class=CQ.Ext.grid.RowSelectionModel)({singleSelect:true})`
   * Le listener `afteredit` vérifie les éléments suivants après la modification d’une cellule de la colonne « **Test** » :
      * La propriété `test` du nœud situé à l’emplacement défini par la colonne « **jcr:path** » est définie dans le référentiel avec la valeur de la cellule.
      * Si l’opération POST est réussie, la valeur est ajoutée à l’objet `store` ; dans le cas contraire, elle est rejetée.
