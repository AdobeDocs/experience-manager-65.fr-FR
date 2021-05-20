---
title: Tutoriel - Créer votre première communication interactive
seo-title: Créer votre première communication interactive
description: Découvrez comment créer votre première communication interactive.
seo-description: Découvrez comment créer votre première communication interactive.
uuid: ed5003c6-ba3a-4fcb-8645-c7b607b22fb5
contentOwner: anujkapo
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: interactive-communications, introduction
discoiquuid: 954da8da-a30b-477d-bde7-3edd86a5be11
feature: Communication interactive
exl-id: b20bb719-5686-466e-8dde-279b8471bfe3
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1057'
ht-degree: 92%

---

# Didacticiel : Créer votre première communication interactive {#tutorial-create-your-first-interactive-communication}

Découvrez comment créer votre première communication interactive.

![01-create-first-adaptive-form-hero-image](assets/01-create-first-adaptive-form-hero-image.png)

Les communications interactives centralisent et gèrent la création, l’assemblage et la livraison de correspondances sécurisées, personnalisées et interactives telles que la correspondance commerciale, les documents, les déclarations, les courriers marketing, les factures et les kits de bienvenue. Les communications interactives peuvent être fournies par deux canaux : impression et web. Le canal d’impression est utilisé pour créer des documents PDF et des communications papier, tandis que le canal web est utilisé pour fournir des expériences en ligne.

Ce didacticiel fournit un cadre de bout en bout pour la création d’une communication interactive. Il présente un cas d’utilisation et plusieurs guides. Chaque guide vous aide à créer des fonctionnalités utilisées comme blocs de construction pour créer une communication interactive.

L’image suivante illustre les blocs de construction nécessaires à la création d’une communication interactive.

![flux de travail](assets/workflow.gif)

À la fin de ce didacticiel, vous serez capable de :

* Créer des blocs de construction (modèle de données de formulaire, fragments de document et modèles)
* Créer une communication interactive
* Tester et publier une communication interactive

## Cas d’utilisation {#use-case}

La procédure commence par l’apprentissage du cas d’utilisation :

Un opérateur de télécommunications envoie des factures mensuelles aux clients par courrier électronique. La facture est une communication interactive. Le courrier électronique inclut :

* Un fichier PDF protégé par mot de passe, appelé Canal d’impression dans ce didacticiel. Il comprend les informations sur le client, sur la facture, le récapitulatif des frais, les modes de paiement possibles de la facture et les informations d’utilisation.
* Un lien vers la version web de la facture, appelée canal web dans ce didacticiel. La version web de la facture, en plus des informations détaillées dans la version PDF, fournit une représentation graphique des informations d’utilisation et des offres personnalisées basées sur Adobe Target. La version web contient également un formulaire de paiement en ligne. Il permet d’effectuer des paiements en ligne sans quitter l’IC.
* Un lien vers des services à valeur ajoutée, tels que le stockage en ligne, les abonnements de musique et les abonnements de vidéos à la demande.

## Prérequis {#prerequisites}

