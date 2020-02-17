---
title: Incorporation de la visionneuse de vidéos ou d’images de médias dynamiques sur une page Web
description: Découvrez comment incorporer des vidéos ou des images de médias dynamiques dans une page Web
uuid: 6f786521-eb6c-4c80-8c15-9bf97b56818f
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
discoiquuid: 4ae76d8a-208f-4099-9f17-a94df424685e
translation-type: tm+mt
source-git-commit: 0595d89409e0ca21f771be5c55c3ec9548a8449f

---


# Embedding the Dynamic Media Video or Image viewer on a web page {#embedding-the-video-or-image-viewer-on-a-web-page}

Use the **[!UICONTROL Embed Code]** feature when you want to play the video or view an asset embedded on a web page. You copy the embed code to the clipboard so you can paste it in your web pages. Editing of the code is not permitted in the **[!UICONTROL Embed Code]** dialog box.

You embed URLs only if you are _not_ using AEM as your WCM. Dans le cas contraire, [vous pouvez ajouter les ressources directement à votre page.](adding-dynamic-media-assets-to-pages.md)

See [Linking URLs to your Web Application.](linking-urls-to-yourwebapplication.md)

See [Delivering Optimized Images for a Responsive Site.](responsive-site.md)

>[!NOTE]
>
>Le code incorporé n’est pas disponible pour la copie tant que vous n’avez pas publié la ressource sélectionnée. En outre, vous devez également publier le paramètre de visionneuse prédéfini ou le paramètre d’image prédéfini.
>
>Voir [Publication de ressources](publishing-dynamicmedia-assets.md).
>
>Voir [Publication de paramètres de visionneuse prédéfinis](managing-viewer-presets.md#publishing-viewer-presets).
>
>Voir [Publication de paramètres d’image prédéfinis](managing-image-presets.md#publishing-image-presets).

**Pour incorporer la visionneuse de vidéos ou d’images de médias dynamiques dans une page Web**

1. Navigate to the *published* video or image asset whose embed code you want to copy.

   N’oubliez pas que le code intégré ne peut être copié qu’*après* la *publication* des ressources. En outre, le paramètre de visionneuse prédéfini ou le paramètre d’image prédéfini doit également être publié.

   Voir [Publication de ressources](publishing-dynamicmedia-assets.md).

   Voir [Publication de paramètres de visionneuse prédéfinis](managing-viewer-presets.md#publishing-viewer-presets).

   Voir [Publication de paramètres d’image prédéfinis](managing-image-presets.md#publishing-image-presets).

1. In the left rail, select the drop-down menu and tap **[!UICONTROL Viewers]**.
1. Dans le rail de gauche, appuyez sur un nom de paramètre prédéfini de la visionneuse. Le paramètre de visionneuse prédéfini est appliqué à la ressource.
1. Appuyez sur **[!UICONTROL Incorporer]**.
1. In the **[!UICONTROL Embed Code]** dialog box, copy the entire code to the clipboard, and then tap **[!UICONTROL Close]**.
1. Collez le code intégré dans vos pages web.

## Utilisation de HTTP/2 pour diffuser vos ressources Dynamic Media {#using-http-to-deliver-your-dynamic-media-assets}

HTTP/2 est le nouveau protocole web qui améliore la manière dont les serveurs et les navigateurs communiquent. Il permet un transfert rapide d’informations et réduit la puissance de traitement nécessaire. Les ressources Dynamic Media peuvent désormais être diffusées sur HTTP/2, un protocole qui garantit de meilleurs temps de réponse et de chargement.

Voir [Diffusion du contenu sur HTTP/2](http2.md) pour tout savoir sur l’utilisation du protocole HTTP/2 avec votre compte Dynamic Media.
