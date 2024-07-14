---
title: Utilisation du vote
description: Découvrez comment ajouter le composant Vote à une page qui permet aux membres de la communauté connectés d’évaluer un élément de contenu particulier, tel qu’une réponse.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
exl-id: aa90bf1b-6053-4949-b061-232d72b80682
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '253'
ht-degree: 1%

---

# Utilisation du vote {#using-voting}

Le composant `Voting` est un outil utile qui permet aux membres de la communauté d’évaluer un élément de contenu particulier, comme une réponse dans un composant Q&amp;R. Avec le composant `Voting`, les membres sélectionnent les flèches haut ou bas pour indiquer leur opinion.

## Ajout d’un vote à une page {#adding-voting-to-a-page}

Pour ajouter un composant `Voting` à une page en mode création, utilisez l’explorateur de composants. Recherchez `Communities / Voting` et faites-le glisser sur la page, par exemple à un emplacement relatif à la fonction pour que les utilisateurs puissent voter.

Pour plus d’informations, consultez la page [Principes de base des composants Communities](basics.md).

Lorsque les [bibliothèques côté client demandées](essentials-voting.md#essentials-for-client-side) sont incluses, voici comment le composant `Voting` apparaît.

![voter-component](assets/voting-component.png)

## Configuration du vote {#configuring-voting}

Sélectionnez le composant `Voting` inséré afin que vous puissiez accéder à l’icône `Configure` qui ouvre la boîte de dialogue de modification.

![configure](assets/configure-new.png)

Sous l’onglet **[!UICONTROL Textes et libellés]**, spécifiez les propriétés utilisées pour enregistrer les votes.

![Vote-label](assets/voting-label.png)

* **[!UICONTROL Étiquette de réponse positive]**

  (*Obligatoire*) Nom de propriété interne d’une réponse positive.

* **[!UICONTROL Étiquette de réponse négative]**

  (*Obligatoire*) Nom de propriété interne d’une réponse négative.

* **[!UICONTROL Nom Tally]**

  (*Obligatoire*) Nom de propriété interne identifiable de cette instance d’un composant Vote.

## Expérience du visiteur du site {#site-visitor-experience}

### Membres {#members}

Les membres ne peuvent voter qu&#39;une seule fois, mais peuvent changer leur vote à tout moment.

### Anonyme {#anonymous}

Le vote anonyme n&#39;est pas pris en charge. Les visiteurs du site doivent s’inscrire (devenir membre) et se connecter pour participer une fois au vote.

## Informations supplémentaires {#additional-information}

Vous trouverez plus d’informations sur la page [Notions fondamentales sur le vote](essentials-voting.md) pour les développeurs.
