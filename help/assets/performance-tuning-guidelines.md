---
title: Réglage des performances  [!DNL Assets]
description: Suggestions et conseils relatifs à  [!DNL Experience Manager]  pour la configuration, les modifications apportées aux composants matériels, les logiciels et éléments réseau pour éviter les goulets d’étranglement et optimiser les performances d’ [!DNL Experience Manager Assets].
contentOwner: AG
mini-toc-levels: 1
role: Architect, Admin
feature: Asset Management
exl-id: 1d9388de-f601-42bf-885b-6a7c3236b97e
solution: Experience Manager, Experience Manager Assets
source-git-commit: 0b90fdd13efc5408ef94ee1966f04a80810b515e
workflow-type: tm+mt
source-wordcount: '2729'
ht-degree: 86%

---

<!-- TBD: Get reviewed by engineering. -->

# Guide de réglage des performances pour [!DNL Adobe Experience Manager Assets] {#assets-performance-tuning-guide}

La configuration de [!DNL Experience Manager Assets] compte plusieurs composants matériels, logiciels et réseau. Selon votre scénario de déploiement, vous pouvez avoir besoin d’apporter des modifications spécifiques à la configuration des composants matériels, logiciels et réseau pour supprimer les goulots d’étranglement en termes de performances.

En outre, l’identification et le respect de certaines instructions en termes d’optimisation des composants matériels et logiciels permettent de créer une base solide afin que votre déploiement de [!DNL Experience Manager Assets] réponde aux attentes en matière de performances, d’évolutivité et de fiabilité.

De faibles performances d’[!DNL Experience Manager Assets] peuvent avoir une incidence sur l’expérience utilisateur en termes de performances interactives, de traitement des ressources, de vitesse de téléchargement et d’autres aspects.

En fait, l’optimisation des performances est une tâche essentielle que vous effectuez avant d’établir des mesures cibles pour chacun de vos projets.

Voici quelques éléments principaux essentiels pour lesquels vous devez identifier et corriger les problèmes de performances avant que ceux-ci aient un impact sur les utilisateurs.

## Plateforme {#platform}

Bien qu’Experience Manager soit pris en charge sur plusieurs plateformes, Adobe a trouvé le meilleur moyen de prendre en charge les outils natifs sous Linux® et Windows, ce qui contribue à des performances optimales et à une facilité d’implémentation. Dans l’idéal, vous devez déployer un système d’exploitation 64 bits pour répondre aux besoins de stockage du déploiement d’[!DNL Experience Manager Assets]. A l’instar de tout déploiement d’Experience Manager, vous devez mettre en œuvre TarMK dans la mesure du possible. Bien que TarMK ne puisse pas mesurer au-delà d’une instance d’auteur simple, il semble offrir de meilleurs résultats que MongoMK. Vous pouvez ajouter des instances de déchargement TarMK pour améliorer la capacité de traitement des workflows de votre déploiement d’[!DNL Experience Manager Assets].

### Dossier temporaire {#temp-folder}

Afin de réduire les délais de chargement des ressources, utilisez un stockage haute performance pour le répertoire temporaire Java. Sous Linux® et Windows, un disque RAM ou SSD peut être utilisé. Dans des environnements cloud, un type de stockage à grande vitesse équivalent peut être utilisé. Par exemple, dans Amazon EC2, un [lecteur éphémère](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/InstanceStorage.html) peut être utilisé pour le dossier temporaire.

En supposant que le serveur dispose de suffisamment de mémoire, configurez un disque RAM. Sous Linux®, exécutez les commandes suivantes pour créer un disque RAM de 8 Go :

```shell
mkfs -q /dev/ram1 800000
 mkdir -p /mnt/aem-tmp
 mount /dev/ram1 /mnt/aem-tmp
 df -H | grep aem-tmp
```

Sous le système d’exploitation Windows, utilisez un pilote tiers pour créer un disque RAM ou pour simplement utiliser le stockage haute performance tel qu’un SSD.

