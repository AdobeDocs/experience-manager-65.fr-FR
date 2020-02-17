---
title: Prise en main des applications monopages dans AEM - Angular
seo-title: Prise en main des applications monopages dans AEM - Angular
description: Cet article présente un exemple d’application d’une seule page d’une seule page d’une seule page d’une seule page d’une seule page d’une seule page d’une seule page d’une seule page.
seo-description: Cet article présente un exemple d’application d’une seule page d’une seule page d’une seule page d’une seule page d’une seule page d’une seule page d’une seule page d’une seule page.
uuid: d3d2fa63-68c8-4a48-8c8d-045f4f8db937
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: spa
content-type: reference
discoiquuid: 9cdd7648-d67e-414d-aedf-a5687da39326
docset: aem65
translation-type: tm+mt
source-git-commit: 2dad220d6593ed542816f8a97b0d4b44f0d57876

---


# Getting Started with SPAs in AEM - Angular{#getting-started-with-spas-in-aem-angular}

Les applications d’une seule page (SPA) peuvent améliorer considérablement l’expérience des utilisateurs de sites web. Le souhait des développeurs est de pouvoir créer des sites avec des structures SPA. Les auteurs, pour leur part, souhaitent modifier facilement du contenu dans AEM pour un site conçu à l’aide de telles structures.

La fonction de création d’application d’une seule page constitue une solution complète pour la prise en charge de ce type d’application dans AEM. Cet article présente une application SPA simplifiée sur le framework Angular, explique comment elle est mise en place, ce qui vous permet de vous mettre rapidement en forme avec votre propre SPA.

>[!NOTE]
>
>Cet article est basé sur la structure angulaire. Pour le document correspondant à la structure de réaction, voir [Prise en main des applications monopages dans AEM - Réagir](/help/sites-developing/spa-getting-started-react.md).

>[!NOTE]
>
>L’éditeur d’application d’une seule page est la solution recommandée pour les projets nécessitant un rendu côté client basé sur la structure d’application d’une seule page (par exemple, Réagir ou Angulaire).

## Présentation {#introduction}

Cet article résume le fonctionnement de base d’une application d’une seule page simple et ce que vous devez savoir pour que la vôtre soit opérationnelle.

Pour plus d’informations sur le fonctionnement des applications monopages dans AEM, reportez-vous aux documents suivants :

* [Présentation et présentation des applications monopages](/help/sites-developing/spa-walkthrough.md)
* [Introduction à la création d’une application d’une seule page](/help/sites-developing/spa-overview.md)
* [Plan directeur d’applications sur une seule page (SPA)](/help/sites-developing/spa-blueprint.md)

>[!NOTE]
>
>Pour pouvoir créer du contenu dans une application d’une seule page, il doit être stocké dans AEM et exposé par le modèle de contenu.
>
>Une SPA développée en dehors d’AEM n’est pas modifiable si elle ne respecte pas le contrat de modèle de contenu.

Ce document décrit la structure d’une application d’une seule page d’une application d’une seule page et illustre son fonctionnement afin que vous puissiez l’appliquer à votre propre application d’une telle compréhension.

## Dépendances, configuration et construction {#dependencies-configuration-and-building}

Outre la dépendance angulaire attendue, l’exemple d’application d’une seule page peut tirer parti de bibliothèques supplémentaires pour rendre la création de l’application d’une seule page plus efficace.

### Dépendances {#dependencies}

Le `package.json` fichier définit les exigences du pack d’application d’une seule page. Les dépendances AEM minimales requises sont répertoriées ici.

```
"dependencies": {
  "@adobe/cq-angular-editable-components": "~1.0.3",
  "@adobe/cq-spa-component-mapping": "~1.0.3",
  "@adobe/cq-spa-page-model-manager": "~1.0.4"
}
```

The `aem-clientlib-generator` is leveraged to make the creation of client libraries automatic as part of the build process.

`"aem-clientlib-generator": "^1.4.1",`

