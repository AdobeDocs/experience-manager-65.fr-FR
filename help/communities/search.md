---
title: Fonction de recherche
seo-title: Fonction de recherche
description: Ajout et configuration de la recherche sur un site Communities
seo-description: Ajout et configuration de la recherche sur un site Communities
uuid: ca633456-911f-447f-881e-653533125d5f
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: 3acac082-efbe-4995-b374-851cb9aaf62d
exl-id: e252b0e5-a2f8-468e-ac8c-951a5b0f2e32
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '466'
ht-degree: 31%

---

# Fonction de recherche {#search-feature}

La fonction de recherche fonctionne avec d’autres fonctions, comme les forums, et permet de rechercher du contenu.

Lors de l’ajout de la possibilité de rechercher des publications faites par des membres de la communauté (le contenu généré par l’utilisateur), il existe deux composants : [Rechercher](#search) et [Résultats de la recherche](#search-results).

La page qui inclut le composant `Search Results` prend en charge la recherche et l’affichage des résultats.

La page qui comprend le composant `Search` permet de lancer une recherche avec les résultats apparaissant sur la page `Search Results`.

La fonction de recherche peut être utilisée avec n’importe quelle autre fonction permettant aux visiteurs et aux membres du site d’afficher du contenu.

## Recherche {#search-features}

### Ajout du composant Rechercher à une page {#add-search-to-a-page}

Pour ajouter un composant `Search` à une page en mode de création, utilisez l’explorateur de composants pour localiser `Communities / Search` et faites-le glisser sur la page. L’utilisation de `Search` nécessite une deuxième page pour la balise `Search Results.`

Pour plus d’informations, voir [Principes de base des composants des communautés](basics.md).

Lorsque la bibliothèque côté client `cq.social.hbs.search` requise est incluse, voici comment le composant `Search` apparaîtra.

![add-search](assets/add-search.png)

### Configuration du composant Rechercher {#configure-the-added-search}

Sélectionnez le composant `Search` inséré pour y accéder et sélectionnez l’icône `Configure` qui ouvre la boîte de dialogue de modification.

![confgirue](assets/configure-new.png)

Sous l’onglet **[!UICONTROL Paramètres de recherche]**, indiquez comment les chemins sont recherchés lorsqu’une requête est entrée par un visiteur.

![search-settings](assets/search-settings.png)

* **[!UICONTROL Chemins de recherche]** Lorsque vous ajoutez des chemins de recherche à l’aide du bouton Ajouter un élément, la recherche de contenu est limitée. Par exemple, pour limiter la recherche à un forum spécifique, sélectionnez un composant de forum placé dans une page :

   * `/content/community-components/en/forum/jcr:content/content/forum`

* **[!UICONTROL Result]**
PageLes résultats s’affichent sur une page distincte spécifiée à l’aide du navigateur pour sélectionner une page contenant le 
`Search Results` component.

## Résultats de la recherche {#search-results}

### Ajout du composant Résultats de la recherche à une page {#add-search-results-to-a-page}

Pour ajouter un composant `Search Results` à une page en mode création, utilisez l’explorateur de composants pour accéder à :

* `Communities / Search Results`

et faites-le glisser sur la page. Contrairement au composant Rechercher, la deuxième page n’est pas nécessaire, car les résultats s’affichent sur la même page.

Si vous utilisez Rechercher ailleurs dans le site web, cette page avec `Search Results` peut être configurée pour être la `Result Page` pour toutes les instances de `Search`.

Pour plus d’informations, voir [Principes de base des composants des communautés](basics.md).

Lorsque la bibliothèque côté client requise, `cq.social.hbs.search`, est incluse, voici comment le composant `Search Result` apparaîtra :

![search-result](assets/search-result1.png)

### Configuration du composant Résultats de la recherche ajouté {#configure-the-added-search-result}

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
