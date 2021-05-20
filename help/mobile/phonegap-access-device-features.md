---
title: Accès aux fonctionnalités du périphérique
seo-title: Accès aux fonctionnalités du périphérique
description: Consultez cette page pour en savoir plus sur la création AEM composants qui accèdent aux fonctionnalités des périphériques. Le référentiel PhoneGap Kitchen Sink Github AEM fournit aux développeurs une application AEM fonctionnelle qui illustre l’utilisation de plusieurs API Cordova de base.
seo-description: Consultez cette page pour en savoir plus sur la création AEM composants qui accèdent aux fonctionnalités des périphériques. Le référentiel PhoneGap Kitchen Sink Github AEM fournit aux développeurs une application AEM fonctionnelle qui illustre l’utilisation de plusieurs API Cordova de base.
uuid: 1996f017-21d3-4d90-9f55-95c626bc4c60
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
discoiquuid: 0019e367-8edc-4a23-bfa4-5beda266ace6
exl-id: 385f7924-e8ab-4dcb-83f0-7b81bead3dda
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '237'
ht-degree: 10%

---

# Accéder aux fonctionnalités du périphérique{#access-device-features}

>[!NOTE]
>
>Adobe recommande d’utiliser l’éditeur d’application d’une seule page (SPA) pour les projets nécessitant un rendu côté client basé sur la structure SPA (par exemple, React). [En savoir plus](/help/sites-developing/spa-overview.md).

## Création de composants AEM qui accèdent aux fonctionnalités de l’appareil {#building-aem-components-that-access-device-features}

Le [référentiel Github AEM PhoneGap Kitchen Sink](https://github.com/blefebvre/aem-phonegap-kitchen-sink) fournit aux développeurs une application d’AEM fonctionnelle qui illustre l’utilisation de plusieurs API Cordova de base. Lorsqu’elle est exécutée sur iOS ou Android via l’interface de ligne de commande de PhoneGap, l’application s’ouvre sur la page suivante qui comprend un lien vers chaque API d’appareil illustrée :

![chlimage_1-107](assets/chlimage_1-107.png)

Le code source de chacun de ces composants de l’API d’appareil est [disponible sur Github](https://github.com/blefebvre/aem-phonegap-kitchen-sink/tree/master/content/src/main/content/jcr_root/apps/brucelefebvre/kitchen-sink/components).

Pour plus d’informations sur l’utilisation de chaque API, je vous recommande de consulter la [documentation du module externe Cordova](https://docs.phonegap.com/en/4.0.0/cordova_plugins_pluginapis.md.html).

## Étapes suivantes {#the-next-steps}

Voir [Suivi des performances de l’application avec Adobe Mobile Analytics](/help/mobile/phonegap-intro-to-app-analytics.md).
