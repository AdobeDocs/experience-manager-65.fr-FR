---
title: Utilisation des évaluations
description: Découvrez comment ajouter un composant Évaluation à une page qui permet aux membres de la communauté connectés d’exprimer leurs opinions en évaluant le contenu.
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
exl-id: 7534ad5d-b408-4b09-bd3d-da7ab009d55b
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '219'
ht-degree: 1%

---

# Utilisation des évaluations {#using-ratings}

Le composant `Rating` est utilisé de manière autonome ou avec d’autres fonctionnalités de Communities. Ce composant permet aux membres de la communauté connectés d’exprimer leurs opinions en évaluant le contenu.

## Ajout d’une évaluation à une page {#adding-a-rating-to-a-page}

Pour ajouter un composant `Rating` à une page en mode création, recherchez le composant `Communities / Rating` et faites-le glisser sur une page, par exemple une position relative à la fonction que les membres doivent évaluer.

Pour plus d’informations, consultez la page [Principes de base des composants Communities](basics.md).

Lorsque les [bibliothèques côté client demandées](rating-basics.md#essentials-for-client-side) sont incluses, voici comment le composant `Rating` apparaît.

![rating](assets/rating.png)

## Configuration de l’évaluation {#configuring-rating}

Sélectionnez le composant `Rating` inséré afin que vous puissiez accéder à l’icône `Configure` qui ouvre la boîte de dialogue de modification.

![configure-new](assets/configure-new.png)

Sous l’onglet **[!UICONTROL Textes et libellés]**, vous spécifiez l’identifiant interne de l’évaluation.

![tallyname](assets/tallyname.png)

**[!UICONTROL Nom Tally]**
(*Obligatoire*) Un nom simple pour `Rating` qui identifie de manière unique cette instance. Doit être un nom de noeud valide pour le référentiel.

## Expérience du visiteur du site {#site-visitor-experience}

### Membres {#members}

Une seule évaluation par membre est autorisée. Le membre peut modifier sa note à tout moment.

### Anonyme {#anonymous}

La publication anonyme d’une évaluation n’est pas prise en charge. Les visiteurs du site doivent s’inscrire (devenir membres) et se connecter pour participer.

## Informations supplémentaires {#additional-information}

Vous trouverez plus d’informations sur la page [Notions fondamentales sur la notation](rating-basics.md) pour les développeurs.
