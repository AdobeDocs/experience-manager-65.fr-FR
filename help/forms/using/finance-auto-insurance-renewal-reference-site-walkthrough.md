---
title: Présentation du site de référence de renouvellement de l’assurance automobile We.Finance
seo-title: Présentation du site de référence de renouvellement de l’assurance automobile We.Finance
description: Présentation du site de référence de renouvellement de l’assurance automobile We.Finance
uuid: c749a6f7-71f1-4f47-b824-9c7b699072c7
contentOwner: dekalra
products: SG_EXPERIENCEMANAGER/6.5/FORMS
content-type: reference
discoiquuid: ad450124-49a5-4afb-aac3-ed3733d6504b
docset: aem65
translation-type: tm+mt
source-git-commit: a873cf3e7efd3bc9cd4744bf09078d9040efcdda
workflow-type: tm+mt
source-wordcount: '748'
ht-degree: 36%

---


# Présentation du site de référence de renouvellement de l’assurance automobile We.Finance{#we-finance-auto-insurance-renewal-reference-site-walkthrough}

## Exemple d’utilisation du site de référence We.Finance  {#we-finance-reference-site-scenario}

Le site Web de We.Finance est un site de services financiers conçu pour vous aider à découvrir les capacités de communication interactives de l&#39;AEM Forms.

Lisez la présentation détaillée du cas d&#39;utilisation de l&#39;assurance auto de We.Finance qui montre comment AEM formulaires et son intégration à Microsoft Dynamics permettent de personnaliser l&#39;expérience client dans une société de service financier. La présentation interactive est conçue pour faciliter la mise en oeuvre de transactions numériques complexes et la communication client dans une société financière.

**La présentation commence par le cas d’utilisation :**

Sarah Rose est déjà cliente chez We.Finance et a acheté une police d’assurance automobile. Elle doit renouveler sa police d’assurance aujourd’hui. Gloria Rios, courtier d’assurance chez We.Finance, envoie un rappel à Sarah concernant le renouvellement de sa police. Sarah suit les instructions figurant dans le courrier électronique et effectue la procédure.

## Présentation de la demande d’assurance automobile {#auto-insurance-application-walkthrough}

Le scénario de l&#39;application d&#39;assurance auto-assurance We.Finance est une narration visuelle pour l&#39;utilisateur et repose sur deux personnages :

* Sarah Rose, une cliente chez We.Finance
* Gloria Rios, courtier d’assurance chez We.Finance

### Gloria envoie une notification de renouvellement de police d’assurance à partir de We.Finance  {#gloria-sends-an-insurance-policy-renewal-communication-from-we-finance}

Gloria se connecte à l’instance AEM, clique sur **Renouvellement de l’assurance automatique,**, puis sur **Ouvrir l’interface utilisateur de l’agent.** Le clic préremplit le document d’assurance avec les détails de la police de Sarah Rose. Gloria clique sur **Envoyer** et un message s’affiche à l’écran &quot;Envoi initié&quot;, puis en quelques secondes &quot;Envoi réussi&quot;.

Sarah reçoit un courrier électronique contenant le sujet &quot;Votre renouvellement d’assurance automatique&quot;.

![Interface utilisateur de l’agent](assets/agent_ui_email_new.png)

#### Démonstration {#see-it-yourself}

Accédez à **Adobe Experience Manager** > **Forms** > **Forms &amp; Documents** > **We.Finance** > **Auto Insurance**. Sélectionnez le renouvellement d&#39;assurance automatique **communication interactive** et cliquez sur **Ouvrir l&#39;interface utilisateur de l&#39;agent**. La communication interactive s’ouvre dans l’interface utilisateur de l’agent. Entrez une adresse électronique valide pour recevoir le courrier électronique contenant le document de stratégie joint, puis cliquez sur Envoyer.

Vous pouvez accéder à la communication interactive Renouvellement d&#39;assurance et la consulter directement à partir de `https://[authorHost]: authorPort]/aem/formdetails.html/content/dam/formsanddocuments/we-finance/autoinsurance/auto-insurance-renewal.`

