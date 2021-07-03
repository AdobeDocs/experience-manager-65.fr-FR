---
title: 'Diffusion de contenu HTTP/2 '
description: HTTP/2 améliore la communication entre les navigateurs et les serveurs, ce qui accélère le transfert d’informations tout en réduisant la puissance de traitement nécessaire.
uuid: d9deb945-bdf5-4d6b-95c8-8bae4442e618
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
discoiquuid: c8e145ad-f021-4043-8190-62151775e296
role: User, Admin
exl-id: 9eb9f309-33e5-4694-84d2-fb2cd3de50a6
feature: Publication,Configuration
source-git-commit: bb46b0301c61c07a8967d285ad7977514efbe7ab
workflow-type: tm+mt
source-wordcount: '732'
ht-degree: 60%

---

# Diffusion de contenu HTTP/2 {#http-delivery-of-content}

Adobe est heureux d’annoncer la disponibilité de HTTP/2 pour la diffusion de contenu, protocole qui permet d’améliorer les performances globales.

>[!NOTE]
>
>Cette fonctionnalité nécessite l’utilisation du réseau CDN prêt à l’emploi fourni avec Adobe Experience Manager Dynamic Media. Aucun autre réseau CDN personnalisé n’est pris en charge avec cette fonctionnalité.

## Qu’est-ce que le HTTP/2 ?  {#what-is-http}

Le HTTP/2 améliore la communication entre les navigateurs et les serveurs, en accélérant le transfert d’informations tout en réduisant la puissance de traitement nécessaire.

Le site web ci-dessous décrit simplement HTTP/2 et les avantages qu’il procure :

[Ce que vous devez savoir sur HTTP/2](https://www.engadget.com/2015-02-24-what-you-need-to-know-about-http-2.html)

## Quels sont les principaux avantages à la transition vers HTTP/2 pour la diffusion de contenu ?  {#what-are-the-key-benefits-of-moving-to-http-for-content-delivery}

L’amélioration des performances peut varier considérablement. Il repose sur de nombreux facteurs, tels que le code de votre site web, la manière dont vous utilisez Dynamic Media, l’appareil, l’écran et l’emplacement du consommateur.

Les tests d’Adobe ont donné les résultats suivants :

* Pour les images, le temps de réponse s’est amélioré de 7 % à 28 % selon l’appareil et le navigateur. Les gains de performance les plus notables ont été enregistrés sur les appareils iOS.
* Pour les visionneuses, les performances en matière de temps de chargement ont augmenté de 15 %.

La démonstration suivante illustre la différence entre le chargement HTTP/1 et le chargement HTTP/2 :

[https://http2.akamai.com/demo](https://http2.akamai.com/demo)

## Puis-je passer à HTTP/2 ?  {#am-i-eligible-to-switch-over-to-http}

Pour utiliser HTTP/2, vous devez satisfaire aux exigences suivantes :

* Utilisez le protocole HTTPS sécurisé pour vos demandes de médias riches.
* Utilisez le CDN de lots Adobe (réseau de diffusion de contenu) dans le cadre de votre licence Dynamic Media.
* Utilisez un domaine dédié (autre que company-h.assetsadobe#.com).

   Si vous disposez déjà d’un domaine dédié, vous pouvez vous inscrire par le biais du support technique.

   Si vous ne disposez pas d’un domaine dédié, Adobe prévoit de programmer votre transition vers HTTP/2 en 2018.

## Quel est le processus d’activation de HTTP/2 pour mon compte Dynamic Media ?  {#what-is-the-process-for-enabling-http-for-my-dynamic-media-account}

Vous lancez la requête pour passer à HTTP/2. ce n&#39;est pas fait automatiquement pour vous.

1. Pour passer à HTTP/2, envoyez une demande d’Adobe à l’assistance clientèle. Voir [Accès au portail d’assistance Adobe Experience Manager](https://helpx.adobe.com/fr/experience-manager/kb/accessing-aem-support-portal.html).

   1. Indiquez les informations suivantes dans votre demande de support :

      1. nom, adresse électronique et numéro de téléphone du contact principal.
      1. Tous les domaines à transférer vers HTTP/2.
      1. Vérifiez que vous utilisez le protocole HTTPS sécurisé pour les demandes de médias riches.
      1. Vérifiez que vous utilisez le CDN par Adobe et que vous n’êtes pas géré avec une relation directe.
      1. Vérifiez que vous utilisez un domaine dédié. Si vous utilisez Dynamic Media, vous utilisez un domaine dédié.
   1. L’assistance clientèle vous ajoute à la liste d’attente des clients HTTP/2 dans l’ordre dans lequel les demandes ont été envoyées.
   1. Lorsqu’Adobe est prêt à traiter votre demande, l’Assistance clientèle vous contacte pour coordonner la transition et définir une date cible.
   1. Une fois la transition terminée, vous en êtes informé et pouvez vérifier que la transition vers HTTP2 a réussi.

      Le navigateur ne détecte pas cette transition, il est donc nécessaire de télécharger une extension.

      Pour Firefox et Chrome, il existe une extension appelée &quot;HTTP/2 and SPDY Indicator&quot;. Les navigateurs ne prennent en charge HTTP/2 qu’en mode sécurisé. Par conséquent, appelez une URL avec le protocole HTTPS pour vérifier. Si http/2 est pris en charge, il est indiqué par l’extension sous la forme d’un symbole de Flash bleu et d’un en-tête &quot;X-Firefox-Spdy&quot; : &quot;h2&quot;.


## Quand puis-je espérer passer à HTTP/2 ?  {#when-can-i-expect-to-be-transitioned-over-to-http}

Les demandes sont traitées dans l’ordre dans lequel elles sont reçues par l’assistance clientèle.

>[!NOTE]
>
>Le délai d’exécution peut être long, car la transition vers HTTP/2 implique l’effacement du cache. Par conséquent, seules quelques transitions client peuvent être traitées simultanément.

## Quels risques présente la transition vers HTTP/2 ?  {#what-are-the-risks-with-moving-to-http}

La transition vers HTTP/2 efface le cache au niveau du CDN, car elle implique la définition d’une nouvelle configuration de CDN.

Le contenu non mis en cache atteint directement les serveurs Adobe d’origine jusqu’à ce que le cache soit reconstruit. C’est pour cette raison qu’Adobe prévoit de ne gérer que quelques transitions à la fois afin d’offrir des performances acceptables lors de l’extraction des demandes du site d’origine.

## Comment puis-je vérifier si une URL ou un site web est activé avec HTTP/2 ?  {#how-can-you-verify-whether-a-url-or-website-is-activated-with-http}

Le navigateur ne détecte pas cette transition, il est donc nécessaire de télécharger une extension.

Pour Firefox et Chrome, il existe une extension appelée &quot;HTTP/2 and SPDY Indicator&quot;. Les navigateurs ne prennent en charge HTTP/2 qu’en mode sécurisé. Par conséquent, appelez une URL avec le protocole HTTPS pour vérifier. Si http/2 est pris en charge, il est indiqué par l’extension sous la forme d’un symbole de Flash bleu et d’un en-tête `X-Firefox-Spdy` : `h2`.
