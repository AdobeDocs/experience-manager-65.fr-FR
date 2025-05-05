---
title: Gestionnaires d’application prêts à l’emploi
description: Consultez cette page pour en savoir plus sur les gestionnaires prêts à l’emploi d’Adobe PhoneGap Enterprise avec AEM.
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
exl-id: e2ddf5d1-0f5b-4f3b-9666-0f388915730e
solution: Experience Manager
feature: Mobile
role: Admin
source-git-commit: 2dae56dc9ec66f1bf36bbb24d6b0315a5f5040bb
workflow-type: tm+mt
source-wordcount: '1387'
ht-degree: 0%

---

# Gestionnaires d’application prêts à l’emploi{#out-of-the-box-app-handlers}

{{ue-over-mobile}}

Consultez les instructions suivantes pour développer des gestionnaires de synchronisation de contenu :

* Les gestionnaires doivent mettre en œuvre *com.day.cq.contentsync.handler.ContentUpdateHandler* (directement ou en étendant une classe qui le fait)
* Les gestionnaires peuvent étendre *com.adobe.cq.mobile.platform.impl.contentsync.handler.AbstractSlingResourceUpdateHandler*
* Le gestionnaire ne doit renvoyer la valeur true que s’il a mis à jour le cache ContentSync. Signaler faux vrai permettra à AEM de créer une mise à jour.
* Le gestionnaire ne doit mettre à jour le cache que si le contenu a été modifié. N’écrivez pas dans le cache si un blanc n’est pas nécessaire, afin d’éviter toute création de mise à jour inutile.

## Gestionnaires prêts à l’emploi {#out-of-the-box-handlers}

Les listes suivantes répertorient les gestionnaires d’application prêts à l’emploi :

**mobileapppages** Effectue le rendu des pages d’application.

* ***type - String*** - mobileapppages
* ***path - String*** - Chemin d’accès à une page
* ***extension - Chaîne*** - Extension qui doit être utilisée dans la requête. Pour les pages, cette fonctionnalité est presque toujours *html*, mais d’autres sont toujours possibles.

* ***selector - String*** - Sélecteurs facultatifs séparés par un point. Les exemples les plus courants sont *touch* pour le rendu des versions mobiles d’une page.

* ***deep - Boolean*** - Propriété booléenne facultative déterminant si les pages enfants doivent également être incluses. La valeur par défaut est *true.*

* ***includeImages - Boolean*** - Propriété booléenne facultative déterminant si les images doivent être incluses. La valeur par défaut est *true*.

   * Par défaut, seuls les composants d’image dont le type de ressource est foundation/components/image sont pris en compte pour l’inclusion.

* ***includeVideos - Boolean*** - La propriété booléenne facultative détermine si les vidéos doivent être incluses. La valeur par défaut est *true*.

* ***includeModifiedPagesOnly - Booléen*** - Si la valeur est false ou omise, effectuer le rendu de toutes les pages et vérifier les mises à jour dans le rendu. Si la valeur est true, la base diffère selon les modifications apportées à une page lastModified.
* ***+ réécriture (nœud)***
  ***- relativeParentPath - String*** - Chemin d’écriture de tous les autres chemins d’accès relatifs à.

>[!NOTE]
>
>Le type de ressource des composants image et vidéo affectés par ce gestionnaire est défini en configurant les propriétés du *com.adobe.cq.mobile.platform.impl.contentsync.handler*.*Service OSGi MobilePagesUpdateHandler*.

**mobilepageassets** Collecte les ressources de page d’application.

**mobilecontentlisting** Répertorie le contenu du fichier zip ContentSync. Il est utilisé par le js côté client sur l’appareil pour effectuer la copie initiale du fichier requise pour les applications AEM.

Ce gestionnaire doit être ajouté à toute configuration de synchronisation de contenu d’applications AEM.

* ***type - String - mobilecontentlisting***
* ***path*** - Chaîne - laissez vide ; doit être présent pour être considéré comme un gestionnaire valide, mais le chemin est déduit pour être le cache ContentSync actuel. Cette valeur est ignorée.
* ***targetRootDirectory* -**&#x200B;chaîne : préfixe à ajouter aux chemins d’accès en tant que racine cible pour la mise à jour du contenu de ce gestionnaire.
* ***order - Long* -**&#x200B;Ordre pour que ContentSync exécute ce gestionnaire. Ce nombre doit être supérieur à tous les autres gestionnaires, par exemple 100. Il doit être exécuté après les gestionnaires de contenu traditionnels.

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

