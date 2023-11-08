---
title: Accès à votre contenu grâce aux API de diffusion AEM
description: Dans cette partie du parcours de développement découplé AEM, découvrez comment utiliser les requêtes GraphQL pour accéder au contenu de vos fragments de contenu.
exl-id: 44f85d00-a958-470a-8a6e-e2ae1580525a
source-git-commit: 38f0496d9340fbcf383a2d39dba8efcbdcd20c6f
workflow-type: tm+mt
source-wordcount: '1332'
ht-degree: 95%

---

# Accès à votre contenu grâce aux API de diffusion AEM {#access-your-content}

Dans cette partie du [Parcours de développement découplé AEM](overview.md), vous pouvez apprendre à utiliser les requêtes GraphQL pour accéder au contenu de vos fragments de contenu et le transmettre à votre application (diffusion découplée).

## Un peu d’histoire...  {#story-so-far}

Dans le document précédent du parcours découplé AEM, [Comment modéliser votre contenu](model-your-content.md), vous avez appris les principes de base de la modélisation de contenu dans AEM. Vous devez donc maintenant comprendre comment modéliser votre structure de contenu, puis réaliser cette structure à l’aide des modèles de fragment de contenu et des fragments de contenu AEM :

* Reconnaître les concepts et la terminologie liés à la modélisation de contenu
* Comprendre pourquoi la modélisation de contenu est nécessaire pour la diffusion de contenu découplé
* Comprendre comment réaliser cette structure à l’aide des modèles de fragment de contenu AEM (et comment créer du contenu avec des fragments de contenu)
* Comprendre comment modéliser votre contenu, les principes comme les exemples de base

Cet article s’appuie sur ces principes de base afin que vous compreniez comment accéder à votre contenu découplé existant dans AEM en utilisant l’API AEM GraphQL.

* **Public** : débutant
* **Objectif** : apprendre comment accéder au contenu de vos fragments de contenu à l’aide des requêtes GraphQL d’AEM :
   * Présentation de GraphQL et de l’API AEM GraphQL.
   * Découvrir les détails de l’API AEM GraphQL.
   * Regardez quelques exemples de requêtes pour voir comment les choses fonctionnent dans la pratique.

## Vous souhaitez accéder à votre contenu ?  {#so-youd-like-to-access-your-content}

Enfin... Vous disposez de tout ce contenu, soigneusement structuré (dans les fragments de contenu) et vous avez hâte d’en nourrir votre nouvelle application. La question est : comment faire ?

Vous avez besoin d’un moyen de cibler un contenu spécifique, de sélectionner ce dont vous avez besoin et de le renvoyer à votre application pour un traitement ultérieur.

Avec Adobe Experience Manager (AEM), vous pouvez accéder de manière sélective à vos fragments de contenu, à l’aide de l’API AEM GraphQL, pour renvoyer uniquement le contenu dont vous avez besoin. Cela signifie que vous pouvez réaliser une diffusion découplée d’un contenu structuré pour l’utiliser dans vos applications.

>[!NOTE]
>
>L’API AEM GraphQL est une mise en œuvre personnalisée, basée sur la spécification de l’API GraphQL standard.

## GraphQL – Introduction {#graphql-introduction}

GraphQL est une spécification open source qui fournit les éléments suivants :

* un langage de requête qui permet de sélectionner du contenu spécifique à partir d’objets structurés
* une exécution permettant de répondre à ces requêtes avec votre contenu structuré

GraphQL est une API *fortement* typée. Cela signifie que *tout* le contenu doit être clairement structuré et organisé par type, de sorte que GraphQL *comprenne* ce à quoi accéder et comment. Les champs de données sont définis dans les schémas GraphQL qui définissent ainsi la structure de vos objets de contenu.

Les points d’entrée GraphQL fournissent ensuite les chemins qui répondent aux requêtes GraphQL.

Cela signifie que votre application peut sélectionner précisément, de manière fiable et efficace le contenu dont elle a besoin, ce qui est exactement ce dont vous avez besoin lorsqu’elle est utilisée avec AEM.

