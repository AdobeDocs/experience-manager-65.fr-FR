---
title: Opérations asynchrones
description: AEM Assets optimise les performances en exécutant certaines tâches consommatrices de ressources de manière asynchrone.
contentOwner: AG
translation-type: tm+mt
source-git-commit: c7d0bcbf39adfc7dfd01742651589efb72959603

---


# Opérations asynchrones {#asynchronous-operations}

Pour réduire l’impact négatif sur les performances, Adobe Experience Manager (AEM) Assets traite de manière asynchrone certaines opérations sur les ressources de longue durée et requérant de nombreuses ressources système.

Ces opérations incluent :

* Suppression de nombreuses ressources
* Déplacement de nombreuses ressources ou de ressources avec de nombreuses références
* Exportation/importation de métadonnées de ressources en masse
* Récupération des ressources dépassant la limite de seuil définie à partir d’un déploiement AEM distant.

Le traitement asynchrone implique de mettre plusieurs tâches en file d’attente et de les exécuter par la suite en série selon la disponibilité des ressources système.

Vous pouvez afficher l’état des tâches asynchrones à partir de la page **[!UICONTROL État des tâches asynchrones]**.

>[!NOTE]
>
>Par défaut, les tâches dans AEM Assets s’exécutent en parallèle. Si N est le nombre de cœurs d’unité centrale, N/2 tâches peuvent s’exécuter en parallèle, par défaut. Pour utiliser des paramètres personnalisés pour la file d’attente des travaux, modifiez la configuration **[!UICONTROL File d’attente par défaut des opérations asynchrones]** à partir de la console web. For more information, see [queue configurations](https://sling.apache.org/documentation/bundles/apache-sling-eventing-and-job-handling.html#queue-configurations).

## Monitor the status of asynchronous operations {#monitoring-the-status-of-asynchronous-operations}

Chaque fois qu’AEM Assets traite une opération asynchrone, vous recevez une notification dans votre boîte de réception et par courrier électronique.

Pour afficher l’état des opérations asynchrones en détail, accédez à la page **[!UICONTROL État des tâches asynchrones]**.

1. Dans l’interface d’Experience Manager, cliquez sur **[!UICONTROL Opérations]** > **[!UICONTROL Tâches]**.

1. Sur la page **[!UICONTROL État des tâches asynchrones]**, passez en revue les détails des opérations.

   ![État et détails des opérations asynchrones](assets/AsyncOperation-status.png)

   Pour vérifier la progression d’une opération particulière, reportez-vous à la valeur dans la colonne **[!UICONTROL État]**. Selon la progression, l’un des états suivants s’affiche :

   * **[!UICONTROL Actif]** : l’opération est en cours de traitement.

   * **[!UICONTROL Réussite]** : l’opération est terminée.

   * **[!UICONTROL Échec]** ou **[!UICONTROL Erreur]** : l’opération n’a pas pu être traitée.

   * **[!UICONTROL Planifié]** : l’opération est planifiée à une date ultérieure.

1. To stop an active operation, select it from the list and click **[!UICONTROL Stop]** from the toolbar.

   ![stop_icon](assets/stop_icon.png)

1. To view extra details, for example description and logs, select the operation and click **[!UICONTROL Open]** from the toolbar.

   ![open_icon](assets/open_icon.png)

   La page des détails de la tâche s’affiche.

   ![job_details](assets/job_details.png)

1. Pour supprimer l’opération de la liste, sélectionnez **[!UICONTROL Supprimer]** dans la barre d’outils. To download the details in a CSV file, click **[!UICONTROL Download]**.

   >[!NOTE]
   >
   >Vous ne pouvez pas supprimer une tâche si son état est Actif ou Placé en file d’attente.

## Purger les tâches terminées {#purging-completed-jobs}

AEM Assets exécute une tâche de purge quotidienne à 1 h 00 du matin afin de supprimer les tâches asynchrones terminées depuis plus d’un jour.

Vous pouvez modifier la planification de la tâche de purge et la durée de conservation des détails des tâches terminées avant leur suppression. Vous pouvez également configurer le nombre maximal de tâches terminées pour lesquelles les détails sont conservés à un moment donné dans le temps.

1. Dans l’interface d’Experience Manager, cliquez sur **[!UICONTROL Outils]** > **[!UICONTROL Opérations]** > Console **** Web.
1. Ouvrez la tâche **[!UICONTROL Purge planifiée des tâches asynchrones de la gestion des ressources numériques Adobe CQ]**.
1. Spécifiez le nombre seuil de jours à l’issue duquel les tâches terminées sont supprimées et le nombre maximal de tâches pour lesquelles des détails sont conservés dans l’historique.

   ![Configuration visant à planifier la purge des tâches asynchrones](assets/configmgr_purge_asyncjobs.png)

1. Enregistrez les modifications.

## Configure thresholds for asynchronous processing {#configuring-thresholds-for-asynchronous-processing}

Vous pouvez configurer le nombre seuil de ressources ou de références pour AEM Assets afin de traiter une opération spécifique de façon asynchrone.

### Configure thresholds for asynchronous delete operations {#configuring-thresholds-for-asynchronous-delete-operations}

Si le nombre de ressources ou de dossiers à supprimer dépasse le nombre seuil, l’opération de suppression est effectuée de façon asynchrone.

1. Dans l’interface d’Experience Manager, cliquez sur **[!UICONTROL Outils]** > **[!UICONTROL Opérations]** > Console **** Web.
1. Dans la console web, ouvrez la configuration **[!UICONTROL Traitement des tâches des opérations de suppression asynchrones]**.
1. Dans le champ **[!UICONTROL Nombre seuil de ressources]**, spécifiez le nombre seuil de ressources/dossiers pour le traitement asynchrone des opérations de suppression.

   ![delete_threshold](assets/delete_threshold.png)

1. Enregistrez les modifications.

### Configure thresholds for asynchronous move operations {#configuring-thresholds-for-asynchronous-move-operations}

Si le nombre de ressources/dossiers ou de références à déplacer dépasse le nombre seuil, l’opération de déplacement est effectuée de façon asynchrone.

1. Dans l’interface d’Experience Manager, cliquez sur **[!UICONTROL Outils]** > **[!UICONTROL Opérations]** > Console **** Web.
1. Dans la console web, ouvrez la configuration **[!UICONTROL Traitement des tâches des opérations de déplacement asynchrones]**.
1. Dans le champ **[!UICONTROL Nombre seuil de ressources/références]**, spécifiez le nombre seuil de ressources/dossiers ou références pour le traitement asynchrone des opérations de déplacement.

   ![move_threshold](assets/move_threshold.png)

1. Enregistrez les modifications.
