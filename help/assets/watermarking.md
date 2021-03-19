---
title: Ajout d’un filigrane à vos ressources numériques
description: Découvrez comment utiliser la fonctionnalité d’application d’un filigrane pour ajouter un filigrane numérique aux ressources.
contentOwner: AG
role: Professionnel, Administrateur
translation-type: tm+mt
source-git-commit: 2e734041bdad7332c35ab41215069ee696f786f4
workflow-type: tm+mt
source-wordcount: '308'
ht-degree: 31%

---


# Mettre vos ressources numériques en filigrane {#watermarking}

[!DNL Adobe Experience Manager Assets] vous permet d’ajouter un filigrane numérique aux fichiers afin d’aider les utilisateurs à vérifier l’authenticité et la propriété des fichiers sur les droits d’auteur. [!DNL Experience Manager Assets] prend en charge le texte à utiliser comme un filigrane sur les fichiers PNG et JPEG.

Pour pouvoir appliquer un filigrane aux ressources, ajoutez l’étape de filigrane dans le flux de travaux [!UICONTROL DAM Update Asset].

1. Accédez à l&#39;interface utilisateur [!DNL Experience Manager] et accédez à **[!UICONTROL Outils]** > **[!UICONTROL Workflow]** > **[!UICONTROL Modèles]**.
1. Dans la page **[!UICONTROL Modèles de flux de travail]**, sélectionnez le flux de travail **[!UICONTROL DAM Update Asset]** et cliquez sur **[!UICONTROL Modifier]**.

1. Dans le panneau latéral, faites glisser l’étape **[!UICONTROL Ajouter le filigrane]** vers le workflow [!UICONTROL DAM Update Asset].

   ![Faites glisser l’étape  [!UICONTROL Ajouter les ] filigranes et ajoutez-la au processus  [!UICONTROL DAM Update ] Asset.](assets/add_watermark_step_aem_assets.png)

   *Figure : Faites glisser l’étape  [!UICONTROL Ajouter les ] filigranes et ajoutez-la au processus  [!UICONTROL DAM Update ] Asset.*

   >[!NOTE]
   >
   >Placez l’étape [!UICONTROL Ajouter le filigrane] n’importe où avant l’étape [!UICONTROL Traiter la miniature].

1. Ouvrez l’étape **[!UICONTROL Ajouter un filigrane]** pour afficher ses propriétés.
1. Sous l’onglet **[!UICONTROL Arguments]**, spécifiez des valeurs valides dans les différents champs, notamment le texte, le type de police, la taille, la couleur, l’emplacement, l’orientation, etc. Pour confirmer les modifications, cliquez sur **[!UICONTROL Terminé]**.

   ![Indiquer les arguments dans l’étape Ajouter un filigrane dans [!DNL Assets]](assets/arguments_add_watermark_aem_assets.png)

   *Figure : Fournissez les arguments dans l’étape d’ajout de filigrane dans  [!DNL Assets].*

1. Enregistrez le flux de travaux **[!UICONTROL DAM Update Asset]** à l’aide de l’étape du filigrane.
1. Dans l’interface utilisateur [!DNL Assets], téléchargez un exemple de fichier. Le filigrane apparaît avec la taille de police, la couleur, etc., à l’emplacement configuré aux étapes ci-dessus.

Pour mettre en filigrane des documents PDF par programmation ou avec des informations dynamiques, pensez à utiliser l’offre [Experience Manager Document Services](/help/forms/using/overview-aem-document-services.md).

## Conseils et restrictions {#tips-limitations}

* Seuls les filigranes basés sur du texte sont pris en charge. Les images ne sont pas utilisées comme filigranes, même si vous pouvez télécharger des images lors de la création du processus [!UICONTROL Ajouter le filigrane].
* Seuls les fichiers PNG et JPEG sont pris en charge pour être mis en filigrane. Les autres formats de fichier ne sont pas filigrane.
