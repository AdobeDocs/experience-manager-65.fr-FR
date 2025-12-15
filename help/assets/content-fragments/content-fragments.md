---
title: Utilisation de fragments de contenu
description: Découvrez comment les fragments de contenu dans Adobe Experience Manager (AEM) vous permettent de concevoir, de créer, d’organiser et d’utiliser du contenu indépendant des pages de façon idéale pour une diffusion découplée.
feature: Content Fragments
role: User
exl-id: 0ee883c5-0cea-46b7-a759-600b8ea3bc3e
solution: Experience Manager, Experience Manager Assets
source-git-commit: 73ec9a0420206ef2cc60a12d316073a443c1d20d
workflow-type: tm+mt
source-wordcount: '2329'
ht-degree: 85%

---

# Utilisation de fragments de contenu {#working-with-content-fragments}

Les fragments de contenu d’Adobe Experience Manager (AEM) vous permettent de concevoir, de créer, d’organiser et de [publier du contenu indépendant des pages](/help/sites-authoring/content-fragments.md). Ils vous permettent de préparer le contenu prêt à être utilisé à plusieurs emplacements/sur plusieurs canaux, ce qui est idéal pour une diffusion découplée.

Les fragments de contenu contiennent du contenu structuré :

* Ils sont basés sur un [modèle de fragment de contenu](/help/assets/content-fragments/content-fragments-models.md), servant à prédéfinir une structure pour le fragment résultant.
* La structure peut varier entre :
   * De base
      * Par exemple, un seul champ de texte multilignes.
      * Utilisée pour préparer du contenu simple à utiliser pour la création de pages.
   * Complexe
      * Combinaison de nombreux champs de divers types de données, y compris texte, nombre, booléen, données et temps.
      * Utilisée soit pour la préparation de contenu plus structuré pour la création de pages, soit pour la diffusion à votre application.
   * Imbriqué
      * Les types de données de référence disponibles vous permettent d’imbriquer votre contenu.
      * Tend à être utilisé pour la diffusion à votre application.

Les fragments de contenu peuvent également être diffusés au format JSON, à l’aide des fonctionnalités d’exportation du modèle Sling (JSON) des composants principaux d’AEM. Cette forme de diffusion :

* permet d’utiliser le composant pour gérer les éléments d’un fragment à diffuser
* permet la diffusion en masse, en ajoutant plusieurs composants principaux de fragments de contenu sur la page utilisée pour la diffusion de l’API

Cette page et les suivantes portent sur les tâches de création, de configuration, de gestion et d’utilisation de vos fragments de contenu :

* [Activation de la fonctionnalité de fragments de contenu pour votre instance](/help/assets/content-fragments/content-fragments-configuration-browser.md)
* [Modèles de fragment de contenu](/help/assets/content-fragments/content-fragments-models.md) : activation, création et définition de vos modèles.
* [Gérer les fragments de contenu](/help/assets/content-fragments/content-fragments-managing.md) - créer vos fragments de contenu ; puis modifier, publier et référencer
* [Variations – création de fragments de contenu](/help/assets/content-fragments/content-fragments-variations.md) : créez le contenu du fragment et créez des variantes du maître.
* [Texte (Markdown)](/help/assets/content-fragments/content-fragments-markdown.md) : utilisation de la syntaxe Markdown pour votre fragment.
* [Utilisation du contenu associé](/help/assets/content-fragments/content-fragments-assoc-content.md) : ajout de contenu associé.
* [Métadonnées – propriétés des fragments](/help/assets/content-fragments/content-fragments-metadata.md) : affichage et modification des propriétés des fragments.
* Utilisez [Fragments de contenu, ainsi que GraphQL, pour diffuser du contenu](/help/assets/content-fragments/content-fragments-graphql.md) à utiliser dans vos applications. Pour vous aider, vous pouvez prévisualiser la [sortie JSON](/help/assets/content-fragments/content-fragments-json-preview.md).

