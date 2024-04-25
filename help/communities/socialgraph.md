---
title: Utilisation de Social Graph
description: Découvrez comment ajouter un composant Suivant à une page qui permet aux membres de la communauté connectés de suivre les activités ou d’être suivis.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
exl-id: 2cd1436b-3727-4757-b28e-70756be78a4e
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '197'
ht-degree: 1%

---

# Utilisation de Social Graph {#using-social-graph}

## Présentation {#introduction}

La possibilité pour un membre de la communauté de suivre [activités](activities.md) et à suivre est établi par le biais de deux composants : `Follow` et `Following`.

La variable `Follow` doit être associé à une autre ressource, et cette association est déjà établie pour les membres et les fonctionnalités de la communauté.

La variable `Following` Le composant liste simplement les membres qui suivent le membre actuel ou qui sont suivis par le membre actuel. Ce graphique social des relations entre les membres est inclus dans le profil utilisateur établi pour une [site communautaire](overview.md#communitiessites).

## Ajout de l’option Suivant à une page {#adding-following-to-a-page}

Si vous souhaitez ajouter une `Following` à une page en mode création, recherchez le composant. `Communities / Following` et faites-le glisser sur la page où le graphique social doit apparaître.

Pour obtenir les informations nécessaires, consultez la section [Principes de base des composants des communautés](basics.md).

Lorsque la variable [bibliothèques côté client requises](essentials-socialgraph.md#essentials-for-client-side) sont incluses, c’est ainsi que la variable `Following` Le composant apparaît :

![following](assets/following.png)

## Configuration suivante {#configuring-following}

Actuellement, il est nécessaire de définir la propriété pour déterminer si le composant affiche la variable `follows` ou la variable `following` relation.

## Informations supplémentaires {#additional-information}

Vous trouverez plus d’informations sur la [Notions fondamentales sur les graphiques sociaux](essentials-socialgraph.md) pour les développeurs.
