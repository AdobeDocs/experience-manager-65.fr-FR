---
title: 'Gestion des ressources  [!DNL Adobe Stock] '
description: Rechercher, récupérer, gérer les licences et gérer les ressources [!DNL Adobe Stock] dans [!DNL Adobe Experience Manager]. Utiliser les ressources sous licence comme toute autre ressource numérique.
contentOwner: Vishabh Gupta
feature: Search, Adobe Stock
role: User, Admin
exl-id: 8ec597df-bb64-4768-bf9c-e8cca4fea25b
hide: true
solution: Experience Manager, Experience Manager Assets
source-git-commit: 07289e891399a78568dcac957bc089cc08c7898c
workflow-type: tm+mt
source-wordcount: '2191'
ht-degree: 100%

---

# Utiliser des ressources de [!DNL Adobe Stock] dans [!DNL Adobe Experience Manager Assets] {#use-adobe-stock-assets-in-aem-assets}

| Version | Lien de l’article |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Cliquez ici](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/manage/aem-assets-adobe-stock.html?lang=fr) |
| AEM 6.5 | Cet article |

<!-- old content

[!DNL Experience Manager Assets] provides users the ability to search, preview, save, and license [!DNL Adobe Stock] assets directly from [!DNL Experience Manager].. 

Organizations can integrate their [!DNL Adobe Stock] enterprise plan with [!DNL Experience Manager Assets] to ensure that licensed assets are broadly available for their creative and marketing projects, with the powerful asset management capabilities of [!DNL Experience Manager].

[!DNL Adobe Stock] service provides designers and businesses with access to millions of high-quality, curated, royalty-free photos, vectors, illustrations, videos, templates, and 3D assets for all their creative projects. [!DNL Experience Manager] users are able to quickly find, preview, and license [!DNL Adobe Stock] assets that are saved in [!DNL Experience Manager], without leaving the [!DNL Experience Manager] interface.
-->

<!-- New overview content
-->

Le service [!DNL Adobe Stock] permet aux concepteurs et aux entreprises d’accéder à des millions de photos, de vecteurs, d’illustrations, de vidéos, de modèles et de ressources 3D organisés, de grande qualité et libres de droits d’auteur pour tous leurs projets de création. 

[!DNL Adobe Stock] pour l’offre d’entreprise, inclut par défaut des droits de partage à l’échelle de l’entreprise. Une fois qu’une ressource a obtenu une licence d’un utilisateur de votre entreprise, d’autres utilisateurs de votre entreprise peuvent l’identifier, la télécharger et l’utiliser sans avoir à la renouveler. Une fois qu’une ressource a obtenu une licence de votre entreprise, le droit de l’utiliser est perpétuel.

Les entreprises peuvent intégrer leur formule d’abonnement [!DNL Adobe Stock] pour entreprise dans [!DNL Experience Manager Assets] pour s’assurer que les ressources sous licence sont mises à la disposition de leurs projets de création et marketing, tout en bénéficiant des puissantes fonctionnalités de gestion de ressources numériques de [!DNL Experience Manager]. Les utilisateurs d’[!DNL Experience Manager] peuvent en un éclair, rechercher, prévisualiser et acquérir sous licence des ressources Adobe Stock qui sont enregistrées dans [!DNL Experience Manager], sans quitter l’interface d’[!DNL Experience Manager].

<!-- Old content
## Prerequisites {#prerequisites}

