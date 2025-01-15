---
title: Ajout d’Adobe Analytics à votre application mobile
description: Consultez cette page pour découvrir comment utiliser Mobile App Analytics dans vos applications Adobe Experience Manager en intégrant Adobe Mobile Services.
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
exl-id: 8d965e94-c368-481d-b000-6e22456c34db
solution: Experience Manager
feature: Mobile
role: Admin
source-git-commit: 2dae56dc9ec66f1bf36bbb24d6b0315a5f5040bb
workflow-type: tm+mt
source-wordcount: '883'
ht-degree: 0%

---

# Ajout d’Adobe Analytics à votre application mobile{#add-adobe-analytics-to-your-mobile-application}

{{ue-over-mobile}}

Vous souhaitez créer des expériences attrayantes et pertinentes pour les utilisateurs de votre application mobile ? Si vous n’utilisez pas le SDK Adobe Mobile Services pour surveiller et mesurer le cycle de vie et l’utilisation des applications, sur quoi basez-vous vos décisions ? Où sont vos clients les plus fidèles ? Comment pouvez-vous garantir que vous restez pertinent et que vous optimisez les conversions ?

Vos utilisateurs accèdent-ils à tout le contenu ? Abandonnent-ils l&#39;application, et si oui, où ? À quelle fréquence restent-ils dans l&#39;application et à quelle fréquence reviennent-ils pour l&#39;utiliser? Quels changements pouvez-vous apporter et ensuite mesurer cette augmentation de la rétention? Qu’en est-il des taux de plantage ? Votre application est-elle en panne pour vos utilisateurs ?

