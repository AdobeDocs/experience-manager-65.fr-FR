---
title: Performance tuning for [!DNL Adobe Experience Manager Assets].
description: Suggestions et conseils [!DNL Experience Manager] sur la configuration, les modifications apportées au matériel, aux logiciels et aux composants réseau afin de supprimer les goulets d'étranglement et d'optimiser les performances [!DNL Experience Manager Assets].
contentOwner: AG
mini-toc-levels: 1
translation-type: tm+mt
source-git-commit: 566add37d6dd7efe22a99fc234ca42878f050aee
workflow-type: tm+mt
source-wordcount: '2723'
ht-degree: 55%

---


<!-- TBD: Get reviewed by engineering. -->

# [!DNL Adobe Experience Manager Assets] guide de réglage des performances {#assets-performance-tuning-guide}

Une [!DNL Experience Manager Assets] configuration contient plusieurs composants matériels, logiciels et réseau. Selon votre scénario de déploiement, vous pouvez avoir besoin d’apporter des modifications spécifiques à la configuration des composants matériels, logiciels et réseau pour supprimer les goulots d’étranglement en termes de performances.

In addition, identifying and adhering to certain hardware and software optimization guidelines helps build a sound foundation that enables your [!DNL Experience Manager Assets] deployment to meet expectations around performance, scalability, and reliability.

Poor performance in [!DNL Experience Manager Assets] can impact user experience around interactive performance, asset processing, download speed, and other areas.

En fait, l’optimisation des performances est une tâche essentielle que vous effectuez avant d’établir des mesures cibles pour chacun de vos projets.

Voici quelques éléments principaux essentiels pour lesquels vous devez identifier et corriger les problèmes de performances avant que ceux-ci aient un impact sur les utilisateurs.

## Plate-forme {#platform}

Bien que Experience Manager soit pris en charge sur plusieurs plates-formes, Adobe a trouvé la meilleure prise en charge des outils natifs sous Linux et Windows, ce qui contribue à des performances optimales et à la facilité d’implémentation. Ideally, you should deploy a 64-bit operating system to meet the high memory requirements of an [!DNL Experience Manager Assets] deployment. Comme pour tout déploiement d’Experience Manager, vous devez implémenter TarMK dans la mesure du possible. Bien que TarMK ne puisse pas mesurer au-delà d’une instance d’auteur simple, il semble offrir de meilleurs résultats que MongoMK. You can add TarMK offload instances to increase the workflow processing power of your [!DNL Experience Manager Assets] deployment.

### Dossier temporaire {#temp-folder}

Pour améliorer les temps de transfert des ressources, utilisez un enregistrement hautement performant pour le répertoire temporaire Java. Sous Linux et Windows, un disque SSD ou RAM peut être utilisé. Dans des environnements cloud, un type de stockage à grande vitesse équivalent peut être utilisé. For example in Amazon EC2, an [ephemeral drive](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/InstanceStorage.html) drive can be used for the temporary folder.

En supposant que le serveur dispose de suffisamment de mémoire, configurez un disque RAM. Sous Linux, exécutez les commandes suivantes pour créer un disque RAM de 8 Go :

```shell
mkfs -q /dev/ram1 800000
 mkdir -p /mnt/aem-tmp
 mount /dev/ram1 /mnt/aem-tmp
 df -H | grep aem-tmp
```

Sous Windows OS, utilisez un pilote tiers pour créer un lecteur RAM ou utilisez simplement un enregistrement hautes performances tel que SSD.

Once the high performance temporary volume is ready, set the JVM parameter `-Djava.io.tmpdir`. For example, you could add the JVM parameter below to the `CQ_JVM_OPTS` variable in the `bin/start` script of [!DNLExperience Manager]:

`-Djava.io.tmpdir=/mnt/aem-tmp`

## Configuration Java {#java-configuration}

### Version Java {#java-version}

