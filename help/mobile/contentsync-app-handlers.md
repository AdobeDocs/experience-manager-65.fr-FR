---
title: Gestionnaires d’applications prêts à l’emploi
description: Consultez cette page pour en savoir plus sur les gestionnaires prêts à l’emploi pour Adobe PhoneGap Enterprise avec AEM.
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
exl-id: e2ddf5d1-0f5b-4f3b-9666-0f388915730e
solution: Experience Manager
feature: Mobile
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '1408'
ht-degree: 1%

---

# Gestionnaires d’applications prêts à l’emploi{#out-of-the-box-app-handlers}

>[!NOTE]
>
>Adobe recommande d’utiliser l’éditeur SPA pour les projets nécessitant un rendu côté client, basé sur un framework, pour une application à une seule page (comme React). [En savoir plus](/help/sites-developing/spa-overview.md).

Consultez les instructions suivantes pour le développement de gestionnaires de synchronisation de contenu :

* Les gestionnaires doivent implémenter *com.day.cq.contentsync.handler.ContentUpdateHandler* (directement ou en étendant une classe qui le fait)
* Les gestionnaires peuvent étendre *com.adobe.cq.mobile.platform.impl.contentsync.handler.AbstractSlingResourceUpdateHandler*
* Le gestionnaire ne doit signaler la valeur true que s’il a mis à jour le cache ContentSync. La création de rapports erronés sur true permettra AEM de créer une mise à jour.
* Le gestionnaire ne doit mettre à jour le cache que si le contenu a réellement changé. N’écrivez pas dans le cache si un blanc n’est pas nécessaire et évitez toute création de mise à jour inutile.

## Gestionnaires prêts à l’emploi {#out-of-the-box-handlers}

La liste suivante répertorie les gestionnaires d’applications prêts à l’emploi :

**mobileapppages** Rendu des pages d’application.

* ***type - String*** - mobileapppages
* ***path - String*** : chemin d’accès à une page
* ***extension - String*** - Extension qui doit être utilisée dans la requête. Pour les pages, cela est presque toujours le cas *html*, mais d’autres sont toujours possibles.

* ***selector - String*** : sélecteurs facultatifs séparés par un point. Les exemples courants sont les suivants : *touch* pour le rendu des versions mobiles d’une page.

* ***deep - Booléen*** - Propriété booléenne facultative déterminant si les pages enfants doivent également être incluses. La valeur par défaut est *true.*

* ***includeImages - Booléen*** - Propriété booléenne facultative déterminant si les images doivent être incluses. La valeur par défaut est *true*.

   * Par défaut, seuls les composants d’image avec un type de ressource foundation/components/image sont pris en compte pour inclusion.

* ***includeVideos - Booléen*** - Une propriété booléenne facultative détermine si les vidéos doivent être incluses. La valeur par défaut est *true*.

* ***includeModifiedPagesOnly - Booléen*** - Si la valeur est false ou si elle est omise, toutes les pages sont rendues et vérifiez les mises à jour dans le rendu. Si la valeur est true, la base diffère des modifications apportées à une page lastModified.
* ***+ rewrite (noeud)***
  ***- relativeParentPath - String*** : chemin d’accès pour écrire tous les autres chemins d’accès relatifs à .

>[!NOTE]
>
>Le type de ressource des composants image et vidéo affectés par ce gestionnaire est défini en configurant les propriétés de la propriété *com.adobe.cq.mobile.platform.impl.contentsync.handler*.*Service OSGi MobilePagesUpdateHandler*.

**mobilepageassets** Collecte des ressources de page d’application.

**mobilecontentlisting** Répertorie le contenu du fichier compressé ContentSync. Il est utilisé par le js côté client sur l’appareil pour effectuer la copie de fichier initiale requise pour les applications AEM.

Ce gestionnaire doit être ajouté à toute configuration ContentSync de l’application AEM.

* ***type - String - mobilecontentlisting***
* ***path*** - Chaîne : laissez vide. Doit être présent pour être considéré comme un gestionnaire valide, mais le chemin d’accès est déduit comme le cache ContentSync actuel. Cette valeur est ignorée.
* ***targetRootDirectory* -**Chaîne : préfixe à ajouter aux chemins en tant que racine cible pour la mise à jour du contenu de ce gestionnaire.
* ***order - Long* -**Ordre de ContentSync pour exécuter ce gestionnaire. Ce nombre doit être supérieur à tous les autres gestionnaires tels que 100. Il doit être exécuté après les gestionnaires de contenu traditionnels.

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

