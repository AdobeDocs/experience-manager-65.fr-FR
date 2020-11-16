---
title: Gestionnaires d’applications prêts à l’emploi
seo-title: Gestionnaires d’applications prêts à l’emploi
description: Suivez cette page pour en savoir plus sur les gestionnaires prêts à l’emploi pour Adobe PhoneGap Enterprise avec AEM.
seo-description: Suivez cette page pour en savoir plus sur les gestionnaires prêts à l’emploi pour Adobe PhoneGap Enterprise avec AEM.
uuid: 436038cb-fb76-4bb5-ae79-5d4043b81dd9
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: developing-adobe-phonegap-enterprise
discoiquuid: fec86f03-f81e-460a-9f84-d6304c95128c
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '1430'
ht-degree: 2%

---


# Gestionnaires d’applications prêts à l’emploi{#out-of-the-box-app-handlers}

>[!NOTE]
>
>Adobe recommande d’utiliser l’éditeur d’application d’une seule page (SPA) pour les projets nécessitant un rendu côté client basé sur la structure SPA (par exemple, React). [En savoir plus](/help/sites-developing/spa-overview.md).

Consultez les instructions suivantes pour le développement de gestionnaires de synchronisation de contenu :

* Les gestionnaires doivent implémenter *com.day.cq.contentsync.handler.ContentUpdateHandler* (directement ou en étendant une classe qui le fait)
* Les gestionnaires peuvent étendre *com.adobe.cq.mobile.platform.impl.contentsync.handler.AbstractSlingResourceUpdateHandler*
* Le gestionnaire ne doit signaler la valeur true que s’il a mis à jour le cache ContentSync. Un rapports erroné sur true permet AEM créer une mise à jour.
* Le gestionnaire ne doit mettre à jour le cache que si le contenu a réellement changé. N’écrivez pas dans le cache si un blanc n’est pas nécessaire et évitez une création de mise à jour inutile.

## Gestionnaires prêts à l&#39;emploi {#out-of-the-box-handlers}

Les gestionnaires d’applications prêts à l’emploi suivants sont disponibles :

**mobileapppages** Rendu des pages d’application.

* ***type - Chaîne*** - mobileapppages
* ***chemin - Chaîne*** - chemin d&#39;accès à une page
* ***extension - Chaîne*** - Extension qui doit être utilisée dans la requête. Pour les pages, c&#39;est presque toujours du *html*, mais d&#39;autres sont toujours possibles.

* ***selector - String*** - Sélecteurs facultatifs séparés par un point. Les exemples courants sont *tactiles* pour le rendu des versions mobiles d’une page.

* ***deep - Boolean*** - Propriété booléenne facultative déterminant si les pages enfants doivent également être incluses. La valeur par défaut est *true.*

* ***includeImages - Boolean*** - Propriété booléenne facultative déterminant si les images doivent être incluses. La valeur par défaut est *true*.

   * Par défaut, seuls les composants d’image avec un type de ressource de fondation/composants/image sont pris en compte pour l’inclusion.

* ***includeVideos - Boolean*** - Une propriété booléenne facultative détermine si les vidéos doivent être incluses. La valeur par défaut est *true*.

* ***includeModifiedPagesOnly - Boolean*** - Si la valeur est false ou omise, effectuez le rendu de toutes les pages et vérifiez les mises à jour dans le rendu. Si la valeur est true, la base diffère en fonction des modifications apportées à une page lastModified.
* ***+ rewrite (noeud)***
   ***- relativeParentPath - String*** - le chemin d&#39;accès par lequel écrire tous les autres chemins relatifs.

>[!NOTE]
>
>Le type de ressource des composants image et vidéo affectés par ce gestionnaire est défini en configurant les propriétés du *com.adobe.cq.mobile.platform.impl.contentsync.handler*.*Service* OSGi MobilePagesUpdateHandler.

**mobilepageassets** Collecte des ressources de page d’application.

**mobilecontentlisting** Liste le contenu du fichier compressé ContentSync. Il est utilisé par les js côté client sur le périphérique pour effectuer la copie de fichier initiale requise pour les applications AEM.

Ce gestionnaire doit être ajouté à toute configuration ContentSync d&#39;AEM applications.

* ***type - Chaîne - mobilecontentlisting***
* ***chemin*** - Chaîne - rester vide, doit être présent pour être considéré comme un gestionnaire valide, mais le chemin d&#39;accès est déduit comme étant le cache ContentSync actuel. Cette valeur est ignorée.
* ***targetRootDirectory* -**Chaîne : préfixe à ajouter aux chemins en tant que racine de cible pour la mise à jour du contenu de ce gestionnaire.
* ***order - Long* -**Order for ContentSync to excute this handler. Ce nombre doit être supérieur à tous les autres gestionnaires tels que 100. Il doit être exécuté après les gestionnaires de contenu traditionnels.

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

