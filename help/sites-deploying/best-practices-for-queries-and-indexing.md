---
title: Bonnes pratiques relatives aux requêtes et à l’indexation
description: Cet article fournit des instructions sur la manière d’optimiser vos index et requêtes.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
exl-id: 6dfaa14d-5dcf-4e89-993a-8d476a36d668
solution: Experience Manager, Experience Manager Sites
feature: Administering
role: Admin
source-git-commit: 48d12388d4707e61117116ca7eb533cea8c7ef34
workflow-type: tm+mt
source-wordcount: '4520'
ht-degree: 98%

---

# Bonnes pratiques relatives aux requêtes et à l’indexation{#best-practices-for-queries-and-indexing}

Avec la transition vers Oak dans AEM 6, certains changements majeurs ont été apportés à la façon dont les requêtes et les index sont gérés. Sous Jackrabbit 2, tout le contenu était indexé par défaut et pouvait être interrogé librement. Dans Oak, les index doivent être créés manuellement sous le nœud `oak:index`. Une requête peut être exécutée sans index, mais pour les jeux de données volumineux, elle l’est très lentement et risque même d’être abandonnée.

Cet article contient les informations suivantes : quand créer des index et dans quels cas ils ne sont pas nécessaires ; des astuces pour ne pas utiliser de requêtes lorsqu’elles ne sont pas indispensables ; des conseils pour optimiser les index et les requêtes.

De plus, assurez-vous de lire la [documentation Oak sur l’écriture de requêtes et d’index](/help/sites-deploying/queries-and-indexing.md). En plus du nouveau concept d’index dans AEM 6, il existe des différences syntaxiques dans les requêtes Oak qui doivent être prises en compte lors de la migration du code à partir d’une installation AEM précédente.

## Quand utiliser des requêtes {#when-to-use-queries}

### Référentiel et conception de taxonomie {#repository-and-taxonomy-design}

Lors de la conception de la taxonomie d’un référentiel, plusieurs facteurs doivent être pris en compte. Il s’agit entre autres des contrôles d’accès, de la localisation et de l’héritage des propriétés de composant et de page.

Lors de la conception d’une taxonomie qui tient compte de ces facteurs, il est également important de penser à la « traversabilité » de la conception de l’indexation. Dans ce contexte, la traversabilité est la capacité d’une taxonomie à permettre un accès prévisible au contenu en fonction de son chemin d’accès. Cela permet d’obtenir un système plus performant, plus facile à gérer qu’un système nécessitant l’exécution de nombreuses requêtes.

De plus, lors de la conception d’une taxonomie, il est important de se demander si l’ordre importe. Dans les cas où un ordre explicite n’est pas nécessaire et qu’un grand nombre de nœuds frères est attendu, il est préférable d’utiliser un type de nœud non ordonné tel que `sling:Folder` ou `oak:Unstructured`. Dans les cas où un ordre est obligatoire, `nt:unstructured` et `sling:OrderedFolder` seraient plus appropriés.

### Requêtes dans les composants {#queries-in-components}

Comme les requêtes peuvent être l’une des opérations les plus contraignantes effectuées sur un système AEM, il est préférable de les éviter dans vos composants. L’exécution de plusieurs requêtes à chaque rendu de page peut souvent dégrader les performances du système. Deux stratégies sont conseillées pour éviter l’exécution de requêtes lors du rendu de composants : le **parcours transversal des nœuds** et la **pré-récupération des résultats**.

#### Parcours transversal des nœuds {#traversing-nodes}

Si le référentiel est conçu de manière à permettre une connaissance préalable de l’emplacement des données requises, le code qui récupère ces données dans les chemins nécessaires peut être déployé sans avoir à exécuter de requêtes pour le trouver.

Par exemple, le rendu de contenu correspondant à une certaine catégorie. Une méthode consiste à organiser le contenu avec une propriété de catégorie qui peut être interrogée pour renseigner un composant qui affiche des éléments dans une catégorie.

Une meilleure approche serait de structurer ce contenu dans une taxonomie par catégorie afin qu’il puisse être récupéré manuellement.

Par exemple, si le contenu est stocké dans une taxonomie similaire à :

```xml
/content/myUnstructuredContent/parentCategory/childCategory/contentPiece
```

Le nœud `/content/myUnstructuredContent/parentCategory/childCategory` peut simplement être récupéré ; ses tâches enfants peuvent être analysées et utilisées pour le rendu du composant.

En outre, lorsque vous traitez un ensemble de résultats petit ou homogène, il peut être plus rapide de parcourir le référentiel et de rassembler les nœuds requis, plutôt que de concevoir une requête pour renvoyer le même ensemble de résultats. En règle générale, les requêtes doivent être évitées lorsque cela est possible.

#### Prérécupération des résultats {#prefetching-results}

Parfois, le contenu ou les exigences liées à un composant ne permettent pas d’utiliser le parcours transversal des nœuds comme méthode de récupération des données requises. Dans ce cas, les requêtes requises doivent être exécutées avant le rendu du composant afin que des performances optimales soient garanties pour les personnes utilisatrices finales.

