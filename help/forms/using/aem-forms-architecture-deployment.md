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
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '2491'
ht-degree: 41%

---


# Topologies d’architecture et de déploiement pour AEM Forms {#architecture-and-deployment-topologies-for-aem-forms}

## Architecture {#architecture}

AEM Forms est une application déployée en AEM sous la forme d’un module AEM. Le package est appelé module complémentaire AEM Forms. Le module complémentaire AEM Forms contient à la fois des services (fournisseurs d’API), qui sont déployés dans le conteneur OSGi AEM, et des servlets ou JSP (qui offrent à la fois des fonctionnalités frontales et d’API REST) gérés par AEM Sling. Le diagramme suivant illustre cette configuration:

![Architecture](assets/architecture.png)

L’architecture d’AEM Forms comprend les composants suivants :

* **Services AEM principaux :** services de base fournis par AEM à une application déployée. Ces services comprennent un référentiel de contenu compatible JCR, un conteneur de service OSGI, un moteur de workflow, un Trust Store, un magasin de clés, etc. Ces services sont accessibles par l’application AEM Forms mais ne sont pas fournis par les modules AEM Forms. Ces services font partie intégrante de la pile AEM globale et divers composants AEM Forms utilisent ces services.
* **Services Forms :** fournit des fonctionnalités liées aux formulaires, telles que la création, l’assemblage, la distribution et l’archivage de documents PDF, l’ajout de signatures numériques pour limiter l’accès aux documents et le décodage de formulaires à code à barres. Ces services sont accessibles au public pour utilisation par le code personnalisé co-déployé dans AEM.
* **Couche Web :** JSP ou servlets, reposant sur les services communs et de formulaires, qui fournissent les fonctionnalités suivantes :

   * **Interface utilisateur frontale de création **: interface utilisateur de création et de gestion de formulaires pour créer et gérer des formulaires.
   * **Interface utilisateur frontale de rendu et de publication de formulaire** : interface utilisateur destinée à être utilisée par les utilisateurs finaux d’AEM Forms (par exemple, des citoyens accédant à un site Web gouvernemental). Ceci fournit des fonctionnalités de rendu de formulaire (affichage de formulaire dans un navigateur Web) et d’envoi.
   * **API REST **: les JSP et servlets exportent un sous-ensemble de services de formulaires à des fins d’utilisation distante par des clients HTTP appropriés, comme le kit SDK mobile des formulaires.

**AEM Forms sur OSGi :** Un environnement AEM Forms sur OSGi est un AEM Author standard ou AEM Publish avec un package AEM Forms déployé dessus. Vous pouvez exécuter AEM Forms sur OSGi dans un [environnement serveur unique, une batterie et des configurations en grappe](/help/sites-deploying/recommended-deploys.md). La configuration de la grappe est disponible uniquement pour les instances d’auteur AEM.

**AEM Forms on JEE:** AEM Forms on JEE est un serveur AEM Forms s’exécutant sur la pile JEE. Il dispose d’AEM Author avec des packages de modules complémentaires AEM Forms et de fonctionnalités AEM Forms JEE supplémentaires co-déployées sur une pile JEE unique s’exécutant sur un serveur d’applications. Vous pouvez exécuter AEM Forms on JEE dans des configurations à serveur unique et en grappe. AEM Forms on JEE n’est nécessaire que pour exécuter la sécurité des documents, la gestion des processus et la mise à niveau vers AEM Forms pour les clients LiveCycles. Voici quelques autres scénarios d’utilisation d’AEM Forms on JEE :

* **Prise en charge de l’espace de travail HTML (pour les utilisateurs de l’espace de travail HTML) :** AEM Forms on JEE active l’authentification unique avec les instances de traitement, diffuse certains fichiers générés sur les instances de traitement et gère l’envoi de formulaires générés dans l’espace de travail HTML.
* **Traitement** avancé des données de communication interactives/formulaires supplémentaires : AEM Forms on JEE peut également être utilisé pour traiter des données de communication interactives/de formulaire (et enregistrer les résultats dans un magasin de données approprié) dans des cas d’utilisation complexes où des fonctionnalités avancées de gestion de processus sont requises.

AEM Forms on JEE fournit également les services de prise en charge suivants aux composants AEM :

