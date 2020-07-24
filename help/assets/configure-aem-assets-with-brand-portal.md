---
title: Configuration d’AEM Assets avec Brand Portal
seo-title: Configuration d’AEM Assets avec Brand Portal
description: Découvrez comment configurer des AEM Assets avec Brand Portal pour publier des ressources et des collections sur Brand Portal.
seo-description: Découvrez comment configurer des AEM Assets avec Brand Portal pour publier des ressources et des collections sur Brand Portal.
uuid: b95c046e-9988-444c-b50e-ff5ec8cafe14
topic-tags: brand-portal
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
discoiquuid: dca5a2ac-1fc8-4251-b073-730fd6f49b1c
docset: aem65
translation-type: tm+mt
source-git-commit: 76f2df9b1d3e6c2ca7a12cc998d64423d49ebc5b
workflow-type: tm+mt
source-wordcount: '2051'
ht-degree: 59%

---


# Configuration d’AEM Assets avec Brand Portal {#configure-integration-65}

Adobe Experience Manager (AEM) Assets est configuré avec Brand Portal via Adobe Developer Console, qui fournit un jeton IMS pour autoriser votre client Brand Portal.

>[!NOTE]
>
>La configuration des AEM Assets avec le portail de marque via Adobe Developer Console est prise en charge sur AEM 6.5.4.0 et versions ultérieures.
>
>Auparavant, Brand Portal était configuré dans l’interface utilisateur classique via la passerelle OAuth héritée, qui fait appel à l’échange de jetons JWT pour obtenir un jeton d’accès IMS en vue de l’autorisation.
>
>La configuration via application OAuth héritée n’est plus prise en charge à partir du 6 avril 2020 et est remplacée par la configuration via Adobe Developer Console.


>[!TIP]
>
>***Pour les clients existants uniquement***
>
>Il est recommandé de continuer à utiliser la configuration de la passerelle OAuth héritée. Si vous rencontrez des problèmes avec la configuration héritée de la passerelle OAuth, supprimez la configuration existante et créez une nouvelle configuration via Adobe Developer Console.



