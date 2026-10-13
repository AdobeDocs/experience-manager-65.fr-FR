---
title: Utilisation du graphique des réseaux sociaux
description: Découvrez comment ajouter un composant Suivant à une page qui permet aux membres connectés de la communauté de suivre des activités ou d’être suivis.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
exl-id: 2cd1436b-3727-4757-b28e-70756be78a4e
solution: Experience Manager
feature: Communities
role: Admin
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
feature_v2:
  - id: b013f126-a97e-52d1-9f79-cb5bbb12114e
    internal-label: Communities
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '199'
ht-degree: 1%
---
# Utilisation du graphique des réseaux sociaux {#using-social-graph}

## Présentation {#introduction}

La capacité d’un membre de la communauté à suivre des [activités](activities.md) et à être suivi est établie par deux volets : `Follow` et `Following`.

Le composant `Follow` doit être associé à une autre ressource. Cette association est déjà établie pour les membres et les fonctionnalités de la communauté.

Le composant `Following` répertorie simplement les membres qui suivent le membre actif ou qui sont suivis par le membre actif. Ce graphique social des relations entre les membres est inclus dans le profil utilisateur établi pour un [site communautaire](overview.md#communitiessites).

## Ajout des éléments suivants à une page {#adding-following-to-a-page}

Si vous souhaitez ajouter un composant `Following` à une page en mode de création, localisez le composant `Communities / Following` et faites-le glisser sur une page où le graphique de réseau social doit apparaître.

Pour plus d’informations, consultez [Principes de base des composants de communautés](basics.md).

Lorsque les [bibliothèques côté client requises](essentials-socialgraph.md#essentials-for-client-side) sont incluses, le composant `Following` s’affiche de la manière suivante :

![suivant](assets/following.png)

## Configuration des éléments suivants {#configuring-following}

Actuellement, il est nécessaire de définir la propriété pour déterminer si le composant affiche la relation `follows` ou la relation `following`.

## Informations supplémentaires {#additional-information}

Pour plus d’informations, consultez la page [Social Graph Essentials](essentials-socialgraph.md) destinée aux développeurs et développeuses.
