---
title: Ajout d’Adobe Analytics à votre application mobile
seo-title: Ajout d’Adobe Analytics à votre application mobile
description: Consultez cette page pour en savoir plus sur l’utilisation de Mobile App Analytics dans vos applications AEM grâce à l’intégration à Adobe Mobile Services.
seo-description: Consultez cette page pour en savoir plus sur l’utilisation de Mobile App Analytics dans vos applications AEM grâce à l’intégration à Adobe Mobile Services.
uuid: d3ff6f9b-0467-4abe-9a59-b3495a6af0f8
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
discoiquuid: cd9d2bea-48d8-4a17-8544-ea25dcad69f3
exl-id: 8d965e94-c368-481d-b000-6e22456c34db
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '971'
ht-degree: 2%

---

# Ajout d’Adobe Analytics à votre application mobile{#add-adobe-analytics-to-your-mobile-application}

>[!NOTE]
>
>Adobe recommande d’utiliser l’éditeur d’application d’une seule page (SPA) pour les projets nécessitant un rendu côté client basé sur la structure SPA (par exemple, React). [En savoir plus](/help/sites-developing/spa-overview.md).

Vous souhaitez créer des expériences attrayantes et pertinentes pour les utilisateurs de vos applications mobiles ? Si vous n’utilisez pas le SDK Mobile Services Adobe pour surveiller et mesurer le cycle de vie et l’utilisation des applications, alors sur quoi basez-vous vos décisions ? Où sont vos clients les plus fidèles ? Comment pouvez-vous garantir que vous restez pertinent et que vous optimisez les conversions ?

Vos utilisateurs accèdent-ils à tout le contenu ? Abandonnent-ils l&#39;application, et si oui, où ? À quelle fréquence restent-ils dans l’application et à quelle fréquence reviennent-ils pour l’utiliser ? Quels changements pouvez-vous introduire et ensuite mesurer cette augmentation de rétention ? Qu’en est-il des taux de plantage ? Votre application est-elle en panne pour vos utilisateurs ?

