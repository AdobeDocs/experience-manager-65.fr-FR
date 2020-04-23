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
translation-type: tm+mt
source-git-commit: e4456e80059479ca874681e20f8546f29ac92597

---


# Utilisation de l’option J’aime {#using-liking}

Le `Liking` composant est un outil utile qui permet aux utilisateurs d’exprimer une opinion sur un élément de contenu particulier, tel qu’un commentaire dans un forum. Avec le `Liking` composant, les membres sélectionnent l’icône en forme de coeur pour indiquer une opinion positive.

## Adding Liking to a Page {#adding-liking-to-a-page}

To add a `Liking` component to a page in author mode, use the component browser to locate:

* `Communities / Liking`

et faites-le glisser sur une page, par exemple une position relative à la fonction que les utilisateurs peuvent aimer.

For necessary information, visit [Communities Components Basics](basics.md).

When the [required client-side libraries](essentials-liking.md#essentials-for-client-side) are included, this is how the `Liking` component will appear.

![chlimage_1-93](assets/chlimage_1-93.png)

## Configuration des mentions J’aime {#configuring-liking}

Select the placed `Liking` component to access and select the `Configure` icon which opens the edit dialog.

![chlimage_1-94](assets/chlimage_1-94.png)

Under the **[!UICONTROL Texts &amp; Labels]** tab, specify the properties used to record likes.

![chlimage_1-95](assets/chlimage_1-95.png)

* **[!UICONTROL Etiquette de réponse positive]**

   (*Obligatoire*) Nom de propriété pour une réponse positive.

* **[!UICONTROL Etiquette de réponse négative]**

   (*Obligatoire*) Nom de propriété pour une réponse négative.

* **[!UICONTROL Nom Tally]**

   (*Required*) The internal, identifiable property name for this instance of a voting component.

## Expérience des visiteurs {#site-visitor-experience}

### Membres {#members}

Les membres peuvent changer de comportement à tout moment.

### Anonyme {#anonymous}

Les mentions &quot;J’aime&quot; anonymes ne sont pas prises en charge. Les du site doivent s&#39;inscrire (devenir membre) et se connecter pour participer à aimer.

## Informations supplémentaires {#additional-information}

More information may be found on the [Liking Essentials](essentials-liking.md) page for developers.
