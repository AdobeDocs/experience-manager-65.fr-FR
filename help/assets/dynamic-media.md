---
title: Utiliser Dynamic Media
description: Découvrez comment utiliser le logiciel afin de diffuser des ressources pour les sites web, mobiles et de réseaux sociaux.
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: introduction
content-type: reference
role: User, Admin
exl-id: f8a80b22-b1a6-475f-b3f1-b2f47822f21d
feature: Collaboration,Asset Management
solution: Experience Manager, Experience Manager Assets
source-git-commit: d6b9dde5201198cb073293b2b8527a458836ff0b
workflow-type: ht
source-wordcount: '416'
ht-degree: 100%

---

# Utiliser Dynamic Media {#working-with-dynamic-media}

[Dynamic Media](https://business.adobe.com/fr/products/experience-manager/assets/dynamic-media.html) fournit des ressources visuelles de marchandisage et de marketing à la demande, automatiquement dimensionnées pour une utilisation sur les sites web, mobiles et de réseaux sociaux. À partir d’un ensemble de ressources de sources originales, le logiciel génère et diffuse en temps réel plusieurs variantes d’un même contenu enrichi par le biais de son réseau mondial et évolutif, aux performances optimisées.

Le logiciel offre des expériences de visionnage interactives, notamment des fonctions vidéo, de zoom et de rotation à 360°. Il incorpore de manière unique les workflows de la gestion des ressources numériques d’Adobe Experience Manager pour simplifier et rationaliser le processus de gestion des campagnes numériques.

<!-- >ARTICLE IS MISSING. GIVES 404 [!NOTE]
>
>A Community article is available on [Working with Adobe Experience Manager and Dynamic Media](https://helpx.adobe.com/experience-manager/using/aem_dynamic_media.html). -->

## Ce que vous pouvez effectuer avec le logiciel : {#what-you-can-do-with-dynamic-media}

Le logiciel vous permet de gérer les ressources avant de les publier. L’utilisation générale des ressources est décrite en détail à la rubrique [Utilisation de ressources numériques](manage-assets.md). Les rubriques générales incluent le chargement, le téléchargement, la modification et la publication des ressources, l’affichage et la modification des propriétés et la recherche de ressources.

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
* [Création de pop-ups personnalisés à l’aide de l’aperçu rapide](custom-pop-ups.md)

Consultez également [Configuration de Dynamic Media](administering-dynamic-media.md).

>[!NOTE]
>
>Pour comprendre les différences entre l’utilisation de Dynamic Media et l’intégration de Dynamic Media Classic à Adobe Experience Manager, consultez [Intégration de Dynamic Media Classic et Dynamic Media](/help/sites-administering/scene7.md#aem-scene-integration-versus-dynamic-media).

## Dynamic Media activé ou Dynamic Media désactivé {#dynamic-media-on-versus-dynamic-media-off}

Les caractéristiques suivantes permettent de déterminer si le logiciel est activé ou non :

* Des rendus dynamiques sont disponibles lors du téléchargement ou de la prévisualisation des ressources.
* Des visionneuses d’images, à 360° et de supports variés sont disponibles.
* Des rendus PTIFF sont créés.

Lorsque vous cliquez sur une ressource image, l’affichage de la ressource est différent avec le logiciel [activé](config-dynamic.md#enabling-dynamic-media). Il utilise les visionneuses HTML5 à la demande.

### Rendus dynamiques {#dynamic-renditions}

Des rendus dynamiques, tels que des paramètres d’image et de visionneuse prédéfinis (sous **[!UICONTROL Dynamique]**), sont disponibles lorsque le logiciel est activé.

![chlimage_1-358](assets/chlimage_1-358.png)

### Visionneuses d’images, à 360° et de supports variés {#image-sets-spins-sets-mixed-media-sets}

Des visionneuses d’images, à 360° et de supports variés sont disponibles lorsque le logiciel est activé.

![chlimage_1-359](assets/chlimage_1-359.png)

### Rendus PTIFF {#ptiff-renditions}

Les ressources compatibles avec Dynamic Media comprennent les `pyramid.tiffs`.

![chlimage_1-360](assets/chlimage_1-360.png)

### Modification des vues des ressources {#asset-views-change}

Lorsque le logiciel est activé, vous pouvez effectuer un zoom avant ou arrière en cliquant sur les boutons `+` et `-`. Vous pouvez également cliquer pour effectuer un zoom sur une zone spécifique. L’option Rétablir vous ramène à la version d’origine. Vous pouvez afficher l’image en plein écran en cliquant sur les flèches diagonales. Une fois le logiciel activé, cela ressemble à ce qui suit :

![chlimage_1-361](assets/chlimage_1-361.png)

Lorsque le logiciel est désactivé, vous pouvez effectuer un zoom avant et arrière et revenir à la taille d’origine :

![chlimage_1-362](assets/chlimage_1-362.png)
