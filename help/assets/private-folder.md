---
title: Dossier privé dans [!DNL Adobe Experience Manager Assets]
description: Learn how to create a private folder in the [!DNL Adobe Experience Manager Assets] and share it with other users and the assign various privileges to them.
contentOwner: AG
translation-type: tm+mt
source-git-commit: b676f73a800c45be12de70b8ba57a332563a49a4
workflow-type: tm+mt
source-wordcount: '642'
ht-degree: 25%

---


# Dossier privé dans [!DNL Adobe Experience Manager Assets] {#private-folder}

You can create a private folder in the [!DNL Adobe Experience Manager Assets] user interface that is available exclusively to you. Vous pouvez partager ce dossier privé avec d’autres utilisateurs et leur attribuer divers privilèges. Selon le niveau de privilège que vous affectez, les utilisateurs peuvent effectuer différentes tâches dans le dossier, par exemple consulter des ressources du dossier ou les modifier.

>[!NOTE]
>
>Le dossier privé comporte au moins un membre doté du rôle Propriétaire.

## Création et partage de dossiers privés {#create-share-private-folder}

Pour créer et partager un dossier privé :

1. In the [!DNL Assets] console, click **[!UICONTROL Create]** from the toolbar and then choose **[!UICONTROL Folder]** from the menu.

   ![Créer un dossier de fichiers](assets/Create-folder.png)

1. In the **[!UICONTROL Create Folder]** dialog, enter a title and name (optional) for the folder, and select **[!UICONTROL Private]** option.

1. Cliquez sur **[!UICONTROL Créer]**. Un dossier privé est créé.

   ![chlimage_1-413](assets/chlimage_1-413.png)

1. To share the folder with other users and the assign privileges to them, select the folder, and click **[!UICONTROL Properties]** from the toolbar.

   ![option info](assets/do-not-localize/info-circle-icon.png)

   >[!NOTE]
   >
   >Le dossier n’est pas visible par les autres utilisateurs tant qu’il n’est pas partagé.

1. In the **[!UICONTROL Folder Properties]** page, select a user from the **[!UICONTROL Add User]** list, assign a role to the user on your private folder, and click **[!UICONTROL Add]**.

   ![chlimage_1-415](assets/chlimage_1-415.png)

   >[!NOTE]
   >
   >Vous pouvez affecter différents rôles (tels que Éditeur, Propriétaire ou Observateur) à l’utilisateur avec lequel vous partagez le dossier. Si vous attribuez un rôle Propriétaire à l’utilisateur, l’utilisateur possède des privilèges Éditeur sur le dossier. En outre, il peut partager le dossier avec d’autres utilisateurs. Si vous affectez le rôle Éditeur, l’utilisateur peut modifier les ressources situées dans votre dossier privé. Si vous attribuez un rôle de lecteur de contenu, l’utilisateur peut uniquement vue les fichiers de votre dossier privé.

   >[!NOTE]
   >
   >Le dossier privé comporte au moins un membre doté du rôle Propriétaire. Par conséquent, l’administrateur ne peut pas supprimer tous les membres propriétaires d’un dossier privé. Toutefois, pour supprimer les propriétaires existants (et l’administrateur lui-même) du dossier privé, l’administrateur doit ajouter un autre utilisateur en tant que propriétaire.

1. Cliquez sur **[!UICONTROL Enregistrer]**. Depending on the role you assign, the user is assigned a set of privileges on your private folder when the user logs in to [!DNL Assets].
1. Cliquez sur **[!UICONTROL OK]** pour fermer le message de confirmation.
1. L’utilisateur avec lequel vous partagez le dossier reçoit une notification de partage. Log in to [!DNL Assets] with the credentials of the user to view the notification.

   ![chlimage_1-416](assets/chlimage_1-416.png)

1. Cliquez sur Notifications pour ouvrir la liste des notifications.

   ![Liste des notifications](assets/Assets-Notification.png)

1. Cliquez sur l’entrée correspondant au dossier privé partagé par l’administrateur pour ouvrir le dossier.

>[!NOTE]
>
>Pour créer un dossier privé, vous devez disposer des autorisations de lecture et de modification de l’ACL sur le dossier parent sous lequel vous souhaitez créer un dossier privé. Si vous n’êtes pas administrateur, ces autorisations ne sont pas activées pour vous par défaut au niveau de `/content/dam`. Dans ce cas, commencez par obtenir ces autorisations pour votre ID utilisateur/groupe avant d’essayer de créer des dossiers privés ou d’afficher les paramètres de dossier.

## Suppression de dossiers privés {#delete-private-folder}

Vous pouvez supprimer un dossier privé en le sélectionnant et en sélectionnant l’option [!UICONTROL Supprimer] dans le menu supérieur ou en utilisant la touche Retour arrière de votre clavier.

### Suppression d’un groupe d’utilisateurs lors de la suppression d’un dossier {#group-removal-on-folder-deletion}

Si vous supprimez un dossier privé à l’aide de la méthode ci-dessus de l’interface utilisateur, les groupes d’utilisateurs associés sont également supprimés. Toutefois, les groupes d’utilisateurs redondants, inutilisés et générés automatiquement existants peuvent être supprimés du référentiel à l’aide de [JMX](#group-clean-up-jmx).

>[!CAUTION]
>
>Si vous supprimez un dossier privé du CRXDE Lite, les groupes d’utilisateurs redondants restent dans le référentiel.

### Utiliser JMX pour nettoyer les groupes d’utilisateurs inutilisés {#group-clean-up-jmx}

Pour nettoyer le référentiel des groupes d’utilisateurs inutilisés :

1. Ouvrez le JMX pour nettoyer les groupes redondants des ressources `http://[server]:[port]/system/console/jmx/com.day.cq.dam.core.impl.team%3Atype%3DClean+redundant+groups+for+Assets`.

1. Appelez la `clean` méthode à partir de ce JMX.

Vous pouvez constater que tous les groupes d’utilisateurs redondants ou les groupes générés automatiquement (créés lors de la création d’un dossier privé portant le même nom qu’un groupe précédemment supprimé) sont supprimés du chemin d’accès `/home/groups/mac/default/<user_name>/<folder_name>`.
