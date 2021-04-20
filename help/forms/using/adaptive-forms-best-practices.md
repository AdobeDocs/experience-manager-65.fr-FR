---
title: Meilleures pratiques pour travailler avec les formulaires adaptatifs
seo-title: Meilleures pratiques pour travailler avec les formulaires adaptatifs
description: Définit les meilleures pratiques à appliquer pour la mise en place d’un projet AEM Forms, le développement de formulaires adaptatifs et l’optimisation des performances du système AEM Forms.
seo-description: Définit les meilleures pratiques à appliquer pour la mise en place d’un projet AEM Forms, le développement de formulaires adaptatifs et l’optimisation des performances du système AEM Forms.
uuid: ed95fc64-56b3-4ea1-a5ba-2e96953fca56
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
discoiquuid: 43c431e4-5286-4f4e-b94f-5a7451c4a22c
feature: Adaptive Forms
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '0'
ht-degree: 0%

---


# Meilleures pratiques pour travailler avec les formulaires adaptatifs {#best-practices-for-working-with-adaptive-forms}

## Présentation {#overview}

Adobe Experience Manager (AEM) Forms vous permet de transformer des opérations complexes en de simples et remarquables expériences numériques. Toutefois, il nécessite un effort concerté pour la mise en œuvre, la création, l’exécution et la conservation d’un écosystème d’AEM Forms efficace et productif.

Ce document fournit des instructions et des recommandations dont peuvent bénéficier l’administrateur, les auteurs et les développeurs de formulaires au moment d’utiliser AEM Forms, notamment le composant de formulaires adaptatifs. Il aborde les meilleures pratiques à appliquer, de l’installation d’un projet de développement de formulaires à la configuration, la personnalisation, la création et l’optimisation d’AEM Forms. Ces meilleures pratiques contribuent globalement aux performances globales de l’écosystème d’AEM Forms.

En outre, voici quelques recommandations de lecture concernant les meilleures pratiques générales d’AEM :

* [Meilleures pratiques : Déploiement et gestion des AEM](/help/sites-deploying/best-practices.md)
* [Meilleures pratiques : création de contenu](/help/sites-authoring/best-practices.md)
* [Meilleures pratiques : administration d’AEM](/help/sites-administering/administer-best-practices.md)
* [Meilleures pratiques : développement de solutions](/help/sites-developing/best-practices.md)

## Installation et configuration d’AEM Forms {#set-up-and-configure-aem-forms}

### Installation du projet de développement de formulaires {#setting-up-forms-development-project}

Une structure de projet simplifiée et normalisée peut considérablement réduire les efforts de développement et de maintenance. Apache Maven est un outil à code source libre recommandé pour la création de projets AEM.

* Utilisez Apache Maven `aem-project-archetype` pour créer et gérer la structure du projet AEM. Il permet de créer la structure et les modèles recommandés pour votre projet AEM. En outre, il fournit des systèmes d’automatisation de création et de contrôle des modifications pour aider à la gestion du projet.

   * Utilisez la commande Maven`archetype:generate` pour générer la structure initiale.
   * Utilisez la commande Maven `eclipse:eclipse` pour générer les fichiers de projet Eclipse et importer le projet dans Eclipse.

Pour plus d’informations, reportez-vous à la section [Comment créer des projets AEM à l’aide d’Apache Maven](/help/sites-developing/ht-projects-maven.md).

* L’outil FileVault ou VLT vous permet de tracer le contenu d’une instance CRX ou AEM dans votre système de fichiers. Il fournit des opérations de gestion du contrôle des modifications, telles que l’archivage et l’extraction du contenu du projet AEM. Voir [Comment utiliser l’outil VLT](/help/sites-developing/ht-vlttool.md).

* Si vous utilisez l’environnement de développement intégré Eclipse, vous pouvez utiliser les outils de développement d’AEM pour l’intégration homogène de l’environnement Eclipse avec les instances AEM, et ainsi créer des applications AEM. Pour plus d’informations, reportez-vous à la section [Outils de développement d’AEM pour Eclipse](/help/sites-developing/aem-eclipse.md).

* Ne stockez aucun contenu ou n&#39;apportez aucune modification dans le dossier /libs. Créez des incrustations dans les dossiers /app pour étendre ou remplacer les fonctionnalités par défaut.

* Lorsque vous créez des packages pour déplacer du contenu, assurez-vous que les chemins de filtre de package sont corrects et que seuls les chemins obligatoires sont mentionnés.

* Ne stockez aucun contenu ou n&#39;apportez aucune modification dans le dossier /libs. Créez des incrustations dans les dossiers /app pour étendre ou remplacer les fonctionnalités par défaut.

* Définissez des dépendances correctes pour les packages afin de forcer un ordre/une séquence d’installation prédéterminé.

* Ne créez aucun noeud référencable dans /libs ou /apps.

### Planification de l’environnement de création {#planning-for-authoring-environment}

Une fois votre projet AEM configuré, définissez la stratégie de création et de personnalisation des composants et modèles de formulaires adaptatifs.

