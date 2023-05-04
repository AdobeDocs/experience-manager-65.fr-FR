---
title: Révision de collections et de ressources situées dans un dossier
description: Mettez en place des workflows de révision pour les ressources dans un dossier ou une collection et partagez ce workflow avec les réviseurs ou les partenaires de conception afin d’obtenir leurs commentaires.
contentOwner: AG
feature: Collaboration, Collections
role: User
exl-id: 23c90e10-aa03-450e-9fb0-2f5be0c5066b
source-git-commit: 3d713021ac410ca2925a282c5dfca98ed4e483ee
workflow-type: tm+mt
source-wordcount: '807'
ht-degree: 81%

---

# Révision de collections et de ressources situées dans un dossier {#review-folder-assets-and-collections}

| Version | Lien de l’article |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Cliquez ici](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/manage/bulk-approval.html?lang=fr) |
| AEM 6.5 | Cet article |

Mettez en place des workflows de révision pour les ressources dans un dossier ou une collection et partagez ce workflow avec les réviseurs ou les partenaires de conception afin d’obtenir leurs commentaires.

[!DNL Adobe Experience Manager Assets] permet de configurer un workflow de révision ad hoc pour les ressources situées dans un dossier ou une collection et de partager ce workflow avec des réviseurs ou des partenaires de conception afin d’obtenir leurs commentaires.

Vous pouvez associer le workflow de révision à un projet ou créer une tâche de révision indépendante.

Une fois que vous avez partagé les ressources, les réviseurs peuvent les approuver ou les rejeter. Les notifications sont envoyées à différentes étapes du workflow pour informer les destinataires prévus de l&#39;achèvement de diverses tâches. Par exemple, lorsque vous partagez un dossier ou une collection, le réviseur reçoit une notification lui indiquant qu’un dossier/une collection a été partagé pour la révision.

Une fois que le réviseur a terminé la révision (approuve ou refuse les ressources), vous recevez une notification de fin de révision.

## Création d’une tâche de révision pour des dossiers {#creating-a-review-task-for-folders}

1. Dans l’interface utilisateur d’[!DNL Assets], sélectionnez le dossier pour lequel vous souhaitez créer une tâche de révision.
1. Dans la barre d’outils, cliquez sur **[!UICONTROL Créer une tâche de révision]** ![créer une tâche de révision](assets/do-not-localize/create-review-task.png) pour ouvrir la page **[!UICONTROL Tâche de révision]**. Si l’option n’apparaît pas dans la barre d’outils, cliquez sur **[!UICONTROL Plus]** puis sélectionnez l’option.

1. (Facultatif) Dans la liste **[!UICONTROL Projets]**, choisissez le projet auquel vous voulez associer la tâche de révision. Par défaut, l’option **[!UICONTROL Aucun]** est sélectionnée. Si vous ne souhaitez associer aucun projet à la tâche de révision, conservez cette sélection.

   >[!NOTE]
   >
   >Seuls les projets pour lesquels vous disposez d’autorisations de niveau Éditeur (ou supérieur) sont visibles dans la variable **[!UICONTROL Projets]** liste.

1. Entrez un nom pour la tâche de révision, puis sélectionnez un approbateur dans la liste **[!UICONTROL Affecter à.]**

   >[!NOTE]
   >
   >Les membres/groupes du projet sélectionné sont disponibles en tant qu’approbateurs dans la liste **[!UICONTROL Affecter à.]**

1. Entrez une description, la priorité et la date d’échéance de la tâche de révision.

   ![task_details](assets/task_details.png)

1. Dans l’onglet Avancé, entrez le libellé à utiliser pour créer l’URI.

   ![review_name](assets/review_name.png)

1. Cliquez sur **[!UICONTROL Envoyer]**, puis sur **[!UICONTROL Terminé]** pour fermer le message de confirmation. Une notification pour la nouvelle tâche est envoyée à l’approbateur.
1. Connectez-vous à [!DNL Assets] en tant qu’approbateur et accédez à l’IU d’[!DNL Assets]. Pour approuver des ressources, cliquez sur **[!UICONTROL Notifications]**, puis sélectionnez la tâche de révision dans la liste.

   ![Notification d’Assets](assets/aemAssetsNotification.png)

