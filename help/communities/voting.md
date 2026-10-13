---
title: Utilisation du vote
description: Découvrez comment ajouter le composant Vote à une page qui permet aux membres de la communauté connectés de noter un élément de contenu particulier, tel qu’une réponse.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
exl-id: aa90bf1b-6053-4949-b061-232d72b80682
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
source-git-commit: 751e1826ed53df7522418e50a206f0fe622256a4
workflow-type: tm+mt
source-wordcount: '257'
ht-degree: 1%
---
# Utilisation du vote {#using-voting}

Le composant `Voting` est un outil utile qui permet aux membres de la communauté d’évaluer un élément de contenu particulier, tel qu’une réponse dans un composant QnA. Avec le composant `Voting`, les membres sélectionnent les flèches vers le haut ou vers le bas pour indiquer leur opinion.

## Ajout d’un vote à une page {#adding-voting-to-a-page}

Pour ajouter un composant `Voting` à une page en mode Création, utilisez l’explorateur de composants. Recherchez `Communities / Voting` et faites-le glisser sur une page, par exemple une position relative à la fonction sur laquelle les utilisateurs pourront voter.

Pour plus d’informations, consultez [Principes de base des composants de communautés](basics.md).

Lorsque les [bibliothèques côté client requises](essentials-voting.md#essentials-for-client-side) sont incluses, le composant `Voting` s’affiche de cette manière.

![vote-composant](assets/voting-component.png)

## Configuration du vote {#configuring-voting}

Sélectionnez le composant de `Voting` placé afin de pouvoir accéder à l’icône de `Configure` qui ouvre la boîte de dialogue de modification et de la sélectionner.

![configurer](assets/configure-new.png)

Sous l’onglet **[!UICONTROL Textes et libellés]**, spécifiez les propriétés utilisées pour enregistrer les votes.

![libellé-vote](assets/voting-label.png)

* **[!UICONTROL Libellé de réponse positive]**

  (*Obligatoire*) Nom de propriété interne d’une réponse positive.

* **[!UICONTROL Libellé de réponse négative]**

  (*Obligatoire*) Nom de propriété interne d’une réponse négative.

* **[!UICONTROL Tally Name]**

  (*Obligatoire*) Nom de propriété interne identifiable pour cette instance d’un composant votant.

## Expérience du visiteur du site {#site-visitor-experience}

### Membres {#members}

Les membres ne peuvent voter qu&#39;une seule fois, mais ils peuvent changer leur vote à tout moment.

### Anonyme {#anonymous}

Le vote anonyme n’est pas pris en charge. Les visiteurs et visiteuses du site doivent s’inscrire (devenir membre) et se connecter pour participer au vote une fois.

## Informations supplémentaires {#additional-information}

Pour plus d’informations, consultez la page [Voting Essentials](essentials-voting.md) destinée aux développeurs et développeuses.
