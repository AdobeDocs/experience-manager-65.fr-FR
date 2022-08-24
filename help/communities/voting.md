---
title: Utilisation du composant Vote
seo-title: Using Voting
description: Ajout du composant Vote à une page
seo-description: Adding the Voting component to a page
uuid: 56e6cced-2f2d-434a-8fde-92a6c2478a04
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: 071cac6d-05c5-47ab-85bc-ead6693ca1f4
exl-id: aa90bf1b-6053-4949-b061-232d72b80682
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '235'
ht-degree: 25%

---

# Utilisation du composant Vote {#using-voting}

Le `Voting` est un outil utile qui permet aux membres de la communauté d’évaluer un élément de contenu particulier, tel qu’une réponse dans un composant Q&amp;R. Avec le `Voting` , les membres sélectionnent les flèches haut ou bas pour indiquer leur opinion.

## Ajout d’un composant Vote à une page {#adding-voting-to-a-page}

Pour ajouter une `Voting` sur une page en mode création, utilisez l’explorateur de composants pour accéder à `Communities / Voting` et faites-le glisser sur la page, par exemple à un emplacement relatif à la fonction sur laquelle les utilisateurs peuvent voter.

Pour obtenir les informations nécessaires, consultez la section [Principes de base des composants des communautés](basics.md).

Lorsque la variable [bibliothèques côté client requises](essentials-voting.md#essentials-for-client-side) sont incluses, c’est ainsi que la variable `Voting` s’affiche.

![composant de vote](assets/voting-component.png)

## Configuration du composant Vote {#configuring-voting}

Sélectionnez le `Voting` pour accéder au composant et le sélectionner. `Configure` qui ouvre la boîte de dialogue de modification.

![configure](assets/configure-new.png)

Sous , **[!UICONTROL Textes et libellés]** , spécifiez les propriétés utilisées pour enregistrer les votes.

![libellé de vote](assets/voting-label.png)

* **[!UICONTROL Etiquette de réponse positive]**

   (*Obligatoire*) Nom de propriété interne d’une réponse positive.

* **[!UICONTROL Etiquette de réponse négative]**

   (*Obligatoire*) Nom de propriété interne d’une réponse négative.

* **[!UICONTROL Nom Tally]**

   (*Obligatoire*) Nom de propriété interne identifiable de cette instance d’un composant Vote.

## Expérience des visiteurs {#site-visitor-experience}

### Membres {#members}

Les membres ne peuvent voter qu’une seule fois, mais peuvent changer leur vote à tout moment.

### Anonyme {#anonymous}

Le vote anonyme n’est pas possible. Les visiteurs du site doivent s’enregistrer (devenir membres) et se connecter pour participer au vote.

## Informations supplémentaires {#additional-information}

Vous trouverez plus d’informations sur la [Notions fondamentales sur le vote](essentials-voting.md) pour les développeurs.
