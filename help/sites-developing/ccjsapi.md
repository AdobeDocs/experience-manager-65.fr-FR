---
title: API JavaScript ClientContext
seo-title: Client Context JavaScript API
description: Découvrez l’API JavaScript pour ClientContext dans Adobe Experience Manager.
seo-description: The JavaScript API for Client Context
uuid: be58998c-f23e-4768-8394-1f1ad3994c4c
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: personalization
content-type: reference
discoiquuid: a6e5810b-dac5-4137-93cf-5d8d53cacc49
feature: Context Hub
exl-id: 24bdf9fc-71e6-4b99-9dad-0f41a5e36b98
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '3157'
ht-degree: 56%

---

# API JavaScript ClientContext{#client-context-javascript-api}

## CQ_Analytics.ClientContextMgr {#cq-analytics-clientcontextmgr}

L’objet CQ_Analytics.ClientContextMgr est un singleton qui contient un ensemble de magasins de sessions auto-enregistrés et fournit des méthodes d’enregistrement, de conservation et de gestion des magasins de sessions.

Étend CQ_Analytics.PersistedSessionStore.

### Méthodes {#methods}

#### getRegisteredStore(name) {#getregisteredstore-name}

Retourne un magasin de session d’un nom spécifié. Voir aussi [Accès à un magasin de sessions](/help/sites-developing/client-context.md#accessing-session-stores).

**Paramètres**

* name : chaîne. Nom du magasin de sessions.

**Renvoie**

Objet CQ_Analytics.SessionStore qui représente le magasin de sessions du nom en question. Renvoie `null` lorsqu’il n’existe pas de magasin pour le nom donné.

#### register(sessionstore) {#register-sessionstore}

Enregistre un magasin de sessions avec ClientContext. Déclenche les événements storeregister et storeupdate à la fin.

**Paramètres**

* sessionstore : CQ_Analytics.SessionStore. Objet magasin de sessions à enregistrer.

**Renvoie**

Aucune valeur renvoyée.

## CQ_Analytics.ClientContextUtils {#cq-analytics-clientcontextutils}

Fournit des méthodes d’écoute pour l’activation et l’enregistrement du magasin de sessions. Consultez également la section [Vérification de la définition et de l’initialisation d’un magasin de session](/help/sites-developing/client-context.md#checking-that-a-session-store-is-defined-and-initialized).

### Méthodes {#methods-1}

#### onStoreInitialized(storeName, callback, delay) {#onstoreinitialized-storename-callback-delay}

Enregistre une fonction de rappel appelée lors de l’initialisation d’un magasin de sessions. Pour les magasins initialisés plusieurs fois, spécifiez un délai de rappel afin que la fonction de rappel ne soit appelée qu’une seule fois :

* Lorsque le magasin est initialisé pendant la période de délai d’une initialisation précédente, l’appel de la fonction précédente est annulé et la fonction est de nouveau appelée pour l’initialisation actuelle.
* Si le délai expire avant une initialisation ultérieure, la fonction de rappel est exécutée deux fois.

Par exemple, un magasin de sessions est basé sur un objet JSON et récupéré via une requête JSON. Les scénarios d’initialisation suivants sont possibles :

* La requête est terminée, les données sont récupérées et chargées dans le magasin. Dans ce cas, l’initialisation se produit une seule fois.
* La requête échoue (expiration du délai). Dans ce cas, l’initialisation n’a pas lieu et le magasin ne contient aucune donnée.
* Le magasin est pré-rempli avec des valeurs par défaut (propriétés init), mais la demande échoue (expiration du délai). Il n’existe qu’une seule initialisation avec des valeurs par défaut.
* Le magasin est prérempli.

Lorsque le délai est défini sur `true` pendant plusieurs millisecondes, la méthode attend avant d’appeler la méthode de rappel. Si un autre événement d’initialisation est déclenché avant le dépassement du délai, il attend que le délai soit dépassé sans événement d’initialisation. Cela permet d’attendre le déclenchement d’un second événement d’initialisation et d’appeler la fonction de rappel dans le cas le plus optimisé.

**Paramètres**

* storeName : chaîne. Nom du magasin de sessions auquel ajouter le récepteur.
* callback : fonction. Fonction à appeler lors de l’initialisation du magasin.
* delay : booléen ou nombre. Durée de report de l’appel à la fonction de rappel, en millisecondes. Une valeur booléenne `true` utilise le délai par défaut de `200 ms`. Une valeur booléenne `false` ou un nombre négatif n’entraîne aucun report.

**Renvoie**

Aucune valeur renvoyée.

#### onStoreRegistered(storeName, rappel) {#onstoreregistered-storename-callback}

Enregistre une fonction de rappel appelée lors de l’enregistrement d’un magasin de sessions. L’événement register se produit lorsqu’un magasin est enregistré sur [CQ_Analytics.ClientContextMgr](#cq-analytics-clientcontextmgr).

**Paramètres**

* storeName : chaîne. Nom du magasin de sessions auquel ajouter le récepteur.
* callback : fonction. Fonction à appeler lors de l’initialisation du magasin.

**Renvoie**

Aucune valeur renvoyée.

## CQ_Analytics.JSONPStore {#cq-analytics-jsonpstore}

Un magasin de session non conservé qui contient des données JSON. Les données sont extraites d’un service JSONP externe. Utilisez la méthode `getInstance` ou `getRegisteredInstance` pour créer une instance de cette classe.

Étend CQ_Analytics.JSONStore.

### Propriétés {#properties}

Voir CQ_Analytics.JSONStore et CQ_Analytics.SessionStore pour les propriétés héritées.

### Méthodes {#methods-2}

Voir aussi CQ_Analytics.JSONStore et CQ_Analytics.SessionStore pour connaître les méthodes héritées.

#### getInstance(storeName, serviceURL, dynamicData, deferLoading, loadingCallback) {#getinstance-storename-serviceurl-dynamicdata-deferloading-loadingcallback}

Crée un objet CQ_Analytics.JSONPStore.

**Paramètres**

* storeName : chaîne. Nom à utiliser comme propriété STORENAME. La valeur de la propriété STOREKEY est définie sur storeName avec tous les caractères en majuscules. Si aucune propriété storeName n’est fournie, la méthode renvoie null.
* serviceURL : chaîne. URL du service JSONP
* dynamicData : objet (facultatif). Données JSON à ajouter aux données d’initialisation du magasin avant l’appel de la fonction de rappel.
* deferLoading : booléen (facultatif). Une valeur true empêche le service JSONP d’être appelé lors de la création d’objet. Une valeur false entraîne l’appel du service JSONP.
* loadingCallback : chaîne (facultatif). Nom de la fonction à appeler pour le traitement de l’objet JSONP renvoyé par le service JSONP. La fonction de rappel doit définir un seul paramètre qui est un objet CQ_Analytics.JSONPStore.

**Renvoie**

Le nouvel objet CQ_Analytics.JSONPStore, ou la valeur null si storeName est null.

#### getServiceURL() {#getserviceurl}

Récupère l’URL du service JSONP que cet objet utilise pour récupérer les données JSON.

**Paramètres**

Aucun.

**Renvoie**

Chaîne représentant l’URL du service ou valeur nulle si aucune URL de service n’a été configurée.

#### load(serviceURL, dynamicData, callback) {#load-serviceurl-dynamicdata-callback}

Appelle le service JSONP. L’URL JSONP est l’URL du service avec comme suffixe le nom d’une fonction de rappel.

**Paramètres**

* serviceURL : chaîne (facultatif). Service JSONP à appeler. Une valeur null entraîne l’utilisation de l’URL de service déjà configurée. Une valeur non nulle définit le service JSONP à utiliser pour cet objet. (Voir setServiceURL.)
* dynamicData : objet (facultatif). Données JSON à ajouter aux données d’initialisation du magasin avant l’appel de la fonction de rappel.
* callback : chaîne (facultatif). Nom de la fonction à appeler pour le traitement de l’objet JSONP renvoyé par le service JSONP. La fonction de rappel doit définir un seul paramètre qui est un objet CQ_Analytics.JSONPStore.

**Renvoie**

Aucune valeur renvoyée.

#### registerNewInstance(storeName, serviceURL, dynamicData, callback) {#registernewinstance-storename-serviceurl-dynamicdata-callback}

Crée un objet CQ_Analytics.JSONPStore et enregistre le magasin avec ClientContext.

**Paramètres**

* storeName : chaîne. Nom à utiliser comme propriété STORENAME. La valeur de la propriété STOREKEY est définie sur storeName avec tous les caractères en majuscules. Si aucune propriété storeName n’est fournie, la méthode renvoie null.
* serviceURL : chaîne (facultatif). URL du service JSONP.
* dynamicData : objet (facultatif). Données JSON à ajouter aux données d’initialisation du magasin avant l’appel de la fonction de rappel.
* callback : chaîne (facultatif). Nom de la fonction à appeler pour le traitement de l’objet JSONP renvoyé par le service JSONP. La fonction de rappel doit définir un seul paramètre qui est un objet CQ_Analytics.JSONPStore.

**Renvoie**

Objet CQ_Analytics.JSONPStore enregistré.

#### setServiceURL(serviceURL) {#setserviceurl-serviceurl}

Définit l’URL du service JSONP à utiliser pour récupérer les données JSON.

**Paramètres**

* serviceURL : chaîne. URL du service JSONP qui fournit des données JSON.

**Renvoie**

Aucune valeur renvoyée.

## CQ_Analytics.JSONStore {#cq-analytics-jsonstore}

Conteneur pour un objet JSON. Créez une instance de cette classe pour créer un magasin de sessions non persistant contenant des données JSON :

`myjsonstore = new CQ_Analytics.JSONStore`

Vous pouvez définir un ensemble de données qui remplit le magasin lors de l’initialisation.

Étend CQ_Analytics.SessionStore.

### Propriétés {#properties-1}

#### STOREKEY {#storekey}

Clé qui identifie le magasin. Utilisez la méthode `getInstance` pour récupérer cette valeur.

#### STORENAME {#storename}

Nom du magasin. Utilisez la méthode `getInstance` pour récupérer cette valeur.

### Méthodes {#methods-3}

Voir également CQ_Analytics.SessionStore pour connaître les méthodes héritées.

#### effacer() {#clear}

Supprime les données du magasin de sessions et supprime toutes les propriétés d’initialisation.

**Paramètres**

Aucun.

**Renvoie**

Aucune valeur renvoyée.

#### getInstance(storeName, jsonData) {#getinstance-storename-jsondata}

Crée un objet CQ_Analytics.JSONStore avec un nom donné et initialisé avec les données JSON spécifiées (appelle la méthode initJSON).

**Paramètres**

* storeName : chaîne. Nom à utiliser comme propriété STORENAME. La valeur de la propriété STOREKEY est définie sur storeName avec tous les caractères en majuscules.
* jsonData : objet. Objet contenant des données JSON.

**Renvoie**

Objet CQ_Analytics.JSONStore.

#### getJSON() {#getjson}

Récupère les données du magasin de sessions au format JSON.

**Paramètres**

Aucun.

**Renvoie**

Objet représentant les données du magasin au format JSON.

#### init() {#init}

Efface le magasin de sessions et l’initialise avec la propriété d’initialisation. Définit l’indicateur d’initialisation sur `true`, puis déclenche les événements `initialize` et `update`.

**Paramètres**

Aucun.

**Renvoie**

Aucune donnée renvoyée.

#### initJSON(jsonData, doNotClear) {#initjson-jsondata-donotclear}

Crée des propriétés d’initialisation à partir des données d’un objet JSON. Vous pouvez éventuellement supprimer toutes les propriétés d’initialisation existantes.

Les noms des propriétés sont dérivés de la hiérarchie des données dans l’objet JSON. L’exemple de code suivant représente un objet JSON :

```xml
{
A: "valueA",
B: {
     B1: "valueBB1"
    }
}
```

Pour cet exemple, les propriétés suivantes sont créées dans le magasin :

```xml
A: "valueA"
B/B1: "valueBB1"
```

**Paramètres**

* jsonData : objet JSON contenant les données à stocker.
* doNotClear : une valeur « true » préserve les propriétés d’initialisation existantes et ajoute celles dérivées de l’objet JSON. Une valeur « false » supprime les propriétés d’initialisation existantes avant d’ajouter celles dérivées de l’objet JSON.

**Renvoie**

Aucune valeur renvoyée.

#### registerNewInstance(storeName, jsonData) {#registernewinstance-storename-jsondata}

Crée un objet CQ_Analytics.JSONStore avec un nom donné et initialisé avec les données JSON spécifiées (appelle la méthode initJSON). Le nouvel objet est automatiquement enregistré auprès de Clickstream Cloud Manager.

**Paramètres**

* storeName : chaîne. Nom à utiliser comme propriété STORENAME. La valeur de la propriété STOREKEY est définie sur storeName avec tous les caractères en majuscules.
* jsonData : objet. Objet contenant des données JSON.

**Renvoie**

Objet CQ_Analytics.JSONStore.

## CQ_Analytics.Observable {#cq-analytics-observable}

Déclenche des événements et permet à d’autres objets d’écouter ces événements et de réagir. Les classes qui étendent cette classe peuvent déclencher des événements qui provoquent l’appel d’écouteurs.

### Méthodes {#methods-4}

#### addListener(event, fct, scope) {#addlistener-event-fct-scope}

Enregistre un écouteur pour un événement. Voir aussi [Création d’un écouteur pour réagir à une mise à jour de magasin de sessions](/help/sites-developing/client-context.md#creating-a-listener-to-react-to-a-session-store-update).

**Paramètres**

* event : chaîne. Nom de l’événement à écouter.
* fct : fonction. Fonction appelée lorsque l’événement se produit.
* scope : objet (facultatif). Champ d’application selon lequel exécuter la fonction de gestionnaire. Le contexte &quot;this&quot; de la fonction de gestionnaire.

**Renvoie**

Aucune valeur renvoyée.

#### removeListener(event, fct) {#removelistener-event-fct}

Supprime le gestionnaire d’événements donné pour un événement.

**Paramètres**

* event : chaîne. Nom de l’événement.
* fct : fonction. Gestionnaire d’événements.

**Renvoie**

Aucune valeur renvoyée.

## CQ_Analytics.PersistedJSONPStore {#cq-analyics-persistedjsonpstore}

Conteneur persistant d’un objet JSON récupéré à partir d’un service JSONP distant.

Étend CQ_Analytics.PersistedJSONStore.

### Méthodes {#methods-5}

Voir également CQ_Analytics.PersistedJSONStore pour connaître les méthodes héritées.

#### getInstance(storeName, serviceURL, dynamicData, deferLoading, loadingCallback) {#getinstance-storename-serviceurl-dynamicdata-deferloading-loadingcallback-1}

Crée un objet CQ_Analytics.PersistedJSONPStore.

**Paramètres**

* storeName : chaîne. Nom à utiliser comme propriété STORENAME. La valeur de la propriété STOREKEY est définie sur storeName avec tous les caractères en majuscules. Si aucune propriété storeName n’est fournie, la méthode renvoie null.
* serviceURL : chaîne. URL du service JSONP
* dynamicData : objet (facultatif). Données JSON à ajouter aux données d’initialisation du magasin avant l’appel de la fonction de rappel.
* deferLoading : booléen (facultatif). Une valeur true empêche le service JSONP d’être appelé lors de la création d’objet. Une valeur false entraîne l’appel du service JSONP.
* loadingCallback : chaîne (facultatif). Nom de la fonction à appeler pour le traitement de l’objet JSONP renvoyé par le service JSONP. La fonction de rappel doit définir un seul paramètre qui est un objet CQ_Analytics.JSONPStore.

**Renvoie**

Nouvel objet CQ_Analytics.PersistedJSONPStore, ou valeur null si storeName est null.

#### getServiceURL() {#getserviceurl-1}

Récupère l’URL du service JSONP que cet objet utilise pour récupérer les données JSON.

**Paramètres**

Aucun.

**Renvoie**

Chaîne représentant l’URL du service ou valeur nulle si aucune URL de service n’a été configurée.

#### load(serviceURL, dynamicData, callback) {#load-serviceurl-dynamicdata-callback-1}

Appelle le service JSONP. L’URL JSONP est l’URL du service avec comme suffixe le nom d’une fonction de rappel.

**Paramètres**

* serviceURL : chaîne (facultatif). Service JSONP à appeler. Une valeur null entraîne l’utilisation de l’URL de service déjà configurée. Une valeur non nulle définit le service JSONP à utiliser pour cet objet. (Voir setServiceURL.)
* dynamicData : objet (facultatif). Données JSON à ajouter aux données d’initialisation du magasin avant l’appel de la fonction de rappel.
* callback : chaîne (facultatif). Nom de la fonction à appeler pour le traitement de l’objet JSONP renvoyé par le service JSONP. La fonction de rappel doit définir un seul paramètre qui est un objet CQ_Analytics.JSONPStore.

**Renvoie**

Aucune valeur renvoyée.

#### registerNewInstance(storeName, serviceURL, dynamicData, callback) {#registernewinstance-storename-serviceurl-dynamicdata-callback-1}

Crée un objet CQ_Analytics.PersistedJSONPStore et enregistre le magasin avec ClientContext.

**Paramètres**

* storeName : chaîne. Nom à utiliser comme propriété STORENAME. La valeur de la propriété STOREKEY est définie sur storeName avec tous les caractères en majuscules. Si aucune propriété storeName n’est fournie, la méthode renvoie null.
* serviceURL : chaîne (facultatif). URL du service JSONP.
* dynamicData : objet (facultatif). Données JSON à ajouter aux données d’initialisation du magasin avant l’appel de la fonction de rappel.
* callback : chaîne (facultatif). Nom de la fonction à appeler pour le traitement de l’objet JSONP renvoyé par le service JSONP. La fonction de rappel doit définir un seul paramètre qui est un objet CQ_Analytics.JSONPStore.

**Renvoie**

Objet CQ_Analytics.PersistedJSONPStore enregistré.

#### setServiceURL(serviceURL) {#setserviceurl-serviceurl-1}

Définit l’URL du service JSONP à utiliser pour récupérer les données JSON.

**Paramètres**

* serviceURL : chaîne. URL du service JSONP qui fournit des données JSON.

**Renvoie**

Aucune valeur renvoyée.

## CQ_Analytics.PersistedJSONStore {#cq-analytics-persistedjsonstore}

Conteneur persistant d’un objet JSON.

Il étend `CQ_Analytics.PersistedSessionStore`.

### Propriétés {#properties-2}

#### STOREKEY {#storekey-1}

Clé qui identifie le magasin. Utilisez la méthode `getInstance` pour récupérer cette valeur.

#### STORENAME {#storename-1}

Nom du magasin. Utilisez la méthode `getInstance` pour récupérer cette valeur.

### Méthodes {#methods-6}

Voir également CQ_Analytics.PersistedSessionStore pour connaître les méthodes héritées.

#### getInstance(storeName, jsonData) {#getinstance-storename-jsondata-1}

Crée un objet CQ_Analytics.PersistedJSONStore avec un nom donné et initialisé avec les données JSON spécifiées (appelle la méthode initJSON).

**Paramètres**

* storeName : chaîne. Nom à utiliser comme propriété STORENAME. La valeur de la propriété STOREKEY est définie sur storeName avec tous les caractères en majuscules.
* jsonData : objet. Objet contenant des données JSON.

**Renvoie**

Objet CQ_Analytics.PersistedJSONStore.

#### getJSON() {#getjson-1}

Récupère les données du magasin de sessions au format JSON.

**Paramètres**

Aucun.

**Renvoie**

Objet représentant les données du magasin au format JSON.

#### initJSON(jsonData, doNotClear) {#initjson-jsondata-donotclear-1}

Crée des propriétés d’initialisation à partir des données d’un objet JSON. Vous pouvez éventuellement supprimer toutes les propriétés d’initialisation existantes.

Les noms des propriétés sont dérivés de la hiérarchie des données dans l’objet JSON. L’exemple de code suivant représente un objet JSON :

```xml
{
A: "valueA",
B: {
     B1: "valueBB1"
    }
}
```

Pour cet exemple, les propriétés suivantes sont créées dans le magasin :

```xml
A: "valueA"
B/B1: "valueBB1"
```

**Paramètres**

* jsonData : objet JSON contenant les données à stocker.
* doNotClear : une valeur « true » préserve les propriétés d’initialisation existantes et ajoute celles dérivées de l’objet JSON. Une valeur « false » supprime les propriétés d’initialisation existantes avant d’ajouter celles dérivées de l’objet JSON.

**Renvoie**

Aucune valeur renvoyée.

#### registerNewInstance(storeName, jsonData) {#registernewinstance-storename-jsondata-1}

Crée un objet CQ_Analytics.PersistedJSONStore avec un nom donné et initialisé avec les données JSON spécifiées (appelle la méthode initJSON). Le nouvel objet est automatiquement enregistré auprès de ClientContext Manager.

**Paramètres**

* storeName : chaîne. Nom à utiliser comme propriété STORENAME. La valeur de la propriété STOREKEY est définie sur storeName avec tous les caractères en majuscules.
* jsonData : objet. Objet contenant des données JSON.

**Renvoie**

Objet CQ_Analytics.PersistedJSONStore.

## CQ_Analytics.PersistedSessionStore {#cq-analytics-persistedsessionstore}

Conteneur de propriétés et de valeurs. Les données sont conservées à l’aide de CQ_Analytics.SessionPersistence. Créez une instance de cette classe pour créer un magasin de sessions persistant :

`mypersistedstore = new CQ_Analytics.PersistedSessionStore`

Étend CQ_Analytics.SessionStore.

### Propriétés {#properties-3}

#### STOREKEY {#storekey-2}

La valeur par défaut est `key`.

### Méthodes {#methods-7}

Voir CQ_Analytics.SessionStore pour connaître les méthodes héritées.

Lorsque les méthodes héritées `clear`, `setProperty`, `setProperties`, `removeProperty` sont utilisées pour modifier les données du magasin, les modifications sont automatiquement conservées, à moins que les propriétés modifiées ne soient marquées comme notPersisted.

#### getStoreKey() {#getstorekey}

Récupère la propriété `STOREKEY`.

**Paramètres**

Aucun

**Renvoie**

Valeur de la propriété `STOREKEY`.

#### isPersisted(name) {#ispersisted-name}

Détermine si une propriété de données est conservée.

**Paramètres**

* name : chaîne. Nom de la propriété.

**Renvoie**

Valeur booléenne de `true` si la propriété est persistante et de `false` si la valeur n’est pas une propriété persistante.

#### persist() {#persist}

Rend persistant le magasin de session. Le mode de persistance par défaut utilise le navigateur `localStorage` en utilisant `ClientSidePersistence` comme nom (`window.localStorage.set("ClientSidePersistance", store);`).

Si localStorage n’est pas disponible ou inscriptible, le magasin est conservé en tant que propriété de la fenêtre.

Déclenche l’événement `persist` à la fin de l’opération.

**Paramètres**

Aucun

**Renvoie**

Aucune valeur renvoyée.

#### reset(deferEvent) {#reset-deferevent}

Supprime toutes les propriétés de données du magasin et conserve le magasin. En option, ne déclenche pas l’événement `udpate` à la fin de l’opération.

**Paramètres**

* deferEvent : une valeur true empêche l’activation de l’événement `update`. Une valeur `false` provoque le déclenchement de l’événement de mise à jour.

**Renvoie**

Aucune valeur renvoyée.

#### setNonPersisted(name) {#setnonpersisted-name}

Marque une propriété de données comme non persistante.

**Paramètres**

* name : chaîne. Nom de la propriété à ne pas conserver.

**Renvoie**

Aucune valeur renvoyée.

## CQ_Analytics.SessionStore {#cq-analytics-sessionstore}

CQ_Analytics.SessionStore représente un magasin de sessions. Créez une instance de cette classe pour créer un magasin de sessions :

`mystore = new CQ_Analytics.SessionStore`

Étend CQ_Analytics.Observable.

### Propriétés {#properties-4}

#### STORENAME {#storename-2}

Nom du magasin de sessions. Utilisez getName pour récupérer la valeur de cette propriété.

### Méthodes {#methods-8}

#### addInitProperty(name, value) {#addinitproperty-name-value}

Ajoute une propriété et une valeur aux données d’initialisation du magasin de sessions.

Utilisez loadInitProperties pour renseigner les données du magasin de sessions avec les valeurs d’initialisation.

**Paramètres**

* name : chaîne. Nom de la propriété à ajouter.
* value : chaîne. La valeur de la propriété à ajouter.

**Renvoie**

Aucune valeur renvoyée.

#### effacer() {#clear-1}

Supprime toutes les propriétés de données du magasin.

**Paramètres**

Aucun.

**Renvoie**

Aucune valeur renvoyée.

#### getData(excluded) {#getdata-excluded}

Renvoie les données du magasin. Facultativement, exclut les propriétés de nom des données. Appelle la méthode `init` si la propriété data du magasin n’existe pas.

**Paramètres**

excluded : (facultatif) tableau de noms de propriétés à exclure des données renvoyées.

**Renvoie**

Objet de propriétés et de leurs valeurs.

#### getInitProperty(name) {#getinitproperty-name}

Récupère la valeur d’une propriété de données.

**Paramètres**

* name : chaîne. Nom de la propriété de données à récupérer.

**Renvoie**

Valeur de la propriété de données. Renvoie `null` si le magasin de sessions ne contient aucune propriété portant le nom spécifié.

#### getName() {#getname}

Renvoie le nom du magasin de sessions.

**Paramètres**

Aucun.

**Renvoie**

Une valeur String qui représente le nom du magasin.

#### getProperty(name, raw) {#getproperty-name-raw}

Renvoie la valeur d’une propriété. La valeur est renvoyée en tant que propriété brute ou valeur filtrée XSS. Appelle la méthode `init` si la propriété data du magasin n’existe pas.

**Paramètres**

* name : chaîne. Nom de la propriété de données à récupérer.
* raw : booléen. Une valeur true renvoie la valeur de la propriété brute à renvoyer. Si la valeur est false, la valeur renvoyée est filtrée XSS.

**Renvoie**

Valeur de la propriété de données.

#### getPropertyNames(excluded) {#getpropertynames-excluded}

Renvoie les noms des propriétés que contient le magasin de sessions. Appelle la méthode `init` si la propriété data du magasin n’existe pas.

**Paramètres**

excluded : (facultatif) tableau de noms de propriétés à omettre des résultats.

**Renvoie**

Tableau de valeurs String représentant les noms des propriétés de session.

#### getSessionStore() {#getsessionstore}

Renvoie le magasin de sessions associé à l’objet actif.

**Paramètres**

Aucun.

**Renvoie**

this

#### init() {#init-1}

Marque le magasin comme initialisé et déclenche l’événement `initialize`.

**Paramètres**

Aucun.

**Renvoie**

Aucune valeur renvoyée.

#### isInitialized() {#isinitialized}

Indique si le magasin de sessions est initialisé.

**Paramètres**

Aucun.

**Renvoie**

Valeur `true` si le magasin est initialisé et `false` s’il ne l’est pas.

#### loadInitProperties(obj, setValues) {#loadinitproperties-obj-setvalues}

Ajoute les propriétés de l’objet en question aux données d’initialisation du magasin de sessions. En option, les données d’objet sont également ajoutées aux données du magasin.

**Paramètres**

* obj : objet qui contient des propriétés énumérables.
* setValues : si cette propriété est définie sur true, les propriétés obj sont ajoutées aux données du magasin de sessions à condition que les données du magasin n’incluent pas déjà une propriété du même nom. Lorsque la valeur est false, aucune donnée n’est ajoutée aux données du magasin de sessions.

**Renvoie**

Aucune valeur renvoyée.

#### removeProperty(name) {#removeproperty-name}

Supprime une propriété du magasin de sessions. Déclenche l’événement `update` à la fin de l’opération. Appelle la méthode `init` si la propriété data du magasin n’existe pas.

**Paramètres**

* name : chaîne. Nom de la propriété à supprimer.

**Renvoie**

Aucune valeur renvoyée.

#### reset() {#reset}

Restaure les valeurs initiales du magasin de données. L’implémentation par défaut supprime simplement toutes les données. Déclenche l’événement `update` à la fin de l’opération.

**Paramètres**

Aucun.

**Renvoie**

Aucune valeur renvoyée.

#### setProperties(properties) {#setproperties-properties}

Définit les valeurs de plusieurs propriétés. Déclenche l’événement `update` à la fin de l’opération. Appelle la méthode `init` si la propriété data du magasin n’existe pas.

**Paramètres**

* Properties : objet. Objet qui contient des propriétés énumérables. Chaque nom et valeur de propriété est ajouté au magasin.

**Renvoie**

Aucune valeur renvoyée.

#### setProperty(name, value) {#setproperty-name-value}

Définit les valeurs d’une propriété. Déclenche l’événement `update` à la fin de l’opération. Appelle la méthode `init` si la propriété data du magasin n’existe pas.

**Paramètres**

* name : chaîne. Nom de la propriété.
* value : chaîne. Valeur de propriété.

**Renvoie**

Aucune valeur renvoyée.
