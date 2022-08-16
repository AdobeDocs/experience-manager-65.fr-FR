---
title: Création d’une page pour les appareils mobiles
seo-title: Authoring a Page for Mobile Devices
description: Lorsque vous créez une page mobile, celle-ci est affichée d’une manière qui émule l’appareil mobile. Lorsque vous créez une page, vous pouvez basculer entre plusieurs émulateurs pour voir ce que l’utilisateur voit lorsqu’il accède à la page.
seo-description: When authoring a mobile page, the page is displayed in a way that emulates the mobile device. When authoring the page, you can switch between several emulators to see what the end-user sees when accessing the page.
uuid: ca16979d-6e5f-444d-b959-ae92542039b2
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: site-features
discoiquuid: 430a27b5-f344-404f-8bf8-0d91b49b605e
exl-id: d5372474-d8aa-4e64-919d-0bd29ba99d99
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '297'
ht-degree: 91%

---

# Création d’une page pour les appareils mobiles{#authoring-a-page-for-mobile-devices}

Lorsque vous créez une page mobile, celle-ci est affichée d’une manière qui émule l’appareil mobile. Lorsque vous créez une page, vous pouvez basculer entre plusieurs émulateurs pour voir ce que l’utilisateur voit lorsqu’il accède à la page.

Les périphériques sont regroupés en fonction des catégories : fonction, intelligent et tactile, selon les fonctionnalités des périphériques pour effectuer le rendu d’une page. Lorsque l’utilisateur final accède à une page mobile, AEM détecte le périphérique et envoie la représentation qui correspond à son groupe de périphériques.

>[!NOTE]
>
>Pour créer un site mobile en fonction d’un site standard existant, créez une Live Copy du site standard. (Voir [Création d’une Live Copy pour différents canaux](/help/sites-administering/msm-livecopy.md).)
>
>Les développeurs d’AEM peuvent créer de nouveaux groupes d’appareils. (Voir [Création de filtres de groupe d’appareils.](/help/sites-developing/groupfilters.md))

Utilisez la procédure suivante pour créer une page mobile :

1. Dans votre navigateur, accédez à la console **Site Admin**.
1. Ouvrez la page **Products** située sous **Sites Web** >> **Geometrixx Mobile Demo Site** >> **English**.

1. Basculez vers un autre émulateur. Pour ce faire, vous pouvez :

   * cliquer sur l’icône de périphérique situé en haut de la page ;
   * cliquer sur le bouton **Modifier** du **sidekick**, puis sélectionner le périphérique dans le menu déroulant.

1. Faites glisser et déposez le composant **Texte et image** de l’onglet Mobile du sidekick vers la page.
1. Modifiez le composant et ajoutez du texte. Pour enregistrer les modifications, cliquez sur **OK.**

La page ressemble à celle-ci :

![mobileipademu](assets/mobileipademu.png)

>[!NOTE]
>
>Les émulateurs sont désactivés lorsqu’une page de l’instance de création est demandée à partir d’un appareil mobile. Vous pouvez ensuite créer à l’aide de l’interface utilisateur tactile.
