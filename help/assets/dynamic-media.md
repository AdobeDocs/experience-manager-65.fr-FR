---
title: Utilisation de Dynamic Media
description: Découvrez comment utiliser Dynamic Media pour diffuser des ressources pour une utilisation sur le web, les appareils mobiles et les réseaux sociaux.
uuid: 4dc0f436-d20e-4e8b-aeff-5515380fa44d
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: introduction
content-type: reference
discoiquuid: a8063d43-923a-42ac-9a16-0c7fadd8f73f
role: User, Admin
exl-id: f8a80b22-b1a6-475f-b3f1-b2f47822f21d
feature: Collaboration,Asset Management
source-git-commit: f4b7566abfa0a8dbb490baa0e849de6c355a3f06
workflow-type: ht
source-wordcount: '0'
ht-degree: 100%

---

# Utilisation de Dynamic Media {#working-with-dynamic-media}

[Dynamic Media](https://business.adobe.com/fr/products/experience-manager/assets/dynamic-media.html) fournit des ressources visuelles de marchandisage et de marketing à la demande, automatiquement dimensionnées pour une utilisation sur le web, les appareils mobiles et les réseaux sociaux. À partir d’un ensemble de ressources de sources originales, Dynamic Media génère et diffuse en temps réel plusieurs variantes d’un même contenu enrichi par le biais de son réseau mondial et évolutif, aux performances optimisées.

Dynamic Media offre des expériences de visualisation interactives, notamment des fonctions vidéo, de zoom et de rotation à 360°. Cette fonctionnalité intègre de manière unique les processus de la solution de gestion des ressources numériques Adobe Experience Manager (Assets), afin de simplifier et rationaliser le processus de gestion des campagnes numériques.

<!-- >ARTICLE IS MISSING. GIVES 404 [!NOTE]
>
>A Community article is available on [Working with Adobe Experience Manager and Dynamic Media](https://helpx.adobe.com/experience-manager/using/aem_dynamic_media.html). -->

## Tâches que vous pouvez effectuer avec Dynamic Media {#what-you-can-do-with-dynamic-media}

Dynamic Media permet de gérer les ressources avant de les publier. L’utilisation générale des ressources est décrite en détail à la rubrique [Utilisation de ressources numériques](manage-assets.md). Les rubriques générales incluent le chargement, le téléchargement, la modification et la publication des ressources, l’affichage et la modification des propriétés et la recherche de ressources.

Les fonctionnalités uniquement incluses dans Dynamic Media sont les suivantes :

* [Bannières de carrousel](carousel-banners.md)
* [Visionneuses d’images](image-sets.md)
* [Images interactives](interactive-images.md)
* [Vidéos interactives](interactive-videos.md)
* [Visionneuses de médias mixtes](mixed-media-sets.md)
* [Images panoramiques](panoramic-images.md)

* [Visionneuses à 360°](spin-sets.md)
* [Vidéo](video.md)
* [Diffusion de ressources Dynamic Media](delivering-dynamic-media-assets.md)
* [Gestion des ressources](managing-assets.md)
* [Création de fenêtres contextuelles personnalisées à l’aide de l’aperçu rapide](custom-pop-ups.md)

Consultez également [Configuration de Dynamic Media](administering-dynamic-media.md).

>[!NOTE]
>
>Pour comprendre les différences entre l’utilisation de Dynamic Media et l’intégration de Dynamic Media Classic à Adobe Experience Manager, consultez [Intégration de Dynamic Media Classic et Dynamic Media](/help/sites-administering/scene7.md#aem-scene-integration-versus-dynamic-media).

## Dynamic Media activé ou Dynamic Media désactivé {#dynamic-media-on-versus-dynamic-media-off}

Les caractéristiques suivantes permettent de déterminer si Dynamic Media est activé ou non :

* Des rendus dynamiques sont disponibles lors du téléchargement ou de la prévisualisation des ressources.
* Des visionneuses d’images, à 360° et de supports variés sont disponibles.
* Des rendus PTIFF sont créés.

Lorsque vous cliquez sur une ressource image, l’affichage de la ressource est différent avec Dynamic Media [activé](config-dynamic.md#enabling-dynamic-media). Dynamic Media utilise les visionneuses HTML5 à la demande.

### Rendus dynamiques {#dynamic-renditions}

Des rendus dynamiques, tels que des paramètres d’image et de visionneuse prédéfinis (sous **[!UICONTROL Dynamique]**), sont disponibles lorsque Dynamic Media est activé.

![chlimage_1-358](assets/chlimage_1-358.png)

### Visionneuses d’images, à 360° et de supports variés {#image-sets-spins-sets-mixed-media-sets}

Des visionneuses d’images, à 360° et de supports variés sont disponibles lorsque Dynamic Media est activé.

![chlimage_1-359](assets/chlimage_1-359.png)

### Rendus PTIFF {#ptiff-renditions}

Les ressources compatibles avec Dynamic Media comprennent les `pyramid.tiffs`.

![chlimage_1-360](assets/chlimage_1-360.png)

### Modification des vues des ressources {#asset-views-change}

Lorsque Dynamic Media est activé, vous pouvez effectuer un zoom avant et arrière en cliquant sur les boutons `+` et `-`. Vous pouvez également cliquer/appuyer pour effectuer un zoom sur une zone spécifique. L’option Revenir à cette version rétablit la version originale, et vous pouvez afficher l’image en mode plein écran en cliquant sur les flèches diagonales. Lorsque Dynamic Media est activé, cette fonctionnalité ressemble à celle-ci :

![chlimage_1-361](assets/chlimage_1-361.png)

Lorsque Dynamic Media est désactivé, vous pouvez effectuer un zoom avant et arrière et revenir à la taille d’origine :

![chlimage_1-362](assets/chlimage_1-362.png)
