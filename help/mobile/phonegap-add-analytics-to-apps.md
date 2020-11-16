---
title: Ajouter Adobe Analytics à votre application mobile
seo-title: Ajouter Adobe Analytics à votre application mobile
description: Suivez cette page pour en savoir plus sur l’utilisation des analyses des applications mobiles dans vos applications AEM en les intégrant à Adobe Mobile Services.
seo-description: Suivez cette page pour en savoir plus sur l’utilisation des analyses des applications mobiles dans vos applications AEM en les intégrant à Adobe Mobile Services.
uuid: d3ff6f9b-0467-4abe-9a59-b3495a6af0f8
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
discoiquuid: cd9d2bea-48d8-4a17-8544-ea25dcad69f3
translation-type: tm+mt
source-git-commit: 8279cd590244a7f2d20cfaf1c7505a3ef57fae4a
workflow-type: tm+mt
source-wordcount: '971'
ht-degree: 2%

---


# Ajouter Adobe Analytics à votre application mobile{#add-adobe-analytics-to-your-mobile-application}

>[!NOTE]
>
>Adobe recommande d’utiliser l’éditeur d’application d’une seule page (SPA) pour les projets nécessitant un rendu côté client basé sur la structure SPA (par exemple, React). [En savoir plus](/help/sites-developing/spa-overview.md).

Souhaitez-vous créer des expériences pertinentes et attrayantes pour vos utilisateurs d’applications mobiles ? Si vous n’utilisez pas l’Adobe Mobile Services SDK pour surveiller et mesurer le cycle de vie et l’utilisation des applications, sur quoi basez-vous vos décisions ? Où sont vos clients les plus fidèles ? Comment pouvez-vous garantir que vous restez pertinent et que vous optimisez les conversions ?

Vos utilisateurs accèdent-ils à tout le contenu ? Est-ce qu&#39;ils abandonnent l&#39;application, et si oui, où ? À quelle fréquence restent-ils dans l’application et à quelle fréquence reviennent-ils pour l’utiliser ? Quels changements pouvez-vous introduire et ensuite mesurer cette augmentation de la rétention ? Qu’en est-il des taux de plantage ? Votre application se bloque-t-elle pour vos utilisateurs ?

