---
title: Invalidation du cache CDN par le biais de Contenu multimédia dynamique
description: L’annulation de la validité du contenu CDN en cache vous permet de mettre à jour rapidement les ressources diffusées par Dynamic Media, au lieu d’attendre l’expiration du cache.
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5.6/ASSETS
topic-tags: dynamic-media
content-type: reference
translation-type: tm+mt
source-git-commit: 9e67e252348f471c052f6c3e88aea61d7a309241
workflow-type: tm+mt
source-wordcount: '305'
ht-degree: 16%

---


# Invalidation du cache CDN par le biais de Contenu multimédia dynamique {#invalidating-cdn-cache-for-dm-assets}

Les ressources Contenu multimédia dynamique sont mises en cache par le réseau CDN (Content Diffusion Network) pour une diffusion rapide à vos clients. Cependant, lorsque vous apportez des mises à jour à ces ressources, vous souhaiterez peut-être que ces modifications prennent effet immédiatement sur votre site Web. La purge ou l’invalidation du cache CDN vous permet de mettre rapidement à jour les fichiers distribués par Contenu multimédia dynamique. Au lieu d’attendre que le cache arrive à expiration à l’aide d’une valeur TTL (durée de vie) (10 heures par défaut), vous pouvez envoyer une demande à partir de Contenu multimédia dynamique pour que le cache arrive à expiration immédiatement.

>[!IMPORTANT]
>
>Ces étapes s’appliquent uniquement au mode Contenu multimédia dynamique - Scene7 dans AEM 6.5, Service Pack 6 ou version ultérieure. <!-- If you are using Dynamic Media in AEM 6.5, Service Pack 5 or earlier [use the steps found here](/help/assets/invalidate-cdn-cache-dm-classic.md). -->

See also [Caching overview in Dynamic Media](https://helpx.adobe.com/fr/experience-manager/scene7/kb/base/caching-questions/scene7-caching-overview.html).

**Pour invalider le contenu mis en cache sur le réseau de diffusion de contenu pour les ressources de médias dynamiques :**

1. Dans AEM version 6.5.6 ou ultérieure, appuyez sur **[!UICONTROL Outils > Actifs > Invalidation CDN.]**

   ![Fonction de validation CDN](/help/assets/assets-dm/cdn-invalidation-path.png)

1. Dans la page Invalidation CDN, définissez les options de votre choix :

   | Option | Description |
   | --- | --- |
   | **[!UICONTROL Invalider les paramètres d’image prédéfinis associés à la ressource dans le réseau de diffusion de contenu]** | Lorsque vous cochez cette option, vous pouvez sélectionner un ou plusieurs fichiers Contenu multimédia dynamique, quel que soit le type MIME, et les paramètres d’image prédéfinis associés pour invalidation du cache.<br>Bien que vous puissiez sélectionner un ou plusieurs dossiers contenant des ressources, l’Adobe ne recommande pas cette approche. Vous devez plutôt sélectionner des fichiers individuels.<br>Passez à l’étape suivante. |
   | **[!UICONTROL Invalidation basée sur un modèle]** | Lorsque vous cochez cette option, vous pouvez sélectionner les fichiers Contenu multimédia dynamique et le modèle d’invalidation que vous avez précédemment créé. Utilisez cette option avec |
   | **[!UICONTROL Ajouter des ressources]** | Blah |
   | **[!UICONTROL Ajouter une URL]** | Ajoutez manuellement des chemins d’URL complets aux fichiers Contenu multimédia dynamique dont vous souhaitez invalider le cache. |

1. 
1. Appuyez sur **[!UICONTROL Suivant.]**
1. 
