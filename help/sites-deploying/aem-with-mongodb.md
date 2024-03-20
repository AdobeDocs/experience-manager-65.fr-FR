---
title: Adobe Experience Manager avec MongoDB
description: Découvrez les tâches et les points à prendre en compte pour réussir le déploiement d’Adobe Experience Manager avec MongoDB.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
docset: aem65
exl-id: 70a39462-8584-4c76-a097-05ee436247b7
solution: Experience Manager, Experience Manager Sites
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '6185'
ht-degree: 98%

---

# Adobe Experience Manager avec MongoDB{#aem-with-mongodb}

Cet article vise à améliorer les connaissances sur les tâches et les considérations nécessaires pour déployer AEM (Adobe Experience Manager) avec MongoDB.

Pour plus d’informations sur le déploiement, consultez la section [Déploiement et maintenance](/help/sites-deploying/deploy.md) de la documentation.

## Quand utiliser MongoDB avec AEM {#when-to-use-mongodb-with-aem}

MongoDB est généralement utilisé pour la prise en charge des déploiements d’instances de création d’AEM lorsque l’un des critères suivants est satisfait :

* plus de 1 000 utilisateurs et utilisatrices uniques par jour ;
* plus de 100 utilisateurs et utilisatrices simultanés ;
* nombre élevé de modifications de page ;
* activations ou déploiements volumineux.

Les critères ci-dessus sont réservés aux instances de création et non aux instances de publication, qui doivent toutes être basées sur TarMK. Le nombre d’utilisateurs et utilisatrices fait référence aux personnes authentifiées, puisque les instances de création n’autorisent pas d’accès non authentifié.

Si les critères ne sont pas remplis, un déploiement TarMK actif/de secours est recommandé pour répondre à la disponibilité. En règle générale, MongoDB doit être pris en compte dans les situations où les exigences de mise à l’échelle sont supérieures à ce qui peut être réalisé avec un seul élément matériel.

