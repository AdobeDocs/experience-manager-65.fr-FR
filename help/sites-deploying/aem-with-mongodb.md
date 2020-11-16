---
title: AEM avec MongoDB
seo-title: AEM avec MongoDB
description: Découvrez les tâches nécessaires et points clés à prendre en compte pour réussir un déploiement d’AEM avec MongoDB.
seo-description: Découvrez les tâches nécessaires et points clés à prendre en compte pour réussir un déploiement d’AEM avec MongoDB.
uuid: 8028832d-10de-4811-a769-fab699c162ec
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: cd3b979f-53d4-4274-b4eb-a9533329192a
docset: aem65
translation-type: tm+mt
source-git-commit: 56006a1f49e4d357cd7ee44a4a1dd1af7189e70a
workflow-type: tm+mt
source-wordcount: '6513'
ht-degree: 92%

---


# AEM avec MongoDB{#aem-with-mongodb}

Cet article vise à parfaire les connaissances relatives aux tâches nécessaires et aux points clé à prendre en compte pour déployer correctement Adobe Experience Manager avec MongoDB.

Pour plus d’informations sur le déploiement, consultez la section [Déploiement et maintenance](/help/sites-deploying/deploy.md) de la documentation.

## Quand faut-il utiliser MongoDB avec AEM ?{#when-to-use-mongodb-with-aem}

MongoDB est généralement utilisé pour prendre en charge les déploiements Auteur d’AEM lorsque l’un des critères suivants est respecté :

* Plus de 1 000 utilisateurs uniques par jour
* Plus de 100 utilisateurs simultanés
* Importants volumes de modifications de page
* Importants déploiements ou activations

Les critères ci-dessus ne sont valables que pour des instances d’auteur et non pas pour des instances de publication qui doivent toutes être basées sur TarMK. Le nombre d’utilisateurs fait référence aux utilisateurs authentifiés, les instances d’auteur n’autorisant pas l’accès non authentifié.

Si les critères ne sont pas remplis, un déploiement TarMK actif/en mode attente est recommandé pour répondre aux impératifs de disponibilité. Généralement, MongoDB doit être envisagé dans les situations où les impératifs d’échelle sont supérieurs aux possibilités offertes par un seul composant matériel.

