---
title: Mise en oeuvre d’un composant de réaction pour l’application d’une seule page
seo-title: Mise en oeuvre d’un composant de réaction pour l’application d’une seule page
description: Cet article présente un exemple d’adaptation d’un composant Réagir simple et existant pour travailler avec l’éditeur d’applications monopages AEM.
seo-description: Cet article présente un exemple d’adaptation d’un composant Réagir simple et existant pour travailler avec l’éditeur d’applications monopages AEM.
uuid: ae6a0a6f-0c3c-4820-9b58-c2a85a9f5291
contentOwner: bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: spa
content-type: reference
discoiquuid: 6ed15763-02cc-45d1-adf6-cf9e5e8ebdb0
docset: aem65
translation-type: tm+mt
source-git-commit: 4c9a0bd73e8d87d3869c6a133f5d1049f8430cd1
workflow-type: tm+mt
source-wordcount: '575'
ht-degree: 11%

---


# Mise en oeuvre d’un composant de réaction pour l’application d’une seule page{#implementing-a-react-component-for-spa}

Les applications d’une seule page (SPA) peuvent améliorer considérablement l’expérience des utilisateurs de sites web. Le souhait des développeurs est de pouvoir créer des sites avec des structures SPA. Les auteurs, pour leur part, souhaitent modifier facilement du contenu dans AEM pour un site conçu à l’aide de telles structures.

La fonction de création d’application d’une seule page constitue une solution complète pour la prise en charge de ce type d’application dans AEM. Cet article présente un exemple d’adaptation d’un composant Réagir simple et existant pour travailler avec l’éditeur d’applications monopages AEM.

>[!NOTE]
>
>L’éditeur d’applications monopages est la solution recommandée pour les projets qui nécessitent un rendu côté client basé sur la structure d’applications monopages (par exemple, Réagir ou Angular).

## Présentation {#introduction}

Grâce au contrat simple et léger requis par AEM et établi entre le SPA et le SPA Editor, prendre une application Javascript existante et l&#39;adapter pour l&#39;utiliser avec un SPA en AEM est une chose simple.

Cet article illustre l&#39;exemple de la composante météorologique de l&#39;exemple d&#39;application d&#39;une seule page d&#39;accueil de Journal We.Retail.

Avant de lire cet article, vous devez connaître la [structure d’une application d’application d’une seule page pour AEM](/help/sites-developing/spa-getting-started-react.md) .

>[!CAUTION]
>Ce document utilise l’application [de Journal](https://github.com/Adobe-Marketing-Cloud/aem-sample-we-retail-journal) We.Retail à des fins de démonstration uniquement. Il ne doit être utilisé pour aucun travail de projet.
>
>Tout projet AEM doit tirer parti de l’archétype [de projet](https://docs.adobe.com/content/help/en/experience-manager-core-components/using/developing/archetype/overview.html)AEM, qui prend en charge les projets d’application d’une seule page à l’aide de React ou d’Angular et qui utilise le SDK d’application d’une seule page.

## La composante météorologique {#the-weather-component}

Le composant météorologique se trouve dans le coin supérieur gauche de l&#39;application de Journal We.Retail. Il affiche la météo actuelle d’un emplacement défini, extrayant dynamiquement les données météorologiques.

### Utilisation du widget météorologique {#using-the-weather-widget}

![screen_shot_2018-06-08at143224](assets/screen_shot_2018-06-08at143224.png)

Lors de la création de contenu de l’application d’une seule page dans l’éditeur d’applications monopages, le composant météorologique apparaît sous la forme de tout autre composant AEM, avec une barre d’outils complète, et il est modifiable.

![screen_shot_2018-06-08at143304](assets/screen_shot_2018-06-08at143304.png)

La ville peut être mise à jour dans une boîte de dialogue comme tout autre composant AEM.

![screen_shot_2018-06-08at143446](assets/screen_shot_2018-06-08at143446.png)

Le changement est persistant et le composant se met automatiquement à jour avec les nouvelles données météorologiques.

![screen_shot_2018-06-08at143524](assets/screen_shot_2018-06-08at143524.png)

### Mise en oeuvre des composants météorologiques {#weather-component-implementation}

Le composant météorologique est en fait basé sur un composant React disponible au public, appelé [React Open Weather](https://www.npmjs.com/package/react-open-weather), qui a été adapté pour fonctionner en tant que composant dans l&#39;exemple d&#39;application SPA du Journal We.Retail.

Voici quelques extraits de la documentation du MNP sur l&#39;utilisation du composant Réagir aux intempéries.

![screen_shot_2018-06-08at144723](assets/screen_shot_2018-06-08at144723.png) ![screen_shot_2018-06-08at144215](assets/screen_shot_2018-06-08at144215.png)

Vérification du code du composant météorologique personnalisé ( `Weather.js`) dans l&#39;application de Journal We.Retail :

* **Ligne 16**: Le widget Réagir au temps ouvert est chargé selon les besoins.
* **Ligne 46**: La `MapTo` fonction associe ce composant Réagir à un composant AEM correspondant afin qu’il puisse être modifié dans l’éditeur d’applications monopages.

* **Lignes 22 à 29**: Le `EditConfig` est défini, en vérifiant si la ville a été peuplée et en définissant la valeur si elle est vide.

* **Lignes 31 à 44**: Le composant Météo étend la `Component` classe et fournit les données requises telles que définies dans la documentation sur l&#39;utilisation du MNP pour le composant Réagir à la météo ouverte et effectue le rendu du composant.

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

Bien qu&#39;un composant principal doive déjà exister, le développeur frontal peut exploiter le composant Réagir aux intempéries dans l&#39;application Web.Retail Journal SPA avec très peu de codage.

## Étape suivante {#next-step}

Pour plus d’informations sur le développement d’applications monopages pour AEM voir l’article [Developing SPAs for AEM](/help/sites-developing/spa-architecture.md).
