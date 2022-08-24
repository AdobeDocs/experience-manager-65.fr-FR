---
title: Utiliser PDF Rasterizer pour générer des rendus
description: Générez des miniatures et des rendus de haute qualité à l’aide de la bibliothèque Adobe PDF Rasterizer.
contentOwner: AG
role: Developer, Admin
feature: Developer Tools,Renditions
exl-id: 6f365d6b-3972-4885-8766-5889e24289f1
source-git-commit: bb46b0301c61c07a8967d285ad7977514efbe7ab
workflow-type: tm+mt
source-wordcount: '721'
ht-degree: 40%

---

# Utilisation de PDF Rasterizer {#using-pdf-rasterizer}

Lorsque vous transférez des fichiers PDF ou AI volumineux et gourmands en contenu vers [!DNL Adobe Experience Manager Assets], la bibliothèque par défaut peut ne pas générer de sortie exacte. La bibliothèque PDF Rasterizer d’Adobe peut générer une sortie plus fiable et plus précise par rapport à la sortie d’une bibliothèque par défaut. Adobe recommande d’utiliser la bibliothèque PDF Rasterizer pour les scénarios suivants :

Adobe recommande d’utiliser la bibliothèque PDF Rasterizer pour ce qui suit :

* Fichiers AI ou fichiers PDF lourds et gourmands en contenu.
* Fichiers AI et fichiers de PDF avec des miniatures qui ne sont pas générées par défaut.
* Fichiers AI contenant des couleurs PMS (Pantone Matching System).

Les miniatures et les aperçus générés à l’aide de PDF Rasterizer sont d’une plus grande qualité par rapport à la sortie native et fournissent donc une expérience d’affichage homogène sur tous les périphériques. La bibliothèque PDF Rasterizer d’Adobe ne prend en charge aucune conversion d’espace colorimétrique. Elle génère toujours une sortie RVB indépendamment de l’espace colorimétrique du fichier source.

1. Installez le module PDF Rasterizer sur votre [!DNL Adobe Experience Manager] déploiement à partir de [Distribution logicielle](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/product/assets/aem-assets-pdf-rasterizer-pkg-4.4.zip).

   >[!NOTE]
   >
   >La bibliothèque PDF Rasterizer est disponible sous Windows et Linux uniquement.

1. Accédez au [!DNL Assets] console de workflow à l’adresse `https://[aem_server]:[port]/workflow`. Ouvrir [!UICONTROL Ressources de mise à jour de gestion des actifs numériques] workflow.

1. Pour empêcher la génération de miniatures et de rendus web pour les fichiers PDF et les fichiers AI à l’aide des méthodes par défaut, procédez comme suit :

   * Ouvrez le **[!UICONTROL Miniatures des processus]** et ajoutez `application/pdf` ou `application/postscript` dans le **[!UICONTROL Ignorer les types MIME]** sous le champ **[!UICONTROL Miniatures]** au besoin.

   ![skip_mime_types-2](assets/skip_mime_types-2.png)

   * Dans le **[!UICONTROL Image web]** onglet, ajouter `application/pdf` ou `application/postscript` under **[!UICONTROL Ignorer la liste]** selon vos besoins.

   ![Configuration pour ignorer le traitement des miniatures pour un format d’image](assets/web_enabled_imageskiplist.png)

1. Ouvrez le **[!UICONTROL Pixelliser le rendu d’aperçu d’image PDF/AI]** et supprimez le type MIME pour lequel vous souhaitez ignorer la génération par défaut des rendus d’image d’aperçu. Par exemple, supprimez le type MIME . `application/pdf`, `application/postscript`ou `application/illustrator` de la **[!UICONTROL Types MIME]** liste.

   ![process_arguments](assets/process_arguments.png)

