---
title: Topologies d’architecture et de déploiement pour AEM Forms
seo-title: Topologies d’architecture et de déploiement pour AEM Forms
description: Informations détaillées sur l’architecture d’AEM Forms et les topologies recommandées pour les nouveaux clients d’AEM et les clients existant, ainsi que pour les clients LiveCycle ES4 évoluant vers AEM Forms.
seo-description: Informations détaillées sur l’architecture d’AEM Forms et les topologies recommandées pour les nouveaux clients d’AEM et les clients existant, ainsi que pour les clients LiveCycle ES4 évoluant vers AEM Forms.
uuid: 90baa57a-4785-4b49-844c-a44717d3c12d
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: installing
geptopics: SG_AEMFORMS/categories/jee
discoiquuid: 0156b5c3-3bef-4213-9ada-c7b6ae96ada4
role: Administrator
exl-id: d4421d46-cfc9-424e-8a88-9d0a2994a5cf
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '2490'
ht-degree: 41%

---

# Topologies d’architecture et de déploiement pour AEM Forms {#architecture-and-deployment-topologies-for-aem-forms}

## Architecture {#architecture}

AEM Forms est une application déployée dans AEM sous la forme d’un package AEM. Le module est appelé module complémentaire AEM Forms. Le package de module complémentaire AEM Forms contient les deux services (fournisseurs d’API), qui sont déployés dans le conteneur OSGi AEM, ainsi que les servlets ou JSP (fournissant des fonctionnalités frontales et d’API REST) gérés par la structure Sling AEM. Le diagramme suivant illustre cette configuration:

![Architecture](assets/architecture.png)

L’architecture d’AEM Forms comprend les composants suivants :

* **Services AEM principaux :** services de base fournis par AEM à une application déployée. Ces services comprennent un référentiel de contenu compatible JCR, un conteneur de services OSGI, un moteur de workflow, un Trust Store, un magasin de clés, etc. Ces services sont accessibles par l’application AEM Forms mais ne sont pas fournis par les modules AEM Forms. Ces services font partie intégrante de la pile AEM globale et divers composants AEM Forms utilisent ces services.
* **Services Forms :** proposez des fonctionnalités liées aux formulaires, telles que la création, l’assemblage, la distribution et l’archivage de documents PDF, l’ajout de signatures numériques pour limiter l’accès aux documents et le décodage de formulaires à code à barres. Ces services sont disponibles publiquement pour utilisation par le code personnalisé co-déployé dans AEM.
* **Couche Web :** JSP ou servlets, reposant sur les services communs et de formulaires, qui fournissent les fonctionnalités suivantes :

   * **Interface utilisateur frontale de création **: interface utilisateur de création et de gestion de formulaires pour créer et gérer des formulaires.
   * **Interface utilisateur frontale de rendu et de publication de formulaire** : interface utilisateur destinée à être utilisée par les utilisateurs finaux d’AEM Forms (par exemple, des citoyens accédant à un site Web gouvernemental). Elle fournit des fonctionnalités de rendu de formulaire (affichage de formulaire dans un navigateur web) et d’envoi.
   * **API REST **: les JSP et servlets exportent un sous-ensemble de services de formulaires à des fins d’utilisation distante par des clients HTTP appropriés, comme le kit SDK mobile des formulaires.

**AEM Forms sur OSGi :** un environnement AEM Forms sur OSGi est un environnement AEM Author standard ou AEM Publish avec le package AEM Forms déployé dessus. Vous pouvez exécuter AEM Forms sur OSGi dans un [environnement serveur unique, une batterie et des configurations en grappe](/help/sites-deploying/recommended-deploys.md). La configuration du cluster est disponible uniquement pour les instances d’auteur AEM.

**AEM Forms on JEE :**  AEM Forms on JEE est un serveur AEM Forms qui s’exécute sur la pile JEE. Il dispose d’AEM Author avec des modules complémentaires AEM Forms et des fonctionnalités AEM Forms JEE supplémentaires co-déployées sur une seule pile JEE s’exécutant sur un serveur d’applications. Vous pouvez exécuter AEM Forms on JEE dans des configurations à serveur unique et en grappe. AEM Forms on JEE est nécessaire uniquement pour exécuter Document Security, Process Management et pour les clients LiveCycle effectuant une mise à niveau vers AEM Forms. Voici quelques scénarios supplémentaires pour l’utilisation d’AEM Forms on JEE :

