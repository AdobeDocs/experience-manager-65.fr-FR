---
title: Utilisation de fragments de contenu
seo-title: Utilisation de fragments de contenu
description: Découvrez comment les fragments de contenu vous permettent de concevoir, de créer, d’organiser et d’utiliser du contenu indépendant des pages.
seo-description: Découvrez comment les fragments de contenu vous permettent de concevoir, de créer, d’organiser et d’utiliser du contenu indépendant des pages.
uuid: d35d5638-43a9-424d-9806-6e8d459980d7
contentOwner: Alison Heimoz
topic-tags: content-fragments
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
content-type: reference
discoiquuid: 7ecc1bcf-38a9-4a59-8dd3-79cb90dec33d
docset: aem65
feature: Fragments de contenu
role: Business Practitioner, Administrator
exl-id: b204df18-2aef-4905-82f8-c777928ba828
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1975'
ht-degree: 99%

---

# Utilisation de fragments de contenu {#working-with-content-fragments}

Les fragments de contenu d’Adobe Experience Manager (AEM) permettent de concevoir, de créer, d’organiser et de [publier du contenu indépendant des pages](/help/sites-authoring/content-fragments.md). Ils permettent de préparer le contenu prêt à être utilisé dans des emplacements multiples/sur plusieurs canaux.

Les fragments de contenu peuvent également être livrés au format JSON, à l’aide des fonctions d’exportation Sling Model (JSON) des composants de base AEM. Cette forme de livraison :

* permet d’utiliser le composant pour gérer les éléments d’un fragment à livrer ;
* permet la livraison en masse, en ajoutant plusieurs composants de base de fragments de contenu sur la page utilisée pour la livraison d’API.

Cette page et les suivantes portent sur les tâches de création, de configuration et de gestion de vos fragments de contenu :

* [Gestion des fragments de contenu](/help/assets/content-fragments/content-fragments-managing.md)    : créez des fragments de contenu, puis modifiez-les, publiez-les et référencez-les.
* [Modèles de fragment de contenu](/help/assets/content-fragments/content-fragments-models.md) : activation, création et définition de vos modèles.
* [Variations – création de fragments de contenu](/help/assets/content-fragments/content-fragments-variations.md) : créez le contenu du fragment et créez des variantes du maître.
* [Texte (Markdown)](/help/assets/content-fragments/content-fragments-markdown.md) : utilisation de la syntaxe Markdown pour votre fragment.
* [Utilisation du contenu associé](/help/assets/content-fragments/content-fragments-assoc-content.md) : ajout de contenu associé.
* [Métadonnées – propriétés des fragments](/help/assets/content-fragments/content-fragments-metadata.md) : affichage et modification des propriétés des fragments.

>[!NOTE]
>
>Ces pages devraient être lues conjointement à [Création de pages avec des fragments de contenu](/help/sites-authoring/content-fragments.md).

Le nombre de canaux de communication augmente tous les ans. En règle générale, les canaux font référence au mécanisme de diffusion :

* Canal physique ; ordinateur de bureau ou appareil mobile par exemple.
* Forme de livraison sur un canal physique ; « page des détails produit »/« page catégorie de produit » sur ordinateur de bureau ou « web mobile »/« Application mobile » pour les appareils mobiles.

Cependant, vous ne voulez probablement pas utiliser exactement le même contenu pour tous les canaux et vous devez optimiser votre contenu en fonction des différents canaux.

Les fragments de contenu vous permettent de :

* Déterminer la manière la plus efficace d’atteindre les publics ciblés sur tous les canaux.
* Créer et gérer du contenu éditorial indépendamment du canal de diffusion.
* Créer des groupes de contenu sur un large éventail de canaux.
* Concevoir des variations de contenu pour des canaux spécifiques.
* Ajouter des images à votre texte en insérant des ressources (fragments de supports variés).

Ces fragments de contenu peuvent ensuite être assemblés pour offrir diverses expériences sur de multiples canaux.

