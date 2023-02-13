---
title: Présentation du site de référence de renouvellement de l’assurance automobile We.Finance
seo-title: We.Finance Auto Insurance Renewal reference site walkthrough
description: Présentation du site de référence de renouvellement de l’assurance automobile We.Finance
uuid: c749a6f7-71f1-4f47-b824-9c7b699072c7
contentOwner: dekalra
products: SG_EXPERIENCEMANAGER/6.5/FORMS
content-type: reference
discoiquuid: ad450124-49a5-4afb-aac3-ed3733d6504b
docset: aem65
exl-id: b6ded6ac-4fb1-49f9-b272-16774c3e89a3
source-git-commit: 9d142ce9e25e048512440310beb05d762468f6a2
workflow-type: ht
source-wordcount: '741'
ht-degree: 100%

---

# Présentation du site de référence de renouvellement de l’assurance automobile We.Finance{#we-finance-auto-insurance-renewal-reference-site-walkthrough}

## Exemple d’utilisation du site de référence We.Finance  {#we-finance-reference-site-scenario}

Le site We.Finance est un site de services financiers conçu pour vous aider à découvrir les fonctionnalités de communications interactives d’AEM Forms.

Lisez la présentation détaillée du cas d’utilisation de l’assurance automobile We.Finance qui explique comment AEM Forms et son intégration à Microsoft Dynamics permettent de personnaliser l’expérience client dans une société de services financiers. La présentation interactive est conçu pour faciliter l’implémentation de transactions numériques complexes et la communication avec les clients dans une société financière.

**La présentation commence par le cas d’utilisation :**

Sarah Rose est déjà cliente chez We.Finance et a acheté une police d’assurance automobile. Elle doit renouveler sa police d’assurance aujourd’hui. Gloria Rios, courtier d’assurance chez We.Finance, envoie un rappel à Sarah concernant le renouvellement de sa police. Sarah suit les instructions figurant dans le courrier électronique et effectue la procédure.

## Présentation de la demande d’assurance automobile {#auto-insurance-application-walkthrough}

Le scénario de l’application à une assurance automobile chez We.Finance est une narration visuelle pour l’utilisateur et met deux personnes en scène :

* Sarah Rose, une cliente chez We.Finance
* Gloria Rios, courtier d’assurance chez We.Finance

### Gloria envoie une notification de renouvellement de police d’assurance à partir de We.Finance {#gloria-sends-an-insurance-policy-renewal-communication-from-we-finance}

Gloria se connecte à l’instance AEM, clique sur **Renouvellement de l’assurance automobile**, puis sur **Ouvrir l’interface utilisateur de l’agent.** Le clic préremplit le document d’assurance avec les détails de la police de Sarah Rose. Gloria clique sur **Envoyer** et un message « Envoi en cours » apparaît à l’écran. Quelques secondes plus tard, le message « Envoyé » s’affiche.

Sarah reçoit un e-mail dont l’objet est « Renouvellement de votre assurance automobile ».

![Interface utilisateur de l’agent](assets/agent_ui_email_new.png)

#### Démonstration {#see-it-yourself}

Accédez à **Adobe Experience Manager** > **Formulaires** > **Formulaires et documents** > **We.Finance** > **Assurance automobile**. Sélectionnez **Communication interactive** du renouvellement de l’assurance automobile, puis cliquez sur **Ouvrir l’interface utilisateur de l’agent**. La communication interactive s’ouvre dans l’interface utilisateur de l’agent. Saisissez une adresse électronique valide pour recevoir un e-mail contenant le document de police joint, puis cliquez sur envoyer.

Vous pouvez accéder à la communication interactive du renouvellement de l’assurance automobile et la consulter directement depuis `https://[authorHost]: authorPort]/aem/formdetails.html/content/dam/formsanddocuments/we-finance/autoinsurance/auto-insurance-renewal.`.

### Sarah reçoit une notification de renouvellement de police d’assurance de We.Finance et décide d’effectuer le renouvellement. {#sarah-receives-an-insurance-policy-renewal-communication-from-we-finance-and-decides-to-renew}

