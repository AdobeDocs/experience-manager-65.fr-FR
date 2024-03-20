---
title: Ajout de ContextHub à des pages et accès à des magasins
description: Ajoutez ContextHub à vos pages pour activer les fonctionnalités ContextHub et créer un lien vers les bibliothèques JavaScript ContextHub
exl-id: ae745af9-b49f-46b9-ab48-2fd256e9a681
solution: Experience Manager, Experience Manager Sites
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '902'
ht-degree: 95%

---

# Ajouter ContextHub à des pages et accéder à des magasins {#adding-contexthub-to-pages-and-accessing-stores}

Ajoutez ContextHub à vos pages pour activer les fonctionnalités ContextHub et créer un lien vers les bibliothèques JavaScript ContextHub.

L’API JavaScript ContextHub permet d’accéder aux données contextuelles gérées par ContextHub. Cette page décrit brièvement les principales fonctionnalités de l’API pour accéder à des données contextuelles et les manipuler. Suivez les liens vers la documentation de référence de l’API pour consulter des informations détaillées et des exemples de code.

## Ajout de ContextHub à un composant de page {#adding-contexthub-to-a-page-component}

Pour activer les fonctionnalités ContextHub et créer un lien vers les bibliothèques JavaScript ContextHub, insérez le composant `contexthub` dans la section `head` de votre page. Le code HTL de votre composant de page devrait ressembler à ceci :

```xml
<sly data-sly-resource="${'contexthub' @ resourceType='granite/contexthub/components/contexthub'}"/>
```

