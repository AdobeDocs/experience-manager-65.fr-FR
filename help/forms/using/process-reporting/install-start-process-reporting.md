---
title: Prise en main du Rapports de processus
seo-title: Prise en main du Rapports de processus
description: Les étapes à suivre pour commencer à utiliser le Rapports de processus AEM Forms on JEE
seo-description: Les étapes à suivre pour commencer à utiliser le Rapports de processus AEM Forms on JEE
uuid: 685cad39-da2c-411d-a0b0-201917438bcf
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: process-reporting
discoiquuid: 7c1fcde0-b983-4b24-bc19-fcee1d4f096b
docset: aem65
translation-type: tm+mt
source-git-commit: 56c6cfd437ef185336e81373bd5f758205b96317
workflow-type: tm+mt
source-wordcount: '1731'
ht-degree: 3%

---


# Getting Started with Process Reporting{#getting-started-with-process-reporting}

Le Rapports de processus permet aux utilisateurs de AEM Forms de requête des informations sur les processus AEM Forms actuellement définis dans l’implémentation de AEM Forms. Cependant, le Rapports de processus n’accède pas directement aux données du référentiel AEM Forms. Les données sont d’abord publiées dans le référentiel de Rapports de processus selon un calendrier défini (*par les* services ProcessDataPublisher et ProcessDataStorage). Les rapports et requêtes du Rapports de processus sont ensuite générés à partir des données du Rapports de processus publiées dans le référentiel. Le Rapports de processus est installé dans le cadre du module Forms Workflow.

Cet article décrit en détail les étapes permettant d’activer la publication des données AEM Forms dans le référentiel de Rapports de processus. Vous pourrez ensuite utiliser le Rapports de processus pour exécuter des rapports et des requêtes. L’article traite également des options disponibles pour configurer les services Process Rapports.

## Conditions préalables au Rapports de traitement {#process-reporting-pre-requisites}

### Purger les processus non essentiels {#purge-non-essential-processes}

Si vous utilisez actuellement Forms Workflow, la base de données AEM Forms peut contenir une grande quantité de données.

Les services de publication Process Rapports publieront toutes les données AEM Forms actuellement disponibles dans la base de données. Cela signifie que si la base de données contient des données héritées sur lesquelles vous ne souhaitez pas exécuter de rapports et de requêtes, toutes ces données seront également publiées dans le référentiel même si elles ne sont pas requises pour le rapports. Il est recommandé de purger ces données avant d’exécuter les services pour publier les données dans le référentiel de Rapports de processus. Cela améliorera les performances du service d’éditeur et du service qui requête les données pour le rapports.

