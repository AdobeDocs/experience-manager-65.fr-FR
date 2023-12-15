---
title: Résumé des nouvelles fonctionnalités | AEM 6.5 Forms
description: Dernières fonctionnalités et améliorations apportées aux formulaires et documents AEM, la solution de gestion de l’expérience numérique la plus avancée au monde.
topic-tags: introduction
products: SG_EXPERIENCEMANAGER/6.5/FORMS
docset: aem65
exl-id: 47b9de1f-b16a-424c-b8b4-e9d7b3dcca86
source-git-commit: 9b18d92ffabc141e83ba9a7c3694257d3dee1ea1
workflow-type: ht
source-wordcount: '637'
ht-degree: 100%

---

# Résumé des nouvelles fonctionnalités | AEM 6.5 Forms{#new-features-summary-aem-forms}

| Produit | Adobe Experience Manager 6.5 |
| -------- | ---------------------------- |
| Version | 6.5.19.0 |
| Type | Mise à jour du pack de services |
| Date | Vendredi 8 décembre 2023 |

## Éléments inclus dans Adobe Experience Manager 6.5 Forms Pack de services 19 (6.5.19.0)

Experience Manager 6.5.19.0 comprend de nouvelles fonctionnalités, des améliorations importantes demandées par les clientes et les clients, des correctifs de bugs ainsi que des améliorations en termes de performances, de stabilité et de sécurité, publiés depuis la version initiale 6.5 d’avril 2019. [Installez ce Pack de services](https://experienceleague.adobe.com/docs/experience-manager-65/release-notes/aem-forms-current-service-pack-installation-instructions.html?lang=fr) sur Experience Manager 6.5.

### Nouvelles fonctionnalités

#### Nouveaux composants principaux des formulaires adaptatifs

Des onglets verticaux, des conditions générales et une case à cocher sont ajoutés afin d’améliorer l’évolutivité des formulaires.

* **[Composant Case à cocher](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/checkbox.html?lang=fr)** : les formulaires adaptatifs basés sur les composants principaux peuvent désormais inclure un composant de case à cocher. Il permet aux utilisateurs et utilisatrices de faire des choix binaires, en sélectionnant ou en désélectionnant une option particulière. Il s’affiche généralement sous la forme d’une petite case sur laquelle vous pouvez cliquer ou appuyer pour basculer entre deux états : cochée et décochée. La case à cocher est un élément de formulaire courant, utilisé pour présenter un choix oui/non ou vrai/faux.

* **[Composant Conditions générales](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/terms-and-conditions.html?lang=fr)** : les formulaires adaptatifs basés sur les composants principaux peuvent désormais inclure un composant Conditions générales. Il permet aux personnes créant les formulaires d’introduire une section spécifique dans le formulaire, dans laquelle les utilisateurs et utilisatrices peuvent consulter les conditions générales ou les accords juridiques associés à l’utilisation d’un service, d’un produit ou d’une plateforme. Ce composant est conçu pour informer les utilisateurs et utilisatrices des règles, des réglementations et des obligations qu’ils acceptent en envoyant le formulaire.

  ![Composants Onglets verticaux, Conditions générales et Case à cocher.](/help/forms/using/assets/forms-components.png)

* **[Composant Onglets verticaux](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/adaptive-forms-components/vertical-tabs.html?lang=fr)** : les formulaires adaptatifs basés sur les composants principaux peuvent désormais organiser le contenu des formulaires en une liste verticale d’onglets, ce qui assure une disposition structurée et navigable. L’utilisation d’onglets verticaux dans un formulaire peut améliorer l’expérience globale de l’utilisateur ou de l’utilisatrice en simplifiant la navigation et en améliorant l’organisation du contenu du formulaire, en particulier lorsqu’un formulaire contient plusieurs sections ou des informations complexes.

#### Version 64 bits d’AEM Forms Designer

La [version 64 bits d’AEM Forms Designer](/help/forms/using/installing-configuring-designer.md) offre des performances, une évolutivité et une gestion de la mémoire améliorées pour optimiser votre expérience de création de formulaires. Grâce à l’architecture 64 bits, vous pouvez aborder facilement des projets plus volumineux et plus complexes, assurant ainsi des workflows de conception transparents et une efficacité optimisée. Améliorez encore vos capacités de conception de formulaire et accueillez l’avenir d’AEM Forms Designer avec cette version de pointe.

#### Connexion de formulaires adaptatifs à une liste Microsoft® SharePoint

AEM Forms fournit une intégration prête à l’emploi pour [envoyer des données de formulaire directement à la liste SharePoint](/help/forms/using/configuring-submit-actions.md#submit-to-microsoft&reg;-sharepoint-list), ce qui vous permet d’utiliser les fonctionnalités des listes SharePoint. Vous pouvez configurer une liste Microsoft® SharePoint comme source de données pour un modèle de données de formulaire et utiliser l’action Envoyer à l’aide du modèle de données de formulaire pour connecter un formulaire adaptatif à la liste SharePoint.

#### Prise en charge de la configuration des propriétés de document d’enregistrement pour les fragments de formulaire adaptatif

Vous pouvez maintenant facilement [personnaliser vos fragments de formulaire adaptatif et ses champs dans l’éditeur de formulaires adaptatifs](/help/forms/using/generate-document-of-record-for-non-xfa-based-adaptive-forms.md).

#### Inclut la version 64 bits de XMLFM

L’itération 64 bits de XMLFM améliore les performances, l’évolutivité et la gestion de la mémoire. Il s’agit du premier service natif 64 bits déployé côté serveur. En exploitant sa capacité inhérente à accéder à des ressources de mémoire considérablement plus importantes par rapport à son équivalent 32 bits, XMLFM 64 bits permet une gestion transparente des charges de travail de rendu plus importantes. Ce jalon représente non seulement un bond en avant en termes de performances, mais il introduit également des améliorations clés de la structure de service native dans le serveur AEM Forms. Cette mise à jour permet au serveur AEM Forms de prendre en charge n’importe quel service natif 64 bits en toute transparence.



## Correctifs

Cette version comprend également des correctifs pour plus de 20 problèmes signalés par des clientes et clients. Pour obtenir la liste détaillée des correctifs inclus dans le Pack de services, voir les [notes de mise à jour](https://experienceleague.adobe.com/docs/experience-manager-65/release-notes/release-notes.html?lang=en#forms-6519?lang=fr).


## Installer le Pack de services

Le Pack de services apporte de nouvelles fonctionnalités et des correctifs de bugs pour AEM Forms on JEE et AEM Forms on OSGi. Les instructions d’installation présentent des modifications par rapport aux Packs de service précédents. Pour obtenir des instructions d’installation, voir les [instructions d’installation du Pack de services AEM Forms](https://experienceleague.adobe.com/docs/experience-manager-65/release-notes/aem-forms-current-service-pack-installation-instructions.html?lang=fr).






<!-- 
## Transaction Reports {#transaction-reports}



Transaction reports lets you capture and track the number of submitted forms, processed documents, and rendered documents. The objective behind tracking these transactions is to make an informed decision about the product usage and rebalancing investments in hardware and software. Some examples of transactions include:

* Submission of an Adaptive Form, an HTML5 Form, or a Form Set
* Rendition of a print or a web version of an interactive communication
* Conversion of a document from one file format to another

For information about configuring and using transaction reports, see [Transaction Reports Overview](../../forms/using/transaction-reports-overview.md).

![A sample transaction report](assets/surface_transaction_reporting.png)

## Interactive Communications {#interactive-communications}

**Define data display patterns**

Interactive Communication authors can now define [data display patterns](create-interactive-communication.md#datadisplaypatterns) for fields, variables, and form data model elements. For example, date, currency, or phone formats.

**Use new types of charts**

You can now add [Quadrant charts and charts with multiple series](../../forms/using/chart-component-interactive-communications.md) to Interactive Communications.

**Sort columns in a table**

You can now [sort columns of a table](../../forms/using/create-interactive-communication.md#sortcolumns) in the Interactive Communication. You can bind and sort table columns with static text or data model objects.

**Use new components in a web channel**

You can now add Button and Separator components to the web channel. For more information, see [Add Button component to the web channel](../../forms/using/create-interactive-communication.md#add-button-component-to-the-web-channel) and [Separator component in web channel](../../forms/using/create-interactive-communication.md#separatorcomponent).

**Layout mode to resize components**

You can now switch to [Layout mode](../../forms/using/resize-using-layout-mode.md) to resize components in the Web channel using a WYSIWYG interface.

**Usability improvements**

Interactive Communication authors can now utilize various easy-to-use operations while creating correspondences. The list of operations includes:

* [Perform undo-redo actions in print and web channels](../../forms/using/create-interactive-communication.md#undoredoactions)
* [Add variables in a document fragment using @ symbol](../../forms/using/texts-interactive-communications.md#searchvariables)
* [Add data model elements in a document fragment using @ symbol](../../forms/using/texts-interactive-communications.md#searchdatamodelproperties)
* [Delete or add a web channel to an existing Interactive Communication](../../forms/using/create-interactive-communication.md#edit-interactive-communication-properties)
* [Bind data source elements with fields and variables using drag-and-drop actions](../../forms/using/create-interactive-communication.md#binddatasourceelements)
* [Highlight unbound fields and variables while authoring Interactive Communication](../../forms/using/create-interactive-communication.md#distinguishunboundfields)
* [Perform additional actions such as copy, group, or more on inherited components in a web channel](../../forms/using/create-interactive-communication.md#componenttoolbar)

**Improvements in sync process**

There are several improvements in the Web channel layout auto-generated using the Print channel.

![Interactive Communications Charts](assets/interactive-communication-charts.png)

## Adaptive Forms {#adaptive-forms}

### Use Adobe Sign's cloud-based digital signatures in Adaptive Forms {#use-adobe-sign-s-cloud-based-digital-signatures-in-adaptive-forms}

[Cloud-based digital signatures](https://helpx.adobe.com/sign/kb/digital-certificate-providers.html) or remote signatures are a new generation of digital signatures that work across desktop, mobile, and the web — and meet the highest levels of compliance and assurance for signer authentication. You can now [sign an Adaptive Form](../../forms/using/working-with-adobe-sign.md) with Cloud-based digital signatures.

#### Embed an Adaptive Form or Interactive Communication in AEM Sites Single Page Applications {#embed-an-adaptive-form-or-interactive-communcation-in-aem-sites-single-page-applications}

AEM Forms lets you [seamlessly embed an Adaptive Form](../../forms/using/embed-adaptive-form-aem-sites-spa.md) or Interactive Communication in an AEM Sites single page application (SPA). The embedded Adaptive Form and Interactive Communication is fully functional and users can fill and submit the form without leaving the page. It helps user remain in context of other elements on the web page and simultaneously interact with the adaptive form or Interactive Communication.

#### Sort columns of Adaptive Form tables {#sort-columns-of-adaptive-form-tables}

You can [sort any column of an Adaptive Form table](../../forms/using/adaptive-forms-tables.md#sortcolumnstable) in an ascending or descending order. You can apply sorting to table columns with static text, data model object properties, or a combination of static text and data model object properties.

#### Restrict the availability of Adaptive Forms templates to specific paths {#restrict-the-availability-of-adaptive-forms-templates-to-specific-paths}

Adaptive forms has added support for the cq:allowedPaths property. The property [restricts availability of Adaptive Forms templates to specific paths](creating-adaptive-form.md#adaptive-form-templates).

#### Add check boxes to the Adaptive Form dynamically {#add-check-boxes-to-the-adaptive-form-dynamically}

You can now define rules to [add checkboxes to the Adaptive Form dynamically](../../forms/using/rule-editor.md#setpropertyrule) based on custom function, a form object, or an object property.

## AEM Workflows {#aem-workflows}

### Use variables in AEM Workflows {#use-variables-in-aem-workflows}

Variables enable workflow steps to hold and pass metadata across workflow steps at runtime. You can create different types of variables for storing different types of data. For example, integers, strings, documents, or form data model instances. Typically, you use a variable or a collection of variables when you need to make a decision based on the value that it holds or to store information that you need later in a process.

Variables are an extension of [MetaDataMap](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/workflow/metadata/MetaDataMap.html) interface available in the previous version. It helps save time spent in developing custom ECMAScript code used to retrieve and update metadata values. You continue using MetaDataMap interface and ECMAScript code to manipulate metadata. Some benefits of using variables over MetaDataMap and ECMAScript are:

* Dynamically store, update, and use values stored in a variable across the workflow without relying on custom code
* Retrieve and update values directly to a form data model and data file (XML/JSON ) of a submitted form
* Store complete documents in a variable to perform document processing

The Go To step, OR Split step, and all AEM Forms workflow steps support variables. You can use MetaDataMap interface to access variables in workflow steps that do not have a native support for variables. For more information, see [Variables in AEM Workflows](../../forms/using/variable-in-aem-workflows.md).

![Setting a variable for in a workflow](assets/variable.png)

#### Use a workflow with different Adaptive Forms  {#use-a-workflow-with-different-adaptive-forms}

You can [specify an Adaptive Form for the assign task](../../forms/using/aem-forms-workflow-step-reference.md#assign-task-step) and document of record step of form-centric workflows on the runtime. It allows a workflow to work with different Adaptive Forms. You can decide the method to select an Adaptive Form while designing the workflow. The Adaptive Form can be located at an absolute path, submitted as payload to the workflow, or available at a path calculated using a variable.

#### Use enhanced logging capabilities of forms-centric workflow steps {#use-enhanced-logging-capabilities-of-forms-centric-workflow-steps}

Logging capabilities of forms-centric workflow steps are standardized. Now, all form-centric workflow steps produce similarly standardized logs. It helps improve debugging speed.

## Data Integration {#data-integration}

You can now:

* [Validate input data](../../forms/using/work-with-form-data-model.md#automated-validation-of-input-data) based on a list of constraints. It helps ensure that only valid data is submitted to data source.
* [Override default endpoint](../../forms/using/configure-data-sources.md#configure-soap-web-services) defined in a WSDL (Web Services Description Language) file.

* [Override default](../../forms/using/configure-data-sources.md#configure-restful-web-services) [scheme, host, and base path](../../forms/using/configure-data-sources.md#configure-restful-web-services) defined in Swagger definition file.

## Platform and Security updates {#platform-and-security-updates}

### Major platform updates {#major-platform-updates}

AEM Forms can be set up using any combination of supported operating systems, application servers, databases, database drivers, JDK, LDAP servers, and email servers. The following are the major changes in [supported platforms](../../forms/using/aem-forms-jee-supported-platforms.md):

<table>
 <tbody>
  <tr>
   <td>Component</td>
   <td>Support Removed</td>
  </tr>
  <tr>
   <td>Operating systems</td>
   <td>
    <ul>
     <li>Microsoft Windows Server 2012 R2</li>
     <li>IBM AIX*</li>
     <li>Sun Solaris*</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Application servers<br /> </td>
   <td>
    <ul>
    <li>WebSphere Liberty profile</li>
    <li>Oracle WebLogic</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Databases</td>
   <td>
    <ul>
     <li>IBM DB2 <br /> </li>
     <li>Oracle RAC</li>
    </ul> </td>
  </tr>
  <tr>
   <td>LDAP servers</td>
   <td>
    <ul>
     <li>Microsoft Active Directory 2012</li>
     <li>Novell eDirectory 8.8.7 </li>
     <li>IBM Lotus Domino 8.5.0 </li>
    </ul> </td>
  </tr>
  <tr>
   <td>Email servers</td>
   <td>
    <ul>
     <li>IBM Lotus Domino 8.5.0 </li>
    </ul> </td>
  </tr>
  <tr>
   <td>Connectors</td>
   <td>
    <ul>
     <li>Connector for Microsoft Sharepoint 2013</li>
     <li>Connector for EMC Documentum 7.0</li>
    </ul> </td>
  </tr>
  <tr>
   <td>AEM Forms app<br /> </td>
   <td>
    <ul>
     <li>Windows 8.1 support</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Java </td>
   <td>
    <ul>
     <li>Java 11</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

&#42; Contact Adobe Support for information on migrating to a different platform

#### New HTML5-based UIs {#new-html-based-uis}

In line with planned EOL of Adobe Flash Player and overall direction of migrating Flash-based content to open standards, AEM 6.5 Forms has replaced Flash-based UI of Health Monitor, Process Management, Reader Extension, and Category Management UI of AEM Forms on JEE Administration Console with HTML5-based UI.

#### Security improvements {#security-improvements}

* AEM 6.5 Forms on JEE administration console UI is now based on Apache Struts 2.5.
* AEM 6.5 Forms now uses jQuery to 3.2.1 and jQuery UI 1.12.1. See, [upgrade documentation](/help/forms/home.md) for the impact of the change.

#### Accessibility improvements {#accessibility-improvements}

AEM 6.5 Forms has improved accessibility of AEM Forms Workspace. 
!-->

