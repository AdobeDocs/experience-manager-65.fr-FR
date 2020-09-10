---
title: Configuration d’AEM Assets avec Brand Portal
seo-title: Configuration d’AEM Assets avec Brand Portal
description: Découvrez comment configurer AEM Assets avec Brand Portal pour publier des ressources et des collections sur Brand Portal.
seo-description: Découvrez comment configurer AEM Assets avec Brand Portal pour publier des ressources et des collections sur Brand Portal.
uuid: b95c046e-9988-444c-b50e-ff5ec8cafe14
topic-tags: brand-portal
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
discoiquuid: dca5a2ac-1fc8-4251-b073-730fd6f49b1c
docset: aem65
translation-type: tm+mt
source-git-commit: 8633216807061c73f4bc692d13f9eba37845cffc
workflow-type: tm+mt
source-wordcount: '2028'
ht-degree: 45%

---


# Configuration d’AEM Assets avec Brand Portal {#configure-integration-65}

Adobe Experience Manager (AEM) Assets est configuré avec Brand Portal via Adobe Developer Console, qui fournit un jeton IMS pour autoriser votre client Brand Portal.

>[!NOTE]
>
>La configuration de AEM Assets avec Brand Portal via Adobe Developer Console est prise en charge sur AEM 6.5.4.0 et versions ultérieures.
>
>Auparavant, le portail de marque était configuré par l’intermédiaire de la passerelle OAuth héritée, qui utilise l’échange de jetons JWT pour obtenir un Jeton d&#39;accès IMS pour l’autorisation.
>
>La configuration via la passerelle OAuth héritée n’est plus prise en charge à partir du 6 avril 2020 et est remplacée par Adobe Developer Console.


>[!TIP]
>
>***Pour les clients existants uniquement***
>
>Il est recommandé de continuer à utiliser la configuration de la passerelle OAuth héritée. Si vous rencontrez des problèmes avec la configuration héritée de la passerelle OAuth, supprimez la configuration existante et créez une nouvelle configuration via Adobe Developer Console.



