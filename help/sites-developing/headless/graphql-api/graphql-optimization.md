---
title: Optimisation des requêtes GraphQL.
description: Découvrez comment optimiser vos requêtes GraphQL lors du filtrage, de la pagination et du tri de vos fragments de contenu dans Adobe Experience Manager as a Cloud Service pour une diffusion de contenu sans interface.
source-git-commit: 1481d613783089046b44d4652d38f7b4b16acc4d
workflow-type: tm+mt
source-wordcount: '1186'
ht-degree: 58%

---


# Optimisation des requêtes GraphQL. {#optimizing-graphql-queries}

>[!NOTE]
>
>Avant d’appliquer ces recommandations d’optimisation, envisagez [Mise à jour des fragments de contenu pour la pagination et le tri dans le filtrage GraphQL](/help/sites-developing/headless/graphql-api/graphql-optimized-filtering-content-update.md) pour de meilleures performances.

Sur une instance d’AEM avec un grand nombre de fragments de contenu que le même modèle partage, les requêtes de liste GraphQL peuvent devenir coûteuses (en termes de ressources).

La raison en est la suivante : *all* les fragments qui partagent un modèle utilisé dans la requête GraphQL doivent être chargés en mémoire. Cela consomme à la fois du temps et de la mémoire. Le filtrage, qui peut réduire le nombre d’éléments dans le jeu de résultats (final), ne peut être appliqué qu’**après** le chargement du jeu de résultats en mémoire.

Ce processus peut donner l’impression que même de petits ensembles de résultats (peuvent) entraîner de mauvaises performances. Toutefois, en réalité, la lenteur est due à la taille de l’ensemble de résultats initial, car elle doit être gérée en interne avant de pouvoir appliquer le filtrage.

Pour réduire les problèmes de performances et de mémoire, ce jeu de résultats initial doit rester aussi petit que possible.

AEM propose deux méthodes d’optimisation des requêtes GraphQL :

