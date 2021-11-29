---
title: Guide de prise en main pour l’accès et la diffusion de fragments de contenu découplés
description: Découvrez comment utiliser l’API HTTP Assets d’AEM pour gérer les fragments de contenu et l’API GraphQL dans la diffusion de contenu de fragments de contenu en mode découplé.
exl-id: 2b72f222-2ba5-4a21-86e4-40c763679c32
source-git-commit: 6c75af3957c319c38177cd62c90e781a982ba91b
workflow-type: tm+mt
source-wordcount: '532'
ht-degree: 88%

---

# Guide de prise en main pour l’accès et la diffusion de fragments de contenu découplés {#accessing-delivering-content-fragments}

Découvrez comment utiliser l’API HTTP Assets d’AEM pour gérer les fragments de contenu et l’API GraphQL dans la diffusion de contenu de fragments de contenu en mode découplé.

## Que sont les API GraphQL et REST Assets ?  {#what-are-the-apis}

[Maintenant que vous avez créé des fragments de contenu](create-content-fragment.md), vous pouvez utiliser les API d’AEM pour une diffusion découplée.

* [L’API GraphQL](/help/assets/content-fragments/graphql-api-content-fragments.md) permet de créer des requêtes d’accès et de diffusion de fragments de contenu.
   * Pour l’utiliser, [Les points de fin doivent être définis et activés dans AEM](/help/assets/content-fragments/graphql-api-content-fragments.md#enabling-graphql-endpoint), et si nécessaire, la variable [Interface GraphiQL installée](/help/assets/content-fragments/graphql-api-content-fragments.md#installing-graphiql-interface).
* [L’API REST Assets](/help/assets/assets-api-content-fragments.md) permet de créer et de modifier des fragments de contenu (et d’autres ressources).

Le reste de ce guide porte sur l’accès à GraphQL et la diffusion de fragments de contenu.

## Comment diffuser un fragment de contenu avec GraphQL {#how-to-deliver-a-content-fragment}

Les architectes de l’information doivent concevoir des requêtes pour leurs points d’entrée de canaux afin de diffuser du contenu. Ces requêtes ne doivent généralement être prises en compte qu’une seule fois par point d’entrée et par modèle. Pour les besoins de ce guide de prise en main, nous ne devrons en créer qu’une.

1. Connectez-vous à AEM et accédez à l’interface GraphiQL :
   * Par exemple : `https://<host>:<port>/content/graphiql.html`.

1. GraphiQL est un éditeur de requêtes intégré au navigateur pour GraphQL. Vous pouvez l’utiliser pour créer des requêtes permettant de récupérer des fragments de contenu afin de les diffuser de manière découplée en mode JSON.
   * Le volet de gauche permet de construire votre requête.
   * Le volet de droite affiche les résultats.
   * L’éditeur de requêtes comprend la saisie du code et des touches d’accès rapide pour exécuter facilement la requête.
      ![Éditeur GraphiQL](../assets/graphiql.png)

1. En supposant que le modèle que nous avons créé s’appelle `person`, avec les champs `firstName`, `lastName` et `position`, nous pouvons créer une requête simple pour récupérer le contenu de notre fragment de contenu.

   ```text
   query 
   {
     personList {
       items {
         _path
         firstName
         lastName
         position
       }
     }
   }
   ```

1. Entrez la requête dans le volet de gauche.
   ![Requête GraphiQL](../assets/graphiql-query.png)

1. Cliquez sur le bouton **Exécuter la requête** ou utilisez le raccourci `Ctrl-Enter` pour faire apparaître les résultats sous la forme JSON dans le volet de droite.
   ![Résultats GraphiQL](../assets/graphiql-results.png)

1. Cliquez sur:
   * **Documents** dans le coin supérieur droit de la page pour afficher la documentation contextuelle afin de vous aider à créer vos requêtes qui s’adaptent à vos propres modèles.
   * **Histoire** dans la barre d’outils supérieure pour afficher les requêtes précédentes.
      ![Documentation GraphiQL](../assets/graphiql-documentation.png)

GraphQL permet d’utiliser des requêtes structurées qui peuvent cibler non seulement des ensembles de données spécifiques ou des objets de données individuels, mais peuvent également fournir des éléments spécifiques des objets, des résultats imbriqués, prend en charge les variables de requête, et bien plus encore.

GraphQL permet d’éviter les requêtes d’API itératives ainsi que la surdiffusion, et permet la diffusion en masse de ce qui est exactement nécessaire pour le rendu en réponse à une requête d’API unique. Le fichier JSON produit peut être utilisé pour diffuser des données vers d’autres sites ou applications.

## Étapes suivantes {#next-steps}

C’est terminé ! Vous possédez maintenant une compréhension de base de la gestion de contenu découplée dans AEM. Bien entendu, il existe beaucoup d’autres ressources que vous pouvez approfondir pour une compréhension complète des fonctionnalités disponibles.

* **[Explorateur de configurations](create-configuration.md)** – Pour plus d’informations sur l’Explorateur de configurations AEM
* **[Fragments de contenu](/help/assets/content-fragments/content-fragments.md)** – Pour plus d’informations sur la création et la gestion de fragments de contenu
* **[Prise en charge des fragments de contenu dans l’API HTTP AEM Assets](/help/assets/assets-api-content-fragments.md)** – Pour plus d’informations sur l’accès direct au contenu AEM via l’API HTTP, via des opérations CRUD (création, lecture, mise à jour, suppression)
* **[API GraphQL](/help/assets/content-fragments/graphql-api-content-fragments.md)** – Pour plus d’informations sur la diffusion découplée de fragments de contenu
