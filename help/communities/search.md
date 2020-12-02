---
title: Fonction de recherche
seo-title: Fonction de recherche
description: Ajouter et configurer la recherche sur un site des communautés
seo-description: Ajouter et configurer la recherche sur un site des communautés
uuid: ca633456-911f-447f-881e-653533125d5f
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: authoring
content-type: reference
discoiquuid: 3acac082-efbe-4995-b374-851cb9aaf62d
translation-type: tm+mt
source-git-commit: 6ab91667ad668abf80ccf1710966169b3a187928
workflow-type: tm+mt
source-wordcount: '466'
ht-degree: 31%

---


# Fonction de recherche {#search-feature}

La fonction de recherche fonctionne avec d’autres fonctions, comme les forums, et permet de rechercher du contenu.

Lors de l’ajout de la possibilité de rechercher des publications faites par des membres de la communauté (le contenu généré par l’utilisateur), il existe deux composants : [Rechercher](#search) et [Résultats de la recherche](#search-results).

La page qui inclut le composant `Search Results` prend en charge la recherche et l&#39;affichage des résultats.

La page qui inclut le composant `Search` permet de lancer une recherche avec les résultats apparaissant sur la page `Search Results`.

La fonction de recherche peut être utilisée avec n’importe quelle autre fonction permettant aux visiteurs et aux membres du site d’afficher du contenu.

## Recherche {#search-features}

### Ajout du composant Rechercher à une page {#add-search-to-a-page}

Pour ajouter un composant `Search` à une page en mode création, utilisez l&#39;explorateur de composants pour localiser `Communities / Search` et faites-le glisser sur la place d&#39;une page. L&#39;utilisation de `Search` nécessite une deuxième page pour `Search Results.`

Pour obtenir les informations nécessaires, consultez [Community Components Basics](basics.md).

Lorsque la bibliothèque client requise, `cq.social.hbs.search`, est incluse, c&#39;est ainsi que le composant `Search` apparaîtra.

![add-search](assets/add-search.png)

### Configuration du composant Rechercher {#configure-the-added-search}

Sélectionnez le composant `Search` placé auquel accéder et sélectionnez l&#39;icône `Configure` qui ouvre la boîte de dialogue de modification.

![confiter](assets/configure-new.png)

Sous l&#39;onglet **[!UICONTROL Paramètres de recherche]**, indiquez comment les chemins sont recherchés lorsqu&#39;une requête est saisie par un visiteur.

![paramètres de recherche](assets/search-settings.png)

* **[!UICONTROL Chemins de recherche]** Lorsque vous ajoutez des chemins de recherche à l’aide du bouton Ajouter un élément, la recherche de contenu est limitée. Par exemple, pour limiter la recherche à un forum spécifique, sélectionnez un composant de forum placé dans une page :

   * `/content/community-components/en/forum/jcr:content/content/forum`

* **[!UICONTROL Page de résultatsLes résultats s&#39;affichent sur une page distincte spécifiée à l&#39;aide du navigateur pour sélectionner une page contenant la variable]**
 
`Search Results` component.

## Résultats de la recherche {#search-results}

### Ajout du composant Résultats de la recherche à une page {#add-search-results-to-a-page}

Pour ajouter un composant `Search Results` à une page en mode création, utilisez l’explorateur de composants pour localiser

* `Communities / Search Results`

et faites-le glisser sur la page. Contrairement au composant Rechercher, la deuxième page n’est pas nécessaire, car les résultats s’affichent sur la même page.

Si vous utilisez Search ailleurs dans le site Web, cette page avec `Search Results` peut être configurée pour être la `Result Page` pour toutes les instances de `Search`.

Pour obtenir les informations nécessaires, consultez [Community Components Basics](basics.md).

Lorsque la bibliothèque côté client requise, `cq.social.hbs.search`, est incluse, c&#39;est ainsi que le composant `Search Result` apparaîtra :

![résultat de la recherche](assets/search-result1.png)

### Configuration du composant Résultats de la recherche ajouté {#configure-the-added-search-result}

Sélectionnez le composant `Search Results` placé auquel accéder et sélectionnez l&#39;icône `Configure` qui ouvre la boîte de dialogue de modification.

![configurer](assets/configure-new.png)

Sous l&#39;onglet **[!UICONTROL Paramètres des résultats de recherche]**, il est possible de spécifier les chemins inclus dans la recherche lorsqu&#39;une requête est saisie par un visiteur.

![search-result-settings](assets/search-result-settings.png)

* **[!UICONTROL Résultats de la recherche par page]**

   Définissez le nombre de rubriques/publications affichées par page. La valeur par défaut est 10.

* **[!UICONTROL Chemins de recherche]**

   En ajoutant des chemins de recherche à l&#39;aide du bouton Ajouter un élément, la recherche de contenu est limitée.

## Informations supplémentaires {#additional-information}

Pour plus d&#39;informations, consultez la page [Recherche d&#39;éléments essentiels](search-implementation.md) à l&#39;intention des développeurs.
