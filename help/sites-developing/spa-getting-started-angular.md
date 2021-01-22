---
title: Prise en main des SPA en AEM - Angular
seo-title: Prise en main des SPA en AEM - Angular
description: Cet article présente un exemple de SPA, explique comment cette application est structurée et vous permet de prendre rapidement en main votre propre SPA à l’aide du framework Angular.
seo-description: Cet article présente un exemple de SPA, explique comment cette application est structurée et vous permet de prendre rapidement en main votre propre SPA à l’aide du framework Angular.
uuid: d3d2fa63-68c8-4a48-8c8d-045f4f8db937
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: spa
content-type: reference
discoiquuid: 9cdd7648-d67e-414d-aedf-a5687da39326
docset: aem65
translation-type: tm+mt
source-git-commit: 4c9a0bd73e8d87d3869c6a133f5d1049f8430cd1
workflow-type: tm+mt
source-wordcount: '1053'
ht-degree: 84%

---


# Prise en main des SPA en AEM - Angular{#getting-started-with-spas-in-aem-angular}

Les applications sur une seule page (SPA) peuvent améliorer considérablement l’expérience des utilisateurs de sites web. Le souhait des développeurs est de pouvoir créer des sites avec des structures SPA. Les auteurs, pour leur part, souhaitent modifier facilement du contenu dans AEM pour un site conçu à l’aide de telles structures.

La fonction de création d’application sur une seule page constitue une solution complète pour la prise en charge de ce type d’application dans AEM. Cet article présente une SPA simplifiée dans le framework Angular, explique comment cette application est structurée et vous permet de prendre rapidement en main votre propre SPA.

>[!NOTE]
>
>Cet article repose sur le framework Angular. Pour obtenir le document correspondant au framework React, voir [Prise en main des SPA dans AEM – React](/help/sites-developing/spa-getting-started-react.md).

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

Ce document décrit la structure d’une SPA simplifiée et explique son fonctionnement pour que vous puissiez appliquer cette compréhension à votre propre SPA.

## Dépendances, configuration et construction {#dependencies-configuration-and-building}

En plus de la dépendance Angular attendue, l’exemple de SPA tire parti de bibliothèques supplémentaires pour optimiser la création de la SPA.

### Dépendances {#dependencies}

Le fichier `package.json` définit les exigences du module SPA global. Les dépendances AEM minimales requises sont répertoriées ici.

```
"dependencies": {
  "@adobe/aem-angular-editable-components": "~1.0.3",
  "@adobe/aem-spa-component-mapping": "~1.0.5",
  "@adobe/aem-spa-page-model-manager": "~1.0.3"
}
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
    clientLibRoot: "./../content/jcr_root/apps/my-angular-app/clientlibs",

    libs: {
        name: "my-angular-app",
        allowProxy: true,
        categories: ["my-angular-app"],
        embed: ["my-angular-app.responsivegrid"],
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

`"build": "ng build --build-optimizer=false && clientlib",`

Une fois généré, le module peut être chargé dans une instance AEM.

### Archétype de projet AEM{#aem-project-archetype}

Un projet AEM doit tirer parti de l’[archétype de projet AEM](https://docs.adobe.com/content/help/fr-FR/experience-manager-core-components/using/developing/archetype/overview.html), qui prend en charge les projets SPA à l’aide de React ou d’Angular et tire parti du SDK SPA.

## Structure d’application {#application-structure}

Si vous ajoutez les dépendances et que vous construisez votre application comme décrit précédemment, vous disposez d’un module SPA opérationnel que vous pouvez charger dans votre instance AEM.

La section suivante de ce document explique comment une SPA est structurée dans AEM et décrit les fichiers importants qui pilotent l’application et leur interfonctionnement.

Un composant image simplifié est utilisé à titre d’exemple, mais tous les composants de l’application reposent sur le même concept.

### app.module.ts {#app-module-ts}

Le point d’entrée dans la SPA est le fichier `app.module.ts` présenté ici de manière simplifiée afin que l’accent porte sur le contenu important.

```
// app.module.ts
import { BrowserModule, BrowserTransferStateModule } from '@angular/platform-browser';
import { NgModule } from '@angular/core';
import { AppComponent } from './app.component';
import { SpaAngularEditableComponentsModule } from '@adobe/aem-angular-editable-components';
import { AppRoutingModule } from './app-routing.module';

@NgModule({
  imports: [ BrowserModule.withServerTransition({ appId: 'my-angular-app' }),
    SpaAngularEditableComponentsModule,
    AppRoutingModule,
    BrowserTransferStateModule ],
  providers: ...,
  declarations: [ ... ],
  entryComponents: [ ... ],
  bootstrap: [ AppComponent ]
})
export class AppModule {}
```

Le fichier `app.module.ts` constitue le point de départ de l’application, contient la configuration initiale du projet et utilise `AppComponent` pour démarrer l’application.

#### Instanciation statique {#static-instantiation}

Lorsque le composant est instancié de manière statique à l’aide du modèle de composant, la valeur doit être transmise du modèle aux propriétés du composant. Les valeurs du modèle sont transmises en tant qu’attributs pour être disponibles ultérieurement en tant que propriétés de composant.

### app.component.ts {#app-component-ts}

Une fois que `app.module.ts` a amorcé `AppComponent`, il peut ensuite initialiser l’application, qui est présentée ici dans une version simplifiée afin que l’accent porte sur le contenu important.

```
// app.component.ts
import { Component } from '@angular/core';
import { ModelManager } from '@adobe/aem-spa-page-model-manager';
import { Constants } from "@adobe/aem-angular-editable-components";

