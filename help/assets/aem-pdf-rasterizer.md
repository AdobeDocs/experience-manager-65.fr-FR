---
title: Utiliser PDF Rasterizer pour générer des rendus
description: Générez des miniatures et des rendus de haute qualité avec la bibliothèque Adobe PDF Rasterizer.
contentOwner: AG
role: Developer, Admin
feature: Developer Tools,Renditions
exl-id: 6f365d6b-3972-4885-8766-5889e24289f1
solution: Experience Manager, Experience Manager Assets
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '694'
ht-degree: 100%

---

# Utilisation de PDF Rasterizer {#using-pdf-rasterizer}

Lorsque vous téléchargez des fichiers PDF ou AI de grande taille et riches en contenu vers [!DNL Adobe Experience Manager Assets], la bibliothèque par défaut risque de ne pas générer une sortie exacte. La bibliothèque Adobe PDF Rasterizer peut générer une sortie plus fiable et plus précise par rapport à la sortie d’une bibliothèque par défaut. Adobe recommande d’utiliser la bibliothèque PDF Rasterizer pour les scénarios suivants :

Adobe recommande d’utiliser la bibliothèque PDF Rasterizer pour ce qui suit :

* Fichiers d’IA ou PDF lourds et gourmands en contenu
* Fichiers d’IA et PDF avec des miniatures qui ne sont pas générées par défaut
* Fichiers d’AI contenant des couleurs PMS (Pantone Matching System)

Les miniatures et les aperçus générés à l’aide de PDF Rasterizer sont de meilleure qualité que ceux de la sortie prête à l’emploi et offrent donc une expérience d’affichage cohérente sur tous les appareils. La bibliothèque PDF Rasterizer d’Adobe ne prend en charge aucune conversion d’espace colorimétrique. La sortie produite est toujours en RGB, quel que soit l’espace colorimétrique du fichier source.

