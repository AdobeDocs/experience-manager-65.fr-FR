---
title: Configuration du service OData de Microsoft Dynamics
seo-title: Microsoft Dynamics ODtata configuration
description: Tirez parti de l’intégration et de l’utilisation des services Microsoft Dynamics en ligne et sur site grâce à un modèle de données de formulaire.
seo-description: Learn how to leverage integrate and work with online and on-premises Microsoft Dynamics services through form data model.
uuid: 37e59633-484b-4a20-808d-2a0bc0d336cc
topic-tags: integration
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 627507f5-1ffc-48f8-8cc9-5dbc5e409ae3
docset: aem65
feature: Form Data Model
exl-id: 90cc9452-e107-4e57-80a3-f44f0bde132e
source-git-commit: 9d142ce9e25e048512440310beb05d762468f6a2
workflow-type: ht
source-wordcount: '1206'
ht-degree: 100%

---

# Configuration du service OData de Microsoft Dynamics{#microsoft-dynamics-odata-configuration}

![data-integeration](assets/data-integeration.png)

Microsoft Dynamics est un logiciel de gestion de la relation client (CRM, Customer Relationship Management) et de planification des ressources de l’entreprise (ERP, Enterprise Resource Planning) qui fournit des solutions d’entreprise pour la création et la gestion de comptes clients, de contacts, de prospects, d’opportunités et de dossiers. [L’intégration de données d’AEM Forms](../../forms/using/data-integration.md) fournit une configuration de service cloud OData pour intégrer Forms aux serveurs Microsoft Dynamics en ligne et sur site. Elle vous permet de créer un modèle de données de formulaire basé sur des entités, des attributs et des services définis dans le service Microsoft Dynamics. Le modèle de données de formulaire peut être utilisé pour créer des formulaires adaptatifs qui interagissent avec le serveur Microsoft Dynamics pour activer les workflows opérationnels. Par exemple :

* Demandez des données au serveur Microsoft Dynamics et préremplissez des formulaires adaptatifs
* Écrire des données sur Microsoft Dynamics pour des envois de formulaires adaptatifs
* Écrivez des données dans Microsoft Dynamics via des entités personnalisées définies dans le modèle de données de formulaire et vice versa

Le module complémentaire AEM Forms inclut également une configuration OData de référence que vous pouvez exploiter pour intégrer rapidement Microsoft Dynamics à AEM Forms.

Lorsque le package est installé, les entités et services suivants sont déployés sur votre instance AEM Forms :

* Service cloud OData MS Dynamics (service OData)
* Modèle de données de formulaire avec entités et services Microsoft Dynamics préconfigurés.

Les entités et services Microsoft Dynamics préconfigurés dans un modèle de données de formulaire ne sont disponibles sur votre instance AEM Forms que si le mode d’exécution de l’instance AEM est défini comme `samplecontent` (par défaut). Le service Cloud OData MS Dynamics (service OData) est également disponible avec d’autres modes d’exécution. Pour plus d’informations sur la configuration des modes d’exécution pour une instance AEM, voir [Modes d’exécution](/help/sites-deploying/configure-runmodes.md).

## Prérequis {#prerequisites}

Avant de commencer à installer et configurer Microsoft Dynamics, vérifiez que vous avez :

* Le [package du module complémentaire AEM Forms](../../forms/using/installing-configuring-aem-forms-osgi.md) a été installé
* Configuré Microsoft Dynamics 365 en ligne ou installé une instance de l’une des versions de Microsoft Dynamics suivantes :

   * Microsoft Dynamics 365 sur site
   * Microsoft Dynamics 2016 sur site

