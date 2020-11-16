---
title: Éléments de stockage dans AEM 6.5
seo-title: Éléments de stockage dans AEM 6.5
description: Obtenez des informations sur les mises en œuvre du stockage de nœud disponibles dans AEM 6.5 et sur la maintenance du référentiel.
seo-description: Obtenez des informations sur les mises en œuvre du stockage de nœud disponibles dans AEM 6.5 et sur la maintenance du référentiel.
uuid: 3b018830-c42e-48e0-9b6f-cd230b02d914
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: 0aa2c22f-32bb-4e50-8328-63ed73c0f19e
legacypath: /content/docs/en/aem/6-0/deploy/upgrade/microkernels-in-aem-6-0
translation-type: tm+mt
source-git-commit: 2fc35bfd93585a586cb1d4e3299261611db49ba6
workflow-type: tm+mt
source-wordcount: '733'
ht-degree: 82%

---


# Éléments de stockage dans AEM 6.5{#storage-elements-in-aem}

Dans cet article, nous allons aborder les éléments suivants :

* [Présentation du stockage dans AEM 6](/help/sites-deploying/storage-elements-in-aem-6.md#overview-of-storage-in-aem)
* [Maintenance du référentiel](/help/sites-deploying/storage-elements-in-aem-6.md#maintaining-the-repository)

## Présentation du stockage dans AEM 6 {#overview-of-storage-in-aem}

L’un des principaux changements dans AEM 6 concerne les innovations au niveau du référentiel.

Actuellement, il existe deux implémentations de stockage de nœud disponibles dans AEM 6 : le stockage tar et le stockage MongoDB.

### Stockage tar {#tar-storage}

#### Exécution d’une toute nouvelle instance AEM installée avec un stockage tar {#running-a-freshly-installed-aem-instance-with-tar-storage}

>[!CAUTION]
>
>Le PID de la banque de noeuds de segments a été modifié par org.apache.jackrabbit.oak.**plugins**.segment.SegmentNodeStoreService dans les versions précédentes de AEM 6 à org.apache.jackrabbit.oak.segment.SegmentNodeStoreService dans AEM 6.3. Assurez-vous d’effectuer les ajustements de configuration nécessaires pour refléter cette modification.

Par défaut, AEM 6 utilise le stockage tar pour stocker les nœuds et les fichiers binaires à l’aide des options de configuration par défaut. Pour configuer manuellement les paramètres de stockage, suivez la procédure ci-dessous :

1. Téléchargez le jar quickstart AEM 6 et placez-le dans un nouveau dossier. 
1. Décompressez AEM en exécutant :

   `java -jar cq-quickstart-6.jar -unpack`

1. Create a folder named `crx-quickstart\install` in the installation directory.

1. Créez un fichier nommé `org.apache.jackrabbit.oak.segment.SegmentNodeStoreService.cfg` dans le dossier nouvellement créé.

1. Modifiez le fichier, puis définissez les options de configuration. Les options suivantes sont disponibles pour l’entrepôt du nœud de segment, qui est la base de cette implémentation du stockage tar AEM :

   * `repository.home` : chemin vers le répertoire racine du référentiel dans lequel sont stockées les différentes données associées au référentiel. Par défaut, les fichiers de segment doivent être stockés dans le répertoire crx-quickstart/segmentstore.
   * `tarmk.size` : taille maximale d’un segment en Mo. La valeur par défaut est 256 Mo.

1. Démarrez AEM.

### Stockage Mongo {#mongo-storage}

#### Exécution d’une instance AEM nouvellement installée avec le stockage Mongo {#running-a-freshly-installed-aem-instance-with-mongo-storage}

AEM 6 peut être configuré pour s’exécuter avec le stockage MongoDB en suivant la procédure ci-dessous :

1. Téléchargez le jar quickstart AEM 6 et placez-le dans un nouveau fichier. 
1. Décompressez AEM en exécutant la commande suivante :

   `java -jar cq-quickstart-6.jar -unpack`

1. Assurez-vous que MongoDB est installé et qu’une instance de `mongod` est en cours d’exécution. Pour plus d’informations, reportez-vous à la section [Configuration de MongoDB](https://docs.mongodb.org/manual/installation/). 
1. Create a folder named `crx-quickstart\install` in the installation directory.
1. Configurez le stock de nœud en créant un fichier de configuration avec le nom de la configuration que vous souhaitez utiliser dans le répertoire `crx-quickstart\install`.

   The Document Node Store (which is the basis for AEM&#39;s MongoDB storage implementation) uses a file called `org.apache.jackrabbit.oak.plugins.document.DocumentNodeStoreService.cfg`

1. Modifiez le fichier, puis définissez les options de configuration. Les options suivantes sont disponibles :

   * `mongouri` : [MongoURI](https://docs.mongodb.org/manual/reference/connection-string/) requis pour se connecter à la base donnée Mongo. La valeur par défaut est de `mongodb://localhost:27017`
   * `db` : nom de la base de donnée Mongo. Par défaut, les nouvelles installations d’AEM 6 utilisent **aem-author** comme nom de la base de données.
   * `cache` : taille du cache en Mo. Elle est distribuée entre différents caches utilisés dans DocumentNodeStore. La valeur par défaut est de 256.
   * `changesSize` : taille en Mo de la collection limitée utilisée dans Mongo pour la mise en cache de la sortie diff. La valeur par défaut est de 256.
   * `customBlobStore` : valeur booléenne indiquant qu’un entrepôt de données personnalisé sera utilisé. La valeur par défaut est false.

1. Créez un fichier de configuration avec le PID de l’entrepôt de données que vous souhaitez utiliser et modifiez le fichier afin de définir les options de configuration. Pour plus d’informations, voir [Configuration des stocks de nœuds et des entrepôts de données](/help/sites-deploying/data-store-config.md).

1. Démarrez le jar AEM 6 avec une sauvegarde du stockage MongoDB en exécutant :

   ```shell
   java -jar cq-quickstart-6.jar -r crx3,crx3mongo
   ```

   Where **`-r`** is the backend runmode. Dans cet exemple, il commence par la prise en charge MongoDB. 

#### Désactiver les pages THP {#disabling-transparent-huge-pages}

Red Hat Linux utilise un algorithme de gestion de la mémoire appelé Transparent Huge Pages (THP). Tandis qu’AEM effectue des lectures et des écritures affinées, THP est optimisé pour des opérations plus volumineuses. Pour cette raison, il est recommandé de désactiver THP sur le stockage Tar et Mongo. Pour désactiver l’algorithme, procédez comme suit :

1. Open the `/etc/grub.conf` file in the text editor of your choice.
1. Add the following line to the **grub.conf** file:

   ```
   transparent_hugepage=never
   ```

1. Enfin, vérifiez si le paramètre a été appliqué en exécutant :

   ```
   cat /sys/kernel/mm/redhat_transparent_hugepage/enabled
   ```

   Si THP est désactivé, la sortie de la commande ci-dessus doit être :

   ```
   always madvise [never]
   ```

>[!NOTE]
>
>De plus, vous pouvez également consulter les ressources suivantes :
>
>* For more information regarding Transparent Huge Pages on Red Hat Linux, see this [article](https://access.redhat.com/solutions/46111).
>* For Linux tuning tips, see this [article](https://helpx.adobe.com/fr/experience-manager/kb/performance-tuning-tips.html).

>



## Maintenance du référentiel {#maintaining-the-repository}

Chaque mise à jour du référentiel crée une nouvelle révision de contenu. Par conséquent, à chaque mise à jour, la taille du référentiel augmente. Pour éviter une croissance incontrôlée au référentiel, il faut nettoyer les anciennes révisions pour libérer de l’espace sur le disque. Cette fonctionnalité de maintenance est appelée le nettoyage des révisions. Le mécanisme de nettoyage des révisions permet de récupérer de l’espace disque en supprimant les données obsolètes du référentiel. Pour de plus amples informations sur le nettoyage des révisions, consultez la page [Nettoyage des révisions](/help/sites-deploying/revision-cleanup.md). 
