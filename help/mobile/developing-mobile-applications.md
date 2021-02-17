---
title: Développement d’applications mobiles dans AEM
seo-title: Développement d’applications mobiles dans AEM
description: Suivez cette page pour début de développement d'applications mobiles dans AEM à l'aide de Adobe PhoneGap Enterprise.
seo-description: Suivez cette page pour début de développement d'applications mobiles dans AEM à l'aide de Adobe PhoneGap Enterprise.
uuid: d8442447-ee04-4bb2-a0d7-17dcc8979dba
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
discoiquuid: fd7bcf17-af7e-4bd6-8137-48401d9743c5
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '602'
ht-degree: 12%

---


# Développement d’applications mobiles dans AEM {#developing-mobile-applications-in-aem}

>[!NOTE]
>
>Adobe recommande d’utiliser l’éditeur d’application d’une seule page (SPA) pour les projets nécessitant un rendu côté client basé sur la structure SPA (par exemple, React). [En savoir plus](/help/sites-developing/spa-overview.md).

AEM tire parti des solutions Adobe PhoneGap and Adobe Publishing, ce qui vous permet de créer et de gérer les applications mobiles riches en contenu multiplateformes basées sur des utilitaires:

* Gérez toutes vos applications mobiles de sociétés au même endroit.
* Passez en revue les applications en cours de développement et d’évaluation des environnements sans avoir à configurer les profils de manière complexe et sans avoir à créer et à télécharger votre application pour le partage.
* Utilisez l’environnement de création AEM pour créer et gérer du contenu enrichi pour vos applications.
* Utilisez le format HTML5 avec Adobe PhoneGap pour créer des expériences enrichies avec des fonctionnalités natives de périphériques.
* Introduisez des Webviews HTML5 dans des applications **natives** préexistantes ou nouvelles par le biais de Cordova WebViews.
* Créez, traitez et partagez du contenu multimédia enrichi sur tous les canaux de la diffusion, y compris Web, mobile-web, mobile-app et print.

AEM s’intègre à l’Adobe **[service de PhoneGap Build](https://build.phonegap.com/)** pour simplifier le processus de création et de déploiement d’applications.

**Adobe** ContentLes utilisateurs peuvent facilement télécharger des mises à jour de page et de contenu en direct (OTA) sur leurs appareils sans avoir à réinstaller l’application ou à télécharger à partir de l’AppStore, de Google Play ou d’autres sources d’application.

**L&#39;** analyse des Adobes est entièrement intégrée dans les applications AEM et permet un suivi détaillé de la distribution, de la géolocalisation, des systèmes d&#39;exploitation, des périphériques, des flux de clics, du suivi des iBeacon, etc.

## Création d’applications {#creating-apps}

Les développeurs peuvent utiliser le [AEM kit de démarrage PhoneGap](https://github.com/Adobe-Marketing-Cloud/aem-phonegap-starter-kit) ainsi que d&#39;autres ressources disponibles dans [https://github.com/adobe-marketing-cloud-apps](https://github.com/adobe-marketing-cloud-apps) pour amorcer des applications AEM avec PhoneGap, y compris une application native de référence exécutant Cordova Webviews.

Le fichier Lisez-moi pour le référentiel Git Starter Kit comprend un didacticiel pour l’utilisation du kit de démarrage :

* Personnalisation de l’identité graphique
* Maven sample build and deployment cibles
* Configuration du référentiel de contrôle de source
* Installation et déploiement dans des instances AEM locales ou distantes
* Désinstallation à partir de AEM

>[!NOTE]
>
>Une autre source d&#39;implémentation de référence, y compris les laboratoires, se trouve sur GitHub [ici](https://github.com/adobe-marketing-cloud-apps) et, la source du &quot;dissipateur de cuisine&quot; [ici](https://github.com/blefebvre/aem-phonegap-kitchen-sink).

## Développement pour les hôtes IOS 9 et HTTP {#developing-for-ios-and-http-hosts}

Les développeurs IOS doivent être informés d&#39;un problème ouvert concernant les applications Cordova s&#39;exécutant sur iOS 9. Ce problème empêche les demandes d’être envoyées à des hôtes non sécurisés (tels que *http://localhost:4502*). Ce problème sera résolu avec une prochaine version de cordova-ios (consommée par l&#39;interface de ligne de commande Cordova), mais en attendant, deux solutions sont disponibles :

1. Pour pallier ce problème, vous pouvez toujours utiliser n’importe quel simulateur iOS 8 sans problème.
1. Si vous devez utiliser iOS 9, votre fichier d’applications -Info.plist (situé après avoir exécuté `cordova platform add ios` dans &quot;&lt;racine de l’application>/platforms/ios/&lt;nom de l’application>/&lt;nom de l’application>-Info.plist&quot;) peut être modifié manuellement afin d’inclure la propriété suivante :

```
<key>NSAppTransportSecurity</key>

<dict>

<key>NSAllowsArbitraryLoads</key> <true/>

</dict>
```

>[!NOTE]
>
>Pour plus d’informations sur &quot;App Transport Security&quot;, consultez la section suivante de [La pré-version iOS9 d’Apple](https://developer.apple.com/library/prerelease/ios/releasenotes/General/WhatsNewIniOS/Articles/iOS9.html#//apple_ref/doc/uid/TP40016198-SW14) et cette [discussion sur le débordement de pile](https://stackoverflow.com/questions/30751053/ios9-ats-what-about-html5-based-apps/).

## Développement d’applications mobiles dans AEM {#developing-mobile-applications-in-aem-1}

* [Démarrage AEM PhoneGap](/help/mobile/starting-aem-phonegap-app.md)
* [Création d’applications mobiles](/help/mobile/building-app-mobile-phonegap.md)
* [Structure d’une application](/help/mobile/phonegap-structure-an-app.md)
* [Création et modification d’applications à l’aide de la console d’applications](/help/mobile/phonegap-apps-console.md)
* [des applications sur une seule page ;](/help/mobile/phonegap-single-page-applications.md)
* [Développement d&#39;applications avec l&#39;interface de ligne de commande PhoneGap](/help/mobile/phonegap-apps-pg-cli.md)
* [Accéder aux fonctionnalités du périphérique](/help/mobile/phonegap-access-device-features.md)
* [Suivi des performances des applications avec les analyses mobiles Adobe](/help/mobile/phonegap-intro-to-app-analytics.md)
* [Ajouter Adobe Analytics à votre application mobile](/help/mobile/phonegap-add-analytics-to-apps.md)
* [Notifications Push](/help/mobile/phonegap-push-notifications.md)
* [Personnalisation du contenu AEM Mobile](/help/mobile/phonegap-aem-mobile-content-personalization.md)
* [L&#39;anatomie d&#39;une application](/help/mobile/phonegap-apps-arch.md)
* [Votre application hybride est-elle prête pour l&#39;AEM Mobile ?](/help/mobile/phonegap-adding-content-to-imported-app.md)

### Ressources supplémentaires {#additional-resources}

Pour en savoir plus sur les rôles et les responsabilités d’un administrateur et d’un développeur, consultez les ressources ci-dessous :

* [Création pour Adobe PhoneGap Enterprise avec AEM](/help/mobile/phonegap.md)
* [Administration de contenu pour Adobe PhoneGap Enterprise avec AEM](/help/mobile/administer-phonegap.md)
