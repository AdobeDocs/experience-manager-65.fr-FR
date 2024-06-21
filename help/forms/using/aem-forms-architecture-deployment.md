---
title: Topologies d’architecture et de déploiement pour AEM Forms
description: Informations détaillées sur l’architecture d’AEM Forms et topologies recommandées pour la nouvelle clientèle d’AEM et la clientèle existante, ainsi que pour la clientèle LiveCycle ES4 évoluant vers AEM Forms.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: installing
geptopics: SG_AEMFORMS/categories/jee
role: Admin
exl-id: d4421d46-cfc9-424e-8a88-9d0a2994a5cf
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms, Foundation Components
source-git-commit: 539da06db98395ae6eaee8103a3e4b31204abbb8
workflow-type: tm+mt
source-wordcount: '2469'
ht-degree: 100%

---

# Topologies d’architecture et de déploiement pour AEM Forms {#architecture-and-deployment-topologies-for-aem-forms}

| Version | Lien de l’article |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Cliquez ici](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/forms-overview/aem-forms-cloud-service-architecture.html?lang=fr) |
| AEM 6.5 | Cet article |

## Architecture {#architecture}

AEM Forms est une application déployée dans AEM sous forme de package AEM. Le package est appelé comme suit : package de modules complémentaires AEM Forms. Le package de modules complémentaires AEM Forms contiennent des services (fournisseurs d’API), qui sont déployés dans le conteneur AEM OSGi, et les servlets ou JSP (octroi de fonctionnalités front-end et API REST) gérés par le framework Sling AEM. Le diagramme suivant illustre cette configuration:

![Architecture](assets/architecture.png)

L’architecture d’AEM Forms comprend les composants suivants :

* **Services AEM principaux :** services de base fournis par AEM à une application déployée. Ces services comprennent un référentiel de contenu compatible JCR, un conteneur de service OSGi, un moteur de workflow, un trust store, un magasin de clés, etc. Ces services sont accessibles par l’application AEM Forms mais ne sont pas fournis par les packages AEM Forms. Ces services font partie intégrante de la pile AEM globale et divers composants AEM Forms utilisent ces services.
* **Services Forms :** fournissez des fonctionnalités liées aux formulaires, telles que la création, l’assemblage, la distribution et l’archivage de documents PDF, l’ajout de signatures numériques pour limiter l’accès aux documents et le décodage de formulaires à codes-barres. Ces services sont disponibles publiquement à des fins d’utilisation par le code personnalisé co-déployé dans AEM.
* **Couche Web :** JSP ou servlets, reposant sur les services communs et de formulaires, qui fournissent les fonctionnalités suivantes :

   * **Interface utilisateur front-end de création** : interface utilisateur de création et de gestion de formulaires pour créer et gérer des formulaires.
   * **Interface utilisateur frontale de rendu et de publication de formulaire** : interface utilisateur destinée à être utilisée par les utilisatrices et utilisateurs finaux d’AEM Forms (par exemple, des citoyennes et citoyens accédant à un site web d’administration). Cette interface fournit des fonctionnalités de rendu de formulaire (affichage du formulaire dans un navigateur web) et d’envoi.
   * **API REST** : les JSP et servlets exportent un sous-ensemble de services de formulaires à des fins d’utilisation distante par des clients HTTP appropriés, comme le kit SDK mobile des formulaires.

**AEM Forms sur OSGi :** un environnement AEM Forms sur OSGi est un environnement dʼauteur ou de publication AEM standard sur lequel est déployé le package AEM Forms. Vous pouvez exécuter AEM Forms sur OSGi dans des [configurations à serveur unique, en batterie et en grappes](/help/sites-deploying/recommended-deploys.md). La mise en grappe n’est disponible que pour les instances dʼauteur AEM.

**AEM Forms sur JEE :** AEM Forms sur JEE est un serveur AEM Forms qui s’exécute sur la pile JEE. Il dispose de lʼinstance dʼauteur AEM avec des packages de modules complémentaires AEM Forms et des fonctionnalités AEM Forms JEE supplémentaires, co-déployés sur une seule pile JEE fonctionnant sur un serveur d’applications. Vous pouvez exécuter AEM Forms sur JEE dans des configurations à serveur unique et en grappes. AEM Forms sur JEE nʼest nécessaire que pour assurer la sécurité des documents, la gestion des processus et pour les clients LiveCycle qui passent à AEM Forms. Voici quelques scénarios supplémentaires dʼutilisation dʼAEM Forms sur JEE :

