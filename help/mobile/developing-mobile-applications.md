---
title: Développement d’applications mobiles dans AEM
description: Consultez cette page pour commencer à développer des applications mobiles dans AEM à l’aide d’Adobe PhoneGap Enterprise.
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
exl-id: cf8ba05c-6dcd-4880-b8bf-72382118cd80
solution: Experience Manager
feature: Mobile
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '552'
ht-degree: 5%

---

# Développement d’applications mobiles dans AEM {#developing-mobile-applications-in-aem}

>[!NOTE]
>
>Adobe recommande d’utiliser l’éditeur SPA pour les projets nécessitant un rendu côté client, basé sur un framework, pour une application à une seule page (comme React). [En savoir plus](/help/sites-developing/spa-overview.md).

AEM utilise Adobe PhoneGap et Adobe Publishing Solutions, ce qui vous permet de créer et de gérer des applications mobiles riches en contenu et basées sur des utilitaires sur plusieurs plateformes :

* Gérez toutes les applications mobiles de vos entreprises au même endroit.
* Passez en revue les applications dans les environnements de développement et d’évaluation sans connaître la complexité des profils de mise en service et sans avoir à créer et charger votre application pour le partage.
* Utilisez l’environnement de création AEM pour créer et gérer du contenu enrichi pour vos applications.
* Utilisez HTML5 avec Adobe PhoneGap pour créer des expériences riches avec des fonctionnalités natives de périphérique.
* Introduisez des webviews HTML5 vers des applications **natives** nouvelles ou préexistantes par le biais des WebViews Cordova.
* Créez, traitez et partagez du contenu multimédia enrichi sur tous les canaux de diffusion, notamment le web, le web mobile, l’application mobile et l’impression.

AEM s’intègre au service Adobe PhoneGap Build (`https://build.phonegap.com/`) pour simplifier le processus de création et de déploiement d’applications.

**Adobe ContentSync** permet aux utilisateurs de télécharger facilement des mises à jour de page et de contenu en direct (OTA) sur leurs appareils sans avoir à réinstaller l’application ou à télécharger à partir de l’appStore, de Google Play ou d’autres sources d’application.

**Adobe Analytics** est entièrement intégré aux applications d’AEM et permet un suivi détaillé de la distribution, de la géolocalisation, des systèmes d’exploitation, des périphériques, des flux de clics, du suivi des balises iBeacon, etc.

## Création d’applications {#creating-apps}

Les développeurs peuvent utiliser le [AEM PhoneGap Starter Kit](https://github.com/Adobe-Marketing-Cloud/aem-phonegap-starter-kit) avec des ressources supplémentaires trouvées dans [https://github.com/adobe-marketing-cloud-apps](https://github.com/adobe-marketing-cloud-apps) pour amorcer AEM applications avec PhoneGap, y compris une application native de référence exécutant Cordova Webviews.

Le fichier Lisez-moi pour le référentiel Git du kit de démarrage comprend un tutoriel sur l’utilisation du kit de démarrage :

* Personnalisation de l’identité graphique
* Exemples de cibles de déploiement et de génération Maven
* Configuration du référentiel de contrôle Source
* Installation et déploiement sur des instances d’AEM locales ou distantes
* Désinstallation à partir d’AEM

>[!NOTE]
>
>Vous trouverez une source de mise en oeuvre de référence supplémentaire, y compris les laboratoires, sur GitHub [ici](https://github.com/adobe-marketing-cloud-apps) et sur la source &quot;cuisine-sink&quot; [ici](https://github.com/blefebvre/aem-phonegap-kitchen-sink).

## Développement pour les hôtes IOS 9 et HTTP {#developing-for-ios-and-http-hosts}

Les développeurs IOS doivent être conscients d’un problème ouvert avec les applications Cordova s’exécutant sur iOS 9. Ce problème empêche les requêtes d’être effectuées sur des hôtes non sécurisés (tels que *http://localhost:4502*). Ce problème sera résolu avec une prochaine version de cordova-ios (consommée par l’interface de ligne de commande Cordova), mais en attendant, deux solutions sont disponibles :

1. Pour pallier ce problème, vous pouvez toujours utiliser n’importe quel simulateur iOS 8 sans problème.
1. Si vous devez utiliser iOS 9, votre fichier apps -Info.plist (trouvé après l’exécution de `cordova platform add ios` dans &quot;&lt;racine de l’application>/platforms/ios/&lt;nom de l’application>/&lt;nom de l’application>-Info.plist&quot;) peut être modifié manuellement afin d’inclure la propriété suivante :

```
<key>NSAppTransportSecurity</key>

<dict>

<key>NSAllowsArbitraryLoads</key> <true/>

</dict>
```

>[!NOTE]
>
>Pour plus d’informations sur &quot;App Transport Security&quot;, reportez-vous à la section suivante de la [documentation de pré-version Apple iOS9](https://developer.apple.com/library/prerelease/ios/releasenotes/General/WhatsNewIniOS/Articles/iOS9.html#//apple_ref/doc/uid/TP40016198-SW14) et de cette [discussion Stack Overflow](https://stackoverflow.com/questions/30751053/ios9-ats-what-about-html5-based-apps/).

## Développement d’applications mobiles dans AEM {#developing-mobile-applications-in-aem-1}

* [Démarrage AEM PhoneGap](/help/mobile/starting-aem-phonegap-app.md)
* [Création d’applications mobiles](/help/mobile/building-app-mobile-phonegap.md)
* [Structure d’une application](/help/mobile/phonegap-structure-an-app.md)
* [Création et modification d’applications à l’aide de la console Applications](/help/mobile/phonegap-apps-console.md)
* [Applications sur une seule page](/help/mobile/phonegap-single-page-applications.md)
* [Développement d’applications avec l’interface de ligne de commande PhoneGap](/help/mobile/phonegap-apps-pg-cli.md)
* [Accès aux fonctionnalités du périphérique](/help/mobile/phonegap-access-device-features.md)
* [Suivi des performances de l’application avec Adobe Mobile Analytics](/help/mobile/phonegap-intro-to-app-analytics.md)
* [Ajout d’Adobe Analytics à votre application mobile](/help/mobile/phonegap-add-analytics-to-apps.md)
* [Notifications Push](/help/mobile/phonegap-push-notifications.md)
* [Personnalisation du contenu AEM Mobile](/help/mobile/phonegap-aem-mobile-content-personalization.md)
* [Anatomie d’une application](/help/mobile/phonegap-apps-arch.md)
* [Votre application hybride est-elle prête pour AEM Mobile ?](/help/mobile/phonegap-adding-content-to-imported-app.md)

### Ressources supplémentaires {#additional-resources}

Pour en savoir plus sur les rôles et les responsabilités d’un administrateur et d’un développeur, consultez les ressources ci-dessous :

* [Création pour Adobe PhoneGap Enterprise avec AEM](/help/mobile/phonegap.md)
* [Administration de contenu pour Adobe PhoneGap Enterprise avec AEM](/help/mobile/administer-phonegap.md)
