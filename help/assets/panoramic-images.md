---
title: Images panoramiques
description: Découvrez comment utiliser les images panoramiques dans Dynamic Media.
uuid: ced3e5bd-93c8-4d5f-a397-1380d4d0a5e7
contentOwner: Rick Brough
topic-tags: dynamic-media
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
content-type: reference
discoiquuid: 632a9074-b747-49a1-a57d-1f42bba1f4e9
docset: aem65
feature: Panoramic Images,Asset Management
role: User, Admin
exl-id: 4d6fbeb1-94db-4154-9e41-b76033fb4398
source-git-commit: 363e5159d290ecfbf4338f6b9793e11b613389a5
workflow-type: tm+mt
source-wordcount: '574'
ht-degree: 49%

---

# Images panoramiques {#panoramic-images}

Cette section décrit comment utiliser la visionneuse d’images panoramiques pour le rendu d’images panoramiques sphériques afin de profiter d’une expérience de visionnage immersive à 360° d’une pièce, d’une propriété, d’un lieu ou d’un paysage.

Voir aussi [Gestion des paramètres prédéfinis de visionneuse](/help/assets/managing-viewer-presets.md).

![panoramic-image2](assets/panoramic-image2.png)

## Téléchargement de ressources pour une utilisation avec la visionneuse d’images panoramiques {#uploading-assets-for-use-with-the-panoramic-image-viewer}

Pour qu’une ressource téléchargée soit une image panoramique sphérique utilisable avec la visionneuse d’images panoramiques, la ressource doit présenter l’une ou l’autre des caractéristiques suivantes, ou les deux :

* Un rapport d’aspect de 2.
Vous pouvez remplacer le paramètre de rapport d’aspect par défaut de 2 en CRXDE Lite à l’emplacement suivant :
   `/conf/global/settings/cloudconfigs/dmscene7/jcr:content`

* Avec les mots-clés `equirectangular`, ou `spherical` et `panorama`, ou `spherical` et `panoramic`. Voir [Utilisation des balises](/help/sites-authoring/tags.md).

Les critères de format et de mots-clés s’appliquent tous deux aux ressources panoramiques pour la page des détails des ressources et le composant WCM `Panoramic Media`.

Pour charger des ressources à utiliser avec la visionneuse d’images panoramiques, voir [Chargement de ressources](/help/assets/manage-assets.md#uploading-assets).

## Configuration de Dynamic Media Classic {#configuring-dynamic-media-classic-scene}

Pour que la visionneuse d’images panoramiques fonctionne correctement dans Adobe Experience Manager, synchronisez les paramètres prédéfinis de la visionneuse d’images panoramiques avec les métadonnées spécifiques à Dynamic Media Classic et Dynamic Media Classic afin que les paramètres prédéfinis de la visionneuse soient mis à jour dans le JCR. Pour accomplir cette synchronisation, configurez Dynamic Media Classic comme suit :

1. Ouvrez [l’application de bureau Dynamic Media Classic](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html?lang=fr#getting-started) puis connectez-vous à votre compte.

1. Dans le coin supérieur droit de la page, sélectionnez **[!UICONTROL Configuration]** > **[!UICONTROL Configuration de l’application]** > **[!UICONTROL Configuration de la publication]** > **[!UICONTROL Serveur d’images]**.
1. Sur la page Publication sur hébergeur d’images, dans le menu déroulant **[!UICONTROL Contexte de publication]** près de la partie supérieure, sélectionnez **[!UICONTROL Image Serving]**.

1. Sur la même page Publication sur hébergeur d’images, localisez l’en-tête **[!UICONTROL Attributs de requête]**.
1. Sous l’en-tête Attributs de requête, localisez **[!UICONTROL Limite de taille de l’image de réponse]**. Ensuite, dans les champs Largeur et Hauteur associés, augmentez la taille maximale autorisée pour les images panoramiques.

   Dynamic Media Classic est limitée à 25 000 000 pixels. La taille maximale autorisée pour les images avec un rapport d’aspect de 2:1 est de 7 000 x 3 500. Toutefois, pour des écrans d’ordinateurs de bureau habituels, une taille de 4 096 x 2 048 pixels suffit.

   >[!NOTE]
   >
   >Seules les images qui respectent la taille d’image maximale autorisée sont prises en charge. Les demandes d’images dont la taille est supérieure à la limite de taille génèrent une réponse 403.

1. Sous l’en-tête Attributs de requête, procédez comme suit :

   * Définissez Mode d’obscurcissement de requête sur **[!UICONTROL Désactivé]**.
   * Définissez Mode de verrouillage de requête sur **[!UICONTROL Désactivé]**.

   Ces paramètres sont nécessaires pour utiliser la variable `Panoramic Media` Composant WCM en Experience Manager.

1. Au bas de la page Publication sur hébergeur d’images, sur le côté gauche, sélectionnez **[!UICONTROL Enregistrer]**.

1. Dans le coin inférieur droit, sélectionnez **[!UICONTROL Fermer]**.

### Résolution des problèmes du composant WCM de média panoramique {#troubleshooting-the-panoramic-media-wcm-component}

Si vous avez déposé une image dans le composant Média panoramique de votre WCM et que l’espace réservé du composant est réduit, résolvez les problèmes suivants :

* Si vous rencontrez une erreur 403 Interdit, cela peut être dû à la taille d’image demandée trop grande. Consultez la section **[!UICONTROL Limite de taille de l’image de réponse]** paramètres dans [Configuration de Dynamic Media Classic](/help/assets/panoramic-images.md#configuring-dynamic-media-classic-scene).

* En cas d’erreur « Verrou incorrect » ou « Erreur d’analyse » sur la page, vérifiez que Mode d’obscurcissement de requête de vérification et Mode de verrouillage de requête sont désactivés.
* Pour une erreur de canevas taché, configurez un chemin d’accès au fichier de définition de l’ensemble de règles et invalidez le CTN pour les demandes précédentes de la ressource image.
* Si la qualité de l’image devient faible après une demande d’image dont le dimensionnement est supérieur à la limite prise en charge, vérifiez que la variable **[!UICONTROL Attributs de codage du JPEG > Qualité]** n’est pas vide. Un paramètre standard pour la variable **[!UICONTROL Qualité]** est `95`. Vous trouverez le paramètre sur la page Publication sur hébergeur d’images. Pour accéder à la page, voir [Configuration de Dynamic Media Classic](/help/assets/panoramic-images.md#configuring-dynamic-media-classic-scene).

## Prévisualisation des images panoramiques {#previewing-panoramic-images}

Voir [Aperçu des ressources](/help/assets/previewing-assets.md).

## Publication des images panoramiques {#publishing-panoramic-images}

Voir [Publication de ressources](/help/assets/publishing-dynamicmedia-assets.md).
