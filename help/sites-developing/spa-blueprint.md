---
title: Plan directeur d’applications sur une seule page (SPA)
seo-title: Plan directeur d’applications sur une seule page (SPA)
description: Ce document décrit le contrat général et indépendant de la structure que tout cadre SPA devrait respecter pour mettre en oeuvre des composants SPA modifiables au sein de l'AEM.
seo-description: Ce document décrit le contrat général et indépendant de la structure que tout cadre SPA devrait respecter pour mettre en oeuvre des composants SPA modifiables au sein de l'AEM.
uuid: 48f2d415-ec34-49dc-a8e1-6feb5a8a5bbe
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: spa
content-type: reference
discoiquuid: 04ac8203-320b-4671-aaad-6e1397b12b6f
docset: aem65
translation-type: tm+mt
source-git-commit: 4c9a0bd73e8d87d3869c6a133f5d1049f8430cd1
workflow-type: tm+mt
source-wordcount: '2112'
ht-degree: 13%

---


# Plan directeur d’applications sur une seule page (SPA){#spa-blueprint}

Pour permettre à l’auteur d’utiliser l’AEM SPA Editor pour modifier le contenu d’un SPA, le  doit respecter certaines exigences, qui sont décrites dans ce document.

>[!NOTE]
>
>L’éditeur SPA est la solution recommandée pour les projets qui nécessitent un rendu côté client SPA structure (par exemple, Réagir ou Angulaire).

## Présentation {#introduction}

