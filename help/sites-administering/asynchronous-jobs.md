---
title: Opérations asynchrones
description: L'Adobe Experience Manager optimise les performances en exécutant de manière asynchrone certaines tâches gourmandes en ressources.
translation-type: tm+mt
source-git-commit: 69b90432ac6028a64f36300819e1bead1ae8d671
workflow-type: tm+mt
source-wordcount: '862'
ht-degree: 26%

---


# Opérations asynchrones {#asynchronous-operations}

Afin de réduire l’impact négatif sur les performances, Adobe Experience Manager traite de manière asynchrone certaines opérations à long terme gourmandes en ressources.

Ces opérations incluent :

* Suppression de nombreuses ressources
* Déplacement de nombreuses ressources ou de ressources avec de nombreuses références
* Exportation/importation de métadonnées de fichier en bloc
* Récupération des ressources, qui dépassent le seuil défini, à partir d’un déploiement de Experience Manager distant
* Déplacement de pages
* Déploiement de Live Copies

Le traitement asynchrone implique la mise en file d’attente de plusieurs tâches et leur exécution en série, sous réserve de la disponibilité des ressources système.

Vous pouvez vue l’état des tâches asynchrones à partir du tableau de bord État **[!UICONTROL de la tâche]** asynchrone dans Navigation **** globale -> **Outils** -> **Opérations -> Tâches.******

