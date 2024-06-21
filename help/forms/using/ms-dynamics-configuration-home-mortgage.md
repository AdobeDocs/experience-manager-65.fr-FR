---
title: Configurer Microsoft Dynamics 365 pour le workflow de prêt immobilier du site de référence We.Finance
description: Découvrez comment utiliser les services Microsoft® Dynamics 365 via des formulaires adaptatifs pour le workflow de crédit immobilier du site de référence We.Finance.
products: SG_EXPERIENCEMANAGER/6.3/FORMS
topic-tags: develop, Configuration
exl-id: 2ac37dc5-d88d-4f98-8576-cd2ca6f0ea3a
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms, Foundation Components
role: Admin, User, Developer
source-git-commit: 539da06db98395ae6eaee8103a3e4b31204abbb8
workflow-type: tm+mt
source-wordcount: '410'
ht-degree: 100%

---

# Configurer Microsoft Dynamics 365 pour le workflow de prêt immobilier du site de référence We.Finance {#configure-microsoft-dynamics-for-the-home-mortgage-workflow-of-the-we-finance-reference-site}

Découvrez comment utiliser les services Microsoft® Dynamics 365 via des formulaires adaptatifs pour le workflow de crédit immobilier du site de référence We.Finance.

## Présentation {#overview}

Microsoft® Dynamics 365 est un logiciel de gestion de la relation client (CRM) et de planification des ressources de l’entreprise (ERP) qui fournit des solutions d’entreprise pour la création et la gestion de comptes clients, de contacts, de prospects, d’opportunités et de dossiers.

AEM Forms fournit un service cloud pour intégrer Dynamics 365 au module [Forms Data Integration](/help/forms/using/data-integration.md). Avant de pouvoir utiliser la page d’accueil de l’application de prêt immobilier avec le scénario Microsoft® Dynamics, vous devez configurer Microsoft® Dynamics 365 pour l’utiliser avec le site de référence We.Finance.

## Prérequis {#prerequisites}

Avant de commencer à installer et configurer Dynamics 365, assurez-vous de disposer des éléments suivants :

* AEM 6.3 Forms Pack de services 1 et versions ultérieures
* Compte Microsoft® Dynamics 365
* Application enregistrée du service Dynamics 365 avec Microsoft® Azure Active Directory
* ID du client et le secret du client pour l’application enregistrée

## Reliez le calculateur de crédit hypothécaire à la page d&#39;accueil de votre site. {#link-the-home-mortgage-calculator-with-your-site-home-page}

1. Sur l’instance de création, accédez à la page suivante :

   `https://[server]:[port]/editor.html/content/we-finance/global/en/loan-landing-page.html`

1. Faites défiler jusqu&#39;au calculateur de crédit hypothécaire.
1. Mettez en surbrillance le panneau de la colonne de droite (celle du calculateur) et sélectionnez-le pour afficher le menu contextuel. Dans le menu contextuel, sélectionnez Configurer. La boîte de dialogue Modifier le conteneur AEM Forms s’affiche.

   ![calculatorconfigurgurepanel](assets/calculatorconfigurepanel.png)

1. Dans la boîte de dialogue Modifier le conteneur AEM Forms, accédez au chemin d’accès de la ressource et sélectionnez home-mortgage-calculator dans le chemin suivant, puis sélectionnez **Confirmer** :

   formsanddocuments/We.Finance/MS Dynamics/

   ![selectassetpath](assets/selectassetpath.png)

1. Sélectionnez **Terminé**.
1. Publiez la page modifiée.

   >[!NOTE]
   >
   >Les liaisons des champs du calculateur avec le modèle de données de formulaire sont préconfigurées via le package du site de référence We.Finance. Pour afficher les liaisons, vous pouvez ouvrir le formulaire en mode création et consulter les références des liaisons des champs.

1. Pour créer une entité personnalisée afin de stocker le dossier du candidat pour une demande de crédit immobilier, importez le package de solution AEMFormsFSIRefsite_1_0.zip dans votre instance Microsoft® Dynamics :

   1. Téléchargez le package à partir de :

      `https://'[server]:[port]'/content/aemforms-refsite-collaterals/we-finance/home-mortgage/ms-dynamics/AEMFormsFSIRefsite_1_0.zip`

   1. Importez le package de solution dans une instance de Microsoft® Dynamics. Dans votre instance Microsoft® Dynamics, accédez à **Paramètres** > **Solutions**, puis sélectionnez **Importer**.

1. Pour définir les coordonnées de l&#39;utilisateur ou de l’utilisatrice à utiliser dans le site de référence, importez le package Sarah Rose Contact.CSV dans votre instance Microsoft® Dynamics :

   1. Téléchargez le package à partir de :

      `https://'[server]:[port]'/content/aemforms-refsite-collaterals/we-finance/home-mortgage/ms-dynamics/Sarah%20Rose%20Contact.csv`

   1. Importez le package dans votre instance Microsoft® Dynamics. Dans votre instance Microsoft® Dynamics, accédez à **Ventes** > **Contacts**, puis sélectionnez **Importer les données**.