>[!NOTE]
>
>Des informations supplémentaires sur le dimensionnement des instances d’auteur et la définition des utilisateurs simultanés sont disponibles dans les [Conseils pour le dimensionnement du matériel](/help/managing/hardware-sizing-guidelines.md#authors-working-in-parallel).

### Déploiement minimal de MongoDB pour AEM {#minimal-mongodb-deployment-for-aem}

Voici un déploiement minimal pour AEM sur MongoDB. Par souci de simplicité, l’arrêt SSL et les composants proxy HTTP ont été généralisés. Il est constitué d&#39;un jeu de réplicas MongoDB unique, avec un Principal et deux secondes.

![chlimage_1-4](assets/chlimage_1-4.png)

Un déploiement minimal nécessite 3 instances `mongod` configurées en tant que jeu de réplicas. Une seule instance sera élue comme étant la principale et les autres instances les secondaires, l’élection étant gérée par `mongod`. Un disque local est associé à chaque instance. Pour que la grappe prenne en charge la charge, un débit minimal de 12 Mo/s avec plus de 3 000 opérations d&#39;E/S par seconde (E/S) est recommandé.

Les auteurs AEM sont connectés aux instances `mongod`, chaque auteur AEM se connectant aux trois instances `mongod`. Les écritures sont envoyées à l’instance principale et les lectures peuvent être lues depuis n’importe quelle instance. Le trafic est réparti en fonction de la charge par un dispatcher à l’une des instances d’auteur d’AEM actives. L’entrepôt de données OAK est un `FileDataStore`. La surveillance MongoDB est assurée par MMS ou MongoDB Ops Manager en fonction de l’emplacement du déploiement. La surveillance au niveau du système d’exploitation et des journaux est fournie par des solutions tierces telles que Splunk ou Ganglia.

Dans ce déploiement, tous les composants sont requis pour réussir l’implémentation. En l’absence d’un seul composant, l’implémentation échoue.

### Systèmes d’exploitation {#operating-systems}

Pour obtenir la liste des systèmes d’exploitation pris en charge par AEM 6, voir la page [Exigences techniques](/help/sites-deploying/technical-requirements.md).

### Environnements {#environments}

Les environnements virtualisés sont pris en charge à condition que la communication soit bonne entre les différentes équipes techniques qui gèrent le projet. Cela inclut l’équipe qui exécute AEM, l’équipe propriétaire du système d’exploitation et l’équipe gérant l’infrastructure virtualisée.

Les exigences particulières relatives à la capacité d’E/S des instances MongoDB doivent être traitées par l’équipe gérant l’environnement virtualisé. Si le projet utilise un déploiement dans le cloud, tel que Amazon Web Services, les instances devront être configurées avec une capacité d’E/S et une cohérence suffisantes pour prendre en charge les instances MongoDB. À défaut, les processus MongoDB et le référentiel Oak fonctionneront de façon irrégulière et instable.

Dans les environnements virtualisés, MongoDB nécessite des configurations d’E/S et de VM spécifiques pour s’assurer que le moteur de stockage de MongoDB n’est pas paralysé par des stratégies d’allocation de ressources VMWare. Une implémentation réussie fera tomber toutes les barrières entre les différentes équipes qui seront alors capables de délivrer la performance attendue.

## Considérations matérielles {#hardware-considerations}

### Stockage {#storage}

Afin d’atteindre le débit de lecture et d’écriture pour de meilleures performances sans avoir besoin d’un redimensionnement horizontal prématuré, MongoDB nécessite généralement un stockage SSD ou un stockage offrant des performances équivalentes au SSD.

### Mémoire RAM {#ram}

Les versions 2.6 et 3.0 de MongoDB qui utilisent le moteur de stockage MMAP requièrent que le jeu de travail de la base de données et ses index tiennent dans la mémoire RAM.

Une mémoire RAM insuffisante entraîne une dégradation importante des performances. La taille du jeu de travail et celle de la base de données dépendent largement de l’application. Si certaines estimations sont possibles, la manière la plus fiable de déterminer la quantité de RAM requise est de construire l’application AEM et de la tester avec une charge.

Pour faciliter le processus de test de charge, vous pouvez supposer que le ratio du jeu de travail par rapport à la taille totale de la base de données est le suivant :

* 1:10 pour un stockage SSD
* 1:3 pour un stockage sur disque dur

Cela signifie que, dans le cas de déploiements SSD, 200 Go de RAM sont nécessaires pour une base de données de 2 To. 

Bien que les mêmes limitations s’appliquent au moteur de stockage WiredTiger dans MongoDB 3.0, la corrélation entre le jeu de travail, la mémoire RAM et le nombre d’erreurs de page n’est pas aussi forte dans la mesure où WiredTiger n’utilise pas le mappage de mémoire comme le fait le moteur de stockage MMAP.

>[!NOTE]
>
>Adobe recommande d’utiliser le moteur de stockage WiredTiger pour les déploiements d’AEM 6.1 utilisant MongoDB 3.0.

### Entrepôt de données {#data-store}

En raison des limitations du jeu de travail MongoDB, il est fortement recommandé que l’entrepôt de données soit indépendant de MongoDB. Dans la plupart des environnements, un `FileDataStore` utilisant un NAS disponible pour toutes les instances AEM doit être utilisé. Pour les cas où Amazon Web Services est utilisé, il existe également un `S3 DataStore`. Si, pour une raison quelconque, l’entrepôt de données est conservé dans MongoDB, sa taille doit être ajoutée à la taille totale de la base de données et les calculs du jeu de travail doivent être ajustés en conséquence. Cela peut impliquer une configuration beaucoup plus importante de mémoire RAM pour conserver des performances sans erreurs de page.

## Surveillance {#monitoring}

La surveillance est indispensable pour réussir l’implémentation du projet. Bien que des connaissances suffisantes permettent d’exécuter AEM sur MongoDB sans surveillance, ce sont généralement les ingénieurs spécialisés pour chaque section du déploiement qui les possèdent.

Cela implique généralement un ingénieur R&amp;D chargé du noyau Apache Oak et un spécialiste MongoDB.

Sans surveillance à tous les niveaux, une connaissance détaillée de la base du code est nécessaire pour diagnostiquer les problèmes. Grâce à une surveillance effective et des conseils appropriés sur les principales statistiques, les équipes d’implémentation sont en mesure de réagir de manière appropriée face à des anomalies.

Bien qu’il soit possible d’utiliser des outils de ligne de commande pour obtenir un instantané rapide du fonctionnement d’un cluster, il est presque impossible de le faire en temps réel sur de nombreux hôtes. Les outils de ligne de commande donnent rarement des informations historiques au-delà de quelques minutes et ne permettent jamais la corrélation croisée entre différents types de mesures. Une brève période de lente synchronisation `mongod` en arrière-plan nécessite un effort manuel important pour corréler l’attente d’E/S ou des niveaux d’écriture excessifs à une ressource de stockage partagée d’une machine virtuelle apparemment non connectée.

### MongoDB Cloud Manager {#mongodb-cloud-manager}

MongoDB Cloud Manager est un service gratuit offert par MongoDB qui permet la surveillance et la gestion des instances de MongoDB. Il offre une visibilité en temps réel sur les performances et l’intégrité du cluster MongoDB. Il gère à la fois les instances hébergées en mode cloud et privé, à condition que l’instance puisse atteindre le serveur de surveillance Cloud Manager.

Il nécessite un agent installé sur l’instance MongoDB qui se connecte au serveur de surveillance. L’agent comporte trois niveaux :

* Un agent d’automatisation qui peut entièrement automatiser toutes les opérations sur le serveur MongoDB.
* Un agent de surveillance qui peut surveiller l’instance `mongod`.
* Un agent de sauvegarde qui peut effectuer des sauvegardes planifiées des données.

Bien que l’utilisation de Cloud Manager pour l’automatisation de la maintenance d’un cluster MongoDB simplifie la plupart des tâches de routine, il n’est pas requis et son utilisation pour la sauvegarde ne l’est pas non plus. Si vous choisissez Cloud Manager pour la surveillance, cette activité est toutefois requise.

Pour plus d’informations sur MongoDB Cloud Manager, consultez la [documentation de MongoDB](https://docs.cloud.mongodb.com/).

### MongoDB Ops Manager {#mongodb-ops-manager}

MongoDB Ops Manager est le même logiciel que MongoDB Cloud Manager. Une fois enregistré, Ops Manager peut être téléchargé et installé localement dans un centre de données privé ou sur tout autre PC portable ou de bureau. Il utilise une base de données MongoDB locale pour stocker les données et communiquer exactement de la même manière que Cloud Manager avec les serveurs gérés. Si certaines de vos stratégies de sécurité interdisent l’utilisation d’un agent de surveillance, MongoDB Ops Manager doit être utilisé à la place.

### Surveillance du système d’exploitation {#operating-system-monitoring}

La surveillance au niveau du système d’exploitation est requise pour exécuter un cluster AEM MongoDB.

Ganglia est un bon exemple d’un tel système. Il fournit une image de l’ampleur et du niveau de détail des informations requises au-delà des mesures simples d’intégrité du système comme le processeur, la charge moyenne et l’espace disque libre. Pour diagnostiquer les problèmes, des informations de niveau inférieur telles que les niveaux de pool d’entropie, l’attente d’E/S du processeur, les sockets à l’état FIN_WAIT2 sont requises.

### Agrégation de journaux {#log-aggregation}

Avec un cluster de plusieurs serveurs, une agrégation centrale des journaux est requise pour un système de production. Des logiciels comme Splunk prennent en charge l’agrégation de journaux et permettent aux équipes d’analyser les modèles de comportement de l’application sans devoir collecter manuellement les journaux.

## Listes de contrôle {#checklists}

Cette section traite des différentes étapes que vous devez suivre pour vous assurer que vos déploiements AEM et MongoDB sont correctement configurés avant l’implémentation de votre projet.

### Réseau {#network}

1. Tout d’abord, assurez-vous que tous les hôtes ont une entrée DNS
1. Tous les hôtes doivent pouvoir être résolus par leur entrée DNS à partir de tous les autres hôtes routables
1. Tous les hôtes MongoDB sont routables à partir de tous les autres hôtes MongoDB du même cluster
1. Les hôtes MongoDB peuvent router des paquets vers MongoDB Cloud Manager et les autres serveurs de surveillance
1. Les serveurs AEM peuvent router des paquets vers tous les serveurs MongoDB
1. La latence des paquets entre un serveur AEM et un serveur MongoDB est inférieure à deux millisecondes, sans perte de paquets et une distribution standard d’une milliseconde ou moins.
1. Assurez-vous qu’il existe moins de deux sauts entre un serveur AEM et un serveur MongoDB
1. Il existe moins de deux sauts entre deux serveurs MongoDB
1. Il n’y a pas de routeurs à un niveau plus élevé que le niveau OSI 3 parmi tous les serveurs principaux (MongoDB ou AEM ou toute combinaison).
1. Si le trunking VLAN ou une autre forme de tunnellisation réseau est utilisé, il doit être conforme aux contrôles de latence des paquets.

### Configuration d’AEM {#aem-configuration}

#### Configuration d’un magasin de nœuds {#node-store-configuration}

Les instances AEM doivent être configurées de manière à utiliser AEM avec MongoMK. La base de l’implémentation de MongoMK dans AEM est le magasin de nœuds de document.

Pour plus d’informations sur la configuration des magasins de nœuds, voir [Configuration des magasins de nœuds et des données dans AEM](/help/sites-deploying/data-store-config.md).

Voici un exemple de configuration du magasin de nœuds de document pour un déploiement MongoDB minimal :

```xml
# org.apache.jackrabbit.oak.plugins.document.DocumentNodeStoreService.config
#MongoDB server details
mongodburi=mongodb://aem:aempassword@mongodbserver1.customer.com:27000,mongodbserver2.customer.com:27000

#Name of MongoDB database to use
db=aem

#Store binaries in custom BlobStore e.g. FileDataStore
customBlobStore=true

cache=2048
blobCacheSize=1024
```

Où :

* `mongodburi`
serveur MongoDB auquel AEM doit se connecter. Les connexions sont établies avec tous les membres connus du jeu de réplicas par défaut. Si MongoDB Cloud Manager est utilisé, la sécurité du serveur est activée. Par conséquent, la chaîne de connexion doit contenir un nom d’utilisateur et un mot de passe appropriés. Les versions non professionnelles de MongoDB prennent uniquement en charge l’authentification par nom d’utilisateur et mot de passe. Pour plus d’informations sur la syntaxe de la chaîne de connexion, consultez la [documentation](https://docs.mongodb.org/manual/reference/connection-string/).

* `db`
nom de la base de données. Le par défaut pour AEM est 
`aem-author`.

* `customBlobStore`
si le déploiement stocke les fichiers binaires dans la base de données, ils feront partie du jeu de travail. Pour cette raison, il est conseillé de ne pas stocker de fichiers binaires dans MongoDB, en autorisant une autre banque de données comme une 
`FileSystem` banque de données sur un NAS.

* `cache`
Taille du cache en mégaoctets. Cette variable est répartie entre les différents caches utilisés dans la variable 
`DocumentNodeStore`. La valeur par défaut est 256 Mo. Cependant, les performances de lecture Oak bénéficieront d’un cache plus important.

* `blobCacheSize` les blobs fréquemment utilisés peuvent être mis en cache par AEM pour éviter qu’ils ne soient récupérés dans l’entrepôt de données. Cela améliorera les performances, en particulier lors du stockage des blobs dans la base de données MongoDB. Tous les entrepôts de données basés sur le système de fichiers bénéficieront du cache disque au niveau du système d’exploitation.

#### Configuration d’un entrepôt de données {#data-store-configuration}

L’entrepôt de données est utilisé pour stocker des fichiers d’une taille supérieure à un seuil. En dessous de ce seuil, les fichiers sont stockés en tant que propriétés dans le magasin de nœuds de document. Si le `MongoBlobStore` est utilisé, une collection dédiée est créée dans MongoDB pour stocker les blobs. Cette collection contribue au jeu de travail de l’instance `mongod` et requiert que `mongod` dispose de plus de RAM pour éviter les problèmes de performance. Pour cette raison, la configuration recommandée est d’éviter le `MongoBlobStore` pour les déploiements de production et d’utiliser `FileDataStore` conjointement à un NAS partagé entre toutes les instances AEM. Dans la mesure où le cache au niveau du système d’exploitation est efficace pour gérer les fichiers, la taille minimale d’un fichier sur le disque doit être proche de celle du disque afin que le système de fichiers soit utilisé efficacement et que de nombreux petits documents ne contribuent pas en excès au jeu de travail de l’instance `mongod`.

Voici une configuration classique d’entrepôt de données pour un déploiement d’AEM minimal avec MongoDB : 

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
Taille en octets. Les fichiers binaires inférieurs ou égaux à cette taille sont stockés dans le magasin de nœuds de document. Plutôt que de stocker l’ID du blob, le contenu du fichier binaire est stocké. Pour les binaires supérieurs à cette taille, l’ID du binaire est stocké en tant que propriété du Document dans la collection de noeuds et le corps du binaire est stocké dans la variable 
`FileDataStore` sur le disque. La taille de bloc du système de fichiers est généralement de 4 096 octets.

* `path`
chemin d’accès à la racine de l’entrepôt de données. Pour un déploiement MongoMK, il doit s’agir d’un système de fichiers partagé disponible pour toutes les instances AEM. Généralement, un serveur NAS (Network Attached Storage) est utilisé. Pour les déploiements de cloud tels que Amazon Web Services, la variable 
`S3DataFileStore` est également disponible.

* `cacheSizeInMB`
taille totale du cache des fichiers binaires en mégaoctets. Il est utilisé pour mettre en cache des binaires inférieurs à la variable 
`maxCacheBinarySize` définie.

* `maxCachedBinarySize`
taille maximale en octets d’un fichier binaire mis en cache dans le cache des fichiers binaires. Si un entrepôt de données basé sur un système de fichiers est utilisé, il n’est pas recommandé d’utiliser des valeurs élevées pour le cache de l’entrepôt de données car les fichiers binaires sont déjà mis en cache par le système d’exploitation.

#### Désactivation de l’indicateur de requête {#disabling-the-query-hint}

Il est recommandé de désactiver l’indicateur de requête envoyé avec toutes les requêtes en ajoutant la propriété

`-Doak.mongo.disableIndexHint=true`

lors du démarrage d’AEM. De cette façon, MongoDB effectue ses calculs sur l’index le plus approprié à utiliser en fonction des statistiques internes.

Si l’indicateur de requête n’est pas désactivé, toute optimisation des performances des index n’aura aucun impact sur les performances d’AEM.

#### Activation du cache permanent pour MongoMK {#enable-persistent-cache-for-mongomk}

Il est recommandé qu’une configuration de cache permanente soit activée pour les déploiements MongoDB, afin de maximiser la vitesse pour les environnements dont les performances de lecture E/S sont élevées. Pour plus d’informations, voir la [documentation Jackrabbit Oak](https://jackrabbit.apache.org/oak/docs/nodestore/persistent-cache.html).

## Optimisation du système d’exploitation pour MongoDB {#mongodb-operating-system-optimizations}

### Prise en charge du système d’exploitation {#operating-system-support}

MongoDB 2.6 utilise un moteur de stockage mappé en mémoire qui est sensible à certains aspects de la gestion au niveau du système d’exploitation entre la mémoire RAM et le disque. Les performances de requête et de lecture de l’instance MongoDB reposent sur l’évitement ou l’élimination des opérations d’E/S lentes souvent appelées « erreurs de page ». Ce sont des erreurs de page qui s’appliquent en particulier au processus `mongod`. Elles ne doivent pas être confondues avec les erreurs de page au niveau du système d’exploitation.

Pour un fonctionnement rapide, la base de données MongoDB doit uniquement accéder aux données déjà présentes en mémoire RAM. Les données auxquelles elle doit accéder sont composées d’index et de données. Cette collection d’index et de données est appelée « jeu de travail ». Lorsque le jeu de travail est supérieur à la RAM disponible, MongoDB doit paginer ces données à partir du disque, ce qui engendre un coût d’E/S et évince les autres données déjà en mémoire. Si l’éviction provoque le rechargement des données à partir du disque, les erreurs de page prédominent et les performances se dégradent. Lorsque le jeu de travail est dynamique et variable, les erreurs de page surviennent en plus grand nombre pour prendre en charge les opérations.

MongoDB s’exécute sur un certain nombre de systèmes d’exploitation, dont un large éventail de variantes Linux, Windows et Mac OS. Pour plus d’informations, voir [https://docs.mongodb.com/manual/installation/#supported-platforms](https://docs.mongodb.com/manual/installation/#supported-platforms). Sur le plan du système d’exploitation, les recommandations relatives à MongoDB varient en fonction de l’OS choisi. Ces recommandations sont documentées à l’adresse [https://docs.mongodb.com/manual/administration/production-checklist-operations/#operating-system-configuration](https://docs.mongodb.com/manual/administration/production-checklist-operations/#operating-system-configuration). Vous en trouverez un résumé ici pour plus de facilité.

#### Linux {#linux}

* Désactivez Transparent Huge Pages et Defrag. Pour plus d’informations, voir [Paramètres Transparent Huge Pages](https://docs.mongodb.com/manual/tutorial/transparent-huge-pages/).
* [Réglez les paramètres de lecture anticipée](https://docs.mongodb.com/manual/administration/production-notes/#readahead) sur les dispositifs où sont stockés vos fichiers de base de données en fonction de votre type d’utilisation.

   * Dans le cas du moteur de stockage MMAPv1, si la taille de votre jeu de travail est supérieure à la mémoire vive (RAM) disponible, et que le schéma d’accès au document est aléatoire, pensez à réduire la lecture anticipée de 32 à 16. Évaluez les différents paramètres afin de trouver une valeur optimale qui maximise la mémoire résidente et réduit le nombre de défauts de page.
   * Dans le cas du moteur de stockage WiredTiger, définissez le paramètre de lecture anticipée sur 0, quel que soit le type de support de stockage (rotatif, SSD, etc.). En règle générale, il est conseillé d’utiliser le paramètre de lecture anticipée par défaut, sauf si les tests font apparaître un avantage quantifiable, reproductible et fiable avec une valeur plus élevée. Le [service d’assistance professionnel de MongoDB](https://docs.mongodb.com/manual/administration/production-notes/#readahead) peut fournir des conseils sur les configurations de lecture anticipée non nulles.

* Désactivez l’outil optimisé si vous exécutez RHEL 7/CentOS 7 dans un environnement virtuel.
* En cas d’exécution de RHEL 7/CentOS 7 dans un environnement virtuel, l’outil optimisé appelle automatiquement un profil de performance dérivé des activités de performance, ce qui définit automatiquement les paramètres de lecture anticipée sur 4 Mo. Cela peut avoir une incidence négative sur les performances.
* Utilisez les planificateurs de disque noop ou deadline pour les lecteurs SSD.
* Utilisez le planificateur de disque noop pour les lecteurs virtualisés dans des machines virtuelles invitées.
* Désactivez NUMA ou définissez vm.zone_reclaim_mode sur 0 et exécutez les instances [mongod](https://docs.mongodb.com/manual/administration/production-notes/#readahead) avec l’entrelacement des nœuds. Pour plus d’informations, voir [ MongoDB and NUMA Hardware](https://docs.mongodb.com/manual/administration/production-notes/#readahead) (MongoDB et matériel NUMA).

* Réglez les valeurs ulimit sur votre matériel en fonction de votre type d’utilisation. Si plusieurs instances [ mongod](https://docs.mongodb.com/manual/reference/program/mongod/#bin.mongod) ou [mongos](https://docs.mongodb.com/manual/reference/program/mongos/#bin.mongos) sont exécutées avec le même utilisateur, dimensionnez les valeurs ulimit en conséquence. Pour plus d’informations, voir [UNIX ulimit Settings](https://docs.mongodb.com/manual/reference/ulimit/) (Paramètres ulimit UNIX).

* Utilisez noatime comme point de montage [dbPath](https://docs.mongodb.com/manual/reference/configuration-options/#storage.dbPath).
* Configurez suffisamment de descripteurs de fichiers (fs.file-max), de PID de noyau (kernel.pid_max) et de threads par processus (kernel.threads-max) pour votre déploiement. Pour les systèmes de grande taille, les valeurs suivantes constituent un bon point de départ :

   * valeur fs.file-max de 98000,
   * valeur kernel.pid_max de 64000,
   * valeur andkernel.threads-max de 64000.

* Assurez-vous qu’un espace d’échange est configuré sur votre système. Pour en savoir plus sur un dimensionnement approprié, consultez la documentation de votre système d’exploitation.
* Assurez-vous que la valeur TCP Keepalive par défaut du système est correctement définie. Une valeur de 300 garantit généralement de meilleures performances pour les jeux de réplicas et les clusters partitionnés. Pour plus d’informations, voir [Does TCP keepalive time affect MongoDB Deployments?](https://docs.mongodb.com/manual/faq/diagnostics/#faq-keepalive) (La valeur TCP keepalive affecte-t-elle les déploiements MongoDB ?) dans la section des questions fréquentes.

#### Windows {#windows}

* Envisagez de désactiver les mises à jour « Heure du dernier accès » NTFS. Cela revient à désactiver atime sur les systèmes de type Unix.

### WiredTiger {#wiredtiger}

Depuis MongoDB 3.2, le moteur de stockage par défaut de MongoDB est WiredTiger. Ce moteur fournit plusieurs fonctionnalités puissantes et évolutives, ce qui le rend beaucoup plus efficace pour les charges de travail de base de données polyvalentes. Ces fonctionnalités sont décrites dans les sections suivantes.

#### Accès simultané au niveau du document {#document-level-concurrency}

WiredTiger utilise un contrôle d’accès simultané au niveau du document pour les opérations d’écriture. De cette manière, plusieurs clients peuvent modifier, en même temps, différents documents d’une collection.

Pour la plupart des opérations de lecture et d’écriture, WiredTiger utilise un contrôle d’accès simultané optimiste. WiredTiger utilise uniquement des verrous intentionnels aux niveaux global, de la base de données et de la collection. Lorsque le moteur de stockage détecte des conflits entre deux opérations, l’une d’elles fait l’objet d’un conflit d’écriture et MongoDB tente alors de la relancer de manière transparente. Certaines opérations globales (généralement des opérations de courte durée impliquant plusieurs bases de données) nécessitent toutefois un verrou global « à l’échelle de l’instance ».

D’autres opérations (la suppression d’une collection, par exemple) nécessitent un verrou de base de données exclusif.

#### Instantanés et points de contrôle {#snapshots-and-checkpoints}

WiredTiger utilise un contrôle d’accès simultané multi-version (MVCC – MultiVersion Concurrency Control). Au début d’une opération, WiredTiger fournit un instantané ponctuel des données à la transaction. Cet instantané fournit une vue cohérente des données en mémoire.

Lors d’une opération d’écriture sur le disque, WiredTiger écrit toutes les données de l’instantané de manière cohérente parmi tous les fichiers de données. Les données désormais [durables](https://docs.mongodb.com/manual/reference/glossary/#term-durable) font office de point de contrôle dans les fichiers de données. Le point de contrôle garantit la cohérence des fichiers de données jusqu’au dernier point de contrôle (celui-ci inclus) ; en d’autres termes, les points de contrôle peuvent faire office de points de récupération.

MongoDB configure WiredTiger de manière à créer des points de contrôle (c’est-à-dire écrire les données d’instantané sur le disque) à intervalles de 60 secondes ou 2 Go de données de journal.

Le point de contrôle précédent reste valide pendant l’écriture d’un nouveau point de contrôle. Dès lors, même si MongoDB s’arrête ou rencontre une erreur lors de l’écriture d’un nouveau point de contrôle, il peut reprendre à partir du dernier point de contrôle valide.

Le nouveau point de contrôle devient accessible et permanent lorsque la table des métadonnées de WiredTiger est mise à jour de façon atomique pour y faire référence. Une fois le nouveau point de contrôle accessible, WiredTiger libère les pages des anciens points de contrôle.

Grâce à WiredTiger, MongoDB peut reprendre à partir du dernier point de contrôle, même sans [journalisation](https://docs.mongodb.com/manual/reference/glossary/#term-durable) ; cependant, pour récupérer les modifications effectuées après le dernier point de contrôle, veuillez l’exécuter avec la [journalisation](https://docs.mongodb.com/manual/core/wiredtiger/#storage-wiredtiger-journal).

#### Journal {#journal}

WiredTiger utilise un journal des transactions à écriture anticipée parallèlement à des [points de contrôle](https://docs.mongodb.com/manual/core/wiredtiger/#storage-wiredtiger-checkpoints) pour garantir la durabilité des données.

Le journal WiredTiger conserve toutes les modifications de données entre les points de contrôle. En cas de fermeture entre deux points de contrôle, MongoDB utilise le journal pour relire toutes les données modifiées depuis le dernier point de contrôle. Pour en savoir plus sur la fréquence à laquelle MongoDB écrit les données de journal sur le disque, voir [Processus de journalisation](https://docs.mongodb.com/manual/core/journaling/#journal-process).

Le journal WiredTiger est compressé à l’aide de la bibliothèque de compression [snappy](https://docs.mongodb.com/manual/core/journaling/#journal-process). Pour spécifier un autre algorithme de compression ou aucune compression, utilisez le paramètre [storage.wiredTiger.engineConfig.journalCompressor](https://docs.mongodb.com/manual/reference/configuration-options/#storage.wiredTiger.engineConfig.journalCompressor).

For more information see: [Journaling with WiredTiger](https://docs.mongodb.com/manual/core/journaling/#journaling-wiredtiger).

>[!NOTE]
>
>La taille d’enregistrement de journal minimale pour WiredTiger est de 128 octets. Si un enregistrement de journal a une taille inférieure ou égale à 128 octets, WiredTiger ne le compresse pas.
>
>Vous pouvez désactiver la journalisation en définissant [storage.journal.enabled](https://docs.mongodb.com/manual/reference/configuration-options/#storage.journal.enabled) sur « false », ce qui peut alléger la charge de travail liée à la gestion du journal.
>
>Dans le cas des instances [autonomes](https://docs.mongodb.com/manual/reference/glossary/#term-standalone), ne pas utiliser le journal signifie que vous perdrez des modifications de données en cas de fermeture inattendue de MongoDB entre deux points de contrôle. Pour les membres des [jeux de réplicas](https://docs.mongodb.com/manual/reference/glossary/#term-replica-set), le processus de réplication peut fournir des garanties suffisantes en matière de durabilité.

#### Compression {#compression}

Avec WiredTiger, MongoDB prend en charge la compression de l’ensemble des collections et des index. La compression réduit l’utilisation du stockage, mais sollicite davantage les ressources processeur.

Par défaut, WiredTiger utilise la compression par bloc avec la bibliothèque de compression [snappy](https://docs.mongodb.com/manual/reference/glossary/#term-snappy) pour toutes les collections et la [compression par préfixe](https://docs.mongodb.com/manual/reference/glossary/#term-prefix-compression) pour tous les index.

Pour les collections, la compression par bloc avec [zlib](https://docs.mongodb.com/manual/reference/glossary/#term-zlib) est également disponible. Pour spécifier un autre algorithme de compression ou aucune compression, utilisez le paramètre [storage.wiredTiger.collectionConfig.blockCompressor](https://docs.mongodb.com/manual/reference/glossary/#term-zlib).

Dans le cas des index, pour désactiver la [compression par préfixe](https://docs.mongodb.com/manual/reference/glossary/#term-prefix-compression), utilisez le paramètre [storage.wiredTiger.indexConfig.prefixCompression](https://docs.mongodb.com/manual/reference/configuration-options/#storage.wiredTiger.indexConfig.prefixCompression).

Les paramètres de compression peuvent également être configurés par collection et par index au cours de la création de ces éléments. Voir [Définition des options du moteur de stockage](https://docs.mongodb.com/manual/reference/method/db.createCollection/#create-collection-storage-engine-options) et l’option [db.collection.createIndex() storageEngine](https://docs.mongodb.com/manual/reference/method/db.collection.createIndex/#createindex-options).

Pour la plupart des charges de travail, les paramètres de compression par défaut constituent le compromis idéal entre efficacité du stockage et exigences de traitement.

Le journal WiredTiger est également compressé par défaut. Pour plus d’informations sur la compression du journal, voir [Journal](https://docs.mongodb.com/manual/core/wiredtiger/#storage-wiredtiger-journal).

#### Utilisation de la mémoire {#memory-use}

Avec WiredTiger, MongoDB utilise à la fois le cache interne de WiredTiger et le cache du système de fichiers.

Depuis la version 3.4, le cache interne de WiredTiger utilise, par défaut, le plus grand des deux éléments suivants :

* 50 % de la RAM moins 1 Go ou
* 256 Mo

Par défaut, WiredTiger utilise la compression par bloc Snappy pour toutes les collections et la compression par préfixe pour tous les index. Les paramètres de compression par défaut peuvent être configurés à un niveau global. Ils peuvent également être définis par collection et par index au cours de la création de ces éléments.

Des représentations différentes sont utilisées pour les données du cache interne WiredTiger par rapport au format sur le disque :

* Les données du cache du système de fichiers sont identiques à celles du format sur le disque, ce qui inclut les avantages de toute compression pour les fichiers de données. Le cache du système de fichiers est utilisé par le système d’exploitation pour réduire les E/S sur le disque.

Dans le cas des index chargés dans le cache interne de WiredTiger, la représentation des données est différente de celle du format sur le disque. Cependant, ils peuvent toujours tirer parti de la compression de préfixe d’index pour réduire l’utilisation de la mémoire vive.

La compression de préfixe d’index déduplique les préfixes communs des champs indexés.

Les données de collection du cache interne de WiredTiger ne sont pas compressées et utilisent une représentation différente de celle du format sur le disque. Avec la compression par bloc, il est possible de réaliser d’importantes économies sur le plan du stockage sur disque, mais les données ne doivent pas être compressées pour que le serveur puisse les traiter.

Via le cache du système de fichiers, MongoDB utilise automatiquement toute la mémoire libre qui n’est pas utilisée par le cache de WiredTiger ou par d’autres processus.

Pour régler la taille du cache interne de WiredTiger, voir [storage.wiredTiger.engineConfig.cacheSizeGB](https://docs.mongodb.com/manual/reference/configuration-options/#storage.wiredTiger.engineConfig.cacheSizeGB) et [--wiredTigerCacheSizeGB](https://docs.mongodb.com/manual/reference/program/mongod/#cmdoption-wiredtigercachesizegb). Évitez d’augmenter la taille du cache interne de WiredTiger au-delà de sa valeur par défaut.

### NUMA {#numa}

L’accès NUMA (Non Uniform Memory Access) permet à un noyau de gérer la façon dont la mémoire est mappée aux cœurs de processeur. Bien que l’accès à la mémoire puisse être potentiellement plus rapide pour les cœurs grâce à un accès aux données requises, NUMA interfère avec MMAP en induisant une latence supplémentaire car les lectures ne peuvent pas être prédites. Pour cette raison, NUMA doit être désactivé pour le processus `mongod` sur tous les systèmes d’exploitation qui dispose de cette fonctionnalité.

En substance, dans une architecture NUMA, la mémoire est connectée aux processeurs et les processeurs sont connectés à un bus. Dans une architecture SMP ou UMA, la mémoire est connectée au bus et partagée par les processeurs. Lorsqu’un thread alloue de la mémoire sur un processeur NUMA, il l’alloue en fonction d’une stratégie. La valeur par défaut est d’allouer de la mémoire associée au processeur local du thread sauf s’il n’y en n’a pas de libre, auquel cas le thread utilise la mémoire d’un processeur libre à un coût plus élevé. Une fois allouée, la mémoire n’est pas transférée entre les processeurs. L’allocation est effectuée par une stratégie héritée du thread parent, qui est en fin de compte le thread qui a démarré le processus.

Dans de nombreuses bases de données qui considèrent la machine comme une architecture de mémoire uniforme multi-cœur, le processeur initial est saturé en premier et le secondaire l’est ultérieurement, en particulier si un thread central est responsable de l’allocation des mémoires tampons. La solution est de modifier la stratégie NUMA du thread principal qui sert à démarrer le processus `mongod`.

La procédure consiste à exécuter la commande suivante :

```shell
numactl --interleaved=all <mongod> -f config
```

Cette stratégie alloue la mémoire de manière « tourniquet (round robin) » sur tous les nœuds du processeur, assurant ainsi une distribution uniforme sur tous les nœuds. Elle ne génère pas un accès le plus performant à la mémoire, contrairement aux systèmes dotés de plusieurs processeurs. Environ la moitié des opérations de mémoire seront plus lentes et seront exécutées sur le bus, mais `mongod` n’a pas été écrit pour cibler NUMA de manière optimale, donc le compromis est raisonnable.

### Problèmes liés à l’accès NUMA {#numa-issues}

If the `mongod` process is started from a location other than the `/etc/init.d` folder, it is probable that it will not be started with the correct NUMA policy. En fonction de la stratégie par défaut, des problèmes peuvent survenir. This is because the various Linux package manager installers for MongoDB also install a service with configuration files located in `/etc/init.d` which perform the step outlined above. If you install and run MongoDB directly from an archive ( `.tar.gz`) then you will need to manually run mongod under the `numactl` process.

>[!NOTE]
>
>Pour plus d’informations sur les stratégies NUMA disponibles, consultez la [documentation numactl](https://linux.die.net/man/8/numactl).

Le processus MongoDB se comporte différemment selon les différentes stratégies d’allocation : 

```

```

* `-membind=<nodes>`
Affectez uniquement les noeuds répertoriés. Mongod n’alloue pas de mémoire sur les nœuds répertoriés et ne peut pas utiliser toute la mémoire disponible.

* `-cpunodebind=<nodes>`
S’exécute uniquement sur les noeuds. Mongod s’exécute uniquement sur les nœuds spécifiés et utilise exclusivement la mémoire disponible sur ces nœuds.

* `-physcpubind=<nodes>`
S’exécute uniquement sur les CPU (coeurs) répertoriés. Mongod ne s’exécute que sur les processeurs répertoriés et n’utilise que la mémoire disponible sur ces processeurs.

* `--localalloc`
Affectez toujours de la mémoire au noeud actuel, mais utilisez tous les noeuds sur lesquels le thread s&#39;exécute. Si un thread effectue une allocation, seule la mémoire disponible pour ce processeur est utilisée.

* `--preferred=<node>`
privilégier l’allocation à un nœud, mais revenir à d’autres si le nœud préféré est saturé. Une notation relative pour définir un nœud peut être utilisée. En outre, les threads s’exécutent sur tous les nœuds.

Certaines des stratégies peuvent entraîner une allocation inférieure à toute la RAM disponible au processus `mongod`. Contrairement à MySQL, MongoDB évite activement la pagination au niveau du système d’exploitation, et, par conséquent, le processus `mongod` peut bénéficier d’une quantité de mémoire disponible inférieure à celle disponible.

#### Permutation {#swapping}

En raison de l’activité intensive des bases de données en termes de mémoire, la permutation au niveau du système d’exploitation doit être désactivée. Par défaut, le processus MongoDB évite la permutation.

#### Systèmes de fichiers distants {#remote-filesystems}

Les systèmes de fichiers distants tels que NFS ne sont pas recommandés pour les fichiers de données internes de MongoDB (les fichiers de base de données de processus mongod), car ils introduisent trop de latence. Ce type de système ne doit pas être confondu avec le système de fichiers partagé requis pour le stockage d’Oak Blob (FileDataStore), où NFS est recommandé.

#### Lecture anticipée {#read-ahead}

La lecture à l&#39;avance doit être réglée de sorte que lorsqu&#39;une page est paginée en utilisant une lecture aléatoire, les blocs inutiles ne sont pas lus à partir du disque, ce qui entraîne une consommation inutile de bande passante d&#39;E/S.

### Exigences Linux {#linux-requirements}

#### Versions minimales du noyau {#minimum-kernel-versions}

* **2.6.23** `ext4` pour les systèmes de fichiers

* **2.6.25** `xfs` pour les systèmes de fichiers

#### Paramètres recommandés pour les disques de base de données {#recommended-settings-for-database-disks}

**Désactiver atime**

Il est recommandé de désactiver `atime`pour les disques qui contiennent les bases de données.

**Définir le planificateur de disque NOOP**

Vous pouvez le faire en procédant comme suit :

Tout d’abord, vérifiez le planificateur d’E/S actuellement défini. La procédure consiste à exécuter la commande suivante :

```shell
cat /sys/block/sdg/queue/scheduler
```

Si la réponse est `noop`, vous n’avez rien à faire.

Si NOOP n’est pas le planificateur d’E/S configuré, vous pouvez le modifier en exécutant : 

```shell
echo noop > /sys/block/sdg/queue/scheduler
```

**Modifier la valeur de la lecture anticipée**

Il est recommandé d’utiliser une valeur égale à 32 pour les disques sur lesquels les bases de données MongoDB s’exécutent. Cela représente 16 kilo-octets. Vous pouvez le définir en exécutant :

```shell
sudo blockdev --setra <value> <device>
```

#### Activer NTP {#enable-ntp}

Assurez-vous que NTP est installé et en cours d’exécution sur la machine hébergeant les bases de données MongoDB. Par exemple, vous pouvez l’installer en utilisant le gestionnaire de modules yum sur une machine CentOS :

```shell
sudo yum install ntp
```

Une fois que le démon NTP a été installé et lancé avec succès, vous pouvez vérifier le fichier de dérive pour le décalage temporel de votre serveur.

#### Désactiver les pages THP {#disable-transparent-huge-pages}

Red Hat Linux utilise un algorithme de gestion de la mémoire appelé Transparent Huge Pages (THP). Il est recommandé de le désactiver si vous utilisez le système d’exploitation pour les charges de travail de base de données.

Vous pouvez le désactiver en suivant la procédure ci-dessous :

1. Open the `/etc/grub.conf` file in the text editor of your choice.
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

In most installations where NUMA is enabled, the MongoDB daemon will disable it automatically if it is run as a service from the `/etc/init.d` folder.

Si ce n’est pas le cas, vous pouvez désactiver NUMA au niveau de chaque processus. Pour le désactiver, exécutez les commandes suivantes :

```shell
numactl --interleave=all <path_to_process>
```

Where `<path_to_process>` is the path to the mongod process.

Ensuite, désactivez la récupération de zone en exécutant :

```shell
echo 0 > /proc/sys/vm/zone_reclaim_mode
```

#### Adapter les paramètres ulimit au processus mongod {#tweak-the-ulimit-settings-for-the-mongod-process}

Linux permet un contrôle configurable de l’allocation des ressources via la commande `ulimit`. Ce paramètre peut être défini par utilisateur ou par processus.

Il est recommandé de configurer ulimit pour le processus mongod selon les [Paramètres ulimit MongoDB recommandés](https://docs.mongodb.org/manual/reference/ulimit/#recommended-ulimit-settings).

#### Test des performances d’E/S de MongoDB {#test-mongodb-i-o-performance}

MongoDB fournit un outil appelé `mongoperf` conçu pour tester les performances d’E/S. Il est conseillé de l’utiliser pour tester les performances de toutes les instances de MongoDB qui composent votre infrastructure.

Pour plus d’informations sur l’utilisation de `mongoperf`, consultez la [documentation MongoDB](https://docs.mongodb.org/manual/reference/program/mongoperf/).

>[!NOTE]
>
>Notez que `mongoperf` est conçu pour être un indicateur des performances de MongoDB sur la plateforme sur laquelle il est exécuté. Pour cette raison, les résultats ne doivent pas être considérés comme définitifs en ce qui concerne les performances d’un système de production.
>
>Pour des résultats de performances plus précis, vous pouvez exécuter des tests complémentaires avec l’outil Linux `fio`.

**Tester les performances de lecture sur les machines virtuelles qui composent votre déploiement**

Après avoir installé l’outil, basculez vers le répertoire de base de données de MongoDB pour effectuer les tests. Ensuite, lancez le premier test en exécutant `mongoperf` avec la configuration suivante :

```shell
echo "{nThreads:32,fileSizeMB:1000,r:true}" | mongoperf
```

La sortie souhaitée devrait atteindre deux gigaoctets par seconde (2 Go/s) et 500 000 opérations d’E/S par seconde (IOPS) s’exécutant à 32 threads pour toutes les instances de MongoDB.

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

La sortie souhaitée devrait être de 12 mégaoctets par seconde et atteindre environ 3 000 IOPS, avec peu de variation dans le nombre de threads.

## Étapes à suivre pour les environnements virtualisés {#steps-for-virtualised-environments}

### VMWare {#vmware}

Si vous utilisez WMWare ESX pour gérer et déployer vos environnements virtualisés, veillez à effectuer les paramétrages suivants à partir de la console ESX afin de prendre en charge MongoDB :

1. Désactivez la création de bulle de mémoire
1. Pré-allouez et réservez de la mémoire pour les machines virtuelles qui hébergeront les bases de données de MongoDB
1. Utilisez le contrôle d’E/S de stockage pour allouer suffisamment d’E/S au processus `mongod`
1. Garantissez les ressources de processeur des machines hébergeant MongoDB en définissant la [réservation de processeur](https://pubs.vmware.com/vsphere-4-esx-vcenter/index.jsp?topic=/com.vmware.vsphere.vmadmin.doc_41/vsp_vm_guide/configuring_virtual_machines/t_allocate_cpu_resources.html)

1. Envisagez d’utiliser des pilotes d’E/S ParaVirtual. For more information on how to do this, check this [knowledgebase article](https://kb.vmware.com/selfservice/microsites/search.do?language=en_US&amp;cmd=displayKC&amp;externalId=1010398).

### Amazon Web Services {#amazon-web-services}

Pour plus d’informations sur la configuration de MongoDB avec Amazon Web Services, consultez l’article [Configure AWS Integration](https://docs.cloud.mongodb.com/tutorial/configure-aws-settings/) (Configuration de l’intégration AWS) sur le site web de MongoDB.

## Sécurisation de MongoDB avant le déploiement {#securing-mongodb-before-deployment}

Consultez cet article de blog sur le [déploiement sécurisé de MongoDB](https://blogs.adobe.com/security/2015/07/securely-deploying-mongodb-3-0.html) pour savoir comment sécuriser la configuration de vos bases de données avant le déploiement.

## Dispatcher {#dispatcher}

### Choix du système d’exploitation pour le dispatcher {#choosing-the-operating-system-for-the-dispatcher}

Afin de réaliser correctement votre déploiement MongoDB, le système d’exploitation qui hébergera le dispatcher doit exécuter **Apache httpd** **version 2.4 ou ultérieure.**

Assurez-vous également que toutes les bibliothèques utilisées dans votre build sont à jour afin de minimiser les risques de sécurité.

### Configuration du Dispatcher {#dispatcher-configuration}

Une configuration classique du dispatcher permet de délivrer entre dix et vingt fois plus de débit de requête pour une seule instance AEM.

Comme le dispatcher est principalement sans état, il peut être facilement redimensionné horizontalement. Dans certains déploiements, il faut interdire aux auteurs d’accéder à certaines ressources. Pour cette raison, il est fortement recommandé d’utiliser un dispatcher avec les instances d’auteur.

L’exécution d’AEM sans dispatcher requiert que l’arrêt SSL et l’équilibrage de charge soient réalisés par une autre application. Ceci est nécessaire car les sessions doivent avoir une affinité avec l’instance AEM sur laquelle elles ont été créées, concept connu sous le nom de « connexions persistantes ». Le but étant de garantir que les mises à jour du contenu présentent une latence minimale.

Consultez la [documentation du dispatcher](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher.html) pour plus d’informations sur la façon de le configurer.

### Configuration supplémentaire {#additional-configuration}

#### Connexions persistantes  {#sticky-connections}

Les connexions persistantes garantissent que les pages personnalisés et données de session d’un utilisateur sont toutes composées sur la même instance d’AEM. Ces données sont stockées sur l’instance, de sorte que les demandes ultérieures du même utilisateur retourneront à la même instance.

Il est recommandé d’activer les connexions persistantes pour toutes les demandes de routage des couches internes vers les instances AEM, en encourageant les demandes suivantes à atteindre la même instance AEM. Cela contribue à minimiser la latence qui est autrement perceptible lorsque le contenu est mis à jour entre les instances.

#### Long en-tête Expires {#long-expires}

Par défaut, le contenu envoyé à partir d’un dispatcher AEM comporte des en-têtes Last-Modified et Etag, sans indication de l’expiration du contenu. Même si cela garantit que l’interface utilisateur reçoit toujours la dernière version de la ressource, cela implique également que le navigateur exécute une opération GET pour vérifier si la ressource a changé. Cela peut entraîner plusieurs demandes auxquelles la réponse HTTP est 304 (non modifié), en fonction du chargement de la page. Pour les ressources qui ne sont pas arrivées à expiration, la définition d’un en-tête Expires et la suppression des en-têtes Last-Modified et ETag entraînent la mise en cache du contenu et aucune autre demande de mise à jour tant que la date de l’en-tête Expires n’est pas atteinte.

Toutefois, l’utilisation de cette méthode signifie qu’il n’existe aucun moyen raisonnable de provoquer l’expiration de la ressource dans le navigateur avant celle de l’en-tête Expires. Pour contourner ce problème, le HtmlClientLibraryManager peut être configuré de manière à utiliser des URL immuables pour les bibliothèques clients.

Ces URL ne changent absolument pas. Lorsque le corps de la ressource contenue dans l’URL est modifié, les modifications sont automatiquement répercutées dans l’URL, ce qui garantit que le navigateur demandera la version correcte de la ressource.

La configuration par défaut ajoute un sélecteur au HtmlClientLibraryManager. En tant que sélecteur, la ressource est mise en cache dans le dispatcher, le sélecteur restant intact. Ce sélecteur peut également être utilisé pour garantir le comportement normal de l’expiration. The default selector follows the `lc-.*?-lc` pattern. Les instructions de configuration Apache httpd suivantes garantissent que toutes les demandes correspondant à ce format sont honorées dans un délai d’expiration approprié.

```xml
Header set Expires "Tue, 20 Jan 2037 04:20:42 GMT" "expr=(%{REQUEST_STATUS} -eq 200) && (%{REQUEST_URI} =~ /.*lc-.*?-lc.*/)"
Header set Cache-Control "public, no-transform, max-age=267840000" "expr=(%{REQUEST_STATUS} -eq 200) && (%{REQUEST_URI} =~ /.*lc-.*?-lc.*/)"
Header unset ETag "expr=(%{REQUEST_STATUS} -eq 200) && (%{REQUEST_URI} =~ /.*lc-.*?-lc.*/)"
Header unset Last-Modified "expr=(%{REQUEST_STATUS} -eq 200) && (%{REQUEST_URI} =~ /.*lc-.*?-lc.*/)"
Header unset Pragma "expr=(%{REQUEST_STATUS} -eq 200) && (%{REQUEST_URI} =~ /.*lc-.*?-lc.*/)"
```

#### Pas de sniffing (nosniff){#no-sniff}

Lorsque le contenu est envoyé sans type de contenu (sans en-tête content-type), de nombreux navigateurs tentent de deviner le type de contenu en lisant les premiers octets du contenu. C’est ce que l’on appelle le « sniffing ». Le sniffing constitue une faille de sécurité car les utilisateurs qui peuvent écrire dans le référentiel peuvent aussi télécharger du contenu malveillant sans aucun type de contenu.

Pour cette raison, il est conseillé d’ajouter un en-tête `no-sniff` aux ressources utilisées par le dispatcher. Toutefois, le dispatcher ne met pas en cache les en-têtes. Cela signifie que le type de contenu d’un contenu issu du système de fichiers local sera déterminé par son extension, et non pas par l’utilisation de l’en-tête content-type d’origine de son serveur d’origine AEM.

L’en-tête nosniff peut être activé en toute sécurité si l’application web est connue pour ne jamais utiliser de ressources mises en cache sans type de fichier défini.

Vous pouvez activer nosniff inclusivement :

```xml
Header set X-Content-Type-Options "nosniff"
```

Il peut également être activé sélectivement :

```xml
RewriteCond %{REQUEST_URI} \.(?:js|jsonp)$ [OR]
RewriteCond %{QUERY_STRING} (callback|jsonp|cb)=\w+
RewriteRule .* - [E=jsonp_request:1]
Header set X-Content-Type-Options "nosniff"  env=jsonp_request
Header setifempty Content-Type application/javascript env=jsonp_request
```

#### Stratégie de sécurité du contenu {#content-security-policy}

Les paramètres du dispatcher par défaut permettent de définir une stratégie de sécurité du contenu (CSP) ouverte. Cela permet à une page de charger des ressources de tous les domaines soumis aux stratégies par défaut du sandbox du navigateur.

Il est souhaitable de restreindre l’emplacement où les ressources peuvent être chargées afin d’éviter de charger du code dans le moteur JavaScript à partir de serveurs étrangers non approuvés ou non vérifiés.

La stratégie de sécurité du contenu (CSP) permet d’affiner les stratégies. Cependant, dans une application complexe, les en-têtes CSP doivent être développés avec précaution, car les stratégies trop restrictives peuvent détériorer certaines parties de l’interface utilisateur.

>[!NOTE]
>
>Pour plus d’informations à ce sujet, voir la [page OWASP sur la stratégie de sécurité du contenu](https://www.owasp.org/index.php/Content_Security_Policy).

### Dimensionnement {#sizing}

Pour plus d’informations sur le dimensionnement, voir [Instructions de dimensionnement du matériel](/help/managing/hardware-sizing-guidelines.md).

### Optimisation des performances de MongoDB {#mongodb-performance-optimization}

Pour obtenir des informations génériques sur les performances de MongoDB, voir [Analyse des performances de MongoDB](https://docs.mongodb.org/manual/administration/analyzing-mongodb-performance/).

## Limites connues {#known-limitations}

### Installations simultanées {#concurrent-installations}

Bien que l’utilisation simultanée de plusieurs instances d’AEM avec une base de données unique soit prise en charge par MongoMK, les installations simultanées ne le sont pas.

Pour contourner ce problème, assurez-vous d’exécuter d’abord l’installation avec un seul membre et d’ajouter les autres à la fin de l’installation.

### Longueur du nom de page {#page-name-length}

If AEM is running on a MongoMK persistence manager deployment, [page names are limited to 150 characters.](/help/sites-authoring/managing-pages.md)

>[!NOTE]
>
>[Consultez la documentation](https://docs.mongodb.com/manual/reference/limits/) de MongoDB pour vous familiariser avec les limites et seuils connus de MongoDB lui-même.

