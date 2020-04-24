---
title: Utilisation de PDF rasterizer pour générer des rendus
description: Cet article présente comment générer des miniatures et des rendus de haute qualité avec la bibliothèque Adobe PDF Rasterizer.
contentOwner: AG
translation-type: tm+mt
source-git-commit: abc4821ec3720969bf1c2fb068744c07477aca46

---


# Utiliser PDF Rasterizer {#using-pdf-rasterizer}

Parfois, lorsque vous téléchargez des fichiers PDF ou AI de grande taille et riches en contenu vers Adobe Experience Manager (AEM) Assets, la bibliothèque par défaut risque de ne pas générer une sortie exacte. Dans de tels cas, la bibliothèque Adobe PDF Rasterizer peut générer une sortie plus fiable et plus précise par rapport à la sortie d’une bibliothèque par défaut.

Adobe recommande d’utiliser la bibliothèque PDF Rasterizer pour ce qui suit :

* Fichiers AI/PDF de grande taille et riches en continu.
* Les fichiers AI et PDF avec des miniatures ne sont pas générés en dehors de la zone.
* Fichiers AI contenant des couleurs PMS (Pantone Matching System).

Les miniatures et les aperçus générés à l’aide de PDF Rasterizer sont d’une plus grande qualité par rapport à la sortie native et fournissent donc une expérience d’affichage homogène sur tous les périphériques. La bibliothèque PDF Rasterizer d’Adobe ne prend en charge aucune conversion d’espace colorimétrique. Elle génère toujours une sortie RVB indépendamment de l’espace colorimétrique du fichier source.

1. Install the PDF Rasterizer package on your AEM deployment from [Package Share](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq640/product/assets/aem-assets-pdf-rasterizer-pkg).

   >[!NOTE]
   >
   >La bibliothèque PDF Rasterizer est disponible sous Windows et Linux uniquement.

1. Accédez à la console de flux de travaux AEM Assets à l’adresse `https://[server]:[port]/workflow`. Open the [!UICONTROL DAM Update Asset] workflow page.

1. Pour éviter la génération de miniatures et de rendus web pour les fichiers PDF et AI à l’aide des méthodes par défaut, procédez comme suit :

   * Open the **[!UICONTROL Process Thumbnails]** step, and add `application/pdf` or `application/postscript` in the **[!UICONTROL Skip Mime Types]** field under the **[!UICONTROL Thumbnails]** tab as necessary.
   ![skip_mime_types-2](assets/skip_mime_types-2.png)

   * In the **[!UICONTROL Web Enabled Image]** tab, add `application/pdf` or `application/postscript` under **[!UICONTROL Skip List]** depending upon your requirements.
   ![Configuration permettant d’ignorer le traitement des miniatures pour un format d’image](assets/web_enabled_imageskiplist.png)

1. Open the **[!UICONTROL Rasterize PDF/AI Image Preview Rendition]** step, and remove the MIME type for which you want to skip the default generation of preview image renditions. For example, remove the MIME type `application/pdf`, `application/postscript`, or `application/illustrator` from the **[!UICONTROL MIME Types]** list.

   ![process_arguments](assets/process_arguments.png)

1. Faites glisser l’étape **[!UICONTROL Gestionnaire PDF Rasterizer]** à partir du panneau latéral et déposez-le en dessous de l’étape **[!UICONTROL Miniatures des processus]**.
1. Configure the following arguments for the **[!UICONTROL PDF Rasterizer Handler]** step:

   * Types MIME : `application/pdf` ou `application/postscript`

   * Commandes: `PDFRasterizer -d -p 1 -s 1280 -t PNG -i ${file}`
   * Ajoutez les tailles des miniatures : 319:319, 140:100, 48:48. Ajoutez une configuration de miniature personnalisée, si nécessaire.
   Voici des arguments de ligne de commande de la commande `PDFRasterizer` :

   * `-d`: Indicateur permettant d’effectuer un rendu lisse du texte, des illustrations vectorielles et des images. Crée des images de meilleure qualité. Toutefois, l’ajout de ce paramètre ralentit l’exécution de la commande et augmente la taille des images.

   * `-p`: Numéro de page. La valeur par défaut est toutes les pages. Le signe * indique toutes les pages.

   * `-s`: Dimensions d’image maximales (hauteur ou largeur). Elle est convertie en ppp pour chaque page. Si les pages sont de tailles différentes, chacune peut être redimensionnée selon une échelle différente. La valeur par défaut est la taille réelle de la page.

   * `-t`: Type d’image de sortie. Les types valides sont JPEG, PNG, GIF et BMP. La valeur par défaut est JPEG.

   * `-i`: Chemin d’accès pour le PDF d’entrée. Ce paramètre est obligatoire.

   * `-h`: Aide


1. Pour supprimer des rendus intermédiaires, sélectionnez **[!UICONTROL Supprimer le rendu généré]**.
1. Pour laisser PDF Rasterizer générer des rendus web, sélectionnez **[!UICONTROL Générer le rendu web]**.

   ![generate_web_renditions1](assets/generate_web_renditions1.png)

1. Specify the settings in the **[!UICONTROL Web Enabled Image]** tab.

   ![web_enabled_image1](assets/web_enabled_image1.png)

1. Enregistrez le workflow.
1. To enable PDF Rasterizer to process PDF pages with PDF libraries, open the **[!UICONTROL DAM Process Subasset]** model from the Workflow console.
1. From the side panel, drag the PDF Rasterizer Handler step under the **[!UICONTROL Create Web-Enabled Image Rendition]** step.
1. Configure the following arguments for the **[!UICONTROL PDF Rasterizer Handler]** step:

   * Types MIME : `application/pdf` ou `application/postscript`

   * Commandes: `PDFRasterizer -d -p 1 -s 1280 -t PNG -i ${file}`
   * Ajoutez les tailles des miniatures : 319:319, 140:100, 48:48. Ajoutez une configuration de miniature personnalisée, si nécessaire.
   Voici des arguments de ligne de commande de la commande PDFRasterizer :

   * `-d`: Indicateur permettant d’effectuer un rendu lisse du texte, des illustrations vectorielles et des images. Crée des images de meilleure qualité. Toutefois, l’ajout de ce paramètre ralentit l’exécution de la commande et augmente la taille des images.

   * `-p`: Numéro de page. La valeur par défaut est toutes les pages. `*` indique toutes les pages.

   * `-s`: Dimensions d’image maximales (hauteur ou largeur). Elle est convertie en ppp pour chaque page. Si les pages sont de tailles différentes, chacune peut être redimensionnée selon une échelle différente. La valeur par défaut est la taille réelle de la page.

   * `-t`: Type d’image de sortie. Les types valides sont JPEG, PNG, GIF et BMP. La valeur par défaut est JPEG.

   * `-i`: Chemin d’accès pour le PDF d’entrée. Ce paramètre est obligatoire.

   * `-h`: Aide


1. Pour supprimer des rendus intermédiaires, sélectionnez **[!UICONTROL Supprimer le rendu généré]**.
1. Pour laisser PDF Rasterizer générer des rendus web, sélectionnez **[!UICONTROL Générer le rendu web]**.

   ![generate_web_renditions](assets/generate_web_renditions.png)

1. Specify the settings in the **[!UICONTROL Web Enabled Image]** tab.

   ![web_enabled_image-1](assets/web_enabled_image-1.png)

1. Enregistrez le workflow.
1. Téléchargez un fichier PDF ou AI vers AEM Assets. PDF Rasterizer génère les miniatures et les rendus web pour le fichier.
