---
title: Réglage des performances  [!DNL Assets].
description: Suggestions et conseils sur  [!DNL Experience Manager] la configuration, les modifications apportées au matériel, aux logiciels et aux composants réseau pour supprimer les goulets d'étranglement et optimiser les performances de  [!DNL Experience Manager Assets].
contentOwner: AG
mini-toc-levels: 1
role: Architecte, Administrateur
feature: Gestion des ressources
translation-type: tm+mt
source-git-commit: 174e0703ae541641e3dc602e700bcd31624ae62c
workflow-type: tm+mt
source-wordcount: '2745'
ht-degree: 53%

---


<!-- TBD: Get reviewed by engineering. -->

# [!DNL Adobe Experience Manager Assets] guide de réglage des performances  {#assets-performance-tuning-guide}

Une configuration [!DNL Experience Manager Assets] contient un certain nombre de composants matériels, logiciels et réseau. Selon votre scénario de déploiement, vous pouvez avoir besoin d’apporter des modifications spécifiques à la configuration des composants matériels, logiciels et réseau pour supprimer les goulots d’étranglement en termes de performances.

En outre, l&#39;identification et le respect de certaines directives d&#39;optimisation du matériel et des logiciels permettent de bâtir une base solide qui permet à votre déploiement [!DNL Experience Manager Assets] de répondre aux attentes en matière de performances, d&#39;évolutivité et de fiabilité.

Les performances médiocres de [!DNL Experience Manager Assets] peuvent avoir un impact sur les performances interactives, le traitement des ressources, la vitesse de téléchargement et d’autres domaines.

En fait, l’optimisation des performances est une tâche essentielle que vous effectuez avant d’établir des mesures cibles pour chacun de vos projets.

Voici quelques éléments principaux essentiels pour lesquels vous devez identifier et corriger les problèmes de performances avant que ceux-ci aient un impact sur les utilisateurs.

## Plate-forme {#platform}

Bien que Experience Manager soit pris en charge sur plusieurs plates-formes, l’Adobe a trouvé la meilleure prise en charge des outils natifs sous Linux et Windows, ce qui contribue à des performances optimales et à la facilité d’implémentation. Idéalement, vous devez déployer un système d&#39;exploitation 64 bits pour répondre aux exigences de mémoire élevées d&#39;un déploiement [!DNL Experience Manager Assets]. Comme pour tout déploiement Experience Manager, vous devez implémenter TarMK chaque fois que possible. Bien que TarMK ne puisse pas mesurer au-delà d’une instance d’auteur simple, il semble offrir de meilleurs résultats que MongoMK. Vous pouvez ajouter des instances de déchargement TarMK pour augmenter la puissance de traitement du flux de travail de votre déploiement [!DNL Experience Manager Assets].

### Dossier temporaire {#temp-folder}

Pour améliorer les temps de transfert des ressources, utilisez un enregistrement hautement performant pour le répertoire temporaire Java. Sous Linux et Windows, un disque SSD ou RAM peut être utilisé. Dans des environnements cloud, un type de stockage à grande vitesse équivalent peut être utilisé. Par exemple, dans Amazon EC2, un lecteur [éphémère](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/InstanceStorage.html) peut être utilisé pour le dossier temporaire.

En supposant que le serveur dispose de suffisamment de mémoire, configurez un disque RAM. Sous Linux, exécutez les commandes suivantes pour créer un disque RAM de 8 Go :

```shell
mkfs -q /dev/ram1 800000
 mkdir -p /mnt/aem-tmp
 mount /dev/ram1 /mnt/aem-tmp
 df -H | grep aem-tmp
```

Sous Windows OS, utilisez un pilote tiers pour créer un lecteur RAM ou utilisez simplement un enregistrement hautes performances tel que SSD.

Une fois que le volume temporaire hautes performances est prêt, définissez le paramètre JVM `-Djava.io.tmpdir`. Par exemple, vous pouvez ajouter le paramètre JVM ci-dessous à la variable `CQ_JVM_OPTS` dans le script `bin/start` de [!DNL Experience Manager] :

