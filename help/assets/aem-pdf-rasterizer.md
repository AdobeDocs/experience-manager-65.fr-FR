---
title: Utilisation de PDF rasterizer pour générer des rendus
description: Générez des miniatures et des rendus de haute qualité à l’aide de la bibliothèque Adobe PDF Rasterizer.
contentOwner: AG
role: Developer, Administrator
feature: Outils de développement,Rendus
exl-id: 6f365d6b-3972-4885-8766-5889e24289f1
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '723'
ht-degree: 43%

---

# Utilisation de PDF Rasterizer {#using-pdf-rasterizer}

Lorsque vous téléchargez des fichiers PDF ou AI volumineux et gourmands en contenu vers [!DNL Adobe Experience Manager Assets], la bibliothèque par défaut peut ne pas générer de sortie exacte. La bibliothèque PDF Rasterizer d’Adobe peut générer une sortie plus fiable et plus précise par rapport à la sortie d’une bibliothèque par défaut. Adobe recommande d’utiliser la bibliothèque PDF Rasterizer pour les scénarios suivants :

Adobe recommande d’utiliser la bibliothèque PDF Rasterizer pour ce qui suit :

* Fichiers AI ou PDF lourds et gourmands en contenu.
* Fichiers AI et fichiers PDF contenant des miniatures qui ne sont pas générées par défaut.
* Fichiers AI contenant des couleurs PMS (Pantone Matching System).

Les miniatures et les aperçus générés à l’aide de PDF Rasterizer sont d’une plus grande qualité par rapport à la sortie native et fournissent donc une expérience d’affichage homogène sur tous les périphériques. La bibliothèque PDF Rasterizer d’Adobe ne prend en charge aucune conversion d’espace colorimétrique. Elle génère toujours une sortie RVB indépendamment de l’espace colorimétrique du fichier source.

1. Installez le package PDF Rasterizer sur votre déploiement [!DNL Adobe Experience Manager] à partir de [Distribution logicielle](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq640/product/assets/aem-assets-pdf-rasterizer-pkg).

   >[!NOTE]
   >
   >La bibliothèque PDF Rasterizer est disponible sous Windows et Linux uniquement.

1. Accédez à la console de workflow [!DNL Assets] à l’adresse `https://[aem_server]:[port]/workflow`. Ouvrez le workflow [!UICONTROL Ressources de mise à jour de gestion des actifs numériques] .

1. Pour empêcher la génération de miniatures et de rendus web pour les fichiers PDF et AI à l’aide des méthodes par défaut, procédez comme suit :

   * Ouvrez l’étape **[!UICONTROL Miniatures des processus]** et ajoutez `application/pdf` ou `application/postscript` dans le champ **[!UICONTROL Types MIME ignorés]** sous l’onglet **[!UICONTROL Miniatures]** si nécessaire.

   ![skip_mime_types-2](assets/skip_mime_types-2.png)

   * Dans l’onglet **[!UICONTROL Image Web]** , ajoutez `application/pdf` ou `application/postscript` sous **[!UICONTROL Liste à ignorer]** en fonction de vos besoins.

   ![Configuration pour ignorer le traitement des miniatures pour un format d’image](assets/web_enabled_imageskiplist.png)

1. Ouvrez l’étape **[!UICONTROL Pixelliser le rendu d’aperçu d’image PDF/AI]** et supprimez le type MIME pour lequel vous souhaitez ignorer la génération par défaut des rendus d’image d’aperçu. Par exemple, supprimez le type MIME `application/pdf`, `application/postscript` ou `application/illustrator` de la liste **[!UICONTROL Types MIME]**.

   ![process_arguments](assets/process_arguments.png)

