---
title: 'Diffusion de contenu HTTP/2  '
description: HTTP/2 améliore la communication entre les navigateurs et les serveurs, ce qui accélère le transfert d’informations tout en réduisant la quantité de puissance de traitement nécessaire.
uuid: d9deb945-bdf5-4d6b-95c8-8bae4442e618
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
discoiquuid: c8e145ad-f021-4043-8190-62151775e296
role: Business Practitioner, Administrator
exl-id: 9eb9f309-33e5-4694-84d2-fb2cd3de50a6
feature: Publishing,Configuration
translation-type: tm+mt
source-git-commit: c9aec973faf4caef741961d92a6f258646aeddb7
workflow-type: tm+mt
source-wordcount: '726'
ht-degree: 52%

---

# DIFFUSION HTTP/2 du contenu {#http-delivery-of-content}

Adobe est heureux d’annoncer la disponibilité de HTTP/2 pour la diffusion de contenu, protocole qui permet d’améliorer les performances globales.

>[!NOTE]
>
>Cette fonctionnalité nécessite l’utilisation du CDN prêt à l’emploi fourni avec Adobe Experience Manager Dynamic Media. Aucun autre CDN personnalisé n’est pris en charge avec cette fonctionnalité.

## Qu’est-ce que le HTTP/2 ? {#what-is-http}

Le HTTP/2 améliore la communication entre les navigateurs et les serveurs, en accélérant le transfert d’informations tout en réduisant la puissance de traitement nécessaire.

Le site web ci-dessous décrit simplement HTTP/2 et les avantages qu’il procure :

[https://www.engadget.com/2015/02/24/what-you-need-to-know-about-http-2/](https://www.engadget.com/2015/02/24/what-you-need-to-know-about-http-2/)

## Quels sont les principaux avantages à la transition vers HTTP/2 pour la diffusion de contenu ? {#what-are-the-key-benefits-of-moving-to-http-for-content-delivery}

L&#39;amélioration des performances peut varier considérablement. Il est basé sur de nombreux facteurs tels que le code de votre site Web, la manière dont vous utilisez Dynamic Media, le périphérique, l’écran et l’emplacement du client.

Les tests d’Adobe ont donné les résultats suivants :

* Pour les images, le temps de réponse s’est amélioré de 7 % à 28 % selon l’appareil et le navigateur. Les gains de performance les plus notables ont été enregistrés sur les appareils iOS.
* Pour les visionneuses, les performances en matière de temps de chargement ont augmenté de 15 %.

La démonstration suivante illustre la différence entre le chargement HTTP/1 et le chargement HTTP/2 :

[https://http2.akamai.com/demo](https://http2.akamai.com/demo)

## Puis-je passer à HTTP/2 ? {#am-i-eligible-to-switch-over-to-http}

Pour utiliser HTTP/2, vous devez satisfaire aux exigences suivantes :

* Utilisez le protocole HTTPS sécurisé pour vos demandes de médias riches.
* Utilisez le CDN de lots Adobe (réseau de diffusion de contenu) dans le cadre de votre licence Dynamic Media.
* Utilisez un domaine dédié (autre que company-h.assetsadobe#.com).

   Si vous disposez déjà d&#39;un domaine dédié, vous pouvez opt-in par le biais du support technique.

   Si vous ne disposez pas d’un domaine dédié, l’Adobe prévoit de programmer votre transition sur HTTP/2 en 2018.

## Quel est le processus d’activation de HTTP/2 pour mon compte Dynamic Media ? {#what-is-the-process-for-enabling-http-for-my-dynamic-media-account}

Vous lancez la demande de basculement sur HTTP/2 ; ce n&#39;est pas automatiquement fait pour vous.

1. Pour passer à HTTP/2, lancez une demande de service à la clientèle Adobe. Voir [Accès au portail d’assistance AEM](https://helpx.adobe.com/fr/experience-manager/kb/accessing-aem-support-portal.html).

   1. Indiquez les informations suivantes dans votre demande de support :

      1. nom, adresse électronique et numéro de téléphone du contact principal.
      1. Tous les domaines à passer à HTTP/2.
      1. Vérifiez que vous utilisez le protocole HTTPS sécurisé pour les demandes de média enrichi.
      1. Vérifiez que vous utilisez le CDN par Adobe et que vous n’êtes pas géré avec une relation directe.
      1. Vérifiez que vous utilisez un domaine dédié. Si vous utilisez Dynamic Media, vous utilisez alors un domaine dédié.
   1. Le service d’assistance clientèle vous ajoute à la liste d’attente des clients HTTP/2 en fonction de l’ordre dans lequel les demandes ont été envoyées.
   1. Lorsque l’Adobe est prêt à traiter votre demande, le service à la clientèle vous contacte pour coordonner la transition et définir une date de cible.
   1. Vous êtes averti une fois terminé et pouvez vérifier la transition réussie sur HTTP2.

      Le navigateur ne détecte pas cette transition, il est donc nécessaire de télécharger une extension.

      Pour Firefox et Chrome, il existe une extension appelée &quot;HTTP/2 et indicateur SPDY&quot;. Les navigateurs ne prennent en charge HTTP/2 qu’en mode sécurisé. Par conséquent, appelez une URL avec le protocole HTTPS pour vérifier. Si http/2 est pris en charge, il est indiqué par l’extension sous la forme d’un symbole de Flash bleu et d’un en-tête &quot;X-Firefox-Spdy&quot; : &quot;h2&quot;.


## Quand puis-je espérer passer à HTTP/2 ? {#when-can-i-expect-to-be-transitioned-over-to-http}

Les demandes sont traitées dans l’ordre dans lequel elles sont reçues par le service d’assistance clientèle.

>[!NOTE]
>
>Il peut y avoir un long délai car la transition à HTTP/2 implique de vider le cache. Par conséquent, seules quelques transitions client peuvent être traitées simultanément.

## Quels risques présente la transition vers HTTP/2 ?  {#what-are-the-risks-with-moving-to-http}

La transition vers HTTP/2 efface le cache au niveau du CDN, car elle implique la définition d’une nouvelle configuration de CDN.

Le contenu non mis en cache atteint directement les serveurs Adobe d’origine jusqu’à ce que le cache soit reconstruit. Ainsi, l&#39;Adobe prévoit de gérer quelques transitions client à la fois afin de maintenir des performances acceptables lors de l&#39;extraction des demandes de l&#39;origine.

## Comment puis-je vérifier si une URL ou un site web est activé avec HTTP/2 ?  {#how-can-you-verify-whether-a-url-or-website-is-activated-with-http}

Le navigateur ne détecte pas cette transition, il est donc nécessaire de télécharger une extension.

Pour Firefox et Chrome, il existe une extension appelée &quot;HTTP/2 et indicateur SPDY&quot;. Les navigateurs ne prennent en charge HTTP/2 qu’en mode sécurisé. Par conséquent, appelez une URL avec le protocole HTTPS pour vérifier. Si http/2 est pris en charge, il est indiqué par l’extension sous la forme d’un symbole de Flash bleu et d’un en-tête `X-Firefox-Spdy` : `h2`.
