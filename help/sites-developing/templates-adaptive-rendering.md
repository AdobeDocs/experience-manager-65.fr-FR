---
title: Rendu de modèle adaptatif
description: Découvrez le rendu de modèles adaptatifs dans Adobe Experience Manager.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
exl-id: 58cac3b1-b7cd-44b2-b89b-f5ee8811c198
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
source-git-commit: 66db4b0b5106617c534b6e1bf428a3057f2c2708
workflow-type: tm+mt
source-wordcount: '492'
ht-degree: 100%

---

# Rendu de modèle adaptatif{#adaptive-template-rendering}

Le rendu de modèle adaptatif permet de gérer une page avec des variantes. Utile à l’origine pour fournir diverses sorties HTML pour les appareils mobiles (par exemple, le téléphone portable par rapport au smartphone), cette fonctionnalité est utile lorsque des expériences doivent être diffusées sur différents appareils qui ont besoin de balises différentes ou d’une sortie HTML différente.

## Vue d’ensemble {#overview}

Les modèles sont créés autour d’une grille réactive. Les pages créées à partir de ces modèles sont entièrement réactives, s’adaptant automatiquement à la fenêtre de l’appareil du client ou de la cliente. À l’aide de la barre d’outils de l’émulateur dans l’éditeur de pages, les auteurs peuvent cibler des dispositions sur des appareils spécifiques.

Il est également possible de configurer des modèles pour prendre en charge le rendu adaptatif. Lorsque les groupes d’appareils sont correctement configurés, la page est rendue avec un sélecteur différent dans l’URL lors de la sélection d’un appareil en mode émulateur. À l’aide d’un sélecteur, un rendu de page spécifique peut être appelé directement via l’URL.

N’oubliez pas de configurer vos groupes d’appareils :

* Chaque appareil doit appartenir à au moins un groupe d’appareils.
* Un appareil peut se trouver dans plusieurs groupes d’appareils.
* Les appareils pouvant appartenir à plusieurs groupes d’appareils, les sélecteurs peuvent être combinés.
* La combinaison de sélecteurs est évaluée de haut en bas, car ils sont conservés dans le référentiel.

>[!NOTE]
>
>Les appareils du groupe d’appareils **Appareils réactifs n’ont jamais de sélecteur, car les appareils reconnus comme prenant en charge le responsive design sont supposés n’avoir pas besoin d’une disposition adaptative.

## Configuration {#configuration}

Les sélecteurs de rendu adaptatif peuvent être configurés pour les groupes d’appareils existants ou pour des [groupes que vous avez vous-même créés.](/help/sites-developing/mobile.md#device-groups)

Dans cet exemple, vous allez configurer le groupe d’appareils existant **Smartphones** pour avoir un sélecteur de rendu adaptatif dans le modèle **Page d’expérience** dans We.Retail.

1. Modifiez le groupe d’appareils qui nécessite un sélecteur adaptatif dans `http://localhost:4502/miscadmin#/etc/mobile/groups`.

   Définissez l’option **Désactiver l’émulateur** et enregistrez.

   ![chlimage_1-157](assets/chlimage_1-157.png)

1. Le sélecteur est disponible pour **Blackberry®** et **iPhone 4** si le groupe d’appareils **Smartphones** est ajouté au modèle et aux structures de page dans les étapes suivantes.

   ![chlimage_1-158](assets/chlimage_1-158.png)

1. Dans CRXDE Lite, autorisez l’utilisation du groupe d’appareils sur votre modèle en l’ajoutant à la propriété de chaîne à valeurs multiples `cq:deviceGroups` sur la structure de votre modèle.

   `/conf/<your-site>/settings/wcm/templates/<your-template>/structure/jcr:content`

   Par exemple, si nous souhaitons ajouter le groupe d’appareils Smartphones :

   `/conf/we-retail/settings/wcm/templates/experience-page/structure/jcr:content`

   ![chlimage_1-159](assets/chlimage_1-159.png)

1. Dans CRXDE Lite, autorisez l’utilisation du groupe d’appareils sur votre site en l’ajoutant à la propriété de chaîne à valeurs multiples `cq:deviceGroups` sur la structure de votre site.

   `/content/<your-site>/jcr:content`

   Par exemple, pour autoriser le groupe d’appareils **Smartphones** :

   `/content/we-retail/jcr:content`

   ![chlimage_1-160](assets/chlimage_1-160.png)

À présent, lorsque vous utilisez l’[émulateur](/help/sites-authoring/responsive-layout.md#layout-definitions-device-emulation-and-breakpoints) dans l’éditeur de pages (par exemple pour [modifier la disposition](/help/sites-authoring/responsive-layout.md)) et que vous choisissez un appareil du groupe d’appareils configuré, la page est rendue avec un sélecteur dans l’URL.

Dans notre exemple, lorsque vous modifiez une page basée sur le modèle **Page d’expérience** et que vous choisissez iPhone 4 dans l’émulateur, la page est rendue, y compris le sélecteur qui est alors `arctic-surfing-in-lofoten.smart.html` au lieu de `arctic-surfing-in-lofoten.html`.

La page peut également être appelée directement à l’aide de ce sélecteur.

![chlimage_1-161](assets/chlimage_1-161.png)
