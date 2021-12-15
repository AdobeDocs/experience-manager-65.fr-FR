---
title: 'Développement sans affichage pour AEM 6.5 Sites '
description: Découvrez comment les puissantes fonctionnalités sans interface d’AEM 6.5 telles que les modèles de contenu, les fragments de contenu et l’API GraphQL fonctionnent ensemble pour vous permettre de gérer vos expériences de manière centralisée et de les diffuser sur plusieurs canaux.
source-git-commit: 2f400d209148278f0695f7b9523b58bba6845cfb
workflow-type: tm+mt
source-wordcount: '493'
ht-degree: 64%

---


# Développement sans affichage pour AEM 6.5 Sites {#headless-development}

Découvrez comment les puissantes fonctionnalités sans interface d’AEM 6.5 telles que les modèles de contenu, les fragments de contenu et l’API GraphQL fonctionnent ensemble pour vous permettre de gérer vos expériences de manière centralisée et de les diffuser sur plusieurs canaux.

## Présentation {#overview}

L’implémentation découplée devient de plus en plus importante pour offrir des expériences à votre public, où qu’il se trouve et quel que soit son canal.

L’implémentation découplée renonce à la gestion des pages et des composants, comme c’est généralement le cas avec les solutions hybrides et complètes, et se concentre sur la création de fragments de contenu réutilisables et neutres du point de vue du canal, ainsi que sur leur diffusion entre canaux. Il s’agit d’un modèle de développement moderne et dynamique pour l’implémentation d’expériences Web.

![Modèles d’implémentation AEM](assets/aem-implementation-models.png)

## Comparaison entre couplage et découplage {#headful-headless}

Ce document se concentre sur le modèle de mise en œuvre entièrement découplée d’AEM. Pour autant, le choix entre couplage et découplage n’est pas nécessairement binaire dans AEM. Vous pouvez utiliser des fonctions découplées afin de gérer et diffuser votre contenu pour différents points d’entrée tout en permettant aux auteurs de contenu de modifier des applications sur une seule page. Le tout dans AEM.

>[!TIP]
>
>Voir le document [Couplage et découplage dans AEM](/help/sites-developing/headful-headless.md) pour plus d’informations.

## AEM 6.5 et sans affichage {#aem-headless}

AEM 6.5 est un outil flexible pour le modèle d’implémentation sans interface utilisateur graphique en offrant trois services puissants :

1. Modèles de contenu
   * Les modèles de contenu sont une représentation structurée du contenu.
   * Ils sont définis par des architectes des informations dans l’éditeur de modèles de fragments de contenu AEM.
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

Un certain nombre de ressources sont disponibles pour que vous puissiez commencer à utiliser les fonctionnalités d’AEM découplé. Elles sont conçues pour différents cas d’utilisation, mais donnent toutes une vue d’ensemble complète des fonctionnalités d’AEM découplé.

| Ressource | Description | Type | Public | Temps estimé |
|---|---|---|---|---|
| [Parcours de développement découplé](/help/journey-headless/developer/overview.md) | **Pour les utilisateurs qui découvrent AEM et qui n’ont pas d’interface utilisateur** pour une présentation complète de l&#39;AEM et de ses fonctionnalités sans tête, depuis la théorie de l&#39;absence de tête jusqu&#39;à la mise en ligne de votre premier projet sans tête. | Guide | Développeurs **nouveau à AEM et sans tête** | 1 heure |
| [Guide de prise en main du mode découplé](/help/sites-developing/headless/getting-started/introduction.md) | **Pour les utilisateurs AEM expérimentés** Si vous avez besoin d’un bref résumé des principales fonctionnalités AEM sans interface utilisateur, consultez cet aperçu de démarrage rapide. | Démarrage rapide | Développeurs, Administrateurs **avec AEM expérience** | 20 minutes |
| [Prise en main avec le tutoriel pratique d’AEM découplé](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/graphql/multi-step/overview.html?lang=fr) | **Si vous préférez une approche pratique et que vous connaissez les AEM**, ce tutoriel aborde directement la création d’un projet simple sans tête. | Tutoriel | Développeurs | 2 heures |