* [L’application pour le service en ligne Microsoft Dynamics a été enregistrée auprès de Microsoft Azure Active Directory](https://docs.microsoft.com/fr-fr/dynamics365/customer-engagement/developer/walkthrough-register-dynamics-365-app-azure-active-directory). Notez les valeurs de l’ID client (également appelé « ID d’application ») et du secret du client pour le service enregistré. Ces valeurs sont utilisées lors de l’utilisation de la [configuration du service cloud pour votre service Microsoft Dynamics](../../forms/using/ms-dynamics-odata-configuration.md#configure-cloud-service-for-your-microsoft-dynamics-service).

## Définition de l’URL de réponse pour l’application Microsoft Dynamics enregistrée {#set-reply-url-for-registered-microsoft-dynamics-application}

Procédez comme suit pour définir l’URL de réponse de l’application Microsoft Dynamics enregistrée :

>[!NOTE]
>
>Utilisez cette procédure uniquement lors de l’intégration d’AEM Forms au serveur Microsoft Dynamics en ligne.

1. Accédez au compte Microsoft Azure Active Directory et ajoutez l’URL de configuration du service cloud suivante dans les paramètres des **URL de réponse** pour votre application enregistrée :

   `https://'[server]:[port]'/libs/fd/fdm/gui/components/admin/fdmcloudservice/createcloudconfigwizard/cloudservices.html`

   ![Azure Directory](assets/azure_directory_new.png)

1. Enregistrez la configuration.

## Configuration de Microsoft Dynamics pour IFD {#configure-microsoft-dynamics-for-ifd}

Microsoft Dynamics utilise l’authentification basée sur les réclamations pour fournir l’accès aux données sur le serveur Microsoft Dynamics CRM aux utilisateurs externes. Pour ce faire, procédez comme suit pour configurer Microsoft Dynamics pour le déploiement par Internet (IFD) et configurer les paramètres de réclamation.

>[!NOTE]
>
>Utilisez cette procédure uniquement lors de l’intégration d’AEM Forms au serveur Microsoft Dynamics sur site.

1. Configurez l’instance Microsoft Dynamics sur site pour IFD, comme décrit dans [Configurer IFD pour Microsoft Dynamics](https://technet.microsoft.com/fr-fr/library/dn609803.aspx).
1. Exécutez les commandes suivantes à l’aide de Windows PowerShell pour configurer les paramètres de réclamation sur Microsoft Dynamics compatible avec IFD :

   ```shell
   Add-PSSnapin Microsoft.Crm.PowerShell
    $ClaimsSettings = Get-CrmSetting -SettingType OAuthClaimsSettings
    $ClaimsSettings.Enabled = $true
    Set-CrmSetting -Setting $ClaimsSettings
   ```

   Pour plus d’informations, voir [Enregistrement de l’application pour CRM local (IFD)](https://msdn.microsoft.com/sl-si/library/dn531010(v=crm.7).aspx#bkmk_ifd).

## Configuration du client OAuth sur une machine AD FS {#configure-oauth-client-on-ad-fs-machine}

Pour enregistrer un client OAuth sur l’ordinateur Active Directory Federation Services (AD FS) et octroyer l’accès sur l’ordinateur AD FS :

>[!NOTE]
>
>Utilisez cette procédure uniquement lors de l’intégration d’AEM Forms au serveur Microsoft Dynamics sur site.

1. Exécutez la commande suivante :

   `Add-AdfsClient -ClientId "<Client-ID>" -Name "<name>" -RedirectUri "<redirect-uri>" -GenerateClientSecret`

   Où :

   * `Client-ID` est un ID client que vous pouvez générer à l’aide d’un générateur de GUID.
   * `redirect-uri` est l’URL du service cloud OData de Microsoft Dynamics dans AEM Forms. Le service cloud par défaut installé avec le package AEM Forms est déployé à l’adresse URL suivante :
      `https://'[server]:[port]'/libs/fd/fdm/gui/components/admin/fdmcloudservice/createcloudconfigwizard/cloudservices.html`

1. Exécutez la commande ci-dessous pour octroyer l’accès sur l’ordinateur AD FS :

   `Grant-AdfsApplicationPermission -ClientRoleIdentifier "<Client-ID>" -ServerRoleIdentifier <resource> -ScopeNames openid`

   Où :

   * `resource` est l’URL d’organisation de Microsoft Dynamics.

1. Microsoft Dynamics utilise le protocole HTTPS. Pour appeler les points de fin AD FS depuis le serveur Forms, installez le certificat de site Microsoft Dynamics dans le fichier de stockage des certificats Java à l’aide de la commande `keytool` sur l’ordinateur exécutant AEM Forms.

## Configurer le service cloud pour votre service Microsoft Dynamics {#configure-cloud-service-for-your-microsoft-dynamics-service}

La configuration du **service cloud OData de MS Dynamics (service OData)** est fournie avec la configuration OData par défaut. Pour le configurer afin qu’il se connecte à votre service Microsoft Dynamics, procédez comme suit.

1. Accédez à **[!UICONTROL Outils > Services cloud > Sources de données]** et appuyez sur le dossier de configuration `global`.
1. Sélectionnez la configuration du **service cloud OData MS Dynamics (service OData)** et appuyez sur **[!UICONTROL Propriétés]**. La boîte de dialogue Propriété de configuration du service cloud s’affiche.

   Dans l’onglet **Paramètres d’authentification** :

   1. Saisissez la valeur pour le champ **Racine du service**. Accédez à l’instance Dynamics et à **Ressources de développement** pour afficher la valeur du champ Racine du service. Par exemple, https://&lt;nom-client>/api/data/v9.1/

   1. Remplacez les valeurs par défaut dans les champs **ID client** (également appelé **ID d’application**), **Secret client**, **URL OAuth**, **URL du jeton d’actualisation**, **URL du jeton d’accès** et **Ressource** avec les valeurs de votre configuration de service Microsoft Dynamics. Il est obligatoire de spécifier l’URL de l’instance dynamique dans le champ **Ressource** afin de configurer Microsoft Dynamics avec un modèle de données de formulaire. Utilisez l’URL racine du service pour dériver l’URL de l’instance dynamique. For example, [https://org.crm.dynamics.com](https://org.crm.dynamics.com/).

   1. Spécifiez **openid** dans le champ **Portée de l’autorisation** pour le processus d’autorisation sur Microsoft Dynamics.

   ![Paramètres d’authentification](assets/dynamics_authentication_settings_new.png)

1. Cliquez sur **[!UICONTROL Connexion à OAuth]**. Vous êtes redirigé vers la page de connexion de Microsoft Dynamics.
1. Connectez-vous avec vos informations d’identification Microsoft Dynamics et autorisez la connexion de la configuration du service cloud au service Microsoft Dynamics. C’est une tâche ponctuelle qui permet d’établir une connexion entre le service cloud et le service.

   Vous êtes ensuite redirigé vers la page de configuration du service cloud, qui affiche un message indiquant que la configuration OData a été enregistrée avec succès.

Le service cloud MS Dynamics OData Cloud Service (Service OData) est configuré et connecté à votre service Dynamics.

## Création d’un modèle de données de formulaire {#create-form-data-model}

Lorsque vous installez le package AEM Forms, un modèle de données de formulaire **Microsoft Dynamics FDM** est déployé sur votre instance AEM. Par défaut, le modèle de données de formulaire utilise le service Microsoft Dynamics configuré dans le service cloud OData MS Dynamics (Service OData) comme source de données.

Lorsque vous ouvrez le modèle de données de formulaire pour la première fois, il se connecte au service Microsoft Dynamics configuré et récupère les entités de votre instance Microsoft Dynamics. Les entités « Contact » et « Prospect » de Microsoft Dynamics sont déjà ajoutées au modèle de données de formulaire.

Pour vérifier le modèle de données de formulaire, accédez à **[!UICONTROL Formulaires > Intégrations de données]**. Sélectionnez **Microsoft Dynamics FDM** et cliquez sur **Modifier** pour ouvrir le modèle de données de formulaire en mode édition. Vous pouvez également ouvrir le modèle de données de formulaire directement à partir de l’URL suivante : 

`https://'[server]:[port]'/aem/fdm/editor.html/content/dam/formsanddocuments-fdm/ms-dynamics-fdm`

![default-fdm-1](assets/default-fdm-1.png)

Ensuite, vous pouvez créer un formulaire adaptatif basé sur le modèle de données de formulaire et l’utiliser dans divers cas de formulaires adaptatifs, tels que :

* Remplir le formulaire adaptatif en obtenant des informations des entités et services Microsoft Dynamics
* Appeler des opérations du serveur Microsoft Dynamics définies dans un modèle de données de formulaire à l’aide de règles de formulaires adaptatifs
* Écrire les données de formulaire envoyées dans les entités Microsoft Dynamics

Il est recommandé de créer une copie du modèle de données de formulaire fourni avec le package AEM Forms et de configurer les modèles de données et les services en fonction de vos besoins. Ainsi, les futures mises à jour du package de ne remplaceront pas votre modèle de données de formulaire.

Pour plus d’informations sur la création et l’utilisation de modèles de données de formulaire dans les processus métier, voir [Intégration de données](../../forms/using/data-integration.md).