* **Gestion intégrée des utilisateurs :** permet aux utilisateurs d’AEM Forms on JEE d’être reconnus comme des utilisateurs d’AEM formulaires sur OSGi et aide à activer l’authentification unique pour les utilisateurs d’OSGi et de JEE. Cela est nécessaire dans les cas où une authentification unique entre AEM formulaires sur OSGi et AEM Forms on JEE est requise (par exemple, l’espace de travail HTML).
* **Hébergement de ressources :** AEM Forms on JEE peut diffuser des ressources (par exemple, des formulaires HTML5) générées sur AEM Forms sur OSGi.

L’interface utilisateur de création AEM Forms ne prend pas en charge la création d’un Document d’enregistrement (DOR), de PDF forms et de Forms HTML5. Ces ressources sont conçues à l’aide de l’application Forms Designer autonome et téléchargées individuellement vers AEM Forms Manager. Vous pouvez également concevoir les formulaires pour AEM Forms on JEE en tant que ressources d’application (dans AEM Forms Workbench) et les déployer sur le serveur AEM Forms on JEE.

AEM Forms sur OSGi et AEM Forms sur JEE disposent tous deux de fonctionnalités de flux de travaux. Vous pouvez rapidement créer et déployer des workflows de base pour diverses tâches sur les formulaires AEM sur OSGi, sans avoir à installer la fonctionnalité complète de gestion des processus de AEM Forms on JEE. Il existe une certaine différence dans les fonctionnalités [du flux de travaux axé sur les formulaires sur AEM Forms sur OSGi et la fonctionnalité de gestion des processus d’AEM Forms sur JEE](capabilities-osgi-jee-workflows.md). Le développement et la gestion de workflows orientés formulaires sur AEM Forms sur OSGi utilisent les fonctionnalités familières de flux de travail AEM et de boîte de réception AEM.

## Terminologies {#terminologies}

L’image suivante affiche diverses configurations de serveur AEM Forms et leurs composants utilisés dans un déploiement AEM Forms classique :

![aem_forms_-_recommendationstopology](assets/aem_forms_-_recommendedtopology.png)

**Auteur :** une instance d’auteur est un serveur AEM Forms exécuté en mode d’exécution de création standard. Il peut s’agir d’un environnement AEM Forms on JEE ou AEM Forms on OSGi. Il est destiné aux utilisateurs internes, aux concepteurs de formulaires et de communication interactive, ainsi qu’aux développeurs. L’élément Publier active les fonctionnalités suivantes :

* **Création et gestion de formulaires et de communications interactives :** les concepteurs et développeurs peuvent créer et modifier des formulaires adaptatifs et des communications interactives, télécharger d’autres types de formulaires créés en externe, par exemple des formulaires créés dans Adobe Forms Designer, et gérer ces ressources à l’aide de la console de Gestionnaire de formulaires.
* **Publication de formulaires et de communications interactives :** les éléments hébergés sur une instance d’auteur peuvent être publiés sur une instance de publication pour exécuter des opérations d’exécution. La publication d’actifs utilise les fonctionnalités de réplication d’AEM. Adobe recommande qu’un agent de réplication soit configuré sur toutes les instances d’auteur pour transférer manuellement les formulaires publiés vers les instances de traitement, et qu’un autre agent de réplication soit configuré sur les instances de traitement avec le déclencheur *A réception* activé pour répliquer automatiquement les formulaires reçus afin de publier les instances.

**Publier :** une instance de publication est un serveur AEM Forms s’exécutant en mode d’exécution Publier standard. Les instances de publication sont destinées aux utilisateurs finaux des applications de formulaires (par exemple, les utilisateurs accédant à un site Web public et envoyant des formulaires). L’élément Publier active les fonctionnalités suivantes :