1. Faites glisser l’étape **[!UICONTROL Gestionnaire PDF Rasterizer]** à partir du panneau latéral et déposez-le en dessous de l’étape **[!UICONTROL Miniatures des processus]**.
1. Configurez les arguments suivants pour l’étape **[!UICONTROL Gestionnaire PDF Rasterizer]** :

   * Types MIME : `application/pdf` ou `application/postscript`
   * Commandes: `PDFRasterizer -d -s 1280 -t PNG -i ${file}`
   * Ajoutez les tailles des miniatures : 319:319, 140:100, 48:48. Ajoutez une configuration de miniature personnalisée, si nécessaire.

   Voici des arguments de ligne de commande de la commande `PDFRasterizer` :

   * `-d`: Indicateur qui permet un rendu fluide du texte, des illustrations vectorielles et des images. Crée des images de meilleure qualité. Toutefois, l’ajout de ce paramètre ralentit l’exécution de la commande et augmente la taille des images.

   * `-s`: Dimension d’image maximale (hauteur ou largeur). Elle est convertie en ppp pour chaque page. Si les pages sont de tailles différentes, chacune peut être redimensionnée selon une échelle différente. La valeur par défaut est la taille réelle de la page.

   * `-t`: Type d’image de sortie. Les types valides sont JPEG, PNG, GIF et BMP. La valeur par défaut est JPEG.

   * `-i`: Chemin d’accès pour les PDF d’entrée. Ce paramètre est obligatoire.

   * `-h`: Aide


1. Pour supprimer des rendus intermédiaires, sélectionnez **[!UICONTROL Supprimer le rendu généré]**.
1. Pour laisser PDF Rasterizer générer des rendus web, sélectionnez **[!UICONTROL Générer le rendu web]**.

   ![generate_web_renditions1](assets/generate_web_renditions1.png)

1. Spécifiez les paramètres dans l’onglet **[!UICONTROL Image Web]**.

   ![web_enabled_image1](assets/web_enabled_image1.png)

1. Enregistrez le workflow.
1. Pour permettre à PDF Rasterizer de traiter des pages PDF avec des bibliothèques PDF, ouvrez le modèle **[!UICONTROL DAM Process Subasset]** à partir de la console [!UICONTROL Workflow].
1. Dans le panneau latéral, faites glisser l’étape Gestionnaire PDF Rasterizer sous l’étape **[!UICONTROL Créer un rendu d’image compatible avec le web]** .
1. Configurez les arguments suivants pour l’étape **[!UICONTROL Gestionnaire PDF Rasterizer]** :

   * Types MIME : `application/pdf` ou `application/postscript`
   * Commandes: `PDFRasterizer -d -s 1280 -t PNG -i ${file}`
   * Ajoutez des tailles de miniature : `319:319`, `140:100`, `48:48`. Ajoutez une configuration de miniature personnalisée selon les besoins.

   Voici des arguments de ligne de commande de la commande `PDFRasterizer` :

   * `-d`: Indicateur qui permet un rendu fluide du texte, des illustrations vectorielles et des images. Crée des images de meilleure qualité. Toutefois, l’ajout de ce paramètre ralentit l’exécution de la commande et augmente la taille des images.

   * `-s`: Dimension d’image maximale (hauteur ou largeur). Elle est convertie en ppp pour chaque page. Si les pages sont de tailles différentes, chacune peut être redimensionnée selon une échelle différente. La valeur par défaut est la taille réelle de la page.

   * `-t`: Type d’image de sortie. Les types valides sont JPEG, PNG, GIF et BMP. La valeur par défaut est JPEG.

   * `-i`: Chemin d’accès pour les PDF d’entrée. Ce paramètre est obligatoire.

   * `-h`: Aide


1. Pour supprimer des rendus intermédiaires, sélectionnez **[!UICONTROL Supprimer le rendu généré]**.
1. Pour laisser PDF Rasterizer générer des rendus web, sélectionnez **[!UICONTROL Générer le rendu web]**.

   ![generate_web_renditions](assets/generate_web_renditions.png)

1. Spécifiez les paramètres dans l’onglet **[!UICONTROL Image Web]**.

   ![web_enabled_image-1](assets/web_enabled_image-1.png)

1. Enregistrez le workflow.
1. Transférez un fichier PDF ou AI vers [!DNL Experience Manager Assets]. PDF Rasterizer génère les miniatures et les rendus web pour le fichier.
