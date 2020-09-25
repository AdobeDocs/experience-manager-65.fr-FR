---
title: Ajout de ContextHub à des pages et accès à des magasins
description: Ajoutez ContextHub à vos pages pour activer les fonctionnalités ContextHub et créer un lien vers les bibliothèques JavaScript ContextHub.
translation-type: tm+mt
source-git-commit: a8ba56849f6bb9f0cf6571fc51f4b5cae71620e0
workflow-type: tm+mt
source-wordcount: '927'
ht-degree: 67%

---


# Ajout de ContextHub à des pages et accès à des magasins {#adding-contexthub-to-pages-and-accessing-stores}

ajoutez ContextHub sur vos pages pour activer les fonctionnalités ContextHub et pour créer un lien vers les bibliothèques Javascript ContextHub.

L’API JavaScript ContextHub permet d’accéder aux données contextuelles gérées par ContextHub. Cette page décrit brièvement les principales fonctionnalités de l’API pour l’accès et la manipulation des données contextuelles. Suivez les liens vers la documentation de référence de l’API pour consulter des informations détaillées et des exemples de code.

## Ajout de ContextHub à un composant de page {#adding-contexthub-to-a-page-component}

To enable the ContextHub features and to link to the ContextHub Javascript libraries, include the `contexthub` component in the `head` section of your page. Le code HTML de votre composant de page doit ressembler à l’exemple suivant :

```xml
<sly data-sly-resource="${'contexthub' @ resourceType='granite/contexthub/components/contexthub'}"/>
```

