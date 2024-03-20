---
title: "Didacticiel\_: créer un modèle de données de formulaire "
description: Découvrez comment configurer MySQL comme source de données, créer un modèle de données de formulaire (FDM), le configurer et tester AEM Forms.
contentOwner: khsingh
products: SG_EXPERIENCEMANAGER/6.3/FORMS
docset: aem65
exl-id: 40bc5af6-9023-437e-95b0-f85d3df7d8aa
solution: Experience Manager, Experience Manager Forms
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '1533'
ht-degree: 74%

---

# Didacticiel : créer un modèle de données de formulaire {#tutorial-create-form-data-model}

![04-create-form-data-model-main](assets/04-create-form-data-model-main.png)

Ce tutoriel fait partie de la série [Création de votre premier formulaire adaptatif](../../forms/using/create-your-first-adaptive-form.md). Adobe recommande de suivre la série dans l’ordre chronologique pour comprendre, exécuter et montrer le cas d’utilisation complet du tutoriel.

## À propos du tutoriel {#about-the-tutorial}

Le module d’intégration de données AEM [!DNL Forms] vous permet de créer un modèle de données de formulaire à partir de sources de données principales disparates, telles que le profil utilisateur AEM, les services web RESTful, les services web basés sur SOAP, les services OData et les bases de données relationnelles. Vous pouvez configurer des objets et des services de modèle de données dans un modèle de données de formulaire et les associer à un formulaire adaptatif. Les champs de formulaire adaptatif sont liés aux propriétés de l’objet de modèle de données. Les services vous permettent de préremplir le formulaire adaptatif et d’écrire les données de formulaire soumises dans l’objet de modèle de données.

Pour plus d’informations sur l’intégration des données de formulaire et sur le modèle de données du formulaire, voir [Intégration de données AEM Forms](../../forms/using/data-integration.md).

Ce tutoriel vous décrit étape par étape le processus de préparation, création, configuration et association d’un modèle de données de formulaire avec un formulaire adaptatif. À la fin de ce didacticiel, vous serez capable de :

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

## Étape 1 : Configurer la base de données MySQL en tant que source de données {#config-database}

Vous pouvez configurer différents types de sources de données pour créer un modèle de données de formulaire. Pour ce didacticiel, vous allez configurer la base de données MySQL que vous avez configurée et remplie avec des exemples de données. Pour plus d’informations sur les autres sources de données prises en charge et sur leur configuration, reportez-vous à la section [Intégration de données d’AEM Forms](../../forms/using/data-integration.md).

Pour configurer votre base de données [!DNL MySQL], procédez comme suit :