* Rendu et envoi de formulaires pour les utilisateurs finaux.
* Transmission des données de formulaire brutes envoyées aux instances de traitement pour un traitement supplémentaire et le stockage dans le système d’enregistrements final. L’implémentation par défaut fournie dans AEM Forms effectue cette opération à l’aide de la fonctionnalité de réplication inverse d’AEM. Un autre type d’implémentation est également disponible pour transférer directement les données du formulaire aux serveurs de traitement au lieu de les enregistrer localement d’abord (cette dernière étape constituant un prérequis pour l’activation de la réplication inverse). Les clients qui s’inquiètent de l’enregistrement de données potentiellement sensibles sur les instances de publication peuvent procéder à cette [mise en oeuvre alternative](/help/forms/using/configuring-draft-submission-storage.md), puisque les instances de traitement se trouvent généralement dans une zone plus sécurisée.
* Rendu et envoi de communications et de lettres interactives : Une communication et une lettre interactives sont rendues sur les instances de publication et les données correspondantes sont envoyées aux instances de traitement pour enregistrement et post-traitement. Les données peuvent être sauvegardées localement sur une instance de publication et traitées par réplication inverse vers une instance de traitement (l’option par défaut) ultérieurement, ou directement transférées vers l’instance de traitement sans enregistrement sur l’instance de publication. Cette dernière implémentation est utile pour les clients soucieux de leur sécurité.

**Traitement :** instance d’AEM Forms s’exécutant en mode d’exécution Auteur sans utilisateurs affectés au groupe de gestionnaires de formulaires. Vous pouvez déployer AEM Forms on JEE ou AEM Forms sur OSGi en tant qu’instance de traitement. Les utilisateurs ne sont pas affectés pour s’assurer que les activités de création et de gestion de formulaires ne sont pas exécutées sur l’instance de traitement et se produisent uniquement sur l’instance d’auteur. Une instance de traitement permet les fonctionnalités suivantes :

* **Traitement des données de formulaire brutes provenant d’une instance de publication :** Cette opération est effectuée principalement sur une instance de traitement via des workflows AEM qui se déclenchent à l’arrivée des données. Les workflows peuvent utiliser l’étape Modèle de données de formulaire fournie prêt à l’emploi pour archiver les données ou le document dans un magasin de données approprié.
* **Stockage sécurisé des données de formulaire :** l’élément Traitement fournit un référentiel derrière le pare-feu pour les données de formulaire brutes qui sont également isolées des utilisateurs. Ni les concepteurs de formulaires sur l’instance d’auteur, ni les utilisateurs finaux sur l’instance de publication ne peuvent accéder à ce référentiel.

   >[!NOTE]
   >
   > Adobe recommande d’utiliser un magasin de données tiers pour enregistrer les données traitées finales au lieu d’utiliser le référentiel AEM.

* **Enregistrement et post-traitement des données de correspondance provenant d’une instance de publication :** AEM workflows effectuent le post-traitement facultatif des définitions de lettre correspondantes. Ces processus peuvent enregistrer les données finales traitées dans des magasins de données externes appropriés.

* **Hébergement** de Workspace HTML : Une instance de traitement héberge le frontal de Workspace HTML. L’espace de travail HTML fournit l’interface utilisateur pour l’affectation de tâche/groupe associée pour les processus de révision et d’approbation.

Une instance de traitement est configurée pour s’exécuter en mode d’exécution Auteur, car :

* Elle active la réplication inverse des données de formulaire brutes d’une instance de publication. Le gestionnaire d&#39;enregistrement de données par défaut requiert la fonction de réplication inverse.
* AEM Workflows, qui constituent le Principal moyen de traiter les données de formulaire brutes provenant d’une instance de publication, sont recommandés pour s’exécuter sur un système de style auteur.

## Exemples de topologies physiques pour AEM Forms on JEE {#sample-physical-topologies-for-aem-forms-on-jee}

Les topologies AEM Forms on JEE recommandées ci-dessous concernent principalement les clients effectuant une mise à niveau à partir d’un LiveCycle ou d’une version précédente de AEM Forms on JEE. Adobe recommande d&#39;utiliser AEM Forms sur OSGi pour les nouvelles installations. Une nouvelle installation d’AEM Forms on JEE n’est recommandée que pour l’utilisation des fonctionnalités Document Security et Process Management.

### Topologie d’utilisation des services de document ou des fonctionnalités de sécurité des documents {#topology-for-using-document-services-or-document-security-capabilities}

