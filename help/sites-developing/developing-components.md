---
title: Développer des composants AEM
seo-title: Developing AEM Components
description: Les composants AEM servent à stocker, mettre en forme et générer le rendu du contenu diffusé dans vos pages Web.
seo-description: AEM components are used to hold, format, and render the content made available on your webpages.
uuid: 1f39daa6-7277-45a2-adcc-74b58c93b8e4
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: components
content-type: reference
discoiquuid: 8cdb6db4-adaa-4eda-af7d-310a0b44b80b
docset: aem65
legacypath: /content/docs/en/aem/6-2/develop/components/components-touch-optimized
exl-id: 573cdc36-e9c3-4803-9c4e-cebd0cf0a56f
source-git-commit: 50d29c967a675db92e077916fb4adef6d2d98a1a
workflow-type: tm+mt
source-wordcount: '3454'
ht-degree: 98%

---

# Développer des composants AEM{#developing-aem-components}

Les composants AEM servent à stocker, mettre en forme et générer le rendu du contenu diffusé dans vos pages Web.

* Lors de la [création de pages](/help/sites-authoring/default-components.md), les composants permettent aux auteurs de modifier et de configurer le contenu.

   * Lors de la construction d’un site [marchand](/help/commerce/cif-classic/administering/ecommerce.md), les composants peuvent, par exemple, collecter et afficher des informations issues du catalogue.
Pour plus d’informations, consultez [Développement du e-commerce](/help/commerce/cif-classic/developing/ecommerce.md).

   * Lors de la construction d’un site de [communauté](/help/communities/author-communities.md), les composants peuvent fournir des informations et en collecter auprès des visiteurs.
Pour plus d’informations, consultez [Développement de communautés](/help/communities/communities.md).

* Dans l’instance de publication, les composants réalisent le rendu du contenu en le présentant comme vous le souhaitez aux visiteurs et visiteuses de votre site web.

>[!NOTE]
>
>Cette page est la suite du document [Composants AEM – Notions de base](/help/sites-developing/components-basics.md).

>[!CAUTION]
>
>Les composants sous `/libs/cq/gui/components/authoring/dialog` s’utilisent uniquement dans l’éditeur (boîtes de dialogue de composants dans l’instance de création). S’ils sont utilisés ailleurs (par exemple dans une boîte de dialogue d’assistant), ils peuvent ne pas se comporter comme prévu.

## Exemples de code {#code-samples}

Cette page contient la documentation de référence (ou des liens vers la documentation de référence) requise pour développer des composants AEM. Consultez [Développement de composants AEM - Exemples de code](/help/sites-developing/developing-components-samples.md) pour des exemples pratiques.

## Structure {#structure}

