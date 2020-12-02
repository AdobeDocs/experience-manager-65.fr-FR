---
title: Utilisation de la fonction J’aime
seo-title: Utilisation de la fonction J’aime
description: Ajoute et configuration du composant J’aime
seo-description: Ajoute et configuration du composant J’aime
uuid: 12103ab7-1a1c-49cd-8dad-6c7508b4550e
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: dcde4e03-78ab-4779-96a1-05ac41f14701
translation-type: tm+mt
source-git-commit: c9fa5624a59f4b9a6f970628b03bbd8b7a277a73
workflow-type: tm+mt
source-wordcount: '234'
ht-degree: 6%

---


# Utilisation de l’option J’aime {#using-liking}

Le composant `Liking` est un outil utile qui permet aux utilisateurs d’exprimer une opinion sur un élément de contenu particulier, tel qu’un commentaire dans un forum. Avec le composant `Liking`, les membres sélectionnent l&#39;icône du coeur pour indiquer une opinion positive.

## Ajouter à une page {#adding-liking-to-a-page}

Pour ajouter un composant `Liking` à une page en mode création, utilisez l’explorateur de composants pour localiser

* `Communities / Liking`

et faites-le glisser sur une page, par exemple une position par rapport à la fonction que les utilisateurs peuvent aimer.

Pour obtenir les informations nécessaires, consultez [Community Components Basics](basics.md).

Lorsque les [bibliothèques client requises](essentials-liking.md#essentials-for-client-side) sont incluses, c&#39;est ainsi que le composant `Liking` s&#39;affiche.

![composant d’aimer](assets/liking-component.png)

## Configuration de l’option J’aime {#configuring-liking}

Sélectionnez le composant `Liking` placé auquel accéder et sélectionnez l&#39;icône `Configure` qui ouvre la boîte de dialogue de modification.

![configure-new](assets/configure-new.png)

Sous l&#39;onglet **[!UICONTROL Textes et étiquettes]**, spécifiez les propriétés utilisées pour enregistrer les mentions J&#39;aime.

![configure-like](assets/configure-liking.png)

* **[!UICONTROL Etiquette de réponse positive]**

   (*Obligatoire*) Nom de propriété pour une réponse positive.

* **[!UICONTROL Etiquette de réponse négative]**

   (*Obligatoire*) Nom de propriété pour une réponse négative.

* **[!UICONTROL Nom Tally]**

   (*Obligatoire*) Nom de propriété interne identifiable pour cette instance d&#39;un composant de vote.

## Expérience des visiteurs {#site-visitor-experience}

### Membres {#members}

Les membres peuvent changer de comportement à tout moment.

### Anonyme {#anonymous}

Les mentions &quot;J’aime&quot; anonymes ne sont pas prises en charge. Les visiteurs du site doivent s&#39;inscrire (devenir membre) et se connecter pour participer à aimer.

## Informations supplémentaires {#additional-information}

Pour plus d&#39;informations, consultez la page [Essentials &quot;J&#39;aime&quot;](essentials-liking.md) destinée aux développeurs.
