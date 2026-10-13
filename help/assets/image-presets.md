---
title: Application de paramètres d’image prédéfinis Dynamic Media
description: Découvrez comment activer des ressources pour afficher des images selon des tailles et des formats différents, ou avec d’autres propriétés d’image générées dynamiquement.
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
feature: Image Presets
role: User,Admin
exl-id: 98d88b59-eb8f-42db-abb8-04506a5b8c30
solution: Experience Manager, Experience Manager Assets
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: d09181b5-a36a-43de-ba01-36641440bc43
    internal-label: Experience Manager Assets
feature_v2:
  - id: d4b6216b-4a89-4ff0-8ac0-5a699ba23100
    internal-label: Images and videos
subfeature_v2:
  - id: a16e03b7-8456-4383-8860-31ab5ab00e9e
    internal-label: Image presets
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '346'
ht-degree: 100%
---
# Application de paramètres d’image prédéfinis Dynamic Media {#applying-image-presets}

Les paramètres d’image prédéfinis permettent aux ressources d’afficher des images selon des tailles et des formats différents, ou avec d’autres propriétés d’image générées dynamiquement. Vous pouvez choisir un paramètre prédéfini lorsque vous exportez des images. Le paramètre prédéfini reformate les images selon les spécifications définies par votre administration.

Vous pouvez en outre sélectionner un paramètre d’image prédéfini réactif (signalé par le bouton **[!UICONTROL RESS]** une fois que vous l’avez sélectionné).

Cette section décrit comment utiliser les paramètres d’image prédéfinis. [L’administration peut créer et configurer des paramètres d’image prédéfinis](managing-image-presets.md).

>[!NOTE]
>
>L’imagerie dynamique fonctionne avec vos paramètres d’image prédéfinis et utilise des informations à la dernière milliseconde de la diffusion pour réduire davantage encore la taille du fichier d’image en fonction de la vitesse de connexion du réseau et du navigateur. Voir [Imagerie numérique](imaging-faq.md) pour plus d’informations.

Vous pouvez appliquer un paramètre d’image prédéfini à une image lorsque vous la prévisualisez.

>[!NOTE]
>
>Dans le mode Dynamic Media - Scene7, les paramètres d’image prédéfinis sont pris en charge uniquement pour les ressources d’image.

**Pour appliquer les paramètres d’image prédéfinis Dynamic Media :**

1. Ouvrez la ressource et, dans le rail de gauche, sélectionnez le menu déroulant, puis l’option **[!UICONTROL Rendus]**.

   >[!NOTE]
   >
   >* Les rendus statiques apparaissent dans la moitié supérieure du volet. Les rendus dynamiques apparaissent dans la moitié inférieure. Vous ne pouvez utiliser l’URL pour afficher l’image qu’avec les rendus dynamiques. Le bouton **[!UICONTROL URL]** n’apparaît que si vous sélectionnez un rendu dynamique. Le bouton **[!UICONTROL RESS]** s’affiche uniquement si vous sélectionnez un paramètre d’image prédéfini réactif.
   >
   >* Le système affiche plusieurs rendus lorsque vous sélectionnez **[!UICONTROL Rendus]** dans l’affichage des détails d’une ressource. Vous pouvez augmenter le nombre de paramètres prédéfinis visibles. Voir [Augmentation du nombre de paramètres d’image prédéfinis affichés](managing-image-presets.md#increasing-or-decreasing-the-number-of-image-presets-that-display).

   ![chlimage_1-208](assets/chlimage_1-208.png)

1. Procédez de l’une des manières suivantes :

   * Sélectionnez un rendu dynamique afin de pouvoir prévisualiser le paramètre d’image prédéfini.
   * Pour afficher la fenêtre pop-up, sélectionnez **[!UICONTROL URL]**, **[!UICONTROL Incorporer]** ou **[!UICONTROL RESS]**.

   >[!NOTE]
   >
   >Si la ressource *et* le paramètre d’image prédéfini ne sont pas encore publiés, le bouton **[!UICONTROL URL]** (ou les boutons **[!UICONTROL URL]** et **[!UICONTROL RESS]**, le cas échéant) n’est pas disponible.
   >
   >Notez également que les paramètres d’image prédéfinis sont automatiquement publiés sur un serveur Dynamic Media
