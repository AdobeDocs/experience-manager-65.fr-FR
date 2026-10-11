---
title: Diffusion de ressources Dynamic Media
description: Découvrez comment diffuser des ressources Dynamic Media, telles que des vidéos et des images, sur vos pages web.
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
docset: aem65
role: User, Admin
exl-id: 274af114-845a-46bd-b091-802cf589687a
feature: Asset Management,Renditions
solution: Experience Manager, Experience Manager Assets
autotag-review: '2026-05-18T18:45:05.823Z'
TQID: 'https://experienceleague.adobe.com/a5ifneRAYCIMHKCGJHGQu9aoQt3EWZu1hiGYItlPZOE'
product_v2:
  - id: e14eb250-3c22-4a07-9061-a78112b2b826
    internal-label: Experience Manager 6.5
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: d09181b5-a36a-43de-ba01-36641440bc43
    internal-label: Experience Manager Assets
feature_v2:
  - id: 7d2b2ec8-499c-5434-9ffd-9218cd71f683
    internal-label: Asset Management
  - id: ac365bec-0634-4744-9473-c42f47320593
    internal-label: Asset management and governance
subfeature_v2:
  - id: e42ab83e-8918-43a7-98a3-62bebbd5bb3a
    internal-label: Renditions
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
level_v2:
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
    internal-label: Beginner
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
    internal-label: Intermediate
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '324'
ht-degree: 92%
---
# Diffusion de ressources Dynamic Media{#delivering-dynamic-media-assets}

La diffusion des ressources Dynamic Media (vidéos et images) dépend de la mise en œuvre de votre site web.

Avec Dynamic Media, vous disposez de plusieurs options :

* Si votre site web est hébergé sur Adobe Experience Manager, vous souhaiterez ajouter les ressources Dynamic Media directement à votre page.
* Si votre site web n’est pas sur Experience Manager, les possibilités suivantes s’offrent à vous :

  * Incorporation de votre vidéo ou image sur votre site Web.
  * Liez des URL à votre application web. Utilisez la liaison lorsque vous souhaitez diffuser un lecteur vidéo dans une fenêtre pop-up ou modale.
  * Si votre site est réactif, vous pouvez [diffuser des images optimisées](/help/assets/responsive-site.md).

>[!NOTE]
>
>L’imagerie dynamique fonctionne avec vos paramètres d’image prédéfinis et utilise des informations à la dernière milliseconde de la diffusion pour réduire davantage encore la taille du fichier d’image en fonction de la vitesse de connexion du réseau et du navigateur. Voir [Imagerie numérique](/help/assets/imaging-faq.md) pour plus d’informations.

Pour plus d’informations, reportez-vous aux rubriques suivantes :

* [Ajout de ressources Dynamic Media aux pages Web](/help/assets/adding-dynamic-media-assets-to-pages.md)
* [Incorporation de la visionneuse de vidéos ou d’images dans une page web](/help/assets/embed-code.md)
* [Activation de la protection de lien dynamique dans Dynamic Media](/help/assets/hotlink-protection.md)
* [Liaison d’URL à votre application Web](/help/assets/linking-urls-to-yourwebapplication.md)
* [Diffusion d’images optimisées pour un site réactif](/help/assets/responsive-site.md)
* [Diffusion de contenu HTTP2](/help/assets/http2.md)
* [Invalidation de votre cache de réseau CDN au moyen de Dynamic Media Classic](/help/assets/invalidate-cdn-cache-dm-classic.md)
* [Utilisation de jeux de règles de transformation d’URL](/help/assets/using-rulesets-to-transform-urls.md)


## Diffusion de ressources Dynamic Media via HTTP/2 {#http-delivery-of-dynamic-media-assets}

Experience Manager prend à présent en charge la diffusion de tout le contenu Dynamic Media (images et vidéo) sur HTTP/2. En d’autres termes, une URL publiée ou un code intégré pour l’image ou la vidéo peut être intégré à toute application qui accepte une ressource hébergée. Cette ressource publiée est ensuite diffusée au moyen du protocole HTTP/2. Cette méthode de distribution améliore la communication entre les navigateurs et les serveurs, ce qui permet d’améliorer les temps de réponse et de chargement de toutes vos ressources Dynamic Media.

Pour en savoir plus, consultez la [Foire aux questions sur la diffusion HTTP/2 du contenu](/help/sites-administering/scene7-http2faq.md).