>[!NOTE]
>
>Ces pages peuvent être lues avec :
>
>* [Création de page à partir de fragments de contenu](/help/sites-authoring/content-fragments.md).
>* [Personnalisation et extensions de fragments de contenu](/help/sites-developing/customizing-content-fragments.md)
>* [Fragments de contenu – Configuration des composants pour le rendu](/help/sites-developing/content-fragments-config-components-rendering.md)
>* [Prise en charge des fragments de contenu dans l’API HTTP AEM Assets](/help/assets/assets-api-content-fragments.md)
>* [API AEM GraphQL à utiliser avec les fragments de contenu](/help/sites-developing/headless/graphql-api/graphql-api-content-fragments.md)

Le nombre de canaux de communication augmente tous les ans. En règle générale, les canaux font référence au mécanisme de diffusion :

* Canal physique (par exemple, bureau ou mobile).
* Forme de diffusion dans un canal physique (par exemple, la « page de détails du produit », la « page de catégorie de produit » pour le bureau, ou le « web mobile » et « l’application mobile » pour le mobile).

Cependant, vous ne souhaitez (probablement) pas utiliser le même contenu pour tous les canaux ; vous devez optimiser votre contenu en fonction du canal spécifique.

Les fragments de contenu vous permettent d’effectuer les actions suivantes :

* Étudier comment atteindre efficacement les audiences cibles sur plusieurs canaux.
* Créer et gérer du contenu éditorial neutre pour les canaux.
* Créer des pools de contenu pour divers canaux.
* Concevoir des variations de contenu pour des canaux spécifiques.
* Ajouter des images à votre texte en insérant des ressources (fragments de supports variés).
* Créer du contenu imbriqué pour refléter la complexité de vos données.

Ces fragments de contenu peuvent ensuite être assemblés pour offrir diverses expériences sur de multiples canaux.