* **Prise en charge de l’espace de travail HTML (pour les utilisateurs de l’espace de travail HTML) :** AEM Forms on JEE active l’authentification unique avec les instances de traitement, diffuse certaines ressources rendues sur les instances de traitement et gère l’envoi de formulaires générés dans l’espace de travail HTML.
* **Traitement complémentaire avancé des données de formulaire/communication interactive** : AEM Forms on JEE peut être utilisé pour traiter des données de formulaire/communication interactive supplémentaires (et enregistrer les résultats dans un magasin de données approprié) dans des cas d’utilisation complexes où des fonctionnalités avancées de gestion de processus sont requises.

AEM Forms on JEE comprend également les services de prise en charge suivants pour les composants AEM :

* **Gestion intégrée des utilisateurs :** permet aux utilisateurs d’AEM Forms on JEE d’être reconnus comme des utilisateurs d’AEM forms on OSGi et aide à activer l’authentification unique pour les utilisateurs d’OSGi et de JEE. Cela est nécessaire dans les cas où une authentification unique entre AEM forms on OSGi et AEM Forms on JEE est requise (par exemple, l’espace de travail HTML).
* **Hébergement de ressources :**  AEM Forms on JEE peut traiter des ressources (par exemple, des formulaires HTML5) rendues sur AEM Forms sur OSGi.

L’interface utilisateur de création d’AEM Forms ne prend pas en charge la création d’un document d’enregistrement (DOR), de PDF forms et de HTML5 Forms. Ces ressources sont conçues à l’aide de l’application Forms Designer autonome et téléchargées individuellement vers AEM Forms Manager. Pour AEM Forms on JEE, les formulaires peuvent également être conçus comme des actifs d’application (dans AEM Forms Workbench) et déployés sur le serveur AEM Forms on JEE.

AEM Forms sur OSGi et AEM Forms sur JEE disposent tous deux de fonctionnalités de workflow. Vous pouvez rapidement créer et déployer des processus de base pour diverses tâches sur AEM forms on OSGi, sans avoir à installer la fonctionnalité de gestion des processus complète d’AEM Forms on JEE. Il existe une différence dans les [fonctionnalités du processus basé sur l’utilisation de Forms sur AEM Forms on OSGi et de la fonctionnalité de gestion des processus d’AEM Forms on JEE](capabilities-osgi-jee-workflows.md). Le développement et la gestion des processus basés sur l’utilisation de Forms sur AEM Forms sur OSGi utilisent les fonctionnalités familières de flux de travail AEM et de boîte de réception AEM.

## Terminologies {#terminologies}

L’image suivante affiche diverses configurations de serveur AEM Forms et leurs composants utilisés dans un déploiement AEM Forms classique :

![aem_forms_-_recommendationstopology](assets/aem_forms_-_recommendedtopology.png)

**Auteur :** une instance d’auteur est un serveur AEM Forms exécuté en mode d’exécution de création standard. Il peut s’agir d’un environnement AEM Forms on JEE ou AEM Forms on OSGi. Il est destiné aux utilisateurs internes, aux concepteurs de formulaires et de communication interactive, ainsi qu’aux développeurs. L’élément Publier active les fonctionnalités suivantes :

* **Création et gestion de formulaires et de communications interactives :** les concepteurs et développeurs peuvent créer et modifier des formulaires adaptatifs et des communications interactives, télécharger d’autres types de formulaires créés en externe, par exemple des formulaires créés dans Adobe Forms Designer, et gérer ces ressources à l’aide de la console de Gestionnaire de formulaires.
* **Publication de formulaires et de communications interactives :** les éléments hébergés sur une instance d’auteur peuvent être publiés sur une instance de publication pour exécuter des opérations d’exécution. La publication d’actifs utilise les fonctionnalités de réplication d’AEM. Adobe recommande qu’un agent de réplication soit configuré sur toutes les instances d’auteur pour transférer manuellement les formulaires publiés vers les instances de traitement, et qu’un autre agent de réplication soit configuré sur les instances de traitement avec le déclencheur *A réception* activé pour répliquer automatiquement les formulaires reçus afin de publier les instances.

**Publier :** une instance de publication est un serveur AEM Forms s’exécutant en mode d’exécution Publier standard. Les instances de publication sont destinées aux utilisateurs finaux des applications de formulaires (par exemple, les utilisateurs accédant à un site Web public et envoyant des formulaires). L’élément Publier active les fonctionnalités suivantes :

