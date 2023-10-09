---
title: Optimisation des requêtes GraphQL.
description: Découvrez comment optimiser vos requêtes GraphQL lors du filtrage, de la pagination et du tri de vos fragments de contenu dans Adobe Experience Manager as a Cloud Service pour une diffusion de contenu sans interface.
exl-id: 47d0570b-224e-4109-b94e-ccc369d7ac5f
source-git-commit: 2ba17c43e84ad449ec858de57812f3ef82fca3e1
workflow-type: tm+mt
source-wordcount: '1940'
ht-degree: 60%

---

# Optimisation des requêtes GraphQL. {#optimizing-graphql-queries}

>[!NOTE]
>
>Avant d’appliquer ces recommandations d’optimisation, envisagez [Mise à jour des fragments de contenu pour la pagination et le tri dans le filtrage GraphQL](/help/sites-developing/headless/graphql-api/graphql-optimized-filtering-content-update.md) pour de meilleures performances.

Ces instructions sont fournies pour vous aider à éviter les problèmes de performances liés à vos requêtes GraphQL.

## Liste de contrôle GraphQL {#graphql-checklist}

La liste de contrôle suivante vise à vous aider à optimiser la configuration et l’utilisation de GraphQL dans Adobe Experience Manager (AEM) as a Cloud Service.

### Principes premiers {#first-principles}

#### Utilisation de requêtes GraphQL persistantes {#use-persisted-graphql-queries}

**Recommandation**

Il est vivement recommandé d’utiliser des requêtes GraphQL persistantes.

Les requêtes GraphQL persistantes permettent de réduire les performances d’exécution des requêtes en utilisant le réseau de diffusion de contenu (CDN). Les demandes d’applications clientes ont persisté avec des demandes de GET pour une exécution rapide prenant en charge Edge.

**Référence supplémentaire**

Voir :

* [Requêtes GraphQL persistantes](/help/sites-developing/headless/graphql-api/persisted-queries.md).
* [Apprendre à utiliser GraphQL avec AEM – Exemples de contenu et de requêtes](/help/sites-developing/headless/graphql-api/content-fragments-graphql-samples.md)

#### Installation du package d’index GraphQL {#install-graphql-index-package}

**Recommandation**

Clients utilisant GraphQL *must* installez le fragment de contenu Experience Manager avec le package d’index GraphQL. Vous pouvez ainsi ajouter la définition d’index requise selon les fonctionnalités que vous utilisez réellement. L’échec de l’installation de ce package peut entraîner des requêtes GraphQL lentes ou en échec.

