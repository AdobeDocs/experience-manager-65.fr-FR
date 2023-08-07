---
title: Intégration de Salesforce avec AEM Forms à l’aide du flux d’informations d’identification client OAuth 2.0
seo-title: Salesforce integration with AEM Forms using OAuth 2.0 client credentials flow
description: Procédure d’intégration de Salesforce avec AEM Forms à l’aide du flux d’informations d’identification client OAuth 2.0
seo-description: Steps to integrate Salesforce integration with AEM Forms using OAuth 2.0 client credentials flow
exl-id: 31f2ccf8-1f4f-4d88-8c5f-ef1b7d1bfb4f
source-git-commit: f11bb43d914a43431cab408ca77690b6ba528a06
workflow-type: tm+mt
source-wordcount: '424'
ht-degree: 52%

---

# Intégration de Salesforce à l’aide du flux d’informations d’identification client OAuth 2.0 {#configure-salesforce-with-ouath-2.0-client-credential}

| Version | Lien de l’article |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Cliquez ici](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/integrate/use-form-data-model/oauth2-client-credentials-flow-for-server-to-server-integration.html) |
| AEM 6.5 | Cet article |

Vous pouvez utiliser les informations d’identification du client OAuth 2.0 pour intégrer AEM Forms à l’application Salesforce. Les informations d’identification du client OAuth 2.0 sont une méthode standard et sécurisée de communication directe sans intervention de l’utilisateur.

![Workflow lors de la définition de la communication entre AEM Forms et l’application Salesforce](/help/forms/using/assets/salesforce-workflow.png)

AEM Forms échange les informations d’identification du client (clé client et secret client), définies dans l’application connectée Salesforce, pour obtenir un jeton d’accès.

L’utilisation des informations d’identification du client OAuth 2.0 présente plusieurs avantages pour l’authentification par rapport à l’authentification Flux de code d’autorisation :

* L’authentification des informations d’identification du client OAuth 2.0 permet plus de cinq connexions par utilisateur.
* AEM configuration de la source de données continue à fonctionner sur la désactivation, les modifications d’accès et la mise à jour du mot de passe pour un utilisateur AEM.

## Conditions préalables requises {#prerequisites}

Avant de définir la communication entre une application Salesforce et un environnement AEM :

* Créez un [Application connectée à Salesforce avec flux d’informations d’identification client OAuth 2.0](https://help.salesforce.com/s/articleView?id=sf.connected_app_client_credentials_setup.htm&amp;type=5) et un utilisateur API uniquement pour votre organisation et obtenez la clé client et le secret client pour l’application.

* Assurez-vous que votre fichier Swagger est correctement configuré pour correspondre aux API de votre entreprise. Vous pouvez également choisir de [créer un fichier Swagger ;](https://experienceleague.adobe.com/docs/experience-manager-learn/cloud-service/forms/integrate-with-salesforce/describe-rest-api.html?lang=fr) à partir de zéro, adapté à l’utilisation dans votre environnement AEM.
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

Maintenant, vous pouvez [création du modèle de données de formulaire](https://experienceleague.adobe.com/docs/experience-manager-65/forms/form-data-model/create-form-data-models.html?lang=fr) pour intégrer la source de données configurée à votre Forms adaptatif.
