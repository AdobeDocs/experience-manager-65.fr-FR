---
title: Guide de prise en main du mode découplé
description: Grâce à ce guide de démarrage rapide, découvrez les fondamentaux des puissantes fonctionnalités d’Adobe Experience Manager (AEM) 6.5 en mode découplé comme les modèles de contenu, les fragments de contenu et l’API GraphQL.
exl-id: 55ebd893-b3cc-47c5-ad84-46df984197fb
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
source-wordcount: '304'
ht-degree: 100%
---
# Guide de prise en main du mode découplé {#introduction}

Les guides de prise en main du mode découplé présentent une méthode simple pour créer, gérer et diffuser des expériences à l’aide d’Adobe Experience Manager (AEM) 6.5 en cinq étapes pour les utilisateurs et utilisatrices qui connaissent déjà AEM et la technologie découplée. Chaque guide s’appuie sur le précédent ; il est donc recommandé de les étudier en détail et dans l’ordre.

1. [Création d’une configuration](create-configuration.md)
1. [Création d’un modèle de fragment de contenu](create-content-model.md)
1. [Création d’un dossier Ressources](create-assets-folder.md)
1. [Création d’un fragment de contenu](create-content-fragment.md)
1. [Accès aux fragments de contenu et leur diffusion](create-api-request.md)

>[!TIP]
>
>Ce guide de prise en main s’appuie sur des connaissances préalables concernant AEM et les technologies découplées.
>
>Si vous découvrez AEM ou le découplage, reportez-vous à nos [parcours de documentation sur le découplage](/help/journey-headless/overview.md) pour une introduction de bout en bout au mode découplé et à la manière dont AEM le prend en charge.

## Audience {#audience}

Les tâches décrites dans les Guides de prise en main du découplage sont nécessaires pour une démonstration de base de bout en bout des capacités de découplage d’AEM. Toute personne disposant d’un accès d’administration à une instance AEM de test peut suivre ces guides pour comprendre la diffusion découplée dans AEM, même si une personne avec une expérience de développement est idéale.

Cependant, dans une situation de production, les tâches seront généralement exécutées par des personnes différentes un nombre variable de fois. Par exemple :

* Les **personnes administratrices** ne doivent normalement définir la configuration initiale et la structure des dossiers pour le contenu qu’une seule fois ou de manière sporadique.
* Les **architectes de l’information** ajoutent généralement de nouveaux modèles au fur et à mesure que les besoins de l’organisation évoluent.
* Les **auteurs et autrices de contenu** créent continuellement des contenus en tant que fragments de contenu sur la base des modèles définis par les architectes.

Les guides de prise en main du découplage indiquent qui effectuerait généralement les tâches décrites et à quelle fréquence.

## Étape suivante {#next-step}

Vous souhaitez en apprendre plus ? Alors commencez par lire la première partie du Guide de prise en main du découplage : [Création d’une configuration](create-configuration.md).
