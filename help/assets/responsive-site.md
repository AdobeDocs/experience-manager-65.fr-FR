---
title: Diffusion d’images optimisées pour un site réactif
description: Utiliser la fonction de code réactif pour diffuser des images optimisées
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
feature: Asset Management
role: User, Admin
exl-id: 753d806f-5f44-4d73-a3a3-a2a0fc3e154b
solution: Experience Manager, Experience Manager Assets
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: d09181b5-a36a-43de-ba01-36641440bc43
    internal-label: Experience Manager Assets
feature_v2:
  - id: 7d2b2ec8-499c-5434-9ffd-9218cd71f683
    internal-label: Asset Management
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '343'
ht-degree: 100%
---
# Diffusion d’images optimisées pour un site réactif {#delivering-optimized-images-for-a-responsive-site}

Utilisez la fonctionnalité de code réactif lorsque vous souhaitez partager le code de diffusion réactive avec votre développeur web. Utilisez la fonctionnalité de code réactif (**[!UICONTROL RESS]**) lorsque vous souhaitez partager le code de diffusion réactive avec votre développeur web.

Cette fonction a un sens si votre site web se trouve sur un composant WCM tiers. Cependant, si votre site web se trouve plutôt sur Adobe Experience Manager, un serveur d’images hors site effectue le rendu de l’image et le communique à la page web.

Voir aussi [Incorporation de la visionneuse de vidéos dans une page web](embed-code.md).

Consultez également la section [Liaison d’URL à une application web](linking-urls-to-yourwebapplication.md).

**Pour diffuser des images optimisées pour un site réactif, procédez comme suit :**

1. Accédez à l’image pour laquelle vous voulez fournir du code réactif et, dans le menu déroulant, sélectionnez **[!UICONTROL Rendus]**.

   ![chlimage_1-408](assets/chlimage_1-408.png)

1. Sélectionnez un paramètre d’image prédéfini réactif. Les boutons **[!UICONTROL URL]** et **[!UICONTROL RESS]** apparaissent.

   ![chlimage_1-409](assets/chlimage_1-208.png)

   >[!NOTE]
   >
   >La ressource sélectionnée *et* le paramètre d’image prédéfini ou le paramètre de visionneuse prédéfini sélectionné doivent être publiés pour que le bouton **[!UICONTROL URL]** ou **[!UICONTROL RESS]** soit disponible.
   >
   >Le mode hybride de Dynamic Media nécessite de publier des paramètres d’image prédéfinis ; le mode Scene7 de Dynamic Media publie automatiquement les paramètres d’image prédéfinis.

1. Sélectionnez **[!UICONTROL RESS]**.

   ![chlimage_1-410](assets/chlimage_1-410.png)

1. Dans la boîte de dialogue **[!UICONTROL Incorporer une image réactive]**, sélectionnez et copiez le texte du code réactif et collez-le dans votre site web pour accéder au fichier réactif.
1. Modifiez les points d’arrêt par défaut dans le code intégré pour qu’ils correspondent aux points d’arrêt du site web réactif directement dans le code. Testez en outre les différentes résolutions d’image diffusées à différents points d’arrêt d’une page.

## Utilisation du protocole HTTP/2 pour diffuser vos ressources Dynamic Media {#using-http-to-delivery-your-dynamic-media-assets}

HTTP/2 est le nouveau protocole Web mis à jour qui améliore la communication entre les navigateurs et les serveurs. Il permet un transfert plus rapide des informations et réduit la puissance de traitement nécessaire. Les ressources Dynamic Media sont désormais prises en charge sur HTTP/2, un protocole qui garantit de meilleurs temps de réponse et de chargement.

Voir [Diffusion du contenu sur HTTP2](http2.md) pour tout savoir sur l’utilisation du protocole HTTP/2 avec votre compte Dynamic Media.
