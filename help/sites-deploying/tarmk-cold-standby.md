---
title: Exécuter AEM avec TarMK Cold Standby
description: Découvrez comment créer, configurer et gérer une configuration TarMK Cold Standby.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: deploying
docset: aem65
feature: Administering
exl-id: dadde3ee-d60c-4b87-9af0-a12697148161
solution: Experience Manager, Experience Manager Sites
role: Admin
source-git-commit: 5575628c54e2e588dfae4c34383af7d6d55ce859
workflow-type: tm+mt
source-wordcount: '2680'
ht-degree: 93%

---

# Exécuter AEM avec TarMK Cold Standby{#how-to-run-aem-with-tarmk-cold-standby}

## Présentation {#introduction}

La capacité Cold Standby du micronoyau Tar permet à une ou plusieurs instances Adobe Experience Manager (AEM) de secours de se connecter à une instance principale. Le processus de synchronisation n’est qu’une façon de le faire, c’est-à-dire qu’il s’effectue uniquement de l’instance principale vers les instances de secours.

L’objectif des instances de secours est de garantir une Live Copy des données du référentiel principal et d’assurer un basculement rapide sans perte de données au cas où l’instance principale serait indisponible pour une raison quelconque.

Le contenu est synchronisé de manière linéaire entre l’instance principale et les instances de secours sans aucune vérification d’intégrité pour détecter la corruption de fichier ou de référentiel. En raison de cette conception, les instances de secours sont des copies exactes de l’instance principale et ne peuvent pas aider à atténuer les incohérences sur les instances principales.

>[!NOTE]
>
>La fonctionnalité Cold Standby est destinée à sécuriser les scénarios où une haute disponibilité est requise sur les instances de **création**. Pour les situations où un niveau de disponibilité élevé est requis sur les instances de **publication** à l’aide du micronoyau Tar, Adobe recommande d’utiliser une batterie de publication.
>
>Pour plus d’informations sur les déploiements disponibles, consultez la page [Déploiements recommandés](/help/sites-deploying/recommended-deploys.md).

>[!NOTE]
>
>Lorsque l’instance de secours est configurée ou dérivée du nœud principal, elle permet uniquement d’accéder à la console suivante (pour les activités liées à l’administration) :
>
>* Console web OSGI
>
>Les autres consoles ne sont pas accessibles.

## Fonctionnement {#how-it-works}

Sur l’instance principale d’AEM, un port TCP est ouvert et écoute les messages entrants. Actuellement, il existe deux types de messages que l’instance de secours envoie à l’instance principale :

* un message demandant l’identifiant du segment de la tête actuelle ;
* un message demandant des données de segment avec un identifiant spécifié.

L’instance de secours demande périodiquement l’identifiant du segment de la tête actuelle de l’instance principale. Si le segment est inconnu localement, il est récupéré. S’il est déjà présent, les segments sont comparés et les segments référencés sont également demandés, si nécessaire.

>[!NOTE]
>
>Les instances de secours ne reçoivent aucun type de requêtes, car elles s’exécutent en mode de synchronisation uniquement. La seule section disponible sur une instance de secours est la console web, afin de faciliter la configuration des lots et des services.

Un déploiement classique du processus TarMK Cold Standby :

![chlimage_1](assets/chlimage_1.png)

## Autres caractéristiques {#other-characteristics}

### Robustesse {#robustness}

Le flux de données est conçu pour détecter et gérer automatiquement les problèmes de connexion et de réseau. Tous les paquets sont regroupés avec des sommes de contrôle et lorsque des problèmes de connexion se produisent ou que des paquets sont endommagés, les mécanismes de reprise sont déclenchés.

#### Performance {#performance}

L’activation de TarMK Cold Standby sur l’instance principale n’a pratiquement aucun impact mesurable sur les performances. La consommation supplémentaire du processeur est faible et le disque dur supplémentaire et les E/S réseau ne devraient pas entraîner de problèmes de performances.