Profitez de [Mobile App Analytics](https://www.adobe.com/ca/solutions/digital-analytics/mobile-web-apps-analytics.html) dans vos applications AEM en intégrant [Adobe Mobile Services](https://www.adobe.com/marketing-cloud/mobile-marketing.html).

instrumentalisez vos applications AEM pour effectuer le suivi, créer des rapports et comprendre la manière dont vos utilisateurs interagissent avec votre application mobile et votre contenu, ainsi que pour mesurer les mesures clés de cycle de vie, telles que les lancements, le temps passé dans l’application et le taux de plantage.

Cette section décrit comment AEM *développeurs* peuvent :

* Intégration de Mobile Analytics dans votre application mobile
* Test de votre suivi d’analyse avec Bloodhound

## Conditions préalables {#prerequisties}

AEM Mobile nécessite un compte Adobe Analytics pour collecter et générer des rapports sur les données de suivi dans votre application. Dans le cadre de la configuration, l’AEM *Administrateur* devra d’abord :

* Configurez un compte Adobe Analytics et créez une suite de rapports pour votre application dans Mobile Services.
* Configurez un Cloud Service AMS dans Adobe Experience Manager (AEM).

## Pour les développeurs : intégrez Mobile Analytics à votre application {#for-developers-integrate-mobile-analytics-into-your-app}

### Configuration de ContentSync pour extraire le fichier de configuration {#configure-contentsync-to-pull-in-configuration-file}

Une fois le compte Analytics configuré, vous devez créer une configuration de synchronisation de contenu pour extraire le contenu dans votre application mobile.

Pour plus d’informations, voir Configuration du contenu de synchronisation du contenu. La configuration doit indiquer à Synchronisation du contenu de placer ADBMobileConfig dans le répertoire /www . Par exemple, dans l’application Geometrixx Outdoors, la configuration de synchronisation de contenu se trouve à l’adresse : */content/phonegap/geometrixx-outdoors/shell/jcr:content/page-app/app-config/ams-ADBMobileConfig*. Il existe également une configuration pour le développement ; toutefois, elle est identique à la configuration non développée dans le cas des Geometrixx Outdoors.

Pour plus d’informations sur le téléchargement d’ADBMobileConfig à partir du tableau de bord Applications de l’AEM d’application mobile, reportez-vous à la section Fichier de configuration du SDK Analytics - Mobile Services - Adobe Mobile Services .

```xml
<jcr:root xmlns:jcr="https://www.jcp.org/jcr/1.0" xmlns:nt="https://www.jcp.org/jcr/nt/1.0"
    jcr:primaryType="nt:unstructured"
    extension="json"
    path="../../../.."
    selector="ADBMobileConfig"
    targetRootDirectory="www"
    type="mobileADBMobileConfigJSON"/>
```

Pour chaque plateforme, ADBMobileConfig doit être copié vers un emplacement spécifique.

Si vous créez avec l’interface de ligne de commande de PhoneGap, vous pouvez le faire avec des scripts de crochets de génération cordova. Vous pouvez le voir dans l’application Geometrixx Outdoors à l’adresse :*content/phonegap/geometrixx-outdoors/shell/_jcr_content/pge-app/app-content/phonegap/scripts/restore_plugins.js.*

Pour iOS, le fichier doit être copié dans le répertoire **Resources** du projet Xcode (par exemple, &quot;platforms/ios/Geometrixx/Resources/ADBMobileConfig.json&quot;). Si l’application est ciblée pour Android, le chemin d’accès à copier est &quot;platforms/android/assets/ADBMobileConfig.json&quot;. Pour plus d’informations sur l’utilisation des hooks pendant la génération de l’interface de ligne de commande PhoneGap, reportez-vous à la section [Trois hooks your Cordova/PhoneGap project need](https://devgirl.org/2013/11/12/three-hooks-your-cordovaphonegap-project-needs/).

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

### Ajout du module externe AMS dans l’application {#add-the-ams-plugin-in-the-app}

Pour que l’application collecte les données, le module externe Adobe Mobile Services (AMS) doit être inclus dans l’application. En incluant le module externe en tant que fonctionnalité dans le fichier config.xml de l’application, un autre point d’extension Cordova peut être utilisé pour ajouter automatiquement le module pendant le processus de génération PhoneGap.

```xml
<feature name="ADBMobile">
    <param name="id" value="https://github.com/Adobe-Marketing-Cloud/mobile-services#0482f9cedf90c98a8d4b07219ece1933b2e46a60"/>
</feature>
```

L’application Geometrixx Outdoors config.xml se trouve à l’adresse */content/phonegap/geometrixx-outdoors/shell/jcr:content/pge-app/app-content/phonegap/www/config.xml*. L’exemple ci-dessus demande une version spécifique du module externe à utiliser en ajoutant un &quot;#&quot;, puis une valeur de balise après l’URL du module externe. Il est recommandé de suivre cette procédure pour vous assurer que les problèmes imprévus ne s’affichent pas en raison de l’ajout de modules externes non testés au cours d’une version.

Une fois ces étapes effectuées, votre application sera activée pour signaler toutes les mesures de cycle de vie fournies par Adobe Analytics. Cela inclut les données telles que les lancements, les blocages et les installations. Si c&#39;est les seules données qui vous tiennent à coeur alors vous avez fini. Si vous souhaitez collecter des données personnalisées, vous devez instrumenter votre code.

### instrumentez votre code pour le suivi complet des applications {#instrument-your-code-for-full-app-tracking}

Plusieurs API de suivi sont fournies dans l’[API du module externe AMS Phonegap.](https://docs.adobe.com/content/help/en/mobile-services/ios/phonegap-ios/phonegap-methods.html)

Vous pourrez ainsi effectuer le suivi des états et des actions, comme l’emplacement des pages vers lesquelles vos utilisateurs accèdent dans votre application, les contrôles qui sont les plus utilisés. Le moyen le plus simple d’instrumenter votre application pour le suivi consiste à utiliser les API Analytics fournies par le module externe AMS.

* ADB.trackState()
* ADB.trackAction()

À titre de référence, vous pouvez consulter le code de l’application Geometrixx Outdoors. Dans l’application Geometrixx Outdoors, toutes les navigations de page sont suivies à l’aide de la méthode ADB.trackState() . Pour plus d’informations, consultez le code source pour /libs/mobileapps/components/angular/ng-page/clientlibs/app-navigation.js

En instrumentant votre code source avec ces appels de méthode, vous pouvez collecter des mesures complètes sur votre application.

#### Propriétés pour la connexion à AMS {#properties-for-connecting-to-ams}

*com.adobe.cq.mobile.mobileservices.impl.service.* MobileServicesHttpClientImpl expose les propriétés suivantes pour la connexion à AMS :

| **Libellé** | **Description** | **Valeur par défaut** |
|---|---|---|
| Point de terminaison API | URL de base des API HTTP Adobe Mobile Services | https://api.omniture.com |
| Config Endpoint | URL utilisée pour récupérer la configuration mobile ADB de l’identifiant de suite de rapports donné | /ams/1.0/app/config/ |
| Applications Mobile Service | Obtention d’une liste d’applications au sein de l’entreprise des utilisateurs | /ams/1.0/apps |
