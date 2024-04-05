---
title: Configuration d’AEM Assets avec Brand Portal
description: Découvrez comment configurer AEM Assets à Brand Portal pour publier des ressources et des collections sur Brand Portal.
topic-tags: brand-portal
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
docset: aem65
feature: Brand Portal
role: Admin
exl-id: ae33181c-9eec-421c-be55-4bd019de40b8
hide: true
solution: Experience Manager, Experience Manager Assets
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '2068'
ht-degree: 100%

---


# Configuration d’AEM Assets avec Brand Portal {#configure-integration-65}

| Version | Lien de l’article |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Cliquez ici](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/brand-portal/configure-aem-assets-with-brand-portal.html?lang=fr) |
| AEM 6.5 | Cet article |

Adobe Experience Manager Assets Brand Portal permet de publier des ressources de marque approuvées d’Adobe Experience Manager Assets vers Brand Portal et de les distribuer aux utilisateurs et utilisatrices de Brand Portal.

AEM Assets est configuré avec Brand Portal via la console Adobe Developer, qui fournit un jeton de compte Adobe Identity Management Services (IMS) pour l’autorisation du client Brand Portal.

>[!NOTE]
>
>La configuration d’AEM Assets avec Brand Portal via la console Adobe Developer est prise en charge sur AEM 6.5.4.0 et les versions ultérieures.
>
>Auparavant, Brand Portal était configuré dans l’interface classique via la passerelle OAuth héritée, qui fait appel à l’échange de jetons d’accès Web JSON (JWT) pour obtenir un jeton IMS en vue de l’autorisation.
>
>La configuration via application OAuth héritée n’est plus prise en charge à partir du 6 avril 2020 et est remplacée par la configuration via la console Adobe Developer.

>[!TIP]
>
>***Pour les clients existants uniquement***
>
>Adobe vous recommande de continuer à utiliser l’ancienne configuration de la passerelle OAuth. Si vous rencontrez des problèmes avec l’ancienne configuration de la passerelle OAuth, supprimez la configuration existante et créez une configuration à l’aide d’Adobe Developer Console.

Cette aide décrit les deux cas d’utilisation suivants :

