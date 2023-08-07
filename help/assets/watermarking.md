---
title: Ajout d’un filigrane à vos ressources numériques
description: Découvrez comment utiliser la fonctionnalité d’application d’un filigrane pour ajouter un filigrane numérique aux ressources.
contentOwner: AG
role: User, Admin
feature: Asset Management
exl-id: bc0cfb0e-3f70-4377-8831-326a7cae73bd
hide: true
source-git-commit: 3d5e9ad8ee19756b05e5a77a3f748bc647fcf734
workflow-type: ht
source-wordcount: '328'
ht-degree: 100%

---

# Ajoutez un filigrane à vos ressources numériques. {#watermarking}

| Version | Lien de l’article |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Cliquez ici](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/manage/watermark-assets.html?lang=fr) |
| AEM 6.5 | Cet article |

[!DNL Adobe Experience Manager Assets] vous permet d’ajouter un filigrane numérique aux ressources pour vérifier l’authenticité et la propriété des droits d’auteur de ces ressources. [!DNL Experience Manager Assets] prend en charge le texte à utiliser comme filigrane dans les fichiers PNG et JPEG.

Pour appliquer le filigrane sur les ressources, ajoutez l’étape d’ajout d’un filigrane dans le workflow [!UICONTROL Ressource de mise à jour de gestion des ressources numériques].

1. Accédez à l’interface utilisateur d’[!DNL Experience Manager], puis accédez à **[!UICONTROL Outils]** > **[!UICONTROL Workflow]** > **[!UICONTROL Modèles]**.
1. Dans la page **[!UICONTROL Modèles de workflows]**, sélectionnez le workflow **[!UICONTROL Ressource de mise à jour de gestion des ressources numériques]**, puis cliquez sur **[!UICONTROL Modifier]**.

1. Dans le panneau latéral, faites glisser l’étape **[!UICONTROL Ajouter un filigrane]** dans le workflow [!UICONTROL Ressources de mise à jour de gestion des ressources numériques].

   ![Faites glisser l’étape [!UICONTROL Ajouter un filigrane] et ajoutez-la au workflow [!UICONTROL Ressource de mise à jour de gestion des ressources numériques]](assets/add_watermark_step_aem_assets.png).

   *Image : faites glisser l’étape [!UICONTROL Ajouter un filigrane] et ajoutez-la au workflow [!UICONTROL Ressource de mise à jour de gestion des ressources numériques]*..

   >[!NOTE]
   >
   >Placez l’étape [!UICONTROL Ajouter un filigrane] n’importe où avant l’étape [!UICONTROL Traitement de la miniature].

1. Ouvrez l’étape **[!UICONTROL Ajouter un filigrane]** pour afficher ses propriétés.
1. Dans l’onglet **[!UICONTROL Arguments]**, spécifiez des valeurs valides dans les différents champs, notamment le texte, le type de police, la taille, la couleur, la position, l’orientation, etc. Pour confirmer les modifications, cliquez sur **[!UICONTROL Terminé]**.

   ![Indiquer les arguments dans l’étape Ajouter un filigrane dans [!DNL Assets]](assets/arguments_add_watermark_aem_assets.png)

   *Image : indiquez les arguments dans l’étape Ajouter un filigrane dans [!DNL Assets].*

1. Enregistrez le workflow **[!UICONTROL Ressource de mise à jour de gestion des ressources numériques]** avec l’étape Ajout d’un filigrane.
1. Dans l’interface utilisateur d’[!DNL Assets], téléchargez un exemple de ressource. Le filigrane apparaît avec la taille de police, la couleur, etc., à l’emplacement configuré aux étapes ci-dessus.

Pour ajouter un filigrane à des documents PDF par programmation ou avec des informations dynamiques, pensez à utiliser les outils d’[Experience Manager Document Services](/help/forms/using/overview-aem-document-services.md).

## Conseils et restrictions {#tips-limitations}

* Seuls les filigranes basés sur du texte sont pris en charge. Des images ne peuvent pas être utilisées comme des filigranes, même si vous pouvez charger des images lors de la création du [!UICONTROL Processus d’ajout d’un filigrane].
* Seuls les fichiers PNG et JPEG sont pris en charge pour recevoir un filigrane. Les autres formats de ressource n’accepteront pas l’ajout d’un filigrane.
