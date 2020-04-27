---
title: Guide de réglage des performances des ressources
description: Suggestions et conseils sur la configuration d’AEM, les modifications apportées au matériel, aux logiciels et aux composants réseau afin de supprimer les goulets d’étranglement et d’optimiser les performances des ressources AEM.
contentOwner: AG
mini-toc-levels: 1
translation-type: tm+mt
source-git-commit: 31234518537ca4a0b7ff36e8d52a3b7b1b8fe4f7

---


<!-- TBD: Get reviewed by engineering. -->

# Assets performance tuning guide {#assets-performance-tuning-guide}

Une configuration d’Adobe Experience Manager (AEM) Assets présente un certain nombre de composants matériels, logiciels et réseau. Selon votre scénario de déploiement, vous pouvez avoir besoin d’apporter des modifications spécifiques à la configuration des composants matériels, logiciels et réseau pour supprimer les goulots d’étranglement en termes de performances.

En outre, l’identification et le respect de certaines instructions en termes d’optimisation des composants matériels et logiciels permettent de créer une base solide afin que le déploiement de AEM Assets réponde aux attentes en matière de performances, d’évolutivité et de fiabilité.

De faibles performances d’AEM Assets peuvent avoir une incidence sur l’expérience utilisateur en termes de performances interactives, de traitement des ressources, de vitesse de téléchargement et d’autres aspects.

En fait, l’optimisation des performances est une tâche essentielle que vous effectuez avant d’établir des mesures cibles pour chacun de vos projets.

Voici quelques éléments principaux essentiels pour lesquels vous devez identifier et corriger les problèmes de performances avant que ceux-ci aient un impact sur les utilisateurs.

## Plate-forme {#platform}

Bien qu’AEM soit pris en charge sur plusieurs plates-formes, Adobe a trouvé le meilleur moyen de prendre en charge les outils natifs sous Linux et Windows, ce qui contribue à offrir des performances optimales et à faciliter l’implémentation. Dans l’idéal, vous devez déployer un système d’exploitation 64 bits pour répondre aux besoins de stockage du déploiement AEM Assets. A l’instar de tout déploiement AEM, vous devez mettre en œuvre TarMK dans la mesure du possible. Bien que TarMK ne puisse pas mesurer au-delà d’une instance d’auteur simple, il semble offrir de meilleurs résultats que MongoMK. Vous pouvez ajouter des instances de déchargement TarMK pour améliorer la capacité de traitement des workflows de votre déploiement d’AEM Assets.

### Dossier temporaire {#temp-folder}

Pour améliorer les temps de transfert des ressources, utilisez des  hautes performances  pour le répertoire temporaire Java. Sous Linux et Windows, un disque SSD ou RAM peut être utilisé. Dans des environnements cloud, un type de stockage à grande vitesse équivalent peut être utilisé. For example in Amazon EC2, an [ephemeral drive](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/InstanceStorage.html) drive can be used for the temporary folder.

En supposant que le serveur dispose de suffisamment de mémoire, configurez un disque RAM. Sous Linux, exécutez les commandes suivantes pour créer un disque RAM de 8 Go :

```shell
mkfs -q /dev/ram1 800000
 mkdir -p /mnt/aem-tmp
 mount /dev/ram1 /mnt/aem-tmp
 df -H | grep aem-tmp
```

Sous Windows OS, utilisez un pilote tiers pour créer un lecteur RAM ou utilisez simplement des  hautes performances tels que SSD.

Once the high performance temporary volume is ready, set the JVM parameter `-Djava.io.tmpdir`. For example, you could add the JVM parameter below to the `CQ_JVM_OPTS` variable in the `bin/start` script of AEM:

`-Djava.io.tmpdir=/mnt/aem-tmp`

## Configuration Java {#java-configuration}

### Version Java {#java-version}

Adobe recommande de déployer AEM Assets sur Java 8 pour des performances optimales.

