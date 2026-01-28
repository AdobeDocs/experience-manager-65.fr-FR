---
title: Meilleures pratiques pour travailler avec les formulaires adaptatifs
description: Explique les bonnes pratiques à appliquer pour configurer un projet AEM Forms, développer des formulaires adaptatifs et optimiser les performances du système AEM Forms.
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
feature: Adaptive Forms,Foundation Components,Core Components
exl-id: 5c75ce70-983e-4431-a13f-2c4c219e8dde
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
source-git-commit: 5699f5814daf16a397eb6129b881ac2035456e39
workflow-type: tm+mt
source-wordcount: '5888'
ht-degree: 100%

---

# Meilleures pratiques pour travailler avec les formulaires adaptatifs {#best-practices-for-working-with-adaptive-forms}

<span class="preview">Adobe recommande d’utiliser les [composants principaux](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=fr) de capture de données modernes et extensibles pour [créer des formulaires adaptatifs](/help/forms/using/create-an-adaptive-form-core-components.md) ou [ajouter des formulaires adaptatifs à des pages AEM Sites](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md). Ces composants représentent une avancée significative dans la création de formulaires adaptatifs, ce qui garantit des expériences utilisateur impressionnantes. Cet article décrit l’ancienne approche de la création de formulaires adaptatifs à l’aide de composants de base. </span>

## Vue d’ensemble {#overview}

Les formulaires Adobe Experience Manager (AEM) peuvent vous aider à transformer des transactions complexes en expériences numériques simples et attrayantes. Toutefois, il faut un effort concerté pour mettre en œuvre, créer, exécuter et maintenir un écosystème AEM Forms efficace et productif.

Ce document fournit des instructions et des recommandations dont peuvent bénéficier les équipes d’administration, de création et de développement de formulaires au moment d’utiliser AEM Forms, en particulier le composant de formulaires adaptatifs. Il aborde les bonnes pratiques à appliquer, depuis la configuration d’un projet de développement de formulaires jusqu’à la configuration, la personnalisation, la création et l’optimisation d’AEM Forms. Ces bonnes pratiques contribuent ensemble aux performances globales de l’écosystème AEM Forms.

En outre, voici quelques recommandations de lecture concernant les meilleures pratiques générales d’AEM :

* [Bonnes pratiques : déploiement et maintien d’AEM](/help/sites-deploying/best-practices.md)
* [Meilleures pratiques : création de contenu](/help/sites-authoring/best-practices.md)
* [Meilleures pratiques : administration d’AEM](/help/sites-administering/administer-best-practices.md)
* [Meilleures pratiques : développement de solutions](/help/sites-developing/best-practices.md)

## Installation et configuration d’AEM Forms {#set-up-and-configure-aem-forms}

### Installation du projet de développement de formulaires {#setting-up-forms-development-project}

Une structure de projet simplifiée et normalisée peut réduire considérablement les efforts de développement et de maintenance. Apache Maven est un outil open-source recommandé pour créer des projets AEM.

* Utilisez le `aem-project-archetype` d’Apache Maven pour créer et gérer la structure d’un projet AEM. Il permet de créer la structure et les modèles recommandés pour votre projet AEM. En outre, il fournit des systèmes d’automatisation de création et de contrôle des modifications pour aider à la gestion du projet.

   * Utilisez la commande Maven`archetype:generate` pour générer la structure initiale.
   * Utilisez la commande Maven `eclipse:eclipse` pour générer les fichiers de projet Eclipse et importer le projet dans Eclipse.

Pour plus d’informations, reportez-vous à la section [Comment créer des projets AEM à l’aide d’Apache Maven](/help/sites-developing/ht-projects-maven.md).

* L’outil FileVault ou VLT vous permet de mapper le contenu d’une instance CRX ou AEM à votre système de fichiers. Il fournit des opérations de gestion de contrôle des modifications, telles que l’archivage et l’extraction du contenu du projet AEM. Voir [Comment utiliser l’outil VLT](/help/sites-developing/ht-vlttool.md).

* Si vous utilisez un environnement de développement intégré à Eclipse, vous pouvez utiliser les outils de développement AEM pour une intégration transparente de l’IDE Eclipse aux instances AEM afin de créer des applications AEM. Pour plus d’informations, voir [Outils de développement AEM pour Eclipse](/help/sites-developing/aem-eclipse.md).

* Ne stockez aucun contenu ou n’apportez aucune modification dans le dossier /libs. Créez des recouvrements dans les dossiers /app pour étendre ou remplacer les fonctionnalités par défaut.

* Lorsque vous créez des packages pour déplacer du contenu, assurez-vous que les chemins de filtre de package sont corrects et que seuls les chemins obligatoires sont mentionnés.

* Ne stockez aucun contenu ou n’apportez aucune modification dans le dossier /libs. Créez des recouvrements dans les dossiers /app pour étendre ou remplacer les fonctionnalités par défaut.

* Définissez des dépendances correctes pour les packages afin de forcer un ordre / une séquence d’installation prédéterminé(e).

* Ne créez aucun nœud référençable dans /libs ou /apps.

### Planification de l’environnement de création {#planning-for-authoring-environment}

Une fois votre projet AEM configuré, définissez la stratégie de création et de personnalisation des composants et modèles de formulaires adaptatifs.

