---
title: Requêtes GraphQL persistantes
description: Découvrez comment conserver les requêtes GraphQL dans Adobe Experience Manager pour optimiser les performances. Les requêtes persistantes peuvent être demandées par les applications clientes à l’aide de la méthode GET HTTP et la réponse peut être mise en cache aux couches Dispatcher et CDN, ce qui améliore finalement les performances des applications clientes.
source-git-commit: 9369f7cb9c507bbd7d7761440ceef907552aeb7d
workflow-type: tm+mt
source-wordcount: '1088'
ht-degree: 100%

---

# Requêtes GraphQL persistantes {#persisted-queries-caching}

Les requêtes persistantes sont des requêtes GraphQL qui sont créées et stockées sur le serveur Adobe Experience Manager (AEM) as a Cloud Service. Elles peuvent être demandées avec une requête GET par les applications clientes. La réponse d’une requête GET peut être mise en cache aux couches Dispatcher et CDN, ce qui améliore finalement les performances de l’application cliente qui la demande. Elles sont en cela différentes des requêtes GraphQL standard, qui sont exécutées à l’aide de requêtes POST dans lesquelles la réponse ne peut pas être facilement mise en cache.

<!--
>[!NOTE]
>
>Persisted Queries are recommended. See [GraphQL Query Best Practices (Dispatcher)](/help/headless/graphql-api/content-fragments.md#graphql-query-best-practices) for details, and the related Dispatcher configuration.
-->

L’[IDE GraphiQL](/help/assets/content-fragments/graphiql-ide.md) est disponible dans AEM pour que vous puissiez le développer, le tester et conserver vos requêtes GraphQL, avant de [le transférer vers votre environnement de production](#transfer-persisted-query-production). Dans les cas qui nécessitent une personnalisation (par exemple, pour la [personnalisation du cache](/help/assets/content-fragments/graphiql-ide.md#caching-persisted-queries)) vous pouvez utiliser l’API ; consultez l’exemple de curl fourni dans [Conservation d’une requête GraphQL](#how-to-persist-query).

## Requêtes et points d’entrée persistants {#persisted-queries-and-endpoints}

Les requêtes persistantes doivent toujours utiliser le point d’entrée associé à la [configuration Sites appropriée](/help/assets/content-fragments/graphql-api-content-fragments.md#graphql-aem-endpoint) afin qu’ils puissent utiliser l’une des fonctionnalités ou les deux :

* Configuration globale et point d’entrée
La requête a accès à tous les modèles de fragment de contenu.
* Configuration(s) de sites spécifiques et point(s) d’entrée
La création d’une requête persistante pour une configuration Sites spécifique nécessite un point d’entrée spécifique à la configuration Sites correspondant (pour fournir l’accès aux modèles de fragment de contenu associés).
Par exemple, pour créer une requête persistante spécifique à la configuration WKND Sites, une configuration de sites spécifique à WKND correspondante et un point d’entrée spécifique à WKND doivent être créés à l’avance.

>[!NOTE]
>
>Voir [Activation de la fonctionnalité de fragment de contenu dans le navigateur de configuration](/help/assets/content-fragments/content-fragments-configuration-browser.md#enable-content-fragment-functionality-in-configuration-browser) pour plus d’informations.
>
>Les **requêtes persistantes GraphQL** doivent être activées pour la configuration appropriée des sites.

Par exemple, s’il existe une requête spécifique appelée `my-query`, qui utilise un modèle `my-model` de la configuration Sites `my-conf` :

* Vous pouvez créer une requête à l’aide du point d’entrée `my-conf` spécifique, puis la requête sera enregistrée comme suit :
   `/conf/my-conf/settings/graphql/persistentQueries/my-query`
* Vous pouvez créer la même requête à l’aide du point d’entrée `global`, mais elle sera dans ce cas enregistrée comme suit :
   `/conf/global/settings/graphql/persistentQueries/my-query`

>[!NOTE]
>
>Il s’agit de deux requêtes différentes, enregistrées sous des chemins différents.
>
>Il se trouve qu’elles utilisent le même modèle – mais via différents points d’entrée.

## Conservation d’une requête GraphQL {#how-to-persist-query}

Il est recommandé d’appliquer des requêtes persistantes dans un environnement de création d’AEM dès le départ, puis de [transférer la requête](#transfer-persisted-query-production) à votre environnement de publication AEM de production, pour être utilisées par les applications.

Il existe différentes méthodes pour créer des requêtes persistantes, notamment :

* IDE GraphiQL - voir [Enregistrement des requêtes persistantes](/help/assets/content-fragments/graphiql-ide.md#saving-persisted-queries) (méthode préférée)
* curl - Consultez l’exemple suivant
* Autres outils, notamment [Postman](https://www.postman.com/)

L’IDE GraphiQL est la méthode **préférée** pour les requêtes persistantes. Pour conserver une requête donnée à l’aide de l’outil de ligne de commande **curl** :

1. Préparez la requête avec une commande PUT sur l’URL du nouveau point d’entrée `/graphql/persist.json/<config>/<persisted-label>`.

   Par exemple, créez une requête persistante :

   ```shell
   $ curl -X PUT \
       -H 'authorization: Basic YWRtaW46YWRtaW4=' \
       -H "Content-Type: application/json" \
       "http://localhost:4502/graphql/persist.json/wknd/plain-article-query" \
       -d \
   '{
     articleList {
       items{
           _path
           author
           main {
               json
           }
       }
     }
   }'
   ```

1. À ce stade, vérifiez la réponse.

   Par exemple, contrôlez le succès :

   ```json
   {
     "action": "create",
     "configurationName": "wknd",
     "name": "plain-article-query",
     "shortPath": "/wknd/plain-article-query",
     "path": "/conf/wknd/settings/graphql/persistentQueries/plain-article-query"
   }
   ```

1. Vous pouvez ensuite exécuter à nouveau la requête persistante avec une commande GET sur l’URL `/graphql/execute.json/<shortPath>`.

   Par exemple, utilisez la requête persistante :

   ```shell
   $ curl -X GET \
       http://localhost:4502/graphql/execute.json/wknd/plain-article-query
   ```

1. Mettez à jour une requête persistante avec une commande POST vers un chemin de requête existant.

   Par exemple, utilisez la requête persistante :

   ```shell
   $ curl -X POST \
       -H 'authorization: Basic YWRtaW46YWRtaW4=' \
       -H "Content-Type: application/json" \
       "http://localhost:4502/graphql/persist.json/wknd/plain-article-query" \
       -d \
   '{
     articleList {
       items{
           _path
           author
           main {
               json
           }
         referencearticle {
           _path
         }
       }
     }
   }'
   ```

1. Créez une requête ordinaire encapsulée.

   Par exemple :

   ```shell
   $ curl -X PUT \
       -H 'authorization: Basic YWRtaW46YWRtaW4=' \
       -H "Content-Type: application/json" \
       "http://localhost:4502/graphql/persist.json/wknd/plain-article-query-wrapped" \
       -d \
   '{ "query": "{articleList { items { _path author main { json } referencearticle { _path } } } }"}'
   ```

1. Créez une requête ordinaire encapsulée avec le contrôle de cache.

   Par exemple :

   ```shell
   $ curl -X PUT \
       -H 'authorization: Basic YWRtaW46YWRtaW4=' \
       -H "Content-Type: application/json" \
       "http://localhost:4502/graphql/persist.json/wknd/plain-article-query-max-age" \
       -d \
   '{ "query": "{articleList { items { _path author main { json } referencearticle { _path } } } }", "cache-control": { "max-age": 300 }}'
   ```

1. Créez une requête persistante avec des paramètres :

   Par exemple :

   ```shell
   $ curl -X PUT \
       -H 'authorization: Basic YWRtaW46YWRtaW4=' \
       -H "Content-Type: application/json" \
       "http://localhost:4502/graphql/persist.json/wknd/plain-article-query-parameters" \
       -d \
   'query GetAsGraphqlModelTestByPath($apath: String!, $withReference: Boolean = true) {
     articleByPath(_path: $apath) {
       item {
         _path
           author
           main {
           plaintext
           }
           referencearticle @include(if: $withReference) {
           _path
           }
         }
       }
     }'
   ```


## Procédure d’exécution d’une requête persistante {#execute-persisted-query}

Pour exécuter une requête persistante, une application cliente effectue une requête GET en utilisant la syntaxe suivante :

```
GET <AEM_HOST>/graphql/execute.json/<PERSISTENT_PATH>
```

Où `PERSISTENT_PATH` est un chemin raccourci vers l’emplacement d’enregistrement de la requête persistante.

1. Par exemple `wknd` est le nom de la configuration et `plain-article-query` est le nom de la requête persistante. Pour exécuter la requête :

   ```shell
   $ curl -X GET \
       https://localhost:4502/graphql/execute.json/wknd/plain-article-query
   ```

1. Exécuter une requête avec des paramètres.

   >[!NOTE]
   >
   > Les variables et valeurs de requête doivent être correctement [encodées](#encoding-query-url) lors de l’exécution d’une requête persistante.

   Par exemple :

   ```xml
   $ curl -X GET \
       "https://localhost:4502/graphql/execute.json/wknd/plain-article-query-parameters%3Bapath%3D%2Fcontent%2Fdam%2Fwknd%2Fen%2Fmagazine%2Falaska-adventure%2Falaskan-adventures%3BwithReference%3Dfalse
   ```

   Voir la section Utiliser [les variables de requête](#query-variables) pour plus d’informations.

## Utiliser les variables de requête {#query-variables}

Les variables de requête peuvent être utilisées avec les requêtes persistantes. Les variables de requête sont ajoutées à la requête précédée d’un point-virgule (`;`) à l’aide du nom et de la valeur de la variable. Plusieurs variables sont séparées par des points-virgules.

Le modèle ressemble à ce qui suit :

```
<AEM_HOST>/graphql/execute.json/<PERSISTENT_QUERY_PATH>;variable1=value1;variable2=value2
```

Par exemple, la requête suivante contient une variable `activity` pour filtrer une liste en fonction d’une valeur d’activité.

```graphql
query getAdventuresByActivity($activity: String!) {
      adventureList (filter: {
        adventureActivity: {
          _expressions: [
            {
              value: $activity
            }
          ]
        }
      }){
        items {
          _path
        adventureTitle
        adventurePrice
        adventureTripLength
      }
    }
  }
```

Cette requête peut être conservée sous un chemin `wknd/adventures-by-activity`. Pour appeler la requête persistante où `activity=Camping` la requête ressemblerait à ceci :

```
<AEM_HOST>/graphql/execute.json/wknd/adventures-by-activity%3Bactivity%3DCamping
```

Notez que `%3B` est l’encodage UTF-8 pour `;` et `%3D` est l’encodage pour `=`. Les variables de requête et les caractères spéciaux doivent être [correctement encodés](#encoding-query-url) pour que la requête persistante s’exécute.

<!--
## Caching your persisted queries {#caching-persisted-queries}

Persisted queries are recommended as they can be cached at the dispatcher and CDN layers, ultimately improving the performance of the requesting client application.

By default AEM will invalidate the Content Delivery Network (CDN) cache based on a default Time To Live (TTL). 

This value is set to:

* 7200 seconds is the default TTL for the Dispatcher and CDN; also known as *shared caches*
  * default: s-maxage=7200
* 60 is the default TTL for the client (for example, a browser)
  * default: maxage=60

If you want to change the TTL for your GraphLQ query, then the query must be either:

* persisted after managing the [HTTP Cache headers - from the GraphQL IDE](#http-cache-headers)
* persisted using the [API method](#cache-api). 

### Managing HTTP Cache Headers in GraphQL  {#http-cache-headers-graphql}

The GraphiQL IDE - see [Saving Persisted Queries](/help/assets/content-fragments/graphiql-ide.md#managing-cache)

### Managing Cache from the API {#cache-api}

This involves posting the query to AEM using CURL in your command line interface. 

For an example:

```xml
curl -X PUT \
    -H 'authorization: Basic YWRtaW46YWRtaW4=' \
    -H "Content-Type: application/json" \
    "https://localhost:4502/graphql/persist.json/wknd/plain-article-query-max-age" \
    -d \
'{ "query": "{articleList { items { _path author main { json } referencearticle { _path } } } }", "cache-control": { "max-age": 300 }}'
```

The `cache-control` can be set at the creation time (PUT) or later on (for example, via a POST request for instance). The cache-control is optional when creating the persisted query, as AEM can provide the default value. See [How to persist a GraphQL query](#how-to-persist-query), for an example of persisting a query using curl.
-->

## Encoder l’URL de requête devant être utilisé par une application {#encoding-query-url}

Pour une utilisation par une application, tout caractère spécial utilisé lors de la création de variables de requête (c’est-à-dire des points-virgules (`;`), le signe égal (`=`), des barres obliques `/`) doit être converti pour utiliser le codage UTF-8 correspondant.

Par exemple :

```xml
curl -X GET \ "https://localhost:4502/graphql/execute.json/wknd/adventure-by-path%3BadventurePath%3D%2Fcontent%2Fdam%2Fwknd%2Fen%2Fadventures%2Fbali-surf-camp%2Fbali-surf-camp"
```

L’URL peut être divisée en plusieurs parties :

| Partie de l’URL | Description |
|----------| -------------|
| `/graphql/execute.json` | Point d’entrée de requête persistante |
| `/wknd/adventure-by-path` | Chemin de requête persistante |
| `%3B` | Encodage de `;` |
| `adventurePath` | Variable de requête |
| `%3D` | Encodage de `=` |
| `%2F` | Encodage de `/` |
| `%2Fcontent%2Fdam...` | Chemin codé vers le fragment de contenu |

En texte brut, l’URI de requête ressemble à ce qui suit :

```plaintext
/graphql/execute.json/wknd/adventure-by-path;adventurePath=/content/dam/wknd/en/adventures/bali-surf-camp/bali-surf-camp
```

Pour utiliser une requête persistante dans une application cliente, le SDK client AEM Headless doit être utilisé pour [JavaScript](https://github.com/adobe/aem-headless-client-js), [Java](https://github.com/adobe/aem-headless-client-java) ou [NodeJS](https://github.com/adobe/aem-headless-client-nodejs). Le SDK client Headless codera automatiquement toutes les variables de requête correctement dans la requête concernée.

## Transférer une requête persistante vers votre environnement de production  {#transfer-persisted-query-production}

Les requêtes persistantes doivent toujours être créées sur un service de création AEM, puis publiées (répliquées) sur un service de publication AEM. Souvent, les requêtes persistantes sont créées et testées dans des environnements inférieurs tels que les environnements locaux ou de développement. Il est alors nécessaire de promouvoir les requêtes persistantes dans des environnements de niveau supérieur, ce qui rend ces requêtes disponibles dans un environnement de publication AEM de production pour que les applications clientes puissent les utiliser.

### Requêtes persistantes de package

Les requêtes persistantes peuvent être intégrées aux [packages AEM](/help/sites-administering/package-manager.md). Les packages AEM peuvent ensuite être téléchargés et installés dans différents environnements. Les packages AEM peuvent également être répliqués d’un environnement de création AEM vers des environnements de publication AEM.

Création d’un package :

1. Accédez à **Outils** > **Déploiement** > **Packages**.
1. Créez un nouveau package en appuyant sur **Créer un package**. Une boîte de dialogue s’ouvre alors pour définir le package.
1. Dans la boîte de dialogue Définition de package, sous **Général**, saisissez un **Nom** comme « wknd-persistent-queries ».
1. Saisissez un numéro de version comme « 1.0 ».
1. Sous **Filtres** ajoutez un nouveau **Filtre**. Utilisez l’outil de recherche de chemin pour sélectionner le dossier `persistentQueries` sous la configuration. Par exemple, pour la configuration `wknd` le chemin d&#39;accès complet sera `/conf/wknd/settings/graphql/persistentQueries`.
1. Appuyez sur **Enregistrer** pour enregistrer la nouvelle définition de package et fermez la boîte de dialogue.
1. Appuyez sur le bouton **Créer** dans la définition de package nouvellement créée.

Une fois le package créé, vous pouvez :

* **Télécharger** le package et effectuer un nouveau chargement sur un autre environnement.
* **Répliquer** le package en appuyant sur **Plus** > **Répliquer**. Cela répliquera le package dans l’environnement de publication AEM connecté.

<!--
1. Using replication/distribution tool:
   1. Go to the Distribution tool.
   1. Select tree activation for the configuration (for example, `/conf/wknd/settings/graphql/persistentQueries`).

* Using a workflow (via workflow launcher configuration):
  1. Define a workflow launcher rule for executing a workflow model that would replicate the configuration on different events (for example, create, modify, amongst others).
-->
