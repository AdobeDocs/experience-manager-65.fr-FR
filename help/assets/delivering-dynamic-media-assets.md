---
title: Diffusion de ressources Dynamic Media
description: Découvrez comment diffuser des ressources Dynamic Media
uuid: 23eddf83-34f5-4aae-8b81-d1cd7a098a7e
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
discoiquuid: e3b44330-d476-49c6-b7ba-079d0d60e500
docset: aem65
translation-type: tm+mt
source-git-commit: 0595d89409e0ca21f771be5c55c3ec9548a8449f

---


# Diffusion de ressources Dynamic Media{#delivering-dynamic-media-assets}

La diffusion des ressources Dynamic Media (vidéos et images) dépend de la mise en œuvre de votre site web.

Avec Dynamic Media, vous disposez de plusieurs options :

* Si votre site web est hébergé sur AEM, vous souhaiterez ajouter les ressources Dynamic Media directement à votre page.
* Si votre site web n’est pas hébergé par AEM, les possibilités suivantes s’offrent à vous :

   * Intégration de votre vidéo ou image à votre site web.
   * Liez des URL à votre application Web. Utilisez la liaison lorsque vous souhaitez diffuser un lecteur vidéo comme fenêtre contextuelle ou modale.
   * Si votre site est réactif, vous pouvez [diffuser des images optimisées.](/help/assets/responsive-site.md)

>[!NOTE]
>
>L’imagerie dynamique fonctionne avec vos paramètres d’image prédéfinis et utilise des informations à la dernière milliseconde de diffusion pour réduire davantage encore la taille du fichier d’image en fonction de la vitesse de connexion du réseau et du navigateur. Voir [Imagerie numérique](/help/assets/imaging-faq.md) pour plus d’informations.

Pour plus d’informations, reportez-vous aux rubriques suivantes :

* [Ajout de ressources Dynamic Media aux pages web](/help/assets/adding-dynamic-media-assets-to-pages.md)
* [Incorporation de la visionneuse de vidéos ou d’images dans une page web](/help/assets/embed-code.md)
* [Activation de la protection de lien dynamique dans Dynamic Media](https://helpx.adobe.com/experience-manager/6-4/help/assets/hotlink-protection.html)
* [Liaison d’URL à une application web](/help/assets/linking-urls-to-yourwebapplication.md)
* [Diffusion d’images optimisées pour un site réactif](/help/assets/responsive-site.md)
* [Diffusion de contenu HTTP2](/help/assets/http2.md)
* [Invalidation de votre contenu CDN mis en cache](/help/assets/invalidate-cdn-cached-content.md)
* [Utilisation de règles de transformation d’URL](/help/assets/using-rulesets-to-transform-urls.md)

## Diffusion de ressources Dynamic Media via HTTP/2 {#http-delivery-of-dynamic-media-assets}

AEM prend à présent en charge la diffusion de tout le contenu Dynamic Media (images et vidéo) sur HTTP/2. En d’autres termes, une URL publiée ou un code intégré pour l’image ou la vidéo peut être intégré dans toute application acceptant une ressource hébergée. Cette ressource publiée est alors distribuée par le biais du protocole HTTP/2. Cette méthode de distribution améliore la communication entre les navigateurs et les serveurs, ce qui permet d’améliorer les temps de réponse et de chargement de toutes vos ressources Dynamic Media.

Pour en savoir plus, reportez-vous aux [Questions fréquentes sur la diffusion de contenu HTTP/2](/help/sites-administering/scene7-http2faq.md).