* Un modèle de formulaire adaptatif est une page AEM spécialisée qui définit la structure et les informations d’en-tête et de pied de page d’un formulaire adaptatif. Un modèle comporte des dispositions, des styles et une structure de base préconfigurés pour un formulaire adaptatif. AEM Forms fournit des modèles et des composants prêts à l’emploi que vous pouvez utiliser pour créer des formulaires adaptatifs. Vous pouvez également créer des modèles et des composants personnalisés en fonction de vos besoins. Il est recommandé de rassembler les exigences relatives aux modèles et composants supplémentaires dont vous aurez besoin dans vos formulaires adaptatifs. Pour plus d’informations, voir [Personnalisation des formulaires et composants adaptatifs](/help/forms/using/adaptive-forms-best-practices.md#customize-components).
* Il est recommandé de charger les modules de formulaire à l’aide de l’interface d’utilisation de Form Manager plutôt que de l’interface d’utilisation du gestionnaire de modules CRX, car le chargement de modules via le gestionnaires de modules CRX peut parfois entraîner des anomalies.
* AEM Forms vous permet de créer des formulaires adaptatifs basés sur les modèles de formulaires suivants. Les modèles de formulaire font office d’interface pour l’échange de données entre un formulaire et un système AEM et fournissent une structure XML pour le flux de données à l’intérieur et à l’extérieur d’un formulaire adaptatif. En outre, les modèles de formulaire imposent des règles et des contraintes aux formulaires adaptatifs sous la forme de schémas et de contraintes XFA.

   * **Aucun** : les formulaires adaptatifs créés avec cette option n’utilisent aucun modèle de formulaire. Les données XML générées à partir de ce type de formulaire présentent une structure plate avec des champs et des valeurs correspondantes.
   * **Schéma XML ou JSON** : les schémas XML et JSON représentent la structure dans laquelle les données sont générées ou utilisées par le système back-end de l’entreprise. Vous pouvez associer un schéma à un formulaire adaptatif et utiliser ses éléments pour ajouter du contenu dynamique à un formulaire adaptatif. Les éléments du schéma sont disponibles dans l’onglet Objet de modèle de données du navigateur de contenu pour la création de formulaires adaptatifs. Vous pouvez faire glisser et déposer les éléments du schéma pour créer le formulaire.
   * **Modèle de formulaire XDP** : il s’agit d’un modèle de formulaire idéal si vous investissez dans des formulaires HTML5 basés sur XFA. Il fournit une méthode directe de conversion des formulaires de type XFA en formulaires adaptatifs. Toutes les règles XFA existantes sont conservées dans les formulaires adaptatifs associés. Les formulaires adaptatifs qui en résultent prennent en charge les éléments XFA, tels que les validations, les événements, les propriétés et les modèles.
   * **Modèle de données de formulaire** : il s’agit du modèle de formulaire idéal si vous souhaitez intégrer les systèmes back-end tels que les bases de données, les services web et un profil utilisateur AEM pour préremplir des formulaires adaptatifs et enregistrer des données de formulaire envoyé dans les systèmes back-end. Un éditeur de modèle de données de formulaire vous permet de définir et de configurer des entités et des services dans un modèle de données de formulaire que vous pouvez utiliser pour créer des formulaires adaptatifs. Pour plus d’informations, voir [Intégration des données AEM Forms](/help/forms/using/data-integration.md).

Il est important de sélectionner avec soin le modèle de données qui correspond à vos besoins, tout en optimisant vos investissements existants dans les ressources XFA et XSD, le cas échéant. Il est recommandé d’utiliser le modèle XSD pour créer des modèles de formulaires, car le fichier XML généré contient les données selon l’expression XPATH définie par le schéma. L’utilisation du modèle XSD comme choix par défaut pour le modèle de données de formulaire s’avère également utile, dans la mesure où il découple le design du formulaire du système backend qui traite et consomme des données. Cela permet d’améliorer les performances du formulaire en raison d’un mappage un à un des champs de formulaire. En outre, la valeur BindRef du champ peut être utilisée comme XPATH de sa valeur de données dans le fichier XML.

Pour plus d’informations, voir [Création d’un formulaire adaptatif](/help/forms/using/creating-adaptive-form.md).

* Il existe des sections communes aux formulaires adaptatifs. Vous pouvez les identifier et définir une stratégie pour promouvoir la réutilisation du contenu. Les formulaires adaptatifs vous permettent de créer des fragments autonomes et de les réutiliser dans plusieurs formulaires. Vous pouvez également enregistrer un panneau dans un formulaire adaptatif en tant que fragment. Toute modification apportée à un fragment est répercutée dans tous les formulaires associés. Cela vous permet de réduire le temps de création et d’assurer la cohérence entre les formulaires. En outre, l’utilisation de fragments rend les formulaires adaptatifs plus légers, ce qui entraîne une amélioration de l’expérience de création, en particulier des formulaires volumineux. Pour plus d’informations, voir [Fragments de formulaire adaptatif](/help/forms/using/adaptive-form-fragments.md).

### Personnalisation des formulaires et composants adaptatifs {#customize-components}

* AEM Forms fournit des modèles prêts à l’emploi que vous pouvez utiliser pour créer des formulaires adaptatifs. Vous pouvez également créer vos propres modèles. AEM fournit des modèles statiques et modifiables.

   * Les modèles statiques sont définis et configurés par les développeurs.
   * Les modèles modifiables sont créés par les auteurs et autrices à l’aide de l’éditeur de modèles. L’éditeur de modèles permet de définir une structure de base et un contenu initial dans un modèle. Toute modification dans la couche de structure est répercutée dans tous les formulaires utilisant ce modèle. Le contenu initial peut inclure un thème préconfiguré, un service de préremplissage, une action d’envoi, etc. Cependant, ces paramètres peuvent être modifiés pour un formulaire à l’aide de l’éditeur de formulaires. Pour plus d’informations, voir [Modèles de formulaires adaptatifs](/help/forms/using/template-editor.md).

* Pour définir le style d’une instance ou d’un panneau spécifique, utilisez [le style en ligne](/help/forms/using/inline-style-adaptive-forms.md). Vous pouvez également définir une classe dans un fichier CSS et spécifier le nom de classe dans la propriété CSS Class du composant.
* Intégrez une bibliothèque cliente à un composant pour appliquer de manière constante des styles aux formulaires adaptatifs ou aux fragments utilisant ce composant. Pour plus d’informations, reportez-vous à la section [Création d’un composant de page de formulaire adaptatif](/help/forms/using/custom-adaptive-forms-templates.md).
* Appliquez des styles définis dans une bibliothèque cliente pour sélectionner les formulaires adaptatifs, en spécifiant le chemin d’accès à la bibliothèque cliente dans le champ relatif au chemin d’accès au fichier CSS des propriétés du conteneur de formulaire adaptatif.
* Pour créer une bibliothèque cliente de vos styles, vous pouvez configurer le fichier CSS personnalisé dans la bibliothèque cliente de base de l’éditeur de thème ou dans les propriétés du conteneur de formulaire.
* Les formulaires adaptatifs proposent des dispositions de panneau (dispositions réactives en onglet ou en accordéon par exemple) ainsi qu’un assistant pour contrôler la disposition des composants de formulaire. Vous pouvez créer des dispositions de panneau personnalisées et les rendre accessibles aux auteurs et autrices de formulaire. Pour plus d’informations, voir [Création de composants de disposition personnalisés pour les formulaires adaptatifs](/help/forms/using/custom-layout-components-forms.md).
* Vous pouvez également personnaliser les composants spécifiques d’un formulaire adaptatif tels que les champs et la disposition des panneaux.

   * Utilisez la fonctionnalité [Recouvrement](/help/sites-developing/overlays.md) d’AEM pour modifier une copie d’un composant. Il n’est pas recommandé de modifier les composants par défaut.
   * Pour personnaliser la disposition des composants de formulaire adaptatif prêts à l’emploi dans /libs, [créez des composants de disposition personnalisés](/help/forms/using/custom-layout-components-forms.md) en plus des [dispositions par défaut](/help/forms/using/layout-capabilities-adaptive-forms.md).
   * Intégrez les interactivités personnalisées en créant des widgets ou des apparences personnalisés. Il n’est pas recommandé de modifier les composants par défaut. Pour plus d’informations, consultez [Structure de l’apparence](/help/forms/using/introduction-widgets.md).

* Pour connaître les recommandations relatives à la gestion des données d’identification personnelle, reportez-vous à la section [Gestion des informations d’identification personnelle.](/help/forms/using/adaptive-forms-best-practices.md#p-handling-personally-identifiable-information-p)

### Création de modèles de formulaires

Vous pouvez créer un formulaire adaptatif à l’aide des modèles de formulaires activés dans **Explorateur de configurations**. Pour activer les modèles de formulaire, reportez-vous à [Création d’un modèle de formulaire adaptatif](https://experienceleague.adobe.com/docs/experience-manager-learn/forms/creating-your-first-adaptive-form/create-adaptive-form-template.html?lang=fr).

Vous pouvez également charger les modèles de formulaires à partir des packages de formulaires adaptatifs créés sur une autre machine de création. Les modèles de formulaires sont disponibles en installant les [packages aemforms-references-*](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=fr). Nous recommandons de suivre les bonnes pratiques suivantes :

* Nous recommandons le mode d’exécution **nosamplecontent** uniquement pour les nœuds d’auteur et non pour les nœuds de publication.
* La création de ressources telles que les formulaires adaptatifs, les thèmes, les modèles ou les configurations cloud s’effectue uniquement sur les nœuds d’auteur, qui peuvent être publiés sur les nœuds de publication configurés.
Pour plus d’informations, reportez-vous à [Publication et annulation de la publication de formulaires et de documents](https://experienceleague.adobe.com/docs/experience-manager-65/forms/publish-process-aem-forms/publishing-unpublishing-forms.html?lang=fr).
* Le package du module complémentaire Forms est nécessaire pour la création et la publication, afin de prendre en charge les opérations de service de document. Il peut donc être considéré comme une dépendance.
Si vous souhaitez uniquement des packages d’exemples de modèle, de thèmes et de documents d’enregistrement liés à Forms, vous pouvez les télécharger à partir de [aemforms-references-* packages](https://experienceleague.adobe.com/docs/experience-manager-65/forms/publish-process-aem-forms/publishing-unpublishing-forms.html?lang=fr).

Pour plus d’informations, reportez-vous aux bonnes pratiques dans [Présentation de la création de formulaires adaptatifs](/help/forms/using/introduction-forms-authoring.md).

## Création de formulaires adaptatifs {#author-adaptive-forms}

### Utilisation de l’interface utilisateur optimisée pour les écrans tactiles pour la création {#using-touch-optimized-ui-for-authoring}

* Utilisez le navigateur d’objets de la barre latérale pour accéder rapidement aux champs dans la partie la plus basse de la hiérarchie du formulaire. Vous pouvez utiliser la zone de recherche pour rechercher des objets dans le formulaire ou l’arborescence d’objets pour passer d’un objet à un autre.
* Pour afficher et modifier les propriétés d’un composant dans le navigateur de composants dans la barre latérale, sélectionnez le composant, puis cliquez sur ![cmppr-1](assets/cmppr-1.png). Vous pouvez également double-cliquer sur un composant pour afficher ses propriétés dans l’explorateur de propriétés.
* Utilisez les raccourcis clavier pour effectuer des actions rapides sur vos formulaires. Voir [Raccourcis clavier AEM Forms](/help/forms/using/keyboard-shortcuts.md).

* L’utilisation des composants de formulaire adaptatif est recommandée uniquement dans les pages de formulaire adaptatif. Les composants dépendent de leur hiérarchie parent. Par conséquent, ne les utilisez pas dans une page AEM.

Consultez également les descriptions des composants et les bonnes pratiques dans [Introduction à la création de formulaires adaptatifs](/help/forms/using/introduction-forms-authoring.md).

### Utilisation de règles dans les formulaires adaptatifs {#using-rules-in-adaptive-forms}

AEM Forms fournit un [éditeur de règles](/help/forms/using/rule-editor.md) qui vous permet de créer des règles pour ajouter un comportement dynamique aux composants de formulaire adaptatif. Grâce à ces règles, vous pouvez évaluer des conditions et déclencher des actions sur des composants, comme par exemple afficher ou masquer des champs, calculer des valeurs, dynamiser une liste déroulante et plus encore.

L’éditeur de règles fournit un éditeur visuel et un éditeur de code pour la définition de règles. Lorsque vous définissez des règles à l’aide de l’éditeur de code, vous devez prendre en compte les éléments suivants :

* Utilisez des noms uniques et pertinents pour les champs de formulaire et les composants afin d’éviter tout conflit potentiel lors de la définition des règles.
* Utilisez l’opérateur `this` pour un composant afin d’y faire mention lors de l’expression d’une règle. Ainsi, la règle reste valide même si le nom du composant est modifié. Par exemple, `field1.valueCommit script: this.value > 10`.

* Utilisez les noms de composant lorsque vous faites référence à d’autres composants de formulaire. Utilisez la propriété `value` pour récupérer la valeur d’un champ ou d’un composant. Par exemple, `field1.value`.

* Désignez les composants selon une hiérarchie relative unique afin d’éviter tout conflit. Par exemple, `parentName.fieldName`.

* Lorsque vous manipulez des règles complexes ou fréquemment utilisées, pensez à définir la logique commerciale comme fonctions dans une bibliothèque cliente distincte que vous pouvez spécifier et réutiliser dans les formulaires adaptatifs. La bibliothèque client doit être une bibliothèque autonome et ne doit donc avoir aucune dépendance externe, à l’exception de jQuery et Underscore.js. Vous pouvez également utiliser la bibliothèque cliente pour imposer la [revalidation côté serveur](/help/forms/using/configuring-submit-actions.md#server-side-revalidation-in-adaptive-form) des données de formulaire envoyées.
* Les formulaires adaptatifs fournissent un ensemble d’API que vous pouvez utiliser pour communiquer et effectuer des actions sur les formulaires adaptatifs. Les principales API sont les suivantes. Pour plus d’informations, voir [Référence d’API de bibliothèque JavaScript pour les formulaires adaptatifs](https://adobe.com/go/learn_aemforms_documentation_63_fr).

   * `guideBridge.reset()` : permet de réinitialiser un formulaire.
   * `guideBridge.submit()` : permet de soumettre un formulaire.
   * `guideBridge.setFocus(somExp, focusOption, runCompletionExp)` : permet de se concentrer sur un champ.
   * `guideBridge.validate(errorList, somExpression, focus)` : permet de valider un formulaire.
   * `guideBridge.getDataXML(options)` : permet d’obtenir les données de formulaire en tant que XML.
   * `guideBridge.resolveNode(somExpression)` : permet d’obtenir un objet de formulaire.
   * `guideBridge.setProperty(somList, propertyName, valueList)` : permet de définir la propriété d’un objet de formulaire.
   * En outre, vous pouvez utiliser les propriétés de champ suivantes :

      * `field.value` pour modifier la valeur d’un champ ;
      * `field.enabled` pour activer/désactiver un champ ;
      * `field.visible` pour modifier la visibilité d’un champ.

* Les auteurs et autrices de formulaires adaptatifs peuvent avoir besoin d’écrire du code JavaScript pour créer une logique métier dans un formulaire. Bien que JavaScript soit puissant et efficace, il est susceptible de compromettre les attentes en matière de sécurité. Par conséquent, vous devez vous assurer que l’auteur ou l’autrice du formulaire est une personne de confiance et qu’il existe des processus pour examiner et approuver le code JavaScript avant qu’un formulaire ne soit mis en production. L’administrateur ou l’administratrice peut restreindre l’accès à l’éditeur de règles de certains groupes d’utilisateurs et d’utilisatrices en fonction de leur rôle ou de leur fonction. Voir [Autorisation d’accès à l’éditeur de règles pour des groupes d’utilisateurs et d’utilisatrices sélectionnés](/help/forms/using/rule-editor-access-user-groups.md).
* Vous pouvez utiliser des expressions dans les règles pour rendre les formulaires adaptatifs dynamiques. Toutes les expressions sont des expressions JavaScript valides qui utilisent des API de modèle de script pour les formulaires adaptatifs. Ces expressions renvoient des valeurs de certains types. Pour plus d’informations sur les expressions et les meilleures pratiques associées, voir [Expressions des formulaires adaptatifs](/help/forms/using/adaptive-form-expressions.md).

* Adobe recommande d’utiliser des opérations synchrones JavaScript plutôt que asynchrones lors de la création de règles avec l’éditeur de règles. L’utilisation d’opérations asynchrones est fortement déconseillée. Cependant, si vous vous trouvez dans une situation où les opérations asynchrones sont inévitables, il est essentiel de mettre en œuvre les fonctions de fermeture (closures) de JavaScript. Vous pouvez ainsi vous protéger de manière efficace contre toute situation de concurrence potentielle, en veillant à ce que vos mises en œuvre de règles offrent des performances optimales et maintiennent la stabilité. 

  Supposons, par exemple, que nous devions récupérer des données d’une API externe, puis appliquer certaines règles basées sur ces données. Nous utilisons une fermeture pour gérer l’appel API asynchrone et nous assurer que les règles sont appliquées après la récupération des données. Voici l’exemple de code :

  ```JavaScript
       function fetchDataFromAPI(apiEndpoint, callback) {
        // Simulate asynchronous API call with setTimeout
        setTimeout(() => {
          // Assuming the API call is successful, we receive some data
          const data = {
            someValue: 42,
          };
          // Invoke the callback with the fetched data
          callback(data);
        }, 2000); // Simulate a 2-second delay for the API call
      }
      // Rule implementation using Closure
      function ruleImplementation(apiEndpoint) {
        // Using a closure to handle the asynchronous API call and rule application
        // say you have set this value in street field inside address panel
        var streetField = address.street;
        fetchDataFromAPI(apiEndpoint, (data) => {
          streetField.value = data.someValue;
        });
      }
      // Example usage of the rule implementation
      const apiEndpoint = "https://example-api.com/data";
      ruleImplementation(apiEndpoint);
  ```

  Dans cet exemple, `fetchDataFromAPI` simule un appel API asynchrone à l’aide de `setTimeout`. Une fois les données récupérées, elle appelle la fonction de rappel fournie, qui correspond à la fermeture permettant de gérer l’application de la règle suivante. La fonction `ruleImplementation` contient la logique de règle.


### Utilisation des thèmes {#working-with-themes}

Les thèmes de formulaires adaptatifs vous permettent de créer des styles réutilisables pouvant être appliqués à tous les formulaires pour une apparence et un style homogènes. Il est recommandé d’utiliser les thèmes pour définir le style des composants et des panneaux de formulaire. Voici quelques bonnes pratiques relatives aux thèmes :

* Utilisez la bibliothèque de ressources pour appliquer rapidement les styles de texte, l’arrière-plan et les images. Lorsqu’un style est ajouté à la bibliothèque de ressources, il est disponible pour d’autres thèmes et dans le mode Style de l’éditeur de formulaires.
* Appliquez des paramètres globaux tels que la police et l’arrière-plan de page à l’aide du sélecteur de niveau page.
* Utilisez les bibliothèques clientes pour importer des styles existants ou avancés dans vos thèmes.
* Vous pouvez remplacer le style pour des champs, des panneaux ou des boutons spécifiques dans un calque de style de formulaire.
* Si un thème ne répond pas à vos besoins en termes de style, vous pouvez utiliser des classes prédéfinies telles que guideFieldNode, guideFieldLabel, guideFieldWidget et guidePanelNode pour appliquer un style commun à tous les formulaires.

Pour plus d’informations, voir [Thèmes](/help/forms/using/themes.md).

### Optimisation des performances de formulaires complexes et volumineux {#optimizing-performance-of-large-and-complex-forms}

Les auteurs et autrices de formulaires et les utilisateurs et utilisatrices finaux sont généralement confrontés à des problèmes de performances lors du chargement de formulaires volumineux en mode création ou au moment de l’exécution. À mesure que le nombre d’objets (champs et panneaux) dans un formulaire augmente, les performances de création et d’exécution commencent à diminuer. Ainsi, il est impossible pour plusieurs auteurs et autrices de travailler simultanément à la création d’un formulaire.

Tenez compte des bonnes pratiques suivantes pour résoudre les problèmes de performances liés aux formulaires volumineux :

* Il est recommandé de créer si possible des formulaires adaptatifs à l’aide du modèle de données de formulaire XSD, et ce, même lors de la conversion d’un XFA en formulaire adaptatif.
* Incluez uniquement les champs et les panneaux dans les formulaires adaptatifs qui capturent les informations de l’utilisateur ou de l’utilisatrice. Maintenez le contenu statique au minimum ou utilisez les URL pour les ouvrir dans une fenêtre séparée.
* Bien que chaque formulaire soit conçu pour un rôle spécifique, certains segments sont communs à la plupart des formulaires. Par exemple, les informations personnelles, l’adresse, les détails du poste, etc. Créez des [fragments de formulaire adaptatif](/help/forms/using/adaptive-form-fragments.md) pour les éléments et sections de formulaire communs et utilisez-les dans les formulaires. Vous pouvez également enregistrer en tant que fragment un panneau d’un formulaire existant. Toute modification apportée à un fragment est répercutée dans tous les formulaires adaptatifs associés. Cette fonction favorise la création en collaboration : plusieurs auteurs peuvent ainsi travailler simultanément sur différents fragments composant un formulaire.

   * Envisagez de créer des fragments de formulaire même pour les sections non réutilisables lors de la création de formulaire. À mesure que les formulaires se développent en taille et en complexité, leur ventilation en fragments peut simplifier considérablement le processus de création et faciliter leur gestion. Cette approche vous permet de vous concentrer sur des parties plus petites et plus gérables du formulaire, plutôt que de traiter le formulaire entier en une seule fois.
   * Comme pour les formulaires adaptatifs, il est recommandé de définir tous les scripts personnalisés et de style spécifiques aux fragments dans la bibliothèque cliente à l’aide de la boîte de dialogue du conteneur de fragments. Tentez également de créer des fragments autonomes qui ne dépendent pas d’objets extérieurs.
   * Évitez d’utiliser des scripts de fragments croisés. Si vous devez désigner un objet situé hors du fragment, essayez de l’intégrer au formulaire parent. Si l’objet doit demeurer dans un autre fragment, mentionnez son nom dans le script.

* Utilisez l’option Enregistrer et reprendre avec l’enregistrement automatique pour enregistrer régulièrement le formulaire adaptatif et permettre aux utilisateurs et aux utilisatrices de revenir plus tard pour le remplir.
* Configurez les fragments à charger en différé. Au moment de l’exécution, le fragment qui doit être chargé en différé n’est rendu que lorsqu’il est nécessaire. Cette option permet de réduire considérablement le temps de chargement des formulaires volumineux. Elle peut également être utilisée dans des fragments avec des panneaux répétables. Pour plus d’informations, voir [Configuration du chargement différé](/help/forms/using/lazy-loading-adaptive-forms.md).

   * Ne configurez pas le chargement différé sur les fragments dans une disposition en grille réactive ou dans le premier panneau.
   * Les composants des pièces jointes et des conditions générales ne sont pas pris en charge dans les fragments chargés en différé.
   * Marquez une valeur dans un panneau chargé en différé comme « Utiliser la valeur globalement » si cette valeur est utilisée dans une autre partie du formulaire afin que la valeur soit disponible lorsque le panneau de contenu est déchargé.
   * Pensez à créer des règles de visibilité pour les fragments qui doivent s’afficher ou être masqués en fonction d’une condition.
* Définissez la valeur de **Nombre d’appels par requête** dans le **Servlet principal Apache Sling** sur un nombre assez élevé. Cela permet au serveur Forms d’autoriser des appels supplémentaires. La configuration indique une valeur par défaut de 1 500. La valeur, 1 500 appels, correspond à d’autres composants d’Experience Manager tels que Sites et Assets. La valeur définie par défaut des formulaires adaptatifs est 20 000. Si vous rencontrez l’erreur `too many calls` dans les journaux ou si le rendu du formulaire échoue, essayez de définir la valeur sur un nombre plus élevé pour résoudre le problème. Si le nombre d’appels est supérieur à 20 000, cela signifie que le formulaire est complexe et qu’il peut prendre un certain temps pour générer le rendu du formulaire dans le navigateur. Cela ne se produit que lors du premier chargement du formulaire. Une fois le formulaire mis en cache, cela n’a aucun impact significatif sur les performances.

### Considérations relatives à la taille du DOM et aux performances du navigateur

Lors de la création de formulaires adaptatifs volumineux et complexes, il est important de tenir compte de l’impact de la taille du DOM sur le rendu et les performances :

* **Impact de la taille du DOM** : bien qu’il n’existe pas de limite stricte pour la taille du DOM dans AEM Forms, une taille excessive peut avoir un impact significatif sur les performances, en particulier lors de la gestion des fragments chargés en différé. Les structures de DOM volumineuses nécessitent davantage de mémoire et de temps de traitement pour le rendu et la manipulation.

* **Différences de rendu entre les navigateurs** : les performances de rendu peuvent varier considérablement selon les navigateurs et les appareils. Certains moteurs de rendu de navigateur traitent différemment les mises à jour de DOM dynamiques, avec des approches différentes pour les recalculs, les reflows et les repaints de style. Cela est particulièrement visible avec le contenu volumineux chargé dynamiquement. Dans certains navigateurs, chaque manipulation importante du DOM peut déclencher un recalcul complet de la disposition et du repaint de la page, ce qui intensifie les problèmes de performances avec les formulaires volumineux ou complexes.

* **Facteurs de performance** : plusieurs facteurs affectent les performances du chargement différé :
   * Taille et complexité des fragments
   * Styles CSS appliqués aux éléments
   * Nombre de reflows déclenchés par les mises à jour dynamiques
   * Fonctionnalités de l’appareil et du navigateur

* **Impact réel** : dans les cas observés, les formulaires avec des tailles de DOM d’environ 400 Ko ont subi des retards de rendu importants allant jusqu’à 15 secondes sur certains navigateurs. Ces retards ne sont pas uniquement dus à la taille du fragment, mais également au traitement CSS et aux redirections de page déclenchés lors de l’insertion de contenu dynamique.

**Bonnes pratiques de gestion de la taille des DOM :**

* Pour le contenu statique, pensez à utiliser les fragments de contenu AEM au lieu d’insérer dynamiquement des blocs HTML volumineux par le biais du chargement différé. Cette approche peut réduire les reflows, les repaints et le temps d’exécution de JavaScript, améliorant ainsi les performances globales de chargement des pages.

* Lorsque les fragments doivent être dynamiques et chargés en différé, divisez les fragments volumineux en fragments plus petits et plus faciles à gérer et ne chargez que les sections requises, le cas échéant.

* Mettez en œuvre des modèles de divulgation progressive, en révélant des champs de formulaire supplémentaires uniquement lorsque cela est nécessaire en fonction des entrées de l’utilisateur ou de l’utilisatrice.

* Testez vos formulaires sur plusieurs navigateurs et appareils, en particulier lorsque vous utilisez des fragments chargés en différé, afin d’assurer des performances cohérentes entre les différents environnements.

* Surveillez et optimisez le CSS utilisé dans vos formulaires, car un CSS volumineux ou mal structuré peut augmenter considérablement le temps de rendu, en particulier lors des mises à jour de contenu dynamique.

Pour plus d’informations techniques sur la façon dont les différents moteurs de rendu du navigateur gèrent les mises à jour, les reflows et les repaints des DOM, pensez à explorer la documentation des moteurs de navigateur, telle que celles fournies par divers fournisseurs de navigateurs.

### Préremplissage des formulaires adaptatifs {#prefilling-adaptive-forms}

Vous pouvez préremplir des champs de formulaire adaptatif avec des données récupérées du serveur backend pour aider les utilisateurs et utilisatrices à remplir rapidement le formulaire et éviter de saisir des erreurs.

* AEM Forms fournit un service de préremplissage pour lire les données d’un fichier XML de données prédéfini et préremplir les champs d’un formulaire adaptatif avec le contenu du fichier XML prérempli.
* Les données XML de préremplissage doivent être conformes au schéma du modèle de formulaire associé au formulaire adaptatif.
* Incluez les sections `afBoundedData` et `afUnBoundedData` dans le fichier XML prérempli pour préremplir les champs liés et non liés d’un formulaire adaptatif.

* Pour les formulaires adaptatifs basés sur un modèle de données de formulaire, AEM Forms fournit un service de préremplissage de modèles de données de formulaire prêts à l’emploi. Le service de préremplissage récupère les sources de données pour les objets de modèle de données dans le formulaire adaptatif et préremplit les valeurs de champ lors du rendu du formulaire.
* Vous pouvez également utiliser les formulaires adaptatifs de préremplissage de fichiers, CRX, service ou protocoles HTTP.
* AEM Forms prend en charge les services de préremplissage personnalisés que vous pouvez intégrer en tant que service OSGi pour préremplir les formulaires adaptatifs.

Pour plus d’informations, voir [Préremplir des champs de formulaire adaptatif](/help/forms/using/prepopulate-adaptive-form-fields.md).

### Signature et envoi de formulaires adaptatifs {#signing-and-submitting-adaptive-forms}

Les formulaires adaptatifs requièrent des actions Envoyer pour traiter les données spécifiées par lʼutilisateur ou l’utilisatrice. Une action Envoyer détermine la tâche effectuée sur les données envoyées à l’aide d’un formulaire adaptatif.

* Il existe plusieurs actions d’envoi disponibles prêtes à l’emploi dans les formulaires adaptatifs. Pour plus de détails, voir [Configurer l’action Envoyer](/help/forms/using/configuring-submit-actions.md).
* Vous pouvez créer une action d’envoi personnalisée si les actions d’envoi par défaut ne remplissent pas votre cas d’utilisation. Pour plus d’informations, voir [Création d’une action Envoyer personnalisée pour les formulaires adaptatifs](/help/forms/using/custom-submit-action-form.md).
* Incluez des validations côté serveur pour empêcher l’envoi de données non valides.

Vous pouvez tirer parti de l’expérience multi-signature d’Adobe Sign dans les formulaires adaptatifs. Tenez compte des points suivants lors de la configuration d’Adobe Sign dans les formulaires adaptatifs. Pour plus d’informations, voir [Utiliser Adobe Sign dans un formulaire adaptatif](/help/forms/using/working-with-adobe-sign.md).

* Le formulaire adaptatif comprenant Adobe Sign est envoyé uniquement après que tous les signataires ont signé le formulaire. Les formulaires affichent l’état En attente de signature jusqu’à ce que le formulaire soit signé par tous les signataires.
* Vous pouvez configurer une expérience de signature dans le formulaire ou rediriger les signataires vers une page de signature lors de l’envoi.
* Configurez une expérience de signature séquentielle ou parallèle, selon le cas.

### Génération d’un document d’enregistrement {#generating-document-of-record}

Un document d’enregistrement (DE) est une version PDF aplatie d’un formulaire adaptatif que vous pouvez imprimer, signer ou archiver.

* Selon le modèle de données de formulaire sur lequel un formulaire adaptatif est basé, vous pouvez configurer un modèle de document d’enregistrement comme suit :

   * **Modèle de formulaire XFA** : utilisez le fichier XDP associé comme modèle de document d’enregistrement.
   * **Schéma XSD** : utilisez le modèle XFA associé qui utilise le même schéma XML que le formulaire adaptatif.
   * **Aucun** : utilisez un document d’enregistrement généré automatiquement.

* Configurez l’en-tête, le pied de page, les images, la couleur, la police, etc. à partir de l’onglet Document d’enregistrement de l’éditeur de formulaires adaptatifs.
* Utilisez `DoRService` pour générer le document d’enregistrement par programmation.
* Excluez les champs masqués du document d’enregistrement.
* Utilisez le paramètre de demande `afAcceptLang` pour afficher le document d’enregistrement dans d’autres paramètres régionaux.

<!--### Debugging and testing adaptive forms {#debugging-and-testing-adaptive-forms}

[AEM Chrome Plug-in](https://adobe-consulting-services.github.io/acs-aem-tools/aem-chrome-plugin/) is a browser extension for Google Chrome that provides tools for debugging adaptive forms. Form authors and developers can use these tools to:

* Identify bottlenecks and optimize performance of form rendering
* Debug keywords and bindRef errors in the form
* Enable and configure logs
* Debug rules and scripts in the form
* Explore and learn about guideBridge APIs

For more information, see [AEM Chrome Plug-in - Adaptive Form](https://adobe-consulting-services.github.io/acs-aem-tools/aem-chrome-plugin/adaptive-form/).-->

### Validation des formulaires adaptatifs sur le serveur AEM {#validating-adaptive-forms-on-aem-server}

Des validations côté serveur sont nécessaires pour empêcher toute tentative de contournement des validations sur le client et tout compromis possible entre les envois de données et les violations des règles de fonctionnement. Les validations côté serveur sont exécutées sur le serveur en chargeant la bibliothèque cliente requise.

* Incluez des fonctions dans une bibliothèque cliente pour valider les expressions dans les formulaires adaptatifs et spécifiez la bibliothèque cliente dans la boîte de dialogue du conteneur de formulaires adaptatifs. Pour plus d’informations, voir [Revalidation côté serveur](/help/forms/using/configuring-submit-actions.md#p-server-side-revalidation-in-adaptive-form-p).
* La validation côté serveur permet de valider le modèle de formulaire. Il est recommandé de créer une bibliothèque client séparée pour les validations et de ne pas la mélanger à d’autres éléments. Par exemple, ne placez pas le style HTML et la manipulation DOM dans la même bibliothèque client.

### Traduction des formulaires adaptatifs {#localizing-adaptive-forms}

AEM fournit des workflows de traduction que vous pouvez utiliser pour traduire les formulaires adaptatifs. Pour plus d’informations, voir [Utilisation du workflow de traduction AEM pour traduire les formulaires adaptatifs](/help/forms/using/using-aem-translation-workflow-to-localize-adaptive-forms.md).

Voici quelques bonnes pratiques à appliquer lors de la traduction de formulaires adaptatifs :

* Utilisez les fragments de formulaire adaptatif pour les éléments courants des formulaires et localisez les fragments. Cela permet de traduire un fragment une seule fois et de répercuter la traduction dans tous les formulaires dans lesquels le fragment traduit est utilisé.
* Les modifications telles que l’ajout d’un nouveau composant ou l’application d’un script dans un formulaire traduit ne sont pas automatiquement traduites. Par conséquent, vous devez finaliser un formulaire avant de le localiser pour éviter plusieurs cycles de localisation.
* Utilisez le paramètre de demande `afAcceptLang` pour remplacer la langue du navigateur et pour rendre le formulaire dans les paramètres régionaux spécifiés. Par exemple, l’URL suivante force à effectuer le rendu du formulaire en japonais, indépendamment des paramètres régionaux spécifiés dans les paramètres du navigateur :

  `https://'[server]:[port]'/<contextPath>/<formFolder>/<formName>.html?wcmmode=disabled&afAcceptLang=ja`

* AEM Forms prend actuellement en charge la localisation du contenu des formulaires adaptatifs vers l’anglais (en), l’espagnol (es), le français (fr), l’italien (it), l’allemand (de), le japonais (ja), le portugais du Brésil (pt-BR), le chinois (zh-CN), le chinois de Taïwan (zh-TW) et le coréen (ko-KR). Cependant, vous pouvez ajouter la prise en charge de nouveaux paramètres régionaux pour les formulaires adaptatifs à l’exécution. Pour plus d’informations, voir [Prise en charge de nouveaux paramètres régionaux pour la localisation de formulaires adaptatifs](/help/forms/using/supporting-new-language-localization.md).

## Préparation du projet de formulaires pour la production {#prepare-forms-project-for-production}

### Ajout d’un serveur de traitement de formulaires {#adding-forms-processing-server}

Vous pouvez configurer une instance supplémentaire du serveur AEM Forms situé derrière le pare-feu dans une zone sécurisée. Vous pouvez utiliser cette instance pour :

* **Traitement par lots** : tâches récurrentes ou programmées par lots comportant une charge importante. Impression d’instructions, génération de correspondances et utilisation de services de document tels que PDF Generator, Output et Assembler, par exemple.
* **Stockage des données à caractère personnel** : enregistrez les données à caractère personnel sur le serveur de traitement. Ceci n’est pas nécessaire si vous utilisez déjà un fournisseur de stockage personnalisé pour le stockage des données à caractère personnel.

### Déplacement d’un projet vers un autre environnement {#moving-project-to-another-environment}

Vous devez souvent déplacer vos projets AEM d’un environnement à un autre. Voici quelques éléments essentiels à retenir lors du déplacement :

* Effectuez une sauvegarde de vos bibliothèques clientes existantes, de votre code personnalisé et de vos configurations.
* Déployez manuellement les packages et correctifs de produits dans l’ordre spécifié dans le nouvel environnement.
* Déployez manuellement des packages de code et des bundles spécifiques au projet et sous la forme d’un package ou d’un bundle distinct sur le nouveau serveur AEM.
* (*AEM Forms on JEE uniquement*) Déployez manuellement les LCA et les DSC sur le serveur de processus des formulaires.
* Utilisez la fonctionnalinté [Export-Import](/help/forms/using/import-export-forms-templates.md) pour déplacer des ressources vers le nouvel environnement. Vous pouvez également configurer l’agent de réplication et publier les ressources.
* Lorsque vous effectuez une mise à niveau, remplacez toutes les API et fonctionnalités obsolètes par de nouvelles API et fonctionnalités.

### Configurer AEM {#configuring-aem}

Voici quelques bonnes pratiques pour configurer AEM afin d’améliorer les performances globales :

* Activez la compression de la bibliothèque client HTML pour Javascript et CSS à partir de la console Felix.
* Masquez toutes les bibliothèques clientes sous `/etc.clientlibs/fd` et toutes les bibliothèques clientes personnalisées supplémentaires dans AEM Dispatcher pour améliorer la réactivité et la sécurité des formulaires publiés. Pour plus d’informations, reportez-vous à la section [Dispatcher](https://helpx.adobe.com/fr/experience-manager/dispatcher/using/dispatcher.html).

* Ne mettez pas en cache les chemins d’accès `/content/forms/af/` et `/content/dam/formsanddocuments/*`. Pour plus d’informations sur la configuration de la mise en cache de formulaires adaptatifs, voir [Mise en cache de formulaires adaptatifs](/help/forms/using/configure-adaptive-forms-cache.md).

* Activez le HTML via le module de compression de serveur web. Pour plus d’informations, voir [Optimisation des performances du serveur AEM Forms](/help/forms/using/performance-tuning-aem-forms.md).
* Augmentez la configuration des appels par requête pour les formulaires volumineux. Voir [Optimisation des performances de formulaires complexes et volumineux](/help/forms/using/adaptive-forms-best-practices.md#optimizing-performance-of-large-and-complex-forms).
* Créez des [pages d’erreur personnalisées affichées par le gestionnaire d’erreur](https://experienceleague.adobe.com/docs/experience-manager-65/developing/platform/customizing-errorhandler-pages.html?lang=fr).
* Sécurisez le serveur AEM Forms.

   * Utilisez le mode d’exécution `nosamplecontent` pour vous assurer qu’aucun exemple de contenu ou d’utilisateur ne soit déployé sur le serveur de production. Voir [Exécution d’AEM selon le mode prêt pour la production](/help/sites-administering/production-ready.md).

* La taille du tas doit être de 8 Go au minimum. Pour connaître les autres paramètres, voir [Optimisation des performances du serveur AEM Forms](/help/forms/using/performance-tuning-aem-forms.md).
* Utilisez les sessions utilisateurs du service au lieu des sessions d’administration pour exécuter les tâches au niveau du service. Pour plus d’informations, voir [Authentification du service](https://sling.apache.org/documentation/the-sling-engine/service-authentication.html).

>[!VIDEO](https://vimeo.com/)

### Configuration du stockage externe pour les données de brouillons et de formulaires envoyés {#external-storage}

Dans un environnement de production, il est recommandé de ne pas stocker des données de formulaire de brouillon ou envoyées dans le référentiel AEM. L’implémentation par défaut des actions d’envoi Stocker, Stocker le contenu et Stocker le PDF du portail Formulaires stocke les données de formulaire dans le référentiel AEM. Ces actions d’envoi sont destinées uniquement à des fins de démonstration. En outre, les fonctions Enregistrer et reprendre et Enregistrement automatique stockent les données dans le portail par défaut. Par conséquent, prenez en compte les recommandations suivantes :

* **Stockage des données de brouillon** : si vous utilisez la fonction Brouillon des formulaires adaptatifs, vous devez implémenter une SPI (Service Provide Interface) personnalisée pour le stockage des données de brouillon dans un espace de stockage plus sécurisé comme une base de données. Pour plus d’informations, voir [Exemple d’intégration d’un composant de brouillons et d’envois à la base de données](/help/forms/using/integrate-draft-submission-database.md).

* **Stockage des données d’envoi** : si vous utilisez l’envoi de stockage du portail de formulaires, vous devez implémenter une SPI personnalisée pour stocker les données d’envoi dans une base de données. Voir [Exemple d’intégration d’un composant brouillons &amp; envois à la base de données](/help/forms/using/integrate-draft-submission-database.md) pour obtenir un exemple d’intégration.

  Vous pouvez également écrire une action d’envoi personnalisée qui stocke les données de formulaires et les pièces jointes dans un espace de stockage sécurisé. Pour plus d’informations, voir [Créer une action Envoyer personnalisée pour les formulaires adaptatifs](/help/forms/using/custom-submit-action-form.md).

* **Longueur de l’ID du brouillon** : lorsque vous enregistrez un formulaire adaptatif en tant que brouillon, un ID de brouillon est généré pour identifier de manière unique le brouillon. La valeur minimale pour la longueur du champ d’ID du brouillon est de 26 caractères. Adobe recommande de définir la longueur de l’ID du brouillon sur 26 caractères ou plus.

### Gestion des données à caractère personnel {#handling-personally-identifiable-information}

L’un des principaux défis pour les entreprises est de savoir comment gérer les données à caractère personnel (DCP). Voici quelques bonnes pratiques qui vous aideront à gérer ces données :

* Utilisez un stockage sécurisé et externe, tel qu’une base de données, pour stocker les données des brouillons et des formulaires envoyés. Voir [Configuration du stockage pour les données de brouillons et de formulaires envoyés](/help/forms/using/adaptive-forms-best-practices.md#external-storage).
* Utilisez le composant de formulaire Conditions générales pour obtenir le consentement explicite de l’utilisateur ou l’utilisatrice avant d’activer l’enregistrement automatique. Dans ce cas, activez l’enregistrement automatique uniquement lorsque l’utilisateur ou l’utilisatrice accepte les conditions du composant Conditions générales.

## Sélectionnez l’éditeur de règles, l’éditeur de code ou les bibliothèques clientes personnalisées pour votre formulaire adaptatif. {#RuleEditor-CodeEditor-ClientLibs}

### Éditeur de règles {#rule-editor}

<!--The AEM Forms Rule Editor offers predefined functions for defining rules in adaptive forms without extensive programming. It facilitates the implementation of conditional logic, data validation, and integration with external sources. This visual interface is especially valuable for business users and form designers, enabling them to create dynamic and complex rules with ease, here we discusss few use cases where rule editor allows you to:-->

L’éditeur de règles d’AEM Forms fournit une interface visuelle pour la création et la gestion des règles, ce qui réduit la nécessité d’un codage étendu. Il peut s’avérer particulièrement utile pour les utilisateurs et utilisatrices professionnels ou les personnes concevant des formulaires qui ne possèdent pas des compétences de programmation avancées, mais qui doivent définir et gérer des règles commerciales dans les formulaires. Nous examinons ici quelques cas d’utilisation où l’éditeur de règles vous permet ce qui suit :

* <!-- Allows you --> Définir des règles commerciales pour vos formulaires sans avoir besoin d’une programmation étendue.
* <!-- Use the Rule Editor when you need --> Implémenter une logique conditionnelle dans vos formulaires. Cela inclut l’affichage ou le masquage des éléments de formulaire, la modification des valeurs de champ selon certaines conditions ou la modification dynamique du comportement de vos formulaires.
* <!--When you want --> Pour appliquer des règles de validation de données aux envois de formulaire, l’éditeur de règles peut être utilisé pour définir des conditions de validation.
* <!-- When you need --> Pour intégrer vos formulaires à des sources de données externes (FDM) ou des services, l’éditeur de règles vous permet de définir des règles pour la récupération, l’affichage ou la manipulation des données lors des interactions avec les formulaires.
* <!-- If you want -->Pour créer des formulaires dynamiques et interactifs qui répondent aux actions de l’utilisateur ou de l’utilisatrice, l’éditeur de règles vous permet de définir des règles qui régissent le comportement des éléments de formulaire en temps réel.

L’éditeur de règles est disponible pour les composants de base et les composants principaux d’AEM Forms.

### Éditeur de code {#code-editor}

L’éditeur de code est un outil d’Adobe Experience Manager (AEM) Forms qui vous permet d’écrire des scripts et du code personnalisés pour des fonctionnalités plus complexes et avancées dans vos formulaires. Nous discutons ici de quelques cas d’utilisation :

* Lorsque vous devez implémenter une logique ou un comportement côté client personnalisé qui va au-delà des fonctionnalités de l’éditeur de règles AEM Forms. L’éditeur de code vous permet d’écrire du code JavaScript pour gérer des interactions, des calculs ou des validations complexes.
* Si votre formulaire nécessite un traitement côté serveur ou une intégration à des systèmes externes, vous pouvez utiliser l’éditeur de code pour écrire un script côté serveur personnalisé. Vous pouvez accéder à l’API guideBridge dans l’éditeur de code pour implémenter toute logique complexe sur les événements et les objets de formulaire.
* Lorsque vous avez besoin d’interfaces utilisateur hautement personnalisées qui vont au-delà des fonctionnalités standard des composants AEM Forms, l’éditeur de code vous permet d’implémenter des styles, des comportements personnalisés ou même de créer des composants de formulaire personnalisés.
* Si votre formulaire implique des opérations asynchrones telles que le chargement asynchrone des données, vous pouvez utiliser l’éditeur de code pour gérer ces opérations par le biais d’un code JavaScript asynchrone personnalisé.

Il est important de noter que l’utilisation de l’éditeur de code nécessite une bonne compréhension de l’architecture JavaScript et d’AEM Forms. En outre, lors de la mise en œuvre du code personnalisé, assurez-vous de suivre les bonnes pratiques, de respecter les directives de sécurité et de tester minutieusement votre code pour éviter tout problème potentiel dans les environnements de production. Vous pouvez implémenter un rappel pour FDM à l’aide de l’éditeur de code.

L’éditeur de code est disponible uniquement pour le composant de base AEM Forms. Pour les composants principaux de formulaire adaptatif, vous pouvez utiliser des fonctions personnalisées pour créer vos propres règles de formulaire, décrites dans la section suivante.

### Fonctions personnalisées {#custom-client-libs}

L’utilisation de bibliothèques clientes personnalisées dans AEM Forms (Adobe Experience Manager Forms) peut s’avérer utile dans divers scénarios afin d’améliorer les fonctionnalités, le style ou le comportement de vos formulaires. Voici quelques cas où l’utilisation de bibliothèques clientes personnalisées peut être appropriée :

* Si vous devez implémenter une conception ou une image de marque unique pour vos formulaires qui vont au-delà des fonctionnalités des options de style par défaut fournies par AEM Forms, vous pouvez choisir de créer des bibliothèques clientes personnalisées pour contrôler l’aspect.
* Lorsque vous avez besoin d’une logique côté client personnalisée, d’une réutilisation des méthodes dans plusieurs formulaires ou de comportements qui ne peuvent pas être réalisés par le biais des fonctionnalités AEM Forms standard. Cela peut inclure des interactions avec des formulaire dynamiques, une validation personnalisée ou l’intégration à des bibliothèques tierces.
* Pour améliorer les performances de vos formulaires en optimisant et en minimisant les ressources côté client. Les bibliothèques clientes personnalisées peuvent être utilisées pour regrouper et compresser des fichiers JavaScript et CSS, ce qui réduit le temps de chargement global de la page.
* Lorsque vous devez intégrer des bibliothèques JavaScript supplémentaires ou des structures qui ne sont pas incluses dans la configuration AEM Forms par défaut. Cela peut s’avérer nécessaire pour des fonctionnalités telles que des sélecteurs de date améliorés, des graphiques ou d’autres composants interactifs.

Avant de décider d’utiliser des bibliothèques clientes personnalisées, il est important de tenir compte des frais de maintenance, des conflits potentiels avec les futures mises à jour et de l’adhésion aux bonnes pratiques. Assurez-vous que vos personnalisations sont bien documentées et testées afin d’éviter des problèmes lors des mises à niveau ou de la collaboration avec d’autres développeurs et développeuses.

>[!NOTE]
> La fonction personnalisée est disponible pour les composants de base et les composants principaux d’AEM Forms.

**Avantages des fonctions personnalisées :**

Les **fonctions personnalisées** offrent un avantage notable par rapport à l’**éditeur de code**, car elles permettent une séparation claire entre le contenu et le code, ce qui améliore la collaboration et simplifie les workflows. Il est recommandé d’utiliser des fonctions personnalisées pour les avantages suivants :

* **Utilisez en toute transparence le contrôle de version comme Git :**
   * L’isolation du code du contenu réduit considérablement les conflits Git lors de la gestion de contenu et favorise un référentiel bien organisé.
   * Les fonctions personnalisées sont utiles pour les projets avec plusieurs contributeurs et contributrices travaillant simultanément.

* **Avantages techniques :**
   * Les fonctions personnalisées offrent la modularité et l’encapsulation.
   * Les modules peuvent être développés, testés et conservés indépendamment.
   * Améliore la réutilisation et la maintenance du code.

* **Processus de développement efficace :**
   * La modularité permet aux développeurs et développeuses de se consacrer aux fonctionnalités spécifiques.
   * Réduit la charge des développeurs et développeuses en réduisant la complexité de l’ensemble de la base de code pour un processus de développement plus efficace.



