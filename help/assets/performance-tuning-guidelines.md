---
title: Réglage des performances [!DNL Assets].
description: Suggestions et conseils sur [!DNL Experience Manager] configuration, modifications apportées aux composants matériels, logiciels et réseau pour supprimer les goulets d’étranglement et optimiser les performances de [!DNL Experience Manager Assets].
contentOwner: AG
mini-toc-levels: 1
role: Architect, Admin
feature: Asset Management
exl-id: 1d9388de-f601-42bf-885b-6a7c3236b97e
source-git-commit: e3caa3e3067cf5e29cfcdf4286047eb346aefa23
workflow-type: tm+mt
source-wordcount: '2753'
ht-degree: 52%

---

<!-- TBD: Get reviewed by engineering. -->

# [!DNL Adobe Experience Manager Assets] guide d’optimisation des performances {#assets-performance-tuning-guide}

Un [!DNL Experience Manager Assets] La configuration contient un certain nombre de composants matériels, logiciels et réseau. Selon votre scénario de déploiement, vous pouvez avoir besoin d’apporter des modifications spécifiques à la configuration des composants matériels, logiciels et réseau pour supprimer les goulots d’étranglement en termes de performances.

En outre, l’identification et le respect de certaines instructions relatives à l’optimisation du matériel et des logiciels vous aident à créer une base solide qui permet à vos [!DNL Experience Manager Assets] déploiement pour répondre aux attentes en matière de performances, d’évolutivité et de fiabilité.

Mauvaise performance dans [!DNL Experience Manager Assets] peuvent avoir un impact sur l’expérience utilisateur en ce qui concerne les performances interactives, le traitement des ressources, la vitesse de téléchargement et d’autres aspects.

En fait, l’optimisation des performances est une tâche essentielle que vous effectuez avant d’établir des mesures cibles pour chacun de vos projets.

Voici quelques éléments principaux essentiels pour lesquels vous devez identifier et corriger les problèmes de performances avant que ceux-ci aient un impact sur les utilisateurs.

## Plateforme {#platform}

Bien que Experience Manager soit pris en charge sur un certain nombre de plateformes, Adobe a trouvé la meilleure prise en charge des outils natifs sous Linux et Windows, ce qui contribue à des performances optimales et à la facilité d’implémentation. Idéalement, vous devez déployer un système d’exploitation 64 bits pour répondre aux exigences de mémoire élevée d’un [!DNL Experience Manager Assets] déploiement. Comme pour tout déploiement de Experience Manager, vous devez implémenter TarMK chaque fois que possible. Bien que TarMK ne puisse pas mesurer au-delà d’une instance d’auteur simple, il semble offrir de meilleurs résultats que MongoMK. Vous pouvez ajouter des instances de déchargement TarMK pour augmenter la puissance de traitement du workflow de votre [!DNL Experience Manager Assets] déploiement.

### Dossier temporaire {#temp-folder}

Pour améliorer les temps de chargement des ressources, utilisez un stockage haute performance pour le répertoire temporaire Java. Sous Linux et Windows, un disque SSD ou RAM peut être utilisé. Dans des environnements cloud, un type de stockage à grande vitesse équivalent peut être utilisé. Par exemple, dans Amazon EC2, une [disque éphémère](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/InstanceStorage.html) Le lecteur peut être utilisé pour le dossier temporaire.

En supposant que le serveur dispose de suffisamment de mémoire, configurez un disque RAM. Sous Linux, exécutez les commandes suivantes pour créer un disque RAM de 8 Go :

```shell
mkfs -q /dev/ram1 800000
 mkdir -p /mnt/aem-tmp
 mount /dev/ram1 /mnt/aem-tmp
 df -H | grep aem-tmp
```

Sous Windows OS, utilisez un pilote tiers pour créer un lecteur RAM ou utilisez simplement un stockage haute performance tel que SSD.

Une fois que le volume temporaire haute performance est prêt, définissez le paramètre JVM . `-Djava.io.tmpdir`. Par exemple, vous pouvez ajouter le paramètre JVM ci-dessous au `CQ_JVM_OPTS` dans la variable `bin/start` script de [!DNL Experience Manager]:

`-Djava.io.tmpdir=/mnt/aem-tmp`

## Configuration Java {#java-configuration}

### Version Java {#java-version}

Adobe recommande de déployer [!DNL Experience Manager Assets] sur Java 8 pour des performances optimales.

<!-- TBD: Link to the latest official word around Java.
-->

### Paramètres JVM  {#jvm-parameters}

