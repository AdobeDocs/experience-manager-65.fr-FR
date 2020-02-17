---
title: Développement d’applications mobiles dans AEM
seo-title: Développement d’applications mobiles dans AEM
description: Suivez cette page pour commencer à développer une application mobile dans AEM à l’aide d’Adobe PhoneGap Enterprise.
seo-description: Suivez cette page pour commencer à développer une application mobile dans AEM à l’aide d’Adobe PhoneGap Enterprise.
uuid: d8442447-ee04-4bb2-a0d7-17dcc8979dba
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
discoiquuid: fd7bcf17-af7e-4bd6-8137-48401d9743c5
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Développement d’applications mobiles dans AEM {#developing-mobile-applications-in-aem}

>[!NOTE]
>
>Adobe recommande d’utiliser l’éditeur d’application d’une seule page (SPA) pour les projets nécessitant un rendu côté client basé sur la structure SPA (par exemple, React). [En savoir plus](/help/sites-developing/spa-overview.md).

AEM tire parti des solutions Adobe PhoneGap and Adobe Publishing, ce qui vous permet de créer et de gérer les applications mobiles riches en contenu multiplateformes basées sur des utilitaires:

* Gérez toutes les applications mobiles de votre entreprise au même endroit.
* Passez en revue les applications dans les environnements de développement et d’évaluation sans avoir à configurer les profils ni à créer et télécharger votre application pour le partage.
* Utilisez l’environnement de création AEM pour créer et gérer du contenu enrichi pour vos applications.
* Utilisez HTML5 avec Adobe PhoneGap pour créer des expériences riches avec des fonctionnalités natives.
* Présentez des vues Web HTML5 à des applications **natives** nouvelles ou préexistantes via Cordova WebViews.
* Créez, traitez et partagez du contenu multimédia enrichi sur tous les canaux de diffusion, y compris le Web, le Web mobile, l’application mobile et l’impression.

AEM s’intègre au service **[Adobe](https://build.phonegap.com/)**PhoneGap Build afin de simplifier le processus de création et de déploiement d’applications.

**Adobe ContentSync** permet aux utilisateurs de télécharger facilement des mises à jour de page et de contenu en direct (OTA) sur leurs appareils sans avoir à réinstaller l’application ou à télécharger depuis l’AppStore, Google Play ou d’autres sources d’application.

**Adobe Analytics** est entièrement intégré aux applications AEM et permet un suivi détaillé de la distribution, de la géolocalisation, des systèmes d’exploitation, des périphériques, des flux de clics, du suivi des balises iBeacon, etc.

## Création d’applications {#creating-apps}

Les développeurs peuvent utiliser le kit [de démarrage](https://github.com/Adobe-Marketing-Cloud/aem-phonegap-starter-kit) AEM PhoneGap ainsi que d&#39;autres ressources disponibles dans [https://github.com/adobe-marketing-cloud-apps](https://github.com/adobe-marketing-cloud-apps) pour amorcer les applications AEM avec PhoneGap, y compris une application native de référence exécutant Cordova Webviews.

Le fichier Lisez-moi pour le référentiel Git du kit de démarrage comprend un didacticiel pour l’utilisation du kit de démarrage :

* Personnalisation de la marque
* Mapper des exemples de cibles de création et de déploiement
* Configuration du référentiel de contrôle de source
* Installation et déploiement dans des instances AEM locales ou distantes
* Désinstallation à partir d’AEM

>[!NOTE]
>
>Vous trouverez d&#39;autres sources d&#39;implémentation de référence, y compris des laboratoires, sur GitHub [ici](https://github.com/adobe-marketing-cloud-apps) et sur la source &quot;cuisine-évier&quot; [ici](https://github.com/blefebvre/aem-phonegap-kitchen-sink).

## Développement pour les hôtes IOS 9 et HTTP {#developing-for-ios-and-http-hosts}

Les développeurs IOS doivent être conscients d&#39;un problème ouvert avec les applications Cordova s&#39;exécutant sur iOS 9. Ce problème empêche les demandes envoyées aux hôtes non sécurisés (tels que *http://localhost:4502*). Ce problème sera résolu avec une prochaine version de cordova-ios (consommée par l&#39;interface de ligne de commande Cordova), mais en attendant, deux solutions sont disponibles :

1. Pour pallier ce problème, vous pouvez toujours utiliser n’importe quel simulateur iOS 8 sans problème.
1. Si vous devez utiliser iOS 9, votre fichier d’applications -Info.plist (situé après l’exécution `cordova platform add ios` dans &quot;&lt;racine de l’application>/platforms/ios/&lt;nom de l’application>/&lt;nom de l’application>-Info.plist&quot;) peut être modifié manuellement pour inclure la propriété suivante :

```
<key>NSAppTransportSecurity</key>

<dict>

<key>NSAllowsArbitraryLoads</key> <true/>

</dict>
```

>[!NOTE]
>
>Pour plus d’informations sur &quot;App Transport Security&quot;, reportez-vous à la section suivante des documents [de pré-version iOS9 d’](https://developer.apple.com/library/prerelease/ios/releasenotes/General/WhatsNewIniOS/Articles/iOS9.html#//apple_ref/doc/uid/TP40016198-SW14) Apple et de cette discussion [sur le débordement de](https://stackoverflow.com/questions/30751053/ios9-ats-what-about-html5-based-apps/)pile.

## Développement d’applications mobiles dans AEM {#developing-mobile-applications-in-aem-1}

* [Démarrage d’AEM PhoneGap](/help/mobile/starting-aem-phonegap-app.md)
* [Création d’applications mobiles](/help/mobile/building-app-mobile-phonegap.md)
* [Structure d’une application](/help/mobile/phonegap-structure-an-app.md)
* [Création et modification d’applications à l’aide de la console d’applications](/help/mobile/phonegap-apps-console.md)
* [Applications sur une seule page (SPA)](/help/mobile/phonegap-single-page-applications.md)
* [Développement d’applications avec l’interface de ligne de commande PhoneGap](/help/mobile/phonegap-apps-pg-cli.md)
* [Accès aux fonctionnalités des périphériques](/help/mobile/phonegap-access-device-features.md)
* [Suivi des performances des applications avec Adobe Mobile Analytics](/help/mobile/phonegap-intro-to-app-analytics.md)
* [Ajout d’Adobe Analytics à votre application mobile](/help/mobile/phonegap-add-analytics-to-apps.md)
* [Notifications Push](/help/mobile/phonegap-push-notifications.md)
* [Personnalisation du contenu AEM Mobile](/help/mobile/phonegap-aem-mobile-content-personalization.md)
* [L&#39;anatomie d&#39;une application](/help/mobile/phonegap-apps-arch.md)
* [Votre application hybride est-elle prête pour AEM Mobile ?](/help/mobile/phonegap-adding-content-to-imported-app.md)

### Ressources supplémentaires {#additional-resources}

Pour en savoir plus sur les rôles et les responsabilités d’un administrateur et d’un développeur, consultez les ressources ci-dessous :

* [Création pour Adobe PhoneGap Enterprise avec AEM](/help/mobile/phonegap.md)
* [Administration de contenu pour Adobe PhoneGap Enterprise avec AEM](/help/mobile/administer-phonegap.md)
