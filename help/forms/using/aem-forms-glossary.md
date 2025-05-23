---
title: Glossaire AEM Forms
description: AEM Forms Glossary fournit une liste complète de termes, définitions et concepts clés utilisés dans Adobe Experience Manager Forms (AEM Forms) pour aider les utilisateurs à comprendre et à utiliser les formulaires adaptatifs et les fonctionnalités associées.
feature: Adaptive Forms
role: Admin, User, Developer
hidefromtoc: true
hide: true
source-git-commit: 37f471e09c13b7ab036ab1043d11dfed98da1d97
workflow-type: tm+mt
source-wordcount: '1773'
ht-degree: 2%

---

# Glossaire AEM Forms

## [Formulaires adaptatifs](https://experienceleague.adobe.com/fr/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/create-an-adaptive-form-on-forms-cs/creating-adaptive-form)

Formulaires dynamiques et réactifs qui ajustent leur mise en page et leur présentation en fonction de l’appareil et des entrées de l’utilisateur, améliorant ainsi l’expérience utilisateur sur différentes plateformes. Inclut la logique conditionnelle, la liaison de données dynamique et le comportement basé sur des règles.

## [Contrôle de version des formulaires adaptatifs](https://experienceleague.adobe.com/fr/docs/experience-manager-65/content/forms/adaptive-forms-core-components/add-versioning-reviews-comments)

Possibilité de gérer plusieurs versions d’un formulaire dans le référentiel, à l’aide du contrôle de version des nœuds JCR. Assure les pistes d’audit et une restauration facile des formulaires adaptatifs.

## [Intégration Adobe Analytics Forms](https://experienceleague.adobe.com/fr/docs/experience-manager-cloud-service/content/forms/integrate/services/enable-adobe-analytics-adaptive-form-using-experience-cloud-setup-automation)

Fournit des informations détaillées sur les interactions utilisateur (par exemple, abandons de champs, temps passé par section) à l’aide d’Adobe Analytics, ce qui permet une optimisation de la conception de formulaire pilotée par les données.

## [Package De Module Complémentaire AEM Forms](https://experienceleague.adobe.com/fr/docs/experience-manager-65/content/forms/install-aem-forms/osgi-installation/installing-configuring-aem-forms-osgi)

Application déployée dans Adobe Experience Manager (AEM) sous la forme d’un package contenant des services (fournisseurs d’API) et des servlets ou des JSP gérés par le framework AEM Sling.

## [AEM Forms sur JEE](https://experienceleague.adobe.com/fr/docs/experience-manager-65/content/forms/install-aem-forms/jee-installation/aem-forms-jee-supported-platforms)

Une option de déploiement d’AEM Forms qui utilise les serveurs Java Enterprise Edition (JEE), offrant une évolutivité au niveau de l’entreprise, une gestion des transactions et une prise en charge des workflows d’entreprise complexes.

## [AEM Forms sur OSGi](https://experienceleague.adobe.com/fr/docs/experience-manager-65/content/implementing/deploying/introduction/technical-requirements)

AEM Forms dans l’environnement OSGi est un environnement de création AEM standard ou AEM Publish sur lequel est déployé le package AEM Forms. Vous pouvez exécuter AEM Forms sur OSGi dans des configurations à serveur unique, en batterie et en grappes. La mise en grappe n’est disponible que pour les instances dʼauteur AEM.

## [Adobe Sign dans AEM Forms](https://experienceleague.adobe.com/fr/docs/experience-manager-65/content/forms/adaptive-forms-advanced-authoring/adobe-sign-integration-adaptive-forms)

Service RESTful pour des workflows de signature numérique sécurisés et transparents. Il s’intègre à AEM Forms à l’aide de l’authentification basée sur OAuth, ce qui permet d’automatiser les collections de signatures et le suivi en temps réel.

## [AEM Forms Document Services 6.5](https://experienceleague.adobe.com/fr/docs/experience-manager-65/content/forms/use-document-services/overview-aem-document-services)

API fournies par la couche web d’AEM Forms pour une consommation à distance par les clients HTTP, comme les SDK mobiles de formulaires.Fonctionnalités d’AEM Forms permettant la création, l’assemblage, la distribution et l’archivage de documents de PDF, l’ajout de signatures numériques et le décodage de Forms à code-barres.

