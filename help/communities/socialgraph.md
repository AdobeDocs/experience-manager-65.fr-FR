---
title: Utilisation du graphique des réseaux sociaux
seo-title: Utilisation du graphique des réseaux sociaux
description: Ajouter un composant Suivant à une page
seo-description: Ajouter un composant Suivant à une page
uuid: 8be6334b-e6c9-40bc-90a8-750b98419470
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: 0ce57ab1-e4c6-4c38-963d-556eef8757f2
translation-type: tm+mt
source-git-commit: 1429a099288f038510cb0a194fb55632297ef371
workflow-type: tm+mt
source-wordcount: '197'
ht-degree: 26%

---


# Utilisation du graphique des réseaux sociaux {#using-social-graph}

## Présentation {#introduction}

La capacité d&#39;un membre de la communauté de suivre [les activités](activities.md) et d&#39;être suivi est établie en deux volets : `Follow` et `Following`.

Le composant `Follow` doit être associé à une autre ressource, et cette association est déjà établie pour les membres et les caractéristiques de la communauté.

Le composant `Following` liste simplement les membres qui suivent le membre actuel ou qui sont suivis par le membre actuel. Ce graphique social des relations entre les membres est inclus dans le profil d’utilisateur établi pour un [site de communauté](overview.md#communitiessites).

## Ajout d’un composant Abonnement à une page {#adding-following-to-a-page}

Si vous souhaitez ajouter un composant `Following` à une page en mode création, recherchez le composant `Communities / Following` et faites-le glisser sur une page sur laquelle le graphique social doit apparaître.

Pour obtenir les informations nécessaires, consultez [Community Components Basics](basics.md).

Lorsque les [bibliothèques client requises](essentials-socialgraph.md#essentials-for-client-side) sont incluses, c&#39;est ainsi que le composant `Following` apparaîtra :

![détails](assets/following.png)

## Configuration du composant Abonnement {#configuring-following}

Actuellement, il est nécessaire de définir la propriété pour déterminer si le composant affiche la relation `follows` ou la relation `following`.

## Informations supplémentaires {#additional-information}

Pour plus d’informations, reportez-vous à la page [Notions fondamentales sur les graphiques des réseaux sociaux](essentials-socialgraph.md).