Plus de détails à ce sujet sont disponibles [sur GitHub ici](https://github.com/wcm-io-frontend/aem-clientlib-generator).

>[!CAUTION]
>
>La version minimale requise est 1.4.1. `aem-clientlib-generator`

The `aem-clientlib-generator` is configured in the `clientlib.config.js` file as follows.

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

### Construction {#building}

En réalité, la construction de l’application utilise [Webpack](https://webpack.js.org/) pour la transpilation, en plus du aem-clientlib-generator pour la création automatique de la bibliothèque cliente. Par conséquent, la commande de construction est similaire à :

`"build": "ng build --build-optimizer=false && clientlib",`

Une fois construit, le module peut être téléchargé dans une instance AEM.

### Maven Archetype for SPA Starter Kit {#maven-archetype-for-spa-starter-kit}

Adobe recommande de tirer parti du kit [de démarrage](https://github.com/adobe/aem-spa-project-archetype) Maven Archetype for SPA pour vous aider à démarrer votre propre projet SPA pour AEM.

## Structure d’application {#application-structure}

L’inclusion des dépendances et la création de votre application, comme décrit précédemment, vous laisseront avec un package d’application d’une seule page qui fonctionne et que vous pourrez télécharger vers votre instance AEM.

La section suivante de ce document décrit la structure d’une application d’une seule page dans AEM, les fichiers importants qui pilotent l’application et la manière dont elles fonctionnent ensemble.

Un composant d’image simplifié est utilisé comme exemple, mais tous les composants de l’application reposent sur le même concept.

### app.module.ts {#app-module-ts}

The entry point into the SPA is the `app.module.ts` file shown here simplified to focus on the important content.

```
// app.module.ts
import { BrowserModule, BrowserTransferStateModule } from '@angular/platform-browser';
import { NgModule } from '@angular/core';
import { AppComponent } from './app.component';
import { SpaAngularEditableComponentsModule } from '@adobe/cq-angular-editable-components';
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

Le `app.module.ts` fichier est le point de départ de l’application. Il contient la configuration initiale du projet et `AppComponent` sert à amorcer l’application.

#### Instanciation statique {#static-instantiation}

Lorsque le composant est instancié de manière statique à l’aide du modèle de composant, la valeur doit être transmise du modèle aux propriétés du composant. Les valeurs du modèle sont transmises sous forme d’attributs pour être disponibles ultérieurement sous forme de propriétés de composant.

### app.component.ts {#app-component-ts}

Une fois `app.module.ts` amorcé `AppComponent`, il peut initialiser l’application, qui est présentée ici dans une version simplifiée pour se concentrer sur le contenu important.

```
// app.component.ts
import { Component } from '@angular/core';
import { ModelManager } from '@adobe/cq-spa-page-model-manager';
import { Constants } from "@adobe/cq-angular-editable-components";

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

En traitant la page, `app.component.ts` les appels `main-content.component.ts` répertoriés ici dans une version simplifiée.

```
import { Component } from '@angular/core';
import { ModelManagerService }     from '../model-manager.service';
import { ActivatedRoute } from '@angular/router';
import { Constants } from "@adobe/cq-angular-editable-components";

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

`MainComponent` accède à la représentation JSON du modèle de page et traite le contenu pour encapsuler/décorer chaque élément de la page. De plus amples détails sur `Page` sont disponibles dans le document [Plan directeur de SPA](/help/sites-developing/spa-blueprint.md#main-pars-header-1694932501).

### image.component.ts {#image-component-ts}

Le `Page` groupe est composé de composants. Une fois le fichier JSON ingéré, le `Page` système peut traiter ces composants, `image.component.ts` comme illustré ici.

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

Les applications d’une seule page dans AEM ont comme principale finalité de mapper les composants SPA aux composants AEM et de mettre à jour le composant lorsque le contenu est modifié (et vice versa). See the document [SPA Editor Overview](/help/sites-developing/spa-overview.md) for an summary of this communication model.

`MapTo('my-angular-app/components/image')(Image, ImageEditConfig);`

La méthode `MapTo` mappe le composant SPA au composant AEM. Elle prend en charge l’utilisation d’une seule chaîne ou d’une table de chaînes.

`ImageEditConfig` est un objet de configuration qui contribue à activer les fonctionnalités de création d’un composant en fournissant les métadonnées nécessaires à l’éditeur pour générer des espaces réservés.

S’il n’y a pas de contenu, des libellés sont fournis sous forme d’espaces réservés pour représenter le contenu vide.

#### Propriétés transmises dynamiquement {#dynamically-passed-properties}

Les données provenant du modèle sont transmises dynamiquement sous forme de propriétés du composant.

### image.component.html {#image-component-html}

Enfin, l’image peut être rendue dans `image.component.html`.

```
// image.component.html
<img [src]="src" [alt]="alt" [title]="title"/>
```

## Partage d’informations entre les composants SPA {#sharing-information-between-spa-components}

Il est régulièrement nécessaire que les composants d’une application d’une seule page partagent des informations. Il existe plusieurs méthodes recommandées pour ce faire, répertoriées ci-dessous dans un ordre croissant de complexité.

* **** Option 1 : Centralisez la logique et diffusez-la aux composants nécessaires, par exemple en utilisant une classe util comme solution purement orientée objet.
* **** Option 2 : Partagez les états des composants à l’aide d’une bibliothèque d’états telle que NgRx.
* **** Option 3 : Utilisez la hiérarchie d’objets en personnalisant et en étendant le composant conteneur.

## Étapes suivantes {#next-steps}

Pour obtenir un guide détaillé sur la création de votre propre application d’une seule page, consultez le didacticiel [Prise en main de l’éditeur d’applications d’une seule page, intitulé AEM SPA Editor - WKND Events Tutorial](https://helpx.adobe.com/experience-manager/kt/sites/using/getting-started-spa-wknd-tutorial-develop.html)(en anglais).

Pour plus d’informations sur la manière de vous organiser pour développer des applications monopages pour AEM, consultez l’article [Développement d’applications monopages pour AEM](/help/sites-developing/spa-architecture.md).

Pour plus d’informations sur le mappage modèle dynamique/composant et son fonctionnement dans les applications monopages dans AEM, voir l’article Mappage modèle [dynamique/composant pour les applications monopages](/help/sites-developing/spa-dynamic-model-to-component-mapping.md).

Si vous souhaitez mettre en oeuvre des applications monopages dans AEM pour une structure autre que React ou Angular ou simplement plonger dans le fonctionnement du SDK SPA pour AEM, reportez-vous à l’article [SPA Blueprint](/help/sites-developing/spa-blueprint.md) .