**mobilecontentpackageslisting** Répertorie le package de contenu AEM dans une application donnée et l’URL du serveur vers lequel effectuer les demandes de mise à jour. Il est utilisé par le côté client sur l’appareil pour demander des mises à jour de contenu

Le gestionnaire doit être utilisé sur la configuration de la synchronisation du contenu de l’interpréteur d’applications AEM (nœud avec page-type=app-instance)

* ***type - String - mobilecontentpackageslisting***
* ***path &#x200B;**-**String*** - Chemin d’accès à un shell d’application (nœud avec pge-type=app-instance).
* ***targetRootDirectory - Chaîne*** - préfixe à ajouter aux chemins en tant que racine cible pour la mise à jour du contenu de ce gestionnaire.
* ***order - Long* -**&#x200B;Ordre d’exécution de ce gestionnaire par ContentSync. Ce nombre doit être supérieur à tous les autres gestionnaires, par exemple 100. Il doit être exécuté après les gestionnaires de contenu traditionnels.

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

**widgetconfig** comprend un fichier config.xml mis à jour qui fusionne toutes les modifications effectuées via le centre de commande avec un fichier config.xml fourni. Si ce gestionnaire n’est pas inclus, les détails de l’application qui sont modifiés via l’interface d’administration ne seront pas inclus dans le cache.

Ce gestionnaire doit être utilisé sur une configuration ContentSync d’AEM App Shell (nœud avec pge-type=[app-instance]).

* ***type - Chaîne* - &#x200B;** widgetconfig
* ***path &#x200B;**-**String*** - Chemin d’accès à un nœud enfant du shell de l’application (nœud avec pge-type=[app-instance]).
* ***targetRootDirectory - Chaîne*** - préfixe à ajouter aux chemins en tant que racine cible pour la mise à jour du contenu de ce gestionnaire.
* ***targetIconDirectory - Chaîne*** - Répertoire dans lequel placer les icônes de l’application

**mobileADBMobileConfigJSON** incluez le fichier ADBMobileConfig.JSON si le service cloud AMS a été configuré.

Ces informations sont utilisées au moment de la compilation pour configurer le plug-in AMS pour la prise en charge analytique.

Le gestionnaire doit être utilisé sur la configuration de la synchronisation du contenu de l’interpréteur d’applications AEM (nœud avec page-type=app-instance)

* ***type - Chaîne*** - mobileADBMobileConfigJSON
* ***path - String*** - Chemin d’accès à un shell d’application (nœud avec pge-type=app-instance ou un RT qui étend /libs/mobileapps/core/components/instance)
* ***targetRootDirectory - Chaîne*** - préfixe à ajouter aux chemins en tant que racine cible pour la mise à jour du contenu de ce gestionnaire

**notificationsconfig** Extrait les configurations de notifications requises sur l’appareil. Les propriétés sont extraites de la configuration de service cloud correspondante du service push associée à l’application.

Les propriétés non AEM dans le nœud jcr:content du service cloud sont extraites et ajoutées au fichier JSON **pge-notifications-config.json** pour inclusion dans la racine www du contenu de l’application.

Les propriétés AEM sont celles dont le nom est espacé de « cq », « sling » ou « jcr ». D’autres propriétés peuvent être exclues à l’aide de la propriété « excludeProperties » sur le nœud de configuration de synchronisation de contenu .

* ***type - Chaîne*** - notificationsconfig
* ***excludeProperties - String[]*** - propriétés à exclure

**contentsyncconfigcontent** collecte le contenu d’une configuration ContentSync existante.

* ***type - Chaîne*** - contentsyncconfigcontent
* ***path - String*** - Chemin d’accès à l’un des éléments suivants :

   * une autre configuration ContentSync ;
   * vers un package de contenu (utilisera sa propriété phonegap-exportTemplate pour trouver sa configuration ContentSync).
   * vers une ressource mobile (le de app-content se trouve sous cette ressource et, si ces packages de contenu ont une propriété page-includeInBuild définie sur true, phonegap-exportTemplate est utilisé pour rechercher sa configuration ContentSync).

* ***autoCreateFirstUpdateBeforeImport - Booléen*** - si vrai, créez une **mise à jour** initiale dans la configuration cible avant l’importation si elle n’existe pas déjà une fois