>[!NOTE]
>
>Par défaut, les tâches asynchrones s’exécutent en parallèle. If *`n`* is the number of CPU cores, *`n/2`* jobs can run in parallel, by default. Pour utiliser des paramètres personnalisés pour la file d’attente des tâches, modifiez la configuration **[!UICONTROL de la file d’attente]** par défaut de l’opération **asynchrone et la configuration de déploiement et de déplacement de page de l’opération** asynchroneà partir de la console Web.
>
>For more information, see [queue configurations](https://sling.apache.org/documentation/bundles/apache-sling-eventing-and-job-handling.html#queue-configurations).

## Monitor the Status of Asynchronous Operations {#monitor-the-status-of-asynchronous-operations}

Chaque fois qu’AEM traite une opération de manière asynchrone, vous recevez une notification dans votre boîte de réception et par courrier électronique (si elle est activée).

Pour afficher l’état des opérations asynchrones en détail, accédez à la page **[!UICONTROL État des tâches asynchrones]**.

1. Dans l’interface du Experience Manager, cliquez sur **[!UICONTROL Opérations]** > **[!UICONTROL Tâches]**.

1. Sur la page **[!UICONTROL État des tâches asynchrones]**, passez en revue les détails des opérations.

   ![Statut et détails des opérations asynchrones](assets/async-operation-status.png)

   To determine the progress of a particular operation, see the value in the **[!UICONTROL Status]** column. Selon la progression, l’un des états suivants s’affiche :

   * **[!UICONTROL Actif]** : l’opération est en cours de traitement.

   * **[!UICONTROL Réussite]** : l’opération est terminée.

   * **[!UICONTROL Échec]** ou **[!UICONTROL Erreur]** : l’opération n’a pas pu être traitée.

   * **[!UICONTROL Planifié]** : l’opération est planifiée à une date ultérieure.

1. To stop an active operation, select it from the list and click **[!UICONTROL Stop]** from the toolbar.

   ![stop_icon](assets/async-stop-icon.png)

1. To view extra details, for example description and logs, select the operation and click **[!UICONTROL Open]** from the toolbar.

   ![open_icon](assets/async-open-icon.png)

   La page des détails de la tâche s’affiche.

   ![job_details](assets/async-job-details.png)

1. Pour supprimer l’opération de la liste, sélectionnez **[!UICONTROL Supprimer]** dans la barre d’outils. To download the details in a CSV file, click **[!UICONTROL Download]**.

   >[!NOTE]
   >
   >You cannot delete a job if its status is either **Active** or **Queued**.

## Purger les tâches terminées {#purging-completed-jobs}

AEM exécute une tâche de purge tous les jours à 01:00 pour supprimer les tâches asynchrones terminées qui ont plus d’un jour d’existence.

Vous pouvez modifier la planification de la tâche de purge et la durée de conservation des détails des tâches terminées avant leur suppression. Vous pouvez également configurer le nombre maximal de tâches terminées pour lesquelles les détails sont conservés à un moment donné dans le temps.

1. Dans la navigation globale, cliquez sur **[!UICONTROL Outils]** > **[!UICONTROL Opérations]** > Console **** Web.
1. Ouvrez la tâche **[!UICONTROL Adobe Granite Async Jobs Purger la tâche]** planifiée.
1. Précisez les paramètres suivants :
   * Nombre seuil de jours après lequel les tâches terminées sont supprimées.
   * Nombre maximal de tâches pour lesquelles des détails sont conservés dans l’historique.
   * expression cron pour le moment où la purge doit s&#39;exécuter.

   ![Configuration visant à planifier la purge des tâches asynchrones](assets/async-purge-job.png)

1. Enregistrez les modifications.

## Configurer le traitement asynchrone {#configuring-asynchronous-processing}

Vous pouvez configurer le nombre seuil de ressources, de pages ou de références pour AEM afin qu’AEM traite une opération particulière de manière asynchrone et bascule les notifications électroniques pour le moment où les tâches sont traitées.

### Configurer des opérations de suppression de ressources asynchrones {#configuring-synchronous-delete-operations}

Si le nombre de fichiers ou de dossiers à supprimer dépasse le seuil, l’opération de suppression est exécutée de manière asynchrone.

1. Dans la navigation globale, cliquez sur **[!UICONTROL Outils]** > **[!UICONTROL Opérations]** > Console **** Web.
1. Dans la console Web, ouvrez la configuration de la file d’attente par défaut du processus **[!UICONTROL asynchrone.]**
1. Dans le champ **[!UICONTROL Nombre seuil de ressources]**, spécifiez le nombre seuil de ressources/dossiers pour le traitement asynchrone des opérations de suppression.

   ![Seuil de suppression des ressources](assets/async-delete-threshold.png)

1. Cochez l’option **Activer la notification** par courrier électronique pour recevoir des notifications par courrier électronique concernant cet état de tâche. Par exemple, succès, échec.
1. Enregistrez les modifications.

### Configuration des opérations de transfert de ressources asynchrones {#configuring-asynchronous-move-operations}

Si le nombre de fichiers/dossiers ou de références à déplacer dépasse le nombre seuil, l’opération de déplacement est exécutée de manière asynchrone.

1. Dans la navigation globale, cliquez sur **[!UICONTROL Outils]** > **[!UICONTROL Opérations]** > Console **** Web.
1. From the web console, open the **[!UICONTROL Async Move Operation Job Processing Configuration.]**
1. Dans le champ **[!UICONTROL Nombre seuil de ressources/références]**, spécifiez le nombre seuil de ressources/dossiers ou références pour le traitement asynchrone des opérations de déplacement.

   ![Seuil de déplacement des ressources](assets/async-move-threshold.png)

1. Cochez l’option **Activer la notification** par courrier électronique pour recevoir des notifications par courrier électronique concernant cet état de tâche. Par exemple, succès, échec.
1. Enregistrez les modifications.

### Configuration des opérations de déplacement de page asynchrones {#configuring-asynchronous-page-move-operations}

Si le nombre de références aux pages à déplacer dépasse le nombre seuil, l’opération de déplacement est exécutée de manière asynchrone.

1. Dans la navigation globale, cliquez sur **[!UICONTROL Outils]** > **[!UICONTROL Opérations]** > Console **** Web.
1. From the web console, open the **[!UICONTROL Async Page Move Operation Job Processing Configuration.]**
1. In the **[!UICONTROL Threshold number of references]** field, specify the threshold number of references for asynchronous processing of page move operations.

   ![Seuil de déplacement de page](assets/async-page-move.png)

1. Cochez l’option **Activer la notification** par courrier électronique pour recevoir des notifications par courrier électronique concernant cet état de tâche. Par exemple, succès, échec.
1. Enregistrez les modifications.

### Configuration des opérations MSM asynchrones {#configuring-asynchronous-msm-operations}

1. Dans la navigation globale, cliquez sur **[!UICONTROL Outils]** > **[!UICONTROL Opérations]** > Console **** Web.
1. From the web console, open the **[!UICONTROL Async Page Move Operation Job Processing Configuration.]**
1. Cochez l’option **Activer la notification** par courrier électronique pour recevoir des notifications par courrier électronique concernant cet état de tâche. Par exemple, succès, échec.

   ![Configuration MSM](assets/async-msm.png)

1. Enregistrez les modifications.
