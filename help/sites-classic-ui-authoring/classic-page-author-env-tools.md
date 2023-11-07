---
title: Création – Environnement et outils
description: La console Sites web vous permet de gérer et de parcourir votre site web. En utilisant deux volets, la structure de votre site web peut être développée et des actions peuvent être entreprises sur les éléments requis.
uuid: 0a9ce725-042a-4697-81fe-ac86cbab0398
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: page-authoring
content-type: reference
discoiquuid: 67625e62-7035-4eb5-8dd5-6840d775a547
docset: aem65
exl-id: 5d7b6b2e-d1d8-4efe-b9ff-c9542b4e67d7
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '898'
ht-degree: 88%

---

# Création – Environnement et outils {#authoring-the-environment-and-tools}

L’environnement de création d’AEM comprend divers mécanismes permettant d’organiser et de modifier votre contenu. Les outils fournis sont accessibles dans plusieurs consoles et éditeurs de page.

## Administration de sites {#site-administration}

La variable **Sites web** vous permet de gérer et de parcourir votre site web. En utilisant les deux volets, la structure de votre site web peut être développée et des actions peuvent être entreprises sur l’élément requis.

![chlimage_1-108](assets/chlimage_1-108.png)

## Modification du contenu de votre page {#editing-your-page-content}

L’IU classique comporte un éditeur de page distinct, qui utilise l’outil de recherche de contenu et le sidekick :

`https://localhost:4502/cf#/content/geometrixx/en/products/triangle.html`

![chlimage_1-109](assets/chlimage_1-109.png)

## Accès à l’Aide {#accessing-help}

Plusieurs ressources d’**aide** peuvent être directement accessibles depuis AEM :