Une fois que le volume temporaire haute performance est prêt, définissez le paramètre JVM `-Djava.io.tmpdir`. Par exemple, vous pouvez ajouter le paramètre JVM sous la variable `CQ_JVM_OPTS` dans le script `bin/start` d’[!DNL Experience Manager] :

`-Djava.io.tmpdir=/mnt/aem-tmp`

## Configuration Java {#java-configuration}

### Version Java {#java-version}

Adobe recommande de déployer [!DNL Experience Manager Assets] sur Java 8 pour des performances optimales.

<!-- TBD: Link to the latest official word around Java.
-->

### Paramètres JVM {#jvm-parameters}

Définissez les paramètres JVM suivants :

* `-XX:+UseConcMarkSweepGC`
* `-Doak.queryLimitInMemory`=500000
* `-Doak.queryLimitReads`=100000
* `-Dupdate.limit`=250000
* `-Doak.fastQuerySize`=true

## Configuration du magasin de données et de la mémoire {#data-store-and-memory-configuration}

### Configuration du magasin de données basé sur les fichiers {#file-data-store-configuration}

Nous recommandons à tous les utilisateurs d’[!DNL Experience Manager Assets] de séparer le magasin de données et l’entrepôt de segments. En outre, la configuration des paramètres `maxCachedBinarySize` et `cacheSizeInMB` peut vous aider à optimiser les performances. Définissez le paramètre `maxCachedBinarySize` selon la plus petite taille de fichier pouvant être contenue dans le cache. Spécifiez la taille du cache en mémoire à utiliser pour l’entrepôt de données dans `cacheSizeInMB`. Adobe vous recommande de définir cette valeur entre 2 et 10 % de la taille totale du tas. Toutefois, les tests de charge/performance peuvent vous aider à déterminer le paramètre idéal.

### Configuration de la taille maximale du cache d’images mis en mémoire tampon    {#configure-the-maximum-size-of-the-buffered-image-cache}

Lors du chargement d’un grand nombre de ressources vers [!DNL Adobe Experience Manager], réduisez la taille maximale configurée du cache d’images mis en mémoire tampon. De cette façon, vous tiendrez compte des pics inattendus de consommation de la mémoire et éviterez l’échec de JVM du fait d’erreurs de mémoire insuffisante. Prenez l’exemple d’un système présentant un tas maximal (paramètre -`Xmx`) de 5 Go, un BlobCache Oak défini sur 1 Go et un cache de documents défini sur 2 Go. Dans ce cas, le cache mis en mémoire tampon prendrait un maximum de 1,25 Go de mémoire, ce qui ne laisserait que 0,75 Go de mémoire pour les pics inattendus.

Configurez la taille du cache mis en mémoire tampon dans la console web OSGi. À l’emplacement `https://host:port/system/console/configMgr/com.day.cq.dam.core.impl.cache.CQBufferedImageCache`, définissez la propriété `cq.dam.image.cache.max.memory` en octets. Par exemple, 1073741824 représente 1 Go (1 024 x 1 024 x 1 024 = 1 Go).

À partir du pack de services 1 d’Experience Manager 6.1, si vous utilisez un nœud `sling:osgiConfig` pour configurer cette propriété, veillez à définir le type de données sur Long.

### Entrepôts de données partagés    {#shared-data-stores}

La mise en œuvre d’un magasin de données basé sur les fichiers, partagé ou S3, peut vous aider à économiser de l’espace disque et à augmenter le débit réseau dans des implémentations à grande échelle. Pour plus d’informations sur les avantages et inconvénients de l’utilisation d’un magasin de données partagé, consultez le guide de dimensionnement d’[Assets](/help/assets/assets-sizing-guide.md).

### Magasin de données S3 {#s-data-store}

La configuration du magasin de données S3 suivante (`org.apache.jackrabbit.oak.plugins.blob.datastore.S3DataStore.cfg`) a permis à Adobe d’extraire 12,8 To d’objets BLOB (Binary Large Objects) d’un magasin de données basé sur les fichiers existant dans un magasin de données S3 vers un site client :

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

