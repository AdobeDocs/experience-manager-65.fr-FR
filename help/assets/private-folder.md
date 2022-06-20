---
title: Dossiers privés pour le partage de ressources
description: Apprenez à créer un dossier privé dans [!DNL Adobe Experience Manager Assets] , à partager avec d’autres utilisateurs et à attribuer à ces derniers différents privilèges.
contentOwner: AG
role: User
feature: Collaboration
exl-id: c1aece06-7c1c-43a0-bea0-6f11ecda7e68
source-git-commit: 068f6c1c2909c2840e9ad4c0ad295538e543d9c9
workflow-type: tm+mt
source-wordcount: '607'
ht-degree: 71%

---

# Dossier privé dans [!DNL Adobe Experience Manager Assets] {#private-folder}

| Version | Lien de l’article |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Cliquez ici.](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/manage/private-folder.html?lang=en) |
| AEM 6.5 | Cet article |
| AEM 6.4 | [Cliquez ici.](https://experienceleague.adobe.com/docs/experience-manager-64/assets/managing/private-folder.html?lang=en) |

Vous pouvez créer un dossier privé dans l’interface utilisateur d’[!DNL Adobe Experience Manager Assets] qui n’est disponible que pour vous. Vous pouvez partager ce dossier privé avec d’autres utilisateurs auxquels vous attribuez différents privilèges. Selon le niveau de privilège que vous attribuez, les utilisateurs peuvent effectuer différentes tâches dans le dossier, par exemple consulter des ressources du dossier ou les modifier.

>[!NOTE]
>
>Le dossier privé comporte au moins un membre ayant un rôle Propriétaire.

## Création et partage de dossiers privés {#create-share-private-folder}

Pour créer et partager un dossier privé :

1. Dans le [!DNL Assets] console, cliquez sur **[!UICONTROL Créer]** dans la barre d’outils, puis choisissez **[!UICONTROL Dossier]** dans le menu.

   ![Créer un dossier de ressources](assets/Create-folder.png)

1. Dans le **[!UICONTROL Créer un dossier]** , saisissez un titre et un nom (facultatif) pour le dossier, puis sélectionnez **[!UICONTROL Privé]** .

1. Cliquez sur **[!UICONTROL Créer]**. Un dossier privé est créé.

   ![chlimage_1-413](assets/chlimage_1-413.png)

1. Pour partager le dossier avec d’autres utilisateurs et leur attribuer des privilèges, sélectionnez le dossier, puis cliquez sur **[!UICONTROL Propriétés]** dans la barre d’outils.

   ![option info](assets/do-not-localize/info-circle-icon.png)

   >[!NOTE]
   >
   >Le dossier n’est pas visible par les autres utilisateurs tant qu’il n’est pas partagé.

1. Dans le **[!UICONTROL Propriétés du dossier]** , sélectionnez un utilisateur dans la **[!UICONTROL Ajouter un utilisateur]** , attribuez un rôle à l’utilisateur dans votre dossier privé, puis cliquez sur **[!UICONTROL Ajouter]**.

   ![chlimage_1-415](assets/chlimage_1-415.png)

   >[!NOTE]
   >
   >Vous pouvez affecter différents rôles, tels que `Editor`, `Owner`, ou `Viewer`, à l’utilisateur avec lequel vous partagez le dossier. Si vous attribuez un rôle `Owner` à l’utilisateur, ce dernier possède des privilèges `Editor` sur le dossier. En outre, il peut partager le dossier avec d’autres utilisateurs. Si vous attribuez le rôle `Editor`, l’utilisateur peut modifier les ressources de votre dossier privé. Si vous affectez le rôle Observateur, l’utilisateur peut uniquement consulter les ressources du dossier privé.

   >[!NOTE]
   >
   >Le dossier privé comporte au moins un membre ayant le rôle `Owner`. Par conséquent, l’administrateur ne peut pas supprimer tous les membres propriétaires d’un dossier privé. Toutefois, pour supprimer les propriétaires existants (et l’administrateur lui-même) du dossier privé, l’administrateur doit ajouter un autre utilisateur en tant que propriétaire.

1. Cliquez sur **[!UICONTROL Enregistrer]**. En fonction du rôle attribué, l’utilisateur se voit attribuer un ensemble de privilèges sur votre dossier privé lorsqu’il se connecte à [!DNL Assets].
1. Cliquez sur **[!UICONTROL OK]** pour fermer le message de confirmation.
1. L’utilisateur avec lequel vous partagez le dossier reçoit une notification de partage. Connectez-vous à [!DNL Assets] avec les informations d’identification de l’utilisateur pour afficher la notification.

   ![chlimage_1-416](assets/chlimage_1-416.png)

1. Cliquez sur [!UICONTROL Notifications] pour ouvrir une liste de notifications.

   ![Liste des notifications](assets/Assets-Notification.png)

1. Cliquez sur l’entrée du dossier privé partagé par l’administrateur pour ouvrir le dossier.

>[!NOTE]
>
>Pour créer un dossier privé, vous devez procéder à la lecture et à la modification [autorisations de contrôle d’accès](/help/sites-administering/security.md#permissions-in-aem) dans le dossier parent sous lequel vous souhaitez créer un dossier privé. Si vous n’êtes pas administrateur, ces autorisations ne sont pas activées pour vous par défaut au niveau de `/content/dam`. Dans ce cas, commencez par obtenir ces autorisations pour votre ID utilisateur/groupe avant d’essayer de créer des dossiers privés ou d’afficher les paramètres de dossier.

## Suppression de dossiers privés {#delete-private-folder}

Vous pouvez supprimer un dossier en le sélectionnant et en sélectionnant [!UICONTROL Supprimer] à partir du menu supérieur ou à l’aide de la touche Retour arrière de votre clavier.

![option de suppression dans le menu supérieur](assets/delete-option.png)

>[!CAUTION]
>
>Si vous supprimez un dossier privé de CRXDE Lite, les groupes d’utilisateurs redondants restent dans le référentiel.

>[!NOTE]
>
>Si vous supprimez un dossier de l’interface utilisateur à l’aide de la méthode ci-dessus, les groupes d’utilisateurs associés sont également supprimés.
>
>Cependant, les groupes d’utilisateurs existants redondants, inutilisés et générés automatiquement peuvent être supprimés du référentiel à l’aide de la méthode `clean` dans JMX dans l’instance de création (`http://[server]:[port]/system/console/jmx/com.day.cq.dam.core.impl.team%3Atype%3DClean+redundant+groups+for+Assets`).
