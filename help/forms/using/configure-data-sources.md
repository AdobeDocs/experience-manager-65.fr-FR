---
title: Configuration des sources de données
seo-title: Configuration des sources de données
description: Découvrez comment configurer différents types de sources de données et tirer parti de la création de modèles de données de formulaire.
seo-description: Découvrez comment configurer différents types de sources de données et tirer parti de la création de modèles de données de formulaire.
uuid: 12360c8c-b596-4f9b-837a-10a8ff5c7448
topic-tags: integration
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 9d78a6dc-fc9c-415b-b817-164fe6648b30
docset: aem65
feature: Modèle de données de formulaire
exl-id: 7a1d9d57-66f4-4f20-91c2-ace5a71a52f2
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '2023'
ht-degree: 58%

---

# Configuration des sources de données{#configure-data-sources}

![](do-not-localize/data-integeration.png)

L’intégration de données AEM Forms permet de configurer des sources de données disparates et de s’y connecter. La prise en charge est assurée par défaut pour les types suivants. Toutefois, avec peu de personnalisation, vous pouvez intégrer d’autres sources de données.

* Bases de données relationnelles : MySQL, Microsoft SQL Server, IBM DB2 et Oracle RDBMS
* Profil utilisateur AEM
* Services web RESTful
* Services web SOAP
* Services OData

L’intégration de données prend en charge l’authentification OAuth2.0, de base ou par clé API par défaut, et permet de mettre en œuvre une authentification personnalisée pour accéder aux services web. Alors que les services RESTful, SOAP et OData sont configurés dans les services cloud AEM, JDBC pour les bases de données relationnelles et Connector pour le profil utilisateur AEM sont configurés dans la console Web AEM.

## Configurer la base de données relationnelle {#configure-relational-database}

Vous pouvez configurer des bases de données relationnelles à l’aide de la configuration de la console Web AEM. Procédez comme suit :

1. Accédez à AEM console web à l’adresse https://server:host/system/console/configMgr.
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
   >    1. Accédez à https://&#39;[server]:[port]&#39;/system/console/crypto.
   >    1. Dans le champ **[!UICONTROL Texte brut]** , spécifiez le mot de passe ou toute chaîne à chiffrer et appuyez sur **[!UICONTROL Protect]**.

   >    
   >    
   >    
   >Le texte chiffré apparaît dans le champ Texte protégé que vous pouvez spécifier dans la configuration.

1. Activer **[!UICONTROL Test lors de l’emprunt]** ou **[!UICONTROL Test lors du renvoi]** pour spécifier que les objets sont validés avant d’être empruntés ou retournés depuis et vers le pool, respectivement.
1. Spécifiez une requête SQL SELECT dans le champ **[!UICONTROL Requête de validation]** pour valider les connexions du pool. La requête doit renvoyer au moins une ligne. En fonction de votre base de données, définissez l’une des options suivantes :

   * SELECT 1 (MySQL et MS SQL)
   * SELECT 1 from dual (Oracle)

1. Appuyez sur **[!UICONTROL Save]** (Enregistrer) pour enregistrer la configuration.

## Configurer le profil utilisateur AEM {#configure-aem-user-profile}

Vous pouvez configurer le profil utilisateur AEM à l’aide de la configuration User Profile Connector dans AEM Web Console. Procédez comme suit :

1. Accédez à AEM console web à l’adresse https://&#39;[server]:[port]&#39;system/console/configMgr.
1. Recherchez **[!UICONTROL AEM Forms Data Integrations - User Profile Connector Configuration]** et appuyez pour ouvrir la configuration en mode d’édition.
1. Dans la boîte de dialogue Configuration du connecteur de profil utilisateur, vous pouvez ajouter, supprimer ou mettre à jour les propriétés du profil utilisateur. Les propriétés spécifiées pourront être utilisées dans le modèle de données de formulaire. Utilisez le format suivant pour spécifier les propriétés du profil utilisateur :

   `name=[property_name_with_location_in_user_profile],type=[property_type]`

   Exemples :

   * `name=profile/phoneNumber,type=string`
   * `name=profile/empLocation/*/city,type=string`

   >[!NOTE]
   >
   >La balise ***** de l’exemple ci-dessus indique tous les noeuds sous le noeud `profile/empLocation/` du profil utilisateur AEM dans la structure CRXDE. Cela signifie que le modèle de données de formulaire peut accéder à la propriété `city` de type `string` présente dans n’importe quel noeud sous le noeud `profile/empLocation/`. Toutefois, les nœuds qui contiennent la propriété spécifiée doivent suivre une structure cohérente.

1. Appuyez sur **[!UICONTROL Save]** (Enregistrer) pour enregistrer la configuration.

## Configurer le dossier pour les configurations de service cloud {#cloud-folder}

