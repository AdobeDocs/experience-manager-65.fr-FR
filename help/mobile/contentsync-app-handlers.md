---
title: Gestionnaires d’applications prêts à l’emploi
seo-title: Gestionnaires d’applications prêts à l’emploi
description: Consultez cette page pour en savoir plus sur les gestionnaires prêts à l’emploi pour Adobe PhoneGap Enterprise avec AEM.
seo-description: Consultez cette page pour en savoir plus sur les gestionnaires prêts à l’emploi pour Adobe PhoneGap Enterprise avec AEM.
uuid: 436038cb-fb76-4bb5-ae79-5d4043b81dd9
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
discoiquuid: fec86f03-f81e-460a-9f84-d6304c95128c
exl-id: e2ddf5d1-0f5b-4f3b-9666-0f388915730e
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1430'
ht-degree: 2%

---

# Gestionnaires d’applications prêts à l’emploi{#out-of-the-box-app-handlers}

>[!NOTE]
>
>Adobe recommande d’utiliser l’éditeur d’application d’une seule page (SPA) pour les projets nécessitant un rendu côté client basé sur la structure SPA (par exemple, React). [En savoir plus](/help/sites-developing/spa-overview.md).

Consultez les instructions suivantes pour le développement de gestionnaires de synchronisation de contenu :

* Les gestionnaires doivent implémenter *com.day.cq.contentsync.handler.ContentUpdateHandler* (directement ou en étendant une classe qui le fait).
* Les gestionnaires peuvent étendre *com.adobe.cq.mobile.platform.impl.contentsync.handler.AbstractSlingResourceUpdateHandler*
* Le gestionnaire ne doit signaler la valeur true que s’il a mis à jour le cache ContentSync. La création de rapports erronés sur true permettra AEM de créer une mise à jour.
* Le gestionnaire ne doit mettre à jour le cache que si le contenu a réellement changé. N’écrivez pas dans le cache si un blanc n’est pas nécessaire et évitez toute création de mise à jour inutile.

## Gestionnaires prêts à l’emploi {#out-of-the-box-handlers}

La liste suivante répertorie les gestionnaires d’applications prêts à l’emploi :

**** mobileapppagesRenders Pages de l’application.

* ***type - Chaîne***  - mobileapppages
* ***path - String***  - chemin d’accès à une page
* ***extension - String***  - extension qui doit être utilisée dans la requête. Pour les pages, cela est presque toujours *html*, mais d’autres sont encore possibles.

* ***selector - String***  : sélecteurs facultatifs séparés par un point. Les exemples courants sont *touch* pour le rendu des versions mobiles d’une page.

* ***deep - Booléen***  - Propriété booléenne facultative déterminant si les pages enfants doivent également être incluses. La valeur par défaut est *true.*

* ***includeImages - Booléen***  - Propriété booléenne facultative déterminant si les images doivent être incluses. La valeur par défaut est *true*.

   * Par défaut, seuls les composants d’image avec un type de ressource foundation/components/image sont pris en compte pour inclusion.

* ***includeVideos - Booléen***  - Une propriété booléenne facultative détermine si les vidéos doivent être incluses. La valeur par défaut est *true*.

* ***includeModifiedPagesOnly - Booléen***  - Si elle est fausse ou omise, elle affiche toutes les pages et vérifie les mises à jour dans le rendu. Si la valeur est true, la base diffère des modifications apportées à une page lastModified.
* ***+ rewrite (noeud)***
   ***- relativeParentPath - Chaîne***  : chemin d’accès auquel écrire tous les autres chemins relatifs.

>[!NOTE]
>
>Le type de ressource des composants image et vidéo affectés par ce gestionnaire est défini en configurant les propriétés de *com.adobe.cq.mobile.platform.impl.contentsync.handler*.*Service OSGi MobilePagesUpdateHandler*.

**** mobilepageassetsCollecte des ressources de page d’application.

**** mobilecontentlistingRépertorie le contenu du fichier compressé ContentSync. Il est utilisé par le js côté client sur l’appareil pour effectuer la copie de fichier initiale requise pour les applications AEM.

Ce gestionnaire doit être ajouté à toute configuration ContentSync de l’application AEM.

* ***type - String - mobilecontentlisting***
* ***path***  - Chaîne - laissez vide. Doit être présent pour être considéré comme un gestionnaire valide, mais le chemin est déduit comme le cache ContentSync actuel. Cette valeur est ignorée.
* ***targetRootDirectory* -**Chaîne : préfixe à ajouter aux chemins en tant que racine cible pour la mise à jour du contenu de ce gestionnaire.
* ***order - Long*  - **Order for ContentSync (Ordre long pour ContentSync) pour exécuter ce gestionnaire. Ce nombre doit être supérieur à tous les autres gestionnaires tels que 100. Il doit être exécuté après les gestionnaires de contenu traditionnels.

