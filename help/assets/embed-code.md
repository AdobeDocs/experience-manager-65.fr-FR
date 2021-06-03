---
title: Intégration de la visionneuse de vidéos ou d’images Dynamic Media dans une page web
description: Découvrez comment intégrer des images ou des vidéos Dynamic Media dans une page web
uuid: 6f786521-eb6c-4c80-8c15-9bf97b56818f
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
discoiquuid: 4ae76d8a-208f-4099-9f17-a94df424685e
feature: Visionneuses
role: Business Practitioner, Administrator
exl-id: 203ea349-ef4c-421c-b4b6-76ee9d46ec34
source-git-commit: b1e0ea01688095b29d8fb18baf6fa0bda660dad5
workflow-type: tm+mt
source-wordcount: '375'
ht-degree: 91%

---

# Intégration de la visionneuse de vidéos ou d’images Dynamic Media, ou de la visionneuse dimensionnelle dans une page web {#embedding-the-video-or-image-viewer-on-a-web-page}

Utilisez la fonction **[!UICONTROL Code incorporé]** lorsque vous souhaitez lire une vidéo ou afficher une ressource incorporée dans une page web. Vous copiez le code incorporé dans le Presse-papiers afin de le coller dans vos pages web. Vous ne pouvez pas modifier le code dans la boîte de dialogue **[!UICONTROL Code incorporé]**.

Vous n’incorporez les URL que si vous *et non* utilisez Adobe Experience Manager comme système de gestion de contenu web. Si vous utilisez Experience Manager comme gestion de contenu web, [vous ajoutez les ressources directement sur votre page](adding-dynamic-media-assets-to-pages.md).

Voir [Liaison d’URL à une application web](linking-urls-to-yourwebapplication.md).

Consultez aussi [Diffusion d’images optimisées pour un site réactif](responsive-site.md).

>[!NOTE]
>
>Le code incorporé n’est pas disponible pour la copie tant que vous n’avez pas publié la ressource sélectionnée. En outre, vous devez également publier le paramètre de visionneuse prédéfini ou le paramètre d’image prédéfini.
>
>Voir [Publication de ressources](publishing-dynamicmedia-assets.md).
>
>Voir [Publication de paramètres de visionneuse prédéfinis](managing-viewer-presets.md#publishing-viewer-presets).
>
>Voir [Publication de paramètres d’image prédéfinis](managing-image-presets.md#publishing-image-presets).

**Intégration de la visionneuse de vidéos ou d’images Dynamic Media dans une page web:**

1. Accédez à la ressource vidéo ou d’image *publiée* dont vous souhaitez copier le code incorporé.

   N’oubliez pas que le code incorporé n’est disponible à la copie *qu’après* la première *publication* des ressources. En outre, le paramètre de visionneuse prédéfini ou le paramètre d’image prédéfini doit également être publié.

   Voir [Publication de ressources](publishing-dynamicmedia-assets.md).

   Voir [Publication de paramètres de visionneuse prédéfinis](managing-viewer-presets.md#publishing-viewer-presets).

   Voir [Publication de paramètres d’image prédéfinis](managing-image-presets.md#publishing-image-presets).

1. Dans le rail de gauche, sélectionnez le menu déroulant et cliquez ou appuyez ensuite sur **[!UICONTROL Visionneuses]**.
1. Dans le rail de gauche, appuyez sur un nom de paramètre prédéfini de la visionneuse. Le paramètre de visionneuse prédéfini est appliqué à la ressource.
1. Appuyez sur **[!UICONTROL Incorporer]**.
1. Dans la boîte de dialogue **[!UICONTROL Code intégré]**, copiez l’ensemble du code dans le Presse-papiers, puis appuyez sur **[!UICONTROL Fermer]**.
1. Collez le code intégré dans vos pages web.

## Utilisation de HTTP/2 pour diffuser vos ressources Dynamic Media {#using-http-to-deliver-your-dynamic-media-assets}

HTTP/2 est le nouveau protocole web qui améliore la manière dont les serveurs et les navigateurs communiquent. Il permet un transfert rapide d’informations et réduit la puissance de traitement nécessaire. Les ressources Dynamic Media peuvent désormais être diffusées sur HTTP/2, un protocole qui garantit de meilleurs temps de réponse et de chargement.

Voir [Diffusion du contenu sur HTTP2](http2.md) pour tout savoir sur l’utilisation du protocole HTTP/2 avec votre compte Dynamic Media.