Consultez les Notes de mise à jour pour connaître la version appropriée à votre Service Pack. Par exemple, pour le dernier Service Pack, voir [Installation du package d’index GraphQL pour les fragments de contenu Experience Manager](/help/release-notes/release-notes.md#install-aem-graphql-index-add-on-package) .

>[!NOTE]
>
>N’installez ce package qu’une seule fois par instance ; il n’est pas nécessaire de le réinstaller avec chaque Pack de services.

**Référence supplémentaire**
Voir :

* [Installer le package d’index GraphQL pour les fragments de contenu d’Experience Manager](/help/release-notes/release-notes.md#install-aem-graphql-index-add-on-package)

### Stratégie de mise en mémoire cache {#cache-strategy}

Plusieurs méthodes de mise en cache peuvent également être utilisées à des fins d’optimisation.

#### Activation de la mise en cache AEM Dispatcher {#enable-aem-dispatcher-caching}

**Recommandation**

[AEM Dispatcher](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/dispatcher.html?lang=fr) est le cache de premier niveau dans le service AEM, avant le cache CDN.

**Référence supplémentaire**

Voir :

* [Requêtes persistantes GraphQL - Activation de la mise en cache dans Dispatcher](/help/sites-developing/headless/graphql-api/graphql-api-content-fragments.md#graphql-persisted-queries-enabling-caching-dispatcher)

#### Utilisation d’un réseau de diffusion de contenu (CDN) {#use-cdn}

**Recommandation**

Les requêtes GraphQL et leurs réponses JSON peuvent être mises en cache si elles sont ciblées comme `GET` lors de l’utilisation d’un réseau de diffusion de contenu. En revanche, les demandes non mises en cache peuvent être très (ressources) coûteuses et lentes à traiter, avec des effets potentiellement néfastes supplémentaires sur les ressources de l’origine.

**Référence supplémentaire**

Voir :

* [Utilisation du réseau de diffusion de contenu dans AEM](https://experienceleague.adobe.com/docs/experience-manager-dispatcher/using/dispatcher.html?lang=fr#using-dispatcher-with-a-cdn)

#### Définition des en-têtes de contrôle du cache HTTP {#set-http-cache-control-headers}

**Recommandation**

Lors de l’utilisation de requêtes GraphQL persistantes avec un réseau de diffusion de contenu, il est recommandé de définir les en-têtes de contrôle du cache HTTP appropriés.

Chaque requête conservée peut avoir son propre ensemble spécifique d’en-têtes de contrôle du cache. Les en-têtes peuvent être définis sur la variable [API GRAPHQL](/help/sites-developing/headless/graphql-api/graphql-api-content-fragments.md) ou le [AEM IDE GraphiQL](/help/sites-developing/headless/graphql-api/graphiql-ide.md).

**Référence supplémentaire**

Voir :

* [Mettre en cache vos requêtes persistantes](/help/sites-developing/headless/graphql-api/persisted-queries.md#caching-persisted-queries)
<!--
* [Managing cache for your persisted queries](/help/sites-developing/headless/graphql-api/graphiql-ide.md#managing-cache)
-->

<!--
#### Use AEM GraphQL pre-caching {#use-aem-graphql-pre-caching}

**Recommendation**

This capability allows AEM to further cache content within the scope of GraphQL queries that can then be assembled as blocks in JSON output rather than line by line. 

**Further Reference**

Please contact Adobe to enable this capability for your AEM Cloud Service program and environments. 
-->

### Optimisation des requêtes GraphQL {#graphql-query-optimization}

Sur une instance AEM avec un grand nombre de fragments de contenu partageant le même modèle, les requêtes de liste GraphQL peuvent devenir coûteuses (en termes de ressources).

Ceci est dû au fait que *tous* les fragments qui partagent un modèle utilisé dans la requête GraphQL doivent être chargés en mémoire. Cela consomme à la fois du temps et de la mémoire. Le filtrage, qui peut réduire le nombre d’éléments dans le jeu de résultats (final), ne peut être appliqué qu’**après** le chargement du jeu de résultats en mémoire.

Cela peut donner l’impression que même de petits ensembles de résultats peuvent entraîner de mauvaises performances. Toutefois, en réalité, la lenteur est due à la taille du jeu de résultats initial, car il doit être géré en interne avant que le filtrage puisse être appliqué.

Pour réduire les problèmes de performances et de mémoire, ce jeu de résultats initial doit rester aussi petit que possible.

AEM propose deux méthodes d’optimisation des requêtes GraphQL :

* [Le filtrage hybride.](#use-aem-graphql-hybrid-filtering)
* La [pagination](#use-aem-graphql-pagination).

   * Le [tri](#use-graphql-sorting) n’est pas directement lié à l’optimisation, mais est lié à la pagination.

Chaque approche comporte ses propres cas d’utilisation et ses propres limites. Cette section fournit des informations sur le filtrage hybride et la pagination, ainsi que sur certaines des [bonnes pratiques](#best-practices) à utiliser dans l’optimisation des requêtes GraphQL.

#### Utiliser AEM filtrage hybride GraphQL {#use-aem-graphql-hybrid-filtering}

**Recommandation**

Le filtrage hybride combine le filtrage JCR avec le filtrage AEM.

Il applique un filtre JCR (sous la forme d’une contrainte de requête) avant de charger le jeu de résultats en mémoire pour le filtrage AEM. Cela permet de réduire le jeu de résultats chargé en mémoire, car le filtre JCR supprime les résultats superflus avant.

>[!NOTE]
>
>Pour des raisons techniques (par exemple, flexibilité, imbrication de fragments), AEM ne peut pas déléguer l’intégralité du filtrage à JCR.

Cette technique permet de conserver la flexibilité offerte par les filtres GraphQL, tout en déléguant autant de filtrage que possible à JCR.

>[!NOTE]
>
>AEM Filtrage hybride nécessite la mise à jour des fragments de contenu existants

**Référence supplémentaire**

Voir :

* [Mise à jour des fragments de contenu pour la pagination et le tri dans le filtrage GraphQL](/help/sites-developing/headless/graphql-api/graphql-optimized-filtering-content-update.md)
* [Exemple de requête avec filtrage par identifiant _tags et excluant des variations](/help/sites-developing/headless/graphql-api/content-fragments-graphql-samples.md#sample-filtering-tag-not-variations)

#### Utilisation de la pagination GraphQL {#use-aem-graphql-pagination}

**Recommandation**

Le temps de réponse des requêtes complexes, avec des jeux de résultats volumineux, peut être amélioré en segmentant les réponses en blocs à l’aide de la pagination, une norme GraphQL.

GraphQL dans AEM prend en charge deux types de pagination :

* La [pagination basée sur les limites/décalages](/help/sites-developing/headless/graphql-api/graphql-api-content-fragments.md#list-offset-limit).
Elle est utilisée pour les requêtes de liste qui se terminent par : `List` ; par exemple, `articleList`.
Pour l’utiliser, vous devez indiquer la position du premier élément à renvoyer (le `offset`) et le nombre d’éléments à renvoyer (la variable `limit`, ou la taille de la page).

* La [pagination basée sur le curseur](/help/sites-developing/headless/graphql-api/graphql-api-content-fragments.md#paginated-first-after) (représentée par `first`et `after`).
Elle fournit un ID unique pour chaque élément ; également appelé curseur.
Dans la requête, vous spécifiez le curseur du dernier élément de la page précédente, ainsi que la taille de la page (le nombre maximal d’éléments à renvoyer).

  Comme la pagination basée sur le curseur ne s’intègre pas dans les structures de données des requêtes basées sur des listes, AEM a introduit un type de requête `Paginated` ; par exemple : `articlePaginated`. Les structures et paramètres de données utilisés suivent la [Spécification de connexion du curseur GraphQL](https://relay.dev/graphql/connections.htm).

  >[!NOTE]
  >
  >AEM prend actuellement en charge la pagination (à l’aide des paramètres `after`/`first`).
  >
  >La pagination ascendante (à l’aide des paramètres `before`/`last`) n’est pas prise en charge.

**Référence supplémentaire**

Voir :

* [Exemple de requête de pagination utilisant first et after](/help/sites-developing/headless/graphql-api/content-fragments-graphql-samples.md#sample-pagination-first-after)

#### Utilisation du tri GraphQL {#use-graphql-sorting}

**Recommandation**

Également une norme GraphQL, le tri permet aux clients de recevoir du contenu JSON dans l’ordre de tri. Cela peut réduire la nécessité d’un traitement supplémentaire sur le client.

Le tri ne peut être efficace que si tous les critères de tri sont liés à des fragments de niveau supérieur.

Si l’ordre de tri inclut un ou plusieurs champs situés sur un fragment imbriqué, tous les fragments partageant le modèle de niveau supérieur doivent être chargés en mémoire. Cela a un impact négatif sur les performances.

>[!NOTE]
>
>Le tri sur les champs de niveau supérieur a également un impact (quoique faible) sur les performances.

**Référence supplémentaire**

Voir :

* [Exemple de requête avec filtrage par identifiant _tags et excluant des variations et tri par nom](/help/sites-developing/headless/graphql-api/content-fragments-graphql-samples.md#sample-filtering-tag-not-variations)

## Bonnes pratiques {#best-practices}

L’objectif principal de toutes les recommandations d’optimisation est de réduire le jeu de résultats initial. Les bonnes pratiques répertoriées ici fournissent des moyens de le faire. Elles peuvent (et doivent) être combinées.

### Filtrer sur les propriétés de niveau supérieur uniquement. {#filter-top-level-properties-only}

Actuellement, le filtrage au niveau JCR ne fonctionne que pour les fragments de niveau supérieur.

Si un filtre s’adresse aux champs d’un fragment imbriqué, AEM doit recharger (en mémoire) tous les fragments qui partagent le modèle sous-jacent.

Vous pouvez toujours optimiser ces requêtes GraphQL en combinant des expressions de filtre sur les champs de fragments de niveau supérieur et ceux des champs de fragments imbriqués avec l’[Opérateur ET](#logical-operations-in-filter-expressions).

### Utiliser la structure de contenu. {#use-content-structure}

Dans AEM, il est généralement considéré comme une bonne pratique d’utiliser la structure de référentiel pour réduire la portée du contenu à traiter.

Cette approche doit également être appliquée aux requêtes GraphQL.

Pour ce faire, appliquez un filtre sur le champ `_path` du fragment de niveau supérieur :

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

Si vous filtrez ou triez des fragments imbriqués, les requêtes paginées peuvent être lentes, car AEM peut encore devoir charger de plus grandes quantités de fragments dans la mémoire. Par conséquent, si vous combinez filtrage et pagination, tenez compte des règles de filtrage (tel qu’indiqué ci-dessus).

Pour la pagination, le tri est tout aussi important car les résultats paginés sont toujours triés, de manière explicite ou implicite.

Si vous souhaitez principalement récupérer les premières pages uniquement, il n’y a aucune différence significative entre l’utilisation des requêtes `...List` ou `...Paginated`. Cependant, si votre application souhaite lire plus d’une ou deux pages, vous devez penser à utiliser la requête `...Paginated`, car celle-ci fonctionne nettement mieux avec les pages ultérieures.

### Opérations logiques dans les expressions de filtre {#logical-operations-in-filter-expressions}

Si vous filtrez des fragments imbriqués, vous pouvez toujours appliquer un filtrage JCR en fournissant un filtre d’accompagnement sur un champ de niveau supérieur combiné à l’aide de la variable `AND` de l’opérateur.

Un cas d’utilisation type consiste à restreindre la portée de la requête à l’aide d’un filtre sur le champ `_path` du fragment de niveau supérieur, puis à filtrer les champs supplémentaires pouvant se trouver au niveau supérieur ou sur un fragment imbriqué.

Dans ce cas, les différentes expressions de filtre sont combinées avec `AND`. Par conséquent, le filtre sur `_path` peut limiter efficacement l’ensemble de résultats initial. Tous les autres filtres sur les champs de niveau supérieur peuvent également contribuer à réduire l’ensemble de résultats initial, à condition qu’ils soient combinés avec `AND`.

Les expressions de filtre combinées avec `OR` ne peuvent pas être optimisées si des fragments imbriqués sont impliqués. Les expressions `OR` ne peuvent être optimisées que si *aucun* fragment imbriqué n’est impliqué.

### Éviter le filtrage sur les champs de texte multiligne {#avoid-filtering-multiline-textfields}

Les champs d’un champ de texte multiligne (html, markdown, plaintext, json) ne peuvent pas être filtrés via une requête JCR, car le contenu de ces champs doit être calculé à la volée.

Si vous devez quand même filtrer sur un champ de texte multiligne, pensez à limiter la taille de l’ensemble de résultats initial en rajoutant des expressions de filtre supplémentaires et en les combinant avec `AND`. Une autre solution consiste à limiter la portée en filtrant sur le champ `_path`.

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

* Des expressions de filtre sur une valeur `Calendar`, `Date` ou `Time` utilisant l’opérateur `NOT_AT`.

### Minimisation de l’imbrication de fragments de contenu {#minimize-content-fragment-nesting}

L’imbrication de fragments de contenu est un excellent moyen de modéliser des structures de contenu personnalisées. Vous pouvez même avoir un fragment avec un fragment imbriqué, un fragment imbriqué, qui a...etc.

Cependant, la création d’une structure avec trop de niveaux peut augmenter les temps de traitement pour une requête GraphQL, car GraphQL doit parcourir la hiérarchie complète de tous les fragments de contenu imbriqués.

L’imbrication profonde peut également avoir des effets négatifs sur la gouvernance du contenu. En règle générale, il est recommandé de limiter l’imbrication de fragments de contenu à moins de cinq ou six niveaux.

### Ne pas générer tous les formats (éléments de texte multi-lignes) {#do-not-output-all-formats}

AEM GraphQL peut renvoyer du texte, créé dans la variable **[Texte multi-lignes](/help/assets/content-fragments/content-fragments-models.md#data-types)** type de données, dans plusieurs formats : Texte enrichi, Texte simple et Texte (Markdown).

La génération des trois formats augmente la taille de la sortie de texte dans JSON d’un facteur de trois. Cela, combiné à des jeux de résultats généralement volumineux à partir de requêtes très larges, peut produire des réponses JSON très volumineuses qui prennent donc beaucoup de temps à calculer. Il est préférable de limiter la sortie aux seuls formats de texte requis pour le rendu du contenu.

### Modification de fragments de contenu {#modifying-content-fragments}

Modifiez uniquement les fragments de contenu et leurs ressources à l’aide de l’interface utilisateur AEM ou des API. N’effectuez pas de modifications directement dans JCR.

### Test de vos requêtes {#test-your-queries}

Le traitement des requêtes GraphQL est similaire au traitement des requêtes de recherche et est beaucoup plus complexe que les requêtes API de contenu entièrement GET simples.

La planification, le test et l’optimisation attendus de vos requêtes dans un environnement contrôlé hors production sont essentiels pour réussir ultérieurement en production.
