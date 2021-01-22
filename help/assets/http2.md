---
title: 'Diffusion de contenu HTTP/2  '
description: HTTP/2 améliore la communication entre les navigateurs et les serveurs, ce qui accélère le transfert d’informations tout en réduisant la puissance de traitement nécessaire.
uuid: d9deb945-bdf5-4d6b-95c8-8bae4442e618
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
discoiquuid: c8e145ad-f021-4043-8190-62151775e296
translation-type: tm+mt
source-git-commit: 0595d89409e0ca21f771be5c55c3ec9548a8449f
workflow-type: tm+mt
source-wordcount: '705'
ht-degree: 100%

---


# Diffusion de contenu HTTP/2    {#http-delivery-of-content}

Adobe est heureux d’annoncer la disponibilité de HTTP/2 pour la diffusion de contenu, protocole qui permet d’améliorer les performances globales.

## Qu’est-ce que le HTTP/2 ?{#what-is-http}

Le HTTP/2 améliore la communication entre les navigateurs et les serveurs, en accélérant le transfert d’informations tout en réduisant la puissance de traitement nécessaire.

Le site web suivant décrit simplement le protocole HTTP/2 et les avantages qu’il procure :

[https://www.engadget.com/2015/02/24/what-you-need-to-know-about-http-2/](https://www.engadget.com/2015/02/24/what-you-need-to-know-about-http-2/)

## Quels sont les principaux avantages à la transition vers HTTP/2 pour la diffusion de contenu ?{#what-are-the-key-benefits-of-moving-to-http-for-content-delivery}

L’amélioration des performances varie considérablement en fonction de facteurs tels que le code de votre site web, la façon dont vous utilisez Dynamic Media, l’appareil, l’écran et l’emplacement du client, etc.

Les tests d’Adobe ont donné les résultats suivants :

* Pour les images, le temps de réponse s’est amélioré de 7 % à 28 % selon l’appareil et le navigateur. Les gains de performance les plus notables ont été enregistrés sur les appareils iOS.
* Pour les visionneuses, les performances en matière de temps de chargement ont augmenté de 15 %.

La démonstration suivante illustre la différence entre le chargement HTTP/1 et le chargement HTTP/2 :

[https://http2.akamai.com/demo](https://http2.akamai.com/demo)

## Puis-je passer à HTTP/2 ?   {#am-i-eligible-to-switch-over-to-http}

Pour utiliser HTTP/2, vous devez satisfaire aux exigences suivantes :

* Utilisez le protocole HTTPS sécurisé pour vos demandes de médias riches.
* Utilisez le CDN de lots Adobe (réseau de diffusion de contenu) dans le cadre de votre licence Dynamic Media.
* Utilisez un domaine dédié (autre que company-h.assetsadobe#.com).

   Si vous possédez déjà un domaine dédié, vous pouvez vous inscrire par le biais du support technique.

   Dans le cas contraire, Adobe programmera votre transition vers HTTP/2 pour 2018.

## Quel est le processus d’activation de HTTP/2 pour mon compte Dynamic Media ?{#what-is-the-process-for-enabling-http-for-my-dynamic-media-account}

Pour basculer vers le HTTP/2, vous devez en faire la demande, car cette procédure n’est pas automatique.

1. Adressez une demande d’assistance technique en vue d’adopter le protocole HTTP/2. Voir [Accès au portail d’assistance AEM](https://helpx.adobe.com/fr/experience-manager/kb/accessing-aem-support-portal.html).

   1. Indiquez les informations suivantes dans votre demande de support :

      1. Nom, adresse électronique et numéro de téléphone du contact principal.
      1. Tous les domaines pour lesquels activer HTTP/2.
      1. Assurez-vous d’utiliser le protocole HTTPS sécurisé pour les demandes de médias enrichis.
      1. Assurez-vous d’utiliser le CDN via Adobe et de ne pas le gérer avec une relation directe.
      1. Assurez-vous d’utiliser un domaine dédié. Si vous utilisez Dynamic Media, vous utilisez déjà un domaine dédié.
   1. L’assistance technique vous ajoutera à la liste d’attente des clients HTTP/2 par ordre chronologique d’envoi des demandes.
   1. Lorsque Adobe est prêt à traiter votre demande, le support vous contacte pour coordonner la transition et définir une date cible.
   1. Vous recevez une notification à l’issue du processus et pouvez vérifier que la transition vers HTTP/2 abouti.

      Le navigateur ne détecte pas cette transition, il est donc nécessaire de télécharger une extension.

      Pour Firefox et Chrome, il existe une extension dénommée « HTTP/2 and SPDY Indicator ». Les navigateurs ne prennent en charge HTTP/2 qu’en mode sécurisé. Par conséquent, appelez une URL avec le protocole HTTPS pour vérifier. Si HTTP/2 est pris en charge, l’extension comprend un symbole Flash de couleur bleue et un en-tête « X-Firefox-Spdy » : « h2 ».


## Quand puis-je espérer passer à HTTP/2 ?{#when-can-i-expect-to-be-transitioned-over-to-http}

Les demandes sont traitées par ordre chronologique de réception par le support technique.

>[!NOTE]
>
>Le délai d’exécution peut être long, car la transition vers HTTP/2 implique l’effacement du cache. Par conséquent, seules quelques transitions client peuvent être traitées simultanément.

## Quels risques présente la transition vers HTTP/2 ?   {#what-are-the-risks-with-moving-to-http}

La transition vers HTTP/2 efface le cache au niveau du CDN, car elle implique la définition d’une nouvelle configuration de CDN.

Le contenu non mis en cache atteint directement les serveurs Adobe d’origine jusqu’à ce que le cache soit reconstruit. C’est pour cette raison qu’Adobe prévoit de ne gérer que quelques transitions à la fois afin d’offrir des performances acceptables lors de l’extraction des demandes de notre site d’origine.

## Comment puis-je vérifier si une URL ou un site web est activé avec HTTP/2 ?   {#how-can-you-verify-whether-a-url-or-website-is-activated-with-http}

Le navigateur ne détecte pas cette transition, il est donc nécessaire de télécharger une extension.

Pour Firefox et Chrome, il existe une extension dénommée « HTTP/2 and SPDY Indicator ». Les navigateurs ne prennent en charge HTTP/2 qu’en mode sécurisé. Par conséquent, appelez une URL avec le protocole HTTPS pour vérifier. Si HTTP/2 est pris en charge, l’extension comprend un symbole Flash de couleur bleue et un en-tête « X-Firefox-Spdy » : « h2 ».
