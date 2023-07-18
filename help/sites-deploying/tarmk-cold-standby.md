---
title: Exécuter AEM avec TarMK Cold Standby
seo-title: How to Run AEM with TarMK Cold Standby
description: Découvrez comment créer, configurer et gérer une configuration TarMK Cold Secondaire.
seo-description: Learn how to create, configure and maintain a TarMK Cold Standby setup.
uuid: 004fdf3e-517c-452b-8db1-a47d6b31d8ba
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: deploying
discoiquuid: 9559e837-a87e-4ee7-8ca6-13b42c74e6bf
docset: aem65
feature: Configuring
exl-id: dadde3ee-d60c-4b87-9af0-a12697148161
source-git-commit: 259f257964829b65bb71b5a46583997581a91a4e
workflow-type: tm+mt
source-wordcount: '2729'
ht-degree: 48%

---

# Exécuter AEM avec TarMK Cold Standby{#how-to-run-aem-with-tarmk-cold-standby}

## Présentation {#introduction}

La capacité Secondaire froide du micronoyau Tar permet à une ou plusieurs instances AEM Secondaires de se connecter à une instance Principale. Le processus de synchronisation n’est qu’une façon de signifier qu’il est effectué uniquement de la Principale aux instances Secondaires.

L’objectif des instances Secondaires est de garantir une Live Copy du référentiel maître et d’assurer un basculement rapide sans perte de données si le maître n’est pas disponible pour une raison quelconque.

Le contenu est synchronisé de manière linéaire entre l’instance Principale et les instances Secondaires sans aucun contrôle d’intégrité pour la corruption de fichier ou de référentiel. En raison de cette conception, les instances Secondaires sont des copies exactes de l’instance Principale et ne peuvent pas aider à atténuer les incohérences sur les instances Principales.

>[!NOTE]
>
>La fonctionnalité Cold Secondaire est destinée à sécuriser les scénarios où une haute disponibilité est requise sur **author** instances. Pour les situations où un niveau de disponibilité élevé est requis sur les instances de **publication** à l’aide du micronoyau Tar, Adobe recommande d’utiliser une ferme de publication.
>
>Pour plus d’informations sur les déploiements disponibles, consultez la page [Déploiements recommandés](/help/sites-deploying/recommended-deploys.md).

>[!NOTE]
>
>Lorsque l’instance secondaire est configurée ou dérivée du nœud principal, elle permet uniquement d’accéder à la console suivante (pour les activités liées à l’administration) :
>
>* Console web OSGI
>
>Les autres consoles ne sont pas accessibles.

## Fonctionnement {#how-it-works}

Sur l’instance de l’AEM Principale, un port TCP est ouvert et écoute les messages entrants. Actuellement, il existe deux types de messages que les Secondaires enverront au maître :

* un message demandant l’identifiant de segment de l’en-tête actuel ;
* un message demandant des données de segment avec un identifiant spécifié ;

Le Secondaire demande périodiquement l’identifiant du segment de l’en-tête actuel de la Principale. Si le segment est inconnu localement, il sera récupéré. S’il est déjà présent, les segments sont comparés et les segments référencés seront également demandés, si nécessaire.

>[!NOTE]
>
>Les instances Secondaires ne reçoivent aucun type de requêtes, car elles s’exécutent en mode de synchronisation uniquement. La seule section disponible sur une instance de secours est la console web, afin de faciliter le regroupement et la configuration des services. 

Un déploiement classique du processus TarMK Cold Standby :

![chlimage_1](assets/chlimage_1.png)

## Autres caractéristiques {#other-characteristics}

### Robustesse {#robustness}

Le flux de données est conçu pour détecter et gérer automatiquement les problèmes de connexion et de réseau. Tous les paquets sont regroupés avec des sommes de contrôle et dès que des problèmes de connexion ou des paquets endommagés se produisent, les mécanismes de reprise sont déclenchés.

#### Performance {#performance}

L’activation de TarMK Cold Secondaire sur la Principale instance n’a pratiquement aucun impact mesurable sur les performances. La consommation supplémentaire du processeur est très faible et le disque dur supplémentaire et les E/S réseau ne doivent pas entraîner de problèmes de performances.