```xml
{
  "files": [
    "config.xml",
    "res/screens/ios/screen-ipad-portrait-2x.png",
    "res/screens/ios/screen-ipad-landscape.png",
    "res/screens/ios/screen-iphone-portrait-2x.png",
    "res/screens/ios/screen-iphone-landscape.png",
    "res/screens/ios/screen-iphone-portrait.png",
    "apps/weretail-app/components/splash-page/clientlibs.css",
    ...
    "pge-content-packages.json"
  ],
  "count": 382,
  "lastModified": 1422902754733
}
```

**** mobilecontentpackageslistingRépertorie le package de contenu AEM dans une application donnée ainsi que l’URL du serveur vers lequel effectuer les demandes de mise à jour. Il est utilisé par les js côté client sur l’appareil pour demander des mises à jour de contenu.

Le gestionnaire doit être utilisé sur AEM Configuration ContentSync de l’interpréteur d’applications (noeud avec pge-type=app-instance).

* ***type - String - mobilecontentpackageslisting***
* ***path **-**String***  - Chemin d’accès à un shell d’application (noeud avec pge-type=app-instance).
* ***targetRootDirectory - Chaîne***  : préfixe à ajouter aux chemins en tant que racine cible pour la mise à jour du contenu de ce gestionnaire.
* ***order - Long*  - **Order for ContentSync pour exécuter ce gestionnaire. Ce nombre doit être supérieur à tous les autres gestionnaires tels que 100. Il doit être exécuté après les gestionnaires de contenu traditionnels.

>[!NOTE]
>
>Le bloc de code suivant n’est pas une implémentation exacte et doit être utilisé comme exemple de référence :

```xml
{
  "content": [
    {
      "name": "en",
      "title": "We Retail Mobile App - English",
      "type": "CONTENT",
      "path": "/content/phonegap/weretail-outdoors/en",
      "updatePath": "/content/phonegap/weretail/en/jcr:content/pge-app/app-config"
    },
    {
      "name": "shell",
      "title": "We Retail Mobile App",
      "type": "INSTANCE",
      "path": "/content/phonegap/weretail-outdoors/shell",
      "updatePath": "/content/phonegap/weretail/shell/jcr:content/pge-app/app-config"
    }
  ],
  "serverURL": "http://localhost:4503/"
}
```

**** widgetconfigInclut un fichier config.xml mis à jour qui fusionne toutes les modifications effectuées via le centre de commandes avec un fichier config.xml fourni. Si ce gestionnaire n’est pas inclus, les détails de l’application qui sont modifiés via l’interface d’administration ne seront pas inclus dans le cache.

Ce gestionnaire doit être utilisé sur une configuration ContentSync de Shell d’application AEM (noeud avec pge-type=[app-instance]).

* ***type - String* - **widgetconfig
* ***path **-**String***  - Chemin d’accès à tout noeud enfant shell d’application (noeud avec pge-type=[app-instance]).
* ***targetRootDirectory - Chaîne***  : préfixe à ajouter aux chemins en tant que racine cible pour la mise à jour du contenu de ce gestionnaire.
* ***targetIconDirectory - Chaîne***  - répertoire dans lequel placer les icônes de l’application.

**** mobileADBMobileConfigJSONI Incluez le fichier ADBMobileConfig.JSON si le service de cloud AMS a été configuré.

Il est utilisé au moment de la compilation pour configurer le module externe AMS pour la prise en charge de l’analyse.

Le gestionnaire doit être utilisé sur AEM Configuration ContentSync de l’interpréteur d’applications (noeud avec pge-type=app-instance).

* ***type - Chaîne***  - mobileADBMobileConfigJSON
* ***path - String***  - Chemin d’accès à un shell d’application (noeud avec pge-type=app-instance ou un RT qui étend /libs/mobileapps/core/components/instance)
* ***targetRootDirectory - String***  - préfixe à ajouter aux chemins en tant que racine cible pour la mise à jour du contenu de ce gestionnaire.

**** notificationsconfigExtrait les configurations de notifications requises sur le périphérique. Les propriétés sont extraites de la configuration de service cloud de service Push correspondante associée à l’application.

Les propriétés non AEM du noeud jcr:content du service cloud sont extraites et ajoutées au fichier JSON **pge-notifications-config.json** pour inclusion à la racine www du contenu de l’application.

Les propriétés AEM sont celles qui sont placées dans un espace de noms avec &quot;cq&quot;, &quot;sling&quot; ou &quot;jcr&quot;. D’autres propriétés peuvent être exclues à l’aide de la propriété &quot;excludeProperties&quot; sur le noeud de configuration content-sync.

* ***type - String***  - notificationsconfig
* ***excludeProperties - String[]***  - propriétés à exclure

**** contentsyncconfigcontentCollecte du contenu à partir d’une configuration ContentSync existante.

* ***type - String***  - contentsyncconfigcontent
* ***path - String***  - Chemin d’accès à l’un des éléments suivants :

   * autre configuration ContentSync
   * dans un module de contenu (utilisera sa propriété phonegap-exportTemplate pour trouver sa configuration ContentSync).
   * à une ressource mobile (app-content se trouve sous cette ressource et, si ces modules de contenu ont une propriété page-includeInBuild qui est vraie, phonegap-exportTemplate est utilisé pour trouver sa configuration ContentSync).

