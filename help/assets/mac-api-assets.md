---
title: API HTTP Assets in [!DNL Adobe Experience Manager].
description: Créez, lisez, mettez à jour, supprimez et gérez des ressources numériques à l’aide de l’API HTTP dans [!DNL Adobe Experience Manager Assets].
contentOwner: AG
translation-type: tm+mt
source-git-commit: 566add37d6dd7efe22a99fc234ca42878f050aee
workflow-type: tm+mt
source-wordcount: '1566'
ht-degree: 36%

---


# API HTTP Assets {#assets-http-api}

## Présentation {#overview}

The Assets HTTP API allows for create-read-update-delete (CRUD) operations on digital assets, including on metadata, on renditions, and on comments, together with structured content using [!DNL Experience Manager] Content Fragments. Elle est exposée sous `/api/assets` et est implémentée en tant qu’API REST. Elle inclut [la prise en charge des fragments de contenu](/help/assets/assets-api-content-fragments.md).

Pour accéder à l’API, procédez comme suit :

1. Ouvrez le document du service API à l’adresse `https://[hostname]:[port]/api.json`.
1. Suivez le lien du service Assets pointant vers `https://[hostname]:[server]/api/assets.json`.

La réponse de l’API est un fichier JSON pour certains types MIME et un code de réponse pour tous les types MIME. La réponse JSON est facultative et peut ne pas être disponible, par exemple pour les fichiers PDF. Vous pouvez faire appel au code de réponse pour d’autres analyses ou actions.

After the [!UICONTROL Off Time], an asset and its renditions are not available via the [!DNL Assets] web interface and through the HTTP API. L’API renvoie un message d’erreur 404 si l’[!UICONTROL heure d’activation] se situe dans le futur ou si l’[!UICONTROL heure de désactivation] se situe dans le passé.

## Fragments de contenu {#content-fragments}

Un [fragment de contenu](/help/assets/content-fragments.md) est un type de ressource spécial. Il permet d’accéder aux données structurées, telles que les textes, les nombres, les dates, etc. Comme il existe plusieurs différences de ressources `standard` (telles que les images ou les documents), certaines règles supplémentaires s’appliquent pour gérer les fragments de contenu.

For further information see [Content Fragments Support in the Experience Manager Assets HTTP API](/help/assets/assets-api-content-fragments.md).

## Modèle de données {#data-model}

L’API HTTP Assets présente deux éléments principaux : des dossiers et des ressources (pour les ressources standard).

