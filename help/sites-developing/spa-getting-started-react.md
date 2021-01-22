---
title: Prise en main des SPA dans AEM - Réagir
seo-title: Prise en main des SPA dans AEM - Réagir
description: Cet article présente un exemple de SPA, explique comment cette application est structurée et vous permet de prendre rapidement en main votre propre SPA à l’aide du framework React.
seo-description: Cet article présente un exemple de SPA, explique comment cette application est structurée et vous permet de prendre rapidement en main votre propre SPA à l’aide du framework React.
uuid: 2beca277-a381-4482-99f6-85005d826d06
contentOwner: bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: spa
content-type: reference
discoiquuid: cc1e5c20-cc9c-4222-8a11-ec5a963d4466
docset: aem65
translation-type: tm+mt
source-git-commit: 4c9a0bd73e8d87d3869c6a133f5d1049f8430cd1
workflow-type: tm+mt
source-wordcount: '1203'
ht-degree: 87%

---


# Prise en main des SPA dans AEM - Réagir{#getting-started-with-spas-in-aem-react}

Les applications sur une seule page (SPA) peuvent améliorer considérablement l’expérience des utilisateurs de sites web. Le souhait des développeurs est de pouvoir créer des sites avec des structures SPA. Les auteurs, pour leur part, souhaitent modifier facilement du contenu dans AEM pour un site conçu à l’aide de telles structures.

La fonction de création d’application sur une seule page constitue une solution complète pour la prise en charge de ce type d’application dans AEM. Cet article présente une SPA simplifiée dans le framework React, explique comment cette application est structurée et vous permet de prendre rapidement en main votre propre SPA.

>[!NOTE]
>
>Cet article repose sur le framework React. Pour obtenir le document correspondant au framework Angular, voir [Prise en main des SPA dans AEM – Angular](/help/sites-developing/spa-getting-started-angular.md).

>[!NOTE]
>
>L’éditeur SPA est la solution recommandée pour les projets qui nécessitent un rendu côté client SPA structure (par exemple, Réagir ou Angulaire).

## Présentation {#introduction}

Cet article résume le fonctionnement de base d’une SPA simple et ce que vous devez savoir pour que la vôtre soit opérationnelle.

Pour plus de détails sur le fonctionnement des SPA dans AEM, consultez les documents suivants :

* [Introduction et présentation des SPA](/help/sites-developing/spa-walkthrough.md)
* [Introduction à la création d’une application d’une seule page](/help/sites-developing/spa-overview.md)
* [Plan directeur d’applications sur une sule page (SPA)](/help/sites-developing/spa-blueprint.md)

>[!NOTE]
>
>Pour pouvoir créer du contenu dans une application d’une seule page, il doit être stocké dans AEM et exposé par le modèle de contenu.
>
>Une SPA développée en dehors d’AEM n’est pas modifiable si elle ne respecte pas le contrat de modèle de contenu.

Ce document décrit la structure d’une SPA simplifiée créée à l’aide du framework React et explique son fonctionnement pour que vous puissiez appliquer cette compréhension à votre propre SPA.

## Dépendances, configuration et construction {#dependencies-configuration-and-building}

En plus de la dépendance React attendue, l’exemple de SPA tire parti de bibliothèques supplémentaires pour optimiser la création de la SPA.

### Dépendances {#dependencies}

Le fichier `package.json` définit les exigences du module SPA global. Les dépendances AEM minimales d’une SPA opérationnelle sont répertoriées ici.

```
  "dependencies": {
    "@adobe/aem-react-editable-components": "~1.0.4",
    "@adobe/aem-spa-component-mapping": "~1.0.5",
    "@adobe/aem-spa-page-model-manager": "~1.0.3"
  }
```

Puisque cet exemple est basé sur le framework React, il existe deux dépendances spécifiques à React qui sont obligatoires dans le fichier `package.json` :

```
react
 react-dom
```

`aem-clientlib-generator` est utilisé pour automatiser la création de bibliothèques clientes dans le cadre du processus de construction.

`"aem-clientlib-generator": "^1.4.1",`

