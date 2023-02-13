---
title: Configurer les magasins de nœuds et les entrepôts de données dans AEM 6
description: Découvrez comment configurer les magasins de nœuds et les entrepôts de données. Apprenez également à exécuter le nettoyage de la mémoire d’entrepôt de données.
content-type: reference
topic-tags: deploying
docset: aem65
feature: Configuring
exl-id: c1c90d6a-ee5a-487d-9a8a-741b407c8c06
source-git-commit: 461424de9158e14e251037004ea3590ed35bb4a0
workflow-type: tm+mt
source-wordcount: '3584'
ht-degree: 99%

---

# Configurer les magasins de nœuds et les entrepôts de données dans AEM 6{#configuring-node-stores-and-data-stores-in-aem}

## Présentation {#introduction}

Dans Adobe Experience Manager (AEM), les données binaires peuvent être stockées indépendamment des nœuds de contenu. Les données binaires sont stockées dans un entrepôt de données alors que les nœuds de contenu sont stockés dans un magasin de nœuds.

Les entrepôts de données et les magasins de nœuds peuvent être configués en utilisant la configuration OSGi. Chaque configuration OSGi est référencé à l’aide d’un PID (identifiant de persistant).

## Étapes de configuration {#configuration-steps}

Pour configurer le magasin de nœuds et l’entrepôt de données, procédez comme suit :

1. Copiez le fichier JAR quickstart AEM dans son répertoire d’installation.
1. Créez un dossier `crx-quickstart/install` dans le répertoire d’installation.
1. Configurez tout d’abord le magasin de nœuds en créant un fichier de configuration avec le nom de l’option de magasin de nœuds que vous voulez utiliser dans le répertoire `crx-quickstart/install`.

   Par exemple, le magasin de nœuds Document (qui constitue la base de l’implémentation de MongoMK d’AEM) utilise le fichier `org.apache.jackrabbit.oak.plugins.document.DocumentNodeStoreService.config`.