* **Prise en charge de Workspace HTML (pour les utilisateurs de Workspace HTML) :** AEM Forms sur JEE permet l’authentification unique auprès des instances de traitement, peut être utilisé pour certaines ressources générées sur les instances de traitement et gère l’envoi de formulaires générés dans lʼespace de travail HTML.
* **Traitement complémentaire avancé des données de formulaire ou de communication interactive** : AEM Forms sur JEE peut être utilisé pour le traitement supplémentaire des données de formulaire ou de communication interactive (et lʼenregistrement des résultats dans une banque de données appropriée) dans le cadre de cas d’utilisations complexes où des fonctionnalités avancées de gestion de processus sont requises.

AEM Forms sur JEE offre également les services suivants aux composants AEM :

* **Gestion intégrée des utilisateurs :** permet aux utilisateurs d’AEM Forms sur JEE d’être reconnus en tant quʼutilisateurs dʼAEM Forms sur OSGi, ainsi que dʼactiver l’authentification unique pour les utilisateurs d’OSGi et de JEE. Ceci est nécessaire dans les cas où une authentification unique entre AEM Forms sur OSGI et AEM Forms sur JEE est requise (par exemple, lʼespace de travail HTML).
* **Hébergement de ressource :** AEM Forms sur JEE peut être utilisé pour des ressources (par exemple, des formulaires HTML5) rendues sur AEM Forms sur OSGi.

L’interface utilisateur dʼauteur AEM Forms ne prend pas en charge la création de documents d’enregistrement (DOR) et de formulaires PDF et HTML5. Ces ressources sont conçues à l’aide de l’application autonome Forms Designer et téléchargées individuellement vers AEM Forms Manager. Par contre, pour AEM Forms sur JEE, les formulaires peuvent être conçus en tant que ressources d’application (dans AEM Forms Workbench) et déployés sur le serveur AEM Forms sur JEE.

AEM Forms sur OSGi et AEM Forms sur JEE disposent de fonctionnalités de workflow. Vous pouvez rapidement créer et déployer des workflows de base pour effectuer différentes tâches sur AEM Forms sur OSGi, sans avoir à installer la fonctionnalité Process Management complète dʼAEM Forms sur JEE. Il y a une certaine différence dans les [Fonctionnalités de workflow basé sur lʼutilisation de Forms sur AEM Forms sur OSGi et la fonctionnalité Process Management d’AEM Forms sur JEE](capabilities-osgi-jee-workflows.md). Le développement et la gestion des workflows basés sur l’utilisation de Forms sur AEM Forms sur OSGi utilisent les fonctionnalités de workflow et de boîte de réception AEM habituelles.

## Terminologies {#terminologies}

L’image suivante affiche diverses configurations de serveur AEM Forms et leurs composants utilisés dans un déploiement AEM Forms classique :

![aem_forms_-_recommendationstopology](assets/aem_forms_-_recommendedtopology.png)

**Création :** une instance de création est un serveur AEM Forms exécuté en mode d’exécution de création standard. Il peut s’agir d’un environnement AEM Forms on JEE ou AEM Forms on OSGi. Il est destiné aux utilisateurs et utilisatrices internes, aux concepteurs et conceptrices de formulaires et de communication interactive, ainsi qu’à l’équipe de développement. Il active les fonctionnalités suivantes :

* **Création et gestion de formulaires et de communications interactives :** les équipes de conception et de développement peuvent créer et modifier des formulaires adaptatifs et des communications interactives, charger d’autres types de formulaires créés en externe, par exemple des formulaires créés dans Adobe Forms Designer, et gérer ces ressources à l’aide de la console de Gestionnaire de formulaires.
* **Publication de formulaires et de communications interactives :** les ressources hébergées sur une instance de création peuvent être publiées sur une instance de publication pour effectuer des opérations d’exécution. La publication des ressources utilise les fonctionnalités de réplication d’AEM. Adobe recommande qu’un agent de réplication soit configuré sur toutes les instances d’auteur pour transférer manuellement les formulaires publiés vers les instances de traitement, et qu’un autre agent de réplication soit configuré sur les instances de traitement avec le déclencheur *A réception* activé pour répliquer automatiquement les formulaires reçus afin de publier les instances.

