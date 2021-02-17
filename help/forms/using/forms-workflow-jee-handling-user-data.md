---
title: Flux de travail AEM Forms JEE | Gestion des données utilisateur
seo-title: Flux de travail AEM Forms JEE | Gestion des données utilisateur
description: Flux de travail AEM Forms JEE | Gestion des données utilisateur
uuid: 3b06ef19-d3c4-411e-9530-2c5d2159b559
topic-tags: grdp
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 5632a8df-a827-4e38-beaa-18b61c2208a3
translation-type: tm+mt
source-git-commit: a873cf3e7efd3bc9cd4744bf09078d9040efcdda
workflow-type: tm+mt
source-wordcount: '1371'
ht-degree: 70%

---


# Flux de travail AEM Forms JEE | Gestion des données utilisateur {#forms-jee-workflows-handling-user-data}

Les workflows AEM Forms JEE fournissent des outils pour concevoir, créer et gérer des processus d’entreprise. Un processus de flux de travail se compose d’une série d’étapes effectuées dans un ordre spécifique. Chaque étape exécute une action spécifique, par exemple, attribuer une tâche à un utilisateur ou envoyer un message électronique. Un processus peut interagir avec les ressources, les comptes utilisateur et les services. Il peut également être déclenché à l’aide de l’une des méthodes suivantes :

* Démarrage d’un processus de l’espace de travail AEM Forms
* Utilisation du service SOAP ou RESTful
* Envoi d’un formulaire adaptatif
* Utilisation d’un dossier de contrôle
* Utilisation du courrier électronique

