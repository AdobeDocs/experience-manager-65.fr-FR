---
title: 'Exemples de magasins candidats ContextHub '
seo-title: 'Exemples de magasins candidats ContextHub '
description: ContextHub fournit plusieurs exemples de magasins candidats que vous pouvez utiliser dans vos solutions
seo-description: ContextHub fournit plusieurs exemples de magasins candidats que vous pouvez utiliser dans vos solutions
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
translation-type: tm+mt
source-git-commit: 80b8571bf745b9e7d22d7d858cff9c62e9f8ed1e
workflow-type: tm+mt
source-wordcount: '490'
ht-degree: 95%

---


# Exemples de magasins candidats ContextHub {#sample-contexthub-store-candidates}

ContextHub fournit plusieurs exemples de magasins candidats que vous pouvez utiliser dans vos solutions. Les informations suivantes sont fournies pour chaque exemple :

* L’emplacement du code source pour pouvoir l’ouvrir à des fins de formation.
* La configuration des magasins créés à partir des magasins candidats.
* La structure des données de magasin pour pouvoir y accéder.

>[!WARNING]
>
>Les exemples de magasins candidats sont fournis comme configurations de référence pour vous aider à créer votre propre configuration dédiée pour votre projet. Ils ne doivent donc pas être utilisés directement.

## Exemple de magasin candidat aem.segmentation {#aem-segmentation-sample-store-candidate}

Magasin pour les segments ContextHub résolus et non résolus. Récupère automatiquement les segments de SegmentManager ContextHub.

### Emplacement du code source {#source-location-segmentation}

`/libs/settings/cloudsettings/legacy/contexthub/segmentation`

### Implémentation de base {#base-implementation-segmentation}

