---
title: Utilisation de la mention J'aime
description: Découvrez comment ajouter et configurer le composant Liaison afin que les utilisateurs et utilisatrices puissent exprimer une opinion sur un élément de contenu particulier, tel qu’un commentaire.
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
exl-id: 226fa91c-4a12-4586-b694-1a52fa2ba358
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '251'
ht-degree: 1%
---
# Utilisation de la mention J&#39;aime {#using-liking}

Le composant `Liking` est un outil utile qui permet aux utilisateurs et aux utilisatrices d’exprimer une opinion sur un élément de contenu particulier, tel qu’un commentaire dans un forum. Avec le composant `Liking`, les membres sélectionnent l&#39;icône de cœur pour indiquer une opinion positive.

## Ajout d’un lien à une page {#adding-liking-to-a-page}

Pour ajouter un composant `Liking` à une page en mode création, utilisez l’explorateur de composants pour localiser .

* `Communities / Liking`

Et faites-le glisser sur une page, par exemple une position relative à la fonction pour que les utilisateurs l’aiment.

Pour plus d’informations, consultez [Principes de base des composants de communautés](basics.md).

Lorsque les [bibliothèques côté client requises](essentials-liking.md#essentials-for-client-side) sont incluses, le composant `Liking` s’affiche de cette manière.

![liking-component](assets/liking-component.png)

## Configuration des préférences {#configuring-liking}

Sélectionnez le composant de `Liking` placé afin de pouvoir accéder à l’icône de `Configure` qui ouvre la boîte de dialogue de modification et de la sélectionner.

![configure-new](assets/configure-new.png)

Sous l’onglet **[!UICONTROL Textes et libellés]**, spécifiez les propriétés utilisées pour enregistrer les mentions J’aime.

![configurer-aimer](assets/configure-liking.png)

* **[!UICONTROL Libellé de réponse positive]**

  (*Obligatoire*) Nom de propriété pour une réponse positive.

* **[!UICONTROL Libellé de réponse négative]**

  (*Obligatoire*) Nom de propriété pour une réponse négative.

* **[!UICONTROL Tally Name]**

  (*Obligatoire*) Nom de propriété interne identifiable pour cette instance d’un composant votant.

## Expérience du visiteur du site {#site-visitor-experience}

### Membres {#members}

Les membres peuvent changer leurs goûts à tout moment.

### Anonyme {#anonymous}

La mention aimé anonyme n’est pas prise en charge. Les visiteurs et visiteuses du site doivent s’inscrire (devenir membre) et se connecter pour participer aux mentions J’aime.

## Informations supplémentaires {#additional-information}

Vous trouverez plus d’informations à ce sujet sur la page [Liking Essentials](essentials-liking.md) destinée aux développeurs et développeuses.
