---
title: Configuration du service OData de Microsoft Dynamics
description: Découvrez comment utiliser, intégrer et utiliser les services Microsoft Dynamics en ligne et sur site à l’aide d’un modèle de données de formulaire.
topic-tags: integration
products: SG_EXPERIENCEMANAGER/6.5/FORMS
docset: aem65
feature: Form Data Model
exl-id: 90cc9452-e107-4e57-80a3-f44f0bde132e
solution: Experience Manager, Experience Manager Forms
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '1207'
ht-degree: 56%

---

# Configuration du service OData de Microsoft Dynamics{#microsoft-dynamics-odata-configuration}

| Version | Lien de l’article |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Cliquez ici](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/integrate/use-form-data-model/ms-dynamics-odata-configuration.html) |
| AEM 6.5 | Cet article |

![data-integeration](assets/data-integeration.png)

Microsoft Dynamics est un logiciel de gestion de la relation client et de planification des ressources de l’entreprise (ERP) qui fournit des solutions d’entreprise pour la création et la gestion de comptes clients, de contacts, de prospects, d’opportunités et de dossiers. [Intégration de données AEM Forms](../../forms/using/data-integration.md) fournit une configuration de service cloud OData pour intégrer Forms au serveur Microsoft Dynamics en ligne et sur site. Il vous permet de créer un modèle de données de formulaire basé sur les entités, les attributs et les services définis dans le service Microsoft Dynamics. Le modèle de données de formulaire peut être utilisé pour créer des formulaires adaptatifs qui interagissent avec le serveur Microsoft Dynamics pour activer les workflows opérationnels. Par exemple :

* Demandez des données au serveur Microsoft Dynamics et préremplissez des formulaires adaptatifs
* Écrire des données sur Microsoft Dynamics pour des envois de formulaires adaptatifs
* Écrire des données dans Microsoft Dynamics par le biais d’entités personnalisées définies dans le modèle de données de formulaire et inversement

Le module complémentaire AEM Forms comprend également une configuration OData de référence que vous pouvez utiliser pour intégrer rapidement Microsoft Dynamics à AEM Forms.

Lorsque le package est installé, les entités et services suivants sont disponibles sur votre instance AEM Forms :

* CLOUD SERVICE OData MS Dynamics (service OData)
* Modèle de données de formulaire avec entités et services Microsoft Dynamics préconfigurés.

Les entités et services Microsoft Dynamics préconfigurés dans un modèle de données de formulaire ne sont disponibles sur votre instance AEM Forms que si le mode d’exécution de l’instance AEM est défini comme `samplecontent` (par défaut). Le service Cloud OData MS Dynamics (service OData) est également disponible avec d’autres modes d’exécution. Pour plus d’informations sur la configuration des modes d’exécution pour une instance AEM, voir [Modes d’exécution](/help/sites-deploying/configure-runmodes.md).

## Prérequis {#prerequisites}

Avant de commencer à configurer Microsoft Dynamics, vérifiez que vous disposez des éléments suivants :

* Le [package du module complémentaire AEM Forms](../../forms/using/installing-configuring-aem-forms-osgi.md) a été installé
* Configuration de Microsoft Dynamics 365 en ligne ou installation d’une instance de l’une des versions de Microsoft Dynamics suivantes :

   * Microsoft Dynamics 365 sur site
   * Microsoft Dynamics 2016 sur site

