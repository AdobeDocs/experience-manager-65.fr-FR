---
title: Fonctionnalité de recherche
description: Ajout et configuration de la recherche sur un site Communities
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
exl-id: e252b0e5-a2f8-468e-ac8c-951a5b0f2e32
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '456'
ht-degree: 1%

---

# Fonctionnalité de recherche {#search-feature}

La fonction de recherche fonctionne avec différentes autres fonctionnalités, telles que les forums, pour permettre de rechercher du contenu.

Lors de l’ajout de la possibilité de rechercher des publications saisies par des membres de la communauté, appelées contenu généré par l’utilisateur, il existe deux composants : [Recherche](#search) et [Résultats de la recherche](#search-results).

La page qui inclut le composant `Search Results` prend en charge la recherche et l’affichage des résultats.

La page qui inclut le composant `Search` fournit un emplacement où lancer une recherche avec les résultats apparaissant sur la page `Search Results`.

La fonction de recherche peut être utilisée avec toute autre fonction qui permet aux visiteurs et aux membres du site d’afficher du contenu.

## Recherche {#search-features}

### Ajouter la recherche à une page {#add-search-to-a-page}

Pour ajouter un composant `Search` à une page en mode création, utilisez l’explorateur de composants pour localiser `Communities / Search` et le faire glisser sur une page. L’utilisation de `Search` nécessite une seconde page pour `Search Results.`

Pour plus d’informations, consultez la page [Principes de base des composants Communities](basics.md).

Lorsque la bibliothèque côté client requise, `cq.social.hbs.search`, est incluse, voici comment le composant `Search` apparaîtra.

![add-search](assets/add-search.png)

### Configuration de la recherche ajoutée {#configure-the-added-search}

Sélectionnez le composant `Search` inséré pour y accéder et sélectionnez l’icône `Configure` qui ouvre la boîte de dialogue de modification.

![confgirue](assets/configure-new.png)

Sous l’onglet **[!UICONTROL Paramètres de recherche]**, spécifiez les chemins de recherche lorsqu’une requête est entrée par un visiteur.

![search-settings](assets/search-settings.png)

* **[!UICONTROL Chemins de recherche]**
En ajoutant des chemins de recherche à l’aide du bouton Ajouter un élément , la recherche de contenu est limitée. Par exemple, pour limiter la recherche à un forum spécifique, sélectionnez un composant de forum placé dans une page :

   * `/content/community-components/en/forum/jcr:content/content/forum`

* **[!UICONTROL Page de résultats]**
Les résultats s’affichent sur une page distincte spécifiée à l’aide du navigateur pour sélectionner une page contenant le composant `Search Results`.

## Résultats de la recherche {#search-results}

### Ajout de résultats de recherche à une page {#add-search-results-to-a-page}

Pour ajouter un composant `Search Results` à une page en mode création, utilisez l’explorateur de composants pour accéder à :

* `Communities / Search Results`

et faites-le glisser sur la page. Contrairement au composant Rechercher, aucune deuxième page n’est nécessaire, car les résultats s’affichent sur la même page.

Si vous utilisez Rechercher ailleurs dans le site web, cette page avec `Search Results` peut être configurée pour être le `Result Page` de toutes les instances de `Search`.

Pour plus d’informations, consultez la page [Principes de base des composants Communities](basics.md).

Lorsque la bibliothèque côté client requise, `cq.social.hbs.search`, est incluse, voici comment le composant `Search Result` apparaîtra :

![search-result](assets/search-result1.png)

### Configuration du résultat de recherche ajouté {#configure-the-added-search-result}

Sélectionnez le composant `Search Results` inséré pour y accéder et sélectionnez l’icône `Configure` qui ouvre la boîte de dialogue de modification.

![configure](assets/configure-new.png)

Sous l’onglet **[!UICONTROL Paramètres des résultats de recherche]**, il est possible de spécifier les chemins inclus dans la recherche lorsqu’une requête est entrée par un visiteur.

![search-result-settings](assets/search-result-settings.png)

* **[!UICONTROL Résultats de la recherche par page]**

  Définissez le nombre de rubriques/publications affichées par page. La valeur par défaut est 10.

* **[!UICONTROL Chemins de recherche]**

  En ajoutant des chemins de recherche à l’aide du bouton Ajouter un élément , la recherche de contenu est limitée.

## Informations supplémentaires {#additional-information}

Pour plus d’informations, reportez-vous à la page [Notions fondamentales sur la recherche](search-implementation.md) pour les développeurs.