Tirez parti des analyses [des applications](https://www.adobe.com/ca/solutions/digital-analytics/mobile-web-apps-analytics.html) mobiles dans vos applications AEM en les intégrant à [Adobe Mobile Services](https://www.adobe.com/marketing-cloud/mobile-marketing.html).

Appliquez des outils à vos applications AEM pour suivre, créer des rapports et comprendre comment vos utilisateurs interagissent avec votre application et votre contenu mobiles et pour mesurer les mesures clés de cycle de vie, telles que les lancements, le temps passé dans l’application et le taux de plantage.

Cette section décrit comment les *développeurs* AEM peuvent :

* Intégration de Mobile Analytics dans votre application mobile
* Testez le suivi de vos analyses avec Bloodhound

## Conditions préalables {#prerequisties}

AEM Mobile requiert un compte Adobe Analytics pour collecter et rapporter les données de suivi dans votre application. Dans le cadre de la configuration, l&#39; *Administrateur* AEM devra d&#39;abord :

* Configurez un compte Adobe Analytics et créez une suite de rapports pour votre application dans Mobile Services.
* Configurez un Cloud Service AMS dans Adobe Experience Manager (AEM).

## Pour les développeurs - Intégrez Mobile Analytics à votre application {#for-developers-integrate-mobile-analytics-into-your-app}

### Configuration de ContentSync pour extraire le fichier de configuration {#configure-contentsync-to-pull-in-configuration-file}

Une fois le compte Analytics configuré, vous devez créer une configuration Content Sync pour extraire le contenu dans votre application mobile.

Pour plus d’informations, voir Configuration du contenu de la synchronisation du contenu. La configuration devra indiquer à Content Sync de placer ADBMobileConfig dans le répertoire /www. Par exemple, dans l’application Geometrixx Outdoors, la configuration Content Sync se trouve à l’emplacement suivant : */content/phonegap/geometrixx-outdoors/shell/jcr:content/page-app/app-config/ams-ADBMobileConfig*. Il existe également une configuration pour le développement ; toutefois, elle est identique à la configuration de non-développement dans le cas des Geometrixx Outdoors.

Pour plus d’informations sur la façon de télécharger ADBMobileConfig depuis votre tableau de bord d’applications AEM pour applications mobiles, consultez le fichier de configuration du SDK Analytics - Mobile Services - Adobe Mobile Services.

```xml
<jcr:root xmlns:jcr="https://www.jcp.org/jcr/1.0" xmlns:nt="https://www.jcp.org/jcr/nt/1.0"
    jcr:primaryType="nt:unstructured"
    extension="json"
    path="../../../.."
    selector="ADBMobileConfig"
    targetRootDirectory="www"
    type="mobileADBMobileConfigJSON"/>
```

Pour chaque plate-forme, ADBMobileConfig doit être copié à un emplacement spécifique.

Si vous générez avec l&#39;interface de ligne de commande PhoneGap, vous pouvez le faire avec des scripts d&#39;accrochage de génération Cordova. Vous pouvez le voir dans l’application Geometrixx Outdoors à l’adresse :*content/phonegap/geometrixx-outdoors/shell/_jcr_content/pge-app/app-content/phonegap/scripts/restore_plugins.js.*

Pour iOS, le fichier devra être copié dans le répertoire **Ressources** du projet XCode (ex. &quot;platforms/ios/Geometrixx/Resources/ADBMobileConfig.json&quot;). Si l’application est ciblée pour Android, le chemin d’accès vers lequel effectuer la copie est &quot;platforms/android/assets/ADBMobileConfig.json&quot;. Pour plus d&#39;informations sur l&#39;utilisation des crochets pendant la génération de l&#39;interface de ligne de commande PhoneGap, consultez la section [Trois crochets dont votre projet Cordova/PhoneGap a besoin](https://devgirl.org/2013/11/12/three-hooks-your-cordovaphonegap-project-needs/).

```xml
///////////////////////////
//          iOS
///////////////////////////
    ios : [
        {
            "www/ADBMobileConfig.json": "platforms/ios/<YOUR_APP_NAME>/Resources/ADBMobileConfig.json"
        }
    ],
///////////////////////////
//          ANDROID
///////////////////////////
    android: [
        {
            "www/ADBMobileConfig.json": "platforms/android/assets/ADBMobileConfig.json"
        }
    ]
```

### Ajouter le module externe AMS dans l’application {#add-the-ams-plugin-in-the-app}

Pour que l’application puisse collecter les données, le module externe Adobe Mobile Services (AMS) doit être inclus dans l’application. En incluant le plug-in en tant que fonctionnalité dans le fichier config.xml de l&#39;application, un autre hook Cordova peut être utilisé pour ajouter automatiquement le plug-in pendant le processus de création PhoneGap.

```xml
<feature name="ADBMobile">
    <param name="id" value="https://github.com/Adobe-Marketing-Cloud/mobile-services#0482f9cedf90c98a8d4b07219ece1933b2e46a60"/>
</feature>
```

Le fichier Geometrixx Outdoors App config.xml se trouve dans */content/phonegap/geometrixx-outdoors/shell/jcr:content/pge-app/app-content/phonegap/www/config.xml*. L’exemple ci-dessus demande une version spécifique du module externe à utiliser en ajoutant un &quot;#&quot;, puis une valeur de balise après l’URL du module externe. Il est recommandé de suivre cette procédure pour s’assurer que les problèmes imprévus ne s’affichent pas en raison de l’ajout de modules externes non testés au cours d’une compilation.

Une fois que vous avez exécuté ces étapes, votre application sera activée pour rapporter toutes les mesures de cycle de vie fournies par Adobe Analytics. Cela inclut les données telles que les lancements, les blocages et les installations. Si c&#39;est les seules données qui vous tiennent à coeur, alors vous avez terminé. Si vous souhaitez collecter des données personnalisées, vous devez instrumentaliser votre code.

### Instrument votre code pour le suivi complet des applications {#instrument-your-code-for-full-app-tracking}

Plusieurs API de suivi sont fournies dans l’API du module externe Phonegap [AMS.](https://docs.adobe.com/content/help/en/mobile-services/ios/phonegap-ios/phonegap-methods.html)

Vous pourrez ainsi effectuer le suivi des états et des actions, tels que l’emplacement des pages sur lesquelles vos utilisateurs naviguent dans votre application, les contrôles les plus utilisés. Le moyen le plus simple d’instrumentaliser votre application pour le suivi consiste à utiliser les API Analytics fournies par le module externe AMS.

* ADB.trackState()
* ADB.trackAction()

A titre de référence, vous pouvez consulter le code de l’application Geometrixx Outdoors. Dans l’application Geometrixx Outdoors, tous les navigations de page sont suivis à l’aide de la méthode ADB.trackState(). Pour plus d’informations, consultez le code source pour /libs/mobileapps/components/angular/ng-page/clientlibs/app-navigation.js

En instrumentant votre code source avec ces appels de méthode, vous pouvez collecter des mesures complètes par rapport à votre application.

#### Propriétés de connexion à AMS {#properties-for-connecting-to-ams}

*com.adobe.cq.mobile.mobileservices.impl.service.* MobileServicesHttpClientImpl expose les propriétés suivantes pour la connexion à AMS :

| **Libellé** | **Description** | **Valeur par défaut** |
|---|---|---|
| Point de terminaison API | URL de base des API HTTP de Mobile Services Adobe | https://api.omniture.com |
| Point de terminaison de configuration | URL utilisée pour récupérer la configuration mobile ADB pour l’identifiant de suite de rapports donné | /ams/1.0/app/config/ |
| Applications Mobile Service | Obtenir une liste d&#39;applications dans la société des utilisateurs | /ams/1.0/apps |

