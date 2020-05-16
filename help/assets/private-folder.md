---
title: Création et partage d’un dossier privé dans AEM
description: Apprenez à créer un dossier privé dans Adobe Experience Manager (AEM) Assets, à le partager avec d’autres utilisateurs et à attribuer à ces derniers différents privilèges.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 979d5074fcf94ca999fd941c77038ab6305cc67d
workflow-type: tm+mt
source-wordcount: '511'
ht-degree: 74%

---


# Partage de dossiers privés {#private-folder-sharing}

Vous pouvez créer dans l’interface utilisateur d’Adobe Experience Manager (AEM) Assets un dossier privé qui n’est disponible que pour vous. Vous pouvez partager ce dossier privé avec d’autres utilisateurs et leur attribuer divers privilèges. Selon le niveau de privilège que vous affectez, les utilisateurs peuvent effectuer différentes tâches dans le dossier, par exemple consulter des ressources du dossier ou les modifier.

>[!NOTE]
>
> Le dossier privé comporte toujours au moins un membre doté du rôle Propriétaire.


1. Dans la console Ressources, appuyez ou cliquez sur **[!UICONTROL Créer]** dans la barre d’outils, puis choisissez **[!UICONTROL Dossier]** dans le menu.

   ![Créer un dossier de fichiers](assets/Create-folder.png)

1. In the **[!UICONTROL Create Folder]** dialog, enter a title and name (optional) for the folder, and select **[!UICONTROL Private]**.

   ![Cochez la case Privé pour rendre le dossier privé.](assets/private-folder.png)

1. Cliquez/appuyez sur **[!UICONTROL Créer]**. Un dossier privé est alors créé dans l’interface utilisateur.

   ![chlimage_1-413](assets/chlimage_1-413.png)

1. Pour partager le dossier avec d’autres utilisateurs et leur attribuer des privilèges, sélectionnez le dossier, puis cliquez/appuyez sur l’icône **[!UICONTROL Propriétés]** de la barre d’outils.

   ![chlimage_1-414](assets/chlimage_1-414.png)

   >[!NOTE]
   >
   >Le dossier n’est pas visible par les autres utilisateurs tant qu’il n’est pas partagé.

1. In the **[!UICONTROL Folder Properties]** page, select a user from the **[!UICONTROL Add User]** list, assign a role to the user on your private folder, and click **[!UICONTROL Add]**.

   ![chlimage_1-415](assets/chlimage_1-415.png)

   >[!NOTE]
   >
   >Vous pouvez affecter différents rôles (tels que Éditeur, Propriétaire ou Observateur) à l’utilisateur avec lequel vous partagez le dossier. Si vous attribuez un rôle Propriétaire à l’utilisateur, l’utilisateur possède des privilèges Éditeur sur le dossier. En outre, il peut partager le dossier avec d’autres utilisateurs. Si vous affectez le rôle Éditeur, l’utilisateur peut modifier les ressources situées dans votre dossier privé. Si vous affectez le rôle Observateur, l’utilisateur ne peut que consulter les ressources du dossier privé.

   >[!NOTE]
   >
   > Le dossier privé comporte toujours au moins un membre doté du rôle Propriétaire. Par conséquent, l’administrateur ne peut pas supprimer tous les membres propriétaires d’un dossier privé. Toutefois, pour supprimer les propriétaires existants de l’administrateur de dossier privé, vous devez ajouter un autre utilisateur en tant que propriétaire.

1. Cliquez sur **[!UICONTROL Enregistrer]**. En fonction du rôle affecté, l’utilisateur se voit attribuer un ensemble de privilèges sur votre dossier privé lorsqu’il se connecte à AEM Assets.
1. Cliquez sur **[!UICONTROL OK]** pour fermer le message de confirmation.
1. L’utilisateur avec lequel vous partagez le dossier reçoit une notification de partage. Connectez-vous à AEM Assets à l’aide des informations d’identification de l’utilisateur pour afficher la notification.

   ![chlimage_1-416](assets/chlimage_1-416.png)

1. Cliquez ou appuyez sur l’icône Notification pour ouvrir la liste des notifications.

   ![Liste des notifications](assets/Assets-Notification.png)

1. Cliquez/appuyez sur l’entrée du dossier privé partagé par l’administrateur pour ouvrir le dossier.

>[!NOTE]
>
>Pour pouvoir créer un dossier privé, vous devez disposer d’autorisations ACL en lecture et en modification au niveau du dossier parent dans lequel vous souhaitez créer un dossier privé. Si vous n’êtes pas administrateur, ces autorisations ne sont pas activées pour vous par défaut au niveau de `/content/dam`. Dans ce cas, commencez par obtenir ces autorisations pour votre ID utilisateur/groupe avant d’essayer de créer des dossiers privés ou d’afficher les paramètres de dossier.