Sur l’instance de secours, vous pouvez vous attendre à une consommation élevée du processeur lors du processus de synchronisation. Comme la procédure n’est pas multithread, elle ne peut pas être accélérée en utilisant plusieurs cœurs. Si aucune donnée n’est modifiée ou transférée, il n’existe aucune activité mesurable. La vitesse de connexion varie en fonction de l’environnement matériel et réseau, mais elle ne dépend pas de la taille du référentiel ou de l’utilisation du protocole SSL. Gardez ce point à l’esprit lorsque vous estimez le temps nécessaire à une synchronisation initiale ou lorsque de nombreuses données ont été modifiées entre-temps sur le nœud principal.

#### Sécurité {#security}

En supposant que toutes les instances s’exécutent dans la même zone de sécurité intranet, le risque d’une violation de sécurité est considérablement réduit. Néanmoins, vous pouvez ajouter une couche de sécurité supplémentaire en activant les connexions SSL entre les instances de secours et les instances principales. Cela réduit la possibilité que les données soient compromises par un intermédiaire.

De plus, vous pouvez spécifier les instances de secours autorisées à se connecter en limitant l’adresse IP des requêtes entrantes. Cela permet de garantir qu’aucune personne de l’intranet ne peut copier le référentiel.

>[!NOTE]
>
>Il est recommandé d’ajouter un équilibreur de charge entre Dispatcher et les serveurs qui font partie de la configuration Cold Standby. L’équilibreur de charge doit être configuré pour diriger le trafic de l’utilisateur ou de l’utilisatrice uniquement vers l’instance **principale**. Cela est nécessaire pour garantir la cohérence et empêcher la copie du contenu sur l’instance de secours par d’autres moyens que le mécanisme Cold Standby. 

## Création d’une configuration TarMK Cold Standby AEM {#creating-an-aem-tarmk-cold-standby-setup}

>[!CAUTION]
>
>Le PID du magasin de nœuds Segment et le service de magasin Standby ont changé dans AEM 6.3 par rapport aux versions précédentes, comme suit :
>
>* de org.apache.jackrabbit.oak.**plugins**.segment.standby.store.StandbyStoreService à org.apache.jackrabbit.oak.segment.standby.store.StandbyStoreService
>* de org.apache.jackrabbit.oak.**plugins**.segment.SegmentNodeStoreService à org.apache.jackrabbit.oak.segment.SegmentNodeStoreService
>
>Effectuez les ajustements de configuration nécessaires afin qu’ils reflètent cette modification.

Pour créer une configuration TarMK Cold Standby, créez d’abord les instances secondaires en effectuant une copie du système de fichiers de l’ensemble du dossier d’installation de l’instance principale vers un nouvel emplacement. Vous pouvez ensuite démarrer chaque instance avec un mode d’exécution spécifiant leur rôle (`primary` ou `standby`).

Vous trouverez ci-dessous la procédure à suivre pour créer une configuration avec une instance principale et une instance de secours :

1. Installez AEM.

