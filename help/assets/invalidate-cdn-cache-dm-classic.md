---
title: Invalidation du cache de réseau CDN par le biais de Dynamic Media Classic
description: L’invalidation du contenu mis en cache sur le réseau de Diffusion de contenu (CDN) vous permet de mettre rapidement à jour les ressources fournies par Dynamic Media Classic, plutôt que d’attendre l’expiration du cache.
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5.5/ASSETS
topic-tags: dynamic-media
content-type: reference
translation-type: tm+mt
source-git-commit: f786b35e77c6b862f7fc6e45d3d0af56a51e3e95
workflow-type: tm+mt
source-wordcount: '700'
ht-degree: 81%

---


# Invalidation du cache de réseau CDN par le biais de Dynamic Media Classic {#invalidating-your-cdn-cached-content}

Les ressources Dynamic Media sont mises en cache par le réseau CDN en vue d’une diffusion rapide. Cependant, lorsque vous appliquez des mises à jour à une ressource, vous pouvez faire en sorte qu’elles soient prises immédiatement en compte. L’invalidation du contenu de réseau de diffusion de continu (CDN) en cache vous permet de mettre à jour rapidement les ressources diffusées par Dynamic Media, au lieu d’attendre l’expiration du cache.

>[!IMPORTANT]
>
>Les étapes suivantes s’appliquent uniquement à Dynamic Media dans AEM 6.5, Service Pack 5 (AEM 6.5.5) ou version antérieure.<br>Si vous utilisez Dynamic Media dans AEM 6.5, Service Pack 6 (AEM 6.5.6) ou une version ultérieure, suivez les étapes décrites dans  [Invalidation du cache CDN par Dynamic Media.](/help/assets/invalidate-cdn-cache-dynamic-media.md)

Voir aussi [Présentation du cache dans Dynamic Media Classic (Scene7)](https://helpx.adobe.com/fr/experience-manager/scene7/kb/base/caching-questions/scene7-caching-overview.html).

**Pour invalider le cache CDN au moyen de Dynamic Media Classic :**

1. Ouvrez l&#39;[application de bureau Dynamic Media Classic](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/intro/dynamic-media-classic-desktop-app.html?lang=en#system-requirements-dmc-app), puis connectez-vous à votre compte.

   Vos informations d’identification et de connexion vous ont été communiquées par Adobe au moment de la configuration. Si vous ne disposez pas de ces informations, contactez l’assistance technique.

1. Près du coin supérieur droit de la page, appuyez sur **[!UICONTROL Configuration > Configuration de l’application > Paramètres généraux.]**
1. Recherchez la zone de texte **[!UICONTROL Modèle d’invalidation sur le réseau de diffusion de contenu]** dans la section Serveurs de la page Paramètres généraux de l’application.

1. Précisez le modèle utilisé pour invalider le cache du réseau de diffusion de contenu (CDN).

   Supposons, par exemple, que vous saisissiez une URL d’image (comprenant des paramètres d’image prédéfinis et des modificateurs) faisant référence à `<ID>`, au lieu d’un ID d’image spécifique, comme dans l’exemple suivant :

   `https://server.com/is/image/Company/<ID>?$product$`

   Si le modèle contient uniquement `<ID>`, Dynamic Media renseigne `https://<server>/is/image`, où `<server>` désigne le nom du serveur de publication défini dans les paramètres généraux et où &lt;ID> correspond au(x) ressources(s) dont la validité doit être annulée.

1. Dans le coin inférieur droit de la page, cliquez sur **[!UICONTROL Fermer.]**
1. Dans l’interface utilisateur de Dynamic Media Classic, sélectionnez un ou plusieurs fichiers, puis cliquez sur **[!UICONTROL Fichier > Invalider le CDN.]** La liste qui s’affiche alors se compose d’une ou de plusieurs URL générées à partir du modèle que vous avez créé et de la ou des ressources que vous avez sélectionnées. Elle utilise l’URL du serveur répertoriée sous « Nom du serveur de publication » dans les paramètres généraux de l’application.

   Par exemple, avec le modèle d’invalidation défini à l’étape précédente, supposons que vous sélectionniez une seule image de ressource nommée `Backpack_B`. Lorsque vous cliquez sur **[!UICONTROL Fichier > Invalider sur le réseau de diffusion de contenu]**, l’URL suivante est générée dans l’interface utilisateur d’invalidation sur le réseau de diffusion de contenu :

   `https://server.com/is/image/Company/Backpack_B?$product$`

1. Dans la zone Liste d’URL, cliquez sur **[!UICONTROL Continuer]** pour effacer le cache de chaque URL spécifique. Notez que vous pouvez modifier une URL ou en ajouter une en la saisissant ou en la copiant dans la zone Liste d’URL ; il n’est pas nécessaire de définir le modèle d’invalidation sur le réseau de diffusion de contenu au préalable.

   Après avoir cliqué sur **[!UICONTROL Continuer]**, un indicateur s’affiche pour vous donner une estimation de la durée nécessaire pour effacer le cache.

   Si vous avez sélectionné plusieurs ressources, puis cliqué sur **[!UICONTROL Fichier > Invalider sur le réseau de diffusion de contenu]**, chaque ressource est référencée dans l’**[!UICONTROL URL du modèle enregistrée.]** Par conséquent, vous pouvez définir un **[!UICONTROL modèle d’invalidation sur le réseau de diffusion de contenu]** faisant référence à chaque URL de paramètre d’image prédéfini qui figure sur votre site web (comme les détails d’un produit, les résultats de la recherche, etc.). Par la suite, lorsque vous sélectionnerez une ou plusieurs images à invalider dans le cache, les URL seront automatiquement renseignées dans l’interface.

   >[!NOTE]
   >
   >Lorsque vous sélectionnez des ressources, puis cliquez sur **[!UICONTROL Fichier > Invalider sur le réseau de diffusion de contenu]**, Dynamic Media utilise un modèle d’invalidation pour créer automatiquement des URL à invalider dans le réseau de diffusion de contenu. Si rien n’est renseigné dans la zone de texte **[!UICONTROL Modèle d’invalidation sur le réseau de diffusion de contenu]**, la liste d’URL renvoyée est vide. La mise en cache sur le réseau de diffusion de contenu n’est pas basée sur les ressources ; elle est basée sur des URL. Il est donc nécessaire de connaître les URL complètes qui se trouvent sur votre site web. Dès que vous avez déterminé ces URL, vous pouvez les ajouter dans la zone de texte **[!UICONTROL Modèle d’invalidation sur le réseau de diffusion de contenu]** (voir les étapes précédentes). Vous pouvez ensuite sélectionner ces ressources et invalider les URL en une seule étape.
   >
   >Une autre option consiste à ajouter des URL complètes dans la liste **[!UICONTROL Invalider sur le réseau de diffusion de contenu]**. Si vous optez pour cette méthode, il n’est pas nécessaire de sélectionner des ressources dans Dynamic Media Classic avant d’accéder à l’option **[!UICONTROL Fichier > Invalider sur le réseau de diffusion de contenu]**.

