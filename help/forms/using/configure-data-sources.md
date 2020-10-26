---
title: Configurer les sources de données
seo-title: Configurer les sources de données
description: Découvrez comment configurer différents types de sources de données et tirer parti de la création de modèles de données de formulaire.
seo-description: Découvrez comment configurer différents types de sources de données et tirer parti de la création de modèles de données de formulaire.
uuid: 12360c8c-b596-4f9b-837a-10a8ff5c7448
topic-tags: integration
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 9d78a6dc-fc9c-415b-b817-164fe6648b30
docset: aem65
translation-type: tm+mt
source-git-commit: ce64b148ba96cc64670aaf96c1b201bafa282b98
workflow-type: tm+mt
source-wordcount: '1810'
ht-degree: 46%

---


# Configurer les sources de données{#configure-data-sources}

![](do-not-localize/data-integeration.png)

L’intégration de données AEM Forms permet de configurer des sources de données disparates et de s’y connecter. La prise en charge est assurée par défaut pour les types suivants. Toutefois, avec peu de personnalisation, vous pouvez intégrer d’autres sources de données.

* Bases de données relationnelles : MySQL, Microsoft SQL Server, IBM DB2 et Oracle RDBMS
* Profil utilisateur AEM
* Services web RESTful
* Services web SOAP
* Services OData

L’intégration des données prend en charge OAuth2.0, l’authentification de base et les types d’authentification de clé d’API prêts à l’emploi et permet l’implémentation de l’authentification personnalisée pour l’accès aux services Web. Alors que les services RESTful, SOAP et OData sont configurés dans les services cloud AEM, JDBC pour les bases de données relationnelles et Connector pour le profil utilisateur AEM sont configurés dans la console Web AEM.

## Configurer la base de données relationnelle {#configure-relational-database}

Vous pouvez configurer des bases de données relationnelles à l’aide de la configuration de la console Web AEM. Procédez comme suit :

1. Accédez à AEM console Web à l’adresse https://server:host/system/console/configMgr.
1. Recherchez la configuration **[!UICONTROL Apache Sling Connection Pooled DataSource]**. Appuyez pour ouvrir la configuration en mode édition.
1. Dans la boîte de dialogue de configuration, spécifiez les détails de la base de données que vous souhaitez configurer, tels que :

   * Nom de la source de données
   * Propriété de service de source de données qui stocke le nom de la source de données
   * Nom de classe Java pour le pilote JDBC
   * URI de connexion JDBC
   * Nom d’utilisateur et mot de passe pour établir la connexion avec le pilote JDBC

   >[!NOTE]
   >
   >Veillez à chiffrer les informations sensibles telles que les mots de passe avant de configurer la source de données. Pour chiffrer :
   >
   >    
   >    
   >    1. Go to https://&#39;[server]:[port]&#39;/system/console/crypto.
   >    1. In the **[!UICONTROL Plain Text]** field, specify the password or any string to encrypt and tap **[!UICONTROL Protect]**.

   >    
   >    
   >    
   >Le texte chiffré apparaît dans le champ Texte protégé que vous pouvez spécifier dans la configuration.

1. Activer **[!UICONTROL Test lors de l’emprunt]** ou **[!UICONTROL Test lors du renvoi]** pour spécifier que les objets sont validés avant d’être empruntés ou retournés depuis et vers le pool, respectivement.
1. Spécifiez une requête SQL SELECT dans le champ **[!UICONTROL Requête de validation]** pour valider les connexions du pool. La requête doit renvoyer au moins une ligne. En fonction de votre base de données, définissez l’une des options suivantes :

   * SELECT 1 (MySQL et MS SQL)
   * SELECT 1 from dual (Oracle)

1. Tap **[!UICONTROL Save]** to save the configuration.

## Configurer le profil utilisateur AEM {#configure-aem-user-profile}

Vous pouvez configurer le profil utilisateur AEM à l’aide de la configuration User Profile Connector dans AEM Web Console. Procédez comme suit :