* [L’application pour le service en ligne Microsoft Dynamics a été enregistrée auprès de Microsoft Azure Active Directory](https://docs.microsoft.com/fr-fr/dynamics365/customer-engagement/developer/walkthrough-register-dynamics-365-app-azure-active-directory). Notez les valeurs de l’ID client (également appelé « ID d’application ») et du secret du client pour le service enregistré. Ces valeurs sont utilisées lors de la [configuration du service cloud pour votre service Microsoft Dynamics](../../forms/using/ms-dynamics-odata-configuration.md#configure-cloud-service-for-your-microsoft-dynamics-service).

## Définition de l’URL de réponse pour l’application Microsoft Dynamics enregistrée {#set-reply-url-for-registered-microsoft-dynamics-application}

Procédez comme suit pour définir l’URL de réponse pour l’application Microsoft Dynamics enregistrée :

>[!NOTE]
>
>Utilisez cette procédure uniquement lors de l’intégration d’AEM Forms au serveur Microsoft Dynamics en ligne.

1. Accédez au compte Microsoft Azure Active Directory et ajoutez l’URL de configuration du service cloud suivante dans les paramètres des **URL de réponse** pour votre application enregistrée :

   `https://'[server]:[port]'/libs/fd/fdm/gui/components/admin/fdmcloudservice/createcloudconfigwizard/cloudservices.html`

   ![Azure Directory](assets/azure_directory_new.png)

1. Enregistrez la configuration.

## Configuration de Microsoft Dynamics pour IFD {#configure-microsoft-dynamics-for-ifd}

Microsoft Dynamics utilise l’authentification basée sur les revendications pour fournir l’accès aux données sur le serveur Microsoft Dynamics CRM aux utilisateurs externes. Pour activer cette fonction, procédez comme suit pour configurer Microsoft Dynamics pour le déploiement Internet (IFD) et configurer les paramètres de demande.

>[!NOTE]
>
>Utilisez cette procédure uniquement lors de l’intégration d’AEM Forms au serveur Microsoft Dynamics sur site.

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
>Utilisez cette procédure uniquement lors de l’intégration d’AEM Forms au serveur Microsoft Dynamics sur site.

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

1. Microsoft Dynamics utilise le protocole HTTPS. Pour appeler les points d’entrée AD FS depuis le serveur Forms, installez le certificat de site Microsoft Dynamics dans le fichier de stockage des certificats Java à l’aide de la commande `keytool` sur l’ordinateur exécutant AEM Forms.

## Configurer le service cloud pour votre service Microsoft Dynamics {#configure-cloud-service-for-your-microsoft-dynamics-service}

La configuration du **service cloud OData de MS Dynamics (service OData)** est fournie avec la configuration OData par défaut. Pour le configurer afin qu’il se connecte à votre service Microsoft Dynamics, procédez comme suit.

1. Accédez à **[!UICONTROL Outils > Cloud Service > Sources de données]**, puis sélectionnez la variable `global` dossier de configuration.
1. Sélectionner **CLOUD SERVICE OData MS Dynamics (service OData)** configuration et sélectionnez **[!UICONTROL Propriétés]**. La boîte de dialogue de propriété de configuration du service cloud s’ouvre.

   Dans l’onglet **Paramètres d’authentification** :

   1. Saisissez la valeur de la variable **Racine du service** champ . Accédez à l’instance Dynamics et à **Ressources de développement** pour afficher la valeur du champ Racine du service. Par exemple, https://&lt;nom-client>/api/data/v9.1/

   1. Remplacez les valeurs par défaut dans les champs **ID client** (également appelé **ID d’application**), **Secret client**, **URL OAuth**, **URL du jeton d’actualisation**, **URL du jeton d’accès** et **Ressource** avec les valeurs de votre configuration de service Microsoft Dynamics. Il est obligatoire de spécifier l’URL de l’instance dynamique dans le champ **Ressource** afin de configurer Microsoft Dynamics avec un modèle de données de formulaire. Utilisez l’URL racine du service pour dériver l’URL de l’instance dynamique. For example, [https://org.crm.dynamics.com](https://org.crm.dynamics.com/).

   1. Spécifiez **openid** dans le champ **Portée de l’autorisation** pour le processus d’autorisation sur Microsoft Dynamics.

   ![Paramètres d’authentification](assets/dynamics_authentication_settings_new.png)

1. Cliquez sur **[!UICONTROL Connexion à OAuth]**. Vous êtes redirigé vers la page de connexion de Microsoft Dynamics.
1. Connectez-vous avec vos informations d’identification Microsoft Dynamics et autorisez la connexion de la configuration du service cloud au service Microsoft Dynamics. Il s’agit d’une tâche unique permettant d’établir une connexion entre le service cloud et le service.

   Vous êtes ensuite redirigé vers la page de configuration du service cloud, qui affiche un message indiquant que la configuration OData a bien été enregistrée.

Le service cloud MS Dynamics OData Cloud Service (Service OData) est configuré et connecté à votre service Dynamics.

## Création d’un modèle de données de formulaire {#create-form-data-model}

Lorsque vous installez le package AEM Forms, un modèle de données de formulaire **Microsoft Dynamics FDM** est déployé sur votre instance AEM. Par défaut, le modèle de données de formulaire utilise le service Microsoft Dynamics configuré dans le service cloud OData MS Dynamics (Service OData) comme source de données.

Lors de l’ouverture initiale du modèle de données de formulaire, il se connecte au service Microsoft Dynamics configuré et récupère les entités de votre instance Microsoft Dynamics. Les entités &quot;contact&quot; et &quot;prospect&quot; de Microsoft Dynamics sont déjà ajoutées dans le modèle de données de formulaire.

Pour consulter le modèle de données de formulaire, accédez à **[!UICONTROL Forms > Intégrations de données]**. Sélectionner **Microsoft Dynamics FDM** et cliquez sur **Modifier** pour ouvrir le modèle de données de formulaire en mode d’édition. Vous pouvez également ouvrir le modèle de données de formulaire directement à partir de l’URL suivante : 

`https://'[server]:[port]'/aem/fdm/editor.html/content/dam/formsanddocuments-fdm/ms-dynamics-fdm`

![default-fdm-1](assets/default-fdm-1.png)

Ensuite, vous pouvez créer un formulaire adaptatif basé sur le modèle de données de formulaire et l’utiliser dans divers cas de formulaires adaptatifs, tels que :

* Remplir le formulaire adaptatif en obtenant des informations des entités et services Microsoft Dynamics
* Appeler des opérations du serveur Microsoft Dynamics définies dans un modèle de données de formulaire à l’aide de règles de formulaires adaptatifs
* Écrire les données de formulaire envoyées dans les entités Microsoft Dynamics

Il est recommandé de créer une copie du modèle de données de formulaire fourni avec le package AEM Forms et de configurer les modèles et services de données en fonction de vos besoins. Cela permet de s’assurer que les futures mises à jour du module ne remplacent pas votre modèle de données de formulaire.

Pour plus d’informations sur la création et l’utilisation d’un modèle de données de formulaire dans les processus métier, voir [Intégration de données](../../forms/using/data-integration.md).
