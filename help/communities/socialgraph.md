---
title: Utilisation du graphique des réseaux sociaux
seo-title: Utilisation du graphique des réseaux sociaux
description: ajouter un composant Suivant à une page
seo-description: ajouter un composant Suivant à une page
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

The ability for a community member to follow [activities](activities.md) as well as be followed is established through two components: `Follow` and `Following`.

The `Follow` component must be associated with another resource, and this association is already established for community members and features.

The `Following` component simply lists the members that are either following the current member or are being followed by the current member. Ce graphique social des relations entre les membres est inclus dans le profil d’utilisateur établi pour un [site de communauté](overview.md#communitiessites).

## Ajout d’un composant Abonnement à une page {#adding-following-to-a-page}

Si vous souhaitez ajouter un `Following` composant à une page en mode création, localisez le composant `Communities / Following` et faites-le glisser sur une page sur laquelle le graphique social doit apparaître.

For necessary information, visit [Communities Components Basics](basics.md).

When the [required client-side libraries](essentials-socialgraph.md#essentials-for-client-side) are included, this is how the `Following` component will appear:

![détails](assets/following.png)

## Configuration du composant Abonnement {#configuring-following}

Currently, it is necessary to set the property to determine whether the component displays the `follows` relationship, or the `following` relationship.

## Informations supplémentaires {#additional-information}

Pour plus d’informations, reportez-vous à la page [Notions fondamentales sur les graphiques des réseaux sociaux](essentials-socialgraph.md).