The integration requires an [enterprise [!DNL Adobe Stock] plan](https://stockenterprise.adobe.com/).
-->

## Conditions préalables à l’intégration d’[!DNL Experience Manager] et [!DNL Adobe Stock] {#integrate-aem-and-adobe-stock}

[!DNL Experience Manager Assets] permet aux utilisateurs et utilisatrices de rechercher, de prévisualiser, d’enregistrer et d’acquérir sous licence des ressources [!DNL Adobe Stock] directement à partir d’[!DNL Experience Manager].

Les conditions préalables ci-après doivent être respectées pour activer cette intégration :

* Une formule d’abonnement à [!DNL Adobe Stock] pour entreprise.
* Un utilisateur ou une utilisatrice disposant d’autorisations dans [!DNL Admin Console] sur le profil de produit Stock par défaut.
* Un utilisateur ou une utilisatrice disposant d’autorisations sur le [!DNL Developer Access profile] pour la création d’une intégration dans [!DNL Adobe Developer Console].

Une formule d’abonnement à [!DNL Adobe Stock] pour entreprise,

* Fournit les droits de produit pour [!DNL Adobe Stock] (Stocks connectés à Experience Manager).
* Achat de crédits dans la [!DNL Adobe Admin Console] pour vos droits de stock.
* Permet de gérer les crédits et les licences à l’échelle mondiale à partir d’[!DNL Adobe Admin Console].

Dans les droits, un profil de produit par défaut pour [!DNL Adobe Stock] existe dans [!DNL Admin Console]. Plusieurs profils peuvent être créés et ils déterminent qui peut acquérir des ressources Stock sous licence. Un utilisateur disposant d’un accès direct au profil de produits peut accéder à [https://stock.adobe.com/fr](https://stock.adobe.com/fr) et acquérir des ressources Stock sous licence. Cependant, il existe une autre méthode d’utilisation de l’Accès des développeurs pour créer une intégration (API). Cette intégration authentifie la communication entre [!DNL Experience Manager Assets] et [!DNL Adobe Stock].

<!-- old content
## Integrate [!DNL Experience Manager] and [!DNL Adobe Stock] {#integrate-aem-and-adobe-stock}

[!DNL Experience Manager Assets] provides users the ability to search, preview, save, and license [!DNL Adobe Stock] assets directly from [!DNL Experience Manager].

**Prerequisites**

The integration requires: 

* An [enterprise [!DNL Adobe Stock] plan](https://stockenterprise.adobe.com/)
* A user with permissions in Admin Console to the default Stock product profile
* A user with permissions to the Developer Access profile for creating integration in Adobe Developer Console

An enterprise [!DNL Adobe Stock] plan,

* Provides product entitlement for [!DNL Adobe Stock] (Stocks connected to Experience Manager)
* Credits purchased into the [!DNL Adobe Admin Console] for your stock entitlement
* Enables Service Account (JWT) authentication within [!DNL Adobe Developer Console] for your stock entitlement
* Enables managing the credits and licensing globally from within [!DNL Adobe Admin Console]

Within the entitlement, a default product profile for [!DNL Adobe Stock] exists in [!DNL Admin Console]. Multiple profiles can be created, and these profiles determines who can license Stock assets. A user having access directly to the product profile can access [https://stock.adobe.com/](https://stock.adobe.com/) and license Stock assets. Whereas there is another method of using the Developer Access to create integration (API) to authenticate communication between [!DNL Experience Manager] and [!DNL Adobe Stock].

>[!NOTE]
>
>The Stock service account (JWT) authentication comes with the enterprise Stock entitlement.
>
>The integration does not support Oauth authentication for enterprise Stock entitlement.

<!-- old content
To allow communication between [!DNL Experience Manager] and [!DNL Adobe Stock], create an IMS configuration and an [!DNL Adobe Stock] configuration in [!DNL Experience Manager].

>[!NOTE]
>
>Only [!DNL Experience Manager] administrators and [!DNL Admin Console] administrators for an organization can perform the integration as it requires administrator privileges.
-->

## Intégration d’[!DNL Experience Manager] et [!DNL Adobe Stock] {#integrate-adobe-stock-with-aem-assets}

En tant que développeur ou développeuse, exécutez les étapes suivantes pour intégrer [!DNL Adobe Experience Manager] et [!DNL Adobe Stock].

1. [Configurer un programme dans la  [!DNL Developer Console]](#set-up-a-program-in-developer-console)
1. [Ajouter la configuration dans l’instance de création  [!DNL AEM] ](#add-configuration-in-the-aem-author-instance)

### Configurer un programme dans la [!DNL Developer Console] {#set-up-a-program-in-developer-console}

Pour configurer un programme dans la [!DNL Developer Console], procédez comme suit :
1. Accédez à la [[!DNL Adobe Developer Console]](https://developer.adobe.com/console/14431/user/servicesandapis) et connectez-vous à votre organisation.
1. Sélectionnez **[!UICONTROL Créer un projet]** dans le tableau de bord **[!UICONTROL Projets]**.
   ![intégrer aem assets à adobe stock](/help/assets/assets/create-new-project-in-adobe-dev-console.png)
1. Cliquez sur **[!UICONTROL Ajouter au projet]** et sélectionnez **[!UICONTROL API]**.
1. Sélectionnez **[!UICONTROL Adobe Stock]**, puis cliquez sur **[!UICONTROL Suivant]**.
1. Spécifiez un **[!UICONTROL Nom d’identification]** et vérifiez que l’option **[!UICONTROL OAuth serveur à serveur]** est sélectionnée, puis cliquez sur **[!UICONTROL Suivant]**.
1. Sélectionnez **[!UICONTROL AEM Assets]** **[!UICONTROL Profil de produit]** et cliquez sur **[!UICONTROL Enregistrer l’API configurée]**. Un message s’affiche pour confirmer que vous avez créé un projet dans la [!DNL Developer Console]. Le tableau de bord de votre projet s’ouvre. Il affiche le nom du projet en haut, **[!UICONTROL Adobe Stock]** sous **[!UICONTROL API]**, **[!UICONTROL AEM Assets]** sous **[!UICONTROL Profil de produit]** et la carte d’informations d’identification **[!UICONTROL OAuth de serveur à serveur]** sous **[!UICONTROL Informations d’identification connectées]**.
   ![intégrer aem assets à adobe stock](/help/assets/assets/adc-project-name.png)
1. Sélectionnez la carte d’informations d’identification **[!UICONTROL OAuth serveur à serveur]**. Les **[!UICONTROL Détails des informations d’identification]** s’affichent. Utilisez ces informations d’identification [!DNL OAuth Server-to-Server] de votre projet, telles que **[!UICONTROL ID client]**, **[!UICONTROL Secret client]**, **[!UICONTROL Portée]**, **[!UICONTROL Nom d’identification]**, **[!UICONTROL ID de compte technique]** et **[!UICONTROL ID d’organisation]** pour [ajouter la configuration dans l’instance de création AEM](#add-configuration-in-the-aem-author-instance).
   ![aem assets et adobe stock](/help/assets/assets/oauth-server-server-credentials-details-page.png)

### Ajouter la configuration dans l’instance de création [!DNL AEM] {#add-configuration-in-the-aem-author-instance}

Exécutez les étapes suivantes pour ajouter une configuration à votre instance de création [!DNL AEM] :

1. [Configurer une nouvelle  [!DNL Adobe Stock IMS configuration]  dans votre instance de création  [!DNL AEM] ](#set-up-adobe-stock-ims-configuration-in-aem-author-instance)
1. [Ajouter la configuration cloud à laquelle connecter  [!DNL Adobe Stock]](#add-cloud-configuration-to-connect-adobe-stock)

#### Configurer une nouvelle [!DNL Adobe Stock IMS configuration] dans votre instance [!DNL AEM author] {#set-up-adobe-stock-ims-configuration-in-aem-author-instance}

Pour configurer une nouvelle [!DNL Adobe Stock IMS configuration] dans votre instance de création [!DNL AEM], procédez comme suit :
1. Connectez-vous à votre instance de création [!DNL AEM].
1. Cliquez sur ![Aem Assets et Adobe Stock](/help/assets/assets/Hammer.svg), sélectionnez **[!UICONTROL Sécurité]**, puis **[!UICONTROL Configurations d’Adobe IMS]**.
1. Cliquez sur **[!UICONTROL Créer]** pour créer une configuration IMS. La page **[!UICONTROL Configuration du compte technique Adobe IMS]** affiche plusieurs champs tels que **[!UICONTROL Solution cloud]**, **[!UICONTROL Titre]**, **[!UICONTROL Serveur d’autorisation]**, **[!UICONTROL ID client]**, **[!UICONTROL Secret client]**, **[!UICONTROL Portée]** et **[!UICONTROL ID d’organisation]**. Suivez ces instructions pour spécifier les détails dans ces champs :
   * **[!UICONTROL Solution Cloud]** : sélectionnez **[!UICONTROL Adobe Stock]**.
   * **[!UICONTROL Titre]** : indiquez un nom pour cette intégration.
   * **[!UICONTROL Serveur d’autorisation]** : ajoutez [https://ims-na1.adobelogin.com/](https://ims-na1.adobelogin.com/) en tant que serveur d’autorisation.
   * **[!UICONTROL ID client]** : accédez au tableau de bord de votre projet, cliquez sur l’option **[!UICONTROL OAuth serveur à serveur]** disponible dans le volet de gauche, sélectionnez **[!UICONTROL Informations d’identification]**, copiez l’**[!UICONTROL ID client]** et collez-le ici (voir [étape 7](#set-up-a-program-in-developer-console)).

   * **[!UICONTROL Secret client]** : accédez au tableau de bord de votre projet, cliquez sur l’option **[!UICONTROL OAuth de serveur à serveur]** disponible dans le volet de gauche, sélectionnez **[!UICONTROL Informations d’identification]**, cliquez sur **[!UICONTROL Récupérer le secret client]**, copiez le **[!UICONTROL secret client]** et collez-le ici (voir [étape 7](#set-up-a-program-in-developer-console)).

   * **[!UICONTROL Portée]** : accédez au tableau de bord de votre projet, cliquez sur l’option **[!UICONTROL OAuth serveur à serveur]** disponible dans le volet de gauche, sélectionnez **[!UICONTROL Informations d’identification]**, copiez la **[!UICONTROL Portée]** et collez-la ici (voir [étape 7](#set-up-a-program-in-developer-console)).

   * **[!UICONTROL ID d’organisation]** : accédez au tableau de bord de votre projet, cliquez sur l’option **[!UICONTROL OAuth serveur à serveur]** disponible dans le volet de gauche, sélectionnez **[!UICONTROL Informations d’identification]**, copiez l’**[!UICONTROL ID d’organisation]** et collez-le ici (voir [étape 7](#set-up-a-program-in-developer-console)).
     ![aem assets et adobe stock](/help/assets/assets/adobe-ims-technical-account-configuration.png)
1. Cliquez sur **[!UICONTROL Créer]**. La page **[!UICONTROL Configurations d’Adobe IMS]** s’ouvre et affiche l’intégration [!DNL Adobe Stock] que vous avez créée.

#### Ajouter la configuration cloud pour vous connecter à [!DNL Adobe Stock] {#add-cloud-configuration-to-connect-adobe-stock}

Exécutez les étapes suivantes pour ajouter la configuration cloud et vous connecter à [!DNL Adobe Stock] :

1. Accédez à votre instance [!DNL AEM author].
1. Cliquez sur ![aem assets et adobe stock](/help/assets/assets/Hammer.svg), sélectionnez **[!UICONTROL Cloud Services]**, recherchez et sélectionnez **[!UICONTROL Adobe Stock]**.
   ![utiliser adobe atock avec aem](/help/assets/assets/adding-cloud-config-to-adobe-stock.png)
1. Cliquez sur **[!UICONTROL Créer]** et la page **[!UICONTROL Configuration Adobe Stock]** affiche plusieurs champs. Suivez ces instructions pour spécifier les détails dans ces champs :
   * **[!UICONTROL Titre]** : accédez à la page **[!UICONTROL Configuration du compte technique Adobe IMS]** (voir [étape 3](#set-up-adobe-stock-ims-configuration-in-aem-author-instance)), copiez le titre et collez-le ici.
   * **[!UICONTROL Configuration Adobe IMS associée]** : sélectionnez l’intégration [!DNL Adobe Stock] que vous avez créée.
   * **[!UICONTROL Paramètres régionaux]** : sélectionnez **[!UICONTROL Anglais (États-Unis)]**.
1. Cliquez sur **[!UICONTROL Enregistrer et fermer]**.
   ![utiliser adobe atock avec aem](/help/assets/assets/adobe-stock-config-page.png)
<!-- old content
## Steps to integrate [!DNL Experience Manager] and [!DNL Adobe Stock] {#integration-steps}

To integrate [!DNL Experience Manager] and [!DNL Adobe Stock], perform the following steps in the listed sequence: 

1. [Obtain public certificate](#public-certificate)
   
   In [!DNL Experience Manager], create an IMS account and generate a public certificate (public key).

1. [Create service account (JWT) connection](#createnewintegration) 
   
   In [!DNL Adobe Developer Console], create a project for your [!DNL Adobe Stock] organization. Under the project, configure an API using the public key to create a service account (JWT) connection. Get the service account credentials and JWT payload information.

1. [Configure IMS account](#create-ims-account-configuration)

   In [!DNL Experience Manager], configure the IMS account using the service account credentials and JWT payload.

1. [Configure cloud service](#configure-the-cloud-service)

   In [!DNL Experience Manager], configure an [!DNL Adobe Stock] cloud service using the IMS account.


### Create an IMS configuration {#create-an-ims-configuration}

The IMS configuration authenticates your [!DNL Experience Manager Assets] author instance with the [!DNL Adobe Stock] entitlement. 

IMS configuration includes two steps:

* [Obtain public certificate](#public-certificate) 
* [Configure IMS account](#create-ims-account-configuration)

### Obtain public certificate {#public-certificate}

The public key (certificate) authenticates your product profile in Adobe Developer Console.

1. Log in to your [!DNL Experience Manager Assets] author instance. The default URL is `http://localhost:4502/aem/start.html`.

1. From the **[!UICONTROL Tools]** panel, navigate to **[!UICONTROL Security]** > **[!UICONTROL Adobe IMS Configurations]**.

1. In Adobe IMS Configurations page, click **[!UICONTROL Create]**. The **[!UICONTROL Adobe IMS Technical Account Configuration]** page opens. 

1. In the **[!UICONTROL Certificate]** tab, select **[!UICONTROL Adobe Stock]** from the **[!UICONTROL Cloud Solution]** dropdown list.  

1. You can create a certificate or reuse an existing certificate for the configuration. 

   To create a certificate, select the **[!UICONTROL Create new certificate]** check box and specify an **alias** for the public key. The alias serves as name of the public key. 

1. Click **[!UICONTROL Create certificate]**. Then, click **[!UICONTROL OK]** to generate the public key.

1. Click the **[!UICONTROL Download Public Key]** icon and save the public key (.crt) file on your machine. The public key is used later to configure API for your Brand Portal tenant and generate service account credentials in Adobe Developer Console.

   Click **[!UICONTROL Next]**.

   ![generate-certificate](assets/stock-integration-ims-account.png)

1. In the **Account** tab, Adobe IMS account is created which requires the service account credentials.

   Open a new tab and [create a service account (JWT) connection in Adobe Developer Console](#createnewintegration). 

### Create service account (JWT) connection {#createnewintegration}

In Adobe Developer Console, projects and APIs are configured at organization level. Configuring an API creates a service account (JWT) connection. There are two methods to configure API, by generating a key pair (private and public keys) or by uploading a public key. In this example, the service account credentials are generated by uploading the public key.

To generate the service account credentials and JWT payload:

1. Log in to Adobe Developer Console with system administrator privileges. The default URL is [https://www.adobe.com/go/devs_console_ui](https://www.adobe.com/go/devs_console_ui).


   Ensure that you have selected the correct IMS organization (Stock entitlement) from the dropdown (organization) list.

1. Click **[!UICONTROL Create new project]**. A blank project with a system-generated name is created for your organization. 

   Click **[!UICONTROL Edit project]**. Update the **[!UICONTROL Project Title]** and **[!UICONTROL Description]**, and then click **[!UICONTROL Save]**.
   
1. In the **[!UICONTROL Project overview]** tab, click **[!UICONTROL Add API]**.

1. In the **[!UICONTROL Add an API window]**, select **[!UICONTROL Adobe Stock]**. Click **[!UICONTROL Next]**. 

1. In the **[!UICONTROL Configure API]** window, select **[!UICONTROL Service Account (JWT)]** authentication. Click **[!UICONTROL Next]**.

   ![create-jwt-credentials](assets/aem-stock-jwt.png)

1. Click **[!UICONTROL Upload your public key]**. Click **[!UICONTROL Select a File]** and upload the public key (.crt file) that you have downloaded in the [obtain public certificate](#public-certificate) section. Click **[!UICONTROL Next]**.

1. Verify the public key and click **[!UICONTROL Next]**.

1. Select the default **[!UICONTROL Adobe Stock]** product profile and click **[!UICONTROL Save configured API]**. 

1. Once the API is configured, you are redirected to the API overview page. From the left navigation under **[!UICONTROL Credentials]**, click the **[!UICONTROL Service Account (JWT)]** option. Here, you can view the credentials and perform actions such as generate JWT tokens, copy credential details, and retrieve client secret.

1. From the **[!UICONTROL Client Credentials]** tab, copy the **[!UICONTROL client ID]**. 

   Click **[!UICONTROL Retrieve Client Secret]** and copy the **[!UICONTROL client secret]**.

   ![generate-jwt-credentials](assets/aem-stock-jwt-credential.png)

1. Navigate to the **[!UICONTROL Generate JWT]** tab and copy the **[!UICONTROL JWT Payload]** information. 

You can now use the client ID (API key), client secret, and JWT payload to [configure the IMS account](#create-ims-account-configuration) in [!DNL Experience Manager Assets].

### Configure IMS account {#create-ims-account-configuration}

You must have the [certificate](#public-certificate) and [service account (JWT) credentials](#createnewintegration) to configure the IMS account.

To configure the IMS account: 

1. Open the IMS Configuration and navigate to the **[!UICONTROL Account]** tab. You kept the page open while [obtaining the public certificate](#public-certificate).

1. Specify a **[!UICONTROL Title]** for the IMS account.

   In the **[!UICONTROL Authorization Server]** field, enter the URL: [https://ims-na1.adobelogin.com/](https://ims-na1.adobelogin.com/).  

   Enter the client ID in the **[!UICONTROL API key]** field, **[!UICONTROL Client Secret]**, and **[!UICONTROL Payload]** (JWT payload) that you have copied while [creating the service account (JWT) connection](#createnewintegration).

1. Click **[!UICONTROL Create]**. An IMS account configuration is created. 

   ![configure-ims-acount](assets/aem-stock-ims-config.png)
   
1. Select the IMS account configuration and click **[!UICONTROL Check Health]**.

   Click **[!UICONTROL Check]** in the dialog box. On successful configuration, a message appears that the *Token is retrieved successfully*.

   ![health-check](assets/aem-stock-healthcheck.png)


### Configure cloud service {#configure-the-cloud-service}

To configure the [!DNL Adobe Stock] cloud service:

1. In the [!DNL Experience Manager] user interface, navigate to **[!UICONTROL Tools]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL Adobe Stock]**.

1. In the [!DNL Adobe Stock Configurations] page, click **[!UICONTROL Create]**.

1. Specify a **[!UICONTROL Title]** for the cloud configuration. 

   Select the IMS configuration that you have created while [configuring the IMS account](#create-ims-account-configuration).

   Select your locale from the dropdown list.

   ![aem-stock-cloud-config](assets/aem-stock-cloud-config.png)

1. Click **[!UICONTROL Save & Close]**. 
 -->
Votre instance de création [!DNL Experience Manager Assets] est désormais intégrée à [!DNL Adobe Stock]. Vous pouvez créer plusieurs configurations [!DNL Adobe Stock] (par exemple, des configurations basées sur des paramètres régionaux). Vous pouvez désormais accéder aux ressources [!DNL Adobe Stock], en rechercher et en obtenir la licence dans l’interface utilisateur d’[!DNL Experience Manager].

![rechercher-des-ressources-stock](assets/aem-stock-searchstocks.png)

>[!NOTE]
>
>À cette étape de l’intégration, seuls les administrateurs peuvent accéder aux ressources [!DNL Adobe Stock], rechercher des ressources Stock (à l’aide de l’omni-recherche) et obtenir la licence des ressources [!DNL Adobe Stock].
>
>Les administrateurs peuvent ajouter des utilisateurs ou des groupes au service cloud d’[!DNL Adobe Stock] et attribuer des autorisations à ces utilisateurs non administrateurs dans [!DNL Experience Manager] pour accéder à la configuration de Stock.

1. Pour ajouter des utilisateurs ou des groupes, sélectionnez la configuration cloud d’[!DNL Adobe Stock] et cliquez sur **[!UICONTROL Propriétés]**.

1. Effectuez une recherche pour ajouter les utilisateurs ou les groupes auxquels vous avez autorisé l’accès à la configuration d’Adobe Stock. Consultez la section [Attribuer des autorisations à un groupe d’utilisateurs](#assign-permissions-to-group).


## Attribution d’autorisations à un groupe d’utilisateurs {#assign-permissions-to-group}

Les administrateurs peuvent créer des groupes d’utilisateurs et autoriser certains utilisateurs ou groupes à accéder au service cloud d’[!DNL Adobe Stock].

Voici les autorisations requises pour qu’un utilisateur puisse rechercher et obtenir la licence des ressources Adobe Stock :

* Configurez le chemin d’accès : `/conf/global/settings/stock`
* Droits : `jcr:read`
* Type d’autorisation : `Allow`

Vous pouvez créer un groupe d’utilisateurs ou attribuer des autorisations à un groupe d’utilisateurs existant. Les autorisations peuvent être attribuées à partir de l’interface d’[!DNL Experience Manager Assets] ou à partir de la console d’[!DNL User Admin].

**Pour accorder l’accès à un groupe d’utilisateurs à partir d’[!DNL Experience Manager] :**

1. Dans l’interface utilisateur d’[!DNL Experience Manager], accédez à **[!UICONTROL Outils]** > **[!UICONTROL Sécurité]** > **[!UICONTROL Groupes]**. Créez un groupe d’utilisateurs pour [!DNL Adobe Stock].

1. Accédez à **[!UICONTROL Outils]** > **[!UICONTROL Sécurité]** > **[!UICONTROL Autorisations]**.

1. Recherchez le groupe d’utilisateurs dans le panneau de gauche et ajoutez une nouvelle **[!UICONTROL Entrée de contrôle d’accès (ACE)]** pour Adobe Stock.

   * Configurez le chemin d’accès : `/conf/global/settings/stock`
   * Droits : `jcr:read`
   * Type d’autorisation : `Allow`

   Cliquez sur **[!UICONTROL Ajouter]**.

   ![autorisations-utilisateur](assets/aem-stock-user-permissions.png)

1. Accédez à **[!UICONTROL Outils]** > **[!UICONTROL Services cloud]** > **[!UICONTROL Adobe Stock]**. Sélectionnez la configuration du cloud d’[!DNL Adobe Stock] et cliquez sur **[!UICONTROL Propriétés]**.

1. Ajoutez le groupe d’utilisateurs nouvellement créé à la configuration d’[!DNL Adobe Stock]. Cliquez sur **[!UICONTROL Enregistrer et fermer]**.

   ![affecter-utilisateur](assets/aem-stock-adduser.png)

**Pour fournir l’accès à un utilisateur à partir de la [!DNL User Admin Console] :**

1. Ouvrez l’Admin Console des utilisateurs d’[!DNL Experience Manager]. L’URL par défaut est `http://localhost:4502/userdamin`.

1. Dans le volet de gauche, recherchez l’utilisateur en saisissant le `user_id` ou le `name`. Double-cliquez pour ouvrir les propriétés de l’utilisateur.

1. Accédez à l’onglet **[!UICONTROL Autorisations]** et activez l’autorisation de `read` pour la configuration cloud d’[!DNL Adobe Stock] : `/conf/global/settings/stock`.

   >[!CAUTION]
   >
   >Si la configuration cloud n’est pas autorisée, l’utilisateur peut uniquement accéder aux **[!UICONTROL Ressources]** dans l’interface d’[!DNL Experience Manager].
   >
   >Pour autoriser l’accès aux [!UICONTROL Ressources] et aux ressources d’[!DNL Adobe Stock], assurez-vous que la configuration cloud est autorisée pour l’utilisateur.

1. Cliquez sur **[!UICONTROL Enregistrer]** pour mettre à jour les autorisations.

   ![affecter-utilisateur-dans-administration-utilisateur](assets/aem-stock-user-admin-console.png)

1. Ajoutez l’utilisateur ou le groupe à la configuration du cloud d’[!DNL Adobe Stock].

## Accès aux ressources d’Adobe Stock {#access-stock-assets}

Un utilisateur non administrateur disposant d’autorisations pour la configuration cloud d’[!DNL Adobe Stock] peut rechercher et obtenir une licence pour les ressources d’[!DNL Adobe Stock] à partir de l’interface d’[!DNL Experience Manager].

L’utilisateur doit effectuer une étape supplémentaire pour activer la configuration cloud d’[!DNL Adobe Stock] avant d’accéder aux ressources [!DNL Adobe Stock]. Cette opération n’est à effectuer qu’une fois. Si des autorisations sont attribuées à l’utilisateur pour plusieurs configurations cloud d’[!DNL Adobe Stock], celui-ci peut sélectionner la configuration souhaitée dans les **[!UICONTROL Préférences utilisateur]**.

Pour activer la configuration cloud d’[!DNL Adobe Stock] :

1. Connectez-vous à [!DNL Experience Manager].

1. Cliquez sur l’icône de l’utilisateur dans le coin supérieur droit, puis cliquez sur **[!UICONTROL Mes préférences]**. La fenêtre des **[!UICONTROL Préférences utilisateur]** s’ouvre.

1. Sélectionnez la **[!UICONTROL Configuration Stock]** souhaitée dans la liste déroulante, puis cliquez sur **[!UICONTROL Accepter]** pour activer la configuration.

   ![préférences-utilisateur](assets/aem-stock-preferences.png)

1. Accédez à **[!UICONTROL Ressources]** > **[!UICONTROL Adobe Stock]**. Vous pouvez désormais afficher, rechercher et obtenir une licence pour les ressources d’[!DNL Adobe Stock].

Le tableau suivant explique le fonctionnement des autorisations utilisateur lors de l’accès aux ressources d’[!DNL Adobe Stock] :

| Utilisateur | Groupe | Autorisations | Accepter la configuration Stock dans les Préférences utilisateur | Accéder aux ressources | Accéder à Adobe Stock |
| --- | --- | --- | --- | --- | --- |
| administrateur | S/O | Tous | S/O | Oui | Oui |
| test-doc1 | Utilisateur DAM | /conf/global/settings/stock/cloud-config | Oui | Oui | Oui |
| test-doc1 | Utilisateur DAM | /conf/global/settings/stock/cloud-config | Non | Erreur : Échec du chargement des données | Non |
| test-doc1 | Utilisateur DAM | **autoriser** : /conf/global/settings/stock **interdire** : /cloud-config | La configuration de Stock n’est pas visible | Oui | Non |


## Utilisation et gestion de ressources [!DNL Adobe Stock] dans [!DNL Experience Manager] {#usemanage}

Grâce à cette fonctionnalité, les entreprises peuvent permettre à leurs utilisateurs de travailler avec des ressources [!DNL Adobe Stock] dans [!DNL Experience Manager Assets]. Dans l’interface utilisateur [!DNL Experience Manager], les utilisateurs peuvent rechercher des ressources [!DNL Adobe Stock] et obtenir des licences pour les ressources requises.

Une fois qu’une ressource [!DNL Adobe Stock] est sous licence dans [!DNL Experience Manager], elle peut être utilisée et gérée comme une ressource standard. Dans [!DNL Experience Manager], les utilisateurs et les utilisatrices peuvent rechercher des ressources, les prévisualiser, les copier, les publier, les partager sur [!DNL Brand Portal] et les utiliser via l’application de bureau [!DNL Experience Manager], etc.

![Rechercher des ressources [!DNL Adobe Stock] et filtrer les résultats à partir de l’espace de travail d’[!DNL Adobe Experience Manager]](assets/adobe-stock-search-results-workspace.png)

**A.** Rechercher des ressources semblables à celles dont l’ID d’[!DNL Adobe Stock] est fourni. **B.** Rechercher des ressources correspondant à la forme ou à l’orientation que vous avez sélectionnée. **C.** Rechercher un ou plusieurs types de ressource pris en charge. **D.** Ouvrir ou réduire le volet Filtres. **E.** Obtenir la licence et enregistrer la ressource sélectionnée dans [!DNL Experience Manager]. **F.** Enregistrer la ressource dans [!DNL Experience Manager] avec filigrane. **G.** Explorer des ressources semblables à la ressource sélectionnée sur le site web d’[!DNL Adobe Stock]. **H.** Afficher des ressources sélectionnées sur le site web d’[!DNL Adobe Stock]. **I.** Nombre de ressources sélectionnées à partir des résultats de la recherche. **J.** Basculer entre les affichages Carte et Liste.

### Recherche de ressources {#find-assets}

Vos utilisateurs [!DNL Experience Manager] peuvent rechercher des ressources dans [!DNL Experience Manager] et dans [!DNL Adobe Stock]. Lorsque l’emplacement de recherche n’est pas limité à [!DNL Adobe Stock], les résultats de recherche en provenance d’[!DNL Experience Manager] et d’[!DNL Adobe Stock] sont affichés.

* Pour rechercher des ressources [!DNL Adobe Stock], cliquez sur **[!UICONTROL Navigation]** > **[!UICONTROL Ressources]** > **[!UICONTROL Rechercher sur Adobe Stock]**.

* Pour rechercher des ressources dans [!DNL Adobe Stock] et [!DNL Experience Manager Assets], cliquez sur ![Rechercher](assets/do-not-localize/search_icon.png).

Vous pouvez également commencer à saisir `Location: Adobe Stock` dans la barre de recherche pour sélectionner des ressources [!DNL Adobe Stock] [!DNL Experience Manager] propose des fonctionnalités de filtrage avancé sur les ressources recherchées, ce qui permet aux utilisateurs de cibler rapidement les ressources requises à l’aide de filtres tels que les types de ressources pris en charge, l’orientation d’image et l’état de licence.

>[!NOTE]
>
>Les ressources recherchées dans [!DNL Adobe Stock] s’affichent dans [!DNL Experience Manager]. Les ressources [!DNL Adobe Stock] ne sont pas récupérées ni stockées dans le référentiel [!DNL Experience Manager] tant qu’un utilisateur n’a pas [enregistré une ressource](/help/assets/aem-assets-adobe-stock.md#saveassets) ou [acquis sous licence et enregistré une ressource ](/help/assets/aem-assets-adobe-stock.md#licenseassets). Les ressources déjà stockées dans [!DNL Experience Manager] sont affichées et mises en surbrillance pour simplifier leur référencement et leur accès. En outre, les ressources [!DNL Stock] sont enregistrées avec quelques métadonnées supplémentaires pour indiquer la source comme étant [!DNL Stock].

![Rechercher des filtres dans [!DNL Experience Manager] et ressources [!DNL Adobe Stock] mises en évidence dans les résultats de recherche](assets/aem-search-filters2.jpg)

### Enregistrement et affichage des ressources requises {#saveassets}

Sélectionnez une ressource que vous souhaitez enregistrer dans [!DNL Experience Manager]. Cliquez sur [!UICONTROL Enregistrer] dans la barre d’outils supérieure, et indiquez le nom et l’emplacement de la ressource. Les ressources sans licence sont enregistrées en local avec un filigrane.

La prochaine fois que vous rechercherez des ressources, les ressources enregistrées seront mises en évidence avec un badge pour indiquer qu’elles sont disponibles dans [!DNL Experience Manager Assets].

>[!NOTE]
>
>Les ressources ajoutées récemment sont assorties d’un badge Nouvelle au lieu du badge Sous licence.

### Acquisition de ressources sous licence {#licenseassets}

Les utilisateurs peuvent acquérir des ressources [!DNL Adobe Stock] sous licence en utilisant le quota de leur abonnement pour entreprise [!DNL Adobe Stock]. Lorsque vous acquérez une ressource sous licence, elle est enregistrée sans filigrane, et elle peut être recherchée et utilisée dans [!DNL Experience Manager Assets].

![Boîte de dialogue permettant d’obtenir la licence et d’enregistrer des ressources [!DNL Adobe Stock] dans [!DNL Experience Manager Assets]](assets/aem-stock_licenseandsave.jpg)


### Accès aux propriétés de ressources et de métadonnées {#access-metadata-and-asset-properties}

Les utilisateurs peuvent accéder aux métadonnées et les prévisualiser, ce qui inclut les propriétés de métadonnées [!DNL Adobe Stock] des ressources enregistrées dans [!DNL Experience Manager], et ajouter des **[!UICONTROL Références de licence]** pour une ressource. Cependant, les mises à jour apportées à une référence de licence ne sont pas synchronisées entre [!DNL Experience Manager] et le site web d’[!DNL Adobe Stock].

Les utilisateurs peuvent afficher les propriétés de toutes les ressources, avec et sans licence.

![Affichage des métadonnées et des références de licence des ressources enregistrées, et accès à ces éléments](assets/metadata_properties.jpg)


## Limites connues {#known-limitations}

* **Problèmes d’intégration avec le pack de services [!DNL Experience Manager] 6.5.7.0 et versions ultérieures** : un problème inattendu est identifié lors de l’intégration à [!DNL Experience Manager] 6.5.7.0 et versions ultérieures. Le problème est en cours de test et devrait être disponible dans [!DNL Experience Manager] 6.5.11.0. Contactez le [!DNL Customer Support] pour obtenir un correctif immédiat.

* **La fonctionnalité de restriction des utilisateurs pour l’obtention de la licence ne fonctionne pas correctement** : tous les utilisateurs qui disposent des autorisations `read` pour la configuration de Stock sont autorisés à rechercher les ressources d’[!DNL Adobe Stock] et à obtenir une licence.

* **Les utilisateurs non administrateurs doivent activer manuellement la configuration cloud d’[!DNL Adobe Stock]** : dans la fenêtre des **[!UICONTROL Préférences utilisateur]**, la **[!UICONTROL Configuration de Stock]** affiche la configuration cloud d’[!DNL Adobe Stock] comme étant activée, mais elle ne fonctionne pas pour un utilisateur non administrateur. L’utilisateur ou l’utilisatrice doit cliquer sur le bouton **[!UICONTROL Accepter]** pour activer la configuration de Stock. En l’absence de cette étape, le système affiche un message d’erreur lors de l’accès aux **[!UICONTROL Ressources]**.

* **L’avertissement d’image éditoriale n’est pas affiché** : lors de l’octroi d’une licence pour une image, les utilisateurs ne peuvent pas vérifier si une image est destinée à une utilisation éditoriale uniquement. Pour lutter contre une éventuelle utilisation abusive, les administrateurs peuvent désactiver l’accès aux ressources éditoriales à partir d’Admin Console.

* **Type de licence affiché incorrect** : il est possible qu’un type de licence incorrect apparaisse dans [!DNL Experience Manager] pour une ressource. Les utilisateurs peuvent se connecter au site web d’[!DNL Adobe Stock] pour afficher le type de licence.

* **Les champs de référence et les métadonnées ne sont pas synchronisés** : lorsqu’un utilisateur met à jour un champ de référence de licence, les informations de référence de licence sont mises à jour dans [!DNL Experience Manager], mais pas sur le site web d’[!DNL Adobe Stock]. De même, si l’utilisateur met à jour les champs de référence sur le site web d’[!DNL Adobe Stock], les mises à jour ne sont pas synchronisées dans [!DNL Experience Manager].

>[!MORELIKETHIS]
>
>* [Tutoriel vidéo sur l’utilisation de ressources  [!DNL Adobe Stock]  avec  [!DNL Experience Manager Assets]](https://experienceleague.adobe.com/docs/experience-manager-learn/assets/creative-workflows/adobe-stock.html?lang=fr)
>* Aide sur la formule Entreprise d’[[!DNL Adobe Stock] ](https://helpx.adobe.com/fr/enterprise/using/adobe-stock-enterprise.html)
>* [[!DNL Adobe Stock] FAQ](https://helpx.adobe.com/fr/stock/faq.html)


<!--old content

### Create an IMS configuration {#create-an-ims-configuration}

1. In the [!DNL Experience Manager] user interface, navigate to **[!UICONTROL Tools]** > **[!UICONTROL Security]** > **[!UICONTROL Adobe IMS Configurations]**. Click **[!UICONTROL Create]** and select **[!UICONTROL Cloud Solution]** > **[!UICONTROL Adobe Stock]**.
1. Either reuse an existing certificate or select **[!UICONTROL Create new certificate]**.
1. Click **[!UICONTROL Create certificate]**. Once created, download the public key. Click **[!UICONTROL Next]**. Leave the [!UICONTROL Adobe IMS Technical Account Configuration] screen open to provide the required values shortly.
1. Access [Adobe Developer Console](https://console.adobe.io). Ensure that your account has administrator permissions for the organization for which the integration is required.
1. Click **[!UICONTROL Create new project]** and click **[!UICONTROL Add API]**. Select **[!UICONTROL Adobe Stock]** from the list of APIs that are available to you. Select [!UICONTROL OAUTH 2.0 Web].
1. Provide **[!UICONTROL Default redirect URI]** and **[!UICONTROL Redirect URI pattern]** values. Click **[!UICONTROL Save configured API]**. Copy the generated ID and secret.
1. In [!UICONTROL Adobe IMS Technical Account Configuration] screen, provide the values in the boxes titled **[!UICONTROL Title]**, **[!UICONTROL Authorization Server]**, **[!UICONTROL API Key]**, **[!UICONTROL Client Secret]**, and **[!UICONTROL Payload]**. For detailed information about these values, see [JWT authentication quick start](https://www.adobe.io/authentication/auth-methods.html#!AdobeDocs/adobeio-auth/master/JWT/JWT.md).

-->

<!-- TBD: Update the URL to update the terminology when AIO team updates their documentation URL. Logged issue github.com/AdobeDocs/adobeio-auth/issues/63.
-->

<!--
### Create [!DNL Adobe Stock] configuration in [!DNL Experience Manager] {#create-adobe-stock-configuration-in-aem}

1. In the [!DNL Experience Manager], navigate to **[!UICONTROL Tools]** > **[!UICONTROL Cloud Services]** > **[!UICONTROL Adobe Stock]**.
1. Click **[!UICONTROL Create]** to create a configuration and associate it with your existing IMS Configuration. Select `PROD` as the environment parameter.
1. In **[!UICONTROL Licensed Assets Path]** field, leave a location as is. Do not change the location where you want to store the [!DNL Adobe Stock] assets.
1. Complete creation by adding all the required properties. Click **[!UICONTROL Save & Close]**.
1. Add [!DNL Experience Manager] users or groups, who can license the assets.

>[!NOTE]
>
>If there are multiple [!DNL Adobe Stock] configurations, select the desired configuration in [!UICONTROL User Preferences] panel. To access the panel from [!DNL Experience Manager] home page, click the user icon and then click **[!UICONTROL User Preferences]** > **[!UICONTROL Stock Configuration]**.
-->

