---
title: Guide de référence pour l’API Javascript ContextHub
seo-title: Guide de référence pour l’API Javascript ContextHub
description: L’API JavaScript ContextHub est disponible pour les scripts lorsque le composant ContextHub a été ajouté à la page.
seo-description: L’API JavaScript ContextHub est disponible pour les scripts lorsque le composant ContextHub a été ajouté à la page.
uuid: 296d6c8e-517f-4837-9e86-ae571ea8aa17
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
discoiquuid: 90605f41-1861-4891-a7c8-b8b5918cd5c6
translation-type: tm+mt
source-git-commit: 9a4ae73c08657195da2741cccdb196bd7f7142c9
workflow-type: tm+mt
source-wordcount: '5029'
ht-degree: 78%

---


# Guide de référence pour l’API Javascript ContextHub{#contexthub-javascript-api-reference}

L’API JavaScript ContextHub est disponible pour les scripts lorsque le composant [ContextHub a été ajouté à la page](/help/sites-developing/ch-adding.md#adding-contexthub-to-a-page-component).

## Constantes ContextHub {#contexthub-constants}

Valeurs constantes définies par l’API JavaScript ContextHub.

### Constantes d’événement {#event-constants}

Le tableau suivant répertorie les noms des événements qui se produisent pour les magasins ContextHub. Voir aussi [ContextHub.Utils.Eventing](/help/sites-developing/contexthub-api.md#contexthub-utils-eventing).

| Constante | Description | Valeur |
|---|---|---|
| ContextHub.Constants.EVENT_NAMESPACE | L&#39;espace de nommage événement de ContextHub | ch |
| ContextHub.Constants.EVENT_ALL_STORES_READY | Indique que tous les magasins requis sont enregistrés, initialisés et prêts à être consommés. | prêt pour tous les magasins |
| ContextHub.Constants.EVENT_STORES_PARTIALLY_READY | Indique que tous les magasins n’ont pas été initialisés dans un délai d’attente donné. | magasins-partiellement prêts |
| ContextHub.Constants.EVENT_STORE_REGISTERED | Déclenché lorsqu&#39;un magasin est enregistré | enregistré en magasin |
| ContextHub.Constants.EVENT_STORE_READY | Indique que les magasins sont prêts à fonctionner. Il est déclenché immédiatement après l’enregistrement, à l’exception du cas des magasins JSONP où il est déclenché lorsque les données sont extraites). | prêt pour le stockage |
| ContextHub.Constants.EVENT_STORE_UPDATED | Déclenché lorsqu’un magasin met à jour sa persistance | store-update |
| ContextHub.Constants.PERSISTENCE_CONTAINER_NAME | Nom du conteneur de persistance | ContextHubPersistence |
| ContextHub.Constants.SERVICE_RAW_RESPONSE_KEY | Stocke le nom de clé de persistance spécifique dans lequel le résultat JSON brut est stocké | /_/raw-response |
| ContextHub.Constants.SERVICE_RESPONSE_TIME_KEY | Stocke un horodatage spécifique indiquant à quel moment les données JSON ont été extraites | /_/temps de réponse |
| ContextHub.Constants.SERVICE_LAST_URL_KEY | Stocke l’URL spécifique du service JSON utilisé lors du dernier appel. | /_/url |
| ContextHub.Constants.IS_CONTAINER_EXPANDED | Indique si l’interface utilisateur de ContextHub est développée. | /_/conteneur étendu |

### Constantes d’événement de l’IU {#ui-event-constants}

Le tableau suivant répertorie les noms des événements qui se produisent pour l’IU ContextHub.

| **Constante** | **Description** | **Valeur** |
|---|---|---|
| ContextHub.Constants.EVENT_UI_MODE_REGISTERED | Déclenché lorsqu&#39;un mode est enregistré | auto-mode-registered |
| ContextHub.Constants.EVENT_UI_MODE_UNREGISTERED | Déclenché lorsqu&#39;un mode n&#39;est pas enregistré | ui-mode-non-enregistré |
| ContextHub.Constants.EVENT_UI_MODE_RENDERER_REGISTERED | Déclenché lorsqu’un rendu en mode est enregistré | ui-mode-renderer-registered |
| ContextHub.Constants.EVENT_UI_MODE_RENDERER_UNREGISTERED | Déclenché lorsqu’un rendu en mode n’est pas enregistré | ui-mode-renderer-non-enregistré |
| ContextHub.Constants.EVENT_UI_MODE_ADDED | Déclenché lorsqu’un nouveau mode est ajouté | ui-mode-ajouté |
| ContextHub.Constants.EVENT_UI_MODE_REMOVED | Déclenché lorsqu’un mode est supprimé | ui-mode-remove |
| ContextHub.Constants.EVENT_UI_MODE_SELECTED | Déclenché lorsqu’un mode est sélectionné par l’utilisateur | ui-mode-selected |
| ContextHub.Constants.EVENT_UI_MODULE_REGISTERED | Déclenché lorsqu&#39;un nouveau module est enregistré | ui-module-registered |
| ContextHub.Constants.EVENT_UI_MODULE_UNREGISTERED | Déclenché lorsqu&#39;un module n&#39;est pas enregistré | ui-module-unregistered |
| ContextHub.Constants.EVENT_UI_MODULE_RENDERER_REGISTERED | Déclenché lorsqu&#39;un rendu de module est enregistré | ui-module-renderer-registered |
| ContextHub.Constants.EVENT_UI_MODULE_RENDERER_UNREGISTERED | Déclenché lorsqu’un rendu de module n’est pas enregistré | ui-module-renderer-unregistered |
| ContextHub.Constants.EVENT_UI_MODULE_ADDED | Déclenché lorsqu’un nouveau module est ajouté | ui-module-ajouté |
| ContextHub.Constants.EVENT_UI_MODULE_REMOVED | Déclenché lorsqu&#39;un module est supprimé | ui-module-remove |
| ContextHub.Constants.EVENT_UI_CONTAINER_ADDED | Déclenché lorsque le conteneur d’interface utilisateur est ajouté à la page | ui-conteneur-ajouté |
| ContextHub.Constants.EVENT_UI_CONTAINER_OPENED | Déclenché lorsque l’interface utilisateur ContextHub est ouverte | ouvert par conteneur automatique |
| ContextHub.Constants.EVENT_UI_CONTAINER_CLOSED | Déclenché lorsque l’interface utilisateur ContextHub est réduite | ui-conteneur-fermé |
| ContextHub.Constants.EVENT_UI_PROPERTY_MODIFIED | Déclenché lorsqu’une propriété est modifiée | ui-property-changed |
| ContextHub.Constants.EVENT_UI_RENDERED | Déclenché chaque fois que l’interface utilisateur ContextHub est rendue (par exemple après un changement de propriété) | rendu par ui |
| ContextHub.Constants.EVENT_UI_INITIALIZED | Déclenché lorsque le conteneur d&#39;interface utilisateur est initialisé | ui-initialisé |
| ContextHub.Constants.ACTIVE_UI_MODE | Indique le mode principal de l’interface utilisateur | /_/principal-ui-mode |

## Guide de référence pour l’API Javascript ContextHub {#contexthub-javascript-api-reference-2}

L’objet ContextHub fournit l’accès à tous les magasins.

### Fonctions (ContextHub) {#functions-contexthub}

#### getAllStores() {#getallstores}

Renvoie tous les magasins ContextHub enregistrés.

Cette fonction ne comporte aucun paramètre.

**Renvoie**

Un objet qui contient tous les magasins ContextHub. Chaque magasin est un objet qui utilise le même nom de magasin.

**Exemple**

L’exemple suivant récupère tous les magasins, puis récupère le magasin de géolocalisation :

```
var allStores = ContextHub.getAllStores();
var geoloc = allStores.geolocation
```

#### getStore(name) {#getstore-name}

Récupère un magasin en tant qu’objet Javascript.

**Paramètres**

* **name :** nom sous lequel le magasin a été enregistré.

**Renvoie**

Un objet qui représente le magasin.

**Exemple**

L’exemple suivant récupère le magasin de géolocalisation :

```
var geoloc = ContextHub.getStore("geolocation");
```

## ContextHub.SegmentEngine.Segment {#contexthub-segmentengine-segment}

Représente un segment ContextHub. Utilisez ContextHub.SegmentEngine.SegmentManager pour récupérer des segments.

### Fonctions (ContextHub.ContextEngine.Segment) {#functions-contexthub-contextengine-segment}

#### getName() {#getname}

Renvoie le nom du segment sous forme de chaîne.

#### getPath() {#getpath}

Renvoie le chemin du référentiel pour la définition de segment sous forme de chaîne.

## ContextHub.SegmentEngine.SegmentManager {#contexthub-segmentengine-segmentmanager}

Fournit un accès aux segments ContextHub.

### Fonctions (ContextHub.SegmentEngine.SegmentManager) {#functions-contexthub-segmentengine-segmentmanager}

#### getResolvedSegments() {#getresolvedsegments}

Renvoie les segments résolus dans le contexte actuel. Cette fonction ne comporte aucun paramètre.

**Renvoie**

Une table d’objets ContextHub.SegmentEngine.Segment.

## ContextHub.Store.Core {#contexthub-store-core}

Classe de base pour les magasins ContextHub.

### Propriétés (ContextHub.Store.Core) {#properties-contexthub-store-core}

#### eventing {#eventing}

Objet [ContextHub.Utils.Eventing](/help/sites-developing/contexthub-api.md#contexthub-utils-eventing). Utilisez cet objet pour que les fonctions de liaison stockent les événements. For information about the default value and initialization, see [init(name,config)](/help/sites-developing/contexthub-api.md#init-name-config).

#### name {#name}

Nom du magasin

#### persistence {#persistence}

Objet ContextHub.Utils.Persistence. For information about the default value and initialization, see `[init(name,config)](/help/sites-developing/contexthub-api.md#init-name-config).`

### Fonctions (ContextHub.Store.Core) {#functions-contexthub-store-core}

#### addAllItems(tree, options) {#addallitems-tree-options}

Fusionne un objet de données ou une table contenant les données de magasin. Chaque paire clé/valeur de l’objet ou de la table est ajoutée au magasin (via la fonction `setItem`) :

* **Objet :** Les clés sont les noms des propriétés.
* **Tableau :** Les clés sont les index de tableau.

Notez que les valeurs peuvent être des objets.

**Paramètres**

* **tree :** (objet ou table). Données à ajouter au magasin.
* **options :**(objet). Objet facultatif d’options transmis à la fonction setItem. Pour plus d’informations, reportez-vous au paramètre `options` de [setItem(key,value,options)](/help/sites-developing/contexthub-api.md#setitem-key-value-options).

**Renvoie**

Une `boolean` valeur :

* Une valeur `true` indique que l’objet de données a été stocké.
* Une valeur `false` indique que le magasin de données reste inchangé.

#### addReference(key, anotherKey) {#addreference-key-anotherkey}

Crée une référence d’une clé à une autre. Une clé ne peut pas se référencer elle-même.

**Paramètres**

* **key :** clé qui référence `anotherKey`.

* **anotherkey :** clé référencée par le paramètre `key`.

**Renvoie**

Une `boolean` valeur :

* Une valeur `true` indique que la référence a été ajoutée.
* Une valeur `false` indique qu’aucune référence n’a été ajoutée.

#### announceReadiness() {#announcereadiness}

Déclenche l’événement `ready` pour ce magasin. Cette fonction ne possède aucun paramètre et ne renvoie aucune valeur.

#### clean() {#clean}

Supprime toutes les données du magasin. La fonction ne possède aucun paramètre et aucune valeur de retour.

#### getItem(key) {#getitem-key}

Renvoie la valeur associée à une clé.

**Paramètres**

* **key :**(chaîne). Clé pour laquelle il faut retourner la valeur.

**Renvoie**

Un objet qui représente la valeur de la clé.

#### getKeys(includeInternals) {#getkeys-includeinternals}

Récupère les clés du magasin. En option, vous pouvez récupérer les clés utilisées en interne par le framework ContextHub.

**Paramètres**

* **includeInternals :** une valeur `true` inclut les clés utilisées en interne dans les résultats. Ces clés commencent par le caractère de soulignement (&quot;_&quot;). La valeur par défaut est `false`.

**Renvoie**

An array of key names ( `string` values).

#### getReferences() {#getreferences}

Récupère les références du magasin.

**Renvoie**

Tableau qui utilise les clés référençant comme index pour les clés référencées :

* Referencing keys correspond with the `key` parameter of the `addReference` function.

* Referenced keys correspond with the `anotherKey` parameter of the `addReference` function.

#### getTree(includeInternals) {#gettree-includeinternals}

Récupère l’arbre de données du magasin. Vous pouvez éventuellement inclure les paires clé/valeur utilisées en interne par le framework ContextHub.

**Paramètres**

* `includeInternals:` Une valeur de `true` inclut des paires clé/valeur utilisées en interne dans les résultats. Les clés de ces données commencent par le caractère de soulignement (&quot;_&quot;). La valeur par défaut est `false`.

**Renvoie**

Un objet qui représente l’arbre de données. Les clés sont les noms des propriétés de l’objet.

#### init(name, config) {#init-name-config}

Initialise le magasin.

* Définit les données du magasin sur un objet vide.
* Définit les références du magasin sur un objet vide.
* The eventChannel is data:*name*, where *name* is the store name.

* Le paramètre StoreDataKey est /store/*name* où *name* correspond au nom du magasin.

**Paramètres**

* **name** : nom du magasin.
* **config :** objet qui contient des propriétés de configuration :

   * eventDeferring : la valeur par défaut est 32.
   * eventing : objet [ContextHub.Utils.Eventing](/help/sites-developing/contexthub-api.md#contexthub-utils-eventing) pour ce magasin. La valeur par défaut est l’objet ContextHub.eventing utilisé.
   * persistence : objet ContextHub.Utils.Persistence pour ce magasin. La valeur par défaut est l’objet ContextHub.persistence.

#### isEventingPaused() {#iseventingpaused}

Détermine si le déclenchement d’événement est suspendu pour ce magasin.

**Renvoie**

Une valeur booléenne :

* `true` : le mode Eventing est suspendu afin qu’aucun événement ne soit déclenché pour ce magasin.
* `false` : le mode Eventing n’est pas suspendu, de sorte que les événements sont déclenchés pour ce magasin.

#### pauseEventing() {#pauseeventing}

Suspend le mode Eventing pour le magasin afin qu’aucun événement ne soit déclenché. Cette fonction ne possède aucun paramètre et ne renvoie aucune valeur.

#### removeItem(key, options) {#removeitem-key-options}

Supprime une paire clé/valeur du magasin.

Lorsqu’une clé est supprimée, la fonction déclenche l’événement `data`. Les données du événement comprennent le nom de la banque, le nom de la clé supprimée, la valeur supprimée, la nouvelle valeur de la clé (nulle) et le type d’action &quot;remove&quot;.

En option, vous pouvez empêcher le déclenchement de l’événement `data`.

**Paramètres**

* **key :** (chaîne). Nom de la clé à supprimer.
* **options :** (objet). Objet d’options. Les propriétés d’objet suivantes sont valides :

   * silent : une valeur `true` empêche le déclenchement de l’événement `data`. La valeur par défaut est `false`.

**Renvoie**

Une `boolean` valeur :

* A value of `true` indicates the key/value pair was removed.
* A value of `false` indicates that the data store is unchanged because the key was not found in the store.

#### removeReference(key) {#removereference-key}

Supprime une référence du magasin.

**Paramètres**

* **key :** référence de clé à supprimer. This parameter corresponds with the `key` parameter of the `addReference` function.

**Renvoie**

Une `boolean` valeur :

* A value of `true` indicates the reference was removed.
* A value of `false` indicates that the key was not valid and the store is unchanged.

#### reset(keepRemainingData) {#reset-keepremainingdata}

Rétablit les valeurs d’origine des données persistantes du magasin. En option, vous pouvez supprimer toutes les autres données du magasin. L’événement est suspendu pour ce magasin pendant sa réinitialisation. Cette fonction ne renvoie aucune valeur.

Les valeurs initiales sont fournies dans la propriété initialValues &#x200B;&#x200B;de l’objet de configuration utilisé pour instancier l’objet magasin.

**Paramètres**

* **keepRemainingData :** (booléen). Une valeur true entraîne la persistance des données non initiales. Une valeur false entraîne la suppression de toutes les données, à l’exception des valeurs initiales.

Rétablit les valeurs d’origine des données persistantes du magasin. En option, vous pouvez supprimer toutes les autres données du magasin. L’événement est suspendu pour ce magasin pendant sa réinitialisation. Cette fonction ne renvoie aucune valeur.

Les valeurs initiales sont fournies dans la propriété initialValues &#x200B;&#x200B;de l’objet de configuration utilisé pour instancier l’objet magasin.

**Paramètres**

* keepRemainingData : (booléen). Une valeur true entraîne la persistance des données non initiales. Une valeur false entraîne la suppression de toutes les données, à l’exception des valeurs initiales.

#### resolveReference(key, retry) {#resolvereference-key-retry}

Récupère une clé référencée. En option, vous pouvez spécifier le nombre d’itérations à utiliser pour résoudre la meilleure correspondance.

**Paramètres**

* **key :** (chaîne). Clé pour laquelle il faut résoudre la référence. This `key` parameter corresponds with the `key` parameter of the `addReference` function.

* **retry :** (nombre). Nombre d’itérations à utiliser.

**Renvoie**

A `string` value that represents the referenced key. Si aucune référence n’est résolue, la valeur du paramètre `key` est renvoyée.

#### resumeEventing() {#resumeeventing}

Rétablit le mode Eventing pour ce magasin afin que les événements soient déclenchés. Cette fonction ne définit aucun paramètre et ne renvoie aucune valeur.

#### setItem(key, value, options) {#setitem-key-value-options}

Ajoute une paire clé/valeur au magasin.

Déclenche l’événement `data` uniquement si la valeur de la clé est différente de la valeur actuellement stockée pour la clé. Vous pouvez éventuellement empêcher le déclenchement de l’événement `data`.

Les données d’événement incluent le nom du magasin, la clé, la valeur précédente, la nouvelle valeur et le type d’action `set`.

**Paramètres**

* **key :** (chaîne). Nom de la clé.
* **options :** (objet). Objet d’options. Les propriétés d’objet suivantes sont valides :

   * silent : une valeur `true` empêche le déclenchement de l’événement `data`. La valeur par défaut est `false`.

* **value :** (objet). Valeur à associer à la clé.

**Renvoie**

Une `boolean` valeur :

* Une valeur `true` indique que l’objet de données a été stocké.
* Une valeur `false` indique que le magasin de données reste inchangé.

## ContextHub.Store.JSONPStore {#contexthub-store-jsonpstore}

Magasin qui contient des données JSON. Les données sont extraites d’un service JSONP externe ou, facultativement, d’un service qui renvoie des données JSON. Spécifiez les détails du service à l’aide de la fonction [`init`](/help/sites-developing/contexthub-api.md#init-name-config) lorsque vous créez une instance de cette classe.

Le magasin utilise la persistance en mémoire (variable Javascript). Les données du magasin sont disponibles uniquement pendant la durée de vie de la page.

ContextHub.Store.JSONPStore extends [ContextHub.Store.Core](/help/sites-developing/contexthub-api.md#contexthub-store-core) and inherits the functions of that class.

### Fonctions (ContextHub.Store.JSONPStore) {#functions-contexthub-store-jsonpstore}

#### configureService(serviceConfig, override) {#configureservice-serviceconfig-override}

Configure les détails de connexion au service JSONP que cet objet utilise. Vous pouvez mettre à jour ou remplacer la configuration existante. La fonction ne renvoie aucune valeur.

**Paramètres**

* **serviceConfig :** objet qui contient les propriétés ci-dessous.

   * host : (chaîne). Nom ou adresse IP du serveur.
   * jsonp : (booléen). Une valeur true indique que le service est un service JSONP, false dans le cas contraire. Si la valeur est true, l’objet {callback:&quot;ContextHub.Callbacks.*Object.name*} est ajouté à l’objet service.params.
   * params : (Objet) Paramètres d’URL représentés sous forme de propriétés d’objet. Les noms des paramètres correspondent aux noms de propriétés et leurs valeurs aux valeurs des propriétés.
   * path : (chaîne). Chemin d’accès au service.
   * port : (nombre). Numéro de port du service.
   * secure : (chaîne ou booléen). Détermine le protocole à utiliser pour l’URL du service:

      * auto : //
      * true : https://
      * false: https://

* **override :** (booléen). A value of `true` causes the existing service configuration to be replaced by the properties of `serviceConfig`. A value of `false` causes the existing service configuration properties to be merged with the properties of `serviceConfig`.

#### getRawResponse() {#getrawresponse}

Renvoie la réponse brute mise en cache depuis le dernier appel au service JSONP. La fonction ne nécessite aucun paramètre.

**Renvoie**

Un objet qui représente la réponse brute.

#### getServiceDetails() {#getservicedetails}

Récupère l’objet de service pour cet objet ContextHub.Store.JSONPStore. L’objet de service contient toutes les informations requises pour créer l’URL du service.

**Renvoie**

Un objet possédant les propriétés suivantes :

* **host :** (chaîne). Nom ou adresse IP du serveur.
* **jsonp :** (booléen). Une valeur true indique que le service est un service JSONP, false dans le cas contraire. Si la valeur est true, l’objet {callback:&quot;ContextHub.Callbacks.*Object.name*} est ajouté à l’objet service.params.

* **params :** (Objet) Paramètres d’URL représentés sous forme de propriétés d’objet. Les noms des paramètres correspondent aux noms de propriétés et leurs valeurs aux valeurs des propriétés.
* **path :** (chaîne). Chemin d’accès au service.
* **port :** (nombre). Numéro de port du service.
* **secure :** (chaîne ou booléen). Détermine le protocole à utiliser pour l’URL du service:

   * auto : //
   * true : https://
   * false: https://

#### getServiceURL(resolve) {#getserviceurl-resolve}

Récupère l’URL du service JSONP.

**Paramètres**

* **resolve :** (booléen). Détermine s’il faut inclure les paramètres résolus dans l’URL. A value of `true` resolves parameters, and `false` does not.

**Renvoie**

A `string` value that represents the service URL.

#### init(name, config) {#init-name-config-1}

initialise l’objet ContextHub.Store.JSONPStore.

**Paramètres**

* **name** : (chaîne). Nom du magasin.
* **config :** (objet). Objet contenant la propriété du service. L’objet JSONPStore utilise les propriétés de l’objet `service` pour construire l’URL du service JSONP :

   * eventDeferring : 32.
   * eventing : objet ContextHub.Utils.Eventing pour ce magasin. La valeur par défaut est l’objet `ContextHub.eventing`.
   * persistence : objet ContextHub.Utils.Persistence pour ce magasin. Par défaut, la persistance de la mémoire est utilisée (objet Javascript).
   * service : (Objet)

      * host : (chaîne). Nom ou adresse IP du serveur.
      * jsonp : (booléen). Une valeur true indique que le service est un service JSONP, false dans le cas contraire. Lorsque la valeur est true, l’ `{callback: "ContextHub.Callbacks.*Object.name*}`objet est ajouté à `service.params`.
      * params : (Objet) Paramètres d’URL représentés sous forme de propriétés d’objet. Les noms et les valeurs des paramètres sont ceux des propriétés de l’objet, respectivement.
      * path : (chaîne). Chemin d’accès au service.
      * port : (nombre). Numéro de port du service.
      * secure : (chaîne ou booléen). Détermine le protocole à utiliser pour l’URL du service:

         * auto : //
         * true : https://
         * false: https://
      * timeout : (nombre). Délai d’attente avant que le service JSONP ne réponde, en millisecondes.
      * ttl : délai minimal en millisecondes qui s’écoule entre les appels au service JSONP. (Voir la fonction [queryService](/help/sites-developing/contexthub-api.md#queryservice-reload)).


#### queryService(reload) {#queryservice-reload}

Interroge le service JSONP distant et met en cache la réponse. If the amount of time since the previous call to this function is less than the value of `config.service.ttl`, the service is not called and the cached response is not changed. En option, vous pouvez forcer l’appel du service. La propriété `config.service.ttl` est définie lors de l’appel de la fonction [init](/help/sites-developing/contexthub-api.md#init-name-config) pour initialiser le magasin.

Déclenche l’événement ready lorsque la requête est terminée. Si l’URL du service JSONP n’est pas définie, la fonction est inactive.

**Paramètres**

* **reload :** (booléen). Une valeur true supprime la réponse mise en cache et force le service JSONP à être appelé.

#### reset {#reset}

Réinitialise les valeurs initiales des données persistantes du magasin, puis appelle le service JSONP. En option, vous pouvez supprimer toutes les autres données du magasin. L’événement est suspendu pour ce magasin pendant que les valeurs initiales sont réinitialisées. Cette fonction ne renvoie aucune valeur.

Les valeurs initiales sont fournies dans la propriété initialValues &#x200B;&#x200B;de l’objet de configuration utilisé pour instancier l’objet magasin.

**Paramètres**

* **keepRemainingData :** (booléen). Une valeur true entraîne la persistance des données non initiales. Une valeur false entraîne la suppression de toutes les données, à l’exception des valeurs initiales.

#### resolveParameter(f) {#resolveparameter-f}

Résout le paramètre donné.

## ContextHub.Store.PersistedJSONPStore {#contexthub-store-persistedjsonpstore}

ContextHub.Store.PersistedJSONPStore étend le paramètre [ContextHub.Store.JSONPStore](/help/sites-developing/contexthub-api.md#contexthub-store-jsonpstore) pour qu’il hérite de toutes les fonctions de cette classe. Toutefois, les données extraites du service JSONP sont conservées conformément à la configuration de la persistance ContextHub. (See [Persistence Modes](/help/sites-developing/ch-adding.md#persistence-modes).)

## ContextHub.Store.PersistedStore {#contexthub-store-persistedstore}

ContextHub.Store.PersistedStore extends [ContextHub.Store.Core](/help/sites-developing/contexthub-api.md#contexthub-store-core) so it inherits all of the functions of that class. Les données de ce magasin sont conservées en fonction de la configuration de la persistance ContextHub.

## ContextHub.Store.SessionStore {#contexthub-store-sessionstore}

ContextHub.Store.SessionStore extends [ContextHub.Store.Core](/help/sites-developing/contexthub-api.md#contexthub-store-core) so it inherits all of the functions of that class. Les données de ce magasin sont conservées en utilisant la persistance en mémoire (objet Javascript).

## ContextHub.UI {#contexthub-ui}

Gère les modules d’IU et les moteurs de rendu des modules d’IU.

### Fonctions (ContextHub.UI) {#functions-contexthub-ui}

#### registerRenderer(moduleType, renderer, dontRender) {#registerrenderer-moduletype-renderer-dontrender}

Enregistre un moteur de rendu de module d’IU avec ContextHub. Une fois le moteur de rendu enregistré, il peut être utilisé pour [créer des modules d’IU](/help/sites-administering/contexthub-config.md#adding-a-ui-module). Utilisez cette fonction lorsque vous [étendez ContextHub.UI.BaseModuleRenderer](/help/sites-developing/ch-extend.md#creating-contexthub-ui-module-types) pour créer un moteur de rendu de module d’IU personnalisé.

**Paramètres**

* **moduleType :** (chaîne). Identificateur du rendu du module d’IU. Si un rendu est déjà enregistré à l’aide de la valeur spécifiée, le rendu existant n’est pas enregistré avant l’enregistrement de ce rendu.
* **rendu :** (Chaîne) Nom de la classe qui effectue le rendu du module d’interface utilisateur.
* **dontRender :** (booléen). Définir sur `true` pour empêcher le rendu de l’IU ContextHub après l’enregistrement du moteur de rendu. La valeur par défaut est `false`.

**Exemple**

L’exemple suivant enregistre un rendu en tant que type de module contextthub.browserinfo.

```
ContextHub.UI.registerRenderer('contexthub.browserinfo', new SurferinfoRenderer());
```

## ContextHub.Utils.Cookie {#contexthub-utils-cookie}

Classe d’utilitaire permettant d’interagir avec les cookies.

### Fonctions (ContextHub.Utils.Cookie) {#functions-contexthub-utils-cookie}

#### exists(key) {#exists-key}

Détermine si un cookie existe.

**Paramètres**

* **key:** Contient `String` la clé du cookie pour lequel vous effectuez des tests.

**Renvoie**

A `boolean` value of true indicates that the cookie exists.

**Exemple**

```
if (ContextHub.Utils.Cookie.exists("name")) {
   // conditionally-executed code
}
```

#### getAllItems(filter) {#getallitems-filter}

Renvoie tous les cookies dont les clés correspondent à un filtre.

**Paramètres**

* **filter** (optionnel) : critères d’appariement des clés de cookie. Pour renvoyer tous les cookies, ne spécifiez aucune valeur. Les types suivants sont pris en charge :

   * Chaîne : la chaîne est comparée à la clé de cookie.
   * Table : chaque élément de la table est un filtre.
   * Un objet RegExp : la fonction de test de l’objet est utilisée pour faire correspondre les clés de cookie.
   * Une fonction : fonction qui teste une clé de cookie pour chercher une correspondance. La fonction doit utiliser la clé de cookie comme paramètre et renvoyer la valeur true si le test confirme une correspondance.

**Renvoie**

Un objet de cookies. Les propriétés d’objet sont les clés des cookies et les valeurs des clés sont les valeurs des cookies.

**Exemple**

```
ContextHub.Utils.Cookie.getAllItems([/^cq-authoring/, /^cq-editor/])
```

#### getItem(key) {#getitem-key-1}

Renvoie une valeur de cookie.

**Paramètres**

* **key :** clé du cookie dont vous voulez renvoyer la valeur.

**Renvoie**

La valeur du cookie ou la valeur `null` si aucun cookie n’a été identifié pour la clé.

**Exemple**

```
ContextHub.Utils.Cookie.getItem("name");
```

#### getKeys(filter) {#getkeys-filter}

Renvoie une table des clés des cookies existants correspondant à un filtre.

**Paramètres**

* **filter :** critères d’appariement des clés de cookie. Les types suivants sont pris en charge :

   * Chaîne : la chaîne est comparée à la clé de cookie.
   * Table : chaque élément de la table est un filtre.
   * Un objet RegExp : la fonction de test de l’objet est utilisée pour faire correspondre les clés de cookie.
   * Une fonction : fonction qui teste une clé de cookie pour chercher une correspondance. La fonction doit utiliser la clé de cookie comme paramètre et renvoyer la valeur `true` si le test confirme une correspondance.

**Renvoie**

Une table de chaînes où chaque chaîne est la clé d’un cookie qui répond aux critères du filtre.

**Exemple**

```
ContextHub.Utils.Cookie.getKeys([/^cq-authoring/, /^cq-editor/])
```

#### removeItem(key, options) {#removeitem-key-options-1}

Supprime un cookie. Pour supprimer le cookie, la valeur est définie sur une chaîne vide et la date d’expiration est définie sur le jour précédant la date actuelle.

**Paramètres**

* **key:** Valeur `String` représentant la clé du cookie à supprimer.

* **options :** objet contenant des valeurs de propriété pour la configuration des attributs de cookie. Voir la fonction ` [setItem](/help/sites-developing/contexthub-api.md#setitem-key-value-options)` pour plus d’informations. La propriété `expires` n’a aucun effet.

**Renvoie**

Cette fonction ne retourne pas de valeur.

**Exemple**

```
ContextHub.Utils.Cookie.vanish([/^cq-authoring/, 'cq-scrollpos']);
```

#### setItem(key, value, options) {#setitem-key-value-options-1}

Crée un cookie de la clé et de la valeur en question et ajoute le cookie au document en cours. En option, vous pouvez spécifier des options qui configurent les attributs du cookie.

**Paramètres**

* **key :** chaîne contenant la clé du cookie.
* **value :** chaîne contenant la valeur du cookie.
* **options :** (facultatif). Objet contenant l’une des propriétés suivantes qui configurent les attributs de cookie :

   * expires: A `date` or `number` value that specifies when the cookie expires. Une valeur de date spécifie l’heure absolue d’expiration. Un nombre (en jours) définit l’heure d’expiration sur l’heure actuelle plus le nombre. La valeur par défaut est `undefined`.
   * secure: A `boolean` value that specifies the `Secure` attribute of the cookie. La valeur par défaut est `false`.
   * path: A `String` value to use as the `Path` attribute of the cookie. La valeur par défaut est `undefined`.

**Renvoie**

Le cookie avec la valeur définie.

**Exemple**

```
ContextHub.Utils.Cookie.setItem("name", "mycookie", {
    expires: 3,
    domain: 'localhost',
    path: '/some/directory',
    secure: true
});
```

#### vanish(filter, options) {#vanish-filter-options}

Supprime tous les cookies répondant aux critères d’un filtre donné. Les cookies sont mis en correspondance à l’aide de la fonction getKeys et supprimés à l’aide de la fonction removeItem.

**Paramètres**

* ** :** argument `filter`filter à utiliser dans l’appel de la fonction `[getKeys](/help/sites-developing/contexthub-api.md#getkeys-filter)`.

* ** :** argument `options`options à utiliser dans l’appel de la fonction `[removeItem](/help/sites-developing/contexthub-api.md#removeitem-key-options)`.

**Renvoie**

Cette fonction ne retourne pas de valeur.

## ContextHub.Utils.Eventing {#contexthub-utils-eventing}

Vous permet d’associer et de dissocier des fonctions aux événements du magasin ContextHub. Accédez aux objets ContextHub.Utils.Eventing d’un magasin à l’aide de sa propriété [eventing](/help/sites-developing/contexthub-api.md#eventing).

### Fonctions (ContextHub.Utils.Eventing) {#functions-contexthub-utils-eventing}

#### off(name, selector) {#off-name-selector}

Dissocie une fonction d’un événement.

**Paramètres**

* **name:** [nom du événement](/help/sites-developing/contexthub-api.md#contexthub-utils-eventing) pour lequel vous annulez la liaison de la fonction.

* **selector :** sélecteur identifiant l’association. (See the `selector` parameter for the [on](/help/sites-developing/contexthub-api.md#on-name-handler-selector-triggerforpastevents) and [once](/help/sites-developing/contexthub-api.md#once-name-handler-selector-triggerforpastevents) functions).

**Renvoie**

Cette fonction ne renvoie aucune valeur.

#### on(name, handler, selector, triggerForPastEvents) {#on-name-handler-selector-triggerforpastevents}

Associe une fonction à un événement. La fonction est appelée à chaque fois que l’événement se produit. En option, la fonction peut être appelée pour les événements qui se sont produits dans le passé, avant que l’association ne soit établie.

**Paramètres**

* **name :** (chaîne). [Nom de l’événement](/help/sites-developing/contexthub-api.md#contexthub-utils-eventing) auquel vous associez la fonction.

* **handler :** (fonction). Fonction à associer à l’événement.
* **selector:** (Chaîne) Identifiant unique de la liaison. Le sélecteur est nécessaire pour identifier l’association si vous souhaitez utiliser la fonction `off` pour supprimer l’association.

* **triggerForPastEvents :** (booléen). Indique si le gestionnaire doit être exécuté pour les événements survenus dans le passé. Une valeur `true` appelle le gestionnaire pour les événements passés. Une valeur `false`appelle le gestionnaire pour les événements futurs. La valeur par défaut est `true`.

**Renvoie**

When the `triggerForPastEvents` argument is `true`, this function returns a `boolean` value that indicates whether the event occurred in the past:

* `true` : l’événement s’est produit dans le passé et le gestionnaire sera appelé.
* `false` : l’événement ne s’est pas produit dans le passé.

If `triggerForPastEvents` is `false`, this function returns no value.

**Exemple**

L’exemple suivant associe une fonction au événement de données de la banque de géolocalisation. La fonction remplit un élément de la page avec la valeur de l’élément de données de latitude de la banque.

```
<div class="location">
    <p>latitude: <span id="lat"></span></p>
</div>

<script>
    var geostore = ContextHub.getStore("geolocation");
    geostore.eventing.on(ContextHub.Constants.EVENT_DATA_UPDATE,getlat,"getlat");

    function getlat(){
       latitude = geostore.getItem("latitude");
       $("#lat").html(latitude);
    }
</script>
```

#### once(name, handler, selector, triggerForPastEvents) {#once-name-handler-selector-triggerforpastevents}

Associe une fonction à un événement. La fonction est appelée une seule fois, pour la première occurrence de l’événement. En option, la fonction peut être appelée pour l’événement qui s’est produit dans le passé, avant que l’association ne soit établie.

**Paramètres**

* **name :** (chaîne). [Nom de l’événement](/help/sites-developing/contexthub-api.md#contexthub-utils-eventing) auquel vous associez la fonction.

* **handler :** (fonction). Fonction à associer à l’événement.
* **selector:** (Chaîne) Identifiant unique de la liaison. Le sélecteur est nécessaire pour identifier l’association si vous souhaitez utiliser la fonction `off` pour supprimer l’association.

* **triggerForPastEvents :** (booléen). Indique si le gestionnaire doit être exécuté pour les événements survenus dans le passé. Une valeur `true` appelle le gestionnaire pour les événements passés. Une valeur `false`appelle le gestionnaire pour les événements futurs. La valeur par défaut est `true`.

**Renvoie**

When the `triggerForPastEvents` argument is `true`, this function returns a `boolean` value that indicates whether the event occurred in the past:

* `true` : l’événement s’est produit dans le passé et le gestionnaire sera appelé.
* `false` : l’événement ne s’est pas produit dans le passé.

If `triggerForPastEvents` is `false`, this function returns no value.

## ContextHub.Utils.inheritance {#contexthub-utils-inheritance}

Classe d’utilitaire qui permet à un objet d’hériter des propriétés et des méthodes d’un autre objet.

### Fonctions (ContextHub.Utils.inheritance) {#functions-contexthub-utils-inheritance}

#### inherit(child, parent) {#inherit-child-parent}

Permet à l’objet d’hériter des propriétés et des méthodes d’un autre objet.

**Paramètres**

* **child :** (objet). Objet qui hérite des propriétés.
* **parent :** (objet). Objet qui définit les propriétés et les méthodes héritées.

## ContextHub.Utils.JSON {#contexthub-utils-json}

Fournit des fonctions pour sérialiser les objets au format JSON et désérialiser des chaînes JSON en objets.

### Fonctions (ContextHub.Utils.JSON) {#functions-contexthub-utils-json}

#### parse(data) {#parse-data}

Analyse une valeur de chaîne au format JSON et la convertit en objet JavaScript.

**Paramètres**

* **data :** valeur de chaîne au format JSON.

**Renvoie**

Un objet Javascript.

**Exemple**

The code `ContextHub.Utils.JSON.parse("{'city':'Basel','country':'Switzerland','population':'173330'}");` returns the following object:

```
Object {
   city: "Basel",
   country: "Switzerland",
   population: 173330
}
```

#### stringify(data) {#stringify-data}

Sérialise les valeurs Javascript et les objets en valeurs de chaîne au format JSON.

**Paramètres**

* **data :** valeur ou objet à sérialiser. Cette fonction prend en charge des valeurs booléennes, tables, nombres chaînes et dates.

**Renvoie**

La valeur de chaîne sérialisée. Lorsque `data` est une valeur R`egExp`, cette fonction renvoie un objet vide. When `data` is a function, returns `undefined`.

**Exemple**

Le code suivant renvoie `"{'city':'Basel','country':'Switzerland','population':'173330'}":`

```
ContextHub.Utils.JSON.stringify({
   city: "Basel",
   country: "Switzerland",
   population: 173330
});
```

## ContextHub.Utils.JSON.tree {#contexthub-utils-json-tree}

Cette classe facilite la manipulation des objets de données à stocker ou à extraire des magasins ContextHub.

### Fonctions (ContextHub.Utils.JSON.tree) {#functions-contexthub-utils-json-tree}

#### addAllItems() {#addallitems}

Crée une copie d’un objet de données et y ajoute l’arbre de données d’un second objet. La fonction renvoie la copie et ne modifie aucun des objets d’origine. Lorsque les arbres de données des deux objets contiennent des clés identiques, la valeur du second objet remplace la valeur du premier.

**Paramètres**

* **tree :** Objet copié.
* **secondTree :** Objet fusionné avec la copie de l’ `tree` objet.

**Renvoie**

Un objet contenant les données fusionnées.

#### cleanup() {#cleanup}

Crée une copie d’un objet, identifie et supprime les éléments de l’arbre de données qui ne contiennent aucune valeur, une valeur nulle ou indéfinie et renvoie la copie.

**Paramètres**

* **tree :** objet à nettoyer.

**Renvoie**

Copie de l’arbre qui est nettoyé.

#### getItem() {#getitem}

Récupère la valeur d’un objet pour une clé donnée.

**Paramètres**

* **tree :** objet de données.
* **key :** clé de la valeur que vous voulez récupérer.

**Renvoie**

La valeur qui correspond à la clé. Si la clé possède des clés enfants, cette fonction renvoie un objet complexe. When the type of the value for the key is `undefined`, `null` is returned.

**Exemple**

Étudions l’objet Javascript suivant :

```
myObject {
  user: {
    location: {
      city: "Basel",
        details: {
          population: 173330,
          elevation: 260
        }
      }
    }
  }
```

L’exemple de code suivant renvoie la valeur `260` :

```
ContextHub.Utils.JSON.tree.getItem(myObject, "/user/location/details/elevation");
```

L’exemple de code suivant récupère la valeur d’une clé possédant des clés enfant :

```
ContextHub.Utils.JSON.tree.getItem(myObject, "/user");
```

La fonction renvoie l’objet suivant :

```
Object {
  location: {
    city: "Basel",
    details: {
      population: 173330,
      elevation: 260
    }
  }
}
```

#### getKeys() {#getkeys}

Récupère toutes les clés de l’arbre de données d’un objet. En option, vous pouvez récupérer uniquement les clés des enfants d’une clé spécifique. Vous pouvez également spécifier un ordre de tri des clés récupérées.

**Paramètres**

* **tree :** objet à partir duquel récupérer les clés de l’arbre de données.
* **parent :** (facultatif). Clé d’un élément de l’arbre de données pour lequel vous souhaitez récupérer les clés des éléments enfants.
* **order :** (facultatif). Fonction qui détermine l’ordre de tri des clés renvoyées. (Voir [Array.prototype.sort](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/sort) sur le réseau de développeurs Mozilla.)

**Renvoie**

Une table de clés.

**Exemple**

Étudions l’objet suivant :

```
myObject {
  location: {
    weather: {
      temperature: "28C",
      humidity: "77%",
      precipitation: "10%",
      wind: "8km/h"
    },
    city: "Basel",
    country: "Switzerland",
    longitude: 7.5925727,
    latitude: 47.557421
  }
}
```

The `ContextHub.Utils.JSON.tree.getKeys(myObject);` script returns the following array:

```
["/location", "/location/city", "/location/country", "/location/latitude", "/location/longitude", "/location/weather", "/location/weather/humidity", "/location/weather/precipitation", "/location/weather/temperature", "/location/weather/wind"]
```

#### removeItem() {#removeitem}

Crée une copie d’un objet donné, supprime la branche spécifiée de l’arbre de données et renvoie la copie modifiée.

**Paramètres**

* tree : objet de données.
* key : clé à supprimer.

**Renvoie**

Une copie de l’objet de données d’origine avec la clé supprimée.

**Exemple**

Étudions l’objet suivant :

```
myObject {
  one: {
    foo: "bar",
    two: {
      three: {
        four: {
          five: 5,
          six: 6
        }
      }
    }
  }
}
```

L’exemple de script suivant supprime la branche /one/two/three/four de l’arbre de données :

```
myObject = ContextHub.Utils.JSON.tree.removeItem(myObject, "/one/two/three/four");
```

La fonction renvoie l’objet suivant :

```
myObject {
  one: {
    foo: "bar"
  }
}
```

#### sanitizeKey(key) {#sanitizekey-key}

Assainit les valeurs de chaîne pour les rendre utilisables sous forme de clés. Pour assainir une chaîne, cette fonction effectue les actions suivantes :

* Réduit plusieurs barres obliques consécutives en une seule barre oblique.
* Supprime les espaces au début et à la fin de la chaîne.
* Divise le résultat en une table de chaînes délimitées par des barres obliques.

Utilisez la table obtenue pour créer une clé utilisable.  **Paramètres**

* **key:** Le `string` but de l&#39;assainissement.

**Renvoie**

An array of `string` values where each string is the portion of the `key` that was demarcated by slashes. représente la clé assainie. Si la table assainie a une longueur égale à zéro, cette fonction renvoie la valeur `null`.

**Exemple**

The following code sanitizes a string to produce the array `["this", "is", "a", "path"]`, and then generates the key `"/this/is/a/path"` from the array:

```
var key = " / this////is/a/path ";
ContextHub.Utils.JSON.tree.sanitizeKey(key)
"/" + ContextHub.Utils.JSON.tree.sanitizeKey(key).join("/");
```

#### setItem(tree, key, value) {#setitem-tree-key-value}

Ajoute une paire clé/valeur à l’arbre de données d’une copie d’un objet. For information about data trees, see [Persistence](/help/sites-developing/contexthub.md#persistence).

**Paramètres**

* tree : objet de données.
* key : clé à associer à la valeur que vous ajoutez. La clé représente le chemin d’accès à l’élément dans l’arbre de données. Cette fonction appelle `ContextHub.Utils.JSON.tree.sanitize` pour assainir la clé avant de l’ajouter.
* value : valeur à ajouter à l’arbre de données.

**Renvoie**

A copy of the `tree` object that includes the `key`/ `value` pair.

**Exemple**

Étudions le code Javascript suivant :

```
var myObject = {
     user: {
        location: {
           city: "Basel"
           }
        }
     };

var myKey = "/user/location/details";

var myValue = {
      population: 173330,
      elevation: 260
     };

myObject = ContextHub.Utils.JSON.tree.setItem(myObject, myKey, myValue);
```

L’objet myObject a la valeur suivante :

## ContextHub.Utils.storeCandidates {#contexthub-utils-storecandidates}

Vous permet d’enregistrer des magasins candidats et de récupérer les candidats enregistrés.

### Fonctions (ContextHub.Utils.storeCandidates) {#functions-contexthub-utils-storecandidates}

#### getRegisteredCandidates(storeType) {#getregisteredcandidates-storetype}

Renvoie les types de magasins enregistrés en tant que magasins candidats. Récupére les candidats enregistrés d’un type de magasin spécifique ou de tous les types de magasin.

**Paramètres**

* **storeType :** (chaîne). Nom du type de magasin. See the `storeType` parameter of the [ `ContextHub.Utils.storeCandidates.registerStoreCandidate`](/help/sites-developing/contexthub-api.md#contexthub-utils-storecandidates) function.

**Renvoie**

Un objet de types de magasin. Les propriétés de l’objet sont les noms des types de magasin et les valeurs de propriété sont une table des magasins candidats enregistrés.

#### getStoreFromCandidates(storeType) {#getstorefromcandidates-storetype}

Renvoie un type de magasin parmi les candidats enregistrés. Si plus d’un type de magasin du même nom est enregistré, la fonction renvoie le type de magasin avec la priorité la plus élevée.

**Paramètres**

* storeType : (chaîne). Nom du magasin candidat. See the `storeType` parameter of the [ `ContextHub.Utils.storeCandidates.registerStoreCandidate`](/help/sites-developing/contexthub-api.md#registerstorecandidate-store-storetype-priority-applies) function.

**Renvoie**

Un objet qui représente le magasin candidat enregistré. Si le type de magasin demandé n’est pas enregistré, une erreur est générée.

#### getSupportedStoreTypes() {#getsupportedstoretypes}

Renvoie les noms des magasins enregistrés en tant que magasins candidats. Cette fonction ne nécessite aucun paramètre.

**Renvoie**

Une table de valeurs sous forme de chaîne où chaque chaîne correspond au type de magasin avec lequel un magasin candidat a été enregistré. See the `storeType` parameter of the [ `ContextHub.Utils.storeCandidates.registerStoreCandidate`](/help/sites-developing/contexthub-api.md#contexthub-utils-storecandidates) function.

#### registerStoreCandidate(store, storeType, priority, applies) {#registerstorecandidate-store-storetype-priority-applies}

Enregistre un objet magasin en tant que magasin candidat avec un nom et une priorité.

La priorité est un nombre qui indique l’importance des magasins de même nom. Lorsqu’un magasin candidat est enregistré sous le même nom qu’un magasin candidat déjà enregistré, le candidat ayant la priorité la plus élevée est utilisé. Lors de l’enregistrement d’un magasin candidat, le magasin est enregistré uniquement si la priorité est supérieure à celle des magasins candidats enregistrés portant le même nom.

**Paramètres**

* **store :** (objet). Objet magasin à enregistrer en tant que magasin candidat.
* **storeType :** (chaîne). Nom du magasin candidat. Cette valeur est requise lors de la création d’une instance du magasin candidat.
* **priority :** (Numéro) La priorité du candidat au magasin.
* **applies :** (fonction). Fonction à appeler pour évaluer l’applicabilité du magasin dans l’environnement actuel. La fonction doit renvoyer la valeur `true` si le magasin est applicable, et `false` dans le cas contraire. The default value is a function that returns true: `function() {return true;}`

**Exemple**

```
ContextHub.Utils.storeCandidates.registerStoreCandidate(myStoreCandidate,
                                'contexthub.mystorecandiate', 0);
```