1. Go to AEM web console at https://&#39;[server]:[port]&#39;system/console/configMgr.
1. Look for **[!UICONTROL AEM Forms Data Integrations - User Profile Connector Configuration]** and tap to open the configuration in edit mode.
1. Dans la boîte de dialogue Configuration du connecteur de profil utilisateur, vous pouvez ajouter, supprimer ou mettre à jour les propriétés du profil utilisateur. Les propriétés spécifiées pourront être utilisées dans le modèle de données de formulaire. Utilisez le format suivant pour spécifier les propriétés du profil utilisateur :

   `name=[property_name_with_location_in_user_profile],type=[property_type]`

   Exemples :

   * `name=profile/phoneNumber,type=string`
   * `name=profile/empLocation/*/city,type=string`

   >[!NOTE]
   >
   >The ***** in the above example denotes all nodes under the `profile/empLocation/` node in AEM user profile in CRXDE structure. It means that the form data model can access the `city` property of type `string` present in any node under the `profile/empLocation/` node. Toutefois, les nœuds qui contiennent la propriété spécifiée doivent suivre une structure cohérente.

1. Tap **[!UICONTROL Save]** to save the configuration.

## Configuration du dossier pour les configurations de service cloud {#cloud-folder}

>[!NOTE]
La configuration du dossier des services cloud est requise pour la configuration des services cloud pour les services RESTful, SOAP et OData.

All cloud service configurations in AEM are consolidated in the `/conf` folder in AEM repository. Par défaut, le dossier `conf` contient le dossier `global` dans lequel vous pouvez créer des configurations de service cloud. Toutefois, vous devez l’activer manuellement pour les configurations cloud. Vous pouvez également créer des dossiers supplémentaires dans `conf` pour créer et organiser des configurations de service cloud.

Pour configurer le dossier pour les configurations de service cloud :

1. Go to **[!UICONTROL Tools > General > Configuration Browser]**.
   * See the [Configuration Browser](/help/sites-administering/configurations.md) documentation for more information.
1. Procédez comme suit pour activer le dossier global pour les configurations cloud ou ignorez cette étape pour créer et configurer un autre dossier pour les configurations de service cloud.

   1. Dans le **[!UICONTROL navigateur de configuration]**, sélectionnez le dossier `global` et appuyez sur **[!UICONTROL Propriétés]**.

   1. Dans la boîte de dialogue **[!UICONTROL Propriétés de configuration]**, activez **[!UICONTROL Configurations cloud]**.

   1. Appuyez sur **[!UICONTROL Enregistrer et fermer]** pour enregistrer la configuration et fermer la boîte de dialogue.

1. Dans le **[!UICONTROL navigateur de configuration]**, appuyez sur **[!UICONTROL Créer]**.
1. Dans la boîte de dialogue **[!UICONTROL Créer une configuration]**, indiquez un titre pour le dossier et activez **[!UICONTROL Configurations cloud]**.
1. Tap **[!UICONTROL Create]** to create the folder enabled for cloud service configurations.

## Configurer les services Web RESTful {#configure-restful-web-services}

