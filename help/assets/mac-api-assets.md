---
title: « API HTTP [!DNL Assets]. »
description: Créer, lire, mettre à jour, supprimer et gérer des ressources numériques à l’aide de l’API HTTP dans  [!DNL Adobe Experience Manager Assets].
contentOwner: AG
role: Developer
feature: APIs,Assets HTTP API,Developer Tools
exl-id: 6bc10f4e-a951-49ba-9c71-f568a7f2e40d
source-git-commit: 3d713021ac410ca2925a282c5dfca98ed4e483ee
workflow-type: tm+mt
source-wordcount: '1746'
ht-degree: 97%

---

# API HTTP [!DNL Assets] {#assets-http-api}

| Version | Lien de l’article |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Cliquez ici](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/admin/mac-api-assets.html?lang=fr) |
| AEM 6.5 | Cet article |

## Présentation {#overview}

L’API HTTP [!DNL Assets] permet d’effectuer des opérations CRUD (créer, lire, mettre à jour, supprimer) sur des ressources numériques, notamment les métadonnées, les rendus et les commentaires, ainsi que sur des contenus structurés grâce à des fragments de contenu [!DNL Experience Manager]. Elle est exposée sous `/api/assets` et est implémentée en tant qu’API REST. Elle comprend [Prise en charge des fragments de contenu](/help/assets/assets-api-content-fragments.md).

Pour accéder à l’API :

1. Ouvrez le document du service API à l’adresse `https://[hostname]:[port]/api.json`.
1. Suivez le lien du service [!DNL Assets] pointant vers `https://[hostname]:[server]/api/assets.json`.

La réponse de l’API est un fichier JSON pour certains types MIME et un code de réponse pour tous les types MIME. La réponse JSON est facultative et peut ne pas être disponible, par exemple pour les fichiers de PDF. Reposez sur le code de réponse pour une analyse ou des actions plus approfondies.

Après l’[!UICONTROL heure de désactivation], une ressource et ses rendus ne sont plus disponibles via l’interface web [!DNL Assets] ni par le biais de l’API HTTP. L’API renvoie un message d’erreur 404 si l’[!UICONTROL heure d’activation] se situe dans le futur ou si l’[!UICONTROL heure de désactivation] se situe dans le passé.

