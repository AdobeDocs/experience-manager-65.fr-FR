---
title: Ressources liées
description: Découvrez comment relier des ressources numériques qui partagent certains attributs communs. Créez également des relations dérivées de la source entre les ressources numériques.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 23d19d9656d61874cd00a9a2473092be0c53b8f8
workflow-type: tm+mt
source-wordcount: '640'
ht-degree: 50%

---


# Ressources liées{#related-assets}

[!DNL Adobe Experience Manager Assets] vous permet de relier manuellement des ressources en fonction des besoins de votre organisation à l’aide de la fonction d’éléments connexes. Par exemple, vous pouvez mettre en relation un fichier de licence avec une ressource ou une image/vidéo portant sur un sujet similaire. Vous pouvez mettre en relation des ressources qui partagent certains attributs communs. Vous pouvez également utiliser cette fonctionnalité pour créer des relations source/dérivés entre des ressources. Par exemple, si un fichier PDF est généré à partir d’un fichier INDD, vous pouvez mettre en relation le fichier PDF avec son fichier INDD source.

Cette fonctionnalité vous permet de partager un fichier PDF ou JPG basse résolution avec des fournisseurs ou des agences et de rendre le fichier INDD haute résolution disponible uniquement sur demande.

>[!NOTE] Seuls les utilisateurs disposant d’autorisations de modification sur les ressources peuvent établir une relation et établir une relation entre les ressources.
>

## Lier les ressources {#relating-assets}

1. From the Experience Manager interface, open the **[!UICONTROL Properties]** page for an asset that you want to relate.

   ![ouvrir la page Propriétés d’une ressource pour établir une relation avec la ressource](assets/asset-properties-relate-assets.png)

   *Figure :[!DNL Assets][!UICONTROL Page de propriétés]pour associer des ressources.*

   Vous pouvez également sélectionner la ressource en mode Liste.

   ![chlimage_1-273](assets/chlimage_1-273.png)

   Sinon, sélectionnez la ressource à partir d’une collection.

   ![chlimage_1-274](assets/chlimage_1-274.png)

1. To relate another asset with the asset you selected, click the **[!UICONTROL Relate]** icon from the toolbar.

   ![chlimage_1-275](assets/chlimage_1-275.png)

1. Utilisez l’une des méthodes suivantes :

   * Pour mettre en relation le fichier source avec la ressource, sélectionnez **[!UICONTROL Source]** dans la liste.
   * Pour mettre en relation un fichier dérivé avec la ressource, sélectionnez **[!UICONTROL Dérivés]** dans la liste.
   * Pour créer une relation réciproque entre les ressources, sélectionnez **[!UICONTROL Autres]** dans la liste.
   ![chlimage_1-276](assets/chlimage_1-276.png)

1. Sur l’écran **[!UICONTROL Sélectionner une ressource]**, accédez à l’emplacement de la ressource que vous souhaitez mettre en relation et sélectionnez-la.

   ![chlimage_1-277](assets/chlimage_1-277.png)

1. Click the **[!UICONTROL Confirm]** icon.
1. Click **[!UICONTROL OK]** to close the dialog. En fonction de la relation que vous avez choisie à l’étape 3, la ressource associée apparaît sous une catégorie appropriée dans la section **[!UICONTROL En relation]**. Par exemple, si la ressource que vous avez mise en relation est le fichier source de la ressource actuelle, elle apparaît sous **[!UICONTROL Source]**.

   ![chlimage_1-278](assets/chlimage_1-278.png)

1. Pour annuler la relation entre un élément, cliquez sur **[!UICONTROL Annuler la relation]** dans la barre d’outils.

   ![chlimage_1-279](assets/chlimage_1-279.png)

1. Select the asset(s) you want to un-relate from the **[!UICONTROL Remove Relations]** dialog, and the click **[!UICONTROL Unrelate]**.

   ![chlimage_1-280](assets/chlimage_1-280.png)

1. Click **[!UICONTROL OK]** to close the dialog. Les ressources pour lesquelles vous avez supprimé des relations sont supprimées de la liste des ressources mises en relation dans la section **[!UICONTROL En relation]**.

## Traduction de ressources associées {#translating-related-assets}

La création de relations source/dérivés entre des ressources à l’aide de la fonctionnalité Ressources mises en relation est également utile dans les processus de traduction. When you run a translation workflow on a derived asset, [!DNL Experience Manager Assets] automatically fetches any asset that the source file references and includes it for translation. De cette manière, la ressource référencée par la ressource source est traduite avec les ressources source et dérivées. Par exemple, supposons que votre copie de langue anglaise inclut une ressource dérivée et son fichier source, comme indiqué sur l’image ci-dessous.

![chlimage_1-281](assets/chlimage_1-281.png)

If the source file is related to another asset, [!DNL Experience Manager Assets] fetches the referenced asset and includes it for translation.

![la page Propriétés du fichier affiche le fichier source du fichier associé à inclure pour la traduction.](assets/asset-properties-source-asset.png)

*Figure : Fichier source des éléments connexes à inclure pour la traduction.*

1. Traduisez les ressources du dossier source dans une langue cible en suivant les étapes de la section [Créer un projet de traduction](translation-projects.md#create-a-new-translation-project). Par exemple, dans ce cas, traduisez vos ressources en français.

1. From the [!UICONTROL Projects] page, open the translation folder.

   ![chlimage_1-283](assets/chlimage_1-283.png)

1. Cliquez sur la mosaïque du projet pour ouvrir la page de détails.

   ![chlimage_1-284](assets/chlimage_1-284.png)

1. Cliquez sur les points de suspension sous la carte Tâche de traduction pour vue l’état de la traduction.

   ![chlimage_1-285](assets/chlimage_1-285.png)

1. Select the asset and then click **[!UICONTROL Reveal in Assets]** from the toolbar to view the translation status for the asset.

   ![chlimage_1-286](assets/chlimage_1-286.png)

1. Pour vérifier si les fichiers associés à la source ont été traduits, cliquez sur le fichier source.

   ![chlimage_1-287](assets/chlimage_1-287.png)

1. Select the asset that is related to the source, and then click **[!UICONTROL Reveal in Assets]**. La ressource associée traduite s’affiche.

   ![chlimage_1-288](assets/chlimage_1-288.png)