Pour plus d’informations sur la purge des données de processus AEM Forms, voir [Purge des données](https://help.adobe.com/en_US/livecycle/11.0/AdminHelp/WS92d06802c76abadb-5145d5d12905ce07e7-7cb2.2.html)de processus.

>[!NOTE]
>
>Pour obtenir des conseils et astuces sur l’utilitaire de purge, reportez-vous à l’article Adobe Developer Connection sur la [purge de processus et de tâches](https://www.adobe.com/content/dam/Adobe/en/devnet/livecycle/pdfs/purging_processes_jobs.pdf).

## Configuration des services de Rapports de processus {#configuring-process-reporting-services}

### Planification de la publication des données de processus {#schedule-process-data-publishing}

Les services Process Rapports publient les données de la base de données AEM Forms vers le référentiel Process Rapports sur une base planifiée.

Cette opération peut être gourmande en ressources et avoir un impact sur les performances des serveurs AEM Forms. Il est recommandé de planifier cette opération en dehors des créneaux horaires occupés de votre serveur AEM Forms.

Par défaut, la publication des données est programmée pour s’exécuter tous les jours à 2h du matin.

Effectuez les étapes suivantes pour modifier le calendrier de publication :

>[!NOTE]
>
>Si vous exécutez l’implémentation AEM Forms sur une grappe, effectuez les étapes suivantes sur chaque noeud de la grappe.

1. Arrêtez l’instance du serveur AEM Forms.
1. &#x200B;

   * (Pour Windows) Ouvrez le `[JBoss root]/bin/run.conf.bat` fichier dans un éditeur.
   * (pour Linux, AIX et Solaris) `[JBoss root]/bin/run.conf.sh` dans un éditeur.

1. Ajouter l’argument JVM `-Dreporting.publisher.cron = <expression>.`

   Exemple : L’expression cron suivante entraîne la publication de données AEM Forms par le Rapports de processus dans le référentiel de Rapports de processus toutes les 5 heures :

   * `-Dreporting.publisher.cron = 0_0_0/5_*_*_?`

1. Save and close the `run.conf.bat` file.

1. Redémarrez l’instance du serveur AEM Forms.

1. Arrêtez l’instance du serveur AEM Forms.
1. Log in to the WebSphere Administrative Console. In the navigation tree, click **Servers** > **Application servers** and then, in the right pane, click the server name.

1. Sous Server Infrastructure, cliquez sur **Java and Process Management**> **Process Definition**.

1. Sous Additional Properties, cliquez sur **Java Virtual Machine**.

   In the Generic JVM arguments box, add the argument `-Dreporting.publisher.cron = <expression>.`

   **Exemple**: L’expression cron suivante entraîne la publication de données AEM Forms par le Rapports de processus dans le référentiel de Rapports de processus toutes les 5 heures :

   * `-Dreporting.publisher.cron = 0_0_0/5_*_*_?`

1. Click **Apply**, click OK, and then click **Save directly to the master configuration**.
1. Redémarrez l’instance du serveur AEM Forms.
1. Arrêtez l’instance du serveur AEM Forms.
1. Connectez-vous à WebLogic Administration Console. L’adresse par défaut de WebLogic Administration Console est `https://[hostname]:[port]/console`.
1. Sous Change Center, cliquez sur **Lock &amp; Edit**.
1. Sous Domain Structure, cliquez sur **Environment** > **Servers** et, dans le volet de droite, cliquez sur le nom du serveur géré.
1. Dans l’écran suivant, cliquez sur les onglets **Configuration** > **Server Start**.
1. Dans la zone Arguments, ajoutez l’argument JVM `-Dreporting.publisher.cron = <expression>`.

   **Exemple**: L’expression cron suivante entraîne la publication de données AEM Forms par le Rapports de processus dans le référentiel de Rapports de processus toutes les 5 heures :

   `-Dreporting.publisher.cron = 0_0_0/5_*_*_?`

1. Cliquez sur **Save**, puis sur **Activate Changes**.
1. Redémarrez l’instance du serveur AEM Forms.

![processdatapublisherservice](assets/processdatapublisherservice.png)

### Service ProcessDataStorage {#processdatastorage-service}

Le service ProcessDataStorageProvider reçoit les données de processus du service ProcessDataPublisher et les enregistre dans le référentiel Process Rapports.

Lors de chaque cycle de publication, les données sont enregistrées dans des sous-dossiers d’un dossier racine prédéfini.

Vous pouvez utiliser Administration Console pour configurer la racine (**par défaut**: `/content/reporting/pm`) emplacement et sous-dossier (**par défaut**: `/yyyy/mm/dd/hh/mi/ss`) format hiérarchique dans lequel les données de processus seraient stockées.

#### Pour configurer les emplacements de référentiel du Rapports de processus {#to-configure-the-process-reporting-repository-locations}

1. Connectez-vous à **Administration Console** avec les informations d’identification d’administrateur. L’URL par défaut d’Administration Console est `https://'[server]:[port]'/adminui`
1. Accédez à **Accueil** > **Services** > **Applications et services** >Gestion des **services et ouvrez le service ProcessDataStorageProvider.******

   ![process-data-enregistrement-service](assets/process-data-storage-service.png)

   **RootFolder**

   Emplacement CRX à l’intérieur duquel les données de processus seraient stockées pour le rapports.

   `Default`: `/content/reporting/pm`

   **Hiérarchie des dossiers**

   Hiérarchie des dossiers dans laquelle les données de processus sont stockées en fonction de l’heure de création du processus.

   `Default`: `/yyyy/mm/dd/hh/mi/ss`

1. Cliquez sur **Save**.

### Service ReportConfiguration {#reportconfiguration-service}

Le service ReportConfiguration est utilisé par le Rapports de processus pour configurer le service de requête de rapports de processus.

#### To configure the ReportingConfiguration service {#to-configure-the-reportingconfiguration-service}

1. Connectez-vous à **Configuration Manager** avec les informations d’identification d’administrateur CRX. The default URL of Configuration Manager is `https://'[server]:[port]'/lc/system/console/configMgr`
1. Ouvrez le service **ReportingConfiguration** .
1. **Nombre d&#39;enregistrements**

   Lors de l’exécution d’une requête sur le référentiel, un résultat peut contenir un grand nombre d’enregistrements. Si le jeu de résultats est volumineux, l’exécution de la requête peut consommer des ressources serveur.

   Pour gérer les jeux de résultats volumineux, le service ReportConfiguration divise le traitement de la requête en lots d’enregistrements. Cela réduit la charge du système.

   `Default`: `1000`

   **Chemin d’Enregistrement CRX**

   Emplacement CRX à l’intérieur duquel les données de processus doivent être stockées pour le rapports.

   `Default`: `/content/reporting/pm`

   >[!NOTE]
   >
   >Il s’agit du même emplacement que celui spécifié dans l’option de configuration ProcessDataStorage **Root Folder**.
   >
   >
   >Si vous mettez à jour l’option Dossier racine dans la configuration ProcessDataStorage, vous devez mettre à jour l’emplacement Chemin d’Enregistrement CRX dans le service ReportConfiguration.

1. Cliquez sur **Enregistrer** et fermez **CQ Configuration Manager**.

### Service ProcessDataPublisher {#processdatapublisher-service}

Le service ProcessDataPublisher importe les données de processus de la base de données AEM Forms et les publie dans le service ProcessDataStorageProvider pour enregistrement.

#### Pour configurer le service ProcessDataPublisher   {#to-configure-processdatapublisher-service-nbsp}

1. Connectez-vous à **Administration Console** avec les informations d’identification d’administrateur.

   L’URL par défaut est `https://'server':port]/adminui/`.

1. Accédez à **Accueil** > **Services** > **Applications et services** >Gestion des **services et ouvrez le service ProcessDataPublisher.******

![processdatapublisherservice-1](assets/processdatapublisherservice-1.png)

**Publier les données**

Activez cette option pour début des données de processus de publication. Par défaut, l’option est désactivée.

Activez le Rapports de processus uniquement lorsque toutes les configurations liées aux composants du Rapports de processus sont configurées de manière appropriée.

Vous pouvez également utiliser cette option pour désactiver la publication des données de processus lorsqu’elle n’est plus nécessaire.

`Default`: `Off`

**Intervalle de lot (s)**

Chaque fois que le service ProcessDataPublisher s’exécute, le service commence par fractionner l’heure depuis la dernière exécution du service par l’intervalle de traitement par lots. Le service traite ensuite chaque intervalle de données AEM Forms séparément.

Cela permet de contrôler la taille des données que l’éditeur traite de bout en bout lors de chaque exécution (lot) au cours d’un cycle.

Par exemple, si l’éditeur s’exécute tous les jours, au lieu de traiter l’ensemble des données pour un jour au cours d’une seule exécution, il divise par défaut le traitement en 24 lots d’une heure chacun.

`Default`: `3600`

`Unit`: `Seconds`

**Délai d&#39;expiration de verrouillage (s)**

Le service d’éditeur acquiert un verrou lorsqu’il début le traitement des données, de sorte que plusieurs instances de l’éditeur ne début pas l’exécution et le traitement simultané des données.

Si un service d’éditeur qui a acquis un verrou est inactif pendant le nombre de secondes défini par la valeur Délai d’expiration du verrou, son verrou est libéré afin que d’autres instances du service d’éditeur puissent poursuivre le traitement.

`Default`: `3600`

`Unit`: `Seconds`

**Publier les données à partir de**

L’environnement d’AEM Forms contient les données du moment où l’environnement a été configuré.

Par défaut, le service ProcessDataPublisher importe toutes les données de la base de données AEM Forms.

En fonction des besoins de votre rapports, si vous prévoyez d’exécuter des rapports et des requêtes sur des données après une date et une heure déterminées, il est recommandé de spécifier la date et l’heure. Le service de publication publiera ensuite la date à partir de cette date.

`Default`: `01-01-1970 00:00:00`

`Format`: `dd-MM-yyyy HH:mm:ss`

## Accès à l’interface utilisateur du Rapports de processus {#accessing-the-process-reporting-user-interface}

L’interface utilisateur du Rapports de processus est basée sur un navigateur.

Une fois que vous avez configuré Process Rapports, vous pouvez début utiliser Process Rapports à l’emplacement suivant dans votre installation AEM Forms :

`https://<server>:<port>/lc/pr`

### Connexion au Rapports de processus {#log-in-to-process-reporting}

Lorsque vous accédez à l’URL du Rapports de processus (https://&lt;serveur>:&lt;port>/lc/pr), l’écran de connexion s’affiche.

Spécifiez vos informations d’identification pour vous connecter au module Rapports de processus.

>[!NOTE]
>
>Pour vous connecter à l’interface utilisateur du Rapports de processus, vous devez disposer de l’autorisation AEM Forms suivante :
>
>`PERM_PROCESS_REPORTING_USER`

![Rapports de connexion au processus](assets/capture1_new.png)

Lorsque vous vous connectez au Rapports de processus, l’écran **[!UICONTROL Accueil]** s’affiche.

### Écran d’accueil du Rapports de processus {#process-reporting-home-screen}

![processus-rapports-accueil-écran](assets/process-reporting-home-screen.png)

**Vue de l&#39;arborescence du Rapports de processus :** L’arborescence de la vue située à gauche de l’écran d’accueil contient les éléments des modules de Rapports de processus.

L&#39;arborescence de la vue comprend les éléments de niveau supérieur suivants :

**Rapports :** Cet élément contient les rapports prêts à l&#39;emploi qui sont livrés avec le Rapports de processus.

Pour plus d’informations sur les rapports prédéfinis, voir Rapports [prédéfinis dans le Rapports](/help/forms/using/process-reporting/pre-defined-reports-in-process-reporting.md)de processus.

**Requêtes ad hoc :** Cet élément contient des options permettant d&#39;effectuer une recherche basée sur des filtres pour les processus et les tâches.

Pour plus d’informations sur les requêtes ad hoc, voir Requêtes [ad hoc dans le Rapports](/help/forms/using/process-reporting/adhoc-queries-in-process-reporting.md)de processus.

**Personnalisé :** Le noeud Personnalisé affiche les rapports personnalisés que vous créez.

Pour la procédure de création et d&#39;affichage de rapports personnalisés, voir Rapports [personnalisés dans le Rapports](/help/forms/using/process-reporting/process-reporting-custom-reports.md)de processus.

**Barre de titre du Rapports de traitement :** La barre de titre du Rapports de processus contient des options génériques que vous pouvez utiliser lorsque vous travaillez dans l’interface utilisateur.

**Titre du Rapports de processus :** Le titre du Rapports de traitement s’affiche dans le coin gauche de la barre de titre.

Cliquez sur le titre à tout moment pour revenir à l’écran d’accueil.

**Heure de la dernière mise à jour :** Les données de processus sont publiées de la base de données AEM Forms vers le référentiel Rapports de processus selon un calendrier défini.

L’heure de la dernière mise à jour affiche la date et l’heure auxquelles les mises à jour de données ont été transférées vers le référentiel de Rapports de processus.

Pour plus d’informations sur le service de publication de données et sur la façon de planifier ce service, voir [Planifier la publication](/help/forms/using/process-reporting/install-start-process-reporting.md#p-schedule-process-data-publishing-p) des données de processus dans l’article Prise en main du Rapports de processus.

**Utilisateur du Rapports de processus :** Le nom d’utilisateur connecté s’affiche à droite de l’heure de la dernière mise à jour.

**Liste déroulante de la barre de titre du Rapports de traitement :** La liste déroulante située dans le coin droit de la barre de titre du Rapports de processus contient les options suivantes :

* **[!UICONTROL Synchronisation]**: Synchronisez le référentiel de Rapports de processus incorporé avec la base de données AEM Forms.
* **[!UICONTROL Aide]**: Vue de la documentation d’aide sur le Rapports de processus.
* **[!UICONTROL Déconnexion]**: Déconnexion du Rapports de processus