Pour plus d’informations sur la création du processus de flux de travaux AEM Forms JEE, voir [Aide de Workbench](http://www.adobe.com/go/learn_aemforms_workbench_65_fr).

## Données utilisateur et stockage de données {#user-data-and-data-stores}

Lorsqu’un processus est déclenché et tout au long de sa progression, il capture des données sur les participants, les données qu’ils ont saisies dans le formulaire associé au processus et les pièces jointes ajoutées au formulaire. Les données sont stockées dans la base de données du serveur AEM Forms JEE et, si elles sont configurées, certaines données telles que les pièces jointes sont stockées dans le répertoire de stockage global de documents (GDS). Le répertoire GDS peut être configuré sur un système de fichiers partagé ou une base de données.

## Accès et suppression des données utilisateur {#access-and-delete-user-data}

Lorsqu’un processus est déclenché, un ID d’instance de processus unique et un ID d’appel de longue durée sont générés et associés à l’instance de processus. Vous pouvez accéder et supprimer des données pour une instance de processus en fonction de l’ID d’appel de longue durée. Vous pouvez déduire l’ID d’appel de longue durée d’une instance de processus avec le nom d’utilisateur de l’initiateur du processus ou des participants au processus qui ont soumis leurs tâches.

Vous ne pouvez toutefois pas identifier l’ID de l’instance de processus pour un initiateur dans les cas suivants :

* **Processus déclenché par un dossier de contrôle** : une instance de processus ne peut pas être identifiée à l’aide de son initiateur si le processus est déclenché par un dossier de contrôle. Dans ce cas, les informations de l’utilisateur sont codées dans les données stockées.
* **Processus lancé à partir d’une instance de publication AEM** : toutes les instances de processus déclenchées depuis une instance de publication AEM ne capturent pas d’informations sur l’initiateur. Toutefois, les données utilisateur peuvent être capturées dans le formulaire associé au processus qui est stocké dans des variables de flux de travail.
* **Processus initié par courrier électronique** : L&#39;ID d&#39;adresse électronique de l&#39;expéditeur est capturé en tant que propriété dans une colonne blob opaque de la table de la  `tb_job_instance` base de données, qui ne peut pas être interrogée directement.

### Identification des ID de l’instance de processus lorsque l’initiateur ou le participant de flux de travail est connu {#initiator-participant}

Suivez les étapes ci-dessous pour identifier les ID de l’instance de processus pour un initiateur ou un participant de flux de travail :

1. Exécutez la commande suivante dans la base de données du serveur AEM Forms pour récupérer l&#39;ID principal de l&#39;initiateur ou du participant du flux de travail dans la table de base de données `edcprincipalentity`.

   ```sql
   select id from edcprincipalentity where canonicalname='user_ID'
   ```

   La requête renvoie l’ID principal pour l’ID `user_ID` spécifié.

1. (**Pour l’initiateur de flux de travail**) Exécutez la commande suivante pour récupérer toutes les tâches associées à l’ID principal pour l’initiateur dans la table de base de données `tb_task`.

   ```sql
   select * from tb_task where start_task = 1 and create_user_id= 'initiator_principal_id'
   ```

   La requête renvoie les tâches initiées par le `initiator`_ `principal_id` spécifié. Il existe deux types de tâche :

   * **Tâches** terminées : Ces tâches ont été envoyées et affichent une valeur alphanumérique dans le  `process_instance_id` champ. Notez tous les ID d’instance de processus pour les tâches envoyées et suivez les étapes.
   * **Tâches lancées mais non terminées** : ces tâches sont lancées mais n’ont pas encore été envoyées. La valeur du champ `process_instance_id` pour ces tâches est **0** (zéro). Dans ce cas, notez les ID de tâche correspondants et consultez l’article [Utilisation de tâches orphelines](#orphan).

1. (**Pour les participants au processus**) Exécutez la commande suivante pour récupérer les ID d&#39;instance de processus associés à l&#39;ID principal du participant au processus pour l&#39;initiateur dans la table de base de données `tb_assignment`.

   ```sql
   select distinct a.process_instance_id from tb_assignment a join tb_queue q on a.queue_id = q.id where q.workflow_user_id='participant_principal_id'
   ```

   La requête renvoie les ID d’instance pour tous les processus associés au participant, y compris ceux pour lesquels le participant n’a pas envoyé de tâche.

   Notez tous les ID d’instance de processus pour les tâches envoyées et suivez les étapes.

   Pour les tâches orphelines ou les tâches où `process_instance_id` est égal à 0 (zéro), notez les identifiants de tâche correspondants et consultez [Travailler avec des tâches orphelines](#orphan).

1. Suivez les instructions de la section [Purger les données utilisateur des instances de processus en fonction des ID d’instance de processus](/help/forms/using/forms-workflow-jee-handling-user-data.md#purge) pour supprimer les données utilisateur des ID d’instance de processus identifiés.

### Identification des ID de l’instance de processus lorsque les données utilisateur sont stockées dans des variables de type primitif {#primitive}

Un processus peut être conçu de telle sorte que les données utilisateur soient capturées dans une variable qui est stockée en tant que blob dans la base de données. Dans ce cas, vous pouvez interroger les données utilisateur uniquement si elles sont stockées dans l’une des variables de type primitif suivantes :

* **Chaîne** : contient l’ID utilisateur tel quel ou sous forme de sous-chaîne. Elle peut être interrogée via SQL.
* **Numérique** : contient l’ID utilisateur tel quel.
* **XML** : contient l’ID utilisateur sous forme de sous-chaîne dans le texte stocké en tant que colonnes de texte dans une base de données. XML peut être interrogé comme les chaînes.

Effectuez les étapes suivantes pour déterminer si un flux de travail qui stocke des données dans des variables de type primitif contient des données pour l’utilisateur :

1. Exécutez la commande de base de données suivante :

   ```sql
   select database_table from omd_object_type where name='pt_<app_name>/<workflow_name>'
   ```

   La requête renvoie un nom de table au format `tb_<number>` pour l&#39;application spécifiée ( `app_name`) et le flux de travail ( `workflow_name`).

   >[!NOTE]
   >
   >La valeur de la propriété `name` peut être complexe si le flux de travail est imbriqué dans des sous-dossiers au sein de l’application. Assurez-vous d’indiquer le chemin d’accès complet et exact du flux de travail. Vous pouvez l’obtenir à partir de la table de base de données `omd_object_type`.

1. Examinez le schéma de table `tb_<number>`. La table contient des variables qui stockent les données utilisateur pour le flux de travail spécifié. Les variables de la table correspondent aux variables du flux de travail.

   Identifiez et notez la variable correspondant à la variable de flux de travail contenant l’ID utilisateur. Si la variable identifiée est de type primitif, vous pouvez exécuter une requête pour déterminer les instances de flux de travail associées à un ID utilisateur.

1. Exécutez la commande de base de données suivante : Dans cette commande, `user_var` est la variable de type primitif qui contient l’ID utilisateur.

   ```sql
   select process_instance_id from <tb_name> where <user_var>=<user_ID>
   ```

   La requête renvoie tous les ID d’instance de processus associés à l’ID `user_ID` spécifié.

1. Suivez les instructions de la section [Purger les données utilisateur des instances de processus en fonction des ID d’instance de processus](/help/forms/using/forms-workflow-jee-handling-user-data.md#purge) pour supprimer les données utilisateur des ID d’instance de processus identifiés.

### Purger les données utilisateur à partir des instances de flux de travail en fonction des ID de l’instance de processus {#purge}

Après avoir identifié les ID de l’instance de processus associés à un utilisateur, procédez comme suit pour supprimer les données utilisateur des instances de processus respectives.

1. Exécutez la commande suivante pour récupérer l’ID et l’état d’appel de longue durée d’une instance de processus à partir de la table `tb_process_instance`.

   ```sql
   select long_lived_invocation_id, status from tb_process_instance where id='process_instance_id'
   ```

   La requête renvoie l’ID d’appel et l’état de longue durée pour le `process_instance_id` spécifié.

1. Créez une instance du client `ProcessManager` public ( `com.adobe.idp.workflow.client.ProcessManager`) en utilisant une instance `ServiceClientFactory` avec les paramètres de connexion corrects.

   Pour plus d’informations, consultez [Class ProcessManager](https://helpx.adobe.com/experience-manager/6-3/forms/ProgramLC/javadoc/com/adobe/idp/workflow/client/ProcessManager.html) dans la référence de l’API Java.

1. Vérifiez l’état de l’instance de flux de travail. Si l’état est différent de 2 (COMPLETE) ou 4 (TERMINÉ), terminez d’abord l’instance en appelant la méthode suivante :

   `ProcessManager.terminateProcess(<long_lived_invocation_id>)`.

1. Purgez l’instance de flux de travail en appelant la méthode suivante :

   `ProcessManager.purgeProcessInstance(<long_lived_invocation_id>)`

   La méthode `purgeProcessInstance` supprime définitivement toutes les données de l’ID d’appel spécifié dans la base de données du serveur AEM Forms et du répertoire de stockage global de documents, s’il est configuré.

### Utilisation des tâches orphelines {#orphan}

Les tâches orphelines sont les tâches dont le processus de conteneur a été initié mais pas encore envoyé. dans ce cas, `process_instance_id` est **0** (zéro). Vous ne pouvez donc pas effectuer le suivi des données utilisateur stockées pour les tâches orphelines à l’aide des ID d’instance de processus. Vous pouvez toutefois les suivre à l’aide de l’ID de tâche d’une tâche orpheline. Vous pouvez identifier les ID de tâches pour un utilisateur dans la table `tb_task` comme décrit dans la section [Identification des ID de l’instance de processus lorsque l’initiateur ou le participant de flux de travail est connu](/help/forms/using/forms-workflow-jee-handling-user-data.md#initiator-participant).

Une fois les ID de tâche obtenus, procédez comme suit pour purger les fichiers et les données associés à une tâche orpheline à partir du stockage global de documents et de la base de données.

1. Exécutez la commande suivante sur la base de données du serveur AEM Forms pour récupérer les ID des tâches identifiées.

   ```sql
   select id from tb_form_data where task_id=<task_id>
   ```

   La requête renvoie une liste d’ID. Pour chaque ID (`fd_id`) renvoyé dans les résultats, créez une liste de chaînes d’ID de session comme suit :

   * _ `wfattach<task_id>`
   * `_wftask<fd_id>`
   * `_wftaskformid<fd_id>`

1. Selon que votre stockage global de document pointe vers un système de fichiers ou une base de données, effectuez l’une des opérations suivantes :

   1. **Stockage global de document dans le système de fichiers** 

      Dans le système de fichiers du stockage global de document :

      1. Recherchez les fichiers dont les extensions sont associées aux chaînes d’ID de session suivantes :
      * `_wfattach<task_id>`
      * `_wftask<fd_id>`
      * `_wftaskformid<fd_id>`

      Les fichiers possédant ces extensions sont les fichiers de marquage. Ils sont enregistrés avec des noms de fichier au format suivant :

      `<file_name_guid>.session<session_id_string>`

      1. Supprimez tous les fichiers de marqueurs et autres fichiers dont le nom de fichier est `<file_name_guid>` du système de fichiers.
   1. **Stockage global de document dans la base de données** 

      Exécutez les commandes suivantes pour chaque ID de session :

      ```sql
      delete from tb_dm_chunk where documentid in (select documentid from tb_dm_session_reference where sessionid=<session_id>)
      delete from tb_dm_session_reference where sessionid=<session_id>
      delete from tb_dm_deletion where sessionid=<session_id>
      ```




1. Exécutez les commandes suivantes pour supprimer les données des ID de tâche de la base de données du serveur AEM Forms :

   ```sql
   delete from tb_task_acl where task_id=<task_id>
   delete from tb_task_attachment where task_id=<task_id>
   delete from tb_form_data where task_id=<task_id>
   delete from tb_assignment where task_id=<task_id>
   delete from tb_task where id=<task_id>
   ```