>[!NOTE]
>
>Vous trouverez des informations supplémentaires sur la taille des instances de création et la définition des utilisateurs et utilisatrices simultanés dans la section [Instructions sur le dimensionnement du matériel](/help/managing/hardware-sizing-guidelines.md#authors-working-in-parallel).

### Déploiement minimal de MongoDB pour AEM {#minimal-mongodb-deployment-for-aem}

Vous trouverez ci-dessous un déploiement minimal pour AEM sur MongoDB. Pour plus de simplicité, les composants de terminaison SSL et de proxy HTTP ont été généralisés. Le déploiement se compose d’un seul jeu de réplicas MongoDB, dont un principal et deux secondaires.

![chlimage_1-4](assets/chlimage_1-4.png)

Un déploiement minimal nécessite trois instances `mongod` configurées en tant qu’ensemble de répliques. Une seule instance est choisie comme principale, les autres étant secondaires. Le choix est géré par `mongod`. Un disque local est associé à chaque instance. Pour que le cluster puisse supporter la charge, un débit minimal de 12 Mo par seconde avec plus de 3 000 opérations d’E/S par seconde (IOPS) est recommandé.

Les auteurs AEM sont connectés aux instances `mongod`, chaque auteur AEM se connectant aux trois instances `mongod`. Les écritures sont envoyées à l’instance principale et les lectures peuvent être lues depuis n’importe quelle instance. Le trafic est distribué en fonction de la charge par un Dispatcher sur l’une des principales instances de création d’AEM. Le magasin de données Oak est un `FileDataStore`. La surveillance de MongoDB est assurée par MMS ou MongoDB Ops Manager en fonction de l’emplacement du déploiement. Le niveau du système d’exploitation et la surveillance des journaux sont fournis par des solutions tierces telles que Splunk ou Ganglia.

Dans ce déploiement, tous les composants sont requis pour réussir l’implémentation. Tout composant manquant rend l’implémentation non fonctionnelle.

### Systèmes d’exploitation {#operating-systems}

Pour obtenir la liste des systèmes d’exploitation pris en charge par AEM 6, consultez la page [Exigences techniques](/help/sites-deploying/technical-requirements.md).

### Environnements {#environments}

Les environnements virtualisés sont pris en charge à condition que la communication soit bonne entre les différentes équipes techniques qui gèrent le projet. Cette prise en charge inclut l’équipe qui exécute AEM, l’équipe propriétaire du système d’exploitation et l’équipe gérant l’infrastructure virtualisée.

Les exigences particulières relatives à la capacité d’E/S des instances de MongoDB doivent être traitées par l’équipe gérant l’environnement virtualisé. Si le projet utilise un déploiement dans le cloud, tel qu’Amazon Web Services, les instances devront être configurées avec une capacité d’E/S et une cohérence suffisantes pour prendre en charge les instances de MongoDB. Dans le cas contraire, les processus de MongoDB et le référentiel Oak s’exécutent de manière non fiable et erratique.

Dans les environnements virtualisés, MongoDB nécessite des configurations d’E/S et de machine virtuelle spécifiques pour s’assurer que le moteur de stockage de MongoDB n’est pas paralysé par des politiques d’allocation de ressources VMWare. Une implémentation réussie garantit qu’il n’existe aucun obstacle entre les différentes équipes et que toutes sont connectées pour offrir les performances requises.

## Considérations matérielles {#hardware-considerations}

### Stockage {#storage}

Pour obtenir un débit de lecture et d’écriture optimal sans avoir à effectuer de mise à l’échelle horizontale prématurée, MongoDB a généralement besoin d’un stockage SSD ou d’un stockage avec des performances équivalentes au SSD.

### Mémoire RAM {#ram}

Les versions 2.6 et 3.0 de MongoDB qui utilisent le moteur de stockage MMAP nécessitent que le jeu de travail de la base de données et ses index correspondent à la mémoire RAM.

Une mémoire RAM insuffisante entraîne une dégradation importante des performances. La taille du jeu de travail et celle de la base de données dépendent largement de l’application. Bien que certaines estimations puissent être faites, le moyen le plus fiable de déterminer la quantité de RAM requise est de créer l’application AEM et de la tester en termes de charge.

Pour faciliter le processus de test de charge, le ratio suivant entre le jeu de travail et la taille totale de la base de données peut être supposé :

* 1:10 pour un stockage sur SSD
* 1:3 pour un stockage sur disque dur

Ces ratios signifient que, pour les déploiements sur SSD, 200 Go de RAM sont nécessaires pour une base de données de 2 To.

Bien que les mêmes limites s’appliquent au moteur de stockage WiredTiger dans MongoDB 3.0, la corrélation entre le jeu de travail, la RAM et les erreurs de page n’est pas si forte. WiredTiger n’utilise pas le mappage de mémoire de la même manière que le moteur de stockage MMAP.

>[!NOTE]
>
>Adobe recommande d’utiliser le moteur de stockage WiredTiger pour les déploiements d’AEM 6.1 qui utilisent MongoDB 3.0.

### Magasin de données {#data-store}

En raison des limitations du jeu de travail MongoDB, il est recommandé que le magasin de données soit indépendant de MongoDB. Dans la plupart des environnements, un `FileDataStore` utilisant un NAS disponible pour toutes les instances AEM doit être utilisé. Pour les cas où Amazon Web Services est utilisé, il existe également un `S3 DataStore`. Si, pour une raison quelconque, le magasin de données est conservé dans MongoDB, sa taille doit être ajoutée à la taille totale de la base de données et les calculs du jeu de travail doivent être ajustés en conséquence. Ce dimensionnement peut impliquer d’allouer plus de RAM pour maintenir les performances sans erreurs de page.

## Surveillance {#monitoring}

La surveillance est essentielle pour une implémentation réussie du projet. Avec suffisamment de connaissances, il est possible d’exécuter AEM sur MongoDB sans surveillance. Toutefois, les personnes possédant ces connaissances sont habituellement des ingénieures et des ingénieurs spécialisés dans chaque section du déploiement.

Ces connaissances spécialisées impliquent généralement un ingénieur ou une ingénieure en R&amp;D travaillant sur Apache Oak Core et une personne spécialisée sur MongoDB.

Sans surveillance à tous les niveaux, une connaissance approfondie de la base de code est nécessaire pour identifier les problèmes. Avec une surveillance en place et des conseils adaptés sur les principales statistiques, les équipes d’implémentation peuvent réagir de manière appropriée aux anomalies.

Bien qu’il soit possible d’utiliser des outils de ligne de commande pour obtenir un instantané rapide du fonctionnement d’un cluster, il s’avère presque impossible de le faire en temps réel sur de nombreux hôtes. Les outils de ligne de commande donnent rarement des informations d’historique au-delà de quelques minutes et ne permettent jamais la corrélation croisée entre différents types de mesures. Une brève période de synchronisation `mongod` en arrière-plan lente nécessite un effort manuel important pour corréler l’attente d’E/S ou des niveaux d’écriture excessifs à une ressource de stockage partagée d’une machine virtuelle apparemment non connectée.

### MongoDB Cloud Manager {#mongodb-cloud-manager}

MongoDB Cloud Manager est un service gratuit offert par MongoDB qui permet la surveillance et la gestion des instances de MongoDB. Il offre une visibilité en temps réel sur les performances et l’intégrité du cluster MongoDB. Il gère à la fois les instances hébergées dans le cloud et de manière privée, à condition que l’instance puisse atteindre le serveur de surveillance de Cloud Manager.

Il nécessite l’installation d’un agent sur l’instance MongoDB qui se connecte au serveur de surveillance. Il existe trois niveaux d’agent :

* Un agent d’automatisation qui peut entièrement automatiser tout ce qui se trouve sur le serveur MongoDB.
* Un agent de surveillance qui peut surveiller l’instance `mongod`.
* Un agent de sauvegarde qui peut effectuer des sauvegardes planifiées des données.

Bien que l’utilisation de Cloud Manager pour l’automatisation de la maintenance d’un cluster MongoDB simplifie la plupart des tâches de routine, il n’est pas requis et son utilisation pour la sauvegarde ne l’est pas non plus. En choisissant Cloud Manager pour la surveillance, la surveillance est toutefois requise.

Pour plus d’informations sur MongoDB Cloud Manager, consultez la [documentation de MongoDB](https://docs.cloud.mongodb.com/).

### MongoDB Ops Manager {#mongodb-ops-manager}

MongoDB Ops Manager est le même logiciel que MongoDB Cloud Manager. Une fois enregistré, Ops Manager peut être téléchargé et installé localement dans un centre de données privé ou sur tout autre PC portable ou de bureau. Il utilise une base de données MongoDB locale pour stocker les données et communique de la même manière que Cloud Manager avec les serveurs gérés. Si vous avez des politiques de sécurité qui interdisent un agent de surveillance, il faut utiliser MongoDB Ops Manager.

### Surveillance du système d’exploitation {#operating-system-monitoring}

La surveillance au niveau du système d’exploitation est requise pour exécuter un cluster MongoDB d’AEM.

Ganglia constitue un bon exemple de ce type de système et donne une idée de l’éventail et du niveau de détail des informations requises, qui vont au-delà des indicateurs de santé de base comme le processeur, la charge moyenne et l’espace disque disponible. Pour diagnostiquer les problèmes, des informations de niveau inférieur telles que les niveaux du pool d’entropie, l’attente E/S du processeur, les sockets à l’état FIN_WAIT2 sont requises.

### Agrégation des journaux {#log-aggregation}

Avec un cluster de plusieurs serveurs, l’agrégation centralisée des journaux est nécessaire pour un système de production. Des logiciels comme Splunk prennent en charge l’agrégation des journaux et permettent aux équipes d’analyser les comportements de l’application sans avoir à collecter manuellement les journaux.

## Listes de contrôle {#checklists}

Cette section décrit les différentes étapes à suivre pour vous assurer que vos déploiements AEM et MongoDB sont correctement configurés avant l’implémentation de votre projet.

### Réseau {#network}

1. Tout d’abord, assurez-vous que tous les hôtes ont une entrée DNS.
1. Tous les hôtes doivent pouvoir être résolus par leur entrée DNS à partir de tous les autres hôtes routables.
1. Tous les hôtes MongoDB sont routables à partir de tous les autres hôtes MongoDB d’un même cluster.
1. Les hôtes MongoDB peuvent acheminer des paquets vers MongoDB Cloud Manager et les autres serveurs de surveillance.
1. Les serveurs AEM peuvent acheminer des paquets vers tous les serveurs MongoDB.
1. La latence des paquets entre un serveur AEM et un serveur MongoDB est inférieure à deux millisecondes, sans perte de paquets et une distribution standard d’une milliseconde ou moins.
1. Assurez-vous qu’il n’y a pas plus de deux sauts entre un serveur AEM et un serveur MongoDB.
1. Il n’y a pas plus de deux sauts entre deux serveurs MongoDB.
1. Il n’existe aucun routeur supérieur à la couche 3 du modèle OSI entre les serveurs principaux (MongoDB ou AEM ou toute combinaison).
1. Si vous utilisez le troncage VLAN ou toute autre forme de tunneling réseau, ces derniers doivent être conformes aux contrôles de latence des paquets.

### Configuration AEM {#aem-configuration}

#### Configuration du magasin de nœuds {#node-store-configuration}

Les instances d’AEM doivent être configurées pour utiliser AEM avec MongoMK. La base de l’implémentation de MongoMK dans AEM est le magasin de nœuds de document.

Pour plus d’informations sur la configuration des magasins de nœuds, voir [Configuration des magasins de nœuds et de données dans AEM](/help/sites-deploying/data-store-config.md).

Vous trouverez ci-dessous un exemple de configuration du magasin de nœuds de document pour un déploiement MongoDB minimal :

```xml
# org.apache.jackrabbit.oak.plugins.document.DocumentNodeStoreService.config
#MongoDB server details
mongodburi=mongodb://aem:aempassword@mongodbserver1.customer.com:27000,mongodbserver2.customer.com:27000

#Name of MongoDB database to use
db=aem

#Store binaries in custom BlobStore for example, FileDataStore
customBlobStore=true

cache=2048
blobCacheSize=1024
```

Où :

* `mongodburi`
Le serveur MongoDB auquel AEM doit se connecter. Les connexions sont établies avec tous les membres connus de l’ensemble de répliques par défaut. Si MongoDB Cloud Manager est utilisé, la sécurité du serveur est activée. Par conséquent, la chaîne de connexion doit contenir un nom d’utilisateur et un mot de passe appropriés. Les versions non professionnelles de MongoDB prennent uniquement en charge l’authentification par nom d’utilisateur et mot de passe. Pour plus d’informations sur la syntaxe de la chaîne de connexion, consultez la [documentation](https://docs.mongodb.org/manual/reference/connection-string/).

* `db`
Le nom de la base de données. La valeur par défaut pour AEM est `aem-author`.

* `customBlobStore`
Si le déploiement stocke les fichiers binaires dans la base de données, ils feront partie du jeu de travail. Pour cette raison, il est conseillé de ne pas stocker de fichiers binaires dans MongoDB, en préférant une banque de données alternative telle qu’une `FileSystem` banque de données sur un NAS.

* `cache`
Taille du cache en Mo. Cet espace est réparti entre les différents caches utilisés dans la variable `DocumentNodeStore`. La valeur par défaut est 256 Mo. Toutefois, les performances de lecture Oak bénéficient d’un cache plus grand.

* `blobCacheSize`
Les blobs fréquemment utilisés peuvent être mis en cache par AEM pour éviter de les récupérer dans le magasin de données. Cela a un impact plus important sur les performances, en particulier lors du stockage des blobs dans la base de données MongoDB. Tous les magasins de données basés sur le système de fichiers bénéficient du cache disque au niveau du système d’exploitation.

#### Configuration du magasin de données {#data-store-configuration}

Le magasin de données sert à stocker des fichiers dont la taille dépasse un certain seuil. En dessous de ce seuil, les fichiers sont stockés en tant que propriétés dans le magasin de nœuds de document. Si le `MongoBlobStore` est utilisé, une collection dédiée est créée dans MongoDB pour stocker les blobs. Cette collection contribue au jeu de travail de l’instance `mongod` et requiert que `mongod` dispose de plus de RAM pour éviter les problèmes de performance. C’est pour cela que nous recommandons d’éviter d’utiliser le `MongoBlobStore` pour les déploiements d’exploitation et d’utiliser `FileDataStore` avec un NAS partagé entre toutes les instances AEM. Comme le cache au niveau du système d’exploitation est efficace pour gérer les fichiers, la taille minimale d’un fichier sur le disque doit être proche de la taille du bloc du disque. Cela permet de s’assurer que le système de fichiers est utilisé de manière efficace et que de nombreux petits documents ne contribuent pas excessivement au jeu de travail de l’instance `mongod`.

Voici une configuration classique de magasin de données pour un déploiement d’AEM minimal avec MongoDB : 

```xml
# org.apache.jackrabbit.oak.plugins.blob.datastore.FileDataStore.config
# The minimum size of an object that should be stored in this data store.
minRecordLength=4096
path=/datastore
maxCachedBinarySize=4096
cacheSizeInMB=128
```

Où :

* `minRecordLength`
Taille en octets. Les fichiers binaires inférieurs ou égaux à cette taille sont stockés dans le magasin de nœuds de document. Le contenu du fichier binaire est stocké à la place de l’ID du blob. Si les fichiers binaires sont supérieurs à cette taille, l’ID du fichier binaire est stocké en tant que propriété du document dans la collection de nœuds. Et le corps du binaire est stocké dans la variable `FileDataStore` sur le disque. La taille de bloc du système de fichiers est généralement de 4 096 octets.

* `path`
Chemin d’accès à la racine du magasin de données. Pour un déploiement MongoMK, il doit s’agir d’un système de fichiers partagé disponible pour toutes les instances AEM. Généralement, un serveur NAS (Network Attached Storage) est utilisé. Pour les déploiements cloud tels que Amazon Web Services, la variable `S3DataFileStore` est également disponible.

* `cacheSizeInMB`
Taille totale du cache des fichiers binaires en mégaoctets. Elle est utilisée pour mettre en cache des fichiers binaires inférieurs à la variable `maxCacheBinarySize` .

* `maxCachedBinarySize`
Taille maximale en octets d’un fichier binaire mis en cache dans le cache des fichiers binaires. Si un magasin de données basé sur un système de fichiers est utilisé, il n’est pas recommandé d’utiliser des valeurs élevées pour le cache du magasin de données, car les fichiers binaires sont déjà mis en cache par le système d’exploitation.

#### Désactiver l’indicateur de requête {#disabling-the-query-hint}

Il est recommandé de désactiver l’indice de requête envoyé avec toutes les requêtes en ajoutant la propriété . `-Doak.mongo.disableIndexHint=true` quand vous commencez à AEM. Cela garantit que MongoDB calcule l’index le plus approprié à utiliser en fonction des statistiques internes.

Si l’indicateur de requête n’est pas désactivé, l’optimisation des performances des index n’a aucun impact sur les performances d’AEM.

#### Activer le cache persistant pour MongoMK {#enable-persistent-cache-for-mongomk}

Il est recommandé d’activer une configuration de cache persistante pour les déploiements de MongoDB, afin de maximiser la vitesse pour les environnements présentant de hautes performances de lecture d’E/S. Pour plus d’informations, voir la [documentation Jackrabbit Oak](https://jackrabbit.apache.org/oak/docs/nodestore/persistent-cache.html).

## Optimisations du système d’exploitation MongoDB {#mongodb-operating-system-optimizations}

### Prise en charge du système d’exploitation {#operating-system-support}

MongoDB 2.6 utilise un moteur de stockage mappé en mémoire sensible à certains aspects de la gestion au niveau du système d’exploitation entre la mémoire RAM et le disque. Les performances de requête et de lecture de l’instance MongoDB reposent sur la possibilité d’éviter ou d’éliminer les opérations d’E/S lentes, souvent appelées erreurs de page. Ces erreurs de page s’appliquent en particulier au processus `mongod`. Ne les confondez pas avec les erreurs de page au niveau du système d’exploitation.

Pour un fonctionnement rapide, la base de données MongoDB ne doit accéder qu’aux données déjà dans la RAM. Les données auxquelles elle doit accéder sont composées d’index et de données. Cette collection d’index et de données est appelée « jeu de travail ». Lorsque le jeu de travail est plus volumineux que la RAM disponible, MongoDB doit paginer ces données à partir du disque, ce qui entraîne un coût d’E/S et évince d’autres données déjà en mémoire. Si cette éviction entraîne le rechargement des données à partir du disque, les erreurs de page dominent et les performances se dégradent. Lorsque le jeu de travail est dynamique et variable, d’autres erreurs de page sont générées pour prendre en charge les opérations.

MongoDB s’exécute sur plusieurs systèmes d’exploitation, notamment un large éventail de versions Linux®, Windows et macOS. Voir [https://docs.mongodb.com/manual/installation/#supported-platforms](https://docs.mongodb.com/manual/installation/#supported-platforms) pour plus d’informations. Selon le choix de votre système d’exploitation, MongoDB propose différentes recommandations au niveau du système d’exploitation. Ces dernières sont documentées à l’adresse [https://docs.mongodb.com/manual/administration/production-checklist-operations/#operating-system-configuration](https://docs.mongodb.com/manual/administration/production-checklist-operations/#operating-system-configuration) et résumées ici pour plus de commodité.

#### Linux® {#linux}

* Désactivez les paramètres Transparent Huge Pages et défragmentez. Voir [Paramètres Transparent Huge Pages](https://docs.mongodb.com/manual/tutorial/transparent-huge-pages/) pour plus d’informations.
* [Réglez les paramètres de lecture anticipée](https://docs.mongodb.com/manual/administration/production-notes/#readahead) sur les périphériques qui stockent vos fichiers de base de données afin que vous puissiez les adapter à votre cas d’utilisation.

   * Pour le moteur de stockage MMAPv1, si votre jeu de travail est plus volumineux que la RAM disponible et que le modèle d’accès aux documents est aléatoire, envisagez de réduire la lecture anticipée à 32 ou 16. Évaluez différents paramètres afin de trouver une valeur optimale qui optimise la mémoire résidente et réduit le nombre d’erreurs de page.
   * Pour le moteur de stockage WiredTiger, définissez la lecture anticipée sur 0, quel que soit le type de support de stockage (tournant, SSD, etc.). En règle générale, utilisez le paramètre de lecture anticipée recommandé à moins que les tests ne présentent un avantage mesurable, répétable et fiable dans une valeur de lecture anticipée plus élevée. La [prise en charge professionnelle de MongoDB](https://docs.mongodb.com/manual/administration/production-notes/#readahead) peut fournir des conseils sur les configurations de lecture anticipée non nulles.

* Désactivez l’outil optimisé si vous exécutez RHEL 7/CentOS 7 dans un environnement virtuel.
* Lorsque RHEL 7/CentOS 7 s’exécute dans un environnement virtuel, l’outil optimisé appelle automatiquement un profil de performance dérivé du débit de performances, qui définit automatiquement les paramètres de lecture anticipée à 4 Mo. Ce paramètre peut avoir un impact négatif sur les performances.
* Utilisez les planificateurs de disque noop ou de date limite pour les lecteurs SSD.
* Utilisez le planificateur de disque noop pour les lecteurs virtualisés dans les machines virtuelles invitées.
* Désactivez NUMA ou définissez `vm.zone_reclaim_mode` sur 0 et exécutez les instances [mongod](https://docs.mongodb.com/manual/administration/production-notes/#readahead) avec entrelacement des nœuds. Pour plus d’informations, voir [MongoDB and NUMA Hardware](https://docs.mongodb.com/manual/administration/production-notes/#readahead) (MongoDB et matériel NUMA).

* Ajustez les valeurs ulimit de votre matériel afin qu’elles correspondent à votre cas d’utilisation. Si plusieurs instances [mongod](https://docs.mongodb.com/manual/reference/program/mongod/#bin.mongod) ou [mongos](https://docs.mongodb.com/manual/reference/program/mongos/#bin.mongos) sont exécutées avec le même utilisateur ou la même utilisatrice, dimensionnez les valeurs ulimit en conséquence. Consultez la section [Paramètres ulimit sous UNIX®](https://docs.mongodb.com/manual/reference/ulimit/) pour plus d’informations.

* Utilisez noatime pour le point de montage [dbPath](https://docs.mongodb.com/manual/reference/configuration-options/#storage.dbPath).
* Configurez un nombre suffisant de handles de fichier (fs.file-max), une limite d’identifiants PID de noyau (kernel.pid_max) et un nombre maximal de threads par processus (kernel.threads-max) pour votre déploiement. Pour les systèmes volumineux, les valeurs suivantes constituent un bon point de départ :

   * fs.file-max : valeur définie sur 98000,
   * kernel.pid_max : valeur définie sur 64000,
   * andkernel.threads-max : valeur définie sur 64000.

* Assurez-vous que votre système dispose d’assez d’espace d’échange. Pour plus d’informations sur la quantité nécessaire, consultez la documentation de votre système d’exploitation.
* Assurez-vous que la valeur du message TCP keepalive par défaut du système est correctement définie. Une valeur de 300 offre souvent de meilleures performances pour les ensembles de répliques et les clusters partitionnés. Consultez l’article [La durée de TCP keepalive affecte-t-elle les déploiements de MongoDB ?](https://docs.mongodb.com/manual/faq/diagnostics/#faq-keepalive) dans les questions fréquentes pour obtenir plus d’informations.

#### Windows {#windows}

* Envisagez de désactiver les mises à jour « Heure du dernier accès » NTFS. Ce paramètre est analogue à la désactivation d’atime sur les systèmes de type Unix.

### WiredTiger {#wiredtiger}

Depuis MongoDB 3.2, le moteur de stockage par défaut pour MongoDB est le moteur de stockage WiredTiger. Grâce à ses fonctionnalités robustes et évolutives, ce moteur accepte les charges de travail générales des bases de données sans rechigner. Les sections suivantes décrivent ces fonctionnalités.

#### Simultanéité au niveau des documents {#document-level-concurrency}

WiredTiger utilise un contrôle de simultanéité au niveau des documents pour les opérations d’écriture. Par conséquent, plusieurs clientes et clients peuvent modifier simultanément différents documents d’une collection.

Pour la plupart des opérations de lecture et d’écriture, WiredTiger utilise un contrôle de simultanéité optimiste. WiredTiger utilise uniquement des verrous d’intention au niveau global, de la base de données et de la collection. Lorsque le moteur de stockage détecte des conflits entre deux opérations, l’une d’entre elles génère un conflit d’écriture, ce qui conduit MongoDB à réessayer l’opération de manière transparente. Certaines opérations globales, généralement des opérations de courte durée impliquant plusieurs bases de données, nécessitent toujours un verrou global à l’échelle de l’instance.

D’autres opérations, telles que l’abandon d’une collection, nécessitent toujours un verrou de base de données exclusif.

#### Instantanés et points de contrôle {#snapshots-and-checkpoints}

WiredTiger utilise la méthode MVCC (MultiVersion Concurrency Control). Au début d’une opération, WiredTiger fournit un instantané ponctuel des données à la transaction. Un instantané présente une vue cohérente des données en mémoire.

Lors d’une opération d’écriture sur le disque, WiredTiger écrit toutes les données de l’instantané de manière cohérente parmi tous les fichiers de données. Les données désormais [durables](https://docs.mongodb.com/manual/reference/glossary/#term-durable) font office de point de contrôle dans les fichiers de données. Le point de contrôle permet de s’assurer que les fichiers de données sont cohérents jusqu’au dernier point de contrôle inclus. En d’autres termes, les points de contrôle peuvent agir comme des points de récupération.

MongoDB configure WiredTiger de façon à créer des points de contrôle (c’est-à-dire écrire les données des instantanés sur le disque) à intervalles de 60 secondes ou de 2 Go de données de journal.

Lors de l’écriture d’un nouveau point de contrôle, le point de contrôle précédent est toujours valide. Ainsi, même si MongoDB s’arrête ou rencontre une erreur lors de l’écriture d’un nouveau point de contrôle, au redémarrage, MongoDB peut récupérer le dernier point de contrôle valide.

Le nouveau point de contrôle devient accessible et permanent lorsque le tableau des métadonnées de WiredTiger est automatiquement mis à jour pour faire référence au nouveau point de contrôle. Une fois le nouveau point de contrôle accessible, WiredTiger libère les pages des anciens points de contrôle.

En utilisant WiredTiger, même si la [journalisation](https://docs.mongodb.com/manual/reference/glossary/#term-durable) est désactivée, MongoDB peut récupérer le dernier point de contrôle. Toutefois, pour récupérer les modifications apportées après le dernier point de contrôle, activez la [journalisation](https://docs.mongodb.com/manual/core/wiredtiger/#storage-wiredtiger-journal).

#### Journal {#journal}

WiredTiger utilise une connexion des transactions à écriture anticipée parallèlement à des [points de contrôle](https://docs.mongodb.com/manual/core/wiredtiger/#storage-wiredtiger-checkpoints) pour garantir la durabilité des données.

Le journal de WiredTiger conserve toutes les modifications de données effectuées entre les points de contrôle. Si MongoDB se ferme entre les points de contrôle, il utilise le journal pour relire toutes les données modifiées depuis le dernier point de contrôle. Pour plus d’informations sur la fréquence à laquelle MongoDB écrit les données de journal sur le disque, voir [Processus de journalisation](https://docs.mongodb.com/manual/core/journaling/#journal-process).

Le journal WiredTiger est compressé à l’aide de la bibliothèque de compression [Snappy](https://docs.mongodb.com/manual/core/journaling/#journal-process). Pour spécifier un autre algorithme de compression ou aucune compression, utilisez le réglage [storage.wiredTiger.engineConfig.journalCompressor](https://docs.mongodb.com/manual/reference/configuration-options/#storage.wiredTiger.engineConfig.journalCompressor).

Voir [Journalisation avec WiredTiger](https://docs.mongodb.com/manual/core/journaling/#journaling-wiredtiger).

>[!NOTE]
>
>La taille minimale d’enregistrement du journal pour WiredTiger est de 128 octets. Si un enregistrement de journal est inférieur ou égal à 128 octets, il n’est pas compressé par WiredTiger.
>
>Vous pouvez désactiver la journalisation en définissant [storage.journal.enabled](https://docs.mongodb.com/manual/reference/configuration-options/#storage.journal.enabled) sur « false », ce qui peut alléger la charge de travail liée à la gestion du journal.
>
>Pour les instances [autonomes](https://docs.mongodb.com/manual/reference/glossary/#term-standalone), si vous n’utilisez pas le journal, vous perdez certaines modifications de données lorsque MongoDB se ferme de manière inattendue entre les points de contrôle. Pour les membres d’[ensembles de répliques](https://docs.mongodb.com/manual/reference/glossary/#term-replica-set), le processus de réplication peut fournir des garanties de durabilité suffisantes.

#### Compression {#compression}

Avec WiredTiger, MongoDB prend en charge la compression pour toutes les collections et tous les index. La compression réduit l’utilisation du stockage, mais l’utilisation du processeur augmente.

Par défaut, WiredTiger utilise la compression par bloc avec la bibliothèque de compression [snappy](https://docs.mongodb.com/manual/reference/glossary/#term-snappy) pour toutes les collections et la [compression par préfixe](https://docs.mongodb.com/manual/reference/glossary/#term-prefix-compression) pour tous les index.

Pour les collections, la compression par bloc avec [zlib](https://docs.mongodb.com/manual/reference/glossary/#term-zlib) est également disponible. Pour spécifier un autre algorithme de compression ou aucune compression, utilisez le réglage [storage.wiredTiger.collectionConfig.blockCompressor](https://docs.mongodb.com/manual/reference/glossary/#term-zlib).

Dans le cas des index, pour désactiver la [compression par préfixe](https://docs.mongodb.com/manual/reference/glossary/#term-prefix-compression), utilisez le paramètre [storage.wiredTiger.indexConfig.prefixCompression](https://docs.mongodb.com/manual/reference/configuration-options/#storage.wiredTiger.indexConfig.prefixCompression).

Les paramètres de compression peuvent également être configurés par collection et par index lors de la création de la collection et de l’index. Voir [Définition des options du moteur de stockage](https://docs.mongodb.com/manual/reference/method/db.createCollection/#create-collection-storage-engine-options) et l’option [storageEngine db.collection.createIndex()](https://docs.mongodb.com/manual/reference/method/db.collection.createIndex/#createindex-options).

Pour la plupart des charges de travail, les paramètres de compression par défaut équilibrent l’efficacité du stockage et les exigences de traitement.

Le journal WiredTiger est également compressé par défaut. Pour plus d’informations sur la compression des journaux, voir [Journal](https://docs.mongodb.com/manual/core/wiredtiger/#storage-wiredtiger-journal).

#### Utilisation de la mémoire {#memory-use}

Avec WiredTiger, MongoDB utilise le cache interne de WiredTiger et le cache du système de fichiers.

À partir de la version 3.4, le cache interne de WiredTiger utilise par défaut la plus grande de l’une des options suivantes :

* 50 % de RAM moins 1 Go, ou
* 256 Mo

Par défaut, WiredTiger utilise la compression par bloc Snappy pour toutes les collections et la compression par préfixe pour tous les index. Vous pouvez configurer les valeurs par défaut de compression à un niveau global ou par collection et par index lors de la création de la collection et de l’index.

Différentes représentations sont utilisées pour les données dans le cache interne de WiredTiger par rapport au format sur le disque :

* Les données du cache du système de fichiers sont identiques au format sur le disque, notamment les avantages de toute compression de fichiers de données. Le cache du système de fichiers est utilisé par le système d’exploitation pour réduire les E/S du disque.

Les index chargés dans le cache interne de WiredTiger ont une représentation des données différente du format sur le disque, mais peuvent toujours tirer parti de la compression par préfixe d’index pour réduire l’utilisation de la RAM.

La compression par préfixe d’index déduplique les préfixes courants à partir de champs indexés.

Les données de collection du cache interne de WiredTiger sont décompressées et utilisent une représentation différente du format sur le disque. La compression par bloc peut permettre d’importantes économies de stockage sur le disque, mais les données doivent être décompressées pour être manipulées par le serveur.

MongoDB utilise automatiquement toute la mémoire libre qui n’est pas utilisée par le cache de WiredTiger ou par d’autres processus via le cache du système de fichiers.

Pour ajuster la taille du cache interne de WiredTiger, voir [storage.wiredTiger.engineConfig.cacheSizeGB](https://docs.mongodb.com/manual/reference/configuration-options/#storage.wiredTiger.engineConfig.cacheSizeGB) et [--wiredTigerCacheSizeGB](https://docs.mongodb.com/manual/reference/program/mongod/#cmdoption-wiredtigercachesizegb). Évitez d’augmenter la taille du cache interne de WiredTiger au-dessus de sa valeur par défaut.

### NUMA {#numa}

Le NUMA (Non Uniform Memory Access) permet à un noyau de gérer la façon dont la mémoire est mappée aux cœurs du processeur. Bien que l’accès à la mémoire puisse être potentiellement plus rapide pour les cœurs grâce à un accès aux données requises, le NUMA interfère avec MMAP en introduisant une latence supplémentaire, car les lectures ne peuvent pas être prédites. Par conséquent, le NUMA doit être désactivé pour le processus `mongod` sur tous les systèmes d’exploitation performants.

Essentiellement, dans une architecture NUMA, la mémoire est connectée aux processeurs et les processeurs sont connectés à un bus. Dans une architecture SMP ou UMA, la mémoire est connectée au bus et partagée par les processeurs. Lorsqu’un thread alloue de la mémoire sur un processeur NUMA, il l’alloue selon une politique. Par défaut, la mémoire est allouée au processeur local du thread, sauf s’il n’y a pas de processeur libre. Dans ce cas, il utilise la mémoire d’un processeur libre à un coût plus élevé. Une fois allouée, la mémoire ne se déplace pas entre les processeurs. L’allocation est effectuée par une politique héritée du thread parent, c’est-à-dire le thread qui a démarré le processus.

Dans de nombreuses bases de données qui considèrent l’ordinateur comme une architecture de mémoire multi-cœurs uniforme, ce scénario entraîne d’abord le remplissage du processeur initial et ensuite le remplissage du processeur secondaire. C’est particulièrement vrai si un thread central est responsable de l’allocation des tampons mémoire. La solution consiste à modifier la politique NUMA du thread principal utilisé pour lancer le processus `mongod` en exécutant la commande suivante :

```shell
numactl --interleaved=all <mongod> -f config
```

Cette politique alloue la mémoire de manière séquentielle sur tous les nœuds de l’unité centrale, ce qui garantit une distribution égale sur tous les nœuds. Elle ne génère pas un accès le plus performant à la mémoire, contrairement aux systèmes dotés de plusieurs processeurs. Environ la moitié des opérations de mémoire sont plus lentes et sont exécutées sur le bus, mais `mongod` n’a pas été écrit pour cibler NUMA de manière optimale, il s’agit donc d’un compromis raisonnable.

### Problèmes liés à l’accès NUMA {#numa-issues}

Si le processus `mongod` est démarré à partir d’un emplacement autre que le dossier `/etc/init.d`, il est probable qu’il ne soit pas démarré avec une politique NUMA adéquate. En fonction de la politique par défaut, des problèmes peuvent survenir. Cela est dû au fait que les différents programmes d’installation des gestionnaires de packages de Linux® pour MongoDB installent également un service avec des fichiers de configuration situés dans `/etc/init.d` qui effectuent l’étape décrite ci-dessus. Si vous installez et exécutez MongoDB directement à partir d’une archive (`.tar.gz`), vous devrez exécuter manuellement mongod sous le processus `numactl`.

>[!NOTE]
>
>Pour plus d’informations sur les stratégies NUMA disponibles, consultez la [documentation numactl](https://linux.die.net/man/8/numactl).

Le processus MongoDB se comporte différemment selon les différentes politiques d’allocation :

```

```

* `-membind=<nodes>`
Alloue de la mémoire seulement sur les nœuds répertoriés. Mongod n’alloue pas de mémoire sur les nœuds répertoriés et ne peut pas utiliser toute la mémoire disponible.

* `-cpunodebind=<nodes>`
S’exécute uniquement sur les nœuds. Mongod ne s’exécute que sur les nœuds spécifiés et utilise exclusivement la mémoire disponible sur ces nœuds.

* `-physcpubind=<nodes>`
S’exécute uniquement sur les processeurs (cœurs) répertoriés. Mongod ne s’exécute que sur les processeurs répertoriés et n’utilise que la mémoire disponible sur ces processeurs.

* `--localalloc`
Alloue toujours de la mémoire sur le nœud actuel, mais utilise tous les nœuds sur lesquels le thread s’exécute. Si un thread effectue une allocation, seule la mémoire disponible pour ce processeur est utilisée.

* `--preferred=<node>`
Privilégie l’allocation à un nœud, mais revient à d’autres si le nœud préféré est saturé. Une notation relative pour définir un nœud peut être utilisée. En outre, les threads s’exécutent sur tous les nœuds.

Certaines des politiques peuvent entraîner une allocation inférieure à toute la RAM disponible au processus `mongod`. Contrairement à MySQL, MongoDB évite activement la pagination au niveau du système d’exploitation, et, par conséquent, le processus `mongod` peut bénéficier d’une quantité de mémoire disponible inférieure à celle apparemment disponible.

#### Permutation {#swapping}

En raison de la grande quantité de mémoire des bases de données, la permutation au niveau du système d’exploitation doit être désactivée. Par défaut, le processus MongoDB évite la permutation.

#### Systèmes de fichiers distants {#remote-filesystems}

Les systèmes de fichiers distants comme NFS ne sont pas recommandés pour les fichiers de données internes de MongoDB (fichiers de base de données de processus mongod), car ils induisent une latence trop importante. Ne pas confondre avec le système de fichiers partagé requis pour le stockage d’Oak Blob (FileDataStore), où NFS est recommandé.

#### Lecture anticipée {#read-ahead}

Réglez la lecture anticipée de sorte que lorsqu’une page est paginée en utilisant une lecture aléatoire, les blocs inutiles ne sont pas lus à partir du disque. De tels résultats signifient une consommation inutile de bande passante des E/S.

### Configuration requise pour Linux® {#linux-requirements}

#### Versions minimales du noyau {#minimum-kernel-versions}

* **2.6.23** pour les fichiers système `ext4`

* **2.6.25** pour les fichiers système `xfs`

#### Paramètres recommandés pour les disques de base de données {#recommended-settings-for-database-disks}

**Désactiver atime**

Il est recommandé de désactiver `atime` pour les disques qui contiennent les bases de données.

**Définir le planificateur de disque NOOP**

Procédez comme suit :

Tout d’abord, vérifiez le planificateur d’E/S défini en exécutant la commande suivante :

```shell
cat /sys/block/sdg/queue/scheduler
```

Si la réponse est `noop`, il n’y a rien d’autre à faire.

Si NOOP n’est pas le planificateur d’E/S configuré, vous pouvez le modifier en exécutant : 

```shell
echo noop > /sys/block/sdg/queue/scheduler
```

**Ajuster la valeur de lecture anticipée**

Il est recommandé d’utiliser la valeur 32 pour les disques sur lesquels s’exécutent les bases de données MongoDB. Cette valeur équivaut à 16 Ko. Vous pouvez la définir en exécutant les opérations suivantes :

```shell
sudo blockdev --setra <value> <device>
```

#### Activer NTP {#enable-ntp}

Vérifiez que NTP est installé et en cours d’exécution sur la machine hébergeant les bases de données MongoDB. Par exemple, vous pouvez l’installer en utilisant le gestionnaire de packages yum sur une machine CentOS :

```shell
sudo yum install ntp
```

Une fois le démon NTP installé et démarré correctement, vous pouvez vérifier le décalage horaire de votre serveur dans le fichier de dérive.

#### Désactiver Transparent Huge Pages {#disable-transparent-huge-pages}

Red Hat® Linux® utilise un algorithme de gestion de la mémoire appelé Transparent Huge Pages (THP). Il est recommandé de désactiver cette option si vous utilisez le système d’exploitation pour les charges de travail de la base de données.

Vous pouvez le désactiver en suivant la procédure ci-dessous :

1. Ouvrez le fichier `/etc/grub.conf` dans l’éditeur de texte de votre choix.
1. Ajoutez la ligne suivante au fichier grub.conf :

   ```xml
   transparent_hugepage=never
   ```

1. Enfin, vérifiez si le paramètre a été appliqué en exécutant :

   ```shell
   cat /sys/kernel/mm/redhat_transparent_hugepage/enabled
   ```

   Si THP est désactivé, la sortie de la commande ci-dessus doit être :

   ```xml
   always madvise [never]
   ```

>[!NOTE]
>
>Pour plus d’informations sur Transparent Huge Pages, consultez cet [article](https://access.redhat.com/solutions/46111).

#### Désactiver NUMA {#disable-numa}

Dans la plupart des installations où NUMA est activé, le démon MongoDB le désactive automatiquement s’il est exécuté en tant que service à partir du dossier `/etc/init.d`.

Si ce n’est pas le cas, vous pouvez désactiver NUMA au niveau de chaque processus. Pour le désactiver, exécutez les commandes suivantes :

```shell
numactl --interleave=all <path_to_process>
```

Où `<path_to_process>` est le chemin d’accès au processus mongod.

Ensuite, désactivez la récupération de zone en exécutant :

```shell
echo 0 > /proc/sys/vm/zone_reclaim_mode
```

#### Adapter les paramètres ulimit au processus mongod {#tweak-the-ulimit-settings-for-the-mongod-process}

Linux® permet un contrôle configurable de l’allocation des ressources via la commande `ulimit`. Cette configuration peut être effectuée par utilisateur ou utilisatrice ou par processus.

Il est recommandé de configurer ulimit pour le processus mongod en fonction des [Paramètres ulimit MongoDB recommandés](https://docs.mongodb.org/manual/reference/ulimit/#recommended-ulimit-settings).

#### Tester les performances d’E/S de MongoDB {#test-mongodb-i-o-performance}

MongoDB fournit un outil appelé `mongoperf` conçu pour tester les performances d’E/S. Il est conseillé de l’utiliser pour tester les performances de toutes les instances de MongoDB qui composent votre infrastructure.

Pour plus d’informations sur l’utilisation de `mongoperf`, consultez la [documentation MongoDB](https://docs.mongodb.org/manual/reference/program/mongoperf/).

>[!NOTE]
>
>`mongoperf` est un indicateur des performances de MongoDB sur la plateforme sur laquelle il est exécuté. Pour cette raison, les résultats ne doivent pas être considérés comme définitifs en ce qui concerne les performances d’un système d’exploitation.
>
>Pour des résultats de performances plus précis, vous pouvez exécuter des tests complémentaires avec l’outil Linux® `fio`.

**Tester les performances de lecture sur les machines virtuelles qui composent votre déploiement**

Après avoir installé l’outil, basculez vers le répertoire de base de données de MongoDB pour effectuer les tests. Ensuite, lancez le premier test en exécutant `mongoperf` avec la configuration suivante :

```shell
echo "{nThreads:32,fileSizeMB:1000,r:true}" | mongoperf
```

La sortie souhaitée devrait atteindre deux gigaoctets par seconde (2 Go/s) et 500 000 opérations d’E/S par seconde (IOPS) s’exécutant à 32 threads pour toutes les instances de MongoDB.

Exécutez un deuxième test, cette fois avec des fichiers mappés en mémoire, en définissant le paramètre `mmf:true` :

```shell
echo "{nThreads:32,fileSizeMB:1000,r:true,mmf:true}" | mongoperf
```

La sortie du second test devrait être considérablement plus élevée que la première, indiquant les performances du transfert mémoire.

>[!NOTE]
>
>Lorsque vous effectuez les tests, vérifiez les statistiques d’utilisation des E/S pour les machines virtuelles en question dans votre système de surveillance du système d’exploitation. Si elles indiquent des valeurs inférieures à 100 % pour les lectures d’E/S, il se peut qu’il y ait un problème avec votre machine virtuelle.

**Tester les performances d’écriture de l’instance MongoDB principale**

Ensuite, vérifiez les performances d’écriture d’E/S de l’instance MongoDB principale en exécutant `mongoperf` à partir du répertoire de base de données MongoDB avec les mêmes paramètres :

```shell
echo "{nThreads:32,fileSizeMB:1000,w:true}" | mongoperf
```

La sortie souhaitée doit être de 12 mégaoctets par seconde et atteindre environ 3 000 IOPS, avec peu de variation entre le nombre de threads.

## Étapes pour les environnements virtualisés {#steps-for-virtualised-environments}

### VMWare {#vmware}

Si vous utilisez VMWare ESX pour gérer et déployer vos environnements virtualisés, veillez à définir les paramétrages suivants à partir de la console ESX afin de prendre en charge les opérations de MongoDB :

1. Désactivez la création de bulle de mémoire.
1. Pré-allouez et réservez de la mémoire pour les machines virtuelles qui hébergent les bases de données de MongoDB.
1. Utilisez le contrôle d’E/S de stockage pour allouer suffisamment d’E/S au processus `mongod`.
1. Garantissez les ressources de processeur des machines hébergeant MongoDB en définissant la [réservation de processeur](https://docs.vmware.com/en/VMware-vSphere/7.0/com.vmware.vsphere.hostclient.doc/GUID-6C9023B2-3A8F-48EB-8A36-44E3D14958F6.html?hWord=N4IghgNiBc4RB7AxmALgUwAQGEAKBVTAJ3QGcEBXIpMkAXyA).

1. Envisagez d’utiliser des pilotes d’E/S ParaVirtual. Voir cet [article de la base de connaissances](https://kb.vmware.com/selfservice/microsites/search.do?language=en_US&amp;cmd=displayKC&amp;externalId=1010398).

### Amazon Web Services {#amazon-web-services}

Pour plus d’informations sur la configuration de MongoDB avec Amazon Web Services, consultez l’article [Configuration de l’intégration d’AWS](https://docs.cloud.mongodb.com/tutorial/configure-aws-settings/) sur le site Web de MongoDB.

## Sécurisation de MongoDB avant le déploiement {#securing-mongodb-before-deployment}

Voir cette publication sur le [déploiement sécurisé de MongoDB](https://blogs.adobe.com/security/2015/07/securely-deploying-mongodb-3-0.html) pour obtenir des conseils sur la manière de sécuriser la configuration de vos bases de données avant le déploiement.

## Dispatcher {#dispatcher}

### Choisir le système d’exploitation pour le Dispatcher {#choosing-the-operating-system-for-the-dispatcher}

Pour servir correctement votre déploiement MongoDB, le système d’exploitation qui héberge le Dispatcher doit exécuter **Apache httpd** **version 2.4 ou ultérieure.**

Assurez-vous également que toutes les bibliothèques utilisées dans votre version sont à jour afin de minimiser les risques de sécurité.

### Configuration du Dispatcher {#dispatcher-configuration}

Une configuration type de Dispatcher diffuse entre 10 et 20 fois plus de débit de requête d’une seule instance AEM.

Comme le Dispatcher est sans état, il peut être facilement redimensionné horizontalement. Dans certains cas, l’accès des auteurs et des autrices à certaines ressources doit être limité. Il est recommandé d’utiliser un Dispatcher avec les instances de création.

L’exécution d’AEM sans un Dispatcher nécessite que la terminaison SSL et l’équilibrage de la charge soient effectués par une autre application. Ceci est nécessaire car les sessions doivent avoir une affinité avec l’instance AEM sur laquelle elles ont été créées, concept connu sous le nom de « connexions persistantes ». Le but est de s’assurer que les mises à jour du contenu présentent un temps de latence minimal.

Consultez la [documentation du dispatcher](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/dispatcher.html?lang=fr) pour plus d’informations sur la façon de le configurer.

### Configuration supplémentaire {#additional-configuration}

#### Connexions persistantes {#sticky-connections}

Les connexions persistantes garantissent que les pages personnalisés et données de session d’un utilisateur sont toutes composées sur la même instance d’AEM. Ces données sont stockées sur l’instance, de sorte que les requêtes suivantes du même utilisateur ou de la même utilisatrice retournent à la même instance.

Il est recommandé d’activer les connexions persistantes pour toutes les requêtes de routage des couches internes vers les instances AEM, en encourageant les requêtes suivantes à atteindre la même instance AEM. Cela permet de minimiser la latence qui est autrement perceptible lorsque le contenu est mis à jour entre les instances.

#### Durée d’expritaion longue {#long-expires}

Par défaut, le contenu envoyé à partir d’un Dispatcher AEM comporte des en-têtes Last-Modified et ETag, sans indication de l’expiration du contenu. Ce flux permet de s’assurer que l’interface utilisateur obtient toujours la dernière version de la ressource. Cela signifie également que le navigateur effectue une opération GET pour voir si la ressource a changé. Par conséquent, cela peut entraîner plusieurs demandes auxquelles la réponse HTTP est 304 (non modifié), en fonction du chargement de la page. Pour les ressources qui n’expirent pas, la définition d’un en-tête Expires et la suppression des en-têtes Last-Modified et ETag entraînent la mise en cache du contenu. De plus, aucune autre demande de mise à jour n’est effectuée tant que la date de l’en-tête Expires n’est pas atteinte.

Toutefois, l’utilisation de cette méthode signifie qu’il n’existe aucun moyen raisonnable de provoquer l’expiration de la ressource dans le navigateur avant celle de l’en-tête Expires. Pour réduire ce workflow, HtmlClientLibraryManager peut être configuré pour utiliser des URL non modifiables pour les bibliothèques clientes.

Il est garanti que ces URL ne changent pas. Lorsque le corps de la ressource contenue dans l’URL est modifié, les modifications sont répercutées dans l’URL, ce qui garantit que le navigateur demandera la version correcte de la ressource.

La configuration par défaut ajoute un sélecteur au HtmlClientLibraryManager. En tant que sélecteur, la ressource est mise en cache dans le Dispatcher en conservant le sélecteur intact. Ce sélecteur peut également être utilisé pour garantir le comportement correct de l’expiration. Le sélecteur par défaut suit le motif `lc-.*?-lc`. Les directives de configuration Apache httpd suivantes garantissent que toutes les requêtes correspondant à ce motif sont traitées avec un délai d’expiration approprié.

```xml
Header set Expires "Tue, 20 Jan 2037 04:20:42 GMT" "expr=(%{REQUEST_STATUS} -eq 200) && (%{REQUEST_URI} =~ /.*lc-.*?-lc.*/)"
Header set Cache-Control "public, no-transform, max-age=267840000" "expr=(%{REQUEST_STATUS} -eq 200) && (%{REQUEST_URI} =~ /.*lc-.*?-lc.*/)"
Header unset ETag "expr=(%{REQUEST_STATUS} -eq 200) && (%{REQUEST_URI} =~ /.*lc-.*?-lc.*/)"
Header unset Last-Modified "expr=(%{REQUEST_STATUS} -eq 200) && (%{REQUEST_URI} =~ /.*lc-.*?-lc.*/)"
Header unset Pragma "expr=(%{REQUEST_STATUS} -eq 200) && (%{REQUEST_URI} =~ /.*lc-.*?-lc.*/)"
```

#### Sans reniflement {#no-sniff}

Lorsque le contenu est envoyé sans type de contenu, de nombreux navigateurs tentent de deviner le type de contenu en lisant les premiers octets du contenu. Cette méthode est appelée le « sniffing », ou reniflement. Le reniflement ouvre une vulnérabilité de sécurité, car les utilisateurs et utilisatrices qui peuvent écrire dans le référentiel peuvent charger du contenu malveillant sans type de contenu.

Pour cette raison, il est conseillé d’ajouter un en-tête `no-sniff` aux ressources utilisées par le Dispatcher. Cependant, le Dispatcher ne met pas en cache les en-têtes. Ainsi, le type de contenu d’un contenu diffusé à partir du système de fichiers local est déterminé par son extension, plutôt que par l’utilisation de l’en-tête content-type d’origine de son serveur AEM d’origine.

L’option sans reniflement peut être activée en toute sécurité si l’application web est connue pour ne jamais fournir de ressources mises en cache sans type de fichier.

Vous pouvez activer l’option sans reniflement de manière inclusive :

```xml
Header set X-Content-Type-Options "nosniff"
```

Elle peut également être activée de manière sélective :

```xml
RewriteCond %{REQUEST_URI} \.(?:js|jsonp)$ [OR]
RewriteCond %{QUERY_STRING} (callback|jsonp|cb)=\w+
RewriteRule .* - [E=jsonp_request:1]
Header set X-Content-Type-Options "nosniff"  env=jsonp_request
Header setifempty Content-Type application/javascript env=jsonp_request
```

#### Politique de sécurité du contenu {#content-security-policy}

Les paramètres du Dispatcher par défaut permettent de définir une politique de sécurité du contenu (CSP) ouverte. Ces paramètres permettent à une page de charger des ressources à partir de tous les domaines soumis aux politiques par défaut de la sandbox du navigateur.

Il est souhaitable de limiter l’emplacement de chargement des ressources pour éviter de charger du code dans le moteur JavaScript à partir de serveurs étrangers non approuvés ou non vérifiés.

La CSP permet d’affiner les politiques. Toutefois, dans une application complexe, les en-têtes CSP doivent être développés avec soin, car les politiques trop restrictives peuvent rompre certaines parties de l’interface utilisateur.

>[!NOTE]
>
>Pour plus d’informations sur son fonctionnement, voir [Page OWASP sur la politique de sécurité du contenu](https://owasp.deteact.com/cheat/cheatsheets/Content_Security_Policy_Cheat_Sheet.html).

### Dimensionnement {#sizing}

Pour plus d’informations sur le dimensionnement, voir [Instructions de dimensionnement du matériel](/help/managing/hardware-sizing-guidelines.md).

### Optimisation des performances de MongoDB {#mongodb-performance-optimization}

Pour obtenir des informations génériques sur les performances de MongoDB, voir [Analyse des performances de MongoDB](https://docs.mongodb.org/manual/administration/analyzing-mongodb-performance/).

## Limites connues {#known-limitations}

### Installations simultanées {#concurrent-installations}

MongoMK prend en charge l’utilisation simultanée de plusieurs instances d’AEM avec une seule base de données, mais ne prend pas en charge les installations simultanées.

Pour contourner ce problème, assurez-vous d’exécuter l’installation avec une seule personne membre et d’ajouter les autres à la fin de l’installation.

### Longueur du nom de page {#page-name-length}

Si AEM est exécuté sur un déploiement de gestionnaire de persistance MongoMK[, les noms de page sont limités à 150 caractères.](/help/sites-authoring/managing-pages.md)

>[!NOTE]
>
>Consultez la [documentation de MongoDB](https://docs.mongodb.com/manual/reference/limits/) pour vous familiariser avec les limites et les seuils connus de MongoDB.
