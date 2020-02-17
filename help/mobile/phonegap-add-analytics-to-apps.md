---
title: Ajout d’Adobe Analytics à votre application mobile
seo-title: Ajout d’Adobe Analytics à votre application mobile
description: Suivez cette page pour en savoir plus sur l’utilisation des analyses d’applications mobiles dans vos applications AEM en les intégrant à Adobe Mobile Services.
seo-description: Suivez cette page pour en savoir plus sur l’utilisation des analyses d’applications mobiles dans vos applications AEM en les intégrant à Adobe Mobile Services.
uuid: d3ff6f9b-0467-4abe-9a59-b3495a6af0f8
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
discoiquuid: cd9d2bea-48d8-4a17-8544-ea25dcad69f3
translation-type: tm+mt
source-git-commit: 58fa0f05bae7ab5ba51491be3171b5c6ffbe870d

---


# Ajout d’Adobe Analytics à votre application mobile{#add-adobe-analytics-to-your-mobile-application}

>[!NOTE]
>
>Adobe recommande d’utiliser l’éditeur d’application d’une seule page (SPA) pour les projets nécessitant un rendu côté client basé sur la structure SPA (par exemple, React). [En savoir plus](/help/sites-developing/spa-overview.md).

Vous souhaitez créer des expériences pertinentes et attrayantes pour vos utilisateurs d’applications mobiles ? Si vous n’utilisez pas le SDK Adobe Mobile Services pour surveiller et mesurer le cycle de vie et l’utilisation des applications, sur quoi basez-vous vos décisions ? Où sont vos clients les plus fidèles ? Comment garantir que vous restez pertinent et que vous optimisez les conversions ?

Vos utilisateurs accèdent-ils à tout le contenu ? Est-ce qu&#39;ils abandonnent l&#39;application, et si oui, où ? À quelle fréquence restent-ils dans l’application et à quelle fréquence reviennent-ils pour l’utiliser ? Quels changements pouvez-vous introduire puis mesurer cette augmentation de la rétention ? Qu’en est-il des taux de plantage ? Votre application se bloque-t-elle pour vos utilisateurs ?