| **Nom du service** | **Description** | **Lien vers la documentation** |
|------------------------------|---------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------|
| **Service Forms** | Effectuez le rendu des PDF forms à l’aide de modèles et de code XML, intégrez les données de formulaire pour l’importation/exportation et prenez en charge le rendu basé sur les fragments. | [Documentation du service Forms](https://experienceleague.adobe.com/fr/docs/experience-manager-65/content/forms/use-document-services/output-service) |
| **Service Output** | Génère des documents en fusionnant des données avec des modèles dans des formats tels que PDF, PCL ou PostScript. | [Documentation du service Output](https://experienceleague.adobe.com/fr/docs/experience-manager-65/content/forms/use-document-services/output-service) |
| **Service Assembler** | Combine, réorganise, valide et enrichit les documents PDF et XDP. | [Documentation du service Assembler](https://experienceleague.adobe.com/fr/docs/experience-manager-65/content/forms/use-document-services/assembler-service) |
| **Service ConvertPDF** | Convertit des documents PDF en formats PostScript ou image tels que PNG, JPEG ou TIFF. | [Documentation du service ConvertPDF](https://experienceleague.adobe.com/fr/docs/experience-manager-65/content/forms/use-document-services/using-convertpdf-service) |
| **Service Barcoded Forms** | Extrait les données des codes à barres dans les fichiers de TIFF et de PDF pour automatiser les processus de capture de données. | [Documentation du service Barcoded Forms](https://experienceleague.adobe.com/fr/docs/experience-manager-65/content/forms/use-document-services/using-barcoded-forms-service) |
| **Service DocAssurance** | Chiffre, déchiffre, signe numériquement et applique des politiques Document Security aux PDF. | [Documentation du service DocAssurance](https://experienceleague.adobe.com/fr/docs/experience-manager-65/content/forms/use-document-services/overview-aem-document-services#doc-assurance-service) |
| **Service PDF Generator** | Convertit des formats de fichiers natifs (par exemple : Microsoft Word, Excel) en documents de PDF. | [Documentation du service PDF Generator](https://experienceleague.adobe.com/fr/docs/experience-manager-65/content/forms/use-document-services/aem-document-services-programmatically#pdfgeneratorservice) |

## [API de communication Forms as a Cloud Service](https://experienceleague.adobe.com/fr/docs/experience-manager-cloud-service/content/forms/using-communications/aem-forms-cloud-service-communications-introduction)

AEM Forms as a Cloud Service fournit des outils avancés pour gérer les formulaires et les workflows de communication, en prenant en charge la création transparente de formulaires numériques, la capture de données et les communications personnalisées. Les API de communication cloud fournissent la génération, la manipulation, la validation et l’intégration sécurisées de documents à la demande et par lots à des systèmes externes via HTTP, garantissant ainsi des opérations rationalisées et sécurisées.

| **Nom du service** | **Description** | **Lien vers la documentation** |
|-------------------------------|------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------|
| **Génération de documents** | Combinez un modèle (XFA ou PDF) avec des données XML pour générer des documents aux formats PDF et d’impression tels que PS, PCL, DPL, IPL et ZPL. | [Documentation sur la génération de documents](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/using-communications/aem-forms-cloud-service-communications-introduction.html?lang=fr#document-generation) |
| **Manipulation de documents** | Combiner et réorganiser des documents PDF. | [Documentation sur la manipulation de documents](https://experienceleague.adobe.com/fr/docs/experience-manager-cloud-service/content/forms/using-communications/aem-forms-cloud-service-communications-introduction#document-manipulation) |
| **Conversion de documents** | Convertissez un PDF en PDF PDF/A et vérifiez sa conformité. | [Documentation sur la conversion de documents](https://experienceleague.adobe.com/fr/docs/experience-manager-cloud-service/content/forms/using-communications/aem-forms-cloud-service-communications-introduction#document-conversion) |
| **Document Assurance** | Ajouter ou supprimer des champs de signature, signer, certifier, chiffrer, déchiffrer et appliquer des droits d’utilisation aux documents de PDF. | [Documentation sur Document Assurance](https://experienceleague.adobe.com/fr/docs/experience-manager-cloud-service/content/forms/using-communications/aem-forms-cloud-service-communications-introduction#doc-assurance) |
| **Signatures numériques** | Intègre Adobe Sign pour une signature électronique sécurisée des formulaires et documents. | [Documentation sur les signatures numériques](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/using-communications/aem-forms-cloud-service-communications-introduction.html?lang=fr#digital-signatures) |


## [AEM Forms Workbench](https://experienceleague.adobe.com/fr/docs/experience-manager-65/content/forms/install-aem-forms/jee-installation/install-workbench)

Application de bureau permettant de créer, modifier et déployer des processus, ainsi que de gérer des processus métier basés sur l’utilisation de Forms. Il permet l’intégration aux services et systèmes back-end.

## [Archétype](https://experienceleague.adobe.com/fr/docs/experience-manager-core-components/using/developing/archetype/overview)

Modèle ou patron dans AEM utilisé pour générer un nouveau projet avec une structure prédéfinie, ce qui facilite la normalisation, la configuration rapide et le respect des bonnes pratiques de développement AEM.

## [Instance d’auteur](https://experienceleague.adobe.com/fr/docs/experience-manager-65/content/forms/publish-process-aem-forms/publishing-unpublishing-forms)

Environnement dans lequel les créateurs et les administrateurs de contenu conçoivent, créent et gèrent du contenu avant de le publier. Prend en charge le contrôle de version, la prévisualisation et le test.

## [Frontend de création](https://experienceleague.adobe.com/fr/docs/experience-manager-65/content/forms/install-aem-forms/aem-forms-architecture-deployment#architecture)

Interface utilisateur de création et de gestion de formulaires dans AEM Forms.

## [Bloc de formulaire adaptatif](https://experienceleague.adobe.com/fr/docs/experience-manager-cloud-service/content/edge-delivery/build-forms/forms-references/form-components)

Unité d’encapsulation qui regroupe logiquement les composants et métadonnées associés, permettant une gestion dynamique des données et une évolutivité facile dans des formulaires à plusieurs étapes.

## [Composants principaux](https://experienceleague.adobe.com/fr/docs/experience-manager-core-components/using/adaptive-forms/introduction)

Blocs de création réutilisables prêts à l’emploi pour la création de formulaires, y compris les champs de formulaire, les conteneurs de mises en page, les boutons et autres éléments interactifs.

## [Gestion des correspondances](https://experienceleague.adobe.com/fr/docs/experience-manager-65/content/forms/letters-correspondences/cm-overview)

Module qui permet aux entreprises de créer, gérer et diffuser une correspondance personnalisée à l’aide de modèles, de règles et de sources de données prédéfinis. Inclut des modèles de lettre, des communications client et la génération de lots.

## [CRX (Content repository extreme)](https://experienceleague.adobe.com/fr/docs/experience-manager-65/content/forms/use-aem-forms-workspace/html-workspace-architecture)

Le référentiel de contenu Java (JCR) intégré d’AEM qui stocke les données structurées et non structurées, ce qui permet le stockage hiérarchique du contenu, des modèles et des configurations.

## [Composant personnalisé](https://experienceleague.adobe.com/fr/docs/experience-manager-core-components/using/adaptive-forms/customize-adaptive-forms-core-components)

Composant personnalisé qui étend les fonctionnalités d’AEM Forms, développé à l’aide des modèles Sling, Sightly (HTL) et Java. Généralement utilisé pour une logique commerciale unique ou une interactivité côté client avancée.

## [Custom XCI (informations de configuration XML)](https://experienceleague.adobe.com/fr/docs/experience-manager-65/content/forms/administrator-help/configure-forms/specifying-xci-configuration-options)

Dans Adobe Experience Manager (AEM) Forms, un fichier XCI personnalisé (informations de configuration XML) permet aux administrateurs de définir des propriétés de rendu spécifiques pour les formulaires et les documents. En configurant les paramètres XCI dans la console d’administration, vous pouvez remplacer les valeurs par défaut du système par des options personnalisées, ce qui garantit un traitement et une présentation personnalisés des formulaires.

## [Intégration de données](https://experienceleague.adobe.com/fr/docs/experience-manager-65/content/forms/form-data-model/data-integration)

Intégration transparente de sources de données externes, telles que des bases de données, des services web ou des API REST, dans des formulaires et des workflows pour offrir des expériences utilisateur dynamiques et personnalisées.

## [Sources de données](https://experienceleague.adobe.com/fr/docs/experience-manager-65/content/forms/form-data-model/configure-data-sources)

Interfaces d’intégration de données externes dans des formulaires, notamment JDBC pour les bases de données relationnelles, les points d’entrée REST pour les services web et OData pour les systèmes SAP. Géré via la structure d’intégration de données AEM Forms.

## [ Fragments de document ](https://experienceleague.adobe.com/fr/docs/experience-manager-65/content/forms/letters-correspondences/lists)

Composants réutilisables de documents, tels que des en-têtes, des pieds de page, des clauses de non-responsabilité ou des clauses, qui peuvent être inclus dynamiquement dans des formulaires ou des correspondances pour garantir la cohérence.

## [Document d’enregistrement (DE)](https://experienceleague.adobe.com/fr/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/generate-document-of-record-for-non-xfa-based-adaptive-forms)

Une fonctionnalité d’AEM Forms qui génère une version d’archivage non modifiable d’un formulaire envoyé, généralement au format PDF, tout en conservant le contenu et la mise en page exacts comme enregistrement de la transaction.

## [Edge Delivery Services ](https://experienceleague.adobe.com/fr/docs/experience-manager-cloud-service/content/edge-delivery/overview)

Diffusion de contenu optimisée pour AEM Forms, ce qui réduit la latence des ressources telles que les formulaires, les thèmes et les bibliothèques clientes, où les auteurs et autrices peuvent mettre à jour et publier du contenu rapidement.

## [Intégration de Forms](https://experienceleague.adobe.com/fr/docs/experience-manager-65/content/forms/form-data-model/data-integration)

implique la connexion d’AEM Forms aux systèmes d’entreprise (par exemple, SAP, Salesforce) à l’aide de lots et de connecteurs OSGi, la prise en charge de flux de données bidirectionnels et de mises à jour en temps réel.

## [Révision de formulaire](https://experienceleague.adobe.com/fr/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/create-reviews-forms)

Fonctionnalité axée sur les workflows permettant aux parties prenantes de passer en revue les formulaires adaptatifs, d’ajouter des annotations et d’approuver les modifications avant publication. Utilise la boîte de réception AEM et la gestion des tâches.

## [Modèle de données de formulaire (FDM)](https://experienceleague.adobe.com/fr/docs/experience-manager-cloud-service/content/forms/integrate/use-form-data-model/using-form-data-model)

Une couche de représentation qui connecte les formulaires adaptatifs aux sources de données principales, ce qui permet l’intégration aux services web RESTful, aux services SOAP et OData. FDM permet aux auteurs de formulaires de mapper directement les champs de formulaire aux structures de données principales, assurant ainsi une synchronisation transparente des entrées utilisateur avec les systèmes externes.

## [Localisation du formulaire](https://experienceleague.adobe.com/fr/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/supporting-new-language-localization)

Processus des formulaires adaptatifs visant à prendre en charge plusieurs langues et paramètres régionaux, en veillant à ce que les formulaires soient accessibles et conviviaux pour une audience diversifiée.

## [ Portail Formulaires ](https://experienceleague.adobe.com/fr/docs/experience-manager-65/content/forms/use-forms-portal/creating-form-portal-page)

Les composants du portail Forms dotent les développeurs Web de composants pour créer et personnaliser un portail Forms sur les sites web créés à l’aide de Adobe Experience Manager (AEM). Il permet aux utilisateurs et utilisatrices de découvrir des formulaires, d’y accéder et de les envoyer efficacement sur les plateformes web et mobiles.

## [Rendu de formulaire et envoi Frontend](https://experienceleague.adobe.com/fr/docs/experience-manager-65/content/forms/install-aem-forms/aem-forms-architecture-deployment#architecture)

Interface utilisateur finale d’AEM Forms qui permet aux utilisateurs et utilisatrices d’afficher et d’envoyer des formulaires via un navigateur web.

## [Jeux de formulaires](https://experienceleague.adobe.com/fr/docs/experience-manager-65/content/forms/html5-forms/formset-in-aem-forms)

Ensemble de formulaires associés regroupés pour être présentés sous la forme d’une entité unique aux utilisateurs, ce qui permet de diviser les processus complexes de collecte de données en sections gérables.

## [Forms Designer](https://experienceleague.adobe.com/fr/docs/experience-manager-cloud-service/content/forms/using-communications/installing-configuring-designer)

Application autonome utilisée pour concevoir le modèle de formulaires dans un formulaire XDP et l’utiliser dans votre AEM Forms pour générer un document d’enregistrement.

## [Workflow centré sur Forms](https://experienceleague.adobe.com/fr/docs/experience-manager-65/content/forms/workflows/aem-forms-workflow)

Ensemble d’étapes automatisées ou manuelles dans AEM Forms qui gèrent les processus d’entreprise, tels que la validation de documents, la publication de contenu ou les notifications d’utilisateur.

## [Communication interactive](https://experienceleague.adobe.com/fr/docs/experience-manager-65/content/forms/getting-started/interactive-communications-overview)

Implémentation personnalisée pour la gestion des communications multicanaux hautement personnalisées. Il combine des données provenant de diverses sources, telles que les systèmes CRM ou ERP, pour fournir des communications sur plusieurs formats tels que le web, les appareils mobiles, les e-mails et l’impression.

## [JCR (Java Content Repository)](https://experienceleague.adobe.com/fr/docs/experience-manager-learn/cloud-service/underlying-technology/introduction-jcr)

Référentiel hiérarchique normalisé destiné au stockage de contenu, de configurations et de métadonnées dans AEM, prenant en charge le stockage structuré et non structuré des données.

## [Lettres](https://experienceleague.adobe.com/fr/docs/experience-manager-65/content/forms/letters-correspondences/create-letter#create-a-letter-template)

Communication client générée à l’aide d’AEM Forms Document Services. Les lettres sont créées à l’aide d’une combinaison de modèles XDP, de modèles de données et de fragments réutilisables, ce qui garantit leur évolutivité dans les scénarios de volume élevé.

## [ Métadonnées dans AEM Forms ](https://experienceleague.adobe.com/fr/docs/experience-manager-65/content/forms/manage-administer-aem-forms/manage-form-metadata)

Les métadonnées permettent une catégorisation et une récupération efficaces des ressources. AEM Forms comprend des métadonnées prédéfinies pour chaque type de ressource et permet une personnalisation. Il fournit également des outils pour créer, gérer et exchange facilement des métadonnées.

## [PDF Generator](https://experienceleague.adobe.com/fr/docs/experience-manager-learn/forms/document-services/using-pdfg-in-aem-forms)

Outil d’AEM Forms qui convertit différents formats de fichiers (par exemple : Word, Excel, PowerPoint) en documents PDF et fournit des fonctionnalités telles que le chiffrement, l’ajout d’un filigrane et la fusion.

## [Instance de publication](https://experienceleague.adobe.com/fr/docs/experience-manager-65/content/forms/publish-process-aem-forms/publishing-unpublishing-forms)

L’environnement dans AEM qui diffuse du contenu en direct aux utilisateurs finaux. Il fournit des formulaires, des pages et d’autres expériences digitales avec des performances optimisées.

## [Éditeur de règles](https://experienceleague.adobe.com/fr/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-core-components/create-an-adaptive-form-on-forms-cs/rule-editor-core-components/rule-editor-core-components)

Outil visuel dans le Forms adaptatif qui permet aux auteurs de définir des règles et une logique personnalisées pour les champs de formulaire, comme la visibilité, la validation et le préremplissage de données, sans avoir à recourir à une expertise en codage.

## [Signatures Scribble](https://experienceleague.adobe.com/fr/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/add-components-to-an-adaptive-form/signing-forms-using-scribble)

Fonction d’AEM Forms permettant aux utilisateurs de signer électroniquement des formulaires en y dessinant directement leur signature à l’aide d’une souris ou d’un appareil tactile.

## [Action Envoyer dans AEM Forms](https://experienceleague.adobe.com/fr/docs/experience-manager-65/content/forms/adaptive-forms-basic-authoring/configuring-submit-actions)

Actions côté serveur ou côté client exécutées lors de l’envoi du formulaire. Par exemple, les appels d’API REST, l’appel d’un workflow ou l’écriture de données dans un JCR (Java Content Repository).

## [Thèmes](https://experienceleague.adobe.com/fr/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-core-components/create-an-adaptive-form-on-forms-cs/using-themes-in-core-components)

Structures de style pilotées par CSS appliquées aux formulaires adaptatifs, utilisant LESS/SASS pour les préprocesseurs. Les thèmes garantissent la conformité aux directives de marque et aux normes d’accessibilité. Vous pouvez personnaliser un thème, modifier ses éléments de conception, sa disposition, ses couleurs, sa typographie et parfois le code sous-jacent.

## [Modèle](https://experienceleague.adobe.com/fr/docs/experience-manager-core-components/using/adaptive-forms/sample-themes-templates-form-data-models-core-components)

Les plans directeurs pour les formulaires adaptatifs, comprenant des éléments structurels (champs, mises en page) et des scripts préconfigurés, vous pouvez créer et personnaliser de nouveaux modèles ou utiliser des modèles prêts à l’emploi existants.

## [Couche Web](https://experienceleague.adobe.com/fr/docs/experience-manager-65/content/forms/install-aem-forms/aem-forms-architecture-deployment#architecture)

Comprend des JSP ou des servlets créés sur des services communs et de formulaires, fournissant des fonctionnalités telles que la création front-end, le rendu de formulaire et l’envoi front-end, ainsi que des API REST.

## [XDP (package de données XML)](https://experienceleague.adobe.com/fr/docs/experience-manager-65/content/forms/manage-administer-aem-forms/get-xdp-pdf-documents-aem)

Format de fichier utilisé dans AEM Forms pour concevoir et structurer des formulaires, permettant leur rendu en tant que PDF ou HTMLS tout en prenant en charge le contenu dynamique et l’interactivité.

## [XFA (XML Forms Architecture)](https://experienceleague.adobe.com/fr/docs/experience-manager-65/content/forms/adaptive-forms-basic-authoring/creating-adaptive-form#create-an-adaptive-form-based-on-an-xfa-form-template)

Une technologie héritée pour créer des PDF forms interactifs et dynamiques. Les formulaires XFA permettent des fonctionnalités avancées, telles que les ajustements de disposition dynamiques, les scripts et l’intégration transparente aux systèmes principaux.

## [Schéma XML ou JSON](https://experienceleague.adobe.com/fr/docs/experience-manager-65/content/forms/adaptive-forms-basic-authoring/creating-adaptive-form#create-an-adaptive-form-based-on-xml-or-json-schema)

Structure normalisée utilisée pour définir le format et l’organisation des données XML ou JSON dans les formulaires et les workflows. Ces schémas assurent une gestion cohérente des données et permettent l’interopérabilité avec des systèmes externes.

<!--

## **Custom Properties**  

Developer-defined metadata attributes added to components or forms for advanced behaviors, accessed via Sling APIs or Groovy scripts for dynamic processing.

## **Embedding** 

Integrating adaptive forms into AEM Sites or external web pages using `<iframe>` or SPA (Single Page Application) models. Embedding supports seamless session handling and cross-origin resource sharing (CORS).

## **CDN (Content Delivery Network)**  

Distributed networks (e.g., Akamai) used for caching and delivering forms-related resources, ensuring high availability and faster load times for geographically distributed users.


## **Dispatcher**  

An AEM caching and load balancing tool configured to optimize delivery of adaptive forms. Its filter rules ensure secure access control while caching frequently accessed forms and assets.

## **Editors**  

Tools like the Adaptive Forms Editor, Theme Editor, and Rule Editor, enabling developers and content authors to customize forms and their behavior without extensive coding.

## **Responsive UI**  

An implementation of media queries and flexible grids, ensuring adaptive forms render seamlessly across various screen sizes and devices.

## **Custom Functions**  

JavaScript-based utilities or REST microservices that provide additional logic (e.g., complex field validation or data pre-population), extending the out-of-the-box capabilities of AEM Forms.

## **Package Manager**  

AEM's CRX Package Manager facilitates importing/exporting adaptive forms, data schemas, or configurations as .zip files, enabling modular deployment in distributed environments.

## **UE (User Experience)**  

Design principles and optimizations applied in AEM Forms to enhance usability, including accessibility features (ARIA roles, tab navigation) and intuitive layouts.

## **Forms Submission Services**

Back-end services for handling form submissions, integrating with the AEM Workflow engine, third-party APIs, or direct JCR persistence.


Foundation components
e-signing
adobe sign
letters
submit action
data sources
adaptive form block
edge delivery services
forms integration
custom component 
themes
template 
custom properties
embedding
CDN
Dispatcher
editors
responsive UI
custom functions
package manager
communication APIs
UE
Forms submission services
Form review
Forms Versioning
Adobe analytics forms integration specific

## **AEM Forms Foundation Components**  
Core reusable elements within AEM Forms, built on Granite UI, enabling developers to create complex forms. They provide robust features like data bindings, field validations, and support for multilingual content.


## **e-Signing**  
An implementation of digital signature standards (e.g., PKCS #7) within AEM Forms, integrated with Adobe Sign APIs to ensure secure and legally binding electronic signatures.

## Workspace

A browser-based interface for users to interact with AEM Forms workflows, tasks, and approvals.

## Sling

A REST-based web framework used in AEM to map request URLs to content resources, enabling efficient content rendering and delivery.

-->