>[!NOTE]
>
>Les **fragments de contenu** et les **[fragments d’expérience](/help/sites-authoring/experience-fragments.md)** représentent deux fonctions distinctes d’AEM :
>
>* Les **fragments de contenu** sont du contenu éditorial, qui peut être utilisé pour accéder à des données structurées, y compris du texte, des chiffres et des dates. Il s’agit d’un contenu pur, avec définition et structure, mais sans conception visuelle et/ou mise en page supplémentaires.
>
>* Les **fragments d’expérience** désignent un contenu parfaitement mis en page : un fragment de page web.
>
>Les fragments d’expérience peuvent être composés de contenu sous la forme de fragments de contenu, mais pas l’inverse.
>
>Pour plus d’informations, voir [Présentation des fragments de contenu et des fragments d’expérience dans AEM](https://experienceleague.adobe.com/docs/experience-manager-learn/sites/content-fragments/understand-content-fragments-and-experience-fragments.html?lang=fr#content-fragments).

>[!NOTE]
>
>Avant la version 6.3 d’AEM, les fragments de contenu étaient créés à l’aide de modèles différents. Les modèles antérieurs à la version 6.3 d’AEM ne sont plus disponibles pour la création de fragments, mais tous les fragments créés avec ces modèles sont toujours pris en charge.

## Fragments de contenu et Content Services {#content-fragments-and-content-services}

AEM Content Services est conçu pour généraliser la description et la diffusion de contenu dans/à partir d’AEM à des canaux autres que des pages web.

Il assure la diffusion du contenu aux canaux autres que les pages web AEM classiques, à l’aide de méthodes normalisées qui peuvent être utilisées par tous les clients. Ces canaux peuvent inclure :

* des applications sur une seule page ;
* des applications mobiles natives ;
* d’autres canaux et points de contact externes à AEM.

La diffusion est effectuée au format JSON à l’aide de l’outil d’exportation JSON.

Les fragments de contenu AEM peuvent être utilisés pour décrire et gérer du contenu structuré. Le contenu structuré est défini dans des modèles qui peuvent contenir divers types de contenu : texte, données numériques, valeur booléenne, date et heure, etc.

Associé aux fonctionnalités d’exportation JSON des composants principaux AEM, ce contenu structuré peut ensuite être utilisé pour livrer le contenu AEM à des canaux autres que les pages AEM.

<!--
>[!NOTE]
>
>See [Headless and AEM](/help/implementing/developing/headless/introduction.md) for an introduction to Headless Development for AEM Sites.
-->

>[!NOTE]
>
>AEM prend également en charge la traduction des fragments de contenu.

<!--
>[!NOTE]
>
>AEM also supports the translation of fragment content. See [Translating Assets](/help/assets/translate-assets.md) for further information.
-->

## Type de contenu {#content-type}

Les fragments de contenu sont :

* stockés en tant que **ressources** :

   * Les fragments de contenu (et leurs variations) peuvent être créés et conservés à partir de la console **Ressources**.
   * Créés et modifiés dans l’éditeur de fragment de contenu.

* Utilisés dans l’[éditeur de page avec le composant Fragment de contenu](/help/sites-authoring/content-fragments.md) (qui fait référence au composant) :

   * Le composant **Fragment de contenu** est disponible pour les créateurs de pages. Il leur permet de référencer et de livrer le fragment de contenu requis au format HTML ou JSON.

* Accessible à l’aide de l’[API AEM GraphQL](/help/sites-developing/headless/graphql-api/graphql-api-content-fragments.md).

Les fragments de contenu sont une structure de contenu qui :

* Ne comportent pas de disposition ou de conception (certaines mises en forme de texte sont possibles en mode Texte enrichi).
* Contiennent une ou plusieurs [parties constituantes](#constituent-parts-of-a-content-fragment).
* Peuvent [contenir des images ou être connectés à celles-ci](#fragments-with-visual-assets).
* peut utiliser du [contenu intermédiaire](#in-between-content-when-page-authoring-with-content-fragments) en cas de référencement sur une page ;
* Sont indépendants du mécanisme de diffusion (c’est-à-dire de la page ou du canal).

### Fragments avec des ressources visuelles {#fragments-with-visual-assets}

Pour donner aux auteurs et autrices plus de contrôle sur leur contenu, il est possible d’ajouter et/ou d’intégrer des images à un fragment de contenu.

Les ressources peuvent être utilisées avec un fragment de contenu de plusieurs façons ; chacune présentant ses propres avantages :

* **Insérer une ressource** dans un fragment (fragments de médias variés)

   * Font partie du fragment (voir [Parties constituantes d’un fragment de contenu](#constituent-parts-of-a-content-fragment)).
   * Définissent la position de la ressource.
   * Reportez-vous à la section [Insertion de ressources dans votre fragment](/help/assets/content-fragments/content-fragments-variations.md#inserting-assets-into-your-fragment) dans l’éditeur de fragments pour plus d’informations.

  >[!NOTE]
  >
  >Les ressources visuelles insérées dans le fragment de contenu sont liées au paragraphe précédent. Lorsque le fragment est ajouté à une page, ces ressources sont déplacées avec le paragraphe en question quand du contenu intermédiaire est ajouté.

* **Contenu associé**

   * Sont connectés à un fragment ; mais pas une partie fixe du fragment (voir [Parties constituantes d’un fragment de contenu](#constituent-parts-of-a-content-fragment)).
   * Permettent une certaine souplesse de positionnement.
   * Sont facilement disponibles pour utilisation (comme contenu intermédiaire) lors de l’utilisation du fragment sur une page.
   * Voir [Contenu associé](/help/assets/content-fragments/content-fragments-assoc-content.md) pour plus d’informations.

* Ressources disponibles dans le **navigateur Ressources** de l’éditeur de page

   * Permettent une flexibilité totale pour la sélection d’une ressource.
   * Permettent une certaine souplesse de positionnement.
   * N’appliquent pas le concept d’approbation pour un fragment spécifique.

<!--
  * See [Assets Browser](/help/sites-authoring/environment-tools.md#assets-browser) for more information.
-->

### Parties constituantes d’un fragment de contenu {#constituent-parts-of-a-content-fragment}

Les ressources de fragment de contenu se composent des parties suivantes (directement ou indirectement) :

* **Éléments de fragment**

   * Les éléments sont corrélés aux champs de données contenant du contenu.
   * Vous utilisez un modèle de contenu pour créer le fragment de contenu. Les éléments (champs) spécifiés dans le modèle définissent la structure du fragment. Ces éléments (champs) peuvent être de différents types de données.

* **Paragraphes de fragment**

   * Blocs de texte, souvent multilignes, délimités comme des entités individuelles.

   * Dans les modes [Texte enrichi](/help/assets/content-fragments/content-fragments-variations.md#rich-text) et [Markdown](/help/assets/content-fragments/content-fragments-variations.md#markdown), un paragraphe peut être formaté en tant qu’en-tête, auquel cas celui-ci et le paragraphe suivant sont considérés comme une unité.

   * Activez le contrôle du contenu lors de la création de pages.

* **Ressources insérées dans un fragment (fragments de supports variés)**

   * Ressources (images) insérées dans le fragment et utilisées en tant que contenu interne d’un fragment.
   * Sont intégrées dans le système de paragraphe du fragment.
   * Peuvent être formatées lorsque le [fragment est utilisé/référencé sur une page](/help/sites-authoring/content-fragments.md).
   * Peuvent uniquement être ajoutées, supprimées ou déplacées dans un fragment à l’aide de l’éditeur de fragment. Ces actions ne peuvent pas être effectuées dans l’éditeur de page.
   * Peuvent uniquement être ajoutées, supprimées ou déplacées dans un fragment à l’aide du [Format Texte enrichi dans l’éditeur de fragments](/help/assets/content-fragments/content-fragments-variations.md#inserting-assets-into-your-fragment).
   * Peuvent uniquement être ajoutées aux éléments de texte multiligne (tout type de fragment).
   * Sont liées au texte précédent (paragraphe).

     >[!CAUTION]
     >
     >Des ressources peuvent être supprimées (par inadvertance) d’un fragment lors du passage au format texte brut.

     >[!NOTE]
     >
     >Les ressources peuvent également être ajoutées en tant que [contenu supplémentaire (intermédiaire)](/help/sites-authoring/content-fragments.md#using-associated-content) lors de l’utilisation d’un fragment sur une page ; à l’aide du contenu associé ou des ressources de l’explorateur de ressources.

* **Contenu associé**

   * Il s’agit d’un contenu externe à un fragment, mais présentant une pertinence éditoriale pour celui-ci. En règle générale, les images, vidéos ou autres fragments.
   * Les ressources individuelles de la collection peuvent être utilisées avec le fragment dans l’éditeur de page lorsqu’il est ajouté à une page. Cela signifie qu’elles sont facultatives, selon les exigences du canal spécifique.
   * Les ressources sont [associées aux fragments via des collections](/help/assets/content-fragments/content-fragments-assoc-content.md) ; les collections associées permettent à l’auteur de déterminer les ressources à utiliser lors de la création d’une page.

      * Les collections peuvent être associées à des fragments, en tant que contenu par défaut, ou selon les auteurs lors de la création du fragment.
      * Les [Collections de ressources (DAM)](/help/assets/manage-collections.md) constituent la base du contenu associé des fragments.
   * Vous pouvez également ajouter le fragment lui-même à une collection pour faciliter le suivi.

* **Métadonnées de fragment**

   * Utilisez les [Schémas de métadonnées de ressources](/help/assets/metadata-schemas.md).
   * Les balises peuvent être créées lorsque vous :

      * Créez et êtes l’auteur ou l’autrice du fragment
      * Ou plus tard :

         * En affichant/modifiant les **Propriétés** du fragment depuis la console
         * En modifiant les **Métadonnées** dans l’éditeur de fragments

  >[!CAUTION]
  >
  >Les profils de traitement des métadonnées ne s’appliquent pas aux fragments de contenu.

* **Maître**

   * Partie du fragment

      * Chaque fragment de contenu comporte une instance de Principal.
      * Le Principal ne peut pas être supprimé.

   * L’instance maître est accessible dans l’éditeur de fragment sous **[Variations](/help/assets/content-fragments/content-fragments-variations.md)**.
   * L’instance maître n’est pas une variation en tant que telle, mais plutôt la base de toutes les variations.

* **Variations**

   * Il s’agit de rendus de texte de fragment spécifiques à une fin éditoriale. Les variations peuvent être associées au canal, sans que cela soit obligatoire, et elles peuvent également servir à des modifications locales ad hoc.
   * Sont créées en tant que copies de l’instance **maître**, mais peuvent ensuite être modifiées si besoin. Il existe un chevauchement de contenu entre les différentes variations.
   * Peuvent être définies lors de la création de fragments.
   * Stockées dans le fragment, afin d’éviter l’éparpillement des copies de contenu.
   * Les variations peuvent être [synchronisées](/help/assets/content-fragments/content-fragments-variations.md#synchronizing-with-master) par Principal si le contenu du Principal a été mis à jour.
   * Peuvent être [résumées](/help/assets/content-fragments/content-fragments-variations.md#summarizing-text) afin de tronquer rapidement le texte sur une longueur prédéfinie.
   * Disponibles sous l’onglet [Variations](/help/assets/content-fragments/content-fragments-variations.md) de l’éditeur de fragment.

### Contenu intermédiaire lors de la création de page avec des fragments de contenu {#in-between-content-when-page-authoring-with-content-fragments}

Contenu intermédiaire :

* Il est disponible dans l’éditeur de page lorsque vous utilisez des fragments de contenu.
* Il s’agit de [contenu supplémentaire ajouté dans le flux d’un fragment](/help/sites-authoring/content-fragments.md#adding-in-between-content) une fois qu’il a été utilisé ou référencé sur une page.
* Il est disponible dans l’[éditeur de page lorsque vous utilisez des fragments de contenu](/help/sites-authoring/content-fragments.md).
* Le contenu intermédiaire peut être ajouté à n’importe quel fragment, où seul un élément est visible.
* Le contenu associé peut être utilisé, de même que les ressources et/ou les composants du navigateur approprié.

>[!CAUTION]
>
>Le contenu intermédiaire est du contenu de page. Il n’est pas stocké dans le fragment de contenu.

### Conditions requises pour utiliser des fragments {#required-by-fragments}

Pour créer des fragments de contenu, tenez compte des points suivants :

* **Modèles de contenu**

   * Sont [activés à l’aide de l’explorateur de configurations](/help/assets/content-fragments/content-fragments-configuration-browser.md).
   * Sont [créés à l’aide d’outils](/help/assets/content-fragments/content-fragments-models.md).
   * Obligatoires pour [créer un fragment](/help/assets/content-fragments/content-fragments-managing.md#creating-content-fragments).
   * Définissent la structure d’un fragment (titre, éléments de contenu et définitions de balise).
   * Les définitions de modèles de contenu requièrent un titre et un élément de données ; tous les autres attributs sont facultatifs.
   * Le modèle peut définir le contenu par défaut, le cas échéant.
   * Les auteurs ne peuvent pas modifier la structure définie lors de la création du contenu d’un fragment.
   * Les modifications apportées à un modèle après la création de fragments de contenu dépendants peuvent avoir un impact sur ces fragments de contenu.

Pour utiliser vos fragments de contenu pour la création de pages, vous avez également besoin des éléments suivants :

* **Composant Fragment de contenu**

   * Utilitaire de diffusion du fragment au format HTML et/ou JSON.
   * Obligatoire pour [référencer le fragment sur une page](/help/sites-authoring/content-fragments.md).
   * Responsable de la disposition et de la diffusion d’un fragment, c’est-à-dire des canaux.
   * Les fragments ont besoin d’un ou de plusieurs composants dédiés pour définir la disposition, ainsi que diffuser tous les éléments/variations et le contenu associé.
   * Faire glisser un fragment sur une page en mode Création permet d’associer automatiquement le composant requis.

## Exemple d’utilisation {#example-usage}

Un fragment, avec ses éléments et ses variations, peut être utilisé afin de créer du contenu homogène sur plusieurs canaux. Lors de la conception de votre fragment, vous devez tenir compte des éléments utilisés et de leur l’emplacement.

## Bonnes pratiques {#best-practices}

Les fragments de contenu peuvent être utilisés pour former des structures complexes. Adobe fournit des recommandations relatives aux bonnes pratiques à appliquer lors de la définition et de l’utilisation de modèles et de fragments.

### Restez simple {#keep-it-simple}

Lors de la modélisation de contenu structuré dans AEM, simplifiez au maximum les structures de contenu afin d’assurer des performances système solides et une gouvernance rationalisée.

### Nombre de modèles {#number-of-models}

Créez autant de modèles de contenu que nécessaire, mais pas plus.

Un nombre trop élevé de modèles complique la gouvernance et peut ralentir les requêtes GraphQL. Un petit ensemble de modèles, maximum de dizaines faibles, est généralement suffisant. Si vous approchez des dizaines élevées ou plus, reconsidérez votre stratégie de modélisation.

### Imbrication de modèles et de fragments (très important) {#nesting-models-and-fragments}

Évitez l’imbrication profonde ou excessive de fragments de contenu à l’aide des références de fragments de contenu, qui permettent aux fragments de référencer d’autres fragments, parfois sur plusieurs niveaux.

L’utilisation intensive des références de fragments de contenu peut avoir un impact significatif sur les performances du système, la réactivité de l’interface utilisateur et l’exécution des requêtes GraphQL. Visez à ne pas imbriquer plus de dix niveaux.

### Nombre de champs de données et de types de données par modèle {#number-of-data-fields-and-types-per-model}

Incluez uniquement les champs de données et les types dont un modèle a vraiment besoin.

Les modèles trop complexes génèrent des fragments trop complexes qui peuvent rendre la création difficile et réduire les performances de l’éditeur.

### Champs de texte enrichi {#rich-text-fields}

Utilisez les champs de texte enrichi (le type de données **texte multiligne**) avec précaution :

* Champs

  Limitez le nombre de champs de texte enrichi par modèle. Pour des raisons de performances, il n’est pas recommandé d’avoir plus de dix champs de texte enrichi dans un modèle. Si nécessaire, il est recommandé d’utiliser des [fragments de contenu imbriqués](/help/assets/content-fragments/content-fragments-models.md#using-references-to-form-nested-content).

* Contenu

  Vous devez également limiter la quantité de texte stockée dans chaque fragment, ainsi que la quantité de mise en forme HTML. Un contenu de texte enrichi très volumineux peut nuire aux performances du système.

### Nombre de variations {#number-of-variations}

Créez autant de variations de fragment que nécessaire, mais pas plus.

Les variations ajoutent un temps de traitement à un fragment de contenu, dans l’environnement de création et lors de la diffusion également. Il est recommandé de maintenir le nombre de variations à un niveau minimal gérable.

Une bonne pratique consiste à ne pas dépasser dix variations par fragment de contenu.

### Test Avant Production {#test-before-production}

En cas de doute, prototypez les structures de contenu prévues avant de les déployer en production. Des preuves de concept précoces, associées à des tests adéquats, tant sur le plan technique que sur celui de l’acceptation par les utilisateurs, peuvent contribuer à éviter des problèmes ultérieurement, lorsque la production est soumise à des délais.
