---
title: Éléments de stockage dans AEM 6.5
seo-title: Storage Elements in AEM 6.5
description: Découvrez les implémentations de stockage de noeud disponibles dans AEM 6.5 et comment gérer le référentiel.
seo-description: Learn about the node storage implementations available in AEM 6.5 and how to maintain the repository.
uuid: 3b018830-c42e-48e0-9b6f-cd230b02d914
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: 0aa2c22f-32bb-4e50-8328-63ed73c0f19e
legacypath: /content/docs/en/aem/6-0/deploy/upgrade/microkernels-in-aem-6-0
exl-id: 52437eb5-f9fb-4945-9950-5a1562fe878d
source-git-commit: 9defa6d1843007e9375d839f72f6993c691a37c0
workflow-type: tm+mt
source-wordcount: '708'
ht-degree: 45%

---

# Éléments de stockage dans AEM 6.5{#storage-elements-in-aem}

Cet article traite des sujets suivants :

* [Présentation du stockage dans AEM 6](/help/sites-deploying/storage-elements-in-aem-6.md#overview-of-storage-in-aem)
* [Maintenance du référentiel](/help/sites-deploying/storage-elements-in-aem-6.md#maintaining-the-repository)

## Présentation du stockage dans AEM 6 {#overview-of-storage-in-aem}

L’une des modifications les plus importantes d’AEM 6 concerne les innovations au niveau du référentiel.

Actuellement, il existe deux implémentations de stockage de noeuds disponibles dans AEM6 : Stockage Tar et stockage MongoDB.

### Stockage tar {#tar-storage}

#### Exécution d’une toute nouvelle instance AEM installée avec un stockage tar {#running-a-freshly-installed-aem-instance-with-tar-storage}

>[!CAUTION]
>
>Le PID du magasin de nœuds de segment a été changé, en remplaçant org.apache.jackrabbit.oak.**plugins**.segment.SegmentNodeStoreService dans les versions précédentes d’AEM 6 à org.apache.jackrabbit.oak.segment.SegmentNodeStoreService dans AEM 6.3. Assurez-vous que les réglages de configuration nécessaires sont effectués afin que les modifications soient répercutées.

Par défaut, AEM 6 utilise le stockage tar pour stocker les nœuds et les fichiers binaires à l’aide des options de configuration par défaut. Vous pouvez configurer manuellement ses paramètres de stockage en procédant comme suit :

1. Téléchargez AEM jar de démarrage rapide 6 et placez-le dans un nouveau dossier.
1. Décompressez l’AEM en exécutant :

   `java -jar cq-quickstart-6.jar -unpack`

1. Créez un dossier nommé `crx-quickstart\install` dans le répertoire d’installation.

1. Créez un fichier nommé `org.apache.jackrabbit.oak.segment.SegmentNodeStoreService.cfg` dans le dossier nouvellement créé.

1. Modifiez le fichier et définissez les options de configuration. Les options suivantes sont disponibles pour le magasin de noeuds de segment, qui est la base de l’implémentation de l’espace de stockage AEM Tar :

   * `repository.home`: Chemin d’accès au répertoire d’accueil du référentiel dans lequel sont stockées diverses données liées au référentiel. Par défaut, les fichiers de segment doivent être stockés dans le répertoire crx-quickstart/segmentstore.
   * `tarmk.size` : taille maximale d’un segment en Mo. La valeur par défaut est 256 Mo.

1. Démarrez AEM.

### Stockage Mongo {#mongo-storage}

#### Exécution d’une instance AEM nouvellement installée avec le stockage Mongo {#running-a-freshly-installed-aem-instance-with-mongo-storage}

AEM 6 peut être configuré pour s’exécuter avec le stockage MongoDB en suivant la procédure ci-dessous :

1. Téléchargez le fichier jar de démarrage rapide AEM 6 et placez-le dans un nouveau dossier.
1. Décompressez l’AEM en exécutant la commande suivante :

   `java -jar cq-quickstart-6.jar -unpack`

1. Assurez-vous que MongoDB est installé et qu’une instance de `mongod` est en cours d’exécution. Pour plus d’informations, reportez-vous à la section [Configuration de MongoDB](https://docs.mongodb.org/manual/installation/). 
1. Créez un dossier nommé `crx-quickstart\install` dans le répertoire d’installation.
1. Configurez l’entrepôt de noeuds en créant un fichier de configuration avec le nom de la configuration que vous souhaitez utiliser dans le `crx-quickstart\install` répertoire .

   Le magasin de nœuds de document (qui sert de base à l’implémentation du stockage MongoDB d’AEM) utilise un fichier nommé `org.apache.jackrabbit.oak.plugins.document.DocumentNodeStoreService.cfg`.

1. Modifiez le fichier et définissez vos options de configuration. Les options suivantes sont disponibles :

   * `mongouri` : [MongoURI](https://docs.mongodb.org/manual/reference/connection-string/) requis pour se connecter à la base de données Mongo. La valeur par défaut est de `mongodb://localhost:27017`.
   * `db` : nom de la base de données Mongo. Par défaut, les nouvelles installations d’AEM 6 utilisent **aem-author** comme nom de la base de données.
   * `cache`: Taille du cache en mégaoctets. Cette taille de cache est répartie entre les différents caches utilisés dans DocumentNodeStore. La valeur par défaut est 256.
   * `changesSize` : taille en Mo de la collection limitée utilisée dans Mongo pour la mise en cache de la sortie diff. La valeur par défaut est 256.
   * `customBlobStore` : valeur booléenne indiquant qu’un magasin de données personnalisé est utilisé. La valeur par défaut est false.

1. Créez un fichier de configuration avec le PID de l’entrepôt de données que vous souhaitez utiliser et modifiez le fichier pour définir les options de configuration. Pour plus d’informations, consultez la section [Configuration des magasins de nœuds et des entrepôts de données](/help/sites-deploying/data-store-config.md).

1. Démarrez le jar AEM 6 avec une sauvegarde du stockage MongoDB en exécutant :

   ```shell
   java -jar cq-quickstart-6.jar -r crx3,crx3mongo
   ```

   Où le mode d’exécution principal est **`-r`**, l’exemple commence avec la prise en charge de MongoDB.

#### Désactivation de la transparence des pages Huge {#disabling-transparent-huge-pages}

Red Hat® Linux® utilise un algorithme de gestion de la mémoire appelé Transparent Huge Pages (THP). Tandis qu’AEM effectue des lectures et des écritures affinées, THP est optimisé pour des opérations plus volumineuses. Par conséquent, il est recommandé de désactiver THP sur le stockage Tar et Mongo. Pour désactiver l’algorithme, procédez comme suit :

1. Ouvrez le fichier `/etc/grub.conf` dans l’éditeur de texte de votre choix.
1. Ajoutez la ligne suivante au fichier **grub.conf** :

   ```
   transparent_hugepage=never
   ```

1. Enfin, vérifiez si le paramètre a été appliqué en exécutant :

   ```
   cat /sys/kernel/mm/redhat_transparent_hugepage/enabled
   ```

   Si THP est désactivé, la sortie de la commande ci-dessus doit être :

   ```
   always madvise [never]
   ```

>[!NOTE]
>
>Consultez les ressources suivantes :
>
>* Pour plus d’informations sur Transparent Huge Pages sous Red Hat® Linux®, voir ceci [article](https://access.redhat.com/solutions/46111).
* Pour obtenir des conseils sur le réglage de Linux®, voir ceci [article](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/configuring/configuring-performance.html?lang=en).
>


## Maintenance du référentiel {#maintaining-the-repository}

Chaque mise à jour du référentiel crée une révision du contenu. Par conséquent, avec chaque mise à jour, la taille du référentiel augmente. Pour éviter une croissance incontrôlée du référentiel, les anciennes révisions doivent être nettoyées pour libérer des ressources de disque. Cette fonctionnalité de maintenance est appelée Nettoyage des révisions. Le mécanisme de nettoyage des révisions récupère l’espace disque en supprimant les données obsolètes du référentiel. Pour de plus amples informations sur le nettoyage des révisions, consultez la page [Nettoyage des révisions](/help/sites-deploying/revision-cleanup.md). 