Les clients AEM Forms prévoyant d’utiliser uniquement des services de document ou des fonctionnalités de sécurité des documents peuvent avoir une topologie similaire à celle affichée ci-dessous. Cette topologie recommande l’utilisation d’une seule instance d’AEM Forms. Vous pouvez également créer une grappe ou une batterie de serveurs AEM Forms, si nécessaire. Cette topologie est recommandée lorsque la plupart des utilisateurs accèdent par programmation aux fonctionnalités du serveur AEM Forms et que l’intervention via l’interface utilisateur est minimale. La topologie s’avère utile pour le traitement par lots des opérations de document. Par exemple, utilisez le service de sortie pour créer quotidiennement des centaines de documents PDF non modifiables.

Bien que AEM Forms vous permette de configurer et d&#39;exécuter toutes les fonctionnalités à partir d&#39;un seul serveur, vous devez toutefois planifier la capacité, équilibrer la charge et configurer des serveurs dédiés pour des fonctionnalités spécifiques dans un environnement de production. Par exemple, pour un environnement qui utilise le service PDF Generator pour convertir des milliers de pages par jour et ajouter des signatures numériques afin de limiter l’accès aux documents, configurez des serveurs AEM Forms distincts pour le service PDF Generator et les fonctionnalités de signature numérique. Cela permet de fournir des performances optimales et de dimensionner les serveurs indépendamment les uns des autres.

![fonctions de base](assets/basic-features.png)

### Topologie pour l’utilisation de la gestion des processus AEM Forms {#topology-for-using-aem-forms-process-management}

Les clients AEM Forms qui prévoient d’utiliser les fonctionnalités de gestion des processus AEM Forms peuvent, par exemple, utiliser une topologie similaire à celle affichée ci-dessous dans Workspace HTML. Le serveur AEM Forms on JEE peut se trouver dans une configuration de serveur unique ou de grappe.

Si vous effectuez une mise à niveau à partir de LiveCycle ES4, cette topologie est étroitement liée à ce que vous avez déjà dans le LiveCycle, à l’exception de l’ajout d’AEM Author intégré à AEM Forms on JEE. De plus, il n’y a pas de changement dans les exigences de mise en grappe pour les clients effectuant une mise à niveau. Si vous utilisiez AEM Forms dans un environnement organisé en grappes, vous pouvez continuer avec la même chose dans AEM 6.5 Forms. Pour une nouvelle installation d’AEM Forms of JEE pour l’utilisation de Workspace HTML, l’exécution de l’instance d’auteur intégrée à l’environnement JEE AEM est une autre exigence.

Le magasin de données de formulaire est un magasin de données tiers utilisé pour stocker les données traitées finales des formulaires et des communications interactives. Il s’agit d’un élément facultatif dans la topologie. Vous pouvez également choisir de configurer une instance de traitement et d’utiliser son référentiel comme système d’enregistrement final, si nécessaire.

![topology_for_usinghtmlworkspace andformsapp](assets/topology_for_usinghtmlworkspaceandformsapp.png)

La topologie est recommandée aux clients qui prévoient d’utiliser le serveur AEM Forms on JEE pour des fonctionnalités de gestion de processus (HTML Workspace) sans utiliser de post-traitement, de formulaires adaptatifs, de formulaires HTML5 et de fonctionnalités de communication interactive.

### Topologie d’utilisation des formulaires adaptatifs, formulaires HTML5, capacités de communication interactive {#topology-for-using-adaptive-forms-html-forms-interactive-communication-capabilities}

Les clients AEM Forms prévoyant d’utiliser les fonctionnalités de capture de données AEM Forms, par exemple, les formulaires adaptatifs, les formulaires HTML5 et les formulaires PDF, peuvent avoir une topologie similaire à celle présentée ci-dessous. Cette topologie est également recommandée pour l’utilisation des capacités de communication interactive de AEM Forms.

![topologie-for-using-forms-osgi-modules](assets/topology-for-using-forms-osgi-modules.png)

Vous pouvez apporter les modifications/personnalisations suivantes à la topologie suggérée ci-dessus :

