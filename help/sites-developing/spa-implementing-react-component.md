---
title: Mise en œuvre d’un composant de réaction pour SPA
seo-title: Mise en œuvre d’un composant de réaction pour SPA
description: Cet article présente un exemple d’adaptation d’un composant React simple et existant pour travailler avec l’éditeur SPA d’AEM.
seo-description: Cet article présente un exemple d’adaptation d’un composant React simple et existant pour travailler avec l’éditeur SPA d’AEM.
uuid: ae6a0a6f-0c3c-4820-9b58-c2a85a9f5291
contentOwner: bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: spa
content-type: reference
discoiquuid: 6ed15763-02cc-45d1-adf6-cf9e5e8ebdb0
docset: aem65
exl-id: f4959c12-54c5-403a-9973-7a4ab5f16bed
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '575'
ht-degree: 19%

---

# Mise en œuvre d’un composant de réaction pour SPA{#implementing-a-react-component-for-spa}

Les applications sur une seule page (SPA) peuvent améliorer considérablement l’expérience des utilisateurs de sites web. Le souhait des développeurs est de pouvoir créer des sites avec des structures SPA. Les auteurs, pour leur part, souhaitent modifier facilement du contenu dans AEM pour un site conçu à l’aide de telles structures.

La fonction de création d’application sur une seule page constitue une solution complète pour la prise en charge de ce type d’application dans AEM. Cet article présente un exemple d’adaptation d’un composant React simple et existant pour travailler avec l’éditeur SPA d’AEM.

>[!NOTE]
>
>L’éditeur SPA est la solution recommandée pour les projets qui nécessitent SPA rendu côté client basé sur une structure (par exemple, React ou Angular).

## Présentation {#introduction}

Grâce au contrat simple et léger qui est requis par AEM et établi entre l’SPA et l’éditeur d’Adobe, l’utilisation d’une application JavaScript existante et son adaptation à un  dans l’ est simple.

Cet article illustre l’exemple du composant météorologique sur l’SPA d’exemple We.Retail Journal.

Vous devez connaître la [structure d’une application SPA pour AEM](/help/sites-developing/spa-getting-started-react.md) avant de lire cet article.

>[!CAUTION]
>Ce document utilise [l’application We.Retail Journal](https://github.com/Adobe-Marketing-Cloud/aem-sample-we-retail-journal) à des fins de démonstration uniquement. Ce dernier ne doit pas être utilisé dans le cadre d’un projet.
>
>Tout projet AEM doit exploiter l’[archétype de projet AEM](https://docs.adobe.com/content/help/fr-FR/experience-manager-core-components/using/developing/archetype/overview.html), qui prend en charge les projets SPA à l’aide de React ou d’Angular et exploite le SDK SPA.

## Composant météorologique {#the-weather-component}

Le composant météorologique se trouve dans le coin supérieur gauche de l’application We.Retail Journal. Il affiche la météo actuelle d’un emplacement défini, en extrayant dynamiquement les données météorologiques.

### Utilisation du widget météo {#using-the-weather-widget}

![screen_shot_2018-06-08at143224](assets/screen_shot_2018-06-08at143224.png)

Lors de la création du contenu de la SPA dans l’éditeur de SPA, le composant météorologique apparaît comme tout autre composant d’AEM, avec une barre d’outils, et il est modifiable.

![screen_shot_2018-06-08at143304](assets/screen_shot_2018-06-08at143304.png)

La ville peut être mise à jour dans une boîte de dialogue comme tout autre composant AEM.

![screen_shot_2018-06-08at143446](assets/screen_shot_2018-06-08at143446.png)

La modification est conservée et le composant se met automatiquement à jour avec les nouvelles données météorologiques.

![screen_shot_2018-06-08at143524](assets/screen_shot_2018-06-08at143524.png)

### Implémentation du composant météorologique {#weather-component-implementation}

Le composant météorologique est en fait basé sur un composant React disponible publiquement, appelé [React Open Weather](https://www.npmjs.com/package/react-open-weather), adapté pour fonctionner comme un composant dans l’exemple d’application SPA We.Retail Journal.

Vous trouverez ci-dessous des extraits de la documentation NPM sur l’utilisation du composant React Open Weather.

![screen_shot_2018-06-08at144723](assets/screen_shot_2018-06-08at144723.png) ![screen_shot_2018-06-08at144215](assets/screen_shot_2018-06-08at144215.png)

Vérification du code du composant météorologique personnalisé ( `Weather.js`) dans l’application We.Retail Journal :

* **Ligne 16** : Le widget React Open Weather est chargé selon les besoins.
* **Ligne 46** : La  `MapTo` fonction associe ce composant React à un composant AEM correspondant afin qu’il puisse être modifié dans l’éditeur SPA.

* **Lignes 22 à 29** : Le  `EditConfig` est défini, en vérifiant si la ville a été renseignée et en définissant la valeur si elle est vide.

* **Lignes 31 à 44** : Le composant Météo étend la  `Component` classe et fournit les données requises telles que définies dans la documentation d’utilisation NPM pour le composant React Open Weather et effectue le rendu du composant.

```javascript
/*~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
 ~ Copyright 2018 Adobe Systems Incorporated
 ~
 ~ Licensed under the Apache License, Version 2.0 (the "License");
 ~ you may not use this file except in compliance with the License.
 ~ You may obtain a copy of the License at
 ~
 ~     https://www.apache.org/licenses/LICENSE-2.0
 ~
 ~ Unless required by applicable law or agreed to in writing, software
 ~ distributed under the License is distributed on an "AS IS" BASIS,
 ~ WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
 ~ See the License for the specific language governing permissions and
 ~ limitations under the License.
 ~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~*/
import React, {Component} from 'react';
import ReactWeather from 'react-open-weather';
import {MapTo} from '@adobe/aem-react-editable-components';

require('./Weather.css');

const WeatherEditConfig = {

    emptyLabel: 'Weather',

    isEmpty: function() {
        return !this.props || !this.props.cq_model || !this.props.cq_model.city || this.props.cq_model.city.trim().length < 1;
    }
};

class Weather extends Component {

    render() {
        let apiKey = "12345678901234567890";
        let city;

        if (this.props.cq_model) {
            city = this.props.cq_model.city;
            return <ReactWeather key={'react-weather' + Date.now()} forecast="today" apikey={apiKey} type="city" city={city} />
        }

        return null;
    }
}

MapTo('we-retail-journal/global/components/weather')(Weather, WeatherEditConfig);
```

Bien qu’un composant principal doive déjà exister, le développeur front-end peut exploiter le composant React Open Weather dans le SPA We.Retail Journal avec très peu de codage.

## Étape suivante {#next-step}

Pour plus d’informations sur le développement de SPA pour AEM, voir l’article [Développement d’un projet d’SPA pour l’](/help/sites-developing/spa-architecture.md).