Sarah reçoit un e-mail contenant une pièce jointe de We.Finance qui lui rappelle que sa police d’assurance automobile est sur le point d’expirer. La pièce jointe contient la version imprimée de sa lettre d’assurance automobile.

Sarah clique sur **Renouveler maintenant** et est redirigée vers la version web de sa lettre d’assurance automobile. En haut de cette lettre, Sarah trouve le nombre de jours restant avant l’expiration de sa police. La page fournit à Sarah un aperçu de base des détails de sa police d’assurance, tels que le numéro de police, le montant dû et d’autres informations telles que les offres de réduction et les récompenses de fidélité. Sarah clique à nouveau sur **Renouveler maintenant** au bas de la police.

![ref1](assets/ref1.png)

#### Fonctionnement {#how-it-works}

Les versions web et imprimées de votre lettre d’assurance automobile sont créées à l’aide des fonctionnalités multicanales des communications interactives.

Le bouton Renouveler maintenant dans le courrier électronique est lié à la demande de renouvellement d’assurance automobile qui se présente sous forme de communication interactive sur une instance de publication.

#### Démonstration {#see-it-yourself-1}

Vous devriez recevoir un courrier électronique avec un fichier PDF joint. Le fichier PDF est une version imprimée de votre lettre d’assurance automobile. Cliquez sur **Renouveler maintenant** pour accéder à la version web de la police. Vérifiez vos informations personnelles et les détails de la police, puis cliquez sur **Renouveler maintenant** pour être redirigé vers une autre communication interactive.

Le bouton **Renouveler maintenant** figurant dans l’e-mail redirige Sarah vers la version web de la police. Vous pouvez consulter l’URL suivante :

`https://[authorServer]:[authorPort]/content/document.html?schema=fdm&documentId=/content/forms/af/we-finance/autoinsurance/auto-insurance-renewal/channels/web.html&customerId=1`

Vous pouvez vérifier le résumé détaillé de votre renouvellement d’assurance automobile et cliquer sur **Renouveler maintenant** au bas de la page.

### Sarah accède à la page de paiement {#sarah-reaches-the-payment-page}

We.Finance redirige Sarah vers la page de paiement. Sarah vérifie à nouveau son numéro de police et la date d’expiration dans ses dossiers. Sur le côté droit de la page, elle vérifie le récapitulatif des paiements de son renouvellement avec une réduction de 10 % sur le montant total.

#### Fonctionnement {#how-it-works-1}

Le bouton Renouveler maintenant redirige Sarah vers la page de paiement. La page de paiement est un formulaire adaptatif.

#### Démonstration {#see-it-yourself-2}

Cliquez sur **Renouveler maintenant** pour accéder à la page de paiement. Saisissez vos informations de carte de crédit, puis cliquez sur **Effectuer un paiement**.

Vous pouvez accéder à la page de paiement dans une instance de création à l’adresse suivante :

`https://[authorServer]:[authorPort]/content/document.html?documentId=/content/forms/af/we-finance/credit-card/ccbillpayment.html&schema=fdm&customerId=1`

### Sarah effectue le paiement et termine le processus. {#sarah-makes-the-payment-and-completes-the-process}

Sarah remplit ses informations de carte de crédit et clique sur **Effectuer un paiement**.

#### Fonctionnement {#how-it-works-2}

Lorsque Sarah remplit les informations de carte de crédit et clique sur le bouton Envoyer, son paiement de carte de crédit est traité et un message de remerciement configuré dans le formulaire adaptatif s’affiche à l’écran.

#### Démonstration {#see-it-yourself-3}

Vous pouvez afficher le message de confirmation après avoir cliqué sur Effectuer un paiement à l’adresse suivante :

`https://[authorServer]:[authorPort]/content/forms/af/we-finance/credit-card/ccbillpayment/jcr:content/guideContainer.guideThankYouPage.html?owner=admin&status=Submitted`
