---
title: Comment mettre à jour votre contenu à l’aide des API AEM Assets
description: Dans cette partie du parcours de développement AEM découplé, découvrez comment utiliser l’API REST pour accéder au contenu de vos fragments de contenu et le mettre à jour.
exl-id: af29cb77-0210-4fc4-8d86-2a833d19b49f
solution: Experience Manager, Experience Manager Sites
feature: Headless,Content Fragments,GraphQL,Persisted Queries,Developing
role: Admin, Developer
source-git-commit: 9a3008553b8091b66c72e0b6c317573b235eee24
workflow-type: tm+mt
source-wordcount: '1029'
ht-degree: 100%

---

# Comment mettre à jour votre contenu à l’aide des API AEM Assets {#update-your-content}

Dans cette partie du [parcours de développement AEM découplé](overview.md), découvrez comment utiliser l’API REST pour accéder au contenu de vos fragments de contenu et le mettre à jour.

## Un peu d’histoire...  {#story-so-far}

Dans le document précédent du parcours découplé AEM, [Comment accéder à votre contenu à l’aide des API de diffusion AEM](access-your-content.md), vous avez appris à accéder à votre contenu en mode découplé via l’API AEM GraphQL et vous devriez maintenant :

* Connaître GraphQL dans ses grandes lignes.
* Comprendre le fonctionnement de l’API AEM GraphQL.
* Connaître quelques exemples pratiques de requêtes.

Cet article s’appuie sur ces principes de base afin que vous compreniez comment accéder au contenu découplé existant dans AEM à l’aide de l’API AEM.

## Objectif {#objective}

* **Audience** : Niveau avancé
* **Objectif** : Découvrir comment utiliser l’API REST pour accéder au contenu de vos fragments de contenu et le mettre à jour :
   * Présentation de l’API HTTP d’AEM Assets.
   * Présentation et description de la prise en charge des fragments de contenu dans l’API.
   * Illustration de détails de l’API.

<!--
  * Look at sample code to see how things work in practice.
-->

## Pourquoi avez-vous besoin de l’API HTTP Assets pour le fragment de contenu {#why-http-api}

À l’étape précédente du parcours en mode découplé, vous avez appris à utiliser l’API AEM GraphQL afin de récupérer votre contenu à l’aide de requêtes.

Alors pourquoi une autre API est-elle nécessaire ?

L’API HTTP Assets vous permet de **Lire** votre contenu, mais elle vous permet également de **Créer**, de **Mettre à jour** et de **Supprimer** le contenu, des actions qui sont impossibles avec l’API GraphQL.

L’API REST Assets est disponible pour chaque installation prête à l’emploi d’une version récente d’Adobe Experience Manager.

## API HTTP Assets {#assets-http-api}

L’API HTTP Assets englobe les éléments suivants :

* API REST Assets
* Prise en charge des fragments de contenu

L’implémentation actuelle de l’API HTTP Assets repose sur le style architectural **REST** et permet d’accéder au contenu (stocké dans AEM) via les opérations **CRUD** (Create, Read, Update, Delete) pour créer, lire, mettre à jour, supprimer.

Grâce à ces opérations, l’API permet d’utiliser Adobe Experience Manager en tant que système de gestion de contenu (CMS) découplé en fournissant Content Services à une application frontale JavaScript. Ou toute autre application pouvant exécuter des requêtes HTTP et gérer les réponses JSON. Par exemple, les applications monopages, basées sur la structure ou personnalisées, nécessitent du contenu fourni via l’API HTTP, souvent au format JSON.

<!--
>[!NOTE]
>
>It is not possible to customize JSON output from the Assets REST API. 

The Assets REST API:

* follows the HATEOAS principle
* implements the SIREN format

## Key Concepts {#key-concepts}

The Assets REST API offers REST-style access to assets stored within an AEM instance. 

It uses the `/api/assets` endpoint and requires the path of the asset to access it (without the leading `/content/dam`). 

* This means that to access the asset at:
  * `/content/dam/path/to/asset`
* You need to request:
  * `/api/assets/path/to/asset` 

For example, to access `/content/dam/wknd/en/adventures/cycling-tuscany`, request `/api/assets/wknd/en/adventures/cycling-tuscany.json` 

>[!NOTE]
>Access over:
>
>* `/api/assets` **does not** need the use of the `.model` selector.
>* `/content/path/to/page` **does** require the use of the `.model` selector.

The HTTP method determines the operation to be executed:

* **GET** - to retrieve a JSON representation of an asset or a folder
* **POST** - to create new assets or folders
* **PUT** - to update the properties of an asset or folder
* **DELETE** - to delete an asset or folder

>[!NOTE]
>
>The request body and/or URL parameters can be used to configure some of these operations; for example, define that a folder or an asset should be created by a **POST** request.

The exact format of supported requests is defined in the API Reference documentation. 

### Transactional Behavior {#transactional-behavior}

All requests are atomic.

This means that subsequent (`write`) requests cannot be combined into a single transaction that could succeed or fail as a single entity.

### Security {#security}

