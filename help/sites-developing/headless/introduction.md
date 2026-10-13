---
title: Développement découplé pour AEM 6.5 Sites
description: Découvrez comment les puissantes fonctionnalités d’AEM 6.5, telles que les modèles de contenu, les fragments de contenu et l’API GraphQL, fonctionnent ensemble pour vous permettre de gérer vos expériences de manière centralisée et de les diffuser sur l’ensemble des canaux.
exl-id: b6598bcf-b2ce-403a-87cf-6895fec8a91b
solution: Experience Manager, Experience Manager Sites
feature: Headless,Content Fragments,GraphQL,Persisted Queries,Developing
role: Admin,Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: c45915cf-e157-4af7-a80d-97b905bcb3a5
    internal-label: Experience Manager Sites
feature_v2:
  - id: bfd4bc52-c397-5127-8f86-8953ba9fc0a3
    internal-label: Headless
  - id: c5d917df-d8bd-5e97-a117-6dde1e9f7103
    internal-label: Developing
  - id: a642c50e-80eb-4fc1-a5d2-f3762d1f841d
    internal-label: Administration
  - id: d429a63e-ade4-4117-b04e-9b996d1c94ef
    internal-label: Integrations
  - id: c124fa01-25c5-42ec-adf6-21d1c114058b
    internal-label: Developer tools
subfeature_v2:
  - id: e9db7c79-8f65-4281-a439-c9049296d903
    internal-label: Content Fragments
  - id: a02b73a7-bdfc-4225-bdfd-69f7891ab55e
    internal-label: GraphQL
  - id: d781bc8f-52af-43f6-84d0-b73e59a130d5
    internal-label: Persisted queries
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '544'
ht-degree: 100%
---
# Développement découplé pour AEM 6.5 Sites {#headless-development}

Découvrez comment les puissantes fonctionnalités d’AEM 6.5, telles que les modèles de contenu, les fragments de contenu et l’API GraphQL, fonctionnent ensemble pour vous permettre de gérer vos expériences de manière centralisée et de les diffuser sur l’ensemble des canaux.

## Présentation {#overview}

La mise en œuvre découplée devient de plus en plus importante pour offrir des expériences à votre audience, où qu’elle se trouve et quel que soit son canal.

La mise en œuvre découplée renonce à la gestion des pages et des composants, comme c’est généralement le cas avec les solutions hybrides et complètes, et se concentre sur la création de fragments de contenu réutilisables et neutres du point de vue du canal, ainsi que sur leur diffusion cross-canal. Il s’agit d’un modèle de développement moderne et dynamique pour l’implémentation d’expériences Web.

![Modèles d’implémentation AEM](/help/sites-developing/headless/getting-started/assets/aem-implementation-models.png)

## Comparaison entre couplage et découplage {#headful-headless}

Ce document se concentre sur le modèle de mise en œuvre entièrement découplée d’AEM. Pour autant, le choix entre couplage et découplage n’est pas nécessairement binaire dans AEM. Vous pouvez utiliser des fonctions découplées afin de gérer et diffuser votre contenu pour différents points d’entrée tout en permettant aux auteurs de contenu de modifier des applications sur une seule page. Le tout dans AEM.

>[!TIP]
>
>Voir le document [Couplage et découplage dans AEM](/help/sites-developing/headful-headless.md) pour plus d’informations.

## AEM 6.5 et le mode découplé {#aem-headless}

AEM 6.5 est un outil flexible pour le modèle de mise en œuvre découplée qui offre trois services puissants :

1. Modèles de contenu
   * Les modèles de contenu sont une représentation structurée du contenu.
   * Ils sont définis par des architectes de l’information dans l’éditeur de modèles de fragments de contenu AEM.
   * Les modèles de contenu servent de base aux fragments de contenu.
1. Fragments de contenu
   * Les fragments de contenu sont des instanciations de modèles de contenu.
   * Ils sont créés par les auteurs de contenu à l’aide de l’éditeur de fragments de contenu d’AEM.
   * Ils sont stockés dans AEM Assets et gérés dans l’interface utilisateur d’administration d’Assets.
1. API de contenu pour la diffusion
   * L’API AEM GraphQL prend en charge la diffusion de fragments de contenu.
   * L’API REST AEM Assets prend en charge les opérations CRUD sur les fragments de contenu.
   * La diffusion directe de contenu est également possible avec l’[exportation JSON du composant principal de fragment de contenu.](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/components/content-fragment-component.html?lang=fr)

## Vos premiers pas avec AEM découplé {#first-steps}

Plusieurs ressources sont disponibles pour que vous commenciez à utiliser les fonctionnalités découplées d’AEM. Elles sont conçues pour différents cas d’utilisation, mais donnent toutes une vue d’ensemble complète des fonctionnalités découplées d’AEM.

| Ressource | Description | Type | Audience | Temps estimé |
|---|---|---|---|---|
| [Parcours de développement découplé](/help/journey-headless/developer/overview.md) | **En tant qu’utilisateurs peu familiers avec AEM et avec les technologies découplées**, faites vos premiers pas avec cette présentation complète d’AEM et de ses fonctionnalités découplées, des bases du découplage à la mise en ligne de votre premier projet découplé. | Guide | Développeurs **débutants avec AEM et le découplage** | 1 heure |
| [Guide de prise en main du mode découplé](/help/sites-developing/headless/getting-started/introduction.md) | **Si vous avez une bonne connaissance d’AEM** et souhaitez un aperçu rapide des principales fonctionnalités d’AEM découplé, consultez cet aperçu de démarrage rapide. | Démarrage rapide | Développeurs, Administrateurs **avec une expérience d’AEM** | 20 minutes |
| [Prise en main avec le tutoriel pratique d’AEM découplé](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/graphql/multi-step/overview.html?lang=fr) | **Si vous préférez une approche pratique et êtes déjà familier avec AEM**, ce tutoriel aborde directement la création d’un projet simple en mode découplé. | Tutoriel | Développeurs | 2 heures |
| [Portail de développement d’AEM](https://experienceleague.adobe.com/landing/experience-manager/headless/developer.html?lang=fr) | Cette collection de ressources est fournie pour les développeurs et développeuses de niveau **débutant** et **expérimenté**. | Collection de ressources | Développeurs et développeuses | |