Adobe recommande le déploiement [!DNL Experience Manager Assets] sur Java 8 pour des performances optimales.

>[!NOTE]
>
>Oracle a arrêté de publier les mises à jour de Java 7 à compter d&#39;avril 2015.

### Paramètres JVM    {#jvm-parameters}

Définissez les paramètres JVM suivants :

* `-XX:+UseConcMarkSweepGC`
* `-Doak.queryLimitInMemory`=500000
* `-Doak.queryLimitReads`=100000
* `-Dupdate.limit`=250000
* `-Doak.fastQuerySize`=true

## Configuration d’entrepôt de données et de mémoire {#data-store-and-memory-configuration}

### Configuration d’entrepôt de données basé sur les fichiers {#file-data-store-configuration}

Separating the data store from the segment store is recommended for all [!DNL Experience Manager Assets] users. En outre, la configuration des paramètres `maxCachedBinarySize` et `cacheSizeInMB` peut vous aider à optimiser les performances. Définissez le paramètre `maxCachedBinarySize` selon la plus petite taille de fichier pouvant être contenue dans le cache. Spécifiez la taille du cache en mémoire à utiliser pour l’entrepôt de données dans `cacheSizeInMB`. Adobe vous recommande de définir cette valeur entre 2 et 10 % de la taille totale du tas. Toutefois, le chargement ou le test des performances peuvent vous aider à déterminer le paramètre idéal.

### Configuration de la taille maximale du cache d’images mis en mémoire tampon    {#configure-the-maximum-size-of-the-buffered-image-cache}

When uploading large amounts of assets to [!DNLAdobe Experience Manager], to allow for unexpected spikes in memory consumption and to prevent JVM fails with OutOfMemoryErrors, reduce the configured maximum size of the buffered image cache. Prenez l’exemple d’un système présentant un tas maximal (paramètre -`Xmx`) de 5 Go, un BlobCache Oak défini sur 1 Go et un cache de documents défini sur 2 Go. Dans ce cas, le cache mis en mémoire tampon prendrait au maximum 1,25 Go, ce qui laisserait seulement 0,75 Go pour les pics inattendus.

Configurez la taille du cache mis en mémoire tampon dans la console web OSGi. À l’emplacement `https://host:port/system/console/configMgr/com.day.cq.dam.core.impl.cache.CQBufferedImageCache`, définissez la propriété `cq.dam.image.cache.max.memory` en octets. Par exemple, 1073741824 représente 1 Go (1 024 x 1 024 x 1 024 = 1 Go).

From Experience Manager 6.1 SP1, if you&#39;re using a `sling:osgiConfig` node for configuring this property, make sure to set the data type to Long. Pour plus de détails, voir [CQBufferedImageCache utilise le tas pendant le téléchargement des ressources](https://helpx.adobe.com/fr/experience-manager/kb/cqbufferedimagecache-consumes-heap-during-asset-uploads.html).

### Entrepôts de données partagés    {#shared-data-stores}

La mise en œuvre d’un entrepôt de données basé sur les fichiers, partagé ou S3, peut vous aider à économiser de l’espace disque et à augmenter le débit réseau dans des implémentations à grande échelle. For more information on the pros and cons of using a shared datastore, see [Assets sizing guide](/help/assets/assets-sizing-guide.md).

### Entrepôt de données S3 {#s-data-store}

La configuration de l’entrepôt de données S3 suivante (`org.apache.jackrabbit.oak.plugins.blob.datastore.S3DataStore.cfg`) a permis à Adobe d’extraire 12,8 To d’objets BLOB (Binary Large Objects) d’un entrepôt de données basé sur les fichiers existant dans un entrepôt de données S3 vers un site client :