Adobe recommande d’activer HTTPS, car de nombreuses entreprises qui possèdent des pare-feu analysent le trafic HTTP, ce qui a une incidence sur les chargements et endommage les fichiers. Pour les chargements de fichiers volumineux, assurez-vous que les utilisateurs disposent d’une connexion filaire au réseau, car les réseaux Wi-Fi saturent rapidement. Pour obtenir des instructions sur l’identification des goulets d’étranglement réseau, consultez le [guide de dimensionnement d’Assets](/help/assets/assets-sizing-guide.md). Pour évaluer les performances du réseau en analysant sa topologie, consultez les [Remarques sur le réseau des ressources](/help/assets/assets-network-considerations.md).

Votre stratégie d’optimisation du réseau dépend essentiellement de la quantité de bande passante disponible et du chargement sur votre instance [!DNL Experience Manager]. Les options de configuration courantes, telles que les pare-feu ou les proxys, peuvent améliorer les performances du réseau. Voici quelques points essentiels à garder à l’esprit :

* Selon votre type d’instance (petite, moyenne ou grande), vérifiez que vous disposez de suffisamment de bande passante réseau pour votre instance Experience Manager. L’allocation d’une bande passante appropriée est particulièrement importante si [!DNL Experience Manager] est hébergé sur AWS.
* Si votre instance [!DNL Experience Manager] est hébergée sur AWS, vous pouvez tirer profit d’une politique de mise à l’échelle polyvalente. Augmentez la taille de l’instance si les utilisateurs s’attendent à une charge élevée. Réduisez sa taille pour une charge moyenne/faible.
* HTTPS : la plupart des utilisateurs et utilisatrices disposent de pare-feu qui détectent le trafic HTTP, ce qui peut avoir un impact négatif sur le chargement des fichiers ou même endommager les fichiers lors de l’opération de chargement.
* Chargements de fichiers volumineux : assurez-vous que les utilisateurs et utilisatrices disposent de connexions câblées au réseau (les connexions Wi-Fi se saturent rapidement).

## Workflows    {#workflows}

### Workflows transitoires {#transient-workflows}

Dans la mesure du possible, définissez le workflow [!UICONTROL Ressource de mise à jour de gestion des ressources numériques] sur l’option Transitoire. Le paramètre réduit considérablement les surcharges nécessaires pour traiter les workflows car, dans ce cas, ceux-ci n’ont pas besoin de respecter les processus de suivi et d’archivage classiques.

1. Accédez à `/miscadmin` dans le déploiement [!DNL Experience Manager] à `https://[aem_server]:[port]/miscadmin`.

1. Développez **[!UICONTROL Outils]** > **[!UICONTROL Workflow]** > **[!UICONTROL Modèles]** > **[!UICONTROL Gestion des ressources numériques]**.

1. Ouvrez la **[!UICONTROL Ressource de mise à jour de la gestion des ressources numériques]**. Depuis le panneau d’outils flottant, basculez vers l’onglet **[!UICONTROL Page]**, puis cliquez sur **[!UICONTROL Propriétés de la page]**.

1. Sélectionnez **[!UICONTROL Workflow transitoire]** puis cliquez sur **[!UICONTROL OK]**.

   >[!NOTE]
   >
   >Certaines fonctions ne prennent pas en charge les workflows transitoires. Si votre déploiement d’[!DNL Assets] requiert ces fonctions, ne configurez pas les workflows transitoires.

Dans les cas où les workflows transitoires ne peuvent pas être utilisés, exécutez la purge des workflows régulièrement pour supprimer les workflows [!UICONTROL Ressource de mise à jour de gestion des ressources numériques] afin de vous assurer que les performances système ne se dégradent pas.

En règle générale, exécutez les workflows de purge une fois par semaine. Toutefois, dans les scénarios qui requièrent un important nombre de ressources, comme l’assimilation de ressources à grande échelle, vous pouvez l’exécuter plus fréquemment.

Pour configurer la purge des workflows, ajoutez une nouvelle configuration de purge de workflow d’Adobe Granite via la console OSGi. Ensuite, configurez et planifiez le workflow dans le cadre de la fenêtre de maintenance hebdomadaire.