Cette aide décrit les deux cas d’utilisation suivants :
* [Nouvelle configuration](#configure-new-integration-65): Si vous êtes un nouvel utilisateur du portail de marques et souhaitez configurer votre instance d’auteur AEM Assets avec Brand Portal, vous pouvez créer une nouvelle configuration sur Adobe Developer Console.
* [Configuration](#upgrade-integration-65)de la mise à niveau : Si vous êtes un utilisateur du portail des marques et que votre instance d’auteur AEM Assets est configurée avec Brand Portal sur la passerelle OAuth héritée, il est recommandé de supprimer les configurations existantes et de créer une nouvelle configuration sur Adobe Developer Console.

Cette aide s’adresse à un public familiarisé avec les technologies suivantes :

* Installation, configuration et administration des packages Adobe Experience Manager et AEM.

* Utilisation de systèmes d’exploitation Linux et Microsoft Windows.

## Conditions préalables {#prerequisites}

Pour configurer AEM Assets avec Brand Portal, vous devez disposer des éléments suivants :

* Une instance d’auteur AEM Assets en cours d’exécution avec le dernier Service Pack
* URL du client Brand Portal
* Un utilisateur disposant de droits d’administrateur système sur l’organisation IMS du client Brand Portal


[Téléchargement et installation d’AEM 6.5](#aemquickstart)

[Télécharger et installer le dernier Service Pack AEM](#servicepack)

### Téléchargement et installation d’AEM 6.5 {#aemquickstart}

Il est recommandé d’utiliser AEM 6.5 pour configurer une instance d’auteur AEM. Si vous ne l’avez pas, téléchargez-le à partir des emplacements suivants :

* If you are an existing AEM customer, download AEM 6.5 from [Adobe Licensing website](http://licensing.adobe.com).

* If you are an Adobe partner, use [Adobe Partner Training Program](https://adobe.allegiancetech.com/cgi-bin/qwebcorporate.dll?idx=82357Q) to request AEM 6.5.

Après avoir téléchargé AEM, consultez la page [Déploiement et maintenance](https://docs.adobe.com/content/help/en/experience-manager-65/deploying/deploying/deploy.html#default-local-install) pour obtenir des instructions sur la configuration d’une instance d’auteur AEM.

### Télécharger et installer le dernier Service Pack AEM {#servicepack}

Pour obtenir des instructions détaillées, voir

* [Notes de mise à jour d’AEM 6.5, Pack de services ](https://docs.adobe.com/content/help/en/experience-manager-65/release-notes/service-pack/sp-release-notes.html)

**Contactez le service à la clientèle** si vous ne parvenez pas à trouver le dernier package ou Service Pack d’AEM.

## Création d’une configuration {#configure-new-integration-65}

La configuration des AEM Assets avec le portail de marque nécessite des configurations à la fois dans l’instance d’auteur AEM Assets et dans la console de développement Adobe.

1. Dans l’instance d’auteur AEM Assets, créez un compte IMS et générez un certificat public (clé publique).

1. Dans Adobe Developer Console, créez un projet pour votre client Brand Portal (organisation).

1. Dans le projet, configurez une API à l’aide de la clé publique pour créer une connexion au compte de service (JWT).

1. Obtenez les informations d’identification du compte de service et les informations de charge utile JWT.

1. Dans l’instance d’auteur AEM Assets, configurez le compte IMS à l’aide des informations d’identification du compte de service et de la charge utile JWT.

1. Dans l’instance d’auteur AEM Assets, configurez le service cloud du portail de marque à l’aide du compte IMS et du point de terminaison du portail de marque (URL de l’organisation).

1. Testez la configuration en publiant un fichier de l’instance d’auteur AEM Assets sur Brand Portal.


>[!NOTE]
>
>Un client du portail de marques ne doit être configuré qu’avec une seule instance d’auteur AEM Assets.
>
>Ne configurez pas un client du portail de marques avec plusieurs instances d’auteur AEM Assets.



Effectuez les étapes suivantes dans la séquence répertoriée si vous configurez des AEM Assets avec Brand Portal pour la première fois :
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
   `http:// localhost:4502/aem/start.html`
1. Dans le panneau **Outils** ![Outils](assets/do-not-localize/tools.png), accédez à **[!UICONTROL Sécurité]** > **[!UICONTROL Configurations d’Adobe IMS]**.

   ![Interface utilisateur de configuration du compte Adobe IMS](assets/ims-config1.png)

1. Dans la page Configurations d’Adobe IMS, cliquez sur **[!UICONTROL Créer]**.

1. Vous êtes redirigé vers la page **[!UICONTROL Configuration du compte technique Adobe IMS]**. Par défaut, l’onglet **Certificat** s’ouvre.

   Sélectionnez la solution cloud **[!UICONTROL Adobe Brand Portal]**.

1. Mark the checkbox **[!UICONTROL Create new certificate]** and specify an **alias** for the certificate. L’alias sert de nom à la boîte de dialogue.

1. Cliquez sur **[!UICONTROL Créer un certificat]**. Cliquez ensuite sur **[!UICONTROL OK]** dans la boîte de dialogue pour générer le certificat public.

   ![Création d’un certificat](assets/ims-config2.png)

1. Cliquez sur **[!UICONTROL Télécharger la clé publique]** et enregistrez le fichier de certificat (.crt) sur votre ordinateur.

   Le fichier de certificat sera utilisé à d’autres étapes pour configurer l’API de votre client Brand Portal et générer les informations d’identification de compte de service dans Adobe Developer Console.

   ![Téléchargement du certificat](assets/ims-config3.png)

1. Cliquez sur **[!UICONTROL Suivant]**.

   Dans l’onglet **Compte**, vous créez le compte Adobe IMS. Pour ce faire, vous aurez besoin des informations d’identification du compte de service générées dans Adobe Developer Console. Gardez cette page ouverte pour l’instant.

   Ouvrez un nouvel onglet et [créez une connexion au compte de service (JWT) dans Adobe Developer Console](#createnewintegration) pour obtenir les informations d’identification et la charge utile JWT qui servent à configurer le compte IMS.

### Création d’une connexion au compte de service (JWT) {#createnewintegration}

Dans Adobe Developer Console, les projets et les API sont configurés au niveau de l’organisation (client Brand Portal). La configuration d’une API crée une connexion au compte de service (JWT) dans Adobe Developer Console. Il existe deux méthodes pour configurer l’API : générer une paire de clés (clés privée et publique) ou télécharger une clé publique. Pour configurer l’instance d’auteur AEM Assets avec Brand Portal, vous devez générer un certificat public (clé publique) dans l’instance d’auteur AEM Assets et créer des informations d’identification dans Adobe Developer Console en téléchargeant la clé publique. Cette clé publique permet de configurer l’API pour l’organisation Brand Portal sélectionnée et de générer les informations d’identification ainsi que la charge utile JWT pour le compte de service. Ces informations d’identification sont également utilisées pour configurer le compte IMS dans l’instance d’auteur AEM Assets. Une fois le compte IMS configuré, vous pouvez configurer le service cloud du portail de marque dans l’instance d’auteur AEM Assets.

Procédez comme suit pour générer les informations d’identification du compte de service et la charge utile JWT :

1. Connectez-vous à Adobe Developer Console avec les privilèges d’administrateur système sur l’organisation IMS (client Brand Portal). L’URL par défaut est

   [https://www.adobe.com/go/devs_console_ui_fr](https://www.adobe.com/go/devs_console_ui_fr)


   >[!NOTE]
   >
   >Assurez-vous d’avoir sélectionné l’organisation IMS appropriée (client Brand Portal) dans la liste déroulante (liste d’organisations) située dans l’angle supérieur droit.

1. Cliquez sur **[!UICONTROL Créer un projet]**. Un projet vierge est créé pour votre organisation.

   Cliquez sur **[!UICONTROL Modifier le projet]** pour mettre à jour le **[!UICONTROL Titre du projet]** et la **[!UICONTROL Description]**, puis cliquez sur **[!UICONTROL Enregistrer]**.

   ![Créer un projet](assets/service-account1.png)

1. Dans l’onglet Aperçu du projet, cliquez sur **[!UICONTROL Ajouter une API]**.

   ![Ajouter une API](assets/service-account2.png)

1. Dans la fenêtre Ajouter une API, sélectionnez **[!UICONTROL AEM Brand Portal]**, puis cliquez sur **[!UICONTROL Suivant]**.

   Assurez-vous d’avoir accès au service AEM Brand Portal.

1. Dans la fenêtre Configurer l’API, cliquez sur **[!UICONTROL Charger votre clé publique]**. Cliquez ensuite sur **[!UICONTROL Sélectionner un fichier]** et chargez le certificat public (fichier .crt) que vous avez téléchargé comme indiqué à la section [Obtention d’un certificat public](#public-certificate).

   Cliquez sur **[!UICONTROL Suivant]**.

   ![Charger la clé publique](assets/service-account3.png)

1. Vérifiez le certificat public et cliquez sur **[!UICONTROL Suivant]**.

1. Sélectionnez le profil de produit par défaut **[!UICONTROL Assets Brand Portal]**, puis cliquez sur **[!UICONTROL Enregistrer la configuration]**.

   ![Sélectionner le profil de produit](assets/service-account4.png)

1. Une fois l’API configurée, vous êtes redirigé vers l’aperçu de l’API. Dans le volet de navigation de gauche, sous **[!UICONTROL Informations d’identification]**, cliquez sur **[!UICONTROL Compte de service (JWT)]**.

   >[!NOTE]
   >
   >Vous pouvez voir les informations d’identification et effectuer d’autres actions (générer des jetons JWT, copier les informations d’identification, récupérer le secret client, etc.), si nécessaire.

1. Dans l’onglet **[!UICONTROL Informations d’identification client]**, copiez l’**[!UICONTROL ID client]**.

   Cliquez sur **[!UICONTROL Récupérer le secret client]** et copiez le **[!UICONTROL secret client]**.

   ![Informations d’identification du compte de service](assets/service-account5.png)

1. Accédez à l’onglet **[!UICONTROL Générer le jeton JWT]** et copiez la **[!UICONTROL Charge utile JWT]**.

Vous pouvez maintenant utiliser l’ID client (clé d’API), le secret client et la charge utile JWT pour [configurer le compte IMS](#create-ims-account-configuration) dans l’instance cloud AEM Assets.

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

### Création d’une configuration de compte IMS {#create-ims-account-configuration}

Vérifiez que vous avez effectué les étapes suivantes :

* [Obtention d’un certificat public](#public-certificate)
* [Création d’une connexion au compte de service (JWT)](#createnewintegration)

Procédez comme suit pour configurer le compte IMS créé selon la section [Obtention d’un certificat public](#public-certificate).

1. Ouvrez la configuration IMS et accédez à l’onglet **[!UICONTROL Comptes]**. You kept the page open while [obtaining public certificate](#public-certificate).

1. Spécifiez un **[!UICONTROL titre]** pour le compte IMS.

   Dans **[!UICONTROL Serveur d’autorisation]**, entrez l’adresse URL : [https://ims-na1.adobelogin.com/](https://ims-na1.adobelogin.com/)

   Collez l’ID client dans la clé d’API, le secret client et la charge utile JWT que vous avez copiés lors de la [création d’une connexion au compte de service (JWT)](#createnewintegration).

   Cliquez sur **[!UICONTROL Créer]**.

   Le compte IMS est configuré.

   ![Configuration du compte IMS](assets/create-new-integration6.png)


1. Sélectionnez la configuration IMS et cliquez sur **[!UICONTROL Contrôle de l’intégrité]**.

   Cliquez sur **[!UICONTROL Vérifier]** dans la boîte de dialogue. Une fois la configuration réussie, un message s’affiche avec la mention *Jeton récupéré avec succès*.

   ![](assets/create-new-integration5.png)

>[!CAUTION]
>
>Vous ne devez avoir qu’une seule configuration IMS. N’en créez pas plusieurs.
>
>Assurez-vous que la configuration IMS réussit le contrôle d’intégrité. Si tel n’est pas le cas, elle n’est pas valide. Vous devez la supprimer et créer une configuration valide.



### Configuration du service cloud {#configure-the-cloud-service}

Suivez les étapes ci-après pour créer un service cloud Portal de marque :

1. Connectez-vous à votre instance d’auteur AEM Assets.

1. Dans le panneau **Outils** ![Outils](assets/do-not-localize/tools.png), accédez à **[!UICONTROL Cloud Services]** > **[!UICONTROL AEM Brand Portal]**.

1. Dans la page Configurations Brand Portal, cliquez sur **[!UICONTROL Créer]**.

1. Saisissez un **[!UICONTROL titre]** pour la configuration.

   Sélectionnez la configuration IMS créée lors de la [configuration du compte IMS](#create-ims-account-configuration).

   In the **[!UICONTROL Service URL]**, enter your Brand Portal tenant (organization) URL.

   ![](assets/create-cloud-service.png)

1. Cliquez sur **[!UICONTROL Enregistrer et fermer]**. La configuration cloud est alors créée. Votre instance d’auteur AEM Assets est maintenant configurée avec le client du portail de marque.

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

   Un message s’affiche en bas de la page pour indiquer que votre package de test a été livré.

   ![](assets/test-integration5.png)

1. Vérifiez les résultats du test sur les quatre agents de réplication un par un.


   >[!NOTE]
   >
   >Evitez de désactiver les agents de réplication. Cela peut entraîner l’échec de la réplication de certains actifs.

Votre instance d’auteur AEM Assets a été correctement configurée avec Brand Portal. Vous pouvez désormais :

* [Publication de ressources à partir d’AEM Assets sur Brand Portal](../assets/brand-portal-publish-assets.md)
* [Publication de dossiers à partir d’AEM Assets sur Brand Portal](../assets/brand-portal-publish-folder.md)
* [Publication de collections à partir d’AEM Assets sur Brand Portal](../assets/brand-portal-publish-collection.md)
* [Configurez l’approvisionnement](https://docs.adobe.com/content/help/en/experience-manager-brand-portal/using/asset-sourcing-in-brand-portal/brand-portal-asset-sourcing.html) en ressources pour permettre aux utilisateurs du portail de marque de contribuer et de publier des ressources en AEM Assets.

## Mise à niveau de la configuration {#upgrade-integration-65}

Effectuez les étapes suivantes dans la séquence répertoriée pour mettre à niveau les configurations existantes :
1. [Vérification des tâches en cours](#verify-jobs)
1. [Supprimer les configurations existantes](#delete-existing-configuration)
1. [Création d’une configuration](#configure-new-integration-65)

### Vérification des tâches en cours {#verify-jobs}

Assurez-vous qu’aucune tâche de publication n’est exécutée sur votre instance d’auteur AEM Assets avant d’apporter des modifications. Pour cela, vous pouvez vérifier les quatre agents de réplication et vous assurer que les files d’attente sont vides.

1. Connectez-vous à votre instance d’auteur AEM Assets.

1. From the **Tools** ![Tools](assets/do-not-localize/tools.png) panel, navigate to **[!UICONTROL Deployment]** > **[!UICONTROL Deployment Replication]**.

1. Sur la page Réplication, cliquez sur **[!UICONTROL Agents sur l’auteur]**.

   ![](assets/test-integration2.png)

1. Localisez les agents de réplication de votre locataire du portail de marque.

   Assurez-vous que la **file d&#39;attente est inactive** pour tous les agents de réplication, aucun travail de publication n&#39;est actif.

   ![](assets/test-integration3.png)

### Supprimer les configurations existantes {#delete-existing-configuration}

Vous devez exécuter la liste de vérification suivante lors de la suppression des configurations existantes.
* Supprimer les quatre agents de réplication
* Suppression du service cloud
* Supprimer un utilisateur MAC

1. Connectez-vous à votre instance d’auteur AEM Assets et ouvrez CRX Lite en tant qu’administrateur. L’URL par défaut est

   `http:// localhost:4502/crx/de/index.jsp`

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


