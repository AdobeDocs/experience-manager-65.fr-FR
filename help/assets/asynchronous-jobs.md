---
title: Configurez des opérations asynchrones dans [!DNL Adobe Experience Manager].
description: Exécutez de manière asynchrone certaines tâches gourmandes en ressources pour optimiser les performances dans [!DNL Experience Manager Assets].
contentOwner: AG
translation-type: tm+mt
source-git-commit: b59f7471ab9f3c5e6eb3365122262b592c8e6244
workflow-type: tm+mt
source-wordcount: '660'
ht-degree: 14%

---


# Opérations asynchrones {#asynchronous-operations}

Afin de réduire l’impact négatif sur les performances, [!DNL Adobe Experience Manger Assets] traite de manière asynchrone certaines opérations d’actifs à long terme et gourmandes en ressources. Le traitement asynchrone implique la mise en file d&#39;attente de plusieurs tâches et leur exécution en série, sous réserve de la disponibilité des ressources système. Ces opérations incluent :

* Suppression de nombreuses ressources.
* Déplacement de nombreuses ressources ou de ressources avec de nombreuses références.
* Exportation et importation de métadonnées de fichier en bloc.
* Récupération des ressources d’un [!DNL Experience Manager] déploiement distant, qui sont supérieures à un seuil défini. La limite est fixée au nombre de ressources.

You can view the status of asynchronous tasks from the **[!UICONTROL Async Job Status]** page.

>[!NOTE]
>
>Par défaut, les [!DNL Assets] tâches s’exécutent en parallèle. If `N` is the number of CPU cores, `N/2` tasks can execute in parallel, by default. To use custom settings for the task queue, modify the **[!UICONTROL Async Operation Default Queue]** configuration from the [!UICONTROL Web Console]. For more information, see [queue configurations](https://sling.apache.org/documentation/bundles/apache-sling-eventing-and-job-handling.html#queue-configurations).

## Monitor the status of asynchronous operations {#monitoring-the-status-of-asynchronous-operations}

Chaque fois que [!DNL Assets] vous traitez une opération de manière asynchrone, vous recevez une notification dans votre [!DNL Experience Manager] boîte de [réception](/help/sites-authoring/inbox.md) et par courrier électronique. Pour afficher l’état des opérations asynchrones en détail, accédez à la page **[!UICONTROL État des tâches asynchrones]**.

1. Dans l’ [!DNL Experience Manager] interface, cliquez sur **[!UICONTROL Opérations]** > **[!UICONTROL Tâches]**.

1. Sur la page **[!UICONTROL État des tâches asynchrones]**, passez en revue les détails des opérations.

   ![Statut et détails des opérations asynchrones](assets/AsyncOperation-status.png)

   Pour connaître la progression d&#39;une opération, consultez la colonne **[!UICONTROL État]** . Selon la progression, l’un des états suivants s’affiche :

   * **[!UICONTROL Actif]** : l’opération est en cours de traitement..
   * **[!UICONTROL Succès]**: L&#39;opération est terminée.
   * **[!UICONTROL Échec]** ou **[!UICONTROL erreur]**: Impossible de traiter l&#39;opération.
   * **[!UICONTROL Programmé]**: Le traitement de l’opération est prévu ultérieurement.

1. To stop an active operation, select it from the list and click **[!UICONTROL Stop]** ![stop icon](assets/do-not-localize/stop_icon.svg) from the toolbar.

1. To view extra details, for example description and logs, select the operation and click **[!UICONTROL Open]** ![open_icon](assets/do-not-localize/edit_icon.svg) from the toolbar. La page Détails de la tâche s’affiche.

   ![Détails d’une tâche d’importation de métadonnées](assets/job_details.png)

1. Pour supprimer l’opération de la liste, sélectionnez **[!UICONTROL Supprimer]** dans la barre d’outils. To download the details in a CSV file, click **[!UICONTROL Download]**.

   >[!NOTE]
   >
   >Vous ne pouvez pas supprimer une tâche si son état est actif ou en file d’attente.

## Purger les tâches terminées {#purge-completed-tasks}

[!DNL Experience Manager Assets] exécute une tâche de purge tous les jours à 10 h pour supprimer les tâches asynchrones terminées qui ont plus d&#39;un jour.

<!-- TBD: Find out from the engineering team and mention the time zone of this 1:00 am task.
-->

Vous pouvez modifier la planification de la tâche de purge et la durée pendant laquelle les détails des tâches terminées sont conservés avant d&#39;être supprimés. Vous pouvez également configurer le nombre maximal de tâches terminées pour lesquelles les détails sont conservés à tout moment.

1. Dans l’ [!DNL Experience Manager] interface, cliquez sur **[!UICONTROL Outils]** > **[!UICONTROL Opérations]** > Console **** Web.
1. Open the **[!UICONTROL Adobe CQ DAM Async Jobs Purge Scheduled]** task.
1. Indiquez le nombre limite de jours après lequel les tâches terminées sont supprimées et le nombre maximal de tâches pour lesquelles les détails sont conservés dans l’historique. Enregistrez les modifications.

   ![Configuration pour planifier la purge de tâches asynchrones](assets/configmgr_purge_asyncjobs.png)

## Configurer un seuil pour les opérations de suppression asynchrones {#configure-thresholds-for-asynchronous-delete-operations}

Si le nombre de fichiers ou de dossiers à supprimer dépasse le seuil défini, l’opération de suppression est exécutée de manière asynchrone.

1. Dans l’ [!DNL Experience Manager] interface, cliquez sur **[!UICONTROL Outils]** > **[!UICONTROL Opérations]** > Console **** Web.
1. From the [!UICONTROL Web Console], open the **[!UICONTROL Async Delete Operation Job Processing]** configuration.
1. Dans la zone **[!UICONTROL Seuil de ressources]** , spécifiez les seuils pour supprimer de manière asynchrone des ressources, des dossiers ou des références. Enregistrez les modifications.

   ![Définir le seuil limite de la tâche de suppression des fichiers](assets/delete_threshold.png)

## Configurer le seuil pour les opérations de déplacement asynchrones {#configure-thresholds-for-asynchronous-move-operations}

Si le nombre de fichiers, de dossiers ou de références à déplacer dépasse le seuil défini, l’opération de déplacement est exécutée de manière asynchrone.

1. Dans l’ [!DNL Experience Manager] interface, cliquez sur **[!UICONTROL Outils]** > **[!UICONTROL Opérations]** > Console **** Web.
1. From the [!UICONTROL Web Console], open the **[!UICONTROL Async Move Operation Job Processing]** configuration.
1. Dans la zone **[!UICONTROL Seuil de ressources/références]** , indiquez les numéros de seuil pour déplacer de manière asynchrone des ressources, des dossiers ou des références. Enregistrez les modifications.

   ![Définir la limite de seuil de la tâche de déplacement des ressources](assets/move_threshold.png)

>[!MORELIKETHIS]
>
>* [Configurez le courrier électronique dans le Experience Manager](/help/sites-administering/notification.md).
>* [Importation et exportation des métadonnées de ressources par lot](/help/assets/metadata-import-export.md).
>* [Utilisez les ressources connectées pour partager des ressources DAM issues de déploiements](/help/assets/use-assets-across-connected-assets-instances.md)distants.