**Publier :** une instance de publication est un serveur AEM Forms fonctionnant en mode d’exécution de publication standard. Les instances de publication sont destinées aux utilisateurs finaux des applications de formulaires (par exemple, les utilisateurs accédant à un site Web public et envoyant des formulaires). L’élément Publier active les fonctionnalités suivantes :

* Rendu et envoi de formulaires pour les utilisatrices et utilisateurs finaux.
* Transmission des données de formulaire brutes envoyées aux instances de traitement pour un traitement supplémentaire et stockage dans le système d’enregistrements final. L’implémentation par défaut fournie dans AEM Forms effectue cette opération à l’aide des fonctionnalités de réplication inverse d’AEM. Un autre type d’implémentation est également disponible pour transférer directement les données du formulaire aux serveurs de traitement au lieu de les enregistrer localement d’abord (cette dernière étape constituant un prérequis pour l’activation de la réplication inverse). Les clients rencontrant des problèmes de stockage des données potentiellement sensibles sur les instances de publication peuvent utiliser cette [alternative d’implémentation](/help/forms/using/configuring-draft-submission-storage.md), car les instances de traitement se trouvent généralement dans une zone plus sécurisée.
* Rendu et envoi de lettres et de communications interactives : une lettre et une communication interactive sont rendues sur les instances de publication et les données correspondantes sont envoyées aux instances de traitement pour le stockage et le post-traitement. Les données peuvent être sauvegardées localement sur une instance de publication et traitées par réplication inverse vers une instance de traitement (l’option par défaut) ultérieurement, ou directement transférées vers l’instance de traitement sans enregistrement sur l’instance de publication. Cette dernière implémentation est utile pour les clients soucieux de leur sécurité.

**Traitement :** une instance d’AEM Forms s’exécutant en mode Auteur sans utilisateurs affectés au groupe de gestionnaires de formulaires. Vous pouvez déployer AEM Forms sur JEE ou AEM Forms sur OSGi en tant qu’instance de traitement. Les utilisateurs n’y sont pas affectés afin de garantir que les activités de création et de gestion de formulaire ne sont pas exécutées sur l’instance de traitement et se produisent uniquement sur l’instance d’auteur. Une instance de traitement permet les fonctionnalités suivantes :

* **Traitement des données de formulaire brutes en provenance d’une instance de publication :** cela est principalement effectué sur une instance de traitement par le biais de workflows AEM qui se déclenchent lors de l’arrivée des données. Les workflows peuvent utiliser l’étape Modèle de données de formulaire prête à l’emploi pour archiver les données ou le document dans un magasin de données approprié.
* **Stockage sécurisé des données de formulaire :** l’élément Traitement fournit un référentiel derrière le pare-feu pour les données de formulaire brutes qui sont également isolées des utilisateurs. Ni les concepteurs de formulaires de l’instance d’auteur, ni les utilisateurs finaux de l’instance de publication ne peuvent accéder à ce référentiel.

  >[!NOTE]
  >
  >Adobe recommande d’utiliser un magasin de données tiers pour enregistrer les données traitées finales au lieu d’utiliser le référentiel AEM.

* **Stockage et post-traitement des données de correspondance provenant d’une instance de publication :** les workflows AEM exécutent le post-traitement facultatif des définitions de lettre correspondantes. Ces processus peuvent enregistrer les données finales traitées dans des magasins de données externes appropriés.

* **Hébergement de HTML Workspace** : une instance de traitement héberge le front-end de HTML Workspace. HTML Workspace fournit l’interface utilisateur pour l’affectation de tâche/groupe associée pour les processus de révision et d’approbation.

Une instance de traitement est configurée pour s’exécuter en mode de création pour les raisons suivantes :

* Elle active la réplication inverse des données de formulaire brutes d’une instance de publication. Le gestionnaire de stockage de données par défaut requiert la fonctionnalité de réplication inverse.
* Il est recommandé d’exécuter les workflows AEM, moyens principaux de traiter les données de formulaires brutes provenant d’une instance de publication, sur un système de style Auteur.

## Exemples de topologies physiques pour AEM Forms on JEE {#sample-physical-topologies-for-aem-forms-on-jee}

Les topologies d’AEM Forms sur JEE recommandées ci-dessous concernent principalement les clients effectuant une mise à niveau à partir de LiveCycle ou d’une version antérieure d’AEM Forms sur JEE. Adobe recommande d’utiliser AEM Forms sur OSGi pour les nouvelles installations. Une nouvelle installation d’AEM Forms sur JEE est recommandée uniquement pour l’utilisation des fonctionnalités Document Security et Process Management.

