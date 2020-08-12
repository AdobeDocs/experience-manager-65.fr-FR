---
title: '"Didacticiel : créer un modèle de données de formulaire "'
seo-title: Didacticiel de création d’un modèle de données de formulaire
description: Créer un modèle de données de formulaire
seo-description: Créer un modèle de données de formulaire
uuid: b9d2bb1b-90f0-44f4-b1e3-0603cdf5f5b8
contentOwner: khsingh
products: SG_EXPERIENCEMANAGER/6.3/FORMS
discoiquuid: 12e6c325-ace0-4a57-8ed4-6f7ceee23099
docset: aem65
translation-type: tm+mt
source-git-commit: 78768e6eab65f452421d8809384500c6eab6b97f
workflow-type: tm+mt
source-wordcount: '1430'
ht-degree: 71%

---


# Didacticiel : créer un modèle de données de formulaire {#tutorial-create-form-data-model}

![04-create-form-data-model-main](assets/04-create-form-data-model-main.png)

Ce didacticiel est une étape de la série [Création de votre premier formulaire adaptatif](../../forms/using/create-your-first-adaptive-form.md). Il est recommandé de suivre la série dans l’ordre chronologique pour comprendre, exécuter et démontrer le cas d’utilisation complet du didacticiel.

## À propos du didacticiel {#about-the-tutorial}

AEM [!DNL Forms] data integration module allows you to create a form data model from disparate backend data sources such as AEM user profile, RESTful web services, SOAP-based web services, OData services, and relational databases. Vous pouvez configurer des objets et des services de modèle de données dans un modèle de données de formulaire et les associer à un formulaire adaptatif. Les champs de formulaire adaptatif sont liés aux propriétés de l’objet du modèle de données. Les services vous permettent de préremplir le formulaire adaptatif et d’écrire les données de formulaire soumises dans l’objet de modèle de données.

Pour plus d’informations sur l’intégration des données de formulaire et sur le modèle de données du formulaire, voir [Intégration de données AEM Forms](../../forms/using/data-integration.md).

Ce didacticiel vous décrit étape par étape le processus de préparation, création, configuration et association d’un modèle de données de formulaire avec un formulaire adaptatif. À la fin de ce didacticiel, vous serez capable de :