* [Nouvelle configuration](#configure-new-integration-65) : si vous êtes un nouvel utilisateur ou une nouvelle utilisatrice de Brand Portal et que vous souhaitez configurer votre instance de création AEM Assets avec Brand Portal, vous pouvez créer une configuration via Adobe Developer Console.
* [Configuration de la mise à niveau](#upgrade-integration-65) : si vous êtes un utilisateur ou une utilisatrice de Brand Portal disposant d’une configuration sur l’ancienne passerelle OAuth, supprimez la configuration existante et créez une configuration via Adobe Developer Console.

Cette aide s’adresse à un public familiarisé avec les technologies suivantes :

* installation, configuration et administration des packages Adobe Experience Manager et AEM ;

* utilisation des systèmes d’exploitation Linux® et Microsoft® Windows.

## Prérequis {#prerequisites}

Pour configurer AEM Assets avec Brand Portal, vous devez disposer des éléments suivants :

* une instance de création AEM Assets en cours d’exécution avec le dernier pack de services ;
* Une adresse URL du client Brand Portal
* Un utilisateur disposant de droits d’administrateur système sur l’organisation IMS du client Brand Portal

[Télécharger et installer AEM 6.5](#aemquickstart)

[Télécharger et installer le dernier pack de services AEM](#servicepack)

### Télécharger et installer AEM 6.5 {#aemquickstart}

Il est recommandé d’utiliser AEM 6.5 pour configurer une instance de création AEM. Si vous ne l’avez pas, téléchargez-le à partir des emplacements suivants :

* Si vous êtes déjà client ou cliente AEM, téléchargez AEM 6.5 sur le [site web Adobe Licensing](https://licensing.adobe.com).

* Si vous êtes un ou une partenaire Adobe, utilisez le [programme de formation des partenaires Adobe](https://adobe.allegiancetech.com/cgi-bin/qwebcorporate.dll?idx=82357Q) pour demander AEM 6.5.

Après avoir téléchargé AEM, consultez la page [Déploiement et maintenance](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/deploying/deploy.html?lang=fr#default-local-install) pour obtenir des instructions sur la configuration d’une instance de création AEM.

### Télécharger et installer le dernier pack de services AEM {#servicepack}

Pour obtenir des instructions détaillées, reportez-vous à la section [Notes de mise à jour du pack de services AEM 6.5](https://experienceleague.adobe.com/docs/experience-manager-65/release-notes/release-notes.html?lang=fr).

**Contactez le service clientèle d’Adobe** si vous ne trouvez pas le dernier package ou le pack de services AEM.

## Création d’une configuration {#configure-new-integration-65}

La configuration d’AEM Assets avec Brand Portal nécessite des configurations à la fois dans l’instance de création AEM Assets et dans Adobe Developer Console.

1. Dans AEM Assets, créez un compte IMS et générez un certificat public (clé publique).
1. Dans Adobe Developer Console, créez un projet pour votre client Brand Portal (organisation).
1. Dans le projet, configurez une API à l’aide de la clé publique pour créer une connexion au compte de service (JWT).
1. Obtenez les informations d’identification du compte de service et les informations de charge utile JWT.
1. Dans AEM Assets, configurez le compte IMS à l’aide des informations d’identification du compte de service et de la charge utile JWT.
1. Dans AEM Assets, configurez le service cloud Brand Portal à l’aide du compte IMS et du point d’entrée Brand Portal (URL de l’organisation).
1. Testez votre configuration en publiant une ressource d’AEM Assets sur Brand Portal.

>[!NOTE]
>
>Une instance de création AEM Assets ne doit être configurée qu’avec un seul client Brand Portal.

Effectuez les étapes suivantes dans l’ordre indiqué si vous configurez AEM Assets avec Brand Portal pour la première fois :

1. [Obtention d’un certificat public](#public-certificate)
1. [Créer une connexion au compte de service (JWT)](#createnewintegration).
1. [Configuration d’un compte IMS](#create-ims-account-configuration)
1. [Configuration du service cloud](#configure-the-cloud-service)
1. [Test de la configuration](#test-integration)

### Création de la configuration IMS {#create-ims-configuration}

La configuration IMS authentifie votre instance de création AEM Assets auprès du client Brand Portal.

La configuration IMS comprend deux étapes :

* [Obtention d’un certificat public](#public-certificate)
* [Configuration d’un compte IMS](#create-ims-account-configuration)

### Obtention d’un certificat public {#public-certificate}

La clé publique (certificat) authentifie votre profil sur Adobe Developer Console.

1. Connectez-vous à votre instance de création AEM Assets. L’URL par défaut est `http://localhost:4502/aem/start.html`.

1. Dans les **Outils** du panneau ![Outils](assets/do-not-localize/tools.png), accédez à **[!UICONTROL Sécurité]** > **[!UICONTROL Configurations d’Adobe IMS]**.

1. Dans la page Configurations d’Adobe IMS, cliquez sur **[!UICONTROL Créer]**. Vous êtes redirigé vers la page **[!UICONTROL Configuration du compte technique Adobe IMS]**. Par défaut, l’onglet **Certificat** s’ouvre.

1. Sélectionnez **[!UICONTROL Adobe Brand Portal]** dans la liste déroulante **[!UICONTROL Solution cloud]**.

1. Cochez la case **[!UICONTROL Créer un certificat]** et spécifiez un **alias** pour la clé publique. L’alias constitue le nom de la clé publique.

1. Cliquez sur **[!UICONTROL Créer un certificat]**. Cliquez sur **[!UICONTROL OK]** pour générer la clé publique.

   ![Création d’un certificat](assets/ims-config2.png)

1. Cliquez sur l’icône **[!UICONTROL Télécharger la clé publique]** et enregistrez le fichier de clé publique (.crt) sur votre ordinateur.

   La clé publique est utilisée ultérieurement pour configurer l’API de votre client Brand Portal et générer des informations d’identification de compte de service dans Adobe Developer Console.

   ![Téléchargement du certificat](assets/ims-config3.png)

1. Cliquez sur **[!UICONTROL Suivant]**.

   Dans l’onglet **Compte**, un compte Adobe IMS est créé, lequel nécessite les informations d’identification du compte de service qui sont générées dans Adobe Developer Console. Gardez cette page ouverte pour l’instant.

   Ouvrez un nouvel onglet et [créez une connexion au compte de service (JWT) dans Adobe Developer Console](#createnewintegration) pour obtenir les informations d’identification et la payload JWT qui servent à configurer le compte IMS.

### Création de la connexion au compte de service (JWT) {#createnewintegration}

Dans Adobe Developer Console, les projets et les API sont configurés au niveau du client Brand Portal (organisation). La configuration d’une API crée une connexion au compte de service (JWT). Il existe deux méthodes pour configurer l’API : générer une paire de clés (clés privée et publique) ou charger une clé publique. Pour configurer AEM Assets avec Brand Portal, vous devez générer une clé publique (certificat) dans AEM Assets et créer des informations d’identification dans Adobe Developer Console en chargeant la clé publique. Ces informations d’identification sont requises pour configurer le compte IMS dans AEM Assets. Une fois le compte IMS configuré, vous pouvez configurer le service cloud Brand Portal dans AEM Assets.

Pour créer les informations d’identification du compte de service et la payload JWT, procédez comme suit :

1. Connectez-vous à Adobe Developer Console avec les privilèges d’administrateur ou d’administratrice système sur l’organisation IMS (client Brand Portal). L’URL par défaut est [https://www.adobe.com/go/devs_console_ui](https://www.adobe.com/go/devs_console_ui).


   >[!NOTE]
   >
   >Assurez-vous d’avoir sélectionné l’organisation IMS appropriée (client Brand Portal) dans la liste déroulante (liste d’organisations) en haut à droite.

1. Cliquez sur **[!UICONTROL Create new project]** (Créer un projet). Un projet vierge portant un nom généré par le système est créé pour votre organisation.

   Cliquez sur **[!UICONTROL Modifier le projet]** pour mettre à jour le **[!UICONTROL Titre du projet]** et la **[!UICONTROL Description]**, puis cliquez sur **[!UICONTROL Enregistrer]**.

1. Dans l’onglet **[!UICONTROL Project overview]** (Aperçu du projet), cliquez sur **[!UICONTROL Add API]** (Ajouter une API).

1. Dans la fenêtre **[!UICONTROL Add API]** (Ajouter une API), sélectionnez **[!UICONTROL AEM Brand Portal]**, puis cliquez sur **[!UICONTROL Next]** (Suivant).

   Assurez-vous d’avoir accès au service AEM Brand Portal.

1. Dans la fenêtre **[!UICONTROL Configure API]** (Configurer l’API), cliquez sur **[!UICONTROL Upload your public key]** (Charger votre clé publique). Cliquez ensuite sur **[!UICONTROL Select a File]** (Sélectionner un fichier) et chargez la clé publique (fichier .crt) que vous avez téléchargé comme indiqué à la section [Obtain public certificate](#public-certificate) (Obtention d’un certificat public).

   Cliquez sur **[!UICONTROL Next]** (Suivant).

   ![Charger la clé publique](assets/service-account3.png)

1. Vérifiez la clé publique et cliquez sur **[!UICONTROL Next]** (Suivant).

1. Sélectionnez **[!UICONTROL Assets Brand Portal]** comme profil de produit par défaut et cliquez sur **[!UICONTROL Save configured API]** (Enregistrer l’API configurée).

   <!-- 
   In Brand Portal, a default profile is created for each organization. The Product Profiles are created in admin console for assigning users to groups (based on the roles and permissions). For configuration with Brand Portal, the OAuth token is created at organization level. Therefore, you must configure the default Product Profile for your organization. 
   -->

   ![Sélectionner le profil de produit](assets/service-account4.png)

1. Après la configuration de l’API, vous êtes redirigé vers sa page d’aperçu. Dans la navigation de gauche, sous **[!UICONTROL Identifiants]**, cliquez sur **[!UICONTROL Compte de service (JWT)]**.

   >[!NOTE]
   >
   >Vous pouvez alors afficher les identifiants et effectuer des actions telles que la génération des jetons JWT, la copie des informations d’identification et la récupération du secret client.

1. Dans l’onglet **[!UICONTROL Client Credentials]** (Informations d’identification client), copiez l’**[!UICONTROL ID client]**.

   Cliquez sur **[!UICONTROL Retrieve Client Secret]** (Récupérer le secret client) et copiez le **[!UICONTROL secret client]**.

   ![Informations d’identification du compte de service](assets/service-account5.png)

1. Accédez à l’onglet **[!UICONTROL Generate JWT]** (Générer le jeton JWT) et copiez les informations **[!UICONTROL JWT Payload]** (Charge utile JWT).

Vous pouvez maintenant utiliser l’ID client (clé API), le secret client et la charge utile JWT pour [configurer le compte IMS](#create-ims-account-configuration) dans AEM Assets.

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

   The API Key, Client Secret key, and JWT payload information that is used to create IMS account configuration.
-->

### Configuration du compte IMS {#create-ims-account-configuration}

Vérifiez que vous avez déjà effectué les étapes suivantes :

* [Obtention d’un certificat public](#public-certificate)
* [Création de la connexion au compte de service (JWT)](#createnewintegration)

Pour configurer le compte IMS, procédez comme suit :

1. Ouvrez la configuration IMS et accédez à l’onglet **[!UICONTROL Compte]**. Vous avez maintenu la page ouverte lors de l’[obtention du certificat public](#public-certificate).

1. Spécifiez un **[!UICONTROL titre]** pour le compte IMS.

   Dans le champ **[!UICONTROL Serveur d’autorisation]**, spécifiez l’adresse URL : [https://ims-na1.adobelogin.com/](https://ims-na1.adobelogin.com/).

   Spécifiez l’ID client dans le champ **[!UICONTROL Clé API]**, le **[!UICONTROL Secret client]** et la **[!UICONTROL Charge utile]** (charge utile JWT) que vous avez copiés lors de la [création d’une connexion au compte de service (JWT)](#createnewintegration).

   Cliquez sur **[!UICONTROL Créer]**.

   Le compte IMS est configuré.

   ![Configuration du compte IMS](assets/create-new-integration6.png)

1. Sélectionnez la configuration de compte IMS et cliquez sur **[!UICONTROL Contrôle de l’intégrité]**.

   Cliquez sur **[!UICONTROL Vérifier]** dans la boîte de dialogue. Une fois la configuration réussie, un message s’affiche avec la mention *Jeton récupéré avec succès*.

   ![Boîte de dialogue de confirmation de configuration saine](assets/create-new-integration5.png)

>[!CAUTION]
>
>Vous ne devez avoir qu’une seule configuration IMS.
>
>Assurez-vous que la configuration IMS réussit le contrôle d’intégrité. Si tel n’est pas le cas, elle n’est pas valide. Supprimez-la et créez une autre configuration valide.

### Configuration du service cloud Brand Portal {#configure-the-cloud-service}

1. Connectez-vous à votre instance de création AEM Assets.

1. Dans le panneau **Outils** ![Outils](assets/do-not-localize/tools.png), accédez à **[!UICONTROL Cloud Services]** > **[!UICONTROL AEM Brand Portal]**.

1. Dans la page Configurations Brand Portal, cliquez sur **[!UICONTROL Créer]**.

1. Saisissez un **[!UICONTROL titre]** pour la configuration.

   Sélectionnez la configuration IMS créée lors de la [configuration du compte IMS](#create-ims-account-configuration).

   Dans le champ **[!UICONTROL URL du service]**, indiquez l’adresse URL de votre client Brand Portal (organisation).

   ![Fenêtre de configuration Brand Portal](assets/create-cloud-service.png)

1. Cliquez sur **[!UICONTROL Enregistrer et fermer]**. La configuration cloud est alors créée.

   Votre instance de création AEM Assets est maintenant configurée avec le client Brand Portal.

### Test et validation de la configuration {#test-integration}

1. Connectez-vous à votre instance cloud AEM Assets.

1. Dans les **Outils** du panneau ![Outils](assets/do-not-localize/tools.png), accédez à **[!UICONTROL Déploiement]** > **[!UICONTROL Réplication]**.

   ![Panneau Outils](assets/test-integration1.png)

1. Sur la page Réplication, cliquez sur **[!UICONTROL Agents sur l’auteur]**.

   ![Page Réplication](assets/test-integration2.png)

   Vous voyez les quatre agents de réplication pour votre client Brand Portal.

   Recherchez les agents de réplication de votre client Brand Portal et cliquez sur l’URL de l’agent de réplication.

   ![Configuration de la réplication des ressources](assets/test-integration3.png)

   >[!NOTE]
   >
   >Les agents de réplication fonctionnent en parallèle et partagent la distribution des tâches à parts égales, ce qui multiplie par quatre la vitesse de publication par rapport à la vitesse d’origine. Une fois le service cloud configuré, aucune configuration supplémentaire n’est nécessaire pour activer les agents de réplication qui sont activés par défaut de façon à permettre la publication en parallèle de plusieurs ressources.

1. Pour vérifier la connexion entre AEM Assets et Brand Portal, cliquez sur l’icône **[!UICONTROL Tester la connexion]**.

   ![Vérification des paramètres de réplication des ressources](assets/test-integration4.png)

   Un message s’affiche indiquant que votre *package de test a bien été livré*.

   ![Sortie de confirmation de test](assets/test-integration5.png)

1. Vérifiez les résultats du test sur les quatre agents de réplication.


   >[!NOTE]
   >
   >Évitez de désactiver un agent de réplication car cela peut entraîner l’échec de la réplication de certaines ressources (en cours de traitement).
   >
   >Assurez-vous que les quatre agents de réplication sont configurés pour éviter toute erreur de délai d’expiration. Consultez [Dépannage des problèmes de publication en parallèle sur Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/publish/troubleshoot-parallel-publishing.html?lang=fr#connection-timeout).
   >
   >Ne modifiez aucun paramètre généré automatiquement.

Vous pouvez maintenant effectuer les tâches suivantes :

* [Publication de ressources à partir d’AEM Assets sur Brand Portal](../assets/brand-portal-publish-assets.md)
* [Publication de ressources de Brand Portal vers AEM Assets](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/asset-sourcing-in-brand-portal/brand-portal-asset-sourcing.html?lang=fr) – Découverte de ressources dans Brand Portal
* [Publication de dossiers à partir d’AEM Assets sur Brand Portal](../assets/brand-portal-publish-folder.md)
* [Publication de collections à partir d’AEM Assets sur Brand Portal](../assets/brand-portal-publish-collection.md)
* [Publication de paramètres prédéfinis, de schémas et de facettes sur Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/publish/publish-schema-search-facets-presets.html?lang=fr)
* [Publication de balises sur Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/publish/brand-portal-publish-tags.html?lang=fr)

Pour plus d’informations, voir la [documentation de Brand Portal](https://experienceleague.adobe.com/docs/experience-manager-brand-portal/using/home.html?lang=fr).


## Mise à niveau de la configuration {#upgrade-integration-65}

Pour mettre à niveau vos configurations existantes vers Adobe Developer Console, procédez comme suit, dans l’ordre indiqué :

1. [Vérification des tâches en cours](#verify-jobs)
1. [Suppression des configurations existantes](#delete-existing-configuration)
1. [Création d’une configuration](#configure-new-integration-65)

### Vérification des tâches en cours {#verify-jobs}

Assurez-vous qu’aucune tâche de publication n’est en cours d’exécution sur votre instance de création AEM Assets avant d’apporter des modifications. Pour ce faire, vous pouvez vérifier le statut des tâches principales sur les quatre agents de réplication et vous assurer que les files d’attente sont inactives.

1. Connectez-vous à votre instance de création AEM Assets.

1. Dans les **Outils** du panneau ![Outils](assets/do-not-localize/tools.png), accédez à **[!UICONTROL Déploiement]** > **[!UICONTROL Réplication du déploiement]**.

1. Sur la page Réplication, cliquez sur **[!UICONTROL Agents sur l’auteur]**.

   ![Agents de réplication pour les ressources](assets/test-integration2.png)

1. Localisez les agents de réplication de votre client Brand Portal.

   Assurez-vous que **La file d’attente est inactive** pour tous les agents de réplication et qu’aucune tâche de publication n’est active.

   ![Paramètres de file d’attente de réplication](assets/test-integration3.png)

### Suppression des configurations existantes {#delete-existing-configuration}

Exécutez la liste de contrôle suivante avant de supprimer les configurations existantes :

* Suppression des quatre agents de réplication
* Suppression du service cloud Brand Portal
* Suppression de l’utilisateur ou l’utilisatrice MAC

1. Connectez-vous à votre instance de création AEM Assets et ouvrez CRX Lite en tant qu’administrateur ou administratrice. L’URL par défaut est `http://localhost:4502/crx/de/index.jsp`.

1. Accédez à `/etc/replications/agents.author` et supprimez les quatre agents de réplication de votre client Brand Portal.

   ![Agent de réplication dans CRXDE](assets/delete-replication-agent.png)

1. Accédez à `/etc/cloudservices/mediaportal` et supprimez la configuration du service cloud Brand Portal.

   ![Détail de l’agent de réplication dans CRXDE](assets/delete-cloud-service.png)

1. Accédez à `/home/users/mac` et supprimez l’**utilisateur Mac** de votre client Brand Portal.

   ![Plus de détails sur l’agent de réplication dans CRXDE](assets/delete-mac-user.png)


Vous pouvez désormais [créer une configuration](#configure-new-integration-65) au moyen d’Adobe Developer Console sur votre instance de création AEM 6.5.



<!--
   Comment Type: draft

   <li> </li>
   -->

<!--
   Comment Type: draft

   <li>Step text</li>
   -->