**mobilecontentpackagesrépertorie** les Listes du package de contenu AEM dans une application donnée ainsi que l’URL de serveur à laquelle envoyer les demandes de mise à jour. Il est utilisé dans les js côté client sur le périphérique pour demander des mises à jour de contenu.

Le gestionnaire doit être utilisé sur AEM App Shell ContentSync Config (noeud avec pge-type=app-instance)

* ***type - Chaîne - mobilecontentpackageslisting***
* ***chemin **-**Chaîne*** - Chemin d’accès à un shell d’application (noeud avec pge-type=app-instance).
* ***targetRootDirectory - String*** - préfixe à ajouter aux chemins en tant que racine de cible pour la mise à jour du contenu de ce gestionnaire.
* ***order - Long* -**Order for ContentSync to execute this handler. Ce nombre doit être supérieur à tous les autres gestionnaires tels que 100. Il doit être exécuté après les gestionnaires de contenu traditionnels.

>[!NOTE]
>
>Le bloc de code suivant n&#39;est pas une implémentation exacte et doit être utilisé comme exemple de référence :

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

**widgetconfig** comprend un fichier config.xml mis à jour qui fusionne toutes les modifications effectuées via le Centre de commandes avec un fichier config.xml fourni. Si ce gestionnaire n’est pas inclus, les détails de l’application qui sont modifiés par l’interface d’administration ne seront pas inclus dans le cache.

Ce gestionnaire doit être utilisé sur une configuration ContentSync AEM Shell (noeud avec pge-type=[app-instance]).

* ***type - Chaîne* - **widgetconfig
* ***chemin **-**Chaîne*** - Chemin d’accès à tout noeud enfant du shell d’application (noeud avec pge-type=[app-instance]).
* ***targetRootDirectory - String*** - préfixe à ajouter aux chemins en tant que racine de cible pour la mise à jour du contenu de ce gestionnaire.
* ***targetIconDirectory - Chaîne*** - répertoire dans lequel placer les icônes de l&#39;application

**mobileADBMobileConfigJSON** Incluez le fichier ADBMobileConfig.JSON si le service de cloud AMS a été configuré.

Cette méthode est utilisée au moment de la compilation pour configurer le module externe AMS pour la prise en charge des analyses.

Le gestionnaire doit être utilisé sur AEM App Shell ContentSync Config (noeud avec pge-type=app-instance)

* ***type - Chaîne*** - mobileADBMobileConfigJSON
* ***chemin - Chaîne*** - Chemin d’accès à un shell d’application (noeud avec pge-type=app-instance ou RT qui étend /libs/mobileapps/core/components/instance)
* ***targetRootDirectory - String*** - préfixe à ajouter aux chemins en tant que racine de cible pour la mise à jour du contenu de ce gestionnaire

**notifications** config Extrait les configurations de notifications requises sur le périphérique. Les propriétés sont extraites de la configuration du service cloud de service Push correspondant associée à l’application.

Les propriétés non-AEM du noeud jcr:content du service cloud sont extraites et ajoutées au fichier JSON **page-notifications-config.json** pour inclusion dans la racine www du contenu de l’application.

Les propriétés AEM sont celles qui sont espacées par un nom avec &quot;cq&quot;, &quot;sling&quot; ou &quot;jcr&quot;. D’autres propriétés peuvent être exclues à l’aide de la propriété &quot;excludeProperties&quot; sur le noeud de configuration content-sync.

* ***type - Chaîne*** - notification-config
* ***excludeProperties - String[]*** - propriétés à exclure

**contentsyncconfigcontent** Collecte le contenu d’une configuration ContentSync existante.

* ***type - Chaîne*** - contentsyncconfigcontent
* ***chemin - Chaîne*** - Chemin d&#39;accès à l&#39;un des éléments suivants :

   * autre configuration ContentSync
   * à un package de contenu (utilisera sa propriété phonegap-exportTemplate pour trouver sa configuration ContentSync)
   * à une ressource Mobile (les contenus d’application se trouvent sous cette ressource et, si ces packages de contenu ont une propriété page-includeInBuild vraie, phonegap-exportTemplate sera utilisé pour trouver sa configuration ContentSync)

* ***autoCreateFirstUpdateBeforeImport - Boolean*** - si true, créez une **mise à jour** initiale dans la configuration de la cible avant d’importer si une fois n’existe pas déjà.