## Fragments de contenu et Content Services    {#content-fragments-and-content-services}

AEM Content Services est conçu pour généraliser la description et la diffusion de contenu dans/à partir d’AEM à des canaux autres que des pages web.

Ils assurent la diffusion du contenu aux canaux autres que les pages web AEM classiques, à l’aide de méthodes normalisées qui peuvent être utilisées par tous les clients. Ces canaux peuvent inclure :

* des applications sur une seule page ;
* des applications mobiles natives ;
* d’autres canaux et points de contact externes à AEM.

La diffusion est effectuée au format JSON.

Les fragments de contenu AEM peuvent être utilisés pour décrire et gérer du contenu structuré. Le contenu structuré est défini dans des modèles pouvant contenir divers types de contenu, notamment du texte, des données numériques et booléennes, la date et l’heure, etc.

Associé aux fonctionnalités d’exportation JSON des composants de base AEM, ce contenu structuré peut ensuite être utilisé pour livrer le contenu AEM à des canaux autres que les pages AEM.

>[!NOTE]
>
>Les **fragments de contenu** et les **[fragments d’expérience](/help/sites-authoring/experience-fragments.md)** représentent deux fonctions distinctes d’AEM :
>* Les **fragments de contenu** sont des contenus éditoriaux, composés essentiellement de texte et des images associées. Il s’agit exclusivement de contenu, sans aucun élément de conception ni de mise en page.
>* Les **fragments d’expérience** désignent un contenu parfaitement mis en page : un fragment de page web.

