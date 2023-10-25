---
title: Rendu de modèle adaptatif
description: Découvrez le rendu du modèle adaptatif dans Adobe Experience Manager.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
exl-id: 58cac3b1-b7cd-44b2-b89b-f5ee8811c198
source-git-commit: b703f356f9475eeeafb1d5408c650d9c6971a804
workflow-type: tm+mt
source-wordcount: '486'
ht-degree: 16%

---

# Rendu de modèle adaptatif{#adaptive-template-rendering}

Le rendu de modèle adaptatif permet de gérer une page avec des variantes. Utile à l’origine pour fournir diverses sorties de HTML pour les appareils mobiles (par exemple, le téléphone portable par rapport au smartphone), cette fonctionnalité est utile lorsque des expériences doivent être diffusées sur différents appareils qui ont besoin de balises différentes ou d’une sortie de HTML différente.

## Vue d’ensemble {#overview}

Les modèles sont construits autour d’une grille réactive et les pages créées à partir de ces modèles sont entièrement réactives, s’ajustant automatiquement à la fenêtre d’affichage de l’appareil client. À l’aide de la barre d’outils de l’émulateur dans l’éditeur de pages, les auteurs peuvent cibler des dispositions sur des appareils spécifiques.

Il est également possible de configurer des modèles pour prendre en charge le rendu adaptatif. Lorsque les groupes d’appareils sont correctement configurés, la page est générée avec un sélecteur différent dans l’URL lors de la sélection d’un appareil en mode émulateur. A l’aide d’un sélecteur, un rendu de page spécifique peut être appelé directement via l’URL.

N’oubliez pas de configurer vos groupes d’appareils :

* Chaque appareil doit appartenir à au moins un groupe d’appareils.
* Un appareil peut se trouver dans plusieurs groupes d’appareils.
* Les appareils pouvant appartenir à plusieurs groupes d’appareils, les sélecteurs peuvent être combinés.
* La combinaison de sélecteurs est évaluée de haut en bas, car ils sont conservés dans le référentiel.

>[!NOTE]
>
>Le groupe d’appareils **Les appareils réactifs n’ont jamais de sélecteur, car les appareils reconnus comme prenant en charge la conception réactive sont supposés n’avoir pas besoin d’une mise en page adaptative.

## Configuration {#configuration}

Les sélecteurs de rendu adaptatif peuvent être configurés pour les groupes d’appareils existants ou pour [des groupes que vous avez vous-même créés.](/help/sites-developing/mobile.md#device-groups)

Dans cet exemple, vous allez configurer le groupe d’appareils existant. **Smart Phones** pour avoir un sélecteur de rendu adaptatif dans le **Page d’expérience** dans We.Retail.

1. Modifiez le groupe d’appareils qui nécessite un sélecteur adaptatif dans `http://localhost:4502/miscadmin#/etc/mobile/groups`.

   Définissez l’option **Désactiver l’émulateur** et enregistrez.

   ![chlimage_1-157](assets/chlimage_1-157.png)

1. Le sélecteur est disponible pour la **BlackBerry®** et **IPHONE 4** fourni au groupe d’appareils ; **Smart Phone** est ajouté aux structures de modèle et de page dans les étapes suivantes.

   ![chlimage_1-158](assets/chlimage_1-158.png)

1. Avec CRXDE Lite, autorisez l’utilisation du groupe d’appareils sur votre modèle en l’ajoutant à la propriété de chaîne à plusieurs valeurs. `cq:deviceGroups` sur la structure de votre modèle.

   `/conf/<your-site>/settings/wcm/templates/<your-template>/structure/jcr:content`

   Par exemple, si vous souhaitez ajouter le groupe d’appareils Smart Phone :

   `/conf/we-retail/settings/wcm/templates/experience-page/structure/jcr:content`

   ![chlimage_1-159](assets/chlimage_1-159.png)

1. Avec CRXDE Lite, autorisez l’utilisation du groupe d’appareils sur votre site en l’ajoutant à la propriété de chaîne à plusieurs valeurs. `cq:deviceGroups` sur la structure de votre site.

   `/content/<your-site>/jcr:content`

   Par exemple, si vous souhaitez autoriser la variable **Smart Phone** groupe d’appareils :

   `/content/we-retail/jcr:content`

   ![chlimage_1-160](assets/chlimage_1-160.png)

Maintenant, lors de l’utilisation de la variable [émulateur](/help/sites-authoring/responsive-layout.md#layout-definitions-device-emulation-and-breakpoints) dans l’éditeur de page (par exemple, lorsque [modification de la mise en page](/help/sites-authoring/responsive-layout.md)) et que vous choisissez un appareil du groupe d’appareils configuré, la page est rendue avec un sélecteur dans l’URL.

Dans cet exemple, lors de la modification d’une page en fonction de la variable **Page d’expérience** et en choisissant iPhone 4 dans l’émulateur, la page est rendue, y compris le sélecteur comme `arctic-surfing-in-lofoten.smart.html` au lieu de `arctic-surfing-in-lofoten.html`

La page peut également être appelée directement à l’aide de ce sélecteur.

![chlimage_1-161](assets/chlimage_1-161.png)