### Sarah reçoit une notification de renouvellement de police d’assurance de We.Finance et décide d’effectuer le renouvellement.{#sarah-receives-an-insurance-policy-renewal-communication-from-we-finance-and-decides-to-renew}

Sarah reçoit un courrier électronique accompagné d’une pièce jointe de We.Finance qui lui rappelle que sa police d’assurance auto est sur le point d’expirer. La pièce jointe est la version imprimée de sa lettre d&#39;assurance auto.

Sarah clique sur **Renouveler maintenant** et est redirigée vers la version Web de sa lettre d’assurance automatique. En plus de cette lettre, Sarah trouve le nombre de jours restants pour l’expiration de sa stratégie. La page fournit à Sarah un aperçu de base des détails de sa police d’assurance, tels que le numéro de police, le montant dû et d’autres informations, telles que les offres d’escompte et les récompenses de fidélité. Sarah clique à nouveau sur **Renouveler maintenant** au bas de la stratégie.

![ref1](assets/ref1.png)

#### Fonctionnement {#how-it-works}

La sortie Web et imprimée de votre lettre d&#39;assurance automatique est créée à l&#39;aide des fonctionnalités multi-canaux d&#39;Interactive Communications.

Le bouton Renouveler maintenant dans le courrier électronique est lié à la demande de renouvellement d’assurance automobile qui se présente sous forme de communication interactive sur une instance de publication.

#### Démonstration  {#see-it-yourself-1}

Vous devriez recevoir un courrier électronique avec un fichier PDF joint. Le PDF est une version imprimée de votre lettre d&#39;assurance auto. Cliquez sur **Renouveler maintenant** pour accéder à la version Web de la stratégie. Vérifiez vos informations personnelles et les détails de votre stratégie et cliquez sur **Renouveler maintenant** pour accéder à une autre communication interactive.

Le bouton **Renouveler maintenant** du courrier électronique dirige Sarah vers la version Web de la stratégie. Vous pouvez consulter l’URL suivante :

`https://[authorServer]:[authorPort]/content/document.html?schema=fdm&documentId=/content/forms/af/we-finance/autoinsurance/auto-insurance-renewal/channels/web.html&customerId=1`

Vous pouvez consulter le résumé détaillé de votre renouvellement d&#39;assurance automatique et cliquer sur **Renouveler maintenant** en bas de la page.

### Sarah accède à la page de paiement {#sarah-reaches-the-payment-page}

We.Finance redirige Sarah vers la page de paiement. Sarah vérifie à nouveau son numéro de stratégie et sa date d’expiration avec ses enregistrements. Sur le côté droit de la page, elle vérifie le Sommaire des paiements de son renouvellement avec une remise de 10 % sur le montant total.

#### Fonctionnement {#how-it-works-1}

Le bouton Renouveler maintenant dirige Sarah vers la page de paiement. La page de paiement est un formulaire adaptatif.

#### Démonstration {#see-it-yourself-2}

Cliquez sur **Renouveler maintenant** pour accéder à la page de paiement. Renseignez les informations de votre carte de crédit, puis cliquez sur **Effectuer le paiement**.

Vous pouvez accéder à la page de paiement dans l’instance de création à l’adresse

`https://[authorServer]:[authorPort]/content/document.html?documentId=/content/forms/af/we-finance/credit-card/ccbillpayment.html&schema=fdm&customerId=1`

### Sarah effectue le paiement et termine le processus.{#sarah-makes-the-payment-and-completes-the-process}

Sarah remplit ses informations de carte de crédit et clique sur **Effectuer un paiement**.

#### Fonctionnement {#how-it-works-2}

Lorsque Sarah remplit les informations de carte de crédit et clique sur le bouton Envoyer, son paiement de carte de crédit est traité et un message de remerciement configuré dans le formulaire adaptatif s’affiche à l’écran.

#### Démonstration  {#see-it-yourself-3}

Vous pouvez vue le message de confirmation après avoir cliqué sur Effectuer le paiement à l’adresse

`https://[authorServer]:[authorPort]/content/forms/af/we-finance/credit-card/ccbillpayment/jcr:content/guideContainer.guideThankYouPage.html?owner=admin&status=Submitted`
