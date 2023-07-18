---
title: Résumé des nouvelles fonctionnalités | AEM 6.5 Forms
seo-title: New features summary | AEM 6.5 Forms
description: Dernières fonctionnalités et améliorations apportées aux formulaires et documents de la solution de gestion de l’expérience digitale la plus avancée au monde.
seo-description: Latest features and improvements to forms and documents of world’s most advanced digital experience management solution.
uuid: 179d372d-b7f6-4771-8349-fc6b7854efac
topic-tags: introduction
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 0e949429-cd5f-4301-aa72-14803cdfab00
docset: aem65
exl-id: 47b9de1f-b16a-424c-b8b4-e9d7b3dcca86
source-git-commit: 1683338f02d01d5d9843368955fa42f309718f26
workflow-type: tm+mt
source-wordcount: '1245'
ht-degree: 99%

---

# Résumé des nouvelles fonctionnalités | AEM 6.5 Forms{#new-features-summary-aem-forms}

## Rapports de transaction {#transaction-reports}

| Version | Lien de l’article |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Cliquez ici](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/forms-overview/latest-innovations.html) |
| AEM 6.5 | Cet article |


Les rapports de transaction vous permettent de capturer et de suivre le nombre de formulaires envoyés, de documents traités et de documents rendus. L’objectif derrière le suivi de ces transactions est de prendre une décision éclairée concernant l’utilisation du produit et de réévaluer les investissements en matériel et en logiciels. Voici quelques exemples de transactions :

* Envoi d’un formulaire adaptatif, d’un formulaire HTML5 ou d’un jeu de formulaires.
* Rendu d’une version imprimée ou d’une version web d’une communication interactive.
* Conversion d’un document d’un format de fichier à un autre.

Pour plus d’informations sur la configuration et l’utilisation des rapports de transaction, consultez la [Présentation des rapports de transaction](../../forms/using/transaction-reports-overview.md).

![Exemple de rapport de transaction](assets/surface_transaction_reporting.png)

## Communications interactives {#interactive-communications}

**Définir des modèles d’affichage de données**

