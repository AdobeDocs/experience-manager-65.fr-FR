---
title: Dossiers privés pour le partage de ressources
description: Découvrez comment créer un dossier privé dans  [!DNL Adobe Experience Manager Assets] et le partager avec d’autres utilisateurs et leur attribuer divers privilèges.
contentOwner: AG
role: Business Practitioner
feature: Collaboration
exl-id: c1aece06-7c1c-43a0-bea0-6f11ecda7e68
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '573'
ht-degree: 15%

---

# Dossier privé dans [!DNL Adobe Experience Manager Assets] {#private-folder}

Vous pouvez créer dans l’interface utilisateur [!DNL Adobe Experience Manager Assets] un dossier privé qui vous est exclusivement accessible. Vous pouvez partager ce dossier privé avec d’autres utilisateurs et leur attribuer divers privilèges. Selon le niveau de privilège que vous affectez, les utilisateurs peuvent effectuer différentes tâches dans le dossier, par exemple consulter des ressources du dossier ou les modifier.

>[!NOTE]
>
>Le dossier privé comporte au moins un membre avec le rôle Propriétaire.

## Création et partage de dossiers privés {#create-share-private-folder}

Pour créer et partager un dossier privé :

1. Dans la console [!DNL Assets], cliquez sur **[!UICONTROL Créer]** dans la barre d’outils, puis sélectionnez **[!UICONTROL Dossier]** dans le menu.

   ![Création d’un dossier de ressources](assets/Create-folder.png)

1. Dans la boîte de dialogue **[!UICONTROL Créer un dossier]**, saisissez un titre et un nom (facultatif) pour le dossier, puis sélectionnez l’option **[!UICONTROL Privé]** .

1. Cliquez sur **[!UICONTROL Créer]**. Un dossier privé est créé.

   ![chlimage_1-413](assets/chlimage_1-413.png)

1. Pour partager le dossier avec d’autres utilisateurs et leur attribuer des privilèges, sélectionnez le dossier, puis cliquez sur **[!UICONTROL Propriétés]** dans la barre d’outils.

   ![option info](assets/do-not-localize/info-circle-icon.png)

   >[!NOTE]
   >
   >Le dossier n’est pas visible par les autres utilisateurs tant qu’il n’est pas partagé.

1. Sur la page **[!UICONTROL Propriétés du dossier]**, sélectionnez un utilisateur dans la liste **[!UICONTROL Ajouter un utilisateur]**, attribuez un rôle à l’utilisateur dans votre dossier privé, puis cliquez sur **[!UICONTROL Ajouter]**.

   ![chlimage_1-415](assets/chlimage_1-415.png)

   >[!NOTE]
   >
   >Vous pouvez affecter différents rôles, tels que `Editor`, `Owner` ou `Viewer` à l’utilisateur avec lequel vous partagez le dossier. Si vous attribuez un rôle `Owner` à l’utilisateur, celui-ci dispose des privilèges `Editor` sur le dossier. En outre, il peut partager le dossier avec d’autres utilisateurs. Si vous attribuez un rôle `Editor` , l’utilisateur peut modifier les ressources de votre dossier privé. Si vous attribuez un rôle de visionneuse, l’utilisateur ne peut afficher que les ressources de votre dossier privé.

   >[!NOTE]
   >
   >Le dossier privé comporte au moins un membre avec le rôle `Owner` . Par conséquent, l’administrateur ne peut pas supprimer tous les membres propriétaires d’un dossier privé. Toutefois, pour supprimer les propriétaires existants (et l’administrateur lui-même) du dossier privé, l’administrateur doit ajouter un autre utilisateur en tant que propriétaire.

1. Cliquez sur **[!UICONTROL Enregistrer]**. Selon le rôle que vous attribuez, l’utilisateur se voit attribuer un ensemble de privilèges sur votre dossier privé lorsqu’il se connecte à [!DNL Assets].
1. Cliquez sur **[!UICONTROL OK]** pour fermer le message de confirmation.
1. L’utilisateur avec lequel vous partagez le dossier reçoit une notification de partage. Connectez-vous à [!DNL Assets] avec les informations d’identification de l’utilisateur pour afficher la notification.

   ![chlimage_1-416](assets/chlimage_1-416.png)

1. Cliquez sur [!UICONTROL Notifications] pour ouvrir une liste de notifications.

   ![Liste des notifications](assets/Assets-Notification.png)

1. Cliquez sur l’entrée du dossier privé partagé par l’administrateur pour ouvrir le dossier.

>[!NOTE]
>
>Pour créer un dossier privé, vous devez disposer des autorisations de lecture et de modification [du contrôle d’accès](/help/sites-administering/security.md#permissions-in-aem) sur le dossier parent sous lequel vous souhaitez créer un dossier privé. Si vous n’êtes pas administrateur, ces autorisations ne sont pas activées pour vous par défaut au niveau de `/content/dam`. Dans ce cas, vous devez d’abord obtenir ces autorisations pour votre identifiant utilisateur/groupe avant de tenter de créer des dossiers privés.

## Suppression de dossiers privés {#delete-private-folder}

Vous pouvez supprimer un dossier en le sélectionnant et en sélectionnant l’option [!UICONTROL Supprimer] dans le menu supérieur, ou en utilisant la touche Retour arrière de votre clavier.

![option de suppression dans le menu supérieur](assets/delete-option.png)

>[!CAUTION]
>
>Si vous supprimez un dossier privé de CRXDE Lite, les groupes d’utilisateurs redondants restent dans le référentiel.

>[!NOTE]
>
>Si vous supprimez un dossier à l’aide de la méthode ci-dessus de l’interface utilisateur, les groupes d’utilisateurs associés sont également supprimés.
>
>Cependant, les groupes d’utilisateurs redondants, inutilisés et générés automatiquement existants peuvent être supprimés du référentiel à l’aide de la méthode `clean` dans JMX dans l’instance d’auteur (`http://[server]:[port]/system/console/jmx/com.day.cq.dam.core.impl.team%3Atype%3DClean+redundant+groups+for+Assets`).