* Configurez une instance d’auteur AEM.
* Installez le [module complémentaire AEM Forms](/help/forms/using/installing-configuring-aem-forms-osgi.md) sur une instance de création
* Configurez la base de données MYSQL.
* Obtenez le pilote de base de données JDBC (fichier JAR) auprès du fournisseur de base de données. Les exemples du tutoriel sont basés sur la base de données MySQL et utilisent le [pilote de base de données JDBC MySQL](https://dev.mysql.com/downloads/connector/j/5.1.html) de l’Oracle.

## Étape 1 : Planifier la communication interactive {#step-plan-the-interactive-communication}

![07-apply-rules-to-adaptive-form_small](assets/07-apply-rules-to-adaptive-form_small.png)

La première étape de la planification d’une communication interactive consiste à finaliser le contenu de cette dernière. Une fois le contenu finalisé, vous devez l’analyser pour identifier les différents types de ressources requis pour créer la communication interactive.

**Objectifs:**

Pour créer une anatomie pour la communication interactive avec les modes de saisie des données suivants :

* Du texte statique
* Modèle de données de formulaire
* Interface utilisateur de l’agent
* Données conditionnelles
* Images

[ ](/help/forms/using/planning-interactive-communications.md)

## Étape 2 : Créer un modèle de données de formulaire {#step-create-form-data-model}

![03-create-adaptive-form-main-image_small](assets/03-create-adaptive-form-main-image_small.png)

Un modèle de données de formulaire vous permet de connecter une communication interactive à des sources de données disparates, par exemple, le profil utilisateur AEM, les services Web RESTful, les services Web basés sur SOAP, les services OData et les bases de données relationnelles. Un modèle de données de formulaire est un schéma de représentation de données unifié des entités et services d’entreprise disponibles dans des sources de données connectées. Vous pouvez utiliser le modèle de données de formulaire avec une communication interactive pour extraire des données de sources de données connectées. Pour plus d’informations sur le modèle de données de formulaire, voir [Intégration de données AEM Forms](/help/forms/using/data-integration.md).

**Objectifs:**

* Configurer l’instance de base de données (base de données MySQL) en tant que source de données
* Créer le modèle de données de formulaire à l’aide de la base de données MySQL en tant que source de données
* Ajouter des objets de modèle de données pour former un modèle de données
* Configurer les services de lecture et d’écriture pour le modèle de données de formulaire
* Créer des associations entre les objets de modèle de données
* Afficher des exemples de données générés automatiquement
* Modifier les exemples de données
* Tester le modèle de données de formulaire et les services configurés avec des données de test

[ ](/help/forms/using/create-form-data-model0.md)

## Étape 3 : Créer des fragments de document {#step-create-document-fragments}

![05-create-form-data-model-main_small](assets/05-create-form-data-model-main_small.png)

Les fragments de document sont des composants réutilisables d’une correspondance utilisés pour composer une communication interactive. Les fragments de document sont des fragments de type : Texte, Liste et Condition.

**Objectifs:**

* Créer des fragments de document
* Créer des variables
* Créer et appliquer des règles

[ ](/help/forms/using/create-document-fragments.md)

## Étape 4 : Créer des modèles {#step-create-templates}

![07-apply-rules-to-adaptive-form_small](assets/07-apply-rules-to-adaptive-form_small.png)

Pour créer une communication interactive, vous devez disposer de modèles disponibles sur le serveur AEM pour les canaux d’impression et web.

Les modèles pour le canal d’impression sont créés dans Adobe Forms Designer et téléchargés sur le serveur AEM. Ces modèles sont ensuite disponibles pour être utilisés lors de la création d’une communication interactive.

Les modèles pour le canal web sont créés dans AEM. Les auteurs et les administrateurs de modèles peuvent créer, modifier et activer des modèles web. Une fois créés et activés, ces modèles sont disponibles pour être utilisés lors de la création d’une communication interactive.

**Objectifs:**

* Créer des modèles XDP pour le canal d’impression à l’aide d’Adobe Forms Designer
* Télécharger les modèles XDP sur le serveur AEM Forms
* Créer et activer des modèles pour le canal web

[ ](/help/forms/using/create-templates-print-web.md)

## Étape 5 : Créer une communication interactive {#step-create-an-interactive-communication}

![09-style-your-adaptive-form-small](assets/09-style-your-adaptive-form-small.png)

Une fois que vous avez créé tous les blocs de construction, tels que le modèle de données de formulaire, les fragments de document et les modèles pour la version web, vous pouvez commencer à créer une communication interactive.

Les communications interactives peuvent être fournies par deux canaux : impression et web. Vous pouvez également créer une communication interactive avec le canal d’impression comme option principale. L’impression comme option principale pour le canal web garantit que le contenu, l’héritage et la liaison des données du canal web sont dérivés du canal d’impression.

**Objectifs:**

* Créer une communication interactive pour le canal d’impression
* Créer une communication interactive pour le canal web
* Créer des communications interactives d’impression et web interactives avec l’impression comme option principale
* Créer un tableau dynamique dans la version web de la communication interactive
* Créer un tableau dans la version web de la communication interactive
* Création d’hyperliens dans la version web de la communication interactive

[ ](/help/forms/using/create-interactive-communication0.md)

## Étape 6 : Tester votre communication interactive {#step-test-your-interactive-communication}

![11-test-votre-formulaire adaptatif](assets/11-test-your-adaptive-form.png)

Une fois que vous avez créé une communication interactive, il est important de tester chaque modification que vous y apportez. Testez tous les champs d’une communication interactive est fastidieux. AEM Forms fournit un SDK (Calvin SDK) pour automatiser les tests de communications interactives dans un navigateur web.

**Objectifs:**

* Créer une suite de tests
* Créer des cas de test
* Exécuter les cas de test

## Étape 7 : Publier votre communication interactive {#step-publish-your-interactive-communication}

![12-publish-your-adaptive-form-_small](assets/12-publish-your-adaptive-form-_small.png)

Une fois que vous avez créé et testé les communications interactives à l’aide des canaux d’impression et web, vous pouvez publier ces ressources. Le cas d’utilisation décrit dans ce didacticiel porte sur l’intégration de ces ressources à un client de messagerie. Le client de messagerie sert de passerelle pour envoyer les communications interactives à plusieurs adresses électroniques.

**Objectifs:**

* Intégrer les communications interactives à un client de messagerie pour pouvoir envoyer une communication aux clients
* Inclure un document PDF en tant que pièce jointe (communication interactive créée dans le canal d’impression)
* Inclure un lien vers la version web de la communication interactive