```conf
accessKey=<snip>
 secretKey=<snip>
 s3Bucket=<snip>
 s3Region=us-standard
 s3EndPoint=<a href="https://s3.amazonaws.com/">s3.amazonaws.com</a>
 connectionTimeout=120000
 socketTimeout=120000
 maxConnections=80
 writeThreads=60
 concurrentUploadsThreads=30
 asyncUploadLimit=30
 maxErrorRetry=1000
 path=/opt/author/crx-quickstart/repository/datastore
 s3RenameKeys=false
 s3Encryption=SSE_S3
 proactiveCaching=true
 uploadRetries=1000
 migrateFailuresCount=400
```

## Optimisation du réseau {#network-optimization}

Adobe recommande d’activer HTTPS, car de nombreuses entreprises qui possèdent des pare-feu analysent le trafic HTTP, ce qui a une incidence sur les chargements et endommage les fichiers. Pour les chargements de fichiers volumineux, assurez-vous que les utilisateurs disposent d’une connexion filaire au réseau, car les réseaux Wi-Fi saturent rapidement. For guidelines on identifying network bottlenecks, see [Assets sizing guide](/help/assets/assets-sizing-guide.md). To assess network performance by analyzing network topology, see [Assets network considerations](/help/assets/assets-network-considerations.md).

Primarily, your network optimization strategy depends upon the amount of bandwidth available and the load on your [!DNLExperience Manager] instance. Les options de configuration courantes, notamment les pare-feu ou les proxys, peuvent améliorer les performances du réseau. Voici quelques points essentiels à prendre en compte :

* En fonction du type d’instance (petit, modéré, grand), veillez à disposer d’une bande passante réseau suffisante pour votre instance Experience Manager. Adequate bandwidth allocation is especially important if [!DNLExperience Manager] is hosted on AWS.
* If your [!DNLExperience Manager] instance is hosted on AWS, you can benefit by having a versatile scaling policy. Augmentez la taille de l’instance si les utilisateurs prévoient une charge élevée. Réduisez-la pour une charge moyenne/faible.
* HTTPS : la plupart des utilisateurs possèdent des pare-feu qui analysent le trafic HTTP, ce qui est susceptible d’avoir une incidence sur le chargement des fichiers ou même endommager des fichiers lors de l’opération de chargement.
* Chargements volumineux : assurez-vous que les utilisateurs disposent d’une connexion filaire au réseau (les connexions Wi-Fi sont rapidement saturées).

## Workflows {#workflows}

### Workflows transitoires {#transient-workflows}

Wherever possible, set the [!UICONTROL DAM Update Asset] workflow to Transient. Le paramètre réduit considérablement les surcharges nécessaires pour traiter les workflows car, dans ce cas, ils n’ont pas besoin de faire l’objet d’un suivi et de processus d’archivage classiques.

1. Accédez à `/miscadmin` l’instance [!DNLEExperience Manager] à `https://[aem_server]:[port]/miscadmin`.

1. Développez **[!UICONTROL Outils]** > **[!UICONTROL Workflow]** > **[!UICONTROL Modèles]** > **[!UICONTROL dam.]**

1. Open **[!UICONTROL DAM Update Asset]**. Depuis le panneau d’outils flottant, basculez vers l’onglet **[!UICONTROL Page]**, puis cliquez sur **[!UICONTROL Propriétés de la page]**.

1. Select **[!UICONTROL Transient Workflow]** and click **[!UICONTROL OK]**.

   >[!NOTE]
   >
   >Certaines fonctions ne prennent pas en charge les workflows transitoires. If your [!DNL Assets] deployment requires these features, do not configure transient workflows.

In cases where transient workflows cannot be used, run workflow purging regularly to delete archived [!UICONTROL DAM Update Asset] workflows to ensure system performance does not degrade.

En règle générale, exécutez les workflows de purge sur une base hebdomadaire. Cependant, dans les scénarios à forte intensité de ressources, comme lors de l’assimilation à grande échelle d’actifs, vous pouvez l’exécuter plus fréquemment.

