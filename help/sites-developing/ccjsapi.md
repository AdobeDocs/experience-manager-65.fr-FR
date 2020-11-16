---
title: API Javascript pour ClientContext
seo-title: API Javascript pour ClientContext
description: L’API Javascript pour ClientContext
seo-description: L’API Javascript pour ClientContext
uuid: be58998c-f23e-4768-8394-1f1ad3994c4c
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
discoiquuid: a6e5810b-dac5-4137-93cf-5d8d53cacc49
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '3163'
ht-degree: 90%

---


# API Javascript pour ClientContext{#client-context-javascript-api}

## CQ_Analytics.ClientContextMgr {#cq-analytics-clientcontextmgr}

L’objet CQ_Analytics.ClientContextMgr est un singleton qui contient un ensemble de magasins de session auto-enregistrés et fournit des méthodes pour enregistrer, conserver et gérer les magasins de session.

Étend CQ_Analytics.PersistedSessionStore.

### Méthodes {#methods}

#### getRegisteredStore(name) {#getregisteredstore-name}

Retourne un magasin de session d’un nom spécifié. Voir aussi [Accès à un magasin de sessions ](/help/sites-developing/client-context.md#accessing-session-stores).

**Paramètres**

* name : chaîne. Nom du magasin de sessions.

**Renvoie**

Objet CQ_Analytics.SessionStore qui représente le magasin de sessions du nom en question. Renvoie `null` lorsqu’il n’existe pas de magasin pour le nom donné.

#### register(sessionstore) {#register-sessionstore}

Enregistre un magasin de sessions avec ClientContext. Déclenche les événements Storeregister et Storeupdate à la fin de l’opération.

**Paramètres**

* sessionstore : CQ_Analytics.SessionStore. Objet de magasin de session à enregistrer.

**Renvoie**

Aucune valeur retournée.

## CQ_Analytics.ClientContextUtils {#cq-analytics-clientcontextutils}

Fournit des méthodes d’écoute pour l’activation et l’enregistrement du magasin de sessions. See also [Checking That a Session Store is Defined and Initialized](/help/sites-developing/client-context.md#checking-that-a-session-store-is-defined-and-initialized).

### Méthodes {#methods-1}

#### onStoreInitialized(storeName, callback, delay) {#onstoreinitialized-storename-callback-delay}

Enregistre une fonction de rappel appelée lors de l’initialisation d’un magasin de sessions. Dans le cas de magasins initialisés plusieurs fois, spécifiez un délai de rappel afin que la fonction de rappel ne soit appelée qu’une seule fois :

* Lorsque le magasin est initialisé pendant la période de report d’une initialisation précédente, l’appel de fonction précédent est annulé. Ensuite, la fonction est appelée à nouveau pour l’initialisation en cours.
* Si la période de report se termine avant une initialisation ultérieure, la fonction de rappel est exécutée deux fois.

Par exemple, un magasin de sessions est basé sur un objet JSON et récupéré via une requête JSON. Les scénarios d’initialisation suivants sont possibles :

* La requête est terminée, les données sont récupérées et chargées dans le magasin. Dans ce cas, l’initialisation se produit une fois.
* La requête échoue (expiration du délai). Dans ce cas, l’initialisation ne se produit pas et les données ne sont pas chargées dans le magasin.
* Le magasin est pré-rempli avec des valeurs par défaut (propriétés init), mais la demande échoue (expiration du délai). Il n’y a qu’une seule initialisation avec des valeurs par défaut.
* Le magasin est pré-rempli.

When the delay is set to `true` or a number of milliseconds, the method waits before calling the callback method. Si un autre événement d’initialisation est déclenché avant le dépassement du délai, il attend que le délai soit dépassé sans événement d’initialisation. Cela permet d’attendre qu’un deuxième événement d’initialisation soit déclenché et appelle la fonction de rappel dans le cas le plus optimal.

**Paramètres**

* storeName : chaîne. Nom du magasin de sessions à ajouter à l’écouteur.
* callback : fonction. Fonction à appeler lors de l’initialisation du magasin.
* delay : booléen ou nombre. Durée de report de l’appel à la fonction de rappel, en millisecondes. A boolean value of `true` uses the default delay of `200 ms`. A boolean value of `false` or a negative number causes no delay to be used.

**Renvoie**

Aucune valeur retournée.

#### onStoreRegistered(storeName, callback) {#onstoreregistered-storename-callback}

Enregistre une fonction de rappel appelée lors de l’enregistrement d’un magasin de sessions. The register event occurs when a store is registered to [CQ_Analytics.ClientContextMgr](#cq-analytics-clientcontextmgr).

**Paramètres**

* storeName : chaîne. Nom du magasin de sessions à ajouter à l’écouteur.
* callback : fonction. Fonction à appeler lors de l’initialisation du magasin.

**Renvoie**

Aucune valeur retournée.

## CQ_Analytics.JSONPStore {#cq-analytics-jsonpstore}

Un magasin de session non conservé qui contient des données JSON. Les données sont extraites d’un service JSONP externe. Use the `getInstance` or `getRegisteredInstance` method to create an instance of this class.

Étend CQ_Analytics.JSONStore.

### Propriétés {#properties}

Voir CQ_Analytics.JSONStore et CQ_Analytics.SessonStore pour les propriétés héritées.

### Méthodes {#methods-2}

Voir aussi CQ_Analytics.JSONStore et CQ_Analytics.SessonStore pour connaître les méthodes héritées.

#### getInstance(storeName, serviceURL, dynamicData, deferLoading, loadingCallback) {#getinstance-storename-serviceurl-dynamicdata-deferloading-loadingcallback}

Crée un objet CQ_Analytics.JSONPStore.

**Paramètres**

* storeName : chaîne. Nom à utiliser comme propriété STORENAME. La valeur de la propriété STOREKEY est définie sur storeName avec tous les caractères en majuscules. Si aucun nom de magasin n’est fourni, la méthode renvoie null.
* serviceURL : chaîne. URL du service JSONP
* dynamicData : objet (facultatif). Données JSON à ajouter aux données d’initialisation du magasin avant l’appel de la fonction de rappel.
* deferLoading : booléen (facultatif). Une valeur true empêche le service JSONP d’être appelé lors de la création d’objet. Une valeur false entraîne l’appel du service JSONP.
* loadingCallback : (Facultatif) Chaîne. Nom de la fonction à appeler pour le traitement de l’objet JSONP renvoyé par le service JSONP. La fonction de rappel doit définir un seul paramètre qui est un objet CQ_Analytics.JSONPStore.

**Renvoie**

Le nouvel objet CQ_Analytics.JSONPStore, ou la valeur null si storeName a la valeur null.

#### getServiceURL() {#getserviceurl}

Récupère l’URL du service JSONP que cet objet utilise pour récupérer les données JSON.

**Paramètres**

Aucune.

**Renvoie**

Chaîne qui représente l’URL du service ou valeur null si aucune URL de service n’a été configurée.

#### load(serviceURL, dynamicData, callback) {#load-serviceurl-dynamicdata-callback}

Appelle le service JSONP. L’URL JSONP est l’URL du service avec comme suffixe le nom d’une fonction de rappel.

**Paramètres**

* serviceURL : chaîne (facultatif). Service JSONP à appeler. Une valeur null entraîne l’utilisation de l’URL de service déjà configurée. Une valeur non nulle définit le service JSONP à utiliser pour cet objet. (Voir setServiceURL.)
* dynamicData : objet (facultatif). Données JSON à ajouter aux données d’initialisation du magasin avant l’appel de la fonction de rappel.
* callback : chaîne (facultatif). Nom de la fonction à appeler pour le traitement de l’objet JSONP renvoyé par le service JSONP. La fonction de rappel doit définir un seul paramètre qui est un objet CQ_Analytics.JSONPStore.

**Renvoie**

Aucune valeur retournée.

#### registerNewInstance(storeName, serviceURL, dynamicData, callback) {#registernewinstance-storename-serviceurl-dynamicdata-callback}

Crée un objet CQ_Analytics.JSONPStore et enregistre le magasin dans le contexte client.

**Paramètres**

* storeName : chaîne. Nom à utiliser comme propriété STORENAME. La valeur de la propriété STOREKEY est définie sur storeName avec tous les caractères en majuscules. Si aucun nom de magasin n’est fourni, la méthode renvoie null.
* serviceURL : chaîne (facultatif). URL du service JSONP
* dynamicData : objet (facultatif). Données JSON à ajouter aux données d’initialisation du magasin avant l’appel de la fonction de rappel.
* callback : chaîne (facultatif). Nom de la fonction à appeler pour le traitement de l’objet JSONP renvoyé par le service JSONP. La fonction de rappel doit définir un seul paramètre qui est un objet CQ_Analytics.JSONPStore.

**Renvoie**

Objet CQ_Analytics.JSONPStore enregistré.

#### setServiceURL(serviceURL) {#setserviceurl-serviceurl}

Définit l’URL du service JSONP à utiliser pour récupérer les données JSON.

**Paramètres**

* serviceURL : chaîne. URL du service JSONP qui fournit des données JSON

**Renvoie**

Aucune valeur retournée.

## CQ_Analytics.JSONStore {#cq-analytics-jsonstore}

Conteneur pour un objet JSON. Créez une instance de cette classe pour créer un magasin de sessions non persistant contenant des données JSON :

`myjsonstore = new CQ_Analytics.JSONStore`

Vous pouvez définir un ensemble de données qui remplit le magasin lors de l’initialisation.

Étend CQ_Analytics.SessionStore.

### Propriétés {#properties-1}

#### STOREKEY {#storekey}

Clé qui identifie le magasin. Utilisez la méthode `getInstance` pour récupérer cette valeur.

#### STORENAME {#storename}

Nom du magasin Utilisez la méthode `getInstance` pour récupérer cette valeur.

### Méthodes {#methods-3}

Voir aussi CQ_Analytics.SessionStore pour connaître les méthodes héritées.

#### effacer() {#clear}

Supprime les données du magasin de sessions et supprime toutes les propriétés d’initialisation.

**Paramètres**

Aucune.

**Renvoie**

Aucune valeur retournée.

#### getInstance(storeName, jsonData) {#getinstance-storename-jsondata}

Crée un objet CQ_Analytics.JSONStore avec un nom donné et initialisé avec les données JSON spécifiées (appelle la méthode initJSON).

**Paramètres**

* storeName : chaîne. Nom à utiliser comme propriété STORENAME. La valeur de la propriété STOREKEY est définie sur storeName avec tous les caractères en majuscules.
* jsonData : objet. Objet qui contient des données JSON.

**Renvoie**

L’objet CQ_Analytics.JSONStore.

#### getJSON() {#getjson}

Récupère les données du magasin de sessions au format JSON.

**Paramètres**

Aucune.

**Renvoie**

Objet qui représente les données du magasin au format JSON.

#### init() {#init}

Efface le magasin de sessions et l’initialise avec la propriété d’initialisation. Sets the initialization flag to `true` and then fires the `initialize` and `update` events.

**Paramètres**

Aucune.

**Renvoie**

Aucune donnée renvoyée

#### initJSON(jsonData, doNotClear) {#initjson-jsondata-donotclear}

Crée des propriétés d’initialisation à partir des données d’un objet JSON. Vous pouvez éventuellement supprimer toutes les propriétés d’initialisation existantes.

Les noms des propriétés sont dérivés de la hiérarchie des données dans l’objet JSON. L’exemple de code suivant représente un objet JSON :

```xml
{
A: "valueA",
B: {
     B1: "valueBB1"
    }
}
```

Pour cet exemple, les propriétés suivantes sont créées dans le magasin :

```xml
A: "valueA"
B/B1: "valueBB1"
```

**Paramètres**

* jsonData : objet JSON contenant les données à stocker.
* doNotClear : La valeur true préserve les propriétés d’initialisation existantes et ajoute celles dérivées de l’objet JSON. La valeur false supprime les propriétés d’initialisation existantes avant d’ajouter celles dérivées de l’objet JSON.

**Renvoie**

Aucune valeur retournée.

#### registerNewInstance(storeName, jsonData) {#registernewinstance-storename-jsondata}

Crée un objet CQ_Analytics.JSONStore avec un nom donné et initialisé avec les données JSON spécifiées (appelle la méthode initJSON). Le nouvel objet est automatiquement enregistré avec Clickstream Cloud Manager.

**Paramètres**

* storeName : chaîne. Nom à utiliser comme propriété STORENAME. La valeur de la propriété STOREKEY est définie sur storeName avec tous les caractères en majuscules.
* jsonData : objet. Objet qui contient des données JSON.

**Renvoie**

L’objet CQ_Analytics.JSONStore.

## CQ_Analytics.Observable {#cq-analytics-observable}

Déclenche des événements et permet à d’autres objets d’écouter ces événements et de réagir. Les classes qui étendent cette classe peuvent déclencher des événements qui provoquent l’appel des écouteurs.

### Méthodes {#methods-4}

#### addListener(event, fct, scope) {#addlistener-event-fct-scope}

Enregistre un écouteur pour un événement. Voir aussi [Création d’un écouteur pour réagir à une mise à jour de magasin de sessions](/help/sites-developing/client-context.md#creating-a-listener-to-react-to-a-session-store-update).

**Paramètres**

* event : chaîne. Nom de l’événement à écouter.
* fct : fonction. Fonction appelée lorsque l’événement se produit.
* scope : (Facultatif) Objet. Champ d’application selon lequel exécuter la fonction de gestionnaire. Contexte &quot;this&quot; de la fonction handler.

**Renvoie**

Aucune valeur retournée.

#### removeListener(event, fct) {#removelistener-event-fct}

Supprime un gestionnaire d’événements donné pour un événement.

**Paramètres**

* event : chaîne. Nom de l’évènement.
* fct : fonction. Gestionnaire d’événement.

**Renvoie**

Aucune valeur retournée.

## CQ_Analyics.PersistedJSONPStore {#cq-analyics-persistedjsonpstore}

Conteneur persistant d’un objet JSON récupéré à partir d’un service JSONP distant.

Étend CQ_Analytics.PersistedJSONStore.

### Méthodes {#methods-5}

Voir aussi CQ_Analytics.PersistedJSONStore pour connaître les méthodes héritées.

#### getInstance(storeName, serviceURL, dynamicData, deferLoading, loadingCallback) {#getinstance-storename-serviceurl-dynamicdata-deferloading-loadingcallback-1}

Crée un objet CQ_Analytics.PersistedJSONPStore.

**Paramètres**

* storeName : chaîne. Nom à utiliser comme propriété STORENAME. La valeur de la propriété STOREKEY est définie sur storeName avec tous les caractères en majuscules. Si aucun nom de magasin n’est fourni, la méthode renvoie null.
* serviceURL : chaîne. URL du service JSONP
* dynamicData : objet (facultatif). Données JSON à ajouter aux données d’initialisation du magasin avant l’appel de la fonction de rappel.
* deferLoading : booléen (facultatif). Une valeur true empêche le service JSONP d’être appelé lors de la création d’objet. Une valeur false entraîne l’appel du service JSONP.
* loadingCallback : (Facultatif) Chaîne. Nom de la fonction à appeler pour le traitement de l’objet JSONP renvoyé par le service JSONP. La fonction de rappel doit définir un seul paramètre qui est un objet CQ_Analytics.JSONPStore.

**Renvoie**

Nouvel objet CQ_Analytics.PersistedJSONPStore, ou null si storeName a la valeur null.

#### getServiceURL() {#getserviceurl-1}

Récupère l’URL du service JSONP que cet objet utilise pour récupérer les données JSON.

**Paramètres**

Aucune.

**Renvoie**

Chaîne qui représente l’URL du service ou valeur null si aucune URL de service n’a été configurée.

#### load(serviceURL, dynamicData, callback) {#load-serviceurl-dynamicdata-callback-1}

Appelle le service JSONP. L’URL JSONP est l’URL du service avec comme suffixe le nom d’une fonction de rappel.

**Paramètres**

* serviceURL : chaîne (facultatif). Service JSONP à appeler. Une valeur null entraîne l’utilisation de l’URL de service déjà configurée. Une valeur non nulle définit le service JSONP à utiliser pour cet objet. (Voir setServiceURL.)
* dynamicData : objet (facultatif). Données JSON à ajouter aux données d’initialisation du magasin avant l’appel de la fonction de rappel.
* callback : chaîne (facultatif). Nom de la fonction à appeler pour le traitement de l’objet JSONP renvoyé par le service JSONP. La fonction de rappel doit définir un seul paramètre qui est un objet CQ_Analytics.JSONPStore.

**Renvoie**

Aucune valeur retournée.

#### registerNewInstance(storeName, serviceURL, dynamicData, callback) {#registernewinstance-storename-serviceurl-dynamicdata-callback-1}

CQ_Analytics.PersistedJSONPStore crée un objet CQ_Analytics.PersistedJSONPStore et enregistre le magasin avec le contexte client.

**Paramètres**

* storeName : chaîne. Nom à utiliser comme propriété STORENAME. La valeur de la propriété STOREKEY est définie sur storeName avec tous les caractères en majuscules. Si aucun nom de magasin n’est fourni, la méthode renvoie null.
* serviceURL : chaîne (facultatif). URL du service JSONP
* dynamicData : objet (facultatif). Données JSON à ajouter aux données d’initialisation du magasin avant l’appel de la fonction de rappel.
* callback : chaîne (facultatif). Nom de la fonction à appeler pour le traitement de l’objet JSONP renvoyé par le service JSONP. La fonction de rappel doit définir un seul paramètre qui est un objet CQ_Analytics.JSONPStore.

**Renvoie**

Objet CQ_Analytics.PersistedJSONPStore enregistré.

#### setServiceURL(serviceURL) {#setserviceurl-serviceurl-1}

Définit l’URL du service JSONP à utiliser pour récupérer les données JSON.

**Paramètres**

* serviceURL : chaîne. URL du service JSONP qui fournit des données JSON

**Renvoie**

Aucune valeur retournée.

## CQ_Analytics.PersistedJSONStore {#cq-analytics-persistedjsonstore}

Conteneur persistant d’un objet JSON.

Extends `CQ_Analytics.PersistedSessionStore`.

### Propriétés {#properties-2}

#### STOREKEY {#storekey-1}

Clé qui identifie le magasin. Utilisez la méthode `getInstance` pour récupérer cette valeur.

#### STORENAME {#storename-1}

Nom du magasin Utilisez la méthode `getInstance` pour récupérer cette valeur.

### Méthodes {#methods-6}

Voir aussi CQ_Analytics.PersistedSessionStore pour connaître les méthodes héritées.

#### getInstance(storeName, jsonData) {#getinstance-storename-jsondata-1}

Crée un objet CQ_Analytics.PersistedJSONStore avec un nom donné et initialisé avec les données JSON spécifiées (appelle la méthode initJSON).

**Paramètres**

* storeName : chaîne. Nom à utiliser comme propriété STORENAME. La valeur de la propriété STOREKEY est définie sur storeName avec tous les caractères en majuscules.
* jsonData : objet. Objet qui contient des données JSON.

**Renvoie**

Objet CQ_Analytics.PersistedJSONStore.

#### getJSON() {#getjson-1}

Récupère les données du magasin de sessions au format JSON.

**Paramètres**

Aucune.

**Renvoie**

Objet qui représente les données du magasin au format JSON.

#### initJSON(jsonData, doNotClear) {#initjson-jsondata-donotclear-1}

Crée des propriétés d’initialisation à partir des données d’un objet JSON. Vous pouvez éventuellement supprimer toutes les propriétés d’initialisation existantes.

Les noms des propriétés sont dérivés de la hiérarchie des données dans l’objet JSON. L’exemple de code suivant représente un objet JSON :

```xml
{
A: "valueA",
B: {
     B1: "valueBB1"
    }
}
```

Pour cet exemple, les propriétés suivantes sont créées dans le magasin :

```xml
A: "valueA"
B/B1: "valueBB1"
```

**Paramètres**

* jsonData : objet JSON contenant les données à stocker.
* doNotClear : La valeur true préserve les propriétés d’initialisation existantes et ajoute celles dérivées de l’objet JSON. La valeur false supprime les propriétés d’initialisation existantes avant d’ajouter celles dérivées de l’objet JSON.

**Renvoie**

Aucune valeur retournée.

#### registerNewInstance(storeName, jsonData) {#registernewinstance-storename-jsondata-1}

Crée un objet CQ_Analytics.PersistedJSONStore avec un nom donné et initialisé avec les données JSON spécifiées (appelle la méthode initJSON). Le nouvel objet est automatiquement enregistré ave le Client Context Manager.

**Paramètres**

* storeName : chaîne. Nom à utiliser comme propriété STORENAME. La valeur de la propriété STOREKEY est définie sur storeName avec tous les caractères en majuscules.
* jsonData : objet. Objet qui contient des données JSON.

**Renvoie**

Objet CQ_Analytics.PersistedJSONStore.

## CQ_Analytics.PersistedSessionStore {#cq-analytics-persistedsessionstore}

Conteneur de propriétés et de valeurs. Les données sont conservées à l’aide de CQ_Analytics.SessionPersistence. Créez une instance de cette classe pour créer un magasin de sessions persistant :

`mypersistedstore = new CQ_Analytics.PersistedSessionStore`

Étend CQ_Analytics.SessionStore.

### Propriétés {#properties-3}

#### STOREKEY {#storekey-2}

La valeur par défaut est `key`.

### Méthodes {#methods-7}

Voir CQ_Analytics.SessionStore pour connaître les méthodes héritées.

When the inherited methods `clear`, `setProperty`, `setProperties`, `removeProperty` are used to change the store data, the changes are automatically persisted, unless the changed properties are flagged as notPersisted.

#### getStoreKey() {#getstorekey}

Retrieves the `STOREKEY` property.

**Paramètres**

Aucune

**Renvoie**

The value of the `STOREKEY` property.

#### isPersisted(name) {#ispersisted-name}

Détermine si une propriété de données est persistante.

**Paramètres**

* name : chaîne. Nom de la propriété.

**Renvoie**

Valeur booléenne `true` si la propriété est persistante et `false` si la valeur n’est pas une propriété persistante.

#### persist() {#persist}

Rend persistant le magasin de session. The default persistence mode uses browser `localStorage` using `ClientSidePersistence` as the name ( `window.localStorage.set("ClientSidePersistance", store);`)

Si localStorage n’est pas disponible ou inscriptible, le magasin est conservé en tant que propriété de la fenêtre.

Déclenche l’événement `persist` à la fin de l’opération.

**Paramètres**

Aucune

**Renvoie**

Aucune valeur retournée.

#### reset(deferEvent) {#reset-deferevent}

Supprime toutes les propriétés de données du magasin et conserve le magasin. En option, ne déclenche pas l’événement `udpate` à la fin de l’opération.

**Paramètres**

* deferEvent : une valeur true empêche l’activation de l’événement `update`. Une valeur `false` provoque le déclenchement de l’événement de mise à jour.

**Renvoie**

Aucune valeur retournée.

#### setNonPersisted(name) {#setnonpersisted-name}

Marque une propriété de données comme non persistante.

**Paramètres**

* name : chaîne. Nom de la propriété qui ne doit pas être persistante.

**Renvoie**

Aucune valeur retournée.

## CQ_Analytics.SessionStore {#cq-analytics-sessionstore}

CQ_Analytics.SessionStore représente un magasin de sessions. Créez une instance de cette classe pour créer un magasin de sessions :

`mystore = new CQ_Analytics.SessionStore`

Étend CQ_Analytics.Observable.

### Propriétés {#properties-4}

#### STORENAME {#storename-2}

Nom du magasin de sessions. Utilisez getName pour récupérer la valeur de cette propriété.

### Méthodes {#methods-8}

#### addInitProperty(name, value) {#addinitproperty-name-value}

Ajoute une propriété et une valeur aux données d’initialisation du magasin de sessions.

Utilisez loadInitProperties pour remplir les données du magasin de sessions avec les valeurs d’initialisation.

**Paramètres**

* name : chaîne. Nom de la propriété à ajouter.
* value : chaîne. Valeur de la propriété à ajouter.

**Renvoie**

Aucune valeur retournée.

#### effacer() {#clear-1}

Supprime toutes les propriétés de données du magasin.

**Paramètres**

Aucune.

**Renvoie**

Aucune valeur retournée.

#### getData(excluded) {#getdata-excluded}

Renvoie les données du magasin. Facultativement, exclut les propriétés de nom des données. Appelle la méthode `init` si la propriété data du magasin n’existe pas.

**Paramètres**

excluded : matrice des noms des propriétés à exclure des données renvoyées (facultatif).

**Renvoie**

Objet de propriétés et leurs valeurs.

#### getInitProperty(name) {#getinitproperty-name}

Récupère la valeur d’une propriété de données.

**Paramètres**

* name : chaîne. Nom de la propriété de données à récupérer.

**Renvoie**

Valeur de la propriété de données. Renvoie `null` si le magasin de sessions ne contient aucune propriété portant le nom spécifié.

#### getName() {#getname}

Renvoie le nom du magasin de sessions.

**Paramètres**

Aucune.

**Renvoie**

Valeur sous forme de chaîne qui représente le nom du magasin.

#### getProperty(name, raw) {#getproperty-name-raw}

Renvoie la valeur d’une propriété. La valeur est renvoyée en tant que propriété brute ou valeur filtrée XSS. Appelle la méthode `init` si la propriété data du magasin n’existe pas.

**Paramètres**

* name : chaîne. Nom de la propriété de données à récupérer.
* raw : booléen. Une valeur true renvoie la valeur de la propriété brute à renvoyer. Une valeur false indique que la valeur renvoyée est filtrée XSS.

**Renvoie**

Valeur de la propriété de données.

#### getPropertyNames(excluded) {#getpropertynames-excluded}

Renvoie les noms des propriétés que contient le magasin de sessions. Appelle la méthode `init` si la propriété data du magasin n’existe pas.

**Paramètres**

excluded : matrice des noms des propriétés à exclure des résultats (facultatif).

**Renvoie**

Matrice de valeurs sous forme de chaîne représentant les noms des propriétés de session.

#### getSessionStore() {#getsessionstore}

Renvoie le magasin de sessions associé à l’objet actif.

**Paramètres**

Aucune.

**Renvoie**

this

#### init() {#init-1}

Marque le magasin comme initialisé et déclenche l’événement `initialize`.

**Paramètres**

Aucune.

**Renvoie**

Aucune valeur retournée.

#### isInitialized() {#isinitialized}

Indique si le magasin de sessions est initialisé.

**Paramètres**

Aucune.

**Renvoie**

Valeur `true` si le magasin est initialisé et `false`  s’il ne l’est pas.

#### loadInitProperties(obj, setValues) {#loadinitproperties-obj-setvalues}

Ajoute les propriétés de l’objet en question aux données d’initialisation du magasin de sessions. Facultativement, les données d’objet sont également ajoutées aux données du magasin.

**Paramètres**

* obj : objet qui contient des propriétés énumérables.
* setValues : si cette propriété est définie sur true, les propriétés obj sont ajoutées aux données du magasin de sessions à condition que les données du magasin n’incluent pas déjà une propriété du même nom. Si la valeur est false, aucune donnée n’est ajoutée aux données du magasin de sessions.

**Renvoie**

Aucune valeur retournée.

#### removeProperty(name) {#removeproperty-name}

Supprime une propriété du magasin de sessions. Déclenche l’événement `update` à la fin de l’opération. Appelle la méthode `init` si la propriété data du magasin n’existe pas.

**Paramètres**

* name : chaîne. Nom de la propriété à supprimer.

**Renvoie**

Aucune valeur retournée.

#### reset() {#reset}

Restaure les valeurs initiales du magasin de données. L’implémentation par défaut supprime simplement toutes les données. Déclenche l’événement `update` à la fin de l’opération.

**Paramètres**

Aucune.

**Renvoie**

Aucune valeur retournée.

#### setProperties(properties) {#setproperties-properties}

Définit les valeurs de plusieurs propriétés. Déclenche l’événement `update` à la fin de l’opération. Appelle la méthode `init` si la propriété data du magasin n’existe pas.

**Paramètres**

* Properties : objet. Objet qui contient des propriétés énumérables. Chaque nom et valeur de la propriété est ajouté au magasin.

**Renvoie**

Aucune valeur retournée.

#### setProperty(name, value) {#setproperty-name-value}

Définit les valeurs d’une propriété. Déclenche l’événement `update` à la fin de l’opération. Appelle la méthode `init` si la propriété data du magasin n’existe pas.

**Paramètres**

* name : chaîne. Nom de la propriété.
* value : chaîne. Valeur de propriété.

**Renvoie**

Aucune valeur retournée.