>[!NOTE]
>
>Consultez *GraphQL*.org et *GraphQL*.com.

<!--
## AEM and GraphQL {#aem-graphql}

GraphQL is used in various locations in AEM; for example:

* Content Fragments
  * A customized API has been developed for this use-case (Headless Delivery to your app).
    * This is the AEM GraphQL API.
* Commerce
  * AEM Commerce consumes data from a Commerce platform via GraphQL.
  * There are GraphQL integrations between AEM and various third-party commerce solutions, used with the extension hooks provided by the CIF Core Components.
    * This does not use the AEM GraphQL API.

>[!NOTE]
>
>This step of the Headless Journey is only concerned with the AEM GraphQL API and Content Fragments.
-->

## API AEM GraphQL {#aem-graphql-api}

L’API GraphQL d’AEM est une version personnalisée basée sur la spécification de l’API GraphQL standard, spécialement configurée pour vous permettre d’exécuter des requêtes (complexes) sur vos fragments de contenu.

Les fragments de contenu sont utilisés, car le contenu est structuré selon des modèles de ce type de fragment. Elle répond ainsi à une des exigences de base de GraphQL.

* Un modèle de fragment de contenu est constitué d’un ou de plusieurs champs.
   * Chaque champ est défini sur un type de données.
* Les modèles de fragment de contenu sont utilisés pour générer les schémas GraphQL AEM correspondants.

Pour vraiment accéder à GraphQL pour AEM (et à son contenu), un point d’entrée est utilisé pour fournir le chemin d’accès.

Le contenu renvoyé, à l’aide de l’API AEM GraphQL, peut ensuite être utilisé par vos applications.

Pour vous aider à saisir et à tester directement des requêtes, une implémentation de l’interface GraphQL standard est également disponible avec GraphQL AEM (qui peut être installée avec AEM). Elle vous offre des fonctionnalités telles que la mise en surbrillance de la syntaxe, la saisie semi-automatique et la suggestion automatique, ainsi qu’un historique et une documentation en ligne.

>[!NOTE]
>
>L’implémentation de l’API AEM GraphQL repose sur les bibliothèques Java GraphQL.

<!--
### Use Cases for Author and Publish Environments {#use-cases-author-publish-environments}

The use cases for the AEM GraphQL API can depend on the type of AEMenvironment:

* Publish environment; used to: 
  * Query content for JS application (standard use-case)

* Author environment; used to: 
  * Query content for "content management purposes":
    * GraphQL in AEM is currently a read-only API.
    * The REST API can be used for CR(u)D operations.
-->

## Fragments de contenu à utiliser avec l’API AEM GraphQL {#content-fragments-use-with-aem-graphql-api}

Les fragments de contenu peuvent servir de base à GraphQL pour les schémas et requêtes AEM car :

* ils vous permettent de concevoir, créer, organiser et publier du contenu indépendant des pages, qui peut être diffusé en toute sécurité ;
* ils sont basés sur un modèle de fragment de contenu, qui prédéfinit la structure du fragment résultant à l’aide d’une sélection de types de données ;
* d’autres couches de structure peuvent être obtenues avec le type de données Référence de fragment, disponible lors de la définition d’un modèle.

### Modèles de fragment de contenu {#content-fragments-models}

Ces modèles de fragment de contenu :

* Sont utilisés pour générer les Schémas, une fois **Activés**.
* fournissent les types de données et les champs requis pour GraphQL ; garantissent que votre application ne demande que ce qui est possible et reçoive ce qui est attendu.
* Le type de données **Références de fragments** peut être utilisé dans votre modèle pour faire référence à un autre fragment de contenu et introduit ainsi des niveaux de structure supplémentaires.

### Références à un fragment {#fragment-references}

La **référence à un fragment** :

* est un type de données spécifique disponible lors de la définition d’un modèle de fragment de contenu ;
* fait référence à un autre fragment, en fonction d’un modèle de fragment de contenu spécifique ;
* Permet de créer, puis de récupérer, des données structurées.

   * Lorsqu’elle est définie comme **référence à sources multiples**, plusieurs sous-fragments peuvent être référencés (récupérés) par le fragment principal.

