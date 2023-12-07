---
title: Diffusion de contenu HTTP2
description: Découvrez comment HTTP/2 améliore la communication entre les navigateurs et les serveurs, ce qui accélère le transfert des informations tout en réduisant la puissance de traitement nécessaire.
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
role: User, Admin
exl-id: 9eb9f309-33e5-4694-84d2-fb2cd3de50a6
feature: Publishing,Configuration
source-git-commit: 04050f31742c926b45235595f6318929d3767bd8
workflow-type: tm+mt
source-wordcount: '749'
ht-degree: 93%

---

# Diffusion de contenu HTTP/2 {#http-delivery-of-content}

Adobe est heureux d’annoncer la disponibilité de HTTP/2 pour la diffusion de contenu, protocole qui permet d’améliorer les performances globales.

>[!NOTE]
>
>Cette fonctionnalité nécessite l’utilisation du réseau CDN prêt à l’emploi fourni avec Adobe Experience Manager Dynamic Media. Aucun autre réseau CDN personnalisé n’est pris en charge avec cette fonctionnalité.

## Qu’est-ce que le HTTP/2 ?  {#what-is-http}

Le HTTP/2 améliore la communication entre les navigateurs et les serveurs, en accélérant le transfert d’informations tout en réduisant la puissance de traitement nécessaire.

Le site web suivant décrit HTTP/2 et ses avantages de manière simple et rapide :

[Ce que vous devez savoir sur le HTTP/2](https://www.engadget.com/2015-02-24-what-you-need-to-know-about-http-2.html)

## Quels sont les principaux avantages de la transition vers le HTTP/2 pour la diffusion de contenu ?  {#what-are-the-key-benefits-of-moving-to-http-for-content-delivery}

L’amélioration des performances peut varier considérablement. Elle repose sur de nombreux facteurs, tels que le code de votre site web, la manière dont vous utilisez Dynamic Media, l’appareil, l’écran et l’emplacement du consommateur.

Les tests effectués par Adobe ont donné les résultats suivants :

* Pour les images, le temps de réponse s’est amélioré de 7 % à 28 % selon l’appareil et le navigateur. Les gains de performances les plus notables ont été enregistrés sur les appareils iOS.
* Pour les visionneuses, les performances de chargement ont été améliorées jusqu’à 15 %.

La démonstration suivante illustre la différence entre le chargement HTTP/1 et HTTP/2 :

[https://http2.akamai.com/demo](https://http2.akamai.com/demo)

## Puis-je passer à HTTP/2 ? {#am-i-eligible-to-switch-over-to-http}

Pour utiliser HTTP/2, vous devez respecter les conditions suivantes :

* Utilisez le protocole HTTPS sécurisé pour vos demandes de médias riches.
* Utilisez le CDN de lots Adobe (réseau de diffusion de contenu) dans le cadre de votre licence Dynamic Media.
* Utilisez un domaine dédié (non-company-h.assetsadobe#.com).

  Si vous possédez déjà un domaine dédié, vous pouvez vous inscrire par le biais de l’assistance clientèle Adobe.

  Dans le cas contraire, Adobe programmera votre transition vers le HTTP/2 pour 2018.

## Quel est le processus d’activation du HTTP/2 pour mon compte Dynamic Media ?  {#what-is-the-process-for-enabling-http-for-my-dynamic-media-account}

Pour basculer vers le HTTP/2, vous devez en faire la demande, car cette procédure n’est pas automatique.

1. Pour passer au HTTP/2, envoyez une demande auprès de l’assistance clientèle d’Adobe. Voir [Ouverture d’un ticket d’assistance](https://experienceleague.adobe.com/?support-solution=General&amp;lang=fr&amp;support-tab=home#support).

   1. Indiquez les informations suivantes dans votre demande de support :

      1. nom, adresse électronique et numéro de téléphone du contact principal.
      1. Tous les domaines pour lesquels activer HTTP/2.
      1. Assurez-vous d’utiliser le protocole HTTPS sécurisé pour les demandes de médias enrichis.
      1. Vérifiez que vous utilisez le CDN par le biais d’Adobe et non le CDN géré avec une relation directe.
      1. Vérifiez que vous utilisez un domaine dédié. Si vous utilisez Dynamic Media, vous utilisez déjà un domaine dédié.

   1. Le service clientèle vous ajoute à la liste d’attente des clients HTTP/2 par ordre chronologique d’envoi des demandes.
   1. Lorsqu’Adobe est prêt à traiter votre demande, le service clientèle vous contacte pour coordonner la transition et définir une date cible.
   1. Vous recevez une notification à l’issue du processus et pouvez vérifier que la transition vers HTTP/2 a abouti.

      Le navigateur ne détecte pas cette transition, il est donc nécessaire de télécharger une extension.

      Pour Firefox et Chrome, il existe une extension appelée « HTTP/2 and SPDY Indicator ». Les navigateurs ne prennent en charge le HTTP/2 qu’en mode sécurisé. Par conséquent, appelez une URL avec le protocole HTTPS pour vérifier. Si le http/2 est pris en charge, l’extension comprend un symbole Flash de couleur bleue et un en-tête « X-Firefox-Spdy » : « h2 ».

## Quand puis-je espérer passer au HTTP/2 ?  {#when-can-i-expect-to-be-transitioned-over-to-http}

Les demandes sont traitées dans l’ordre dans lequel l’assistance clientèle les reçoit.

>[!NOTE]
>
>Le délai d’exécution peut être long, car la transition vers le HTTP/2 implique l’effacement du cache. Par conséquent, seules quelques transitions client peuvent être traitées simultanément.

## Quels risques présente la transition vers HTTP/2 ? {#what-are-the-risks-with-moving-to-http}

La transition vers HTTP/2 efface votre cache sur le réseau CDN, car elle implique de passer à une nouvelle configuration du réseau CDN.

Le contenu non mis en cache atteint directement les serveurs Adobe d’origine jusqu’à ce que le cache soit reconstruit. C’est pour cette raison qu’Adobe prévoit de ne gérer que quelques transitions à la fois afin d’offrir des performances acceptables lors de l’extraction des demandes du site d’origine.

## Comment puis-je vérifier si une URL ou un site Web est activé avec le HTTP/2 ? {#how-can-you-verify-whether-a-url-or-website-is-activated-with-http}

Le navigateur ne détecte pas cette transition, il est donc nécessaire de télécharger une extension.

Pour Firefox et Chrome, il existe une extension appelée « HTTP/2 and SPDY Indicator ». Les navigateurs ne prennent en charge le HTTP/2 qu’en mode sécurisé. Par conséquent, appelez une URL avec le protocole HTTPS pour vérifier. Si le http/2 est pris en charge, l’extension comprend un symbole Flash de couleur bleue et un en-tête `X-Firefox-Spdy` : `h2`.
