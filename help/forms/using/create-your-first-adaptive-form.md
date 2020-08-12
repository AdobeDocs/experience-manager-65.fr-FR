---
title: '"Didacticiel : Créer votre premier formulaire adaptatif"'
seo-title: '"Didacticiel : Créer votre premier formulaire adaptatif"'
description: Apprenez à créer des formulaires professionnels, interactifs et réactifs.
seo-description: Apprenez à créer des formulaires professionnels, interactifs et réactifs.
uuid: ee351a3f-ea6a-4b4c-8045-4948ad51b7c1
topic-tags: introduction
discoiquuid: 1142bcd4-e3a7-41ce-a710-132ae6c21dbe
docset: aem65
translation-type: tm+mt
source-git-commit: 43c04a8b2f1e2e7f2067cec055d8737dfc7b3e84
workflow-type: tm+mt
source-wordcount: '1071'
ht-degree: 73%

---


# Tutorial: Create your first adaptive form {#tutorial-create-your-first-adaptive-form}

![01-create-first-adaptive-form-hero-image](assets/01-create-first-adaptive-form-hero-image.png)

## Présentation {#introduction}

Êtes-vous à la recherche d’une **expérience de création de formulaires** adaptée aux appareils mobiles qui simplifie l’inscription, renforce l’engagement et réduit la durée d’exécution ? Les **formulaires adaptatifs** vous conviendront parfaitement. Les formulaires adaptatifs offrent une expérience de création de formulaires mobile, automatisée et compatible avec Analytics. Vous pouvez facilement créer des formulaires réactifs et interactifs, utiliser des processus automatisés pour réduire les tâches administratives et répétitives et utiliser l’analyse des données pour améliorer et personnaliser l’expérience que les clients ont avec vos formulaires.

Ce didacticiel fournit un cadre de bout en bout pour la création d’un formulaire adaptatif. Il présente un cas d’utilisation et plusieurs guides. Chaque guide vous aide à apprendre et à ajouter de nouvelles fonctionnalités au formulaire adaptatif créé dans le cadre de ce didacticiel. Un formulaire adaptatif de travail est disponible après chaque guide. Le guide de création de formulaire adaptatif est disponible. Les guides suivants seront bientôt disponibles. À la fin de ce didacticiel, vous serez capable de :

* créer un formulaire adaptatif et un modèle de données de formulaire ;
* appliquer un style à votre formulaire adaptatif ;
* utiliser l’éditeur de règles de formulaire adaptatif pour créer des règles métier ;
* tester et publier un formulaire adaptatif.

![create-adaptive-form-workflow](assets/create-daptive-form-workflow.png)

La procédure commence par l’apprentissage du cas d’utilisation :

Un site Web propose une gamme de produits pour des clients divers. Les clients parcourent le portail, sélectionnent et commandent les produits. Chaque client crée un compte et fournit des adresses de livraison et de facturation. Une cliente, Sara Rose, cherche à ajouter son adresse de livraison sur le site Web. Le site Web fournit un formulaire en ligne pour ajouter et mettre à jour les adresses d&#39;expédition.

The website runs on Adobe Experience Manager (AEM) and uses AEM [!DNL Forms] for data capture and processing. Le formulaire d’ajout et de mise à jour d’adresse est un formulaire adaptatif. Le site Web stocke les coordonnées du client dans une base de données. Ils utilisent le formulaire d&#39;ajout d&#39;adresse et de mise à jour pour récupérer et afficher les adresses disponibles. Il utilise également le formulaire adaptatif pour accepter les adresses mises à jour et les nouvelles adresses.

### Condition requise {#prerequisite}