### Prévisualisation JSON {#json-preview}

Pour faciliter la conception et le développement de vos modèles de fragments de contenu, vous pouvez prévisualiser la sortie JSON dans l’éditeur de fragments de contenu.

![Aperçu JSON](assets/cfm-model-json-preview.png "Aperçu JSON")

<!--
## GraphQL Schema Generation from Content Fragments {#graphql-schema-generation-content-fragments}

GraphQL is a strongly typed API, which means that content must be clearly structured and organized by type. The GraphQL specification provides a series of guidelines on how to create a robust API for interrogating content on a certain instance. To do this, a client needs to fetch the Schema, which contains all the types necessary for a query. 

For Content Fragments, the GraphQL schemas (structure and types) are based on **Enabled** Content Fragment Models and their data types.

>[!CAUTION]
>
>All the GraphQL schemas (derived from Content Fragment Models that have been **Enabled**) are readable through the GraphQL endpoint.
>
>This means that you need to ensure that no sensitive content is available, to ensure that no sensitive data is exposed via GraphQL endpoints; for example, this includes information that could be present as field names in the model definition.

For example, if a user created a Content Fragment Model called `Article`, then AEM generates the object `article` that is of a type `ArticleModel`. The fields within this type correspond to the fields and data types defined in the model.

1. A Content Fragment Model:

   ![Content Fragment Model for use with GraphQL](assets/graphqlapi-cfmodel.png "Content Fragment Model for use with GraphQL")

