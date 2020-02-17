---
title: Prévisualisation de fichiers 3D
description: Découvrez comment prévisualiser des fichiers 3D
contentOwner: Rick Brough
docset: aem65
translation-type: tm+mt
source-git-commit: 0595d89409e0ca21f771be5c55c3ec9548a8449f

---


# Prévisualisation de fichiers 3D{#previewing-3d-assets}

Experience Manager prend en charge le téléchargement, la diffusion et l’aperçu interactif des ressources 3D dans le cadre du processus de création.

La visionneuse 3D interactive est disponible sur la page de détails de la ressource dans AEM. La visionneuse comprend, entre autres, un ensemble de contrôles de caméra interactifs qui permettent d’orbiter, de zoomer et de faire un panoramique sur la ressource 3D.

## Formats pris en charge pour l’aperçu 3D{#supported-3d-previewing-assets}

L’aperçu 3D interactif prend en charge les formats de fichier suivants :

| Extension de fichier 3D | Format de fichier | Type MIME | Notes |
|---|---|---|---|
| GLB | Transmission GL binaire | model/gltf-binary |  |
| GLTF | Format de transmission GL | model/gltf+json | Voir **la note** ci-dessous. |
| OBJ | Fichier d’objet 3D WaveFront | application/x-tgif |  |
| STL | Stéréolithographie | application/vnd.ms-pki.stl |  |
| DN | Adobe Dimension | model/x-adobe-dn | Prise en charge de l&#39;ingestion uniquement; aperçu non disponible. |
| USDZ | Archive zip de description de scène universelle | model/vnd.usdz+zip | Prise en charge de l&#39;ingestion uniquement; aperçu non disponible. |

**Remarque**: Si le rendu des matériaux n’est pas effectué dans l’aperçu d’un modèle gLTF, assurez-vous qu’ils sont correctement nommés et qu’ils se trouvent dans un `textures` dossier situé dans le même dossier racine que le modèle, comme suit :

    Asset (folder)
    model.
    gltfmodel.
    bintextures (folder)
    Material_0_baseColor.
    jpegMaterial_0_normal.jpeg

## Performance considerations when you preview 3D assets{#performance-3d-previewing-assets}

Le temps d’ouverture d’un fichier 3D dans la page d’affichage des détails du fichier dépend de plusieurs facteurs, tels que la bande passante, la complexité de l’image et les latences sur le serveur.

En outre, les fonctionnalités de l’ordinateur client (station de travail, ordinateur portable ou périphérique tactile mobile, par exemple) sont également importantes à prendre en compte lorsque vous manipulez l’appareil de manière interactive. Un système relativement puissant avec de bonnes capacités graphiques peut rendre l’expérience interactive d’affichage en 3D plus fluide et plus favorable.

**Pour prévisualiser des fichiers 3D**

1. Assurez-vous d’avoir chargé des ressources 3D dans AEM.
Voir Formats [pris en charge pour l’aperçu](#supported-3d-previewing-assets) 3D et le [téléchargement de fichiers](/help/assets/managing-assets-touch-ui.md#uploading-assets).
1. Dans AEM, sur la page de **[!UICONTROL navigation]** , appuyez sur **[!UICONTROL Ressources > Fichiers]**.

   ![Page de navigation](/help/assets/assets-dm/navigation-assets.png)

1. Près du coin supérieur droit de la page, dans la liste déroulante Affichage, appuyez sur Affichage **** carte, puis accédez à un fichier 3D à prévisualiser.

   ![Sélection de carte 3D](/help/assets/assets-dm/3d-card-select.png)
   _En mode Affichage par carte, appuyez sur la carte du fichier 3D à prévisualiser._

1. Appuyez sur la carte du fichier 3D pour l’ouvrir dans la page d’affichage des détails du fichier.

   ![Aperçu 3D interactif](/help/assets/assets-dm/3d-preview.png)
   _Aperçu interactif d’un fichier 3D dans la page d’affichage des détails du fichier._
1. Sur la page d’affichage des détails de la ressource 3D, effectuez l’une des opérations suivantes :
   * **Tournez votre appareil photo**: orbitez votre vue autour de la scène et des objets 3D.
      * _Souris_: Cliquez avec le bouton gauche + faites glisser.
      * _Ecran_ tactile : Appuyez sur un seul doigt et faites glisser.
   * **Panoramique de l&#39;appareil photo**(Pan your view left, right, up ou down).
      * _Souris_: Cliquez avec le bouton droit et faites glisser.
      * _Ecran_ tactile : Appuyez deux doigts et faites glisser.
   * **Zoom sur la caméra**(Zoom): permet de zoomer sur la caméra pour qu&#39;elle se déplace dans et hors des zones de la scène 3D.
      * _Souris_: Roue de défilement.
      * _Ecran_ tactile : Pincement à deux doigts.
   * **Recentrer votre appareil photo**: recentrez votre appareil photo sur un point de la scène 3D.
      * _Souris_: Double-cliquez.
      * _Ecran_ tactile : Appuyez deux fois.
   * **Réinitialiser**(Reset)près du coin inférieur droit de la page, appuyez sur l&#39;icône Réinitialiser (Reset) pour rétablir le point d&#39;affichage cible au centre du fichier 3D. Réinitialiser rapproche également la caméra d’un peu plus près pour afficher l’actif dans son intégralité et à une taille d’affichage raisonnable.
   * **Mode** Plein écran (Full screen): pour passer en mode Plein écran, dans le coin inférieur droit de la page, appuyez sur l&#39;icône Plein écran.

1. When you are finished, near the upper-right corner of the page, tap **[!UICONTROL Close]**.