Définissez les paramètres JVM suivants :

* `-XX:+UseConcMarkSweepGC`
* `-Doak.queryLimitInMemory`=500000
* `-Doak.queryLimitReads`=100000
* `-Dupdate.limit`=250000
* `-Doak.fastQuerySize`=true

## Configuration d’entrepôt de données et de mémoire {#data-store-and-memory-configuration}

### Configuration d’entrepôt de données basé sur les fichiers {#file-data-store-configuration}

Il est recommandé de séparer l’entrepôt de données de l’entrepôt de segments pour tous les [!DNL Experience Manager Assets] utilisateurs. En outre, la configuration des paramètres `maxCachedBinarySize` et `cacheSizeInMB` peut vous aider à optimiser les performances. Définissez le paramètre `maxCachedBinarySize` selon la plus petite taille de fichier pouvant être contenue dans le cache. Spécifiez la taille du cache en mémoire à utiliser pour l’entrepôt de données dans `cacheSizeInMB`. Adobe vous recommande de définir cette valeur entre 2 et 10 % de la taille totale du tas. Toutefois, le chargement ou le test des performances peuvent vous aider à déterminer le paramètre idéal.

### Configuration de la taille maximale du cache d’images mis en mémoire tampon    {#configure-the-maximum-size-of-the-buffered-image-cache}

Lors du chargement de grandes quantités de ressources vers [!DNL Adobe Experience Manager], pour permettre des pics inattendus de la consommation de mémoire et empêcher l’échec de JVM avec des erreurs OutOfMemoryErrors, réduisez la taille maximale configurée du cache d’images mis en mémoire tampon. Prenez l’exemple d’un système présentant un tas maximal (paramètre -`Xmx`) de 5 Go, un BlobCache Oak défini sur 1 Go et un cache de documents défini sur 2 Go. Dans ce cas, le cache mis en mémoire tampon prendrait au maximum 1,25 Go, ce qui laisserait seulement 0,75 Go pour les pics inattendus.

Configurez la taille du cache mis en mémoire tampon dans la console web OSGi. À l’emplacement `https://host:port/system/console/configMgr/com.day.cq.dam.core.impl.cache.CQBufferedImageCache`, définissez la propriété `cq.dam.image.cache.max.memory` en octets. Par exemple, 1073741824 représente 1 Go (1 024 x 1 024 x 1 024 = 1 Go).

