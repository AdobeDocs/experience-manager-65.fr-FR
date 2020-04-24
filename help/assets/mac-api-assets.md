---
title: API HTTP Assets
description: Découvrez l’implémentation, le modèle de données et les fonctions de l’API Assets HTTP. Utilisez l’API Assets HTTP pour effectuer diverses tâches avec les ressources.
contentOwner: AG
translation-type: tm+mt
source-git-commit: abc4821ec3720969bf1c2fb068744c07477aca46

---


# API HTTP Assets {#assets-http-api}

## Présentation {#overview}

L’API HTTP Assets permet d’effectuer des opérations CRUD (créer, lire, mettre à jour, supprimer) sur les ressources, y compris les fichiers binaires, les métadonnées, les rendus et les commentaires, avec du contenu structuré à l’aide de fragments de contenu AEM. Elle est exposée sous `/api/assets` et est implémentée en tant qu’API REST. Elle inclut [la prise en charge des fragments de contenu](/help/assets/assets-api-content-fragments.md).

Pour accéder à l’API, procédez comme suit :

1. Ouvrez le document du service API à l’adresse `https://[hostname]:[port]/api.json`.
1. Suivez le lien du service Assets pointant vers `https://[hostname]:[server]/api/assets.json`.

La réponse de l’API est un fichier JSON pour certains types MIME et un code de réponse pour tous les types MIME. La réponse JSON est facultative et peut ne pas être disponible, par exemple pour les fichiers PDF. Vous pouvez faire appel au code de réponse pour d’autres analyses ou actions.

Après l’[!UICONTROL heure de désactivation], une ressource et ses rendus ne sont plus disponibles via l’interface web d’Assets ou via l’API HTTP. L’API renvoie un message d’erreur 404 si l’[!UICONTROL heure d’activation] se situe dans le futur ou si l’[!UICONTROL heure de désactivation] se situe dans le passé.

## Fragments de contenu {#content-fragments}

Un [fragment de contenu](/help/assets/content-fragments.md) est un type de ressource spécial. Il permet d’accéder aux données structurées, telles que les textes, les nombres, les dates, etc. Comme il existe plusieurs différences de ressources `standard` (telles que les images ou les documents), certaines règles supplémentaires s’appliquent pour gérer les fragments de contenu.

Pour plus d’informations, voir [Prise en charge de fragments de contenu dans l’API HTTP Assets d’AEM](/help/assets/assets-api-content-fragments.md).

## Modèle de données {#data-model}

L’API HTTP Assets présente deux éléments principaux : des dossiers et des ressources (pour les ressources standard).

