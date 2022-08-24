---
title: Création d’une page pour les appareils mobiles
seo-title: Authoring a Page for Mobile Devices
description: Lors de la création pour les appareils mobiles, vous pouvez basculer entre plusieurs émulateurs pour voir ce que l’utilisateur final voit.
seo-description: When authoring for mobile, you can switch between several emulators to see what the end-user sees
uuid: a7a1ba68-d608-4819-88d1-0dab5955d3f4
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: site-features
discoiquuid: 9554cdb3-b604-4d50-9760-89b9e7a7755f
exl-id: 9c6c6386-5ffd-4fa6-9aa1-f5b0e31d1046
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '225'
ht-degree: 88%

---

# Création d’une page pour les appareils mobiles{#authoring-a-page-for-mobile-devices}

Lorsque vous créez une page mobile, celle-ci est affichée d’une manière qui émule l’appareil mobile. Lorsque vous créez une page, vous pouvez basculer entre plusieurs émulateurs pour voir ce que l’utilisateur voit lorsqu’il accède à la page.

Les périphériques sont regroupés en fonction des catégories : fonction, intelligent et tactile, selon les fonctionnalités des périphériques pour effectuer le rendu d’une page. Lorsque l’utilisateur final accède à une page mobile, AEM détecte le périphérique et envoie la représentation qui correspond à son groupe de périphériques.

>[!NOTE]
>
>Pour créer un site mobile en fonction d’un site standard existant, créez une Live Copy du site standard. (Voir [Création d’une Live Copy pour différents canaux](/help/sites-administering/msm-livecopy.md).)
>
>Les développeurs d’AEM peuvent créer de nouveaux groupes d’appareils. (Voir [Création de filtres de groupe d’appareils](/help/sites-developing/groupfilters.md).)

Utilisez la procédure suivante pour créer une page mobile :

1. À partir de la navigation globale, ouvrez la console **Sites**.
1. Ouvrir la page **We.Retail** -> **États-Unis** -> **Anglais**.

1. Basculer vers **Aperçu** mode .
1. Basculez vers l’émulateur de votre choix en cliquant sur l’icône de périphérique située en haut de la page.
1. Faites glisser les composants à partir du navigateur de composants et déposez-les sur la page.

La page ressemble à ce qui suit :

![mobileipademu](assets/mobileipademu.png)

>[!NOTE]
>
>Les émulateurs sont désactivés lorsqu’une page de l’instance de création est demandée à partir d’un appareil mobile.