Sur le Secondaire, vous pouvez vous attendre à une consommation élevée du processeur lors du processus de synchronisation. Étant donné que la procédure n’est pas multi-thread, elle ne peut pas être accélérée en utilisant plusieurs coeurs. Si aucune donnée n’est modifiée ou transférée, il n’y aura aucune activité mesurable. La vitesse de connexion varie en fonction de l’environnement matériel et réseau, mais elle ne dépend pas de la taille du référentiel ou de l’utilisation du protocole SSL. Gardez cela à l’esprit lorsque vous estimez le temps nécessaire à une synchronisation initiale ou lorsque de nombreuses données ont été modifiées entre-temps sur le noeud Principal.

#### Sécurité {#security}

En supposant que toutes les instances s’exécutent dans la même zone de sécurité intranet, le risque d’une violation de sécurité est considérablement réduit. Néanmoins, vous pouvez ajouter une couche de sécurité supplémentaire en activant les connexions SSL entre les Secondaires et le maître. Cela réduit la possibilité que les données soient compromises par un intermédiaire.

De plus, vous pouvez spécifier les instances Secondaires autorisées à se connecter en limitant l’adresse IP des requêtes entrantes. Cela permet de garantir qu’aucun utilisateur de l’intranet ne peut copier le référentiel.

>[!NOTE]
>
>Il est recommandé d’ajouter un équilibreur de charge entre Dispatcher et les serveurs qui font partie de la configuration de Coldy Secondaire. L’équilibreur de charge doit être configuré pour diriger le trafic de l’utilisateur uniquement vers le **Principal** afin d’assurer la cohérence et d’empêcher la copie du contenu sur l’instance Secondaire par d’autres moyens que le mécanisme Secondaire Cold.

## Création d’une configuration Secondaire TarMK Cold {#creating-an-aem-tarmk-cold-standby-setup}

>[!CAUTION]
>
>Le PID du magasin de noeuds Segment et le service de stockage Secondaire ont changé dans AEM 6.3 par rapport aux versions précédentes, comme suit :
>
>* de org.apache.jackrabbit.oak.**plugins**.segment.standby.store.StandbyStoreService à org.apache.jackrabbit.oak.segment.standby.store.StandbyStoreService
>* de org.apache.jackrabbit.oak.**plugins**.segment.SegmentNodeStoreService à org.apache.jackrabbit.oak.segment.SegmentNodeStoreService
>
>Veillez à effectuer les ajustements de configuration nécessaires pour refléter cette modification.

Pour créer une configuration Secondaire à froid TarMK, vous devez d’abord créer les instances Secondaires en effectuant une copie du système de fichiers de l’ensemble du dossier d’installation de la Principale vers un nouvel emplacement. Vous pouvez ensuite démarrer chaque instance avec un mode d’exécution spécifiant son rôle (`primary` ou `standby`).

Consultez ci-dessous la procédure devant être suivie afin de créer une installation avec une instance principale et une instance de secours : 

1. Installez AEM.