>[!NOTE]
>
>Oracle a cessé de publier les mises à jour pour Java 7 à compter d’avril 2015.

### Paramètres JVM    {#jvm-parameters}

Définissez les paramètres JVM suivants :

* `-XX:+UseConcMarkSweepGC`
* `-Doak.queryLimitInMemory`=500000
* `-Doak.queryLimitReads`=100000
* `-Dupdate.limit`=250000
* `-Doak.fastQuerySize`=true

## Configuration d’entrepôt de données et de mémoire {#data-store-and-memory-configuration}

### Configuration d’entrepôt de données basé sur les fichiers {#file-data-store-configuration}

Nous recommandons à tous les utilisateurs d’AEM Assets de séparer l’entrepôt de données et l’entrepôt de segments. En outre, la configuration des paramètres `maxCachedBinarySize` et `cacheSizeInMB` peut vous aider à optimiser les performances. Définissez le paramètre `maxCachedBinarySize` selon la plus petite taille de fichier pouvant être contenue dans le cache. Spécifiez la taille du cache en mémoire à utiliser pour l’entrepôt de données dans `cacheSizeInMB`. Adobe vous recommande de définir cette valeur entre 2 et 10 % de la taille totale du tas. Toutefois, le chargement ou le test des performances peuvent vous aider à déterminer le paramètre idéal.

### Configuration de la taille maximale du cache d’images mis en mémoire tampon    {#configure-the-maximum-size-of-the-buffered-image-cache}

Lors du chargement d’un grand nombre de ressources vers Adobe Experience Manager, réduisez la taille maximale configurée du cache d’images mis en mémoire tampon. De cette façon, vous tiendrez compte des pics inattendus de consommation de la mémoire et éviterez l’échec de JVM avec des erreurs de mémoire insuffisante. Prenez l’exemple d’un système présentant un tas maximal (paramètre -`Xmx`) de 5 Go, un BlobCache Oak défini sur 1 Go et un cache de documents défini sur 2 Go. Dans ce cas, le cache mis en mémoire tampon prendrait au maximum 1,25 Go, ce qui laisserait seulement 0,75 Go pour les pics inattendus.

Configurez la taille du cache mis en mémoire tampon dans la console web OSGi. À l’emplacement `https://host:port/system/console/configMgr/com.day.cq.dam.core.impl.cache.CQBufferedImageCache`, définissez la propriété `cq.dam.image.cache.max.memory` en octets. Par exemple, 1073741824 représente 1 Go (1 024 x 1 024 x 1 024 = 1 Go).