If the Assets REST API is used within an environment without specific authentication requirements, AEM's CORS filter needs to be configured correctly.

>[!NOTE]
>
>For further information see:
>
>* CORS/AEM explained
>* Video - Developing for CORS with AEM

In environments with specific authentication requirements, OAuth is recommended.

## Available Features {#available-features}

Content Fragments are a specific type of Asset, see Working with Content Fragments.

For further information about features available through the API see:

* The Assets REST API (Additional Resources) 
* Entity Types, where the features specific to each supported type (as relevant to Content Fragments) are explained 

### Paging {#paging}

The Assets REST API supports paging (for GET requests) via the URL parameters:

* `offset` - the number of the first (child) entity to retrieve
* `limit` - the maximum number of entities returned

The response will contain paging information as part of the `properties` section of the SIREN output. This `srn:paging` property contains the total number of (child) entities ( `total`), the offset and the limit ( `offset`, `limit`) as specified in the request.

>[!NOTE]
>
>Paging is typically applied on container entities (that is, folders or assets with renditions), as it relates to the children of the requested entity.

#### Example: Paging {#example-paging}

`GET /api/assets.json?offset=2&limit=3`

```json
...
"properties": {
    ...
    "srn:paging": {
        "total": 7,
        "offset": 2,
        "limit": 3
    }
    ...
}
...
```

## Entity Types {#entity-types}

### Folders {#folders}

Folders act as containers for assets and other folders. They reflect the structure of the AEM content repository.

The Assets REST API exposes access to the properties of a folder; for example, its name, title, and so on. Assets are exposed as child entities of folders, and sub-folders.

>[!NOTE]
>
>Depending on the asset type of the child assets and folders the list of child entities may already contain the full set of properties that defines the respective child entity. Alternatively, only a reduced set of properties may be exposed for an entity in this list of child entities.

### Assets {#assets}

If an asset is requested, the response will return its metadata; such as title, name and other information as defined by the respective asset schema.

The binary data of an asset is exposed as a SIREN link of type `content`.

Assets can have multiple renditions. These are typically exposed as child entities, one exception being a thumbnail rendition, which is exposed as a link of type `thumbnail` ( `rel="thumbnail"`).
-->

## API HTTP Assets et fragments de contenu {#assets-http-api-content-fragments}

Les fragments de contenu sont utilisés pour une diffusion en mode découplé. Un fragment de contenu est un type spécial de ressource. Ils permettent d’accéder aux données structurées, telles que les textes, les nombres, les dates, etc.

<!--
As there are several differences to *standard* assets (such as images or audio), some additional rules apply to handling them.

### Representation {#representation}

Content fragments:

* Do not expose any binary data.
* Are completely contained in the JSON output (within the `properties` property).

* Are also considered atomic, that is, the elements and variations are exposed as part of the fragment's properties vs. as links or child entities. This allows for efficient access to the payload of a fragment.

### Content Models and Content Fragments {#content-models-and-content-fragments}

Currently the models that define the structure of a content fragment are not exposed through an HTTP API. Therefore the *consumer* needs to know about the model of a fragment (at least a minimum) - although most information can be inferred from the payload; as data types, and so on. are part of the definition.

To create a content fragment, the (internal repository) path of the model has to be provided.

### Associated Content {#associated-content}

Associated content is currently not exposed.
-->

## Utilisation de l’API REST Assets {#using-aem-assets-rest-api}

### Accès {#access}

L’API REST Assets utilise le point d’entrée `/api/assets` et nécessite le chemin d’accès de la ressource pour y accéder (sans `/content/dam` en préfixe).

* Cela signifie que pour accéder à la ressource à l’adresse suivante :
   * `/content/dam/path/to/asset`
* Vous devez demander :
   * `/api/assets/path/to/asset`

Par exemple, pour accéder à `/content/dam/wknd/en/adventures/cycling-tuscany`, demandez `/api/assets/wknd/en/adventures/cycling-tuscany.json`

>[!NOTE]
>Accès via :
>
>* `/api/assets` **ne nécessite pas** l’utilisation du sélecteur `.model`.
>* `/content/path/to/page` **nécessite** l’utilisation du sélecteur `.model`.

### Opération {#operation}

La méthode HTTP détermine l’opération à exécuter :

* **GET** : pour récupérer une représentation JSON d’une ressource ou d’un dossier
* **POST** : pour créer des ressources ou des dossiers
* **PUT** : pour mettre à jour les propriétés d’une ressource ou d’un dossier
* **SUPPRIMER** - pour supprimer une ressource ou un dossier.

>[!NOTE]
>
>Le corps de la requête et/ou les paramètres URL peuvent être utilisés pour configurer certaines de ces opérations ; par exemple, spécifier qu’un dossier ou une ressource doivent être créés par une requête **POST**.

Le format exact des requêtes prises en charge est défini dans la documentation Référence d’API.

L’utilisation peut varier selon que vous utilisez un environnement d’auteur ou de publication AEM dans votre cas d’utilisation spécifique.