* ***autoFillBeforeImport - Booléen*** - Si la valeur est true, mettez à jour/remplissez la configuration cible avant l’importation
* ***configSuffix - Chaîne*** - chaîne à ajouter au chemin d’accès indiqué sur la propriété « phonegap-exportTemplate » de app-content. Vous pouvez l’utiliser pour distinguer différents modèles d’exportation. Par exemple, cette propriété peut être définie sur **« -dev »** pour indiquer que *« /../../../appconfig-dev »* doit être utilisé (par opposition à *« /../../appconfig »*).

**app-assets** Inclut toutes les ressources associées à une instance d’application. Ce gestionnaire inclut toutes les ressources trouvées sous le chemin spécifié avec toutes les ressources référencées par la propriété appAssetPath d’une instance d’application.

* ***type - Chaîne*** - app-assets

* ***path &#x200B;**-**String*** - Chemin d’accès à un emplacement sous une instance d’application où les ressources d’application sont stockées

**mobileappoffers** Un nouveau gestionnaire de synchronisation de contenu a été introduit pour le cas d’utilisation de Personalization afin de générer le contenu ciblé. Le gestionnaire « mobileappoffers » sait comment effectuer le rendu des offres cibles associées qui ont été créées par l’auteur du contenu. Le gestionnaire mobileappoffers étend le gestionnaire de mise à jour des pages abstraites. De ce fait, de nombreuses propriétés sont similaires. Les détails du gestionnaire mobileappOffers possèdent les propriétés suivantes.

Le gestionnaire mobileapppers étend le gestionnaire mobileapppages et ajoute les propriétés suivantes :

* ***locationRoot - Chaîne*** - spécifiez l’emplacement de l’application mobile
* ***includePageTypes - Chaîne*** - La valeur par défaut prend en charge cq/personalization/components/teaserpage et cq/personalization/components/offerproxy
* ***selector - String*** - doit être défini sur tandt
* ***path - String***- Chemin d’accès à la marque de la campagne

**mobileappconfig** Le gestionnaire de synchronisation de contenu mobileappconfig permet d’injecter des données JSON dans le fichier MobileAppsConfig.json. Pour enregistrer une classe de fournisseur, les développeurs ajouteront leur classe MobileAppsInfoProvider à la liste des fournisseurs. Le gestionnaire effectue une itération sur la liste des MobileAppsInfoProviders et permet au fournisseur d’injecter des données dans le fichier json obtenu. La liste des propriétés prises en charge par ce gestionnaire est la suivante :

* ***path &#x200B;**-**String*** - Chemin d’accès à un nœud d’instance d’application avec pge-type=app-instance ou un RT qui étend /libs/mobileapps/core/components/instance
* ***providers - Chaîne*** `[]` - liste des MobileAppsInfoProviders entièrement qualifiés
* ***targetRootDirectory - Chaîne*** - Répertoire dans lequel écrire le fichier MobileAppsConfig.json.
* **fileName - String** - nom facultatif du fichier dans lequel écrire le fichier JSON, par défaut MobileAppsConfig.json

Il est possible de configurer plusieurs gestionnaires mobileappconfig avec un ensemble unique de fournisseurs qui écrivent dans différents fichiers JSON.

### Test des gestionnaires de synchronisation de contenu {#testing-content-sync-handlers}

**Étapes de vérification de l’intégrité** Effacer le cache

* Effacer le cache
* Exécuter le gestionnaire (mise à jour du cache)
* Réexécutez le gestionnaire (le cache ne doit pas être mis à jour).

**Étapes de débogage**

* Exécuter la configuration
* Exportation de votre configuration ou révision sur un appareil
* Si le rendu échoue, recherchez les *styles/assets/libs* manquants ou les chemins d’accès incorrects vers *styles/assets/libs*

**Journalisation** Activez la journalisation du débogage ContentSync via les configurations de l’enregistreur OSGI sur le package `com.day.cq.contentsync`. Vous pourrez ainsi suivre l’exécution des gestionnaires et s’ils ont mis à jour le cache et signalé la mise à jour du cache.

## Ressources supplémentaires {#additional-resources}

Pour en savoir plus sur les rôles et les responsabilités d’un administrateur et d’un développeur, consultez les ressources ci-dessous :

* [Création pour Adobe PhoneGap Enterprise avec AEM](/help/mobile/phonegap.md)
* [Administration de contenu pour Adobe PhoneGap Enterprise avec AEM](/help/mobile/administer-phonegap.md)

>[!NOTE]
>
>Pour commencer à développer des applications AEM Mobile, cliquez [ici](/help/mobile/getting-started-aem-mobile.md).