À partir de Experience Manager 6.1 SP1, si vous utilisez un `sling:osgiConfig` pour configurer cette propriété, veillez à définir le type de données sur Long. Pour plus de détails, voir [CQBufferedImageCache utilise le tas pendant le téléchargement des ressources](https://helpx.adobe.com/fr/experience-manager/kb/cqbufferedimagecache-consumes-heap-during-asset-uploads.html).

### Entrepôts de données partagés    {#shared-data-stores}

La mise en œuvre d’un entrepôt de données basé sur les fichiers, partagé ou S3, peut vous aider à économiser de l’espace disque et à augmenter le débit réseau dans des implémentations à grande échelle. Pour plus d’informations sur les avantages et inconvénients de l’utilisation d’une banque de données partagée, voir [Guide de dimensionnement des ressources](/help/assets/assets-sizing-guide.md).

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

Adobe recommande d’activer HTTPS, car de nombreuses entreprises qui possèdent des pare-feu analysent le trafic HTTP, ce qui a une incidence sur les chargements et endommage les fichiers. Pour les chargements de fichiers volumineux, assurez-vous que les utilisateurs disposent d’une connexion filaire au réseau, car les réseaux Wi-Fi saturent rapidement. Pour obtenir des instructions sur l’identification des goulets d’étranglement réseau, voir [Guide de dimensionnement des ressources](/help/assets/assets-sizing-guide.md). Pour évaluer les performances du réseau en analysant la topologie du réseau, voir [Considérations sur le réseau d’Assets](/help/assets/assets-network-considerations.md).

Votre stratégie d’optimisation du réseau dépend principalement de la quantité de bande passante disponible et de la charge associée à votre [!DNL Experience Manager] instance. Les options de configuration courantes, notamment les pare-feu ou les proxys, peuvent améliorer les performances du réseau. Voici quelques points essentiels à prendre en compte :

* En fonction du type d’instance (petite, moyenne, grande), assurez-vous de disposer de suffisamment de bande passante réseau pour votre instance de Experience Manager. Une allocation de bande passante adéquate est particulièrement importante si [!DNL Experience Manager] est hébergée sur AWS.
* Si votre [!DNL Experience Manager] est hébergée sur AWS. Vous pouvez bénéficier d’une stratégie de mise à l’échelle polyvalente. Augmentez la taille de l’instance si les utilisateurs prévoient une charge élevée. Réduisez-la pour une charge moyenne/faible.
* HTTPS : la plupart des utilisateurs possèdent des pare-feu qui analysent le trafic HTTP, ce qui est susceptible d’avoir une incidence sur le chargement des fichiers ou même endommager des fichiers lors de l’opération de chargement.
* Chargements volumineux : assurez-vous que les utilisateurs disposent d’une connexion filaire au réseau (les connexions Wi-Fi sont rapidement saturées).

## Workflows    {#workflows}

### Workflows transitoires {#transient-workflows}

Dans la mesure du possible, définissez la variable [!UICONTROL Ressources de mise à jour de gestion des actifs numériques] workflow vers Transitoire. Le paramètre réduit considérablement les surcharges nécessaires pour traiter les workflows car, dans ce cas, ils n’ont pas besoin de faire l’objet d’un suivi et de processus d’archivage classiques.

1. Accédez à `/miscadmin` dans le [!DNL Experience Manager] déploiement à `https://[aem_server]:[port]/miscadmin`.

1. Développer **[!UICONTROL Outils]** > **[!UICONTROL Workflow]** > **[!UICONTROL Modèles]** > **[!UICONTROL dam]**.

1. Ouvrir **[!UICONTROL Ressources de mise à jour de gestion des actifs numériques]**. Depuis le panneau d’outils flottant, basculez vers l’onglet **[!UICONTROL Page]**, puis cliquez sur **[!UICONTROL Propriétés de la page]**.

1. Sélectionner **[!UICONTROL Processus transitoire]** et cliquez sur **[!UICONTROL OK]**.

   >[!NOTE]
   >
   >Certaines fonctions ne prennent pas en charge les workflows transitoires. Si votre [!DNL Assets] Le déploiement nécessite ces fonctionnalités, ne configurez pas de workflows transitoires.

Dans les cas où les workflows transitoires ne peuvent pas être utilisés, exécutez régulièrement la purge des workflows pour supprimer les workflows archivés. [!UICONTROL Ressources de mise à jour de gestion des actifs numériques] les workflows pour s’assurer que les performances du système ne se dégradent pas.

En règle générale, exécutez les workflows de purge une fois par semaine. Cependant, dans les scénarios gourmands en ressources, tels que l’ingestion de ressources à grande échelle, vous pouvez l’exécuter plus fréquemment.

Pour configurer la purge des workflows, ajoutez une nouvelle configuration de purge de workflow d’Adobe Granite via la console OSGi. Configurez et planifiez ensuite le workflow dans le cadre de la période de maintenance hebdomadaire.

Si la purge s’exécute trop longtemps, elle s’arrête. Par conséquent, vous devez vous assurer que vos tâches de purge se terminent pour éviter les cas où l’exécution de la purge des workflows échoue en raison du nombre élevé de workflows.

Par exemple, après avoir exécuté de nombreux workflows transitoires (ce qui crée des noeuds d’instance de workflow), vous pouvez exécuter [Outil de suppression de processus ACS AEM Commons](https://adobe-consulting-services.github.io/acs-aem-commons/features/workflow-remover.html) sur une base ponctuelle. Il supprime les instances de workflow terminées et redondantes immédiatement sans attendre l’exécution du planificateur de purge de workflow d’Adobe Granite.

### Tâches parallèles maximales    {#maximum-parallel-jobs}

Par défaut, [!DNL Experience Manager] exécute un nombre maximal de tâches parallèles égal au nombre de processeurs sur le serveur. Le problème avec ce paramètre est que pendant les périodes de charge importante, tous les processeurs sont occupés par [!UICONTROL Ressources de mise à jour de gestion des actifs numériques] workflows, ralentissement de la réactivité de l’interface utilisateur et prévention [!DNL Experience Manager] d’exécuter d’autres processus qui assurent la stabilité et les performances du serveur. En tant que bonne pratique, définissez cette valeur sur la moitié des processeurs disponibles sur le serveur en procédant comme suit :

1. Activé [!DNL Experience Manager] Création, accès `https://[aem_server]:[port]/system/console/slingevent`.

1. Cliquez sur **[!UICONTROL Modifier]** sur chaque file d’attente de workflow correspondant à votre implémentation, par exemple **[!UICONTROL File d’attente des workflows transitoires Granite]**.

1. Mettre à jour la valeur de **[!UICONTROL Tâches parallèles maximales]** et cliquez sur **[!UICONTROL Enregistrer]**.

Configurer une file d’attente à la moitié des processeurs disponibles est une solution exploitable pour commencer. Cependant, vous pouvez être amené à augmenter ou à réduire ce nombre pour atteindre un débit maximal et l’ajuster selon l’environnement. Il existe des files d’attente distinctes pour les workflows transitoires et non transitoires, ainsi que d’autres processus, tels que les workflows externes. Si plusieurs files d’attente configurées à 50 % des processeurs sont activées simultanément, le système peut devenir rapidement surchargé. Les files d’attente utilisées varient considérablement selon les différentes implémentations de l’utilisateur. Par conséquent, vous devrez peut-être les configurer de manière réfléchie pour un maximum d’efficacité sans sacrifier la stabilité des serveurs.

### Configuration des ressources de mise à jour de gestion des ressources numériques {#dam-update-asset-configuration}

Le [!UICONTROL Ressources de mise à jour de gestion des actifs numériques] workflow contient une suite complète d’étapes configurées pour les tâches, telles que la génération de PTIFF Dynamic Media et [!DNL Adobe InDesign Server] intégration. Cependant, plusieurs de ces étapes peuvent être inutiles à la plupart des utilisateurs. Adobe vous recommande de créer une copie personnalisée de la variable [!UICONTROL Ressources de mise à jour de gestion des actifs numériques] modèle de workflow et supprimez toutes les étapes inutiles. Dans ce cas, mettez à jour les lanceurs pour [!UICONTROL Ressources de mise à jour de gestion des actifs numériques] pour pointer vers le nouveau modèle.

L’exécution de la variable [!UICONTROL Ressources de mise à jour de gestion des actifs numériques] Un workflow intensif peut considérablement augmenter la taille de votre banque de données de fichiers. Les résultats d’un test effectué par Adobe ont montré que la taille de l’entrepôt de données peut augmenter d’environ 400 Go si environ 5 500 workflows sont exécutés pendant une période de 8 heures.

Il s’agit d’une augmentation temporaire ; l’entrepôt de données est restauré à sa taille d’origine après avoir exécuté la tâche Nettoyage de la mémoire d’entrepôt de données.

En règle générale, la tâche Nettoyage de la mémoire d’entrepôt de données s’exécute chaque semaine avec d’autres tâches de maintenance planifiées.

Si vous disposez d’un espace disque limité et exécutez [!UICONTROL Ressources de mise à jour de gestion des actifs numériques] les workflows intensivement, pensez à planifier la tâche de nettoyage plus fréquemment.

#### Génération de rendus au moment de l’exécution {#runtime-rendition-generation}

Les clients utilisent des images de tailles et de formats différents sur leur site web ou pour les distribuer à leurs partenaires professionnels. Étant donné que chaque rendu s’ajoute à l’encombrement d’une ressource dans le référentiel, Adobe recommande d’utiliser cette fonction judicieusement. Pour limiter le nombre de ressources nécessaires pour traiter et stocker des images, vous pouvez générer ces images au moment de l’exécution plutôt que comme rendus pendant l’assimilation.

De nombreux clients de sites mettent en œuvre un servlet d’image qui redimensionne ou recadre les images lorsque cela est nécessaire, ce qui a pour effet d’appliquer une charge supplémentaire à l’instance de publication. Toutefois, tant que ces images peuvent être mises en cache, le défi peut être plus facilement relevé.

Une autre approche consiste à utiliser la technologie Dynamic Media pour annuler entièrement la manipulation d’images. En outre, vous pouvez déployer Brand Portal qui prend en charge les responsabilités de génération de rendu de la [!DNL Experience Manager] mais également l’ensemble du niveau de publication.

#### ImageMagick {#imagemagick}

Si vous personnalisez la variable [!UICONTROL Ressources de mise à jour de gestion des actifs numériques] pour générer des rendus à l’aide d’ImageMagick, Adobe vous recommande de modifier la variable `policy.xml` fichier à l’emplacement `/etc/ImageMagick/`. Par défaut, ImageMagick utilise l’espace disque disponible entier pour le volume du système d’exploitation et la quantité de mémoire disponible. Apportez les modifications de configuration suivantes dans le `policymap` section `policy.xml` pour limiter ces ressources.

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

En outre, définissez le chemin du dossier temporaire d’ImageMagick dans le fichier `configure.xml` (ou en définissant la variable d’environnement `MAGICK_TEMPORARY_PATH`) sur une partition de disque disposant d’un espace et d’IOPS appropriés.

>[!CAUTION]
>
>Une configuration incorrecte peut rendre votre serveur instable si ImageMagick utilise tout l’espace disque disponible. Les modifications de stratégie requises pour traiter des fichiers volumineux à l’aide d’ImageMagick peuvent avoir une incidence sur la variable [!DNL Experience Manager] performance. Pour plus d’informations, voir [Installation et configuration d’ImageMagick](/help/assets/best-practices-for-imagemagick.md).

>[!NOTE]
>
>ImageMagick `policy.xml` et `configure.xml` Les fichiers sont disponibles à l’adresse `/usr/lib64/ImageMagick-&#42;/config/` au lieu de `/etc/ImageMagick/`.Voir [Documentation d’ImageMagick](https://www.imagemagick.org/script/resources.php) pour l’emplacement des fichiers de configuration.

Si vous utilisez [!DNL Experience Manager] sur Adobe Managed Services (AMS), contactez le service clientèle si vous envisagez de traiter un grand nombre de fichiers PSD ou PSB volumineux. Collaborez avec le représentant du service clientèle d’Adobe afin de mettre en oeuvre ces bonnes pratiques pour votre déploiement AMS et de choisir les meilleurs outils et modèles possibles pour les formats propriétaires d’Adobe. [!DNL Experience Manager] peut ne pas traiter des fichiers PSB à très haute résolution de plus de 3 000 x 2 3 000 pixels.

### Écriture différée XMP {#xmp-writeback}

XMP l’écriture différée met à jour la ressource d’origine chaque fois que les métadonnées sont modifiées dans [!DNL Experience Manager], ce qui se traduit par ce qui suit :

* La ressource elle-même est modifiée
* Une version de la ressource est créée
* [!UICONTROL Ressource de mise à jour de gestion des actifs numériques est exécuté par rapport à la ressource]

Les résultats répertoriés consomment une grande quantité de ressources. Par conséquent, Adobe recommande de désactiver l’écriture différée XMP si elle n’est pas requise. Pour plus d’informations, voir [Écriture différée XMP](https://experienceleague.adobe.com/docs/experience-manager-64/assets/administer/xmp-writeback.html?lang=fr).

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

## Recherche des index    {#search-indexes}

Installer [les derniers Service Packs ;](/help/release-notes/release-notes.md) et les correctifs liés aux performances, car ils incluent souvent des mises à jour des index système. Voir [conseils sur l’optimisation des performances](https://experienceleague.adobe.com/docs/experience-manager-65/assets/administer/performance-tuning-guidelines.html?lang=en) pour certaines optimisations d’index.

Créez des index personnalisés pour les demandes que vous exécutez régulièrement. Pour plus d’informations, consultez la [méthodologie pour l’analyse des requêtes lentes](https://aemfaq.blogspot.com/2014/08/oak-query-log-file-analyzer-tool.html) et la [création d’index personnalisés](/help/sites-deploying/queries-and-indexing.md). Pour des informations complémentaires au sujet des meilleures pratiques de requête et d’index, consultez les [Meilleures pratiques pour les requêtes et l’indexation](/help/sites-deploying/best-practices-for-queries-and-indexing.md).

### Configurations de l’index Lucene {#lucene-index-configurations}

Certaines optimisations peuvent être effectuées sur les configurations d’index Oak qui peuvent contribuer à améliorer [!DNL Experience Manager Assets] performance. Mettez à jour les configurations d’index pour améliorer le temps de réindexation :

1. Ouvrir CRXDe `/crx/de/index.jsp` et connectez-vous en tant qu’utilisateur administrateur.
1. Accédez à `/oak:index/lucene`.
1. Ajouter un `String[]` property `excludedPaths` avec des valeurs `/var`, `/etc/workflow/instances`, et `/etc/replication`.
1. Accédez à `/oak:index/damAssetLucene`. Ajouter un `String[]` property `includedPaths` avec valeur `/content/dam`. Enregistrer les modifications.

Si vos utilisateurs n’ont pas besoin d’effectuer une recherche de texte intégral de ressources, par exemple, en parcourant le texte des documents du PDF, désactivez-le. Vous améliorez les performances de l’index en désactivant l’indexation de texte intégral. Pour désactiver [!DNL Apache Lucene] extraction de texte, procédez comme suit :

1. Dans [!DNL Experience Manager] interface, accès [!UICONTROL Gestionnaire de modules].
1. Téléchargez et installez le module disponible à l’adresse [disable_indexingbinarytextextraction-10.zip](assets/disable_indexingbinarytextextraction-10.zip).

### Paramètre guessTotal {#guess-total}

Lors de la création de requêtes qui génèrent d’importants ensembles de résultats, utilisez le paramètre `guessTotal` de façon à éviter une utilisation élevée de la mémoire lors de l’exécution.

## Problèmes connus {#known-issues}

### Fichiers volumineux {#large-files}

Il existe deux problèmes importants connus relatifs aux fichiers volumineux dans [!DNL Experience Manager]. Lorsque la taille des fichiers est supérieure à 2 Go, la synchronisation de reprise progressive peut s’exécuter en cas de mémoire insuffisante. Dans certains cas, cela empêche la synchronisation de reprise de s’exécuter. Dans d’autres cas, cela entraîne le blocage de l’instance principale. Ce scénario s’applique à tout fichier dans [!DNL Experience Manager] qui dépasse 2 Go, y compris les modules de contenu.

De même, lorsque les fichiers atteignent 2 Go lors de l’utilisation d’un entrepôt de données S3 partagé, il peut s’écouler un certain temps avant que le fichier ne soit entièrement conservé du cache vers le système de fichiers. Par conséquent, lorsque vous avez recours à une réplication sans binaire, il est possible que les données binaires ne soient pas conservées avant la fin de la réplication. Cette situation peut entraîner des problèmes, surtout si la disponibilité des données est importante.

## Test de performance {#performance-testing}

Pour chaque [!DNL Experience Manager] , établissez un régime de test de performance qui peut identifier et résoudre rapidement les goulets d’étranglement. Voici quelques points clés.

### Test réseau    {#network-testing}

Pour tous les problèmes liés aux performances du réseau du client, effectuez les tâches suivantes :

* Tester les performances du réseau sur le réseau du client
* Testez les performances du réseau sur le réseau Adobe. Pour les clients AMS, consultez votre CSE pour effectuer des tests sur le réseau Adobe.
* Tester les performances du réseau depuis un autre point d’accès
* En utilisant un outil localisateur de réseau
* Tester par rapport au Dispatcher

### [!DNL Experience Manager] test de déploiement {#aem-deployment-testing}

Pour réduire la latence et atteindre un débit élevé grâce à une utilisation efficace du processeur et au partage de charge, surveillez les performances de votre [!DNL Experience Manager] déploiement régulier. En particulier :

* Exécutez des tests de chargement sur le [!DNL Experience Manager] déploiement.
* Surveiller les performances de chargement et la réactivité de l’interface utilisateur.

## [!DNL Experience Manager Assets] liste de contrôle des performances et impact des tâches de gestion des ressources {#checklist}

* Autoriser HTTPS à contourner tous les renifleurs de trafic HTTP d’entreprise.
* Utiliser une connexion câblée pour le chargement de ressources volumineuses.
* Déploiement sur Java 8.
* Définition de paramètres JVM optimaux.
* Configurez un entrepôt de données de système de fichiers ou un entrepôt de données S3.
* Désactivez la génération de sous-ressources. Si elle est activée, AEM workflow crée une ressource distincte pour chaque page dans une ressource multi-page. Chacune de ces pages est une ressource individuelle qui consomme de l’espace disque supplémentaire, nécessite un contrôle de version et un traitement de workflow supplémentaire. Si vous n’avez pas besoin de pages distinctes, désactivez les activités de génération et d’extraction de sous-ressources.
* Activer les workflows transitoires.
* Régler les files d’attente de workflows Granite pour limiter les tâches concurrentes.
* Configurer [!DNL ImageMagick] pour limiter la consommation des ressources.
* Supprimez les étapes inutiles du [!UICONTROL Ressources de mise à jour de gestion des actifs numériques] workflow.
* Configurer la purge des workflows et versions.
* Optimisez les index avec les derniers Service Packs et correctifs. Vérifiez auprès du service clientèle d’Adobe toutes les optimisations d’index supplémentaires qui peuvent être disponibles.
* Utilisez guessTotal afin d’optimiser les performances des requêtes.
* Si vous configurez [!DNL Experience Manager] pour détecter les types de fichiers à partir du contenu des fichiers (en activant **[!UICONTROL Service Day CQ DAM Mime Type]** dans le **[!UICONTROL Console web d’AEM]**), téléchargez de nombreux fichiers en bloc pendant les heures creuses, car cela consomme beaucoup de ressources.