@Component({
  selector: 'app-root',
  template: `
    <router-outlet></router-outlet>
  `
})

export class AppComponent {
  items;
  itemsOrder;
  path;

  constructor() {
    ModelManager.initialize().then(this.updateData.bind(this));
  }

  private updateData(model) {
    this.path = model[Constants.PATH_PROP];
    this.items = model[Constants.ITEMS_PROP];
    this.itemsOrder = model[Constants.ITEMS_ORDER_PROP];
  }
}
```

### main-content.component.ts {#main-content-component-ts}

En traitant la page, `app.component.ts` appelle `main-content.component.ts` répertorié ici dans une version simplifiée.

```
import { Component } from '@angular/core';
import { ModelManagerService }     from '../model-manager.service';
import { ActivatedRoute } from '@angular/router';
import { Constants } from "@adobe/aem-angular-editable-components";

@Component({
  selector: 'app-main',
  template: `
    <aem-page class="structure-page" [attr.data-cq-page-path]="path" [cqPath]="path" [cqItems]="items" [cqItemsOrder]="itemsOrder" ></aem-page>
  `
})

export class MainContentComponent {
  items;
  itemsOrder;
  path;

  constructor( private route: ActivatedRoute,
    private modelManagerService: ModelManagerService) {
    this.modelManagerService.getData({ path: this.route.snapshot.data.path }).then((data) => {
      this.path = data[Constants.PATH_PROP];
      this.items = data[Constants.ITEMS_PROP];
      this.itemsOrder = data[Constants.ITEMS_ORDER_PROP];
    });
  }
}
```

`MainComponent` accède à la représentation JSON du modèle de page et traite le contenu pour encapsuler/décorer chaque élément de la page. De plus amples détails sur la `Page` sont disponibles dans le document [Plan directeur d’applications sur une seule page (SPA)](/help/sites-developing/spa-blueprint.md#main-pars-header-1694932501).

### image.component.ts {#image-component-ts}

L’élément `Page` est composé de composants. Une fois le fichier JSON ingéré, l’élément `Page` peut traiter ces composants, comme `image.component.ts` illustré ici.

```
/// image.component.ts
import { Component, Input } from '@angular/core';

const ImageEditConfig = {

    emptyLabel: 'Image',

    isEmpty: function(cqModel) {
        return !cqModel || !cqModel.src || cqModel.src.trim().length < 1;
    }
};

@Component({
  selector: 'app-image',
  templateUrl: './image.component.html',
})

export class ImageComponent {
  @Input() src: string;
  @Input() alt: string;
  @Input() title: string;
}

MapTo('my-angular-app/components/image')(ImageComponent, ImageEditConfig);
```

Les SPA dans AEM ont comme principale finalité de mapper les composants SPA aux composants AEM et de mettre à jour le composant lorsque le contenu est modifié (et vice versa). Consultez le document [Aperçu de l’éditeur de SPA](/help/sites-developing/spa-overview.md), qui résume ce modèle de communication.

`MapTo('my-angular-app/components/image')(Image, ImageEditConfig);`

La méthode `MapTo` mappe le composant SPA au composant AEM. Elle prend en charge l’utilisation d’une seule chaîne ou d’une table de chaînes.

`ImageEditConfig` est un objet de configuration qui contribue à activer les fonctionnalités de création d’un composant en fournissant les métadonnées nécessaires à l’éditeur pour générer des espaces réservés.

S’il n’y a pas de contenu, des libellés sont fournis sous forme d’espaces réservés pour représenter le contenu vide.

#### Propriétés transmises dynamiquement {#dynamically-passed-properties}

Les données provenant du modèle sont transmises dynamiquement en tant que propriétés du composant.

### image.component.html {#image-component-html}

Enfin, l’image peut être rendue dans `image.component.html`.

```
// image.component.html
<img [src]="src" [alt]="alt" [title]="title"/>
```

## Partage d’informations entre les composants SPA {#sharing-information-between-spa-components}

Il est régulièrement nécessaire que les composants d’une application sur une seule page partagent des informations. Il existe plusieurs méthodes recommandées pour cela, énumérées ci-dessous dans un ordre de complexité croissant.

* **Option 1 :** centralisez la logique et procédez à une diffusion vers les composants nécessaires ; par exemple, en utilisant une classe util comme solution orientée objet pure.
* **Option 2 :** partagez des états de composant en utilisant une bibliothèque d’états telle que NgRx.
* **Option 3 :** tirez parti de la hiérarchie d’objets en personnalisant et en étendant le composant de conteneur.

## Étapes suivantes {#next-steps}

Pour obtenir un guide détaillé sur la création de votre propre SPA, consultez le [Guide de prise en main de l’AEM Éditeur de la SPA - Événements WKND ](https://helpx.adobe.com/fr/experience-manager/kt/sites/using/getting-started-spa-wknd-tutorial-develop.html).

Pour plus d&#39;informations sur la façon de vous organiser pour développer SPA pour AEM voir l&#39;article [Développer un SPA pour l&#39;](/help/sites-developing/spa-architecture.md).

Pour plus d&#39;informations sur le mappage modèle dynamique/composant et comment il fonctionne dans SPA dans AEM, consultez l&#39;article [Modèle dynamique/mappage de composants pour le ](/help/sites-developing/spa-dynamic-model-to-component-mapping.md).

Si vous souhaitez mettre en oeuvre des SPA dans AEM pour un cadre autre que Réagir ou Angular ou tout simplement plonger dans le fonctionnement du SDK SPA pour les , reportez-vous à l&#39;article [Plan directeur du ](/help/sites-developing/spa-blueprint.md).