Tirez parti de [Mobile App Analytics](https://business.adobe.com/products/analytics/mobile-marketing.html) dans vos applications Adobe Experience Manager (AEM) en intégrant à [Adobe Mobile Services](https://business.adobe.com/products/campaign/mobile-marketing.html).

Instrumentez vos applications AEM pour suivre, générer des rapports et comprendre comment vos utilisateurs interagissent avec votre application et votre contenu mobiles, et pour mesurer les mesures de cycle de vie clés telles que les lancements, le temps passé dans l’application et le taux de plantage.

Cette section décrit comment AEM *Developers* peut :

* Intégration de Mobile Analytics dans votre application mobile
* Tester votre suivi Analytics avec Bloodhound

## Conditions préalables {#prerequisties}

AEM Mobile nécessite un compte Adobe Analytics pour collecter et générer des rapports sur les données de tracking dans votre application. Dans le cadre de la configuration, l’*administrateur* d’AEM doit d’abord :

* Configurez un compte Adobe Analytics et créez une suite de rapports pour votre application dans Mobile Services.
* Configurez un Cloud Service AMS dans Adobe Experience Manager (AEM).

## Pour les développeurs - Intégrer Mobile Analytics à votre application {#for-developers-integrate-mobile-analytics-into-your-app}

### Configurer ContentSync pour extraire le fichier de configuration {#configure-contentsync-to-pull-in-configuration-file}

Une fois le compte Analytics configuré, créez une configuration de synchronisation du contenu pour extraire le contenu dans votre application mobile.

Pour plus d’informations, voir Configuration du contenu de synchronisation du contenu. La configuration doit demander à la synchronisation de contenu de placer ADBMobileConfig dans le répertoire /www. Par exemple, dans l’application Geometrixx Outdoors, la configuration de la synchronisation du contenu se trouve à l’adresse : */content/phonegap/geometrixx-outdoors/shell/jcr:content/pge-app/app-config/ams-ADBMobileConfig*. Il existe également une configuration pour le développement. Toutefois, elle est identique à la configuration hors développement s’il existe des Geometrixx Outdoors.

Pour plus d&#39;informations sur le téléchargement d&#39;ADBMobileConfig depuis le tableau de bord de votre application mobile AEM Apps, reportez-vous à la section Analytics - Mobile Services - Fichier de configuration SDK Adobe Mobile Services.

```xml
<jcr:root xmlns:jcr="https://www.jcp.org/jcr/1.0" xmlns:nt="https://www.jcp.org/jcr/nt/1.0"
    jcr:primaryType="nt:unstructured"
    extension="json"
    path="../../../.."
    selector="ADBMobileConfig"
    targetRootDirectory="www"
    type="mobileADBMobileConfigJSON"/>
```

Chaque plateforme nécessite que l&#39;ADBMobileConfig soit copié vers un emplacement spécifique.

Si vous créez avec l’interface de ligne de commande PhoneGap, vous pouvez le faire avec des scripts de hook de création Cordova. Vous pouvez le voir dans l’application Geometrixx Outdoors à l’adresse :*content/phonegap/geometrixx-outdoors/shell/_jcr_content/pge-app/app-content/phonegap/scripts/restore_plugins.js.*

Pour iOS, le fichier doit être copié dans le répertoire **Resources** du projet XCode (par exemple, « platforms/ios/Geometrixx/Resources/ADBMobileConfig.json »). Si l’application est ciblée pour Android™, le chemin d’accès à copier est « platforms/android/assets/ADBMobileConfig.json ». Pour plus d’informations sur l’utilisation des points d’extension pendant la génération de l’interface de ligne de commande PhoneGap, voir [ Trois points d’extension dont votre projet Cordova/PhoneGap a besoin ](https://gist.github.com/jlcarvalho/22402d013bc72f795d45a01836ce735c).

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

Pour que l’application puisse collecter les données, le plug-in Adobe Mobile Services (AMS) doit être inclus dans l’application. En incluant le plug-in en tant que fonctionnalité dans le fichier config.xml de l’application, un autre hook Cordova peut être utilisé pour ajouter automatiquement le plug-in pendant le processus de création PhoneGap.

```xml
<feature name="ADBMobile">
    <param name="id" value="https://github.com/Adobe-Marketing-Cloud/mobile-services#0482f9cedf90c98a8d4b07219ece1933b2e46a60"/>
</feature>
```

L’application Geometrixx Outdoors config.xml se trouve à l’adresse */content/phonegap/geometrixx-outdoors/shell/jcr:content/pge-app/app-content/phonegap/www/config.xml*. L’exemple ci-dessus demande une version spécifique du plug-in à utiliser en ajoutant un « # », puis une valeur de balise après l’URL du plug-in. Il s’agit d’une bonne pratique à suivre pour vous assurer que des problèmes imprévus n’apparaissent pas en raison de l’ajout de modules externes non testés lors d’une création.

Après avoir effectué ces étapes, votre application sera activée pour générer des rapports sur toutes les mesures de cycle de vie fournies par Adobe Analytics. Cela inclut les données telles que les lancements, les blocages et les installations. Si ce sont les seules données qui vous intéressent, alors c&#39;est fini. Si vous souhaitez collecter des données personnalisées, vous devez instrumenter votre code.

### Instrumenter votre code pour le suivi complet des applications {#instrument-your-code-for-full-app-tracking}

Plusieurs API de suivi sont fournies dans l’[API du plug-in AMS Phonegap](https://github.com/Adobe-Marketing-Cloud/mobile-services/blob/master/docs/ios/phonegap/phonegap-methods.md).

Ils vous permettent de suivre les états et les actions, comme l’emplacement où vos utilisateurs et utilisatrices naviguent dans votre application, et les contrôles les plus utilisés. Le moyen le plus simple d’instrumenter votre application pour le suivi consiste à utiliser les API Analytics fournies par le plug-in AMS.

* ADB.trackState()
* ADB.trackAction()

À titre de référence, consultez le code dans l’application Geometrixx Outdoors. Dans l’application Geometrixx Outdoors, toute navigation sur les pages est suivie à l’aide de la méthode ADB.trackState() . Pour plus d’informations, consultez le code source de /libs/mobileapps/components/angular/ng-page/clientlibs/app-navigation.js .

En instrumentant votre code source avec ces appels de méthode, vous pouvez collecter des mesures complètes sur votre application.

#### Propriétés de connexion à AMS {#properties-for-connecting-to-ams}

*com.adobe.cq.mobile.mobileservices.impl.service.MobileServicesHttpClientImp* l expose les propriétés suivantes pour la connexion à AMS :

| **Libellé** | **Description** | **Par défaut** |
|---|---|---|
| Point d’entrée de l’API | URL de base des API HTTP Adobe Mobile Services | https://api.omniture.com |
| Configurer le point d’entrée | URL utilisée pour récupérer la configuration ADB Mobile pour l’identifiant de suite de rapports donné | /ams/1.0/app/config/ |
| Applications Mobile Service | Obtention d’une liste d’applications au sein de la société utilisateurs | /ams/1.0/apps |