Si la purge s’exécute trop longtemps, elle s’arrête. Par conséquent, vous devez vous assurer que vos tâches de purge sont terminées afin d’éviter les situations où la purge des workflows ne se termine pas en raison du nombre élevé de workflows.

Par exemple, après l’exécution d’un grand nombre de workflows transitoires (ce qui crée des nœuds d’instance de workflow), vous pouvez exécuter l’[outil de suppression de workflow ACS AEM Commons](https://adobe-consulting-services.github.io/acs-aem-commons/features/workflow-remover.html) sur une base ponctuelle. Il supprime immédiatement les instances de workflow redondantes et terminées au lieu d’attendre que le planificateur de purge de workflow Adobe Granite s’exécute.

### Tâches parallèles maximales    {#maximum-parallel-jobs}

Par défaut, [!DNL Experience Manager] exécute un nombre maximal de tâches parallèles qui est égal au nombre de processeurs sur le serveur. Le problème avec ce paramètre est que pendant les périodes de charge importante, tous les processeurs sont occupés par des workflows [!UICONTROL Ressource de mise à jour de la gestion des ressources numériques], ce qui ralentit la réactivité de l’interface utilisateur et empêche [!DNL Experience Manager] d’exécuter d’autres processus qui assurent la stabilité et les performances du serveur. En tant que bonne pratique, définissez cette valeur sur la moitié des processeurs disponibles sur le serveur en procédant comme suit :

1. Dans l’Auteur d’[!DNL Experience Manager], accédez à `https://[aem_server]:[port]/system/console/slingevent`.

1. Cliquez sur **[!UICONTROL Modifier]** sur chaque file d’attente de workflow appropriée à votre implémentation (par exemple, la **[!UICONTROL file d’attente de workflow transitoire de Granite]**).

1. Modifiez la valeur des **[!UICONTROL Tâches parallèles maximales]**, puis cliquez sur **[!UICONTROL Enregistrer]**.

Configurer une file d’attente à la moitié des processeurs disponibles est une solution exploitable pour commencer. Cependant, vous pouvez être amené à augmenter ou à réduire ce nombre pour atteindre un débit maximal et l’ajuster selon l’environnement. Il existe des files d’attente distinctes pour les workflows transitoires et non transitoires, ainsi que d’autres processus, tels que les workflows externes. Si plusieurs files d’attente configurées à 50 % des processeurs sont activées simultanément, le système peut devenir rapidement surchargé. Les files d’attente utilisées varient considérablement selon les différentes implémentations de l’utilisateur. Par conséquent, vous devrez peut-être les configurer de manière réfléchie pour garantir une efficacité maximale sans sacrifier la stabilité du serveur.

### Configuration des ressources de mise à jour de gestion des ressources numériques {#dam-update-asset-configuration}

Le workflow [!UICONTROL Ressource de mise à jour de gestion des ressources numériques] contient plusieurs étapes qui sont configurées pour les tâches, telles que la génération de Dynamic Media PTIFF et l’intégration d’[!DNL Adobe InDesign Server]. Cependant, plusieurs de ces étapes peuvent être inutiles à la plupart des utilisateurs. Adobe vous recommande de créer une copie personnalisée du modèle de workflow [!UICONTROL Ressource de mise à jour de gestion des ressources numériques], et de supprimer toutes les étapes inutiles. Dans ce cas, mettez à jour les lanceurs pour que la [!UICONTROL ressource de mise à jour de gestion des ressources numériques] pointent vers le nouveau modèle.

L’exécution intensive du workflow [!UICONTROL &#x200B; Ressource de mise à jour de gestion des ressources numériques &#x200B;] peut augmenter considérablement la taille de votre banque de données de fichiers. Les résultats d’une expérience effectuée par Adobe ont montré que la taille du magasin de données peut augmenter d’environ 400 Go si environ 5 500 workflows sont effectués dans les 8 heures.

Il s’agit d’une augmentation temporaire, et le magasin de données est restauré à sa taille d’origine après l’exécution de la tâche de récupération de l’espace mémoire du magasin de données.

En règle générale, la tâche de récupération de l’espace mémoire du magasin de données s’exécute chaque semaine avec d’autres tâches de maintenance planifiées.

Si vous disposez d’un espace disque limité et exécutez de façon intensive le workflow [!UICONTROL Ressource de mise à jour de gestion des ressources numériques], pensez à planifier la tâche de nettoyage plus fréquemment.

#### Génération de rendus au moment de l’exécution {#runtime-rendition-generation}

Les clients utilisent des images de tailles et de formats différents sur leur site web ou pour les distribuer à leurs partenaires professionnels. Étant donné que chaque rendu s’ajoute à l’encombrement d’une ressource dans le référentiel, Adobe recommande d’utiliser cette fonction judicieusement. Pour réduire la quantité de ressources nécessaires au traitement et au stockage des images, vous pouvez générer ces images au moment de l’exécution plutôt que sous forme de rendus lors de l’ingestion.

De nombreux clients de sites mettent en œuvre un servlet d’image qui redimensionne ou recadre les images lorsque cela est nécessaire, ce qui a pour effet d’appliquer une charge supplémentaire à l’instance de publication. Cependant, tant que ces images peuvent être mises en cache, le défi peut être atténué.

Une autre approche consiste à utiliser la technologie Dynamic Media pour annuler entièrement la manipulation d’images. En outre, vous pouvez déployer un Brand Portal qui accepte non seulement les responsabilités de génération de rendu à partir de l’infrastructure [!DNL Experience Manager], mais également la totalité du niveau de publication.

#### ImageMagick {#imagemagick}

Si vous personnalisez le workflow [!UICONTROL Ressource de mise à jour de gestion des ressources numériques] pour générer des rendus à l’aide d’ImageMagick, Adobe vous recommande de modifier le fichier `policy.xml` à l’adresse `/etc/ImageMagick/`. Par défaut, ImageMagick utilise l’espace disque disponible entier pour le volume du système d’exploitation et la quantité de mémoire disponible. Effectuez les modifications de configuration suivantes dans la section `policymap` de `policy.xml` pour limiter ces ressources.

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
>Une configuration incorrecte peut rendre votre serveur instable si ImageMagick utilise tout l’espace disque disponible. Les modifications de politique requises pour traiter des fichiers volumineux à l’aide d’ImageMagick peuvent avoir une incidence sur les performances d’[!DNL Experience Manager]. Pour plus d’informations, consultez la section [Installation et configuration d’ImageMagick](/help/assets/best-practices-for-imagemagick.md).

>[!NOTE]
>
>Les fichiers `policy.xml` et `configure.xml` d’ImageMagick sont disponibles à l’adresse `/usr/lib64/ImageMagick-&#42;/config/` au lieu de `/etc/ImageMagick/`. Consultez la [documentation d’ImageMagick](https://www.imagemagick.org/script/resources.php) pour obtenir l’emplacement des fichiers de configuration.

Si vous utilisez [!DNL Experience Manager] dans Adobe Managed Services (AMS), contactez l’assistance clientèle d’Adobe si vous envisagez de traiter un grand nombre de fichiers PSD ou PSB volumineux. Collaborez avec un représentant du service clientèle d’Adobe afin de mettre en œuvre ces bonnes pratiques pour votre déploiement AMS et de choisir les meilleurs outils et modèles possibles pour les formats propriétaires d’Adobe. Il se peut qu’[!DNL Experience Manager] ne puisse pas traiter des fichiers PSB à très haute résolution de plus de 30 000 x 23 000 pixels.

### Écriture différée XMP {#xmp-writeback}

L’écriture différée XMP met à jour les ressources d’origine chaque fois que les métadonnées sont modifiées dans [!DNL Experience Manager], ce qui permet ce qui suit :

* La ressource elle-même est modifiée.
* Une nouvelle version de la ressource est créée
* La [!UICONTROL Ressource de mise à jour de gestion des ressources numériques] est exécutée par rapport à la ressource.

Les résultats répertoriés consomment une grande quantité de ressources. Par conséquent, Adobe recommande la désactivation de l’écriture différée XMP si elle n’est pas obligatoire. Pour plus d&#39;informations, consultez la section [Écriture différée XMP](/help/assets/xmp-writeback.md).

L’importation d’un grand nombre de métadonnées peut entraîner une activité d’écriture différée XMP gourmande en ressources si l’indicateur Exécuter les workflows est coché. Planifiez une telle importation pendant une période de faible utilisation du serveur afin que les performances des autres utilisateurs et utilisatrices ne soient pas affectées.

## Réplication {#replication}

Lors de la réplication des ressources vers un grand nombre d’instances de publication (par exemple, dans une implémentation Sites), Adobe vous recommande d’utiliser la réplication par chaîne. Dans ce cas, l’instance de création se réplique sur une instance de publication unique qui, à son tour, se réplique sur les autres instances de publication, libérant ainsi l’instance de création.

### Configuration de la réplication en chaîne    {#configure-chain-replication}

1. Sélectionnez l’instance de publication vers laquelle vous souhaitez effectuer les réplications en chaîne
1. Sur cette instance de publication, ajoutez des agents de réplication qui pointent vers les autres instances de publication
1. Sur chacun de ces agents de réplication, activez « À réception » dans l’onglet « Déclencheurs »

>[!NOTE]
>
>Adobe ne recommande pas d’activer automatiquement les ressources. Cependant, si nécessaire, Adobe recommande d’effectuer cette opération en tant qu’étape finale d’un workflow, généralement Ressource de mise à jour de gestion des ressources numériques.

## Recherche des index    {#search-indexes}

Installez [les derniers pack de services](/help/release-notes/release-notes.md) et les correctifs liés aux performances, car ils incluent souvent des mises à jour des index système. Consultez les [conseils sur l’optimisation des performances](https://experienceleague.adobe.com/fr/docs/experience-manager-65/content/assets/administer/performance-tuning-guidelines) pour certaines optimisations d’index.

Créez des index personnalisés pour les demandes que vous exécutez régulièrement. Pour plus d’informations, consultez la [méthodologie d’analyse des requêtes lentes](https://aemfaq.blogspot.com/2014/08/oak-query-log-file-analyzer-tool.html) et [la conception d’index personnalisés](/help/sites-deploying/queries-and-indexing.md). Pour des informations complémentaires au sujet des bonnes pratiques concernant les requêtes et les index, consultez les [Bonnes pratiques relatives aux requêtes et à l’indexation](/help/sites-deploying/best-practices-for-queries-and-indexing.md).

### Configurations de l’index Lucene {#lucene-index-configurations}

Certaines optimisations peuvent être effectuées sur les configurations d’index Oak qui peuvent améliorer les performances d’[!DNL Experience Manager Assets]. Mettez à jour les configurations d’index pour améliorer le temps de réindexation :

1. Ouvrez CRXDe `/crx/de/index.jsp` et connectez-vous en tant qu’utilisateur administrateur.
1. Accédez à `/oak:index/lucene`.
1. Ajouter une propriété `String[]` `excludedPaths` avec des valeurs `/var`, `/etc/workflow/instances` et `/etc/replication`.
1. Accédez à `/oak:index/damAssetLucene`. Ajouter une propriété `String[]` `includedPaths` avec la valeur `/content/dam`. Enregistrez les modifications.

Si vos utilisateurs n’ont pas besoin d’effectuer une recherche de texte intégral de ressources, par exemple, lorsqu’ils parcourent le texte des documents PDF, désactivez-la. Vous améliorez les performances de l’index en désactivant l’indexation de texte intégral. Pour désactiver l’extraction de texte [!DNL Apache Lucene], procédez comme suit :

1. Dans l’interface [!DNL Experience Manager], accédez à [!UICONTROL Gestionnaire de packages].
1. Téléchargez et installez le package disponible à l’adresse [disable_indexingbinarytextextraction-10.zip](assets/disable_indexingbinarytextextraction-10.zip).

### Paramètre guessTotal {#guess-total}

Lors de la création de requêtes qui génèrent d’importants ensembles de résultats, utilisez le paramètre `guessTotal` de façon à éviter une utilisation élevée de la mémoire lors de l’exécution.

## Problèmes connus {#known-issues}

### Fichiers volumineux {#large-files}

Il existe deux problèmes importants connus relatifs aux fichiers volumineux dans [!DNL Experience Manager]. Lorsque la taille des fichiers est supérieure à 2 Go, la synchronisation de reprise progressive peut s’exécuter en cas de mémoire insuffisante. Dans certains cas, cela empêche la synchronisation de reprise de s’exécuter. Dans d’autres cas, cela entraîne le blocage de l’instance principale. Ce scénario s’applique à tous les fichiers dans [!DNL Experience Manager] dont la taille est supérieure à 2 Go, y compris les packages de contenu.

De même, lorsque les fichiers atteignent 2 Go lors de l’utilisation d’un magasin de données S3 partagé, la restitution du fichier à partir du cache vers le système de fichiers peut prendre un certain temps. Par conséquent, lorsque vous avez recours à une réplication sans binaire, il est possible que les données binaires ne soient pas conservées avant la fin de la réplication. Cette situation peut entraîner des problèmes, surtout si la disponibilité des données est importante.

## Test de performance {#performance-testing}

Pour chaque déploiement d’[!DNL Experience Manager], créez un régime de tests de performances qui permet d’identifier et de résoudre les goulots d’étranglement rapidement. Voici quelques points clés.

### Test réseau    {#network-testing}

Pour tous les problèmes de performances réseau du client, effectuez les tâches suivantes :

* Tester les performances du réseau depuis le réseau client
* Testez les performances du réseau depuis le réseau Adobe. Pour les clients AMS, consultez votre CSE pour effectuer des tests sur le réseau Adobe.
* Tester les performances du réseau à partir d’un autre point d’accès
* En utilisant un outil de référence de réseau
* Test par rapport au Dispatcher

### Test de déploiement d’[!DNL Experience Manager] {#aem-deployment-testing}

Afin de réduire au maximum la latence et d’obtenir un débit élevé grâce à l’utilisation efficace du processeur et au partage de charge, surveillez régulièrement les performances de votre déploiement d’[!DNL Experience Manager]. En particulier :

* Exécutez des tests de chargement pour le déploiement d’[!DNL Experience Manager].
* Surveillez les performances de chargement et la réactivité de l’interface utilisateur.

## Liste de contrôle des performances d’[!DNL Experience Manager Assets] et de l’impact des tâches de gestion des ressources {#checklist}

* Autoriser HTTPS à contourner tous les renifleurs de trafic HTTP d’entreprise.
* Utilisez une connexion câblée pour le chargement de ressources volumineuses.
* Déployez sur Java 8.
* Définissez des paramètres JVM optimaux.
* Configurez un magasin de données de système de fichiers ou un magasin de données S3.
* Désactivez la génération de sous-ressources. Si elle est activée, le workflow d’AEM crée une ressource distincte pour chaque page dans une ressource multi-page. Chacune de ces pages est une ressource en elle-même, qui consomme de l’espace disque supplémentaire et requiert la création de versions et un traitement de workflow supplémentaire. Si vous n’avez pas besoin de pages séparées, désactivez les activités d’extraction de page et de génération de sous-ressources.
* Activez les workflows transitoires.
* Réglez les files d’attente de workflows Granite pour limiter les tâches concurrentes.
* Configurez [!DNL ImageMagick] pour limiter la consommation de ressources.
* Supprimez les étapes inutiles du workflow [!UICONTROL Ressource de mise à jour de gestion des ressources numériques].
* Configurez la purge des workflows et des versions.
* Optimisez les index avec les derniers packs de services et correctifs. Vérifiez auprès de l’assistance clientèle Adobe toutes les optimisations d’index supplémentaires qui pourraient être disponibles.
* Utilisez guessTotal afin d’optimiser les performances des requêtes.
* Si vous configurez [!DNL Experience Manager] pour détecter des types de fichiers à partir de leur contenu (en activant le **[!UICONTROL service de type MIME de gestion des ressources numériques Day CQ]** dans la **[!UICONTROL Console web AEM]**), chargez les fichiers en bloc aux heures creuses, car cela consomme beaucoup de ressources.
