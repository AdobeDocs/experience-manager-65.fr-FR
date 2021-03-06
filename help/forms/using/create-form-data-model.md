---
title: '"Didacticiel : créer un modèle de données de formulaire "'
seo-title: Create Form Data Model Tutorial
description: Création d’un modèle de données de formulaire
seo-description: Create form data model
uuid: b9d2bb1b-90f0-44f4-b1e3-0603cdf5f5b8
contentOwner: khsingh
products: SG_EXPERIENCEMANAGER/6.3/FORMS
discoiquuid: 12e6c325-ace0-4a57-8ed4-6f7ceee23099
docset: aem65
exl-id: 40bc5af6-9023-437e-95b0-f85d3df7d8aa
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: ht
source-wordcount: '1421'
ht-degree: 100%

---

# Didacticiel : créer un modèle de données de formulaire {#tutorial-create-form-data-model}

![04-create-form-data-model-main](assets/04-create-form-data-model-main.png)

Ce didacticiel est une étape de la série [Création de votre premier formulaire adaptatif](../../forms/using/create-your-first-adaptive-form.md). Il est recommandé de suivre la série dans l’ordre chronologique pour comprendre, exécuter et démontrer le cas d’utilisation complet du didacticiel.

## À propos du didacticiel {#about-the-tutorial}

Le module d’intégration de données AEM [!DNL Forms] vous permet de créer un modèle de données de formulaire à partir de sources de données principales disparates telles que le profil utilisateur AEM, les services web RESTful, les services web basés sur SOAP, les services OData et les bases de données relationnelles. Vous pouvez configurer des objets et des services de modèle de données dans un modèle de données de formulaire et les associer à un formulaire adaptatif. Les champs de formulaire adaptatif sont liés aux propriétés de l’objet du modèle de données. Les services vous permettent de préremplir le formulaire adaptatif et d’écrire les données de formulaire soumises dans l’objet de modèle de données.

Pour plus d’informations sur l’intégration des données de formulaire et sur le modèle de données du formulaire, voir [Intégration de données AEM Forms](../../forms/using/data-integration.md).

Ce didacticiel vous décrit étape par étape le processus de préparation, création, configuration et association d’un modèle de données de formulaire avec un formulaire adaptatif. À la fin de ce didacticiel, vous serez capable de :