Plus de détails à ce sujet sont disponibles [sur GitHub ici](https://github.com/wcm-io-frontend/aem-clientlib-generator).

>[!CAUTION]
>
>La version minimale de `aem-clientlib-generator` requise est 1.4.1.

`aem-clientlib-generator` est configuré dans le fichier `clientlib.config.js`comme suit.

```
module.exports = {
    // default working directory (can be changed per 'cwd' in every asset option)
    context: __dirname,

    // path to the clientlib root folder (output)
    clientLibRoot: "./../content/jcr_root/apps/my-react-app/clientlibs",

    libs: {
        name: "my-react-app",
        allowProxy: true,
        categories: ["my-react-app"],
        embed: ["my-react-app.responsivegrid"],
        jsProcessor: ["min:gcc"],
        serializationFormat: "xml",
        assets: {
            js: [
                "dist/**/*.js"
            ],
            css: [
                "dist/**/*.css"
            ]
        }
    }
};
```

### Génération {#building}

En réalité, la construction de l’application utilise [Webpack](https://webpack.js.org/) pour la transpilation, en plus du aem-clientlib-generator pour la création automatique de la bibliothèque cliente. Par conséquent, la commande de construction est similaire à :

`"build": "webpack && clientlib --verbose"`

Une fois généré, le module peut être chargé dans une instance AEM.

### Archétype de projet AEM{#aem-project-archetype}

Un projet AEM doit tirer parti de l’[archétype de projet AEM](https://docs.adobe.com/content/help/fr-FR/experience-manager-core-components/using/developing/archetype/overview.html), qui prend en charge les projets SPA à l’aide de React ou d’Angular et tire parti du SDK SPA.

## Structure d’application {#application-structure}

Si vous ajoutez les dépendances et que vous construisez votre application comme décrit précédemment, vous disposez d’un module SPA opérationnel que vous pouvez charger dans votre instance AEM.

La section suivante de ce document explique comment une SPA est structurée dans AEM et décrit les fichiers importants qui pilotent l’application et leur interfonctionnement.

Un composant image simplifié est utilisé à titre d’exemple, mais tous les composants de l’application reposent sur le même concept.

### index.js {#index-js}

Le point d’entrée dans la SPA est bien entendu le fichier `index.js` présenté ici de manière simplifiée afin que l’accent porte sur le contenu important.

```
import ReactDOM from 'react-dom';
import App from './App';
import { ModelManager, Constants } from "@adobe/aem-spa-page-model-manager";

...

ModelManager.initialize().then((pageModel) => {
ReactDOM.render(
    <App cqChildren={pageModel[Constants.CHILDREN_PROP]} cqItems={pageModel[Constants.ITEMS_PROP]} cqItemsOrder={pageModel[Constants.ITEMS_ORDER_PROP]} cqPath={ModelManager.rootPath} locationPathname={ window.location.pathname }/>
, document.getElementById('page'));

});
```

La principale finalité de `index.js` est de tirer parti de la fonction `ReactDOM.render` pour déterminer où, dans le DOM, injecter l’application.

Cela est une utilisation standard de cette fonction, non spécifique à cet exemple d’application.

#### Instanciation statique {#static-instantiation}

Lorsque le composant est instancié de manière statique à l’aide du modèle de composant (par exemple, JSX), la valeur doit être transmise du modèle aux propriétés du composant.

### App.js {#app-js}

En effectuant le rendu de l’application, `index.js` appelle `App.js`, présenté ici dans une version simplifiée afin que l’accent porte sur le contenu important.

```
import {Page, withModel } from '@adobe/aem-react-editable-components';

...

class App extends Page {
...
}

export default withModel(App);
```

`App.js` sert principalement à encapsuler les composants racine qui forment l’application. Le point d’entrée d’une application est la page.

### Page.js {#page-js}

En rendant la page, `App.js` appelle `Page.js` répertorié ici dans une version simplifiée.

```
import {Page, MapTo, withComponentMappingContext } from "@adobe/aem-react-editable-components";

...

class AppPage extends Page {
...
}

MapTo('my-react-app/components/structure/page')(withComponentMappingContext(AppPage));
```

Dans cet exemple, la classe `AppPage` étend `Page`, qui contient les méthodes de contenu interne pouvant ensuite être utilisées.

`Page` accède à la représentation JSON du modèle de page et traite le contenu pour encapsuler/décorer chaque élément de la page. De plus amples détails sur la `Page` sont disponibles dans le document [Plan directeur d’applications sur une seule page (SPA)](/help/sites-developing/spa-blueprint.md#main-pars-header-1694932501).

### Image.js {#image-js}

Avec la page rendue, les composants tels que `Image.js` présentés ici peuvent être rendus.

```
import React, {Component} from 'react';
import {MapTo} from '@adobe/aem-react-editable-components';

require('./Image.css');

const ImageEditConfig = {

    emptyLabel: 'Image',

    isEmpty: function() {
        return !this.props || !this.props.src || this.props.src.trim().length < 1;
    }
};

class Image extends Component {

    render() {
        return (<img src={this.props.src}>);
    }
}

MapTo('my-react-app/components/content/image')(Image, ImageEditConfig);
```

Les SPA dans AEM ont comme principale finalité de mapper les composants SPA aux composants AEM et de mettre à jour le composant lorsque le contenu est modifié (et vice versa). Consultez le document [Aperçu de l’éditeur de SPA](/help/sites-developing/spa-overview.md), qui résume ce modèle de communication.

`MapTo('my-react-app/components/content/image')(Image, ImageEditConfig);`

La méthode `MapTo` mappe le composant SPA au composant AEM. Elle prend en charge l’utilisation d’une seule chaîne ou d’une table de chaînes.

`ImageEditConfig` est un objet de configuration qui contribue à activer les fonctionnalités de création d’un composant en fournissant les métadonnées nécessaires à l’éditeur pour générer des espaces réservés.

S’il n’y a pas de contenu, des libellés sont fournis sous forme d’espaces réservés pour représenter le contenu vide.

#### Propriétés transmises dynamiquement {#dynamically-passed-properties}

Les données provenant du modèle sont transmises dynamiquement en tant que propriétés du composant.

## Exportation de contenu modifiable {#exporting-editable-content}

Vous pouvez exporter un composant et le laisser modifiable.

```
import React, { Component } from 'react';
import { MapTo } from '@adobe/aem-react-editable-components';

...

const EditConfig = {...}

class PageClass extends Component {...};

...

export default MapTo('my-react-app/react/components/structure/page')(PageClass, EditConfig);
```

La fonction `MapTo` renvoie un `Component`, qui résulte d’une composition étendant le composant `PageClass` fourni avec les noms de classe et les attributs qui permettent la création. Ce composant peut être exporté pour être instancié ultérieurement dans le balisage de votre application.

Lorsqu’il est exporté à l’aide des fonctions `MapTo` ou `withModel`, le composant `Page` est encapsulé avec un composant `ModelProvider` qui fournit aux composants standard un accès à la dernière version du modèle de page ou à un emplacement précis dans ce modèle de page.

Pour plus d’informations, voir le document [Plan directeur d’applications sur une seule page (SPA)](/help/sites-developing/spa-blueprint.md#main-pars-header-329251743).

>[!NOTE]
>
>Par défaut, vous recevez le modèle complet du composant lorsque vous utilisez la fonction `withModel`.

## Partage d’informations entre les composants SPA {#sharing-information-between-spa-components}

Il est régulièrement nécessaire que les composants d’une application sur une seule page partagent des informations. Il existe plusieurs méthodes recommandées pour cela, énumérées ci-dessous dans un ordre de complexité croissant.

* **Option 1 :** Centralisez la logique et procédez à une diffusion vers les composants nécessaires ; par exemple en utilisant React Context.
* **Option 2 :** Partagez des états de composant en utilisant une bibliothèque d’états telle que Redux.
* **Option 3 :** Tirez parti de la hiérarchie d’objets en personnalisant et en étendant le composant de conteneur.

## Étapes suivantes {#next-steps}

Pour obtenir un guide détaillé sur la création de votre propre SPA, consultez le [Guide de prise en main de l’AEM Éditeur de la SPA - Événements WKND ](https://helpx.adobe.com/fr/experience-manager/kt/sites/using/getting-started-spa-wknd-tutorial-develop.html).

Pour plus d&#39;informations sur la façon de vous organiser pour développer SPA pour AEM voir l&#39;article [Développer un SPA pour l&#39;](/help/sites-developing/spa-architecture.md).

Pour plus d&#39;informations sur le mappage modèle dynamique/composant et comment il fonctionne dans SPA dans AEM, consultez l&#39;article [Modèle dynamique/mappage de composants pour le ](/help/sites-developing/spa-dynamic-model-to-component-mapping.md).

Si vous souhaitez mettre en oeuvre des SPA dans AEM pour un cadre autre que Réagir ou Angular ou tout simplement plonger dans le fonctionnement du SDK SPA pour les , reportez-vous à l&#39;article [Plan directeur du ](/help/sites-developing/spa-blueprint.md).