1. Installez le package PDF Rasterizer sur votre déploiement [!DNL Adobe Experience Manager] à partir de la [Distribution logicielle](https://experience.adobe.com/#/downloads/content/software-distribution/en/aem.html?package=/content/software-distribution/en/details.html/content/dam/aem/public/adobe/packages/cq650/product/assets/aem-assets-pdf-rasterizer-pkg-4.6.zip?lang=fr).

   >[!NOTE]
   >
   >La bibliothèque PDF Rasterizer est disponible sous Windows et Linux® uniquement.

1. Accédez à la console de workflow [!DNL Assets] à l’adresse `https://[aem_server]:[port]/workflow`. Ouvrez le workflow [!UICONTROL Ressource de mise à jour de la gestion des ressources numériques].

1. Pour éviter la génération de miniatures et de rendus Web pour les fichiers PDF et d’AI à l’aide des méthodes par défaut, procédez comme suit :

   * Ouvrez l’étape **[!UICONTROL Traiter les miniatures]**, puis ajoutez `application/pdf` ou `application/postscript` dans le champ **[!UICONTROL Ignorer les types MIME]** sous l’onglet **[!UICONTROL Miniatures]**, en fonction de vos besoins.

   ![skip_mime_types-2](assets/skip_mime_types-2.png)

   * Dans l’onglet **[!UICONTROL Image Web activée]**, ajoutez `application/pdf` ou `application/postscript` sous **[!UICONTROL Liste à ignorer]**, en fonction de vos besoins.

   ![Configuration pour ignorer le traitement des miniatures pour un format d’image](assets/web_enabled_imageskiplist.png)

1. Ouvrez l’étape **[!UICONTROL Pixelliser le rendu d’aperçus d’image PDF/AI]** et supprimez le type MIME pour lequel vous souhaitez ignorer l’étape de génération par défaut des rendus d’images d’aperçu. Par exemple, supprimez le type MIME `application/postscript`, `application/pdf` ou `application/illustrator` dans la liste **[!UICONTROL Types MIME]**.

   ![process_arguments](assets/process_arguments.png)

1. Faites glisser l’étape **[!UICONTROL Gestionnaire PDF Rasterizer]** à partir du panneau latéral et déposez-le en dessous de l’étape **[!UICONTROL Traiter les miniatures]**.
1. Configurez les arguments suivants pour l’étape **[!UICONTROL Gestionnaire PDF Rasterizer]** :

   * Types MIME : `application/pdf` ou `application/postscript`
   * Commandes : `PDFRasterizer -d -s 1280 -t PNG -i ${file}`
   * Ajoutez les tailles des miniatures : 319:319, 140:100, 48:48. Ajoutez une configuration de miniature personnalisée, si nécessaire.

   Les arguments de ligne de commande de la commande `PDFRasterizer` peuvent inclure les éléments suivants :

   * `-d` : indicateur pour activer le rendu lissé du texte, des illustrations vectorielles et des images. Crée des images de meilleure qualité. Toutefois, l’inclusion de ce paramètre entraîne une exécution lente de la commande et une augmentation de la taille des images.

   * `-s` : dimension maximale de l’image (hauteur ou largeur). Elle est convertie en ppp pour chaque page. Si les pages sont de tailles différentes, chacune peut être redimensionnée selon une échelle différente. La valeur par défaut est la taille réelle de la page.

   * `-t` : type d’image en sortie. Les types valides sont JPEG, PNG, GIF et BMP. La valeur par défaut est JPEG.

   * `-i` : chemin du PDF en entrée. Ce paramètre est obligatoire.

   * `-h` : Aide

1. Pour supprimer des rendus intermédiaires, sélectionnez **[!UICONTROL Supprimer le rendu généré]**.
1. Pour permettre à PDF Rasterizer de générer des rendus Web, sélectionnez **[!UICONTROL Générer le rendu Web]**.

   ![generate_Web_renditions1](assets/generate_web_renditions1.png)

1. Spécifiez les paramètres dans l’onglet **[!UICONTROL Image Web]**.

   ![Web_enabled_image1](assets/web_enabled_image1.png)

1. Enregistrez le workflow.
1. Afin d’activer PDF Rasterizer pour traiter des pages PDF avec des bibliothèques PDF, ouvrez le modèle **[!UICONTROL Sous-ressource du processus de gestion des ressources numériques]** dans la console [!UICONTROL Processus].
1. Dans le panneau latéral, faites glisser l’étape Gestionnaire PDF Rasterizer sous l’étape **[!UICONTROL Créer un rendu d’image compatible sur le Web]**.
1. Configurez les arguments suivants pour l’étape **[!UICONTROL Gestionnaire PDF Rasterizer]** :

   * Types MIME : `application/pdf` ou `application/postscript`
   * Commandes : `PDFRasterizer -d -s 1280 -t PNG -i ${file}`
   * Ajoutez les tailles des miniatures : `319:319`, `140:100`, `48:48`. Ajoutez une configuration de miniature personnalisée, si nécessaire.

   Les arguments de ligne de commande de la commande `PDFRasterizer` peuvent inclure les éléments suivants :

   * `-d` : indicateur pour activer le rendu lissé du texte, des illustrations vectorielles et des images. Crée des images de meilleure qualité. Toutefois, l’inclusion de ce paramètre entraîne une exécution lente de la commande et une augmentation de la taille des images.

   * `-s` : dimension maximale de l’image (hauteur ou largeur). Elle est convertie en ppp pour chaque page. Si les pages sont de tailles différentes, chacune peut être redimensionnée selon une échelle différente. La valeur par défaut est la taille réelle de la page.

   * `-t` : type d’image en sortie. Les types valides sont JPEG, PNG, GIF et BMP. La valeur par défaut est JPEG.

   * `-i` : chemin du PDF en entrée. Ce paramètre est obligatoire.

   * `-h` : Aide

1. Pour supprimer des rendus intermédiaires, sélectionnez **[!UICONTROL Supprimer le rendu généré]**.
1. Pour permettre à PDF Rasterizer de générer des rendus Web, sélectionnez **[!UICONTROL Générer le rendu Web]**.

   ![generate_Web_renditions](assets/generate_web_renditions.png)

1. Spécifiez les paramètres dans l’onglet **[!UICONTROL Image Web activée]**.

   ![Web_enabled_image-1](assets/web_enabled_image-1.png)

1. Enregistrez le workflow.
1. Chargement d’un fichier PDF ou IA vers [!DNL Experience Manager Assets]. PDF Rasterizer génère les miniatures et les rendus Web pour le fichier.