* Rendu et envoi de formulaires pour les utilisateurs finaux.
* Transmission des données de formulaire brutes envoyées aux instances de traitement pour un traitement supplémentaire et le stockage dans le système d’enregistrements final. L’implémentation par défaut fournie dans AEM Forms effectue cette opération à l’aide de la fonctionnalité de réplication inverse d’AEM. Un autre type d’implémentation est également disponible pour transférer directement les données du formulaire aux serveurs de traitement au lieu de les enregistrer localement d’abord (cette dernière étape constituant un prérequis pour l’activation de la réplication inverse). Les clients qui ont des préoccupations concernant le stockage de données potentiellement sensibles sur les instances de publication peuvent procéder à cette [mise en oeuvre alternative](/help/forms/using/configuring-draft-submission-storage.md), car les instances de traitement se trouvent généralement dans une zone plus sécurisée.
* Rendu et envoi de communications et de lettres interactives : Une communication interactive et une lettre sont rendues sur les instances de publication et les données correspondantes sont envoyées aux instances de traitement pour le stockage et le post-traitement. Les données peuvent être sauvegardées localement sur une instance de publication et traitées par réplication inverse vers une instance de traitement (l’option par défaut) ultérieurement, ou directement transférées vers l’instance de traitement sans enregistrement sur l’instance de publication. Cette dernière implémentation est utile pour les clients soucieux de leur sécurité.

**Traitement :** instance d’AEM Forms s’exécutant en mode d’exécution Auteur sans utilisateurs affectés au groupe de gestionnaires de formulaires. Vous pouvez déployer AEM Forms on JEE ou AEM Forms on OSGi en tant qu’instance de traitement. Les utilisateurs ne sont pas affectés pour s’assurer que les activités de création et de gestion de formulaires ne sont pas exécutées sur l’instance de traitement et se produisent uniquement sur l’instance d’auteur. Une instance de traitement permet les fonctionnalités suivantes :

* **Traitement des données de formulaire brutes provenant d’une instance de publication :**  cette opération s’effectue principalement sur une instance de traitement via AEM workflows qui se déclenchent lorsque les données arrivent. Les processus peuvent utiliser l’étape Modèle de données de formulaire fournie d’usine pour archiver les données ou le document dans un entrepôt de données approprié.
* **Stockage sécurisé des données de formulaire :** l’élément Traitement fournit un référentiel derrière le pare-feu pour les données de formulaire brutes qui sont également isolées des utilisateurs. Ni les concepteurs de formulaires sur l’instance d’auteur, ni les utilisateurs finaux sur l’instance de publication ne peuvent accéder à ce référentiel.

   >[!NOTE]
   >
   > Adobe recommande d’utiliser un entrepôt de données tiers pour enregistrer les données traitées finales au lieu d’utiliser AEM référentiel.

* **Stockage et post-traitement des données de correspondance provenant d’une instance de publication :** AEM workflows effectuent le post-traitement facultatif des définitions de lettre correspondantes. Ces processus peuvent enregistrer les données finales traitées dans des magasins de données externes appropriés.

* **Hébergement** de Workspace HTML : Une instance de traitement héberge l’interface frontale de Workspace HTML. Workspace HTML fournit l’interface utilisateur pour l’affectation de tâche/groupe associée pour les processus de révision et d’approbation.

Une instance de traitement est configurée pour s’exécuter en mode d’exécution Auteur car :

* Elle active la réplication inverse des données de formulaire brutes d’une instance de publication. Le gestionnaire de stockage de données par défaut nécessite la fonctionnalité de réplication inverse.
* AEM Workflows, qui sont les Principaux moyens de traitement des données de formulaire brutes provenant d’une instance de publication, sont recommandés pour s’exécuter sur un système de type création.

## Exemples de topologies physiques pour AEM Forms on JEE {#sample-physical-topologies-for-aem-forms-on-jee}

Les topologies d’AEM Forms on JEE recommandées ci-dessous concernent principalement les clients effectuant une mise à niveau à partir de LiveCycle ou d’une version précédente d’AEM Forms on JEE. Adobe recommande d’utiliser AEM Forms sur OSGi pour les nouvelles installations. Une nouvelle installation d’AEM Forms on JEE est recommandée uniquement pour l’utilisation des fonctionnalités Document Security et Process Management.

