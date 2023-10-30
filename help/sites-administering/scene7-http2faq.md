---
title: FAQ sur la diffusion de contenu HTTP/2
description: Découvrez la diffusion de contenu HTTP2 et comment elle peut améliorer les performances globales de votre contenu web.
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
exl-id: 2428914c-5fb0-439e-a1ef-8ee30b890f58
source-git-commit: 06a6d4e0ba2aeaefcfb238233dd98e8bbd6731da
workflow-type: tm+mt
source-wordcount: '782'
ht-degree: 92%

---

# FAQ sur la diffusion de contenu HTTP/2{#http-delivery-of-content-faq}

Adobe se réjouit d’annoncer la disponibilité de la diffusion de contenu HTTP/2. Lorsque vous utilisez HTTP/2, une augmentation globale des performances est remarquée.

## Qu’est-ce que le HTTP/2 ?  {#what-is-http}

Le HTTP/2 améliore la communication entre les navigateurs et les serveurs, en accélérant le transfert d’informations tout en réduisant la puissance de traitement nécessaire.

Le site web suivant décrit HTTP/2 et ses avantages de manière simple et rapide :

[Ce que vous devez savoir sur le HTTP/2](https://www.engadget.com/2015-02-24-what-you-need-to-know-about-http-2.html)

## Quels sont les principaux avantages de la transition vers le HTTP/2 pour la diffusion de contenu ?  {#what-are-the-key-benefits-of-moving-to-http-for-content-delivery}

L’amélioration des performances varie considérablement en fonction de facteurs tels que le code de votre site web, la façon dont vous utilisez Dynamic Media, l’appareil, l’écran et l’emplacement du client, etc.

Les tests effectués par Adobe ont donné les résultats suivants :

* Pour les images, le temps de réponse s’est amélioré de 7 % à 28 % selon l’appareil et le navigateur. Les gains de performances les plus notables ont été enregistrés sur les appareils iOS.
* Pour les visionneuses, les performances de chargement ont augmenté de 15 %.

La démonstration suivante illustre la différence entre le chargement HTTP/1 et HTTP/2 :

[https://http2.akamai.com/demo](https://http2.akamai.com/demo)

## Puis-je passer à HTTP/2 ? {#am-i-eligible-to-switch-over-to-http}

Pour utiliser HTTP/2, vous devez respecter les conditions suivantes :

* Utilisez le protocole HTTPS sécurisé pour vos demandes de médias riches.
* Utilisez le CDN de lots Adobe (réseau de diffusion de contenu) dans le cadre de votre licence Dynamic Media.
* Utilisez un domaine dédié (c’est-à-dire `images.company.com` ou `mycompany.scene7.com`), et non un domaine Dynamic Media générique (c’est-à-dire `s7d1.scene7.com`, `s7d2.scene7.com` ou `s7d13.scene7.com`).

  Pour trouver vos domaines, ouvrez l’[application de bureau Dynamic Media Classic](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html?lang=fr#getting-started), puis connectez-vous à un ou plusieurs comptes de votre entreprise. Accédez à **[!UICONTROL Configuration]** > **[!UICONTROL Configuration de l’application]** > **[!UICONTROL Paramètres généraux]**. Recherchez le champ intitulé **Nom du serveur publié**. Si vous utilisez actuellement un domaine Dynamic Media générique, vous pouvez demander une migration vers votre domaine personnalisé dans le cadre de cette transition.

## Quel est le processus d’activation de HTTP/2 pour mon compte Dynamic Media ?  {#what-is-the-process-for-enabling-http-for-my-scene-account}

1. [Utilisez l’Admin Console pour créer un dossier de support](https://helpx.adobe.com/fr/enterprise/using/support-for-experience-cloud.html) et demander à passer en HTTP/2 ; ce processus n’est pas automatique.
1. Indiquez les informations suivantes dans votre dossier de support :

   * Nom, adresse électronique et numéro de téléphone du contact principal.
   * Tous les domaines pour lesquels activer HTTP/2. C’est-à-dire, `images.company.com` ou `mycompany.scene7.com`.

     Pour trouver vos domaines, ouvrez l’[application de bureau Dynamic Media Classic](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html?lang=fr#getting-started), puis connectez-vous à un ou plusieurs comptes de votre entreprise. Accédez à **[!UICONTROL Configuration]** > **[!UICONTROL Configuration de l’application]** > **[!UICONTROL Paramètres généraux]**. Recherchez le champ intitulé **[!UICONTROL Nom du serveur publié]**.

   * Vérifiez que vous utilisez le protocole sécurisé HTTPS pour les demandes de médias riches.
   * Vérifiez que vous utilisez le réseau CDN via Adobe et qu’il n’est pas géré avec une relation directe.
   * Assurez-vous d’utiliser un domaine dédié. C’est-à-dire `images.company.com` ou `mycompany.scene7.com`, et non d’un domaine Dynamic Media tel que `s7d1.scene7.com`, `s7d2.scene7.com`, `s7d13.scene7.com`.

     Pour trouver vos domaines, ouvrez l’[application de bureau Dynamic Media Classic](https://experienceleague.adobe.com/docs/dynamic-media-classic/using/getting-started/signing-out.html?lang=fr#getting-started), puis connectez-vous à un ou plusieurs comptes de votre entreprise. Accédez à **[!UICONTROL Configuration]** > **[!UICONTROL Configuration de l’application]** > **[!UICONTROL Paramètres généraux]**. Recherchez le champ intitulé **[!UICONTROL Nom du serveur publié]**. Si vous utilisez actuellement un domaine Dynamic Media générique, vous pouvez demander une migration vers votre domaine personnalisé dans le cadre de cette transition.

1. L’assistance clientèle Adobe vous ajoute à la liste d’attente des clients HTTP/2 par ordre chronologique d’envoi des demandes.
1. Lorsqu’Adobe est prêt à traiter votre demande, l’assistance clientèle vous contacte pour coordonner la transition et définir une date cible.
1. Vous recevez une notification à l’issue du processus et pouvez vérifier que la transition vers HTTP/2 a abouti.

## Quand puis-je espérer passer à HTTP/2 ? {#when-can-i-expect-to-be-transitioned-over-to-http}

Les demandes sont traitées dans l’ordre dans lequel l’assistance clientèle Adobe les reçoit.

>[!NOTE]
>
>Le délai d’exécution est long car la transition vers le HTTP/2 implique l’effacement du cache. Par conséquent, seules quelques transitions client peuvent être traitées simultanément.

## Quels risques présente la transition vers HTTP/2 ? {#what-are-the-risks-with-moving-to-http}

La transition vers HTTP/2 efface votre cache sur le réseau CDN, car elle implique de passer à une nouvelle configuration du réseau CDN.

Le contenu non mis en cache atteint directement les serveurs Adobe d’origine jusqu’à ce que le cache soit reconstruit. C’est pour cette raison qu’Adobe prévoit de ne gérer que quelques transitions à la fois afin d’offrir des performances acceptables lors de l’extraction des demandes du site d’origine d’Adobe.

## Comment puis-je vérifier si une URL ou un site web est activé avec le HTTP/2 ? {#how-can-you-verify-whether-a-url-or-website-is-activated-with-http}

Téléchargez une extension que vous pouvez utiliser avec votre navigateur web. Pour Firefox et Chrome, il existe une extension appelée **[!UICONTROL HTTP/2 and SPDY Indicator]**. Les navigateurs ne prennent en charge HTTP/2 qu’en mode sécurisé. Par conséquent, appelez une URL avec le protocole HTTPS pour vérifier. Si le HTTP/2 est pris en charge, l’extension comprend un symbole Flash de couleur bleue et un en-tête « X-Firefox-Spdy » : « h2 ».