>
>
Les fragments d’expérience peuvent être composés de contenu sous la forme de fragments de contenu, mais pas l’inverse.
>
>Pour plus d’informations, voir également [Présentation des fragments de contenu et d’expérience dans AEM](https://docs.adobe.com/content/help/en/experience-manager-learn/sites/content-fragments/understand-content-fragments-and-experience-fragments.html).

>[!CAUTION]
>
>Les fragments de contenu ne sont pas disponibles dans l’interface utilisateur classique.
>
>Le composant Fragment de contenu apparaît dans le sidekick de l’interface utilisateur classique, mais les fonctions associées ne sont pas disponibles.

>[!NOTE]
>
>AEM prend également en charge la traduction des fragments de contenu. Voir [Création de projets de traduction pour les fragments de contenu](/help/assets/creating-translation-projects-for-content-fragments.md) pour plus d’informations.

## Types de fragments de contenu {#types-of-content-fragment}

Les fragments de contenu peuvent être comme suit :

* Des fragments simples
Ils n’ont pas de structure prédéfinie. Ils contiennent uniquement du texte et des images.
Ils sont basés sur le modèle de fragment simple.

* Des fragments présentant du contenu structuré
Ils sont basés sur un [modèle de fragment de contenu](/help/assets/content-fragments/content-fragments-models.md), qui prédéfinit une structure pour le fragment résultant.
Ils peuvent également être utilisés pour réaliser des Content Services à l’aide de l’exportateur JSON.

## Type de contenu {#content-type}

Les fragments de contenu sont :

* Stockés en tant que **ressources** :

   * Les fragments de contenu (et leurs variations) peuvent être créés et gérés à partir de la console **Ressources**.
   * Créés et modifiés dans l’éditeur de fragment de contenu.

* Utilisés dans l’[éditeur de page au moyen du composant Fragment de contenu](/help/sites-authoring/content-fragments.md) (qui fait référence au composant) :

   * Le composant **Fragment de contenu** est disponible pour les créateurs de pages. Il leur permet de référencer et de livrer le fragment de contenu requis au format HTML ou JSON.

Les fragments de contenu sont une structure de contenu qui :

* ne possède aucun élément de conception ni de mise en page (mise en forme partielle possible en mode texte enrichi) ;
* contient une ou plusieurs [parties constituantes](#constituent-parts-of-a-content-fragment) ;
* peut [contenir, ou être connecté à, des images](#fragments-with-visual-assets) ;
* peut utiliser du [contenu intermédiaire](#in-between-content-when-page-authoring-with-content-fragments) en cas de référencement sur une page ;

* est indépendant du mécanisme de livraison (c’est-à-dire de la page ou du canal).

### Fragments avec des ressources visuelles {#fragments-with-visual-assets}

Pour donner aux auteurs plus de contrôle sur leur contenu, il est possible d’ajouter et/ou d’intégrer des images à un fragment de contenu.

Les ressources peuvent être utilisées avec un fragment de contenu de plusieurs façons ; chacune présentant ses propres avantages :

* **Insérer une ressource** dans un fragment (fragments de supports variés)

   * Font partie intégrante du fragment (voir [Parties constituantes d’un fragment de contenu](#constituent-parts-of-a-content-fragment)).
   * Définissent la position de la ressource.
   * Voir [Insertion de ressources dans votre fragment](/help/assets/content-fragments/content-fragments-variations.md#inserting-assets-into-your-fragment) dans l’éditeur de fragment pour plus d’informations.

   >[!NOTE]
   >
   >Les ressources visuelles insérées dans le fragment de contenu sont liées au paragraphe précédent. Lorsque le fragment est ajouté à une page, ces ressources sont déplacées avec le paragraphe en question lorsque du contenu intermédiaire est ajouté.

* **Contenu associé**

   * Sont connectés à un fragment ; mais pas à une partie fixe du fragment (voir [Parties constituantes d’un fragment de contenu](#constituent-parts-of-a-content-fragment)).
   * Permettent une certaine souplesse de positionnement.
   * Sont disponibles et pratiques (en tant que contenu intermédiaire) lorsque vous utilisez le fragment sur une page.
   * Voir [Contenu associé](/help/assets/content-fragments/content-fragments-assoc-content.md) pour plus d’informations.

* Ressources disponibles dans le **navigateur Ressources** de l’éditeur de page

   * Permettent une flexibilité totale pour la sélection d’une ressource.
   * Permettent une certaine souplesse de positionnement.
   * N’appliquent pas le concept d’approbation pour un fragment spécifique.
   * Voir le [navigateur de ressources](/help/sites-authoring/author-environment-tools.md#assets-browser) pour plus d’informations.

### Parties constituantes d’un fragment de contenu {#constituent-parts-of-a-content-fragment}

Les ressources de fragment de contenu se composent des parties suivantes (directement ou indirectement) :

* **Éléments de fragment**

   * Les éléments sont en corrélation avec les champs de données possédant du contenu.
   * Pour les fragments avec du contenu structuré, vous utilisez un modèle de contenu afin de créer le fragment de contenu. Les éléments (champs) spécifiés dans le modèle définissent la structure du fragment. Ces éléments (champs) peuvent être de divers types de données.
   * Pour les fragments simples :

      * Le contenu est conservé dans un ou plusieurs champs de texte multiligne ou éléments.
      * Les éléments sont définis dans le modèle de fragment (ils ne peuvent pas être définis lors de la création du fragment, voir [Modèles de fragments de contenu](/help/sites-developing/content-fragment-templates.md)).

* **Paragraphes de fragment**

   * Des blocs de texte qui sont :

      * séparés par des espaces verticaux (retour chariot) ;
      * dans des éléments de texte multiligne ; au sein de fragments simples ou structurés.
   * Dans les modes [Texte enrichi](/help/assets/content-fragments/content-fragments-variations.md#rich-text) et [Markdown](/help/assets/content-fragments/content-fragments-variations.md#markdown), un paragraphe peut être formaté en tant qu’en-tête, auquel cas celui-ci et le paragraphe suivant sont considérés comme une unité.

   * Activent le contrôle du contenu lors de la création de la page.


* **Ressources insérées dans un fragment (fragments de supports variés)**

   * Ressources (images) insérées dans le fragment et utilisées en tant que contenu interne d’un fragment.
   * Sont intégrées dans le système de paragraphe du fragment.
   * Peuvent être formatées lorsque le [fragment est utilisé/référencé sur une page](/help/sites-authoring/content-fragments.md).
   * Ne peuvent pas être ajoutées, supprimées ni déplacées dans un fragment à l’aide de l’éditeur de fragment. Ces actions ne peuvent pas être effectuées dans l’éditeur de page.
   * Peuvent uniquement être ajoutées, supprimées ou déplacées dans un fragment en utilisant le format [texte enrichi de l’éditeur de fragment](/help/assets/content-fragments/content-fragments-variations.md#inserting-assets-into-your-fragment).
   * Peuvent uniquement être ajoutées aux éléments de texte multiligne (tout type de fragment).
   * Sont liées au texte précédent (paragraphe).

   >[!CAUTION]
   >
   >Peuvent être supprimées (par inadvertance) d’un fragment lors du passage au format texte brut.

   >[!NOTE]
   >
   >Les ressources peuvent également être ajoutées en tant que [contenu supplémentaire (intermédiaire)](/help/sites-authoring/content-fragments.md#using-associated-content) lors de l’utilisation d’un fragment sur une page en utilisant le contenu associé ou les ressources du navigateur de ressources.

* **Contenu associé**

   * Il s’agit d’un contenu externe, mais avec la pertinence éditoriale d’un fragment. En règle générale, des images, des vidéos ou d’autres types de fragments.
   * Les ressources individuelles de la collection peuvent être utilisées avec le fragment dans l’éditeur de page, lorsqu’il est ajouté à une page. Cela signifie qu’elles sont facultatives, en fonction des exigences du canal spécifique.
   * Les ressources sont [associées aux fragments via des collections](/help/assets/content-fragments/content-fragments-assoc-content.md) ; les collections associées permettent à l’auteur de déterminer les ressources à utiliser lors de la création d’une page.

      * Les collections peuvent être associées à des fragments à l’aide de modèles, en tant que contenu par défaut, ou par les auteurs lors de la création du fragment.
      * Les [Collections de ressources (DAM)](/help/assets/manage-collections.md) servent de base au contenu associé des fragments.
   * Vous pouvez également ajouter le fragment lui-même à une collection pour en faciliter le suivi.


* **Métadonnées de fragment**

   * Utilisez les [schémas de métadonnées de ressources](/help/assets/metadata.md).
   * Des balises peuvent être créées lorsque vous :

      * Créez le fragment
      * Ou ensuite :

         * Lors de l’affichage/de la modification des **propriétés** de fragment dans la console
         * Lors de la modification des **métadonnées** dans l’éditeur de fragment

   >[!CAUTION]
   >
   >Les profils de traitement de métadonnées ne s’appliquent pas aux fragments de contenu.

* **Maître**

   * Une partie intégrante du fragment

      * Chaque fragment de contenu possède une instance maître.
      * L’instance maître ne peut pas être supprimée.
   * L’instance maître est accessible dans l’éditeur de fragment sous **[Variations](/help/assets/content-fragments/content-fragments-variations.md)**.
   * L’instance maître n’est pas une variation en tant que telle, mais plutôt la base de toutes les variations.


* **Variations**

   * Il s’agit de rendus de texte de fragment spécifiques à fin éditoriale. Les variations peuvent être associées au canal, sans que cela soit obligatoire, et elles peuvent également servir à des modifications locales ad hoc.
   * Sont créées en tant que copies de l’instance **maître**, mais peuvent ensuite être modifiées si besoin. Il existe généralement un chevauchement de contenu entre les différentes variations.
   * Peuvent être définies lors de la création du fragment ou être prédéfinies dans les modèles de fragment.
   * Stockées dans le fragment, afin d’éviter l’éparpillement des copies de contenu.
   * Les variantes peuvent être [synchronisées](/help/assets/content-fragments/content-fragments-variations.md#synchronizing-with-master) avec l’instance maître si son contenu a été mis à jour.
   * Peuvent être [résumées](/help/assets/content-fragments/content-fragments-variations.md#summarizing-text) afin de tronquer rapidement le texte sur une longueur prédéfinie.
   * Disponibles sous l’onglet [Variations](/help/assets/content-fragments/content-fragments-variations.md) de l’éditeur de fragment.

### Contenu intermédiaire lors de la création de page avec des fragments de contenu {#in-between-content-when-page-authoring-with-content-fragments}

Contenu intermédiaire :

* Il est disponible dans l’[éditeur de page lorsque vous utilisez des fragments de contenu](/help/sites-authoring/content-fragments.md).
* Il s’agit de [contenu supplémentaire ajouté dans le flux d’un fragment](/help/sites-authoring/content-fragments.md#adding-in-between-content) une fois qu’il a été utilisé ou référencé sur une page.
* Le contenu intermédiaire peut être ajouté à n’importe quel fragment, où seul un élément est visible.
* Le contenu associé peut être utilisé, tout comme les ressources et/ou les composants du navigateur approprié.

>[!CAUTION]
>
>Le contenu intermédiaire est du contenu de page. Il n’est pas stocké dans le fragment de contenu.

### Conditions requises pour utiliser des fragments {#required-by-fragments}

Pour créer, modifier et utiliser des fragments de contenu, vous aurez également besoin des éléments suivants :

* **Modèles de contenu**

   * Il est [activé, puis créé à l’aide d’outils](/help/assets/content-fragments/content-fragments-models.md).
   * Obligatoire pour [créer un fragment structuré](/help/assets/content-fragments/content-fragments-managing.md#creating-content-fragments).
   * Définissent la structure d’un fragment (titre, éléments de contenu et définitions de balise).
   * Les définitions de modèles de contenu requièrent un titre et un élément de données ; tous les autres attributs sont facultatifs. En outre, le modèle définit une portée minimale du fragment et du contenu par défaut, le cas échéant. Les auteurs ne peuvent pas modifier la structure définie lors de la création du contenu d’un fragment.

* **Modèle de fragment**

   * Obligatoire pour [créer un fragment simple](/help/assets/content-fragments/content-fragments-managing.md#creating-content-fragments).
   * Généralement [développé pendant la mise en œuvre d’un projet](/help/sites-developing/content-fragment-templates.md) ; il ne peut pas être créé lors de la création.
   * Définit les propriétés de base d’un fragment simple (titre, nombre d’éléments de texte, définitions de balises).
   * Les définitions de modèles requièrent un titre et un élément de texte ; tous les autres attributs sont facultatifs. En outre, le modèle définit une portée minimale du fragment et du contenu par défaut, le cas échéant. Les auteurs peuvent ultérieurement étendre un fragment au-delà de ce qui a été défini dans le modèle.

* **Composant de fragment de contenu**

   * Essentiel pour livrer le fragment au format HTML et/ou JSON.
   * Obligatoire pour [référencer le fragment sur une page](/help/sites-authoring/content-fragments.md).
   * Responsable de la mise en page et de la diffusion d’un fragment, c’est-à-dire des canaux.
   * Les fragments ont besoin d’un ou de plusieurs composants dédiés pour définir la mise en page, ainsi que diffuser tous les éléments/variations et le contenu associé.
   * Faire glisser un fragment sur une page en mode Création permet d’associer automatiquement le composant requis.

## Exemple d’utilisation  {#example-usage}

Un fragment, avec ses éléments et ses variations, peut être utilisé afin de créer du contenu homogène sur plusieurs canaux. Lors de la conception d’un fragment, vous devez prendre en compte où vous utiliserez chacun de ses éléments.

### L’exemple de We.Retail {#we-retail-sample}

Un exemple de fragment est visible à l’adresse :

`https://localhost:4502/assets.html/content/dam/we-retail/en/experiences/arctic-surfing-in-lofoten`
