---
title: Utilisation du composant Vote
seo-title: Utilisation du composant Vote
description: Ajout du composant Vote à une page
seo-description: Ajout du composant Vote à une page
uuid: 56e6cced-2f2d-434a-8fde-92a6c2478a04
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: 071cac6d-05c5-47ab-85bc-ead6693ca1f4
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Utilisation du composant Vote {#using-voting}

The `Voting` component is a useful tool that allows community members to rate a particular piece of content, such as an answer within a QnA component. With the `Voting` component, members select up or down arrows to indicate their opinion.

## Ajout d’un composant Vote à une page {#adding-voting-to-a-page}

Pour ajouter un `Voting` composant à une page en mode d’auteur, utilisez le navigateur de composants pour le localiser `Communities / Voting` et le faire glisser vers son emplacement sur une page, par exemple une position relative à la fonction sur laquelle les utilisateurs peuvent voter.

For necessary information, visit [Communities Components Basics](basics.md).

When the [required client-side libraries](essentials-voting.md#essentials-for-client-side) are included, this is how the `Voting` component will appear.

![chlimage_1-307](assets/chlimage_1-307.png)

## Configuration du composant Vote {#configuring-voting}

Select the placed `Voting` component to access and select the `Configure` icon which opens the edit dialog.

![chlimage_1-308](assets/chlimage_1-308.png)

Under the **[!UICONTROL Texts &amp; Labels]** tab, specify the properties used to record votes.

![chlimage_1-309](assets/chlimage_1-309.png)

* **[!UICONTROL Libellé]** de réponse positive (*Obligatoire*) Nom de propriété interne pour une réponse positive.

* **[!UICONTROL Étiquette]** de réponse négative (*Obligatoire*) Nom de propriété interne pour une réponse négative.

* **[!UICONTROL Nom]** du compte (*Obligatoire*) Nom de propriété interne identifiable pour cette instance d’un composant de vote.

## Expérience des visiteurs {#site-visitor-experience}

### Membres {#members}

Les membres ne peuvent voter qu’une seule fois, mais peuvent changer leur vote à tout moment.

### Anonyme {#anonymous}

Le vote anonyme n’est pas possible. Les visiteurs du site doivent s’enregistrer (devenir membres) et se connecter pour participer au vote.

## Informations supplémentaires {#additional-information}

More information may be found on the [Voting Essentials](essentials-voting.md) page for developers.
