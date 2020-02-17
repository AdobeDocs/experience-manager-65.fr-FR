---
title: API Assets HTTP
description: Découvrez l’implémentation, le modèle de données et les fonctions de l’API Assets HTTP. Utilisez l’API Assets HTTP pour effectuer diverses tâches avec les ressources.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 0ff23556444fcb161b0adf744bb72fdc50322d92

---


# API HTTP Assets {#assets-http-api}

## Présentation {#overview}

L’API HTTP Assets permet de créer, lire, mettre à jour et supprimer (CRUD) des opérations sur les ressources, y compris des fichiers binaires, des métadonnées, des rendus et des commentaires, ainsi que du contenu structuré à l’aide de fragments de contenu AEM. Il est exposé à `/api/assets` et implémenté en tant qu’API REST. Elle inclut [la prise en charge des fragments de contenu](/help/assets/assets-api-content-fragments.md).

Pour accéder à l’API, procédez comme suit :

1. Open the API service document at `https://[hostname]:[port]/api.json`.
1. Suivez le lien du service Ressources qui mène à `https://[hostname]:[server]/api/assets.json`.

La réponse API est un fichier JSON pour certains types MIME et un code de réponse pour tous les types MIME. La réponse JSON est facultative et peut ne pas être disponible, par exemple pour les fichiers PDF. Vous pouvez faire appel au code de réponse pour d’autres analyses ou actions.

Après l’heure [!UICONTROL de]désactivation, une ressource et ses rendus ne sont pas disponibles via l’interface Web Ressources ou via l’API HTTP. L’API renvoie un message d’erreur 404 si l’heure  d’activation est dans le futur ou si l’heure [!UICONTROL d’] arrêt est dans le passé.

## Fragments de contenu {#content-fragments}

Un [fragment de contenu](/help/assets/content-fragments.md) est un type de ressource spécial. Il permet d’accéder aux données structurées, telles que les textes, les nombres, les dates, etc. Comme il existe plusieurs différences de ressources `standard` (telles que les images ou les documents), certaines règles supplémentaires s’appliquent pour gérer les fragments de contenu.

Pour plus d’informations, voir [Prise en charge de fragments de contenu dans l’API HTTP Assets d’AEM](/help/assets/assets-api-content-fragments.md).

## Modèle de données {#data-model}

L’API HTTP Assets présente deux éléments principaux : des dossiers et des ressources (pour les ressources standard).

Il expose également des éléments plus détaillés pour les modèles de données personnalisés décrivant le contenu structuré dans les fragments de contenu. Pour plus d’informations, voir [Modèles de données de fragments de contenu](/help/assets/assets-api-content-fragments.md#content-fragments).

### Dossiers {#folders}

Les dossiers sont comme des répertoires dans les systèmes de fichiers traditionnels. Ils font office de conteneurs pour d’autres dossiers ou ressources. Les dossiers se composent des éléments suivants :

**Entités**: Les entités d’un dossier sont ses éléments enfants, qui peuvent être des dossiers et des ressources.

**Propriétés**:
* `name`  — Nom du dossier. Il s’agit de la même chose que le dernier segment du chemin d’accès à l’URL sans l’extension
* `title` — Titre facultatif du dossier pouvant être affiché au lieu de son nom

>[!NOTE]
>
>Certaines propriétés de dossier ou de ressource sont associées à un préfixe différent. Le `jcr` préfixe `jcr:title`, `jcr:description`et `jcr:language` est remplacé par le préfixe `dc` . Hence in the returned JSON, `dc:title` and `dc:description` contain the values of `jcr:title` and `jcr:description`, respectively.

**Les dossiers de liens** présentent trois liens :
* `self`: Lien vers lui-même
* `parent`: Lien vers le dossier parent
* `thumbnail`: (Facultatif) Lien vers une image miniature de dossier

### Assets {#assets}

Dans AEM, un fichier contient les éléments suivants :

* Propriétés et métadonnées de la ressource
* Plusieurs rendus tels que le rendu d’origine (qui est la ressource transférée initialement), une vignette et divers autres rendus. Les rendus supplémentaires peuvent être des images de tailles différentes, différents codages vidéo ou des pages extraites de PDF ou InDesign.
* Commentaires facultatifs

Pour plus d’informations sur les éléments dans les fragments de contenu, voir [Prise en charge des fragments de contenu dans l’API HTTP Assets d’AEM](/help/assets/assets-api-content-fragments.md#content-fragments).

Dans AEM, un dossier comporte les composants suivants :

* Entités : Les enfants de Assets sont ses rendus.
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
>Pour faciliter la lecture, la notation cURL complète n’est pas utilisée dans les exemples suivants. In fact the notation does correlate with [Resty](https://github.com/micha/resty) which is a script wrapper for `cURL`.

**Conditions préalables**

* Aller à `https://[aem_server]:[port]/system/console/configMgr`.
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

La classe de l&#39;entité renvoyée est assets/folder.

Les propriétés des entités contenues représentent un sous-ensemble du jeu complet des propriétés de chaque entité. In order to obtain a full representation of the entity, clients should retrieve the contents of the URL pointed to by the link with a `rel` of `self`.

## Création d’un dossier {#create-a-folder}

Creates a new `sling`: `OrderedFolder` at the given path. Si un * est donné à la place d’un nom de noeud, la servlet utilisera le nom du paramètre comme nom de noeud. Accepted as request data is either a Siren representation of the new folder or a set of name-value pairs, encoded as `application/www-form-urlencoded` or `multipart`/ `form`- `data`, useful for creating a folder directly from an HTML form. Les propriétés du dossier peuvent, en outre, être spécifiées en tant que paramètres de requête URL.

The operation will fail with a `500` response code if the parent node of the given path does not exist. If the folder already exists a `409` response code is returned.

**Paramètres**

* `name` - Nom du dossier

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
* `file` - Référence du fichier

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

Met à jour les propriétés de métadonnées d’une ressource. Si vous mettez à jour une propriété dans l’ `dc:` espace de noms, l’API met à jour la même propriété dans l’ `jcr` espace de noms. L’API ne synchronise pas les propriétés sous les deux espaces de noms.

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

Crée un rendu pour une ressource. Si le nom du paramètre de requête n’est pas fourni, le nom du fichier est utilisé comme nom du rendu.

**Paramètres**

* `name` - Nom du rendu
* `file` - Référence du fichier

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

* `message` - Message
* `annotationData` - Données d’annotation (JSON)

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