Cette aide décrit les deux cas d’utilisation suivants :
* [Nouvelle configuration](#configure-new-integration-65): Si vous êtes un nouvel utilisateur du portail Marques et souhaitez configurer votre instance d’auteur AEM Assets avec Brand Portal, vous pouvez créer une configuration sur Adobe Developer Console.
* [Configuration](#upgrade-integration-65)de la mise à niveau : Si vous êtes déjà un utilisateur du portail de marques dont l’instance d’auteur AEM Assets est configurée avec Brand Portal sur la passerelle OAuth héritée, supprimez la configuration existante et créez-en une nouvelle sur Adobe Developer Console.

Cette aide s’adresse à un public familiarisé avec les technologies suivantes :

* Installation, configuration et administration des packages Adobe Experience Manager et AEM.

* Utilisation de systèmes d’exploitation Linux et Microsoft Windows.

## Conditions préalables {#prerequisites}

Pour configurer AEM Assets avec Brand Portal, vous devez disposer des éléments suivants :

* Une instance d’auteur AEM Assets en cours d’exécution avec le dernier Service Pack.
* URL du client du portail de la marque.
* Un utilisateur disposant de droits d’administrateur système sur l’organisation IMS du client Brand Portal


[Téléchargement et installation de AEM 6.5](#aemquickstart)

[Télécharger et installer le dernier Service Pack AEM](#servicepack)

### Téléchargement et installation de AEM 6.5 {#aemquickstart}

Il est recommandé d’avoir AEM 6.5 pour configurer une instance d’auteur AEM. Si vous ne l’avez pas, téléchargez-le à partir des emplacements suivants :

* If you are an existing AEM customer, download AEM 6.5 from [Adobe Licensing website](http://licensing.adobe.com).

* If you are an Adobe partner, use [Adobe Partner Training Program](https://adobe.allegiancetech.com/cgi-bin/qwebcorporate.dll?idx=82357Q) to request AEM 6.5.

Après avoir téléchargé AEM, consultez la page [Déploiement et maintenance](https://docs.adobe.com/content/help/en/experience-manager-65/deploying/deploying/deploy.html#default-local-install) pour obtenir des instructions sur la configuration d’une instance d’auteur AEM.

### Télécharger et installer le dernier Service Pack AEM {#servicepack}

Pour obtenir des instructions détaillées, voir

* [Notes de mise à jour d’AEM 6.5, Pack de services ](https://docs.adobe.com/content/help/en/experience-manager-65/release-notes/service-pack/sp-release-notes.html)

**Contactez le service à la clientèle** si vous ne parvenez pas à trouver le dernier pack AEM ou Service Pack.

## Création d’une configuration {#configure-new-integration-65}

La configuration d’AEM Assets avec Brand Portal nécessite des configurations à la fois dans l’instance d’auteur AEM Assets et dans la console de développement Adobe.

1. En AEM Assets, créez un compte IMS et générez un certificat public (clé publique).
1. Dans Adobe Developer Console, créez un projet pour votre client Brand Portal (organisation).
1. Dans le projet, configurez une API à l’aide de la clé publique pour créer une connexion au compte de service (JWT).
1. Obtenez les informations d’identification du compte de service et les informations de charge utile JWT.
1. En AEM Assets, configurez le compte IMS à l’aide des informations d’identification du compte de service et de la charge utile JWT.
1. Dans AEM Assets, configurez le service cloud du portail des marques à l’aide du compte IMS et du point de terminaison du portail des marques (URL de l’organisation).
1. Testez votre configuration en publiant un fichier d’AEM Assets vers Brand Portal.


>[!NOTE]
>
>Une instance d’auteur AEM Assets ne doit être configurée qu’avec un seul client du portail de marques.



Effectuez les étapes suivantes dans la séquence répertoriée si vous configurez AEM Assets avec Brand Portal pour la première fois :
1. [Obtention d’un certificat public](#public-certificate)
1. [Création d’une connexion au compte de service (JWT)](#createnewintegration)
1. [Configuration du compte IMS](#create-ims-account-configuration)
1. [Configuration du service cloud](#configure-the-cloud-service)
1. [Test de la configuration](#test-integration)

### Création de la configuration IMS {#create-ims-configuration}

La configuration IMS authentifie votre client Brand Portal avec l’instance d’auteur AEM Assets.

La configuration IMS comprend deux étapes :

* [Obtention d’un certificat public](#public-certificate)
* [Configuration du compte IMS](#create-ims-account-configuration)

### Obtention d’un certificat public {#public-certificate}

Un certificat public permet d’authentifier votre profil sur Adobe Developer Console.

1. Connectez-vous à votre instance d’auteur AEM Assets. L’URL par défaut est
   `http://localhost:4502/aem/start.html`

1. Dans le panneau **Outils** ![Outils](assets/do-not-localize/tools.png), accédez à **[!UICONTROL Sécurité]** > **[!UICONTROL Configurations d’Adobe IMS]**.

   ![Interface utilisateur de configuration du compte Adobe IMS](assets/ims-config1.png)

1. Dans la page Configurations d’Adobe IMS, cliquez sur **[!UICONTROL Créer]**.

1. Vous êtes redirigé vers la page **[!UICONTROL Configuration du compte technique Adobe IMS]**. Par défaut, l’onglet **Certificat** s’ouvre.

   Sélectionnez la solution cloud **[!UICONTROL Adobe Brand Portal]**.

1. Mark the **[!UICONTROL Create new certificate]** checkbox and specify an **alias** for the certificate. L’alias sert de nom à la boîte de dialogue.

1. Cliquez sur **[!UICONTROL Créer un certificat]**. Cliquez ensuite sur **[!UICONTROL OK]** dans la boîte de dialogue pour générer le certificat public.

   ![Création d’un certificat](assets/ims-config2.png)

1. Cliquez sur **[!UICONTROL Télécharger la clé publique]** et enregistrez le fichier de certificat (.crt) sur votre ordinateur.

   Le fichier de certificat sera utilisé ultérieurement pour configurer l’API de votre client du portail de marque et générer les informations d’identification du compte de service dans la console de développement des Adobes.

   ![Téléchargement du certificat](assets/ims-config3.png)

1. Cliquez sur **[!UICONTROL Suivant]**.

   In the **Account** tab, the Adobe IMS account is created but for that you will need the service account credentials that are generated in Adobe Developer Console. Gardez cette page ouverte pour l’instant.

   Ouvrez un nouvel onglet et [créez une connexion au compte de service (JWT) dans Adobe Developer Console](#createnewintegration) pour obtenir les informations d’identification et la charge utile JWT qui servent à configurer le compte IMS.

### Création d’une connexion au compte de service (JWT) {#createnewintegration}

Dans Adobe Developer Console, les projets et les API sont configurés au niveau du client (organisation) du portail de la marque. La configuration d’une API crée une connexion au compte de service (JWT) dans Adobe Developer Console. Il existe deux méthodes pour configurer l’API : générer une paire de clés (clés privée et publique) ou télécharger une clé publique. Pour configurer AEM Assets avec Brand Portal, vous devez générer un certificat public (clé publique) dans AEM Assets et créer des informations d’identification dans Adobe Developer Console en téléchargeant la clé publique. Cette clé publique est utilisée pour configurer l’API pour le client du portail de marque sélectionné et génère les informations d’identification et la charge utile JWT pour le compte de service. Ces informations d’identification sont également utilisées pour configurer le compte IMS en AEM Assets. Une fois le compte IMS configuré, vous pouvez configurer le service cloud du portail de marque en AEM Assets.

Procédez comme suit pour générer les informations d’identification du compte de service et la charge utile JWT :

1. Connectez-vous à Adobe Developer Console avec les privilèges d’administrateur système sur l’organisation IMS (client Brand Portal). L’URL par défaut est

   [https://www.adobe.com/go/devs_console_ui_fr](https://www.adobe.com/go/devs_console_ui_fr)


   >[!NOTE]
   >
   >Assurez-vous d’avoir sélectionné l’organisation IMS appropriée (locataire du portail de marque) dans la liste de liste déroulante (organisation) située dans l’angle supérieur droit.

1. Cliquez sur **[!UICONTROL Créer un projet]**. Un projet vierge est créé pour votre organisation.

   Cliquez sur **[!UICONTROL Modifier le projet]** pour mettre à jour le **[!UICONTROL Titre du projet]** et la **[!UICONTROL Description]**, puis cliquez sur **[!UICONTROL Enregistrer]**.

   ![Créer un projet](assets/service-account1.png)

1. In the **[!UICONTROL Project overview]** tab, click **[!UICONTROL Add API]**.

   ![Ajouter une API](assets/service-account2.png)

1. In the **[!UICONTROL Add an API window]**, select **[!UICONTROL AEM Brand Portal]** and click **[!UICONTROL Next]**.

   Assurez-vous d’avoir accès au service AEM Brand Portal.

1. In the **[!UICONTROL Configure API]** window, click **[!UICONTROL Upload your public key]**. Cliquez ensuite sur **[!UICONTROL Sélectionner un fichier]** et chargez le certificat public (fichier .crt) que vous avez téléchargé comme indiqué à la section [Obtention d’un certificat public](#public-certificate).

   Cliquez sur **[!UICONTROL Suivant]**.

   ![Charger la clé publique](assets/service-account3.png)

1. Vérifiez le certificat public et cliquez sur **[!UICONTROL Suivant]**.

1. Select the default product profile **[!UICONTROL Assets Brand Portal]** and click **[!UICONTROL Save configured API]**.

   <!-- 
   In Brand Portal, a default profile is created for each organization. The Product Profiles are created in admin console for assigning users to groups (based on the roles and permissions). For configuration with Brand Portal, the OAuth token is created at organization level. Therefore, you must configure the default Product Profile for your organization. 
   -->

   ![Sélectionner le profil de produit](assets/service-account4.png)

1. Une fois l’API configurée, vous êtes redirigé vers l’aperçu de l’API. Dans le volet de navigation de gauche, sous **[!UICONTROL Informations d’identification]**, cliquez sur **[!UICONTROL Compte de service (JWT)]**.

   >[!NOTE]
   >
   >Vous pouvez voir les informations d’identification et effectuer d’autres actions (générer des jetons JWT, copier les informations d’identification, récupérer le secret client, etc.), si nécessaire.

1. Dans l’onglet **[!UICONTROL Informations d’identification client]**, copiez l’**[!UICONTROL ID client]**.

   Cliquez sur **[!UICONTROL Récupérer le secret client]** et copiez le **[!UICONTROL secret client]**.

   ![Informations d’identification du compte de service](assets/service-account5.png)

1. Accédez à l’onglet **[!UICONTROL Générer le jeton JWT]** et copiez la **[!UICONTROL Charge utile JWT]**.

You can now use the client ID (API key), client secret, and JWT payload to [configure the IMS account](#create-ims-account-configuration) in AEM Assets.

<!--
### Create Adobe I/O integration {#createnewintegration}

Adobe I/O integration generates API Key, Client Secret, and Payload (JWT) which is required in setting up the IMS Account configurations.

1. Login to Adobe I/O Console with system administrator privileges on the IMS organization of the Brand Portal tenant.

   Default URL: [https://console.adobe.io/](https://console.adobe.io/) 

1. Click **[!UICONTROL Create Integration]**.

1. Select **[!UICONTROL Access an API]**, and click **[!UICONTROL Continue]**.

   ![Create New Integration](assets/create-new-integration1.png)

1. Create a new integration page opens. 
   
   Select your organization from the drop-down list.

   In **[!UICONTROL Experience Cloud]**, Select **[!UICONTROL AEM Brand Portal]** and click **[!UICONTROL Continue]**. 

   If the Brand Portal option is disabled for you, ensure that you have selected correct organization from the drop-down box above the **[!UICONTROL Adobe Services]** option. If you do not know your organization, contact your administrator.

   ![Create Integration](assets/create-new-integration2.png)

1. Specify a name and description for the integration. Click **[!UICONTROL Select a File from your computer]** and upload the `AEM-Adobe-IMS.crt` file downloaded in the [obtain public certificates](#public-certificate) section.

1. Select the profile of your organization. 

   Or, select the default profile **[!UICONTROL Assets Brand Portal]** and click **[!UICONTROL Create Integration]**. The integration is created.

1. Click **[!UICONTROL Continue to integration details]** to view the integration information. 

   Copy the **[!UICONTROL API Key]** 
   
   Click **[!UICONTROL Retrieve Client Secret]** and copy the Client Secret key.

   ![API Key, Client Secret, and payload information of an integration](assets/create-new-integration3.png)

1. Navigate to **[!UICONTROL JWT]** tab, and copy the **[!UICONTROL JWT payload]**.

   The API Key, Client Secret key, and JWT payload information will be used to create IMS account configuration.
-->

### Configuration du compte IMS {#create-ims-account-configuration}

Vérifiez que vous avez effectué les étapes suivantes :

* [Obtention d’un certificat public](#public-certificate)
* [Création d’une connexion au compte de service (JWT)](#createnewintegration)

Effectuez les étapes suivantes pour configurer le compte IMS.

1. Open the IMS Configuration and navigate to the **[!UICONTROL Account]** tab. You kept the page open while [obtaining the public certificate](#public-certificate).

1. Spécifiez un **[!UICONTROL titre]** pour le compte IMS.

   Dans **[!UICONTROL Serveur d’autorisation]**, entrez l’adresse URL : [https://ims-na1.adobelogin.com/](https://ims-na1.adobelogin.com/)

   Collez la clé **** d’API (ID client), la clé secrète **** client et la charge **** utile (charge JWT) que vous avez copiée lors de la [création de la connexion du compte de service (JWT).](#createnewintegration)

   Cliquez sur **[!UICONTROL Créer]**.

   Le compte IMS est configuré.

   ![Configuration du compte IMS](assets/create-new-integration6.png)


1. Sélectionnez la configuration de compte IMS et cliquez sur **[!UICONTROL Contrôle de l’intégrité]**.

   Cliquez sur **[!UICONTROL Vérifier]** dans la boîte de dialogue. Une fois la configuration réussie, un message s’affiche avec la mention *Jeton récupéré avec succès*.

   ![](assets/create-new-integration5.png)

>[!CAUTION]
>
>Vous ne devez avoir qu’une seule configuration IMS.
>
>Assurez-vous que la configuration IMS réussit le contrôle d’intégrité. Si tel n’est pas le cas, elle n’est pas valide. Vous devez la supprimer et créer une configuration valide.



### Configuration du service cloud {#configure-the-cloud-service}

Pour configurer le service cloud Brand Portal, procédez comme suit :

1. Connectez-vous à votre instance d’auteur AEM Assets.

1. Dans le panneau **Outils** ![Outils](assets/do-not-localize/tools.png), accédez à **[!UICONTROL Cloud Services]** > **[!UICONTROL AEM Brand Portal]**.

1. Dans la page Configurations Brand Portal, cliquez sur **[!UICONTROL Créer]**.

1. Saisissez un **[!UICONTROL titre]** pour la configuration.

   Sélectionnez la configuration IMS créée lors de la [configuration du compte IMS](#create-ims-account-configuration).

   Dans **[!UICONTROL URL du service]**, entrez votre client Brand Portal (URL de l’organisation).

   ![](assets/create-cloud-service.png)

1. Cliquez sur **[!UICONTROL Enregistrer et fermer]**. La configuration cloud est alors créée.

   Votre instance d’auteur AEM Assets est maintenant configurée avec le client du portail de marque.

### Test de la configuration {#test-integration}

Pour valider la configuration, procédez comme suit :

1. Connectez-vous à votre instance cloud AEM Assets.

1. From the **Tools** ![Tools](assets/do-not-localize/tools.png) panel, navigate to **[!UICONTROL Deployment]** > **[!UICONTROL Replication]**.

   ![](assets/test-integration1.png)

1. Sur la page Réplication, cliquez sur **[!UICONTROL Agents sur l’auteur]**.

   ![](assets/test-integration2.png)

1. Quatre agents de réplication sont créés pour chaque client.

   Localisez les agents de réplication de votre locataire du portail de marque.

   Cliquez sur l’URL de l’agent de réplication.

   ![](assets/test-integration3.png)


   >[!NOTE]
   >
   >Les agents de réplication fonctionnent en parallèle et partagent la répartition des tâches de manière égale, augmentant ainsi la vitesse de publication de quatre fois la vitesse initiale. Une fois le service cloud configuré, aucune configuration supplémentaire n’est requise pour activer les agents de réplication activés par défaut pour permettre la publication parallèle de plusieurs actifs.


1. Pour vérifier la connexion entre AEM Assets et Brand Portal, cliquez sur **[!UICONTROL Tester la connexion]**.

   ![](assets/test-integration4.png)

   Un message s’affiche en bas de la page pour indiquer que votre *module de test est livré avec succès.

   ![](assets/test-integration5.png)

1. Vérifiez les résultats du test sur les quatre agents de réplication.


   >[!NOTE]
   >
   >Evitez de désactiver les agents de réplication. Cela peut entraîner l’échec de la réplication de certains actifs.
   >
   >Assurez-vous que les quatre agents de réplication sont configurés pour éviter les erreurs de délai d’attente. See [troubleshoot issues in parallel publishing to Brand Portal](https://docs.adobe.com/content/help/en/experience-manager-brand-portal/using/publish/troubleshoot-parallel-publishing.html#connection-timeout).

Votre instance d’auteur AEM Assets a été correctement configurée avec Brand Portal. Vous pouvez désormais :

* [Publication de ressources à partir d’AEM Assets sur Brand Portal](../assets/brand-portal-publish-assets.md)
* [Publication de dossiers à partir d’AEM Assets sur Brand Portal](../assets/brand-portal-publish-folder.md)
* [Publication de collections à partir d’AEM Assets sur Brand Portal](../assets/brand-portal-publish-collection.md)
* [Sources de ressources dans le portail](https://docs.adobe.com/content/help/en/experience-manager-brand-portal/using/asset-sourcing-in-brand-portal/brand-portal-asset-sourcing.html) des marques - Publiez des ressources de Brand Portal vers AEM Assets.

## Mise à niveau de la configuration {#upgrade-integration-65}

Effectuez les étapes suivantes dans la séquence répertoriée pour mettre à niveau les configurations existantes :
1. [Vérification des tâches en cours](#verify-jobs)
1. [Supprimer les configurations existantes](#delete-existing-configuration)
1. [Création d’une configuration](#configure-new-integration-65)

### Vérification des tâches en cours {#verify-jobs}

Assurez-vous qu’aucune tâche de publication n’est exécutée sur votre instance d’auteur AEM Assets avant d’apporter des modifications. Pour cela, vous pouvez vérifier les quatre agents de réplication et vous assurer que les files d’attente sont inactives.

1. Connectez-vous à votre instance d’auteur AEM Assets.

1. From the **Tools** ![Tools](assets/do-not-localize/tools.png) panel, navigate to **[!UICONTROL Deployment]** > **[!UICONTROL Deployment Replication]**.

1. Sur la page Réplication, cliquez sur **[!UICONTROL Agents sur l’auteur]**.

   ![](assets/test-integration2.png)

1. Localisez les agents de réplication de votre locataire du portail de marque.

   Assurez-vous que la **file d&#39;attente est inactive** pour tous les agents de réplication, qu&#39;aucune tâche de publication n&#39;est principale.

   ![](assets/test-integration3.png)

### Supprimer les configurations existantes {#delete-existing-configuration}

Vous devez exécuter la liste de contrôle suivante lors de la suppression des configurations existantes.
* Supprimer les quatre agents de réplication
* Suppression du service cloud de Brand Portal
* Supprimer un utilisateur MAC

1. Connectez-vous à votre instance d’auteur AEM Assets et ouvrez CRX Lite en tant qu’administrateur. L’URL par défaut est

   `http://localhost:4502/crx/de/index.jsp`

1. Accédez à `/etc/replications/agents.author` et supprimez les quatre agents de réplication de votre locataire du portail de marque.

   ![](assets/delete-replication-agent.png)

1. Accédez à `/etc/cloudservices/mediaportal` la configuration **du** Cloud Service et supprimez-la.

   ![](assets/delete-cloud-service.png)

1. Accédez à `/home/users/mac` l’utilisateur **** MAC de votre locataire du portail de marque et supprimez-le.

   ![](assets/delete-mac-user.png)


Vous pouvez désormais [créer une configuration](#configure-new-integration-65) via Adobe Developer Console sur votre instance d’auteur AEM 6.5.



<!--
   Comment Type: draft

   <li> </li>
   -->

<!--
   Comment Type: draft

   <li>Step text</li>
   -->


