---
title: Prévisualisation de fichiers 3D
description: Découvrez comment prévisualiser des fichiers 3D
contentOwner: Rick Brough
docset: aem65
translation-type: tm+mt
source-git-commit: cec6c4f9a1a75eb049dd4b8461c36c8d58d46f79
workflow-type: tm+mt
source-wordcount: '564'
ht-degree: 100%

---


# Prévisualisation de ressources 3D dans AEM{#previewing-3d-assets-aem}

Adobe Experience Manager prend en charge le chargement, la diffusion et l’aperçu interactif des ressources 3D dans le cadre du processus de création.

La visionneuse 3D interactive est disponible sur la page de détails de la ressource dans AEM. La visionneuse comprend, entre autres, un ensemble de contrôles de caméra interactifs qui permettent d’orbiter, de zoomer et de faire un panoramique sur la ressource 3D.

<!-- See also [Working with 3D assets in Dynamic Media](/help/assets/assets-3d.md). -->

## Formats pris en charge pour la prévisualisation 3D dans AEM {#supported-3d-previewing-assets}

L’aperçu 3D interactif prend en charge les formats de fichier suivants :

| Extension de fichier 3D | Format de fichier | Type MIME | Remarques |
|---|---|---|---|
| GLB | Transmission GL binaire | model/gltf-binary |  |
| GLTF | Format de transmission GL | model/gltf+json | Consultez **la remarque** ci-dessous. |
| OBJ | Fichier d’objet 3D WaveFront | application/x-tgif |  |
| STL | Stéréolithographie | application/vnd.ms-pki.stl |  |
| DN | Adobe Dimension | model/x-adobe-dn | Prise en charge de l’assimilation uniquement, prévisualisation non disponible. |
| USDZ | Fichier zip de description de scène universelle | model/vnd.usdz+zip | Prise en charge de l’assimilation uniquement, prévisualisation non disponible. |

**Remarque** : si le rendu des matériaux n’est pas effectué dans la prévisualisation d’un modèle gLTF, assurez-vous qu’ils sont correctement nommés et qu’ils se trouvent dans un dossier `textures` situé dans le même dossier racine que le modèle, comme suit :

    Asset (folder)
    model.gltf
    model.bin
    textures (folder)
    material_0_baseColor.jpeg
    material_0_normal.jpeg

## Considérations de performance lors de la prévisualisation de ressources 3D dans AEM {#performance-3d-previewing-assets}

Le temps d’ouverture d’un fichier 3D dans la page d’affichage des détails du fichier dépend de plusieurs facteurs, tels que la bande passante, la complexité de l’image et les latences sur le serveur.

De plus, les capacités de l’ordinateur client, par exemple un poste de travail, un ordinateur portable ou un appareil mobile tactile, doivent être prises en compte lorsque vous manipulez la caméra de manière interactive. Un système relativement puissant avec de bonnes capacités graphiques peut rendre l’expérience interactive d’affichage en 3D plus fluide et plus favorable.

**Pour prévisualiser des ressources 3D dans AEM**

1. Assurez-vous d’avoir chargé des ressources 3D dans AEM.
Consultez [Formats pris en charge pour la prévisualisation 3D](#supported-3d-previewing-assets) et [Téléchargement de ressources](/help/assets/manage-assets.md#uploading-assets).
1. Dans AEM, sur la page de **[!UICONTROL navigation]**, appuyez sur **[!UICONTROL Ressources > Fichiers.]**

   ![Page de navigation](/help/assets/assets-dm/navigation-assets.png)

1. Près du coin supérieur droit de la page, dans la liste déroulante Affichage, appuyez sur **[!UICONTROL Affichage carte]**, puis accédez au fichier 3D à prévisualiser.

   ![Sélection de carte 3D](/help/assets/assets-dm/3d-card-select.png)
   _En mode Affichage carte, appuyez sur la carte du fichier 3D à prévisualiser._

1. Appuyez sur la carte de la ressource 3D pour l’ouvrir sur la page des détails de la ressource.

   ![Prévisualisation 3D interactive](/help/assets/assets-dm/3d-preview.png)
   _Prévisualisation interactive d’un fichier 3D dans la page d’affichage des détails du fichier._
1. Sur la page d’affichage des détails de la ressource 3D, effectuez l’une des opérations suivantes :
   * **Tournez votre appareil photo** : faites tourner votre angle de vue autour de la scène et des objets 3D.
      * _Souris_ : cliquez avec le bouton gauche et faites glisser.
      * _Écran tactile_ : appuyez sur un seul doigt et faites glisser.
   * **Panoramique** : basculez votre angle de vue vers la gauche, la droite, le haut ou le bas.
      * _Souris_ : cliquez avec le bouton droit et faites glisser.
      * _Écran tactile_ : appuyez avec deux doigts et faites glisser.
   * **Zoom** : permet de zoomer pour déplacer l’appareil dans et hors des zones de la scène 3D.
      * _Souris_ : roulette de défilement.
      * _Écran tactile_ : rapprocher les deux doigts.
   * **Recentrer** : recentrez l’angle de vue sur un point d’un objet de la scène 3D.
      * _Souris_ : double-cliquez.
      * _Écran tactile_ : appuyez deux fois.
   * **Réinitialiser** : près du coin inférieur droit de la page, appuyez sur l’icône Réinitialiser pour rétablir le point d’affichage cible au centre du fichier 3D. De plus, Réinitialiser rapproche ou éloigne l’angle de vue pour afficher la ressource dans son intégralité et à une taille raisonnable.
   * **Mode Plein écran** : pour passer en mode Plein écran, dans le coin inférieur droit de la page, appuyez sur l’icône Plein écran.

1. Lorsque vous avez terminé, en haut à droite de la page, appuyez sur **[!UICONTROL Fermer.]**
