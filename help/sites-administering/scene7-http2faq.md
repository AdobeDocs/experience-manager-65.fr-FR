---
title: FAQ sur la diffusion de contenu HTTP2
seo-title: FAQ sur la diffusion de contenu HTTP2
description: Découvrez la diffusion de contenu HTTP2.
seo-description: Découvrez la diffusion de contenu HTTP2.
uuid: e837c3e0-6e48-46f1-b510-847c9976807a
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: afbe9f80-c2a3-4a46-b9d6-4c9406667d7f
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# FAQ sur la diffusion de contenu HTTP2{#http-delivery-of-content-faq}

Adobe se réjouit d’annoncer la disponibilité de la diffusion de contenu HTTP/2. Lors de l’utilisation de HTTP/2, vous remarquerez une amélioration générale des performances.

## What is HTTP/2? {#what-is-http}

Le HTTP/2 améliore la communication entre les navigateurs et les serveurs, en accélérant le transfert d’informations, tout en réduisant la puissance de traitement nécessaire.

Le site web ci-dessous décrit simplement HTTP/2 et les avantages qu’il procure :

[https://www.engadget.com/2015/02/24/what-you-need-to-know-about-http-2/](https://www.engadget.com/2015/02/24/what-you-need-to-know-about-http-2/)

## What are the key benefits of moving to HTTP/2 for content delivery? {#what-are-the-key-benefits-of-moving-to-http-for-content-delivery}

L’amélioration des performances varie considérablement en fonction de facteurs, comme le code de votre site web, la façon dont vous utilisez Scene7, l’appareil, l’écran et l’emplacement de l’utilisateur, etc.

Les tests d’Adobe ont donné les résultats suivants :

* Pour les images, le temps de réponse s’est amélioré de 7 % à 28 % selon l’appareil et le navigateur. Les gains de performance les plus notables ont été enregistrés sur les appareils iOS.
* Pour les visionneuses, les performances en matière de temps de chargement ont augmenté de 15 %.

La démonstration suivante illustre la différence entre le chargement HTTP/1 et le chargement HTTP/2 :

[https://http2.akamai.com/demo](https://http2.akamai.com/demo)

## Puis-je passer à HTTP/2 ? {#am-i-eligible-to-switch-over-to-http}

Pour utiliser HTTP/2, vous devez satisfaire aux exigences suivantes :

* Utilisez le protocole HTTPS sécurisé pour vos demandes de médias riches.
* Utilisez le CDN (réseau de diffusion de contenu) fourni par Adobe dans le cadre de votre licence Dynamic Media Classic.
* Utilisez un domaine dédié (c’est-à-dire `images.company.com` ou `mycompany.scene7.com`), et non un domaine Dynamic Media Classic générique (c’est-à-dire `s7d1.scene7.com`, `s7d2.scene7.com`ou `s7d13.scene7.com`).

   Pour trouver vos domaines, [connectez-vous à votre instance Scene7 Publishing System](https://www.adobe.com/marketing-cloud/experience-manager/scene7-login.html) pour chaque compte d’entreprise.

    Cliquez sur **[!UICONTROL Configuration > Configuration de l’application > Paramètres généraux]**. Recherchez le champ intitulé **Nom du serveur publié**. Si vous utilisez actuellement un domaine Scene7 générique, vous pouvez demander une migration vers votre domaine personnalisé dans le cadre de cette transition.

## What is the process for enabling HTTP/2 for my Dynamic Media Classic account? {#what-is-the-process-for-enabling-http-for-my-scene-account}

You must initiate an Adobe Technical Support (`s7support@adobe.com`) request to switch over to HTTP/2; it is not automatically done for you.

1. Indiquez les informations suivantes dans votre demande adressée au support technique :

   * Nom, adresse électronique et numéro de téléphone du contact principal.
   * Tous les domaines pour lesquels activer HTTP2. C&#39;est-à-dire, `images.company.com` ou `mycompany.scene7.com`.
   Pour trouver vos domaines, [connectez-vous à votre instance Scene7 Publishing System](https://www.adobe.com/marketing-cloud/experience-manager/scene7-login.html) pour chaque compte d’entreprise.

    Cliquez sur **[!UICONTROL Configuration > Configuration de l’application > Paramètres généraux]**. Recherchez le champ intitulé **[!UICONTROL Nom du serveur publié]**.

   * Vérifiez que vous utilisez le protocole sécurisé HTTPS pour les demandes de médias riches.
   * Vérifiez que vous utilisez le CDN par le biais d’Adobe et non le CDN géré avec une relation directe.
   * Assurez-vous d’utiliser un domaine dédié. Il ne s’agit pas d’un domaine Scene7 générique tel que `images.company.com` , `mycompany.scene7.com``s7d1.scene7.com`, `s7d2.scene7.com``s7d13.scene7.com`.
   Pour trouver vos domaines, [connectez-vous à votre instance Scene7 Publishing System](https://www.adobe.com/marketing-cloud/experience-manager/scene7-login.html) pour chaque compte d’entreprise.

    Cliquez sur **[!UICONTROL Configuration > Configuration de l’application > Paramètres généraux]**. Recherchez le champ intitulé **[!UICONTROL Nom du serveur publié]**. Si vous utilisez actuellement un domaine Scene7 générique, vous pouvez demander une migration vers votre domaine personnalisé dans le cadre de cette transition.

   1. Le support technique vous ajoute à la liste des clients HTTP/2 en fonction de l’ordre dans lequel les demandes ont été envoyées.
   1. Lorsque Adobe est prêt à traiter votre demande, le support vous contacte pour coordonner la transition et définir une date cible.
   1. Vous recevez une notification à l’issue du processus et pouvez vérifier que la transition vers HTTP2 a abouti.



## When can I expect to be transitioned over to HTTP/2? {#when-can-i-expect-to-be-transitioned-over-to-http}

Les demandes sont traitées dans l’ordre dans lequel elles sont reçues par le support technique.

>[!NOTE]
>
>Le délai d’exécution peut être long, car la transition vers HTTP/2 implique l’effacement du cache. Par conséquent, seules quelques transitions client peuvent être traitées simultanément.

## Quels risques présente la transition vers HTTP/2 ? {#what-are-the-risks-with-moving-to-http}

La transition vers HTTP/2 efface le cache au niveau du CDN, car elle implique la définition d’une nouvelle configuration de CDN.

Le contenu non mis en cache atteint directement les serveurs Adobe d’origine jusqu’à ce que le cache soit reconstruit. C’est pour cette raison qu’Adobe prévoit de ne gérer que quelques transitions à la fois afin d’offrir des performances acceptables lors de l’extraction des demandes de notre site d’origine.

## Comment puis-je vérifier si une URL ou un site web est activé avec HTTP/2 ? {#how-can-you-verify-whether-a-url-or-website-is-activated-with-http}

Vous devez télécharger une extension à utiliser avec votre navigateur web. For Firefox and Chrome there is an extension called **[!UICONTROL HTTP/2 and SPDY Indicator]**. Les navigateurs ne prennent en charge HTTP/2 qu’en mode sécurisé. Il est donc nécessaire d’appeler une adresse URL avec le protocole HTTPS pour vérifier. Si HTTP/2 est pris en charge, cela est indiqué par l’extension sous la forme d’un symbole bleu Flash et d’un en-tête &quot;X-Firefox-Spdy&quot; : &quot;h2&quot;.