Les auteurs de communications interactives peuvent désormais définir des [modèles d’affichage des données](create-interactive-communication.md#datadisplaypatterns) pour les champs, les variables et les éléments du modèle de données du formulaire. Par exemple, les formats de date, de devise ou de téléphone.

**Utiliser de nouveaux types de graphiques**

Vous pouvez désormais ajouter des [graphiques à quadrants et des graphiques à séries multiples](../../forms/using/chart-component-interactive-communications.md) aux communications interactives.

**Tri des colonnes d’un tableau**

Vous pouvez désormais [trier les colonnes d’un tableau](../../forms/using/create-interactive-communication.md#sortcolumns) dans la communication interactive. Vous pouvez lier et trier les colonnes d’un tableau avec du texte statique ou des objets de modèle de données.

**Utiliser de nouveaux composants dans un canal web**

Vous pouvez désormais ajouter des composants Bouton et Séparateur au canal web. Pour plus d’informations, consultez les sections [Ajouter un composant Bouton au canal web](../../forms/using/create-interactive-communication.md#add-button-component-to-the-web-channel) et [composant Séparateur dans le canal web](../../forms/using/create-interactive-communication.md#separatorcomponent).

**Mode de disposition pour redimensionner les composants**

Vous pouvez maintenant passer en [Mode de disposition](../../forms/using/resize-using-layout-mode.md) pour redimensionner les composants du canal web à l’aide d’une interface WYSIWYG.

**Améliorations apportées à lʼutilisation**

Les auteurs de communications interactives peuvent désormais effectuer différentes opérations simples lors de la création de correspondances. La liste des opérations comprend :

* [Effectuer des actions Annuler/rétablir dans les canaux d’impression et web.](../../forms/using/create-interactive-communication.md#undoredoactions)
* [Ajouter des variables dans un fragment de document à l’aide du symbole @](../../forms/using/texts-interactive-communications.md#searchvariables)
* [Ajouter des éléments de modèle de données dans un fragment de document à l’aide du symbole @](../../forms/using/texts-interactive-communications.md#searchdatamodelproperties)
* [Supprimer ou ajouter un canal web à une communication interactive existante](../../forms/using/create-interactive-communication.md#edit-interactive-communication-properties)
* [Lier des éléments de source de données avec des champs et des variables à l’aide dʼactions de type glisser-déposer.](../../forms/using/create-interactive-communication.md#binddatasourceelements)
* [Mettre en surbrillance les champs et les variables non liés lors de la création d’une communication interactive](../../forms/using/create-interactive-communication.md#distinguishunboundfields)
* [Effectuer des actions supplémentaires telles que copier, associer ou plus sur les composants hérités dans un canal web.](../../forms/using/create-interactive-communication.md#componenttoolbar)

**Améliorations apportées au processus de synchronisation**

Plusieurs améliorations ont été apportées à la disposition du canal web générée automatiquement à l’aide du canal d’impression.

![Graphiques dans les communications interactives](assets/interactive-communication-charts.png)

## Formulaires adaptatifs {#adaptive-forms}

### Utiliser les signatures numériques dans le cloud dʼAdobe Sign dans les formulaires adaptatifs {#use-adobe-sign-s-cloud-based-digital-signatures-in-adaptive-forms}

[Les signatures numériques basées sur le cloud ou les signatures distantes sont une nouvelle génération de signatures numériques qui fonctionnent sur les postes de travail, les appareils mobiles et le web, et qui répondent aux niveaux de conformité et d’assurance les plus élevés pour l’authentification des signataires. ](https://helpx.adobe.com/fr/sign/kb/digital-certificate-providers.html) Vous pouvez désormais [signer un formulaire adaptatif](../../forms/using/working-with-adobe-sign.md) avec des signatures numériques présentes dans le cloud.

#### Incorporer un formulaire adaptatif ou une communication interactive dans les applications dʼune seule page d’AEM Sites {#embed-an-adaptive-form-or-interactive-communcation-in-aem-sites-single-page-applications}

AEM Forms vous permet d’[incorporer aisément un formulaire adaptatif](../../forms/using/embed-adaptive-form-aem-sites-spa.md) ou une communication interactive dans une application dʼune seule page d’AEM Sites (SPA). Le formulaire adaptatif et la communication interactive incorporés sont entièrement fonctionnels et les utilisateurs peuvent les remplir et les envoyer sans quitter la page. Cela permet à l’utilisateur de rester dans le contexte des autres éléments de la page web et d’interagir simultanément avec le formulaire adaptatif ou la communication interactive.

#### Trier les colonnes des tableaux de formulaires adaptatifs {#sort-columns-of-adaptive-form-tables}

Vous pouvez [trier n’importe quelle colonne d’un tableau de formulaire adaptatif](../../forms/using/adaptive-forms-tables.md#sortcolumnstable) en ordre croissant ou décroissant. Vous pouvez appliquer un tri aux colonnes du tableau avec du texte statique, des propriétés dʼobjet de modèle de données ou une combinaison des deux.

#### Limiter la disponibilité des modèles adaptatifs Forms à des emplacements spécifiques {#restrict-the-availability-of-adaptive-forms-templates-to-specific-paths}

Les formulaires adaptatifs prennent désormais en charge la propriété cq:allowedPaths. La propriété [limite la disponibilité des modèles adaptatifs Forms à des emplacements spécifiques](creating-adaptive-form.md#adaptive-form-templates).

#### Ajouter de façon dynamique des cases à cocher au formulaire adaptatif {#add-check-boxes-to-the-adaptive-form-dynamically}

Vous pouvez désormais définir des règles pour [ajouter de façon dynamique des cases à cocher au formulaire adaptatif](../../forms/using/rule-editor.md#setpropertyrule) selon une fonction personnalisée, un objet de formulaire ou une propriété dʼobjet.

## Workflows AEM {#aem-workflows}

### Utiliser les variables dans les workflows AEM {#use-variables-in-aem-workflows}

Les variables permettent aux étapes de workflow de contenir et de transmettre des métadonnées entre les étapes de workflow au moment de l’exécution. Vous pouvez créer différents types de variables pour stocker différents types de données. Par exemple, des entiers, des chaînes, des documents ou des instances de modèle de données de formulaire. En règle générale, vous utilisez une variable ou une collection de variables lorsque vous devez prendre une décision en fonction de la valeur qu’elle contient ou pour stocker des informations dont vous aurez besoin ultérieurement dans un processus.

Les variables sont une extension de lʼinterface [MetaDataMap](https://helpx.adobe.com/fr/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/workflow/metadata/MetaDataMap.html) disponible dans la version précédente. Elles offrent un gain de temps dans le développement de code ECMAScript personnalisé utilisé pour récupérer et mettre à jour les valeurs des métadonnées. Vous manipulez toujours les métadonnées au moyen de lʼinterface MetaDataMap et du code ECMAScript. Lʼutilisation de variables par rapport à MetaDataMap et ECMAScript présente certains avantages :

* Stocker, mettre à jour et utiliser de manière dynamique les valeurs stockées dans une variable dans l’ensemble du workflow, sans recourir à du code personnalisé
* Récupérer et mettre à jour les valeurs directement dans un modèle de données de formulaire et dans le fichier de données (XML/JSON ) d’un formulaire envoyé
* Stocker les documents complets dans une variable pour effectuer leur traitement

L’étape Accéder à, l’étape Division OU et toutes les étapes dʼAEM Forms Workflow prennent en charge les variables. Vous pouvez utiliser l’interface MetaDataMap pour accéder à des variables dans des étapes de workflow qui ne prennent pas en charge les variables de manière native. Pour plus d’informations, consultez la section [Variables dans les workflows AEM](../../forms/using/variable-in-aem-workflows.md).

![Définir une variable pour un workflow](assets/variable.png)

#### Utiliser un workflow avec différents formulaires adaptatifs  {#use-a-workflow-with-different-adaptive-forms}

Vous pouvez [spécifier un formulaire adaptatif pour l’étape Affecter une tâche](../../forms/using/aem-forms-workflow-step-reference.md#assign-task-step) et l’étape Générer un document d’enregistrement des workflows basés sur l’utilisation de Forms au moment de lʼexécution. Il permet à un workflow de fonctionner avec différents formulaires adaptatifs. Vous pouvez choisir la méthode de sélection dʼun formulaire adaptatif lors de la conception du workflow. Le formulaire adaptatif peut être situé à un chemin absolu, envoyé comme payload au workflow, ou disponible à un chemin calculé à l’aide d’une variable.

#### Utiliser les fonctionnalités de journalisation améliorées des étapes de workflows basés sur l’utilisation de Forms {#use-enhanced-logging-capabilities-of-forms-centric-workflow-steps}

Les fonctionnalités de journalisation des étapes de workflows basés sur l’utilisation de Forms sont normalisées. Désormais, toutes les étapes de workflows basés sur l’utilisation de Forms génèrent des journaux normalisés similaires. Cela permet d’améliorer la vitesse de débogage.

## Intégration de données  {#data-integration}

Vous pouvez maintenant effectuer les tâches suivantes :

* [Valider les données d’entrée](../../forms/using/work-with-form-data-model.md#automated-validation-of-input-data) en fonction dʼune liste de contraintes. Cela permet de s’assurer que seules des données valides sont envoyées à la source de données.
* [Remplacer le point d’entrée par défaut](../../forms/using/configure-data-sources.md#configure-soap-web-services) défini dans un fichier WSDL (Web Services Description Language).

* [Remplacer le [schéma, lʼhôte et le chemin dʼaccès de base](../../forms/using/configure-data-sources.md#configure-restful-web-services) par défaut](../../forms/using/configure-data-sources.md#configure-restful-web-services) définis dans le fichier de définition Swagger.

## Mises à jour de la plateforme et de la sécurité {#platform-and-security-updates}

### Principales mises à jour de la plateforme {#major-platform-updates}

AEM Forms peut être installé à l’aide de n’importe quelle combinaison de systèmes d’exploitation, serveurs d’applications, bases de données, pilotes de base de données, JDK, serveurs LDAP et serveurs de messagerie électronique pris en charge. Les principales modifications en matière de [plateformes prises en charge](../../forms/using/aem-forms-jee-supported-platforms.md) sont les suivantes :

<table>
 <tbody>
  <tr>
   <td>Composant</td>
   <td>Prise en charge supprimée</td>
  </tr>
  <tr>
   <td>Systèmes d’exploitation</td>
   <td>
    <ul>
     <li>Microsoft Windows Server 2012 R2</li>
     <li>IBM AIX*</li>
     <li>Sun Solaris*</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Serveurs d’applications<br /> </td>
   <td>
    <ul>
    <li>Profil WebSphere Liberty</li>
    <li>Oracle WebLogic </li>
    </ul> </td>
  </tr>
  <tr>
   <td>Bases de données</td>
   <td>
    <ul>
     <li>IBM DB2 <br /> </li>
     <li>Oracle RAC</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Serveurs LDAP</td>
   <td>
    <ul>
     <li>Microsoft Active Directory 2012</li>
     <li>Novell eDirectory 8.8.7 </li>
     <li>IBM Lotus Domino 8.5.0 </li>
    </ul> </td>
  </tr>
  <tr>
   <td>Serveurs de messagerie</td>
   <td>
    <ul>
     <li>IBM Lotus Domino 8.5.0 </li>
    </ul> </td>
  </tr>
  <tr>
   <td>Connecteurs</td>
   <td>
    <ul>
     <li>Connector for Microsoft Sharepoint 2013</li>
     <li>Connector for EMC Documentum 7.0</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Application AEM Forms<br /> </td>
   <td>
    <ul>
     <li>Prise en charge de Windows 8.1</li>
    </ul> </td>
  </tr>
  <tr>
   <td>Java </td>
   <td>
    <ul>
     <li>Java 11</li>
    </ul> </td>
  </tr>
 </tbody>
</table>

&#42;Contactez l’assistance Adobe pour plus d’informations sur la migration vers une autre plateforme.

#### Nouvelles interfaces utilisateur au format HTML5 {#new-html-based-uis}

Suite à la fin de vie prochaine d’Adobe Flash Player et à la migration générale du contenu Flash vers des normes ouvertes, AEM Forms 6.5 a remplacé les interfaces utilisateur Flash de Health Monitor, Process Management, Reader Extension ainsi que l’interface utilisateur de la gestion des catégories de la console d’administration d’AEM Forms sur JEE par des interfaces utilisateur au format HTML5.

#### Améliorations apportées à la sécurité {#security-improvements}

* L’interface utilisateur de la console d’administration d’AEM Forms sur JEE version 6.5 repose désormais sur Apache Struts 2.5.
* AEM Forms 6.5 utilise désormais jQuery 3.2.1 et l’interface utilisateur jQuery 1.12.1. Consultez la [documentation de mise à niveau](/help/forms/home.md) pour appréhender l’impact de la modification.

#### Améliorations apportées à l’accessibilité {#accessibility-improvements}

AEM Forms 6.5 améliore l’accessibilité de l’espace de travail d’AEM Forms.