Ce document décrit le contrat général que tout cadre SPA doit respecter (c&#39;est-à-dire le type de couche de support AEM) pour mettre en oeuvre des composants de SPA modifiables dans l&#39;.

>[!NOTE]
>
>Les exigences suivantes sont indépendantes de la structure. Si ces exigences sont satisfaites, un calque spécifique à l’infrastructure, constitué de modules, de composants et de services, peut être fourni.
>
>**Ces exigences sont déjà satisfaites pour les cadres Réagir et Angular en AEM.** Les exigences de ce plan directeur ne sont pertinentes que si vous souhaitez mettre en oeuvre un autre cadre à utiliser avec AEM.

>[!CAUTION]
>
>Bien que les capacités SPA de AEM soient indépendantes de la structure, seules les structures React et Angular sont actuellement prises en charge.

Pour permettre à l’auteur d’utiliser l’Éditeur de page AEM pour modifier les données exposées par une structure d’application d’une seule page, un projet doit être en mesure d’interpréter la structure du modèle représentant la sémantique des données stockées pour une application dans le référentiel AEM. Pour atteindre cet objectif, deux bibliothèques indépendantes du cadre sont fournies : le `PageModelManager` et le `ComponentMapping`.

### PageModelManager {#pagemodelmanager}

La `PageModelManager` bibliothèque est fournie sous la forme d&#39;un module de gestion de réseau à utiliser par un projet SPA. Il accompagne l’application sur une seule page et fait office de gestionnaire de modèles de données.

Au nom de l’application sur une seule page, il extrait la récupération et la gestion de la structure JSON qui représente la structure de contenu proprement dite. Il est également responsable de la synchronisation avec le SPA pour lui indiquer quand il doit rendre à nouveau ses composants.

Voir le package NPM [@adobe/aem-spa-page-model-manager](https://www.npmjs.com/package/@adobe/aem-spa-page-model-manager)

Lors de l’initialisation de l’application `PageModelManager`, la bibliothèque charge d’abord le modèle racine fourni de l’application (par l’intermédiaire d’un paramètre, d’une propriété meta ou de l’URL active). Si la bibliothèque identifie que le modèle de la page active ne fait pas partie du modèle racine qu’elle récupère et l’inclut comme modèle de page enfant.

![page_model_consolidation](assets/page_model_consolidation.png)

### ComponentMapping {#componentmapping}

The `ComponentMapping` module is provided as an NPM package to the front-end project. Il stocke les composants frontaux et permet aux SPA de mapper les composants frontaux aux types de ressources AEM. Ceci active une résolution dynamique des composants lors de l’analyse du modèle JSON de l’application.

Chaque élément présent dans le modèle contient un `:type` champ qui expose un type de ressource AEM. Une fois monté, le composant frontal peut être rendu à l’aide du fragment de modèle reçu des bibliothèques sous-jacentes.

#### Mappage du modèle dynamique au composant {#dynamic-model-to-component-mapping}

Pour plus d’informations sur la façon dont le mappage du modèle dynamique au composant se produit dans le SDK SPA JavaScript pour AEM, reportez-vous à l’article Modèle [dynamique vers mappage de composants pour SPA](/help/sites-developing/spa-dynamic-model-to-component-mapping.md).

### Couche spécifique au cadre {#framework-specific-layer}

Une troisième couche doit être mise en oeuvre pour chaque structure frontale. Cette troisième bibliothèque est chargée d&#39;interagir avec les bibliothèques sous-jacentes et de fournir une série de points d&#39;entrée bien intégrés et faciles à utiliser pour interagir avec le modèle de données.

Le reste de ce document décrit les exigences de cette couche spécifique de cadre intermédiaire et aspire à être indépendante du cadre. En respectant les exigences suivantes, une couche spécifique au cadre peut être fournie pour que les composants du projet interagissent avec les bibliothèques sous-jacentes chargées de la gestion du modèle de données.

## Concepts généraux {#general-concepts}

### Modèle de page {#page-model}

La structure de contenu de la page est stockée dans AEM. Le modèle de la page est utilisé pour mapper et instancier les composants de l’application d’une seule page (SPA). Les développeurs d’applications d’une seule page créent des composants SPA qu’ils mappent sur des composants AEM. Pour ce faire, ils utilisent le type de ressource (ou le chemin d&#39;accès au composant AEM) comme clé unique.

Les composants SPA doivent être synchronisés avec le modèle de page et être mis à jour en fonction des modifications apportées au contenu. Un modèle qui a recours à des composants dynamiques doit être utilisé pour instancier des composants à la volée, suivant la structure de modèle de page fournie.

### Champs Meta {#meta-fields}

The page model leverages the JSON Model Exporter, which is itself based on the [Sling Model](https://sling.apache.org/documentation/bundles/models.html) API. Les modèles sling exportables exposent la liste de champs suivante afin de permettre aux bibliothèques sous-jacentes d’interpréter le modèle de données :

* `:type`: Type de la ressource AEM (par défaut = type de ressource)
* `:children`: Enfants hiérarchiques de la ressource actuelle. Les enfants ne font pas partie du contenu interne de la ressource actuelle (se trouvent sur les éléments représentant une page)
* `:hierarchyType`: Type hiérarchique d&#39;une ressource. Actuellement, le type de page `PageModelManager` est pris en charge

* `:items`: Ressources de contenu enfant de la ressource actuelle (structure imbriquée, présente uniquement sur les conteneurs)
* `:itemsOrder`: Liste ordonnée des enfants. L’objet de mappage JSON ne garantit pas l’ordre de ses champs. En disposant à la fois de la carte et de la baie actuelle, le consommateur de l&#39;API bénéficie des avantages des deux structures.
* `:path`: Chemin d’accès au contenu d’un élément (présent sur les éléments représentant une page)

Voir aussi [Prise en main d’AEM Content Services](https://helpx.adobe.com/fr/experience-manager/kt/sites/using/content-services-tutorial-use.html).

### Module spécifique au cadre {#framework-specific-module}

La séparation des préoccupations aide à faciliter la mise en oeuvre du projet. Par conséquent, un package spécifique au régime npm devrait être fourni. Ce package est chargé d’agréger et d’exposer les modules, services et composants de base. Ces composants doivent encapsuler la logique de gestion des modèles de données et fournir un accès aux données attendues par le composant du projet. Le module est également chargé d&#39;exposer de façon transitoire les points d&#39;entrée utiles des bibliothèques sous-jacentes.

Pour faciliter l&#39;interopérabilité des bibliothèques, l&#39;Adobe conseille au module spécifique au cadre de regrouper les bibliothèques suivantes. Si nécessaire, la couche peut encapsuler et adapter les API sous-jacentes avant de les exposer au projet.

* [@adobe/aem-spa-page-model-manager](https://www.npmjs.com/package/@adobe/aem-spa-page-model-manager)
* [@adobe/aem-spa-component-mapping](https://www.npmjs.com/package/@adobe/aem-spa-component-mapping)

#### Mises en œuvre {#implementations}

#### Réagir {#react}

module npm : [@adobe/aem-response-editable-components](https://www.npmjs.com/package/@adobe/aem-react-editable-components)

#### Angular {#angular}

module npm : à venir

## Services principaux et composants {#main-services-and-components}

Les entités suivantes devraient être mises en oeuvre conformément aux lignes directrices spécifiques à chaque cadre. En fonction de l&#39;architecture du cadre, la mise en oeuvre peut varier considérablement, mais les fonctionnalités décrites doivent être fournies.

### Fournisseur de modèles {#the-model-provider}

Les composants du projet doivent déléguer l&#39;accès aux fragments d&#39;un modèle à un fournisseur de modèles. Le fournisseur de modèles est alors chargé d&#39;écouter les modifications apportées au fragment spécifié du modèle et de renvoyer le modèle mis à jour au composant délégué.

Pour ce faire, le Fournisseur de modèles doit s&#39;inscrire au ` [PageModelManager](/help/sites-developing/spa-blueprint.md#pagemodelmanager)`. Ensuite, lorsqu’une modification se produit, elle reçoit et transmet les données mises à jour au composant de délégation. Par convention, la propriété mise à la disposition du composant de délégation qui transportera le fragment de modèle est nommée `cqModel`. L’implémentation est libre de fournir cette propriété au composant mais doit prendre en compte des aspects tels que l’intégration à l’architecture de la structure, la découverte et la facilité d’utilisation.

### Le décorateur HTML du composant {#the-component-html-decorator}

Le décorateur de composants est chargé de décorer le code HTML extérieur de l’élément de chaque instance de composant avec une série d’attributs de données et de noms de classe attendus par l’éditeur de page.

#### Déclaration des composants {#component-declaration}

Les métadonnées suivantes doivent être ajoutées à l&#39;élément HTML externe produit par le composant du projet. Ils permettent à l’éditeur de page de récupérer la configuration de modification correspondante.

* `data-cq-data-path`: Chemin d’accès à la ressource relative à la variable `jcr:content`

#### Modification de la déclaration de capacité et de l’espace réservé {#editing-capability-declaration-and-placeholder}

Les métadonnées et les noms de classe suivants doivent être ajoutés à l&#39;élément HTML externe produit par le composant du projet. Ils permettent à l’éditeur de page d’accéder aux fonctionnalités liées à l’offre.

* `cq-placeholder`: Nom de classe qui identifie l&#39;espace réservé pour un composant vide
* `data-emptytext`: Libellé à afficher par l’incrustation lorsqu’une instance de composant est vide

**Espace réservé pour les composants vides**

Chaque composant doit être étendu avec une fonctionnalité qui décorera l’élément HTML externe avec des attributs de données et des noms de classe spécifiques aux espaces réservés et aux incrustations connexes lorsque le composant est identifié comme vide.

**A propos de l&#39;état vide d&#39;un composant**

* Le composant est-il logiquement vide ?
* Quel doit être l’étiquette affichée par l’incrustation lorsque le composant est vide ?

### Conteneur {#container}

Un conteneur est un composant conçu pour contenir des composants enfants et en effectuer le rendu. Pour ce faire, le conteneur effectue une itération sur les propriétés `:itemsOrder`, `:items` et `:children` des propriétés de son modèle.

Le conteneur obtient dynamiquement les composants enfants à partir du magasin de la ` [ComponentMapping](/help/sites-developing/spa-blueprint.md#componentmapping)` bibliothèque. Le conteneur étend ensuite le composant enfant avec les fonctionnalités du fournisseur de modèles et l&#39;instancie finalement.

### Page  {#page}

Le `Page` composant étend le `Container` composant. Un conteneur est un composant destiné à contenir et à générer des composants enfants, y compris des pages enfants. Pour ce faire, le conteneur effectue une itération sur les propriétés `:itemsOrder`, `:items`et `:children` des propriétés de son modèle. Le `Page` composant obtient dynamiquement les composants enfants à partir du magasin de la bibliothèque [ComponentMapping](/help/sites-developing/spa-blueprint.md#componentmapping) . Il `Page` est responsable de l’instanciation des composants enfants.

### Grille réactive {#responsive-grid}

Le composant Grille réactive est un conteneur. Il contient une variante spécifique du fournisseur de modèles représentant ses colonnes. La grille réactive et ses colonnes sont chargées de décorer l&#39;élément HTML externe du composant du projet avec les noms de classe spécifiques contenus dans le modèle.

Le composant de grille réactive doit être prémappé à son homologue AEM car ce composant est complexe et rarement personnalisé.

#### Champs de modèle spécifiques {#specific-model-fields}

* `gridClassNames:` Noms de classe fournis pour la grille dynamique
* `columnClassNames:` Noms de classe fournis pour la colonne réactive

Voir aussi la ressource npm [@adobe/aem-response-editable-components#srccomponentsreponvegridjsx](https://www.npmjs.com/package/@adobe/aem-react-editable-components#srccomponentsresponsivegridjsx)

#### Espace réservé de la grille réactive {#placeholder-of-the-reponsive-grid}

Le composant SPA est mappé à un conteneur graphique tel que la grille réactive et doit ajouter un espace réservé enfant virtuel lors de la création du contenu. When the content of the SPA is being authored by the Page Editor, that content is embedded into the editor using an iframe and the `data-cq-editor` attribute is added to the document node of that content. Lorsque l’ `data-cq-editor` attribut est présent, le conteneur doit inclure un HTMLElement pour représenter la zone avec laquelle l’auteur interagit lors de l’insertion d’un nouveau composant dans la page.

Par exemple :

```
<div data-cq-data-path={"path/to/the/responsivegrid/*"} className="new section aem-Grid-newComponent"/>
```

>[!NOTE]
>
>Les noms de classe utilisés dans l’exemple sont actuellement requis par l’éditeur de page.
>
>* `"new section"` : indique que l’élément en cours est l’espace réservé du conteneur.
>* `"aem-Grid-newComponent"`: Normalise le composant pour la création de mise en page.

>



#### Mappage de composant {#component-mapping}

La [`Component Mapping`](/help/sites-developing/spa-blueprint.md#componentmapping) bibliothèque sous-jacente et sa `MapTo` fonction peuvent être encapsulées et étendues afin de fournir les fonctionnalités relatives à la configuration d&#39;édition fournie avec la classe de composants actuelle.

```
const EditConfig = {

    emptyLabel: 'My Component',

    isEmpty: function() {
        return !this.props || !this.props.cqModel || this.props.cqModel.isEmpty;
    }
};

class MyComponent extends Component {

    render() {
        return <div className={'my-component'}></div>;
    }
}

MapTo('component/resource/path')(MyComponent, EditConfig);
```

Dans l’implémentation ci-dessus, le composant de projet est étendu avec la fonctionnalité de vide avant d’être réellement enregistré dans le magasin de mappage [des](/help/sites-developing/spa-blueprint.md#componentmapping) composants. Pour ce faire, encapsulez et étendez la [`ComponentMapping`](/help/sites-developing/spa-blueprint.md#componentmapping) bibliothèque afin d’introduire la prise en charge de l’objet `EditConfig` de configuration :

```
/**
 * Configuration object in charge of providing the necessary data expected by the page editor to initiate the authoring. The provided data will be decorating the associated component
 *
 * @typedef {{}} EditConfig
 * @property {String} [dragDropName]       If defined, adds a specific class name enabling the drag and drop functionality
 * @property {String} emptyLabel           Label to be displayed by the placeholder when the component is empty. Optionally returns an empty text value
 * @property {function} isEmpty            Should the component be considered empty. The function is called using the context of the wrapper component giving you access to the component model
 */

/**
 * Map a React component with the given resource types. If an {@link EditConfig} is provided the <i>clazz</i> is wrapped to provide edition capabilities on the AEM Page Editor
 *
 * @param {string[]} resourceTypes                      - List of resource types for which to use the given <i>clazz</i>
 * @param {class} clazz                                 - Class to be instantiated for the given resource types
 * @param {EditConfig} [editConfig]                     - Configuration object for enabling the edition capabilities
 * @returns {class}                                     - The resulting decorated Class
 */
ComponentMapping.map = function map (resourceTypes, clazz, editConfig) {};
```

## Contrat avec l’éditeur de page {#contract-with-the-page-editor}

Les composants du projet doivent générer au minimum les attributs de données suivants pour permettre à l’éditeur d’interagir avec eux.

* `data-cq-data-path`: Chemin relatif du composant tel que fourni par le `PageModel` (p. ex. `"root/responsivegrid/image"`). Cet attribut ne doit pas être ajouté aux pages.

En résumé, pour être interprété par l’éditeur de page comme modifiable, un composant de projet doit respecter le contrat suivant :

* Fournissez les attributs attendus pour associer une instance de composant frontal à une ressource AEM.
* Fournissez la série attendue d&#39;attributs et de noms de classe qui permet la création d&#39;espaces réservés vides.
* Fournissez les noms de classe attendus permettant le glisser-déposer des ressources.

### Structure d’élément HTML standard {#typical-html-element-structure}

Le fragment suivant illustre la représentation HTML type d’une structure de contenu de page. Voici quelques points importants :

* L’élément de grille réactive contient les noms de classe, précédés de `aem-Grid--`
* The responsive column element carries class names prefixed with `aem-GridColumn--`
* Une grille réactive qui est également la colonne d’une grille parent est encapsulée, de sorte que les deux préfixes précédents n’apparaissent pas sur le même élément.
* Elements corresponding to editable resources carry a `data-cq-data-path` property. Consultez la section [Contrat avec l&#39;éditeur](#contract-wtih-the-page-editor) de page de ce document.

```
<div data-cq-data-path="/content/page">
    <div class="aem-Grid aem-Grid--12 aem-Grid--default--12">
        <div class="aem-container aem-GridColumn aem-GridColumn--default--12" data-cq-data-path="/content/page/jcr:content/root/responsivegrid">
            <div class="aem-Grid aem-Grid--12 aem-Grid--default--12">
                <div class="cmp-image cq-dd-image aem-GridColumn aem-GridColumn--default--12" data-cq-data-path="/root/responsivegrid/image">
                    <img src="/content/we-retail-spa-sample/react/jcr%3acontent/root/responsivegrid/image.img.jpeg/1512113734019.jpeg">
                </div>
            </div>
        </div>
    </div>
</div>
```

## Navigation et Routage {#navigation-and-routing}

L’application est propriétaire du routage. Le développeur principal doit d’abord implémenter un composant Navigation (mappé à un composant de navigation AEM). Ce composant rendrait les liens URL à utiliser conjointement avec une série d&#39;itinéraires qui afficheront ou masqueront des fragments de contenu.

La [`PageModelManager`](/help/sites-developing/spa-blueprint.md#pagemodelmanager) bibliothèque sous-jacente et son ` [ModelRouter](/help/sites-developing/spa-routing.md)` module (activé par défaut) sont responsables de la prérécupération et de l&#39;accès au modèle associé à un chemin de ressource donné.

Les deux entités se rapportent à la notion de routage, mais le ` [ModelRouter](/help/sites-developing/spa-routing.md)` seul responsable du ` [PageModelManager](/help/sites-developing/spa-blueprint.md#pagemodelmanager)` chargement avec un modèle de données structuré en synchronisation avec l&#39;état actuel de l&#39;application.

Consultez l&#39;article [SPA Routage](/help/sites-developing/spa-routing.md) modèle pour plus d&#39;informations.

## SPA en action {#spa-in-action}

Découvrez le fonctionnement d’une application sur une seule page simple et exercez-vous avec une application de ce type en consultant le document [Prise en main des applications sur une seule page dans AEM](/help/sites-developing/spa-getting-started-react.md).

## Informations complémentaires {#further-reading}

Pour plus d’informations sur les applications sur une seule page dans AEM, consultez les documents suivants :

* [Présentation de la création d’applications sur une seule page](/help/sites-developing/spa-overview.md) pour un aperçu de ces applications dans AEM et le modèle de communication
* [Prise en main des applications sur une seule page dans AEM](/help/sites-developing/spa-getting-started-react.md) pour obtenir une description d’une application SPA simple et de son fonctionnement