* ***autoCreateFirstUpdateBeforeImport - Booléen***  - si la valeur est true, créez une  **** mise à jour initiale dans la configuration cible avant de procéder à l’importation si une fois n’existe pas déjà.

* ***autoFillBeforeImport - Booléen***  - si la valeur est true, mettez à jour/remplissez la configuration cible avant d’importer
* ***configSuffix - String***  - chaîne à ajouter au chemin indiqué sur la propriété &quot;phonegap-exportTemplate&quot; de app-content. Vous pouvez l’utiliser pour distinguer différents modèles d’exportation. Par exemple, cette propriété peut être définie sur **&quot;-dev&quot;** pour indiquer que *&quot;/../../../../appconfig-dev&quot;* doit être utilisé (par opposition à *&quot;/../../../appconfig&quot;*).

**app-** assetsInclut toutes les ressources associées à une instance d’application. Ce gestionnaire inclut toutes les ressources trouvées sous le chemin spécifié, ainsi que toutes les ressources référencées par la propriété appAssetPath d’une instance d’application.

* ***type - Chaîne***  - app-assets

* ***path **-**String***  - chemin d’accès à un emplacement sous une instance d’application où les ressources de l’application sont stockées

**** mobileappoffersUn nouveau gestionnaire de synchronisation de contenu a été introduit pour le cas d’utilisation de la personnalisation pour le rendu du contenu ciblé. Le gestionnaire &quot;mobileappoffers&quot; sait comment effectuer le rendu des offres cibles associées qui ont été créées par l’auteur du contenu. Le gestionnaire mobileappoffers étend le gestionnaire de mise à jour des pages abstraites. De ce fait, de nombreuses propriétés sont similaires. Les détails du gestionnaire mobileappoffers présentent les propriétés suivantes.

Le gestionnaire mobileappsoffers étend le gestionnaire mobileappspages et ajoute les propriétés suivantes :

* ***locationRoot - String***  - spécifiez l’emplacement de l’application mobile.
* ***includePageTypes - String***  - prend par défaut en charge cq/personalization/components/teaserpage et cq/personalization/components/offerproxy.
* ***selector - String***  - doit être défini sur tandt
* ***path - Chaîne*** : chemin d’accès à la marque de la campagne.

**** mobileappconfigLe gestionnaire de synchronisation de contenu mobileappconfig permet d’injecter des données JSON dans le fichier MobileAppsConfig.json. Pour enregistrer une classe de fournisseur, les développeurs ajouteront leur classe MobileAppsInfoProvider à la liste des fournisseurs. Le gestionnaire effectue une itération sur la liste de MobileAppsInfoProviders et permet au fournisseur d’injecter des données dans le fichier json résultant. La liste des propriétés prises en charge par ce gestionnaire est la suivante :

* ***path **-**Chaîne***  - chemin d’accès à un noeud d’instance d’application avec pge-type=app-instance ou un RT qui étend /libs/mobileapps/core/components/instance
* ***provider - String*** `[]`  - liste des MobileAppsInfoProviders entièrement qualifiés
* ***targetRootDirectory - String***  - répertoire dans lequel écrire le fichier MobileAppsConfig.json.
* **fileName - String**  - nom facultatif du fichier sur lequel écrire le JSON. Par défaut, il s’agit de MobileAppsConfig.json.

Il est possible que plusieurs gestionnaires mobileappconfig soient configurés chacun avec un ensemble unique de fournisseurs écrivant dans différents fichiers JSON.

### Test des gestionnaires de synchronisation de contenu {#testing-content-sync-handlers}

**Procédure de vérification du cache** IntegrityClear

* Effacer le cache
* Exécution de votre gestionnaire (mise à jour du cache)
* Exécutez à nouveau votre gestionnaire (le cache ne doit pas être mis à jour).

**Procédure de débogage**

* Exécution de votre configuration
* Exportation de votre configuration ou révision sur le périphérique
* Si le rendu échoue, recherchez les *styles/assets/libs* manquants ou recherchez les mauvais chemins d’accès à *styles/assets/libs*

**** LoggingEnable ContentSync Debug logging via les configurations de journalisation OSGI sur le package  `com.day.cq.contentsync` Cela vous permet de suivre les gestionnaires exécutés et s’ils ont mis à jour le cache et signalé la mise à jour du cache.

## Ressources supplémentaires {#additional-resources}

Pour en savoir plus sur les rôles et les responsabilités d’un administrateur et d’un développeur, consultez les ressources ci-dessous :

* [Création pour Adobe PhoneGap Enterprise avec AEM](/help/mobile/phonegap.md)
* [Administration de contenu pour Adobe PhoneGap Enterprise avec AEM](/help/mobile/administer-phonegap.md)

>[!NOTE]
>
>Pour commencer à développer des applications AEM Mobile, cliquez [ici](/help/mobile/getting-started-aem-mobile.md).