`-Djava.io.tmpdir=/mnt/aem-tmp`

## Configuration Java {#java-configuration}

### Version Java {#java-version}

Adobe recommande de déployer [!DNL Experience Manager Assets] sur Java 8 pour optimiser les performances.

<!-- TBD: Link to the latest official word around Java.
-->

### Paramètres JVM    {#jvm-parameters}

Définissez les paramètres JVM suivants :

* `-XX:+UseConcMarkSweepGC`
* `-Doak.queryLimitInMemory`=500000
* `-Doak.queryLimitReads`=100000
* `-Dupdate.limit`=250000
* `-Doak.fastQuerySize`=true

## Configuration d’entrepôt de données et de mémoire {#data-store-and-memory-configuration}

### Configuration d’entrepôt de données basé sur les fichiers {#file-data-store-configuration}

Il est recommandé de séparer le magasin de données du magasin de segments pour tous les utilisateurs [!DNL Experience Manager Assets]. En outre, la configuration des paramètres `maxCachedBinarySize` et `cacheSizeInMB` peut vous aider à optimiser les performances. Définissez le paramètre `maxCachedBinarySize` selon la plus petite taille de fichier pouvant être contenue dans le cache. Spécifiez la taille du cache en mémoire à utiliser pour l’entrepôt de données dans `cacheSizeInMB`. Adobe vous recommande de définir cette valeur entre 2 et 10 % de la taille totale du tas. Toutefois, le chargement ou le test des performances peuvent vous aider à déterminer le paramètre idéal.

### Configuration de la taille maximale du cache d’images mis en mémoire tampon     {#configure-the-maximum-size-of-the-buffered-image-cache}

Lorsque vous téléchargez de grandes quantités de ressources vers [!DNL Adobe Experience Manager], pour permettre des pics inattendus de la consommation de mémoire et pour éviter l’échec de la JVM avec OutOfMemoryErrors, réduisez la taille maximale configurée du cache d’images en mémoire tampon. Prenez l’exemple d’un système présentant un tas maximal (paramètre -`Xmx`) de 5 Go, un BlobCache Oak défini sur 1 Go et un cache de documents défini sur 2 Go. Dans ce cas, le cache mis en mémoire tampon prendrait au maximum 1,25 Go, ce qui laisserait seulement 0,75 Go pour les pics inattendus.

Configurez la taille du cache mis en mémoire tampon dans la console web OSGi. À l’emplacement `https://host:port/system/console/configMgr/com.day.cq.dam.core.impl.cache.CQBufferedImageCache`, définissez la propriété `cq.dam.image.cache.max.memory` en octets. Par exemple, 1073741824 représente 1 Go (1 024 x 1 024 x 1 024 = 1 Go).

