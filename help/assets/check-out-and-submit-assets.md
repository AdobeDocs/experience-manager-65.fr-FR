---
title: Archivez et extrayez vos ressources numériques pour les modifier.
description: Découvrez comment extraire les ressources pour modification et les archiver à nouveau une fois les modifications effectuées.
contentOwner: AG
translation-type: tm+mt
source-git-commit: ee94193ff31c60e954be0070ecf84e447effc4f6
workflow-type: tm+mt
source-wordcount: '437'
ht-degree: 51%

---


# Check-in and check-out files in [!DNL Experience Manager] DAM {#check-in-and-check-out-files-in-assets}

[!DNL Adobe Experience Manager Assets] permet d’extraire des ressources pour les modifier et de les ré-archiver après y avoir apporté les modifications. Après avoir extrait une ressource, vous seul pouvez la modifier, l’annoter, la publier, la déplacer ou la supprimer. Le fait d’extraire une ressource entraîne son verrouillage. Other users cannot perform any of these operations on the asset until you check the asset back in to [!DNL Assets]. Toutefois, ils peuvent modifier les métadonnées de la ressource verrouillée.

Vous avez besoin d’un accès en écriture à ces ressources pour être en mesure de les extraire ou de les archiver.

Cette caractéristique permet d’empêcher les autres utilisateurs d’écraser les modifications apportées par un auteur lorsque plusieurs utilisateurs issus de plusieurs équipes collaborent à la modification des workflows.

## Extraire les fichiers {#checking-out-assets}

1. From the [!DNL Assets] user interface, select the asset you want to check out. Vous pouvez également sélectionner plusieurs ressources à extraire.
1. Dans la barre d&#39;outils, cliquez sur **[!UICONTROL Passage en caisse]**.
L&#39;option **[!UICONTROL Passage en caisse]** bascule vers **[!UICONTROL Archivage]**.
Pour vérifier si d’autres utilisateurs peuvent modifier la ressource que vous avez extraite, connectez-vous comme un utilisateur différent. Un symbole de verrou s’affiche sur la miniature de la ressource que vous avez récupérée.

   ![chlimage_1-471](assets/chlimage_1-471.png)

   Sélectionnez la ressource. Notez que la barre d’outils n’affiche aucune option permettant de modifier, d’annoter, de publier ou de supprimer la ressource.

   ![chlimage_1-472](assets/chlimage_1-472.png)

   You can click **[!UICONTROL View Properties]** to edit the metadata for the locked asset.

1. Cliquez sur **[!UICONTROL Modifier]** pour ouvrir le fichier en mode d’édition.

   ![chlimage_1-473](assets/chlimage_1-473.png)

1. Modifiez la ressource et enregistrez les modifications. Par exemple, recadrez l’image et enregistrez-la.

   ![chlimage_1-474](assets/chlimage_1-474.png)

   Vous pouvez également choisir d’annoter ou de publier la ressource.

1. Sélectionnez le fichier modifié dans l’ [!DNL Assets] interface, puis cliquez sur **[!UICONTROL Archiver]** dans la barre d’outils. The modified asset is checked in to [!DNL Assets] and is available to other users for editing.

## Forced check in {#forced-check-in}

Les administrateurs peuvent archiver les ressources extraites par d’autres utilisateurs.

1. Log in to [!DNL Assets] as an administrator.
1. From the [!DNL Assets] user interface select one or more assets that have been checked out by other users.

   ![chlimage_1-476](assets/chlimage_1-476.png)

1. Dans la barre d’outils, cliquez sur **[!UICONTROL Annuler le verrouillage]**. La ressource est à nouveau archivée et disponible pour modification pour d’autres utilisateurs.

## Bonnes pratiques et restrictions {#tips-limitations}

* Il est possible de supprimer un *dossier* contenant des fichiers extraits. Avant de supprimer un dossier, assurez-vous qu’aucun fichier numérique n’est extrait par les utilisateurs.

>[!MORELIKETHIS]
>
>* [Comprendre l&#39;archivage et l&#39;extraction dans l&#39;application de bureau Experience Manager](https://docs.adobe.com/content/help/en/experience-manager-desktop-app/using/using.html#how-app-works2)
>* [Didacticiel vidéo pour comprendre comment archiver et extraire des ressources](https://docs.adobe.com/content/help/en/experience-manager-learn/assets/collaboration/checkin-checkout-technical-video-understand.html)