Il expose également des éléments plus détaillés pour les modèles de données personnalisés décrivant le contenu structuré dans les fragments de contenu. Pour plus d’informations, voir [Modèles de données de fragments de contenu](/help/assets/assets-api-content-fragments.md#content-fragments).

### Dossiers {#folders}

Les dossiers sont comparables aux répertoires des systèmes de fichiers traditionnels. Ils font office de conteneurs pour d’autres dossiers ou ressources. Les dossiers se composent des éléments suivants :

**Entités** : les entités d’un dossier sont ses éléments enfants qui peuvent, à leur tour, être des dossiers et des ressources.

**Propriétés** :
* `name` : nom du dossier. Identique au dernier segment du chemin d’URL, sans l’extension.
* `title` : titre facultatif du dossier pouvant être affiché au lieu de son nom.

>[!NOTE]
>
>Certaines propriétés de dossier ou de ressource sont associées à un préfixe différent. Le préfixe `jcr` de `jcr:title`, `jcr:description` et `jcr:language` est remplacé par le préfixe `dc`. Par conséquent, dans le JSON renvoyé, `dc:title` et `dc:description` contiennent respectivement les valeurs de `jcr:title` et `jcr:description`.

Les dossiers **Liens** présentent trois liens :
* `self` : lien vers lui-même
* `parent` : lien vers le dossier parent
* `thumbnail` : (Facultatif) lien vers une miniature de dossier

### Ressources {#assets}

Dans AEM, une ressource contient les éléments suivants :

* Propriétés et métadonnées de la ressource
* Plusieurs rendus tels que le rendu d’origine (qui est la ressource transférée initialement), une vignette et divers autres rendus. Les rendus supplémentaires peuvent être des images de tailles différentes, différents codages vidéo ou des pages extraites de PDF ou InDesign.
* Commentaires facultatifs

Pour plus d’informations sur les éléments dans les fragments de contenu, voir [Prise en charge des fragments de contenu dans l’API HTTP Assets d’AEM](/help/assets/assets-api-content-fragments.md#content-fragments).

Dans AEM, un dossier comprend les composants suivants :

* Entités : les enfants des ressources sont ses rendus.
* Propriétés
* Liens

L’API Assets HTTP offre les fonctionnalités suivantes :

* Récupérer une liste de dossiers
* Créer un dossier
* Créer une ressource  
* Mettre à jour le fichier binaire d’une ressource
* Mettre à jour les métadonnées d’une ressource
* Créer un rendu de ressource
* Mettre à jour un rendu de ressource
* Créer un commentaire de ressource
* Copier un dossier ou une ressource
* Déplacer un dossier ou une ressource
* Supprimer un dossier, une ressource ou un rendu

>[!NOTE]
>
>Pour faciliter la lecture, la notation cURL complète n’est pas utilisée dans les exemples suivants. En fait, la notation est liée à [Resty](https://github.com/micha/resty) qui est un wrapper de script pour `cURL`.

**Conditions préalables**

* Accédez à `https://[aem_server]:[port]/system/console/configMgr`.
* Navigate to **Adobe Granite CSRF Filter**.
* Make sure the property **Filter Methods** includes: POST, PUT, DELETE.

## Récupérer une liste de dossiers {#retrieve-a-folder-listing}

Récupère une représentation Siren d’un dossier existant et de ses entités enfants (sous-dossiers ou ressources).

**Demande**

```
GET /api/assets/myFolder.json
```

**Codes de réponse**

```
200 - OK - success
404 - NOT FOUND - folder does not exist or is not accessible
500 - INTERNAL SERVER ERROR - if something else goes wrong
```

**Réponse**

La classe de l’entité renvoyée est assets/folder (ressources/dossier).

Les propriétés des entités contenues représentent un sous-ensemble du jeu complet des propriétés de chaque entité. Pour obtenir une représentation complète de l’entité, les clients doivent récupérer le contenu de l’URL vers laquelle pointe le lien avec l’élément `rel` `self`.

## Création d’un dossier {#create-a-folder}

Crée un dossier `sling`: `OrderedFolder` à l’emplacement indiqué. Si un * est donné à la place d’un nom de noeud, la servlet utilise le nom du paramètre comme nom de noeud. Cela est accepté dans la mesure où les données de la demande consistent en une représentation Siren du nouveau dossier ou un ensemble de paires nom-valeur, codé sous la forme `application/www-form-urlencoded` ou `multipart`/ `form`- `data`, ce qui se révèle utile pour créer directement un dossier à partir d’un formulaire HTML. Les propriétés du dossier peuvent, en outre, être spécifiées en tant que paramètres de requête URL.

L’opération échoue et un code de réponse `500` est renvoyé si le nœud parent du chemin d’accès indiqué n’existe pas. Si le fichier existe déjà, un code de réponse `409` est renvoyé.

**Paramètres**

* `name` : nom du dossier

**Demande**

```
POST /api/assets/myFolder -H"Content-Type: application/json" -d '{"class":"assetFolder","properties":{"title":"My Folder"}}'
```

ou

```
POST /api/assets/* -F"name=myfolder" -F"title=My Folder"
```

**Codes de réponse**

```
201 - CREATED - on successful creation
409 - CONFLICT - if folder already exist
412 - PRECONDITION FAILED - if root collection cannot be found or accessed
500 - INTERNAL SERVER ERROR - if something else goes wrong
```

## Créer une ressource {#create-an-asset}

Crée une ressource DAM à l’emplacement indiqué avec le fichier spécifié. Si un * est donné à la place d’un nom de noeud, la servlet utilisera le nom du paramètre ou le nom du fichier comme nom de noeud.

**Paramètres**

* `name` - Nom du fichier
* `file` : référence du fichier

**Demande**

```
POST /api/assets/myFolder/myAsset.png -H"Content-Type: image/png" --data-binary "@myPicture.png"
```

ou

```
POST /api/assets/myFolder/* -F"name=myAsset.png" -F"file=@myPicture.png"
```

**Codes de réponse**

```
201 - CREATED - if Asset has been created successfully
409 - CONFLICT - if Asset already exist
412 - PRECONDITION FAILED - if root collection cannot be found or accessed
500 - INTERNAL SERVER ERROR - if something else goes wrong
```

## Mettre à jour le fichier binaire d’une ressource {#update-asset-binary}

Met à jour un binaire Ressources (rendu avec le nom original). Cela déclenchera le processus de ressources par défaut, à condition qu’il soit configuré.

**Demande**

```
PUT /api/assets/myfolder/myAsset.png -H"Content-Type: image/png" --data-binary @myPicture.png
```

**Codes de réponse**

```
200 - OK - if Asset has been updated successfully
404 - NOT FOUND - if Asset could not be found or accessed at the provided URI
412 - PRECONDITION FAILED - if root collection cannot be found or accessed
500 - INTERNAL SERVER ERROR - if something else goes wrong
```

## Mettre à jour les métadonnées d’une ressource {#update-asset-metadata}

Met à jour les propriétés de métadonnées d’une ressource. Si vous mettez à jour une propriété dans le  du `dc:` , l’API met à jour la même propriété dans le `jcr` de la . L’API ne synchronise pas les propriétés sous les deux  .

**Demande**

```
PUT /api/assets/myfolder/myAsset.png -H"Content-Type: application/json" -d '{"class":"asset", "properties":{"dc:title":"My Asset"}}'
```

**Codes de réponse**

```
200 - OK - if Asset has been updated successfully
404 - NOT FOUND - if Asset could not be found or accessed at the provided URI
412 - PRECONDITION FAILED - if root collection cannot be found or accessed
500 - INTERNAL SERVER ERROR - if something else goes wrong
```

## Créer un rendu de ressource {#create-an-asset-rendition}

Crée un rendu pour une ressource. Si le nom de paramètre de requête n’est pas fourni, le nom de fichier est utilisé comme nom du rendu.

**Paramètres**

* `name` : nom du rendu
* `file` : référence du fichier

**Demande**

```
POST /api/assets/myfolder/myasset.png/renditions/web-rendition -H"Content-Type: image/png" --data-binary "@myRendition.png"
```

ou

```
POST /api/assets/myfolder/myasset.png/renditions/* -F"name=web-rendition" -F"file=@myRendition.png"
```

**Codes de réponse**

```
201 - CREATED - if Rendition has been created successfully
404 - NOT FOUND - if Asset could not be found or accessed at the provided URI
412 - PRECONDITION FAILED - if root collection cannot be found or accessed
500 - INTERNAL SERVER ERROR - if something else goes wrong
```

## Mettre à jour un rendu de ressource {#update-an-asset-rendition}

Met à jour et remplace le rendu d’une ressource par les nouvelles données binaires.

**Demande**

```
PUT /api/assets/myfolder/myasset.png/renditions/myRendition.png -H"Content-Type: image/png" --data-binary @myRendition.png
```

**Codes de réponse**

```
200 - OK - if Rendition has been updated successfully
404 - NOT FOUND - if Asset could not be found or accessed at the provided URI
412 - PRECONDITION FAILED - if root collection cannot be found or accessed
500 - INTERNAL SERVER ERROR - if something else goes wrong
```

## Créer un commentaire de ressource {#create-an-asset-comment}

Crée un commentaire de ressource.

**Paramètres**

* `message` : message
* `annotationData` : données d’annotation (JSON)

**Demande**

```
POST /api/assets/myfolder/myasset.png/comments/* -F"message=Hello World." -F"annotationData={}"
```

**Codes de réponse**

```
201 - CREATED - if Comment has been created successfully
404 - NOT FOUND - if Asset could not be found or accessed at the provided URI
412 - PRECONDITION FAILED - if root collection cannot be found or accessed
500 - INTERNAL SERVER ERROR - if something else goes wrong
```

## Copier un dossier ou une ressource {#copy-a-folder-or-asset}

Copie un fichier ou une ressource de l’emplacement indiqué vers une nouvelle destination.

**En-têtes de requête**

```
X-Destination - a new destination URI within the API solution scope to copy the resource to
X-Depth - either 'infinity' or '0'. The value '0' only copies the resource and its properties, no children.
X-Overwrite - 'F' to prevent overwriting an existing destination
```

**Demande**

```
COPY /api/assets/myFolder -H"X-Destination: /api/assets/myFolder-copy"
```

**Codes de réponse**

```
201 - CREATED - if folder/asset has been copied to a non-existing destination
204 - NO CONTENT - if the folder/asset has been copied to an existing destination
412 - PRECONDITION FAILED - if a request header is missing or
500 - INTERNAL SERVER ERROR - if something else goes wrong
```

## Déplacer un dossier ou une ressource {#move-a-folder-or-asset}

Déplace un dossier ou une ressource de l’emplacement indiqué vers une nouvelle destination.

**En-têtes de requête**

```
X-Destination - a new destination URI within the API solution scope to copy the resource to
X-Depth - either 'infinity' or '0'. The value '0' only copies the resource and its properties, no children.
X-Overwrite - either 'T' to force deletion of existing resources or 'F' to prevent overwriting an existing resource.
```

**Demande**

```
MOVE /api/assets/myFolder -H"X-Destination: /api/assets/myFolder-moved"
```

**Codes de réponse**

```
201 - CREATED - if folder/asset has been copied to a non-existing destination
204 - NO CONTENT - if the folder/asset has been copied to an existing destination
412 - PRECONDITION FAILED - if a request header is missing or
500 - INTERNAL SERVER ERROR - if something else goes wrong
```

## Supprimer un dossier, une ressource ou un rendu {#delete-a-folder-asset-or-rendition}

Supprime une ressource (arborescence) à l’emplacement indiqué.

**Demande**

```
DELETE /api/assets/myFolder
```

ou

```
DELETE /api/assets/myFolder/myAsset.png
```

ou

```xml
DELETE /api/assets/myFolder/myAsset.png/renditions/original
```

**Codes de réponse**

```
200 - OK - if folder has been deleted successfully
412 - PRECONDITION FAILED - if root collection cannot be found or accessed
500 - INTERNAL SERVER ERROR - if something else goes wrong
```