Dans Experience Manager 6.1 SP1, si vous utilisez un noeud `sling:osgiConfig` pour configurer cette propriété, veillez à définir le type de données sur Long. Pour plus de détails, voir [CQBufferedImageCache utilise le tas pendant le téléchargement des ressources](https://helpx.adobe.com/fr/experience-manager/kb/cqbufferedimagecache-consumes-heap-during-asset-uploads.html).

### Entrepôts de données partagés     {#shared-data-stores}

La mise en œuvre d’un entrepôt de données basé sur les fichiers, partagé ou S3, peut vous aider à économiser de l’espace disque et à augmenter le débit réseau dans des implémentations à grande échelle. Pour plus d’informations sur les avantages et les inconvénients de l’utilisation d’une banque de données partagée, voir [Guide de dimensionnement des ressources](/help/assets/assets-sizing-guide.md).

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

Adobe recommande d’activer HTTPS, car de nombreuses entreprises qui possèdent des pare-feu analysent le trafic HTTP, ce qui a une incidence sur les chargements et endommage les fichiers. Pour les chargements de fichiers volumineux, assurez-vous que les utilisateurs disposent d’une connexion filaire au réseau, car les réseaux Wi-Fi saturent rapidement. Pour obtenir des instructions sur l&#39;identification des goulets d&#39;étranglement réseau, voir [Guide de dimensionnement des ressources](/help/assets/assets-sizing-guide.md). Pour évaluer les performances du réseau en analysant la topologie du réseau, voir [Considérations relatives au réseau des ressources](/help/assets/assets-network-considerations.md).

En premier lieu, votre stratégie d&#39;optimisation réseau dépend de la quantité de bande passante disponible et de la charge sur votre instance [!DNL Experience Manager]. Les options de configuration courantes, notamment les pare-feu ou les proxys, peuvent améliorer les performances du réseau. Voici quelques points essentiels à prendre en compte :

* En fonction du type d’instance (petit, modéré, grand), veillez à disposer d’une bande passante réseau suffisante pour votre instance de Experience Manager. Une allocation de bande passante adéquate est particulièrement importante si [!DNL Experience Manager] est hébergé sur AWS.
* Si votre instance [!DNL Experience Manager] est hébergée sur AWS, vous pouvez en bénéficier en appliquant une stratégie de mise à l’échelle polyvalente. Augmentez la taille de l’instance si les utilisateurs prévoient une charge élevée. Réduisez-la pour une charge moyenne/faible.
* HTTPS : la plupart des utilisateurs possèdent des pare-feu qui analysent le trafic HTTP, ce qui est susceptible d’avoir une incidence sur le chargement des fichiers ou même endommager des fichiers lors de l’opération de chargement.
* Chargements volumineux : assurez-vous que les utilisateurs disposent d’une connexion filaire au réseau (les connexions Wi-Fi sont rapidement saturées).

## Workflows {#workflows}

### Workflows transitoires {#transient-workflows}

Dans la mesure du possible, définissez le workflow [!UICONTROL DAM Update Asset] sur Temporaire. Le paramètre réduit considérablement les surcharges nécessaires pour traiter les workflows car, dans ce cas, ils n’ont pas besoin de faire l’objet d’un suivi et de processus d’archivage classiques.

1. Accédez à `/miscadmin` dans le déploiement [!DNL Experience Manager] à `https://[aem_server]:[port]/miscadmin`.

1. Développez **[!UICONTROL Outils]** > **[!UICONTROL Workflow]** > **[!UICONTROL Modèles]** > **[!UICONTROL dam]**.

1. Ouvrez **[!UICONTROL DAM Update Asset]**. Depuis le panneau d’outils flottant, basculez vers l’onglet **[!UICONTROL Page]**, puis cliquez sur **[!UICONTROL Propriétés de la page]**.

1. Sélectionnez **[!UICONTROL Processus transitoire]** et cliquez sur **[!UICONTROL OK]**.

   >[!NOTE]
   >
   >Certaines fonctions ne prennent pas en charge les workflows transitoires. Si votre déploiement [!DNL Assets] requiert ces fonctionnalités, ne configurez pas de workflows transitoires.

Dans les cas où des workflows transitoires ne peuvent pas être utilisés, exécutez régulièrement le processus de purge pour supprimer les workflows [!UICONTROL DAM Update Asset] archivés afin de s&#39;assurer que les performances du système ne se dégradent pas.

En règle générale, exécutez les workflows de purge sur une base hebdomadaire. Cependant, dans les scénarios à forte intensité de ressources, comme lors de l’assimilation à grande échelle d’actifs, vous pouvez l’exécuter plus fréquemment.

Pour configurer la purge des workflows, ajoutez une nouvelle configuration de purge de workflow d’Adobe Granite via la console OSGi. Configurez et planifiez ensuite le workflow dans le cadre de la période de maintenance hebdomadaire.

Si la purge s’exécute trop longtemps, elle s’arrête. Par conséquent, vous devez vous assurer que vos tâches de purge se terminent pour éviter les cas où l’exécution de la purge des workflows échoue en raison du nombre élevé de workflows.

Par exemple, après avoir exécuté de nombreux workflows non transitoires (qui créent des noeuds d’instance de workflow), vous pouvez exécuter [ACS AEM Commons Workflow Remover](https://adobe-consulting-services.github.io/acs-aem-commons/features/workflow-remover.html) sur une base ad hoc. Il supprime les instances de workflow terminées et redondantes immédiatement sans attendre l’exécution du planificateur de purge de workflow d’Adobe Granite.

### Tâches parallèles maximales     {#maximum-parallel-jobs}

Par défaut, [!DNL Experience Manager] exécute un nombre maximal de tâches parallèles égal au nombre de processeurs sur le serveur. Le problème avec ce paramètre est que, pendant les périodes de charge importante, tous les processeurs sont occupés par des workflows [!UICONTROL DAM Update Asset], ce qui ralentit la réactivité de l&#39;interface utilisateur et empêche [!DNL Experience Manager] d&#39;exécuter d&#39;autres processus qui garantissent les performances et la stabilité du serveur. En tant que bonne pratique, définissez cette valeur sur la moitié des processeurs disponibles sur le serveur en procédant comme suit :

1. Sur [!DNL Experience Manager] Auteur, accédez à `https://[aem_server]:[port]/system/console/slingevent`.

1. Cliquez sur **[!UICONTROL Modifier]** dans chaque file d&#39;attente de processus correspondant à votre implémentation, par exemple **[!UICONTROL Granite Transient Workflow Queue]**.

1. Mettez à jour la valeur de **[!UICONTROL Nombre maximal de tâches parallèles]** et cliquez sur **[!UICONTROL Enregistrer]**.

Configurer une file d’attente à la moitié des processeurs disponibles est une solution exploitable pour commencer. Cependant, vous pouvez être amené à augmenter ou à réduire ce nombre pour atteindre un débit maximal et l’ajuster selon l’environnement. Il existe des files d’attente distinctes pour les workflows transitoires et non transitoires, ainsi que d’autres processus, tels que les workflows externes. Si plusieurs files d’attente configurées à 50 % des processeurs sont activées simultanément, le système peut devenir rapidement surchargé. Les files d’attente utilisées varient considérablement selon les différentes implémentations de l’utilisateur. Par conséquent, vous devrez peut-être les configurer de manière réfléchie pour un maximum d’efficacité sans sacrifier la stabilité des serveurs.

### Configuration des ressources de mise à jour de gestion des ressources numériques {#dam-update-asset-configuration}

Le workflow [!UICONTROL DAM Update Asset] contient une suite complète d&#39;étapes configurées pour les tâches, telles que la génération PTIFF Dynamic Media et l&#39;intégration [!DNL Adobe InDesign Server]. Cependant, plusieurs de ces étapes peuvent être inutiles à la plupart des utilisateurs. Adobe vous recommande de créer une copie personnalisée du modèle de flux de travaux [!UICONTROL DAM Update Asset] et de supprimer toutes les étapes inutiles. Dans ce cas, mettez à jour les lanceurs pour [!UICONTROL DAM Update Asset] afin de pointer vers le nouveau modèle.

L&#39;exécution intensive du flux de travail [!UICONTROL DAM Update Asset] peut augmenter considérablement la taille de la banque de données de vos fichiers. Les résultats d’un test effectué par Adobe ont montré que la taille de l’entrepôt de données peut augmenter d’environ 400 Go si environ 5 500 workflows sont exécutés pendant une période de 8 heures.

Il s’agit d’une augmentation temporaire ; l’entrepôt de données est restauré à sa taille d’origine après avoir exécuté la tâche Nettoyage de la mémoire d’entrepôt de données.

En règle générale, la tâche Nettoyage de la mémoire d’entrepôt de données s’exécute chaque semaine avec d’autres tâches de maintenance planifiées.

Si vous disposez d’un espace disque limité et que vous exécutez [!UICONTROL les workflows ] DAM Update Asset intensément, pensez à planifier la tâche de collecte des déchets plus fréquemment.

#### Génération de rendus au moment de l’exécution {#runtime-rendition-generation}

Les clients utilisent des images de tailles et de formats différents sur leur site web ou pour les distribuer à leurs partenaires professionnels. Étant donné que chaque rendu s’ajoute à l’encombrement d’une ressource dans le référentiel, Adobe recommande d’utiliser cette fonction judicieusement. Pour limiter le nombre de ressources nécessaires pour traiter et stocker des images, vous pouvez générer ces images au moment de l’exécution plutôt que comme rendus pendant l’assimilation.

De nombreux clients de sites mettent en œuvre un servlet d’image qui redimensionne ou recadre les images lorsque cela est nécessaire, ce qui a pour effet d’appliquer une charge supplémentaire à l’instance de publication. Toutefois, tant que ces images peuvent être mises en cache, le défi peut être plus facilement relevé.

Une autre approche consiste à utiliser la technologie Dynamic Media pour redistribuer entièrement la manipulation d&#39;image. En outre, vous pouvez déployer le portail de marque qui prend en charge non seulement les responsabilités de génération de rendu de l&#39;infrastructure [!DNL Experience Manager], mais également l&#39;ensemble du niveau de publication.

#### ImageMagick {#imagemagick}

Si vous personnalisez le flux de travaux [!UICONTROL DAM Update Asset] pour générer des rendus à l’aide d’ImageMagick, l’Adobe vous recommande de modifier le fichier `policy.xml` à l’emplacement `/etc/ImageMagick/`. Par défaut, ImageMagick utilise l’espace disque disponible entier pour le volume du système d’exploitation et la quantité de mémoire disponible. Effectuez les modifications de configuration suivantes dans la section `policymap` de `policy.xml` pour limiter ces ressources.

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
>Une configuration incorrecte peut rendre votre serveur instable si ImageMagick utilise tout l’espace disque disponible. Les modifications de stratégie requises pour traiter des fichiers volumineux à l’aide d’ImageMagick peuvent avoir un impact sur les performances de [!DNL Experience Manager]. Pour plus d’informations, voir [Installation et configuration d’ImageMagick](/help/assets/best-practices-for-imagemagick.md).

>[!NOTE]
>
>Les fichiers ImageMagick `policy.xml` et `configure.xml` sont disponibles à l&#39;adresse `/usr/lib64/ImageMagick-&#42;/config/` au lieu de `/etc/ImageMagick/`.Voir [la documentation ImageMagick](https://www.imagemagick.org/script/resources.php) pour connaître l&#39;emplacement des fichiers de configuration.

Si vous utilisez [!DNL Experience Manager] sur Adobe Managed Services (AMS), contactez le service à la clientèle d’Adobe si vous prévoyez de traiter de nombreux fichiers PSD ou PSB volumineux. Collaborez avec le service à la clientèle d’Adobe pour mettre en oeuvre ces meilleures pratiques pour votre déploiement AMS et choisir les meilleurs outils et modèles possibles pour les formats propriétaires des Adobes. [!DNL Experience Manager] peut ne pas traiter de fichiers PSB très haute résolution de plus de 3 000 x 2 3 000 pixels.

### Écriture différée XMP {#xmp-writeback}

XMP l’écriture différée met à jour la ressource d’origine chaque fois que des métadonnées sont modifiées dans [!DNL Experience Manager], ce qui se traduit par les éléments suivants :

* La ressource elle-même est modifiée
* Une version de la ressource est créée
* [!UICONTROL Ressource de mise à jour de gestion des actifs numériques est exécuté par rapport à la ressource]

Les résultats répertoriés consomment une grande quantité de ressources. Par conséquent, Adobe recommande la [désactivation de l’écriture différée XMP](https://helpx.adobe.com/fr/experience-manager/kb/disable-xmp-writeback.html), si cela n’est pas obligatoire.

L’importation d’une grande quantité de métadonnées peut entraîner une activité d’écriture différée XMP gourmande en ressources si l’indicateur d’exécution de workflow est vérifié. Planifiez une importation de ce type quand le serveur est peu utilisé afin que les performances d’autres utilisateurs ne soient pas affectées.

## Réplication {#replication}

Lors de la réplication des ressources vers un grand nombre d’instances de publication (par exemple, dans une implémentation de sites), Adobe vous recommande d’utiliser la réplication par chaîne. Dans ce cas, l’instance d’auteur est répliquée vers une instance de publication unique qui est répliquée à son tour vers d’autres instances de publication, ce qui libère l’instance d’auteur.

### Configuration de la réplication en chaîne     {#configure-chain-replication}

1. Sélectionnez l’instance de publication vers laquelle vous souhaitez effectuer les réplications en chaîne
1. Sur cette instance de publication, ajoutez des agents de réplication qui pointent vers d’autres instances de publication
1. Sur chacun de ces agents de réplication, activez « À la réception » dans l’onglet « Déclencheurs »

>[!NOTE]
>
>Adobe ne recommande pas d’activer automatiquement les ressources. Cependant, si nécessaire, Adobe recommande d’effectuer cette opération en tant que dernière étape d’un workflow, généralement Ressource de mise à jour de gestion des actifs numériques.

## Recherche des index     {#search-indexes}

Installez [les derniers Service Packs](/help/release-notes/sp-release-notes.md) et les correctifs liés aux performances, car ceux-ci incluent souvent des mises à jour des index système. Voir [conseils d&#39;optimisation des performances](https://helpx.adobe.com/fr/experience-manager/kb/performance-tuning-tips.html) pour certaines optimisations d&#39;index.

Créez des index personnalisés pour les demandes que vous exécutez régulièrement. Pour plus d’informations, consultez la [méthodologie pour l’analyse des requêtes lentes](https://aemfaq.blogspot.com/2014/08/oak-query-log-file-analyzer-tool.html) et la [création d’index personnalisés](/help/sites-deploying/queries-and-indexing.md). Pour des informations complémentaires au sujet des meilleures pratiques de requête et d’index, consultez les [Meilleures pratiques pour les requêtes et l’indexation](/help/sites-deploying/best-practices-for-queries-and-indexing.md).

### Configurations de l’index Lucene {#lucene-index-configurations}

Certaines optimisations peuvent être effectuées sur les configurations de l&#39;index Oak, ce qui permet d&#39;améliorer les [!DNL Experience Manager Assets] performances. Mettez à jour les configurations d’index pour améliorer le temps de réindexation :

1. Ouvrez CRXDe `/crx/de/index.jsp` et connectez-vous en tant qu’utilisateur administrateur.
1. Accédez à `/oak:index/lucene`.
1. Ajoutez une propriété `String[]` `excludedPaths` avec des valeurs `/var`, `/etc/workflow/instances` et `/etc/replication`.
1. Accédez à `/oak:index/damAssetLucene`. Ajoutez une propriété `String[]` `includedPaths` avec la valeur `/content/dam`. Enregistrer les modifications.

Si vos utilisateurs n’ont pas besoin de rechercher des ressources en texte intégral, par exemple, en recherchant du texte dans des documents PDF, désactivez-le. Vous améliorez les performances de l’index en désactivant l’indexation de texte intégral. Pour désactiver l&#39;extraction de texte [!DNL Apache Lucene], procédez comme suit :

1. Dans l&#39;interface [!DNL Experience Manager], accédez à [!UICONTROL Package Manager].
1. Téléchargez et installez le package disponible à l’adresse [disable_indexingbinarytextextraction-10.zip](assets/disable_indexingbinarytextextraction-10.zip).

### Paramètre guessTotal {#guess-total}

Lors de la création de requêtes qui génèrent d’importants ensembles de résultats, utilisez le paramètre `guessTotal` de façon à éviter une utilisation élevée de la mémoire lors de l’exécution.

## Problèmes connus {#known-issues}

### Fichiers volumineux {#large-files}

Il existe deux problèmes importants connus relatifs aux fichiers volumineux dans [!DNL Experience Manager]. Lorsque la taille des fichiers est supérieure à 2 Go, la synchronisation de reprise progressive peut s’exécuter en cas de mémoire insuffisante. Dans certains cas, cela empêche la synchronisation de reprise de s’exécuter. Dans d’autres cas, cela entraîne le blocage de l’instance principale. Ce scénario s’applique à tout fichier [!DNL Experience Manager] de plus de 2 Go, y compris les packages de contenu.

De même, lorsque les fichiers atteignent une taille de 2 Go lors de l’utilisation d’un magasin de données S3 partagé, il peut s’écouler un certain temps avant que le fichier soit complètement conservé du cache au système de fichiers. Par conséquent, lorsque vous avez recours à une réplication sans binaire, il est possible que les données binaires ne soient pas conservées avant la fin de la réplication. Cette situation peut entraîner des problèmes, surtout si la disponibilité des données est importante.

## Test de performance {#performance-testing}

Pour chaque déploiement de [!DNL Experience Manager], établir un régime de test des performances permettant d&#39;identifier et de résoudre rapidement les goulets d&#39;étranglement. Voici quelques points clés.

### Test réseau     {#network-testing}

Pour tous les problèmes liés aux performances du réseau du client, effectuez les tâches suivantes :

* Tester les performances du réseau sur le réseau du client
* Testez les performances du réseau sur le réseau Adobe. Pour les clients AMS, consultez votre CSE pour effectuer des tests sur le réseau Adobe.
* Tester les performances du réseau depuis un autre point d’accès
* En utilisant un outil localisateur de réseau
* Tester par rapport au Dispatcher

### [!DNL Experience Manager] test de déploiement  {#aem-deployment-testing}

Pour réduire la latence et obtenir un débit élevé grâce à une utilisation efficace du processeur et au partage de la charge, surveillez régulièrement les performances de votre déploiement [!DNL Experience Manager]. En particulier :

* Exécutez des tests de charge par rapport au déploiement [!DNL Experience Manager].
* Surveiller les performances de chargement et la réactivité de l’interface utilisateur.

## [!DNL Experience Manager Assets] liste de contrôle des performances et impact des tâches de gestion des actifs  {#checklist}

* Autoriser HTTPS à contourner tous les renifleurs de trafic HTTP d’entreprise.
* Utiliser une connexion câblée pour le chargement de ressources volumineuses.
* Déploiement sur Java 8.
* Définition de paramètres JVM optimaux.
* Configurez une banque de données de système de fichiers ou une banque de données S3.
* Désactivez la génération de sous-ressources. Si elle est activée, AEM processus crée un actif distinct pour chaque page d’une ressource de plusieurs pages. Chacune de ces pages est une ressource individuelle qui consomme de l&#39;espace disque supplémentaire, nécessite un contrôle de version et un traitement supplémentaire du flux de travail. Si vous n’avez pas besoin de pages distinctes, désactivez la génération de sous-ressources et les activités d’extraction de page.
* Activer les workflows transitoires.
* Régler les files d’attente de workflows Granite pour limiter les tâches concurrentes.
* Configurez [!DNL ImageMagick] pour limiter la consommation des ressources.
* Supprimez les étapes inutiles du workflow [!UICONTROL DAM Update Asset].
* Configurer la purge des workflows et versions.
* Optimisez les index avec les derniers Service Packs et correctifs. Vérifiez auprès du service à la clientèle Adobe si d’autres optimisations d’index sont disponibles.
* Utilisez guessTotal afin d’optimiser les performances des requêtes.
* Si vous configurez [!DNL Experience Manager] pour détecter les types de fichiers à partir du contenu des fichiers (en activant **[!UICONTROL Day CQ DAM Mime Type Service]** dans la **[!UICONTROL AEM Web Console]**), téléchargez de nombreux fichiers en vrac pendant les heures creuses, car il consomme beaucoup de ressources.