>[!NOTE]
La configuration du dossier de services cloud est requise pour la configuration des services cloud pour les services RESTful, SOAP et OData.

Toutes les configurations de service cloud dans AEM sont consolidées dans le dossier `/conf` du référentiel AEM. Par défaut, le dossier `conf` contient le dossier `global` dans lequel vous pouvez créer des configurations de service cloud. Toutefois, vous devez l’activer manuellement pour les configurations cloud. Vous pouvez également créer des dossiers supplémentaires dans `conf` pour créer et organiser des configurations de service cloud.

Pour configurer le dossier pour les configurations de service cloud :

1. Accédez à **[!UICONTROL Outils > Général > Navigateur de configuration]**.
   * Pour plus d’informations, consultez la documentation relative au [Navigateur de configuration](/help/sites-administering/configurations.md).
1. Procédez comme suit pour activer le dossier global pour les configurations cloud ou ignorez cette étape pour créer et configurer un autre dossier pour les configurations de service cloud.

   1. Dans le **[!UICONTROL navigateur de configuration]**, sélectionnez le dossier `global` et appuyez sur **[!UICONTROL Propriétés]**.

   1. Dans la boîte de dialogue **[!UICONTROL Propriétés de configuration]**, activez **[!UICONTROL Configurations cloud]**.

   1. Appuyez sur **[!UICONTROL Enregistrer et fermer]** pour enregistrer la configuration et fermer la boîte de dialogue.

1. Dans le **[!UICONTROL navigateur de configuration]**, appuyez sur **[!UICONTROL Créer]**.
1. Dans la boîte de dialogue **[!UICONTROL Créer une configuration]**, indiquez un titre pour le dossier et activez **[!UICONTROL Configurations cloud]**.
1. Appuyez sur **[!UICONTROL Créer]** pour créer le dossier activé pour les configurations de service cloud.

## Configuration des services web RESTful {#configure-restful-web-services}