### Topologie d’utilisation des services de document ou des fonctionnalités de sécurité des documents {#topology-for-using-document-services-or-document-security-capabilities}

Les clients AEM Forms prévoyant d’utiliser uniquement des services de document ou des fonctionnalités de sécurité des documents peuvent avoir une topologie similaire à celle affichée ci-dessous. Cette topologie recommande d’utiliser une seule instance d’AEM Forms. Vous pouvez également créer une grappe ou une ferme de serveurs AEM Forms, si nécessaire. Cette topologie est recommandée lorsque la plupart des utilisateurs accèdent par programmation aux fonctionnalités du serveur AEM Forms et que l’intervention via l’interface utilisateur est minimale. La topologie est utile pour les opérations de traitement par lots de Document Services. Par exemple, utilisez le service de sortie pour créer quotidiennement des centaines de documents PDF non modifiables.

Bien qu’AEM Forms vous permette de configurer et d’exécuter toutes les fonctionnalités à partir d’un seul serveur, vous devez toutefois planifier la capacité, équilibrer la charge et configurer des serveurs dédiés pour des fonctionnalités spécifiques dans un environnement de production. Par exemple, pour un environnement qui utilise le service PDF Generator pour convertir des milliers de pages par jour et ajouter des signatures numériques afin de limiter l’accès aux documents, configurez des serveurs AEM Forms distincts pour le service PDF Generator et les fonctionnalités de signature numérique. Cela permet de fournir des performances optimales et de dimensionner les serveurs indépendamment les uns des autres.

![basic-features](assets/basic-features.png)

### Topologie pour l’utilisation de la gestion de processus AEM Forms {#topology-for-using-aem-forms-process-management}

Les clients AEM Forms qui envisagent d’utiliser les fonctionnalités de gestion de processus AEM Forms, par exemple, Workspace HTML peut avoir une topologie similaire à celle affichée ci-dessous. Le serveur AEM Forms on JEE peut se trouver dans une configuration de serveur ou de grappe unique.

Si vous effectuez une mise à niveau à partir de LiveCycle ES4, cette topologie reflète fidèlement ce que vous avez déjà dans LiveCycle, à l’exception de l’ajout d’AEM Author intégré à AEM Forms on JEE. De plus, il n’y a pas de changement dans les exigences de mise en grappe pour les clients effectuant une mise à niveau. Si vous utilisiez AEM Forms dans un environnement en grappe, vous pouvez continuer avec cette méthode dans AEM 6.5 Forms. Pour une nouvelle installation d’AEM Forms of JEE pour l’utilisation de HTML Workspace, l’exécution d’AEM instance d’auteur intégrée à l’environnement JEE est une exigence supplémentaire.

L’entrepôt de données de formulaire est un entrepôt de données tiers utilisé pour stocker les données finales traitées des formulaires et des communications interactives. Il s’agit d’un élément facultatif dans la topologie. Vous pouvez également choisir de configurer une instance de traitement et d’utiliser son référentiel comme système d’enregistrement final, si nécessaire.

![topology_for_usinghtmlworkspace andformsapp](assets/topology_for_usinghtmlworkspaceandformsapp.png)

La topologie est recommandée aux clients qui envisagent d’utiliser le serveur AEM Forms on JEE pour les fonctionnalités de gestion des processus (Workspace HTML) sans utiliser de post-traitement, de formulaires adaptatifs, de formulaires HTML5 et de fonctionnalités de communication interactive.

### Topologie d’utilisation des formulaires adaptatifs, des formulaires HTML5, des fonctionnalités de communication interactive {#topology-for-using-adaptive-forms-html-forms-interactive-communication-capabilities}

Les clients AEM Forms prévoyant d’utiliser les fonctionnalités de capture de données AEM Forms, par exemple, les formulaires adaptatifs, les formulaires HTML5 et les formulaires PDF, peuvent avoir une topologie similaire à celle présentée ci-dessous. Cette topologie est également recommandée pour l’utilisation des fonctionnalités de communication interactive d’AEM Forms.

![topology-for-using-forms-osgi-modules](assets/topology-for-using-forms-osgi-modules.png)

Vous pouvez apporter les modifications/personnalisations suivantes à la topologie suggérée ci-dessus :

