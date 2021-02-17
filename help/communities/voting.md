---
title: Utilisation du composant Vote
seo-title: Utilisation du composant Vote
description: Ajouter le composant Voting à une page
seo-description: Ajouter le composant Voting à une page
uuid: 56e6cced-2f2d-434a-8fde-92a6c2478a04
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: 071cac6d-05c5-47ab-85bc-ead6693ca1f4
translation-type: tm+mt
source-git-commit: c190d5f223c85f6c49fea1391d8a3d2baff20192
workflow-type: tm+mt
source-wordcount: '244'
ht-degree: 25%

---


# Utilisation du composant Vote {#using-voting}

Le composant `Voting` est un outil utile qui permet aux membres de la communauté d’évaluer un élément de contenu particulier, tel qu’une réponse dans un composant QnA. Avec le composant `Voting`, les membres sélectionnent des flèches vers le haut ou vers le bas pour indiquer leur opinion.

## Ajout d’un composant Vote à une page {#adding-voting-to-a-page}

Pour ajouter un composant `Voting` à une page en mode création, utilisez l&#39;explorateur de composants pour localiser `Communities / Voting` et faites-le glisser sur une page, par exemple une position relative à la fonction sur laquelle les utilisateurs peuvent voter.

Pour obtenir les informations nécessaires, consultez [Community Components Basics](basics.md).

Lorsque les [bibliothèques client requises](essentials-voting.md#essentials-for-client-side) sont incluses, c&#39;est ainsi que le composant `Voting` s&#39;affiche.

![composante de vote](assets/voting-component.png)

## Configuration du composant Vote {#configuring-voting}

Sélectionnez le composant `Voting` placé auquel accéder et sélectionnez l&#39;icône `Configure` qui ouvre la boîte de dialogue de modification.

![configurer](assets/configure-new.png)

Sous l&#39;onglet **[!UICONTROL Textes et étiquettes]**, spécifiez les propriétés utilisées pour enregistrer les votes.

![libellé de vote](assets/voting-label.png)

* **[!UICONTROL Etiquette de réponse positive]**

   (*Obligatoire*) Nom de propriété interne pour une réponse positive.

* **[!UICONTROL Etiquette de réponse négative]**

   (*Obligatoire*) Nom de propriété interne pour une réponse négative.

* **[!UICONTROL Nom Tally]**

   (*Obligatoire*) Nom de propriété interne identifiable pour cette instance d&#39;un composant de vote.

## Expérience des visiteurs {#site-visitor-experience}

### Membres {#members}

Les membres ne peuvent voter qu’une seule fois, mais peuvent changer leur vote à tout moment.

### Anonyme {#anonymous}

Le vote anonyme n’est pas possible. Les visiteurs du site doivent s’enregistrer (devenir membres) et se connecter pour participer au vote.

## Informations supplémentaires {#additional-information}

Pour plus d&#39;informations, consultez la page [Voting Essentials](essentials-voting.md) destinée aux développeurs.
