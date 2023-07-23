---
title: Meilleures pratiques pour travailler avec les formulaires adaptatifs
seo-title: Best practices for working with adaptive forms
description: Explique les bonnes pratiques à appliquer pour configurer un projet AEM Forms, développer des formulaires adaptatifs et optimiser les performances du système AEM Forms.
seo-description: Explains best practices for setting up an AEM Forms project, developing adaptive forms, and optimizing the performance for AEM Forms system.
uuid: ed95fc64-56b3-4ea1-a5ba-2e96953fca56
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
discoiquuid: 43c431e4-5286-4f4e-b94f-5a7451c4a22c
feature: Adaptive Forms
exl-id: 5c75ce70-983e-4431-a13f-2c4c219e8dde
source-git-commit: e7a3558ae04cd6816ed73589c67b0297f05adce2
workflow-type: tm+mt
source-wordcount: '4586'
ht-degree: 41%

---

# Meilleures pratiques pour travailler avec les formulaires adaptatifs {#best-practices-for-working-with-adaptive-forms}

<span class="preview"> Adobe recommande d’utiliser la capture de données moderne et extensible. [Composants principaux](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=fr) pour [création d’un Forms adaptatif](/help/forms/using/create-an-adaptive-form-core-components.md) ou [Ajout de Forms adaptatif à des pages AEM Sites](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md). Ces composants représentent une avancée significative dans la création de Forms adaptatif, ce qui garantit des expériences utilisateur impressionnantes. Cet article décrit l’approche plus ancienne de la création de Forms adaptatif à l’aide de composants de base. </span>

## Présentation {#overview}

Les formulaires Adobe Experience Manager (AEM) peuvent vous aider à transformer des transactions complexes en expériences numériques simples et attrayantes. Toutefois, il nécessite un effort concerté pour mettre en oeuvre, créer, exécuter et maintenir un écosystème AEM Forms efficace et productif.

Ce document fournit des instructions et des recommandations dont peuvent bénéficier l’administrateur, les auteurs et les développeurs de formulaires lorsque vous utilisez AEM Forms, en particulier le composant de formulaires adaptatifs. Il aborde les meilleures pratiques, de la configuration d’un projet de développement de formulaires à la configuration, la personnalisation, la création et l’optimisation d’AEM Forms. Ces bonnes pratiques contribuent globalement aux performances globales de l’écosystème AEM Forms.

En outre, voici quelques recommandations de lecture concernant les meilleures pratiques générales d’AEM :

* [Bonnes pratiques : déploiement et maintien d’AEM](/help/sites-deploying/best-practices.md)
* [Meilleures pratiques : création de contenu](/help/sites-authoring/best-practices.md)
* [Meilleures pratiques : administration d’AEM](/help/sites-administering/administer-best-practices.md)
* [Meilleures pratiques : développement de solutions](/help/sites-developing/best-practices.md)

## Installation et configuration d’AEM Forms {#set-up-and-configure-aem-forms}

### Configuration d’un projet de développement de formulaires {#setting-up-forms-development-project}

Une structure de projet simplifiée et normalisée peut réduire considérablement les efforts de développement et de maintenance. Apache Maven est un outil open source recommandé pour créer AEM projets.

* Utilisez le `aem-project-archetype` d’Apache Maven pour créer et gérer la structure d’un projet AEM. Il permet de créer la structure et les modèles recommandés pour votre projet AEM. En outre, il fournit des systèmes d’automatisation de création et de contrôle des modifications pour aider à la gestion du projet.

   * Utilisez la commande Maven`archetype:generate` pour générer la structure initiale.
   * Utilisez la commande Maven `eclipse:eclipse` pour générer les fichiers de projet Eclipse et importer le projet dans Eclipse.

Pour plus d’informations, reportez-vous à la section [Comment créer des projets AEM à l’aide d’Apache Maven](/help/sites-developing/ht-projects-maven.md).

* L’outil FileVault ou VLT vous permet de mapper le contenu d’une instance CRX ou AEM à votre système de fichiers. Il fournit des opérations de gestion de contrôle des modifications, telles que l’archivage et l’extraction du contenu du projet AEM. Voir [Comment utiliser l’outil VLT](/help/sites-developing/ht-vlttool.md).

* Si vous utilisez un environnement de développement intégré à Eclipse, vous pouvez utiliser AEM outils de développement pour une intégration transparente de l’IDE Eclipse avec les instances AEM afin de créer des applications AEM. Pour plus d’informations, voir [AEM outils de développement pour Eclipse](/help/sites-developing/aem-eclipse.md).

* Ne stockez aucun contenu ou n’apportez aucune modification dans le dossier /libs. Créez des recouvrements dans les dossiers /app pour étendre ou remplacer les fonctionnalités par défaut.

* Lorsque vous créez des packages pour déplacer du contenu, assurez-vous que les chemins de filtre de package sont corrects et que seuls les chemins obligatoires sont mentionnés.

* Ne stockez aucun contenu ou n’apportez aucune modification dans le dossier /libs. Créez des recouvrements dans les dossiers /app pour étendre ou remplacer les fonctionnalités par défaut.

* Définissez des dépendances correctes pour les packages afin de forcer un ordre / une séquence d’installation prédéterminé(e).

* Ne créez aucun nœud référençable dans /libs ou /apps.

