---
title: Utilisation de l’option J’aime
description: Découvrez comment ajouter et configurer le composant J’aime afin que les utilisateurs puissent exprimer une opinion sur un élément de contenu particulier, tel qu’un commentaire.
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
source-wordcount: '247'
ht-degree: 1%

---

# Utilisation de l’option J’aime {#using-liking}

Le composant `Liking` est un outil utile qui permet aux utilisateurs d’exprimer une opinion sur un élément de contenu particulier, comme un commentaire dans un forum. Avec le composant `Liking`, les membres sélectionnent l’icône représentant un coeur pour indiquer une opinion positive.

## Ajout de mentions J’aime à une page {#adding-liking-to-a-page}

Pour ajouter un composant `Liking` à une page en mode création, utilisez l’explorateur de composants pour accéder à :

* `Communities / Liking`

Faites-le glisser sur la page, par exemple à une position relative à la fonction que les utilisateurs peuvent aimer.

Pour plus d’informations, consultez la page [Principes de base des composants Communities](basics.md).

Lorsque les [bibliothèques côté client demandées](essentials-liking.md#essentials-for-client-side) sont incluses, voici comment le composant `Liking` apparaît.

![liking-component](assets/liking-component.png)

## Configuration de l’option J’aime {#configuring-liking}

Sélectionnez le composant `Liking` inséré afin que vous puissiez accéder à l’icône `Configure` qui ouvre la boîte de dialogue de modification.

![configure-new](assets/configure-new.png)

Sous l’onglet **[!UICONTROL Textes et libellés]**, spécifiez les propriétés utilisées pour enregistrer les mentions &quot;J’aime&quot;.

![configure-liking](assets/configure-liking.png)

* **[!UICONTROL Étiquette de réponse positive]**

  (*Obligatoire*) Nom de propriété d’une réponse positive.

* **[!UICONTROL Étiquette de réponse négative]**

  (*Obligatoire*) Nom de propriété d’une réponse négative.

* **[!UICONTROL Nom Tally]**

  (*Obligatoire*) Nom de propriété interne identifiable de cette instance d’un composant Vote.

## Expérience du visiteur du site {#site-visitor-experience}

### Membres {#members}

Les membres peuvent changer leurs goûts à tout moment.

### Anonyme {#anonymous}

Les liens anonymes ne sont pas pris en charge. Les visiteurs du site doivent s’inscrire (devenir membres) et se connecter pour participer à l’activité de votre choix.

## Informations supplémentaires {#additional-information}

Pour plus d’informations, reportez-vous à la page [Notions fondamentales sur la mention J’aime](essentials-liking.md) pour les développeurs.