>[!CAUTION]
>
>[L’API HTTP met à jour les propriétés des métadonnées](#update-asset-metadata) dans l’espace de noms `jcr`. Toutefois, l’interface utilisateur d’Experience Manager met à jour les propriétés de métadonnées dans l’espace de noms `dc`.

## Fragments de contenu {#content-fragments}

Un [fragment de contenu](/help/assets/content-fragments/content-fragments.md) est un type de ressource spécial. Il permet d’accéder aux données structurées, telles que les textes, les nombres, les dates, etc. Comme il existe plusieurs différences de ressources `standard` (telles que les images ou les documents), certaines règles supplémentaires s’appliquent pour gérer les fragments de contenu.

Pour plus d’informations, voir [Prise en charge de fragments de contenu dans l’API HTTP Experience Manager Assets](/help/assets/assets-api-content-fragments.md).

## Modèle de données {#data-model}

L’API HTTP d’[!DNL Assets] présente deux éléments principaux : des dossiers et des ressources (pour les ressources standard).

Il expose également des éléments plus détaillés pour les modèles de données personnalisés décrivant le contenu structuré dans les fragments de contenu. Voir [Modèles de données de fragment de contenu](/help/assets/assets-api-content-fragments.md#content-fragments) pour plus d’informations.

### Dossiers {#folders}

Les dossiers sont comparables aux répertoires des systèmes de fichiers traditionnels. Il s’agit de conteneurs pour d’autres dossiers ou assertions. Les dossiers se composent des éléments suivants :

**Entités** : les entités d’un dossier sont ses éléments enfants qui peuvent, à leur tour, être des dossiers et des ressources.

**Propriétés** :

* `name` est le nom du dossier. Il est identique au dernier segment du chemin d’URL, sans l’extension.
* `title` est un titre facultatif du dossier pouvant être affiché au lieu de son nom.

>[!NOTE]
>
>Certaines propriétés de dossier ou de ressource sont associées à un préfixe différent. Le préfixe `jcr` de `jcr:title`, `jcr:description` et `jcr:language` est remplacé par le préfixe `dc`. Par conséquent, dans le JSON renvoyé, `dc:title` et `dc:description` contiennent respectivement les valeurs de `jcr:title` et `jcr:description`.

Les dossiers **Liens** présentent trois liens :

* `self` : lien vers lui-même.
* `parent` : lien vers le dossier parent.
* `thumbnail` : (facultatif) lien vers une miniature de dossier.

### Assets {#assets}

Dans Experience Manager, une ressource contient les éléments suivants :

* Propriétés et métadonnées de la ressource.
* Plusieurs rendus tels que le rendu d’origine (qui est la ressource chargée initialement), une miniature et divers autres rendus. Les rendus supplémentaires peuvent être des images de tailles différentes, différents codages vidéo ou des pages extraites de fichiers PDF ou [!DNL Adobe InDesign].
* Commentaires facultatifs.

Pour plus d’informations sur les éléments des fragments de contenu, voir [Prise en charge de fragments de contenu dans l’API HTTP Experience Manager Assets](/help/assets/assets-api-content-fragments.md#content-fragments).

Dans [!DNL Experience Manager], un dossier comprend les composants suivants :

* Entités : les enfants des ressources sont ses rendus.
* Propriétés.
* Liens.

L’API HTTP d’[!DNL Assets] offre les fonctionnalités suivantes :

* [Récupérer une liste de dossiers](#retrieve-a-folder-listing)
* [Créer un dossier](#create-a-folder)
* [Créer une ressource](#create-an-asset)
* [Mettre à jour le fichier binaire d’une ressource](#update-asset-binary)
* [Mettre à jour les métadonnées d’une ressource](#update-asset-metadata)
* [Créer un rendu de ressource](#create-an-asset-rendition)
* [Mettre à jour un rendu de ressource](#update-an-asset-rendition)
* [Créer un commentaire de ressource](#create-an-asset-comment)
* [Copier un dossier ou une ressource](#copy-a-folder-or-asset)
* [Déplacer un dossier ou une ressource](#move-a-folder-or-asset)
* [Supprimer un dossier, une ressource ou un rendu](#delete-a-folder-asset-or-rendition)

>[!NOTE]
>
>Pour faciliter la lecture, la notation cURL complète n’est pas utilisée dans les exemples suivants. En fait, la notation est liée à [Resty](https://github.com/micha/resty) qui est un wrapper de script pour `cURL`.

**Conditions préalables**

* Accédez à l’adresse `https://[aem_server]:[port]/system/console/configMgr`.
* Accédez au **[!UICONTROL Filtre CSRF Adobe Granite]**.
* Assurez-vous que la propriété **[!UICONTROL Méthodes de filtrage]** inclut : `POST`, `PUT`, `DELETE`.

## Récupérer une liste de dossiers {#retrieve-a-folder-listing}

Récupère une représentation Siren d’un dossier existant et de ses entités enfants (sous-dossiers ou ressources).

**Requête** : `GET /api/assets/myFolder.json`

**Codes de réponse** : les codes de réponse sont les suivants :

* 200 – OK – succès.
* 404 – INTROUVABLE – le dossier n’existe pas ou n’est pas accessible.
* 500 – ERREUR INTERNE DU SERVEUR – si une autre erreur s’est produite.

**Réponse** : la classe de l’entité renvoyée est une ressource ou un dossier. Les propriétés des entités contenues représentent un sous-ensemble du jeu complet des propriétés de chaque entité. Pour obtenir une représentation complète de l’entité, les clients doivent récupérer le contenu de l’URL vers laquelle pointe le lien avec l’élément `rel` `self`.

## Créer un dossier {#create-a-folder}

Crée un dossier `sling` : `OrderedFolder` à l’emplacement indiqué. Si un astérisque (`*`) est indiqué au lieu d’un nom de nœud, le servlet utilisera le nom du paramètre comme nom de nœud. Cela est accepté dans la mesure où les données de la requête consistent en une représentation Siren du nouveau dossier ou un ensemble de paires nom-valeur, codé sous la forme `application/www-form-urlencoded` ou `multipart`/ `form`- `data`, ce qui se révèle utile pour créer directement un dossier à partir d’un formulaire HTML. Les propriétés du dossier peuvent, en outre, être spécifiées en tant que paramètres de requête URL.

Un appel d’API échoue avec un code de réponse `500` si le nœud parent du chemin d’accès fourni n’existe pas. Un appel renvoie un code de réponse `409` si le dossier existe déjà.

**Paramètres** : `name` est le nom du dossier.

**Requête**

* `POST /api/assets/myFolder -H"Content-Type: application/json" -d '{"class":"assetFolder","properties":{"jcr:title":"My Folder"}}'`
* `POST /api/assets/* -F"name=myfolder" -F"jcr:title=My Folder"`

**Codes de réponse** : les codes de réponse sont les suivants :

* 201 – CRÉÉ – en cas de réussite de la création.
* 409 – CONFLIT – si un dossier existe déjà.
* 412 – ÉCHEC DE LA PRÉCONDITION – si la collection racine est introuvable ou inaccessible.
* 500 – ERREUR INTERNE DU SERVEUR – si une autre erreur s’est produite.

## Créer une ressource  {#create-an-asset}

Placez le fichier fourni à l’emplacement indiqué pour créer une ressource dans le référentiel de gestion des ressources numériques. Si un astérisque `*` est indiqué au lieu d’un nom de nœud, le servlet utilise le nom du paramètre ou du fichier comme nom de nœud.

**Paramètres** : les paramètres sont `name` pour le nom de la ressource et `file` pour la référence au fichier.

**Requête**

* `POST /api/assets/myFolder/myAsset.png -H"Content-Type: image/png" --data-binary "@myPicture.png"`
* `POST /api/assets/myFolder/* -F"name=myAsset.png" -F"file=@myPicture.png"`

**Codes de réponse** : les codes de réponse sont les suivants :

* 201 – CRÉÉ – Si la ressource a été créée avec succès.
* 409 – CONFLIT – Si une ressource existe déjà.
* 412 – ÉCHEC DE LA PRÉCONDITION – si la collection racine est introuvable ou inaccessible.
* 500 – ERREUR INTERNE DU SERVEUR – si une autre erreur s’est produite.

## Mettre à jour un fichier binaire de ressource {#update-asset-binary}

Met à jour un fichier binaire de ressource (rendu avec le nom d’origine). La mise à jour déclenche l’exécution du workflow de traitement des ressources par défaut, s’il est configuré.

**Requête** : `PUT /api/assets/myfolder/myAsset.png -H"Content-Type: image/png" --data-binary @myPicture.png`

**Codes de réponse** : les codes de réponse sont les suivants :

* 200 – OK – si la ressource a été mise à jour avec succès.
* 404 – INTROUVABLE – si la ressource n’a pas été trouvée ou est inaccessible à l’aide de l’URI fourni.
* 412 – ÉCHEC DE LA PRÉCONDITION – si la collection racine est introuvable ou inaccessible.
* 500 – ERREUR INTERNE DU SERVEUR – si une autre erreur s’est produite.

## Mettre à jour les métadonnées d’une ressource {#update-asset-metadata}

Met à jour les propriétés de métadonnées d’une ressource. Si vous mettez à jour une propriété du namespace `dc:`, l’API met à jour cette même propriété dans le namespace `jcr`. L’API ne synchronise pas les propriétés des deux namespaces.

**Requête** : `PUT /api/assets/myfolder/myAsset.png -H"Content-Type: application/json" -d '{"class":"asset", "properties":{"jcr:title":"My Asset"}}'`

**Codes de réponse** : les codes de réponse sont les suivants :

* 200 – OK – si la ressource a été mise à jour avec succès.
* 404 – INTROUVABLE – si la ressource n’a pas été trouvée ou est inaccessible à l’aide de l’URI fourni.
* 412 – ÉCHEC DE LA PRÉCONDITION – si la collection racine est introuvable ou inaccessible.
* 500 – ERREUR INTERNE DU SERVEUR – si une autre erreur s’est produite.

### Mise à jour des métadonnées de synchronisation entre l’espace de noms `dc` et `jcr` {#sync-metadata-between-namespaces}

La méthode API met à jour les propriétés de métadonnées dans l’espace de noms `jcr`. Les mises à jour effectuées à l’aide de l’interface utilisateur modifient les propriétés de métadonnées dans l’espace de noms `dc`. Pour synchroniser les valeurs des métadonnées entre l’espace de noms `dc` et `jcr`, vous pouvez créer un workflow et configurer Experience Manager pour exécuter le workflow lors de la modification des ressources. Utilisez un script ECMA pour synchroniser les propriétés de métadonnées requises. L’exemple de script suivant synchronise la chaîne de titre entre `dc:title` et `jcr:title`.

```javascript
var workflowData = workItem.getWorkflowData();
if (workflowData.getPayloadType() == "JCR_PATH")
{
 var path = workflowData.getPayload().toString();
 var node = workflowSession.getSession().getItem(path);
 var metadataNode = node.getNode("jcr:content/metadata");
 var jcrcontentNode = node.getNode("jcr:content");
if (jcrcontentNode.hasProperty("jcr:title"))
{
 var jcrTitle = jcrcontentNode.getProperty("jcr:title");
 metadataNode.setProperty("dc:title", jcrTitle.toString());
 metadataNode.save();
}
}
```

## Créer un rendu de ressource {#create-an-asset-rendition}

Créer un rendu pour une ressource. Si le nom de paramètre de requête n’est pas fourni, le nom de fichier est utilisé comme nom du rendu.

**Paramètres** : les paramètres sont `name` pour le nom du rendu et `file` pour la référence au fichier.

**Requête**

* `POST /api/assets/myfolder/myasset.png/renditions/web-rendition -H"Content-Type: image/png" --data-binary "@myRendition.png"`
* `POST /api/assets/myfolder/myasset.png/renditions/* -F"name=web-rendition" -F"file=@myRendition.png"`

**Codes de réponse** : les codes de réponse sont les suivants :

* 201 – CRÉÉ – si le rendu a été créé avec succès.
* 404 – INTROUVABLE – si la ressource n’a pas été trouvée ou est inaccessible à l’aide de l’URI fourni.
* 412 – ÉCHEC DE LA PRÉCONDITION – si la collection racine est introuvable ou inaccessible.
* 500 – ERREUR INTERNE DU SERVEUR – si une autre erreur s’est produite.

## Mettre à jour un rendu de ressource {#update-an-asset-rendition}

Met à jour et remplace le rendu d’une ressource par les nouvelles données binaires.

**Requête** : `PUT /api/assets/myfolder/myasset.png/renditions/myRendition.png -H"Content-Type: image/png" --data-binary @myRendition.png`

**Codes de réponse** : les codes de réponse sont les suivants :

* 200 – OK – si le rendu a été mis à jour avec succès.
* 404 – INTROUVABLE – si la ressource n’a pas été trouvée ou est inaccessible à l’aide de l’URI fourni.
* 412 – ÉCHEC DE LA PRÉCONDITION – si la collection racine est introuvable ou inaccessible.
* 500 – ERREUR INTERNE DU SERVEUR – si une autre erreur s’est produite.

## Ajouter un commentaire pour une ressource {#create-an-asset-comment}

Crée un commentaire de ressource.

**Paramètres** : les paramètres sont `message` pour le corps de message du commentaire et `annotationData` pour les données d’annotation au format JSON.

**Requête** : `POST /api/assets/myfolder/myasset.png/comments/* -F"message=Hello World." -F"annotationData={}"`

**Codes de réponse** : les codes de réponse sont les suivants :

* 201 – CRÉÉ – si le commentaire a été créé avec succès.
* 404 – INTROUVABLE – si la ressource n’a pas été trouvée ou est inaccessible à l’aide de l’URI fourni.
* 412 – ÉCHEC DE LA PRÉCONDITION – si la collection racine est introuvable ou inaccessible.
* 500 – ERREUR INTERNE DU SERVEUR – si une autre erreur s’est produite.

## Copier un dossier ou une ressource {#copy-a-folder-or-asset}

Copie un fichier ou une ressource disponible à l’emplacement indiqué vers une nouvelle destination.

**En-têtes de la requête** : les paramètres sont les suivants :

* `X-Destination` – un nouvel URI de destination appartenant à la portée de la solution d’API pour copier la ressource.
* `X-Depth` – `infinity` ou `0`. L’utilisation du code `0` entraîne la copie exclusive de la ressource et de ses propriétés, mais pas de ses enfants.
* `X-Overwrite` – utilisez le code `F` pour éviter le remplacement d’une ressource à la destination existante.

**Requête** : `COPY /api/assets/myFolder -H"X-Destination: /api/assets/myFolder-copy"`

**Codes de réponse** : les codes de réponse sont les suivants :

* 201 – CRÉÉ – si le dossier ou la ressource a été copié vers une destination inexistante.
* 204 – AUCUN CONTENU – si le dossier ou la ressource a été copié vers une destination existante.
* 412 – ÉCHEC DE LA PRÉCONDITION – s’il manque un en-tête de requête.
* 500 – ERREUR INTERNE DU SERVEUR – si une autre erreur s’est produite.

## Déplacer un dossier ou une ressource {#move-a-folder-or-asset}

Déplace un dossier ou une ressource de l’emplacement indiqué vers une nouvelle destination.

**En-têtes de la requête** : les paramètres sont les suivants :

* `X-Destination` – un nouvel URI de destination appartenant à la portée de la solution d’API pour copier la ressource.
* `X-Depth` – `infinity` ou `0`. L’utilisation du code `0` entraîne la copie exclusive de la ressource et de ses propriétés, mais pas de ses enfants.
* `X-Overwrite` – Utiliser soit `T` pour forcer la suppression d’une ressource existante, soit `F` pour éviter le remplacement d’une ressource existante.

**Requête** : `MOVE /api/assets/myFolder -H"X-Destination: /api/assets/myFolder-moved"`

N’utilisez pas `/content/dam` dans l’URL. Voici un exemple de commande permettant de déplacer des ressources et de remplacer des ressources existantes :

```shell
curl -u admin:admin -X MOVE https://[aem_server]:[port]/api/assets/source/file.png -H "X-Destination: https://[aem_server]:[port]/api/assets/destination/file.png" -H "X-Overwrite: T"
```

**Codes de réponse** : les codes de réponse sont les suivants :

* 201 – CRÉÉ – si le dossier ou la ressource a été copié vers une destination inexistante.
* 204 – AUCUN CONTENU – si le dossier ou la ressource a été copié vers une destination existante.
* 412 – ÉCHEC DE LA PRÉCONDITION – s’il manque un en-tête de requête.
* 500 – ERREUR INTERNE DU SERVEUR – si une autre erreur s’est produite.

## Supprimer un dossier, une ressource ou un rendu {#delete-a-folder-asset-or-rendition}

Supprime une ressource (arborescence) pour le chemin indiqué.

**Requête**

* `DELETE /api/assets/myFolder`
* `DELETE /api/assets/myFolder/myAsset.png`
* `DELETE /api/assets/myFolder/myAsset.png/renditions/original`

**Codes de réponse** : les codes de réponse sont les suivants :

* 200 – OK – si le dossier a été supprimé avec succès.
* 412 – ÉCHEC DE LA PRÉCONDITION – si la collection racine est introuvable ou inaccessible.
* 500 – ERREUR INTERNE DU SERVEUR – si une autre erreur s’est produite.

## Conseils et restrictions {#tips-best-practices-limitations}

* [L’API HTTP met à jour les propriétés des métadonnées](#update-asset-metadata) dans l’espace de noms `jcr`. Toutefois, l’interface utilisateur d’Experience Manager met à jour les propriétés de métadonnées dans l’espace de noms `dc`.

* L’API HTTP Assets ne renvoie pas les métadonnées complètes. Les espaces de noms sont codés en dur et seuls ces espaces de noms sont renvoyés. Pour obtenir des métadonnées complètes, consultez le chemin d’accès à la ressource `/jcr_content/metadata.json`.
