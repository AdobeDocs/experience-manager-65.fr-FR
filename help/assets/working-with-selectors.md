---
title: Utilisation des sélecteurs
description: Sélection de ressources pour les images interactives, vidéos interactives et bannières de carrousel
uuid: 6231739c-bf49-4069-90a4-57848cc68d9a
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
discoiquuid: 262eb911-3dcb-475d-b410-8bcac1347905
translation-type: tm+mt
source-git-commit: 0595d89409e0ca21f771be5c55c3ec9548a8449f

---


# Utilisation des sélecteurs {#working-with-selectors}

Lorsque vous travaillez avec une image interactive, une vidéo interactive ou une bannière de carrousel, vous sélectionnez des fichiers et vous sélectionnez des sites et des produits pour les zones réactives et les zones cliquables à lier. Lorsque vous travaillez avec des visionneuses d’images, des visionneuses à 360° et des visionneuses de fichiers multimédia, vous sélectionnez également des fichiers à l’aide du sélecteur de fichiers.

Cette rubrique décrit comment utiliser les sélecteurs de produits, de sites et de ressources, y compris comment naviguer, filtrer et trier dans les sélecteurs.

Vous accédez aux sélecteurs lorsque vous créez des ensembles de carrousels, vous ajoutez des zones réactives et des zones cliquables et vous créez des vidéos et des images interactives.

Par exemple, dans cette bannière de carrousel, vous utilisez le sélecteur de produit si vous liez une zone réactive ou une zone cliquable à une page de visualisation rapide ; utilisez le sélecteur de site si vous liez une zone réactive ou une zone cliquable à un hyperlien ; utilisez le sélecteur de ressources lorsque vous créez une diapositive.

![chlimage_1-520](assets/chlimage_1-520.png)

Lorsque vous sélectionnez (au lieu de saisir manuellement) l’emplacement des zones réactives ou des zones cliquables, vous utilisez le sélecteur. Le sélecteur de site fonctionne uniquement si vous êtes un client AEM Sites. Le sélecteur de produits nécessite également AEM Commerce.

## Selecting products {#selecting-products}

Utilisez le sélecteur de produits pour choisir un produit lorsque vous souhaitez qu’une zone réactive ou une zone cliquable fournisse une vue rapide d’un produit spécifique dans votre catalogue de produits.

1. Navigate to the Carousel Set, Interactive Image, or Interactive Video, and tap the **[!UICONTROL Actions]** tab (only available if you have defined a hotspot or image map).

   The Product selector is in the **[!UICONTROL Action Type** area.

   ![chlimage_1-521](assets/chlimage_1-521.png)

1. Tap the **[!UICONTROL Product Selector]** icon (magnifying glass) and navigate to a product in the catalog.

   ![chlimage_1-522](assets/chlimage_1-522.png)

   You can also filter by keyword or tag by tapping **[!UICONTROL Filter]** and entering keywords, or selecting tags, or both.

   ![chlimage_1-523](assets/chlimage_1-523.png)

   You can change where AEM browses for product data by tapping **[!UICONTROL Browse]** and navigating to another folder.

   ![chlimage_1-524](assets/chlimage_1-524.png)

   Tap **[!UICONTROL Sort]** by to change whether AEM sorts by newest to oldest or oldest to newest.

   ![chlimage_1-525](assets/chlimage_1-525.png)

   Tap **[!UICONTROL View as]** to change how you view products – either **[!UICONTROL List View]** or **[!UICONTROL Card View]**.

   ![chlimage_1-526](assets/chlimage_1-526.png)

1. Une fois le produit sélectionné, le champ reçoit la miniature et le nom du produit.

   ![chlimage_1-527](assets/chlimage_1-527.png)

1. When in **[!UICONTROL Preview]** mode, you can tap the hotspot or image map, and see what the Quickview looks like.

   ![chlimage_1-528](assets/chlimage_1-528.png)

## Sélection de sites {#selecting-sites}

Utilisez le sélecteur de sites pour choisir une page web lorsque vous souhaitez qu’une zone réactive ou une zone cliquable pointe vers une page web gérée dans AEM Sites.

1. Navigate to the Carousel Set, Interactive Image, or Interactive Video, and tap the **[!UICONTROL Actions]** tab (only available if you have defined a hotspot or image map).

   The Site Selector is in the **[!UICONTROL Action Type]** area.

   ![chlimage_1-529](assets/chlimage_1-529.png)

1. Tap the **[!UICONTROL Site Selector]** icon (folder with magnifying glass) and navigate to a page in your AEM sites that you want to link the hotspot or image map to.

   ![chlimage_1-530](assets/chlimage_1-530.png)

1. Une fois le site sélectionné, le champ reçoit le chemin d’accès.

   ![chlimage_1-531](assets/chlimage_1-531.png)

1. When in **[!UICONTROL Preview]** mode if you tap the hotspot or image map, you navigate to the AEM site page you specified.

## Sélection des ressources {#selecting-assets}

Utilisez ce sélecteur pour choisir les images à utiliser dans une bannière de carrousel, une vidéo interactive, des visionneuses d’images, des visionneuses de supports variés et des visionneuses à 360°. In interactive Video, the asset selector is available when you tap **[!UICONTROL Select Assets]** in the **[!UICONTROL Content]** tab. Dans les visionneuses de carrousel, le sélecteur de ressources est disponible lorsque vous créez une diapositive. Dans les visionneuses d’images, les visionneuses de supports variés et les visionneuses à 360°, le sélecteur de fichiers est disponible lorsque vous créez une visionneuse d’images, une visionneuse de supports variés ou une visionneuse à 360°, respectivement.

See also [Asset Picker](search-assets.md#assetselector) for more information.

1. Accédez à la visionneuse de carrousel et créez une diapositive. Or, navigate to the Interactive Video, go the **[!UICONTROL Content]** tab and select assets. Vous pouvez également créer une visionneuse de supports variés, une visionneuse d’images ou une visionneuse à 360°.
1. Tap the **[!UICONTROL Asset Selector]** icon (folder with magnifying glass) and navigate to an asset.

   ![chlimage_1-532](assets/chlimage_1-532.png)

   You can also filter by keyword or tag by tapping **[!UICONTROL Filter]** and entering keywords, or adding criteria, or both.

   ![chlimage_1-533](assets/chlimage_1-533.png)

   Vous pouvez modifier l’emplacement où AEM recherche les ressources en accédant à un autre dossier dans le champ **[!UICONTROL Chemin]**.

   Tap **[!UICONTROL Collection]** to only search for assets within collections.

   ![chlimage_1-534](assets/chlimage_1-534.png)

   Tap **[!UICONTROL View as]** to change how you view products - either **[!UICONTROL List View]**, **[!UICONTROL Column View]**, or **[!UICONTROL Card View]**.

   ![chlimage_1-535](assets/chlimage_1-535.png)

1. Cochez la case pour sélectionner le fichier. La ressource s’affiche.

   ![chlimage_1-536](assets/chlimage_1-536.png)

