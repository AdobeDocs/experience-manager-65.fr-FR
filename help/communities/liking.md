---
title: Utilisation de l’option J’aime
description: Découvrez comment ajouter et configurer le composant J’aime afin que les utilisateurs puissent exprimer une opinion sur un élément de contenu particulier, tel qu’un commentaire.
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
exl-id: 226fa91c-4a12-4586-b694-1a52fa2ba358
source-git-commit: b8887b4a6f757352e9dbfdf074c10e9ccd6dbd4f
workflow-type: tm+mt
source-wordcount: '247'
ht-degree: 4%

---

# Utilisation de l’option J’aime {#using-liking}

La variable `Liking` component est un outil utile qui permet aux utilisateurs d’exprimer une opinion sur un élément de contenu particulier, comme un commentaire dans un forum. Avec la variable `Liking` , les membres sélectionnent l’icône représentant un coeur pour indiquer une opinion positive.

## Ajout de mentions J’aime à une page {#adding-liking-to-a-page}

Pour ajouter une `Liking` sur une page en mode création, utilisez l’explorateur de composants pour accéder à

* `Communities / Liking`

Faites-le glisser sur la page, par exemple à une position relative à la fonction que les utilisateurs peuvent aimer.

Pour obtenir les informations nécessaires, consultez la section [Principes de base des composants des communautés](basics.md).

Lorsque la variable [bibliothèques côté client requises](essentials-liking.md#essentials-for-client-side) sont incluses, c’est ainsi que la variable `Liking` s’affiche.

![association-component](assets/liking-component.png)

## Configuration de l’option J’aime {#configuring-liking}

Sélectionnez le `Liking` afin que vous puissiez accéder au `Configure` qui ouvre la boîte de dialogue de modification.

![configure-new](assets/configure-new.png)

Sous , **[!UICONTROL Textes et libellés]** , spécifiez les propriétés utilisées pour enregistrer les mentions J’aime.

![configure-liking](assets/configure-liking.png)

* **[!UICONTROL Etiquette de réponse positive]**

  (*Obligatoire*) Nom de propriété d’une réponse positive.

* **[!UICONTROL Etiquette de réponse négative]**

  (*Obligatoire*) Nom de propriété d’une réponse négative.

* **[!UICONTROL Nom Tally]**

  (*Obligatoire*) Nom de propriété interne identifiable de cette instance d’un composant Vote.

## Expérience du visiteur du site {#site-visitor-experience}

### Membres {#members}

Les membres peuvent changer leurs goûts à tout moment.

### Anonyme {#anonymous}

Les liens anonymes ne sont pas pris en charge. Les visiteurs du site doivent s’inscrire (devenir membres) et se connecter pour participer à l’activité de votre choix.

## Informations supplémentaires {#additional-information}

Vous trouverez plus d’informations sur la [Notions fondamentales relatives aux mentions J’aime](essentials-liking.md) pour les développeurs.
