---
title: Prévisualisation de fichiers 3D
description: Découvrez comment prévisualiser des ressources 3D
contentOwner: Rick Brough
docset: aem65
feature: Ressources 3D
role: Business Practitioner
exl-id: fdebbc2b-c04d-4cdd-b7c2-8e9a2a854e79
source-git-commit: 666bc5d943af371726708cb2ef157a9b3f07eb8e
workflow-type: tm+mt
source-wordcount: '553'
ht-degree: 65%

---

# Prévisualisation de ressources 3D dans Adobe Experience Manager{#previewing-3d-assets-aem}

Experience Manager prend en charge le téléchargement, la diffusion et l’aperçu interactif des ressources 3D dans le cadre du processus de création.

La visionneuse 3D interactive est disponible à partir de la page des détails de la ressource dans Experience Manager. La visionneuse comprend, entre autres, un ensemble de contrôles de caméra interactifs qui permettent d’orbiter, de zoomer et de faire un panoramique sur la ressource 3D.

<!-- See also [Working with 3D assets in Dynamic Media](/help/assets/assets-3d.md). -->

## Formats pris en charge pour l’aperçu 3D en Experience Manager {#supported-3d-previewing-assets}

L’aperçu 3D interactif prend en charge les formats de fichier suivants :

| Extension de fichier 3D | Format de fichier | Type MIME | Remarques |
|---|---|---|---|
| GLB | Transmission GL binaire | model/gltf-binary |  |
| GLTF | Format de transmission GL | model/gltf+json | Consultez **la remarque** ci-dessous. |
| OBJ | Fichier d’objet 3D WaveFront | application/x-tgif |  |
| STL | Stéréolithographie | application/vnd.ms-pki.stl |  |
| DN | Adobe Dimension | model/x-adobe-dn | Prise en charge de l’assimilation uniquement, prévisualisation non disponible. |
| USDZ | Fichier zip de description de scène universelle | model/vnd.usdz+zip | Prise en charge de l’assimilation uniquement, prévisualisation non disponible. |

>[!NOTE]
>
>Si les matériaux ne sont pas rendus dans l’aperçu d’un modèle gLTF, assurez-vous qu’ils sont correctement nommés et dans un dossier `textures` dans le même dossier racine que le modèle, comme suit :

    Asset (folder)
    model.gltf
    model.bin
    textures (folder)
    material_0_baseColor.jpeg
    material_0_normal.jpeg

## Considérations de performance lors de la prévisualisation de ressources 3D en Experience Manager{#performance-3d-previewing-assets}

Le temps d’ouverture d’un fichier 3D dans la page d’affichage des détails du fichier dépend de plusieurs facteurs, tels que la bande passante, la complexité de l’image et les latences sur le serveur.

De plus, les capacités de l’ordinateur client, par exemple un poste de travail, un ordinateur portable ou un appareil mobile tactile, doivent être prises en compte lorsque vous manipulez la caméra de manière interactive. Un système relativement puissant avec de bonnes capacités graphiques peut rendre l’expérience interactive d’affichage en 3D plus fluide et plus favorable.

**Pour prévisualiser des ressources 3D dans Experience Manager :**

1. Assurez-vous d’avoir chargé des ressources 3D dans Experience Manager.
Consultez [Formats pris en charge pour la prévisualisation 3D](#supported-3d-previewing-assets) et [Téléchargement de ressources](/help/assets/manage-assets.md#uploading-assets).
1. Dans Experience Manager, sur la page **[!UICONTROL Navigation]**, appuyez sur **[!UICONTROL Ressources > Fichiers.]**

   ![Page de navigation](/help/assets/assets-dm/navigation-assets.png)

1. Près du coin supérieur droit de la page, dans la liste déroulante Mode, appuyez sur **[!UICONTROL Mode Carte]**, puis accédez au fichier 3D à prévisualiser.

   ![Sélection de carte 3D](/help/assets/assets-dm/3d-card-select.png)
   _En mode Carte, appuyez sur la carte du fichier 3D à prévisualiser._

1. Appuyez sur la carte de la ressource 3D.

   ![Prévisualisation 3D interactive](/help/assets/assets-dm/3d-preview.png)
   _Prévisualisation interactive d’un fichier 3D dans la page d’affichage des détails du fichier._
1. Sur la page d’affichage des détails de la ressource 3D, effectuez l’une des opérations suivantes :

   | Mode | Description | Action de souris | Action de l’écran tactile |
   | --- | --- | --- | --- |
   | **Tournez votre appareil photo** | Faites tourner la vue autour de la scène 3D et des objets. | Cliquez avec le bouton gauche et faites glisser. | Appuyez sur un seul doigt et faites glisser. |
   | **Panoramique** | Faites défiler votre vue vers la gauche, la droite, le haut ou le bas. | Cliquez avec le bouton droit de la souris et faites glisser. | Appuyez avec deux doigts et faites glisser. |
   | **Zoom sur la caméra** | Se déplacer dans et hors des zones de la scène 3D. | Roue de défilement. | Pincement à deux doigts. |
   | **Recréez votre appareil photo** | Recentrez l’angle de vue sur un point d’un objet de la scène 3D. | Double-cliquer. | Double appui. |
   | **Réinitialiser** | Dans le coin inférieur droit de la page, appuyez sur l’icône Réinitialiser pour rétablir le point d’affichage cible au centre de la ressource 3D. De plus, Réinitialiser rapproche ou éloigne l’angle de vue pour afficher la ressource dans son intégralité et à une taille raisonnable. |  |  |
   | **Mode Plein écran** | Pour passer en mode Plein écran, dans le coin inférieur droit de la page, appuyez sur l’icône Plein écran. |  |  |

1. Lorsque vous avez terminé, en haut à droite de la page, appuyez sur **[!UICONTROL Fermer.]**
