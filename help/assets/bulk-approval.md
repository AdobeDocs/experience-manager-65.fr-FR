---
title: Révision de collections et de ressources situées dans un dossier
description: Mettez en place des workflow de révision pour les ressources dans un dossier ou une collection et partagez ce processus avec les réviseurs ou les partenaires de conception afin d’obtenir leurs commentaires.
contentOwner: AG
translation-type: tm+mt
source-git-commit: e71b87b12d45bf12f29af917fddebeddedb18056

---


# Révision de collections et de ressources situées dans un dossier {#review-folder-assets-and-collections}

Mettez en place des workflow de révision pour les ressources dans un dossier ou une collection et partagez ce processus avec les réviseurs ou les partenaires de conception afin d’obtenir leurs commentaires.

Adobe Experience Manager (AEM) Assets permet de configurer un workflow de révision ad hoc pour les ressources situées dans un dossier ou une collection et de partager ce workflow avec des réviseurs ou des partenaires de conception afin d’obtenir leurs commentaires.

Vous pouvez associer le workflow de révision à un projet ou créer une tâche de révision indépendante.

Une fois que vous avez partagé les ressources, les réviseurs peuvent les approuver ou les rejeter. Les notifications sont envoyées à différentes étapes du workflow pour informer les destinataires voulus de la fin des diverses tâches. Par exemple, lorsque vous partagez un dossier ou une collection, le réviseur reçoit une notification lui indiquant qu’un dossier/une collection a été partagé(e) pour la révision.

Une fois que le réviseur a terminé la révision (approuvé ou rejeté les ressources), vous recevez une notification de fin de révision.

## Create a review task for folders {#creating-a-review-task-for-folders}

1. Dans l’interface utilisateur Assets, sélectionnez le dossier pour lequel vous souhaitez créer une tâche de révision.
1. From the toolbar, tap **[!UICONTROL Create Review Task]** to open the **[!UICONTROL Review Task]** page. If you cannot see the option in the toolbar, tap/click **[!UICONTROL More]** and then select the option.

   ![chlimage_1-403](assets/chlimage_1-403.png)

1. (Optional) From the **[!UICONTROL Project]** list, select the project to which you want to associate the review task. By default, the **[!UICONTROL None]** option is selected. Si vous ne souhaitez associer aucun projet à la tâche de révision, conservez cette sélection.

   >[!NOTE]
   >
   >Seuls les projets pour lesquels vous disposez d’autorisations de niveau Éditeur (ou supérieur) apparaissent dans la liste **[!UICONTROL Projets]**.

1. Entrez un nom pour la tâche de révision, puis sélectionnez un approbateur dans la liste **[!UICONTROL Affecter à.]**

   >[!NOTE]
   >
   >Les membres/groupes du projet sélectionné sont disponibles en tant qu’approbateurs dans la liste **[!UICONTROL Affecter à.]**

1. Entrez une description, la priorité et la date d’échéance de la tâche de révision.

   ![_details](assets/task_details.png)

1. Dans l’onglet Avancé, entrez le libellé à utiliser pour créer l’URI.

   ![review_name](assets/review_name.png)

1. Appuyez/cliquez sur **[!UICONTROL Envoyer]**, puis sur **[!UICONTROL Terminé]** pour fermer le message de confirmation. Une notification pour la nouvelle tâche est envoyée à l’approbateur.
1. Connectez-vous à AEM Assets en tant qu’approbateur et accédez à l’IU Assets. To approve assets, tap **[!UICONTROL Notifications]** and then select the review task from the list.

   ![Notification de ressources](assets/aemAssetsNotification.png)

1. Dans la page **[!UICONTROL Tâche de révision]**, examinez les détails de la tâche de révision, puis appuyez/cliquez sur **[!UICONTROL Réviser]**.
1. In the **[!UICONTROL Review Task]** page, select assets, and tap **[!UICONTROL Approve/Reject]** to approve or reject, as appropriate.

   ![review_](assets/review_task.png)

1. Appuyez sur **[!UICONTROL Terminer]** dans la barre d’outils. In the dialog, enter a comment and tap/click  **[!UICONTROL Complete]** to confirm.
1. Accédez à l’interface utilisateur Ressources et ouvrez le dossier. Les icônes d’état d’approbation des ressources s’affichent dans les  de carte et les  de .

   **Mode Carte**

   ![Vérifier l’état tel qu’il apparaît dans le de cartes](assets/chlimage_1-404.png)

   **Mode Liste**

   ![Vérifier l&#39;état tel qu&#39;il est vu dans  de](assets/review_status_listview.png)

## Create a review task for collections {#creating-a-review-task-for-collections}

1. Sur la page Collections, sélectionnez la collection pour laquelle vous souhaitez créer une tâche de révision.
1. From the toolbar, tap **[!UICONTROL Create Review Task]** to open the **[!UICONTROL Review Task]** page. If you cannot see the option on the toolbar, tap **[!UICONTROL More]** and then select the option.

   ![chlimage_1-405](assets/chlimage_1-405.png)

1. (Optional) From the **[!UICONTROL Project]** list, select the project to which you want to associate the review task. By default, the **[!UICONTROL None]** option is selected. Si vous ne souhaitez associer aucun projet à la tâche de révision, conservez cette sélection.

   >[!NOTE]
   >
   >Seuls les projets pour lesquels vous disposez d’autorisations de niveau Éditeur (ou supérieur) apparaissent dans la liste **[!UICONTROL Projets]**.

1. Entrez un nom pour la tâche de révision, puis sélectionnez un approbateur dans la liste **[!UICONTROL Affecter à.]**

   >[!NOTE]
   >
   >Les membres/groupes du projet sélectionné sont disponibles en tant qu’approbateurs dans la liste **[!UICONTROL Affecter à.]**

1. Entrez une description, la priorité et la date d’échéance de la tâche de révision.

   ![_details-collection](assets/task_details-collection.png)

1. Appuyez/cliquez sur **[!UICONTROL Envoyer]**, puis sur **[!UICONTROL Terminé]** pour fermer le message de confirmation. Une notification pour la nouvelle tâche est envoyée à l’approbateur.
1. Connectez-vous à AEM Assets en tant qu’approbateur et accédez à la console Ressources. To approve assets, tap **[!UICONTROL Notifications]** and then select the review task from the list.
1. Dans la page **[!UICONTROL Tâche de révision]**, examinez les détails de la tâche de révision, puis appuyez/cliquez sur **[!UICONTROL Réviser]**.
1. Toutes les ressources situées dans la collection sont visibles dans le panneau de révision. Select the assets and tap **[!UICONTROL Approve/Reject]** to approve or reject assets, as appropriate.

   ![review___collection](assets/review_task_collection.png)

1. Appuyez sur **[!UICONTROL Terminer]** dans la barre d’outils. In the dialog, enter a comment and tap/click **[!UICONTROL Complete]** to confirm.
1. Accédez à la console Collections et ouvrez la collection. Les icônes d’état d’approbation pour les ressources apparaissent dans les modes Carte et Liste.

   ![collection_reviewstatuscardview](assets/collection_reviewstatuscardview.png)

   *Figure :  de carte*

   ![collection_reviewstatuslistview](assets/collection_reviewstatuslistview.png)

   *Figure :*