1. The corresponding GraphQL schema (output from GraphiQL automatic documentation):
   ![GraphQL Schema based on Content Fragment Model](assets/graphqlapi-cfm-schema.png "GraphQL Schema based on Content Fragment Model")

   This shows that the generated type `ArticleModel` contains several [fields](#fields). 
   
   * Three of them have been controlled by the user: `author`, `main` and `referencearticle`.

   * The other fields were added automatically by AEM, and represent helpful methods to provide information about a certain Content Fragment; in this example, `_path`, `_metadata`, `_variations`. These [helper fields](#helper-fields) are marked with a preceding `_` to distinguish between what has been defined by the user and what has been auto-generated.

1. After a user creates a Content Fragment based on the Article model, it can then be interrogated through GraphQL. For examples, see the Sample Queries.md#graphql-sample-queries) (based on a sample Content Fragment structure for use with GraphQL.

In GraphQL for AEM, the schema is flexible. This means that it is auto-generated each and every time a Content Fragment Model is created, updated or deleted. The data schema caches are also refreshed when you update a Content Fragment Model.

The Sites GraphQL service listens (in the background) for any modifications made to a Content Fragment Model. When updates are detected, only that part of the schema is regenerated. This optimization saves time and provides stability.

So for example, if you:

1. Install a package containing `Content-Fragment-Model-1` and `Content-Fragment-Model-2`:
 
   1. GraphQL types for `Model-1` and `Model-2` will be generated.

1. Then modify `Content-Fragment-Model-2`:

   1. Only the `Model-2` GraphQL type will get updated.

   1. Whereas `Model-1` will remain the same. 

>[!NOTE]
>
>This is important to note in case you want to do bulk updates on Content Fragment Models through the REST api, or otherwise.

The schema is served through the same endpoint as the GraphQL queries, with the client handling the fact that the schema is called with the extension `GQLschema`. For example, performing a simple `GET` request on `/content/cq:graphql/global/endpoint.GQLschema` will result in the output of the schema with the Content-type: `text/x-graphql-schema;charset=iso-8859-1`.

### Schema Generation - Unpublished Models {#schema-generation-unpublished-models}

When Content Fragments are nested it can happen that a parent Content Fragment Model is published, but a referenced model is not.

>[!NOTE]
>
>The AEM UI prevents this happening, but if publishing is made programmatically, or with content packages, it can occur.

When this happens, AEM generates an *incomplete* Schema for the parent Content Fragment Model. This means that the Fragment Reference, which is dependent on the unpublished model, is removed from the schema.

## AEM GraphQL Endpoints {#aem-graphql-endpoints}

An endpoint is the path used to access GraphQL for AEM. Using this path you (or your app) can:

* access the GraphQL schemas,
* send your GraphQL queries,
* receive the responses (to your GraphQL queries).

AEM allows for:

* A global endpoint - available for use by all sites.
* Endpoints for specific Sites configurations - that you can configure (in the Configuration Browser), specific to a specified site/project.

## Permissions {#permissions}

The permissions are those required for accessing Assets.

## The AEM GraphiQL Interface {#aem-graphiql-interface}

To help you directly input, and test queries, an implementation of the standard GraphiQL interface is available for use with AEM GraphQL. This can be installed with AEM.

>[!NOTE]
>
>GraphiQL is bound the global endpoint (and does not work with other endpoints for specific Sites configurations).

It provides features such as syntax-highlighting, auto-complete, auto-suggest, together with a history and online documentation.

![GraphiQL Interface](assets/graphiql-interface.png "GraphiQL Interface")
-->

## Utilisation concrète de l’API AEM GraphQL {#actually-using-aem-graphiql}

### Configuration initiale {#initial-setup}

Avant de commencer à lancer des requêtes sur votre contenu, suivez les étapes suivantes :

* Activez votre point d’entrée ;
   * Utilisez Outils > Ressources > GraphQL .
   * [Activer votre point d’entrée GraphQL](/help/sites-developing/headless/graphql-api/graphql-endpoint.md#enabling-graphql-endpoint)

* Accéder à GraphiQL (si nécessaire)
   * [Interface d’AEM GraphiQL](/help/sites-developing/headless/graphql-api/graphql-api-content-fragments.md#graphiql-interface)

### Exemple de structure {#sample-structure}

Pour utiliser l’API AEM GraphQL dans une requête, nous pouvons utiliser les deux structures de modèle de fragment de contenu très basiques :

* Société
   * Nom – Texte
   * PDG (Personne) – Référence du fragment
   * Employés (personnes) – Références du fragment
* Personne
   * Nom – Texte
   * Prénom – Texte

Comme vous pouvez le voir, les champs PDG et Employés font référence aux fragments de personne.

Les modèles de fragment sont utilisés :

* lors de la création du contenu dans l’éditeur de fragment de contenu ;
* pour générer les schémas GraphQL que vous interrogerez.

### Où tester vos requêtes {#where-to-test-your-queries}

Les requêtes peuvent être saisies dans la variable [Interface GraphiQL](/help/sites-developing/headless/graphql-api/graphiql-ide.md), par exemple, à l’adresse :

* `http://localhost:4502/aem/graphiql.html`

![Interface GraphiQL](assets/graphiql-interface.png "Interface GraphiQL")

### Prise en main des requêtes {#getting-Started-with-queries}

Une requête simple consiste à renvoyer le nom de toutes les entrées du schéma Société. Vous demandez ici une liste de tous les noms de sociétés :

```xml
query {
  companyList {
    items {
      name
    }
  }
}
```

Une requête un peu plus complexe consiste à sélectionner toutes les personnes qui n’ont pas de nom « Tâches ». Toutes les personnes qui ne portent pas le nom Tâches seront ainsi filtrées. Ce filtrage est réalisé à l’aide de l’opérateur EQUALS_NOT (il en existe bien d’autres) :

```xml
query {
  personList(filter: {
    name: {
      _expressions: [
        {
          value: "Jobs"
          _operator: EQUALS_NOT
        }
      ]
    }
  }) {
    items {
      name
      firstName
    }
  }
}
```

Vous pouvez également créer des requêtes plus complexes. Par exemple, faites une requête pour toutes les sociétés qui ont au moins un employé nommé « Smith ». Cette requête illustre le filtrage pour toute personne portant le nom « Smith », qui renvoie des informations provenant des fragments imbriqués :

```xml
query {
  companyList(filter: {
    employees: {
      _match: {
        name: {
          _expressions: [
            {
              value: "Smith"
            }
          ]
        }
      }
    }
  }) {
    items {
      name
      ceo {
        name
        firstName
      }
      employees {
        name
        firstName
      }
    }
  }
}
```

<!-- need code / curl / cli examples-->

Pour obtenir des détails complets sur l’utilisation de l’API AEM GraphQL, ainsi que la configuration des éléments nécessaires, vous pouvez vous référer aux sections suivantes :

* Apprendre à utiliser GraphQL avec AEM ;
* L’exemple de structure de fragment de contenu ;
* Apprendre à utiliser GraphQL avec AEM – Exemple de contenu et de requêtes

## Et après ? {#whats-next}

Maintenant que vous avez appris à accéder à votre contenu en mode découplé et à y effectuer des requêtes à l’aide de l’API AEM GraphQL, vous pouvez [apprendre à utiliser l’API REST pour accéder au contenu de vos fragments de contenu et le mettre à jour](update-your-content.md).

## Ressources supplémentaires {#additional-resources}

* [GraphQL.org](https://graphql.org)
   * [Schémas](https://graphql.org/learn/schema/)
   * [Variables](https://graphql.org/learn/queries/#variables)
   * [Bibliothèques Java GraphQL](https://graphql.org/code/#java)
* [GraphiQL](https://graphql.org/learn/serving-over-http/#graphiql)
* [Apprendre à utiliser GraphQL avec AEM ;](/help/sites-developing/headless/graphql-api/graphql-api-content-fragments.md)
   * [Activation de votre point d’entrée GraphQL](/help/sites-developing/headless/graphql-api/graphql-endpoint.md#enabling-graphql-endpoint)
   * [Installation de l’interface AEM GraphiQL](/help/sites-developing/headless/graphql-api/graphql-api-content-fragments.md#installing-graphiql-interface)
* [L’exemple de structure de fragment de contenu ;](/help/sites-developing/headless/graphql-api/content-fragments-graphql-samples.md#content-fragment-structure-graphql)
* [Apprendre à utiliser GraphQL avec AEM – Exemple de contenu et de requêtes](/help/sites-developing/headless/graphql-api/content-fragments-graphql-samples.md)
   * [Exemple de requête – Un fragment de ville unique et spécifique](/help/sites-developing/headless/graphql-api/content-fragments-graphql-samples.md#sample-single-specific-city-fragment)
   * [Exemple de requête pour des métadonnées – Liste des métadonnées pour les distinctions intitulées GB](/help/sites-developing/headless/graphql-api/content-fragments-graphql-samples.md#sample-metadata-awards-gb)
   * [Exemple de requête – Toutes les villes avec une variante nommée](/help/sites-developing/headless/graphql-api/content-fragments-graphql-samples.md#sample-cities-named-variation)
* [Activation de la fonctionnalité de fragments de contenu dans l’explorateur de configurations](/help/assets/content-fragments/content-fragments-configuration-browser.md#enable-content-fragment-functionality-in-configuration-browser)
* [Utilisation de fragments de contenu](/help/assets/content-fragments/content-fragments.md)
   * [Modèles de fragment de contenu](/help/assets/content-fragments/content-fragments-models.md)
   * [Sortie JSON](/help/assets/content-fragments/content-fragments-json-preview.md)
* [Comprendre le partage des ressources cross-origin (CORS)](https://experienceleague.adobe.com/docs/experience-manager-learn/foundation/security/understand-cross-origin-resource-sharing.html?lang=fr#understand-cross-origin-resource-sharing-(cors))
* [Prise en main d’AEM découplé](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/graphql/overview.html?lang=fr) – Une courte série de tutoriels vidéo qui donne un aperçu de l’utilisation des fonctionnalités d’AEM découplé, notamment la modélisation de contenu et GraphQL.

<!--
* [Generating Access Tokens for Server Side APIs](/help/implementing/developing/introduction/generating-access-tokens-for-server-side-apis.md)
-->