1. Faites glisser l’étape **[!UICONTROL Gestionnaire PDF Rasterizer]** à partir du panneau latéral et déposez-le en dessous de l’étape **[!UICONTROL Miniatures des processus]**.
1. Configurez les arguments suivants pour la variable **[!UICONTROL Gestionnaire PDF Rasterizer]** étape :

   * Types MIME : `application/pdf` ou `application/postscript`
   * Commandes: `PDFRasterizer -d -s 1280 -t PNG -i ${file}`
   * Ajoutez les tailles des miniatures : 319:319, 140:100, 48:48. Ajoutez une configuration de miniature personnalisée, si nécessaire.

   Voici des arguments de ligne de commande de la commande `PDFRasterizer` :

   * `-d`: Indicateur qui permet un rendu fluide du texte, des illustrations vectorielles et des images. Crée des images de meilleure qualité. Toutefois, l’ajout de ce paramètre ralentit l’exécution de la commande et augmente la taille des images.

   * `-s`: Dimension d’image maximale (hauteur ou largeur). Elle est convertie en ppp pour chaque page. Si les pages sont de tailles différentes, chacune peut être redimensionnée selon une échelle différente. La valeur par défaut est la taille réelle de la page.

   * `-t`: Type d’image de sortie. Les types valides sont JPEG, PNG, GIF et BMP. La valeur par défaut est JPEG.

   * `-i`: Chemin du PDF d’entrée. Ce paramètre est obligatoire.

   * `-h`: Aide


1. Pour supprimer des rendus intermédiaires, sélectionnez **[!UICONTROL Supprimer le rendu généré]**.
1. Pour laisser PDF Rasterizer générer des rendus web, sélectionnez **[!UICONTROL Générer un rendu web]**.

   ![generate_web_renditions1](assets/generate_web_renditions1.png)

1. Spécifiez les paramètres dans la variable **[!UICONTROL Image web]** .

   ![web_enabled_image1](assets/web_enabled_image1.png)

1. Enregistrez le workflow.
1. Pour permettre à PDF Rasterizer de traiter des pages de PDF avec des bibliothèques de PDF, ouvrez le **[!UICONTROL Sous-ressource de processus DAM]** du modèle [!UICONTROL Workflow] console.
1. Dans le panneau latéral, faites glisser l’étape Gestionnaire PDF Rasterizer sous le **[!UICONTROL Créer un rendu d’image compatible avec le Web]** étape .
1. Configurez les arguments suivants pour la variable **[!UICONTROL Gestionnaire PDF Rasterizer]** étape :

   * Types MIME : `application/pdf` ou `application/postscript`
   * Commandes: `PDFRasterizer -d -s 1280 -t PNG -i ${file}`
   * Ajoutez des tailles de miniature : `319:319`, `140:100`, `48:48`. Ajoutez une configuration de miniature personnalisée selon les besoins.

   Voici des arguments de ligne de commande de la commande `PDFRasterizer` :

   * `-d`: Indicateur qui permet un rendu fluide du texte, des illustrations vectorielles et des images. Crée des images de meilleure qualité. Toutefois, l’ajout de ce paramètre ralentit l’exécution de la commande et augmente la taille des images.

   * `-s`: Dimension d’image maximale (hauteur ou largeur). Elle est convertie en ppp pour chaque page. Si les pages sont de tailles différentes, chacune peut être redimensionnée selon une échelle différente. La valeur par défaut est la taille réelle de la page.

   * `-t`: Type d’image de sortie. Les types valides sont JPEG, PNG, GIF et BMP. La valeur par défaut est JPEG.

   * `-i`: Chemin du PDF d’entrée. Ce paramètre est obligatoire.

   * `-h`: Aide


1. Pour supprimer des rendus intermédiaires, sélectionnez **[!UICONTROL Supprimer le rendu généré]**.
1. Pour laisser PDF Rasterizer générer des rendus web, sélectionnez **[!UICONTROL Générer un rendu web]**.

   ![generate_web_renditions](assets/generate_web_renditions.png)

1. Spécifiez les paramètres dans la variable **[!UICONTROL Image web]** .

   ![web_enabled_image-1](assets/web_enabled_image-1.png)

1. Enregistrez le workflow.
1. Chargement d’un fichier de PDF ou d’un fichier AI vers [!DNL Experience Manager Assets]. PDF Rasterizer génère les miniatures et les rendus web pour le fichier.
