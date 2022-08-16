---
title: Prise en main de Process Reporting
seo-title: Getting Started with Process Reporting
description: Étapes à suivre pour commencer à utiliser le module Process Reporting d’AEM Forms on JEE
seo-description: The steps you need to follow to get started with AEM Forms on JEE Process Reporting
uuid: 685cad39-da2c-411d-a0b0-201917438bcf
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: process-reporting
discoiquuid: 7c1fcde0-b983-4b24-bc19-fcee1d4f096b
docset: aem65
exl-id: 1272e854-fa64-4bfd-b073-8fbcf210e9b5
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1710'
ht-degree: 100%

---

# Prise en main de Process Reporting{#getting-started-with-process-reporting}

Process Reporting permet aux utilisateurs d’AEM Forms de demander des renseignements à propos des processus AEM Forms actuellement définis dans le cadre de la mise en œuvre d’AEM Forms. Toutefois, Process Reporting n’accède pas directement aux données à partir du référentiel AEM Forms. Les données sont d’abord publiées dans le référentiel Process Reporting selon un calendrier (*par les services ProcessDataPublisher et ProcessDataStorage*). Les rapports et requêtes de Process Reporting sont ensuite générés à partir des données Process Reporting publiées dans le référentiel. Process Reporting est installé dans le cadre du module Forms Workflow.

Cet article décrit les étapes à suivre pour activer la publication des données AEM Forms dans le référentiel Process Reporting. Ensuite, vous pourrez utiliser Process Reporting pour exécuter des rapports et des requêtes. L’article couvre également les options disponibles pour configurer les services Process Reporting.

## Conditions préalables relatives à Process Reporting {#process-reporting-pre-requisites}

### Purge des processus non essentiels {#purge-non-essential-processes}

Si vous utilisez actuellement Forms Workflow, la base de données AEM Forms peut contenir une grande quantité de données.

Les services de publication Process Reporting publieront toutes les données AEM Forms actuellement disponibles dans la base de données. Par conséquent, si la base de données contient des données héritées pour lesquelles vous ne souhaitez pas exécuter de rapports et de requêtes, toutes ces données seront également publiées dans le référentiel, même si elles ne sont pas requises pour la création de rapports. Il est recommandé de purger ces données avant d’exécuter les services pour publier les données dans le référentiel Process Reporting. Vous améliorez ainsi les performances du service d’éditeur et du service qui interroge les données pour la création de rapports.