Il expose également des éléments plus détaillés pour les modèles de données personnalisés décrivant le contenu structuré dans les fragments de contenu. Pour plus d’informations, voir [Modèles de données de fragments de contenu](/help/assets/assets-api-content-fragments.md#content-fragments).

### Dossiers {#folders}

Les dossiers sont comparables aux répertoires des systèmes de fichiers traditionnels. Ils font office de conteneurs pour d’autres dossiers ou ressources. Les dossiers se composent des éléments suivants :

**Entités** : les entités d’un dossier sont ses éléments enfants qui peuvent, à leur tour, être des dossiers et des ressources.

**Propriétés** :

* `name` est le nom du dossier. Il s’agit de la même chose que le dernier segment du chemin d’accès à l’URL sans l’extension.
* `title` est un titre facultatif du dossier qui peut être affiché à la place de son nom.

>[!NOTE]
>
>Certaines propriétés de dossier ou de ressource sont associées à un préfixe différent. Le préfixe `jcr` de `jcr:title`, `jcr:description` et `jcr:language` est remplacé par le préfixe `dc`. Par conséquent, dans le JSON renvoyé, `dc:title` et `dc:description` contiennent respectivement les valeurs de `jcr:title` et `jcr:description`.

Les dossiers **Liens** présentent trois liens :

* `self` : lien vers lui-même.
* `parent`: Lien vers le dossier parent.
* `thumbnail`: (Facultatif) Lien vers une image miniature de dossier.

### Ressources {#assets}

Dans Experience Manager, un fichier contient les éléments suivants :

* Propriétés et métadonnées de la ressource.
* Plusieurs rendus tels que le rendu d’origine (qui est la ressource transférée initialement), une vignette et divers autres rendus. Additional renditions may be images of different sizes, different video encodings, or extracted pages from PDF or [!DNL Adobe InDesign] files.
* Commentaires facultatifs.

For information about elements in Content Fragments see [Content Fragments Support in Experience Manager Assets HTTP API](/help/assets/assets-api-content-fragments.md#content-fragments).

In [!DNL Experience Manager] a folder has the following components:

* Entités : Les enfants des actifs sont ses rendus.
* Propriétés.
* Liens.

L’API Assets HTTP offre les fonctionnalités suivantes :

* Récupérer une liste de dossiers.
* Créer un dossier.
* Créer une ressource.
* Mettre à jour le fichier binaire d’une ressource.
* Mettre à jour les métadonnées d’une ressource.
* Créer un rendu de ressource.
* Mettre à jour un rendu de ressource.
* Créer un commentaire de ressource.
* Copier un dossier ou une ressource.
* Déplacer un dossier ou une ressource.
* Supprimer un dossier, une ressource ou un rendu.

>[!NOTE]
>
>Pour faciliter la lecture, la notation cURL complète n’est pas utilisée dans les exemples suivants. En fait, la notation est liée à [Resty](https://github.com/micha/resty) qui est un wrapper de script pour `cURL`.

**Conditions préalables**

* Accédez à l’adresse `https://[aem_server]:[port]/system/console/configMgr`.
* Navigate to **[!UICONTROL Adobe Granite CSRF Filter]**.
* Assurez-vous que la propriété Méthodes **[!UICONTROL de]** filtrage inclut les éléments suivants : `POST`, `PUT`, `DELETE`.

## Récupérer une liste de dossiers {#retrieve-a-folder-listing}

Récupère une représentation Siren d’un dossier existant et de ses entités enfants (sous-dossiers ou ressources).

**Demande**: `GET /api/assets/myFolder.json`

**Codes** de réponse : Les codes de réponse sont les suivants :

* 200 - OK - succès.
* 404 - NON TROUVÉ - le dossier n&#39;existe pas ou n&#39;est pas accessible.
* 500 - ERREUR DU SERVEUR INTERNE - si quelque chose d&#39;autre ne va pas.

**Réponse**: La classe de l&#39;entité renvoyée est une ressource ou un dossier. Les propriétés des entités contenues sont un sous-ensemble du jeu complet de propriétés de chaque entité. Pour obtenir une représentation complète de l’entité, les clients doivent récupérer le contenu de l’URL vers laquelle pointe le lien avec l’élément `rel` `self`.

## Créer un dossier {#create-a-folder}

Crée un dossier `sling` : `OrderedFolder` à l’emplacement indiqué. If a `*` is provided instead of a node name, the servlet uses the parameter name as node name. Cela est accepté dans la mesure où les données de la demande consistent en une représentation Siren du nouveau dossier ou un ensemble de paires nom-valeur, codé sous la forme `application/www-form-urlencoded` ou `multipart`/ `form`- `data`, ce qui se révèle utile pour créer directement un dossier à partir d’un formulaire HTML. Les propriétés du dossier peuvent, en outre, être spécifiées en tant que paramètres de requête URL.

Un appel d’API échoue avec un code de `500` réponse si le noeud parent du chemin d’accès fourni n’existe pas. Un appel renvoie un code de réponse `409` si le dossier existe déjà.

**Paramètres**: `name` est le nom du dossier.

**Demande**

* `POST /api/assets/myFolder -H"Content-Type: application/json" -d '{"class":"assetFolder","properties":{"title":"My Folder"}}'`
* `POST /api/assets/* -F"name=myfolder" -F"title=My Folder"`

**Codes** de réponse : Les codes de réponse sont les suivants :

* 201 - CRÉÉ - sur la création réussie.
* 409 - CONFLIT - si un dossier existe déjà.
* 412 - ÉCHEC DE LA PRÉCONDITION - si la collection racine est introuvable ou est inaccessible.
* 500 - ERREUR DU SERVEUR INTERNE - si quelque chose d&#39;autre ne va pas.

## Créer une ressource {#create-an-asset}

Placez le fichier fourni à l’emplacement indiqué pour créer un actif dans le référentiel DAM. If a `*` is provided instead of a node name, the servlet uses the parameter name or the file name as node name.

**Paramètres**: Les paramètres concernent `name` le nom de la ressource et `file` la référence au fichier.

**Demande**

* `POST /api/assets/myFolder/myAsset.png -H"Content-Type: image/png" --data-binary "@myPicture.png"`
* `POST /api/assets/myFolder/* -F"name=myAsset.png" -F"file=@myPicture.png"`

**Codes** de réponse : Les codes de réponse sont les suivants :

* 201 - CRÉÉ - si la création de l’actif a réussi.
* 409 - CONFLIT - si l&#39;actif existe déjà.
* 412 - ÉCHEC DE LA PRÉCONDITION - si la collection racine est introuvable ou est inaccessible.
* 500 - ERREUR DU SERVEUR INTERNE - si quelque chose d&#39;autre ne va pas.

## Mise à jour d’un fichier binaire de ressource {#update-asset-binary}

Met à jour le binaire d’un fichier (rendu avec le nom original). Une mise à jour déclenche l’exécution du processus de traitement des ressources par défaut, s’il est configuré.

**Demande**: `PUT /api/assets/myfolder/myAsset.png -H"Content-Type: image/png" --data-binary @myPicture.png`

**Codes** de réponse : Les codes de réponse sont les suivants :

* 200 - OK - si la mise à jour de la ressource a réussi.
* 404 - NON TROUVÉ - si le fichier n’a pas été trouvé ou n’a pas été accessible à l’URI fourni.
* 412 - ÉCHEC DE LA PRÉCONDITION - si la collection racine est introuvable ou est inaccessible.
* 500 - ERREUR DU SERVEUR INTERNE - si quelque chose d&#39;autre ne va pas.

## Mettre à jour les métadonnées d’une ressource {#update-asset-metadata}

Met à jour les propriétés de métadonnées d’une ressource. Si vous mettez à jour une propriété de l’ `dc:` espace de nommage, l’API met à jour la même propriété dans l’ `jcr` espace de nommage. L’API ne synchronise pas les propriétés sous les deux espaces de nommage.

**Demande**: `PUT /api/assets/myfolder/myAsset.png -H"Content-Type: application/json" -d '{"class":"asset", "properties":{"dc:title":"My Asset"}}'`

**Codes** de réponse : Les codes de réponse sont les suivants :

* 200 - OK - si la mise à jour de la ressource a réussi.
* 404 - NON TROUVÉ - si le fichier n’a pas été trouvé ou n’a pas été accessible à l’URI fourni.
* 412 - ÉCHEC DE LA PRÉCONDITION - si la collection racine est introuvable ou est inaccessible.
* 500 - ERREUR DU SERVEUR INTERNE - si quelque chose d&#39;autre ne va pas.

## Créer un rendu de ressource {#create-an-asset-rendition}

Créez un rendu de ressource pour une ressource. Si le nom du paramètre de requête n’est pas fourni, le nom du fichier est utilisé comme nom du rendu.

**Paramètres**: Les paramètres servent `name` au nom du rendu et `file` à la référence du fichier.

**Demande**

* `POST /api/assets/myfolder/myasset.png/renditions/web-rendition -H"Content-Type: image/png" --data-binary "@myRendition.png"`
* `POST /api/assets/myfolder/myasset.png/renditions/* -F"name=web-rendition" -F"file=@myRendition.png"`

**Codes** de réponse : Les codes de réponse sont les suivants :

* 201 - CRÉÉ - si le rendu a été créé avec succès.
* 404 - NON TROUVÉ - si le fichier n’a pas été trouvé ou n’a pas été accessible à l’URI fourni.
* 412 - ÉCHEC DE LA PRÉCONDITION - si la collection racine est introuvable ou est inaccessible.
* 500 - ERREUR DU SERVEUR INTERNE - si quelque chose d&#39;autre ne va pas.

## Mettre à jour un rendu de ressource {#update-an-asset-rendition}

Met à jour et remplace le rendu d’une ressource par les nouvelles données binaires.

**Demande**: `PUT /api/assets/myfolder/myasset.png/renditions/myRendition.png -H"Content-Type: image/png" --data-binary @myRendition.png`

**Codes** de réponse : Les codes de réponse sont les suivants :

* 200 - OK - si le rendu a été mis à jour avec succès.
* 404 - NON TROUVÉ - si le fichier n’a pas été trouvé ou n’a pas été accessible à l’URI fourni.
* 412 - ÉCHEC DE LA PRÉCONDITION - si la collection racine est introuvable ou est inaccessible.
* 500 - ERREUR DU SERVEUR INTERNE - si quelque chose d&#39;autre ne va pas.

## Ajouter un commentaire sur une ressource {#create-an-asset-comment}

Crée un commentaire de ressource.

**Paramètres**: Les paramètres concernent `message` le corps du message du commentaire et `annotationData` les données d’annotation au format JSON.

**Demande**: `POST /api/assets/myfolder/myasset.png/comments/* -F"message=Hello World." -F"annotationData={}"`

**Codes** de réponse : Les codes de réponse sont les suivants :

* 201 - CRÉÉ - si le commentaire a été créé avec succès.
* 404 - NON TROUVÉ - si le fichier n’a pas été trouvé ou n’a pas été accessible à l’URI fourni.
* 412 - ÉCHEC DE LA PRÉCONDITION - si la collection racine est introuvable ou est inaccessible.
* 500 - ERREUR DU SERVEUR INTERNE - si quelque chose d&#39;autre ne va pas.

## Copier un dossier ou une ressource {#copy-a-folder-or-asset}

Copie un dossier ou une ressource disponible à l’emplacement indiqué vers une nouvelle destination.

**En-têtes** de demande : Les paramètres sont les suivants :

* `X-Destination` - un nouvel URI de destination dans la portée de la solution d&#39;API pour copier la ressource.
* `X-Depth` - soit `infinity` soit `0`. L&#39;utilisation `0` de cette ressource copie uniquement la ressource et ses propriétés et non ses enfants.
* `X-Overwrite` - Utilisation `F` pour empêcher le remplacement d&#39;un fichier à la destination existante.

**Demande**: `COPY /api/assets/myFolder -H"X-Destination: /api/assets/myFolder-copy"`

**Codes** de réponse : Les codes de réponse sont les suivants :

* 201 - CRÉÉ - si le dossier/la ressource a été copié vers une destination non existante.
* 204 - AUCUN CONTENU - si le dossier/fichier a été copié vers une destination existante.
* 412 - ÉCHEC DE LA PRÉCONDITION - si un en-tête de requête est manquant.
* 500 - ERREUR DU SERVEUR INTERNE - si quelque chose d&#39;autre ne va pas.

## Déplacer un dossier ou une ressource {#move-a-folder-or-asset}

Déplace un dossier ou une ressource de l’emplacement indiqué vers une nouvelle destination.

**En-têtes de requête**: Les paramètres sont les suivants :

* `X-Destination` - un nouvel URI de destination dans la portée de la solution d&#39;API pour copier la ressource.
* `X-Depth` - soit `infinity` soit `0`. L&#39;utilisation `0` de cette ressource copie uniquement la ressource et ses propriétés et non ses enfants.
* `X-Overwrite` - Utiliser soit `T` pour forcer la suppression d&#39;une ressource existante, soit `F` pour empêcher le remplacement d&#39;une ressource existante.

**Demande**: `MOVE /api/assets/myFolder -H"X-Destination: /api/assets/myFolder-moved"`

**Codes** de réponse : Les codes de réponse sont les suivants :

* 201 - CRÉÉ - si le dossier/la ressource a été copié vers une destination non existante.
* 204 - AUCUN CONTENU - si le dossier/fichier a été copié vers une destination existante.
* 412 - ÉCHEC DE LA PRÉCONDITION - si un en-tête de requête est manquant.
* 500 - ERREUR DU SERVEUR INTERNE - si quelque chose d&#39;autre ne va pas.

## Supprimer un dossier, une ressource ou un rendu {#delete-a-folder-asset-or-rendition}

Supprime une ressource (-tree) au chemin d&#39;accès fourni.

**Demande**

* `DELETE /api/assets/myFolder`
* `DELETE /api/assets/myFolder/myAsset.png`
* `DELETE /api/assets/myFolder/myAsset.png/renditions/original`

**Codes** de réponse : Les codes de réponse sont les suivants :

* 200 - OK - si le dossier a été supprimé avec succès.
* 412 - ÉCHEC DE LA PRÉCONDITION - si la collection racine est introuvable ou est inaccessible.
* 500 - ERREUR DU SERVEUR INTERNE - si quelque chose d&#39;autre ne va pas.