1. Modifiez le fichier et définissez vos options de configuration.
1. Créez un fichier de configuration avec le PID de l’entrepôt de données que vous souhaitez utiliser. Modifiez le fichier pour définir les options de configuration. 

   >[!NOTE]
   >
   >Consultez les [Configurations des magasins de nœuds](#node-store-configurations) et [Configurations des magasins de données](#data-store-configurations) pour les options de configuration.

1. Démarrez AEM.

## Configurations des magasins de nœuds {#node-store-configurations}

>[!CAUTION]
>
>Les versions plus récentes d’Oak utilisent de nouveaux format et schéma d’affectation de noms pour les fichiers de configuration OSGi. Le nouveau schéma d’affectation de noms requiert que le fichier de configuration soit nommé **.config**. Le nouveau format exige que les valeurs soient saisies et est [documenté ici](https://sling.apache.org/documentation/development/slingstart.html#default-configuration-format).
>
>Si vous effectuez une mise à niveau à partir d’une version plus ancienne d’Oak, veillez d’abord à sauvegarder le dossier `crx-quickstart/install`. Après la mise à niveau, restaurez les contenus du dossier à l’installation mise à niveau, puis modifiez l’extension des fichiers de configuration de **.cfg** en **.config**.
>
>Si vous lisez cet article en vue de vous préparer pour effectuer une mise à niveau à partir d’une installation d’**AEM 5.x**, n’oubliez pas de consulter la documentation de [mise à niveau](https://docs.adobe.com/content/docs/fr/aem/6-0/deploy/upgrade.html ) en premier.

### Magasins de nœuds de segment {#segment-node-store}

Le magasin de nœuds de segment constitue la base de l’implémentation de TarMK d’Adobe dans AEM 6. Il utilise le PID `org.apache.jackrabbit.oak.segment.SegmentNodeStoreService` pour la configuration.

>[!CAUTION]
>
>Le PID de la boutique de nœuds de segment a été remplacé par `org.apache.jackrabbit.oak.plugins.segment.SegmentNodeStoreService in previous versions` de AEM 6 à `org.apache.jackrabbit.oak.segment.SegmentNodeStoreService` dans AEM 6.3. Veillez à effectuer les ajustements de configuration nécessaires pour refléter cette modification.

Vous pouvez configurer les options suivantes :

* `repository.home` : chemin vers le répertoire racine du référentiel dans lequel sont stockées les données associées au référentiel. Par défaut, les fichiers de segment sont stockés dans le répertoire `crx-quickstart/segmentstore`. 

* `tarmk.size` : taille maximale d’un segment, en Mo. La valeur maximale par défaut étant de 256 Mo.
* `customBlobStore` : valeur booléenne indiquant qu’un magasin de données personnalisé est utilisé. La valeur par défaut est définie sur true pour AEM 6.3 et pour les versions ultérieures. Pour les versions antérieures à AEM 6.3, la valeur par défaut était false.

Voici un exemple de fichier `org.apache.jackrabbit.oak.segment.SegmentNodeStoreService.config` :

```shell
#Path to repo
repository.home="crx-quickstart/repository"

#Max segment size
tarmk.size=I"256"

#Custom data store
customBlobStore=B"true"
```

#### Magasin de nœuds de document {#document-node-store}

Le magasin de nœuds de document est la base de l’implémentation d’AEM MongoMK. Le * * PID `org.apache.jackrabbit.oak.plugins.document.DocumentNodeStoreService` est utilisé. Les options de configuration suivantes sont disponibles :

* `mongouri` : [MongoURI](https://docs.mongodb.org/manual/reference/connection-string/) requis pour se connecter à la base donnée Mongo. La valeur par défaut est de `mongodb://localhost:27017`.

* `db` : nom de la base de données Mongo. La valeur par défaut est **Oak**. ``. However, new AEM 6 installations use **aem-author** `` comme nom de la base de données par défaut.

* `cache` : taille du cache, en Mo. Elle est distribuée entre différents caches utilisés dans DocumentNodeStore. La valeur par défaut est `256`.

* `changesSize` : taille en Mo de la collection limitée utilisée dans Mongo pour la mise en cache de la sortie diff. La valeur par défaut est `256`.

* `customBlobStore` : valeur booléenne indiquant qu’un magasin de données personnalisé sera utilisé. La valeur par défaut est de `false`.

Voici un exemple de fichier `org.apache.jackrabbit.oak.plugins.document.DocumentNodeStoreService.config` :

```shell
#Mongo server details
mongouri="mongodb://localhost:27017"

#Name of Mongo database to use
db="aem-author"

#Store binaries in custom BlobStore
customBlobStore=B"false"
```

## Configurations des entrepôts de données {#data-store-configurations}

Lorsque vous traitez un grand nombre de fichiers binaires, il est recommandé d’utiliser un entrepôt de données externe au lieu du magasin de nœuds par défaut pour optimiser la performance.

Par exemple, si votre projet requiert un grand nombre de ressources multimédias, vous pouvez les stocker dans l’entrepôt de données de fichier ou S3 afin d’y accéder plus rapidement qu’en les stockant directement dans MongoDB.

L’entrepôt de données basé sur les fichiers offre de meilleures performances que MongoDB. De plus, les opérations de sauvegarde et de restauration Mongo sont plus lentes lorsque le nombre de ressources est élevé. 

Reportez-vous aux sections ci-dessous pour plus d’informations sur les différents entrepôts de données et les différentes configurations.

>[!NOTE]
>
>Pour activer les magasins de données personnalisés, vous devez vérifier que `customBlobStore` est défini sur `true` dans le fichier de configuration de magasin de nœuds respectif ([magasin de nœuds de segment](/help/sites-deploying/data-store-config.md#segment-node-store) ou [magasin de nœuds de document](/help/sites-deploying/data-store-config.md#document-node-store)).

### Fichier Magasin de données {#file-data-store}

Il s’agit de l’implémentation de [FileDataStore](https://jackrabbit.apache.org/api/trunk/org/apache/jackrabbit/core/data/FileDataStore.html) présent dans Jackrabbit 2, qui offre une méthode pour stocker les données binaires comme tout autre fichier sur le système de fichiers. Le PID `org.apache.jackrabbit.oak.plugins.blob.datastore.FileDataStore` est utilisé.

Voici les options de configuration disponibles :

* `repository.home` : chemin vers le répertoire racine du référentiel dans lequel sont stockées les différentes données associées au référentiel. Par défaut, les fichiers binaires sont stockés dans le répertoire `crx-quickstart/repository/datastore`.

* `path` : chemin d’accès au répertoire dans lequel les fichiers seront stockés. Si spécifié, la priorité est définie sur la valeur de `repository.home`.

* `minRecordLength` : taille minimale en octets d’un fichier stocké dans le magasin de données. Un contenu binaire inférieur à cette valeur est intégré.

>[!NOTE]
>
>Lorsque vous utilisez un NAS pour stocker les entrepôts de données basés sur les fichiers partagés, assurez-vous d’utiliser uniquement les appareils les plus performants afin d’éviter des problèmes de performances.

## Entrepôt de données Amazon S3 {#amazon-s-data-store}

AEM peut être configuré pour stocker des donnés dans le service Simple Storage Service (S3) d’Amazon. Celui-ci utilise le PID `org.apache.jackrabbit.oak.plugins.blob.datastore.S3DataStore.config` pour la configuration.

Pour activer la fonctionnalité du magasin de données S3, un pack de fonctionnalités contenant le connecteur du magasin de données S3 doit être téléchargé et installé. Accédez au [référentiel Adobe](https://repo1.maven.org/maven2/com/adobe/granite/com.adobe.granite.oak.s3connector/), puis téléchargez la dernière version des versions 1.10.x du pack de fonctionnalités (par exemple, com.adobe.granite.oak.s3connector-1.10.0.zip). En outre, vous devez également télécharger et installer le dernier pack de services AEM, comme indiqué à la page [Notes de mise à jour d’AEM 6.5](/help/release-notes/release-notes.md).

>[!NOTE]
>
>Lorsque vous utilisez AEM avec TarMK, les fichiers binaires sont stockés par défaut dans `FileDataStore`. Pour utiliser TarMK avec le magasin de données S3, vous devez lancer AEM à l’aide du mode d’exécution `crx3tar-nofds`, par exemple :

```shell
java -jar <aem-jar-file>.jar -r crx3tar-nofds
```

À la fin du téléchargement, vous pouvez installer et configurer le connecteur S3 comme suit :

1. Extrayez le contenu du fichier ZIP du pack de fonctionnalités dans un dossier temporaire.

1. Accédez au dossier temporaire et naviguez jusqu’à l’emplacement suivant :

   ```xml
   jcr_root/libs/system/install
   ```

   Copiez l’intégralité du contenu de l’emplacement ci-dessus vers `<aem-install>/crx-quickstart/install.`.

1. Si AEM est déjà configuré pour fonctionner avec le stockage Tar ou MongoDB, supprimez tous les fichiers de configuration existants du dossier ***&lt;aem-install>***/*crx-quickstart*/*install* avant de continuer. Les fichiers à supprimer sont les suivants :

   * `For MongoMK: org.apache.jackrabbit.oak.plugins.document.DocumentNodeStoreService.config`
   * `For TarMK: org.apache.jackrabbit.oak.segment.SegmentNodeStoreService.config`

1. Retournez à l’emplacement temporaire où le pack de fonctionnalités a été extrait, puis copiez le contenu du dossier suivant : 

   * `jcr_root/libs/system/config`

   vers

   * `<aem-install>/crx-quickstart/install`

   Veillez à copier uniquement les fichiers de configuration nécessaires pour votre configuration actuelle. Que ce soit pour une configuration de magasin de données partagé et dédié, copiez le fichier `org.apache.jackrabbit.oak.plugins.blob.datastore.S3DataStore.config`.

   >[!NOTE]
   >
   >Dans une configuration en cluster, effectuez les étapes ci-dessus sur tous les nœuds du cluster, l’un après l’autre. Veillez également à utiliser les mêmes configurations S3 pour tous les nœuds.

1. Modifiez le fichier, puis ajoutez les options de configuration requises par votre configuration.
1. Démarrez AEM.

## Mise à nouveau vers une nouvelle version du connecteur S3 1.10.x {#upgrading-to-a-new-version-of-the-s-connector}

Si vous devez effectuer une mise à niveau vers une nouvelle version du connecteur S3 1.10.x (par exemple, de la version 1.10.0 vers la version 1.10.4), procédez comme suit :

1. Désactivez l’instance AEM.

1. Accédez à `<aem-install>/crx-quickstart/install/15` dans le dossier d’installation d’AEM et effectuez une sauvegarde du contenu.
1. Après la sauvegarde, supprimez l’ancienne version du connecteur S3 et ses dépendances en supprimant tous les fichiers jar dans le dossier `<aem-install>/crx-quickstart/install/15`, par exemple :

   * **oak-blob-cloud-1.6.1.jar**
   * **aws-java-sdk-osgi-1.10.76.jar**

   >[!NOTE]
   >
   >Les noms de fichier présentés ci-dessus sont utilisés à titre d’illustration uniquement.

1. Téléchargez la dernière version du pack de fonctionnalités 1.10.x à partir du [référentiel Adobe](https://repo1.maven.org/maven2/com/adobe/granite/com.adobe.granite.oak.s3connector/).
1. Décompressez le contenu dans un dossier séparé, puis accédez à `jcr_root/libs/system/install/15`.
1. Copiez les fichiers jar dans le dossier d’installation AEM **&lt;aem-install>**/crx-quickstart/install/15.
1. Démarrez AEM et vérifiez les fonctionnalités du connecteur.

Vous pouvez utiliser le fichier de configuration avec les options présentées ci-dessous.

<!--
* accessKey: The AWS access key.
* secretKey: The AWS secret access key. **Note:** When the `accessKey` or `secretKey` is not specified then the [IAM role](https://docs.aws.amazon.com/sdk-for-java/v1/developer-guide/java-dg-roles.html) is used for authentication.
* s3Bucket: The bucket name.
* s3Region: The bucket region.
* path: The path of the data store. The default is **&lt;AEM install folder&gt;/repository/datastore**
* minRecordLength: The minimum size of an object that should be stored in the data store. The minimum/default is **16KB.**
* maxCachedBinarySize: Binaries with size less than or equal to this size will be stored in memory cache. The size is in bytes. The default is **17408 **(17 KB).
* cacheSize: The size of the cache. The value is specified in bytes. The default is **64GB**.
* secret: Only to be used if using binaryless replication for shared datastore setup.
* stagingSplitPercentage: The percentage of cache size configured to be used for staging asynchronous uploads. The default value is **10**.
* uploadThreads: The number of uploads threads that are used for asynchronous uploads. The default value is **10**.
* stagingPurgeInterval: The interval in seconds for purging finished uploads from the staging cache. The default value is **300** seconds (5 minutes).
* stagingRetryInterval: The retry interval in seconds for failed uploads. The default value is **600** seconds (10 minutes).
-->

### Options du fichier de configuration du connecteur S3 {#s3-connector-configuration-file-options}

>[!NOTE]
>
>Le connecteur S3 prend en charge l’authentification des utilisateurs IAM et celle des rôles IAM. Pour utiliser l’authentification des rôles IAM, omettez les valeurs `accessKey` et `secretKey` de votre fichier de configuration. Le connecteur S3 est alors défini par défaut sur le [rôle IAM](https://docs.aws.amazon.com/sdk-for-java/v1/developer-guide/java-dg-roles.html) affecté à l’instance.

| Clé | Description | Valeur par défaut | Requise |
| --- | --- | --- | --- |
| accessKey | Identifiant de clé d’accès de l’utilisateur IAM ayant accès au compartiment. |  | Oui, lorsque vous n’utilisez pas les rôles IAM. |
| secretKey | Clé d’accès secrète de l’utilisateur IAM ayant accès au compartiment. |  | Oui, lorsque vous n’utilisez pas les rôles IAM. |
| cacheSize | Taille (en octets) du cache local. | 64 Go | Nombre |
| connectionTimeout | Définissez la durée d’attente (en millisecondes) avant l’expiration lors de l’établissement initial d’une connexion. | 10 000 | Nombre |
| maxCachedBinarySize | Les fichiers binaires dont la taille est inférieure ou égale à cette valeur (en octets) seront stockés dans le cache de mémoire. | 17 408 (17 Ko) | Nombre |
| maxConnections | Définissez le nombre maximal de connexions HTTP ouvertes autorisées. | 50 | Nombre |
| maxErrorRetry | Définissez le nombre maximal de nouvelles tentatives pour les requêtes (pouvant être retentées) ayant échoué. | 3 | Nombre |
| minRecordLength | Taille minimale d’un objet (en octets) devant être enregistré dans l’entrepôt de données. | 16384 | Nombre |
| path | Chemin d’accès local de l’entrepôt de données AEM. | `crx-quickstart/repository/datastore` | Nombre |
| proxyHost | Définissez l’hôte proxy facultatif par lequel le client se connectera. |  | Nombre |
| proxyPort | Définissez le port proxy facultatif par lequel le client se connectera. |  | Nombre |
| s3Bucket | Nom du compartiment S3. |  | Oui |
| s3EndPoint | Point d’entrée de l’API REST S3. |  | Nombre |
| s3Region | Région où réside le compartiment. Consultez cette [page](https://docs.aws.amazon.com/general/latest/gr/s3.html) pour plus de détails. | Région dans laquelle l’instance AWS est en cours d’exécution. | Nombre |
| socketTimeout | Définissez la durée d’attente (en millisecondes) pour que les données soient transférées au cours d’une connexion ouverte établie avant que la connexion n’expire et ne soit coupée. | 50 000 | Nombre |
| stagingPurgeInterval | Intervalle (en secondes) pour purger les téléchargements terminés à partir du cache intermédiaire. | 300 | Nombre |
| stagingRetryInterval | Intervalle (en secondes) entre deux tentatives de téléchargement ayant échoué. | 600 | Nombre |
| stagingSplitPercentage | Pourcentage de `cacheSize` à utiliser pour l’évaluation des téléchargements asynchrones. | 10 | Nombre |
| uploadThreads | Nombre de threads de téléchargement utilisés pour les téléchargements asynchrones. | 10 | Nombre |
| writeThreads | Nombre de threads simultanés utilisés pour l’écriture via S3 Transfer Manager. | 10 | Nombre |

<!---
### Bucket region options {#bucket-region-options}

<table>
 <tbody>
  <tr>
   <td>US Standard</td>
   <td><code>us-standard</code></td>
  </tr>
  <tr>
   <td>US West</td>
   <td><code>us-west-2</code></td>
  </tr>
  <tr>
   <td>US West (Northern California)</td>
   <td><code>us-west-1</code></td>
  </tr>
  <tr>
   <td>EU (Ireland)<br /> </td>
   <td><code>EU</code></td>
  </tr>
  <tr>
   <td>Asia Pacific (Singapore)<br /> </td>
   <td><code>ap-southeast-1</code></td>
  </tr>
  <tr>
   <td>Asia Pacific (Sydney)<br /> </td>
   <td><code>ap-southeast-2</code></td>
  </tr>
  <tr>
   <td>Asia Pacific (Tokyo)</td>
   <td><code>ap-northeast-1</code></td>
  </tr>
  <tr>
   <td>South America (Sao Paolo)<br /> </td>
   <td><code>sa-east-1</code></td>
  </tr>
 </tbody>
</table>
-->

### Mise en cache du magasin de données {#data-store-caching}

>[!NOTE]
>
>Les implémentations de `S3DataStore`, du magasin de données `CachingFileDataStore` et d’`AzureDataStore` prennent en charge la mise en cache du système de fichiers local. L’implémentation du `CachingFileDataStore` est utile lorsque le magasin de données est sur le système NFS (Network File System).

Lors de la mise à niveau à partir d’une ancienne implémentation de mise en cache (pré-oak 1.6), il existe une différence dans la structure du répertoire de cache du système de fichiers local. Dans l’ancienne structure de cache, les fichiers téléchargés et chargés étaient placés directement dans le chemin du cache. La nouvelle structure permet d’isoler les chargements des téléchargements afin de les stocker dans deux répertoires nommés `upload` et `download` dans le chemin du cache. Le processus de mise à niveau doit être transparent et tout chargement en attente doit être planifié. De plus, les fichiers précédemment chargés dans le cache seront placés dans le cache lors de l’initialisation.

Il est également possible de mettre le cache à niveau hors ligne à l’aide de la commande oak-run `datastorecacheupgrade`. Pour plus d’informations sur l’exécution de la commande, consultez le fichier [lisez-moi](https://svn.apache.org/repos/asf/jackrabbit/oak/trunk/oak-run/README.md ) du module oak-run.

Le cache est soumis à une limite de taille qui peut être configurée à l’aide du paramètre cacheSize.

#### Téléchargements {#downloads}

Le cache local sera vérifié pour l’enregistrement du fichier/blob demandé avant de pouvoir y accéder à partir du magasin de données. Lorsque la taille du cache dépasse la limite configurée (voir le paramètre `cacheSize`) lors de l’ajout d’un fichier, certains des fichiers seront évincés pour récupérer de l’espace.

#### Téléchargement asynchrone {#async-upload}

Le cache prend en charge les téléchargements asynchrones vers le DataStore. Les fichiers sont placés localement, dans le cache (sur le système de fichiers) et une tâche asynchrone commence à les télécharger. Le nombre de téléchargements asynchrones est limité par la taille du cache intermédiaire. La taille du cache intermédiaire est configurée à l’aide du paramètre `stagingSplitPercentage`. Ce paramètre définit le pourcentage de taille de cache à utiliser pour le cache intermédiaire. En outre, le pourcentage de cache disponible pour les téléchargements est calculé comme suit : **(100 - `stagingSplitPercentage`) &#42;`cacheSize`**.

Les chargements asynchrones sont multithread et le nombre de thread est configuré à l’aide du paramètre `uploadThreads`.

Les fichiers sont déplacés vers le cache principal de téléchargement une fois les téléchargements effectués. Lorsque la taille du cache intermédiaire dépasse sa limite, les fichiers sont téléchargés de manière synchrone vers le DataStore jusqu’à ce que les téléchargements asynchrones précédents soient terminés et que de l’espace soit à nouveau disponible dans le cache intermédiaire. Les fichiers chargés sont supprimés de la zone de transit par une tâche périodique dont l’intervalle est configuré par le paramètre `stagingPurgeInterval`.

Les chargements ayant échoué (en raison d’une interruption du réseau, par exemple) sont placés dans une file d’attente pour effectuer régulièrement de nouvelles tentatives. L’intervalle de nouvelle tentative est configuré à l’aide du `stagingRetryInterval parameter`.

#### Configuration d’une réplication sans binaire avec Amazon S3 {#configuring-binaryless-replication-with-amazon-s}

Pour configurer une réplication sans binaire avec S3, les étapes suivantes sont nécessaires :

1. Installez les instances de création et de publication, puis vérifiez qu’elles démarrent correctement.
1. Accédez aux paramètres de l’agent de réplication, en ouvrant une page sur *https://localhost:4502/etc/replication/agents.author/publish.html*.
1. Appuyez sur le bouton **Modifier** dans la section **Paramètres**.
1. Modifiez l’option **Type de sérialisation** en **Sans fichier binaire**. 

1. Ajoutez le paramètre « `true`=`binaryless` » dans l’URI de transport. Après la modification, l’URI doit ressembler à ce qui suit :

   *https://localhost:4503/bin/receive?sling:authRequestLogin=1&amp;binaryless=true*

1. Redémarrez toutes les instances de création et de publication pour que les modifications soient appliquées.

#### Création d’un cluster à l’aide de S3 et MongoDB {#creating-a-cluster-using-s-and-mongodb}

1. Décompressez le quickstart CQ en utilisant la commande suivante :

   `java -jar cq-quickstart.jar -unpack`

1. Après la décompression d’AEM, créez un dossier à l’intérieur du répertoire d’installation *crx-quickstart*/*install*.

1. Créez ces deux fichiers à l’intérieur du dossier `crx-quickstart` :

   * *org.apache.jackrabbit.oak.plugins.document.DocumentNodeStoreService.* *config*

   * *org.apache.jackrabbit.oak.plugins.blob.datastore.S3DataStore*.*config*

   Une fois que ces fichiers ont été créés, ajoutez les options de configuration selon vos besoins.

1. Installez les deux lots requis pour l’entrepôt de données S3, comme expliqué plus haut.
1. Vérifiez que MongoDB est installé et qu’une instance de `mongod` est en cours d’exécution.
1. Démarrez AEM à l’aide de la commande suivante :

   `java -Xmx1024m -jar cq-quickstart.jar -r crx3,crx3mongo`

1. Répétez les étapes 1 à 4 pour la seconde instance d’AEM.
1. Démarrez la seconde instance d’AEM.

#### Configuration d’un entrepôt de données partagé  {#configuring-a-shared-data-store}

1. Créez d’abord le fichier de configuration d’entrepôt de données sur chaque instance devant partager l’entrepôt de données :

   * Si vous utilisez `FileDataStore`, créez un fichier nommé `org.apache.jackrabbit.oak.plugins.blob.datastore.FileDataStore.config`, puis placez-le dans le dossier `<aem-install>/crx-quickstart/install`.

   * Si vous utilisez S3 comme magasin de données, créez un fichier nommé `rg.apache.jackrabbit.oak.plugins.blob.datastore.S3DataStore.config` dans le dossier `<aem-install>/crx-quickstart/install`, comme ci-dessus.

1. Modifiez les fichiers de donfiguration d’entrepôt de données sur chaque instance pour qu’ils pointent vers le même entrepôt de données. Pour en savoir plus, voir [cet article](/help/sites-deploying/data-store-config.md#data-store-configurations).
1. Si l’instance a été clonée à partir d’un serveur existant, vous devez supprimer le `clusterId` de la nouvelle instance à l’aide du dernier outil oak-run lorsque le référentiel est hors ligne. La commande que vous devez exécuter est la suivante :

   ```xml
   java -jar oak-run.jar resetclusterid < repository path | Mongo URI >
   ```

   >[!NOTE]
   >
   >Si un magasin de nœuds de segment est configuré, le chemin du référentiel doit être spécifié. Par défaut, le chemin est `<aem-install-folder>/crx-quickstart/repository/segmentstore.` Si un magasin de nœuds de document est configuré, vous pouvez utiliser une [URI de chaîne de connexion Mongo](https://docs.mongodb.org/manual/reference/connection-string/).

   >[!NOTE]
   >
   >L’outil Oak-run peut être téléchargé à partir de cet emplacement :
   >
   >
   >[https://mvnrepository.com/artifact/org.apache.jackrabbit/oak-run/](https://mvnrepository.com/artifact/org.apache.jackrabbit/oak-run/)
   >
   >
   >Différentes versions de l’outil doivent être utilisées selon la version d’Oak utilisée avec l’installation AEM. Vérifiez les exigences de version énumérés ci-dessous avant d’utiliser l’outil :
   >
   >
   >
   >    * Pour les versions **1.2.x** d’Oak, utilisez Oak-run **1.2.12 ou une version ultérieure**.
   >    * Pour des versions d’Oak **plus récentes que celle ci-dessus**, utilisez la version d’Oak-run qui correspond au système Oak de votre installation AEM.


1. Enfin, validez la configuration. Pour cela, vous devez rechercher un fichier unique ajouté à l’entrepôt de données par chaque référentiel le partageant. Le format des fichiers est `repository-[UUID]`, où l’UUID est l’identifiant unique de chaque référentiel.

   Une configuration correcte devrait être donc dotée d’autant de fichiers uniques que de référentiels partageant l’entrepôt de données.

   Les fichiers sont stockés différemment, selon l’entrepôt de données :

   * Pour le `FileDataStore`, les fichiers sont créés sous le chemin racine du dossier du magasin de données.
   * Pour `S3DataStore`, les fichiers sont créés dans le compartiment S3 configuré sous le dossier `META`.

## Entrepôt de données Azure  {#azure-data-store}

AEM peut être configuré pour stocker des donnés dans le service de stockage Azure de Microsoft. Celui-ci utilise le PID `org.apache.jackrabbit.oak.plugins.blob.datastore.AzureDataStore.config` pour la configuration.

Pour activer la fonctionnalité du magasin de données Azure, un Pack de fonctionnalités contenant le connecteur Azure doit être téléchargé et installé. Accédez au [référentiel Adobe](https://repo1.maven.org/maven2/com/adobe/granite/com.adobe.granite.oak.azureblobconnector/), puis téléchargez la dernière version des versions 1.6.x du pack de fonctionnalités (par exemple, com.adobe.granite.oak.azureblobconnector-1.6.3.zip).

>[!NOTE]
>
>Lorsque vous utilisez AEM avec TarMK, les fichiers binaires sont stockés par défaut dans FileDataStore. Pour utiliser TarMK avec le magasin de données Azure, vous devez démarrer AEM à l’aide du mode d’exécution `crx3tar-nofds`, par exemple :

```shell
java -jar <aem-jar-file>.jar -r crx3tar-nofds
```

Une fois téléchargé, vous pouvez installer et configurer le connecteur Azure comme suit :

1. Extrayez le contenu du fichier zip du pack de fonctionnalités dans un dossier temporaire.

1. Accédez au dossier temporaire et copiez le contenu de `jcr_root/libs/system/install` vers le dossier `<aem-install>crx-quickstart/install`.
1. Si AEM est déjà configuré pour fonctionner avec le stockage Tar ou MongoDB, supprimez tous les fichiers de configuration existants du dossier `/crx-quickstart/install` avant de continuer. Les fichiers à supprimer sont les suivants : 

   Pour MongoMK :

   `org.apache.jackrabbit.oak.plugins.document.DocumentNodeStoreService.config`

   Pour TarMK :

   `org.apache.jackrabbit.oak.segment.SegmentNodeStoreService.config`

1. Retournez à l’emplacement temporaire où a été extrait le pack de fonctionnalités, puis copiez le contenu de `jcr_root/libs/system/config` vers le dossier `<aem-install>/crx-quickstart/install`.
1. Modifiez le fichier de configuration et ajoutez les options de configuration requises par votre configuration.
1. Démarrez AEM.

Vous pouvez utiliser le fichier de configuration avec les options suivantes :

* azureSas=&quot;&quot; : dans la version 1.6.3 du connecteur, la signature d’accès partagé Azure (SAS) est pris en charge. **Si les informations d’identification SAS et de stockage figurent dans le fichier de configuration, SAS a la priorité.** Pour plus d’informations sur SAS, consultez la [documentation officielle](https://docs.microsoft.com/fr-fr/azure/storage/common/storage-dotnet-shared-access-signature-part-1 ). Assurez-vous que le caractère ’=’ est placé dans une séquence d’échappement telle que ’\=’.

* azureBlobEndpoint=&quot;&quot; : point d’entrée Blob Azure. Par exemple, https://&lt;storage-account>.blob.core.windows.net.
* accessKey=&quot;&quot; : nom du compte de stockage. Pour plus d’informations sur les informations d’identification de l’authentification Microsoft Azure, reportez-vous à la [documentation officielle](https://azure.microsoft.com/fr-fr/documentation/articles/storage-create-storage-account). 

* secretKey=&quot;&quot; : clé d’accès au stockage. Assurez-vous que le caractère ’=’ est placé dans une séquence d’échappement telle que ’\=’.
* container=&quot;&quot; : nom du conteneur de stockage blob Microsoft Azure. Le conteneur est le regroupement d’un ensemble de blobs. Pour plus de détails, consultez[ la documentation officielle](https://msdn.microsoft.com/en-us/library/dd135715.aspx). 
* maxConnections=&quot;&quot; : nombre de demandes simultanées par opération. La valeur par défaut est 1.
* maxErrorRetry=&quot;&quot; : nombre de nouvelles tentatives par demande. La valeur par défaut est 3.
* socketTimeout=&quot;&quot; : intervalle d’expiration, en millisecondes, utilisé pour la demande. la valeur par défaut est de 5 minutes.

En plus des paramètres ci-dessus, les paramètres suivants peuvent également être configurés :

* path : chemin d’accès du magasin de données. La valeur par défaut est `<aem-install>/repository/datastore.`.
* RecordLength : taille minimale d’un objet devant être enregistré dans le magasin de données. La valeur par défaut est de 16 Ko. 
* maxCachedBinarySize : les binaires dont la taille est inférieure ou égale à cette taille seront stockés dans le cache de la mémoire. La taille est exprimée en octets. La valeur par défaut est de 17408 (17 ko).
* cacheSize : taille du cache. La valeur est exprimée en octets. La valeur par défaut est 64 Go.
* secret : à utiliser uniquement si la réplication sans binaire est utilisée pour la configuration du magasin de données partagé.
* stagingSplitPercentage : pourcentage de la taille du cache configuré afin d’être utilisé pour les chargements asynchrones intermédiaires. La valeur par défaut est 10.
* uploadThreads : nombre de threads de chargement utilisés pour les chargements asynchrones. La valeur par défaut est 10.
* stagingPurgeInterval : intervalle en secondes pour purger les chargements terminés à partir du cache intermédiaire. La valeur par défaut est 300 secondes (5 minutes).
* stagingRetryInterval : intervalle en secondes entre les nouvelles tentatives pour les chargements ayant échoué. La valeur par défaut est de 600 secondes (10 minutes).

>[!NOTE]
>
>Tous les paramètres doivent être mis entre guillemets, par exemple :

```shell
accessKey="ASDASDERFAERAER"
secretKey="28932hfjlkwdo8fufsdfas\=\="
```

## Nettoyage de la mémoire du magasin de données  {#data-store-garbage-collection}

Le processus de nettoyage de la mémoire du magasin de données est utilisé pour supprimer tous les fichiers inutilisés dans le magasin de données en vue de libérer de l’espace disque.

Vous pouvez exécuter le nettoyage de la mémoire du magasin de données en :

1. En accédant à la console JMX qui se trouve à l’adresse *https://&lt;serveraddress:port>/system/console/jmx*
1. Recherchant **RepositoryManagement.** Une fois que vous aurez trouvé le gestionnaire de référentiel MBean, cliquez dessus pour afficher les options disponibles.
1. Accédez à la fin de la page, puis cliquez sur le lien **startDataStoreGC(boolean markOnly)**.
1. Dans la boîte de dialogue suivante, saisissez `false` pour le paramètre `markOnly`, puis cliquez sur **Invoquer** :

   ![chlimage_1-9](assets/chlimage_1-9.png)

   >[!NOTE]
   >
   >Le paramètre `markOnly` indique si la phase de balayage du nettoyage sera exécutée ou non.

## Nettoyage de la mémoire d’entrepôt de données pour les entrepôts de données partagés  {#data-store-garbage-collection-for-a-shared-data-store}

>[!NOTE]
>
>Lorsque le nettoyage de la mémoire est effectué dans une configuration d’entrepôt de données partagé ou en cluster (avec Mongo ou Segment Tar), le journal peut contenir des avertissements sur l’impossibilité de supprimer certains ID de blob. Ces avertissements se produisent, car les ID de blob supprimés durant un nettoyage précédent sont à nouveau référencés de manière incorrecte par d’autres nœuds partagés ou clusters qui n’ont pas d’informations sur les suppressions des ID. Lorsque le nettoyage est effectué, un avertissement est donc enregistré dans le journal après une tentative de suppression d’un ID qui avait déjà été supprimé lors du précédent nettoyage. Ce comportement n’a toutefois aucune incidence sur les performances ou la fonctionnalité.

>[!NOTE]
>
>Si vous utilisez une configuration de magasin de données partagée et que le nettoyage de la mémoire du magasin de données est désactivé, l’exécution de la tâche de nettoyage du binaire Lucene peut soudainement augmenter l’espace disque utilisé. Pour éviter cela, vous devez désactiver BlobTracker sur toutes les instances d’auteur et de publication comme suit :
>
>1. Désactivez l’instance AEM.
>2. Ajoutez le paramètre `blobTrackSnapshotIntervalInSecs=L"0"` dans le fichier `crx-quickstart/install/org.apache.jackrabbit.oak.segment.SegmentNodeStoreService.config`. Ce paramètre nécessite Oak 1.12.0, 1.10.2 ou une version ultérieure.
>3. Redémarrez l’instance AEM.


Avec des versions plus récentes d’AEM, le nettoyage de la mémoire du magasin de données peut également être effectué sur des magasins de données partagés par plusieurs référentiels. Pour pouvoir exécuter le nettoyage de la mémoire du magasin de données sur un magasin de données partagé, procédez comme suit : 

1. Vérifiez que les tâches de maintenance configurées pour le nettoyage de la mémoire du magasin de données sont désactivées sur toutes les instances de référentiel partageant le magasin de données.
1. Exécutez les étapes mentionnées dans [Nettoyage de la mémoire binaire](/help/sites-deploying/data-store-config.md#data-store-garbage-collection) sur **toutes** les instances de référentiel partageant le magasin de données. Veillez toutefois à saisir `true` pour le paramètre `markOnly` avant de cliquer sur le bouton Invoquer :

   ![chlimage_1-10](assets/chlimage_1-10.png)

1. Après avoir effectué la procédure ci-dessus sur toutes les instances, exécutez à nouveau le nettoyage de l’entrepôt de données à partir d’**une** des instances :

   1. Accédez à la console JMX, puis sélectionnez le gestionnaire de référentiel MBean.
   1. Cliquez sur le lien **Click startDataStoreGC(boolean markOnly)**.
   1. Dans la boîte de dialogue suivante, saisissez à nouveau `false` pour le paramètre `markOnly`.
   Cela permettra d’assembler tous les fichiers trouvés à l’aide de la phase de repérage utilisée précédemment et de supprimer ensuite le reste inutilisé du magasin de données.
