---
title: Accès aux fonctionnalités du périphérique
description: Consultez cette page pour en savoir plus sur la création de composants Adobe Experience Manager (AEM) qui accèdent aux fonctionnalités des périphériques. Le référentiel GitHub PhoneGap Kitchen AEM fournit aux développeurs une application AEM fonctionnelle qui illustre l’utilisation de plusieurs API Cordova de base.
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
exl-id: 385f7924-e8ab-4dcb-83f0-7b81bead3dda
solution: Experience Manager
feature: Mobile
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '171'
ht-degree: 15%

---

# Accès aux fonctionnalités du périphérique{#access-device-features}

>[!NOTE]
>
>Adobe recommande d’utiliser l’éditeur SPA pour les projets nécessitant un rendu côté client, basé sur un framework, pour une application à une seule page (comme React). [En savoir plus](/help/sites-developing/spa-overview.md).

## Création de composants Adobe Experience Manager (AEM) qui accèdent aux fonctions des périphériques {#building-aem-components-that-access-device-features}

La variable [AEM PhoneGap Kitchen Sink](https://github.com/blefebvre/aem-phonegap-kitchen-sink) Le référentiel GitHub fournit aux développeurs une application d’AEM fonctionnelle qui illustre l’utilisation de plusieurs API Cordova principales. Lorsqu’elle est exécutée sur iOS ou Android™ via l’interface de ligne de commande de PhoneGap, l’application s’ouvre sur la page suivante qui comprend un lien vers chaque API d’appareil illustrée :

![chlimage_1-107](assets/chlimage_1-107.png)

Le code source de chacun de ces composants de l’API d’appareil est : [disponible sur GitHub](https://github.com/blefebvre/aem-phonegap-kitchen-sink/tree/master/content/src/main/content/jcr_root/apps/brucelefebvre/kitchen-sink/components).

Pour plus d’informations sur l’utilisation de chaque API, consultez la documentation du module externe Cordova (`https://docs.phonegap.com/en/4.0.0/cordova_plugins_pluginapis.md.html`).

## Les étapes suivantes {#the-next-steps}

Voir [Suivi des performances de l’application avec Adobe Mobile Analytics](/help/mobile/phonegap-intro-to-app-analytics.md).