1. Arrêtez votre instance et copiez son dossier d’installation à l’emplacement d’exécution de l’instance Cold Standby. Même si vous utilisez plusieurs ordinateurs différents, veillez à attribuer à chaque dossier un nom explicite (comme *aem-principal* ou *aem-secondaire*) pour différencier les instances.
1. Accédez au dossier d&#39;installation de l&#39;instance principale, puis :

   1. Vérifiez et supprimez toutes les configurations OSGi précédentes qui pourraient être présentes dans `aem-primary/crx-quickstart/install`.

   1. Créez un dossier appelé `install.primary` sous `aem-primary/crx-quickstart/install`.

   1. Créez les configurations requises pour le magasin de nœuds et le magasin de données de votre choix dans `aem-primary/crx-quickstart/install/install.primary`.
   1. Créez un fichier nommé `org.apache.jackrabbit.oak.segment.standby.store.StandbyStoreService.config` au même emplacement et configurez-le conformément aux exigences. Pour plus d’informations sur les options de configuration, consultez la section [Configuration](/help/sites-deploying/tarmk-cold-standby.md#configuration). 

   1. Si vous utilisez une instance AEM TarMK avec magasin de données externe, créez un dossier nommé `crx3` sous `aem-primary/crx-quickstart/install`, nommé `crx3`.

   1. Placez le fichier de configuration du magasin de données dans le dossier `crx3`. 

   Par exemple, si vous exécutez une instance AEM TarMK avec un magasin de données de fichiers externe, vous aurez besoin des fichiers de configuration suivants :

   * `aem-primary/crx-quickstart/install/install.primary/org.apache.jackrabbit.oak.segment.SegmentNodeStoreService.config`
   * `aem-primary/crx-quickstart/install/install.primary/org.apache.jackrabbit.oak.segment.standby.store.StandbyStoreService.config`
   * `aem-primary/crx-quickstart/install/crx3/org.apache.jackrabbit.oak.plugins.blob.datastore.FileDataStore.config`

   Vous trouverez ci-dessous des exemples de configuration pour l’instance principale :

   **Exemple de** **org.apache.jackrabbit.oak.segment.SegmentNodeStoreService.config**

   ```xml
   org.apache.sling.installer.configuration.persist=B"false"
   customBlobStore=B"true"
   standby=B"false"
   ```

   **Exemple de org.apache.jackrabbit.oak.segment.SegmentNodeStoreService.config**

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

1. Démarrez l’instance principale en veillant à spécifier le mode d’exécution principal :

   ```shell
   java -jar quickstart.jar -r primary,crx3,crx3tar
   ```

1. Création d’un enregistreur de journalisation Apache Sling pour le package **org.apache.jackrabbit.oak.segment**. Définissez le niveau du journal sur « Déboguer », puis dirigez la sortie du journal vers un fichier journal distinct, tel que */logs/tarmk-coldstandby.log*. Pour plus d’informations, consultez la section [Journalisation](/help/sites-deploying/configure-logging.md).
1. Accédez à l’emplacement de l’instance **secondaire** et démarrez-la en exécutant le fichier jar.
1. Créez la même configuration de journalisation que pour l’instance principale. Arrêtez ensuite l’instance.
1. Ensuite, préparez l’instance secondaire. Pour ce faire, procédez comme pour l’instance principale :

   1. Supprimez tous les fichiers dont vous pourriez disposer dans `aem-standby/crx-quickstart/install`.
   1. Créez un dossier appelé `install.standby` sous `aem-standby/crx-quickstart/install`.

   1. Créez deux fichiers de configuration nommés :

      * `org.apache.jackrabbit.oak.segment.SegmentNodeStoreService.config`
      * `org.apache.jackrabbit.oak.segment.standby.store.StandbyStoreService.config`

   1. Créez un dossier appelé `crx3` sous `aem-standby/crx-quickstart/install`.

   1. Créez une configuration de magasin de données et placez-la sous `aem-standby/crx-quickstart/install/crx3`. Pour cet exemple, le fichier que vous devez créer est :

      * org.apache.jackrabbit.oak.plugins.blob.datastore.FileDataStore.config

   1. Modifiez les fichiers et créez les configurations nécessaires.

   Vous trouverez ci-dessous des exemples de fichiers de configuration pour une instance secondaire standard :

   **Exemple de org.apache.jackrabbit.oak.segment.SegmentNodeStoreService.config**

   ```xml
   org.apache.sling.installer.configuration.persist=B"false"
   name="Oak-Tar"
   service.ranking=I"100"
   standby=B"true"
   customBlobStore=B"true"
   ```

   **Exemple de org.apache.jackrabbit.oak.segment.standby.store.StandbyStoreService.config**

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

1. Démarrez l’instance **secondaire** en utilisant le mode d’exécution secondaire :

   ```xml
   java -jar quickstart.jar -r standby,crx3,crx3tar
   ```

Le service peut également être configuré à l’aide de la console Web, en procédant comme suit :

1. Accédez à la console web : *https://serveraddress:serverport/system/console/configMgr*
1. Recherchez un service nommé **Apache Jackrabbit Oak Segment Tar Cold Standby Service** et double-cliquez dessus pour modifier les paramètres.
1. Enregistrez les paramètres et redémarrez les instances pour que les nouveaux paramètres puissent prendre effet.

>[!NOTE]
>
>Vous pouvez vérifier le rôle d’une instance à tout moment en vérifiant la présence des modes d’exécution **principaux** ou **secondaires** dans la console Web des paramètres Sling.
>
>Pour ce faire, accédez à *https://localhost:4502/system/console/status-slingsettings* et vérifiez la ligne **« Modes d’exécution »**.

## Première synchronisation {#first-time-synchronization}

Une fois la préparation terminée et l’instance secondaire lancée pour la première fois, le trafic réseau entre les instances est important, car l’instance secondaire rattrape l’instance principale. Vous pouvez consulter les journaux pour connaître le statut de la synchronisation.

Dans l’instance secondaire *tarmk-coldstandby.log*, vous voyez des entrées de ce type :

```xml
    *DEBUG* [defaultEventExecutorGroup-2-1] org.apache.jackrabbit.oak.segment.standby.store.StandbyStore trying to read segment ec1f739c-0e3c-41b8-be2e-5417efc05266

    *DEBUG* [nioEventLoopGroup-3-1] org.apache.jackrabbit.oak.segment.standby.codec.SegmentDecoder received type 1 with id ec1f739c-0e3c-41b8-be2e-5417efc05266 and size 262144

    *DEBUG* [defaultEventExecutorGroup-2-1] org.apache.jackrabbit.oak.segment.standby.store.StandbyStore got segment ec1f739c-0e3c-41b8-be2e-5417efc05266 with size 262144

    *DEBUG* [defaultEventExecutorGroup-2-1] org.apache.jackrabbit.oak.segment.file.TarWriter Writing segment ec1f739c-0e3c-41b8-be2e-5417efc05266 to /mnt/crx/author/crx-quickstart/repository/segmentstore/data00016a.tar
```

Dans l’instance secondaire *error.log*, vous devriez voir l’entrée suivante :

```xml
*INFO* [FelixStartLevel] org.apache.jackrabbit.oak.segment.standby.store.StandbyStoreService started standby sync with 10.20.30.40:8023 at 5 sec.
```

Dans le fragment de code de journal ci-dessus, *10.20.30.40* est l’adresse IP de l’adresse IP principale.

Dans l’instance **principale** *tarmk-coldstandby.log*, vous voyez des entrées de ce type :

```xml
    *DEBUG* [nioEventLoopGroup-3-2] org.apache.jackrabbit.oak.segment.standby.store.CommunicationObserver got message 's.d45f53e4-0c33-4d4d-b3d0-7c552c8e3bbd' from client c7a7ce9b-1e16-488a-976e-627100ddd8cd

    *DEBUG* [nioEventLoopGroup-3-2] org.apache.jackrabbit.oak.segment.standby.server.StandbyServerHandler request segment id d45f53e4-0c33-4d4d-b3d0-7c552c8e3bbd

    *DEBUG* [nioEventLoopGroup-3-2] org.apache.jackrabbit.oak.segment.standby.server.StandbyServerHandler sending segment d45f53e4-0c33-4d4d-b3d0-7c552c8e3bbd to /10.20.30.40:34998

    *DEBUG* [nioEventLoopGroup-3-2] org.apache.jackrabbit.oak.segment.standby.store.CommunicationObserver did send segment with 262144 bytes to client c7a7ce9b-1e16-488a-976e-627100ddd8cd
```

Dans ce cas, le « client » mentionné dans le journal est l’instance **secondaire**.

Une fois que ces entrées n’apparaissent plus dans le journal, vous pouvez en déduire que le processus de synchronisation est terminé.

Bien que les entrées ci-dessus indiquent que le mécanisme d’interrogation fonctionne correctement, il est souvent utile d’identifier s’il existe bien des données en cours de synchronisation pendant que le processus d’interrogation a lieu. Pour ce faire, recherchez les entrées comme suit :

```xml
*DEBUG* [defaultEventExecutorGroup-156-1] org.apache.jackrabbit.oak.segment.file.TarWriter Writing segment 3a03fafc-d1f9-4a8f-a67a-d0849d5a36d5 to /<<CQROOTDIRECTORY>>/crx-quickstart/repository/segmentstore/data00014a.tar
```

De même, lorsque l’exécution a lieu avec un `FileDataStore` non partagé, des messages comme celui-ci confirment que les fichiers binaires sont correctement transmis :

```xml
*DEBUG* [nioEventLoopGroup-228-1] org.apache.jackrabbit.oak.segment.standby.codec.ReplyDecoder received blob with id eb26faeaca7f6f5b636f0ececc592f1fd97ea1a9#169102 and size 169102
```

### Configuration {#configuration}

Les paramètres OSGi ci-dessous sont disponibles pour le service Cold Standby.

* **Conserver la configuration :** quand il est activé, ce paramètre permet de stocker la configuration dans le référentiel au lieu des fichiers de configuration OSGi traditionnels. Adobe vous recommande de garder ce paramètre désactivé sur des systèmes de production afin que la configuration principale ne soit pas effectuée par l’instance secondaire.

* **Mode (`mode`) :** permet de choisir le mode d’exécution de l’instance.

* **Port (port) :** le port à utiliser pour la communication. La valeur par défaut est `8023`.

* **Hôte principal (`primary.host`) :** l’hôte de l’instance principale. Ce paramètre s’applique uniquement à l’instance de secours.
* **Intervalle de synchronisation (`interval`) :** ce paramètre détermine l’intervalle entre la requête de synchronisation et s’applique uniquement à l’instance de secours.

* **Plages IP autorisées (`primary.allowed-client-ip-ranges`) :** plages IP sur lesquelles l’instance principale autorise la connexion.
* **Sécuriser (`secure`) &#x200B;** : active le chiffrement SSL. Pour pouvoir utiliser ce paramètre, il doit être activé sur toutes les instances.
* **Délai d’expiration de lecture Standby (`standby.readtimeout`) :** délai d’expiration pour les demandes provenant de l’instance de secours, en millisecondes. La valeur par défaut utilisée est de 60 000 (une minute).

* **Nettoyage automatique de secours (`standby.autoclean`) :** appelez cette méthode de nettoyage si la taille du magasin augmente lors d’un cycle de synchronisation..

>[!NOTE]
>
>Adobe recommande que l’instance principale et secondaire aient des identifiants de référentiel différents afin de pouvoir les identifier séparément pour des services tels que le déchargement.
>
>La meilleure façon de garantir que cela est bien couvert est de supprimer *sling.id* dans l’instance secondaire et de la redémarrer.

## Procédures de basculement {#failover-procedures}

Si pour une raison quelconque l’instance principale échoue, vous pouvez choisir l’une des instances secondaires pour la remplacer, en modifiant le mode d’exécution de lancement, tel qu’expliqué ci-après :

>[!NOTE]
>
>Modifiez les fichiers de configuration afin qu’ils correspondent aux paramètres utilisés pour l’instance principale.

1. Accédez à l’emplacement de l’instance de secours sur votre ordinateur et arrêtez-la. 

1. Si vous avez configuré un équilibreur de charge, vous pouvez supprimer l’instance principale à partir de la configuration de l’équilibreur de charge.
1. Sauvegardez le dossier `crx-quickstart` depuis le dossier d’installation secondaire. Cela peut être utilisé comme point de départ lors de la configuration d’une nouvelle instance secondaire.

1. Redémarrez l’instance à l’aide du mode d’exécution `primary` :

   ```shell
   java -jar quickstart.jar -r primary,crx3,crx3tar
   ```

1. Ajoutez la nouvelle instance principale à la répartition de charge.
1. Créez et démarrez une nouvelle instance secondaire. Pour plus d’informations, reportez-vous à la procédure ci-dessus de la section [Création d’une configuration AEM TarMK Cold Standby](/help/sites-deploying/tarmk-cold-standby.md#creating-an-aem-tarmk-cold-standby-setup).

## Application de correctifs à une configuration Cold Standby {#applying-hotfixes-to-a-cold-standby-setup}

La méthode recommandée pour appliquer des correctifs à une configuration Cold Standby consiste à les installer sur l’instance principale, puis à la cloner dans une nouvelle instance Cold Standby avec les correctifs installés.

Pour ce faire, procédez comme suit :

1. Arrêtez le processus de synchronisation sur l’instance Cold Standby en accédant à la console JMX et en utilisant le bean **org.apache.jackrabbit.oak: Status (&quot;Standby&quot;)**. Pour plus d’informations sur la façon de procéder, reportez-vous à la section [Surveillance](#monitoring).
1. Arrêtez l’instance Cold Standby.
1. Installez le correctif sur l’instance principale. Pour plus d’informations sur la façon d’installer un correctif, consultez la section [Fonctionnement des packages](/help/sites-administering/package-manager.md).
1. Après l’installation, vérifiez si les problèmes persistent sur l’instance.
1. Supprimez l’instance Cold Standby en supprimant son dossier d’installation.
1. Arrêtez l’instance principale et clonez-la en effectuant une copie du système de fichiers de l’intégralité de son dossier d’installation vers l’emplacement Cold Standby.
1. Reconfigurez le clone nouvellement créé pour qu’il agisse comme une instance Cold Standby. Voir [Création d’une configuration Cold Standby TarMK AEM.](/help/sites-deploying/tarmk-cold-standby.md#creating-an-aem-tarmk-cold-standby-setup)
1. Démarrez les instances principale et Cold Standby.

## Surveillance {#monitoring}

La fonctionnalité expose des informations à l’aide de JMX ou de MBeans. Vous pouvez ainsi inspecter l’état actuel de l’instance de secours et de l’instance principale à l’aide de la [&#x200B; console JMX &#x200B;](/help/sites-administering/jmx-console.md). Ces informations se trouvent dans un MBean de `type org.apache.jackrabbit.oak:type="Standby"` nommé `Status`.

**Secondaire**

En observant une instance secondaire, vous exposez un nœud. L’ID est généralement un UUID générique.

Ce nœud possède cinq attributs en lecture seule :

* `Running:` valeur booléenne indiquant si le processus de synchronisation fonctionne.

* `Mode:` client : suivi des UUID utilisés pour identifier une instance. Notez que cet UUID change chaque fois que la configuration est mise à jour.

* `Status:` représentation textuelle du statut actuel (par exemple `running` ou `stopped`).

* `FailedRequests:` le nombre d’erreurs consécutives.
* `SecondsSinceLastSuccess:` nombre de secondes depuis la dernière communication réussie avec le serveur. La valeur `-1` s’affiche si aucune communication n’a été effectuée.

Il existe également trois méthodes invocables : 

* `start():` lance le processus de synchronisation.
* `stop():` arrête le processus de synchronisation.
* `cleanup():` exécute l’opération de nettoyage de l’instance de secours.

**Instance principale**

L’observation de l’instance principale expose des informations générales au moyen d’un MBean dont la valeur d’ID est le numéro de port utilisé par le service secondaire TarMK (8023 par défaut). La plupart des méthodes et attributs sont les mêmes que pour l’instance secondaire, mais certains diffèrent :

* `Mode:` affiche toujours la valeur `primary`.

En outre, il est possible de récupérer les informations relatives à un maximum de dix clients (instances de secours) connectés au principal. L’ID MBean est l’UUID de l’instance. Il n’existe pas de méthodes pouvant être appelées pour ces MBeans, mais il existe quelques attributs utiles en lecture seule :

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
>Si vous exécutez le [Nettoyage des révisions en ligne](/help/sites-deploying/revision-cleanup.md) sur l’instance principale, la procédure manuelle présentée ci-dessous n’est pas nécessaire. Par ailleurs, si vous utilisez le nettoyage des révisions en ligne, l’opération `cleanup ()` sur l’instance secondaire sera effectuée automatiquement.

>[!NOTE]
>
>N’exécutez pas de nettoyage des révisions hors ligne sur le serveur secondaire. Cela n’est pas nécessaire et ne réduit pas la taille de l’entrepôt de segments.

Adobe recommande d’exécuter une maintenance régulière pour éviter l’augmentation excessive du référentiel au fil du temps. Pour effectuer manuellement la maintenance du référentiel Cold Standby, suivez les étapes ci-dessous :

1. Arrêtez le processus secondaire sur l’instance secondaire en accédant à la console JMX et en utilisant le bean **org.apache.jackrabbit.oak: Status (&quot;Standby&quot;)**. Pour plus d’informations sur cette procédure, reportez-vous à la section [Surveillance](/help/sites-deploying/tarmk-cold-standby.md#monitoring) ci-dessous.

1. Arrêtez l’instance AEM principale.
1. Exécutez l’outil de compression Oak sur l’instance principale. Pour plus d’informations, consultez la section [Maintenance du référentiel](/help/sites-deploying/storage-elements-in-aem-6.md#maintaining-the-repository).
1. Démarrez l’instance principale.
1. Démarrez le processus secondaire sur l’instance secondaire à l’aide du bean JMX décrit dans la première étape.
1. Observez les journaux et attendez la fin de la synchronisation. Il se peut que vous observiez une augmentation substantielle au niveau du référentiel secondaire à ce moment-là.
1. Exécutez l’opération `cleanup()` sur l’instance de secours, en utilisant le bean JMX décrit dans la première étape.

Il se peut que la synchronisation de l’instance de secours avec l’instance principale prenne plus de temps que prévu, car la compression hors ligne consiste à réécrire l’historique du référentiel, augmentant ainsi substantiellement le temps de calcul des modifications du référentiel. Une fois ce processus terminé, le référentiel sur l’instance secondaire a approximativement la même taille que le référentiel sur l’instance principale.

Comme alternative, le référentiel principal peut être copié manuellement sur le référentiel secondaire après avoir exécuté la compression sur le référentiel principal, reconstruisant essentiellement le référentiel secondaire à chaque exécution de la compression.

### Récupération de l’espace mémoire du magasin de données {#data-store-garbage-collection}

ll est important d’exécuter de temps en temps une récupération de l’espace mémoire sur les instances du magasin de données des fichiers. Sinon, les fichiers binaires supprimés restent sur le système de fichiers, ce qui contribue à surcharger le lecteur. Pour lancer la récupération de l’espace mémoire, suivez la procédure ci-dessous :

1. Exécutez le processus de maintenance du référentiel Cold Standby, comme expliqué dans la section [ci-dessus](/help/sites-deploying/tarmk-cold-standby.md#cold-standby-repository-maintenance).
1. Une fois le processus de maintenance terminé et les instances redémarrées, procédez comme suit :

   * Sur l’instance principale, exécutez la récupération de l’espace mémoire du magasin de données par le biais du bean JMX approprié, comme décrit dans la section [Exécuter la récupération de l’espace mémoire du magasin de données via la console JMX](/help/sites-administering/data-store-garbage-collection.md#running-data-store-garbage-collection-via-the-jmx-console).
   * Sur l’instance secondaire, la récupération de l’espace mémoire du magasin de données est uniquement disponible via le MBean **BlobGarbageCollection** - `startBlobGC()`. Le MBean **RepositoryManagement** n’est pas disponible sur l’instance de secours.

   >[!NOTE]
   >
   >Si vous n’utilisez pas de magasin de données partagé, la récupération de l’espace mémoire doit d’abord être exécutée sur l’instance principale, puis sur l’instance secondaire.