* [Configurer la base de données MySQL comme source de données](#config-database)
* [Créer un modèle de données de formulaire à l’aide de la base de données MySQL](#create-fdm)
* [Configurer un modèle de données de formulaire](#config-fdm)
* [Tester le modèle de données de formulaire](#test-fdm)

Le modèle de données de formulaire se présentera comme ceci :

![form-data-model_l](assets/form-data-model_l.png)

**A.** Sources de données configurées **B.** Schémas de sources de données **C.** Services disponibles **D.** Objets de modèle de données **E.** Services configurés

## Prérequis {#prerequisites}

Avant de commencer, vérifiez que vous disposez des éléments suivants :

* Base de données [!DNL MySQL] avec des exemples de données comme indiqué dans la section Conditions préalables de [Création de votre premier formulaire adaptatif](../../forms/using/create-your-first-adaptive-form.md)
* Bundle OSGi pour le pilote JDBC [!DNL MySQL], comme expliqué dans la section [Regrouper le pilote de base de données JDBC](/help/sites-developing/jdbc.md#bundling-the-jdbc-database-driver)
* Formulaire adaptatif, comme expliqué dans le tout premier didacticiel de mise en route [Créer un formulaire adaptatif](/help/forms/using/create-adaptive-form.md).

## Étape 1 : configurer la base de données MySQL comme source de données {#config-database}

Vous pouvez configurer différents types de sources de données pour créer un modèle de données de formulaire. Pour ce didacticiel, nous allons configurer la base de données MySQL que vous avez configurée et remplie avec des exemples de données. Pour plus d’informations sur les autres sources de données prises en charge et sur leur configuration, reportez-vous à la section [Intégration de données AEM Forms](../../forms/using/data-integration.md).

Pour configurer votre base de données [!DNL MySQL], procédez comme suit :

1. Installez le pilote JDBC pour la base de données [!DNL MySQL] en tant que bundle OSGi :

   1. Connectez-vous à l’instance d’auteur AEM [!DNL Forms] en tant qu’administrateur et accédez aux bundles de la console web d’AEM. L’URL par défaut est [https://localhost:4502/system/console/bundles](https://localhost:4502/system/console/bundles).

   1. Cliquez sur **[!UICONTROL Installer/Mettre à jour]**. Une boîte de dialogue [!UICONTROL Télécharger/installer les bundles] s’affiche.

   1. Appuyez sur **[!UICONTROL Choisir un fichier]** pour rechercher et sélectionner le bundle OSGi du pilote JDBC [!DNL MySQL] Sélectionnez les cases à cocher **[!UICONTROL Démarrer le bundle]** et **[!UICONTROL Actualiser les packages]** et cliquez sur **[!UICONTROL Installer ou mettre à jour]**. Assurez-vous que le pilote JDBC [!DNL Oracle Corporation's] pour [!DNL MySQL] est actif. Le pilote est installé.

1. Configurez la base de données [!DNL MySQL] comme source de données :

   1. Accédez à la console web d’AEM à l’adresse [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr).
   1. Recherchez la configuration **Apache Sling Connection Pooled DataSource**. Appuyez pour ouvrir la configuration en mode édition.
   1. Dans la boîte de dialogue de configuration, indiquez ce qui suit :

      * **Nom de la source de données :** vous pouvez spécifier un nom. Spécifiez par exemple **WeRetailMySQL**.
      * **Nom de la propriété de service de source de données** : spécifiez le nom de la propriété de service contenant le nom de la source de données. Il est spécifié lors de l’enregistrement de l’instance de source de données en tant que service OSGi. Par exemple, **datasource.name**.
      * **Classe de pilote JDBC** : spécifiez le nom de la classe Java du pilote JDBC. Pour la base de données [!DNL MySQL], spécifiez **com.mysql.jdbc.Driver**.
      * **URI de connexion JDBC** : spécifiez l’URL de connexion de la base de données. Pour la base de données [!DNL MySQL] s’exécutant sur le port 3306 et le schéma weretail, l’URL est : `jdbc:mysql://'server':3306/weretail?autoReconnect=true&useUnicode=true&characterEncoding=utf-8`.
      * **Nom d’utilisateur :** nom d’utilisateur de la base de données. Il est nécessaire d’activer le pilote JDBC pour établir une connexion avec la base de données.
      * **Mot de passe :** mot de passe de la base de données. Il est nécessaire d’activer le pilote JDBC pour établir une connexion avec la base de données.
      * **Test lors de l’emprunt :** activez l’option **[!UICONTROL Test lors de l’emprunt.]**
      * **Test lors du renvoi :** activez l’option **[!UICONTROL Test lors du renvoi.]**
      * **Requête de validation :** spécifiez une requête SQL SELECT pour valider les connexions du pool. La requête doit renvoyer au moins une ligne. Par exemple, **sélectionnez * depuis customerdetails**.
      * **Isolation de transaction** : définissez la valeur sur **READ_COMMITTED**.

         Laissez les [valeurs](https://tomcat.apache.org/tomcat-7.0-doc/jdbc-pool.html) par défaut des autres propriétés et cliquez sur **[!UICONTROL Enregistrer]**.

         Une configuration similaire à la suivante est créée.

         ![relational-database-data-source-configuration](assets/relational-database-data-source-configuration.png)

## Étape 2 : Créer un modèle de données de formulaire {#create-fdm}

AEM [!DNL Forms] fournit une interface utilisateur intuitive pour [créer un modèle de données de formulaire](data-integration.md) à partir des sources de données configurées. Vous pouvez utiliser plusieurs sources de données dans un modèle de données de formulaire. Dans notre cas d’utilisation, nous utiliserons la source de données [!DNL MySQL] configurée.

Procédez comme suit pour créer un modèle de données de formulaire :

1. Dans l’instance d’auteur AEM, accédez à **[!UICONTROL Forms]** (Formulaires) > **[!UICONTROL Data Integrations]** (Intégrations de données).
1. Appuyez sur **[!UICONTROL Create]** (Créer) > **[!UICONTROL Form Data Model]** (Modèle de données de formulaire).
1. Dans la boîte de dialogue Créer un modèle de données de formulaire, spécifiez un **nom** pour le modèle de données de formulaire. Par exemple, **customer-shipping-billing-details**. Appuyez sur **[!UICONTROL Suivant]**.
1. L’écran Sélectionner la source de données répertorie toutes les sources de données configurées. Sélectionnez la source de données **WeRetailMySQL** et cliquez sur **[!UICONTROL Créer]**.

   ![data-source-selection](assets/data-source-selection.png)

Le modèle de données de formulaire **customer-shipping-billing-details** est créé.

## Étape 3 : configurer un modèle de données de formulaire {#config-fdm}

La configuration d’un modèle de données de formulaire comprend :

* L’ajout d’objets et de services de modèle de données
* La configuration des services de lecture et d’écriture pour les objets de modèle de données

Procédez comme suit pour configurer le modèle de données de formulaire :

1. Dans l’instance d’auteur AEM, accédez à **[!UICONTROL Formulaires]** > **[!UICONTROL Intégrations de données]**. L’URL par défaut est [https://localhost:4502/aem/forms.html/content/dam/formsanddocuments-fdm](https://localhost:4502/aem/forms.html/content/dam/formsanddocuments-fdm).
1. Le modèle de données de formulaire **customer-shipping-billing-details** que vous avez créé précédemment est répertorié ici. Ouvrez-le en mode d’édition.

   La source de données sélectionnée **WeRetailMySQL** est configurée dans le modèle de données de formulaire.

   ![default-fdm](assets/default-fdm.png)

1. Développez l’arborescence de la source de données WeRailMySQL. Sélectionnez les objets et services de modèle de données suivants dans le schéma **weretail** > **customerdetails** du modèle de données de formulaire :

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
   >Les services par défaut d’obtention, de mise à jour et d’insertion des sources de données JDBC sont intégrés au modèle de données de formulaire.

1. Configurez les services de lecture et d’écriture pour les objets de modèle de données.

   1. Sélectionnez l’objet de modèle de données **customerdetails** et appuyez sur **[!UICONTROL Modifier les propriétés]**.
   1. Sélectionnez **[!UICONTROL get]** dans la liste déroulante Service de lecture. L’argument **id** qui est la clé principale de l’objet de modèle de données customerdetails est ajouté automatiquement. Cliquez sur ![aem_6_3_edit](assets/aem_6_3_edit.png) et configurez l’argument comme suit.

      ![read-default](assets/read-default.png)

   1. De même, sélectionnez **[!UICONTROL update]** en tant que Service d’écriture. L’objet **customerdetails** est ajouté automatiquement en tant qu’argument. L’argument est configuré comme suit.

      ![write-default](assets/write-default.png)

      Ajoutez et configurez l’argument **id** comme suit.

      ![id-arg](assets/id-arg.png)

   1. Appuyez sur **[!UICONTROL Terminé]** pour enregistrer les propriétés de l’objet de modèle de données. Cliquez ensuite sur **[!UICONTROL Enregistrer]** pour enregistrer le modèle de données de formulaire.

      Les services **[!UICONTROL get]** et **[!UICONTROL update]** sont ajoutés en tant que services par défaut pour l’objet de modèle de données.

      ![data-model-object](assets/data-model-object.png)

1. Accédez à l’onglet **[!UICONTROL Services]** et configurez les services **[!UICONTROL get]** et **[!UICONTROL update]**.

   1. Sélectionnez le service **[!UICONTROL get]** et cliquez sur **[!UICONTROL Modifier les propriétés]**. La boîte de dialogue Propriétés s’ouvre.
   1. Spécifiez les éléments suivants dans la boîte de dialogue Modifier les propriétés :

      * **Titre** : spécifiez le titre du service. Par exemple : extraire l’adresse d’expédition.
      * **Description** : spécifiez la description contenant le fonctionnement détaillé du service. Par exemple :

         Ce service récupère l’adresse de livraison et les autres détails du client dans la base de données [!DNL MySQL].

      * **Objet de modèle de sortie** : sélectionnez le schéma contenant les données du client. Par exemple :

         schéma customerdetail

      * **Revenir au tableau** : désactivez l’option **Revenir au tableau**.
      * **Arguments** : sélectionnez l’argument nommé **ID**.

      Appuyez sur **[!UICONTROL Terminé]**. Le service de récupération des détails des clients de la base de données MySQL est configuré.

      ![shiiping-address-retrieval](assets/shiiping-address-retrieval.png)

   1. Sélectionnez le service **[!UICONTROL update]** et cliquez sur **[!UICONTROL Modifier les propriétés]**. La boîte de dialogue Propriétés s’ouvre.

   1. Spécifiez les éléments suivants dans la boîte de dialogue [!UICONTROL Modifier les propriétés] :

      * **Titre** : spécifiez le titre du service. Par exemple, Mettre à jour l’adresse de livraison.
      * **Description** : spécifiez la description contenant le fonctionnement détaillé du service. Par exemple :

         Ce service met à jour l’adresse de livraison et les champs associés dans la base de données MySQL.

      * **Objet de modèle d’entrée** : sélectionnez le schéma contenant les données du client. Par exemple :

         schéma customerdetail

      * **Type de sortie** : sélectionnez **VALEUR BOOLEENNE**.

      * **Arguments** : sélectionnez l’argument nommé **ID** et **customerdetails**.
      Appuyez sur **[!UICONTROL Terminé]**. Le service **[!UICONTROL update]** permettant de mettre à jour les détails du client dans la base de données est configuré.[!DNL MySQL]

      ![shiiping-address-update](assets/shiiping-address-update.png)



L’objet et les services de modèle de données dans le modèle de données de formulaire sont configurés. Vous pouvez à présent tester le modèle de données de formulaire.

## Étape 4 : tester le modèle de données de formulaire {#test-fdm}

Vous pouvez tester les objets et services de modèle de données pour vérifier si le modèle de données de formulaire est correctement configuré.

Procédez comme suit pour effectuer le test :

1. Accédez à l’onglet **[!UICONTROL Modèle]**, sélectionnez l’objet de modèle de données **customerdetails** et appuyez sur **[!UICONTROL Tester l’objet de modèle]**.
1. Dans la fenêtre [!UICONTROL Tester le modèle/service], sélectionnez **[!UICONTROL Objet de modèle de lecture]** dans le menu déroulant **[!UICONTROL Sélectionner le modèle/service]**.
1. Dans la section **customerdetails**, spécifiez une valeur pour l’argument **id** qui existe dans la [!DNL MySQL] base de données configurée et appuyez sur **[!UICONTROL Test]**.

   Les détails du client associés à l’ID spécifié sont récupérés et affichés dans la section **[!UICONTROL Sortie]**, comme indiqué ci-dessous.

   ![test-read-model](assets/test-read-model.png)

1. De même, vous pouvez tester l’objet de modèle et les services Écriture.

   Dans l’exemple suivant, le service update met à jour les informations relatives à l’adresse de l’ID 7102715 dans la base de données.

   ![test-write-model](assets/test-write-model.png)

   À présent, si vous testez à nouveau le service de lecture de modèle pour l’ID 7107215, il récupérera et affichera les détails du client mis à jour comme indiqué ci-dessous.

   ![read-updated](assets/read-updated.png)