### Topologie d’utilisation des services de document ou des fonctionnalités de sécurité des documents {#topology-for-using-document-services-or-document-security-capabilities}

Les clientes et clients AEM Forms prévoyant d’utiliser uniquement des services de document ou des fonctionnalités de sécurité des documents peuvent avoir une topologie similaire à celle affichée ci-dessous. Cette topologie recommande d’utiliser une seule instance d’AEM Forms. Si nécessaire, vous pouvez également créer une grappe ou une ferme de serveurs AEM Forms. Cette topologie est recommandée lorsque la plupart des utilisateurs accèdent par programme aux fonctionnalités du serveur AEM Forms et que l’intervention via l’interface utilisateur est minimale. La topologie est utile dans les opérations de traitement par lots des services de document. Par exemple, utilisez le service de sortie pour créer quotidiennement des centaines de documents PDF non modifiables.

Bien qu’AEM Forms vous permette de configurer et d’exécuter toutes les fonctionnalités depuis un seul serveur, vous devez planifier la capacité, équilibrer la charge et configurer des serveurs dédiés pour des fonctionnalités spécifiques dans un environnement de production. Par exemple, pour un environnement utilisant le service PDF Generator pour convertir des milliers de pages par jour et ajouter des signatures numériques afin de limiter l’accès aux documents, configurez des serveurs AEM Forms distincts pour le service PDF Generator et les fonctionnalités de signature numérique. Cela permet de fournir des performances optimales et de dimensionner les serveurs indépendamment les uns des autres.

![basic-features](assets/basic-features.png)

### Topologie pour l’utilisation de la gestion des processus AEM Forms {#topology-for-using-aem-forms-process-management}

Les clients AEM Forms prévoyant d’utiliser les fonctionnalités de gestion de processus AEM Forms, par exemple HTML Workspace, peuvent avoir une topologie similaire à celle affichée ci-dessous. Le serveur AEM Forms sur JEE peut se trouver dans une configuration de serveur ou de cluster unique.

Si vous effectuez une mise à niveau à partir de LiveCycle ES4, cette topologie reflète fidèlement ce que vous avez déjà dans LiveCycle, à l’exception de l’ajout de l’instance de création d’AEM intégrée à AEM Forms sur JEE. De plus, il n’y a pas de changement dans les exigences de mise en grappe pour les clients effectuant une mise à niveau. Si vous utilisiez AEM Forms dans un environnement en cluster, vous pouvez continuer à le faire dans AEM 6.5 Forms. Pour une nouvelle installation d’AEM Forms sur JEE pour l’utilisation de l’espace de travail HTML, l’exécution de l’instance de création AEM intégrée à l’environnement JEE est une exigence supplémentaire.

Form data store est un magasin de données tiers utilisé pour stocker les données finales traitées des formulaires et des communications interactives. Il s’agit d’un élément facultatif dans la topologie. Vous pouvez également choisir de configurer une instance de traitement et d’utiliser son référentiel comme système d’enregistrement final, si nécessaire.

![topology_for_usinghtmlworkspaceandformsapp](assets/topology_for_usinghtmlworkspaceandformsapp.png)

Cette topologie est recommandée aux clients qui envisagent d’utiliser AEM Forms sur un serveur JEE pour les fonctionnalités de gestion des processus (Espace de travail HTML) sans utiliser de post-traitement, de formulaires adaptatifs, de formulaires HTML5 et de fonctionnalités de communication interactive.

### Topologie pour l’utilisation de formulaires adaptatifs, de formulaires HTML5 et de fonctionnalités de communication interactive {#topology-for-using-adaptive-forms-html-forms-interactive-communication-capabilities}

Les clients AEM Forms prévoyant d’utiliser les fonctionnalités de capture de données AEM Forms, par exemple, les formulaires adaptatifs, les formulaires HTML5 et les formulaires PDF, peuvent avoir une topologie similaire à celle présentée ci-dessous. Cette topologie est également recommandée pour l’utilisation des fonctionnalités de communication interactive d’AEM Forms.

![topologie-pour-l’utilisation-des-modules-Forms-sur-osgi](assets/topology-for-using-forms-osgi-modules.png)

Vous pouvez apporter les modifications/personnalisations suivantes à la topologie suggérée ci-dessus :