* Il est vivement recommandé de lier la création à une instance d’auteur (et il n’existe actuellement aucun moyen de répliquer un fragment pour publier à l’aide de cette API).
* La diffusion est possible à partir des deux, car AEM diffuse le contenu demandé au format JSON uniquement.

   * Le stockage et la diffusion depuis une instance de création AEM doivent suffire pour les applications de bibliothèque de médias situées derrière le pare-feu.

   * Pour une diffusion web en direct, une instance de publication AEM est recommandée.

>[!CAUTION]
>
>La configuration du Dispatcher sur les instances AEM peut bloquer l’accès à `/api`.

>[!NOTE]
>
>Pour plus d’informations, voir la Référence d’API. En particulier, [API Adobe Experience Manager Assets – Fragments de contenu](https://www.adobe.io/experience-manager/reference-materials/6-5/assets-api-content-fragments/index.html).

### Lecture/Diffusion {#read-delivery}

Mode d’utilisation :

`GET /{cfParentPath}/{cfName}.json`

Par exemple :

`http://<host>/api/assets/wknd/en/adventures/cycling-tuscany.json`

La réponse est un JSON sérialisé avec le contenu structuré comme dans le fragment de contenu. Les références sont diffusées en tant qu’URL de référence.

Deux types d’opérations de lecture sont possibles :

* Lecture d’un fragment de contenu spécifique par chemin, ce qui renvoie la représentation JSON du fragment de contenu.
* Lecture d’un dossier de fragments de contenu par chemin : cela renvoie les représentations JSON de tous les fragments de contenu du dossier.

### Créer {#create}

Mode d’utilisation :

`POST /{cfParentPath}/{cfName}`

Le corps doit contenir une représentation JSON du fragment de contenu à créer, notamment tout contenu initial devant être défini sur les éléments de fragment de contenu. Il est obligatoire de définir la propriété `cq:model`, qui doit pointer vers un modèle de fragment de contenu valide. Sans cela, il se produira une erreur. Il est également nécessaire d’ajouter un en-tête `Content-Type`, défini sur `application/json`.

### Mettre à jour {#update}

Mode d’utilisation :

`PUT /{cfParentPath}/{cfName}`

Le corps doit contenir une représentation JSON de ce qui doit être mis à jour pour le fragment de contenu donné.

Il peut simplement s’agir du titre ou de la description d’un fragment de contenu, d’un élément unique ou de toutes les valeurs et/ou métadonnées d’un élément.

### Supprimer {#delete}

Mode d’utilisation :

`DELETE /{cfParentPath}/{cfName}`

Pour plus d’informations sur l’utilisation de l’API REST d’AEM Assets, vous pouvez accéder aux éléments suivants :

* API HTTP Assets d’Adobe Experience Manager (ressources supplémentaires)
* Prise en charge des fragments de contenu dans l’API HTTP AEM Assets (ressources supplémentaires)

## Et après ? {#whats-next}

Maintenant que vous avez terminé cette partie du parcours de développement découplé AEM, vous devriez pouvoir :

* Comprendre les principes de base de l’API HTTP d’AEM Assets.
* Comprendre comment les fragments de contenu sont pris en charge dans cette API.

<!--
* Have experience with sample code and know how the API works in practice.
-->

<!-- The "How to put it all together" page is not going to be published until the first public release of the Headless SDK. Temporarily commenting out the reference below. -->

<!--You should continue your AEM headless journey by next reviewing the document [How to Put It All Together - Your App and Your Content in AEM Headless](put-it-all-together.md) where you learn how to take your AEM Headless project and prepare it for going live.-->

Poursuivez votre parcours dans AEM découplé en consultant le document [Comment mettre en ligne votre application en mode découplé](go-live.md) dans lequel vous mettez en ligne votre projet AEM découplé.

## Ressources supplémentaires {#additional-resources}

* [API HTTP Assets](/help/assets/mac-api-assets.md)
* [API REST de fragments de contenu](/help/assets/assets-api-content-fragments.md)
   * [Référence d’API](/help/assets/assets-api-content-fragments.md#api-reference)
* [API Adobe Experience Manager Assets – Fragments de contenu](https://www.adobe.io/experience-manager/reference-materials/6-5/assets-api-content-fragments/index.html)
* [Utilisation de fragments de contenu](/help/assets/content-fragments/content-fragments.md)
* [AEM Core Components](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=fr)
* [CORS/AEM expliqué](https://helpx.adobe.com/fr/experience-manager/kt/platform-repository/using/cors-security-article-understand.html)
* [Vidéo – Développement pour CORS et AEM](https://helpx.adobe.com/fr/experience-manager/kt/platform-repository/using/cors-security-technical-video-develop.html)
* [Présentation d’AEM en tant que CMS découplé](/help/sites-developing/headless/introduction.md)
* Le [Portail de développement AEM](https://experienceleague.adobe.com/landing/experience-manager/headless/developer.html?lang=fr)
* [Tutoriels pour Headless dans AEM](https://experienceleague.adobe.com/docs/experience-manager-learn/getting-started-with-aem-headless/overview.html?lang=fr)
