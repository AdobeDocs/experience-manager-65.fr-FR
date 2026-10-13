---
title: Créer une page de contenu pour les appareils mobiles
description: Lors de la création pour les appareils mobiles, vous pouvez basculer entre plusieurs émulateurs pour voir ce que la personne utilisatrice finale voit.
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: site-features
exl-id: 9c6c6386-5ffd-4fa6-9aa1-f5b0e31d1046
solution: Experience Manager, Experience Manager Sites
feature: Authoring
role: User,Admin,Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: c45915cf-e157-4af7-a80d-97b905bcb3a5
    internal-label: Experience Manager Sites
feature_v2:
  - id: e2c1b6d3-bb7e-4fe8-8c72-f7b403298e91
    internal-label: Authoring
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '229'
ht-degree: 100%
---
# Création d’une page pour les appareils mobiles{#authoring-a-page-for-mobile-devices}

Lorsque vous créez une page mobile, celle-ci est affichée d’une manière qui émule l’appareil mobile. Lors de la création de la page, vous pouvez basculer entre plusieurs émulateurs pour voir ce que la personne utilisatrice finale voit lorsqu’elle accède à la page.

Les périphériques sont regroupés dans les catégories fonctionnalité, intelligent et tactile selon les capacités des périphériques à effectuer le rendu d’une page. Lorsque la personne utilisatrice finale accède à une page mobile, AEM détecte le périphérique et envoie la représentation qui correspond à son groupe de périphériques.

>[!NOTE]
>
>Pour créer un site mobile en fonction d’un site standard existant, créez une Live Copy du site standard. (Reportez-vous à [Création d’une live copy pour différents canaux](/help/sites-administering/msm-livecopy.md).)
>
>L’équipe de développement d’AEM peut créer de nouveaux groupes d’appareils. (Voir [Création de filtres de groupe d’appareils](/help/sites-developing/groupfilters.md).)

Utilisez la procédure suivante pour créer une page mobile :

1. À partir de la navigation globale, ouvrez la console **Sites**.
1. Ouvrez la page **We.Retail** -> **États-Unis** -> **Anglais**.

1. Basculez en mode **Aperçu**.
1. Basculez vers l’émulateur de votre choix en cliquant sur l’icône du périphérique en haut de la page.
1. Faites glisser et déposez des composants de l’explorateur de composants vers la page.

La page ressemble à ce qui suit :

![mobileipademu](assets/mobileipademu.png)

>[!NOTE]
>
>Les émulateurs sont désactivés lorsqu’une page de l’instance de création est demandée à partir d’un appareil mobile.
