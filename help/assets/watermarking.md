---
title: Ajout d’un filigrane à vos ressources numériques
description: Découvrez comment utiliser la fonctionnalité d’application d’un filigrane pour ajouter un filigrane numérique aux ressources.
contentOwner: AG
role: User, Admin
feature: Asset Management
exl-id: bc0cfb0e-3f70-4377-8831-326a7cae73bd
source-git-commit: 068f6c1c2909c2840e9ad4c0ad295538e543d9c9
workflow-type: tm+mt
source-wordcount: '340'
ht-degree: 31%

---

# Mise en filigrane de vos ressources numériques {#watermarking}

| Version | Lien de l’article |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Cliquez ici.](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/manage/watermark-assets.html?lang=en) |
| AEM 6.5 | Cet article |
| AEM 6.4 | [Cliquez ici.](https://experienceleague.adobe.com/docs/experience-manager-64/assets/administer/watermarking.html?lang=en) |

[!DNL Adobe Experience Manager Assets] vous permet d’ajouter un filigrane numérique aux ressources, ce qui permet aux utilisateurs de vérifier l’authenticité et la propriété des droits d’auteur des ressources. [!DNL Experience Manager Assets] prend en charge le texte à utiliser comme un filigrane sur les fichiers PNG et JPEG.

Pour appliquer un filigrane aux ressources, ajoutez l’étape de filigrane dans la [!UICONTROL Ressources de mise à jour de gestion des actifs numériques] workflow.

1. Accédez au [!DNL Experience Manager] dans l’interface utilisateur, puis accédez à **[!UICONTROL Outils]** > **[!UICONTROL Workflow]** > **[!UICONTROL Modèles]**.
1. Dans la **[!UICONTROL Modèles de processus]** , sélectionnez **[!UICONTROL Ressources de mise à jour de gestion des actifs numériques]** workflow et clic **[!UICONTROL Modifier]**.

1. Dans le panneau latéral, faites glisser le **[!UICONTROL Ajouter un filigrane]** à l’étape [!UICONTROL Ressources de mise à jour de gestion des actifs numériques] workflow.

   ![Faites glisser le [!UICONTROL Ajouter un filigrane] et ajoutez à la [!UICONTROL Ressources de mise à jour de gestion des actifs numériques] workflow](assets/add_watermark_step_aem_assets.png)

   *Figure : Faites glisser le [!UICONTROL Ajouter un filigrane] et ajoutez à la [!UICONTROL Ressources de mise à jour de gestion des actifs numériques] workflow.*

   >[!NOTE]
   >
   >Placez le [!UICONTROL Ajouter un filigrane] n’importe où avant [!UICONTROL Miniature de processus] étape .

1. Ouvrez l’étape **[!UICONTROL Ajouter un filigrane]** pour afficher ses propriétés.
1. Sous l’onglet **[!UICONTROL Arguments]**, spécifiez des valeurs valides dans les différents champs, notamment le texte, le type de police, la taille, la couleur, l’emplacement, l’orientation, etc. Pour confirmer les modifications, cliquez sur **[!UICONTROL Terminé]**.

   ![Indiquer les arguments dans l’étape Ajouter un filigrane dans [!DNL Assets]](assets/arguments_add_watermark_aem_assets.png)

   *Figure : Fournissez les arguments de l’étape Ajouter un filigrane dans [!DNL Assets].*

1. Enregistrez le **[!UICONTROL Ressources de mise à jour de gestion des actifs numériques]** workflow avec l’étape du filigrane.
1. Dans la [!DNL Assets] dans l’interface utilisateur, téléchargez un exemple de ressource. Le filigrane apparaît avec la taille de police, la couleur, etc., à l’emplacement configuré aux étapes ci-dessus.

Pour mettre des documents PDF en filigrane par programmation ou avec des informations dynamiques, pensez à utiliser [Experience Manager Document Services](/help/forms/using/overview-aem-document-services.md) offre.

## Conseils et restrictions {#tips-limitations}

* Seuls les filigranes basés sur du texte sont pris en charge. Les images ne sont pas utilisées comme filigranes, même si vous pouvez télécharger des images lors de la création du [!UICONTROL Ajout d’un processus de filigrane].
* Seuls les fichiers PNG et JPEG sont pris en charge pour être mis en filigrane. Les autres formats de ressource ne sont pas filigrane.
