---
title: Invalidation du cache du réseau de diffusion de contenu par le biais de Dynamic Media Classic
description: L’invalidation du contenu en cache du réseau de diffusion de continu (CDN) vous permet de mettre à jour rapidement les ressources diffusées par Dynamic Media, au lieu d’attendre l’expiration du cache.
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5.5/ASSETS
topic-tags: dynamic-media
content-type: reference
feature: CDN Cache,Dynamic Media Classic
role: User, Admin
exl-id: 7020343a-b556-4091-9717-93fcc55e623b
solution: Experience Manager, Experience Manager Assets
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '716'
ht-degree: 100%

---

# Invalidation du cache du réseau de diffusion de contenu par le biais de Dynamic Media Classic {#invalidating-your-cdn-cached-content}

Les ressources Dynamic Media sont mises en cache par le réseau de diffusion de contenu (CDN) pour une diffusion rapide. Cependant, lorsque vous appliquez des mises à jour à une ressource, vous pouvez faire en sorte qu’elles soient prises immédiatement en compte. L’invalidation du CDN en cache vous permet de mettre à jour rapidement les ressources diffusées par Dynamic Media, au lieu d’attendre l’expiration du cache.

>[!NOTE]
>
>Cette fonctionnalité nécessite l’utilisation du réseau CDN prêt à l’emploi fourni avec Adobe Experience Manager Dynamic Media. Aucun autre réseau CDN personnalisé n’est pris en charge avec cette fonctionnalité.

>[!IMPORTANT]
>
>Les étapes suivantes s’appliquent uniquement à Dynamic Media dans Adobe Experience Manager 6.5, Service Pack 5 (Experience Manager 6.5.5) ou version antérieure.<br>Si vous utilisez Dynamic Media dans le pack de services 6 d’Experience Manager 6.5 (Experience Manager 6.5.6) ou une version ultérieure, suivez les étapes décrites dans la section [Invalidation du cache CDN via Dynamic Media](/help/assets/invalidate-cdn-cache-dynamic-media.md).

<!-- REMOVED MARCH 28, 2022 BECAUSE OF 404; NO REDIRECT WAS PUT IN PLACE BY SUPPORT See also [Cache overview in Dynamic Media Classic (Scene7)](https://helpx.adobe.com/experience-manager/scene7/kb/base/caching-questions/scene7-caching-overview.html). -->

**Invalidation du cache du réseau CDN par le biais de Dynamic Media Classic :**

1. Ouvrez [l’application de bureau Dynamic Media Classic](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/intro/dynamic-media-classic-desktop-app.html?lang=fr#system-requirements-dmc-app) puis connectez-vous à votre compte.

   Vos informations d’identification et de connexion vous ont été communiquées par Adobe au moment de la configuration. Si vous ne possédez pas ces informations, contactez l’assistance clientèle d’Adobe.

1. Dans le coin supérieur droit de la page, accédez à **[!UICONTROL Configuration]** > **[!UICONTROL Configuration de l’application]** > **[!UICONTROL Paramètres généraux]**.
1. Recherchez la zone de texte **[!UICONTROL Modèle d’invalidation sur le réseau de diffusion de contenu]** dans la section Serveurs de la page Paramètres généraux de l’application.

1. Précisez le modèle utilisé pour invalider le cache du réseau de diffusion de contenu (CDN).

   Supposons, par exemple, que vous saisissiez une URL d’image (comprenant des paramètres d’image prédéfinis et des modificateurs) faisant référence à `<ID>`, au lieu d’un ID d’image spécifique, comme dans l’exemple suivant :

   `https://server.com/is/image/Company/<ID>?$product$`

   Si le modèle contient uniquement `<ID>`, Dynamic Media renseigne `https://<server>/is/image`, où `<server>` désigne le nom du serveur de publication défini dans les paramètres généraux et où &lt;ID> correspond aux ressources dont la validité doit être annulée.

1. Dans le coin inférieur droit de la page, sélectionnez **[!UICONTROL Fermer]**.
1. Dans l’interface utilisateur de Dynamic Media Classic, sélectionnez une ou plusieurs ressources, puis accédez à **[!UICONTROL Fichier]** > **[!UICONTROL Invalider le CDN]**. La liste qui s’affiche alors se compose d’une ou de plusieurs URL générées à partir du modèle que vous avez créé et des ressources que vous avez sélectionnées. Elle utilise l’URL du serveur répertoriée sous « Nom du serveur de publication » dans les paramètres généraux de l’application.

   Par exemple, avec le modèle d’invalidation défini à l’étape précédente, supposons que vous sélectionniez une seule image de ressource nommée `Backpack_B`. Lorsque vous accédez à **[!UICONTROL Fichier]** > **[!UICONTROL Invalider sur le réseau CDN]**, l’URL suivante est générée dans l’interface utilisateur d’invalidation sur le réseau CDN :

   `https://server.com/is/image/Company/Backpack_B?$product$`

1. Dans la zone Liste d’URL, sélectionnez **[!UICONTROL Continuer]** pour effacer le cache de chaque URL spécifique. Vous pouvez modifier une URL ou en ajouter une en la saisissant ou en la copiant dans la zone Liste d’URL ; il n’est pas nécessaire de définir le modèle d’invalidation sur le réseau de diffusion de contenu au préalable.

   Après avoir sélectionné **[!UICONTROL Continuer]**, un indicateur s’affiche pour vous donner une estimation de la durée nécessaire pour effacer le cache.

   Si vous avez sélectionné plusieurs ressources, puis accédé à **[!UICONTROL Fichier]** > **[!UICONTROL Invalider sur le réseau CDN]**, chaque ressource est référencée dans l’**[!UICONTROL URL du modèle]** enregistrée. Par conséquent, vous pouvez définir un **[!UICONTROL modèle d’invalidation sur le réseau de diffusion de contenu]** faisant référence à chaque URL de paramètre prédéfini d’image qui figure sur votre site web comme les détails d’un produit et les résultats de recherche. Par la suite, lorsque vous sélectionnerez une ou plusieurs images à invalider dans le cache, les URL seront automatiquement renseignées dans l’interface.

   >[!NOTE]
   >
   >Lorsque vous sélectionnez des ressources, puis cliquez sur **[!UICONTROL Fichier]** > **[!UICONTROL Invalider le CDN]**, Dynamic Media utilise un modèle d’invalidation pour créer automatiquement des URL à invalider dans le réseau de diffusion de contenu. Si rien n’est renseigné dans la zone de texte **[!UICONTROL Modèle d’invalidation sur le réseau de diffusion de contenu]**, la liste d’URL renvoyée est vide. La mise en cache sur le réseau de diffusion de contenu n’est pas basée sur les ressources ; elle est basée sur des URL. Il est donc nécessaire de connaître les URL complètes qui se trouvent sur votre site web. Dès que vous avez déterminé ces URL, vous pouvez les ajouter dans la zone de texte **[!UICONTROL Modèle d’invalidation sur le réseau de diffusion de contenu]** (voir les étapes précédentes). Vous pouvez ensuite sélectionner ces ressources et invalider les URL en une seule étape.
   >
   >Une autre option consiste à ajouter des URL complètes dans la liste **[!UICONTROL Invalider sur le réseau de diffusion de contenu]**. Si vous optez pour cette méthode, il n’est pas nécessaire de sélectionner des ressources dans Dynamic Media Classic avant d’accéder à l’option **[!UICONTROL Fichier > Invalider sur le réseau de diffusion de contenu]**.