1. Arrêtez votre instance et copiez son dossier d’installation à l’emplacement d’exécution de l’instance Secondaire froide. Même si l’exécution s’effectue à partir de différents ordinateurs, veillez à attribuer à chaque dossier un nom explicite (comme *aem-Principal* ou *aem-Secondaire*) pour différencier les instances.
1. Accédez au dossier d&#39;installation de l&#39;instance Principale et :

   1. Vérifiez et supprimez toutes les configurations OSGi précédentes qui pourraient être répertoriées sous `aem-primary/crx-quickstart/install`.

   1. Créez un fichier appelé `install.primary` sous `aem-primary/crx-quickstart/install`.

   1. Créez les configurations requises pour le magasin de nœuds et l’entrepôt de données de votre choix sous `aem-primary/crx-quickstart/install/install.primary`.
   1. Créez un fichier nommé `org.apache.jackrabbit.oak.segment.standby.store.StandbyStoreService.config` au même emplacement et configurez-le conformément aux exigences. Pour plus d’informations sur les options de configuration, consultez la section [Configuration](/help/sites-deploying/tarmk-cold-standby.md#configuration). 

   1. Si vous utilisez une instance AEM TarMK avec magasin de données externe, créez un dossier nommé `crx3` sous `aem-primary/crx-quickstart/install`, nommé `crx3`.

   1. Placez le fichier de configuration du magasin de données dans le dossier `crx3`. 

   Par exemple, si vous exécutez une instance AEM TarMK avec un magasin de données de fichiers externe, vous aurez besoin de ces fichiers de configuration :

   * `aem-primary/crx-quickstart/install/install.primary/org.apache.jackrabbit.oak.segment.SegmentNodeStoreService.config`
   * `aem-primary/crx-quickstart/install/install.primary/org.apache.jackrabbit.oak.segment.standby.store.StandbyStoreService.config`
   * `aem-primary/crx-quickstart/install/crx3/org.apache.jackrabbit.oak.plugins.blob.datastore.FileDataStore.config`

   Vous trouverez ci-dessous des exemples de configuration pour une instance principale :

   **Exemple de** **org.apache.jackrabbit.oak.segment.SegmentNodeStoreService.config**

   ```xml
   org.apache.sling.installer.configuration.persist=B"false"
   customBlobStore=B"true"
   standby=B"false"
   ```

   **Exemple de org.apache.jackrabbit.oak.segment.Secondaire.store.StandbyStoreService.config**

   ```xml
   org.apache.sling.installer.configuration.persist=B"false"
   mode="primary"
   port=I"8023"
   ```

   **Exemple de org.apache.jackrabbit.oak.plugins.blob.datastore.FileDataStore.config**

   ```xml
   org.apache.sling.installer.configuration.persist=B"false"
   path="./crx-quickstart/repository/datastore"
   minRecordLength=I"16384"
   ```

1. Démarrez la Principale en vous assurant de spécifier le mode d’exécution Principal :

   ```shell
   java -jar quickstart.jar -r primary,crx3,crx3tar
   ```

1. Créez un enregistreur de journalisation Apache Sling pour le **org.apache.jackrabbit.oak.segment** module. Définissez le niveau du journal sur « Déboguer », puis orientez la sortie du journal vers un fichier journal distinct, tel que */logs/tarmk-coldstandby.log*. Pour plus d’informations, consultez la section [Journalisation](/help/sites-deploying/configure-logging.md).
1. Accédez à l’emplacement du **Secondaire** et démarrez-le en exécutant le fichier jar.
1. Créez la même configuration de journalisation que pour la Principale. Arrêtez ensuite l’instance.
1. Ensuite, préparez l’instance Secondaire. Pour ce faire, procédez comme pour l’instance Principale :

   1. Supprimez tous les fichiers que vous pouvez avoir sous `aem-standby/crx-quickstart/install`.
   1. Créez un dossier nommé `install.standby` sous `aem-standby/crx-quickstart/install`.

   1. Créez deux fichiers de configuration nommés :

      * `org.apache.jackrabbit.oak.segment.SegmentNodeStoreService.config`
      * `org.apache.jackrabbit.oak.segment.standby.store.StandbyStoreService.config`

   1. Créez dossier nommé `crx3` sous `aem-standby/crx-quickstart/install`

   1. Créer une configuration de magasin de données et placez-la sous `aem-standby/crx-quickstart/install/crx3`. Pour cet exemple, le fichier que vous devez créer est le suivant :

      * org.apache.jackrabbit.oak.plugins.blob.datastore.FileDataStore.config

   1. Editez les fichiers et créez les paramétrages nécessaires.

   Vous trouverez ci-dessous des exemples de fichiers de configuration pour une instance Secondaire standard :

   **Exemple de org.apache.jackrabbit.oak.segment.SegmentNodeStoreService.config**

   ```xml
   org.apache.sling.installer.configuration.persist=B"false"
   name="Oak-Tar"
   service.ranking=I"100"
   standby=B"true"
   customBlobStore=B"true"
   ```

   **Exemple de org.apache.jackrabbit.oak.segment.Secondaire.store.StandbyStoreService.config**

   ```xml
   org.apache.sling.installer.configuration.persist=B"false"
   mode="standby"
   primary.host="127.0.0.1"
   port=I"8023"
   secure=B"false"
   interval=I"5"
   standby.autoclean=B"true"
   ```

   **Exemple de org.apache.jackrabbit.oak.plugins.blob.datastore.FileDataStore.config**

   ```xml
   org.apache.sling.installer.configuration.persist=B"false"
   path="./crx-quickstart/repository/datastore"
   minRecordLength=I"16384"
   ```

1. Démarrez le **Secondaire** en utilisant le mode d’exécution Secondaire :

   ```xml
   java -jar quickstart.jar -r standby,crx3,crx3tar
   ```

Le service peut également être configuré via la console web, en procédant comme suit :

1. Accédez à la console web : *https://serveraddress:serverport/system/console/configMgr*.
1. Recherche d’un service appelé **Service Secondaire Tar de segment Apache Jackrabbit Oak** et double-cliquez dessus pour modifier les paramètres.
1. Enregistrez les paramètres et redémarrez les instances pour que les nouveaux paramètres puissent prendre effet.

>[!NOTE]
>
>Vous pouvez vérifier le rôle d’une instance à tout moment en vérifiant la présence des modes d’exécution **principaux** ou **de secours** dans la console web des paramètres Sling.
>
>Ceci peut être effectué en accédant à *https://localhost:4502/system/console/status-slingsettings* et en vérifiant la ligne **« modes d’exécution »**.

## Première synchronisation  {#first-time-synchronization}

Une fois la préparation terminée et le Secondaire démarré pour la première fois, le trafic réseau entre les instances sera important, car le Secondaire rattrape la Principale. Vous pouvez consulter les logs pour connaître l&#39;état de la synchronisation.

Sur l’instance de secours *tarmk-coldstandby.log*, vous verrez des entrées de ce type :

```xml
    *DEBUG* [defaultEventExecutorGroup-2-1] org.apache.jackrabbit.oak.segment.standby.store.StandbyStore trying to read segment ec1f739c-0e3c-41b8-be2e-5417efc05266

    *DEBUG* [nioEventLoopGroup-3-1] org.apache.jackrabbit.oak.segment.standby.codec.SegmentDecoder received type 1 with id ec1f739c-0e3c-41b8-be2e-5417efc05266 and size 262144

    *DEBUG* [defaultEventExecutorGroup-2-1] org.apache.jackrabbit.oak.segment.standby.store.StandbyStore got segment ec1f739c-0e3c-41b8-be2e-5417efc05266 with size 262144

    *DEBUG* [defaultEventExecutorGroup-2-1] org.apache.jackrabbit.oak.segment.file.TarWriter Writing segment ec1f739c-0e3c-41b8-be2e-5417efc05266 to /mnt/crx/author/crx-quickstart/repository/segmentstore/data00016a.tar
```

Dans le *error.log*, vous devriez voir une entrée telle que :

```xml
*INFO* [FelixStartLevel] org.apache.jackrabbit.oak.segment.standby.store.StandbyStoreService started standby sync with 10.20.30.40:8023 at 5 sec.
```

Dans le fragment de code de journal ci-dessus, *10.20.30.40* est l’adresse IP de la Principale.

Dans le **Principal** *tarmk-coldstandby.log*, vous verrez des entrées telles que :

```xml
    *DEBUG* [nioEventLoopGroup-3-2] org.apache.jackrabbit.oak.segment.standby.store.CommunicationObserver got message ‘s.d45f53e4-0c33-4d4d-b3d0-7c552c8e3bbd’ from client c7a7ce9b-1e16-488a-976e-627100ddd8cd

    *DEBUG* [nioEventLoopGroup-3-2] org.apache.jackrabbit.oak.segment.standby.server.StandbyServerHandler request segment id d45f53e4-0c33-4d4d-b3d0-7c552c8e3bbd

    *DEBUG* [nioEventLoopGroup-3-2] org.apache.jackrabbit.oak.segment.standby.server.StandbyServerHandler sending segment d45f53e4-0c33-4d4d-b3d0-7c552c8e3bbd to /10.20.30.40:34998

    *DEBUG* [nioEventLoopGroup-3-2] org.apache.jackrabbit.oak.segment.standby.store.CommunicationObserver did send segment with 262144 bytes to client c7a7ce9b-1e16-488a-976e-627100ddd8cd
```

Dans ce cas, le &quot;client&quot; mentionné dans le journal est le **Secondaire** instance.

Une fois que ces entrées n’apparaissent plus dans le journal, vous pouvez supposer que le processus de synchronisation est terminé.

Bien que les entrées ci-dessus indiquent que le mécanisme d’interrogation fonctionne correctement, il est souvent utile d’identifier s’il existe bien des données en cours de synchronisation pendant que le processus d’interrogation a lieu. Pour ce faire, recherchez les entrées comme suit :

```xml
*DEBUG* [defaultEventExecutorGroup-156-1] org.apache.jackrabbit.oak.segment.file.TarWriter Writing segment 3a03fafc-d1f9-4a8f-a67a-d0849d5a36d5 to /<<CQROOTDIRECTORY>>/crx-quickstart/repository/segmentstore/data00014a.tar
```

De même, lorsque l’exécution a lieu avec un fichier `FileDataStore` non partagé, des messages comme celui-ci confirmeront que les fichiers binaires sont correctement transmis :

```xml
*DEBUG* [nioEventLoopGroup-228-1] org.apache.jackrabbit.oak.segment.standby.codec.ReplyDecoder received blob with id eb26faeaca7f6f5b636f0ececc592f1fd97ea1a9#169102 and size 169102
```

### Configuration {#configuration}

Les paramètres OSGi suivants sont disponibles pour le service Cold Secondaire :

* **Persist Configuration :** s’il est activé, la configuration est stockée dans le référentiel au lieu des fichiers de configuration OSGi traditionnels. Il est recommandé de garder ce paramètre désactivé sur des systèmes d’exploitation afin que la configuration principale ne soit pas effectuée par l’instance de secours.

* **Mode (`mode`) :** permet de sélectionner le mode d’exécution d’une instance.

* **Port (port) :** le port à utiliser pour la communication. La valeur par défaut est `8023`.

* **Hôte principal (`primary.host`) :** l’hôte de l’instance principale. Ce paramètre s’applique uniquement à l’instance de secours.
* **Intervalle de synchronisation (`interval`) :** ce paramètre détermine l’intervalle entre la requête de synchronisation et s’applique uniquement à l’instance de secours.

* **Plages IP autorisées (`primary.allowed-client-ip-ranges`) :** plages IP sur lesquelles l’instance principale autorisera la connexion.
* **Sécuriser (`secure`) ** : active le chiffrement SSL. Pour que ce paramètre fonctionne, il doit être activé sur toutes les instances.
* **Délai d’expiration de lecture Standby (`standby.readtimeout`) :** délai d’expiration pour les demandes provenant de l’instance de secours, en millisecondes. La valeur par défaut utilisée est de 60 000 (une minute).

* **Nettoyage automatique de secours (`standby.autoclean`) :** appelez cette méthode de nettoyage si la taille du magasin augmente lors d’un cycle de synchronisation..

>[!NOTE]
>
>Il est vivement recommandé que les identifiants de référentiel Principal et Secondaire soient différents afin de les rendre séparément inutilisables pour des services tels que le déchargement.
>
>La meilleure façon de s’assurer que cette opération est de supprimer la variable *sling.id* sur le Secondaire et redémarrant l&#39;instance.

## Procédures de basculement {#failover-procedures}

Si l’instance principale échoue, vous pouvez choisir l’une des instances de secours pour la remplacer, en modifiant le mode d’exécution de lancement, tel qu’expliqué ci-après :

>[!NOTE]
>
>Les fichiers de configuration doivent également être modifiés afin qu’ils correspondent aux paramètres utilisés pour une instance principale.

1. Accédez à l’emplacement de l’instance de secours sur votre ordinateur et arrêtez-la. 

1. Si vous avez configuré un équilibreur de charge, vous pouvez supprimer l’instance principale à partir de la configuration de l’équilibreur de charge.
1. Sauvegardez le dossier `crx-quickstart` depuis le dossier d’installation de secours. Cela peut être utilisé comme point de départ lors de la configuration d’une nouvelle instance de secours. 

1. Redémarrez l’instance à l’aide du mode d’exécution `primary` :

   ```shell
   java -jar quickstart.jar -r primary,crx3,crx3tar
   ```

1. Ajoutez la nouvelle Principale à l’équilibreur de charge.
1. Créez et démarrez une nouvelle instance Secondaire. Pour plus d’informations, reportez-vous à la procédure ci-dessus de la section [Création d’une configuration AEM TarMK Cold Standby](/help/sites-deploying/tarmk-cold-standby.md#creating-an-aem-tarmk-cold-standby-setup).

## Application de correctifs à une configuration Secondaire à froid {#applying-hotfixes-to-a-cold-standby-setup}

La méthode recommandée pour appliquer des correctifs à une configuration Cold Standby consiste à les installer sur la Principale instance, puis à les cloner dans une nouvelle instance Cold Secondaire avec les correctifs installés.

Pour ce faire, procédez comme suit :

1. Arrêtez le processus de synchronisation sur l’instance Cold Standby en accédant à la console JMX et en utilisant le bean **org.apache.jackrabbit.oak: Status (&quot;Standby&quot;)**. Pour plus d’informations sur la façon de procéder, reportez-vous à la section [Surveillance](#monitoring).
1. Arrêtez l&#39;instance Secondaire froide.
1. Installez le correctif sur la Principale instance. Pour plus d’informations sur la façon d’installer un correctif, consultez la section [Fonctionnement des packages](/help/sites-administering/package-manager.md).
1. Après l’installation, vérifiez si les problèmes persistent sur l’instance.
1. Supprimez l’instance Secondaire froide en supprimant son dossier d’installation.
1. Arrêtez la Principale instance et clonez-la en exécutant une copie du système de fichiers de l’intégralité de son dossier d’installation à l’emplacement du Secondaire froid.
1. Reconfigurez le clone nouvellement créé pour agir comme une instance Secondaire froide. Pour plus d’informations, voir [Création d’une configuration  TarMK Cold Secondaire.](/help/sites-deploying/tarmk-cold-standby.md#creating-an-aem-tarmk-cold-standby-setup)
1. Démarrez les instances Principale et Secondaire froide.

## Surveillance {#monitoring}

La fonction expose les informations à l’aide de JMX ou de MBeans. Cela vous permet d’examiner l’état actuel du Secondaire et du maître à l’aide de la variable [Console JMX](/help/sites-administering/jmx-console.md). Ces informations se trouvent dans un MBean de `type org.apache.jackrabbit.oak:type="Standby"` nommé `Status`.

**Secondaire**

En observant une instance Secondaire, vous exposez un noeud. L’ID est généralement un UUID générique.

Ce noeud possède cinq attributs en lecture seule :

* `Running:` valeur booléenne indiquant si le processus de synchronisation fonctionne.

* `Mode:` client : suivi des UUID utilisés pour identifier une instance. Notez que cet UUID change chaque fois que la configuration est mise à jour.

* `Status:` représentation textuelle du statut actuel (par exemple `running` ou `stopped`).

* `FailedRequests:` le nombre d’erreurs consécutives.
* `SecondsSinceLastSuccess:` nombre de secondes depuis la dernière communication réussie avec le serveur. La valeur `-1` s’affiche si aucune communication n’a réussie.

Il existe également trois méthodes invocables : 

* `start():` lance le processus de synchronisation.
* `stop():` arrête le processus de synchronisation.
* `cleanup():` exécute l’opération de nettoyage de l’instance de secours.

**Instance principale**

L’observation de la Principale expose certaines informations générales via un MBean dont la valeur d’identifiant est le numéro de port utilisé par le service Secondaire TarMK (8023 par défaut). La plupart des méthodes et attributs sont identiques à ceux du Secondaire, mais certains diffèrent :

* `Mode:` affiche toujours la valeur `primary`.

De plus, des informations relatives à 10 clients (instances Secondaires) au maximum connectés au maître peuvent être récupérées. L’ID MBean est l’UUID de l’instance. Il n’existe aucune méthode invokable pour ces MBeans, mais certains attributs en lecture seule très utiles :

* `Name:` l’ID du client.
* `LastSeenTimestamp:` l’horodatage de la dernière demande dans une représentation textuelle.
* `LastRequest:` la dernière demande du client.
* `RemoteAddress:` l’adresse IP du client.
* `RemotePort:` le port que le client a utilisé pour la dernière demande.
* `TransferredSegments:` le nombre total de segments transférés à ce client.
* `TransferredSegmentBytes:` le nombre total d’octets transférés à ce client.

## Maintenance du référentiel Cold Standby {#cold-standby-repository-maintenance}

### Nettoyage de révision {#revision-clean}

>[!NOTE]
>
>Si vous exécutez le [Nettoyage des révisions en ligne](/help/sites-deploying/revision-cleanup.md) sur l’instance principale, la procédure manuelle présentée ci-dessous n’est pas nécessaire. Par ailleurs, si vous utilisez ce processus, l’opération `cleanup ()` sur l’instance secondaire sera effectuée automatiquement.

>[!NOTE]
>
>N’exécutez pas le nettoyage des révisions hors ligne sur le Secondaire. Cela n’est pas nécessaire et ne réduit pas la taille de l’entrepôt de segments.

Adobe recommande d’exécuter une maintenance régulière pour éviter l’augmentation excessive de référentiel au fil du temps. Pour effectuer manuellement la maintenance Secondaire du référentiel à froid, procédez comme suit :

1. Arrêtez le processus secondaire sur l’instance secondaire en accédant à la console JMX et en utilisant le bean **org.apache.jackrabbit.oak: Status (&quot;Standby&quot;)**. Pour plus d’informations sur cette procédure, reportez-vous à la section [Surveillance](/help/sites-deploying/tarmk-cold-standby.md#monitoring) ci-dessous.

1. Arrêtez la Principale instance AEM.
1. Exécutez l’outil de compression Oak sur la Principale instance. Pour plus d’informations, consultez la section [Maintenance du référentiel](/help/sites-deploying/storage-elements-in-aem-6.md#maintaining-the-repository).
1. Démarrez la Principale instance.
1. Démarrez le processus Secondaire sur l’instance Secondaire en utilisant le même bean JMX que celui décrit à la première étape.
1. Observez les journaux et attendez la fin de la synchronisation. Il se peut qu’une augmentation substantielle au niveau du référentiel de secours se produise à ce moment-là.
1. Exécutez l’opération `cleanup()` sur l’instance de secours, en utilisant le bean JMX décrit dans la première étape.

Il se peut que la synchronisation de l’instance de secours avec l’instance principale prenne plus de temps que prévu, car la compression hors ligne consiste à réécrire l’historique du référentiel, augmentant ainsi substantiellement le temps de calcul des modifications du référentiel. Notez également qu’une fois ce processus terminé, le référentiel sur l’instance de secours aura approximativement la même taille que le référentiel sur l’instance principale.

Vous pouvez également copier manuellement le référentiel Principal vers le Secondaire après l’exécution de la compression sur la Principale, en reconstruisant essentiellement le Secondaire à chaque exécution de la compression.

### Récupérer de l’espace mémoire du magasin de données {#data-store-garbage-collection}

Il est important d’exécuter de temps en temps le nettoyage de la mémoire sur les instances du magasin de données des fichiers. Autrement, les fichiers binaires supprimés resteront sur le système de fichiers, ce qui contribue à surcharger le lecteur. Pour lancer la récupération de l’espace mémoire, suivez la procédure ci-dessous :

1. Exécutez le processus de maintenance du référentiel Cold Standby, comme expliqué dans la section [ci-dessus](/help/sites-deploying/tarmk-cold-standby.md#cold-standby-repository-maintenance).
1. Une fois le processus de maintenance terminé et les instances relancées, procédez comme suit :

   * Sur l’instance principale, exécutez le nettoyage de la mémoire du magasin de données via le bean JMX approprié, tel que décrit dans [cet article](/help/sites-administering/data-store-garbage-collection.md#running-data-store-garbage-collection-via-the-jmx-console).
   * Sur l’instance de secours, le nettoyage de la mémoire du magasin de données est uniquement disponible via le MBean **BlobGarbageCollection** - `startBlobGC()`. Le **RepositoryManagement** MBean n’est pas disponible sur l’instance de secours.

   >[!NOTE]
   >
   >Si vous n’utilisez pas de magasin de données partagé, le nettoyage de la mémoire doit d’abord être exécuté sur l’instance principale, puis sur l’instance de secours.
