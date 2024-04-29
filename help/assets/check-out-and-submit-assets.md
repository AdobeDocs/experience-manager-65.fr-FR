---
title: Archivage et extraction de fichiers dans  [!DNL Assets]
description: Découvrez comment extraire les ressources pour modification et les archiver à nouveau une fois les modifications effectuées.
contentOwner: AG
role: User
feature: Asset Management
exl-id: 544ef73c-4e4b-433f-a173-fdf1c8f45d8e
hide: true
solution: Experience Manager, Experience Manager Assets
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: ht
source-wordcount: '433'
ht-degree: 100%

---

# Archivage et extraction de fichiers dans la gestion des ressources numériques [!DNL Experience Manager] {#check-in-and-check-out-files-in-assets}

| Version | Lien de l’article |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Cliquez ici](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/manage/check-out-and-submit-assets.html?lang=fr) |
| AEM 6.5 | Cet article |

[!DNL Adobe Experience Manager Assets] permet d’extraire des ressources pour les modifier et de les ré-archiver après y avoir apporté les modifications. Après avoir extrait une ressource, vous seul pouvez la modifier, l’annoter, la publier, la déplacer ou la supprimer. Le fait d’extraire une ressource entraîne son verrouillage. Les autres utilisateurs ne peuvent effectuer aucune de ces opérations sur la ressource tant que vous ne l’avez pas archivée dans [!DNL Assets]. Toutefois, ils peuvent modifier les métadonnées de la ressource verrouillée.

Vous avez besoin d’un accès en écriture à ces ressources pour être en mesure de les extraire ou de les archiver.

Cette caractéristique permet d’empêcher les autres utilisateurs d’écraser les modifications apportées par un auteur lorsque plusieurs utilisateurs issus de plusieurs équipes collaborent à la modification des workflows.

## Extraction de ressources {#checking-out-assets}

1. Dans l’interface utilisateur d’[!DNL Assets], sélectionnez la ressource que vous souhaitez extraire. Vous pouvez également sélectionner plusieurs ressources à extraire.
1. Dans la barre d’outils, cliquez sur **[!UICONTROL Extraction]**. L’option **[!UICONTROL Extraction]** passe en **[!UICONTROL Archivage]**.
Pour vérifier si d’autres utilisateurs peuvent modifier la ressource que vous avez extraite, connectez-vous comme un utilisateur différent. Un symbole représentant un verrou s’affiche sur la miniature de la ressource que vous avez extraite.

   ![chlimage_1-471](assets/chlimage_1-471.png)

   Sélectionnez la ressource. Notez que la barre d’outils n’affiche aucune option vous permettant de modifier, d’annoter, de publier ou de supprimer la ressource.

   ![chlimage_1-472](assets/chlimage_1-472.png)

   Pour modifier les métadonnées de la ressource verrouillée, cliquez sur **[!UICONTROL Afficher les propriétés]**.

1. Cliquez sur **[!UICONTROL Modifier]** pour ouvrir la ressource en mode d’édition.

   ![chlimage_1-473](assets/chlimage_1-473.png)

1. Modifiez la ressource et enregistrez les modifications. Par exemple, recadrez l’image et enregistrez-la.

   ![chlimage_1-474](assets/chlimage_1-474.png)

   Vous pouvez également choisir d’annoter ou de publier la ressource.

1. Sélectionnez la ressource modifiée dans l’interface [!DNL Assets], puis cliquez sur **[!UICONTROL Archiver]** dans la barre d’outils. La ressource modifiée est archivée dans [!DNL Assets] et peut être modifiée par les autres utilisateurs.

## Archivage forcé {#forced-check-in}

Les administrateurs peuvent archiver les ressources extraites par d’autres utilisateurs.

1. Connectez-vous à [!DNL Assets] en tant qu’administrateur.
1. Dans l’interface utilisateur d’[!DNL Assets], sélectionnez une ou plusieurs ressources extraites par d’autres utilisateurs.

   ![chlimage_1-476](assets/chlimage_1-476.png)

1. Dans la barre d’outils, cliquez sur **[!UICONTROL Verrouillage de version]**. La ressource est à nouveau archivée et disponible pour modification pour d’autres utilisateurs.

## Bonnes pratiques et restrictions {#tips-limitations}

* Il est possible de supprimer un *dossier* contenant des fichiers de ressources extraits. Avant de supprimer un dossier, assurez-vous qu’aucune ressource numérique n’ait été extraite par les utilisateurs.

>[!MORELIKETHIS]
>
>* [Présentation de l’archivage et de l’extraction dans l’appli de bureau [!DNL Experience Manager]  ](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html?lang=fr#how-app-works2)
>* [Tutoriel vidéo pour comprendre l’archivage et l’extraction [!DNL Assets]](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/collaboration/check-in-and-check-out.html?lang=fr)
