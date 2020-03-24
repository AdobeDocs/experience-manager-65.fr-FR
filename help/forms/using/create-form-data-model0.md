---
title: '"Didacticiel : créer un modèle de données de formulaire"'
seo-title: Créer un modèle de données de formulaire pour la communication interactive
description: Créer un modèle de données de formulaire pour la communication interactive
seo-description: Créer un modèle de données de formulaire pour la communication interactive
uuid: b56d3dac-be54-4812-b958-38a085686218
contentOwner: anujkapo
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: e5413fb3-9d50-4f4f-9db8-7e53cd5145d5
docset: aem65
translation-type: tm+mt
source-git-commit: 1449ce9aba3014b13421b32db70c15ef09967375

---


# Didacticiel : créer un modèle de données de formulaire{#tutorial-create-form-data-model}

![04-create-form-data-model-main](assets/04-create-form-data-model-main.png)

This tutorial is a step in the [Create your first Interactive Communication](/help/forms/using/create-your-first-interactive-communication.md) series. Il est recommandé de suivre la série dans l’ordre chronologique pour comprendre, exécuter et démontrer le cas d’utilisation complet du didacticiel.

## À propos du didacticiel {#about-the-tutorial}

Le module d’intégration des données AEM Forms vous permet de créer un modèle de données de formulaire à partir de sources de données principales disparates, telles que les  d’utilisateurs AEM, les services Web RESTful, les services Web SOAP, les services OData et les bases de données relationnelles. Vous pouvez configurer des objets et des services de modèle de données dans un modèle de données de formulaire et les associer à un formulaire adaptatif. Les champs de formulaire adaptatif sont liés aux propriétés de l’objet du modèle de données. Les services vous permettent de préremplir le formulaire adaptatif et d’écrire les données de formulaire soumises dans l’objet de modèle de données.