* [Configurer la base de données MySQL comme source de données](#config-database)
* [Créer un modèle de données de formulaire à l’aide de la base de données MySQL](#create-fdm)
* [Configurer un modèle de données de formulaire](#config-fdm)
* [Tester le modèle de données de formulaire](#test-fdm)

Le modèle de données de formulaire se présentera comme ceci :

![form-data-model_l](assets/form-data-model_l.png)

**A.** Sources de données configurées **B.** schémas de source de données **C.** Services disponibles **D.** Objets de modèle de données E. Services configurés ****

## Conditions préalables {#prerequisites}

Avant de commencer, vérifiez que vous disposez des éléments suivants :

* [!DNL MySQL]Base de données avec des exemples de données comme indiqué dans la section Conditions préalables de [Création de votre premier formulaire adaptatif](../../forms/using/create-your-first-adaptive-form.md)
* OSGi bundle for [!DNL MySQL] JDBC driver as explained in [Bundling the JDBC Database Driver](/help/sites-developing/jdbc.md#bundling-the-jdbc-database-driver)
* Adaptive form as explained in the first tutorial [Create an adaptive form](/help/forms/using/create-adaptive-form.md)

## Étape 1 : Configurer la base de données MySQL comme source de données {#config-database}

Vous pouvez configurer différents types de sources de données pour créer un modèle de données de formulaire. Pour ce didacticiel, nous allons configurer la base de données MySQL que vous avez configurée et remplie avec des exemples de données. Pour plus d’informations sur les autres sources de données prises en charge et sur leur configuration, reportez-vous à la section [Intégration de données AEM Forms](../../forms/using/data-integration.md).

Do the following to configure your [!DNL MySQL] database:

1. Install JDBC driver for [!DNL MySQL] database as an OSGi bundle:

   1. Log in to AEM [!DNL Forms] Author Instance as an administrator and go to AEM web console bundles. The default URL is [https://localhost:4502/system/console/bundles](https://localhost:4502/system/console/bundles).

   1. Tap **[!UICONTROL Install/Update]**. Une boîte de dialogue [!UICONTROL Télécharger/installer les bundles] s’affiche.

   1. Appuyez sur **[!UICONTROL Choisir un fichier]** pour rechercher et sélectionner le bundle OSGi du pilote JDBC [!DNL MySQL] Select **[!UICONTROL Start Bundle]** and **[!UICONTROL Refresh Packages]**, and tap **[!UICONTROL Install or Update]**. Ensure that the [!DNL Oracle Corporation's] JDBC Driver for [!DNL MySQL] is active. Le pilote est installé.

1. Configure [!DNL MySQL] database as a data source:

   1. Go to AEM web console at [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr).
   1. Recherchez la configuration **Apache Sling Connection Pooled DataSource**. Appuyez pour ouvrir la configuration en mode édition.
   1. Dans la boîte de dialogue de configuration, indiquez ce qui suit :

      * **Nom de la source de données :** vous pouvez spécifier un nom. Spécifiez par exemple **WeRetailMySQL**.
      * **Nom de la propriété de service de source de données** : spécifiez le nom de la propriété de service contenant le nom de la source de données. Il est spécifié lors de l’enregistrement de l’instance de source de données en tant que service OSGi. Par exemple, **datasource.name**.
      * **Classe de pilote JDBC** : spécifiez le nom de la classe Java du pilote JDBC. For [!DNL MySQL] database, specify **com.mysql.jdbc.Driver**.
      * **URI de connexion JDBC** : spécifiez l’URL de connexion de la base de données. Pour [!DNL MySQL] la base de données s’exécutant sur le port 3306 et le schéma weretail, l’URL est : `jdbc:mysql://'server':3306/weretail?autoReconnect=true&useUnicode=true&characterEncoding=utf-8`
      * **Nom d’utilisateur :** nom d’utilisateur de la base de données. Il est nécessaire d’activer le pilote JDBC pour établir une connexion avec la base de données.
      * **Mot de passe :** mot de passe de la base de données. Il est nécessaire d’activer le pilote JDBC pour établir une connexion avec la base de données.
      * **Test lors de l’emprunt :** activez l’option **[!UICONTROL Test lors de l’emprunt.]**
      * **Test lors du renvoi :** activez l’option **[!UICONTROL Test lors du renvoi.]**
      * **Requête de validation :** spécifiez une requête SQL SELECT pour valider les connexions du pool. La requête doit renvoyer au moins une ligne. Par exemple, **sélectionnez * depuis customerdetails**.
      * **Isolation de transaction** : définissez la valeur sur **READ_COMMITTED**.

         Leave other properties with default [values](https://tomcat.apache.org/tomcat-7.0-doc/jdbc-pool.html) and tap **[!UICONTROL Save]**.

         Une configuration similaire à la suivante est créée.

         ![relationnel-base-de-données-source-configuration](assets/relational-database-data-source-configuration.png)

## Étape 2 : Créer un modèle de données de formulaire {#create-fdm}

AEM [!DNL Forms] provides an intuitive user interface to [create a form data model](data-integration.md) from configured data sources. Vous pouvez utiliser plusieurs sources de données dans un modèle de données de formulaire. For our use case, we will use the configured [!DNL MySQL] data source.

Procédez comme suit pour créer un modèle de données de formulaire :

1. Dans l’instance d’auteur AEM, accédez à **[!UICONTROL Forms]** (Formulaires) > **[!UICONTROL Data Integrations]** (Intégrations de données).
1. Appuyez sur **[!UICONTROL Create]** (Créer) > **[!UICONTROL Form Data Model]** (Modèle de données de formulaire).
1. Dans la boîte de dialogue Créer un modèle de données de formulaire, spécifiez un **nom** pour le modèle de données de formulaire. Par exemple, **customer-shipping-billing-details**. Appuyez sur **[!UICONTROL Next]** (Suivant).
1. L’écran Sélectionner la source de données répertorie toutes les sources de données configurées. Select **WeRetailMySQL** data source and tap **[!UICONTROL Create]**.

   ![source de données-sélection](assets/data-source-selection.png)

The **customer-shipping-billing-details** form data model is created.

## Étape 3 : Configurer un modèle de données de formulaire {#config-fdm}

La configuration d’un modèle de données de formulaire comprend :

* L’ajout d’objets et de services de modèle de données
* La configuration des services de lecture et d’écriture pour les objets de modèle de données

Procédez comme suit pour configurer le modèle de données de formulaire :

1. On AEM author instance, navigate to **[!UICONTROL Forms]** > **[!UICONTROL Data Integrations]**. The default URL is [https://localhost:4502/aem/forms.html/content/dam/formsanddocuments-fdm](https://localhost:4502/aem/forms.html/content/dam/formsanddocuments-fdm).
1. The **customer-shipping-billing-details** form data model you created earlier is listed here. Ouvrez-le en mode d’édition.

   La source de données sélectionnée **WeRetailMySQL** est configurée dans le modèle de données de formulaire.

   ![default-fdm](assets/default-fdm.png)

1. Développez l’arborescence de la source de données WeRailMySQL. Select the following data model objects and services from **weretail** > **customerdetails** schema to form data model:

   * **Objets de modèle de données**:

      * id
      * name
      * shippingAddress
      * city
      * state
      * zipcode
   * **Services :**

      * get
      * mise à jour

   Appuyez sur **Ajouter la sélection** pour ajouter des objets et des services de modèle de données sélectionnés au modèle de données de formulaire.

   ![Schéma WeRetail](assets/weretail_schema_new.png)

   >[!NOTE]
   >
   >Les services get, update et insert par défaut pour les sources de données JDBC sont fournis prêts à l’emploi avec le modèle de données de formulaire.

1. Configurez les services de lecture et d’écriture pour les objets de modèle de données.

   1. Sélectionnez l’objet de modèle de données **customerdetails** et appuyez sur **[!UICONTROL Modifier les propriétés]**.
   1. Sélectionnez **[!UICONTROL get]** dans la liste déroulante Service de lecture. L’argument **id** qui est la clé principale de l’objet de modèle de données customerdetails est ajouté automatiquement. Appuyez sur ![aem_6_3_edit](assets/aem_6_3_edit.png) et configurez l’argument comme suit.

      ![read-default](assets/read-default.png)

   1. De même, sélectionnez **[!UICONTROL update]** en tant que Service d’écriture. L’objet **customerdetails** est ajouté automatiquement en tant qu’argument. L’argument est configuré comme suit.

      ![write-default](assets/write-default.png)

      Ajoutez et configurez l’argument **id** comme suit.

      ![id-arg](assets/id-arg.png)

   1. Appuyez sur **[!UICONTROL Terminé]** pour enregistrer les propriétés de l’objet de modèle de données. Then, tap **[!UICONTROL Save]** to save the form data model.

      Les services **[!UICONTROL get]** et **[!UICONTROL update]** sont ajoutés en tant que services par défaut pour l’objet de modèle de données.

      ![data-model-object](assets/data-model-object.png)

1. Accédez à l’onglet **[!UICONTROL Services]** et configurez les services **[!UICONTROL get]** et **[!UICONTROL update]**.

   1. Select the **[!UICONTROL get]** service and tap **[!UICONTROL Edit Properties]**. La boîte de dialogue Propriétés s’ouvre.
   1. Spécifiez les éléments suivants dans la boîte de dialogue Modifier les propriétés :

      * **Titre** : spécifiez le titre du service. Par exemple : extraire l’adresse d’expédition.
      * **Description** : spécifiez la description contenant le fonctionnement détaillé du service. Par exemple :

         This service retrieves shipping address and other customer details from [!DNL MySQL] database

      * **Objet de modèle de sortie** : sélectionnez le schéma contenant les données du client. Par exemple :

         schéma de détails du client

      * **Revenir au tableau** : désactivez l’option **Revenir au tableau**.
      * **Arguments** : sélectionnez l’argument nommé **ID**.

      Appuyez sur **[!UICONTROL Done]** (Terminé). Le service de récupération des détails des clients de la base de données MySQL est configuré.

      ![expédition-récupération-adresse](assets/shiiping-address-retrieval.png)

   1. Select the **[!UICONTROL update]** service and tap **[!UICONTROL Edit Properties]**. La boîte de dialogue Propriétés s’ouvre.

   1. Specify the following in the [!UICONTROL Edit Properties] dialog:

      * **Titre** : spécifiez le titre du service. Par exemple, Mettre à jour l’adresse de livraison.
      * **Description** : spécifiez la description contenant le fonctionnement détaillé du service. Par exemple :

         Ce service met à jour l’adresse de livraison et les champs associés dans la base de données MySQL.

      * **Objet de modèle d’entrée** : sélectionnez le schéma contenant les données du client. Par exemple :

         schéma de détails du client

      * **Type de sortie** : sélectionnez **VALEUR BOOLEENNE**.

      * **Arguments** : sélectionnez l’argument nommé **ID** et **customerdetails**.
      Appuyez sur **[!UICONTROL Done]** (Terminé). Le service **[!UICONTROL update]** permettant de mettre à jour les détails du client dans la base de données est configuré.[!DNL MySQL]

      ![envoi-adresse-mise à jour](assets/shiiping-address-update.png)



L’objet et les services de modèle de données dans le modèle de données de formulaire sont configurés. Vous pouvez à présent tester le modèle de données de formulaire.

## Étape 4 : tester le modèle de données de formulaire {#test-fdm}

Vous pouvez tester l’objet et les services du modèle de données pour vérifier que le modèle de données de formulaire est correctement configuré.

Procédez comme suit pour effectuer le test :

1. Accédez à l’onglet **[!UICONTROL Modèle]**, sélectionnez l’objet de modèle de données **customerdetails** et appuyez sur **[!UICONTROL Tester l’objet de modèle]**.
1. Dans la fenêtre [!UICONTROL Tester le modèle/service], sélectionnez **[!UICONTROL Objet de modèle de lecture]** dans le menu déroulant **[!UICONTROL Sélectionner le modèle/service]**.
1. Dans la section **customerdetails**, spécifiez une valeur pour l’argument **id**[!DNL MySQL] qui existe dans la base de données configurée et appuyez sur **[!UICONTROL Test]**.

   Les détails du client associés à l’ID spécifié sont récupérés et affichés dans la section **[!UICONTROL Sortie]**, comme indiqué ci-dessous.

   ![test-read-model](assets/test-read-model.png)

1. De même, vous pouvez tester l’objet de modèle et les services Écriture.

   Dans l’exemple suivant, le service update met à jour les informations relatives à l’adresse de l’ID 7102715 dans la base de données.

   ![test-write-model](assets/test-write-model.png)

   À présent, si vous testez à nouveau le service de lecture de modèle pour l’ID 7107215, il récupérera et affichera les détails du client mis à jour comme indiqué ci-dessous.

   ![read-update](assets/read-updated.png)