### Planification de l’environnement de création {#planning-for-authoring-environment}

Une fois votre projet AEM configuré, définissez la stratégie de création et de personnalisation des composants et modèles de formulaires adaptatifs.

* Un modèle de formulaire adaptatif est une page d’AEM spécialisée qui définit la structure et les informations d’en-tête et de pied de page d’un formulaire adaptatif. Un modèle comporte des mises en page, des styles et une structure de base préconfigurés pour un formulaire adaptatif. AEM Forms fournit des modèles et des composants prêts à l’emploi que vous pouvez utiliser pour créer des formulaires adaptatifs. Cependant, vous pouvez créer des modèles et des composants personnalisés selon vos besoins. Il est recommandé de rassembler les exigences relatives aux modèles et composants supplémentaires dont vous aurez besoin dans vos formulaires adaptatifs. Pour plus d’informations, voir [Personnalisation des formulaires et composants adaptatifs](/help/forms/using/adaptive-forms-best-practices.md#customize-components).
* AEM Forms vous permet de créer des formulaires adaptatifs basés sur les modèles de formulaires suivants. Les modèles de formulaire font office d’interface pour l’échange de données entre un formulaire et un système AEM et fournissent une structure XML pour le flux de données à l’intérieur et à l’extérieur d’un formulaire adaptatif. En outre, les modèles de formulaire imposent des règles et des contraintes aux formulaires adaptatifs sous la forme de schémas et de contraintes XFA.

   * **Aucun**: Les formulaires adaptatifs créés avec cette option n’utilisent aucun modèle de formulaire. Les données XML générées à partir de ce type de formulaire présentent une structure plate avec des champs et des valeurs correspondantes.
   * **Schéma XML ou JSON** : les schémas XML et JSON représentent la structure dans laquelle les données sont générées ou utilisées par le système back-end de l’entreprise. Vous pouvez associer un schéma à un formulaire adaptatif et utiliser ses éléments pour ajouter du contenu dynamique à un formulaire adaptatif. Les éléments du schéma sont disponibles dans l’onglet Objet du modèle de données du navigateur de contenu pour la création de formulaires adaptatifs. Vous pouvez faire glisser et déposer les éléments du schéma pour créer le formulaire.
   * **Modèle de formulaire XFA**: Il s’agit d’un modèle de formulaire idéal si vous avez des investissements dans des formulaires HTML5 basés sur XFA. Il fournit un moyen direct de convertir vos formulaires basés sur XFA en formulaires adaptatifs. Toutes les règles XFA existantes sont conservées dans les formulaires adaptatifs associés. Les formulaires adaptatifs obtenus prennent en charge les éléments XFA, tels que les validations, les événements, les propriétés et les modèles.
   * **Modèle de données de formulaire** : il s’agit du modèle de formulaire idéal si vous souhaitez intégrer les systèmes back-end tels que les bases de données, les services web et un profil utilisateur AEM pour préremplir des formulaires adaptatifs et enregistrer des données de formulaire envoyé dans les systèmes back-end. Un éditeur de modèle de données de formulaire vous permet de définir et de configurer des entités et des services dans un modèle de données de formulaire que vous pouvez utiliser pour créer des formulaires adaptatifs. Pour plus d’informations, voir [Intégration de données AEM Forms](/help/forms/using/data-integration.md).

Il est important de sélectionner avec soin le modèle de données qui correspond à vos besoins, tout en optimisant vos investissements existants dans les ressources XFA et XSD, le cas échéant. Il est recommandé d’utiliser XSD Model pour créer des modèles de formulaire car le fichier XML généré contient les données selon l’expression XPATH définie par le schéma. L’utilisation du modèle XSD comme choix par défaut pour le modèle de données de formulaire s’avère également utile, dans la mesure où il découple la conception de formulaire du système principal qui traite et consomme des données, et améliore les performances du formulaire en raison d’un mappage un à un des champs de formulaire. En outre, BindRef du champ peut être transformé en XPATH de sa valeur de données en XML.

Pour plus d’informations, voir [Création d’un formulaire adaptatif](/help/forms/using/creating-adaptive-form.md).

* Il existe des sections courantes dans les formulaires adaptatifs. Vous pouvez les identifier et définir une stratégie pour promouvoir la réutilisation du contenu. Les formulaires adaptatifs vous permettent de créer des fragments autonomes et de les réutiliser dans plusieurs formulaires. Vous pouvez également enregistrer un panneau dans un formulaire adaptatif en tant que fragment. Toute modification apportée à un fragment est répercutée dans tous les formulaires associés. Cela vous permet de réduire le temps de création et d’assurer la cohérence entre les formulaires. En outre, l’utilisation de fragments rend les formulaires adaptatifs plus légers, ce qui entraîne une amélioration de l’expérience de création, en particulier des formulaires volumineux. Pour plus d’informations, voir [Fragments de formulaire adaptatif](/help/forms/using/adaptive-form-fragments.md).

### Personnalisation des formulaires et composants adaptatifs {#customize-components}

* AEM Forms fournit des modèles de formulaire adaptatif prêts à l’emploi que vous pouvez utiliser pour créer des formulaires adaptatifs. Vous pouvez également créer vos propres modèles. AEM fournit des modèles statiques et modifiables.

   * Les modèles statiques sont définis et configurés par les développeurs.
   * Les modèles modifiables sont créés par les auteurs à l’aide de l’éditeur de modèles. L&#39;éditeur de modèles permet de définir une structure de base et un contenu initial dans un modèle. Toute modification du calque de structure est répercutée dans tous les formulaires utilisant ce modèle. Le contenu initial peut inclure un thème préconfiguré, un service de préremplissage, une action d’envoi, etc. Cependant, ces paramètres peuvent être modifiés pour un formulaire à l’aide de l’éditeur de formulaire. Pour plus d’informations, voir [Modèles de formulaires adaptatifs](/help/forms/using/template-editor.md).

* Pour définir le style d’une instance ou d’un panneau spécifique, utilisez [le style en ligne](/help/forms/using/inline-style-adaptive-forms.md). Vous pouvez également définir une classe dans un fichier CSS et spécifier son nom dans la propriété Classe CSS du composant.
* Incluez une bibliothèque cliente dans un composant pour appliquer de manière cohérente des styles aux formulaires adaptatifs ou aux fragments qui utilisent ce composant. Pour plus d’informations, voir [Création d’un composant de page de formulaire adaptatif](/help/forms/using/custom-adaptive-forms-templates.md).
* Appliquez des styles définis dans une bibliothèque cliente pour sélectionner des formulaires adaptatifs en spécifiant le chemin d’accès à la bibliothèque cliente dans le champ de chemin d’accès au fichier CSS dans les propriétés du conteneur de formulaires adaptatifs.
* Pour créer une bibliothèque cliente de vos styles, vous pouvez configurer le fichier CSS personnalisé dans la bibliothèque cliente de base de l’éditeur de thème ou dans les propriétés du conteneur de formulaires.
* Les formulaires adaptatifs fournissent des dispositions de panneau, telles que réactives, avec onglets, accordéons et assistant, pour contrôler la disposition des composants de formulaire dans un panneau. Vous pouvez créer des dispositions de panneau personnalisées et les rendre disponibles pour les auteurs de formulaires. Pour plus d’informations, voir [Création de composants de disposition personnalisés pour les formulaires adaptatifs](/help/forms/using/custom-layout-components-forms.md).
* Vous pouvez également personnaliser des composants de formulaire adaptatif spécifiques tels que les champs et la disposition des panneaux.

   * Utilisez la variable [Incrustation](/help/sites-developing/overlays.md) de l’AEM pour modifier une copie d’un composant. Il n’est pas recommandé de modifier les composants par défaut.
   * Pour personnaliser la mise en page des composants de formulaire adaptatif prêts à l’emploi dans /libs, [créer des composants de disposition personnalisés ;](/help/forms/using/custom-layout-components-forms.md) en plus de la fonction [dispositions par défaut](/help/forms/using/layout-capabilities-adaptive-forms.md).
   * Introduisez des interactivités personnalisées en créant des widgets ou des apparences personnalisés. Il n’est pas recommandé de modifier les composants par défaut. Pour plus d’informations, voir [Structure de l’apparence](/help/forms/using/introduction-widgets.md).

* Pour connaître les recommandations relatives à la gestion des données d’identification personnelle, reportez-vous à la section [Gestion des informations d’identification personnelle.](/help/forms/using/adaptive-forms-best-practices.md#p-handling-personally-identifiable-information-p)

### Création de modèles de formulaire

Vous pouvez créer un formulaire adaptatif à l’aide des modèles de formulaire activés dans **Explorateur de configurations**. Pour activer les modèles de formulaire, reportez-vous à [Création d’un modèle de formulaire adaptatif](https://experienceleague.adobe.com/docs/experience-manager-learn/forms/creating-your-first-adaptive-form/create-adaptive-form-template.html?lang=fr).

Vous pouvez également charger les modèles de formulaire à partir des packages de formulaires adaptatifs créés sur l’ordinateur d’un autre auteur. Les modèles de formulaire sont disponibles en installant [aemforms-references-* packages](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/forms-updates/aem-forms-releases.html?lang=fr). Nous recommandons de suivre les bonnes pratiques suivantes :
* Nous recommandons le mode d’exécution **nosamplecontent** uniquement pour les nœuds d’auteur et non pour les nœuds de publication.
* La création de ressources telles que les formulaires adaptatifs, les thèmes, les modèles ou les configurations cloud s’effectue uniquement sur les nœuds d’auteur, qui peuvent être publiés sur les nœuds de publication configurés.
Pour plus d’informations, reportez-vous à [Publication et annulation de la publication de formulaires et de documents](https://experienceleague.adobe.com/docs/experience-manager-65/forms/publish-process-aem-forms/publishing-unpublishing-forms.html?lang=fr).
* Le package du module complémentaire Forms est nécessaire pour la création et la publication, afin de prendre en charge les opérations de service de document. Il peut donc être considéré comme une dépendance.
Si vous souhaitez uniquement des packages d’exemples de modèle, de thèmes et de documents d’enregistrement liés à Forms, vous pouvez les télécharger à partir de [aemforms-references-* packages](https://experienceleague.adobe.com/docs/experience-manager-65/forms/publish-process-aem-forms/publishing-unpublishing-forms.html?lang=fr).

Pour plus d’informations, reportez-vous aux bonnes pratiques dans [Présentation de la création de formulaires adaptatifs](/help/forms/using/introduction-forms-authoring.md).

## Création de formulaires adaptatifs {#author-adaptive-forms}

### Utilisation de l’IU optimisée pour les écrans tactiles pour la création {#using-touch-optimized-ui-for-authoring}

* Utilisez le navigateur d’objets de la barre latérale pour accéder rapidement aux champs dans la partie la plus basse de la hiérarchie du formulaire. Vous pouvez utiliser la zone de recherche pour rechercher des objets dans le formulaire ou l’arborescence d’objets pour passer d’un objet à un autre.
* Pour afficher et modifier les propriétés d’un composant dans le navigateur de composants dans la barre latérale, sélectionnez le composant, puis cliquez sur ![cmppr-1](assets/cmppr-1.png). Vous pouvez également double-cliquer sur un composant pour afficher ses propriétés dans l’explorateur de propriétés.
* Utilisez les raccourcis clavier pour exécuter des actions rapides sur vos formulaires. Voir [Raccourcis clavier AEM Forms](/help/forms/using/keyboard-shortcuts.md).

* Les composants de formulaire adaptatif sont recommandés pour une utilisation uniquement dans les pages de formulaire adaptatif. Les composants dépendent de leur hiérarchie parent. Par conséquent, ne les utilisez pas dans une page AEM.

Voir également les descriptions des composants et les bonnes pratiques dans [Présentation de la création de formulaires adaptatifs](/help/forms/using/introduction-forms-authoring.md).

### Utilisation de règles dans les formulaires adaptatifs {#using-rules-in-adaptive-forms}

AEM Forms fournit une [éditeur de règles](/help/forms/using/rule-editor.md) qui vous permet de créer des règles pour ajouter un comportement dynamique aux composants de formulaire adaptatif. Grâce à ces règles, vous pouvez évaluer des conditions et déclencher des actions sur des composants, comme par exemple afficher ou masquer des champs, calculer des valeurs, dynamiser une liste déroulante et plus encore.

L’éditeur de règles fournit un éditeur visuel et un éditeur de code pour la création de règles. Tenez compte des points suivants lors de l’écriture de règles en mode éditeur de code :

* Utilisez des noms significatifs et uniques pour les champs de formulaire et les composants afin d’éviter tout conflit potentiel lors de la création de règles.
* Utilisez l’opérateur `this` pour un composant afin d’y faire mention lors de l’expression d’une règle. Ainsi, la règle reste valide même si le nom du composant est modifié. Par exemple, `field1.valueCommit script: this.value > 10`.

* Utilisez les noms de composant lorsque vous faites référence à d’autres composants de formulaire. Utilisez la propriété `value` pour récupérer la valeur d’un champ ou d’un composant. Par exemple, `field1.value`.

* Désignez les composants selon une hiérarchie relative unique afin d’éviter tout conflit. Par exemple, `parentName.fieldName`.

* Lorsque vous manipulez des règles complexes ou fréquemment utilisées, pensez à définir la logique commerciale comme fonctions dans une bibliothèque cliente distincte que vous pouvez spécifier et réutiliser dans les formulaires adaptatifs. La bibliothèque client doit être une bibliothèque autonome et ne doit donc avoir aucune dépendance externe, à l’exception de jQuery et Underscore.js. Vous pouvez également utiliser la bibliothèque cliente pour imposer la [revalidation côté serveur](/help/forms/using/configuring-submit-actions.md#server-side-revalidation-in-adaptive-form) des données de formulaire envoyées.
* Les formulaires adaptatifs fournissent un ensemble d’API que vous pouvez utiliser pour communiquer et effectuer des actions sur les formulaires adaptatifs. Certaines des API clés sont les suivantes. Pour plus d’informations, voir [Référence de l’API de la bibliothèque JavaScript pour Adaptive Forms](https://adobe.com/go/learn_aemforms_documentation_63_fr).

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

* Les auteurs de formulaires adaptatifs peuvent avoir besoin d’écrire du code JavaScript pour créer une logique métier dans un formulaire. Bien que JavaScript soit puissant et efficace, il est probable qu’il puisse compromettre les attentes en matière de sécurité. Par conséquent, vous devez vous assurer que l’auteur du formulaire est une personne de confiance et qu’il existe des processus pour examiner et approuver le code JavaScript avant qu’un formulaire ne soit mis en production. L’administrateur peut restreindre l’accès à l’éditeur de règles aux groupes d’utilisateurs en fonction de leur rôle ou de leur fonction. Voir [Accorder l’accès à l’éditeur de règles à certains groupes d’utilisateurs](/help/forms/using/rule-editor-access-user-groups.md).
* Vous pouvez utiliser des expressions dans les règles pour rendre les formulaires adaptatifs dynamiques. Toutes les expressions sont des expressions JavaScript valides et utilisent des API de modèle de script de formulaires adaptatifs. Ces expressions renvoient des valeurs de certains types. Pour plus d’informations sur les expressions et les meilleures pratiques associées, voir [Expressions des formulaires adaptatifs](/help/forms/using/adaptive-form-expressions.md).

### Utilisation des thèmes {#working-with-themes}

Adaptatif pour les thèmes permet de créer des styles réutilisables qui peuvent être appliqués à l’ensemble des formulaires pour un aspect et un style cohérents. Il est recommandé d’utiliser les thèmes pour définir le style des composants et des panneaux de formulaire. Voici quelques bonnes pratiques relatives aux thèmes :

* Utilisez la bibliothèque de ressources pour une application rapide des styles de texte, de l’arrière-plan et des images. Lorsqu’un style est ajouté à la bibliothèque de ressources, il est disponible pour d’autres thèmes et dans le mode Style de l’éditeur de formulaires.
* Appliquez des paramètres globaux tels que la police et l’arrière-plan de page à l’aide du sélecteur de niveau page.
* Utilisez les bibliothèques clientes pour importer des styles existants ou avancés dans vos thèmes.
* Vous pouvez remplacer le style pour des champs, des panneaux ou des boutons spécifiques dans un calque de style de formulaire.
* Si un thème ne répond pas à vos besoins en termes de style, vous pouvez utiliser des classes prédéfinies telles que guideFieldNode, guideFieldLabel, guideFieldWidget et guidePanelNode pour appliquer un style commun à tous les formulaires.

Pour plus d’informations, voir [Thèmes](/help/forms/using/themes.md).

### Optimisation des performances de formulaires complexes et volumineux {#optimizing-performance-of-large-and-complex-forms}

Les auteurs de formulaires et les utilisateurs finaux sont généralement confrontés à des problèmes de performances lors du chargement de formulaires volumineux en mode création ou au moment de l’exécution. À mesure que le nombre d’objets (champs et panneaux) dans le formulaire augmente, l’expérience de création et d’exécution commence à se dégrader. Cela empêche également plusieurs auteurs de collaborer et de créer simultanément un formulaire.

Tenez compte des bonnes pratiques suivantes pour résoudre les problèmes de performances liés aux formulaires volumineux :

* Il est recommandé de créer si possible des formulaires adaptatifs à l’aide du modèle de données de formulaire XSD, et ce, même lors de la conversion d’un XFA en formulaire adaptatif.
* Incluez uniquement les champs et les panneaux dans les formulaires adaptatifs qui capturent les informations de l’utilisateur. Pensez à conserver un contenu statique minimal ou utilisez des URL pour les ouvrir dans une fenêtre distincte.
* Bien que chaque formulaire soit conçu pour un usage spécifique, il existe des segments communs dans la plupart des formulaires. Par exemple, les détails personnels, l’adresse, les détails de l’emploi, etc. Créez des [fragments de formulaire adaptatif](/help/forms/using/adaptive-form-fragments.md) pour les éléments et sections de formulaire communs et utilisez-les dans les formulaires. Vous pouvez également enregistrer un panneau dans un formulaire existant en tant que fragment. Toute modification apportée à un fragment est répercutée dans tous les formulaires adaptatifs associés. Cette fonction favorise la création en collaboration : plusieurs auteurs peuvent ainsi travailler simultanément sur différents fragments composant un formulaire.

   * Comme pour les formulaires adaptatifs, il est recommandé de définir tous les scripts personnalisés et de style spécifiques aux fragments dans la bibliothèque cliente à l’aide de la boîte de dialogue du conteneur de fragments. Essayez également de créer des fragments auto-suffisants qui ne dépendent pas d’objets en dehors de celui-ci.
   * Évitez d’utiliser des scripts de fragments croisés. S’il existe un objet en dehors du fragment auquel vous devez vous référer, essayez de faire de cet objet une partie du formulaire parent. Si l’objet doit rester dans un autre fragment, reportez-vous à celui-ci par son nom dans le script.

* Utilisez l’option Enregistrer et reprendre avec l’enregistrement automatique pour enregistrer régulièrement le formulaire adaptatif et permettre aux utilisateurs de le revoir ultérieurement pour remplir le formulaire.
* Configurez les fragments à charger en différé. Au moment de l’exécution, les fragments marqués pour chargement différé sont rendus uniquement lorsqu’ils sont requis. Cela réduit considérablement le temps de chargement des formulaires volumineux. Elle est également prise en charge dans les fragments avec des panneaux répétables. Pour plus d’informations, voir [Configuration du chargement différé](/help/forms/using/lazy-loading-adaptive-forms.md).

   * Ne configurez pas le chargement différé sur les fragments dans une mise en page en grille réactive ou dans le premier panneau.
   * Les composants des pièces jointes et des conditions générales ne sont pas pris en charge dans les fragments chargés en différé.
   * Marquez une valeur dans un panneau chargé différé comme Utiliser la valeur globalement si cette valeur est utilisée dans une autre partie du formulaire afin que la valeur soit disponible lorsque le panneau contenant est déchargé.
   * Pensez à créer des règles de visibilité pour les fragments qui doivent s’afficher ou être masqués en fonction d’une condition.
* Définissez la valeur de **Nombre d’appels par requête** dans le **Servlet principal Apache Sling** sur un nombre assez élevé. Cela permet au serveur Forms d’autoriser des appels supplémentaires. La configuration indique une valeur par défaut de 1 500. La valeur, 1 500 appels, correspond à d’autres composants d’Experience Manager tels que Sites et Assets. La valeur définie par défaut des formulaires adaptatifs est 20 000. Si vous rencontrez l’erreur `too many calls` dans les journaux ou si le rendu du formulaire échoue, essayez de définir la valeur sur un nombre plus élevé pour résoudre le problème. Si le nombre d’appels est supérieur à 20 000, cela signifie que le formulaire est complexe et qu’il peut prendre un certain temps pour générer le rendu du formulaire dans le navigateur. Cela ne se produit que lors du premier chargement du formulaire. Une fois le formulaire mis en cache, cela n’a aucun impact significatif sur les performances.

### Préremplir les formulaires adaptatifs {#prefilling-adaptive-forms}

Vous pouvez préremplir des champs de formulaire adaptatif avec des données récupérées du serveur principal pour aider les utilisateurs à remplir rapidement le formulaire et éviter de saisir des erreurs.

* AEM Forms fournit un service de préremplissage pour lire les données d’un fichier XML de données prédéfini et préremplir les champs d’un formulaire adaptatif avec le contenu dans le fichier XML prérempli.
* Les données XML de préremplissage doivent être conformes au schéma du modèle de formulaire associé au formulaire adaptatif.
* Incluez les sections `afBoundedData` et `afUnBoundedData` dans le fichier XML prérempli pour préremplir les champs liés et non liés d’un formulaire adaptatif.

* Pour les formulaires adaptatifs basés sur un modèle de données de formulaire, AEM Forms fournit un service de préremplissage de modèles de données de formulaire prêts à l’emploi. Le service de préremplissage interroge les sources de données pour les objets de modèle de données dans le formulaire adaptatif et préremplit les valeurs de champ lors du rendu du formulaire.
* Vous pouvez également utiliser les formulaires adaptatifs de préremplissage de fichiers, crx, service ou http.
* AEM Forms prend en charge les services de préremplissage personnalisés que vous pouvez brancher en tant que service OSGi pour préremplir les formulaires adaptatifs.

Pour plus d’informations, voir [Préremplir des champs de formulaire adaptatif](/help/forms/using/prepopulate-adaptive-form-fields.md).

### Signature et envoi de formulaires adaptatifs {#signing-and-submitting-adaptive-forms}

Les formulaires adaptatifs nécessitent des actions Envoyer pour traiter les données spécifiées par l’utilisateur. Une action Envoyer détermine la tâche effectuée sur les données envoyées à l’aide d’un formulaire adaptatif.

* Il existe plusieurs actions d’envoi disponibles prêtes à l’emploi dans les formulaires adaptatifs. Pour plus de détails, voir [Configurer l’action Envoyer](/help/forms/using/configuring-submit-actions.md).
* Vous pouvez créer une action d’envoi personnalisée si les actions d’envoi par défaut ne remplissent pas votre cas d’utilisation. Pour plus d’informations, voir [Création d’une action Envoyer personnalisée pour les formulaires adaptatifs](/help/forms/using/custom-submit-action-form.md).
* Incluez des validations côté serveur pour empêcher l’envoi de données non valides.

Vous pouvez tirer parti de l’expérience multi-signes d’Adobe Sign dans les formulaires adaptatifs. Tenez compte des points suivants lors de la configuration d’Adobe Sign dans les formulaires adaptatifs. Pour plus d’informations, voir [Utiliser Adobe Sign dans un formulaire adaptatif](/help/forms/using/working-with-adobe-sign.md).

* Le formulaire adaptatif comprenant Adobe Sign est envoyé uniquement après que tous les signataires ont signé le formulaire. Les formulaires affichent l’état En attente de signature jusqu’à ce que le formulaire soit signé par tous les signataires.
* Vous pouvez configurer une expérience de signature dans le formulaire ou rediriger les signataires vers une page de signature lors de l’envoi.
* Configurez une expérience de signature séquentielle ou parallèle, selon le cas.

### Génération d’un document d’enregistrement {#generating-document-of-record}

Un document d’enregistrement est une version de PDF aplati d’un formulaire adaptatif que vous pouvez imprimer, signer ou archiver.

* Selon le modèle de données de formulaire sur lequel un formulaire adaptatif est basé, vous pouvez configurer un modèle de document d’enregistrement comme suit :

   * **Modèle de formulaire XFA**: Utilisez le fichier XDP associé comme modèle de DE.
   * **Schéma XSD**: Utilisez le modèle XFA associé qui utilise le même schéma XML que celui utilisé par le formulaire adaptatif.
   * **Aucun**: Utilisation d’un document d’enregistrement généré automatiquement.

* Configurez l’en-tête, le pied de page, les images, la couleur, la police, etc. à partir de l’onglet Document d’enregistrement de l’éditeur de formulaire adaptatif.
* Utilisez `DoRService` pour générer le document d’enregistrement par programmation.
* Excluez les champs masqués du document d’enregistrement.
* Utilisez le paramètre de demande `afAcceptLang` pour afficher le document d’enregistrement dans une autre langue.

### Débogage et test des formulaires adaptatifs {#debugging-and-testing-adaptive-forms}

[Module externe Chrome AEM](https://adobe-consulting-services.github.io/acs-aem-tools/aem-chrome-plugin/) est une extension de navigateur pour Google Chrome qui fournit des outils de débogage des formulaires adaptatifs. Les auteurs et les développeurs de formulaires peuvent utiliser ces outils pour :

* Identifier les goulets d’étranglement et optimiser les performances de rendu du formulaire
* Déboguer les mots-clés et les erreurs bindRef dans le formulaire
* Activation et configuration des journaux
* Débogage des règles et des scripts dans le formulaire
* Exploration et en savoir plus sur les API guideBridge

Pour plus d’informations, voir [Plug-in AEM pour Chrome - Formulaire adaptatif](https://adobe-consulting-services.github.io/acs-aem-tools/aem-chrome-plugin/adaptive-form/).

### Validation des formulaires adaptatifs sur AEM serveur {#validating-adaptive-forms-on-aem-server}

Des validations côté serveur sont nécessaires pour empêcher toute tentative de contournement des validations sur le client et tout compromis possible entre les envois de données et les violations des règles de fonctionnement. Les validations côté serveur sont exécutées sur le serveur en chargeant la bibliothèque cliente requise.

* Incluez des fonctions dans une bibliothèque cliente pour valider les expressions dans les formulaires adaptatifs et spécifiez la bibliothèque cliente dans la boîte de dialogue du conteneur de formulaires adaptatifs. Pour plus d’informations, voir [Revalidation côté serveur](/help/forms/using/configuring-submit-actions.md#p-server-side-revalidation-in-adaptive-form-p).
* La validation côté serveur permet de valider le modèle de formulaire. Il est recommandé de créer une bibliothèque cliente distincte pour les validations et de ne pas la mélanger à d’autres éléments tels que le style de HTML et la manipulation DOM dans la même bibliothèque cliente.

### Localisation des formulaires adaptatifs {#localizing-adaptive-forms}

AEM fournit des processus de traduction que vous pouvez utiliser pour localiser les formulaires adaptatifs. Pour plus d’informations, voir [Utilisation AEM processus de traduction pour localiser les formulaires adaptatifs](/help/forms/using/using-aem-translation-workflow-to-localize-adaptive-forms.md).

Voici quelques bonnes pratiques à appliquer lors de la localisation de formulaires adaptatifs :

* Utilisez les fragments de formulaire adaptatif pour les éléments courants des formulaires et localisez les fragments. Cela permet de localiser un fragment une seule fois et de le refléter dans tous les formulaires dans lesquels le fragment localisé est utilisé.
* Les modifications telles que l’ajout d’un nouveau composant ou l’application d’un script dans un formulaire localisé ne sont pas localisées automatiquement. Par conséquent, vous devez finaliser un formulaire avant de le localiser pour éviter plusieurs cycles de localisation.
* Utilisez le paramètre de requête `afAcceptLang` pour remplacer la langue du navigateur et pour rendre le formulaire dans la langue spécifiée. Par exemple, l’URL suivante force à effectuer le rendu du formulaire en japonais, indépendamment du paramètre régional spécifié dans les paramètres du navigateur :

  `https://'[server]:[port]'/<contextPath>/<formFolder>/<formName>.html?wcmmode=disabled&afAcceptLang=ja`

* AEM Forms prend actuellement en charge la localisation du contenu des formulaires adaptatifs vers l’anglais (en), l’espagnol (es), le français (fr), l’italien (it), l’allemand (de), le japonais (ja), le portugais du Brésil (pt-BR), le chinois (zh-CN), le chinois de Taïwan (zh-TW) et le coréen (ko-KR). Cependant, vous pouvez ajouter la prise en charge de nouveaux paramètres régionaux pour les formulaires adaptatifs à l’exécution. Pour plus d’informations, voir [Prise en charge de nouveaux paramètres régionaux pour la localisation de formulaires adaptatifs](/help/forms/using/supporting-new-language-localization.md).

## Préparation du projet Forms à des fins de production {#prepare-forms-project-for-production}

### Ajout d’un serveur de traitement de formulaires {#adding-forms-processing-server}

Vous pouvez configurer une instance supplémentaire du serveur AEM Forms situé derrière le pare-feu dans une zone sécurisée. Vous pouvez utiliser cette instance pour :

* **Traitement par lots** : tâches récurrentes ou programmées par lots comportant une charge importante. Par exemple, l’impression d’instructions, la génération de correspondances et l’utilisation de services de document tels que PDF Generator, Output et Assembler.
* **Stockage des données de PII**: Enregistrez les données PII sur le serveur de traitement. Cela n’est pas nécessaire si vous utilisez déjà un fournisseur de stockage personnalisé pour le stockage des données de PII.

### Déplacement d’un projet vers un autre environnement {#moving-project-to-another-environment}

Vous devez souvent déplacer vos projets AEM d’un environnement à un autre. Voici quelques éléments essentiels à retenir lors du déplacement :

* Effectuez une sauvegarde de vos bibliothèques clientes existantes, de votre code personnalisé et de vos configurations.
* Déployez manuellement les packages et correctifs de produits dans l’ordre indiqué dans le nouvel environnement.
* Déployez manuellement et sous la forme d’un package ou d’un lot distinct sur le nouveau serveur AEM des modules de code et des lots spécifiques au projet.
* (*AEM Forms on JEE uniquement*) Déployez manuellement les LCA et les DSC sur le serveur de processus des formulaires.
* Utilisation [Export-Import](/help/forms/using/import-export-forms-templates.md) pour déplacer des ressources vers le nouvel environnement. Vous pouvez également configurer l’agent de réplication et publier les ressources.
* Lorsque vous effectuez une mise à niveau, remplacez toutes les API et fonctionnalités obsolètes par de nouvelles API et fonctionnalités.

### Configurer AEM {#configuring-aem}

Voici quelques bonnes pratiques pour configurer AEM afin d’améliorer les performances globales :

* Activez la compression de la bibliothèque client HTML pour Javascript et CSS à partir de la console Felix.
* Masquez toutes les bibliothèques clientes sous `/etc.clientlibs/fd` et toutes les bibliothèques clientes personnalisées supplémentaires dans AEM Dispatcher pour améliorer la réactivité et la sécurité des formulaires publiés. Pour plus d’informations, reportez-vous à la section [Dispatcher](https://helpx.adobe.com/fr/experience-manager/dispatcher/using/dispatcher.html).

* Ne mettez pas en cache les chemins d’accès `/content/forms/af/` et `/content/dam/formsanddocuments/*`. Pour plus d’informations sur la configuration de la mise en cache de formulaires adaptatifs, voir [Mise en cache de formulaires adaptatifs](/help/forms/using/configure-adaptive-forms-cache.md).

* Activez le HTML via le module de compression de serveur web. Pour plus d’informations, voir [Réglage des performances du serveur AEM Forms](/help/forms/using/performance-tuning-aem-forms.md).
* Augmentez la configuration des appels par requête pour les formulaires volumineux. Voir [Optimisation des performances de formulaires complexes et volumineux](/help/forms/using/adaptive-forms-best-practices.md#optimizing-performance-of-large-and-complex-forms).
* Créer [pages d’erreur personnalisées affichées par le gestionnaire d’erreur](https://experienceleague.adobe.com/docs/experience-manager-65/developing/platform/customizing-errorhandler-pages.html?lang=fr).
* Sécurisez le serveur AEM Forms.

   * Utilisez le mode d’exécution `nosamplecontent` pour vous assurer qu’aucun exemple de contenu ou d’utilisateur ne soit déployé sur le serveur de production. Voir [Exécution d’AEM selon le mode prêt pour la production](/help/sites-administering/production-ready.md).

* Laissez la taille du tas à 8 Go au minimum. Pour connaître les autres paramètres, voir [Réglage des performances du serveur AEM Forms](/help/forms/using/performance-tuning-aem-forms.md).
* Utilisez les sessions utilisateurs du service au lieu des sessions d’administration pour exécuter les tâches au niveau du service. Pour plus d’informations, voir [Authentification du service](https://sling.apache.org/documentation/the-sling-engine/service-authentication.html).

>[!VIDEO](https://vimeo.com/)

### Configuration du stockage externe pour les données de brouillons et de formulaires envoyés {#external-storage}

Dans un environnement de production, il est recommandé de ne pas stocker les données de formulaire envoyées dans AEM référentiel. L’implémentation par défaut des actions d’envoi Magasin, Stocker le contenu et Stocker le PDF du portail Forms stocke les données de formulaire dans AEM référentiel. Ces actions d’envoi sont destinées uniquement à des fins de démonstration. En outre, les fonctions Enregistrer et reprendre et Enregistrement automatique stockent les données dans le portail par défaut. Par conséquent, prenez en compte les recommandations suivantes :

* **Stockage des données de brouillon** : si vous utilisez la fonction Brouillon des formulaires adaptatifs, vous devez implémenter une SPI (Service Provide Interface) personnalisée pour le stockage des données de brouillon dans un espace de stockage plus sécurisé comme une base de données. Pour plus d’informations, voir [Exemple d’intégration d’un composant de brouillons et d’envois à la base de données](/help/forms/using/integrate-draft-submission-database.md).

* **Stockage des données d’envoi** : si vous utilisez l’envoi de stockage du portail de formulaires, vous devez implémenter une SPI personnalisée pour stocker les données d’envoi dans une base de données. Voir [Exemple d’intégration d’un composant brouillons &amp; envois à la base de données](/help/forms/using/integrate-draft-submission-database.md) pour obtenir un exemple d’intégration.

  Vous pouvez également écrire une action d’envoi personnalisée qui stocke les données de formulaires et les pièces jointes dans un espace de stockage sécurisé. Pour plus d’informations, voir [Créer une action Envoyer personnalisée pour les formulaires adaptatifs](/help/forms/using/custom-submit-action-form.md).

* **Longueur de l’ID du brouillon** : lorsque vous enregistrez un formulaire adaptatif en tant que brouillon, un ID de brouillon est généré pour identifier de manière unique le brouillon. La valeur minimale pour la longueur du champ d’ID du brouillon est de 26 caractères. Adobe recommande de définir la longueur de l’ID du brouillon sur 26 caractères ou plus.

### Gestion des informations d’identification personnelle {#handling-personally-identifiable-information}

L’un des principaux défis pour les entreprises est de savoir comment gérer les données d’identification personnelle (PII). Voici quelques bonnes pratiques qui vous aideront à gérer ces données :

* Utilisez un stockage sécurisé et externe, tel qu’une base de données, pour stocker les données des brouillons et des formulaires envoyés. Voir [Configuration du stockage pour les données de brouillons et de formulaires envoyés](/help/forms/using/adaptive-forms-best-practices.md#external-storage).
* Utilisez le composant de formulaire Termes et conditions pour obtenir le consentement explicite de l’utilisateur avant d’activer l’enregistrement automatique. Dans ce cas, activez l’enregistrement automatique uniquement lorsque l’utilisateur accepte les conditions du composant Termes et conditions .