Notez que vous devez également configurer si la barre d’outils ContextHub s’affiche ou non en mode Aperçu. Voir [Affichage et masquage de l’UI ContextHub](ch-configuring.md#showing-and-hiding-the-contexthub-ui).

## À propos des magasins ContextHub {#about-contexthub-stores}

Utilisez les magasins ContextHub pour conserver les données contextuelles. ContextHub fournit les types de magasins suivants qui constituent la base de tous les types de magasins :

* [PersistedStore](contexthub-api.md#contexthub-store-persistedstore)
* [SessionStore](contexthub-api.md#contexthub-store-sessionstore)
* [JSONPStore](contexthub-api.md#contexthub-store-persistedjsonpstore)
* [PersistedJSONPStore](contexthub-api.md#contexthub-store-persistedstore)

Tous les types de magasins sont des extensions de la classe [`ContextHub.Store.Core`](contexthub-api.md#contexthub-store-core). Pour plus d’informations sur la création d’un type de magasin, voir [Création de magasins personnalisés](ch-extend.md#creating-custom-store-candidates). Pour plus d’informations sur les exemples de types de magasin, voir [Exemples de candidats de magasins ContextHub](ch-samplestores.md).

### Modes de persistance {#persistence-modes}

Les magasins ContextHub utilisent l’un des modes de persistance suivants :

* **Local :** utilise HTML5 localStorage pour conserver les données. Le stockage Local est conservé dans le navigateur entre les sessions.
* **Session** : utilise HTML5 sessionStorage pour conserver les données. Le stockage Session est conservé pendant la durée de la session du navigateur et est disponible pour toutes les fenêtres du navigateur.
* **Cookie :** utilise la prise en charge native des cookies par le navigateur pour le stockage des données. Les données des cookies sont envoyées vers et depuis le serveur dans les requêtes HTTP.
* **Window.name** : utilise la propriété window.name pour conserver les données.
* **Memory** : utilise un objet JavaScript pour conserver les données.

Par défaut, ContextHub utilise le mode de persistance Local. Si le navigateur ne prend pas en charge ou n’autorise pas HTML5 localStorage, la persistance Session est utilisée. Si le navigateur ne prend pas en charge ou n’autorise pas HTML5 sessionStorage, la persistance Window.name est utilisée.

### Données du magasin {#store-data}

En interne, le stockage des données forme une arborescence, permettant l’ajout de valeurs sous la forme de types principaux ou d’objets complexes. Lorsque vous ajoutez des objets complexes aux magasins, les propriétés de l’objet forment des branches dans l’arborescence de données. Par exemple, l’objet complexe suivant est ajouté à un magasin vide nommé location :

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

L’arborescence des données du magasin peut être conceptualisée comme suit :

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

L’arborescence définit les éléments de données du magasin sous la forme de paires clé/valeur. Dans l’exemple ci-dessus, la clé `/number` correspond à la valeur `321` et la clé `/data/country` à la valeur `Switzerland`.

### Manipulation d’objets {#manipulating-objects}

ContextHub fournit la classe [`ContextHub.Utils.JSON.tree`](contexthub-api.md#contexthub-utils-json-tree) pour manipuler des objets JavaScript. Utilisez les fonctions de cette classe pour manipuler des objets JavaScript avant de les ajouter à un magasin ou après les avoir récupérés d’un magasin.

En outre, la classe [`ContextHub.Utils.JSON`](contexthub-api.md#contexthub-utils-json) fournit des fonctions pour sérialiser des objets en chaînes et désérialiser des chaînes en objets. Utilisez cette classe pour gérer les données JSON afin de prendre en charge les navigateurs qui n’intègrent pas, en natif, les fonctions `JSON.parse` et `JSON.stringify`.

## Interaction avec les magasins ContextHub {#interacting-with-contexthub-stores}

Utilisez l’objet JavaScript [`ContextHub`](contexthub-api.md#ui-event-constants) pour obtenir un magasin comme objet JavaScript. Une fois que vous avez obtenu l’objet de magasin, vous pouvez manipuler les données qu’il contient. Utilisez la fonction [`getAllStores`](contexthub-api.md#getallstores) ou [`getStore`](contexthub-api.md#getstore-name) pour obtenir le magasin.

### Accès aux données du magasin {#accessing-store-data}

La classe JavaScript [`ContexHub.Store.Core`](contexthub-api.md#contexthub-store-core) définit plusieurs fonctions permettant d’interagir avec les données du magasin. Les fonctions suivantes stockent et récupèrent plusieurs éléments de données contenus dans des objets :

* [addAllItems](contexthub-api.md#addallitems-tree-options)
* [getTree](contexthub-api.md#gettree-includeinternals)

Les éléments de données individuels sont stockés sous la forme d’un ensemble de paires clé/valeur. Pour stocker et récupérer des valeurs, spécifiez la clé correspondante :

* [getItem](contexthub-api.md#getitem-key)
* [setItem](contexthub-api.md#setitem-key-value-options)

Notez que les magasins candidats personnalisés peuvent définir des fonctions supplémentaires qui permettent d’accéder aux données du magasin.

>[!NOTE]
>
>Par défaut, ContextHub ne connaît pas les utilisateurs et utilisatrices actuellement connectés sur les serveurs de publication. Il considère ces utilisateurs et utilisatrices comme étant « anonymes ».
>
>Vous pouvez sensibiliser ContextHub aux utilisateurs et utilisatrices connectés en chargeant le magasin de profils. Consultez l’[exemple de code sur GitHub ici](https://github.com/Adobe-Marketing-Cloud/aem-sample-we-retail/blob/master/ui.apps/src/main/content/jcr_root/apps/weretail/components/structure/header/clientlib/js/utilities.js).

### Génération d’événements ContextHub {#contexthub-eventing}

ContextHub comprend un framework d’événements qui vous permet de répondre automatiquement aux événements du magasin. Chaque objet du magasin contient un objet [`ContextHub.Utils.Eventing`](contexthub-api.md#contexthub-utils-eventing) disponible sous la forme d’une propriété [`eventing`](contexthub-api.md#eventing) du magasin. Utilisez la fonction [`on`](contexthub-api.md#on-name-handler-selector-triggerforpastevents) ou [`once`](contexthub-api.md#once-name-handler-selector-triggerforpastevents) pour lier une fonction JavaScript à un événement de magasin.

## Utiliser ContextHub pour manipuler des cookies {#using-context-hub-to-manipulate-cookies}

L’API JavaScript ContextHub offre une prise en charge de plusieurs navigateurs pour la gestion des cookies de navigateur. L’espace de noms [`ContextHub.Utils.Cookie`](contexthub-api.md#contexthub-utils-cookie) définit plusieurs fonctions permettant de créer, de manipuler et de supprimer des cookies.

## Identification de segments ContextHub résolus {#determining-resolved-contexthub-segments}

Le moteur de segments ContextHub vous permet de déterminer quels segments enregistrés sont résolus dans le contexte actuel. Utilisez la fonction getResolvedSegments de la classe [`ContextHub.SegmentEngine.SegmentManager`](contexthub-api.md#contexthub-segmentengine-segmentmanager) pour récupérer les segments résolus. Utilisez ensuite la fonction `getName` ou `getPath` de la classe [`ContextHub.SegmentEngine.Segment`](contexthub-api.md#contexthub-segmentengine-segment) pour tester un segment.

### Segments ContextHub {#contexthub-segments}

Les segments ContextHub sont installés sous le nœud `/conf/<site>/settings/wcm/segments`.

Les segments suivants sont installés avec le [site de tutoriel WKND](getting-started.md).

* summer
* winter

Les règles utilisées pour résoudre ces segments sont résumées comme suit :

* Tout d’abord, le magasin [geolocation](ch-samplestores.md#contexthub-geolocation-sample-store-candidate) est utilisé pour déterminer la latitude de l’utilisateur.
* Ensuite, l’élément de données du mois du [magasin surferinfo](ch-samplestores.md#contexthub-surferinfo-sample-store-candidate) détermine la saison où il se trouve dans cette latitude.

>[!WARNING]
>
>Les segments installés sont fournis en tant que configurations de référence pour vous aider à créer votre propre configuration dédiée pour votre projet. Ne les utilisez pas directement.

## Débogage de ContextHub {#debugging-contexthub}

Il existe plusieurs options pour déboguer ContextHub, y compris la génération de journaux. Voir [Configuration de ContextHub](ch-configuring.md#logging-debug-messages-for-contexthub) pour plus d’informations.

## Affichage d’un aperçu de la structure ContextHub {#see-an-overview-of-the-contexthub-framework}

ContextHub fournit une [page de diagnostics](ch-diagnostics.md) qui affiche un aperçu de son framework.
