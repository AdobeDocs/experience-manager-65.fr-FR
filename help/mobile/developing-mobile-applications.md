---
title: Développement d’applications mobiles dans AEM
seo-title: Developing Mobile Applications in AEM
description: Consultez cette page pour commencer à développer des applications mobiles dans AEM à l’aide d’Adobe PhoneGap Enterprise.
seo-description: Follow this page to start developing mobile application in AEM using Adobe PhoneGap Enterprise.
uuid: d8442447-ee04-4bb2-a0d7-17dcc8979dba
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
discoiquuid: fd7bcf17-af7e-4bd6-8137-48401d9743c5
exl-id: cf8ba05c-6dcd-4880-b8bf-72382118cd80
source-git-commit: 259f257964829b65bb71b5a46583997581a91a4e
workflow-type: tm+mt
source-wordcount: '582'
ht-degree: 1%

---

# Développement d’applications mobiles dans AEM {#developing-mobile-applications-in-aem}

>[!NOTE]
>
>Adobe recommande d’utiliser l’éditeur de SPA pour les projets qui nécessitent un rendu côté client basé sur la structure d’application d’une seule page (par exemple, React). [En savoir plus](/help/sites-developing/spa-overview.md).

AEM exploite Adobe PhoneGap et les solutions de publication d’Adobe, ce qui vous permet de créer et de gérer des applications mobiles riches en contenu et basées sur des utilitaires sur plusieurs plateformes :

* Gérez toutes les applications mobiles de vos entreprises au même endroit.
* Passez en revue les applications dans les environnements de développement et d’évaluation sans connaître la complexité des profils de mise en service et sans avoir à créer et charger votre application pour le partage.
* Utilisez l’environnement de création AEM pour créer et gérer du contenu enrichi pour vos applications.
* Utilisez HTML5 avec Adobe PhoneGap pour créer des expériences riches avec des fonctionnalités natives de périphérique.
* Introduction de webviews HTML5 aux vues nouvelles ou préexistantes **natif** applications via les WebViews Cordova.
* Créez, traitez et partagez du contenu multimédia enrichi sur tous les canaux de diffusion, notamment le web, le web mobile, l’application mobile et l’impression.

AEM s’intègre au service Adobe PhoneGap Build (`https://build.phonegap.com/`) pour simplifier le processus de création et de déploiement de l’application.

**Adobe ContentSync** permet aux utilisateurs de télécharger facilement des mises à jour de page et de contenu en direct (OTA) sur leurs appareils sans avoir à réinstaller l’application ou à télécharger à partir de l’appStore, de Google Play ou d’autres sources d’applications.

**Adobe Analytics** est entièrement intégré aux applications AEM et permet un suivi détaillé de la distribution, de la géolocalisation, des systèmes d’exploitation, des périphériques, des flux de clics, du suivi des balises iBeacon, etc.

## Création d’applications {#creating-apps}

Les développeurs peuvent utiliser la variable [AEM PhoneGap Starter Kit](https://github.com/Adobe-Marketing-Cloud/aem-phonegap-starter-kit) ainsi que les ressources supplémentaires trouvées dans [https://github.com/adobe-marketing-cloud-apps](https://github.com/adobe-marketing-cloud-apps) pour démarrer des applications AEM avec PhoneGap, y compris une application native de référence exécutant Cordova Webviews.

Le fichier Lisez-moi pour le référentiel Git du kit de démarrage comprend un tutoriel sur l’utilisation du kit de démarrage :

* Personnalisation de l’identité graphique
* Exemples de cibles de déploiement et de génération Maven
* Configuration du référentiel de contrôle de source
* Installation et déploiement sur des instances d’AEM locales ou distantes
* Désinstallation à partir d’AEM

>[!NOTE]
>
>Vous trouverez une source d’implémentation de référence supplémentaire, y compris des laboratoires, sur GitHub. [here](https://github.com/adobe-marketing-cloud-apps) et, la source &quot;cuisine-sink&quot; [here](https://github.com/blefebvre/aem-phonegap-kitchen-sink).

## Développement pour les hôtes IOS 9 et HTTP {#developing-for-ios-and-http-hosts}

Les développeurs IOS doivent être conscients d’un problème ouvert avec les applications Cordova s’exécutant sur iOS 9. Ce problème empêche les demandes envoyées à des hôtes non sécurisés (tels que *http://localhost:4502*). Ce problème sera résolu avec une prochaine version de cordova-ios (consommée par l’interface de ligne de commande Cordova), mais en attendant, deux solutions sont disponibles :

1. Pour pallier ce problème, vous pouvez toujours utiliser n’importe quel simulateur iOS 8 sans problème.
1. Si vous devez utiliser iOS 9, vos applications -Info.plist (trouvées après exécution `cordova platform add ios` dans &quot;&lt;app root=&quot;&quot;>/platforms/ios/&lt;app name=&quot;&quot;>/&lt;app name=&quot;&quot;>Le fichier &quot;-Info.plist&quot;) peut être modifié manuellement pour inclure la propriété suivante :

```
<key>NSAppTransportSecurity</key>

<dict>

<key>NSAllowsArbitraryLoads</key> <true/>

</dict>
```

>[!NOTE]
>
>Pour plus d’informations sur &quot;App Transport Security&quot;, reportez-vous à la section suivante de [Apple - Documentation bêta iOS9](https://developer.apple.com/library/prerelease/ios/releasenotes/General/WhatsNewIniOS/Articles/iOS9.html#//apple_ref/doc/uid/TP40016198-SW14) et ceci [Débat sur l’Overflow de pile](https://stackoverflow.com/questions/30751053/ios9-ats-what-about-html5-based-apps/).

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