* [Le filtrage hybride.](#hybrid-filtering)
* La [pagination](#paging).

   * Le [tri](#sorting) n’est pas directement lié à l’optimisation, mais est lié à la pagination.

Chaque approche comporte ses propres cas d’utilisation et ses propres limites. Ce document fournit des informations sur le filtrage hybride et la pagination, avec quelques [bonnes pratiques](#best-practices) pour optimiser les requêtes GraphQL.

## Le filtrage hybride. {#hybrid-filtering}

Le filtrage hybride combine le filtrage JCR avec le filtrage AEM.

Il applique un filtre JCR (sous la forme d’une contrainte de requête) avant de charger le jeu de résultats en mémoire pour le filtrage AEM. Ce processus permet de réduire le jeu de résultats chargé en mémoire, car le filtre JCR supprime au préalable les résultats superflus.

>[!NOTE]
>
>Pour des raisons techniques (par exemple, flexibilité, imbrication de fragments), AEM ne peut pas déléguer l’intégralité du filtrage à JCR.

Cette technique permet de conserver la flexibilité offerte par les filtres GraphQL, tout en déléguant autant de filtrage que possible à JCR.

## Pagination {#paging}

GraphQL dans AEM prend en charge deux types de pagination :

* [pagination basée sur les limites/décalages](/help/sites-developing/headless/graphql-api/graphql-api-content-fragments.md#list-offset-limit)
Ce type de pagination est utilisé pour les requêtes de liste ; ces requêtes se terminent par 
`List` ; par exemple, `articleList`.
Pour l’utiliser, vous devez indiquer la position du premier élément à renvoyer (le `offset`) et le nombre d’éléments à renvoyer (la variable `limit`, ou la taille de la page).

* [pagination basée sur le curseur](/help/sites-developing/headless/graphql-api/graphql-api-content-fragments.md#paginated-first-after) (représenté par `first`et `after`) Ce type de pagination fournit un identifiant unique pour chaque élément ; également appelé curseur.
Dans la requête, vous spécifiez le curseur du dernier élément de la page précédente, ainsi que la taille de la page (le nombre maximal d’éléments à renvoyer).

   Comme la pagination basée sur le curseur ne s’intègre pas dans les structures de données des requêtes basées sur des listes, AEM a introduit un type de requête `Paginated` ; par exemple : `articlePaginated`. Les structures et paramètres de données utilisés suivent la [Spécification de connexion du curseur GraphQL](https://relay.dev/graphql/connections.htm).

   >[!NOTE]
   >
   >AEM prend actuellement en charge la pagination (à l’aide des paramètres `after`/`first`).
   >
   >La pagination ascendante (à l’aide des paramètres `before`/`last`) n’est pas prise en charge.

## Tri {#sorting}

Le tri ne peut être efficace que si tous les critères de tri sont liés à des fragments de niveau supérieur.

Si l’ordre de tri inclut un ou plusieurs champs qui se trouvent sur un fragment imbriqué, tous les fragments partageant le modèle de niveau supérieur doivent être chargés en mémoire. Ce flux a un impact négatif sur les performances.

>[!NOTE]
>
>Le tri sur les champs de niveau supérieur a également un impact (quoique faible) sur les performances.

## Bonnes pratiques {#best-practices}

L’objectif principal de toutes les optimisations est de réduire le jeu de résultats initial. Les bonnes pratiques répertoriées ici fournissent des moyens de le faire. Elles peuvent (et doivent) être combinées.

### Filtrer sur les propriétés de niveau supérieur uniquement. {#filter-top-level-properties-only}

Actuellement, le filtrage au niveau JCR ne fonctionne que pour les fragments de niveau supérieur.

Si un filtre s’adresse aux champs d’un fragment imbriqué, AEM doit recharger (en mémoire) tous les fragments qui partagent le modèle sous-jacent.

Vous pouvez toujours optimiser ces requêtes GraphQL en combinant des expressions de filtre sur les champs de fragments de niveau supérieur et sur les champs de fragments imbriqués avec la propriété [Opérateur ET](#logical-operations-in-filter-expressions).

### Utiliser la structure de contenu. {#use-content-structure}

Dans AEM, il est recommandé d’utiliser la structure de référentiel pour réduire la portée du contenu à traiter.

Appliquez cette approche aux requêtes GraphQL en appliquant un filtre sur la variable `_path` champ du fragment de niveau supérieur :

```graphql
{
  someList(filter: {
    _path: {
      _expressions: [ 
        {
          value: "/content/dam/some/sub/path/",
          _operator: STARTS_WITH
        }
      ]
    }
  }) {
    items {
      # ...
    }
  }
}
```

>[!NOTE]
>
>Le dernier `/` sur `value` est requis pour obtenir les meilleures performances.

### Utiliser la pagination. {#use-paging}

Vous pouvez également utiliser la pagination pour réduire le jeu de résultats initial ; en particulier si vos requêtes n’utilisent aucun filtrage et tri.

Si vous filtrez ou triez les fragments imbriqués, les requêtes paginées peuvent être lentes, car AEM doit toujours charger de plus grandes quantités de fragments en mémoire. Par conséquent, si vous combinez filtrage et pagination, tenez compte des règles de filtrage (tel qu’indiqué ci-dessus).

Pour la pagination, le tri est tout aussi important car les résultats paginés sont toujours triés, de manière explicite ou implicite.

Si vous souhaitez principalement récupérer les premières pages uniquement, il n’y a aucune différence significative entre l’utilisation des requêtes `...List` ou `...Paginated`. Cependant, si votre application souhaite lire plus d’une ou deux pages, vous devez penser à utiliser la requête `...Paginated`, car celle-ci fonctionne nettement mieux avec les pages ultérieures.

### Opérations logiques dans les expressions de filtre {#logical-operations-in-filter-expressions}

Si vous filtrez des fragments imbriqués, vous pouvez toujours appliquer un filtrage JCR en fournissant un filtre d’accompagnement sur un champ de niveau supérieur combiné à l’aide de la variable `AND` de l’opérateur.

Un cas d’utilisation type consiste à restreindre la portée de la requête à l’aide d’un filtre sur la variable `_path` champ du fragment de niveau supérieur. Filtrez ensuite les champs supplémentaires pouvant se trouver au niveau supérieur ou sur un fragment imbriqué.

Dans ce cas, les différentes expressions de filtre sont combinées avec `AND`. Par conséquent, le filtre sur `_path` peut limiter efficacement l’ensemble de résultats initial. Tous les autres filtres sur les champs de niveau supérieur peuvent également contribuer à réduire l’ensemble de résultats initial, à condition qu’ils soient combinés avec `AND`.

Les expressions de filtre combinées avec `OR` ne peuvent pas être optimisées si des fragments imbriqués sont impliqués. Telle `OR` les expressions ne peuvent être optimisées que si *non* les fragments imbriqués sont impliqués.

### Éviter le filtrage sur les champs de texte multiligne {#avoid-filtering-multiline-textfields}

Les champs d&#39;un champ de texte multiligne (html, markdown, plaintext, json) ne peuvent pas être filtrés via une requête JCR, car le contenu de ces champs doit être calculé à la volée.

Si vous devez toujours filtrer sur un champ de texte multiligne, pensez à limiter la taille du jeu de résultats initial en ajoutant des expressions de filtre supplémentaires et en les combinant avec `AND`. Une autre solution consiste à limiter la portée en filtrant sur le champ `_path`.

### Éviter le filtrage sur des champs virtuels {#avoid-filtering-virtual-fields}

Les champs virtuels (la plupart des champs commençant par `_`) sont calculés lors de l’exécution d’une requête GraphQL et se trouvent par conséquent hors de portée du filtrage basé sur JCR.

Le champ `_path` est une exception importante : il peut être utilisé efficacement pour réduire la taille de l’ensemble de résultats initial, si le contenu est structuré en conséquence (voir [Utiliser la structure de contenu](#use-content-structure)).

### Filtrage : exclusions {#filtering-exclusions}

Il existe plusieurs autres situations dans lesquelles une expression de filtre ne peut pas être évaluée au niveau JCR (et doit donc être évitée pour obtenir les meilleures performances) :

* Des expressions de filtre sur une valeur `Float` utilisant l’option de filtre `_sensitiveness`, et où `_sensitiveness` est défini sur toute autre valeur que `0.0`.

* Des expressions de filtre sur une valeur `String` utilisant l’option de filtrage `_ignoreCase`.

* Filtrage sur des valeurs `null`.

* Filtres sur des tableaux avec `_apply: ALL_OR_EMPTY`.

* Filtres sur des tableaux avec `_apply: INSTANCES`, `_instances: 0`.

* Des expressions de filtre utilisant l’opérateur `CONTAINS_NOT`.

* Filtrage des expressions sur un `Calendar`, `Date`ou `Time` qui utilisent la variable `NOT_AT` de l’opérateur.
