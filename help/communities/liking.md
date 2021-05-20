---
title: Utilisation de l’option J’aime
seo-title: Utilisation de l’option J’aime
description: Ajout et configuration du composant J’aime
seo-description: Ajout et configuration du composant J’aime
uuid: 12103ab7-1a1c-49cd-8dad-6c7508b4550e
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: dcde4e03-78ab-4779-96a1-05ac41f14701
exl-id: 226fa91c-4a12-4586-b694-1a52fa2ba358
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '234'
ht-degree: 6%

---

# Utilisation de l’option J’aime {#using-liking}

Le composant `Liking` est un outil utile qui permet aux utilisateurs d’exprimer une opinion sur un élément de contenu particulier, comme un commentaire dans un forum. Avec le composant `Liking` , les membres sélectionnent l’icône représentant un coeur pour indiquer une opinion positive.

## Ajout de mentions J’aime à une page {#adding-liking-to-a-page}

Pour ajouter un composant `Liking` à une page en mode création, utilisez l’explorateur de composants pour accéder à :

* `Communities / Liking`

et faites-le glisser sur la page, par exemple à une position relative à la fonction que les utilisateurs peuvent aimer.

Pour plus d’informations, voir [Principes de base des composants des communautés](basics.md).

Lorsque les [bibliothèques côté client requises](essentials-liking.md#essentials-for-client-side) sont incluses, voici comment le composant `Liking` apparaîtra.

![association-component](assets/liking-component.png)

## Configuration de l’option J’aime {#configuring-liking}

Sélectionnez le composant `Liking` inséré pour y accéder et sélectionnez l’icône `Configure` qui ouvre la boîte de dialogue de modification.

![configure-new](assets/configure-new.png)

Sous l’onglet **[!UICONTROL Textes et libellés]** , spécifiez les propriétés utilisées pour enregistrer les mentions &quot;J’aime&quot;.

![configure-liking](assets/configure-liking.png)

* **[!UICONTROL Etiquette de réponse positive]**

   (*Obligatoire*) Nom de propriété d’une réponse positive.

* **[!UICONTROL Etiquette de réponse négative]**

   (*Obligatoire*) Nom de propriété d’une réponse négative.

* **[!UICONTROL Nom Tally]**

   (*Obligatoire*) Nom de propriété interne identifiable pour cette instance d’un composant Vote.

## Expérience des visiteurs {#site-visitor-experience}

### Membres {#members}

Les membres peuvent changer de comportement à tout moment.

### Anonyme {#anonymous}

Les liens anonymes ne sont pas pris en charge. Les visiteurs du site doivent s’inscrire (devenir membres) et se connecter pour participer à l’activité de votre choix.

## Informations supplémentaires {#additional-information}

Pour plus d’informations, reportez-vous à la page [Notions fondamentales sur l’amour](essentials-liking.md) pour les développeurs.