1. Installez le pilote JDBC pour la base de données [!DNL MySQL] en tant que bundle OSGi :

   1. Téléchargez le [!DNL MySQL]lot OSGi du pilote JDBC à partir de `http://www.java2s.com/ref/jar/download-orgosgiservicejdbc100jar-file.html`. <!-- This URL is an insecure link but using https is not possible -->
   1. Connectez-vous à l’instance d’auteur AEM [!DNL Forms] en tant qu’administrateur et accédez aux bundles de la console web d’AEM. L’URL par défaut est [https://localhost:4502/system/console/bundles](https://localhost:4502/system/console/bundles).

   1. Sélectionner **[!UICONTROL Installer/Mettre à jour]**. Une boîte de dialogue [!UICONTROL Télécharger/installer les bundles] s’affiche.

   1. Sélectionnez **[!UICONTROL Choisir un fichier]** pour parcourir et sélectionnez le [!DNL MySQL] lot OSGi du pilote JDBC. Sélectionnez **[!UICONTROL Démarrer le regroupement]** et **[!UICONTROL actualiser les packages]**, puis sélectionnez **[!UICONTROL Installer ou Mettre à jour]**. Assurez-vous que le pilote JDBC [!DNL Oracle Corporation's] pour [!DNL MySQL] est actif. Le pilote est installé.

1. Configurez la base de données [!DNL MySQL] comme source de données :

   1. Accédez à la console web d’AEM à l’adresse [https://localhost:4502/system/console/configMgr](https://localhost:4502/system/console/configMgr).
   1. Recherchez la configuration **Apache Sling Connection Pooled DataSource**. Sélectionnez cette option pour ouvrir la configuration en mode d’édition.
   1. Dans la boîte de dialogue de configuration, indiquez ce qui suit :

      * **Nom de la source de données :** vous pouvez spécifier n’importe quel nom. Spécifiez par exemple **WeRetailMySQL**.
      * **Nom de la propriété du service de la source de données** : indiquez le nom de la propriété de service contenant le nom de la source de données. Il est spécifié lors de l’enregistrement de l’instance de source de données en tant que service OSGi. Par exemple, **datasource.name**.
      * **Classe de pilote JDBC**: spécifiez le nom de classe Java™ du pilote JDBC. Pour la base de données [!DNL MySQL], spécifiez **com.mysql.jdbc.Driver**.
      * **URI de connexion JDBC** : spécifiez l’URL de connexion de la base de données. Pour [!DNL MySQL] une base de données s’exécutant sur le port 3306 et le schéma `weretail`, l’URL est la suivante : `jdbc:mysql://'server':3306/weretail?autoReconnect=true&useUnicode=true&characterEncoding=utf-8`

      >[!NOTE]
      >
      > Lorsque la base de données [!DNL MySQL] se trouve derrière un pare-feu, alors le nom d’hôte de la base de données n’est pas un DNS public. L’adresse IP de la base de données doit être ajoutée dans le *fichier /etc/hosts* de la machine hôte AEM.

      * **Nom d’utilisateur :** nom d’utilisateur de la base de données. Il est nécessaire d’activer le pilote JDBC pour établir une connexion avec la base de données.
      * **Mot de passe :** mot de passe de la base de données. Il est nécessaire d’activer le pilote JDBC pour établir une connexion avec la base de données.

      >[!NOTE]
      >
      >AEM Forms ne prend pas en charge l’authentification NT pour [!DNL MySQL]. Accédez à AEM console Web à https://localhost:4502/system/console/configMgr [](https://localhost:4502/system/console/configMgr) et recherchez « Source de données mise en pool de connexions Apache Sling ». Pour la propriété « JDBC connection URI », définissez la valeur de « integratedSecurity » sur False et utilisez le nom d’utilisateur et le mot de passe créés pour vous connecter à [!DNL MySQL] la base de données.

      * **Test lors de l’emprunt :** activez l’option **[!UICONTROL Test lors de l’emprunt.]**
      * **Test lors du renvoi :** activez l’option **[!UICONTROL Test lors du renvoi.]**
      * **Requête de validation :** spécifiez une requête SQL SELECT pour valider les connexions du pool. La requête doit renvoyer au moins une ligne. Par exemple, **sélectionnez &#42; depuis customerdetails**.
      * **Isolation de transaction** : définissez la valeur sur **READ_COMMITTED**.

        Conservez les autres propriétés avec les valeurs](https://tomcat.apache.org/tomcat-7.0-doc/jdbc-pool.html) par défaut [et sélectionnez **[!UICONTROL Enregistrer]**.

        Une configuration similaire à la suivante est créée.

        ![relational-database-data-source-configuration](assets/relational-database-data-source-configuration.png)

## Étape 2 : Créer un modèle de données de formulaire {#create-fdm}

AEM [!DNL Forms] fournit une interface utilisateur intuitive pour [créer un modèle de données de formulaire](data-integration.md) à partir des sources de données configurées. Vous pouvez utiliser plusieurs sources de données dans un modèle de données de formulaire. Pour ce cas d’utilisation, vous pouvez utiliser la source de données configurée [!DNL MySQL] .

Procédez comme suit pour créer un modèle de données de formulaire :

1. Dans l’instance d’auteur AEM, accédez à **[!UICONTROL Forms]** (Formulaires) > **[!UICONTROL Data Integrations]** (Intégrations de données).
1. Sélectionnez **[!UICONTROL Créer]** > **[!UICONTROL modèle]** de données de formulaire.
1. Dans la boîte de dialogue Créer un modèle de données de formulaire, spécifiez un **nom** pour le modèle de données de formulaire. Par exemple, **customer-shipping-billing-details**. Sélectionnez **[!UICONTROL Suivant]**.
1. L’écran Sélectionner la source de données répertorie toutes les sources de données configurées. Sélectionner **WeRetailMySQL** source de données et sélectionnez **[!UICONTROL Créer]**.

   ![data-source-selection](assets/data-source-selection.png)

Le modèle de données de formulaire **customer-shipping-billing-details** est créé.

## Étape 3 : Configurer le modèle de données de formulaire {#config-fdm}

La configuration du modèle de données de formulaire implique :

* L’ajout d’objets et de services de modèle de données
* La configuration des services de lecture et d’écriture des objets de modèle de données

Pour configurer un modèle de données de formulaire, procédez comme suit :

1. Dans l’instance d’auteur AEM, accédez à **[!UICONTROL Formulaires]** > **[!UICONTROL Intégrations de données]**. L’URL par défaut est [https://localhost:4502/aem/forms.html/content/dam/formsanddocuments-fdm](https://localhost:4502/aem/forms.html/content/dam/formsanddocuments-fdm).
1. Le modèle de données de formulaire **customer-shipping-billing-details** que vous avez créé précédemment est répertorié ici. Ouvrez-le en mode d’édition.

   La source de données sélectionnée **WeRetailMySQL** est configuré dans le modèle de données de formulaire.

   ![default-fdm](assets/default-fdm.png)

1. Développez l’arborescence de la source de données WeRailMySQL. Sélectionnez les objets et services de modèle de données suivants dans le schéma weretail > customerdetails **afin de pouvoir former un modèle de** données : ****

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

   Sélectionnez **Add Selected** pour ajouter les objets et services de modèle de données sélectionnés au modèle de données de formulaire.

   ![Schéma WeRetail](assets/weretail_schema_new.png)

   >[!NOTE]
   >
   >Les services par défaut d’obtention, de mise à jour et d’insertion des sources de données JDBC sont intégrés au modèle de données de formulaire.

1. Configurez les services de lecture et d’écriture pour le modèle de données de formulaire.

   1. Sélectionnez la variable **customerdetails** objet de modèle de données et sélectionnez **[!UICONTROL Modifier les propriétés]**.
   1. Sélectionnez **[!UICONTROL get]** dans la liste déroulante Service de lecture. L’argument **id** qui est la clé principale de l’objet de modèle de données customerdetails est ajouté automatiquement. Sélectionnez ![aem_6_3_edit](assets/aem_6_3_edit.png) et configurez l’argument comme suit.

      ![read-default](assets/read-default.png)

   1. De même, sélectionnez **[!UICONTROL mettre à jour]** comme service d’écriture. L’objet **customerdetails** est automatiquement ajouté en tant qu’argument. L’argument est configuré comme suit.

      ![write-default](assets/write-default.png)

      Ajoutez et configurez l’argument **id** comme suit.

      ![id-arg](assets/id-arg.png)

   1. Sélectionnez **[!UICONTROL Terminé]** pour enregistrer les propriétés de l’objet de modèle de données. Sélectionnez ensuite **[!UICONTROL Enregistrer]** pour enregistrer le modèle de données de formulaire.

      Les services **[!UICONTROL get]** et **[!UICONTROL update]** sont ajoutés en tant que services par défaut pour l’objet de modèle de données.

      ![data-model-object](assets/data-model-object.png)

1. Accédez à l’onglet **[!UICONTROL Services]** et configurez les services **[!UICONTROL get]** et **[!UICONTROL update]**.

   1. Sélectionnez le **[!UICONTROL service get]** et sélectionnez **[!UICONTROL Edit Properties]**. La boîte de dialogue Propriétés s’ouvre.
   1. Spécifiez les éléments suivants dans la boîte de dialogue Modifier les propriétés :

      * **Titre** : indiquez le titre du service. Par exemple : récupérer l’adresse d’expédition.
      * **Description** : spécifiez la description contenant le fonctionnement détaillé du service. Par exemple :

        Ce service récupère l’adresse de livraison et d’autres détails du client à partir de la [!DNL MySQL] base de données

      * **Objet de modèle de sortie** : sélectionnez le schéma contenant les données du client. Par exemple :

        schéma customerdetail

      * **Tableau de retour** : désactivez l’option **Tableau de retour**.
      * **Arguments** : sélectionnez l’argument nommé **ID**.

      Sélectionnez **[!UICONTROL Terminé]**. Le service de récupération des détails des clients de la base de données MySQL est configuré.

      ![shiiping-address-retrieval](assets/shiiping-address-retrieval.png)

   1. Sélectionnez le service de mise à jour ]**et sélectionnez**[!UICONTROL  Modifier les **[!UICONTROL propriétés]**. La boîte de dialogue Propriétés s’ouvre.

   1. Spécifiez les éléments suivants dans la boîte de dialogue [!UICONTROL Modifier les propriétés] :

      * **Titre** : indiquez le titre du service. Par exemple, Mettre à jour l’adresse d’expédition.
      * **Description** : indiquez la description contenant le fonctionnement détaillé du service. Par exemple :

        Ce service met à jour l’adresse de livraison et les champs associés dans la base de données MySQL.

      * **Objet de modèle d’entrée** : sélectionnez le schéma contenant les données du client. Par exemple :

        schéma customerdetail

      * **Type de sortie** : sélectionnez **VALEUR BOOLEENNE**.

      * **Arguments** : sélectionnez le nom **de l’argument ID** et **les détails** du client.

      Sélectionnez **[!UICONTROL Terminé]**. Le service **[!UICONTROL update]** permettant de mettre à jour les détails du client dans la base de données est configuré.[!DNL MySQL]

      ![shiiping-address-update](assets/shiiping-address-update.png)

L’objet du modèle de données et les services contenus dans le modèle de données de formulaire sont configurés. Vous pouvez maintenant tester le modèle de données de formulaire.

## Étape 4 : Tester le modèle de données de formulaire {#test-fdm}

Vous pouvez tester les objets et services de modèle de données pour vérifier si le modèle de données de formulaire est correctement configuré.

Procédez comme suit pour effectuer le test :

1. Accédez à l’onglet **[!UICONTROL Modèle]**, sélectionnez l’objet de modèle de données customerdetails **, puis sélectionnez**[!UICONTROL  Tester l’objet **]** de modèle.
1. Dans la fenêtre [!UICONTROL Tester le modèle/service], sélectionnez **[!UICONTROL Objet de modèle de lecture]** dans le menu déroulant **[!UICONTROL Sélectionner le modèle/service]**.
1. Dans la **section customerdetails** , spécifiez une valeur pour l’argument **id** qui existe dans la base de données configurée [!DNL MySQL] et sélectionnez **[!UICONTROL Tester]**.

   Les détails du client associés à l’ID spécifié sont récupérés et affichés dans la section **[!UICONTROL Sortie]**, comme indiqué ci-dessous.

   ![test-read-model](assets/test-read-model.png)

1. De même, vous pouvez tester l’objet et les services de modèle en écriture.

   Dans l’exemple suivant, le service Mettre à jour met à jour avec succès les détails de l’adresse de l’ID 7102715 dans la base de données.

   ![test-write-model](assets/test-write-model.png)

   Maintenant, si vous testez à nouveau le service de modèle de lecture pour l’ID 7107215, il récupère et affiche les détails mis à jour du client comme indiqué ci-dessous.

   ![read-updated](assets/read-updated.png)


>[!NOTE]
>
> Vous pouvez créer et utiliser la configuration de liste SharePoint à l’aide du modèle de données de formulaire dans un formulaire adaptatif pour enregistrer des données ou un document d’enregistrement généré dans une liste SharePoint. Reportez-vous à [Connecter un formulaire adaptatif à la liste Microsoft® SharePoint pour](/help/forms/using/configuring-submit-actions.md#create-a-sharepoint-list-configuration) obtenir des instructions détaillées.