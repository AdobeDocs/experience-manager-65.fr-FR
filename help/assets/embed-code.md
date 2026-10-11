---
title: Incorporation de la visionneuse de vidéos ou d’images Dynamic Media, ou de la visionneuse dimensionnelle dans une page web
description: Découvrez comment incorporer des images 3D, des images ou des vidéos Dynamic Media dans une page web.
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
feature: Viewers
role: User, Admin
exl-id: 203ea349-ef4c-421c-b4b6-76ee9d46ec34
solution: Experience Manager, Experience Manager Assets
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: d09181b5-a36a-43de-ba01-36641440bc43
    internal-label: Experience Manager Assets
feature_v2:
  - id: bd0d2470-932c-4269-8eca-6d939b72d9ef
    internal-label: Dynamic Media
subfeature_v2:
  - id: d17d085a-e808-49dd-b9a6-85a996b999bd
    internal-label: Viewers
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '385'
ht-degree: 91%
---
# Incorporation de la visionneuse de vidéos ou d’images Dynamic Media, ou de la visionneuse dimensionnelle dans une page web {#embedding-the-video-or-image-viewer-on-a-web-page}

Utilisez la fonction **[!UICONTROL Code incorporé]** lorsque vous souhaitez lire une vidéo ou afficher une ressource incorporée dans une page web. Vous copiez le code intégré dans le presse-papiers pour pouvoir le coller dans vos pages web. La modification du code n’est pas autorisée dans la boîte de dialogue **[!UICONTROL Code intégré]**.

Vous devez incorporer les URL uniquement si vous *n’utilisez pas* Adobe Experience Manager comme outil de gestion de contenu web. Dans le cas contraire, [vous pouvez ajouter les ressources directement à votre page](adding-dynamic-media-assets-to-pages.md).

Voir [Liaison d’URL à une application web](linking-urls-to-yourwebapplication.md).

Consultez [Diffusion d’images optimisées pour un site réactif](responsive-site.md).

>[!NOTE]
>
>Vous ne pouvez pas copier le code intégré tant que la ressource sélectionnée n’a pas été publiée. En outre, vous devez également publier le paramètre de visionneuse prédéfini ou le paramètre d’image prédéfini.
>
>Consultez la section [Publication de ressources](publishing-dynamicmedia-assets.md).
>
>Voir [Publication de paramètres de visionneuse prédéfinis](managing-viewer-presets.md#publishing-viewer-presets).
>
>Voir [Publication de paramètres d’image prédéfinis](managing-image-presets.md#publishing-image-presets).

**Pour incorporer la visionneuse de vidéos ou d’images ou la visionneuse dimensionnelle Dynamic Media dans une page Web :**

1. Accédez à la ressource vidéo ou d’image *publiée* dont vous souhaitez copier le code intégré.

   N’oubliez pas que le code intégré n’est disponible à la copie qu’*après* la première *publication* des ressources. En outre, le paramètre de visionneuse prédéfini ou le paramètre d’image prédéfini doit également être publié.

   Consultez la section [Publication de ressources](publishing-dynamicmedia-assets.md).

   Voir [Publication de paramètres de visionneuse prédéfinis](managing-viewer-presets.md#publishing-viewer-presets).

   Voir [Publication de paramètres d’image prédéfinis](managing-image-presets.md#publishing-image-presets).

1. Dans le rail de gauche, sélectionnez le menu déroulant et sélectionnez ensuite **[!UICONTROL Visionneuses]**.
1. Dans le rail de gauche, sélectionnez un nom de paramètre prédéfini de la visionneuse. Le paramètre de visionneuse prédéfini est appliqué à la ressource.
1. Sélectionnez **[!UICONTROL Incorporer]**.
1. Dans la boîte de dialogue **[!UICONTROL Code intégré]**, copiez l’ensemble du code dans le Presse-papiers, puis sélectionnez **[!UICONTROL Fermer]**.
1. Collez le code intégré dans vos pages web.

## Utilisation de HTTP/2 pour diffuser vos ressources Dynamic Media {#using-http-to-deliver-your-dynamic-media-assets}

HTTP/2 est le nouveau protocole Web mis à jour qui améliore la communication entre les navigateurs et les serveurs. Il permet un transfert plus rapide des informations et réduit la puissance de traitement nécessaire. Les ressources Dynamic Media peuvent désormais être diffusées sur HTTP/2, un protocole qui garantit de meilleurs temps de réponse et de chargement.

Voir [Diffusion du contenu sur HTTP2](http2.md) pour tout savoir sur l’utilisation du protocole HTTP/2 avec votre compte Dynamic Media.