Pour plus d’informations sur la purge des données de processus AEM Forms, voir [Purger les données de processus](https://help.adobe.com/fr_FR/livecycle/11.0/AdminHelp/WS92d06802c76abadb-5145d5d12905ce07e7-7cb2.2.html).

>[!NOTE]
>
>Pour obtenir des conseils et astuces sur l’utilitaire de purge, reportez-vous à l’article Adobe Developer Connection sur la [purge des processus et des tâches](https://www.adobe.com/content/dam/Adobe/en/devnet/livecycle/pdfs/purging_processes_jobs.pdf).

## Configurer les services Process Reporting {#configuring-process-reporting-services}

### Planifier la publication des données de processus {#schedule-process-data-publishing}

Les services Process Reporting publient les données de la base de données AEM Forms dans le référentiel Process Reporting selon un calendrier précis.

Cette opération peut nécessiter de nombreuses ressources et avoir un impact sur les performances des serveurs AEM Forms. Il est recommandé de planifier cette opération en dehors des créneaux horaires occupés de votre serveur AEM Forms.

Par défaut, la publication des données est planifiée tous les jours à 02h00.

Effectuez les étapes suivantes pour modifier le calendrier de publication :

>[!NOTE]
>
>Si vous réalisez la mise en œuvre d’AEM Forms sur un cluster, effectuez les étapes suivantes sur chaque nœud du cluster.

1. Arrêtez l’instance du serveur AEM Forms.
1. &#x200B;

   * (Pour Windows) Ouvrez le fichier `[JBoss root]/bin/run.conf.bat` dans un éditeur.
   * (Pour Linux, AIX et Solaris) Ouvrez le fichier `[JBoss root]/bin/run.conf.sh` dans un éditeur.

1. Ajoutez l’argument JVM `-Dreporting.publisher.cron = <expression>.`

   Exemple : l’expression cron suivante entraîne la publication par Process Reporting de données AEM Forms dans le référentiel Process Reporting toutes les 5 heures :

   * `-Dreporting.publisher.cron = 0_0_0/5_*_*_?`

1. Enregistrez et fermez le fichier `run.conf.bat`.

1. Redémarrez l’instance du serveur AEM Forms.

1. Arrêtez l’instance du serveur AEM Forms.
1. Connectez-vous à la console d’administration WebSphere. Dans l’arborescence de navigation, cliquez sur **Serveurs** > **Serveurs d’applications**, puis sur le nom du serveur dans le volet de droite.

1. Sous Server Infrastructure, cliquez sur **Java and Process Management** > **Process Definition**.

1. Sous Additional Properties, cliquez sur **Java Virtual Machine**.

   Dans la zone d’arguments JVM génériques, ajoutez l’argument `-Dreporting.publisher.cron = <expression>.`

   **Exemple** : l’expression cron suivante entraîne la publication par Process Reporting de données AEM Forms dans le référentiel Process Reporting toutes les 5 heures :

   * `-Dreporting.publisher.cron = 0_0_0/5_*_*_?`

1. Cliquez sur **Appliquer**, sur OK, puis sur **Enregistrer directement vers la configuration maître**.
1. Redémarrez l’instance du serveur AEM Forms.
1. Arrêtez l’instance du serveur AEM Forms.
1. Connectez-vous à la console d’administration WebLogic. L’adresse par défaut de la console d’administration WebLogic `https://[hostname]:[port]/console`.
1. Sous Change Center, cliquez sur **Lock &amp; Edit**.
1. Sous Domain Structure, cliquez sur **Environment** > **Servers** et, dans le volet de droite, cliquez sur le nom du serveur géré.
1. Dans l’écran suivant, cliquez sur les onglets **Configuration** > **Server Start**.
1. Dans la zone Arguments, ajoutez l’argument JVM `-Dreporting.publisher.cron = <expression>`.

   **Exemple** : l’expression cron suivante entraîne la publication par Process Reporting de données AEM Forms dans son référentiel. Cette action survient toutes les 5 heures :

   `-Dreporting.publisher.cron = 0_0_0/5_*_*_?`

1. Cliquez sur **Save**, puis sur **Activate Changes**.
1. Redémarrez l’instance du serveur AEM Forms.

![processdatapublisherservice](assets/processdatapublisherservice.png)

### Service ProcessDataStorage {#processdatastorage-service}

Le service ProcessDataStorageProvider reçoit les données de processus du service ProcessDataPublisher et enregistre les données dans le référentiel Process Reporting.

À chaque cycle de publication, les données sont enregistrées dans des sous-dossiers d’un dossier racine prédéfini.

Vous pouvez utiliser la console d’administration pour configurer l’emplacement racine (**par défaut** : `/content/reporting/pm`) et le format de la hiérarchie (**par défaut** : `/yyyy/mm/dd/hh/mi/ss`) des sous-dossiers dans lesquels les données de processus sont stockées.

#### Pour configurer les emplacements du référentiel Process Reporting {#to-configure-the-process-reporting-repository-locations}

1. Connectez-vous à la **Console d’administration** avec vos informations d’identification d’administrateur. L’URL par défaut de la console d’administration est `https://'[server]:[port]'/adminui`.
1. Accédez à **Accueil** > **Services** > **Applications et services** > **Gestion des services**, puis ouvrez le service **ProcessDataStorageProvider**.

   ![process-data-storage-service](assets/process-data-storage-service.png)

   **Dossier racine**

   Emplacement CRX à l’intérieur duquel les données de processus sont stockées pour la création de rapports.

   `Default`: `/content/reporting/pm`

   **Hiérarchie de dossiers**

   Hiérarchie de dossiers à l’intérieur de laquelle les données de processus sont stockées en fonction de l’heure de création du processus.

   `Default`: `/yyyy/mm/dd/hh/mi/ss`

1. Cliquez sur **Enregistrer**.

### Service ReportConfiguration {#reportconfiguration-service}

Le service ReportConfiguration est utilisé par Process Reporting pour configurer son service de requête.

#### Pour configurer le service ReportingConfiguration {#to-configure-the-reportingconfiguration-service}

1. Connectez-vous à **Configuration Manager** avec vos informations d’identification d’administrateur CRX. L’URL par défaut de Configuration Manager est `https://'[server]:[port]'/lc/system/console/configMgr`.
1. Ouvrez le service **ReportingConfiguration**.
1. **Nombre d’enregistrements**

   Lors de l’exécution d’une requête sur le référentiel, un résultat peut potentiellement contenir un grand nombre d’enregistrements. Si le jeu de résultats est volumineux, l’exécution de la requête peut consommer des ressources serveur.

   Pour gérer les jeux de résultats volumineux, le service ReportConfiguration divise le traitement des requêtes en lots d’enregistrements. Cela réduit la charge du système.

   `Default`: `1000`

   **Chemin de stockage CRX**

   Emplacement CRX à l’intérieur duquel les données de processus doivent être stockées pour la création de rapports.

   `Default`: `/content/reporting/pm`

   >[!NOTE]
   >
   >Il s’agit du même emplacement que celui spécifié dans l’option **Dossier racine** de la configuration ProcessDataStorage.
   >
   >
   >Si vous mettez à jour l’option de dossier racine dans la configuration ProcessDataStorage, vous devez mettre à jour l’emplacement du chemin de stockage CRX dans le service ReportConfiguration.

1. Cliquez sur **Enregistrer** et fermez **CQ Configuration Manager**.

### Service ProcessDataPublisher {#processdatapublisher-service}

Le service ProcessDataPublisher importe les données de processus de la base de données AEM Forms et les publie dans le service ProcessDataStorageProvider pour le stockage.

#### Pour configurer le service ProcessDataPublisher  {#to-configure-processdatapublisher-service-nbsp}

1. Connectez-vous à la **Console d’administration** avec vos informations d’identification d’administrateur.

   L’URL par défaut est `https://'server':port]/adminui/`.

1. Accédez à **Accueil** > **Services** > **Applications et services** > **Gestion des services** et ouvrez le service **ProcessDataPublisher**.

![processdatapublisherservice-1](assets/processdatapublisherservice-1.png)

**Publier les données**

Activez cette option pour démarrer la publication des données de processus. Par défaut, cette option est désactivée.

Activez uniquement Process Reporting lorsque toutes les configurations liées à ses composants sont configurées de manière appropriée.

Vous pouvez également utiliser cette option pour désactiver la publication des données de processus lorsqu’elle n’est plus nécessaire.

`Default`: `Off`

**Intervalle de lot (sec.)**

Chaque fois que le service ProcessDataPublisher s’exécute, il divise d’abord le temps depuis la dernière exécution du service par l’intervalle de lot. Le service traite ensuite séparément chaque intervalle de données AEM Forms.

Cela permet de contrôler la taille des données que l’éditeur traite de bout en bout au cours de chaque exécution (lot) au cours d’un cycle.

Par exemple, si l’éditeur s’exécute tous les jours, au lieu de traiter l’ensemble des données pendant un jour au cours d’une seule exécution, il divise par défaut le traitement en 24 lots d’une heure chacun.

`Default`: `3600`

`Unit`: `Seconds`

**Verrouiller le délai d’expiration (sec.)**

Le service d’éditeur acquiert un verrou lorsqu’il démarre le traitement des données, de sorte que plusieurs instances de l’éditeur ne commencent pas à exécuter et à traiter les données de manière simultanée.

Si un service d’éditeur qui a acquis un verrou reste inactif pendant le nombre de secondes défini par la valeur Délai d’expiration du verrou, il est déverrouillé afin de permettre à d’autres instances du service d’éditeur de continuer le traitement.

`Default`: `3600`

`Unit`: `Seconds`

**Publier des données à partir de**

L’environnement AEM Forms contient les données du moment où l’environnement a été configuré.

Par défaut, le service ProcessDataPublisher importe toutes les données de la base de données AEM Forms.

En fonction de vos besoins de création de rapports, si vous prévoyez d’exécuter des rapports et des requêtes sur des données après une certaine date et heure, il est recommandé de spécifier la date et l’heure. Le service de publication publiera alors la date à partir de ce moment.

`Default`: `01-01-1970 00:00:00`

`Format`: `dd-MM-yyyy HH:mm:ss`

## Accéder à l’interface utilisateur Process Reporting {#accessing-the-process-reporting-user-interface}

L’interface utilisateur de Process Reporting est basée sur un navigateur.

Une fois que vous avez configuré Process Reporting, vous pouvez commencer à l’utiliser à l’emplacement suivant de votre installation AEM Forms :

`https://<server>:<port>/lc/pr`

### Se connecter à Process Reporting {#log-in-to-process-reporting}

Lorsque vous accédez à l’URL Process Reporting (https://&lt;server>:&lt;port>/lc/pr), l’écran de connexion s’affiche.

Indiquez vos informations d’identification pour vous connecter au module Process Reporting.

>[!NOTE]
>
>Pour vous connecter à l’interface utilisateur Process Reporting, vous devez disposer de l’autorisation AEM Forms suivante :
>
>`PERM_PROCESS_REPORTING_USER`

![Se connecter à Process Reporting](assets/capture1_new.png)

Lorsque vous vous connectez à Process Reporting, l’écran **[!UICONTROL d’accueil]** s’affiche.

### Écran d’accueil de Process Reporting {#process-reporting-home-screen}

![process-reporting-home-screen](assets/process-reporting-home-screen.png)

**Arborescence de Process Reporting :** l’arborescence sur le côté gauche de l’écran d’accueil contient les éléments des modules Process Reporting.

L’arborescence est composée des éléments de niveau supérieur suivants :

**Rapports :** cet élément contient les rapports d’usine fournis avec Process Reporting.

Pour plus d’informations sur les rapports prédéfinis, voir [Rapports prédéfinis dans Process Reporting](/help/forms/using/process-reporting/pre-defined-reports-in-process-reporting.md).

**Requêtes ad hoc :** cet élément contient des options permettant d’effectuer une recherche de processus et de tâches basée sur des filtres.

Pour plus d’informations sur les requêtes ad hoc, voir [Requêtes ad hoc dans Process Reporting](/help/forms/using/process-reporting/adhoc-queries-in-process-reporting.md).

**Personnalisé :** le nœud Personnalisé affiche les rapports personnalisés que vous créez.

Pour connaître la procédure de création et d’affichage de rapports personnalisés, voir [Rapports personnalisés dans Process Reporting](/help/forms/using/process-reporting/process-reporting-custom-reports.md).

**Barre de titre Process Reporting :** elle contient des options génériques que vous pouvez utiliser lorsque vous travaillez dans l’interface utilisateur.

**Titre Process Reporting :** il s’affiche dans le coin gauche de la barre de titre.

Cliquez sur le titre à tout moment pour revenir à l’écran d’accueil.

**Heure de la dernière mise à jour :** les données de processus sont publiées de la base de données AEM Forms vers le référentiel Process Reporting selon un calendrier précis.

L’heure de la dernière mise à jour affiche la date et l’heure auxquelles les mises à jour de données ont été transmises au référentiel Process Reporting.

Pour plus d’informations sur le service de publication de données et sur la planification de ce service, voir [Planification de la publication des données de processus](/help/forms/using/process-reporting/install-start-process-reporting.md#p-schedule-process-data-publishing-p) dans l’article Prise en main de Process Reporting.

**Utilisateur Process Reporting :** le nom d’utilisateur connecté s’affiche à la droite de l’heure de la dernière mise à jour.

**Liste déroulante de la barre de titre de Procces Reporting :** la liste déroulante située dans le coin droit de la barre de titre Process Reporting comprend les options suivantes :

* **[!UICONTROL Synchronisation]** : synchronisez le référentiel Process Reporting incorporé à la base de données AEM Forms.
* **[!UICONTROL Aide]** : consultez la documentation d’aide sur Process Reporting.
* **[!UICONTROL Déconnexion]** : se déconnecter de Process Reporting