Pour plus d’informations sur l’intégration des données de formulaire et sur le modèle de données du formulaire, voir [Intégration de données AEM Forms](https://helpx.adobe.com/experience-manager/6-3/forms/using/data-integration.html).

Ce didacticiel vous décrit étape par étape le processus de préparation, création, configuration et association d’un modèle de données de formulaire avec une communication interactive. À la fin de ce didacticiel, vous serez capable de :

* [Configurer la base de données](../../forms/using/create-form-data-model0.md#step-set-up-the-database)
* [Configurer la base de données MySQL comme source de données](../../forms/using/create-form-data-model0.md#step-configure-mysql-database-as-data-source)
* [Créer un modèle de données de formulaire](../../forms/using/create-form-data-model0.md#step-create-form-data-model)
* [Configurer un modèle de données de formulaire](../../forms/using/create-form-data-model0.md#step-configure-form-data-model)
* [Tester le modèle de données de formulaire](../../forms/using/create-form-data-model0.md#step-test-form-data-model-and-services)

Le modèle de données de formulaire se présente comme ceci :

![Modèle de données de formulaire](assets/form_data_model_callouts_new.png)

**A.** Sources de données configurées **B.** de source de données  **C.** Services disponibles **D.** Objets de modèle de données **E.** Services configurés

## Conditions préalables {#prerequisites}

Avant de commencer, vérifiez que vous disposez des éléments suivants :

* Base de données MySQL avec des exemples de données comme indiqué dans la section [Configurer la base de données](../../forms/using/create-form-data-model0.md#step-set-up-the-database).
* OSGi bundle for MySQL JDBC driver as explained in [Bundling the JDBC Database Driver](https://helpx.adobe.com/experience-manager/6-3/help/sites-developing/jdbc.html#bundling-the-jdbc-database-driver)

## Étape 1 : Configurer la base de données {#step-set-up-the-database}

Une base de données est essentielle pour créer une communication interactive. Ce didacticiel utilise une base de données pour afficher le modèle de données de formulaire et les fonctionnalités de persistance des communications interactives. Configurez une base de données comprenant les tableaux des clients, des factures et des appels.
 L’image suivante présente des exemples de données pour le tableau des clients :

![sample_data_cust](assets/sample_data_cust.png)

Utilisez l’instruction DDL suivante pour créer la table **du client** dans la base de données.

```sql
CREATE TABLE `customer` (
   `mobilenum` int(11) NOT NULL,
   `name` varchar(45) NOT NULL,
   `address` varchar(45) NOT NULL,
   `alternatemobilenumber` int(11) DEFAULT NULL,
   `relationshipnumber` int(11) DEFAULT NULL,
   `customerplan` varchar(45) DEFAULT NULL,
   PRIMARY KEY (`mobilenum`),
   UNIQUE KEY `mobilenum_UNIQUE` (`mobilenum`)
 ) ENGINE=InnoDB DEFAULT CHARSET=utf8
```

Utilisez l’instruction DDL suivante pour créer la table des **factures** dans la base de données.

```sql
CREATE TABLE `bills` (
   `billplan` varchar(45) NOT NULL,
   `latepayment` decimal(4,2) NOT NULL,
   `monthlycharges` decimal(4,2) NOT NULL,
   `billdate` date NOT NULL,
   `billperiod` varchar(45) NOT NULL,
   `prevbal` decimal(4,2) NOT NULL,
   `callcharges` decimal(4,2) NOT NULL,
   `confcallcharges` decimal(4,2) NOT NULL,
   `smscharges` decimal(4,2) NOT NULL,
   `internetcharges` decimal(4,2) NOT NULL,
   `roamingnational` decimal(4,2) NOT NULL,
   `roamingintnl` decimal(4,2) NOT NULL,
   `vas` decimal(4,2) NOT NULL,
   `discounts` decimal(4,2) NOT NULL,
   `tax` decimal(4,2) NOT NULL,
   PRIMARY KEY (`billplan`)
 ) ENGINE=InnoDB DEFAULT CHARSET=utf8
```

Utilisez l’instruction DDL suivante pour créer la table des **appels** dans la base de données.

```sql
CREATE TABLE `calls` (
   `mobilenum` int(11) DEFAULT NULL,
   `calldate` date DEFAULT NULL,
   `calltime` varchar(45) DEFAULT NULL,
   `callnumber` int(11) DEFAULT NULL,
   `callduration` varchar(45) DEFAULT NULL,
   `callcharges` decimal(4,2) DEFAULT NULL,
   `calltype` varchar(45) DEFAULT NULL
 ) ENGINE=InnoDB DEFAULT CHARSET=utf8
```

The **calls** table includes the call details such as call date, call time, call number, call duration, and call charges. The **customer** table is linked to the calls table using the Mobile Number (mobilenum) field. For each mobile number listed in the **customer** table, there are multiple records in the **calls** table. Par exemple, vous pouvez récupérer les informations sur l’appel pour le numéro de téléphone mobile **1457892541** en vous reportant au tableau des appels.****

The **bills** table includes the bill details such as bill date, bill period, monthly charges, and call charges. The **customer** table is linked to the **bills** table using the Bill Plan field. There is a plan associated to each customer in the **customer** table. The **bills** table includes the pricing details for all the existing plans. Par exemple, vous pouvez extraire les informations de plan de **Sarah** à partir du tableau des clients et utiliser ces informations pour extraire les informations de tarification à partir du tableau des factures.********

## Étape 2 : Configurer la base de données MySQL comme source de données {#step-configure-mysql-database-as-data-source}

Vous pouvez configurer différents types de sources de données pour créer un modèle de données de formulaire. Pour ce didacticiel, vous allez configurer la base de données MySQL qui est configurée et remplie avec des exemples de données. Pour plus d’informations sur les autres sources de données prises en charge et sur leur configuration, reportez-vous à la section [Intégration de données AEM Forms](https://helpx.adobe.com/experience-manager/6-3/forms/using/data-integration.html).

Procédez comme suit pour configurer votre base de données MySQL :

1. Installez le pilote JDBC pour la base de données MySQL en tant que lot OSGi :

   1. Connectez-vous à l’instance d’auteur AEM Forms en tant qu’administrateur et accédez aux bundles de la console web d’AEM. The default URL is [https://localhost:4502/system/console/bundles](https://localhost:4502/system/console/bundles).
   1. Tap **Install/Update**. Une boîte de dialogue **Télécharger/installer les bundles** s’affiche.

   1. Appuyez sur **Choisir un fichier** pour rechercher et sélectionner le bundle OSGi du pilote JDBC MySQL. Select **Start Bundle** and **Refresh Packages**, and tap **Install** or **Update**. Assurez-vous que le pilote JDBC d’Oracle Corporation pour MySQL est actif. Le pilote est installé.

1. Configurer la base de données MySQL comme source de données :

   1. Go to AEM web console at [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr).
   1. Recherchez la configuration **Apache Sling Connection Pooled DataSource**. Appuyez pour ouvrir la configuration en mode édition.
   1. Dans la boîte de dialogue de configuration, indiquez ce qui suit :

      * **Nom de la source de données :** vous pouvez spécifier un nom. For example, specify **MySQL**.

      * **Nom de la propriété de service de source de données** : spécifiez le nom de la propriété de service contenant le nom de la source de données. Il est spécifié lors de l’enregistrement de l’instance de source de données en tant que service OSGi. Par exemple, **datasource.name**.

      * **Classe de pilote JDBC** : spécifiez le nom de la classe Java du pilote JDBC. Pour la base de données MySQL, spécifiez **com.mysql.jdbc.Driver**.

      * **URI de connexion JDBC** : spécifiez l’URL de connexion de la base de données. Pour la base de données MySQL s’exécutant sur le port 3306 et  teleca, l’URL est : `jdbc:mysql://[server]:3306/teleca?autoReconnect=true&useUnicode=true&characterEncoding=utf-8`
      * **Nom d’utilisateur :** nom d’utilisateur de la base de données. Il est nécessaire d’activer le pilote JDBC pour établir une connexion avec la base de données.
      * **Mot de passe :** mot de passe de la base de données. Il est nécessaire d’activer le pilote JDBC pour établir une connexion avec la base de données.
      * **Test lors de l’emprunt :** activez l’option **Test lors de l’emprunt.**

      * **Test lors du renvoi :** activez l’option **Test lors du renvoi.**

      * **Requête de validation :** spécifiez une requête SQL SELECT pour valider les connexions du pool. La requête doit renvoyer au moins une ligne. For example, **select * from customer**.

      * **Isolation de transaction** : définissez la valeur sur **READ_COMMITTED**.
   Leave other properties with default [values](https://tomcat.apache.org/tomcat-7.0-doc/jdbc-pool.html) and tap **Save**.

   Une configuration similaire à la suivante est créée.

   ![Configuration Apache](assets/apache_configuration_new.png)

## Étape 3 : Créer un modèle de données de formulaire {#step-create-form-data-model}

AEM Forms provide an intuitive user interface to [create a form data mode](https://helpx.adobe.com/experience-manager/6-3/forms/using/data-integration.html#main-pars_header_1524967585)l from configured data sources. Vous pouvez utiliser plusieurs sources de données dans un modèle de données de formulaire. Pour le cas d’utilisation de ce didacticiel, vous utiliserez MySQL comme source de données.

Procédez comme suit pour créer un modèle de données de formulaire :

1. In AEM author instance, navigate to **Forms** > **Data Integrations**.
1. Tap **Create** > **Form Data Model**.
1. In the Create Form Data Model wizard, specify a **name** for the form data model. For example, **FDM_Create_First_IC**. Appuyez sur **Suivant**.
1. L’écran Sélectionner la source de données répertorie toutes les sources de données configurées. Select **MySQL** data source and tap **Create**.

   ![Source de données MYSQL](assets/fdm_mysql_data_source_new.png)

1. Cliquez sur **Terminé**. The **FDM_Create_First_IC** form data model is created.

## Étape 4 : Configurer un modèle de données de formulaire {#step-configure-form-data-model}

La configuration d’un modèle de données de formulaire inclut :

* [l’ajout d’objets et de services de modèle de données](#add-data-model-objects-and-services)
* [la création de propriétés enfants calculées pour un objet de modèle de données](#create-computed-child-properties-for-data-model-object)
* [l’ajout d’associations entre les objets de modèle de données](#add-associations-between-data-model-objects)
* [la modification des propriétés d’objet du modèle de données](#edit-data-model-object-properties)
* [la configuration des services pour les objets de modèle de données](#configure-services)

### Ajouter des objets et des services de modèle de données {#add-data-model-objects-and-services}

1. On AEM author instance, navigate to **Forms** > **Data Integrations**. The default URL is [https://localhost:4502/aem/forms.html/content/dam/formsanddocuments-fdm](https://localhost:4502/aem/forms.html/content/dam/formsanddocuments-fdm).
1. The **FDM_Create_First_IC** form data model you created earlier is listed here. Sélectionnez-le, puis appuyez sur **Modifier**.

   The selected data source **MySQL** is displayed in the **Data Sources** pane.

   ![Source de données MYSQL pour FDM](assets/mysql_fdm_new.png)

1. Développez l’arborescence de la source de données **MySQL**. Select the following data model objects and services from **teleca** schema:

   * **Objets de modèle de données**:

      * bills
      * calls
      * customer
   * **Services :**

      * get
      * mise à jour
   Appuyez sur **Ajouter la sélection** pour ajouter des objets et des services de modèle de données sélectionnés au modèle de données de formulaire.

   ![Sélectionner des services d’objets de modèle de données](assets/select_data_model_object_services_new.png)

   Les factures, les appels et les objets du modèle de données client sont affichés dans le volet de droite de l’onglet **Modèle**. Les services get et update sont affichés dans l’onglet **Services**.

   ![Objets de modèle de données](assets/data_model_objects_new.png)

### Créer des propriétés enfants calculées pour un objet de modèle de données {#create-computed-child-properties-for-data-model-object}

Une propriété calculée est celle dont la valeur est calculée sur la base d’une règle ou d’une expression. À l’aide d’une règle, vous pouvez définir la valeur d’une propriété calculée sur une chaîne littérale, un nombre, le résultat d’une expression mathématique ou la valeur d’une autre propriété dans le modèle de données de formulaire.

En fonction du cas d’utilisation, créez la propriété enfant calculée **usagecharges** dans l’objet de modèle de données **bills** à l’aide de l’expression mathématique suivante :

* usage charges = call charges + conference call charges + SMS charges + mobile internet charges + roaming national + roaming international + VAS (all these properties exist in the bills data model object)
For more information on the **usagecharges** child computed property, see [Plan the Interactive Communication](/help/forms/using/planning-interactive-communications.md).

Exécutez les étapes suivantes pour créer des propriétés enfant calculées pour un objet de modèle de données bills :

1. Select the check box at the top of the **bills** data model object to select it and tap **Create Child Property**.
1. Dans le panneau **Créer une propriété enfant** :

   1. Saisissez **usagecharges** comme nom de propriété enfant.
   1. Activez **Calculé**.
   1. Select **Float** as the type and tap **Done** to add the child property to the **bills** data model object.
   ![Créer une propriété enfant](assets/create_child_property_new.png)

1. Tap **Edit Rule** to open the Rule Editor.
1. Appuyez sur **Créer**. The **Set Value** rule window opens.
1. Dans la liste déroulante Sélectionner une option, sélectionnez **Expression mathématique**.

   ![Éditeur de règles sur les frais d&#39;utilisation](assets/usage_charges_rule_editor_new.png)

1. In the mathematical expression, select **callcharges** and **confcallcharges** as first and second objects, respectively. Sélectionnez **plus** en tant qu’opérateur. Appuyez sur l’expression mathématique puis sur **Etendre l’expression** pour ajouter les objets **smscharges**, **internetcharges**, **roamingnational**, **roamingintnl** et **vas** à l’expression.

   L’image suivante décrit l’expression mathématique dans l’éditeur de règles :

   ![Règle des frais d’utilisation](assets/usage_charges_rule_all_new.png)

1. Appuyez sur **Terminé**. La règle est créée dans l’éditeur de règles.
1. Tap **Close** to close the Rule Editor window.

### Ajouter des associations entre les objets de modèle de données {#add-associations-between-data-model-objects}

Une fois les objets de modèle de données définis, vous pouvez créer des associations entre eux. L’association peut lier un objet à un autre ou à plusieurs objets. Par exemple, plusieurs personnes à charge peuvent être associées à un employé. Il s’agit d’une association d’un objet à plusieurs objets, désignée par 1:n sur la ligne reliant les objets de modèle de données associés. Toutefois, si une association renvoie un nom d’employé unique pour un ID d’employé donné, elle est appelée association un-à-un.

Lorsque vous ajoutez des objets de modèle de données associés dans une source de données à un modèle de données de formulaire, leurs associations sont conservées et affichées sous forme de lignes de flèche.

En fonction du cas d’utilisation, créez les associations suivantes entre les objets de modèle de données :

| Association | Objets de modèle de données |
|---|---|
| 1:n | client:appels (plusieurs appels peuvent être associés à un client dans une facture mensuelle) |
| 1:1 | client:factures (une facture est associée à un client pour un mois donné) |

Procédez comme suit pour créer des associations entre objets de modèle de données :

1. Select the check box at the top of the **customer** data model object to select it and tap **Add Association**. The **Add Association** property pane opens.
1. Dans le panneau **Ajouter une association** :

   * Spécifiez un titre pour l’association. Ce champ est facultatif.
   * Sélectionnez **Un à plusieurs** dans la liste déroulante **Type**.

   * Sélectionnez **calls** dans la liste déroulante **Objet de modèle**.

   * Sélectionnez **get** dans la liste déroulante **Service**.

   * Tap **Add** to link the **customer** data model object to **calls** data model object using a property. En fonction du cas d’utilisation, l’objet de modèle de données calls doit être lié à la propriété de numéro de mobile dans l’objet de modèle de données customer. The **Add Argument** dialog box opens.
   ![Association Ajouter](assets/add_association_new.png)

1. Dans la boîte de dialogue **Ajouter un argument** :

   * Sélectionnez **mobilenum** dans la liste déroulante **Nom**. La propriété Numéro mobile est une propriété commune disponible dans les objets de modèle de données customer et calls. Par conséquent, elle est utilisée pour créer une association entre les objets de modèle de données customer et calls.
Plusieurs enregistrements d’appels sont disponibles dans le tableau des appels pour chaque numéro de téléphone disponible dans l’objet de modèle customer.

   * Spécifiez un titre et une description facultatifs pour l’argument.
   * Sélectionnez **customer** dans la liste déroulante **Liaison à**.

   * Sélectionnez **mobilenum** dans la liste déroulante **Valeur de liaison**.

   * Appuyez sur **Ajouter**.
   ![Ajouter association pour un argument](assets/add_association_argument_new.png)

   La propriété mobilenum s’affiche dans la section **Arguments**.

   ![Association d&#39;arguments Ajouter](assets/add_argument_association_new.png)

1. Tap **Done** to create a 1:n association between customer and calls data model objects.

   Une fois que vous avez créé une association entre les objets de modèle de données customer et calls, créez une association 1:1 entre les objets de modèle de données customer et bills.

1. Select the check box at the top of the **customer** data model object to select it and tap **Add Association**. The **Add Association** property pane opens.
1. Dans le panneau **Ajouter une association** :

   * Spécifiez un titre pour l’association. Ce champ est facultatif.
   * Select **One to One** from the **Type** drop-down list.

   * Select **bills** from the **Model Object** drop-down list.

   * Sélectionnez **get** dans la liste déroulante **Service.** The **billplan** property, which is the primary key for the bills table, is already available in the **Arguments** section.
 Les objets de modèle de données bills et customer sont respectivement liés à l’aide des propriétés billplan (factures) et customerplan (client). Créez une liaison entre ces propriétés pour récupérer les détails du plan pour tout client disponible dans la base de données MySQL.

   * Sélectionnez **customer** dans la liste déroulante **Liaison à**.

   * Sélectionnez **customerplan** dans la liste déroulante **Valeur de liaison**.

   * Tap **Done** to create a binding between the billplan and customerplan properties.
   ![Association Ajouter pour la facture client](assets/add_association_customer_bills_new.png)

   L’image suivante décrit les associations entre les objets de modèle de données et les propriétés utilisées pour créer des associations entre eux :

   ![fdm_associations](assets/fdm_associations.gif)

### Modifier les propriétés de l’objet de modèle de données {#edit-data-model-object-properties}

Après avoir créé des associations entre l’objet customer et d’autres objets de modèle de données, modifiez les propriétés du client pour définir la propriété en fonction de laquelle les données sont extraites de l’objet de modèle de données. En fonction du cas d’utilisation, le numéro de mobile est utilisé comme propriété pour extraire des données de l’objet de modèle de données customer.

1. Select the check box at the top of the **customer** data model object to select it and tap **Edit Properties**. Le panneau **Modifier les propriétés** s’ouvre.
1. Spécifiez **customer** comme **objet de modèle de niveau supérieur**.
1. Sélectionnez **get** dans la liste déroulante **Service de lecture**.
1. Dans la section **Arguments** :

   * Sélectionnez **Attribut de requête** dans la liste déroulante **Liaison à**.

   * Spécifiez **mobilenum** comme valeur de liaison.

1. Sélectionnez **update** dans la liste déroulante **Service d’écriture**.
1. Dans la section **Arguments** :

   * Pour la propriété **mobilenum**, sélectionnez **customer** dans la liste déroulante **Liaison à**.

   * Sélectionnez **mobilenum** dans la liste déroulante **Valeur de liaison**.

1. Tap **Done** to save the properties.

   ![Configuration de Services](assets/configure_services_customer_new.png)

1. Select the check box at the top of the **calls** data model object to select it and tap **Edit Properties**. Le panneau **Modifier les propriétés** s’ouvre.
1. Désactiver l’**Objet de niveau supérieur** pour l’objet de modèle de données **calls**.
1. Appuyez sur **Terminé**.

   Répétez les étapes 8 à 10 pour configurer les propriétés pour l’objet de modèle de données **bills**.

### Configuration de Services {#configure-services}

1. Accédez à l’onglet **Services**.
1. Select the **get** service and tap **Edit Properties**. Le panneau **Modifier les propriétés** s’ouvre.
1. Dans le panneau **Modifier les propriétés** :

   * Saisissez un titre et une description facultatifs.
   * Sélectionnez **customer** depuis la liste déroulante **Objet de modèle de sortie**.

   * Tap **Done** to save the properties.
   ![Modification des propriétés](assets/edit_properties_get_details_new.png)

1. Select the **update** service and tap **Edit Properties**. Le panneau **Modifier les propriétés** s’ouvre.
1. Dans le panneau **Modifier les propriétés** :

   * Saisissez un titre et une description facultatifs.
   * Select **customer** from the **Input Model Object** drop-down list.

   * Appuyez sur **Terminé**.
   * Appuyez sur **Enregistrer** pour enregistrer le modèle de données de formulaire.
   ![Mettre à jour les propriétés du service](assets/update_service_properties_new.png)

## Étape 5 : Tester le modèle de données de formulaire et les services {#step-test-form-data-model-and-services}

Vous pouvez tester l’objet et les services du modèle de données pour vérifier que le modèle de données de formulaire est correctement configuré.

Procédez comme suit pour effectuer le test :

1. Go to the **Model** tab, select the **customer** data model object, and tap **Test Model Object**.
1. In the **Test Form Data Model** window, select **Read model object** from the **Select Model/Service** drop-down list.
1. In the **Input** section, specify a value for the **mobilenum** property that exists in the configured MySQL database and tap **Test**.

   Les détails du client associés à la propriété mobilenum spécifiée sont récupérés et affichés dans la section Output, comme illustré ci-dessous. Fermez la boîte de dialogue.

   ![Test du modèle de données](assets/test_data_model_new.png)

1. Accédez à l’onglet **Services**.
1. Select the **get** service and tap **Test Service.**
1. In the **Input** section, specify a value for the **mobilenum** property that exists in the configured MySQL database and tap **Test**.

   Les détails du client associés à la propriété mobilenum spécifiée sont récupérés et affichés dans la section Output, comme illustré ci-dessous. Fermez la boîte de dialogue.

   ![Service de test](assets/test_service_new.png)

### Modifier et enregistrer des exemples de données {#edit-and-save-sample-data}

L’éditeur de modèle de données de formulaire vous permet de générer des exemples de données pour toutes les propriétés d’objet de modèle de données, y compris les propriétés calculées, dans un modèle de données de formulaire. Il s’agit d’un ensemble de valeurs aléatoires conformes au type de données configuré pour chaque propriété. Vous pouvez également modifier et enregistrer des données qui sont conservées même si vous régénérez les exemples de données.

Procédez comme suit pour générer, modifier et enregistrer des exemples de données :

1. On the form data model page, tap **Edit Sample Data**. Cela génère et affiche les exemples de données dans la fenêtre Modifier les exemples de données.

   ![Modifier les exemples de données](assets/edit_sample_data_new.png)

1. Dans la fenêtre **Modifier les exemples de données**, modifiez les données selon les besoins puis appuyez sur **Enregistrer**. Fermez la fenêtre.


