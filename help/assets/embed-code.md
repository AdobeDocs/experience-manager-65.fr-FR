---
title: Incorporation de la visionneuse de vidéos, d’images ou de dimensions Dynamic Media dans une page web
description: Découvrez comment incorporer des vidéos, des images ou des images 3D Dynamic Media dans une page web
uuid: 6f786521-eb6c-4c80-8c15-9bf97b56818f
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
discoiquuid: 4ae76d8a-208f-4099-9f17-a94df424685e
feature: Visionneuses
role: User, Admin
exl-id: 203ea349-ef4c-421c-b4b6-76ee9d46ec34
source-git-commit: f4b7566abfa0a8dbb490baa0e849de6c355a3f06
workflow-type: tm+mt
source-wordcount: '381'
ht-degree: 64%

---

# Incorporation de la visionneuse de vidéos, d’images ou de dimensions Dynamic Media dans une page web {#embedding-the-video-or-image-viewer-on-a-web-page}

Utilisez la fonction **[!UICONTROL Code incorporé]** lorsque vous souhaitez lire une vidéo ou afficher une ressource incorporée dans une page web. Vous copiez le code incorporé dans le Presse-papiers afin de le coller dans vos pages web. Vous ne pouvez pas modifier le code dans la boîte de dialogue **[!UICONTROL Code incorporé]**.

Vous devez incorporer les URL uniquement si vous *n’utilisez pas* Adobe Experience Manager comme outil de gestion de contenu web. Dans le cas contraire, [vous pouvez ajouter les ressources directement à votre page](adding-dynamic-media-assets-to-pages.md).

Voir [Liaison d’URL à une application web](linking-urls-to-yourwebapplication.md).

Voir [Diffuser des images optimisées pour un site réactif](responsive-site.md).

>[!NOTE]
>
>Le code incorporé n’est pas disponible pour la copie tant que vous n’avez pas publié la ressource sélectionnée. En outre, vous devez également publier le paramètre de visionneuse prédéfini ou le paramètre d’image prédéfini.
>
>Voir [Publication de ressources](publishing-dynamicmedia-assets.md).
>
>Voir [Publier les paramètres prédéfinis de la visionneuse](managing-viewer-presets.md#publishing-viewer-presets).
>
>Voir [Publication des paramètres d’image prédéfinis](managing-image-presets.md#publishing-image-presets).

**Pour incorporer la visionneuse de vidéos, d’images ou de dimensions Dynamic Media dans une page web :**

1. Accédez à la ressource vidéo ou d’image *publiée* dont vous souhaitez copier le code incorporé.

   N’oubliez pas que le code incorporé n’est disponible à la copie *qu’après* la première *publication* des ressources. En outre, le paramètre de visionneuse prédéfini ou le paramètre d’image prédéfini doit également être publié.

   Voir [Publication de ressources](publishing-dynamicmedia-assets.md).

   Voir [Publier les paramètres prédéfinis de la visionneuse](managing-viewer-presets.md#publishing-viewer-presets).

   Voir [Publication des paramètres d’image prédéfinis](managing-image-presets.md#publishing-image-presets).

1. Dans le rail de gauche, sélectionnez le menu déroulant et sélectionnez **[!UICONTROL Visionneuses]**.
1. Dans le rail de gauche, sélectionnez un nom de paramètre prédéfini de visionneuse. Le paramètre de visionneuse prédéfini est appliqué à la ressource.
1. Sélectionnez **[!UICONTROL Incorporer]**.
1. Dans la boîte de dialogue **[!UICONTROL Code incorporé]**, copiez le code entier dans le Presse-papiers, puis sélectionnez **[!UICONTROL Fermer]**.
1. Collez le code intégré dans vos pages web.

## Utilisation de HTTP/2 pour diffuser vos ressources Dynamic Media   {#using-http-to-deliver-your-dynamic-media-assets}

HTTP/2 est le nouveau protocole web qui améliore la manière dont les serveurs et les navigateurs communiquent. Il permet un transfert rapide d’informations et réduit la puissance de traitement nécessaire. Les ressources Dynamic Media peuvent désormais être diffusées sur HTTP/2, un protocole qui garantit de meilleurs temps de réponse et de chargement.

Voir [Diffusion du contenu sur HTTP2](http2.md) pour tout savoir sur l’utilisation du protocole HTTP/2 avec votre compte Dynamic Media.
