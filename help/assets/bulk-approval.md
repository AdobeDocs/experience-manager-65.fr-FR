---
title: Révision de collections et de ressources situées dans un dossier
description: Mettez en place des workflow de révision pour les ressources dans un dossier ou une collection et partagez ce processus avec les réviseurs ou les partenaires de conception afin d’obtenir leurs commentaires.
contentOwner: AG
feature: Collaboration, collections
role: Professionnel
translation-type: tm+mt
source-git-commit: 2e734041bdad7332c35ab41215069ee696f786f4
workflow-type: tm+mt
source-wordcount: '788'
ht-degree: 62%

---


# Révision de collections et de ressources situées dans un dossier {#review-folder-assets-and-collections}

Mettez en place des workflows de révision pour les ressources dans un dossier ou une collection et partagez ce workflow avec les réviseurs ou les partenaires de conception afin d’obtenir leurs commentaires.

[!DNL Adobe Experience Manager Assets] permet de configurer un workflow de révision ad hoc pour les ressources situées dans un dossier ou une collection et de partager ce workflow avec des réviseurs ou des partenaires de conception afin d’obtenir leurs commentaires.

Vous pouvez associer le workflow de révision à un projet ou créer une tâche de révision indépendante.

Une fois que vous avez partagé les ressources, les réviseurs peuvent les approuver ou les rejeter. Les notifications sont envoyées à différentes étapes du workflow pour informer les destinataires voulus de la fin des diverses tâches. Par exemple, lorsque vous partagez un dossier ou une collection, le réviseur reçoit une notification lui indiquant qu’un dossier/une collection a été partagé pour la révision.

Une fois que le réviseur a terminé la révision (approuvé ou rejeté les ressources), vous recevez une notification de fin de révision.

## Créer une tâche de révision pour les dossiers {#creating-a-review-task-for-folders}

1. Dans l&#39;interface utilisateur [!DNL Assets], sélectionnez le dossier pour lequel vous souhaitez créer une tâche de révision.
1. Dans la barre d’outils, cliquez sur **[!UICONTROL Créer une Tâche de révision]** ![créer une tâche de révision](assets/do-not-localize/create-review-task.png) pour ouvrir la page **[!UICONTROL Tâche de révision]**. Si l’option n’est pas visible dans la barre d’outils, cliquez sur **[!UICONTROL Plus]**, puis sélectionnez l’option.

1. (Facultatif) Dans la liste **[!UICONTROL Projets]**, choisissez le projet auquel vous voulez associer la tâche de révision. Par défaut, l’option **[!UICONTROL Aucun]** est sélectionnée. Si vous ne souhaitez associer aucun projet à la tâche de révision, conservez cette sélection.

   >[!NOTE]
   >
   >Seuls les projets pour lesquels vous disposez d’autorisations de niveau Éditeur (ou supérieur) apparaissent dans la liste **[!UICONTROL Projets]**.

1. Entrez un nom pour la tâche de révision, puis sélectionnez un approbateur dans la liste **[!UICONTROL Affecter à.]**

   >[!NOTE]
   >
   >Les membres/groupes du projet sélectionné sont disponibles en tant qu’approbateurs dans la liste **[!UICONTROL Affecter à.]**

1. Entrez une description, la priorité et la date d’échéance de la tâche de révision.

   ![task_details](assets/task_details.png)

1. Dans l’onglet Avancé, entrez le libellé à utiliser pour créer l’URI.

   ![review_name](assets/review_name.png)

1. Cliquez sur **[!UICONTROL Envoyer]**, puis sur **[!UICONTROL Terminé]** pour fermer le message de confirmation. Une notification pour la nouvelle tâche est envoyée à l’approbateur.
1. Connectez-vous à [!DNL Assets] en tant qu’approbateur et accédez à l’IU [!DNL Assets] Pour approuver des actifs, cliquez sur **[!UICONTROL Notifications]**, puis sélectionnez la tâche de révision dans la liste.

   ![Notification des ressources](assets/aemAssetsNotification.png)

