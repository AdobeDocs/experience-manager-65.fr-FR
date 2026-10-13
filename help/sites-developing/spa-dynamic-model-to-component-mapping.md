---
title: Mappage du modèle dynamique avec les composants pour les SPA
description: Découvrez comment s’effectue le mappage du modèle dynamique aux composants dans le SDK JavaScript SPA pour Adobe Experience Manager.
contentOwner: bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: spa
content-type: reference
exl-id: 5b2ccac0-bf1d-4f06-8743-7fce6fb68378
solution: Experience Manager, Experience Manager Sites
feature: Developing,SPA Editor
role: Developer
index: false
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: c45915cf-e157-4af7-a80d-97b905bcb3a5
    internal-label: Experience Manager Sites
feature_v2:
  - id: c5d917df-d8bd-5e97-a117-6dde1e9f7103
    internal-label: Developing
  - id: c124fa01-25c5-42ec-adf6-21d1c114058b
    internal-label: Developer tools
subfeature_v2:
  - id: a9f7d31e-bbe1-4475-966a-5f213546fcd9
    internal-label: SPA Editor
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '336'
ht-degree: 100%
---

# Mappage du modèle dynamique aux composants pour les SPA{#dynamic-model-to-component-mapping-for-spas}

Ce document décrit comment s’effectue le mappage dynamique du modèle aux composants dans le SDK JavaScript SPA pour Adobe Experience Manager (AEM).

{{ue-over-spa}}

## Module ComponentMapping {#componentmapping-module}

Le module `ComponentMapping` est fourni au projet front-end sous la forme d’un package NPM. Il contient les composants front-end et permet à l’application sur une seule page (SPA) de mapper les composants front-end avec les types de ressources AEM. Cela permet une résolution dynamique des composants lors de l’analyse du modèle JSON de l’application.

Chaque élément présent dans le modèle contient un champ `:type` qui expose un type de ressource AEM. Une fois monté, le composant front-end peut être rendu à l’aide du fragment de modèle reçu des bibliothèques associées.

Pour plus d’informations sur l’analyse des modèles et l’accès des composants front-end au modèle, consultez le document [Plan directeur SPA](/help/sites-developing/spa-blueprint.md).

Consultez également le package npm : [https://www.npmjs.com/package/@adobe/aem-spa-component-mapping](https://www.npmjs.com/package/@adobe/aem-spa-component-mapping).

## SPA pilotée par un modèle {#model-driven-single-page-application}

Les applications monopages qui utilisent le SDK JavaScript d’application monopage pour AEM sont basées sur des modèles :

1. Les composants front-end s’enregistrent eux-mêmes dans le [magasin de mappage de composants](/help/sites-developing/spa-dynamic-model-to-component-mapping.md#componentmapping-module).
1. Ensuite, le [conteneur](/help/sites-developing/spa-blueprint.md#container), qui a reçu un modèle du [fournisseur de modèles](/help/sites-developing/spa-blueprint.md#the-model-provider), effectue une itération sur son contenu de modèle (`:items`).

1. S’il y a une page, ses enfants (`:children`) obtiennent d’abord une classe de composant du [mappage des composants](/help/sites-developing/spa-blueprint.md#componentmapping), puis l’instancient.

## Initialisation de l’application {#app-initialization}

Chaque composant est étendu grâce aux capacités du [`ModelProvider`](/help/sites-developing/spa-blueprint.md#the-model-provider). L’initialisation se présente donc sous la forme générale suivante :

1. Chaque fournisseur de modèles s’initialise et écoute les modifications apportées au fragment de modèle qui correspond à son composant interne.
1. Le gestionnaire [`PageModelManager`](/help/sites-developing/spa-blueprint.md#pagemodelmanager) doit être initialisé tel qu’il est représenté par le [flux d’initialisation](/help/sites-developing/spa-blueprint.md).

1. Une fois stocké, le gestionnaire de modèles de page renvoie le modèle complet de l’application.
1. Ce modèle est ensuite transmis au composant racine front-end [Conteneur](/help/sites-developing/spa-blueprint.md#container) de l’application.
1. Les fragments du modèle sont finalement propagés à chaque composant enfant.

![app_model_initialization](assets/app_model_initialization.png)
