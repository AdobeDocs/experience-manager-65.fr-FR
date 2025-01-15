---
title: Développement d’applications mobiles dans AEM
description: Consultez cette page pour commencer à développer une application mobile dans AEM à l’aide d’Adobe PhoneGap Enterprise.
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
exl-id: cf8ba05c-6dcd-4880-b8bf-72382118cd80
solution: Experience Manager
feature: Mobile
role: Admin
source-git-commit: 2dae56dc9ec66f1bf36bbb24d6b0315a5f5040bb
workflow-type: tm+mt
source-wordcount: '531'
ht-degree: 1%

---

# Développement d’applications mobiles dans AEM {#developing-mobile-applications-in-aem}

{{ue-over-mobile}}

AEM utilise les solutions de publication Adobe PhoneGap et Adobe, qui vous permettent de créer et de gérer des applications mobiles multiplateformes riches en contenu et basées sur des utilitaires :

* Gérez toutes les applications mobiles de votre entreprise en un seul endroit.
* Examinez les applications dans les environnements de développement et d’évaluation sans la complexité des profils d’approvisionnement et les efforts supplémentaires nécessaires pour créer et charger votre application pour le partage.
* Utilisez l’environnement de création AEM pour créer et gérer du contenu riche pour vos applications.
* Utilisez HTML5 avec Adobe PhoneGap pour créer des expériences riches avec des fonctionnalités natives sur les appareils.
* Introduisez les Webviews HTML 5 dans les applications **natives** nouvelles ou préexistantes via Cordova WebViews.
* Créez, organisez et partagez du contenu multimédia enrichi sur tous les canaux de diffusion, y compris le web, le web mobile, les applications mobiles et l’impression.

AEM s’intègre au service Adobe PhoneGap Build (`https://build.phonegap.com/`) pour simplifier le processus de création et de déploiement de l’application.

**Adobe ContentSync** permet aux utilisateurs de télécharger facilement des mises à jour de pages et de contenus par les airs sur leurs appareils sans avoir à réinstaller l&#39;application ou à la télécharger à partir de l&#39;appStore, de Google Play ou d&#39;autres sources d&#39;application.

**Adobe Analytics** est entièrement intégré aux applications AEM et permet le suivi détaillé de la distribution, de la géolocalisation, des systèmes d’exploitation, des appareils, des flux de clics, du suivi iBeacon et plus encore.

## Création d’applications {#creating-apps}

Les développeurs peuvent utiliser le [kit de démarrage AEM PhoneGap](https://github.com/Adobe-Marketing-Cloud/aem-phonegap-starter-kit) ainsi que des ressources supplémentaires disponibles dans [https://github.com/adobe-marketing-cloud-apps](https://github.com/adobe-marketing-cloud-apps) pour amorcer les applications AEM avec PhoneGap, y compris une application native de référence exécutant Cordova Webviews.

Le fichier Lisez-moi du référentiel Git du Starter Kit comprend un tutoriel expliquant comment utiliser le Starter Kit :

* Personnaliser l’identité graphique
* Exemple de build Maven et cibles de déploiement
* Configuration du référentiel de contrôle Source
* Installation et déploiement sur des instances AEM locales ou distantes
* Désinstaller à partir d’AEM

>[!NOTE]
>
>D’autres sources d’implémentation de référence, y compris des laboratoires, sont disponibles sur GitHub [ici](https://github.com/adobe-marketing-cloud-apps) et la source « cuisine-évier » [ici](https://github.com/blefebvre/aem-phonegap-kitchen-sink).

## Développement pour les hôtes IOS 9 et HTTP {#developing-for-ios-and-http-hosts}

Les développeurs IOS doivent être informés qu’un problème lié aux applications Cordova s’exécutant sur iOS 9 est en cours d’exécution. Ce problème empêche les demandes d&#39;être envoyées à des hôtes non sécurisés (comme *http://localhost:4502*). Ce problème sera résolu dans une prochaine version de cordova-ios (utilisée par l’interface de ligne de commande Cordova), mais en attendant, deux solutions de contournement sont disponibles :

1. Pour pallier ce problème, vous pouvez toujours utiliser n’importe quel simulateur iOS 8 sans problème.
1. Si vous devez utiliser iOS 9, le fichier apps -Info.plist (qui se trouve après l’exécution de `cordova platform add ios` dans « &lt;app root>/platform/ios/&lt;app name>/&lt;app name>-Info.plist ») peut être modifié manuellement pour inclure la propriété suivante :

```
<key>NSAppTransportSecurity</key>

<dict>

<key>NSAllowsArbitraryLoads</key> <true/>

</dict>
```

>[!NOTE]
>
>Pour plus d’informations sur « App Transport Security », consultez la section suivante de la [documentation de version préliminaire d’Apple iOS9](https://developer.apple.com/library/prerelease/ios/releasenotes/General/WhatsNewIniOS/Articles/iOS9.html#//apple_ref/doc/uid/TP40016198-SW14) et cette [discussion sur le débordement de la pile](https://stackoverflow.com/questions/30751053/ios9-ats-what-about-html5-based-apps/).

## Développement d’applications mobiles dans AEM {#developing-mobile-applications-in-aem-1}

* [Démarrage d’AEM PhoneGap](/help/mobile/starting-aem-phonegap-app.md)
* [Création d’applications mobiles](/help/mobile/building-app-mobile-phonegap.md)
* [Structure d’une application](/help/mobile/phonegap-structure-an-app.md)
* [Création et modification d’applications à l’aide de la console Applications](/help/mobile/phonegap-apps-console.md)
* [Applications sur une seule page](/help/mobile/phonegap-single-page-applications.md)
* [Développement d’applications avec l’interface de ligne de commande PhoneGap](/help/mobile/phonegap-apps-pg-cli.md)
* [Accéder aux fonctionnalités de l’appareil](/help/mobile/phonegap-access-device-features.md)
* [Suivi des performances des applications avec Adobe Mobile Analytics](/help/mobile/phonegap-intro-to-app-analytics.md)
* [Ajout d’Adobe Analytics à votre application mobile](/help/mobile/phonegap-add-analytics-to-apps.md)
* [Notifications Push](/help/mobile/phonegap-push-notifications.md)
* [Personnalisation du contenu AEM Mobile](/help/mobile/phonegap-aem-mobile-content-personalization.md)
* [L’anatomie d’une application](/help/mobile/phonegap-apps-arch.md)
* [Votre application hybride est-elle prête pour AEM Mobile ?](/help/mobile/phonegap-adding-content-to-imported-app.md)

### Ressources supplémentaires {#additional-resources}

Pour en savoir plus sur les rôles et les responsabilités d’un administrateur et d’un développeur, consultez les ressources ci-dessous :

* [Création pour Adobe PhoneGap Enterprise avec AEM](/help/mobile/phonegap.md)
* [Administration de contenu pour Adobe PhoneGap Enterprise avec AEM](/help/mobile/administer-phonegap.md)