* ***autoFillBeforeImport - Boolean*** - si true, mettez à jour/remplissez la configuration de cible avant d&#39;importer
* ***configSuffix - String*** - chaîne à ajouter au chemin indiqué sur la propriété &quot;phonegap-exportTemplate&quot; de app-content. Vous pouvez l’utiliser pour distinguer différents modèles d’exportation. Par exemple, cette propriété peut être définie sur **&quot;-dev&quot;** pour indiquer que *&quot;/../../../appconfig-dev&quot;* doit être utilisée (par opposition à *&quot;/../../.../appconfig&quot;*).

**app-assets** Inclut tous les actifs associés à une instance d’application. Ce gestionnaire inclut tous les actifs trouvés sous le chemin d’accès spécifié ainsi que les actifs référencés par la propriété appAssetPath d’une instance d’application.

* ***type - Chaîne*** - app-assets

* ***chemin **-**Chaîne*** - chemin d’accès à un emplacement sous une instance d’application où les ressources de l’application sont stockées

**mobileappoffers** Un nouveau gestionnaire de synchronisation de contenu a été introduit pour le cas d’utilisation de la personnalisation pour le rendu du contenu ciblé. Le gestionnaire &quot;mobileappoffers&quot; sait comment générer les offres d’cible associées qui ont été créées par l’auteur du contenu. Le gestionnaire mobileappoffers étend le gestionnaire de mise à jour des pages abstraites. De ce fait, bon nombre des propriétés sont similaires. Les détails du gestionnaire mobileappoffers possèdent les propriétés suivantes.

Le gestionnaire mobileappsoffers étend le gestionnaire mobileappspages et ajoute les propriétés suivantes :

* ***locationRoot - Chaîne*** - indiquez l’emplacement de l’application mobile.
* ***includePageTypes - String*** - prend en charge par défaut cq/personalization/components/teaserpage et cq/personalization/components/offerproxy
* ***selector - String*** - doit être défini sur tandt
* ***chemin - Chaîne***- chemin d’accès à la marque de la campagne

**mobileappconfig** Le gestionnaire de synchronisation de contenu mobileappconfig permet d’injecter des données JSON dans le fichier MobileAppsConfig.json. Pour enregistrer un développeur de classe de fournisseur, vous devez ajouter sa classe MobileAppsInfoProvider à la liste des fournisseurs. Le gestionnaire effectue une itération sur la liste de MobileAppsInfoProviders et permet au fournisseur d&#39;injecter des données dans le fichier json résultant. La liste des propriétés que ce gestionnaire prend en charge est la suivante :

* ***chemin **-**Chaîne*** - chemin d’accès à un noeud d’instance d’application avec pge-type=app-instance ou un RT qui étend /libs/mobileapps/core/components/instance
* ***fournisseurs - Chaîne*** `[]` - liste de fournisseurs d&#39;informations MobileAppsInfoProviders pleinement qualifiés
* ***targetRootDirectory - String*** - répertoire dans lequel écrire le fichier MobileAppsConfig.json.
* **fileName - String** - Nom facultatif du fichier dans lequel écrire le fichier JSON, par défaut MobileAppsConfig.json

Il est possible de configurer plusieurs gestionnaires mobileappconfig chacun avec un ensemble unique de fournisseurs écrivant dans différents fichiers JSON.

### Test des gestionnaires de synchronisation de contenu {#testing-content-sync-handlers}

**Procédure de vérification de l’intégrité** Effacer le cache

* Effacer le cache
* Exécution de votre gestionnaire (mise à jour du cache)
* Réexécutez votre gestionnaire (le cache ne doit pas être mis à jour).

**Procédure de débogage**

* Exécutez votre configuration
* Exporter votre configuration ou votre révision sur le périphérique
* Si le rendu échoue, recherchez les *styles/ressources/libs* manquants ou recherchez les chemins incorrects vers les *styles/ressources/libs.*

**Journalisation** Activer la journalisation du débogage de ContentSync via les configurations de journalisation OSGI sur le package `com.day.cq.contentsync` Vous pourrez ainsi suivre les gestionnaires exécutés et s’ils ont mis à jour le cache et signalé la mise à jour du cache.

## Ressources supplémentaires {#additional-resources}

Pour en savoir plus sur les rôles et les responsabilités d’un administrateur et d’un développeur, consultez les ressources ci-dessous :

* [Création pour Adobe PhoneGap Enterprise avec AEM](/help/mobile/phonegap.md)
* [Administration de contenu pour Adobe PhoneGap Enterprise avec AEM](/help/mobile/administer-phonegap.md)

>[!NOTE]
>
>Pour commencer à développer des applications AEM Mobile, cliquez [ici](/help/mobile/getting-started-aem-mobile.md).

