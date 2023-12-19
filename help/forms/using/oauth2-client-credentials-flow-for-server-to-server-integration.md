---
title: Intégration de Salesforce avec AEM Forms à l’aide du flux d’informations d’identification client OAuth 2.0
description: Procédure d’intégration de Salesforce avec AEM Forms à l’aide du flux d’informations d’identification client OAuth 2.0
exl-id: 4c356aa6-ebd4-40b9-89e3-bc4519e4a7c5
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '402'
ht-degree: 100%

---

# Intégration de Salesforce à l’aide du flux d’informations d’identification client OAuth 2.0 {#configure-salesforce-with-ouath-2.0-client-credential}

| Version | Lien de l’article |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Cliquez ici](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/integrate/use-form-data-model/oauth2-client-credentials-flow-for-server-to-server-integration.html?lang=fr) |
| AEM 6.5 | Cet article |

Vous pouvez utiliser les informations d’identification du client OAuth 2.0 pour intégrer AEM Forms à l’application Salesforce. Les informations d’identification du client OAuth 2.0 consistent en une méthode standard et sécurisée de communication directe sans intervention utilisateur.

![Workflow lors de la définition de la communication entre AEM Forms et l’application Salesforce](/help/forms/using/assets/salesforce-workflow.png).

AEM Forms échange les informations d’identification du client (consumer key et secret du client), définies dans l’application connectée Salesforce, pour obtenir un jeton d’accès.

L’utilisation des informations d’identification du client OAuth 2.0 présente plusieurs avantages par rapport à l’authentification à l’aide du flux de code d’autorisation :

* L’authentification des informations d’identification du client OAuth 2.0 permet plus de cinq connexions par utilisateur ou utilisatrice.
* La configuration de la source de données AEM continue à fonctionner lors de la désactivation, des modifications d’accès et de la mise à jour du mot de passe pour un utilisateur ou une utilisatrice AEM.

## Conditions préalables requises {#prerequisites}

Avant de définir la communication entre une application Salesforce et un environnement AEM, assurez-vous de disposer des éléments suivants :

* Créez une [application connectée à Salesforce avec le flux d’informations d’identification client OAuth 2.0](https://help.salesforce.com/s/articleView?id=sf.connected_app_client_credentials_setup.htm&amp;type=5) et un utilisateur ou une utilisatrice API uniquement pour votre entreprise et obtenez la consumer key et le secret client pour l’application.

* Assurez-vous que votre fichier Swagger est correctement configuré pour correspondre aux API de votre entreprise. Vous pouvez également choisir de [créer un fichier Swagger](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/forms/integrate-with-salesforce/describe-rest-api.html?lang=fr) à partir de zéro, adapté à l’utilisation dans votre environnement AEM.
>[!NOTE]
>
> AEM 6.5 prend uniquement en charge les spécifications de fichier Swagger 2.0.

+++

## Étapes de configuration de Salesforce avec le flux d’informations d’identification client {#steps-to-create-aem-datasource-configuration}

1. Connectez-vous à votre instance de création.
1. Accédez à **[!UICONTROL Outils]** > **[!UICONTROL Services cloud]** > **[!UICONTROL Sources de données]**.
1. Sélectionnez le dossier de configuration.
1. Cliquez sur **[!UICONTROL Créer]**. **[!UICONTROL Créer une configuration de source de données]** apparaît.
1. Spécifiez le **[!UICONTROL Titre]** et sélectionnez le **[!UICONTROL Type de service]** comme **[!UICONTROL Service RESTful]**.
1. Cliquez sur **[!UICONTROL Suivant]**.
1. Sélectionnez la **[!UICONTROL Source Swagger]** comme **[!UICONTROL Fichier].**
   >[!NOTE]
   >
   > Dès que le fichier Swagger est sélectionné, le schéma, le nom de l’hôte et le chemin d’accès de base sont automatiquement renseignés.

1. Chargez le fichier Swagger créé à partir de votre ordinateur local en cliquant sur **[!UICONTROL Parcourir]**.
1. Sélectionnez le **[!UICONTROL Type d’authentification]** comme **[!UICONTROL OAuth 2.0]**. Le panneau **[!UICONTROL Paramètres d’authentification]** s’affiche.
1. Sélectionnez le **[!UICONTROL Type d’octroi]** comme **[!UICONTROL Informations d’identification client]**.
1. Spécifiez l’**[!UICONTROL ID client]** et le **[!UICONTROL Secret du client]** obtenus à partir de l’application connectée à Salesforce.
1. Spécifiez l’**[!UICONTROL URL du jeton d’accès]** au format
   `https://[MyDomainName].my.salesforce.com/services/oauth2/token`.

   >[!NOTE]
   >
   > Chaque organisation possède son propre nom de domaine spécifique.

1. Cliquez sur **[!UICONTROL Tester la connexion]**.
1. Si la connexion est établie, cliquez sur le bouton **[!UICONTROL Créer]**.

Vous pouvez désormais [créer le modèle de données de formulaire](https://experienceleague.adobe.com/docs/experience-manager-65/forms/form-data-model/create-form-data-models.html?lang=fr) pour intégrer la source de données configurée à vos formulaires adaptatifs.