* L’utilisation de l’espace de travail HTML et de l’application AEM Forms nécessite une instance de création ou de traitement AEM. Vous pouvez utiliser l’instance de création AEM intégrée au serveur AEM Forms on JEE au lieu de configurer un serveur de création AEM externe supplémentaire.
* Une instance de création ou de traitement AEM est requise uniquement pour les workflows basés sur l’utilisation de Forms sur OSGi, les formulaires adaptatifs, le portail Formulaires et la communication interactive.
* L’interface utilisateur de l’agent de communication interactive est généralement exécutée au sein de l’entreprise. Vous pouvez donc conserver un serveur de publication pour l’interface utilisateur de l’agent au sein du réseau privé.
* L’instance d’AEM Forms sur OSGi intégrée à AEM Forms sur serveur JEE peut également exécuter des workflows basés sur l’utilisation de Forms sur OSGi et des dossiers de contrôle.

## Exemples de topologies physiques pour AEM Forms on OSGi {#sample-physical-topologies-for-using-aem-forms-on-osgi}

### Topologie pour la capture de données, la communication interactive et le workflow basé sur l’utilisation de Forms sur OSGi {#topology-for-data-capture-interactive-communication-form-centric-workflow-on-osgi-capabilities}

Les clients AEM Forms prévoyant d’utiliser les fonctionnalités de capture de données AEM Forms, par exemple, les formulaires adaptatifs, les formulaires HTML5 et les formulaires PDF, peuvent avoir une topologie similaire à celle présentée ci-dessous. Cette topologie est également recommandée pour l’utilisation de la fonctionnalité de communications interactives et de processus basés sur l’utilisation de Forms on OSGi, par exemple pour utiliser la boîte de réception AEM et l’application AEM Forms pour les flux de processus métier.

![cas-d’utilisation-interactifs-du-workflow-osgi-af-cm](assets/interactive-use-cases-af-cm-osgi-workflow.png)

### Topologie d’utilisation des fonctionnalités de dossier de contrôle pour le traitement par lots hors ligne {#topology-for-using-watched-folder-capabilities-for-offline-batch-processing}

Les clientes et clients AEM Forms qui envisagent d’utiliser des dossiers de contrôle pour le traitement par lots peuvent avoir une topologie similaire à celle affichée ci-dessous. La topologie présente un environnement en cluster, mais vous décidez d’utiliser une seule instance ou une batterie de serveurs AEM Forms en fonction de la charge. La source de données tierce est votre propre système d’enregistrement. Il agit comme une source d’entrée pour les dossiers de contrôle. La topologie affiche également la sortie sous la forme d’un fichier imprimé. Vous pouvez également stocker le contenu de sortie dans un système de fichiers, l’envoyer par e-mail et utiliser d’autres méthodes personnalisées pour utiliser les résultats.

![traitement-par-lot-hors-ligne-via-les-dossiers-de-contrôle](assets/offline-batch-processing-via-watched-folders.png)

### Topologie d’utilisation des fonctionnalités des services de document pour le traitement hors ligne basé sur l’API {#topology-for-using-document-services-capabilities-for-offline-api-based-processing}

Les clientes et clients AEM Forms prévoyant d’utiliser uniquement la fonctionnalité de services de document peuvent avoir une topologie similaire à celle affichée ci-dessous. Cette topologie recommande d’utiliser un cluster de serveurs AEM Forms on OSGi. Cette topologie est recommandée lorsque la plupart des utilisateurs et utilisatrices accèdent par programmation aux fonctionnalités du serveur AEM Forms (à l’aide d’API) et que l’intervention via l’interface utilisateur est minimale. La topologie est très utile dans plusieurs cas de logiciels clients. Par exemple, plusieurs clients utilisant le service PDF Generator pour créer des documents PDF à la demande.

Bien qu’AEM Forms vous permette de configurer et d’exécuter toutes les fonctionnalités à partir d’un seul serveur, vous devez planifier la capacité, équilibrer la charge et configurer des serveurs dédiés pour des fonctionnalités spécifiques dans un environnement de production. Par exemple, pour un environnement utilisant le service PDF Generator pour convertir des milliers de pages par jour et plusieurs formulaires adaptatifs pour capturer des données, configurez des serveurs AEM Forms distincts pour le service PDF Generator et les fonctionnalités de formulaires adaptatifs. Cela permet de fournir des performances optimales et de dimensionner les serveurs indépendamment les uns des autres.

![traitement-hors-ligne-basé-sur-l’api](assets/offline-api-based-processing.png)
