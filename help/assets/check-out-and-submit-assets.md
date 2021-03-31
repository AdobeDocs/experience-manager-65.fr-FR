---
title: Archiver et extraire des fichiers dans  [!DNL Assets]
description: Découvrez comment extraire les ressources pour modification et les archiver à nouveau une fois les modifications effectuées.
contentOwner: AG
role: Professionnel
feature: Gestion des ressources
translation-type: tm+mt
source-git-commit: ad0672c345262712e51e821fa4e050b505063ac4
workflow-type: tm+mt
source-wordcount: '431'
ht-degree: 50%

---


# Fichiers d&#39;arrivée et de départ dans [!DNL Experience Manager] DAM {#check-in-and-check-out-files-in-assets}

[!DNL Adobe Experience Manager Assets] permet d’extraire des ressources pour les modifier et de les ré-archiver après y avoir apporté les modifications. Après avoir extrait une ressource, vous seul pouvez la modifier, l’annoter, la publier, la déplacer ou la supprimer. Le fait d’extraire une ressource entraîne son verrouillage. Les autres utilisateurs ne peuvent pas effectuer l’une de ces opérations sur la ressource tant que vous n’avez pas réactivé la ressource dans [!DNL Assets]. Toutefois, ils peuvent modifier les métadonnées de la ressource verrouillée.

Vous avez besoin d’un accès en écriture à ces ressources pour être en mesure de les extraire ou de les archiver.

Cette caractéristique permet d’empêcher les autres utilisateurs d’écraser les modifications apportées par un auteur lorsque plusieurs utilisateurs issus de plusieurs équipes collaborent à la modification des workflows.

## Extraire les ressources {#checking-out-assets}

1. Dans l&#39;interface utilisateur [!DNL Assets], sélectionnez la ressource à extraire. Vous pouvez également sélectionner plusieurs ressources à extraire.
1. Dans la barre d’outils, cliquez sur **[!UICONTROL Passage en caisse]**. L&#39;option **[!UICONTROL Passage en caisse]** passe à **[!UICONTROL Passage en caisse]**.
Pour vérifier si d’autres utilisateurs peuvent modifier la ressource que vous avez extraite, connectez-vous comme un utilisateur différent. Un symbole de verrou s’affiche sur la miniature de la ressource que vous avez récupérée.

   ![chlimage_1-471](assets/chlimage_1-471.png)

   Sélectionnez la ressource. Notez que la barre d’outils n’affiche aucune option permettant de modifier, d’annoter, de publier ou de supprimer la ressource.

   ![chlimage_1-472](assets/chlimage_1-472.png)

   Pour modifier les métadonnées du fichier verrouillé, cliquez sur **[!UICONTROL Propriétés de la Vue]**.

1. Cliquez sur **[!UICONTROL Modifier]** pour ouvrir la ressource en mode d’édition.

   ![chlimage_1-473](assets/chlimage_1-473.png)

1. Modifiez la ressource et enregistrez les modifications. Par exemple, recadrez l’image et enregistrez-la.

   ![chlimage_1-474](assets/chlimage_1-474.png)

   Vous pouvez également choisir d’annoter ou de publier la ressource.

1. Sélectionnez le fichier modifié dans l&#39;interface [!DNL Assets], puis cliquez sur **[!UICONTROL Archiver]** dans la barre d&#39;outils. L’actif modifié est archivé dans [!DNL Assets] et est disponible pour modification pour d’autres utilisateurs.

## Archivage forcé {#forced-check-in}

Les administrateurs peuvent archiver les ressources extraites par d’autres utilisateurs.

1. Connectez-vous à [!DNL Assets] en tant qu’administrateur.
1. Dans l&#39;interface utilisateur [!DNL Assets], sélectionnez une ou plusieurs ressources qui ont été extraites par d&#39;autres utilisateurs.

   ![chlimage_1-476](assets/chlimage_1-476.png)

1. Dans la barre d’outils, cliquez sur **[!UICONTROL Verrouiller]**. La ressource est à nouveau archivée et disponible pour modification pour d’autres utilisateurs.

## Bonnes pratiques et restrictions {#tips-limitations}

* Il est possible de supprimer un *dossier* contenant des fichiers extraits. Avant de supprimer un dossier, assurez-vous qu’aucun fichier numérique n’est extrait par les utilisateurs.

>[!MORELIKETHIS]
>
>* [Comprendre l&#39;archivage et l&#39;extraction  [!DNL Experience Manager] dans l&#39;application de bureau](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html?lang=en#how-app-works2)
>* [Didacticiel vidéo pour comprendre la procédure d&#39;enregistrement et de départ [!DNL Assets]](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/collaboration/check-in-and-check-out.html)

