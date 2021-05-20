---
title: Résumé des nouvelles fonctionnalités | AEM 6.5 Forms
seo-title: Résumé des nouvelles fonctionnalités | AEM 6.5 Forms
description: Dernières fonctionnalités et améliorations apportées aux formulaires et documents de la solution de gestion de l’expérience numérique la plus avancée du monde.
seo-description: Dernières fonctionnalités et améliorations apportées aux formulaires et documents de la solution de gestion de l’expérience numérique la plus avancée du monde.
uuid: 179d372d-b7f6-4771-8349-fc6b7854efac
topic-tags: introduction
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 0e949429-cd5f-4301-aa72-14803cdfab00
docset: aem65
exl-id: 47b9de1f-b16a-424c-b8b4-e9d7b3dcca86
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1245'
ht-degree: 16%

---

# Résumé des nouvelles fonctionnalités | AEM 6.5 Forms{#new-features-summary-aem-forms}

## Rapports de transaction {#transaction-reports}

Les rapports de transaction vous permettent de capturer et de suivre le nombre de formulaires envoyés, de documents traités et de documents rendus. L’objectif du suivi de ces transactions est de prendre une décision éclairée sur l’utilisation du produit et de rééquilibrer les investissements en matériel et en logiciels. Voici quelques exemples de transactions :

* Envoi d’un formulaire adaptatif, d’un formulaire HTML5 ou d’un jeu de formulaires
* Rendu d’une version imprimée ou web d’une communication interactive
* Conversion d’un document d’un format de fichier à un autre

Pour plus d’informations sur la configuration et l’utilisation des rapports de transaction, voir [Présentation des rapports de transaction](../../forms/using/transaction-reports-overview.md).

![Exemple de rapport de transaction](assets/surface_transaction_reporting.png)

## Communications interactives {#interactive-communications}

**Définition des modèles d’affichage des données**