La structure de base d’un composant est décrite à la page [Composants AEM – Notions de base](/help/sites-developing/components-basics.md#structure). Ce document traite à la fois les interfaces utilisateur tactile et classique. Même si vous n’avez pas besoin d’utiliser les paramètres classiques de votre nouveau composant, il peut être utile d’en prendre connaissance lors de l’héritage de composants existants.

## Optimiser les composants et les boîtes de dialogue existants {#extending-existing-components-and-dialogs}

Selon le composant que vous souhaitez implémenter, il peut être possible d’optimiser ou de personnaliser une instance existante, plutôt que de définir et de développer l’ensemble de la [structure](#structure) à partir de zéro.

Lors de l’optimisation ou de la personnalisation d’un composant existant ou d’une boîte de dialogue existanet, vous pouvez copier ou répliquer la structure entière ou la structure requise pour la boîte de dialogue avant d’apporter vos modifications.

### Optimiser un composant existant {#extending-an-existing-component}

L’optimisation d’un composant existant peut être réalisée avec la [Hiérarchie du type de ressource](/help/sites-developing/components-basics.md#component-hierarchy-and-inheritance) et les mécanismes d’héritage qui s’y rapportent.

>[!NOTE]
>
>Il est également possible de redéfinir les composants avec une superposition en fonction de la logique du chemin de recherche. Cependant, dans ce cas, [Sling Resource Merger](/help/sites-developing/sling-resource-merger.md) n’est pas déclenché et `/apps` doit définir le recouvrement en entier.

>[!NOTE]
>
>Le [composant de fragment de contenu](/help/sites-developing/customizing-content-fragments.md) peut également être personnalisé et optimisé, bien que la structure complète et les relations avec les ressources doivent être prises en compte.

### Personnaliser une boîte de dialogue de composant existante {#customizing-a-existing-component-dialog}

Il est également possible de remplacer une *boîte de dialogue de composant* en utilisant le [Sling Resource Merger](/help/sites-developing/sling-resource-merger.md) et en définissant la propriété `sling:resourceSuperType`.

Ainsi, vous avez seulement besoin de redéfinir les modifications à apporter et non pas toute la boîte de dialogue (en utilisant `sling:resourceSuperType`). Cette méthode est désormais recommandée pour optimiser une boîte de dialogue de composant.

Voir [Sling Resource Merger](/help/sites-developing/sling-resource-merger.md) pour plus d’informations.

## Définir le balisage {#defining-the-markup}

Votre composant est rendu dans le langage [HTML](https://www.w3schools.com/htmL/html_intro.asp). Votre composant doit définir les balises HTML nécessaires pour réaliser le rendu du contenu selon les besoins, dans les environnements de création et de publication.

### Utiliser le langage de modèle HTML {#using-the-html-template-language}

Le [langage de modèle HTML (HTL)](https://experienceleague.adobe.com/docs/experience-manager-htl/using/overview.html?lang=fr) a été introduit avec AEM 6.0 et remplace JSP (JavaServer Pages) en tant que système de modèle côté serveur privilégié et recommandé pour HTML. Pour les développeurs et développeuses web qui souhaitent créer des sites eb d’entreprise robustes, le langage HTL permet d’améliorer la sécurité et l’efficacité du développement.

>[!NOTE]
>
>Bien que HTL et JSP puissent être utilisés pour le développement de composants, nous allons illustrer le développement avec HTL sur cette page, car il s’agit du langage de script recommandé pour AEM.

## Développer la logique de contenu {#developing-the-content-logic}

Cette logique facultative sélectionne et/ou calcule le contenu dont il faut réaliser le rendu. Elle est appelée à partir d’expressions HTL avec le modèle Use-API approprié.

Le mécanisme permettant de séparer la logique de l’aspect aide à définir clairement ce qui est appelé pour un affichage donné. Cela permet également une logique différente pour différentes vues d’une même ressource.

### Utilisation de Java {#using-java}

[L’Use-API Java HTL permet à un fichier HTL d’accéder aux méthodes d’assistance dans une classe Java personnalisée. ](https://experienceleague.adobe.com/docs/experience-manager-htl/content/java-use-api.html?lang=fr) Cela vous permet d’utiliser le code JavaScript pour implémenter la logique de sélection et de configuration du contenu du composant.

### Utiliser JavaScript {#using-javascript}

[L’Use-API JavaScript HTL permet à un fichier HTL d’accéder au code d’assistance écrit en JavaScript](https://experienceleague.adobe.com/docs/experience-manager-htl/content/java-use-api.html?lang=fr). Vous pouvez ainsi utiliser du code JavaScript pour implémenter la logique de sélection et de configuration du contenu du composant.

### Utiliser les bibliothèques HTML côté client {#using-client-side-html-libraries}

Les sites web modernes reposent largement sur un traitement côté client piloté par un code JavaScript et CSS complexe. Organiser et optimiser la diffusion de ce code est une opération qui peut se révéler complexe.

Pour résoudre ce problème, AEM fournit **Dossiers de bibliothèques côté client**, qui vous permet de stocker votre code côté client dans le référentiel, de l’organiser en catégories et de définir quand et comment chaque catégorie de code doit être diffusée au client. Le système de bibliothèque côté client se charge alors de la génération des liens appropriés dans la page Web finale pour charger le code correct.

Consultez [Utilisation de bibliothèques HTML côté client](/help/sites-developing/clientlibs.md) pour plus d’informations.

## Configurer le comportement de modification {#configuring-the-edit-behavior}

Vous pouvez configurer le comportement de modification d’un composant, notamment ses attributs tels que les actions disponibles pour le composant, les caractéristiques de l’éditeur local et les écouteurs liés aux événements sur le composant. La configuration est commune aux interfaces utilisateur tactile et classique, avec toutefois certaines différences spécifiques.

La [configuration du comportement de modification d’un composant](/help/sites-developing/components-basics.md#edit-behavior) s’effectue en ajoutant un nœud `cq:editConfig` de type `cq:EditConfig` sous le nœud de composant (de type `cq:Component`), ainsi qu’en ajoutant des nœuds enfants et des propriétés spécifiques.

## Configurer le comportement de prévisualisation {#configuring-the-preview-behavior}

Le cookie [Mode Gestion de contenu Web](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/wcm/api/WCMMode.html) est défini lors du passage en mode **Aperçu** même lorsque la page n’est pas rafraîchie.

Pour les composants dont le rendu est sensible au Mode Gestion de contenu Web, ils doivent être définis de manière à s’actualiser eux-mêmes, puis s’appuyer sur la valeur du cookie.

>[!NOTE]
>
>Dans l’IU tactile, seules les valeurs `EDIT` et `PREVIEW` sont utilisées pour le cookie [Mode Gestion de contenu Web](https://developer.adobe.com/experience-manager/reference-materials/6-5/javadoc/com/day/cq/wcm/api/WCMMode.html).

## Créer et configurer une boîte de dialogue {#creating-and-configuring-a-dialog}

Les boîtes de dialogue permettent à l’auteur d’interagir avec le composant. L’utilisation d’une boîte de dialogue permet aux auteurs et aux administrateurs de modifier le contenu, de configurer le composant ou de définir les paramètres de conception (dans une [Boîte de dialogue de conception](#creating-and-configuring-a-design-dialog)).

### IU Coral et IU Granite {#coral-ui-and-granite-ui}

[Coral UI](https://developer.adobe.com/experience-manager/reference-materials/6-5/coral-ui/coralui3/index.html) et [Granite UI](https://developer.adobe.com/experience-manager/reference-materials/6-5/granite-ui/api/jcr_root/libs/granite/ui/index.html) définissent l’aspect moderne d’AEM.

[L’IU Granite offre un vaste éventail de composants de base (widgets)](https://developer.adobe.com/experience-manager/reference-materials/6-5/granite-ui/api/jcr_root/libs/granite/ui/index.html) nécessaires pour créer une boîte de dialogue dans l’environnement de création. Si nécessaire, vous pouvez étendre cette sélection et [créer votre propre widget](#creatinganewwidget).

Pour plus d’informations, consultez :

* IU Coral

   * Fournit une interface utilisateur uniforme dans toutes les solutions cloud.
   * [Concepts de l’IU tactile AEM - IU Coral](/help/sites-developing/touch-ui-concepts.md#coral-ui)
   * [Guide de l’IU Coral](https://developer.adobe.com/experience-manager/reference-materials/6-5/coral-ui/coralui3/index.html)

* IU Granite

   * Fournit le balisage de l’IU Coral encapsulé dans les composants Sling pour la création de consoles d’interface utilisateur et de boîtes de dialogue.
   * [Concepts de l’IU tactile AEM - IU Granite](/help/sites-developing/touch-ui-concepts.md#coral-ui)
   * [Documentation relative à l’interface utilisateur Granite](https://developer.adobe.com/experience-manager/reference-materials/6-5/granite-ui/api/jcr_root/libs/granite/ui/index.html)

>[!NOTE]
>
>En raison de la nature des composants de l’IU Granite (et des différences avec les widgets ExtJS), il existe des différences entre la façon dont les composants interagissent avec l’IU tactile et l’[IU classique](/help/sites-developing/developing-components-classic.md).

### Créer une boîte de dialogue {#creating-a-new-dialog}

Les boîtes de dialogue pour l’interface utilisateur tactile :

* sont nommées `cq:dialog` ;
* sont définies sous forme de nœud `nt:unstructured` avec le jeu de propriétés `sling:resourceType` ;

* sont situées sous leur nœud `cq:Component` et à côté de leur définition de composant ;
* sont rendues côté serveur (en tant que composants Sling), en fonction de la structure de leur contenu et de la propriété `sling:resourceType` ;
* utilisent le framework de l’interface utilisateur Granite ;
* contiennent une structure de nœud décrivant les champs contenus dans la boîte de dialogue.

   * Ces nœuds sont `nt:unstructured` avec la propriété `sling:resourceType` obligatoire.

Un exemple de structure de nœud pourrait être :

```xml
newComponent (cq:Component)
  cq:dialog (nt:unstructured)
    content
      layout
      items
        column
          items
            file
            description
```

La personnalisation d’une boîte de dialogue est similaire au développement d’un composant dans la mesure où la boîte de dialogue est elle-même un composant (c’est-à-dire un balisage rendu par un script de composant avec le comportement/style fourni par une bibliothèque cliente).

Pour consulter des exemples, voir :

* `/libs/foundation/components/text/cq:dialog`
* `/libs/foundation/components/download/cq:dialog`

>[!NOTE]
>
>Si un composant ne possède pas de boîte de dialogue définie pour l’IU tactile, la boîte de dialogue de l’IU classique est utilisée comme solution de secours à l’intérieur d’une couche de compatibilité. Pour personnaliser ce type de boîte de dialogue, vous devez personnaliser la boîte de dialogue de l’IU classique. Consultez [Composants AEM pour l’IU classique](/help/sites-developing/developing-components-classic.md).

### Personnalisation des champs de boîte de dialogue {#customizing-dialog-fields}

>[!NOTE]
>
>Voir :
>
>* la session AEM Gems sur [Personnalisation des champs de boîte de dialogue](https://experienceleague.adobe.com/docs/experience-manager-gems-events/gems/gems2015/aem-customizing-dialog-fields-in-touch-ui.html?lang=fr).
>* l’exemple de code correspondant traité dans [Exemple de code - Comment personnaliser les champs de boîte de dialogue](/help/sites-developing/developing-components-samples.md#code-sample-how-to-customize-dialog-fields).
>

#### Créer un champ {#creating-a-new-field}

Les widgets de l’IU tactile sont implémentés en tant que composants de l’IU Granite.

Pour créer un nouveau widget à utiliser dans une boîte de dialogue de composant pour l’IU tactile, vous devez [créer un composant de champ de l’IU Granite](/help/sites-developing/granite-ui-component.md).

>[!NOTE]
>
>Pour plus d’informations sur l’interface utilisateur Granite, reportez-vous à la [documentation sur l’interface utilisateur Granite](https://developer.adobe.com/experience-manager/reference-materials/6-5/granite-ui/api/jcr_root/libs/granite/ui/index.html).

Si vous configurez votre boîte de dialogue comme un conteneur simple pour un élément de formulaire, vous pouvez également voir le contenu principal du contenu de la boîte de dialogue sous la forme de champs de formulaire. La création d’un champ de formulaire nécessite la création d’un type de ressource. Cela équivaut à créer un composant. Pour vous aider dans cette tâche, l’IU Granite propose un composant de champ générique duquel hériter (en utilisant `sling:resourceSuperType`) :

`/libs/granite/ui/components/coral/foundation/form/field`

Plus précisément, l’IU Granite offre divers composants de champ qui conviennent pour une utilisation dans des boîtes de dialogue (ou, de manière plus générale, dans des [formulaires](https://developer.adobe.com/experience-manager/reference-materials/6-5/granite-ui/api/jcr_root/libs/granite/ui/components/foundation/form/index.html)).

>[!NOTE]
>
>Cela diffère de l’IU classique où les widgets sont représentés par des nœuds `cq:Widgets`, chacun avec un `xtype` particulier pour établir la relation avec le widget ExtJS correspondant. Du point de vue de la mise en œuvre, ces widgets sont rendus côté client par le framework ExtJS.

Une fois que vous avez créé votre type de ressource, vous pouvez instancier le champ en ajoutant un nouveau nœud dans la boîte de dialogue, avec la propriété `sling:resourceType` faisant référence au type de ressource que vous venez d’introduire.

#### Créer une bibliothèque cliente pour le style et le comportement {#creating-a-client-library-for-style-and-behavior}

Si vous souhaitez définir le style et le comportement de votre composant, vous pouvez créer une [bibliothèque cliente](/help/sites-developing/clientlibs.md) qui définit vos CSS/LESS et JS personnalisés.

Afin que la bibliothèque cliente soit chargée uniquement pour votre boîte de dialogue de composant (c’est-à-dire qu’elle ne soit pas chargée pour un autre composant), vous devez définir la propriété **`extraClientlibs`** de la boîte de dialogue sur le nom de catégorie de la bibliothèque cliente que vous venez de créer. Ceci est conseillé si votre bibliothèque cliente est assez volumineuse ou si votre champ est spécifique à cette boîte de dialogue et n’est pas nécessaire dans les autres boîtes de dialogue.

Afin que la bibliothèque cliente soit chargée pour toutes les boîtes de dialogue, définissez la propriété Catégorie de votre bibliothèque cliente sur `cq.authoring.dialog`. Il s’agit du nom de la catégorie de la bibliothèque cliente qui est incluse par défaut lors du rendu de toutes les boîtes de dialogue. Faites-le si votre bibliothèque cliente est petite et/ou si votre champ est générique et peut être réutilisé dans d’autres boîtes de dialogue.

Pour consulter un exemple, reportez-vous à :

* `cqgems/customizingfield/components/colorpicker/clientlibs`

   * fournie par l’[exemple de code](/help/sites-developing/developing-components-samples.md#code-sample-how-to-customize-dialog-fields)

#### Extension (par héritage) d’un champ {#extending-inheriting-from-a-field}

Selon vos besoins, vous pouvez effectuer l’une des opérations suivantes :

* Étendre un champ de l’IU Granite par héritage de composant (`sling:resourceSuperType`)
* Étendez un widget donné à partir de la bibliothèque de widgets sous-jacente (dans le cas de l’UI Granite, il s’agit de l’UI Coral), en suivant l’API de bibliothèque de widgets (héritage JS/CSS).

#### Accès aux champs de boîte de dialogue {#access-to-dialog-fields}

Vous pouvez également utiliser les conditions de rendu (`rendercondition`) pour contrôler qui a accès à des onglets/champs spécifiques dans votre boîte de dialogue. Par exemple :

```xml
+ mybutton
  - sling:resourceType = granite/ui/components/coral/foundation/button
  + rendercondition
    - sling:resourceType = myapp/components/renderconditions/group
    - groups = ["administrators"]
```

### Gestion des événements de champ {#handling-field-events}

La méthode de gestion des événements dans les champs de boîte de dialogue est désormais appliquée avec les [écouteurs d’une bibliothèque cliente personnalisée](#listeners-in-a-custom-client-library). Il s’agit d’un changement par rapport à l’ancienne méthode des [listeners dans la structure de contenu](#listenersinthecontentstructureclassicui).

#### Listeners dans une bibliothèque cliente personnalisée {#listeners-in-a-custom-client-library}

Pour injecter une logique dans votre champ, vous devez :

1. Faites en sorte que votre champ soit marqué d’une classe CSS donnée (le *hook*).
1. Définissez, dans votre bibliothèque client, un listener JS lié à ce nom de classe CSS (cela garantit que votre logique personnalisée ne concerne que votre champ et n’affecte pas d’autres champs du même type).

Pour ce faire, vous devez connaître la bibliothèque de widgets sous-jacente avec laquelle vous souhaitez interagir. Consultez la [documentation relative à l’IU Coral](https://developer.adobe.com/experience-manager/reference-materials/6-5/coral-ui/coralui3/index.html) pour identifier l’événement auquel vous voulez réagir. Cette opération est très similaire au processus que vous deviez effectuer avec ExtJS dans le passé : recherchez la page de documentation d’un widget donné, puis vérifiez les détails de son API d’événement.

Pour consulter un exemple, reportez-vous à :

* `cqgems/customizingfield/components/clientlibs/customizingfield`

   * fournie par l’[exemple de code](/help/sites-developing/developing-components-samples.md#code-sample-how-to-customize-dialog-fields)

#### Listeners dans la structure de contenu {#listeners-in-the-content-structure}

Dans l’IU classique avec ExtJS, il était habituel de trouver des écouteurs pour un widget donné dans la structure de contenu. L’obtention de la même valeur dans l’interface utilisateur tactile est différente, car le code de listener JS (ou tout autre code tout court) n’est plus défini dans le contenu.

La structure du contenu décrit la structure sémantique ; elle ne devrait (doit) pas impliquer la nature du widget sous-jacent. En l’absence de code JS dans la structure du contenu, vous pouvez modifier les détails d’implémentation sans avoir à modifier la structure du contenu. En d’autres termes, vous pouvez modifier la bibliothèque de widgets sans avoir à toucher la structure de contenu.

#### Détection de la disponibilité de la boîte de dialogue {#dialog-ready}

Si vous utilisez un script JavaScript personnalisé qui doit être exécuté uniquement lorsque la boîte de dialogue est disponible et prête, vous devez écouter l’événement `dialog-ready`.

Ce événement est déclenché chaque fois que la boîte de dialogue se charge (ou se recharge) et est prête à l’emploi, soit chaque fois qu’une modification (création ou mise à jour) a lieu dans le DOM de la boîte de dialogue.

`dialog-ready` peut être utilisé pour associer du code personnalisé JavaScript qui effectue des personnalisations dans les champs d’une boîte de dialogue ou pour des tâches similaires.

### Validation de champ {#field-validation}

#### Champ obligatoire {#mandatory-field}

Pour marquer un champ donné comme obligatoire, définissez la propriété suivante sur le nœud de contenu de votre champ :

* Nom : `required`
* Type : `Boolean`

Pour consulter un exemple, reportez-vous à :

```xml
/libs/foundation/components/page/cq:dialog/content/items/tabs/items/basic/items/column/items/title/items/title
```

#### Validation de champ (UI Granite) {#field-validation-granite-ui}

La validation du champ dans l’IU Granite et les composants de l’IU Granite (équivalent aux widgets) est effectuée à l’aide de l’API `foundation-validation`. [Consultez la `foundation-valdiation`documentation de Granite pour plus de détails.](https://developer.adobe.com/experience-manager/reference-materials/6-5/granite-ui/api/jcr_root/libs/granite/ui/components/coral/foundation/clientlibs/foundation/js/validation/index.html)

Pour consulter des exemples, voir :

* `cqgems/customizingfield/components/clientlibs/customizingfield/js/validations.js`

   * fourni par l’[exemple de code](/help/sites-developing/developing-components-samples.md#code-sample-how-to-customize-dialog-fields)

* `/libs/cq/gui/components/authoring/dialog/clientlibs/dialog/js/validations.js`

## Création et configuration d’une boîte de dialogue Conception {#creating-and-configuring-a-design-dialog}

La boîte de dialogue Conception est utilisée lorsqu’un composant possède des détails de conception modifiables en [mode Conception](/help/sites-authoring/default-components-designmode.md).

La définition est très similaire à celle d’une boîte de dialogue[ servant à modifier le contenu](#creating-a-new-dialog), à la différence qu’elle est définie comme un nœud :

* Nom du nœud : `cq:design_dialog`
* Type : `nt:unstructured`

## Création et configuration d’un éditeur intégré {#creating-and-configuring-an-inplace-editor}

Un éditeur local permet à l’utilisateur de modifier le contenu directement dans le flux de paragraphe, sans avoir besoin d’ouvrir une boîte de dialogue. Par exemple, les composants Texte et Titre standard possèdent tous deux un éditeur intégré.

Un éditeur intégré n’est pas nécessaire/déterminant pour chaque type de composant.

Voir [Extension de la création de pages - Ajout d’un nouvel éditeur intégré](/help/sites-developing/customizing-page-authoring-touch.md#add-new-in-place-editor) pour plus d’informations.

## Personnalisation de la barre d’outils de composant {#customizing-the-component-toolbar}

Le [Barre d’outils de composant](/help/sites-developing/touch-ui-structure.md#component-toolbar) permet aux utilisateurs d’accéder à un éventail d’actions pour le composant, telles que la modification, la configuration, la copie et la suppression.

Voir [Extension de la création de page - Ajouter une nouvelle action à une barre d’outils de composant](/help/sites-developing/customizing-page-authoring-touch.md#add-new-action-to-a-component-toolbar) pour plus d’informations.

## Configuration d’un composant pour le rail de références (emprunté/prêté) {#configuring-a-component-for-the-references-rail-borrowed-lent}

Si votre nouveau composant fait référence au contenu d’autres pages, vous pouvez déterminer si vous souhaitez qu’il affecte les sections **Contenu emprunté** et **Contenu prêté** du rail de [**références**](/help/sites-authoring/basic-handling.md#references).

AEM prêt à l’emploi ne vérifie que le composant Référence. Pour ajouter votre composant, vous devez configurer le bundle OSGi **Configuration de référence du contenu de création de gestion de contenu Web**.

Créez une nouvelle entrée dans la définition, en spécifiant votre composant, avec la propriété à vérifier. Par exemple :

`/apps/<*your-Project*>/components/reference@parentPath`

>[!NOTE]
>
>Lorsque vous utilisez AEM, plusieurs méthodes permettent de gérer les paramètres de configuration pour ces services. Consultez [Configuration d’OSGi](/help/sites-deploying/configuring-osgi.md) pour avoir plus de détails et connaître les pratiques recommandées.

## Activation et ajout de votre composant au système de paragraphes {#enabling-and-adding-your-component-to-the-paragraph-system}

Une fois le composant développé, il doit être activé pour être utilisé dans un système de paragraphes approprié, de sorte qu’il puisse être utilisé sur les pages requises.

Pour ce faire, procédez comme suit :

* utilisez le [mode de conception](/help/sites-authoring/default-components-designmode.md) lors de la modification d’une page spécifique.
* [en définissant la propriété `components` sur le système de paragraphe d’un modèle](/help/sites-developing/components-basics.md#adding-your-component-to-the-paragraph-system).

## Configuration d’un système de paragraphes de manière à faire glisser une ressource pour créer une instance de composant {#configuring-a-paragraph-system-so-that-dragging-an-asset-creates-a-component-instance}

AEM offre la possibilité de configurer un système de paragraphes sur votre page afin qu’une[ instance de votre nouveau composant soit automatiquement créée lorsqu’un utilisateur ou une utilisatrice fait glisser une ressource (appropriée) sur une instance de cette page](/help/sites-authoring/editing-content.md#insertingacomponenttouchoptimizedui) (au lieu d’avoir toujours à faire glisser un composant vide sur la page).

Ce comportement, et la relation ressource-à-composant requise, peuvent être configurés :

1. Sous la définition de paragraphe de votre conception de page. Par exemple :

   * `/etc/designs/<myApp>/page/par`

   Créez un nœud :

   * Nom : `cq:authoring`
   * Type : `nt:unstructured`

1. Sous cela, créez un nouveau nœud qui contiendra tous les mappages actif à composant :

   * Nom : `assetToComponentMapping`
   * Type : `nt:unstructured`

1. Pour chaque mappage actif à composant, créez un nœud :

   * Nom : text ; il est recommandé que le nom indique l’actif et le type de composant associé, par exemple, « image ».
   * Type : `nt:unstructured`

   Chacun possédant les propriétés suivantes :

   * `assetGroup` :

      * Type : `String`
      * Valeur : groupe auquel l’actif associé appartient, par exemple, `media`

   * `assetMimetype` :

      * Type : `String`
      * Valeur : type mime de l’actif associé, par exemple `image/*`

   * `droptarget` :

      * Type : `String`
      * Valeur : cible de dépôt, par exemple, `image`

   * `resourceType` :

      * Type : `String`
      * Valeur : ressource de composant associée, par exemple, `foundation/components/image`

   * `type` :

      * Type : `String`
      * Valeur : type, par exemple, `Images`

Pour voir des exemples, reportez-vous à :

* `/etc/designs/geometrixx/jcr:content/page/par/cq:authoring`
* `/etc/designs/geometrixx-outdoors/jcr:content/page/par/cq:authoring`
* `/etc/designs/geometrixx-media/jcr:content/article/article-content-par/cq:authoring`

CODE SUR GITHUB

Vous pouvez trouver le code de cette page sur GitHub.

* [Ouvrez le projet aem-project-archetype sur GitHub](https://github.com/adobe/aem-project-archetype).
* Téléchargez le projet sous la forme d’[un fichier ZIP](https://github.com/adobe/aem-project-archetype/archive/master.zip).

>[!NOTE]
>
>La création automatique d’instances de composant est désormais facile à configurer dans l’interface utilisateur lors de l’utilisation de [composants de base](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=fr) et de modèles modifiables. Consultez [Création de modèles de page](/help/sites-authoring/templates.md#editing-a-template-structure-template-author) pour plus d’informations sur la définition des composants automatiquement associés à des types de média donnés.

## Utilisation de l’extension AEM Brackets {#using-the-aem-brackets-extension}

L’[extension AEM Brackets](/help/sites-developing/aem-brackets.md) fournit un workflow fluide pour modifier les composants AEM et les bibliothèques clientes. Elle se base sur l’éditeur de code [Brackets](https://brackets.io/).

L’extension :

* Facilite la synchronisation (aucun Maven ou File Vault requis) pour améliorer le rendement des développeurs et permet également aux développeurs de front-end ayant des connaissances limitées en matière d’AEM de participer à des projets.
* Fournit une prise en charge d’[HTL](https://experienceleague.adobe.com/docs/experience-manager-htl/using/overview.html?lang=fr), le langage de modèle conçu pour simplifier le développement des composants et renforcer la sécurité.

>[!NOTE]
>
>Brackets est le mécanisme recommandé pour créer des composants. Il remplace la fonctionnalité CRXDE Lite - Créer un composant, qui a été conçue pour l’interface utilisateur classique.

## Migration à partir d’un composant classique {#migrating-from-a-classic-component}

Lors de la migration d’un composant de l’IU classique vers un composant pouvant être utilisé avec l’IU tactile (exclusivement ou conjointement), les problèmes suivants doivent être anticipés : 

* HTL

   * L’utilisation d’[HTL](https://experienceleague.adobe.com/docs/experience-manager-htl/using/overview.html?lang=fr) n’est pas obligatoire, mais si le composant doit être mis à jour, c’est l’occasion idéale pour envisager une [migration de JSP vers HTL](/help/sites-developing/components-basics.md#htl-vs-jsp).

* Les composants :

   * migrent le code [`cq:listener`](/help/sites-developing/developing-components.md#migrating-cq-listener-code)  qui utilise des fonctions spécifiques à l’IU classique ;
   * Plugin RTE. Pour plus d’informations, consultez [Configuration de l’éditeur de texte enrichi](/help/sites-administering/rich-text-editor.md) ;
   * [migrent le code `cq:listener`](#migrating-cq-listener-code) qui utilise des fonctions spécifiques à l’IU classique.

* Boîtes de dialogue

   * Créez une boîte de dialogue à utiliser dans l’interface utilisateur tactile. Pour des raisons de compatibilité, l’IU tactile peut utiliser la définition d’une boîte de dialogue d’IU classique, si aucune boîte de dialogue n’a été définie pour l’IU tactile.
   * Les [Outils de modernisation d’AEM](/help/sites-developing/modernization-tools.md) sont fournis pour vous aider à étendre les composants existants.
   * Le [mappage d’ExtJS aux composants de l’IU Granite](/help/sites-developing/touch-ui-concepts.md#extjs-and-corresponding-granite-ui-components) fournit une présentation pratique des xtypes ExtJS et des types de nœud avec les types de ressources équivalents dans l’IU Granite.
   * Personnalisation des champs ; pour plus d’informations, consultez la session AEM Gems sur la [Personnalisation des champs de boîte de dialogue](https://experienceleague.adobe.com/docs/experience-manager-gems-events/gems/gems2015/aem-customizing-dialog-fields-in-touch-ui.html?lang=fr).
   * Migration des types vers la [Validation de l’interface utilisateur Granite](https://developer.adobe.com/experience-manager/reference-materials/6-5/granite-ui/api/jcr_root/libs/granite/ui/components/foundation/clientlibs/foundation/js/validation/index.html)
   * Utilisation des listeners JS ; pour plus d’informations, voir [Gestion des événements de champ](#handling-field-events) et la session AEM Gems sur la [Personnalisation des champs de boîte de dialogue](https://experienceleague.adobe.com/docs/experience-manager-gems-events/gems/gems2015/aem-customizing-dialog-fields-in-touch-ui.html?lang=fr).

### Migration du code cq:listener {#migrating-cq-listener-code}

Si vous migrez un projet conçu pour l’IU classique, le code `cq:listener` (et les bibliothèques clientes associées aux composants) peut utiliser des fonctions spécifiques à l’IU classique (telles que `CQ.wcm.*`). Pour la migration, vous devez mettre à jour ce code en utilisant les objets/fonctions équivalents dans l’IU tactile.

Si votre projet est complètement migré vers l’interface utilisateur tactile, vous devez remplacer ce code pour utiliser les objets et fonctions appropriés à l’interface utilisateur tactile.

Cependant, si votre projet doit prendre en charge à la fois l’interface utilisateur classique et l’interface utilisateur tactile pendant la période de migration (scénario habituel), vous devez implémenter un système de basculement pour différencier le code distinct référençant les objets appropriés.

Ce mécanisme de basculement peut être implémenté comme suit :

```
if (Granite.author) {
    // touch UI
} else {
    // classic UI
}
```

## Documentation de votre composant {#documenting-your-component}

En tant que développeur ou développeuse, vous aimez accéder facilement à la documentation d’un composant afin de pouvoir comprendre rapidement :

* sa description ;
* son utilisation prévue ;
* la structure et les propriétés du contenu
* les API exposées et les points d’extension
* et ainsi de suite

Pour cette raison, il est facile de rendre tout markdown de documentation existant disponible dans le composant lui-même.

Placez un fichier `README.md` dans la structure du composant. Ce markdown s’affiche dans la [console du composant](/help/sites-authoring/default-components-console.md).

![chlimage_1-7](assets/chlimage_1-7.png)

Le MarkDown pris en charge est le même que pour les [fragments de contenu](/help/assets/content-fragments/content-fragments-markdown.md).