**mobilecontentpackageslisting** Répertorie le package de contenu AEM dans une application donnée et le serverURL vers lequel effectuer les requêtes de mise à jour. Il est utilisé par les js côté client sur l’appareil pour demander des mises à jour de contenu.

Le gestionnaire doit être utilisé sur AEM Configuration ContentSync de l’interpréteur d’applications (noeud avec pge-type=app-instance).

* ***type - String - mobilecontentpackageslisting***
* ***path **-**Chaîne*** - Chemin d’accès à un shell d’application (noeud avec pge-type=app-instance).
* ***targetRootDirectory - String*** : préfixe à ajouter aux chemins d’accès en tant que racine cible pour la mise à jour du contenu de ce gestionnaire.
* ***order - Long* -**Ordre d’exécution de ContentSync pour ce gestionnaire. Ce nombre doit être supérieur à tous les autres gestionnaires tels que 100. Il doit être exécuté après les gestionnaires de contenu traditionnels.

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

**widgetconfig** Comprend un fichier config.xml mis à jour qui fusionne toutes les modifications effectuées via le centre de commandes avec un fichier config.xml fourni. Si ce gestionnaire n’est pas inclus, les détails de l’application qui sont modifiés via l’interface d’administration ne seront pas inclus dans le cache.

Ce gestionnaire doit être utilisé sur une configuration ContentSync de Shell d’application AEM (noeud avec pge-type=[app-instance]).

* ***type - String* - **widgetconfig
* ***path **-**Chaîne*** - Chemin d’accès à tout noeud enfant shell d’application (noeud avec pge-type=[app-instance]).
* ***targetRootDirectory - String*** : préfixe à ajouter aux chemins d’accès en tant que racine cible pour la mise à jour du contenu de ce gestionnaire.
* ***targetIconDirectory - String*** : répertoire dans lequel placer les icônes de l’application

**mobileADBMobileConfigJSON** Incluez le fichier ADBMobileConfig.JSON si le service de cloud AMS a été configuré.

Il est utilisé au moment de la compilation pour configurer le module externe AMS pour la prise en charge de l’analyse.

Le gestionnaire doit être utilisé sur AEM Configuration ContentSync de l’interpréteur d’applications (noeud avec pge-type=app-instance).

* ***type - String*** - mobileADBMobileConfigJSON
* ***path - String*** - Chemin d’accès à un shell d’application (noeud avec page-type=app-instance ou RT qui étend /libs/mobileapps/core/components/instance)
* ***targetRootDirectory - String*** : préfixe à ajouter aux chemins d’accès en tant que racine cible pour la mise à jour du contenu de ce gestionnaire.

**notificationsconfig** Extrait les configurations de notifications requises sur le périphérique. Les propriétés sont extraites de la configuration de service cloud de service Push correspondante associée à l’application.

Les propriétés non AEM dans le noeud jcr:content du service cloud sont extraites et ajoutées au noeud **page-notifications-config.json** Fichier JSON à inclure dans la racine www du contenu de l’application.

Les propriétés AEM sont celles qui sont placées dans un espace de noms avec &quot;cq&quot;, &quot;sling&quot; ou &quot;jcr&quot;. D’autres propriétés peuvent être exclues à l’aide de la propriété &quot;excludeProperties&quot; sur le noeud de configuration content-sync.

* ***type - String*** - notificationsconfig
* ***excludeProperties - String[]*** - propriétés à exclure

**contentsyncconfigcontent** Collecte le contenu d’une configuration ContentSync existante.

* ***type - String*** - contentsyncconfigcontent
* ***path - String*** - Chemin d’accès à l’un des :

   * autre configuration ContentSync
   * dans un module de contenu (utilisera sa propriété phonegap-exportTemplate pour trouver sa configuration ContentSync).
   * à une ressource mobile (app-content se trouve sous cette ressource et, si ces modules de contenu ont une propriété page-includeInBuild qui est vraie, phonegap-exportTemplate est utilisé pour trouver sa configuration ContentSync).

* ***autoCreateFirstUpdateBeforeImport - Booléen*** - si la valeur est true, créez une **update** dans la configuration cible avant l’importation si une fois n’existe pas déjà