* L’utilisation de HTML Workspace et de l’application AEM Forms nécessite une instance de création ou de traitement d’AEM. Vous pouvez utiliser l’instance de création AEM intégrée au serveur AEM Forms on JEE au lieu de configurer un serveur de création AEM externe supplémentaire.
* Une instance de création ou de traitement AEM est requise uniquement pour les processus basés sur l’utilisation de Forms sur OSGi, les formulaires adaptatifs, le portail de formulaires et la communication interactive.
* l’interface utilisateur de l’agent de communication interactive est généralement exécutée au sein de l’entreprise. Vous pouvez donc conserver un serveur de publication pour l’interface utilisateur de l’agent dans le réseau privé.
* AEM les formulaires sur une instance OSGi intégrée au serveur AEM Forms on JEE peuvent également exécuter des processus basés sur Forms sur OSGi et des dossiers de contrôle.

## Exemples de topologies physiques pour AEM Forms on OSGi {#sample-physical-topologies-for-using-aem-forms-on-osgi}

### Topologie pour les fonctionnalités de capture de données, de communication interactive, de processus basé sur l’utilisation de Forms on OSGi {#topology-for-data-capture-interactive-communication-form-centric-workflow-on-osgi-capabilities}

Les clients AEM Forms prévoyant d’utiliser les fonctionnalités de capture de données AEM Forms, par exemple, les formulaires adaptatifs, les formulaires HTML5 et les formulaires PDF, peuvent avoir une topologie similaire à celle présentée ci-dessous. Cette topologie est également recommandée pour l’utilisation de la fonctionnalité de communications interactives et de processus basés sur l’utilisation de Forms on OSGi, par exemple pour utiliser la boîte de réception AEM et l’application AEM Forms pour les flux de processus métier.

![interactive-use-cases-af-cm-osgi-workflow](assets/interactive-use-cases-af-cm-osgi-workflow.png)

### Topologie d’utilisation des fonctionnalités de dossier de contrôle pour le traitement par lots hors ligne {#topology-for-using-watched-folder-capabilities-for-offline-batch-processing}

Les clients AEM Forms qui envisagent d’utiliser des dossiers de contrôle pour le traitement par lots peuvent avoir une topologie similaire à celle affichée ci-dessous. La topologie affiche un environnement organisé en grappes, mais vous décidez d’utiliser une seule instance ou une ferme de serveurs AEM Forms en fonction de la charge. La source de données tierce est votre propre système d’enregistrement. Il agit comme une source d’entrée pour les dossiers de contrôle. La topologie affiche également la sortie sous la forme d’un fichier imprimé. Vous pouvez également stocker le contenu de sortie dans un système de fichiers, l’envoyer par courrier électronique et utiliser d’autres méthodes personnalisées pour utiliser les résultats.

![traitement par lot hors ligne-via-dossiers-surveillés](assets/offline-batch-processing-via-watched-folders.png)

### Topologie d’utilisation des fonctionnalités des services de document pour le traitement hors ligne basé sur l’API {#topology-for-using-document-services-capabilities-for-offline-api-based-processing}

Les clients AEM Forms prévoyant d’utiliser uniquement la fonctionnalité de services de document peuvent avoir une topologie similaire à celle affichée ci-dessous. Cette topologie recommande d’utiliser une grappe de serveurs AEM Forms on OSGi. Cette topologie est recommandée lorsque la plupart des utilisateurs accèdent par programmation aux fonctionnalités du serveur AEM Forms (à l’aide d’API) et que l’intervention via l’interface utilisateur est minimale. La topologie est très utile dans plusieurs cas de logiciels clients. Par exemple, plusieurs clients utilisant le service PDF Generator pour créer des documents PDF à la demande.

Bien qu’AEM Forms vous permette de configurer et d’exécuter toutes les fonctionnalités à partir d’un seul serveur, vous devez planifier la capacité, équilibrer la charge et configurer des serveurs dédiés pour des fonctionnalités spécifiques dans un environnement de production. Par exemple, pour un environnement utilisant le service PDF Generator pour convertir des milliers de pages par jour et plusieurs formulaires adaptatifs pour capturer des données, configurez des serveurs AEM Forms distincts pour le service PDF Generator et les fonctionnalités de formulaires adaptatifs. Cela permet de fournir des performances optimales et de dimensionner les serveurs indépendamment les uns des autres.

![traitement basé sur les api hors ligne](assets/offline-api-based-processing.png)
