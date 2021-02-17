---
title: Configuration des magasins de nœuds et des entrepôts de données dans AEM 6
seo-title: Configuration des magasins de nœuds et des entrepôts de données dans AEM 6
description: Découvrez comment configurer les magasins de nœuds et les entrepôts de données. Apprenez également à exécuter le nettoyage de la mémoire d’entrepôt de données.
seo-description: Découvrez comment configurer les magasins de nœuds et les entrepôts de données. Apprenez également à exécuter le nettoyage de la mémoire d’entrepôt de données.
uuid: 1a58c0ba-1c32-4539-ad0d-0a27c8c4ff5e
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: deploying
discoiquuid: b97482f2-2791-4d14-ae82-388302d9eab3
docset: aem65
legacypath: /deploy/platform/data-store-config
translation-type: tm+mt
source-git-commit: 93cb84763cfd77b67a5dd1481caab79337f6e7c4
workflow-type: tm+mt
source-wordcount: '3423'
ht-degree: 66%

---


# Configuration des magasins de nœuds et des entrepôts de données dans AEM 6{#configuring-node-stores-and-data-stores-in-aem}

## Présentation {#introduction}

Dans Adobe Experience Manager (AEM), les données binaires peuvent être stockées indépendamment des nœuds de contenu. Les données binaires sont stockées dans un entrepôt de données alors que les nœuds de contenu sont stockés dans un magasin de nœuds.

Les entrepôts de données et les magasins de nœuds peuvent être configués en utilisant la configuration OSGi. Chaque configuration OSGi est référencé à l’aide d’un PID (identifiant de persistant).

## Étapes de configuration {#configuration-steps}

Pour configurer le magasin de nœuds et l’entrepôt de données, procédez comme suit :

1. Copiez le fichier JAR quickstart AEM dans son répertoire d’installation.
1. Créez un dossier `crx-quickstart/install` dans le répertoire d’installation.
1. Configurez tout d’abord le magasin de nœuds en créant un fichier de configuration avec le nom de l’option de magasin de nœuds que vous voulez utiliser dans le répertoire `crx-quickstart/install`.

   Par exemple, le magasin de noeuds de Document (qui est la base de l’implémentation AEM MongoMK) utilise le fichier `org.apache.jackrabbit.oak.plugins.document.DocumentNodeStoreService.config`.