Outre les [barres d’outils de la console](/help/sites-classic-ui-authoring/author-env-basic-handling.md#accessing-help), vous pouvez également accéder à l’aide à partir du sidekick (à l’aide de l’icône ?) lors de la modification d’une page :

![Sidekick réduit](do-not-localize/sidekick-collapsed-2.png)

Ou en utilisant le bouton **Aide** dans la boîte de dialogue de modification de composants spécifiques pour que l’aide contextuelle s’affiche.

## Sidekick {#sidekick}

La variable **Composants** dans l’onglet du sidekick, vous pouvez parcourir les composants pouvant être ajoutés à la page active. Le groupe requis peut être développé, puis un composant déplacé vers l’emplacement requis sur la page.

![chlimage_1-110](assets/chlimage_1-110.png)

## L’outil de recherche de contenu {#the-content-finder}

L’outil de recherche de contenu est un moyen simple et rapide de rechercher des ressources et/ou du contenu dans le référentiel lors de la modification d’une page.

Utilisez l’outil de recherche de contenu pour localiser une plage de ressources. Le cas échéant, vous pouvez faire glisser un élément et le déposer dans un paragraphe de votre page :

* [Images](#finding-images)
* [Documents](#finding-documents)
* [Films](#finding-movies)
* [Navigateur de Dynamic Media](/help/sites-administering/scene7.md#scene7contentbrowser)
* [Pages](#finding-pages)

* [Paragraphes](#referencing-paragraphs-from-other-pages)
* [Produits](#products)
* Ou pour [parcourir le site Web par structure de référentiel](#the-content-finder)

Avec toutes les options, vous pouvez [rechercher des éléments spécifiques](#the-content-finder).

### Recherche d’images {#finding-images}

Cet onglet répertorie toutes les images du référentiel.

Après avoir créé un paragraphe Image sur votre page, vous pouvez faire glisser un élément et le déposer dans le paragraphe.

![chlimage_1-111](assets/chlimage_1-111.png)

### Recherche de documents {#finding-documents}

Cet onglet répertorie tous les documents du référentiel.

Après avoir créé un paragraphe Télécharger sur votre page, vous pouvez faire glisser un élément et le déposer dans le paragraphe.

![chlimage_1-112](assets/chlimage_1-112.png)

### Recherche de films {#finding-movies}

Cet onglet répertorie tous les films (par exemple, les éléments Flash) du référentiel.

Après avoir créé un paragraphe approprié (par exemple, Flash) sur votre page, vous pouvez faire glisser un élément et le déposer dans le paragraphe.

![chlimage_1-113](assets/chlimage_1-113.png)

### Produits {#products}

Cet onglet répertorie tous les produits. Après avoir créé un paragraphe approprié (par exemple, Produit) sur votre page, vous pouvez faire glisser un élément et le déposer dans le paragraphe.

![chlimage_1-114](assets/chlimage_1-114.png)

### Trouver des pages {#finding-pages}

Cet onglet présente toutes les pages. Double-cliquez sur une page pour l’ouvrir à des fins d’édition.

![chlimage_1-115](assets/chlimage_1-115.png)

### Référencement de paragraphes à partir d’autres pages {#referencing-paragraphs-from-other-pages}

Cet onglet vous permet de rechercher une autre page. Tous les paragraphes de cette page seront répertoriés. Vous pouvez ensuite faire glisser un paragraphe sur la page active, ce qui crée une référence au paragraphe d’origine.

![chlimage_1-116](assets/chlimage_1-116.png)

### Utilisation de la vue intégrale de référentiel {#using-the-full-repository-view}

Cet onglet affiche toutes les ressources du référentiel.

![chlimage_1-117](assets/chlimage_1-117.png)

### Utilisation de la recherche avec l’explorateur de contenu {#using-search-with-the-content-browser}

Avec toutes les options, vous pouvez rechercher des éléments spécifiques. Toutes les balises et ressources correspondant au modèle de recherche sont répertoriées :

![screen_shot_2012-02-08at100746am](assets/screen_shot_2012-02-08at100746am.png)

Vous pouvez également utiliser des caractères génériques pour la recherche. Les caractères génériques pris en charge sont les suivants :

* `*`
Correspond à une suite de zéro ou de plusieurs caractères.

* `?`
Correspond à un seul caractère.

>[!NOTE]
>
>Un « nom » de propriété pseudo doit être utilisé pour effectuer une recherche de caractères génériques.

Par exemple, si l’image disponible se nomme :

`ad-nmvtis.jpg`

les schémas de recherche suivants la trouvent (ainsi que toute autre image correspondant au schéma) :

* `name:*nmv*`
* `name:AD*`
La correspondance de caractères n’est *pas* sensible à la casse.

* `name:ad?nm??is.*`
Vous pouvez utiliser un nombre indéfini de caractères génériques dans une requête.

>[!NOTE]
>
>Vous pouvez également utiliser la recherche [SQL2](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/org/apache/jackrabbit/commons/query/sql2/package-summary.html).

## Affichage de références {#showing-references}

AEM vous permet de voir les pages liées à la page sur laquelle vous travaillez actuellement.

Pour afficher les références de page directes :

1. Dans le sidekick, sélectionnez l’icone d’onglet **Page**.

   ![screen_shot_2012-02-16at83127pm](assets/screen_shot_2012-02-16at83127pm.png)

1. Sélectionnez **Afficher les références...** AEM ouvre la fenêtre Références et affiche les pages qui font référence à la page sélectionnée, y compris leurs chemins d’accès.

   ![screen_shot_2012-02-16at83311pm](assets/screen_shot_2012-02-16at83311pm.png)

Dans certains cas, le sidekick permet d’exécuter d’autres actions, notamment :

* [Lancements](/help/sites-classic-ui-authoring/classic-launches.md)
* [Live Copies](/help/sites-administering/msm.md)

* [Plan directeur](/help/sites-administering/msm-best-practices.md)

D’autres [relations interpages sont visibles dans la console Sites web](/help/sites-classic-ui-authoring/author-env-basic-handling.md#page-information-on-the-websites-console).

## Journal d’audit {#audit-log}

Le **journal d’audit** est accessible depuis l’onglet **Informations** du sidekick. Il répertorie les actions récentes ayant eu lieu sur la page active ; par exemple :

![chlimage_1-118](assets/chlimage_1-118.png)

## Informations sur la page {#page-information}

La console Sites Web [fournit des informations sur l’état actuel de la page.](/help/sites-classic-ui-authoring/author-env-basic-handling.md#page-information-on-the-websites-console) par exemple publication, modification, verrouillé, live copy, etc.

## Modes de page {#page-modes}

Lors de la modification d’une page dans l’IU classique, plusieurs modes sont accessibles à l’aide des icônes au bas du sidekick :

![Modes de page](do-not-localize/chlimage_1-12.png)

La rangée d’icônes située au bas du sidekick permet de changer de mode pour le traitement des pages :

* [Modifier](/help/sites-classic-ui-authoring/classic-page-author-edit-mode.md)
Il s’agit du mode par défaut qui permet de modifier la page, d’ajouter ou de supprimer des composants et d’effectuer d’autres modifications.

* [Aperçu](/help/sites-classic-ui-authoring/classic-page-author-edit-content.md#previewing-pages)
Ce mode permet de prévisualiser la page comme si elle apparaissait sur votre site web sous sa forme définitive.

* [Conception](/help/sites-classic-ui-authoring/classic-page-author-design-mode.md#main-pars-procedure-0)
Dans ce mode, vous avez la possibilité de modifier la conception de la page en configurant les composants accessibles.

>[!NOTE]
>
>D’autres options sont également disponibles :
>
>* [Génération de modèles automatique](/help/sites-classic-ui-authoring/classic-feature-scaffolding.md)
>* [ClientContext](/help/sites-administering/client-context.md)
>* Sites web : ouvre la console Sites web .
>* Recharger - Actualise la page.

## Raccourcis clavier {#keyboard-shortcuts}

Divers [raccourcis clavier](/help/sites-classic-ui-authoring/classic-page-author-keyboard-shortcuts.md) sont disponibles.