* ***autoFillBeforeImport - Booléen*** - si la valeur est true, mettez à jour/remplissez la configuration cible avant d’importer
* ***configSuffix - String*** - chaîne à ajouter au chemin indiqué sur la propriété &quot;phonegap-exportTemplate&quot; de app-content. Vous pouvez l’utiliser pour distinguer différents modèles d’exportation. Par exemple, cette propriété peut être définie sur **&quot;-dev&quot;** pour indiquer que *&quot;/../../../appconfig-dev&quot;* doit être utilisé (par opposition à *&quot;/../../../appconfig&quot;*).

**app-assets** Inclut toutes les ressources associées à une instance d’application. Ce gestionnaire inclut toutes les ressources trouvées sous le chemin spécifié, ainsi que toutes les ressources référencées par la propriété appAssetPath d’une instance d’application.

* ***type - String*** - app-assets

* ***path **-**Chaîne*** : chemin d’accès à un emplacement sous une instance d’application où les ressources de l’application sont stockées

**mobileappoffers** Un nouveau gestionnaire de synchronisation de contenu a été introduit pour le cas d’utilisation de la personnalisation pour le rendu du contenu ciblé. Le gestionnaire &quot;mobileappoffers&quot; sait comment effectuer le rendu des offres cibles associées qui ont été créées par l’auteur du contenu. Le gestionnaire mobileappoffers étend le gestionnaire de mise à jour des pages abstraites. De ce fait, de nombreuses propriétés sont similaires. Les détails du gestionnaire mobileappoffers présentent les propriétés suivantes.

Le gestionnaire mobileappsoffers étend le gestionnaire mobileappspages et ajoute les propriétés suivantes :

* ***locationRoot - String*** : spécifiez l’emplacement de l’application mobile.
* ***includePageTypes - String*** - prend par défaut en charge cq/personalization/components/teaserpage et cq/personalization/components/offer
* ***selector - String*** - doit être défini sur tandt
* ***path - String***: chemin d’accès à la marque de la campagne

**mobileappconfig** Le gestionnaire de synchronisation de contenu mobileappconfig permet d’injecter des données JSON dans le fichier MobileAppsConfig.json. Pour enregistrer une classe de fournisseur, les développeurs ajouteront leur classe MobileAppsInfoProvider à la liste des fournisseurs. Le gestionnaire effectue une itération sur la liste de MobileAppsInfoProviders et permet au fournisseur d’injecter des données dans le fichier json résultant. La liste des propriétés prises en charge par ce gestionnaire est la suivante :

* ***path **-**Chaîne*** : chemin d’accès à un noeud d’instance d’application avec page-type=app-instance ou RT qui étend /libs/mobileapps/core/components/instance
* ***provider - String*** `[]` - la liste des MobileAppsInfoProviders pleinement qualifiés
* ***targetRootDirectory - String*** : répertoire dans lequel écrire le fichier MobileAppsConfig.json.
* **fileName - String** : nom facultatif du fichier auquel écrire le fichier JSON. Par défaut, il s’agit de MobileAppsConfig.json.

Il est possible que plusieurs gestionnaires mobileappconfig soient configurés chacun avec un ensemble unique de fournisseurs écrivant dans différents fichiers JSON.

### Test des gestionnaires de synchronisation de contenu {#testing-content-sync-handlers}

**Procédure de vérification de l’intégrité** Effacer le cache

* Effacer le cache
* Exécution de votre gestionnaire (mise à jour du cache)
* Exécutez à nouveau votre gestionnaire (le cache ne doit pas être mis à jour).

**Procédure de débogage**

* Exécution de votre configuration
* Exportation de votre configuration ou révision sur le périphérique
* Si le rendu échoue, vérifiez l’absence *styles/assets/libs* ou vérifier les mauvais chemins d’accès à *styles/assets/libs*

**Journalisation** Activation de la journalisation du débogage de synchronisation de contenu via les configurations de journalisation OSGI sur le package `com.day.cq.contentsync` Cela vous permet de suivre les gestionnaires exécutés et s’ils ont mis à jour le cache et signalé la mise à jour du cache.

## Ressources supplémentaires {#additional-resources}

Pour en savoir plus sur les rôles et les responsabilités d’un administrateur et d’un développeur, consultez les ressources ci-dessous :

* [Création pour Adobe PhoneGap Enterprise avec AEM](/help/mobile/phonegap.md)
* [Administration de contenu pour Adobe PhoneGap Enterprise avec AEM](/help/mobile/administer-phonegap.md)

>[!NOTE]
>
>Pour commencer à développer des applications AEM Mobile, cliquez sur [here](/help/mobile/getting-started-aem-mobile.md).
