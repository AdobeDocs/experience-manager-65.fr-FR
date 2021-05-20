---
title: Utilisation du graphique des réseaux sociaux
seo-title: Utilisation du graphique des réseaux sociaux
description: Ajout d’un composant Suivant à une page
seo-description: Ajout d’un composant Suivant à une page
uuid: 8be6334b-e6c9-40bc-90a8-750b98419470
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: 0ce57ab1-e4c6-4c38-963d-556eef8757f2
exl-id: 2cd1436b-3727-4757-b28e-70756be78a4e
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '197'
ht-degree: 26%

---

# Utilisation du graphique des réseaux sociaux {#using-social-graph}

## Présentation {#introduction}

La possibilité pour un membre de la communauté de suivre les [activités](activities.md) et d’être suivi est établie par deux composants : `Follow` et `Following`.

Le composant `Follow` doit être associé à une autre ressource, et cette association est déjà établie pour les membres et les fonctionnalités de la communauté.

Le composant `Following` répertorie simplement les membres qui suivent le membre actuel ou qui sont suivis par le membre actuel. Ce graphique social des relations entre les membres est inclus dans le profil d’utilisateur établi pour un [site de communauté](overview.md#communitiessites).

## Ajout d’un composant Abonnement à une page {#adding-following-to-a-page}

Si vous souhaitez ajouter un composant `Following` à une page en mode création, recherchez le composant `Communities / Following` et faites-le glisser sur une page où le graphique social doit apparaître.

Pour plus d’informations, voir [Principes de base des composants des communautés](basics.md).

Lorsque les [bibliothèques côté client requises](essentials-socialgraph.md#essentials-for-client-side) sont incluses, voici comment le composant `Following` apparaîtra :

![détails](assets/following.png)

## Configuration du composant Abonnement {#configuring-following}

Actuellement, il est nécessaire de définir la propriété pour déterminer si le composant affiche la relation `follows` ou la relation `following`.

## Informations supplémentaires {#additional-information}

Pour plus d’informations, reportez-vous à la page [Notions fondamentales sur les graphiques des réseaux sociaux](essentials-socialgraph.md).