* Configurez une instance d’auteur AEM.
* Installez le [module complémentaire AEM Forms](../../forms/using/installing-configuring-aem-forms-osgi.md) sur une instance de création.
* Obtenez le pilote de base de données JDBC (fichier JAR) auprès du fournisseur de base de données. Examples in the tutorial are based on [!DNL MySQL] database and use [!DNL Oracle's] [MySQL JDBC database driver](https://dev.mysql.com/downloads/connector/j/5.1.html).

* Configurez une base de données contenant les données client avec les champs affichés ci-dessous. Une base de données n’est pas essentielle pour créer un formulaire adaptatif. Ce didacticiel utilise une base de données pour afficher les fonctionnalités de modèle de données de formulaire et de persistance d’AEM [!DNL Forms].

![adaptiveformdata](assets/adaptiveformdata.png)

## Étape 1 : création d’un formulaire adaptatif {#step-create-an-adaptive-form}

![03-create-adaptive-form-main-image_small](assets/03-create-adaptive-form-main-image_small.png)

Les formulaires adaptatifs sont de nouvelle génération, attrayants, réactifs, dynamiques et par nature adaptatifs. En utilisant des formulaires adaptatifs, vous pouvez offrir des expériences personnalisées et ciblées. AEM [!DNL Forms] provide a drag-and-drop WYSIWYG editor to create adaptive forms. Pour plus d’informations sur les formulaires adaptatifs, voir [Présentation de la création de formulaires adaptatifs](../../forms/using/introduction-forms-authoring.md).

Goals:

* Créer un formulaire adaptatif permettant à un client d’ajouter une adresse de livraison
* Mettre en forme les champs d’un formulaire adaptatif pour afficher et accepter les informations d’un client
* Créer une action d’envoi pour envoyer un courrier électronique contenant du contenu de formulaire
* Prévisualiser et envoyer un formulaire adaptatif

[![Consultez le Guide](https://helpx.adobe.com/content/dam/help/en/marketing-cloud/how-to/digital-foundation/_jcr_content/main-pars/image_1250343773/see-the-guide-sm.png)](create-adaptive-form.md)

## Étape 2 : création d’un modèle de données de formulaire {#step-create-form-data-model}

![05-create-form-data-model-main_small](assets/05-create-form-data-model-main_small.png)

Un modèle de données de formulaire permet de connecter un formulaire adaptatif à des sources de données disparates, par exemple, le profil utilisateur AEM, les services Web RESTful, les services Web basés sur SOAP, les services OData et les bases de données relationnelles. Un modèle de données de formulaire est un schéma de représentation de données unifié des entités et services d’entreprise disponibles dans des sources de données connectées. Vous pouvez utiliser le modèle de données de formulaire avec un formulaire adaptatif pour extraire, mettre à jour, supprimer et ajouter des données aux sources de données connectées.

Goals:

* Configure the website&#39;s database instance ([!DNL MySQL] database) as a data sources
* Create the form data model using [!DNL MySQL] database as a data source
* Ajouter des objets de modèle de données pour former un modèle de données
* Configurer les services de lecture et d’écriture pour le modèle de données de formulaire
* Tester le modèle de données de formulaire et les services configurés avec des données de test

[![Consultez le Guide](https://helpx.adobe.com/content/dam/help/en/marketing-cloud/how-to/digital-foundation/_jcr_content/main-pars/image_1250343773/see-the-guide-sm.png)](create-form-data-model.md)

## Étape 3 : application de règles aux champs de formulaires adaptatifs {#step-apply-rules-to-adaptive-form-fields}

![07-apply-rules-to-adaptive-form_small](assets/07-apply-rules-to-adaptive-form_small.png)

Les formulaires adaptatifs fournissent un éditeur pour l’écriture de règles sur des objets de formulaire adaptatifs. Ces règles déterminent les actions à déclencher sur des objets de formulaire en fonction des conditions prédéfinies, des saisies de l’utilisateur et des actions de l’utilisateur sur le formulaire.  Cela permet d’assurer la précision et accélère le remplissage des formulaires.

Goals:

* Créer et appliquer des règles aux champs de formulaires adaptatifs
* Utiliser des règles pour déclencher des services de modèle de données de formulaire pour mettre à jour les données dans la base de données

[![Consultez le Guide](https://helpx.adobe.com/content/dam/help/en/marketing-cloud/how-to/digital-foundation/_jcr_content/main-pars/image_1250343773/see-the-guide-sm.png)](apply-rules-to-adaptive-form-fields.md)

## Étape 4 : appliquer un style à votre formulaire adaptatif {#step-style-your-adaptive-form}

![](/help/forms/using/assets/09-style-your-adaptive-form-small.png)

Adaptive forms provide themes and an [editor](../../forms/using/themes.md) to create themes for the adaptive forms. Un thème contient les informations de style pour les composants et les panneaux, et vous pouvez réutiliser un thème dans plusieurs formulaires. Ces styles incluent les propriétés telles que les couleurs d’arrière-plan, les couleurs d’état, la transparence, l’alignement et la taille. Lorsque vous appliquez un thème à votre formulaire, le style spécifié se reflète sur des composants correspondants de votre formulaire. Les formulaires adaptatifs prennent également en charge le style en ligne pour les styles spécifiques à un formulaire.

Goals:

* Appliquer un thème prêt à l’emploi à un formulaire adaptatif
* Créer un thème pour formulaire adaptatif à l’aide de l’éditeur de thème
* Utiliser des polices Web dans un thème personnalisé

[![Consultez le Guide](https://helpx.adobe.com/content/dam/help/en/marketing-cloud/how-to/digital-foundation/_jcr_content/main-pars/image_1250343773/see-the-guide-sm.png)](style-your-adaptive-form.md)

## Étape 5 : test de votre formulaire adaptatif {#step-test-your-adaptive-form}

![11-test-votre-formulaire adaptatif](assets/11-test-your-adaptive-form.png)

Les formulaires adaptatifs font partie intégrante de vos interactions avec les clients. Il est important de tester vos formulaires adaptatifs à chaque modification que vous y apportez. Tester tous les champs d’un formulaire est fastidieux. AEM [!DNL Forms] provide an SDK (Calvin SDK) to automate testing of adaptive forms. Calvin vous permet d’automatiser les tests de vos formulaires adaptatifs dans le navigateur Web.

Goals:

* Créer une suite de tests pour le formulaire adaptatif
* Création de cas de test pour les formulaires adaptatifs
* Exécuter les cas de test

[![Consultez le Guide](https://helpx.adobe.com/content/dam/help/en/marketing-cloud/how-to/digital-foundation/_jcr_content/main-pars/image_1250343773/see-the-guide-sm.png)](testing-your-adaptive-form.md)

## Étape 6: publication de votre formulaire adaptatif {#step-publish-your-adaptive-form}

![12-publish-your-adaptive-form-_small](assets/12-publish-your-adaptive-form-_small.png)

You can publish adaptive forms as a stand-alone form (single page application), include in AEM [Sites page](/help/forms/using/embed-adaptive-form-aem-sites.md), or list on an AEM [!DNL Site] using [Forms Portal](../../forms/using/introduction-publishing-forms.md).

Goals:

* Publier le formulaire adaptatif en tant que page AEM
* Incorporer le formulaire adaptatif dans une [!DNL Sites] page AEM
* Incorporer le formulaire adaptatif dans une page Web externe (une page Web non AEM hébergée en dehors de l’AEM)

[![Consultez le Guide](https://helpx.adobe.com/content/dam/help/en/marketing-cloud/how-to/digital-foundation/_jcr_content/main-pars/image_1250343773/see-the-guide-sm.png)](publish-your-adaptive-form.md)