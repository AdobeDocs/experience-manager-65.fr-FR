---
title: Annulation de la validité du contenu mis en cache dans le réseau de diffusion de contenu (CDN)
description: L’annulation de la validité du contenu CDN en cache vous permet de mettre à jour rapidement les ressources diffusées par Dynamic Media, au lieu d’attendre l’expiration du cache.
uuid: 0fd88e31-9745-4c98-a245-9f5d0766cad4
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
discoiquuid: e6c9b50b-c27c-48bf-b3c0-9994e7bf6d7e
translation-type: tm+mt
source-git-commit: 0595d89409e0ca21f771be5c55c3ec9548a8449f

---


# Annulation de la validité du contenu mis en cache dans le réseau de diffusion de contenu (CDN) {#invalidating-your-cdn-cached-content}

Les ressources Dynamic Media sont mises en cache par le réseau CDN en vue d’une diffusion rapide. Cependant, lorsque vous appliquez des mises à jour à une ressource, vous pouvez faire en sorte qu’elles soient prises immédiatement en compte. L’annulation de la validité du contenu CDN en cache vous permet de mettre à jour rapidement les ressources diffusées par Dynamic Media, au lieu d’attendre l’expiration du cache.

Voir aussi Présentation du [cache dans Dynamic Media Classic (Scene7)](https://helpx.adobe.com/experience-manager/scene7/kb/base/caching-questions/scene7-caching-overview.html).

**Pour annuler la validité du contenu CDN mis en cache, procédez comme suit :** 

1. Connectez-vous à votre compte Dynamic Media Classic (Scene7) :

   [https://www.adobe.com/marketing-cloud/experience-manager/scene7-login.html](https://www.adobe.com/marketing-cloud/experience-manager/scene7-login.html)

   Vos informations d’identification et de connexion vous ont été communiquées par Adobe au moment de la configuration. Si vous ne disposez pas de ces informations, contactez l’assistance technique.

1.  Cliquez sur **[!UICONTROL Configuration > Configuration de l’application > Paramètres généraux]**.
1. Recherchez la zone de texte **[!UICONTROL Modèle d’invalidation sur le réseau de diffusion de contenu]** dans la section Serveurs de la page Paramètres généraux de l’application.

1. Précisez le modèle utilisé pour invalider le cache du réseau de diffusion de contenu (CDN).

   For example, suppose you enter an image URL (including image presets or modifiers) referencing `<ID>`, instead of a specific image ID as in the following example:

   `https://server.com/is/image/Company/<ID>?$product$`

   If the Template just contains `<ID>`, then Dynamic Media fills in `https://<server>/is/image` where `<server>` is the Publish Server Name that is defined in General Settings and &lt;ID> is the asset(s) selected to be invalidated.

1. Dans le coin inférieur droit de la page, cliquez sur **[!UICONTROL Fermer]**.
1. Dans l’interface utilisateur de Dynamic Media Classic (Scene7), sélectionnez une ou plusieurs ressources, puis cliquez sur **[!UICONTROL Fichier > Invalider sur le réseau de diffusion de contenu]**. La liste qui s’affiche alors se compose d’une ou de plusieurs URL générées à partir du modèle que vous avez créé et de la ou des ressources que vous avez sélectionnées. Elle utilise l’URL du serveur répertoriée sous « Nom du serveur de publication » dans les paramètres généraux de l’application.

   Par exemple, avec le modèle d’invalidation défini à l’étape précédente, supposons que vous sélectionniez une seule image de ressource nommée `Backpack_B`. Lorsque vous cliquez sur **[!UICONTROL Fichier > Invalider sur le réseau de diffusion de contenu]**, l’URL suivante est générée dans l’interface utilisateur d’invalidation sur le réseau de diffusion de contenu :

   `https://server.com/is/image/Company/Backpack_B?$product$`

1. Dans la zone Liste d’URL, cliquez sur **[!UICONTROL Continuer]** pour effacer le cache de chaque URL spécifique. Notez que vous pouvez modifier une URL ou en ajouter une en la saisissant ou en la copiant dans la zone Liste d’URL ; il n’est pas nécessaire de définir le modèle d’invalidation sur le réseau de diffusion de contenu au préalable.

   Après avoir cliqué sur **[!UICONTROL Continuer]**, un indicateur s’affiche pour vous donner une estimation de la durée nécessaire pour effacer le cache.

   Si vous avez sélectionné plusieurs ressources, puis cliqué sur **[!UICONTROL Fichier > Invalider sur le réseau de diffusion de contenu]****[!UICONTROL , chaque ressource est référencée dans l’URL du modèle enregistrée]**. Therefore, you can define a **[!UICONTROL CDN Invalidate Template]** referencing each URL image preset that is referenced on your website (such as product detail, search results, and so forth). Par la suite, lorsque vous sélectionnerez une ou plusieurs images à invalider dans le cache, les URL seront automatiquement renseignées dans l’interface.

   >[!NOTE]
   >
   >Lorsque vous sélectionnez des ressources, puis cliquez sur **[!UICONTROL Fichier > Invalider sur le réseau de diffusion de contenu]**, Dynamic Media utilise un modèle d’invalidation pour créer automatiquement des URL à invalider dans le réseau de diffusion de contenu. If there is nothing in the **[!UICONTROL CDN Invalidate Template]** text box, then you get a blank URL list. La mise en cache dans le réseau de diffusion de contenu n’est pas basée sur les ressources, mais sur les URL. Par conséquent, il convient de connaître les URL complètes qui figurent sur votre site web. After you determine those URLs, you can add them to the **[!UICONTROL Invalidate CDN Template]** text box earlier in the steps. Vous pouvez ensuite sélectionner ces ressources et invalider les URL en une seule étape.
   >
   >Another option is to add complete URLs to the **[!UICONTROL Invalidate CDN]** list. Si vous optez pour cette méthode, il n’est pas nécessaire de sélectionner des ressources dans Dynamic Media Classic avant d’accéder à l’option **[!UICONTROL Fichier > Invalider sur le réseau de diffusion de contenu]**.