* Un modèle de formulaire adaptatif correspond à une page AEM spécialisée qui définit la structure et les informations d’en-tête/de pied de page d’un formulaire adaptatif. Il est composé de dispositions, de styles et d’une structure de base préconfigurés pour un formulaire adaptatif. AEM Forms propose des modèles et des composants prêts à l’emploi que vous pouvez utiliser pour créer des formulaires adaptatifs. Toutefois, vous pouvez créer des modèles et des composants personnalisés en fonction de vos besoins. Il est recommandé de regrouper les conditions dont vous aurez besoin dans vos formulaires adaptatifs pour les modèles et composants supplémentaires. Pour plus d’informations, reportez-vous à la section [Personnalisation des composants et formulaires adaptatifs](/help/forms/using/adaptive-forms-best-practices.md#customize-components).
* AEM Forms vous permet de créer des formulaires adaptatifs qui reposent sur les modèles de formulaire suivants. Les modèles de formulaire ont un rôle d’interface destinée à l’échange des données entre un formulaire et un système AEM, et fournissent une structure XML pour le flux de données dans le formulaire adaptatif ou à l’extérieur. En outre, les modèles de formulaire imposent des règles et contraintes aux formulaires adaptatifs sous forme de schéma et de contraintes XFA.

   * **Aucun** : les formulaires adaptatifs créés avec cette option n’utilisent pas de modèle de formulaire. Les données XML générées à partir de ce type de formulaire présentent une structure plate avec des champs et des valeurs correspondantes.
   * **SCHÉMA** XML ou JSON : Les schémas XML et JSON représentent la structure dans laquelle les données sont produites ou utilisées par le système principal de votre entreprise. Vous pouvez associer un schéma à un formulaire adaptatif et utiliser ses éléments pour ajouter du contenu dynamique à un formulaire adaptatif. Les éléments du schéma sont disponibles dans l’onglet Objet du modèle de données du navigateur de contenu pour la création de formulaires adaptatifs. Vous pouvez faire glisser et déposer les éléments du schéma pour créer le formulaire.
   * **Modèle de formulaire XFA** : il s’agit du modèle de formulaire idéal si vous avez des investissements dans des formulaires HTML5 de type XFA. Il fournit une méthode directe de conversion des formulaires de type XFA en formulaires adaptatifs. Toutes les règles XFA existantes sont conservées dans les formulaires adaptatifs associés. Les formulaires adaptatifs qui en résultent prennent en charge les éléments XFA, tels que les validations, les événements, les propriétés et les motifs.
   * **Modèle** de données de formulaire : Il s’agit d’un modèle de formulaire préféré si vous souhaitez intégrer vos systèmes principaux tels que les bases de données, les services Web et le profil utilisateur AEM pour préremplir les formulaires adaptatifs et réécrire les données de formulaire envoyées dans les systèmes principaux. Un éditeur de modèle de données de formulaire vous permet de définir et de configurer des entités et des services dans un modèle de données de formulaire que vous pouvez utiliser pour créer des formulaires adaptatifs. Pour plus d’informations, voir [Intégration des données AEM Forms](/help/forms/using/data-integration.md).

Il est important de sélectionner avec soin le modèle de données qui correspond à vos besoins, tout en optimisant vos investissements existants dans les ressources XFA et XSD, le cas échéant. Il est recommandé d’utiliser XSD Model pour créer des modèles de formulaire car le fichier XML généré contient les données selon l’expression XPATH définie par le schéma. L’utilisation de XSD Model comme choix par défaut pour le modèle de données de formulaire est également utile, car il dissocie la conception de formulaire du système d’arrière-plan qui traite et consomme les données et il améliore les performances du formulaire en raison du mappage un-à-un du champ de formulaire. En outre, la valeur BindRef du champ peut être utilisée comme XPATH de sa valeur de données dans le fichier XML.

Pour plus d’informations, voir [Création d’un formulaire adaptatif](/help/forms/using/creating-adaptive-form.md).

* Il existe des sections communes aux formulaires adaptatifs. Vous pouvez les identifier et définir une stratégie pour encourager la réutilisation du contenu. Les formulaires adaptatifs vous permettent de créer des fragments autonomes et de les réutiliser dans plusieurs formulaires. Vous pouvez également enregistrer un panneau sous forme de fragment dans un formulaire adaptatif. Toute modification effectuée dans un fragment est répercutée dans tous les formulaires associés. Cette fonction vous permet de réduire le temps de création et garantit la cohérence entre les formulaires. En outre, l’utilisation de fragments réduit le volume des formulaires adaptatifs, ce qui entraîne une amélioration des fonctions de création, plus particulièrement pour les formulaires volumineux. Pour plus d’informations, voir [Fragments de formulaire adaptatif](/help/forms/using/adaptive-form-fragments.md).

### Personnalisation des composants et formulaires adaptatifs {#customize-components}

* AEM Forms propose des modèles de formulaire adaptatif prêts à l’emploi que vous pouvez utiliser pour créer des formulaires adaptatifs. Vous pouvez également créer vos propres modèles. AEM fournit des modèles statiques et modifiables.

   * Les modèles statiques sont définis et configurés par les développeurs.
   * Les modèles modifiables sont créés par les auteurs à l’aide de l’éditeur de modèles. L’éditeur de modèle vous permet de définir une structure de base et un contenu initial dans un modèle. Toute modification dans la couche de structure est reflétée dans tous les formulaires utilisant ce modèle. Le contenu initial peut inclure un thème préconfiguré, un service de préremplissage, une action d’envoi, etc. Toutefois, ces paramètres peuvent être modifiés pour un formulaire à l’aide de l’éditeur de formulaires. Pour plus d’informations, voir [Modèles de formulaires adaptatifs](/help/forms/using/template-editor.md).

* Pour la mise en forme d’une instance de champ ou de panneau spécifique, utilisez [la mise en forme en ligne ](/help/forms/using/inline-style-adaptive-forms.md). Vous pouvez également définir une classe dans un fichier CSS et spécifier le nom de classe dans la propriété CSS Class du composant.
* Intégrez une bibliothèque client à un composant pour appliquer de manière constante des styles aux formulaires adaptatifs ou fragments utilisant ce composant. Pour plus d’informations, reportez-vous à la section [Création d’un composant de page de formulaire adaptatif](/help/forms/using/custom-adaptive-forms-templates.md).
* Appliquez des styles définis dans une bibliothèque client pour sélectionner les formulaires adaptatifs, en spécifiant le chemin d’accès à la bibliothèque client dans le champ relatif au chemin d’accès au fichier CSS des propriétés du conteneur de formulaire adaptatif.
* Pour créer une bibliothèque client de vos styles, vous pouvez configurer le fichier CSS personnalisé dan la bibliothèque client de base de l’éditeur de thème ou dans les propriétés du conteneur de formulaire.
* Les formulaires adaptatifs proposent des mises en page de panneau (dispositions réactives en onglet ou en accordéon par exemple) ainsi qu’un assistant pour contrôler la disposition des composants de formulaire. Vous pouvez créer des dispositions de panneau personnalisées et les rendre accessibles aux auteurs de formulaire. Pour plus d’informations, voir [Création de composants de disposition personnalisés pour les formulaires adaptatifs](/help/forms/using/custom-layout-components-forms.md).
* Vous pouvez également personnaliser les composants spécifiques d’un formulaire adaptatif tels que les champs et la disposition des panneaux.

   * Utilisez la fonctionnalité [Recouvrement](/help/sites-developing/overlays.md) d’AEM pour modifier une copie d’un composant. Il n’est pas recommandé de modifier les composants par défaut.
   * Pour personnaliser la mise en page des composants de formulaire adaptatif prêts à l’emploi dans /libs,[ créez des composants de disposition personnalisés](/help/forms/using/custom-layout-components-forms.md) en plus des [dispositions par défaut](/help/forms/using/layout-capabilities-adaptive-forms.md).
   * Intégrez les interactivités personnalisées en créant des widgets ou des apparences personnalisés. Il n’est pas recommandé de modifier les composants par défaut. Pour plus d’informations, reportez-vous à la section [Aspect des structures](/help/forms/using/introduction-widgets.md).

* Pour connaître les recommandations relatives à la gestion des données d’identification personnelle, reportez-vous à la section [Gestion des informations d’identification personnelle.](/help/forms/using/adaptive-forms-best-practices.md#p-handling-personally-identifiable-information-p)

## Création de formulaires adaptatifs {#author-adaptive-forms}

### Utilisation de l’interface utilisateur optimisée pour les écrans tactiles pour la rédaction {#using-touch-optimized-ui-for-authoring}

* Utilisez le navigateur Objets dans la barre latérale pour accéder rapidement aux champs situés au plus profond de la hiérarchie de formulaires. Vous pouvez utiliser la zone de recherche pour rechercher des objets dans le formulaire ou l’arborescence d’objets pour passer d’un objet à un autre.
* Pour vue et modifier les propriétés d&#39;un composant dans l&#39;explorateur de composants de la barre latérale, sélectionnez le composant et cliquez sur ![cmppr-1](assets/cmppr-1.png). Vous pouvez également cliquer deux fois sur un composant pour afficher ses propriétés dans le navigateur de propriétés.
* Utilisez les raccourcis clavier pour effectuer des actions rapides sur vos formulaires. Voir [Raccourcis clavier AEM Forms](/help/forms/using/keyboard-shortcuts.md).

* L’utilisation des composants de formulaire adaptatif est recommandée uniquement dans les pages de formulaire adaptatif. Les composants dépendent de leur hiérarchie parent. Par conséquent, ne les utilisez pas dans une page AEM.

Consultez également les descriptions des composants et les meilleures pratiques dans [Introduction à la création de formulaires adaptatifs](/help/forms/using/introduction-forms-authoring.md).

### Utilisation de règles dans les formulaires adaptatifs  {#using-rules-in-adaptive-forms}

AEM Forms fournit un [éditeur de règles](/help/forms/using/rule-editor.md) qui vous permet de créer des règles pour ajouter un comportement dynamique aux composants de formulaire adaptatif. Ces règles vous permettent d’évaluer les conditions et de déclencher des actions sur les composants, telles que l’affichage ou le masquage de champs, le calcul de valeurs, la modification dynamique de la liste déroulante, etc.

L’éditeur de règles fournit un éditeur vidéo et un éditeur de code destinés à la définition des règles. Lorsque vous définissez les règles à l’aide de l’éditeur de code, vous devez prendre en compte les éléments suivants :

* Utilisez des noms uniques et pertinents pour les champs de formulaire et les composants afin d’éviter tout conflit potentiel lors de la définition des règles.
* Utilisez l’opérateur `this` pour un composant afin d’y faire mention lors de l’expression d’une règle. Ainsi, la règle reste valide même si le nom du composant est modifié. Par exemple, `field1.valueCommit script: this.value > 10`.

* Utilisez les noms de composant lorsque vous faites référence à d’autres composants de formulaire. Utilisez la propriété `value` pour récupérer la valeur d’un champ ou d’un composant. Par exemple, `field1.value`.

* Désignez les composants selon une hiérarchie relative unique afin d’éviter tout conflit. Par exemple, `parentName.fieldName`.

* Lorsque vous manipulez des règles complexes ou couramment utilisées, pensez à écrire une logique métier en tant que fonctions dans une bibliothèque cliente distincte que vous pouvez spécifier et réutiliser dans les formulaires adaptatifs. La bibliothèque client doit être une bibliothèque autonome et ne doit donc avoir aucune dépendance externe, à l’exception de jQuery et Underscore.js. Vous pouvez également utiliser la bibliothèque cliente pour appliquer [la revalidation côté serveur](/help/forms/using/configuring-submit-actions.md#server-side-revalidation-in-adaptive-form) des données de formulaire envoyées.
* Les formulaires adaptatifs fournissent un ensemble d’API que vous pouvez utiliser pour communiquer et effectuer des actions sur des formulaires adaptatifs. Certains des API clés se présentent comme suit. Pour plus d’informations, reportez-vous à la section [Référence d’API de bibliothèque JavaScript pour les formulaires adaptatifs](https://adobe.com/go/learn_aemforms_documentation_63).

   * `guideBridge.reset()`: Réinitialise un formulaire.
   * `guideBridge.submit()`: Envoie un formulaire.
   * `guideBridge.setFocus(somExp, focusOption, runCompletionExp)`: Définit la cible d’action sur un champ.
   * `guideBridge.validate(errorList, somExpression, focus)`: Valide un formulaire.
   * `guideBridge.getDataXML(options)`: Obtient les données du formulaire au format XML.
   * `guideBridge.resolveNode(somExpression)`: Récupère un objet de formulaire.
   * `guideBridge.setProperty(somList, propertyName, valueList)`: Définit la propriété d’un objet de formulaire.
   * En outre, vous pouvez utiliser les propriétés de champ suivantes :

      * `field.value` pour modifier la valeur d’un champ ;
      * f`ield.enabled`   pour activer/désactiver un champ ;
      * `field.visible` pour modifier la visibilité d’un champ.

* Les auteurs de formulaire adaptatif peuvent avoir à écrire du code JavaScript pour créer la logique d’entreprise dans un formulaire. Lorsque JavaScript est puissant et efficace, il est probable qu’il fasse un compromis sur les attentes en matière de sécurité. Par conséquent, vous devez vous assurer que l’auteur du formulaire est une personne de confiance et qu’il existe des processus permettant de passer en revue et d’approuver le code JavaScript avant qu’un formulaire soit mis en production. L’administrateur peut restreindre l’accès à l’éditeur de règles aux groupes d’utilisateurs en fonction de leur rôle ou de leur fonction. Voir [Autorisation d’accès à l’éditeur de règles pour des groupes d’utilisateurs définis](/help/forms/using/rule-editor-access-user-groups.md).
* Vous pouvez utiliser des expressions dans les règles pour rendre les formulaires adaptatifs dynamiques. Toutes les expressions sont des expressions JavaScript valides qui utilisent des API de modèle de script pour les formulaires adaptatifs. Ces expressions renvoient des valeurs de certains types. Pour plus d’informations sur les expressions et les meilleures pratiques associées, voir [Expressions des formulaires adaptatifs](/help/forms/using/adaptive-form-expressions.md).

### Utilisation des thèmes {#working-with-themes}

Les thèmes de formulaires adaptatifs vous permettent de créer des styles réutilisables pouvant être appliqués à tous les formulaires pour une apparence et un style homogènes. Il est recommandé d’utiliser les thèmes pour définir le style des composants et des panneaux de formulaire. Voici quelques meilleures pratiques en matière de thèmes :

* Utilisez la bibliothèque de ressources pour une application rapide des styles de texte, de l’arrière-plan et des images. Lorsqu’un style est ajouté à la bibliothèque de ressources, il est disponible pour d’autres thèmes et dans le mode Style de l’éditeur de formulaires.
* Appliquez des paramètres globaux tels que la police et l’arrière-plan de la page à l’aide du sélecteur de niveau de page.
* Utilisez les bibliothèques client pour importer le style existant ou avancé dans vos thèmes.
* Vous pouvez remplacer le style pour des champs, des panneaux ou des boutons spécifiques dans un calque de style de formulaire.
* Si un thème ne répond pas à vos besoins en matière de style, vous pouvez utiliser les classes prédéfinies telles que guideFieldNode, guideFieldLabel, guideFieldWidget et guidePanelNode pour appliquer un style commun dans plusieurs formulaires.

Pour plus d’informations, voir [Thèmes](/help/forms/using/themes.md).

### Optimisation des performances de formulaires complexes et volumineux  {#optimizing-performance-of-large-and-complex-forms}

Les auteurs de formulaires et les utilisateurs finaux sont généralement confrontés à des problèmes de performances lors du chargement de formulaires volumineux dans le mode de création ou lors de l’exécution. A mesure que le nombre d’objets (champs et panneaux) dans un formulaire augmente, les performances de création et d’exécution commencent à diminuer. Ainsi, il est impossible pour plusieurs auteurs de travailler simultanément à la création d’un formulaire.

Afin de résoudre ces problèmes de performances dans les formulaires volumineux, appliquez les meilleures pratiques suivantes :

* Il est recommandé de créer si possible des formulaires adaptatifs à l’aide du modèle de données de formulaire XSD, et ce, même lors de la conversion d’un XFA en formulaire adaptatif.
* Intégrez uniquement les champs et panneaux dans les formulaires adaptatifs qui recueillent les informations des utilisateurs. Maintenez le contenu statique au minimum ou utilisez les URL pour les ouvrir dans une fenêtre séparée.
* Bien que chaque formulaire soit conçu pour un rôle spécifique, certains segments sont communs à la plupart des formulaires. Par exemple, les informations personnelles, l’adresse, les détails du poste, etc. Créez [des fragments de formulaire adaptatif](/help/forms/using/adaptive-form-fragments.md) pour les éléments et sections de formulaire courants et utilisez-les dans les formulaires. Vous pouvez également enregistrer en tant que fragment un panneau d’un formulaire existant. Toute modification effectuée dans un fragment est répercutée dans tous les formulaires adaptatifs associés. Cette fonction favorise la création en collaboration : plusieurs auteurs peuvent ainsi travailler simultanément sur différents fragments composant un formulaire.

   * Comme pour les formulaires adaptatifs, il est recommandé de définir les scripts personnalisés et le style spécifiques aux fragments dans la bibliothèque client, via la boîte de dialogue relative au conteneur de fragment. Tentez également de créer des fragments autonomes qui ne dépendent pas d’objets extérieurs.
   * Évitez d’utiliser un script de fragments croisés. Si vous devez désigner un objet situé hors du fragment, essayez de l’intégrer au formulaire parent. Si l’objet doit demeurer dans un autre fragment, mentionnez son nom dans le script..

* Utilisez Enregistrer et reprendre avec l’enregistrement automatique pour enregistrer le formulaire adaptatif périodiquement et permettre aux utilisateurs de revenir plus tard pour remplir le formulaire.
* Configurez les fragments à charger en différé. Au moment de l’exécution, le fragment qui doit être chargé en différé n’est rendu que lorsqu’il est nécessaire. Cette option permet de réduire considérablement le temps de chargement pour les formulaires volumineux. Elle peut également être utilisée dans des fragments avec des panneaux répétables. Pour plus d’informations, reportez-vous à la section [Configuration du chargement différé](/help/forms/using/lazy-loading-adaptive-forms.md).

   * Ne configurez pas le chargement différé sur des fragments d’une mise en page en grille réactive ou dans le premier panneau.
   * Les composants des pièces jointes et des conditions générales ne sont pas pris en charge dans les fragments chargés en différé.
   * Marquez une valeur dans un panneau chargé en différé comme Utiliser la valeur globalement si cette valeur est utilisée dans une autre partie du formulaire afin qu’elle soit disponible lorsque le panneau de contenu est déchargé.
   * Pensez à créer des règles de visibilité pour les fragments qui doivent s’afficher ou être masqués en fonction d’une condition.

### Préremplissage des formulaires adaptatifs  {#prefilling-adaptive-forms}

Vous pouvez préremplir des champs de formulaires adaptatifs avec des données extraites du système d’arrière-plan pour aider les utilisateurs à remplir rapidement le formulaire et éviter de saisir des erreurs.

* AEM Forms fournit un service de préremplissage pour lire les données d’un fichier XML de données prédéfini et préremplir les champs d’un formulaire adaptatif avec le contenu du fichier XML prérempli.
* Les données XML préremplies doivent être conformes au schéma du modèle de formulaire associé au formulaire adaptatif.
* Incluez les sections `afBoundedData` et `afUnBoundedData` dans le fichier XML prérempli pour préremplir les champs liés et non liés d’un formulaire adaptatif.

* Pour les formulaires adaptatifs basés sur le modèle de données de formulaire, AEM Forms fournit le service de préremplissage de modèle de données de formulaire prêt à l’emploi. Le service de préremplissage récupère les sources de données pour les objets de modèle de données dans le formulaire adaptatif et préremplit les valeurs de champ lors du rendu du formulaire.
* Vous pouvez également utiliser les formulaires adaptatifs de préremplissage de protocoles de fichier, crx, de services ou http.
* AEM Forms prend en charge les services de préremplissage personnalisés que vous pouvez brancher en tant que service OSGi pour préremplir des formulaires adaptatifs.

Pour plus d’informations, voir [Préremplissage des champs de formulaire adaptatif](/help/forms/using/prepopulate-adaptive-form-fields.md).

### Signature et envoi de formulaires adaptatifs {#signing-and-submitting-adaptive-forms}

Les formulaires adaptatifs requièrent des actions Envoyer pour traiter les données spécifiées par l’utilisateur. Une action Envoyer détermine la tâche exécutée sur les données envoyées à l’aide d’un formulaire adaptatif.

* Il existe plusieurs actions d’envoi disponibles prêtes à l’emploi dans les formulaires adaptatifs. Pour plus d&#39;informations, voir [Configuration de l&#39;action Envoyer](/help/forms/using/configuring-submit-actions.md).
* Vous pouvez créer une action d’envoi personnalisée si les actions d’envoi par défaut ne remplissent pas votre cas d’utilisation. Pour plus d’informations, voir [Création d’une action Envoyer personnalisée pour les formulaires adaptatifs](/help/forms/using/custom-submit-action-form.md).
* Incluez des validations côté serveur pour empêcher l’envoi de données non valides.

Vous pouvez tirer parti de l’expérience multi-signature d’Adobe Sign dans les formulaires adaptatifs. Tenez compte des points suivants lors de la configuration d’Adobe Sign dans les formulaires adaptatifs. Pour plus d’informations, voir [Utilisation d’Adobe Sign dans un formulaire adaptatif](/help/forms/using/working-with-adobe-sign.md).

* Le formulaire adaptatif comprenant Adobe Sign est envoyé uniquement après que tous les signataires ont signé le formulaire. Les formulaires affichent l’état En attente de signature jusqu’à ce que le formulaire soit signé par tous les signataires.
* Vous pouvez configurer une expérience de signature intégrée ou rediriger les signataires vers une page de signature lors de l’envoi.
* Configurez l’expérience de signature séquentielle ou parallèle, le cas échéant.

### Génération d’un document d’enregistrement  {#generating-document-of-record}

Un document d’enregistrement (DE) est une version PDF aplatie d’un formulaire adaptatif que vous pouvez imprimer, signer ou archiver.

* Selon le modèle de données de formulaire depuis lequel est établi un formulaire adaptatif, vous pouvez configurer un modèle de document d’enregistrement comme suit :

   * **Modèle de formulaire XFA** : utilisation du fichier XDP associé en tant que modèle de document d’enregistrement.
   * **Schéma XSD** : utilisation du modèle XFA associé qui emploie le même schéma XML que le formulaire adaptatif.
   * **Aucun** : utilisation d’un document d’enregistrement généré automatiquement.

* Configurez l’en-tête, le pied de page, les images, la couleur, la police, etc. directement depuis l’onglet Document d’enregistrement de l’éditeur de formulaires adaptatifs.
* Utilisez `DoRService` pour générer le document d’enregistrement par programmation.
* Excluez les champs masqués du document d’enregistrement.
* Utilisez le paramètre de requête `afAcceptLang` pour vue le DE dans un autre paramètre régional.

### Débogage et test des formulaires adaptatifs {#debugging-and-testing-adaptive-forms}

[Le module externe Chrome AEM](https://adobe-consulting-services.github.io/acs-aem-tools/aem-chrome-plugin/) est une extension de navigateur pour Google Chrome qui propose des outils de débogage des formulaires adaptatifs. Les auteurs de formulaire et les développeurs peuvent utiliser ces outils pour effectuer les actions suivantes :

* Identification des étranglements et optimisation des performances en matière de rendu des formulaires
* Correction des erreurs de mots-clés et bindRef dans le formulaire
* Activation et configuration des journaux
* Débogage des règles et des scripts dans le formulaire
* Découverte et apprentissage des API guideBridge

Pour plus d’informations, voir [AEM Module Chrome - Formulaire adaptatif](https://adobe-consulting-services.github.io/acs-aem-tools/aem-chrome-plugin/adaptive-form/).

Calvin SDK est une API utilitaire pour les développeurs de formulaires adaptatifs pour les tester. Le SDK Calvin est construit sur la structure de test [Hobbes.js](https://docs.adobe.com/docs/fr/aem/6-3/develop/ref/test-api/index.html). Vous pouvez utiliser le cadre pour tester les éléments suivants :

* Expérience de rendu d’un formulaire adaptatif
* Expérience de remplissage automatique d’un formulaire adaptatif
* Expérience d’envoi d’un formulaire adaptatif
* Règles d’expression
* Validations
* Chargement différé

Pour plus d’informations, voir [Automatiser les tests des formulaires adaptatifs](/help/forms/using/calvin.md).

### Validation de formulaires adaptatifs sur le serveur AEM  {#validating-adaptive-forms-on-aem-server}

Les validations côté serveur sont nécessaires pour empêcher toute tentative de contournement des validations du client, toute erreur potentielle lors de l’envoi de données et toute violation des règles de fonctionnement. Les validations côté serveur sont exécutées sur le serveur lors du chargement de la bibliothèque client requise.

* Intégrez des fonctionnalités à une bibliothèque client pour valider les expressions dans les formulaires adaptatifs, et définissez la bibliothèque client dans la boîte de dialogue relative au conteneur des formulaires adaptatifs. Pour plus d’informations, reportez-vous à la section [Revalidation côté serveur](/help/forms/using/configuring-submit-actions.md#p-server-side-revalidation-in-adaptive-form-p).
* La validation côté serveur permet de valider le modèle de formulaire. Il est recommandé de créer une bibliothèque client séparée pour les validations et de ne pas la mélanger à d’autres éléments. Par exemple, ne placez pas le style HTML et la manipulation DOM HTML dans la même bibliothèque client.

### Localisation des formulaires adaptatifs  {#localizing-adaptive-forms}

AEM fournit des flux de travaux de traduction que vous pouvez utiliser pour localiser les formulaires adaptatifs. Pour plus d’informations, voir [Utilisation de processus de traduction AEM pour la localisation des formulaires adaptatifs](/help/forms/using/using-aem-translation-workflow-to-localize-adaptive-forms.md).

Certaines meilleures pratiques en matière de localisation des formulaires adaptatifs sont les suivantes :

* Utilisez les fragments de formulaire adaptatif pour les éléments communs à tous les formulaires et localisez les fragments. De cette façon, vous localisez un fragment une seule fois et il apparaît localisé dans tous les formulaires où il est utilisé.
* Les modifications telles que l’ajout d’un nouveau composant ou l’application d’un script dans un formulaire localisé ne sont pas localisées automatiquement. Par conséquent, vous devez finaliser un formulaire avant de le localiser pour éviter plusieurs cycles de localisation.
* Utilisez le paramètre de requête `afAcceptLang` pour remplacer la langue du navigateur et pour rendre le formulaire dans la langue spécifiée. Par exemple, l’URL suivante force le rendu du formulaire en japonais, quel que soit le paramètre régional spécifié dans le navigateur :

   `https://'[server]:[port]'/<contextPath>/<formFolder>/<formName>.html?wcmmode=disabled&afAcceptLang=ja`

* AEM Forms prend actuellement en charge la localisation du contenu des formulaires adaptatifs en anglais (en), espagnol (es), français (fr), italien (it), allemand (de), japonais (ja), portugais-brésilien (pt-BR), chinois (zh-CN), chinois-taïwanais (zh-TW) et coréen (ko-KR). Cependant, vous pouvez ajouter la prise en charge de nouveaux paramètres régionaux pour les formulaires adaptatifs à l’exécution.  Pour plus d’informations, voir [Support de nouveaux paramètres régionaux pour la localisation de formulaires adaptatifs](/help/forms/using/supporting-new-language-localization.md).

## Préparation du projet de formulaires à des fins de production  {#prepare-forms-project-for-production}

### Ajout du serveur de traitement de formulaires {#adding-forms-processing-server}

Vous pouvez configurer une instance supplémentaire du serveur AEM Forms situé derrière le pare-feu dans une zone sécurisée. Vous pouvez utiliser cette instance pour :

* **Traitement** par lots : tâches récurrentes ou planifiées dans des lots à charge importante. Par exemple, l’impression d’instructions, la génération de correspondances et l’utilisation de services de document comme PDF Generator, Output et Assembler.
* **Le stockage des données d’identification personnelle** : enregistrer ses données d’identification personnelle sur le serveur de traitement. Cette fonction n’est pas nécessaire si vous utilisez déjà un fournisseur personnalisé de stockage pour les données d’identification personnelle.

### Déplacement du projet vers un autre environnement  {#moving-project-to-another-environment}

Il est souvent nécessaire de déplacer vos projets AEM d’un environnement à un autre. Certaines étapes clés à ne pas oublier lors du déplacement sont les suivantes :

* Effectuez une sauvegarde des bibliothèques client existantes, de votre code personnalisé, ainsi que des configurations définies.
* Déployez manuellement les packages et correctifs du produit dans l’ordre spécifié dans le nouvel environnement.
* Déployez manuellement et distinctement les packages et lots de code spécifiques au projet sur le nouveau serveur AEM.
* (*AEM Forms on JEE uniquement*) Déployez manuellement les LCA et les DSC sur le serveur de processus des formulaires.
* Utilisez la fonctionnalité [Importation/exportation](/help/forms/using/import-export-forms-templates.md) pour déplacer des actifs vers le nouvel environnement. Vous pouvez également configurer l’agent de réplication et publier les actifs.
* Lors de la mise à niveau, remplacez toutes les API et fonctionnalités obsolètes par de nouvelles API et fonctionnalités.

### Configuration d’AEM {#configuring-aem}

Certaines des meilleures pratiques de configuration d’AEM pour l’amélioration des performances générales sont les suivantes :

* Activez la compression de la bibliothèque client HTML pour Javascript et CSS à partir de la console Felix. Voir [Clientlibs expliqués par exemple](https://blogs.adobe.com/experiencedelivers/experience-management/clientlibs-explained-example/).
* Mettez en cache toutes les bibliothèques clientes à `/etc.clientlibs/fd` et toutes les bibliothèques clientes personnalisées supplémentaires sur le répartiteur d’AEM afin d’accroître la réactivité et la sécurité de vos formulaires publiés. Pour plus d’informations, reportez-vous à la section [Dispatcher](https://helpx.adobe.com/experience-manager/dispatcher/using/dispatcher.html).

* Ne mettez pas en cache les chemins `/content/forms/af/` et `/content/dam/formsanddocuments/*`. pour plus d’informations sur la configuration de la mise en cache des formulaires adaptatifs, voir [Mise en cache des formulaires adaptatifs](/help/forms/using/configure-adaptive-forms-cache.md).

* Activez l’HTML via le module de compression de serveur Web. Pour plus d’informations, reportez-vous à la section [Réglage des performances du serveur AEM Forms](/help/forms/using/performance-tuning-aem-forms.md).
* Augmentez la configuration des appels par demande pour les formulaires volumineux. Reportez-vous à la section [Optimisation des performances des formulaires complexes et volumineux](/help/forms/using/adaptive-forms-best-practices.md#optimizing-performance-of-large-and-complex-forms).
* Créez [des pages d’erreur personnalisées affichées par le gestionnaire d’erreurs](https://helpx.adobe.com/experience-manager/6-2/sites-developing/customizing-errorhandler-pages.html).
* Sécurisez le serveur AEM Forms.

   * Utilisez le mode d’exécution `nosamplecontent` pour vous assurer qu’aucun exemple de contenu ou d’utilisateur ne soit déployé sur le serveur de production. Voir [Exécution d’AEM en mode prêt pour la production](/help/sites-administering/production-ready.md).

* La taille de tas doit avoir une capacité d’au moins 8 Go. Pour plus d’informations sur les autres paramètres, reportez-vous à la section [Réglage des performances du serveur AEM Forms](/help/forms/using/performance-tuning-aem-forms.md).
* Utilisez les sessions utilisateur du service au lieu des sessions administrateur pour exécuter les tâches au niveau du service. Pour plus d’informations, reportez-vous à la section [Authentification du service](https://sling.apache.org/documentation/the-sling-engine/service-authentication.html).

>[!VIDEO](https://vimeo.com/)

### Configuration du stockage pour les données de brouillons et de formulaires envoyés {#external-storage}

Dans un environnement de production, il est recommandé de ne pas stocker les données de formulaire envoyées dans le référentiel AEM. La mise en œuvre par défaut des actions d’envoi Forms Portal Store, Stocker le contenu et Stocker le PDF stockent les données de formulaire dans le référentiel AEM. Ces actions d’envoi servent uniquement à des fins de démonstration. En outre, les fonctions Enregistrer et reprendre et Enregistrement automatique stockent les données dans le portail par défaut. Tenez donc compte des recommandations suivantes :

* **Stockage des données de brouillon** : si vous utilisez la fonction Brouillon des formulaires adaptatifs, vous devez implémenter une SPI (Service Provide Interface) personnalisée pour le stockage des données de brouillon dans un espace de stockage plus sécurisé comme une base de données. Pour plus d’informations, voir [Exemple d’intégration d’un composant de brouillons et d’envois à la base de données](/help/forms/using/integrate-draft-submission-database.md).

* **Stockage des données** d&#39;envoi : Si vous utilisez le magasin d’envoi de Forms Portal, vous devez implémenter une interface SPI personnalisée pour stocker les données d’envoi dans une base de données. Voir [Exemple d’intégration du composant brouillons &amp; envois à la base de données](/help/forms/using/integrate-draft-submission-database.md) pour un exemple d’intégration.

   Vous pouvez également écrire une action d’envoi personnalisée qui stocke les données de formulaires et les pièces jointes dans un espace de stockage sécurisé. Voir [Création d’une action Envoyer personnalisée pour les formulaires adaptatifs](/help/forms/using/custom-submit-action-form.md) pour plus d’informations.

* **Longueur de l&#39;ID** de brouillon : Lorsque vous enregistrez un formulaire adaptatif en tant que brouillon, un ID de brouillon est généré pour identifier de manière unique le brouillon. La longueur minimale du champ ID de brouillon est de 26 caractères. L’Adobe recommande de définir la longueur du brouillon d’ID sur 26 caractères ou plus.

### Traitement des informations d’identification personnelle {#handling-personally-identifiable-information}

Le traitement des données d’identification personnelle (PII) représente l’un des principaux défis pour les entreprises. Certaines des meilleures pratiques de gestion de telles données sont les suivantes :

* Utilisez un stockage sécurisé et externe, comme une base de données, pour le stockage des données de brouillons et de formulaires envoyés. Voir [Configuration de l’enregistrement externe pour les brouillons et les données de formulaires envoyés](/help/forms/using/adaptive-forms-best-practices.md#external-storage).
* Utilisez le composant de formulaire relatif aux termes et conditions pour demander le consentement explicite de l’utilisateur avant l’enregistrement automatique. Dans ce cas, activez l’enregistrement automatique uniquement lorsque l’utilisateur accepte les conditions énoncées.

