---
title: Application de workflows aux ressources
description: Découvrez comment appliquer des workflows aux ressources, aux dossiers et aux collections dans AEM Assets.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 0ff23556444fcb161b0adf744bb72fdc50322d92

---


# Application de processus aux ressources de traitement {#applying-workflows-to-assets}

L’application de workflow aux ressources numériques est identique à l’application de workflow aux pages d’un site web. For a complete guide on how to create and use workflows in AEM, see [start workflows](/help/sites-authoring/workflows-participating.md).

Utilisez les workflow dans les ressources numériques pour activer les ressources ou créer des filigranes. La plupart des workflow destinés aux ressources sont automatiquement activés, comme le workflow permettant de créer automatiquement un rendu après la modification d’une image.

If a workflow available in Classic UI is not available in Touch-enabled UI, like Request to Activate and Request to Deactivate, see [make workflow models](/help/sites-developing/workflows-models.md#classic2touchui).

## Application d’un workflow à une ressource AEM {#applying-a-workflow-to-an-aem-asset}

For details of applying a workflow to an AEM asset, see [start a workflow on an asset](/help/assets/managing-assets-touch-ui.md#starting-a-workflow-on-an-asset).

## Application d’un workflow à plusieurs ressources {#applying-a-workflow-to-multiple-assets}

1. Dans la console Ressources, accédez à l’emplacement des ressources pour lesquelles vous souhaitez démarrer un workflow, puis sélectionnez les ressources.
1. Click/ tap the Experience Manager logo, and the choose **[!UICONTROL Timeline]** from the menu to display the timeline.

   ![screen_shot_2019-03-06at123325pm](assets/chlimage_1-136.png)

1. Cliquez/appuyez sur **[!UICONTROL Actions]** dans la partie inférieure.

   ![chlimage_1-30](assets/chlimage_1-137.png)

1. Appuyez sur **[!UICONTROL Démarrer le processus]**.
1. Dans la section **[!UICONTROL Démarrer le workflow]**, sélectionnez un modèle de workflow dans la liste.

   ![chlimage_1-31](assets/chlimage_1-138.png)

1. (Facultatif) Spécifiez le titre du workflow, qui peut permettre de référencer l’instance du workflow.
1. Tap **[!UICONTROL Start]** and then tap **[!UICONTROL Confirm]** in the dialog. Le workflow s’exécute sur toutes les ressources sélectionnées.

## Application d’un workflow à plusieurs dossiers {#applying-a-workflow-to-multiple-folders}

La procédure à suivre pour appliquer un workflow à plusieurs dossiers est similaire à celle observée permettant d’appliquer un workflow à plusieurs ressources. Select the folders in the Assets console, and perform steps 2-7 of the procedure [apply a workflow to multiple assets](/help/assets/assets-workflow.md#applying-a-workflow-to-multiple-assets).

## Application d’un workflow à une collection {#applying-a-workflow-to-a-collection}

Voir [Application d’un processus à une collection](/help/assets/managing-collections-touch-ui.md#running-a-workflow-on-a-collection).