RESTful web service can be described using [Swagger specifications](https://swagger.io/specification/) in JSON or YAML format in a Swagger definition file. Pour configurer le service Web RESTful dans les services cloud AEM, veillez à disposer du fichier Swagger sur votre système de fichiers ou de l’URL d’hébergement du fichier.

Procédez comme suit pour configurer les services RESTful :

1. Accédez à **[!UICONTROL Outils > Services cloud > Sources de données]**. Appuyez sur pour sélectionner le dossier dans lequel vous souhaitez créer une configuration de cloud.

   See [Configure folder for cloud service configurations](../../forms/using/configure-data-sources.md#cloud-folder) for information about creating and configuring a folder for cloud service configurations.

1. Tap **[!UICONTROL Create]** to open the **[!UICONTROL Create Data Source Configuration wizard]**. Indiquez un nom et éventuellement un titre pour la configuration, sélectionnez **[!UICONTROL Service RESTful]** dans la liste déroulante **[!UICONTROL Type de service]**, recherchez et sélectionnez éventuellement une image miniature pour la configuration, puis appuyez sur **[!UICONTROL Suivant]**.
1. Spécifiez les informations suivantes pour le service RESTful :

   * Sélectionnez URL ou Fichier dans la liste déroulante Source Swagger et, en conséquence, spécifiez l’URL Swagger vers le fichier de définition Swagger ou téléchargez le fichier Swagger depuis votre système de fichiers local.
   * En fonction de l’entrée Source Swagger, les champs suivants sont prérenseignés avec des valeurs :

      * Schéma : Protocoles de transfert utilisés par l’API REST. Le nombre de types de schéma affichés dans la liste déroulante dépend des schémas définis dans la source Swagger.
      * Hôte : Nom de domaine ou adresse IP de l’hôte qui diffuse l’API REST. Ce champ est obligatoire.
      * Chemin d’accès de base : Préfixe d’URL pour tous les chemins d’API. Ce champ est facultatif.\
         Si nécessaire, modifiez les valeurs prérenseignées pour ces champs.
   * Sélectionnez le type d’authentification — Aucun, OAuth2.0, Authentification de base, Clé d’API, Authentification personnalisée ou Authentification mutuelle — pour accéder au service RESTful et, en conséquence, fournir des détails pour l’authentification.

   Si vous sélectionnez Clé **** d&#39;API comme type d&#39;authentification, spécifiez la valeur de la clé d&#39;API. La clé d&#39;API peut être envoyée en tant qu&#39;en-tête de requête ou en tant que paramètre de requête. Sélectionnez l’une de ces options dans la liste déroulante **[!UICONTROL Emplacement]** et indiquez le nom de l’en-tête ou du paramètre de requête dans le champ Nom **[!UICONTROL du]** paramètre en conséquence.

   Si vous sélectionnez l’authentification **** mutuelle comme type d’authentification, voir Authentification mutuelle basée sur des [certificats pour les services](#mutual-authentication)Web RESTful et SOAP.

1. Appuyez sur **[!UICONTROL Créer]** pour créer la configuration cloud pour le service RESTful.

## Configurer les services Web SOAP {#configure-soap-web-services}

Les services Web basés sur SOAP sont décrits à l’aide des [spécifications WSDL (Web Services Description Language).](https://www.w3.org/TR/wsdl) Pour configurer le service Web SOAP dans les services cloud AEM, vérifiez que vous disposez de l’URL WSDL pour le service Web et procédez comme suit :

1. Accédez à **[!UICONTROL Outils > Services cloud > Sources de données]**. Appuyez sur pour sélectionner le dossier dans lequel vous souhaitez créer une configuration de cloud.

   See [Configure folder for cloud service configurations](../../forms/using/configure-data-sources.md#cloud-folder) for information about creating and configuring a folder for cloud service configurations.

1. Tap **[!UICONTROL Create]** to open the **[!UICONTROL Create Data Source Configuration wizard]**. Indiquez un nom et éventuellement un titre pour la configuration, sélectionnez **[!UICONTROL Service Web SOAP]** dans la liste déroulante **[!UICONTROL Type de service]**, sélectionnez et sélectionnez une image miniature pour la configuration, puis appuyez sur **[!UICONTROL Suivant]**.
1. Spécifiez les éléments suivants pour le service Web SOAP :

   * URL WSDL pour le service Web.
   * Point de fin du service. Spécifiez une valeur dans ce champ pour remplacer le point de terminaison de service mentionné dans WSDL.
   * Sélectionnez le type d’authentification : Aucun, OAuth2.0, Authentification de base, Authentification personnalisée, Jeton X509 ou Authentification mutuelle, pour accéder au service SOAP et, par conséquent, fournir les détails de l’authentification.

      Si vous sélectionnez Jeton **** X509 comme type d’authentification, configurez le certificat X509. Pour plus d’informations, voir [Configuration des certificats](install-configure-document-services.md#set-up-certificates-for-reader-extension-and-encryption-service).
Spécifiez l’alias KeyStore pour le certificat X509 dans le champ **[!UICONTROL Key Alias]** (Alias de clé). Spécifiez la durée, en secondes, jusqu’à ce que la demande d’authentification reste valide, dans le champ **[!UICONTROL Durée de vie]** . Vous pouvez également choisir de signer le corps du message ou l’en-tête d’horodatage ou les deux.

      Si vous sélectionnez l’authentification **** mutuelle comme type d’authentification, voir Authentification mutuelle basée sur des [certificats pour les services](#mutual-authentication)Web RESTful et SOAP.

1. Appuyez sur **[!UICONTROL Créer]** pour créer la configuration cloud pour le service Web SOAP.

## Configurer les services OData {#config-odata}

Un service OData est identifié par son URL racine de service. Pour configurer un service OData dans les services cloud AEM, vérifiez que vous disposez de l’URL racine du service et procédez comme suit :

>[!NOTE]
Pour obtenir un guide pas à pas sur la configuration de Microsoft Dynamics 365, en ligne ou sur site, voir [Configuration OData de Microsoft Dynamics](/help/forms/using/ms-dynamics-odata-configuration.md).

1. Accédez à **[!UICONTROL Outils > Services cloud > Sources de données]**. Appuyez sur pour sélectionner le dossier dans lequel vous souhaitez créer une configuration de cloud.

   See [Configure folder for cloud service configurations](../../forms/using/configure-data-sources.md#cloud-folder) for information about creating and configuring a folder for cloud service configurations.

1. Tap **[!UICONTROL Create]** to open the **[!UICONTROL Create Data Source Configuration wizard]**. Indiquez un nom et éventuellement un titre pour la configuration, sélectionnez **[!UICONTROL Service OData]** dans la liste déroulante **[!UICONTROL Type de service]**, recherchez et sélectionnez éventuellement une image miniature pour la configuration, puis appuyez sur **[!UICONTROL Suivant]**.
1. Spécifiez les informations suivantes pour le service OData :

   * URL racine du service pour le service OData à configurer.
   * Sélectionnez le type d’authentification — Aucun, OAuth2.0, Authentification de base ou Authentification personnalisée — pour accéder au service OData et, par conséquent, fournir les détails de l’authentification.

   >[!NOTE]
   Vous devez sélectionner le type d’authentification OAuth 2.0 pour vous connecter aux services Microsoft Dynamics à l’aide du point de terminaison OData en tant que racine du service.

1. Tap **Create** to create the cloud configuration for the OData service.

## Authentification mutuelle basée sur des certificats pour les services Web RESTful et SOAP {#mutual-authentication}

Lorsque vous activez l’authentification mutuelle pour le modèle de données de formulaire, la source de données et AEM serveur exécutant le modèle de données de formulaire authentifient l’identité de chacun avant de partager des données. Vous pouvez utiliser l’authentification mutuelle pour les connexions REST et SOAP (sources de données). Pour configurer l’authentification mutuelle pour un modèle de données de formulaire sur votre environnement AEM Forms :

1. Téléchargez la clé privée (certificat) sur [!DNL AEM Forms] le serveur. Pour télécharger la clé privée :
   1. Connectez-vous à votre [!DNL AEM Forms] serveur en tant qu’administrateur.
   1. Navigate to **[!UICONTROL Tools]** > **[!UICONTROL Security]** > **[!UICONTROL Users]**. Sélectionnez l’ `fd-cloudservice` utilisateur et appuyez sur **[!UICONTROL Propriétés]**.
   1. Ouvrez l&#39;onglet **[!UICONTROL Keystore]** , développez l&#39;option **[!UICONTROL Ajouter la clé privée à partir du fichier]** KeyStore, téléchargez le fichier KeyStore, spécifiez les alias, mots de passe et appuyez sur **[!UICONTROL Envoyer]**. Le certificat est téléchargé.  L’alias de clé privée est mentionné dans le certificat et défini lors de la création du certificat.
1. Téléchargez le certificat d’approbation vers le Trust Store global. Pour télécharger le certificat :
   1. Accédez à **[!UICONTROL Outils]** > **[!UICONTROL Sécurité]** > **[!UICONTROL Trust Store]**.
   1. Développez l’option **[!UICONTROL Ajouter le certificat à partir du fichier]** CER, appuyez sur **[!UICONTROL Sélectionner un fichier]** de certificat, téléchargez le certificat et appuyez sur **[!UICONTROL Envoyer]**.
1. Configurez les services Web [SOAP](#configure-soap-web-services) ou [RESTful](#configure-restful-web-services) comme source de données et sélectionnez l’authentification **** mutuelle comme type d’authentification. Si vous configurez plusieurs certificats auto-signés pour `fd-cloudservice` l’utilisateur, spécifiez le nom de l’alias de clé pour le certificat.

## Étapes suivantes {#next-steps}

Vous avez configuré la source de données. Vous pouvez ensuite créer un modèle de données de formulaire ou, si vous avez déjà créé un modèle de données de formulaire sans source de données, vous pouvez l’associer aux sources de données que vous venez de configurer. See [Create form data model](/help/forms/using/create-form-data-models.md) for details.
