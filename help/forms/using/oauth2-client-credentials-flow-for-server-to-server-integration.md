---
title: Intégration de Salesforce avec AEM Forms à l’aide du flux d’informations d’identification du client OAuth 2.0
seo-title: Salesforce integration with AEM Forms using OAuth 2.0 client credentials flow
description: Procédure d’intégration de Salesforce à AEM Forms à l’aide du flux d’informations d’identification du client OAuth 2.0
seo-description: Steps to integrate Salesforce integration with AEM Forms using OAuth 2.0 client credentials flow
source-git-commit: f03513c98455e00beef37819a5a47ba56dfa5028
workflow-type: tm+mt
source-wordcount: '503'
ht-degree: 0%

---


# Intégration de Salesforce à l’aide du flux d’informations d’identification du client OAuth 2.0  {#configure-salesforce-with-ouath-2.0-client-credential}

Pour intégrer AEM Forms à l’application Salesforce, le flux d’informations d’identification du client OAuth 2.0 est utilisé. Il s’agit d’une méthode de communication directe normalisée et sécurisée sans intervention de l’utilisateur. Dans ce flux, l’application cliente (AEM formulaire) échange les informations d’identification du client, définies dans l’application connectée Salesforce, pour obtenir un jeton d’accès. Les informations d’identification client requises incluent la clé client et le secret client.

## Avantages de l’intégration de Salesforce à AEM Forms à l’aide du flux d’informations d’identification du client OAuth 2.0 {#advantages-of-integrating-saleforce-aemforms}

AEM Forms prend en charge l’intégration de Salesforce avec le flux de code d’autorisation, en plus du flux d’informations d’identification du client OAuth 2.0. Dans le flux Code d’autorisation OAuth 2.0, l’application cliente (AEM Forms) obtient un accès aux ressources pour le compte d’un utilisateur Salesforce, ce qui présente certaines limites :

* Un maximum de cinq connexions par utilisateur est autorisé. D’autres connexions révoquent automatiquement les anciennes connexions.
* Si un utilisateur est désactivé, perd l’accès ou met à jour un mot de passe, la configuration AEM source de données cesse de fonctionner.

## Prérequis {#prerequisites}

Pour récupérer et récupérer des données entre les environnements Salesforce et AEM, certaines conditions préalables doivent être remplies avant de poursuivre :

+++ **Configuration d’une application connectée à Saleforce avec un flux d’informations d’identification client et un utilisateur API uniquement**

Il est obligatoire de créer une application Salesforce connectée à l’aide du flux d’informations d’identification du client OAuth 2.0 et d’un utilisateur API uniquement pour votre organisation. Pour obtenir des instructions détaillées, reportez-vous à l’article [Flux d’informations d’identification client OAuth 2.0 pour l’intégration serveur à serveur](https://help.salesforce.com/s/articleView?id=sf.connected_app_client_credentials_setup.htm&amp;type=5). Ces étapes vous aident à obtenir la clé du consommateur et le secret du consommateur.

>[!NOTE]
>
> Veillez à noter la clé du consommateur et le secret du consommateur, car ils sont requis lors de la création d’une configuration de source de données AEM.

+++

+++ **Création d’un fichier Swagger**

Swagger est un ensemble open source de règles, de spécifications et d’outils permettant de développer et de décrire des API RESTful. [Création d’un fichier swagger](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/forms/integrate-with-salesforce/describe-rest-api.html) avant d’intégrer Salesforce à AEM Forms.

    >[!REMARQUE]
    >
    > AEM 6.5 prend uniquement en charge les spécifications de fichier Swagger 2.0.

+++

## Étapes de configuration de Salesforce avec le flux d’informations d’identification client {#steps-to-create-aem-datasource-configuration}

1. Connectez-vous à votre instance d’auteur .
1. Accédez à **[!UICONTROL Outils]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL Sources de données]**.
1. Sélectionnez le dossier de configuration.
1. Cliquez sur **[!UICONTROL Créer]** et le **[!UICONTROL Création d’une configuration de source de données]** apparaît.
1. Spécifiez la variable **[!UICONTROL Titre]** et sélectionnez la variable **[!UICONTROL Type de service]** as **[!UICONTROL Service RESTful]**.
1. Cliquez sur **[!UICONTROL Suivant]**.
1. Sélectionnez la **[!UICONTROL Source Swagger]** as **[!UICONTROL Fichier].**
   >[!NOTE]
   >
   > Dès que le fichier swagger est sélectionné, le schéma, le nom de l’hôte et le chemin d’accès de base sont automatiquement renseignés.

1. Chargez le fichier swagger créé à partir de votre ordinateur local en cliquant sur **[!UICONTROL Parcourir]**.
1. Sélectionnez la **[!UICONTROL Type d’authentification]** as **[!UICONTROL OAuth 2.0]** et le **[!UICONTROL Paramètres d’authentification]** s’affiche.
1. Sélectionnez la **[!UICONTROL Type d’octroi]** as **[!UICONTROL Informations d’identification client]**.
1. Spécifiez la variable **[!UICONTROL ID client]** et **[!UICONTROL Secret du client]** obtenu à partir de l’application connectée Salesforce.
1. Spécifiez la variable **[!UICONTROL URL du jeton d’accès]** au format
   `https://[MyDomainName].my.salesforce.com/services/oauth2/token`.

   >[!NOTE]
   >
   > Chaque organisation possède son propre nom de domaine spécifique.

1. Cliquez sur **[!UICONTROL Tester la connexion]**.
1. Si la connexion réussit, cliquez sur le bouton **[!UICONTROL Créer]** bouton .

Maintenant, vous pouvez [création du modèle de données de formulaire](https://experienceleague.adobe.com/docs/experience-manager-65/forms/form-data-model/create-form-data-models.html?lang=en) pour intégrer la source de données configurée à votre formulaire adaptatif.