1. Sur la page **[!UICONTROL Tâche de révision]**, examinez les détails de la tâche de révision, puis cliquez sur **[!UICONTROL Réviser]**.
1. Sur la page **[!UICONTROL Tâche de révision]**, sélectionnez les ressources, puis cliquez sur **[!UICONTROL Approuver/Rejeter]** pour approuver ou rejeter les modifications.

   ![review_task](assets/review_task.png)

1. Cliquez sur **[!UICONTROL Terminé]** dans la barre d’outils. Dans la boîte de dialogue, saisissez un commentaire, puis cliquez sur **[!UICONTROL Terminé]** pour confirmer.
1. Accédez à l’interface utilisateur d’[!DNL Assets] et ouvrez le dossier. Les icônes de statut d’approbation des ressources s’affichent dans les vues Carte et Liste.

   **Mode Carte**

   ![Statut de révision tel qu’affiché en mode Carte](assets/chlimage_1-404.png)

   **Vue Liste**

   ![Statut de révision tel qu’affiché dans la vue Liste](assets/review_status_listview.png)

## Création d’une tâche de révision pour les collections {#creating-a-review-task-for-collections}

1. Sur la page Collections, sélectionnez la collection pour laquelle vous souhaitez créer une tâche de révision.
1. Dans la barre d’outils, cliquez sur **[!UICONTROL Créer une tâche de révision]** ![créer une tâche de révision](assets/do-not-localize/create-review-task.png) pour ouvrir la page **[!UICONTROL Tâche de révision]**. Si l’option n’apparaît pas dans la barre d’outils, cliquez sur **[!UICONTROL Plus]** puis sélectionnez l’option.

1. (Facultatif) Dans la liste **[!UICONTROL Projets]**, choisissez le projet auquel vous voulez associer la tâche de révision. Par défaut, l’option **[!UICONTROL Aucun]** est sélectionnée. Si vous ne souhaitez associer aucun projet à la tâche de révision, conservez cette sélection.

   >[!NOTE]
   >
   >Seuls les projets pour lesquels vous disposez d’autorisations de niveau Éditeur (ou supérieur) sont visibles dans la variable **[!UICONTROL Projets]** liste.

1. Entrez un nom pour la tâche de révision, puis sélectionnez un approbateur dans la liste **[!UICONTROL Affecter à.]**

   >[!NOTE]
   >
   >Les membres/groupes du projet sélectionné sont disponibles en tant qu’approbateurs dans la liste **[!UICONTROL Affecter à.]**

1. Entrez une description, la priorité et la date d’échéance de la tâche de révision.

   ![task_details-collection](assets/task_details-collection.png)

1. Cliquez sur **[!UICONTROL Envoyer]**, puis sur **[!UICONTROL Terminé]** pour fermer le message de confirmation. Une notification pour la nouvelle tâche est envoyée à l’approbateur.
1. Connectez-vous à [!DNL Assets] en tant qu’approbateur et accédez à la console [!DNL Assets]. Pour approuver des ressources, cliquez sur **[!UICONTROL Notifications]**, puis sélectionnez la tâche de révision dans la liste.
1. Sur la page **[!UICONTROL Tâche de révision]**, examinez les détails de la tâche de révision, puis cliquez sur **[!UICONTROL Réviser]**.
1. Toutes les ressources situées dans la collection sont visibles dans le panneau de révision. Sélectionnez les ressources, puis cliquez sur **[!UICONTROL Approuver/Rejeter]** pour approuver ou rejeter les ressources, selon les besoins.

   ![review_task_collection](assets/review_task_collection.png)

1. Cliquez sur **[!UICONTROL Terminé]** dans la barre d’outils. Dans la boîte de dialogue, saisissez un commentaire, puis cliquez sur **[!UICONTROL Terminé]** pour confirmer.
1. Accédez à la console Collections et ouvrez la collection. Les icônes d’état d’approbation des ressources s’affichent en mode Carte et Liste.

   ![collection_reviewstatuscardview](assets/collection_reviewstatuscardview.png)

   *Image : mode Carte.*

   ![collection_reviewstatuslistview](assets/collection_reviewstatuslistview.png)

   *Image : vue Liste.*