Le magasin candidat aem.segmentation étend [`ContextHub.Store.PersistedJSONPStore`](/help/sites-developing/contexthub-api.md#contexthub-store-persistedjsonpstore).

### Configuration {#configuration-segmentation}

Lorsque vous créez un magasin aem.segmentation, vous n’avez pas besoin de fournir une configuration détaillée. La configuration par défaut spécifie l’emplacement des définitions de segment ContextHub.

```xml
{
   "service":{
      "jsonp":false,
      "timeout":1000,
      "path":"/etc/segmentation/contexthub.segment.js"
   }
}
```

## Exemple de magasin candidat contexthub.geolocation {#contexthub-geolocation-sample-store-candidate}

Le magasin candidat de modèles contexthub.geolocation utilise Google Maps pour obtenir et stocker des informations sur l’emplacement du client.

### Emplacement du code source {#source-location-geolocation}

`/libs/settings/cloudsettings/legacy/contexthub/geolocation`

### Implémentation de base {#base-implementation-geolocation}

Le candidat du magasin contexthub.geolocation s&#39;étend [`ContextHub.Store.PersistedJSONPStore`](/help/sites-developing/contexthub-api.md#contexthub-store-persistedjsonpstore).

### Configuration {#configuration-geolocation}

La configuration par défaut spécifie des informations sur le service Google et les coordonnées de latitude et de longitude initiales.

```xml
{
        "service": {
            "jsonp": false,
            "timeout": 1000,
            "ttl": 1800000,
            "secure": false,
            "host": "maps.googleapis.com",
            "port": 80,
            "path": "/maps/api/geocode/json"
        },

        "eventDeferring": 16,

        "html5coordinatesDiscoveryAPI": {
            "timeout": 30000,
            "ttl": 900000,
            "highAccuracy": false
        },

        "initialValues": {
            "latitude": 37.331375,
            "longitude": -121.893992
        }
    }
```

### Éléments de données {#data-items-geolocation}

Le magasin utilise une arborescence de données similaire à l’exemple suivant :

```xml
{
   "latitude":"37.331375",
   "longitude":"-121.893992"
}
```

>[!NOTE]
>
>Une stratégie de sécurité introduite dans Chrome 50.x requiert que tous les appels liés à la géolocalisation soient effectués via une connexion sécurisée. Par conséquent, AEM force l’utilisation de https pour les appels d’API de géolocalisation si AEM s’exécute également sur https. Sinon, http est utilisé afin de respecter la politique de même origine. Voir [cet article de blog Google](https://developers.google.com/web/updates/2016/04/geolocation-on-secure-contexts-only) pour plus de détails sur les changements dans Chrome.

## Exemple de magasin candidat contexthub.surferinfo  {#contexthub-surferinfo-sample-store-candidate}

Stocke des informations sur l’environnement client actuel, telles que l’appareil, la fenêtre, le navigateur, la date et l’heure.

### Emplacement du code source {#source-location-surferinfo}

`/libs/settings/cloudsettings/legacy/contexthub/surferinfo`

### Implémentation de base {#base-implementation-surferinfo}

Le candidat du magasin contexthub.datetime étend [`ContextHub.Store.PersistedStore`](/help/sites-developing/contexthub-api.md#contexthub-store-persistedstore).

### Configuration {#configuration-surferinfo}

La configuration par défaut est héritée de `ContextHub.Store.PersistedStore`.

### Éléments de données {#data-items-surferinfo}

Les magasins qui utilisent ce magasin candidat ont un arbre de données similaire à l’exemple suivant :

```xml
{
   "display":{
      "resolution":{
         "width":1440,
         "height":900
      },
      "devicePixelRatio":1,
      "colorDepth":24,
      "nrOfColors":16777216,
      "pixelsPerInch":96,
      "orientation":{
         "mode":"landscape",
         "direction":"normal"
      }
   },
   "window":{
      "dimension":{
         "width":1395,
         "height":652
      },
      "percentageUsage":0.7
   },
   "browser":{
      "version":"39.0",
      "family":"Firefox",
      "userAgent":"Mozilla/5.0 (Macintosh; Intel Mac OS X 10.9; rv:39.0) Gecko/20100101 Firefox/39.0"
   },
   "device":{
      "category":"Desktop",
      "type":"Desktop",
      "model":"PC",
      "version":""
   },
   "isMobile":true,
   "os":{
      "name":"Mac OS X",
      "version":"10"
   },
   "year":2015,
   "month":7,
   "day":22,
   "hour":14,
   "minutes":1
}
```

## Exemple de magasin candidat granite.emulators {#granite-emulators-sample-store-candidate}

L’exemple de magasin candidat granite.emulators stocke des informations sur les appareils clients.

### Emplacement du code source {#source-location-emulators}

`/libs/settings/cloudsettings/legacy/contexthub/emulators`

### Implémentation de base {#base-implementation-emulators}

Le candidat du magasin contexthub.geolocation s&#39;étend [`ContextHub.Store.PersistedStore`](/help/sites-developing/contexthub-api.md#contexthub-store-persistedstore).

### Configuration {#configuration-emulators}

La configuration par défaut inclut un tableau nommé `defaultEmulators` qui contient des informations sur différents appareils. Lorsque vous créez un magasin, fournissez des profils d’appareil différents dans la propriété Configuration détaillée selon les besoins, en respectant le format illustré dans l’exemple suivant :

```xml
{
   "defaultEmulators":[
        {
            "id": "iphone-6",
            "title": "iPhone 6",
            "type": "mobile",
            "platform": "iOS",
            "platformVersion": "8.1.3",
            "width": 750,
            "height": 1334,
            "canRotate": true,
            "orientation": "Portrait",
            "device-pixel-ratio": 2
        },
        {
            "id": "iphone-6-plus",
            "title": "iPhone 6 Plus",
            "type": "mobile",
            "platform": "iOS",
            "platformVersion": "8.1.3",
            "width": 1080,
            "height": 1920,
            "canRotate": true,
            "orientation": "Portrait",
            "device-pixel-ratio": 3
        },
        {
            "id": "galaxy-s4",
            "title": "Samsung Galaxy S4",
            "type": "mobile",
            "platform": "Android",
            "platformVersion": "4.4.2 KitKat",
            "width": 1080,
            "height": 1920,
            "canRotate": true,
            "orientation": "Portrait",
            "device-pixel-ratio": 3
        }
    ]
}
```

### Éléments de données {#data-items-emulators}

L’arborescence de données de magasin est similaire à l’exemple suivant :

```xml
{
   "devices":[
      {"id":"native",
      "title":"Native",
      "type":"screen",
      "width":1395,
      "height":374,
      "orientation":"Landscape",
      "platform":"Mac OS X",
      "platformVersion":"10",
      "canRotate":false
      },
      {"id":"ipad-3",
      "title":"iPad 3 / 4 / Air",
      "type":"tablet",
      "platform":"iOS",
      "platformVersion":"8.1.3",
      "width":1536,
      "height":2048,
      "canRotate":true,
      "orientation":"Portrait",
      "device-pixel-ratio":2
      },
      {"id":"iphone-6",
      "title":"iPhone 6",
      "type":"mobile",
      "platform":"iOS",
      "platformVersion":"8.1.3",
      "width":750,
      "height":1334,
      "canRotate":true,
      "orientation":"Portrait",
      "device-pixel-ratio":2
      },
      {"id":"galaxy-s4",
      "title":"Samsung Galaxy S4",
      "type":"mobile",
      "platform":"Android",
      "platformVersion":"4.4.2 KitKat",
      "width":1080,
      "height":1920,
      "canRotate":true,
      "orientation":"Portrait",
      "device-pixel-ratio":3
      }
   ],
   "currentDeviceId":"native",
   "orientations":[
      {"id":"landscape",
      "title":"Landscape"
      },
      {"id":"portrait",
       "title":"Portrait"
      }
   ],
   "currentDevice":{
      "id":"native",
      "title":"Native",
      "type":"screen",
      "width":1395,
      "height":374,
      "orientation":"Landscape",
      "platform":"Mac OS X",
      "platformVersion":"10",
      "canRotate":false
   }
}
```

## Exemple de magasin candidat granite.profile   {#granite-profile-sample-store-candidate}

Stocke des informations sur l’utilisateur actuel.

### Emplacement du code source {#source-location-profile}

`/libs/settings/cloudsettings/legacy/contexthub/profile`

### Implémentation de base {#base-implementation-profile}

Le candidat du magasin contexthub.datetime étend [`ContextHub.Store.PersistedJSONPStore`](/help/sites-developing/contexthub-api.md#contexthub-store-persistedjsonpstore).

### Configuration {#configuration-profile}

La configuration par défaut suivante est utilisée. Vous ne devriez pas changer cette configuration.

```xml
{
   "service":{
      "jsonp":false,
      "timeout":1000,
      "path":"${contexthub:/store/profile/path}.infinity.json"
   },
   "initialValues":{"path":"/home/users/a/anonymous"}
}
```

### Éléments de données {#data-items-profile}

Les magasins qui utilisent ce magasin candidat ont un arbre de données similaire à l’exemple suivant :

```xml
{
   "displayName":"anonymous",
   "path":"/home/users/6/6zavE_DGre6Ad9Y5E0Ba",
   "avatar":"/etc/designs/default/images/social/avatar.png",
   "authorizableId":"anonymous"
}
```
