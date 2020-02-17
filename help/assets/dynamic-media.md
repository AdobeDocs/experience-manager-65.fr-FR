---
title: Utilisation de Dynamic Media
description: Découvrez comment utiliser Dynamic Media pour diffuser des ressources pour une utilisation sur le web, les appareils mobiles et les réseaux sociaux.
uuid: 4dc0f436-d20e-4e8b-aeff-5515380fa44d
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: introduction
content-type: reference
discoiquuid: a8063d43-923a-42ac-9a16-0c7fadd8f73f
translation-type: tm+mt
source-git-commit: 0595d89409e0ca21f771be5c55c3ec9548a8449f

---


# Utilisation de Dynamic Media {#working-with-dynamic-media}

[Dynamic Media](https://www.adobe.com/solutions/web-experience-management/dynamic-media.html) fournit des ressources visuelles de marchandisage et de marketing à la demande, automatiquement dimensionnées pour une utilisation sur le Web, les appareils mobiles et les réseaux sociaux. A partir d’un ensemble de ressources, Dynamic Media génère et diffuse en temps réel plusieurs variantes d’un même contenu enrichi par le biais de son réseau mondial et évolutif, aux performances optimisées.

Dynamic Media permet un affichage interactif, notamment le zoom, la rotation à 360° et la vidéo. Dynamic Media incorpore de manière unique les processus de la gestion des actifs numériques d’Adobe Experience Manager pour simplifier et rationaliser le processus de gestion des campagnes numériques.

>[!NOTE]
>
>Un article de la communauté (en anglais) intitulé [Working with Adobe Experience Manager and Dynamic Media](https://helpx.adobe.com/experience-manager/using/aem_dynamic_media.html) porte sur l’utilisation d’Adobe Experience Manager et de Dynamic Media.

## Tâches que vous pouvez effectuer avec Dynamic Media {#what-you-can-do-with-dynamic-media}

Dynamic Media permet de gérer les ressources avant de les publier. L’utilisation générale des ressources est décrite en détail à la rubrique [Utilisation de ressources numériques](managing-assets-touch-ui.md). Les rubriques générales incluent le chargement, le téléchargement, la modification et la publication des ressources, l’affichage et la modification des propriétés et la recherche de ressources.

Les fonctionnalités Contenu multimédia dynamique uniquement sont les suivantes :

* [Bannières de carrousel](carousel-banners.md)
* [Visionneuses d’images](image-sets.md)
* [Images interactives](interactive-images.md)
* [Vidéos interactives](interactive-videos.md)
* [Visionneuses de supports variés](mixed-media-sets.md)
* [Images panoramiques](panoramic-images.md)

* [Visionneuses à 360°](spin-sets.md)
* [Vidéo](video.md)
* [Diffusion de ressources Dynamic Media](delivering-dynamic-media-assets.md)
* [Gestion des ressources](managing-assets.md)
* [Utilisation d’aperçus rapides pour créer des fenêtres contextuelles personnalisées](custom-pop-ups.md)

Voir également [Configuration de Dynamic Media](administering-dynamic-media.md).

>[!NOTE]
>
>Pour comprendre les différences entre l’utilisation de Contenu multimédia dynamique et l’intégration de Contenu multimédia dynamique classique avec AEM, voir Intégration de Contenu multimédia [dynamique classique et Contenu multimédia](/help/sites-administering/scene7.md#aem-scene-integration-versus-dynamic-media)dynamique.

## Contenu multimédia dynamique activé ou Contenu multimédia dynamique désactivé {#dynamic-media-on-versus-dynamic-media-off}

Vous pouvez déterminer si la fonction Contenu multimédia dynamique est activée en fonction des caractéristiques suivantes :

* Des rendus dynamiques sont disponibles lors du téléchargement ou de la prévisualisation de fichiers.
* Des visionneuses d’images, des visionneuses à 360°, des visionneuses de supports mixtes sont disponibles.
* Des rendus PTIFF sont créés.

When you click an image asset, the view of the asset is different with Dynamic Media [enabled](config-dynamic.md#enabling-dynamic-media). Dynamic Media utilise les visionneuses HTML5 à la demande.

### Dynamic renditions {#dynamic-renditions}

Des rendus dynamiques, tels que des paramètres d’image et de visionneuse prédéfinis (sous **[!UICONTROL Dynamique]**), sont disponibles lorsque Dynamic Media est activé.

![chlimage_1-358](assets/chlimage_1-358.png)

### Visionneuses d’images, à 360° et de supports variés {#image-sets-spins-sets-mixed-media-sets}

Des visionneuses d’images, à 360° et de supports variés sont disponibles lorsque Dynamic Media est activé.

![chlimage_1-359](assets/chlimage_1-359.png)

### PTIFF renditions {#ptiff-renditions}

Dynamic media enabled assets include `pyramid.tiffs`.

![chlimage_1-360](assets/chlimage_1-360.png)

### Modification des vues des ressources {#asset-views-change}

With Dynamic Media enabled, you can zoom in and out by clicking the `+` and `-` buttons. You can also click/tap to zoom into certain area. Revert brings you to the original version and you can make the image full screen by clicking the diagonal arrows. Dynamic Media enabled looks like this:

![chlimage_1-361](assets/chlimage_1-361.png)

Avec Contenu multimédia dynamique désactivé, vous pouvez effectuer un zoom avant ou arrière et rétablir la taille d’origine :

![chlimage_1-362](assets/chlimage_1-362.png)