* L’utilisation d’Workspace HTML et d’une application AEM Forms requiert un auteur AEM ou une instance de traitement. Vous pouvez utiliser l’instance de création AEM intégrée au serveur AEM Forms on JEE au lieu de configurer un serveur de création AEM externe supplémentaire.
* Une instance d’auteur ou de traitement AEM n’est requise que pour les workflows orientés Forms sur OSGi, les formulaires adaptatifs, le portail de formulaires et les communications interactives.
* l&#39;interface utilisateur de l&#39;agent de communication interactive est généralement exécutée au sein de l&#39;entreprise. Ainsi, vous pouvez conserver un serveur de publication pour l’interface utilisateur de l’agent dans le réseau privé.
* AEM formulaires sur une instance OSGi intégrée au serveur AEM Forms on JEE peuvent également exécuter des workflows centrés sur Forms sur OSGi et les dossiers de contrôle.

## Exemples de topologies physiques pour AEM Forms on OSGi {#sample-physical-topologies-for-using-aem-forms-on-osgi}

### Topologie pour la capture de données, la communication interactive, le processus orienté formulaire sur les fonctionnalités OSGi {#topology-for-data-capture-interactive-communication-form-centric-workflow-on-osgi-capabilities}

Les clients AEM Forms prévoyant d’utiliser les fonctionnalités de capture de données AEM Forms, par exemple, les formulaires adaptatifs, les formulaires HTML5 et les formulaires PDF, peuvent avoir une topologie similaire à celle présentée ci-dessous. Cette topologie est également recommandée pour l’utilisation de la fonctionnalité de communications interactives et de processus basés sur l’utilisation de Forms on OSGi, par exemple pour utiliser la boîte de réception AEM et l’application AEM Forms pour les flux de processus métier.

![interactif-use-case-af-cm-osgi-workflow](assets/interactive-use-cases-af-cm-osgi-workflow.png)

### Topologie d’utilisation des fonctionnalités de dossier de contrôle pour le traitement par lots hors ligne {#topology-for-using-watched-folder-capabilities-for-offline-batch-processing}

Les clients AEM Forms qui envisagent d’utiliser des dossiers de contrôle pour le traitement par lots peuvent avoir une topologie similaire à celle affichée ci-dessous. La topologie affiche un environnement organisé en grappes, mais vous décidez d’utiliser une instance unique ou une batterie de serveurs AEM Forms en fonction de la charge. La source de données tierce est votre propre système d’enregistrement. Il agit comme une source d’entrée pour les dossiers de contrôle. La topologie affiche également la sortie sous la forme d’un fichier imprimé. Vous pouvez également stocker le contenu de sortie dans un système de fichiers, l’envoyer par courrier électronique et utiliser d’autres méthodes personnalisées pour utiliser les résultats.

![traitement par lot hors ligne-via-dossiers-de-contrôle](assets/offline-batch-processing-via-watched-folders.png)

### Topologie d’utilisation des fonctionnalités des services de document pour le traitement hors ligne basé sur l’API {#topology-for-using-document-services-capabilities-for-offline-api-based-processing}

Les clients AEM Forms prévoyant d’utiliser uniquement la fonctionnalité de services de document peuvent avoir une topologie similaire à celle affichée ci-dessous. Cette topologie recommande d’utiliser une grappe de serveurs AEM Forms on OSGi. Cette topologie est recommandée lorsque la plupart des utilisateurs accèdent par programmation aux fonctionnalités du serveur AEM Forms (à l’aide d’API) et que l’intervention via l’interface utilisateur est minimale. La topologie est très utile dans plusieurs cas de logiciels clients. Par exemple, plusieurs clients utilisant le service PDF Generator pour créer des documents PDF à la demande.

Bien qu’AEM Forms vous permette de configurer et d’exécuter toutes les fonctionnalités à partir d’un seul serveur, vous devez planifier la capacité, équilibrer la charge et configurer des serveurs dédiés pour des fonctionnalités spécifiques dans un environnement de production. Par exemple, pour un environnement utilisant le service PDF Generator pour convertir des milliers de pages par jour et plusieurs formulaires adaptatifs pour capturer des données, configurez des serveurs AEM Forms distincts pour le service PDF Generator et les fonctionnalités de formulaires adaptatifs. Cela permet de fournir des performances optimales et de dimensionner les serveurs indépendamment les uns des autres.

![traitement basé sur les api hors ligne](assets/offline-api-based-processing.png)