1. Modifiez le fichier et définissez vos options de configuration.
1. Créez un fichier de configuration avec le PID de l’entrepôt de données que vous souhaitez utiliser. Modifiez le fichier pour définir les options de configuration. 

   >[!NOTE]
   >
   >Voir [Configurations des magasins de nœuds](#node-store-configurations) et [Configurations des entrepôts de données](#data-store-configurations) pour les options de configuration.

1. Démarrez AEM.

## Configurations des magasins de nœuds  {#node-store-configurations}

>[!CAUTION]
>
>Les versions plus récentes d’Oak utilisent de nouveaux format et schéma d’affectation de noms pour les fichiers de configuration OSGi. Le nouveau schéma d’affectation de noms requiert que le fichier de configuration soit nommé **.config**. Le nouveau format exige que les valeurs soient saisies et est [documenté ici](https://sling.apache.org/documentation/development/slingstart.html#default-configuration-format).
>
>Si vous effectuez une mise à niveau à partir d’une version plus ancienne d’Oak, veillez d’abord à sauvegarder le dossier `crx-quickstart/install`. Après la mise à niveau, restaurez les contenus du dossier à l’installation mise à niveau, puis modifiez l’extension des fichiers de configuration de **.cfg** en **.config**.
>
>Si vous lisez cet article en vue de vous préparer pour effectuer une mise à niveau à partir d’une installation d’**AEM 5.x**, n’oubliez pas de consulter la documentation de [mise à niveau](https://docs.adobe.com/content/docs/fr/aem/6-0/deploy/upgrade.html ) en premier.

### Magasins de nœuds de segment  {#segment-node-store}

Le magasin de nœuds de segment constitue la base de l’implémentation de TarMK d’Adobe dans AEM 6. Il utilise le PID `org.apache.jackrabbit.oak.segment.SegmentNodeStoreService` pour la configuration.

>[!CAUTION]
>
>Le PID du magasin de noeuds de segments est passé de `org.apache.jackrabbit.oak.plugins.segment.SegmentNodeStoreService in previous versions` de l&#39;AEM 6 à `org.apache.jackrabbit.oak.segment.SegmentNodeStoreService` dans AEM 6.3. Assurez-vous d&#39;effectuer les ajustements de configuration nécessaires pour tenir compte de cette modification.

Vous pouvez configurer les options suivantes :

* `repository.home` : chemin vers le répertoire racine du référentiel dans lequel sont stockées les données associées au référentiel. Par défaut, les fichiers de segment sont stockés dans le répertoire `crx-quickstart/segmentstore`. 

* `tarmk.size` : taille maximale d’un segment en Mo. La valeur maximale par défaut étant de 256 Mo.
* `customBlobStore` : valeur booléenne indiquant qu’un entrepôt de données personnalisé est utilisé. La valeur par défaut est true pour AEM versions 6.3 et ultérieures. Pour les versions antérieures à AEM 6.3, la valeur par défaut était false.

Voici un exemple de fichier `org.apache.jackrabbit.oak.segment.SegmentNodeStoreService.config` :

```shell
#Path to repo
repository.home="crx-quickstart/repository"

#Max segment size
tarmk.size=I"256"

#Custom data store
customBlobStore=B"true"
```

#### Magasin de nœuds de document {#document-node-store}

Le magasin de noeuds de document est la base de l’implémentation AEM MongoMK. Il utilise le `org.apache.jackrabbit.oak.plugins.document.DocumentNodeStoreService`* *PID. Les options de configuration suivantes sont disponibles :

* `mongouri` : [MongoURI](https://docs.mongodb.org/manual/reference/connection-string/) requis pour se connecter à la base donnée Mongo. La valeur par défaut est de `mongodb://localhost:27017`

* `db` : nom de la base de donnée Mongo. La valeur par défaut est **Oak** ``. However, new AEM 6 installations use **aem-author** ``comme nom de base de données par défaut.

* `cache` : taille du cache en Mo. Elle est distribuée entre différents caches utilisés dans DocumentNodeStore. La valeur par défaut est de `256`

* `changesSize` : taille en Mo de la collection limitée utilisée dans Mongo pour la mise en cache de la sortie diff. La valeur par défaut est de `256`

* `customBlobStore` : valeur booléenne indiquant qu’un entrepôt de données personnalisé sera utilisé. La valeur par défaut est de `false`.

Voici un exemple de fichier `org.apache.jackrabbit.oak.plugins.document.DocumentNodeStoreService.config` :

```shell
#Mongo server details
mongouri="mongodb://localhost:27017"

#Name of Mongo database to use
db="aem-author"

#Store binaries in custom BlobStore
customBlobStore=B"false"
```

## Configurations des entrepôts de données {#data-store-configurations}

Lorsque vous traitez un grand nombre de fichiers binaires, il est recommandé d’utiliser un entrepôt de données externe au lieu de l’entrepôt de nœuds par défaut pour optimiser la performance.

Par exemple, si votre projet requiert un grand nombre de ressources multimédias, vous pouvez les stocker dans l’entrepôt de données de fichier ou S3 afin d’y accéder plus rapidement qu’en les stockant directement dans MongoDB.

L’entrepôt de données basé sur les fichiers offre de meilleures performances que MongoDB. De plus, les opérations de sauvegarde et de restauration Mongo sont plus lentes lorsque le nombre de ressources est élevé. 

Reportez-vous aux sections ci-dessous pour plus d’informations sur les différents entrepôts de données et les différentes configurations.

>[!NOTE]
>
>Pour activer les entrepôts de données personnalisés, vous devez vérifier que `customBlobStore` est défini sur `true` dans le fichier de configuration de magasin de nœuds respectif ([magasin de nœuds de segment](/help/sites-deploying/data-store-config.md#segment-node-store) ou [magasin de nœuds de document](/help/sites-deploying/data-store-config.md#document-node-store)).

### Entrepôt de données basé sur les fichiers {#file-data-store}

Il s’agit de l’implémentation de [FileDataStore ](https://jackrabbit.apache.org/api/2.8/org/apache/jackrabbit/core/data/FileDataStore.html) présent dans Jackrabbit 2, qui offre une méthode pour stocker les données binaires comme tout autre fichier sur le système de fichiers. Il utilise le PID `org.apache.jackrabbit.oak.plugins.blob.datastore.FileDataStore`.

Voici les options de configuration disponibles :

* `repository.home` : chemin vers le répertoire racine du référentiel dans lequel sont stockées les différentes données associées au référentiel. Par défaut, les fichiers binaires sont stockés dans le répertoire `crx-quickstart/repository/datastore`.

* `path`: Chemin d’accès au répertoire sous lequel les fichiers seront stockés. Si spécifié, il prévaut sur la valeur `repository.home`.

* `minRecordLength` : taille minimale en octets d’un fichier stocké dans l’entrepôt de données. Un contenu binaire inférieur à cette valeur est intégré.

>[!NOTE]
>
>Lorsque vous utilisez un NAS pour stocker les entrepôts de données basés sur les fichiers partagés, assurez-vous d’utiliser uniquement les appareils les plus performants afin d’éviter des problèmes de performances.

## Entrepôt de données S3 Amazon  {#amazon-s-data-store}

AEM peut être configuré pour stocker des données dans Amazon Simple Enregistrement Service (S3). Il utilise le PID `org.apache.jackrabbit.oak.plugins.blob.datastore.S3DataStore.config` pour la configuration.

Pour activer la fonctionnalité de l’entrepôt de données S3, un Feature Pack contenant le connecteur d’entrepôt de données S3 doit être téléchargé et installé. Accédez au [référentiel Adobe](https://repo.adobe.com/nexus/content/groups/public/com/adobe/granite/com.adobe.granite.oak.s3connector/), puis téléchargez la dernière version des versions 1.10.x du Feature Pack (par exemple, com.adobe.granite.oak.s3connector-1.10.0.zip). De plus, vous devez également télécharger et installer le dernier Service Pack AEM, tel qu&#39;il est indiqué sur la [page Notes de mise à jour AEM 6.5](/help/release-notes/sp-release-notes.md).

>[!NOTE]
>
>Lorsque vous utilisez AEM  avec TarMK, les fichiers binaires sont stockés par défaut dans `FileDataStore`. Pour utiliser TarMK avec la banque de données S3, vous devez début AEM en utilisant le mode d’exécution `crx3tar-nofds`, par exemple :

```shell
java -jar <aem-jar-file>.jar -r crx3tar-nofds
```

À la fin du téléchargement, vous pouvez installer et configurer le connecteur S3 comme suit :

1. Extrayez le contenu du fichier zip du Feature Pack dans un dossier temporaire.

1. Accédez au dossier temporaire et naviguez jusqu’à l’emplacement suivant :

   ```xml
   jcr_root/libs/system/install
   ```

   Copiez tout le contenu de l’emplacement ci-dessus dans `<aem-install>/crx-quickstart/install.`

1. Si AEM est déjà configuré pour fonctionner avec l’enregistrement Tar ou MongoDB, supprimez tous les fichiers de configuration existants du dossier ***&lt;aem-install>***/*crx-quickstart*/*install* avant de continuer. Les fichiers à supprimer sont les suivants :

   * `For MongoMK: org.apache.jackrabbit.oak.plugins.document.DocumentNodeStoreService.config`
   * `For TarMK: org.apache.jackrabbit.oak.segment.SegmentNodeStoreService.config`

1. Retournez à l’emplacement temporaire où le Feature Pack a été extrait, puis copiez le contenu du dossier suivant : 

   * `jcr_root/libs/system/config`

   vers

   * `<aem-install>/crx-quickstart/install`

   Veillez à copier uniquement les fichiers de configuration nécessaires pour votre configuration actuelle. Pour une configuration d’entrepôts de données partagé et dédié, copiez le fichier `org.apache.jackrabbit.oak.plugins.blob.datastore.S3DataStore.config`.

   >[!NOTE]
   >
   >Dans une configuration en cluster, effectuez les étapes ci-dessus sur tous les nœuds du cluster, l’un après l’autre. Veillez également à utiliser les mêmes configurations S3 pour tous les nœuds.

1. Modifiez le fichier, puis ajoutez les options de configuration requises par votre configuration.
1. Démarrez AEM.

### Mise à nouveau vers une nouvelle version du connecteur 1.10.x S3 {#upgrading-to-a-new-version-of-the-s-connector}

Si vous devez effectuer une mise à niveau vers une nouvelle version du connecteur 1.10.x S3 (par exemple, de la version 1.10.0 vers la version 1.10.4), procédez comme suit :

1. Désactivez l’instance AEM.

1. Accédez à `<aem-install>/crx-quickstart/install/15` dans le dossier d’installation AEM et effectuez une sauvegarde de son contenu.
1. Après la sauvegarde, supprimez l’ancienne version de S3 Connector et ses dépendances en supprimant tous les fichiers jar du dossier `<aem-install>/crx-quickstart/install/15`, par exemple :

   * **oak-blob-cloud-1.6.1.jar**
   * **aws-java-sdk-osgi-1.10.76.jar**

   >[!NOTE]
   >
   >Les noms de fichier présentés ci-dessus sont utilisés à des fins d’illustration uniquement.

1. Téléchargez la dernière version du Feature Pack 1.8.x depuis le [référentiel Adobe](https://repo.adobe.com/nexus/content/groups/public/com/adobe/granite/com.adobe.granite.oak.s3connector/).
1. Décompressez le contenu dans un dossier distinct, puis accédez à `jcr_root/libs/system/install/15`.
1. Copiez les fichiers jar dans le dossier d’installation AEM **&lt;aem-install>**/crx-quickstart/install/15.
1. Démarrez AEM et vérifiez les fonctionnalités du connecteur.

Vous pouvez utiliser le fichier de configuration avec les options suivantes :

* accessKey : Clé d’accès AWS.
* secretKey : clé d’accès secrète AWS. **Remarque :** Vous pouvez également utiliser les rôles  [IAM ](https://docs.aws.amazon.com/sdk-for-java/v1/developer-guide/java-dg-roles.html) pour l’authentification. Si vous utilisez des rôles IAM, vous n’avez plus besoin de spécifier les attributs `accessKey` et `secretKey`.

* s3Bucket : Nom du compartiment.
* s3Region : La région du seau.
* chemin : Chemin d’accès du magasin de données. La valeur par défaut est **&lt;AEM dossier d’installation>/repository/datastore**
* minRecordLength: Taille minimale d’un objet qui doit être stocké dans le magasin de données. La valeur minimale/par défaut est **16 Ko.**
* maxCachedBinarySize : Les binaires dont la taille est inférieure ou égale à cette taille seront stockés dans le cache mémoire. La taille est en octets. La valeur par défaut est **17408 **(17 Ko).

* cacheSize : Taille du cache. La valeur est spécifiée en octets. La valeur par défaut est **64 Go**.
* secret : Uniquement à utiliser en cas d&#39;utilisation de la réplication sans binaire pour la configuration de la banque de données partagée.
* stagingSplitPourcentage : Pourcentage de la taille du cache configuré pour être utilisé pour le test des téléchargements asynchrones. La valeur par défaut est **10**.
* uploadThreads : Nombre de threads de transfert utilisés pour les téléchargements asynchrones. La valeur par défaut est **10**.
* stagingPurgeInterval : Intervalle en secondes de purge des téléchargements terminés du cache d’évaluation. La valeur par défaut est de **300** secondes (5 minutes).
* stagingRetryInterval : Intervalle de nouvelle tentative en secondes pour les téléchargements ayant échoué. La valeur par défaut est de **600** secondes (10 minutes).

### Options de régions de compartiment {#bucket-region-options}

<table>
 <tbody>
  <tr>
   <td>US Standard</td>
   <td><code>us-standard</code></td>
  </tr>
  <tr>
   <td>Ouest américain</td>
   <td><code>us-west-2</code></td>
  </tr>
  <tr>
   <td>Ouest des États-Unis (Californie du Nord)</td>
   <td><code>us-west-1</code></td>
  </tr>
  <tr>
   <td>UE (Irlande)<br /> </td>
   <td><code>EU</code></td>
  </tr>
  <tr>
   <td>Asie-Pacifique (Singapour)<br /> </td>
   <td><code>ap-southeast-1</code></td>
  </tr>
  <tr>
   <td>Asie-Pacifique (Sydney)<br /> </td>
   <td><code>ap-southeast-2</code></td>
  </tr>
  <tr>
   <td>Asie-Pacifique (Tokyo)</td>
   <td><code>ap-northeast-1</code></td>
  </tr>
  <tr>
   <td>Amérique du Sud (Sao Paolo)<br /> </td>
   <td><code>sa-east-1</code></td>
  </tr>
 </tbody>
</table>

**Mise en cache de DataStore**

>[!NOTE]
>
>Les implémentations DataStore de `S3DataStore`, `CachingFileDataStore` et `AzureDataStore` prennent en charge la mise en cache du système de fichiers local. L&#39;implémentation de `CachingFileDataStore` est utile lorsque DataStore est sur NFS (Network File System).


Lors de la mise à niveau à partir d’une ancienne implémentation de mise en cache (pré-oak 1.6), il existe une différence dans la structure du répertoire de cache du système de fichiers local. Dans l’ancienne structure de cache, les fichiers téléchargés et chargés étaient placés directement dans le chemin du cache. La nouvelle structure sépare les téléchargements et téléchargements et les stocke dans deux répertoires nommés `upload` et `download` sous le chemin du cache. Le processus de mise à niveau doit être transparent et tout téléchargement en attente doit être planifié. De plus, les fichiers précédemment téléchargés dans le cache seront placés dans le cache lors de l’initialisation.

Vous pouvez également mettre à niveau le cache hors ligne en utilisant la commande `datastorecacheupgrade` de oak-run. Pour plus d’informations sur l’exécution de la commande, consultez le fichier [lisez-moi](https://svn.apache.org/repos/asf/jackrabbit/oak/trunk/oak-run/README.md ) du module oak-run.

Le cache a une taille limite et il peut être configuré à l’aide du paramètre cacheSize.

**Téléchargements**

Le cache local sera vérifié pour l’enregistrement du fichier/blob demandé avant de pouvoir y accéder à partir du DataStore. Lorsque la taille du cache dépasse la limite configurée (voir le paramètre `cacheSize`) lors de l’ajout d’un fichier, certains des fichiers seront évincés pour récupérer de l’espace.

**Téléchargement asynchrone**

Le cache prend en charge les téléchargements asynchrones vers le DataStore. Les fichiers sont placés localement, dans le cache (sur le système de fichiers) et une tâche asynchrone commence à les télécharger. Le nombre de téléchargements asynchrones est limité par la taille du cache intermédiaire. La taille du cache intermédiaire est configurée à l’aide du paramètre `stagingSplitPercentage`. Ce paramètre définit le pourcentage de taille de cache à utiliser pour le cache intermédiaire. En outre, le pourcentage de cache disponible pour les téléchargements est calculé comme suit : **(100 - `stagingSplitPercentage`) *`cacheSize`**.

Les téléchargements asynchrones sont multithreads et le nombre de threads est configuré à l’aide du paramètre `uploadThreads`.

Les fichiers sont déplacés vers le cache principal de téléchargement une fois les téléchargements effectués. Lorsque la taille du cache intermédiaire dépasse sa limite, les fichiers sont téléchargés de manière synchrone vers le DataStore jusqu’à ce que les téléchargements asynchrones précédents soient terminés et que de l’espace soit à nouveau disponible dans le cache intermédiaire. Les fichiers téléchargés sont supprimés de la zone d’évaluation par un travail périodique dont l’intervalle est configuré par le paramètre `stagingPurgeInterval`.

Les téléchargements ayant échoué (en raison d’une interruption du réseau, par exemple) sont placés dans une file d’attente pour effectuer régulièrement de nouvelles tentatives. L&#39;intervalle de nouvelle tentative est configuré à l&#39;aide de `stagingRetryInterval parameter`.

#### Configuration d’une réplication sans binaire avec Amazon S3 {#configuring-binaryless-replication-with-amazon-s}

Pour configurer une réplication sans binaire avec S3, les étapes suivantes sont nécessaires :

1. Installez les instances de création et de publication, puis vérifiez qu’elles démarrent correctement.
1. Accédez aux paramètres de l&#39;agent de réplication en ouvrant une page sur *https://localhost:4502/etc/replication/agents.author/publish.html*.
1. Appuyez sur le bouton **Modifier** dans la section **Paramètres**.
1. Modifiez l’option **Serialization type** en **Binary less**. 

1. Ajoutez le paramètre &quot; `binaryless`= `true`&quot; dans l&#39;URI de transport. Après la modification, l’URI doit ressembler à ce qui suit :

   *https://localhost:4503/bin/receive?sling:authRequestLogin=1&amp;binaryless=true*

1. Redémarrez toutes les instances de création et de publication pour que les modifications soient appliquées.

#### Création d’un cluster à l’aide de S3 et MongoDB  {#creating-a-cluster-using-s-and-mongodb}

1. Décompressez le quickstart CQ en utilisant la commande suivante :

   `java -jar cq-quickstart.jar -unpack`

1. Après la décompression d’AEM, créez un dossier à l’intérieur du répertoire d’installation *crx-quickstart*/*install*.

1. Créez ces deux fichiers à l’interieur du dossier `crx-quickstart` :

   * *org.apache.jackrabbit.oak.plugins.document.DocumentNodeStoreService.* *config*

   * *org.apache.jackrabbit.oak.plugins.blob.datastore.S3DataStore*.*config*

   Une fois que ces fichiers ont été créés, ajoutez les options de configuration selon vos besoins.

1. Installez les deux lots requis pour l’entrepôt de données S3, comme expliqué plus haut.
1. Vérifiez que MongoDB est installé et qu’une instance de `mongod` est en cours d’exécution.
1. Démarrez AEM à l’aide de la commande suivante :

   `java -Xmx1024m -XX:MaxPermSize=256M -jar cq-quickstart.jar -r crx3,crx3mongo`

1. Répétez les étapes 1 à 4 pour la seconde instance d’AEM.
1. Démarrez la seconde instance d’AEM.

#### Configuration d’un entrepôt de données partagé   {#configuring-a-shared-data-store}

1. Créez d’abord le fichier de configuration d’entrepôt de données sur chaque instance devant partager l’entrepôt de données :

   * Si vous utilisez un `FileDataStore`, créez un fichier nommé `org.apache.jackrabbit.oak.plugins.blob.datastore.FileDataStore.config` et placez-le dans le dossier `<aem-install>/crx-quickstart/install`.

   * Si vous utilisez S3 comme magasin de données, créez un fichier nommé o `rg.apache.jackrabbit.oak.plugins.blob.datastore.S3DataStore.config` dans le dossier `<aem-install>/crx-quickstart/install` comme indiqué ci-dessus.

1. Modifiez les fichiers de donfiguration d’entrepôt de données sur chaque instance pour qu’ils pointent vers le même entrepôt de données. Pour en savoir plus, voir [cet article](/help/sites-deploying/data-store-config.md#data-store-configurations).
1. Si l’instance a été clonée à partir d’un serveur existant, vous devez supprimer le `clusterId` de la nouvelle instance à l’aide du dernier outil oak-run lorsque le référentiel est hors ligne. La commande que vous devez exécuter est la suivante :

   ```xml
   java -jar oak-run.jar resetclusterid < repository path | Mongo URI >
   ```

   >[!NOTE]
   >
   >Si un magasin de nœuds de segment est configuré, le chemin du référentiel doit être spécifié. Par défaut, le chemin d’accès est `<aem-install-folder>/crx-quickstart/repository/segmentstore.` Si un magasin de noeuds de Document est configuré, vous pouvez utiliser un URI de chaîne de connexion [Mongo](https://docs.mongodb.org/manual/reference/connection-string/).

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


1. Enfin, validez la configuration. Pour cela, vous devez rechercher un fichier unique ajouté à l’entrepôt de données par chaque référentiel le partageant. Le format des fichiers est `repository-[UUID]`, où l’UUID est un identifiant unique de chaque référentiel individuel.

   Une configuration correcte devrait être donc dotée d’autant de fichiers uniques que de référentiels partageant l’entrepôt de données.

   Les fichiers sont stockés différemment, selon l’entrepôt de données :

   * Pour `FileDataStore`, les fichiers sont créés sous le chemin racine du dossier de l’entrepôt de données.
   * Pour `S3DataStore`, les fichiers sont créés dans le compartiment S3 configuré sous le dossier `META`.

## Entrepôt de données Azure {#azure-data-store}

AEM peut être configuré pour stocker des donnés dans le service de stockage Azure de Microsoft. Il utilise le PID `org.apache.jackrabbit.oak.plugins.blob.datastore.AzureDataStore.config` pour la configuration.

Pour activer la fonctionnalité d’entrepôt de données Azure, un Feature Pack contenant le connecteur Azure doit être téléchargé et installé. Accédez au [Adobe Repository](https://repo.adobe.com/nexus/content/groups/public/com/adobe/granite/com.adobe.granite.oak.azureblobconnector/) et téléchargez la dernière version des versions 1.6.x de Feature Pack (par exemple, com.adobe.granite.oak.azureblobconnector-1.6.3.zip).

>[!NOTE]
>
>Lorsque vous utilisez AEM  avec TarMK, les fichiers binaires sont stockés par défaut dans FileDataStore. Pour utiliser TarMK avec Azure DataStore, vous devez début AEM en utilisant le mode d&#39;exécution `crx3tar-nofds`, par exemple :

```shell
java -jar <aem-jar-file>.jar -r crx3tar-nofds
```

Une fois téléchargé, vous pouvez installer et configurer le connecteur Azure comme suit :

1. Extrayez le contenu du fichier zip du Feature Pack dans un dossier temporaire.

1. Accédez au dossier temporaire et copiez le contenu de `jcr_root/libs/system/install` dans le dossier `<aem-install>crx-quickstart/install`.
1. Si AEM est déjà configuré pour fonctionner avec l&#39;enregistrement Tar ou MongoDB, supprimez les fichiers de configuration existants du dossier `/crx-quickstart/install` avant de continuer. Les fichiers à supprimer sont les suivants : 

   Pour MongoMK :

   `org.apache.jackrabbit.oak.plugins.document.DocumentNodeStoreService.config`

   Pour TarMK :

   `org.apache.jackrabbit.oak.segment.SegmentNodeStoreService.config`

1. Revenez à l’emplacement temporaire où le Feature Pack a été extrait et copiez le contenu de `jcr_root/libs/system/config` dans le dossier `<aem-install>/crx-quickstart/install`.
1. Modifiez le fichier de configuration et ajoutez les options de configuration requises par votre configuration.
1. Démarrez AEM.

Vous pouvez utiliser le fichier de configuration avec les options suivantes :

* azureSas=&quot;&quot;: Dans la version 1.6.3 du connecteur, la prise en charge du service SAS (Azure Shared Access Signature) a été ajoutée. **Si les informations d’identification SAS et de stockage figurent dans le fichier de configuration, SAS a la priorité.** Pour plus d’informations sur SAS, consultez la [documentation officielle](https://docs.microsoft.com/fr-fr/azure/storage/common/storage-dotnet-shared-access-signature-part-1 ). Assurez-vous que le caractère &quot;=&quot; est placé en séquence d’échappement comme &quot;\=&quot;.

* azureBlobEndpoint=&quot;&quot; : point de terminaison Blob Azure. Par exemple, https://&lt;enregistrement-account>.blob.core.windows.net.
* accessKey=&quot;&quot; : nom du compte de stockage. Pour plus d’informations sur les informations d’identification de l’authentification Microsoft Azure, reportez-vous à la [documentation officielle](https://azure.microsoft.com/fr-fr/documentation/articles/storage-create-storage-account). 

* secretKey=&quot;&quot; : clé d’accès au stockage. Assurez-vous que le caractère &quot;=&quot; est placé en séquence d’échappement comme &quot;\=&quot;.
* container=&quot;&quot; : nom du conteneur de stockage blob Microsoft Azure. Le conteneur est le regroupement d’un ensemble de blobs. Pour plus de détails, consultez[ la documentation officielle](https://msdn.microsoft.com/fr-fr/library/dd135715.aspx ). 
* maxConnections=&quot;&quot; : nombre de demandes simultanées par opération. La valeur par défaut est 1.
* maxErrorRetry=&quot;&quot;: Nombre de Reprises par requête. La valeur par défaut est 3.
* socketTimeout=&quot;&quot;: Intervalle d’expiration, en millisecondes, utilisé pour la demande. la valeur par défaut est de 5 minutes.

En plus des paramètres ci-dessus, les paramètres suivants peuvent également être configurés :

* chemin : Chemin d’accès du magasin de données. La valeur par défaut est `<aem-install>/repository/datastore.`
* RecordLength: Taille minimale d’un objet qui doit être stocké dans le magasin de données. La valeur par défaut est de 16 Ko.
* maxCachedBinarySize : Les binaires dont la taille est inférieure ou égale à cette taille seront stockés dans le cache mémoire. La taille est en octets. La valeur par défaut est 17408 (17 Ko).
* cacheSize : Taille du cache. La valeur est spécifiée en octets. La valeur par défaut est de 64 Go.
* secret : Uniquement à utiliser en cas d&#39;utilisation de la réplication sans binaire pour la configuration de la banque de données partagée.
* stagingSplitPourcentage : Pourcentage de la taille du cache configuré pour être utilisé pour le test des téléchargements asynchrones. La valeur par défaut est 10.
* uploadThreads : Nombre de threads de transfert utilisés pour les téléchargements asynchrones. La valeur par défaut est 10.
* stagingPurgeInterval : Intervalle en secondes de purge des téléchargements terminés du cache d’évaluation. La valeur par défaut est de 300 secondes (5 minutes).
* stagingRetryInterval : Intervalle de nouvelle tentative en secondes pour les téléchargements ayant échoué. La valeur par défaut est de 600 secondes (10 minutes).

>[!NOTE]
>
>Tous les paramètres doivent être placés entre guillemets, par exemple :

```shell
accessKey="ASDASDERFAERAER"
secretKey="28932hfjlkwdo8fufsdfas\=\="
```

## Nettoyage de la mémoire d’entrepôt de données {#data-store-garbage-collection}

Le processus de nettoyage de la mémoire d’entrepôt de données est utilisé pour supprimer tous les fichiers inutilisés dans l’entrepôt de données en vue de libérer de l’espace disque.

Vous pouvez exécuter la collecte des déchets de la banque de données en procédant comme suit :

1. Accédez à la console JMX située à l’adresse *https://&lt;adresse du serveur:port>/system/console/jmx*.
1. Recherchant **RepositoryManagement.** Une fois que vous aurez trouvé le gestionnaire de référentiel MBean, cliquez dessus pour afficher les options disponibles.
1. Accédez à la fin de la page, puis cliquez sur le lien **startDataStoreGC(boolean markOnly)**.
1. Dans la boîte de dialogue suivante, saisissez `false`   pour le paramètre `markOnly`, puis cliquez sur **Invoke** :

   ![chlimage_1-9](assets/chlimage_1-9.png)

   >[!NOTE]
   >
   >Le paramètre `markOnly` indique si la phase de balayage du nettoyage sera exécutée ou non.

## Nettoyage de la mémoire d’entrepôt de données pour les entrepôts de données partagés {#data-store-garbage-collection-for-a-shared-data-store}

>[!NOTE]
>
>Lorsque le nettoyage de la mémoire est effectué dans une configuration d’entrepôt de données partagé ou en cluster (avec Mongo ou Segment Tar), le journal peut contenir des avertissements sur l’impossibilité de supprimer certains ID de blob. Cela se produit car les ID d’objet blob supprimés dans une précédente collecte de déchets sont de nouveau référencés de manière incorrecte par d’autres noeuds de la grappe ou partagés qui ne disposent pas d’informations sur les suppressions d’ID. Lorsque le nettoyage est effectué, un avertissement est donc enregistré dans le journal après une tentative de suppression d’un ID qui avait déjà été supprimé lors du précédent nettoyage. Ce comportement n’a toutefois aucune incidence sur les performances ou la fonctionnalité.

Avec des versions plus récentes d’AEM, le nettoyage de la mémoire d’entrepôt de données peut également être effectué sur des entrepôts de données partagés par plusieurs référentiels. Pour pouvoir exécuter le nettoyage de la mémoire d’entrepôt de données sur un entrepôt de données partagé, procédez comme suit : 

1. Vérifiez que les tâches de maintenance configurées pour le nettoyage de la mémoire d’entrepôt de données sont désactivées sur toutes les instances de référentiel partageant l’entrepôt de données.
1. Exécutez les étapes mentionnées dans [Collecte de déchets binaire](/help/sites-deploying/data-store-config.md#data-store-garbage-collection) individuellement sur **toutes** les instances de référentiel partageant le magasin de données. Toutefois, veillez à entrer `true` pour le paramètre `markOnly` avant de cliquer sur le bouton Appeler :

   ![chlimage_1-10](assets/chlimage_1-10.png)

1. Après avoir effectué la procédure ci-dessus sur toutes les instances, exécutez à nouveau le nettoyage de l’entrepôt de données à partir d’**une** des instances :

   1. Accédez à la console JMX, puis sélectionnez le gestionnaire de référentiel Mbean.
   1. Cliquez sur le lien **Click startDataStoreGC(boolean markOnly)**.
   1. Dans la boîte de dialogue suivante, saisissez à nouveau `false` pour le paramètre `markOnly`.

   Cela permettra d’assembler tous les fichiers trouvés à l’aide de la phase de repérage utilisée précédemment et de supprimer ensuite le reste inutilisé de l’entrepôt de données.