Si les résultats requis pour le composant peuvent être calculés au moment de sa création et qu’aucun changement de contenu n’est attendu, la requête peut être exécutée lolrsque l’auteur ou l’autrice applique des modifications dans la boîte de dialogue.

Si les données ou le contenu changent régulièrement, la requête peut être exécutée selon un planning ou via un listener pour la mise à jour des données sous-jacentes. Ensuite, les résultats peuvent être écrits à un emplacement partagé dans le référentiel. Tous les composants qui ont besoin de ces données peuvent ensuite extraire les valeurs de ce nœud unique sans avoir à exécuter une requête lors de l’exécution.

## Optimisation des requêtes {#query-optimization}

Lors de l’exécution d’une requête qui n’utilise pas d’index, des avertissements sont consignés concernant le parcours transversal de nœuds. S’il s’agit d’une requête qui va être exécutée fréquemment, créez un index. Pour déterminer l’index qu’utilise une requête donnée, l’outil [Expliquer la requête](/help/sites-administering/operations-dashboard.md#explain-query) est recommandé. Pour plus d’informations, la journalisation DEBUG peut être activée pour les API de recherche pertinentes.

>[!NOTE]
>
>Après avoir modifié une définition d’index, l’index doit être reconstruit (réindexé). Selon la taille de l’index, cette opération peut prendre un certain temps.

Lors de l’exécution de requêtes complexes, la ventilation de la requête en plusieurs requêtes plus petites et la jonction des données par du code après coup est plus performante, dans certains cas. Dans ce cas, il est recommandé de comparer les performances des deux méthodes afin de déterminer la meilleure option pour le cas d’utilisation en question.

AEM permet d’écrire des requêtes de trois façons :

* Via les [API QueryBuilder](/help/sites-developing/querybuilder-api.md) (recommandé)
* À l’aide de XPath (recommandé)
* À l’aide de SQL2

Bien que toutes les requêtes soient converties en SQL2 avant d’être exécutées, la surcharge liée à la conversion des requêtes est minime et, par conséquent, la plus grande préoccupation lors du choix d’un langage de requête sera la lisibilité et le niveau de confort de l’équipe de développement.

>[!NOTE]
>
>Si QueryBuilder est utilisé, il détermine le nombre de résultats par défaut, opération qui est plus lente dans Oak par rapport aux versions précédentes de Jackrabbit. Pour compenser cela, vous pouvez utiliser le [paramètre guessTotal](/help/sites-developing/querybuilder-api.md#using-p-guesstotal-to-return-the-results).

### Outil Expliquer la requête {#the-explain-query-tool}

Comme pour tout langage de requête, la première étape pour optimiser une requête consiste à comprendre comment elle sera exécutée. Pour effectuer cette activité, vous pouvez utiliser l’[outil Expliquer la requête](/help/sites-administering/operations-dashboard.md#explain-query) qui fait partie du tableau de bord des opérations. Grâce à cet outil, une requête peut être expliquée. Un avertissement s’affiche si la requête entraîne des problèmes avec un référentiel volumineux, ainsi que le temps d’exécution et les index qui seront utilisés. L’outil peut également charger une liste de requêtes lentes et populaires qui peuvent ensuite être expliquées et optimisées.

### Journalisation DEBUG pour les requêtes {#debug-logging-for-queries}

Pour obtenir des informations supplémentaires sur la manière dont Oak choisit l’index à utiliser et sur la manière dont le moteur de requête exécute réellement une requête, une configuration de journalisation **DEBUG** peut être ajoutée pour les packages suivants :

* org.apache.jackrabbit.oak.plugins.index
* org.apache.jackrabbit.oak.query
* com.day.cq.search

Veillez à supprimer ce journal lorsque vous avez terminé de déboguer votre requête. Il a tendance à générer une activité importante et peut éventuellement remplir votre disque avec des fichiers journaux.

Pour plus d’informations sur la façon de procéder, reportez-vous à la [documentation sur la journalisation](/help/sites-deploying/configure-logging.md).

### Statistiques d’index {#index-statistics}

Lucene enregistre un bean JMX qui fournit des détails sur le contenu indexé, y compris la taille et le nombre de documents présents dans chacun des index.

Vous pouvez le consulter en accédant à la console JMX à l’adresse `https://server:port/system/console/jmx`.

Une fois la connexion à la console JMX effectuée, recherchez les **Statistiques de l’index Lucene** pour le trouver. D’autres statistiques d’index sont disponibles dans le MBean **IndexStats**.

Pour les statistiques de requête, consultez le MBean nommé **Statistiques de requête Oak**.

Si vous souhaitez explorer davantage vos index au moyen d’un outil comme [Luke](https://code.google.com/archive/p/luke/), vous devez utiliser la console Oak pour vider l’index depuis le `NodeStore` dans un répertoire de système de fichiers. Pour obtenir des instructions sur la façon de procéder, consultez la [documentation Lucene](https://jackrabbit.apache.org/oak/docs/query/lucene.html).

Vous pouvez également extraire les index de votre système au format JSON. Pour ce faire, accédez à `https://server:port/oak:index.tidy.-1.json`.

### Limites des requêtes {#query-limits}

**Pendant le développement**

Définissez des seuils bas pour `oak.queryLimitInMemory` (par exemple, 10 000) et Oak. `queryLimitReads` (par exemple, 5 000) et optimisez les requêtes coûteuses lorsque vous obtenez une exception UnsupportedOperationException indiquant : « la requête lit plus de x nœuds... ».

Cela permet d’éviter les requêtes gourmandes en ressources (c’est-à-dire sans support d’index ou avec un support d’index moins couvrant). Par exemple, une requête qui lit 1 million de nœuds entraînerait une augmentation des E/S et aurait un impact négatif sur les performances globales de l’application. Toute requête qui échoue en raison des limites ci-dessus doit être analysée et optimisée.

#### **Après le déploiement** {#post-deployment}

* Surveillez les journaux à la recherche de requêtes déclenchant une traversée de nœuds importante ou une consommation élevée de mémoire de tas : ``

   * `*WARN* ... java.lang.UnsupportedOperationException: The query read or traversed more than 100000 nodes. To avoid affecting other tasks, processing was stopped.`
   * Optimisez la requête pour réduire le nombre de nœuds parcourus.

* Surveillez les journaux à la recherche de requêtes déclenchant une consommation importante de mémoire de tas :

   * `*WARN* ... java.lang.UnsupportedOperationException: The query read more than 500000 nodes in memory. To avoid running out of memory, processing was stopped`
   * Optimisez la requête pour réduire la consommation de mémoire de tas.

Pour les versions AEM 6.0 à 6.2, vous pouvez ajuster le seuil du parcours transversal des nœuds à l’aide des paramètres JVM du script de démarrage AEM pour éviter que les requêtes volumineuses ne surchargent l’environnement.

Les valeurs recommandées sont les suivantes :

* `-Doak.queryLimitInMemory=500000`
* `-Doak.queryLimitReads=100000`

Dans AEM 6.3, les deux paramètres ci-dessus sont préconfigurés prêts à l’emploi et peuvent être conservés dans les paramètres OSGi QueryEngineSettings.

Plus d’informations disponibles sous : [https://jackrabbit.apache.org/oak/docs/query/query-engine.html#Slow_Queries_and_Read_Limits](https://jackrabbit.apache.org/oak/docs/query/query-engine.html#Slow_Queries_and_Read_Limits)

## Conseils pour créer des index efficaces {#tips-for-creating-efficient-indexes}

### Dois-je créer un index ? {#should-i-create-an-index}

La première question à poser lors de la création ou de l’optimisation d’index est de savoir s’ils sont nécessaires pour une situation donnée. Si vous n’exécutez la requête en question qu’une seule fois ou seulement occasionnellement et à une heure creuse pour le système par le biais d’un traitement par lot, il peut être préférable de ne pas créer d’index du tout.

Une fois un index créé, chaque fois que les données indexées sont mises à jour, l’index doit également l’être. Étant donné que cela se répercute sur les performances du système, les index ne doivent être créés que s’ils sont indispensables.

En outre, les index ne sont utiles que si les données contenues dans ceux-ci sont suffisamment uniques pour les justifier. Examinez un index dans un livre et les sujets qu’il aborde. Lors de l’indexation d’un ensemble de rubriques dans un texte, il y a généralement des centaines ou des milliers d’entrées, ce qui vous permet d’accéder rapidement à un sous-ensemble de pages pour trouver rapidement les informations que vous recherchez. Si cet index ne comportait que deux ou trois entrées, chacune indiquant plusieurs centaines de pages, l’index ne serait pas utile. Ce même concept s’applique aux index des bases de données. S’il n’y a que quelques valeurs uniques, l’index est inutile. Cela étant, s’il est trop volumineux, l’index risque d’être inutile. Pour consulter les statistiques d’index, reportez-vous à [Statistiques d’index](/help/sites-deploying/best-practices-for-queries-and-indexing.md#index-statistics) ci-dessus.

### Index Lucene ou de propriété ? {#lucene-or-property-indexes}

Les index Lucene ont été introduits dans Oak 1.0.9 et proposent de puissantes optimisations par rapport aux index de propriété introduits lors du lancement initial d’AEM 6. Lorsque vous décidez d’utiliser des index Lucene ou des index de propriété, veuillez tenir compte des points suivants :

* Les index Lucene proposent bien plus de fonctionnalités que les index de propriété. Par exemple, un index de propriété ne peut indexer qu’une seule propriété, tandis qu’un index Lucene peut en inclure plusieurs. Pour plus d’informations sur toutes les fonctionnalités disponibles dans les index Lucene, veuillez consulter la [documentation](https://jackrabbit.apache.org/oak/docs/query/lucene.html).
* Les index Lucene sont asynchrones. Bien que cela représente une amélioration considérable des performances, cela peut également entraîner un délai entre le moment où les données sont écrites dans le référentiel et celui où l’index est mis à jour. S’il est essentiel que les requêtes renvoient des résultats 100 % exacts, un index de propriété est requis.
* Étant asynchrones, les index Lucene ne peuvent pas imposer des contraintes d’unicité. Si leur utilisation est un impératif, un index de propriété doit être créé.

En règle générale, il est recommandé d’utiliser les index Lucene à moins qu’il ne soit absolument nécessaire d’utiliser les index de propriété afin de bénéficier de performances et de flexibilité accrues.

### Indexation Solr {#solr-indexing}

AEM prend également en charge l’indexation Solr par défaut. L’outil prend en charge la recherche de texte intégral, mais aussi tout type de requête JCR. Solr doit être pris en compte lorsque les instances AEM n’ont pas la capacité du processeur pour gérer le nombre de demandes requises dans les déploiements intensifs en recherche, tels que les sites web pilotés par la recherche avec un grand nombre d’utilisateurs et d’utilisatrices en même temps. Alternativement, Solr peut être implémenté dans une approche basée sur un robot d’exploration pour tirer parti de certaines des fonctionnalités les plus avancées de la plateforme.

Les index Solr peuvent être configurés pour être exécutés de manière intégrée sur le serveur AEM pour les environnements de développement ou peuvent être déchargés sur une instance distante afin d’améliorer l’évolutivité de la recherche dans les environnements de production et d’évaluation. Bien que la recherche de déchargement améliore l’évolutivité, elle introduit également une latence et elle n’est pour cette raison pas recommandée sauf si nécessaire. Pour plus d’informations sur la configuration de l’intégration Solr et sur la création d’index Solr, voir [Documentation sur l’indexation et les requêtes Oak](/help/sites-deploying/queries-and-indexing.md#the-solr-index).

>[!NOTE]
>
>En adoptant l’approche de recherche Solr intégrée, il est possible de décharger l’indexation sur un serveur Solr. Si les fonctionnalités plus avancées du serveur Solr sont utilisées selon une approche de robot d’exploration, un travail de configuration supplémentaire est nécessaire.

L’inconvénient de cette méthode est que, bien que les requêtes AEM respectent par défaut les listes de contrôle d’accès et masquent ainsi les résultats auxquels les utilisateurs et utilisatrices n’ont pas accès, l’externalisation de la recherche sur un serveur Solr ne prend pas en charge cette fonctionnalité. Si la recherche doit être externalisée de cette manière, une attention particulière doit être accordée à ce que les personnes utilisatrices ne reçoivent pas de résultats qu’elles ne devraient pas voir.

Les cas d’utilisation potentiels où cette méthode peut être appropriée sont les cas où les données de recherche provenant de plusieurs sources peuvent nécessiter un regroupement. Prenons l’exemple d’un site hébergé sur AEM et d’un second site hébergé sur une plateforme tierce. Solr peut être configuré pour analyser le contenu des deux sites et le stocker dans un index agrégé. Cela permet des recherches intersite.

### Observations relatives à la conception {#design-considerations}

La documentation Oak pour les index Lucene répertorie plusieurs points à prendre en compte lors de la conception des index :

* Si la requête utilise des restrictions de chemin différentes, utilisez `evaluatePathRestrictions`. Cela permet à la requête de renvoyer le sous-ensemble de résultats sous le chemin spécifié, puis de les filtrer selon la requête. Sinon, la requête recherchera tous les résultats correspondant aux paramètres de requête du référentiel, puis les filtrera en fonction du chemin d’accès.
* Si la requête utilise le tri, définissez une propriété explicite pour la propriété triée et définissez `ordered` sur `true`. Cela permet d’ordonner les résultats en tant que tels dans l’index et d’économiser sur les opérations de tri coûteuses au moment de l’exécution de la requête.

* Ne placez que ce qui est nécessaire dans l’index. L’ajout de fonctionnalités ou de propriétés inutiles entraîne la croissance de l’index et ralentit les performances.
* Dans un index de propriété, un nom de propriété unique contribue à réduire la taille de l’index, mais dans le cas des index Lucene, l’utilisation de `nodeTypes` et `mixins` est conseillée pour obtenir des index cohérents. L’interrogation d’une propriété `nodeType` ou `mixin` spécifique est plus performante que celle d’une propriété `nt:base`. Si vous suivez cette approche, définissez `indexRules` pour les `nodeTypes` en question.

* Si vos requêtes sont exécutées uniquement sous certains chemins, créez ces index sous ces chemins. Il n’est pas nécessaire que les index se trouvent à la racine du référentiel.
* Utilisez un seul index lorsque toutes les propriétés indexées sont liées pour permettre à Lucene d’évaluer autant de restrictions de propriété que possible en mode natif. En outre, une requête n’utilise qu’un seul index, même lors de l’exécution d’une jointure.

### CopyOnRead {#copyonread}

Dans les cas où le `NodeStore` est stocké à distance, une option appelée `CopyOnRead` peut être activée. L’option entraîne l’écriture de l’index distant sur le système de fichiers local lors de sa lecture. Cela peut contribuer à améliorer les performances des requêtes qui sont souvent exécutées sur ces index distants.

Cela peut être configuré dans la console OSGi sous le service **LuceneIndexProvider** et est activé par défaut à partir de Oak 1.0.13.

### Suppression des index {#removing-indexes}

Lors de la suppression d’un index, il est toujours recommandé de le désactiver temporairement en définissant la propriété `type` sur `disabled` et de vérifier que votre application fonctionne correctement avant de le supprimer. Un index n’est pas mis à jour lorsqu’il est désactivé. Il se peut donc qu’il ne dispose pas du contenu correct s’il est réactivé, et qu’il doive être réindexé.

Après la suppression d’un index de propriété sur une instance TarMK, la compression doit être exécutée pour récupérer tout l’espace disque utilisé. Pour les index Lucene, le contenu réel de l’index se trouve dans le BlobStore. Une récupération de l’espace mémoire de magasin de données est donc nécessaire.

Lors de la suppression d’un index sur une instance MongoDB, le coût de suppression est proportionnel au nombre de nœuds dans l’index. La suppression d’un index volumineux pouvant entraîner des problèmes, la méthode recommandée consiste à désactiver l’index et à le supprimer uniquement pendant une fenêtre de maintenance, à l’aide d’un outil tel que **oak-mongo.js**. Notez que cette méthode ne doit pas être utilisée pour le contenu de nœud normal, car elle peut introduire des incohérences de données.

>[!NOTE]
>
>Pour plus d’informations sur oak-mongo.js, consultez [Outils de ligne de commande](https://jackrabbit.apache.org/oak/docs/command_line.html) de la documentation Oak.

### Aide-mémoire sur les requêtes JCR {#jcrquerycheatsheet}

Pour prendre en charge la création de requêtes JCR et de définitions d’index efficaces, l’[Aide-mémoire sur les requêtes JCR](assets/JCR_query_cheatsheet-v1.1.pdf) peut être téléchargé et utilisé comme référence pendant le développement. Il contient des exemples de requêtes pour QueryBuilder, XPath et SQL-2, couvrant plusieurs scénarios qui se comportent différemment en termes de performances des requêtes. Il fournit également des recommandations sur la version ou la personnalisation d’index Oak. Le contenu de cet aide-mémoire s’applique à AEM 6.5 et à AEM as a Cloud Service.

## Réindexation {#re-indexing}

Cette section présente les **seules** raisons valables qui justifient une réindexation des index Oak.

En dehors des raisons exposées ci-dessous, la réindexation des index Oak ne change **pas** le comportement et ne résout aucun problème, mais augmente indiscutablement la charge sur AEM.

La réindexation des index Oak doit être évitée à moins d’être justifiée par l’une des raisons décrites dans les tableaux ci-dessous.

>[!NOTE]
>
>Avant de consulter les tableaux ci-dessous pour déterminer si une réindexation est utile, vérifiez **toujours** que :
>
>* la requête est correcte ;
>* la requête résout l’index prévu (en utilisant [Expliquer la requête](/help/sites-administering/operations-dashboard.md#diagnosis-tools)) ;
>* le processus d’indexation est terminé.
>

### Modifications de la configuration de l’index Oak {#oak-index-configuration-changes}

Les seules conditions acceptables pour la réindexation des index Oak sont si la configuration d’un index Oak a changé.

*La réindexation doit toujours être envisagée en tenant compte de son impact sur les performances globales d’AEM et être réalisée pendant les périodes de faible activité ou de maintenance.*

Problèmes possibles et solutions :

* [Modification de la définition d’un index de propriété](#property-index-definition-change)
* [Modification de la définition d’un index Lucene](#lucene-index-definition-change)

#### Modification de la définition d’un index de propriété {#property-index-definition-change}

* S’applique pour/si :

   * Toutes les versions d’Oak
   * Uniquement les [index de propriété](https://jackrabbit.apache.org/oak/docs/query/property-index.html)

* Symptômes :

   * Nœuds existants avant la mise à jour de la définition de l’index de propriété manquants dans les résultats

* Comment vérifier :

   * Déterminez si des noeuds manquants ont été créés/modifiés avant le déploiement de la définition d’index mise à jour.
   * Vérifiez les propriétés `jcr:created` ou `jcr:lastModified` de tous les nœuds manquants par rapport à l’heure de modification de l’index.

* Mode de résolution :

   * [Réindexez](/help/sites-deploying/best-practices-for-queries-and-indexing.md#how-to-re-index) l’index Lucene.
   * Vous pouvez également toucher (effectuer une opération d’écriture bénigne) les nœuds manquants.

      * Requiert des touches manuelles ou du code personnalisé
      * Nécessite que le jeu de nœuds manquants soit connu.
      * Nécessite de modifier toute propriété sur le nœud.

#### Modification de la définition d’un index Lucene {#lucene-index-definition-change}

* S’applique pour/si :

   * Toutes les versions d’Oak
   * Seulement les [index Lucene](https://jackrabbit.apache.org/oak/docs/query/lucene.html)

* Symptômes :

   * L’index Lucene ne contient pas les résultats attendus.
   * Les résultats de requête ne reflètent pas le comportement attendu de la définition de l’index.
   * Le plan de requête ne signale pas la sortie attendue en fonction de la définition de l’index.

* Comment vérifier :

   * Vérifiez que la définition de l’index a été modifiée à l’aide du MBean JMX de statistiques sur les index Lucene (LuceneIndex), méthode `diffStoredIndexDefinition`.

* Mode de résolution :

   * Versions d’Oak antérieures à la version 1.6 :

      * [Réindexez](#how-to-re-index) l’index Lucene.

   * Oak versions 1.6 et ultérieures

      * Si le contenu existant n’est pas concerné par les modifications, seule une actualisation est nécessaire.

         * [Actualisez](https://jackrabbit.apache.org/oak/docs/query/lucene.html#stored-index-definition) l’index Lucene en définissant [oak:queryIndexDefinition]@refresh=true.

      * Sinon, [réindexez](#how-to-re-index) l’index Lucene.

         * Remarque : l’état de l’index de la dernière bonne réindexation (ou l’indexation initiale) est utilisé jusqu’au déclenchement d’une nouvelle réindexation.

### Erreurs et situations exceptionnelles {#erring-and-exceptional-situations}

Le tableau suivant décrit les seules situations d’erreur et d’exception acceptables dans lesquelles la réindexation des index Oak résoudra le problème.

Si un problème qui ne correspond pas aux critères décrits ci-dessous se produit sur AEM, **ne réindexez pas** les index, car cela ne résoudra pas le problème.

Problèmes possibles et solutions :

* [Le binaire de l’index Lucene est manquant](#lucene-index-binary-is-missing)
* [Le binaire de l’index Lucene est corrompu](#lucene-index-binary-is-corrupt)

#### Le binaire de l’index Lucene est manquant {#lucene-index-binary-is-missing}

* S’applique pour/si :

   * Toutes les versions d’Oak
   * Seulement les [index Lucene](https://jackrabbit.apache.org/oak/docs/query/lucene.html)

* Symptômes :

   * L’index Lucene ne contient pas les résultats attendus.

* Comment vérifier :

   * Le fichier journal des erreurs contient une exception indiquant qu’un fichier binaire de l’index Lucene est manquant.

* Mode de résolution :

   * Effectuez une vérification du référentiel de traversée ; par exemple :

     [http://localhost:4502/system/console/repositorycheck](http://localhost:4502/system/console/repositorycheck)

     La traversée du référentiel détermine si d’autres fichiers binaires (à part les fichiers lucene) sont manquants.

   * Si des binaires autres que les index Lucene sont manquants, restaurez à partir de la sauvegarde.
   * Sinon, [réindexez](#how-to-re-index) *tous* les index Lucene.
   * Remarque :

     Cette condition indique qu’un magasin de données mal configuré peut entraîner l’absence de TOUT fichier binaire (par exemple, les fichiers binaires des ressources).

     Dans ce cas, restaurez la dernière version fonctionnelle connue du référentiel pour récupérer tous les binaires manquants.

#### Le binaire de l’index Lucene est corrompu {#lucene-index-binary-is-corrupt}

* S’applique pour/si :

   * Toutes les versions d’Oak
   * Seulement les [index Lucene](https://jackrabbit.apache.org/oak/docs/query/lucene.html)

* Symptômes :

   * L’index Lucene ne contient pas les résultats attendus.

* Comment vérifier :

   * La requête `AsyncIndexUpdate` (toutes les cinq secondes) échoue avec une exception dans le fichier error.log :

     `...a Lucene index file is corrupt...`

* Mode de résolution :

   * Supprimez la copie locale de l’index Lucene.

      1. Arrêtez AEM.
      1. Supprimez la copie locale de l’index Lucene dans `crx-quickstart/repository/index`.
      1. Redémarrez AEM.

   * Si cela ne résout pas le problème et que les exceptions `AsyncIndexUpdate` persistent, alors :

      1. [Réindexez](#how-to-re-index) l’index erroné.
      1. Ouvrez également un ticket auprès de l’[assistance d’Adobe](https://helpx.adobe.com/fr/support.html).

### Réindexation {#how-to-re-index}

>[!NOTE]
>
>Dans AEM 6.5, la méthode [oak-run.jar constitue la SEULE méthode prise en charge](/help/sites-deploying/indexing-via-the-oak-run-jar.md#reindexingapproachdecisiontree) pour effectuer une réindexation sur des référentiels MongoMK ou RDBMK.

#### Réindexation des index de propriété {#re-indexing-property-indexes}

* Utilisez [oak-run.jar](/help/sites-deploying/oak-run-indexing-usecases.md#usecase3reindexing) pour réindexer l’index de propriété.
* Définissez la propriété async-reindex sur true dans l’index de propriété.

   * `[oak:queryIndexDefinition]@reindex-async=true`

* Réindexez l’index de propriété de manière asynchrone à l’aide de la console web via le MBean **PropertyIndexAsyncReindex** ;

  par exemple,

  [http://localhost:4502/system/console/jmx/org.apache.jackrabbit.oak%3Aname%3Dasync%2Ctype%3DPropertyIndexAsyncReindex](http://localhost:4502/system/console/jmx/org.apache.jackrabbit.oak%3Aname%3Dasync%2Ctype%3DPropertyIndexAsyncReindex)

#### Réindexation des index de propriété Lucene {#re-indexing-lucene-property-indexes}

* Utilisez [oak-run.jar pour réindexer](/help/sites-deploying/oak-run-indexing-usecases.md#usecase3reindexing) l’index de propriété Lucene.
* Définissez la propriété async-reindex sur true dans l’index de propriété Lucene.

   * `[oak:queryIndexDefinition]@reindex-async=true`

>[!NOTE]
>
>La section précédente résume et encadre les conseils de réindexation Oak à partir de la [documentation Apache Oak](https://jackrabbit.apache.org/oak/docs/query/indexing.html#reindexing) dans le contexte d’AEM.

### Pré-extraction de texte des fichiers binaires {#text-pre-extraction-of-binaries}

La pré-extraction du texte est le processus d’extraction et de traitement du texte des binaires, directement à partir du magasin de données par le biais d’un processus isolé, et d’exposition directe du texte extrait aux réindexations ultérieures des index Oak.

* La pré-extraction de texte Oak est recommandée pour l’indexation ou la réindexation des index Lucene sur les référentiels contenant de grands volumes de fichiers (binaires) qui comportent du texte extractible (par exemple, des PDF, des documents Word, des PPT, TXT, etc.) pouvant faire l’objet d’une recherche en texte intégral via des index Oak déployés ; par exemple, `/oak:index/damAssetLucene`.
* La pré-extraction de texte ne bénéficie qu’à l’indexation/la réindexation des index Lucene et NON PAS aux index de propriété Oak, étant donné que les index de propriété n’extraient pas de texte à partir de fichiers binaires.
* La pré-extraction de texte a un impact positif élevé lors de la réindexation d’un texte intégral de fichiers binaires lourds en texte (PDF, Doc, TXT, etc.), où, en tant que référentiel d’images, les performances ne seront pas les mêmes puisque les images ne contiennent pas de texte extractible.
* La pré-extraction de texte effectue l’extraction du texte associé à la recherche de texte intégral de manière très efficace et l’expose au processus d’indexation/de réindexation Oak d’une manière très efficace à utiliser.

#### Quand la pré-extraction de texte PEUT-elle être utilisée ? {#when-can-text-pre-extraction-be-used}

Réindexation d’un index Lucene **existant** avec extraction binaire activée

* La réindexation traite **tous** les contenus candidats du référentiel. Lorsque les binaires desquels extraire du texte intégral sont nombreux ou complexes, une charge de calcul accrue destinée à effectuer l’extraction de texte intégral est placée sur AEM. La pré-extraction de texte déplace le « travail coûteux en calcul » de l’extraction de texte vers un processus isolé qui accède directement au magasin de données AEM, en évitant la surcharge et le conflit de ressources dans AEM.

Prise en charge du déploiement d’un **nouvel** index Lucene vers AEM avec l’extraction binaire activée

* Lorsqu’un nouvel index (avec extraction de binaires activée) est déployé dans AEM, Oak indexe automatiquement tout le contenu candidat sur l’indexation en texte intégral asynchrone suivante. Pour les mêmes raisons que celles décrites dans la réindexation ci-dessus, cela peut entraîner une charge excessive sur AEM.

#### Dans quels cas la pré-extraction de texte NE peut-elle PAS être utilisée ? {#when-can-text-pre-extraction-not-be-used}

La pré-extraction de texte ne peut pas être utilisée pour un nouveau contenu ajouté au référentiel, et elle n’est pas non plus nécessaire.

Le nouveau contenu est ajouté au référentiel. Il sera indexé de manière naturelle et incrémentielle par le processus d’indexation de texte intégral asynchrone (par défaut, toutes les 5 secondes).

Si AEM fonctionne normalement, par exemple en chargeant des ressources via l’IU web ou en programmant l’ingestion des ressources, AEM indexe automatiquement et progressivement le nouveau contenu binaire en texte intégral. Étant donné que la quantité de données est incrémentielle et relativement petite (environ la quantité de données pouvant être conservées dans le référentiel en 5 secondes), AEM peut effectuer l’extraction de texte intégral à partir des fichiers binaires pendant l’indexation sans affecter les performances globales du système.

#### Conditions préalables à l’utilisation de la pré-extraction de texte {#prerequisites-to-using-text-pre-extraction}

* Vous réindexerez un index Lucene qui effectue une extraction binaire en texte intégral ou déploiera un nouvel index qui indexera les fichiers binaires en texte intégral du contenu existant.
* Le contenu (fichiers binaires) à partir duquel pré-extraire le texte doit se trouver dans le référentiel.
* Une fenêtre de maintenance pour générer le fichier CSV ET effectuer la réindexation finale.
* Versions d’Oak : 1.0.18 et version ultérieure, 1.2.3 et version ultérieure
* [oak-run.jar](https://mvnrepository.com/artifact/org.apache.jackrabbit/oak-run/)version 1.7.4+
* Un dossier/partage de système de fichiers pour stocker le texte extrait accessible depuis les instances AEM d’indexation

   * La configuration OSGi de pré-extraction de texte nécessite un chemin d’accès au système de fichiers vers les fichiers texte extraits. Ils doivent donc être accessibles directement à partir de l’instance AEM (lecteur local ou montage de partage de fichiers).

#### Comment pré-extraire du texte {#how-to-perform-text-pre-extraction}

>[!NOTE]
>
>***Les commandes oak-run.jar décrites ci-dessous sont entièrement énumérées sur [https://jackrabbit.apache.org/oak/docs/query/pre-extract-text.html](https://jackrabbit.apache.org/oak/docs/query/pre-extract-text.html)***
>
>Le schéma ci-dessus et les étapes ci-dessous servent à expliquer et à compléter les étapes de pré-extraction de texte technique décrites dans la documentation d’Apache Oak.

![Flux de processus de pré-extraction de texte](assets/chlimage_1-139.png)

**Génération de la liste du contenu à pré-extraire**

*Exécutez l’étape 1 (a-b) au cours d’une fenêtre de maintenance/période de faible utilisation lorsque le magasin de nœuds est parcouru pendant cette opération, ce qui peut entraîner une charge importante sur le système.*

1a. Exécutez `oak-run.jar --generate` pour créer une liste de nœuds dont le texte sera pré-extrait.

1b. La liste des nœuds (1a) est stockée dans le système de fichiers sous la forme d’un fichier CSV.

L’intégralité du magasin de nœuds est parcourue transversalement (comme spécifié par les chemins dans la commande oak-run) chaque fois que `--generate` est exécuté et qu’un **nouveau** fichier CSV est créé. Le fichier CSV **n’est pas** réutilisé entre les exécutions discrètes du processus de pré-extraction de texte (étapes 1 et 2).

**Pré-extraction de texte dans le système de fichiers**

*L’étape 2 (a-c) peut être exécutée pendant le fonctionnement normal d’AEM, car elle interagit uniquement avec le magasin de données.*

2a. Exécutez `oak-run.jar --tika` pour pré-extraire le texte des nœuds binaires énumérés dans le fichier CSV généré dans (1b).

2b. Le processus lancé à l’étape (2a) accède directement aux nœuds binaires définis dans le fichier CSV du magasin de données et extrait le texte.

2c. Le texte extrait est stocké sur un système de fichiers dans un format que peut ingérer le processus de réindexation Oak (3a).

Le texte pré-extrait est identifié dans le fichier CSV par l’empreinte binaire. Si le fichier binaire est le même, le même texte pré-extrait peut être utilisé sur les instances AEM. Comme la publication AEM est généralement un sous-ensemble de la création AEM, le texte pré-extrait de la création AEM peut souvent être utilisé pour réindexer également la publication AEM (en supposant que la publication AEM dispose d’un accès système de fichiers aux fichiers texte extraits).

Le texte pré-extrait peut être ajouté de manière incrémentielle au fil du temps. La pré-extraction du texte ignore l’extraction pour les binaires précédemment extraits. Il est donc recommandé de conserver le texte pré-extrait au cas où la réindexation devrait se reproduire dans le futur (en supposant que le contenu extrait ne soit pas trop volumineux. Si c’est le cas, évaluez la compression du contenu entre temps, car le texte se compresse bien).

**Réindexation des index Oak, en recherchant le texte intégral à partir de fichiers texte extraits**

*Exécutez la réindexation (étapes 3a-b) au cours d’une période de maintenance ou de faible utilisation, car le magasin de nœuds est parcouru pendant cette opération, ce qui peut entraîner une charge importante sur le système.*

3a. La [réindexation](#how-to-re-index) des index Lucene est appelée dans AEM.

3b. La configuration OSGi d’Apache Jackrabbit Oak DataStore PreExtractedTextProvider (configurée pour pointer sur le texte extrait via un chemin de système de fichiers) indique à Oak d’extraire le texte intégral des fichiers extraits et évite de toucher directement aux données stockées dans le référentiel et de les traiter.