Pour configurer la purge des workflows, ajoutez une nouvelle configuration de purge de workflow d’Adobe Granite via la console OSGi. Configurez et planifiez ensuite le workflow dans le cadre de la période de maintenance hebdomadaire.

Si la purge s’exécute trop longtemps, elle s’arrête. Par conséquent, vous devez vous assurer que vos tâches de purge se terminent pour éviter les cas où l’exécution de la purge des workflows échoue en raison du nombre élevé de workflows.

For example, after executing numerous non-transient workflows (that creates workflow instance nodes), you can execute [ACS AEM Commons Workflow Remover](https://adobe-consulting-services.github.io/acs-aem-commons/features/workflow-remover.html) on an ad-hoc basis. Il supprime les instances de workflow terminées et redondantes immédiatement sans attendre l’exécution du planificateur de purge de workflow d’Adobe Granite.

### Tâches parallèles maximales    {#maximum-parallel-jobs}

By default, [!DNLExperience Manager] runs a maximum number of parallel jobs equal to the number of processors on the server. The problem with this setting is that during periods of heavy load, all of the processors are occupied by [!UICONTROL DAM Update Asset] workflows, slowing down UI responsiveness and preventing [!DNLExperience Manager] from running other processes that safeguard server performance and stability. En tant que bonne pratique, définissez cette valeur sur la moitié des processeurs disponibles sur le serveur en procédant comme suit :

1. Dans [!DNLEExperience Manager] Author, accédez à `https://[aem_server]:[port]/system/console/slingevent`.

1. Click **[!UICONTROL Edit]** on each workflow queue that is relevant to your implementation, for example **[!UICONTROL Granite Transient Workflow Queue]**.

1. Update the value of **[!UICONTROL Maximum Parallel Jobs]** and click **[!UICONTROL Save]**.

Configurer une file d’attente à la moitié des processeurs disponibles est une solution exploitable pour commencer. Cependant, vous pouvez être amené à augmenter ou à réduire ce nombre pour atteindre un débit maximal et l’ajuster selon l’environnement. Il existe des files d’attente distinctes pour les workflows transitoires et non transitoires, ainsi que d’autres processus, tels que les workflows externes. Si plusieurs files d’attente configurées à 50 % des processeurs sont activées simultanément, le système peut devenir rapidement surchargé. Les files d’attente utilisées varient considérablement selon les différentes implémentations de l’utilisateur. Par conséquent, vous devrez peut-être les configurer de manière réfléchie pour un maximum d’efficacité sans sacrifier la stabilité des serveurs.

### Configuration des ressources de mise à jour de gestion des ressources numériques {#dam-update-asset-configuration}

The [!UICONTROL DAM Update Asset] workflow contains a full suite of steps that are configured for tasks, such as Scene7 PTIFF generation and [!DNL Adobe InDesign Server] integration. Cependant, plusieurs de ces étapes peuvent être inutiles à la plupart des utilisateurs. Adobe recommends you create a custom copy of the [!UICONTROL DAM Update Asset] workflow model, and remove any unnecessary steps. In this case, update the launchers for [!UICONTROL DAM Update Asset] to point to the new model.

Running the [!UICONTROL DAM Update Asset] workflow intensively can sharply increase the size of your file datatastore. Les résultats d’un test effectué par Adobe ont montré que la taille de l’entrepôt de données peut augmenter d’environ 400 Go si environ 5 500 workflows sont exécutés pendant une période de 8 heures.

Il s’agit d’une augmentation temporaire ; l’entrepôt de données est restauré à sa taille d’origine après avoir exécuté la tâche Nettoyage de la mémoire d’entrepôt de données.

En règle générale, la tâche Nettoyage de la mémoire d’entrepôt de données s’exécute chaque semaine avec d’autres tâches de maintenance planifiées.

If you have a limited disk space and run [!UICONTROL DAM Update Asset] workflows intensively, consider scheduling the garbage collection task more frequently.

#### Génération de rendus au moment de l’exécution {#runtime-rendition-generation}

Les clients utilisent des images de tailles et de formats différents sur leur site web ou pour les distribuer à leurs partenaires professionnels. Étant donné que chaque rendu s’ajoute à l’encombrement d’une ressource dans le référentiel, Adobe recommande d’utiliser cette fonction judicieusement. Pour limiter le nombre de ressources nécessaires pour traiter et stocker des images, vous pouvez générer ces images au moment de l’exécution plutôt que comme rendus pendant l’assimilation.

De nombreux clients de sites mettent en œuvre un servlet d’image qui redimensionne ou recadre les images lorsque cela est nécessaire, ce qui a pour effet d’appliquer une charge supplémentaire à l’instance de publication. Toutefois, tant que ces images peuvent être mises en cache, le défi peut être plus facilement relevé.

Une autre méthode consiste à utiliser la technologie Scene7 pour transférer entièrement la manipulation de l’image. Additionally, you can deploy Brand Portal that not only takes over rendition generation responsibilities from the [!DNLExperience Manager] infrastructure, but also the entire publish tier.

#### ImageMagick {#imagemagick}

If you customize the [!UICONTROL DAM Update Asset] workflow to generate renditions using ImageMagick, Adobe recommends you modify the `policy.xml` file at `/etc/ImageMagick/`. Par défaut, ImageMagick utilise l’espace disque disponible entier pour le volume du système d’exploitation et la quantité de mémoire disponible. Make the following configuration changes within the `policymap` section of `policy.xml` to limit these resources.

```xml
<policymap>
  <!-- <policy domain="system" name="precision" value="6"/> -->
  <policy domain="resource" name="temporary-path" value="/ephemeral0/imagemagick_tmp"/>
  <policy domain="resource" name="memory" value="1000MiB"/>
  <policy domain="resource" name="map" value="1000MiB"/>
  <!-- <policy domain="resource" name="area" value="1gb"/> -->
  <policy domain="resource" name="disk" value="10000MiB"/>
  <!-- <policy domain="resource" name="file" value="768"/> -->
  <policy domain="resource" name="thread" value="1"/>
  <policy domain="resource" name="throttle" value="50"/>
  <!-- <policy domain="resource" name="time" value="3600"/> -->
</policymap>
```

En outre, définissez le chemin du dossier temporaire d’ImageMagick dans le fichier `configure.xml` (ou en définissant la variable d’environnement `MAGIC_TEMPORARY_PATH`) sur une partition de disque disposant d’un espace et d’IOPS appropriés.

>[!CAUTION]
>
>Une configuration incorrecte peut rendre votre serveur instable si ImageMagick utilise tout l’espace disque disponible. The policy changes required to process large files using ImageMagick may impact the [!DNLExperience Manager] performance. Pour plus d’informations, voir [Installation et configuration d’ImageMagick](/help/assets/best-practices-for-imagemagick.md).

>[!NOTE]
>
>Les fichiers `policy.xml` et ImageMagick sont disponibles à la `configure.xml` place de `/usr/lib64/ImageMagick-&#42;/config/` .Voir la documentation `/etc/ImageMagick/`[](https://www.imagemagick.org/script/resources.php) ImageMagick pour connaître l’emplacement des fichiers de configuration.

If you are using [!DNL Experience Manager] on Adobe Managed Services (AMS), reach out to Adobe Customer Care if you plan to process lots of large PSD or PSB files. Adressez-vous au représentant du service à la clientèle d’Adobe pour mettre en oeuvre ces meilleures pratiques pour votre déploiement AMS et choisir les meilleurs outils et modèles possibles pour les formats propriétaires d’Adobe. [!DNL Experience Manager] peut ne pas traiter de fichiers PSB très haute résolution de plus de 3 000 x 2 3 000 pixels.

### Écriture différée XMP {#xmp-writeback}

XMP writeback updates the original asset whenever metadata is modified in [!DNL Experience Manager], which results in the following:

* La ressource elle-même est modifiée
* Une version de la ressource est créée
* [!UICONTROL Ressource de mise à jour de gestion des actifs numériques est exécuté par rapport à la ressource]

Les résultats répertoriés consomment une grande quantité de ressources. Par conséquent, Adobe recommande la [désactivation de l’écriture différée XMP](https://helpx.adobe.com/fr/experience-manager/kb/disable-xmp-writeback.html), si cela n’est pas obligatoire.

L’importation d’une grande quantité de métadonnées peut entraîner une activité d’écriture différée XMP gourmande en ressources si l’indicateur d’exécution de workflow est vérifié. Planifiez une importation de ce type quand le serveur est peu utilisé afin que les performances d’autres utilisateurs ne soient pas affectées.

## Réplication {#replication}

Lors de la réplication des ressources vers un grand nombre d’instances de publication (par exemple, dans une implémentation de sites), Adobe vous recommande d’utiliser la réplication par chaîne. Dans ce cas, l’instance d’auteur est répliquée vers une instance de publication unique qui est répliquée à son tour vers d’autres instances de publication, ce qui libère l’instance d’auteur.

### Configuration de la réplication en chaîne    {#configure-chain-replication}

1. Sélectionnez l’instance de publication vers laquelle vous souhaitez effectuer les réplications en chaîne
1. Sur cette instance de publication, ajoutez des agents de réplication qui pointent vers d’autres instances de publication
1. Sur chacun de ces agents de réplication, activez « À la réception » dans l’onglet « Déclencheurs »

>[!NOTE]
>
>Adobe ne recommande pas d’activer automatiquement les ressources. Cependant, si nécessaire, Adobe recommande d’effectuer cette opération en tant que dernière étape d’un workflow, généralement Ressource de mise à jour de gestion des actifs numériques.

## Indices de recherche {#search-indexes}

Veillez à mettre en œuvre les derniers Service Packs et les correctifs liés aux performances étant donné qu’ils contiennent souvent des mises à jour des index du système. Voir les conseils [d’optimisation des](https://helpx.adobe.com/fr/experience-manager/kb/performance-tuning-tips.html) performances pour connaître certaines optimisations d’index.

Créez des index personnalisés pour les demandes que vous exécutez régulièrement. Pour plus d’informations, consultez la [méthodologie pour l’analyse des requêtes lentes](https://aemfaq.blogspot.com/2014/08/oak-query-log-file-analyzer-tool.html) et la [création d’index personnalisés](/help/sites-deploying/queries-and-indexing.md). Pour des informations complémentaires au sujet des meilleures pratiques de requête et d’index, consultez les [Meilleures pratiques pour les requêtes et l’indexation](/help/sites-deploying/best-practices-for-queries-and-indexing.md).

### Configurations de l’index Lucene {#lucene-index-configurations}

Some optimizations can be done on the Oak index configurations that can help improve [!DNL Experience Manager Assets] performance. Mettez à jour les configurations d’index pour améliorer le temps de réindexation :

1. Open CRXDe `/crx/de/index.jsp` and log in as an administrative user.
1. Accédez à `/oak:index/lucene`.
1. Ajouter une `String[]` propriété `excludedPaths` avec des valeurs `/var`, `/etc/workflow/instances`et `/etc/replication`.
1. Accédez à `/oak:index/damAssetLucene`. Ajouter une `String[]` propriété `includedPaths` avec une valeur `/content/dam`. Enregistrez les modifications.

Si vos utilisateurs n’ont pas besoin de rechercher des ressources en texte intégral, par exemple, en recherchant du texte dans des documents PDF, désactivez-le. Vous améliorez les performances de l’index en désactivant l’indexation de texte intégral. Pour désactiver l’extraction [!DNL Apache Lucene] de texte, procédez comme suit :

1. Dans [!DNL Experience Manager] l’interface, accédez à [!UICONTROL Package Manager].
1. Téléchargez et installez le package disponible à l’adresse [disable_indexingbinarytextextraction-10.zip](assets/disable_indexingbinarytextextraction-10.zip).

### Paramètre guessTotal {#guess-total}

Lors de la création de requêtes qui génèrent d’importants ensembles de résultats, utilisez le paramètre `guessTotal` de façon à éviter une utilisation élevée de la mémoire lors de l’exécution.

## Problèmes connus {#known-issues}

### Fichiers volumineux {#large-files}

Il existe deux problèmes importants connus relatifs aux fichiers volumineux dans [!DNL Experience Manager]. Lorsque la taille des fichiers est supérieure à 2 Go, la synchronisation de reprise progressive peut s’exécuter en cas de mémoire insuffisante. Dans certains cas, cela empêche la synchronisation de reprise de s’exécuter. Dans d’autres cas, cela entraîne le blocage de l’instance principale. This scenario applies to any file in [!DNL Experience Manager] that is larger than 2GB, including content packages.

De même, lorsque les fichiers atteignent une taille de 2 Go lors de l’utilisation d’un magasin de données S3 partagé, il peut s’écouler un certain temps avant que le fichier soit complètement conservé du cache au système de fichiers. Par conséquent, lorsque vous avez recours à une réplication sans binaire, il est possible que les données binaires ne soient pas conservées avant la fin de la réplication. Cette situation peut entraîner des problèmes, surtout si la disponibilité des données est importante.

## Test de performance {#performance-testing}

For every [!DNL Experience Manager] deployment, establish a performance testing regime that can identify and resolve bottlenecks quickly. Voici quelques points clés.

### Test réseau    {#network-testing}

Pour tous les problèmes liés aux performances du réseau du client, effectuez les tâches suivantes :

* Tester les performances du réseau sur le réseau du client
* Testez les performances du réseau sur le réseau Adobe. Pour les clients AMS, consultez votre CSE pour effectuer des tests sur le réseau Adobe.
* Tester les performances du réseau depuis un autre point d’accès
* En utilisant un outil localisateur de réseau
* Tester par rapport au Dispatcher

### [!DNL Experience Manager] test d’instance {#aem-instance-testing}

To minimize latency and achieve high throughput through efficient CPU utilization and load-sharing, monitor the performance of your [!DNL Experience Manager] instance regularly. En particulier :

* Run load tests against the [!DNL Experience Manager] instance.
* Surveiller les performances de chargement et la réactivité de l’interface utilisateur.

## [!DNL Experience Manager Assets] liste de contrôle des performances et impact des tâches de gestion des actifs {#checklist}

* Autoriser HTTPS à contourner tous les renifleurs de trafic HTTP d’entreprise.
* Utiliser une connexion câblée pour le chargement de ressources volumineuses.
* Déploiement sur Java 8.
* Définition de paramètres JVM optimaux.
* Configurez une banque de données de système de fichiers ou une banque de données S3.
* Activer les workflows transitoires.
* Régler les files d’attente de workflows Granite pour limiter les tâches concurrentes.
* Configure [!DNL ImageMagick] to limit resource consumption.
* Remove unnecessary steps from the [!UICONTROL DAM Update Asset] workflow.
* Configurer la purge des workflows et versions.
* Optimisez les index avec les derniers Service Pack et correctifs. Contactez le service à la clientèle d’Adobe pour connaître les optimisations d’index supplémentaires éventuellement disponibles.
* Utilisez guessTotal afin d’optimiser les performances des requêtes.
* If you configure [!DNL Experience Manager] to detect file types from the content of the files (by enabling **[!UICONTROL Day CQ DAM Mime Type Service]** in the **[!UICONTROL AEM Web Console]**), upload many files in bulk during non-peak hours as it is resource-intensive.