Notez que vous devez également déterminer si la barre d’outils ContextHub apparaît ou non dans le mode Aperçu. Voir [Affichage et masquage de l’IU ContextHub](ch-configuring.md#showing-and-hiding-the-contexthub-ui).

## À propos des magasins ContextHub {#about-contexthub-stores}

Utilisez des magasins ContextHub pour conserver des données contextuelles. ContextHub fournit les types de magasins suivants, qui constituent la base de tous les types :

* [PersistedStore](contexthub-api.md#contexthub-store-persistedstore)
* [SessionStore](contexthub-api.md#contexthub-store-sessionstore)
* [JSONPStore](contexthub-api.md#contexthub-store-persistedjsonpstore)
* [PersistedJSONPStore](contexthub-api.md#contexthub-store-persistedstore)

Tous les types de magasins sont des extensions de la classe [`ContextHub.Store.Core`](contexthub-api.md#contexthub-store-core). Pour plus d’informations sur la création d’un type de magasin, voir [Création de magasins personnalisés](ch-extend.md#creating-custom-store-candidates). Pour plus d’informations sur les exemples de types de magasins, voir [Exemples de candidats au titre de magasins ContextHub](ch-samplestores.md).

### Modes de persistance {#persistence-modes}

Les magasins ContextHub utilisent l’un des modes de persistance suivants :

* **Local** : utilise HTML5 localStorage pour conserver les données. L’espace de stockage local est conservé sur le navigateur entre les sessions.
* **Session :** Utilise le stockage de session HTML5 pour conserver les données. Le stockage de session est conservé pendant toute la durée de la session du navigateur et est disponible dans toutes les fenêtres du navigateur.
* **Cookie** : utilise la prise en charge native des cookies du navigateur pour le stockage des données. Les données de cookie sont échangées avec le serveur dans des requêtes HTTP.
* **Window.name** : utilise la propriété window.name pour conserver les données.
* **Mémoire** : utilise un objet JavaScript pour conserver les données.

Par défaut, ContextHub utilise le mode de persistance Local. Si le navigateur ne prend pas en charge ni n’autorise HTML5 localStorage, la persistance de session est utilisée. Si le navigateur ne prend pas en charge ni n’autorise HTML5 sessionStorage, la persistance Window.name est utilisée.

### Données du magasin {#store-data}

En interne, les données de magasin forment une structure arborescente, ce qui permet d’ajouter des valeurs en tant qu’objets complexes ou que types principaux. Lorsque vous ajoutez des objets complexes à des magasins, leurs propriétés forment des branches dans l’arborescence de données. Par exemple, l’objet complexe suivant est ajouté à une boutique vide nommée emplacement :

```javascript
Object {
   number: 321,
   data: {
      city: "Basel",
      country: "Switzerland",
      details: {
         population: 173330,
         elevation: 260
      }
   }
}
```

La structure arborescente du magasin peut être conceptualisée comme suit :

```text
/
|- number
|- data
      |- city
      |- country
      |- details
            |- population
            |- elevation
```

La structure arborescente définit les éléments de données du magasin sous la forme de paires clé/valeur. In the above example, the key `/number` corresponds with the value `321`, and the key `/data/country` corresponds with the value `Switzerland`.

### Manipulation d’objets {#manipulating-objects}

ContextHub provides the [`ContextHub.Utils.JSON.tree`](contexthub-api.md#contexthub-utils-json-tree) class for manipulating Javascript objects. Utilisez les fonctions de cette classe pour manipuler des objets JavaScript avant de les ajouter à un magasin ou après les avoir récupérés d’un magasin.

Additionally, the [`ContextHub.Utils.JSON`](contexthub-api.md#contexthub-utils-json) class provides functions for serializing objects to stings, and deserializing strings to objects. Use this class for handling JSON data to support browsers that do not natively include the `JSON.parse` and `JSON.stringify` functions.

## Interaction avec les magasins ContextHub {#interacting-with-contexthub-stores}

Utilisez l’objet JavaScript [`ContextHub`](contexthub-api.md#ui-event-constants) pour obtenir un magasin comme objet JavaScript. Une fois que vous avez obtenu l’objet de magasin, vous pouvez manipuler les données qu’il contient. Use the [`getAllStores`](contexthub-api.md#getallstores) or the [`getStore`](contexthub-api.md#getstore-name) function to obtain the store.

### Accès aux données du magasin {#accessing-store-data}

The [`ContexHub.Store.Core`](contexthub-api.md#contexthub-store-core) Javascript class defines several functions for interacting with store data. Les fonctions suivantes stockent et récupèrent plusieurs éléments de données contenus dans des objets :

* [addAllItems](contexthub-api.md#addallitems-tree-options)
* [getTree](contexthub-api.md#gettree-includeinternals)

Les différents éléments de données sont stockés sous la forme d’un ensemble de paires clé/valeur. Pour stocker et récupérer des valeurs, spécifiez la clé correspondante :

* [getItem](contexthub-api.md#getitem-key)
* [setItem](contexthub-api.md#setitem-key-value-options)

Notez que les magasins candidats personnalisés peuvent définir des fonctions supplémentaires qui permettent d’accéder aux données du magasin.

>[!NOTE]
>
>Par défaut, ContextHub ne connaît pas les utilisateurs actuellement connectés sur les serveurs de publication. Il considère ces utilisateurs comme étant anonymes.
>
>Vous pouvez sensibiliser ContextHub aux utilisateurs connectés en chargeant le magasin de profils. Refer to [sample code on GitHub here](https://github.com/Adobe-Marketing-Cloud/aem-sample-we-retail/blob/master/ui.apps/src/main/content/jcr_root/apps/weretail/components/structure/header/clientlib/js/utilities.js).

### Génération d’événements ContextHub {#contexthub-eventing}

ContextHub comprend une structure d’événements qui vous permet de répondre automatiquement aux événements du magasin. Chaque objet du magasin contient un objet [`ContextHub.Utils.Eventing`](contexthub-api.md#contexthub-utils-eventing) disponible sous la forme d’une propriété [`eventing`](contexthub-api.md#eventing) du magasin. Utilisez la fonction [`on`](contexthub-api.md#on-name-handler-selector-triggerforpastevents) ou [`once`](contexthub-api.md#once-name-handler-selector-triggerforpastevents) pour lier une fonction JavaScript à un événement de magasin.

## Utilisation de ContextHub pour manipuler des cookies {#using-context-hub-to-manipulate-cookies}

L’API JavaScript ContextHub offre une prise en charge de plusieurs navigateurs pour la gestion des cookies de navigateur. The [`ContextHub.Utils.Cookie`](contexthub-api.md#contexthub-utils-cookie) namespace defines several functions for creating, manipulating, and deleting cookies.

## Identification de segments ContextHub résolus {#determining-resolved-contexthub-segments}

Le moteur de segments ContextHub vous permet de déterminer quels segments enregistrés sont résolus dans le contexte actuel. Utilisez la fonction getResolvedSegments de la classe [`ContextHub.SegmentEngine.SegmentManager`](contexthub-api.md#contexthub-segmentengine-segmentmanager) pour récupérer les segments résolus. Then, use the `getName` or `getPath` function of the [`ContextHub.SegmentEngine.Segment`](contexthub-api.md#contexthub-segmentengine-segment) class to test for a segment.

### Segments ContextHub {#contexthub-segments}

ContextHub segments are installed below the `/conf/<site>/settings/wcm/segments` node.

Les segments suivants sont installés avec le site de didacticiel [WKND.](getting-started.md)

* summer
* winter

Les règles utilisées pour résoudre ces segments sont résumées comme suit :

* Tout d’abord, le magasin de [géolocalisation](ch-samplestores.md#contexthub-geolocation-sample-store-candidate) est utilisé pour déterminer la latitude de l’utilisateur.
* Ensuite, l&#39;élément de données du mois du magasin [](ch-samplestores.md#contexthub-surferinfo-sample-store-candidate) surferinfo détermine la saison où il se trouve dans cette latitude.

>[!WARNING]
>
>Les segments installés sont fournis en tant que configurations de référence pour vous aider à créer votre propre configuration dédiée pour votre projet et ne doivent donc pas être utilisés directement.

## Débogage de ContextHub {#debugging-contexthub}

Il existe un certain nombre d’options pour déboguer ContextHub, y compris la génération de journaux. See [Configuring ContextHub for more information.](ch-configuring.md#logging-debug-messages-for-contexthub)

## Affichage d’un aperçu de la structure ContextHub {#see-an-overview-of-the-contexthub-framework}

ContextHub fournit une [page de diagnostics](ch-diagnostics.md) qui affiche un aperçu de sa structure.