1. Dans la page **[!UICONTROL Tâche de révision]**, examinez les détails de la tâche de révision, puis cliquez sur **[!UICONTROL Réviser]**.
1. Dans la page **[!UICONTROL Réviser la Tâche]**, sélectionnez les ressources, puis cliquez sur **[!UICONTROL Approuver/Rejeter]** pour approuver ou rejeter, selon le cas.

   ![review_task](assets/review_task.png)

1. Cliquez sur **[!UICONTROL Terminé]** dans la barre d’outils. Dans la boîte de dialogue, saisissez un commentaire et cliquez sur **[!UICONTROL Terminer]** pour confirmer.
1. Accédez à l&#39;interface utilisateur [!DNL Assets] et ouvrez le dossier. Les icônes d’état d’approbation des ressources s’affichent dans la vue de carte et la vue de liste.

   **Mode Carte**

   ![Vérifier l’état tel qu’il apparaît dans la vue de cartes](assets/chlimage_1-404.png)

   **Mode Liste**

   ![Vérifier l’état tel qu’il est affiché dans liste vue](assets/review_status_listview.png)

## Créer une tâche de révision pour les collections {#creating-a-review-task-for-collections}

1. Sur la page Collections, sélectionnez la collection pour laquelle vous souhaitez créer une tâche de révision.
1. Dans la barre d’outils, cliquez sur **[!UICONTROL Créer une Tâche de révision]** ![créer une tâche de révision](assets/do-not-localize/create-review-task.png) pour ouvrir la page **[!UICONTROL Tâche de révision]**. Si vous ne pouvez pas voir l’option dans la barre d’outils, cliquez sur **[!UICONTROL Plus]**, puis sélectionnez l’option.

1. (Facultatif) Dans la liste **[!UICONTROL Projets]**, choisissez le projet auquel vous voulez associer la tâche de révision. Par défaut, l’option **[!UICONTROL Aucun]** est sélectionnée. Si vous ne souhaitez associer aucun projet à la tâche de révision, conservez cette sélection.

   >[!NOTE]
   >
   >Seuls les projets pour lesquels vous disposez d’autorisations de niveau Éditeur (ou supérieur) apparaissent dans la liste **[!UICONTROL Projets]**.

1. Entrez un nom pour la tâche de révision, puis sélectionnez un approbateur dans la liste **[!UICONTROL Affecter à.]**

   >[!NOTE]
   >
   >Les membres/groupes du projet sélectionné sont disponibles en tant qu’approbateurs dans la liste **[!UICONTROL Affecter à.]**

1. Entrez une description, la priorité et la date d’échéance de la tâche de révision.

   ![task_details-collection](assets/task_details-collection.png)

1. Cliquez sur **[!UICONTROL Envoyer]**, puis sur **[!UICONTROL Terminé]** pour fermer le message de confirmation. Une notification pour la nouvelle tâche est envoyée à l’approbateur.
1. Connectez-vous à [!DNL Assets] en tant qu’approbateur et accédez à la console [!DNL Assets]. Pour approuver des actifs, cliquez sur **[!UICONTROL Notifications]**, puis sélectionnez la tâche de révision dans la liste.
1. Dans la page **[!UICONTROL Tâche de révision]**, examinez les détails de la tâche de révision, puis cliquez sur **[!UICONTROL Réviser]**.
1. Toutes les ressources situées dans la collection sont visibles dans le panneau de révision. Sélectionnez les actifs et cliquez sur **[!UICONTROL Approuver/Rejeter]** pour approuver ou rejeter les actifs, selon le cas.

   ![review_task_collection](assets/review_task_collection.png)

1. Cliquez sur **[!UICONTROL Terminé]** dans la barre d’outils. Dans la boîte de dialogue, saisissez un commentaire et cliquez sur **[!UICONTROL Terminer]** pour confirmer.
1. Accédez à la console Collections et ouvrez la collection. Les icônes d’état d’approbation pour les ressources apparaissent dans les modes Carte et Liste.

   ![collection_reviewstatuscardview](assets/collection_reviewstatuscardview.png)

   *Figure : Vue de carte.*

   ![collection_reviewstatuslistview](assets/collection_reviewstatuslistview.png)

   *Figure : Vue de liste.*