Tirez parti des analyses [des applications](https://www.adobe.com/ca/solutions/digital-analytics/mobile-web-apps-analytics.html) mobiles dans vos applications AEM en les intégrant à [Adobe Mobile Services](https://www.adobe.com/marketing-cloud/mobile-marketing.html).

Appliquez des outils à vos applications AEM pour effectuer le suivi, créer des rapports et comprendre comment vos utilisateurs interagissent avec votre application mobile et votre contenu, ainsi que pour mesurer les mesures clés de cycle de vie telles que les lancements, le temps passé dans l’application et le taux de plantage.

Cette section décrit comment les *développeurs* AEM peuvent :

* Intégration de Mobile Analytics dans votre application mobile
* Testez le suivi des analyses avec Bloodhound

## Conditions préalables {#prerequisties}

AEM Mobile requiert un compte Adobe Analytics pour collecter et rapporter les données de suivi dans votre application. Dans le cadre de la configuration, l’ *administrateur* AEM devra d’abord :

* Configurez un compte Adobe Analytics et créez une suite de rapports pour votre application dans Mobile Services.
* Configurez un service AMS Cloud dans Adobe Experience Manager (AEM).

## Pour les développeurs - Intégrez Mobile Analytics à votre application {#for-developers-integrate-mobile-analytics-into-your-app}

### Configuration de ContentSync pour extraire le fichier de configuration {#configure-contentsync-to-pull-in-configuration-file}

Une fois le compte Analytics configuré, vous devez créer une configuration de synchronisation de contenu pour intégrer le contenu dans votre application mobile.

Pour plus d’informations, voir Configuration du contenu de la synchronisation du contenu. La configuration devra indiquer à Content Sync de placer ADBMobileConfig dans le répertoire /www. Par exemple, dans l’application Geometrixx Outdoors, la configuration Content Sync se trouve à l’emplacement suivant : */content/phonegap/geometrixx-outdoors/shell/jcr:content/page-app/app-config/ams-ADBMobileConfig*. Il existe également une configuration pour le développement ; toutefois, elle est identique à la configuration sans développement dans le cas de Geometrixx Outdoors.

Pour plus d&#39;informations sur le téléchargement d&#39;ADBMobileConfig à partir de votre tableau de bord Applications AEM d&#39;application mobile, reportez-vous à la section Fichier de configuration Analytics - Mobile Services - Adobe Mobile Services SDK.

```xml
<jcr:root xmlns:jcr="https://www.jcp.org/jcr/1.0" xmlns:nt="https://www.jcp.org/jcr/nt/1.0"
    jcr:primaryType="nt:unstructured"
    extension="json"
    path="../../../.."
    selector="ADBMobileConfig"
    targetRootDirectory="www"
    type="mobileADBMobileConfigJSON"/>
```

Pour chaque plateforme, ADBMobileConfig doit être copié à un emplacement spécifique.

Si vous construisez avec l&#39;interface de ligne de commande PhoneGap, vous pouvez le faire avec des scripts Hook de génération Cordova. Vous pouvez le voir dans l’application Geometrixx Outdoors à l’adresse : content/phonegap/geometrixx-outdoors/shell/_jcr_content/pge-app/app-content/phonegap/scripts/restore_plugins.js *.*

Pour iOS, le fichier devra être copié dans le répertoire **Ressources** du projet XCode (ex. &quot;platforms/ios/Geometrixx/Resources/ADBMobileConfig.json&quot;). Si l’application est ciblée pour Android, le chemin vers lequel la copie doit être effectuée est &quot;platforms/android/assets/ADBMobileConfig.json&quot;. Pour plus d&#39;informations sur l&#39;utilisation des crochets pendant la génération de l&#39;interface de ligne de commande PhoneGap, consultez la section [Trois crochets dont votre projet Cordova/PhoneGap a besoin](https://devgirl.org/2013/11/12/three-hooks-your-cordovaphonegap-project-needs/).

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

Pour que l’application collecte les données, le module externe Adobe Mobile Services (AMS) doit être inclus dans l’application. En incluant le plug-in comme fonctionnalité dans le fichier config.xml de l&#39;application, un autre hook Cordova peut être utilisé pour ajouter automatiquement le plug-in pendant le processus de création PhoneGap.

```xml
<feature name="ADBMobile">
    <param name="id" value="https://github.com/Adobe-Marketing-Cloud/mobile-services#0482f9cedf90c98a8d4b07219ece1933b2e46a60"/>
</feature>
```

Le fichier config.xml de l’application Geometrixx Outdoors se trouve sous */content/phonegap/geometrixx-outdoors/shell/jcr:content/pge-app/app-content/phonegap/www/config.xml*. L’exemple ci-dessus demande l’utilisation d’une version spécifique du module externe en ajoutant un &quot;#&quot;, puis une valeur de balise après l’URL du module externe. Il est recommandé de suivre cette procédure pour vous assurer que les problèmes imprévus ne s’affichent pas en raison de l’ajout de modules externes non testés pendant une génération.

Une fois que vous avez effectué ces étapes, votre application sera activée pour rapporter toutes les mesures de cycle de vie fournies par Adobe Analytics. Cela inclut les données telles que les lancements, les blocages et les installations. Si c&#39;est les seules données qui vous intéressent, alors vous en avez fini. Si vous souhaitez collecter des données personnalisées, vous devez utiliser l’instrument de votre code.

### Instrument de votre code pour le suivi complet des applications {#instrument-your-code-for-full-app-tracking}

Plusieurs API de suivi sont fournies dans l’API du module externe Phonegap [AMS.](https://marketing.adobe.com/resources/help/en_US/mobile/ios/phonegap_methods.html)

Vous pourrez ainsi effectuer le suivi des états et des actions, tels que l’emplacement des pages sur lesquelles vos utilisateurs naviguent dans votre application, les contrôles les plus utilisés. Le moyen le plus simple d’instrumentaliser votre application pour le suivi consiste à utiliser les API Analytics fournies par le module externe AMS.

* ADB.trackState()
* ADB.trackAction()

À titre de référence, vous pouvez consulter le code de l’application Geometrixx Outdoors. Dans l’application Geometrixx Outdoors, tous les navigations de page sont suivis à l’aide de la méthode ADB.trackState(). Pour plus d’informations, consultez le code source pour /libs/mobileapps/components/angular/ng-page/clientlibs/app-navigation.js

En instrumentant votre code source avec ces appels de méthode, vous pouvez collecter des mesures complètes par rapport à votre application.

### Test du suivi Analytics avec Bloodhound {#testing-analytics-tracking-with-bloodhound}

![](do-not-localize/chlimage_1.jpeg)

Avant de procéder au déploiement en production, vous pouvez éventuellement utiliser l’outil Adobe [Bloodhound](https://marketing.adobe.com/developer/gallery/bloodhound-app-measurement-qa-tool-1) pour tester votre configuration Analytics. Pour tester votre configuration Analytics, vous devez modifier votre fichier ADBMobileConfig.json afin de pointer vers le serveur sur lequel Bloodhound s’exécute au lieu du serveur Analytics réel. Pour effectuer cette modification, modifiez l’entrée suivante à partir de votre fichier ADBMobileConfig.json.

```xml
...
"analytics": {
    "rsids": "YOUR_RSID",
    "server": "YOUR_TRACKING_SERVER:YOUR_TRACKING_PORT",
...
```

Modifier pour correspondre à cette entrée :

```xml
...
"analytics": {
    "rsids": "YOUR_RSID",
    "server": "localhost:50000",
...
```

Toutes les données collectées par le module externe AMS seront redirigées vers Bloodhound afin que vous puissiez afficher les résultats.

#### Propriétés de Connexion à AMS {#properties-for-connecting-to-ams}

*com.adobe.cq.mobile.mobileservices.impl.service.* MobileServicesHttpClientImpl expose les propriétés suivantes pour la connexion à AMS :

| **Etiquette** | **Description** | **Default** |
|---|---|---|
| Point de terminaison API | URL de base des API HTTP d’Adobe Mobile Services | https://api.omniture.com |
| Point de fin de configuration | URL utilisée pour récupérer la configuration mobile ADB pour l’identifiant de suite de rapports donné | /ams/1.0/app/config/ |
| Applications Mobile Service | Obtenir la liste des applications au sein de l’entreprise des utilisateurs | /ams/1.0/apps |