À compter d’AEM 6.1 SP1, si vous utilisez un nœud `sling:osgiConfig` pour configurer cette propriété, veillez à définir le type de données sur Long. Pour plus de détails, voir [CQBufferedImageCache utilise le tas pendant le téléchargement des ressources](https://helpx.adobe.com/fr/experience-manager/kb/cqbufferedimagecache-consumes-heap-during-asset-uploads.html).

### Entrepôts de données partagés    {#shared-data-stores}

La mise en œuvre d’un entrepôt de données basé sur les fichiers, partagé ou S3, peut vous aider à économiser de l’espace disque et à augmenter le débit réseau dans des implémentations à grande échelle. For more information on the pros and cons of using a shared datastore, see [Assets Sizing Guide](/help/assets/assets-sizing-guide.md).

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

Adobe recommande d’activer HTTPS, car de nombreuses entreprises qui possèdent des pare-feu analysent le trafic HTTP, ce qui a une incidence sur les chargements et endommage les fichiers. Pour les chargements de fichiers volumineux, assurez-vous que les utilisateurs disposent d’une connexion filaire au réseau, car les réseaux Wi-Fi saturent rapidement. For guidelines on identifying network bottlenecks, see [Assets Sizing Guide](/help/assets/assets-sizing-guide.md). Pour évaluer les performances du réseau en analysant sa topologie, consultez les [Remarques sur le réseau des ressources](/help/assets/assets-network-considerations.md).

Votre stratégie d’optimisation du réseau dépend essentiellement de la quantité de bande passante disponible et du chargement sur votre instance AEM. Les options de configuration courantes, notamment les pare-feu ou les proxys, peuvent améliorer les performances du réseau. Voici quelques points essentiels à prendre en compte :

* Selon votre type d’instance (petite, moyenne ou grande), vérifiez que vous disposez de suffisamment de bande passante réseau pour votre instance AEM. L’allocation d’une bande passante appropriée est particulièrement importante si AEM est hébergé sur AWS.
* Si votre instance AEM est hébergée sur AWS, vous pouvez tirer profit d’une stratégie de mise à l’échelle polyvalente. Augmentez la taille de l’instance si les utilisateurs prévoient une charge élevée. Réduisez-la pour une charge moyenne/faible.
* HTTPS : la plupart des utilisateurs possèdent des pare-feu qui analysent le trafic HTTP, ce qui est susceptible d’avoir une incidence sur le chargement des fichiers ou même endommager des fichiers lors de l’opération de chargement.
* Chargements volumineux : assurez-vous que les utilisateurs disposent d’une connexion filaire au réseau (les connexions Wi-Fi sont rapidement saturées).

## Workflows {#workflows}

### Workflows transitoires {#transient-workflows}

Wherever possible, set the [!UICONTROL DAM Update Asset] workflow to Transient. Le paramètre réduit considérablement les surcharges nécessaires pour traiter les workflows car, dans ce cas, ils n’ont pas besoin de faire l’objet d’un suivi et de processus d’archivage classiques.

1. Accédez à `/miscadmin` l’instance AEM à l’adresse `https://[aem_server]:[port]/miscadmin`.

1. Développez **[!UICONTROL Outils]** > **[!UICONTROL Processus]** > **[!UICONTROL Modèles]** > **[!UICONTROL Barrage.]**

1. Open **[!UICONTROL DAM Update Asset]**. Depuis le panneau d’outils flottant, basculez vers l’onglet **[!UICONTROL Page]**, puis cliquez sur **[!UICONTROL Propriétés de la page]**.

1. Select **[!UICONTROL Transient Workflow]** and click **[!UICONTROL OK]**.

   >[!NOTE]
   >
   >Certaines fonctions ne prennent pas en charge les workflows transitoires. If your [!DNL Assets] deployment requires these features, do not configure transient workflows.

In cases where transient workflows cannot be used, run workflow purging regularly to delete archived [!UICONTROL DAM Update Asset] workflows to ensure system performance does not degrade.

En règle générale, exécutez le  de purge chaque semaine. Cependant, dans les scénarios nécessitant beaucoup de ressources, comme lors de l’ingestion d’actifs à grande échelle, vous pouvez l’exécuter plus fréquemment.

Pour configurer la purge des workflows, ajoutez une nouvelle configuration de purge de workflow d’Adobe Granite via la console OSGi. Configurez et planifiez ensuite le workflow dans le cadre de la période de maintenance hebdomadaire.

Si la purge s’exécute trop longtemps, elle s’arrête. Par conséquent, vous devez vous assurer que vos tâches de purge se terminent pour éviter les cas où l’exécution de la purge des workflows échoue en raison du nombre élevé de workflows.

For example, after executing numerous non-transient workflows (that creates workflow instance nodes), you can execute [ACS AEM Commons Workflow Remover](https://adobe-consulting-services.github.io/acs-aem-commons/features/workflow-remover.html) on an ad-hoc basis. Il supprime les instances de workflow terminées et redondantes immédiatement sans attendre l’exécution du planificateur de purge de workflow d’Adobe Granite.

### Tâches parallèles maximales    {#maximum-parallel-jobs}

Par défaut, AEM exécute un nombre maximal de tâches parallèles qui est égal au nombre de processeurs sur le serveur. The problem with this setting is that during periods of heavy load, all of the processors are occupied by [!UICONTROL DAM Update Asset] workflows, slowing down UI responsiveness and preventing AEM from running other processes that safeguard server performance and stability. En tant que bonne pratique, définissez cette valeur sur la moitié des processeurs disponibles sur le serveur en procédant comme suit :

1. Sur Experience Manager Author, accédez à `https://[aem_server]:[port]/system/console/slingevent`.

1. Click **[!UICONTROL Edit]** on each workflow queue that is relevant to your implementation, for example **[!UICONTROL Granite Transient Workflow Queue]**.

1. Update the value of **[!UICONTROL Maximum Parallel Jobs]** and click **[!UICONTROL Save]**.

Configurer une file d’attente à la moitié des processeurs disponibles est une solution exploitable pour commencer. Cependant, vous pouvez être amené à augmenter ou à réduire ce nombre pour atteindre un débit maximal et l’ajuster selon l’environnement. Il existe des files d’attente distinctes pour les workflows transitoires et non transitoires, ainsi que d’autres processus, tels que les workflows externes. Si plusieurs files d’attente configurées à 50 % des processeurs sont activées simultanément, le système peut devenir rapidement surchargé. Les files d’attente utilisées varient considérablement selon les différentes implémentations de l’utilisateur. Par conséquent, vous devrez peut-être les configurer de manière réfléchie pour un maximum d’efficacité sans sacrifier la stabilité des serveurs.

### Configuration des ressources de mise à jour de gestion des ressources numériques {#dam-update-asset-configuration}

The [!UICONTROL DAM Update Asset] workflow contains a full suite of steps that are configured for tasks, such as Scene7 PTIFF generation and InDesign Server integration. Cependant, plusieurs de ces étapes peuvent être inutiles à la plupart des utilisateurs. Adobe recommends you create a custom copy of the [!UICONTROL DAM Update Asset] workflow model, and remove any unnecessary steps. In this case, update the launchers for [!UICONTROL DAM Update Asset] to point to the new model.

Running the [!UICONTROL DAM Update Asset] workflow intensively can sharply increase the size of your file datatastore. Les résultats d’un test effectué par Adobe ont montré que la taille de l’entrepôt de données peut augmenter d’environ 400 Go si environ 5 500 workflows sont exécutés pendant une période de 8 heures.

Il s’agit d’une augmentation temporaire ; l’entrepôt de données est restauré à sa taille d’origine après avoir exécuté la tâche Nettoyage de la mémoire d’entrepôt de données.

En règle générale, la tâche Nettoyage de la mémoire d’entrepôt de données s’exécute chaque semaine avec d’autres tâches de maintenance planifiées.

If you have a limited disk space and run [!UICONTROL DAM Update Asset] workflows intensively, consider scheduling the garbage collection task more frequently.

#### Génération de rendus au moment de l’exécution {#runtime-rendition-generation}

Les clients utilisent des images de tailles et de formats différents sur leur site web ou pour les distribuer à leurs partenaires professionnels. Étant donné que chaque rendu s’ajoute à l’encombrement d’une ressource dans le référentiel, Adobe recommande d’utiliser cette fonction judicieusement. Pour limiter le nombre de ressources nécessaires pour traiter et stocker des images, vous pouvez générer ces images au moment de l’exécution plutôt que comme rendus pendant l’assimilation.

De nombreux clients de sites mettent en œuvre un servlet d’image qui redimensionne ou recadre les images lorsque cela est nécessaire, ce qui a pour effet d’appliquer une charge supplémentaire à l’instance de publication. Toutefois, tant que ces images peuvent être mises en cache, le défi peut être plus facilement relevé.

Une autre méthode consiste à utiliser la technologie Scene7 pour transférer entièrement la manipulation de l’image. Vous pouvez également déployer Brand Portal, qui accepte non seulement les responsabilités de génération de rendu à partir de l’infrastructure AEM, mais également la totalité du niveau de publication.

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
>Une configuration incorrecte peut rendre votre serveur instable si ImageMagick utilise tout l’espace disque disponible. Les modifications de stratégie requises pour traiter des fichiers volumineux à l’aide d’ImageMagick peuvent avoir une incidence sur les performances d’AEM. Pour plus d’informations, voir [Installation et configuration d’ImageMagick](/help/assets/best-practices-for-imagemagick.md).

>[!NOTE]
>
>Les fichiers ImageMagick `policy.xml` et `configure.xml` les fichiers sont disponibles à la `/usr/lib64/ImageMagick-&#42;/config/` place de `/etc/ImageMagick/`.Voir la documentation [](https://www.imagemagick.org/script/resources.php) ImageMagick pour connaître l’emplacement des fichiers de configuration.

Si vous utilisez Experience Manager sur Adobe Managed Services (AMS), contactez le service à la clientèle d’Adobe si vous prévoyez de traiter un grand nombre de fichiers PSD ou PSB volumineux. Contactez le représentant du service à la clientèle Adobe pour mettre en oeuvre ces bonnes pratiques pour votre déploiement AMS et choisir les meilleurs outils et modèles possibles pour les formats propriétaires d’Adobe. Experience Manager peut ne pas traiter les fichiers PSB haute résolution de plus de 3 000 x 2 3 000 pixels.

### Écriture différée XMP {#xmp-writeback}

L’écriture différée XMP met à jour les ressources d’origine chaque fois que les métadonnées sont modifiées dans AEM, ce qui permet ce qui suit :

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

Certaines optimisations peuvent être effectuées sur les configurations d’index Oak afin d’améliorer les performances d’AEM Assets. Mettez à jour les configurations d’index pour améliorer le temps de réindexation :

1. Open CRXDe `/crx/de/index.jsp` and log in as an administrative user
1. Naviguer jusqu’à `/oak:index/lucene`
1. Ajouter une propriété String[] `excludedPaths` avec des valeurs `/var`, `/etc/workflow/instances`et `/etc/replication`.
1. Accédez à `/oak:index/damAssetLucene`. Ajouter une `String[]` propriété `includedPaths` avec une valeur `/content/dam`.
1. Enregistrer.

<!-- TBD: Review by engineering if required in 6.5 docs or not.

(AEM6.1 and 6.2 only) Update the `ntBaseLucene` index to improve asset delete and move performance:

1. Browse to `/oak:index/ntBaseLucene/indexRules/nt:base/properties`

1. Add two nt:unstructured nodes `slingResource` and `damResolvedPath` under `/oak:index/ntBaseLucene/indexRules/nt:base/properties`

1. Set the properties below on the nodes (where `ordered` and `propertyIndex` properties are of type `Boolean`:

   ```conf
   slingResource
   name="sling:resource"
   ordered=false
   propertyIndex= true
   type="String"
   damResolvedPath
   name="dam:resolvedPath"
   ordered=false
   propertyIndex=true
   type="String"
   ```

1. On the `/oak:index/ntBaseLucene` node, set the property `reindex=true`. Click **[!UICONTROL Save All]**.
1. Monitor the error.log to see when indexing is completed:
   Reindexing completed for indexes: [/oak:index/ntBaseLucene]
1. You can also see that indexing is completed by refreshing the /oak:index/ntBaseLucene node in CRXDe as the reindex property would go back to false
1. Once indexing is completed then go back to CRXDe and set the "type" property to disabled on these two indexes

    * */oak:index/slingResource*
    * */oak:index/damResolvedPath*

1. Click "Save All"
-->

Désactiver l’extraction de texte Lucene :

Si vos utilisateurs n’ont pas besoin d’effectuer une recherche de texte intégral sur des fichiers, par exemple, en effectuant une recherche dans le texte du PDF, désactivez-le. Vous améliorez les performances de l’index en désactivant l’indexation en texte intégral.

1. Go to the AEM package manager `/crx/packmgr/index.jsp`.
1. Téléchargez et installez le package disponible sur [disable_indexingbinarytextextraction-10.zip](assets/disable_indexingbinarytextextraction-10.zip).

### Paramètre guessTotal {#guess-total}

Lors de la création de requêtes qui génèrent d’importants ensembles de résultats, utilisez le paramètre `guessTotal` de façon à éviter une utilisation élevée de la mémoire lors de l’exécution.

## Problèmes connus {#known-issues}

### Fichiers volumineux {#large-files}

Il existe deux problèmes importants connus relatifs aux fichiers volumineux dans AEM. Lorsque la taille des fichiers est supérieure à 2 Go, la synchronisation de reprise progressive peut s’exécuter en cas de mémoire insuffisante. Dans certains cas, cela empêche la synchronisation de reprise de s’exécuter. Dans d’autres cas, cela entraîne le blocage de l’instance principale. Ce scénario s’applique à tous les fichiers dans AEM dont la taille est supérieure à 2 Go, y compris les modules de contenu.

De même, lorsque les fichiers atteignent 2 Go lors de l’utilisation d’un entrepôt de données S3 partagé, cela peut prendre un certain temps pour que le fichier soit entièrement conservé du cache vers le système de fichiers. Par conséquent, lorsque vous avez recours à une réplication sans binaire, il est possible que les données binaires ne soient pas conservées avant la fin de la réplication. Cette situation peut entraîner des problèmes, surtout si la disponibilité des données est importante.

## Test de performance {#performance-testing}

Pour chaque déploiement AEM, créez un régime de tests de performances qui permet d’identifier et de résoudre les goulots d’étranglement rapidement. Voici quelques points clés.

### Test réseau    {#network-testing}

Pour tous les problèmes liés aux performances du réseau du client, effectuez les tâches suivantes :

* Tester les performances du réseau sur le réseau du client
* Testez les performances du réseau sur le réseau Adobe. Pour les clients AMS, consultez votre CSE pour effectuer des tests sur le réseau Adobe.
* Tester les performances du réseau depuis un autre point d’accès
* En utilisant un outil localisateur de réseau
* Tester par rapport au Dispatcher

### Test de l’instance AEM    {#aem-instance-testing}

Pour réduire la latence et obtenir un débit élevé grâce à une utilisation efficace du processeur et au partage de la charge, surveillez régulièrement les performances de votre instance AEM. En particulier :

* Exécuter des tests de charge par rapport à l’instance AEM
* Surveiller les performances de chargement et la réactivité de l’interface utilisateur

## Liste de contrôle des performances d’AEM Assets    et impact des tâches de gestion des ressources    {#checklist}

* Autoriser HTTPS à contourner tous les renifleurs de trafic HTTP d’entreprise
* Utiliser une connexion câblée pour le chargement de ressources volumineuses
* Déploiement sur Java 8.
* Définition de paramètres JVM optimaux
* Configurer un entrepôt de données de système de fichiers ou un entrepôt de données S3
* Activer les workflows transitoires
* Régler les files d’attente de workflows Granite pour limiter les tâches concurrentes
* Configurer ImageMagick pour limiter la consommation de ressources
* Remove unnecessary steps from the [!UICONTROL DAM Update Asset] workflow
* Configurer la purge des workflows et versions
* Optimisez les index avec les derniers Service Pack et correctifs. Vérifiez auprès du support Adobe toutes les optimisations d’index supplémentaires qui pourraient être disponibles.
* Utilisez guessTotal afin d’optimiser les performances des requêtes.
* Si vous configurez AEM pour détecter des types de fichiers à partir de leur contenu (en activant le **[!UICONTROL service de type MIME de gestion des actifs numériques Day CQ]** dans la **[!UICONTROL Console web AEM]**), chargez les fichiers en masse aux heures creuses, car cela consomme beaucoup de ressources.