Les auteurs de communication interactive peuvent désormais définir des [modèles d’affichage de données](create-interactive-communication.md#datadisplaypatterns) pour les champs, les variables et les éléments de modèle de données de formulaire. Formats de date, de devise ou de téléphone, par exemple.

**Utiliser de nouveaux types de graphiques**

Vous pouvez désormais ajouter des [graphiques quadrant et des graphiques avec plusieurs séries](../../forms/using/chart-component-interactive-communications.md) aux communications interactives.

**Tri des colonnes d&#39;un tableau**

Vous pouvez désormais [trier les colonnes d’un tableau](../../forms/using/create-interactive-communication.md#sortcolumns) dans la communication interactive. Vous pouvez lier et trier les colonnes du tableau avec du texte statique ou des objets de modèle de données.

**Utilisation de nouveaux composants dans un canal web**

Vous pouvez désormais ajouter des composants Bouton et Séparateur au canal web. Pour plus d’informations, voir [Ajouter le composant Bouton au canal web](../../forms/using/create-interactive-communication.md#add-button-component-to-the-web-channel) et [Composant Séparateur dans le canal web](../../forms/using/create-interactive-communication.md#separatorcomponent).

**Mode Mise en page pour redimensionner les composants**

Vous pouvez désormais passer en [mode Mise en page](../../forms/using/resize-using-layout-mode.md) pour redimensionner les composants du canal web à l’aide d’une interface WYSIWYG.

**Améliorations de la convivialité**

Les auteurs de communication interactive peuvent désormais utiliser diverses opérations simples d’utilisation lors de la création de correspondances. La liste des opérations comprend :

* [Exécution d’actions d’annulation dans les canaux papier et web](../../forms/using/create-interactive-communication.md#undoredoactions)
* [Ajout de variables dans un fragment de document à l’aide du symbole @](../../forms/using/texts-interactive-communications.md#searchvariables)
* [Ajout d’éléments de modèle de données dans un fragment de document à l’aide du symbole @](../../forms/using/texts-interactive-communications.md#searchdatamodelproperties)
* [Supprimer ou ajouter un canal web à une communication interactive existante](../../forms/using/create-interactive-communication.md#edit-interactive-communication-properties)
* [Liaison des éléments de source de données avec des champs et des variables à l’aide d’actions de glisser-déposer](../../forms/using/create-interactive-communication.md#binddatasourceelements)
* [Mettre en surbrillance les champs et variables non liés lors de la création d’une communication interactive](../../forms/using/create-interactive-communication.md#distinguishunboundfields)
* [Actions supplémentaires telles que la copie, le groupe ou plus sur les composants hérités dans un canal web](../../forms/using/create-interactive-communication.md#componenttoolbar)

**Améliorations du processus de synchronisation**

Plusieurs améliorations ont été apportées à la disposition du canal web générée automatiquement à l’aide du canal d’impression.

![Graphiques de communications interactives](assets/interactive-communication-charts.png)

## Formulaires adaptatifs {#adaptive-forms}

### Utilisation des signatures numériques Adobe Sign basées sur le cloud dans Forms adaptatif {#use-adobe-sign-s-cloud-based-digital-signatures-in-adaptive-forms}

[Les signatures numériques basées sur le cloud ou les signatures distantes sont une nouvelle génération de signatures numériques qui fonctionnent sur les postes de travail, les appareils mobiles et le web, et qui répondent aux niveaux de conformité et d’assurance les plus élevés pour l’authentification des signataires. ](https://helpx.adobe.com/fr/sign/kb/digital-certificate-providers.html) Vous pouvez désormais [signer un formulaire adaptatif](../../forms/using/working-with-adobe-sign.md) avec des signatures numériques basées sur le cloud.

#### Incorporation d’un formulaire adaptatif ou d’une communication interactive dans des applications d’une seule page AEM Sites {#embed-an-adaptive-form-or-interactive-communcation-in-aem-sites-single-page-applications}

AEM Forms vous permet d’[incorporer aisément un formulaire adaptatif](../../forms/using/embed-adaptive-form-aem-sites-spa.md) ou une communication interactive dans une application d’une seule page AEM Sites (SPA). Le formulaire adaptatif et la communication interactive incorporés sont entièrement fonctionnels et les utilisateurs peuvent remplir et envoyer le formulaire sans quitter la page. Il permet à l’utilisateur de rester dans le contexte d’autres éléments de la page web et d’interagir simultanément avec le formulaire adaptatif ou la communication interactive.

#### Trier les colonnes des tableaux de formulaire adaptatif {#sort-columns-of-adaptive-form-tables}

Vous pouvez [trier n’importe quelle colonne d’un tableau de formulaire adaptatif](../../forms/using/adaptive-forms-tables.md#sortcolumnstable) dans un ordre croissant ou décroissant. Vous pouvez appliquer un tri aux colonnes du tableau avec du texte statique, des propriétés d’objet de modèle de données ou une combinaison de propriétés de texte statique et d’objet de modèle de données.

#### Limiter la disponibilité des modèles de Forms adaptatif à des chemins spécifiques {#restrict-the-availability-of-adaptive-forms-templates-to-specific-paths}

Les formulaires adaptatifs ont ajouté la prise en charge de la propriété cq:allowedPaths. La propriété [limite la disponibilité des modèles de Forms adaptatif à des chemins spécifiques](creating-adaptive-form.md#adaptive-form-templates).

#### Ajouter dynamiquement des cases à cocher au formulaire adaptatif {#add-check-boxes-to-the-adaptive-form-dynamically}

Vous pouvez désormais définir des règles pour [ajouter des cases à cocher au formulaire adaptatif dynamiquement](../../forms/using/rule-editor.md#setpropertyrule) en fonction d’une fonction personnalisée, d’un objet de formulaire ou d’une propriété d’objet.

## Workflows AEM {#aem-workflows}

### Utilisation de variables dans AEM Workflows {#use-variables-in-aem-workflows}

Les variables permettent aux étapes d’un workflow de contenir et de transmettre des métadonnées entre les étapes d’un workflow au moment de l’exécution. Vous pouvez créer différents types de variables pour stocker différents types de données. Par exemple, des entiers, des chaînes, des documents ou des instances de modèle de données de formulaire. En règle générale, vous utilisez une variable ou une collection de variables lorsque vous devez prendre une décision en fonction de la valeur qu’elle contient ou pour stocker des informations dont vous aurez besoin ultérieurement dans un processus.

Les variables sont une extension de l’interface [MetaDataMap](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/adobe/granite/workflow/metadata/MetaDataMap.html) disponible dans la version précédente. Cela permet de gagner du temps lors du développement du code ECMAScript personnalisé utilisé pour récupérer et mettre à jour les valeurs de métadonnées. Vous continuez à utiliser l’interface MetaDataMap et le code ECMAScript pour manipuler les métadonnées. Voici quelques avantages de l’utilisation de variables sur MetaDataMap et ECMAScript :

* Stockage, mise à jour et utilisation dynamiques des valeurs stockées dans une variable dans l’ensemble du workflow sans recourir au code personnalisé
* Récupérer et mettre à jour les valeurs directement dans un modèle de données de formulaire et un fichier de données (XML/JSON ) d’un formulaire envoyé
* Stocker les documents complets dans une variable pour effectuer le traitement des documents

L’étape Aller à , ou Partage , et toutes les étapes du processus AEM Forms prennent en charge les variables. Vous pouvez utiliser l’interface MetaDataMap pour accéder à des variables dans les étapes de workflow qui ne prennent pas en charge les variables de manière native. Pour plus d’informations, voir [Variables dans AEM Workflows](../../forms/using/variable-in-aem-workflows.md).

![Définition d’une variable pour dans un workflow](assets/variable.png)

#### Utilisation d’un workflow avec différents Forms adaptatifs {#use-a-workflow-with-different-adaptive-forms}

Vous pouvez [spécifier un formulaire adaptatif pour l’étape d’affectation ](../../forms/using/aem-forms-workflow-step-reference.md#assign-task-step) et de document d’enregistrement des processus basés sur l’utilisation de formulaires au moment de l’exécution. Il permet à un workflow de fonctionner avec différents Forms adaptatifs. Vous pouvez choisir la méthode de sélection d’un formulaire adaptatif lors de la conception du processus. Le formulaire adaptatif peut être situé à un chemin absolu, envoyé en tant que charge utile au workflow ou disponible à un chemin calculé à l’aide d’une variable.

#### Utilisation des fonctionnalités de journalisation améliorées des étapes de processus centrées sur les formulaires {#use-enhanced-logging-capabilities-of-forms-centric-workflow-steps}

Les fonctionnalités de journalisation des étapes de workflow centrées sur les formulaires sont normalisées. Désormais, toutes les étapes de processus centrées sur les formulaires génèrent des journaux normalisés similaires. Cela permet d’améliorer la vitesse de débogage.

## Intégration de données {#data-integration}

Vous pouvez maintenant effectuer les tâches suivantes :

* [Validez les ](../../forms/using/work-with-form-data-model.md#automated-validation-of-input-data) données d’entrée en fonction d’une liste de contraintes. Cela permet de s’assurer que seules les données valides sont envoyées à la source de données.
* [Remplacez le point de ](../../forms/using/configure-data-sources.md#configure-soap-web-services) terminaison par défaut défini dans un fichier WSDL (Web Services Description Language).

* [Remplacez ](../../forms/using/configure-data-sources.md#configure-restful-web-services) [par défaut le schéma, l’hôte et le ](../../forms/using/configure-data-sources.md#configure-restful-web-services) chemin de base définis dans le fichier de définition Swagger.

## Mises à jour de plateforme et de sécurité {#platform-and-security-updates}

### Mises à jour majeures de la plateforme {#major-platform-updates}

AEM Forms peut être installé à l’aide de n’importe quelle combinaison de systèmes d’exploitation, serveurs d’applications, bases de données, pilotes de base de données, JDK, serveurs LDAP et serveurs de messagerie électronique pris en charge. Voici les modifications majeures apportées aux [plateformes prises en charge](../../forms/using/aem-forms-jee-supported-platforms.md) :

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
     <li>Oracle RAC</li>
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
     <li>Prise en charge de Windows 8.1</li>
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

* Contactez l’assistance Adobe pour plus d’informations sur la migration vers une autre plateforme.

#### Nouvelles interfaces utilisateur HTML5 {#new-html-based-uis}

Conformément à la fin de Flash Player de l’Adobe prévue et à la direction générale de la migration du contenu basé sur les Flashs vers des normes ouvertes, AEM 6.5 Forms a remplacé l’interface utilisateur basée sur les Flashs de Health Monitor, Process Management, Reader Extension et l’interface utilisateur de gestion des catégories de la console d’administration d’AEM Forms on JEE par une interface utilisateur basée sur HTML5.

#### Améliorations de la sécurité {#security-improvements}

* L’interface utilisateur d’Administration Console pour Forms on JEE d’AEM 6.5 est désormais basée sur Apache Struts 2.5.
* AEM 6.5 Forms utilise désormais jQuery vers la version 3.2.1 et l’interface utilisateur jQuery 1.12.1. Voir [documentation de mise à niveau](/help/forms/home.md) pour connaître l’impact de la modification.

#### Améliorations de l’accessibilité {#accessibility-improvements}

AEM version 6.5 de Forms a amélioré l’accessibilité d’AEM Forms Workspace.