Le service Web RESTful peut être décrit à l’aide des [spécifications Swagger](https://swagger.io/specification/) au format JSON ou YAML dans un fichier de définition Swagger. Pour configurer le service Web RESTful dans les services cloud AEM, vérifiez que le fichier Swagger se trouve sur votre système de fichiers ou que l’URL où le fichier est hébergé.

Procédez comme suit pour configurer les services RESTful :

1. Accédez à **[!UICONTROL Outils > Cloud Services > Sources de données]**. Appuyez pour sélectionner le dossier dans lequel vous souhaitez créer une configuration cloud.

   Pour plus d’informations sur la création et la configuration d’un dossier pour les configurations de service cloud, voir [Configurer le dossier pour les configurations de service cloud](../../forms/using/configure-data-sources.md#cloud-folder).

1. Appuyez sur **[!UICONTROL Créer]** pour ouvrir l’**[!UICONTROL assistant Créer une configuration de source de données]**. Indiquez un nom et éventuellement un titre pour la configuration, sélectionnez **[!UICONTROL Service RESTful]** dans la liste déroulante **[!UICONTROL Type de service]**, recherchez et sélectionnez éventuellement une image miniature pour la configuration, puis appuyez sur **[!UICONTROL Suivant]**.
1. Spécifiez les informations suivantes pour le service RESTful :

   * Sélectionnez URL ou Fichier dans la liste déroulante Source Swagger et spécifiez l’URL Swagger vers le fichier de définition Swagger ou chargez le fichier Swagger depuis votre système de fichiers local.
   * Selon l’entrée Source Swagger, les champs suivants sont prérenseignés avec des valeurs :

      * Schéma : protocoles de transfert utilisés par l’API REST. Le nombre de types de schémas qui s’affichent dans la liste déroulante dépend des schémas définis dans la source Swagger.
      * Hôte : nom de domaine ou adresse IP de l’hôte qui sert l’API REST. Ce champ est obligatoire.
      * Chemin d’accès de base : le préfixe d’URL de tous les chemins d’API. Ce champ est facultatif.\
         Si nécessaire, modifiez les valeurs prérenseignées pour ces champs.
   * Sélectionnez le type d’authentification - Aucun, OAuth2.0, Authentification de base, Clé API, Authentification personnalisée ou Authentification mutuelle - pour accéder au service RESTful et fournir en conséquence des détails sur l’authentification.

   Si vous sélectionnez **[!UICONTROL Clé API]** comme type d’authentification, spécifiez la valeur de la clé API. La clé API peut être envoyée en tant qu’en-tête de requête ou en tant que paramètre de requête. Sélectionnez l’une de ces options dans la liste déroulante **[!UICONTROL Emplacement]** et indiquez le nom de l’en-tête ou du paramètre de requête dans le champ **[!UICONTROL Nom du paramètre]**.

   Si vous sélectionnez **[!UICONTROL Authentification mutuelle]** comme type d’authentification, voir [Authentification mutuelle basée sur un certificat pour les services Web RESTful et SOAP](#mutual-authentication).

1. Appuyez sur **[!UICONTROL Créer]** pour créer la configuration cloud pour le service RESTful.

### Configuration du client HTTP du modèle de données de formulaire pour optimiser les performances {#fdm-http-client-configuration}

[!DNL Experience Manager Forms] le modèle de données de formulaire lors de l’intégration aux services web RESTful en tant que source de données inclut des configurations de client HTTP pour l’optimisation des performances.
Effectuez les étapes suivantes pour configurer le client HTTP du modèle de données de formulaire :

1. Connectez-vous à [!DNL Experience Manager Forms] Instance d’auteur en tant qu’administrateur et accédez aux lots de la console web [!DNL Experience Manager]. L’URL par défaut est [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr).

1. Appuyez sur **[!UICONTROL Form Data Model Http Client Configuration pour la source de données REST]**.

1. Dans la boîte de dialogue [!UICONTROL Form Data Model Http Client Configuration for REST data source] :

   * Indiquez le nombre maximal de connexions autorisées entre le modèle de données de formulaire et les services web RESTful dans le champ **[!UICONTROL Limite de connexions au total]** . La valeur par défaut est de 20 connexions.

   * Indiquez le nombre maximal de connexions autorisées pour chaque itinéraire dans le champ **[!UICONTROL Limite de connexions par itinéraire]** . La valeur par défaut est de 2 connexions.

   * Indiquez la durée pour laquelle une connexion HTTP persistante est conservée en vie, dans le champ **[!UICONTROL Conserver en vie]** . La valeur par défaut est de 15 secondes.

   * Indiquez la durée pendant laquelle le serveur [!DNL Experience Manager Forms] attend l’établissement d’une connexion, dans le champ **[!UICONTROL Délai de connexion]** . La valeur par défaut est de 10 secondes.

   * Indiquez la période d’inactivité maximale entre deux paquets de données dans le champ **[!UICONTROL Délai d’inactivité du socket]** . La valeur par défaut est de 30 secondes.


## Configuration des services web SOAP {#configure-soap-web-services}

Les services web SOAP sont décrits à l’aide des [spécifications WSDL (Web Services Description Language)](https://www.w3.org/TR/wsdl). Pour configurer le service Web SOAP dans les services cloud AEM, vérifiez que vous disposez de l’URL WSDL pour le service Web et procédez comme suit :

1. Accédez à **[!UICONTROL Outils > Cloud Services > Sources de données]**. Appuyez pour sélectionner le dossier dans lequel vous souhaitez créer une configuration cloud.

   Pour plus d’informations sur la création et la configuration d’un dossier pour les configurations de service cloud, voir [Configurer le dossier pour les configurations de service cloud](../../forms/using/configure-data-sources.md#cloud-folder).

1. Appuyez sur **[!UICONTROL Créer]** pour ouvrir l’**[!UICONTROL assistant Créer une configuration de source de données]**. Indiquez un nom et éventuellement un titre pour la configuration, sélectionnez **[!UICONTROL Service Web SOAP]** dans la liste déroulante **[!UICONTROL Type de service]**, sélectionnez et sélectionnez une image miniature pour la configuration, puis appuyez sur **[!UICONTROL Suivant]**.
1. Spécifiez les éléments suivants pour le service Web SOAP :

   * URL WSDL pour le service Web.
   * Point d’entrée du service. Spécifiez une valeur dans ce champ pour remplacer le point d’entrée du service mentionné dans WSDL.
   * Sélectionnez le type d’authentification (Aucun, OAuth2.0, Authentification de base, Authentification personnalisée, Jeton X509 ou Authentification mutuelle) pour accéder au service SOAP et fournir en conséquence les détails de l’authentification.

      Si vous sélectionnez **[!UICONTROL Jeton X509]** comme type d’authentification, configurez le certificat X509. Pour plus d’informations, voir [Configuration des certificats](install-configure-document-services.md#set-up-certificates-for-reader-extension-and-encryption-service).
Spécifiez l’alias KeyStore pour le certificat X509 dans le champ **[!UICONTROL Alias de clé]**. Spécifiez la durée, en secondes, jusqu’à ce que la demande d’authentification reste valide, dans le champ **[!UICONTROL Durée de vie]**. Vous pouvez également choisir de signer le corps du message ou l’en-tête d’horodatage ou les deux.

      Si vous sélectionnez **[!UICONTROL Authentification mutuelle]** comme type d’authentification, voir [Authentification mutuelle basée sur un certificat pour les services Web RESTful et SOAP](#mutual-authentication).

1. Appuyez sur **[!UICONTROL Créer]** pour créer la configuration cloud pour le service web SOAP.

## Configuration des services OData {#config-odata}

Un service OData est identifié par son URL racine de service. Pour configurer un service OData dans les services cloud AEM, vérifiez que vous disposez de l’URL racine du service et procédez comme suit :

>[!NOTE]
Pour obtenir un guide pas à pas sur la configuration de Microsoft Dynamics 365, en ligne ou sur site, voir [Configuration OData de Microsoft Dynamics](/help/forms/using/ms-dynamics-odata-configuration.md).

1. Accédez à **[!UICONTROL Outils > Cloud Services > Sources de données]**. Appuyez pour sélectionner le dossier dans lequel vous souhaitez créer une configuration cloud.

   Pour plus d’informations sur la création et la configuration d’un dossier pour les configurations de service cloud, voir [Configurer le dossier pour les configurations de service cloud](../../forms/using/configure-data-sources.md#cloud-folder).

1. Appuyez sur **[!UICONTROL Créer]** pour ouvrir l’**[!UICONTROL assistant Créer une configuration de source de données]**. Indiquez un nom et éventuellement un titre pour la configuration, sélectionnez **[!UICONTROL Service OData]** dans la liste déroulante **[!UICONTROL Type de service]**, cherchez et sélectionnez éventuellement une miniature pour la configuration, puis appuyez sur **[!UICONTROL Suivant]**.
1. Spécifiez les informations suivantes pour le service OData :

   * URL racine du service pour le service OData à configurer.
   * Sélectionnez le type d’authentification - Aucun, OAuth2.0, Authentification de base ou Authentification personnalisée - pour accéder au service OData et fournir en conséquence les détails de l’authentification.

   >[!NOTE]
   Vous devez sélectionner le type d’authentification OAuth 2.0 pour vous connecter aux services Microsoft Dynamics à l’aide du point d’entrée OData en tant que racine du service.

1. Appuyez sur **Créer** pour créer la configuration de cloud pour le service OData.

## Authentification mutuelle basée sur des certificats pour les services Web RESTful et SOAP {#mutual-authentication}

Lorsque vous activez l’authentification mutuelle pour le modèle de données de formulaire, la source de données et AEM serveur exécutant le modèle de données de formulaire authentifient l’identité de l’autre avant de partager des données. Vous pouvez utiliser l’authentification mutuelle pour les connexions REST et SOAP (sources de données). Pour configurer l’authentification mutuelle pour un modèle de données de formulaire dans votre environnement AEM Forms :

1. Téléchargez la clé privée (certificat) sur le serveur [!DNL AEM Forms]. Pour charger la clé privée :
   1. Connectez-vous à votre serveur [!DNL AEM Forms] en tant qu’administrateur.
   1. Accédez à **[!UICONTROL Outils]** > **[!UICONTROL Sécurité]** > **[!UICONTROL Utilisateurs]**. Sélectionnez l’utilisateur `fd-cloudservice` et appuyez sur **[!UICONTROL Propriétés]**.
   1. Ouvrez l’onglet **[!UICONTROL Keystore]**, développez l’option **[!UICONTROL Ajouter une clé privée à partir du fichier KeyStore]**, téléchargez le fichier KeyStore, spécifiez les alias et mots de passe, puis appuyez sur **[!UICONTROL Envoyer]**. Le certificat est téléchargé.  L’alias de la clé privée est mentionné dans le certificat et défini lors de la création du certificat.
1. Téléchargez le certificat de confiance dans le Trust Store global. Pour télécharger le certificat :
   1. Accédez à **[!UICONTROL Outils]** > **[!UICONTROL Sécurité]** > **[!UICONTROL Trust Store]**.
   1. Développez l’option **[!UICONTROL Ajouter un certificat à partir du fichier CER]**, appuyez sur **[!UICONTROL Sélectionner le fichier de certificat]**, téléchargez le certificat, puis appuyez sur **[!UICONTROL Envoyer]**.
1. Configurez les services Web [SOAP](#configure-soap-web-services) ou [RESTful](#configure-restful-web-services) comme source de données et sélectionnez **[!UICONTROL Authentification mutuelle]** comme type d’authentification. Si vous configurez plusieurs certificats auto-signés pour l’utilisateur `fd-cloudservice`, indiquez le nom de l’alias de clé pour le certificat.

## Étapes suivantes {#next-steps}

Vous avez configuré la source de données. Vous pouvez ensuite créer un modèle de données de formulaire ou, si vous avez déjà créé un modèle de données de formulaire sans source de données, vous pouvez l’associer aux sources de données que vous venez de configurer. Voir [Création d’un modèle de données de formulaire](/help/forms/using/create-form-data-models.md) pour plus de détails.
