---
title: Résolution des problèmes de lenteur des requêtes
seo-title: Troubleshooting Slow Queries
description: Découvrez comment résoudre les problèmes de requêtes lentes dans Adobe Experience Manager.
seo-description: null
uuid: ad09546a-c049-44b2-99a3-cb74ee68f040
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: c01e42ff-e338-46e6-a961-131ef943ea91
exl-id: 3405cdd3-3d1b-414d-9931-b7d7b63f0a6f
source-git-commit: b703f356f9475eeeafb1d5408c650d9c6971a804
workflow-type: tm+mt
source-wordcount: '2269'
ht-degree: 99%

---

# Résolution des problèmes de lenteur des requêtes{#troubleshooting-slow-queries}

## Classifications des requêtes lentes {#slow-query-classifications}

Il existe trois principales classifications des requêtes lentes dans AEM, répertoriées par sévérité :

1. **Requêtes sans index**

   * Requêtes qui **ne se basent pas** sur un index et parcourent le contenu du JCR pour collecter des résultats.

1. **Requêtes mal restreintes (ou au périmètre mal défini)**

   * Requêtes qui se réfèrent à un index, mais qui doivent parcourir toutes les entrées de l’index pour collecter les résultats.

1. **Requêtes avec un ensemble de résultats volumineux**

   * Requêtes qui renvoient un grand nombre de résultats.

Les deux premières classifications de requêtes (sans index et insuffisamment restreintes) sont lentes. Elles sont lentes, car elles obligent le moteur de requête Oak à inspecter chaque résultat **potentiel** (nœud de contenu ou entrée d’index) afin d’identifier celui qui fait partie de l’ensemble **actuel** de résultats.

L’inspection de chaque résultat potentiel est ce qu’on appelle le parcours.

Puisque chaque résultat potentiel doit être inspecté, le coût de détermination de l’ensemble actuel de résultats augmente de façon linéaire avec le nombre de résultats potentiels.

En ajoutant des restrictions à la requête et en affinant les index, les données d&#39;index peuvent être stockées dans un format optimisé pour permettre une récupération rapide des résultats et réduire ou éliminer la nécessité d&#39;inspecter linéairement les ensembles de résultats potentiels.

Dans AEM 6.3, par défaut, lorsqu’un parcours de 100 000 est atteint, la requête échoue et renvoie une exception. Cette limite n’existe pas par défaut dans les versions antérieures à AEM 6.3, mais elle peut être définie via la configuration OSGi des paramètres du moteur de requête Apache Jackrabbit et le bean JMX QueryEngineSettings (propriété LimitReads).

### Détection de requêtes sans index {#detecting-index-less-queries}

#### Pendant le développement {#during-development}

Expliquez **toutes** les requêtes et assurez-vous que leurs plans de requête ne contiennent pas l’explication **/&amp;ast; traverse**. Exemple de traversée du plan de requête :

* **PLAN :** `[nt:unstructured] as [a] /* traverse "/content//*" where ([a].[unindexedProperty] = 'some value') and (isdescendantnode([a], [/content])) */`

#### Après le déploiement {#post-deployment}

* Contrôlez le journal `error.log` à la recherche de requêtes de traversée sans index :

   * `*INFO* org.apache.jackrabbit.oak.query.QueryImpl Traversal query (query without index) ... ; consider creating and index`
   * Ce message n’est consigné que si aucun index n’est disponible et si la requête parcourt potentiellement de nombreux nœuds. Les messages ne sont pas consignés si un index est disponible, mais il s’agit d’un parcours de petite taille, il est donc rapide.

* Rendez-vous sur la console des opérations [Performances des requêtes](/help/sites-administering/operations-dashboard.md#query-performance) d’AEM et [expliquez](/help/sites-administering/operations-dashboard.md#explain-query) les requêtes lentes en recherchant les explications de traversée ou de requête sans index.

### Détection de requêtes insuffisamment restreintes {#detecting-poorly-restricted-queries}

#### Pendant le développement {#during-development-1}

Expliquez toutes les requêtes et assurez-vous qu’elles se résolvent sur un index réglé pour correspondre aux restrictions de propriété de la requête.

* Dans une couverture de plan de requête idéale, `indexRules` est défini pour toutes les restrictions de propriété et, au minimum, pour les restrictions de propriété les plus strictes de la requête.
* Les requêtes qui trient les résultats doivent être résolues sur un index de propriété Lucene avec des règles d’index pour les propriétés de tri qui définissent `orderable=true.`.

#### Par exemple, l’index `cqPageLucene` par défaut ne comprend pas de règle d’index pour `jcr:content/cq:tags`. {#for-example-the-default-cqpagelucene-does-not-have-an-index-rule-for-jcr-content-cq-tags}

Avant d’ajouter la règle d’index cq:tags

* **Règle d’index cq:tags**

   * N’existe pas par défaut

* **Requête Query Builder**

  ```js
  type=cq:Page
  property=jcr:content/cq:tags
  property.value=my:tag
  ```

* **Plan de requête**

  `[cq:Page] as [a] /* lucene:cqPageLucene(/oak:index/cqPageLucene) *:* where [a].[jcr:content/cq:tags] = 'my:tag' */`

Cette requête est résolue sur l’index `cqPageLucene`. Cependant, étant donné qu’il n’existe pas de règle d’index de propriété pour `jcr:content` ou `cq:tags`, lorsque cette restriction est évaluée, chaque enregistrement de l’index `cqPageLucene` est vérifié afin de déterminer une correspondance. Cela signifie que si l’index contient un million de nœuds `cq:Page`, alors un million d’enregistrements sont vérifiés pour déterminer l’ensemble de résultats.

Après avoir ajouté la règle d’index cq:tags

* **Règle d’index cq:tags**

  ```js
  /oak:index/cqPageLucene/indexRules/cq:Page/properties/cqTags
  @name=jcr:content/cq:tags
  @propertyIndex=true
  ```

* **Requête Query Builder**

  ```js
  type=cq:Page
  property=jcr:content/cq:tags
  property.value=myTagNamespace:myTag
  ```

* **Plan de requête**

  `[cq:Page] as [a] /* lucene:cqPageLucene(/oak:index/cqPageLucene) jcr:content/cq:tags:my:tag where [a].[jcr:content/cq:tags] = 'my:tag' */`

L’ajout de la règle d’index pour `jcr:content/cq:tags` dans l’index `cqPageLucene` permet de stocker les données `cq:tags` dans un format optimisé.

Lors de l’exécution d’une requête avec la restriction `jcr:content/cq:tags`, l’index peut rechercher des résultats en fonction de leur valeur. Cela signifie que si 100 nœuds `cq:Page` ont `myTagNamespace:myTag` comme valeur, seuls ces 100 résultats sont renvoyés. Les 999 000 autres résultats sont exclus des contrôles de restriction, ce qui améliore les performances d’un facteur 10 000.

Plus de restrictions de requête réduisent les ensembles de résultats éligibles et améliorent encore l’optimisation des requêtes.

De même, en l’absence de règle d’index supplémentaire pour la propriété `cq:tags`, même une requête en texte intégral avec une restriction définie sur `cq:tags` s’avérerait peu performante, dans la mesure où les résultats de l’index renverraient toutes les correspondances en texte intégral. La restriction définie sur cq:tags serait filtrée par la suite.

Une autre cause de filtrage post-index est le manque de prise en compte des listes de contrôle d’accès pendant le développement. Veillez à ce que la requête ne renvoie pas des chemins susceptibles d’être inaccessibles à l’utilisateur ou l’utilisatrice. Pour ce faire, vous pouvez améliorer la structure du contenu et fournir une restriction de chemin d’accès appropriée sur la requête.

Une méthode utile pour identifier si l’index Lucene renvoie de nombreux résultats pour retourner un petit sous-ensemble en tant que résultat de la requête consiste à activer les journaux DEBUG pour `org.apache.jackrabbit.oak.plugins.index.lucene.LucenePropertyIndex`. Cela vous permet de voir combien de documents sont en train d&#39;être chargés à partir de l’index. Le nombre de résultats finaux par rapport au nombre de documents chargés ne devrait pas être disproportionné. Pour plus d’informations, consultez la section [Journalisation](/help/sites-deploying/configure-logging.md).

#### Après le déploiement {#post-deployment-1}

* Contrôlez le `error.log` à la recherche de requêtes de traversée :

   * `*WARN* org.apache.jackrabbit.oak.spi.query.Cursors$TraversingCursor Traversed ### nodes ... consider creating an index or changing the query`

* Rendez-vous sur la console des opérations [Performances des requêtes](/help/sites-administering/operations-dashboard.md#query-performance) d’AEM et [expliquez](/help/sites-administering/operations-dashboard.md#explain-query) les requêtes lentes en recherchant les plans de requête qui ne résolvent pas les restrictions de propriété de requête sur des règles de propriété d’index.

### Détection de requêtes comportant un ensemble de résultats volumineux {#detecting-large-result-set-queries}

#### Pendant le développement {#during-development-2}

Définissez des seuils bas pour oak.queryLimitInMemory (par exemple, 10 000) et oak.queryLimitReads (par exemple, 5 000) et optimisez la requête consommatrice lorsque vous recnontrez une exception UnsupportedOperationException qui indique que « La requête a lu plus de x nœuds...».

La définition de seuils bas permet d’éviter les requêtes gourmandes en ressources (c’est-à-dire sans support d’index ou avec un support d’index moins couvrant). Par exemple, une requête qui lit un million de nœuds entraînerait une augmentation des E/S et aurait un impact négatif sur les performances globales de l’application. Ainsi, toute requête qui échoue en raison des limites ci-dessus doit être analysée et optimisée.

#### Après le déploiement {#post-deployment-2}

* Surveillez les journaux à la recherche de requêtes déclenchant une traversée de nœuds importante ou une consommation élevée de mémoire de tas : ``

   * `*WARN* ... java.lang.UnsupportedOperationException: The query read or traversed more than 100000 nodes. To avoid affecting other tasks, processing was stopped.`
   * Optimisez la requête afin de réduire le nombre de nœuds parcourus.

* Surveillez les journaux à la recherche de requêtes déclenchant une consommation importante de mémoire de tas :

   * `*WARN* ... java.lang.UnsupportedOperationException: The query read more than 500000 nodes in memory. To avoid running out of memory, processing was stopped`
   * Optimisez la requête pour réduire la consommation de mémoire de tas.

Pour les versions d’AEM 6.0 à 6.2, vous pouvez ajuster le seuil du parcours transversal des nœuds à l’aide des paramètres JVM du script de démarrage AEM pour éviter que les requêtes volumineuses ne surchargent l’environnement. Les valeurs recommandées sont les suivantes :

* `-Doak.queryLimitInMemory=500000`
* `-Doak.queryLimitReads=100000`

Dans AEM 6.3, les paramètres ci-dessus sont préconfigurés par défaut et peuvent être modifiés dans les paramètres OSGi QueryEngineSettings.

Plus d’informations disponibles sous : [https://jackrabbit.apache.org/oak/docs/query/query-engine.html#Slow_Queries_and_Read_Limits](https://jackrabbit.apache.org/oak/docs/query/query-engine.html#Slow_Queries_and_Read_Limits).

## Optimisation des performances des requêtes {#query-performance-tuning}

La devise de l’optimisation des performances des requêtes dans AEM est la suivante :

**« Plus il y a de restrictions, mieux c&#39;est. »**

Les sections suivantes décrivent les ajustements recommandés pour garantir les performances des requêtes. Optimisez d’abord la requête, une activité moins intrusive, puis, si nécessaire, ajustez les définitions d’index.

### Ajustement de l’instruction de la requête {#adjusting-the-query-statement}

AEM prend en charge les langages de requête suivants :

* Query Builder
* JCR-SQL2
* XPath

L’exemple suivant utilise Query Builder étant donné que c’est le langage de requête le plus courant utilisé par l’équipe de développement AEM, mais les mêmes principes s’appliquent à JCR-SQL2 et XPath.

1. Ajoutez une restriction de type de nœud afin que la requête soit résolue sur un index de propriété Lucene existant.

* **Requête non optimisée**

  ```js
  property=jcr:content/contentType
  property.value=article-page
  ```

* **Requête optimisée**

  ```js
  type=cq:Page
  property=jcr:content/contentType
  property.value=article-page
  ```

  Dans le cas des requêtes dépourvues d’une restriction du type de nœud, AEM suppose qu’il s’agit du type de nœud `nt:base`, dont chaque nœud d’AEM est un sous-type, ce qui se traduit effectivement par l’absence de restriction de ce type.

  Le fait de définir `type=cq:Page` limite cette requête aux seuls nœuds `cq:Page` et résout la requête sur l’index cqPageLucene d’AEM, ce qui limite les résultats à un sous-ensemble de nœuds (uniquement les nœuds `cq:Page`) dans AEM.

1. Ajustez la restriction de type de nœud de la requête afin que la requête soit résolue sur un index de propriété Lucene existant.

* **Requête non optimisée**

  ```js
  type=nt:hierarchyNode
  property=jcr:content/contentType
  property.value=article-page
  ```

* **Requête optimisée**

  ```js
  type=cq:Page
  property=jcr:content/contentType
  property.value=article-page
  ```

  `nt:hierarchyNode` est le type de nœud parent de `cq:Page`. En supposant que `jcr:content/contentType=article-page` n’est appliqué qu’aux nœuds `cq:Page` par le biais de l’application personnalisée d’Adobe, cette requête renvoie uniquement des nœuds `cq:Page` où `jcr:content/contentType=article-page` est appliqué. Ce flux est toutefois une restriction sous-optimale, pour les raisons suivantes :

   * Un autre nœud hérite de `nt:hierarchyNode` (par exemple, `dam:Asset`) ce qui augmente inutilement l’ensemble des résultats potentiels.
   * Il n’existe aucun index fourni par AEM pour `nt:hierarchyNode`, car il y en a un qui est fourni pour `cq:Page`.

  Le fait de définir `type=cq:Page` limite cette requête aux seuls nœuds `cq:Page` et résout la requête sur l’index cqPageLucene d’AEM, ce qui limite les résultats à un sous-ensemble de nœuds (uniquement les nœuds cq:Page) dans AEM.

1. Vous pouvez également ajuster la ou les restrictions de propriété, de sorte que la requête soit résolue sur un index de propriété existant.

* **Requête non optimisée**

  ```js
  property=jcr:content/contentType
  property.value=article-page
  ```

* **Requête optimisée**

  ```js
  property=jcr:content/sling:resourceType
  property.value=my-site/components/structure/article-page
  ```

  Le fait de remplacer la restriction de propriété de `jcr:content/contentType` (une valeur personnalisée) par la propriété bien connue `sling:resourceType` permet à la requête d’être résolue sur l’index de propriété `slingResourceType` qui indexe tout le contenu en fonction de `sling:resourceType`.

  Les index de propriété (contrairement aux index de propriété Lucene) sont mieux utilisés lorsque la requête ne se distingue pas par le type de nœud et qu’une seule restriction de propriété domine l’ensemble de résultats.

1. Ajoutez la restriction de chemin la plus stricte possible à la requête. Par exemple, préférez `/content/my-site/us/en` à `/content/my-site`, ou `/content/dam` à `/`.

* **Requête non optimisée**

  ```js
  type=cq:Page
  path=/content
  property=jcr:content/contentType
  property.value=article-page
  ```

* **Requête optimisée**

  ```js
  type=cq:Page
  path=/content/my-site/us/en
  property=jcr:content/contentType
  property.value=article-page
  ```

  Limiter la restriction de chemin d’accès de `path=/content` à `path=/content/my-site/us/en` permet aux index de réduire le nombre d’entrées d’index qui doivent être inspectées. Lorsque la requête permet une excellente restriction du chemin d’accès, au-delà du simple `/content` ou `/content/dam`, assurez-vous que `evaluatePathRestrictions=true` est associé à l’index.

  Notez que l’utilisation de `evaluatePathRestrictions` augmente la taille de l’index.

1. Si possible, évitez d’utiliser des fonctions et opérations de requête telles que `LIKE` et `fn:XXXX`, car leur coût évolue en fonction du nombre de résultats basés sur une restriction.

* **Requête non optimisée**

  ```js
  type=cq:Page
  property=jcr:content/contentType
  property.operation=like
  property.value=%article%
  ```

* **Requête optimisée**

  ```js
  type=cq:Page
  fulltext=article
  fulltext.relPath=jcr:content/contentType
  ```

  L’évaluation de la condition LIKE est lente car aucun index ne peut être utilisé si le texte commence par un caractère générique (&quot;%...’). La condition jcr:contains autorise un index en texte intégral et est, de ce fait, à privilégier. Pour cela, l’index de propriété Lucene doit présenter indexRule pour `jcr:content/contentType` avec `analayzed=true`.

  L’utilisation de fonctions de requêtes telles que `fn:lowercase(..)` peut rendre l’optimisation plus difficile, car il n’existe pas d’équivalents plus rapides (hormis des configurations d’analyseur d’index plus complexes et moins discrètes). Il est préférable d’identifier d’autres restrictions d’étendue afin d’améliorer les performances globales de la requête, ce qui nécessite que les fonctions fonctionnent sur le plus petit ensemble de résultats potentiels possible.

1. ***Cet ajustement est spécifique à Query Builder et ne s’applique pas à JCR-SQL2 ni à XPath.***

   Utilisez le paramètre [guessTotal de Query Builder](/help/sites-developing/querybuilder-api.md#using-p-guesstotal-to-return-the-results) si le jeu complet de résultats n’est **pas** nécessaire immédiatement.

   * **Requête non optimisée**

     ```js
     type=cq:Page
     path=/content
     ```

   * **Requête optimisée**

     ```js
     type=cq:Page
     path=/content
     p.guessTotal=100
     ```

   Lorsque la requête s’exécute rapidement mais que le nombre de résultats est élevé, le paramètre `guessTotal` constitue un élément d’optimisation essentiel pour les requêtes Query Builder.

   `p.guessTotal=100` indique à Query Builder de ne collecter que les 100 premiers résultats. Et, pour définir un indicateur booléen indiquant s’il existe au moins un résultat supplémentaire (mais pas le nombre d’autres résultats, car le comptage de ce nombre entraîne une lenteur). Cette optimisation excelle pour la pagination ou le chargement infini, où seul un sous-ensemble de résultats est affiché de manière incrémentielle.

## Réglage d’un index existant {#existing-index-tuning}

1. Si la requête optimale correspond à un index de propriété, il ne reste rien à faire, car les index de propriété peuvent être réglés au minimum.
1. Autrement, la requête doit être résolue sur un index de propriété Lucene. Si aucun index ne peut être résolu, passez à Création d’un index.
1. Si nécessaire, convertissez la requête en XPath ou JCR-SQL2.

   * **Requête Query Builder**

     ```js
     query type=cq:Page
     path=/content/my-site/us/en
     property=jcr:content/contentType
     property.value=article-page
     orderby=@jcr:content/publishDate
     orderby.sort=desc
     ```

   * **XPath généré à partir de la requête Query Builder**

     ```js
     /jcr:root/content/my-site/us/en//element(*, cq:Page)[jcr:content/@contentType = 'article-page'] order by jcr:content/@publishDate descending
     ```

1. Fournissez le XPath (ou JCR-SQL2) au générateur de définitions d’index Oak sur le lien `https://oakutils.appspot.com/generate/index` afin de générer la définition d’index de propriété Lucene optimisée.<!-- The above URL is 404 as of April 24, 2023 -->

   **Définition d’index de propriété Lucene générée**

   ```xml
   - evaluatePathRestrictions = true
   - compatVersion = 2
   - type = "lucene"
   - async = "async"
   - jcr:primaryType = oak:QueryIndexDefinition
       + indexRules
       + cq:Page
           + properties
           + contentType
               - name = "jcr:content/contentType"
               - propertyIndex = true
           + publishDate
               - ordered = true
               - name = "jcr:content/publishDate"
   ```

1. Fusionnez manuellement la définition générée dans l’index de propriété Lucene qui existe de manière additive. Veillez à ne pas supprimer les configurations existantes, car elles peuvent être utilisées pour répondre à d’autres requêtes.

   1. Recherchez l’index de propriété Lucene existant qui couvre cq:Page (à l’aide du gestionnaire d’index). Dans ce cas, `/oak:index/cqPageLucene`.
   1. Identifiez le delta de configuration entre la définition d’index optimisée (étape 4) et l’index existant (/oak:index/cqPageLucene), et ajoutez les configurations manquantes de l’index optimisé à la définition de l’index existant.
   1. Selon les bonnes pratiques de réindexation AEM, une actualisation ou une réindexation est ordonnée, si le contenu existant peut être affecté par cette modification de configuration d’index.

## Création d’un index {#create-a-new-index}

1. Vérifiez que la requête ne correspond pas à un index de propriété Lucene existant. Si tel est le cas, reportez-vous à la section ci-dessus sur le réglage et l’index existant.
1. Si nécessaire, convertissez la requête en XPath ou JCR-SQL2.

   * **Requête Query Builder**

     ```js
     type=myApp:Author
     property=firstName
     property.value=ira
     ```

   * **XPath généré à partir de la requête Query Builder**

     ```js
     //element(*, myApp:Page)[@firstName = 'ira']
     ```

1. Fournissez le XPath (ou JCR-SQL2) au générateur de définitions d’index Oak sur le lien `https://oakutils.appspot.com/generate/index` afin de générer la définition d’index de propriété Lucene optimisée.<!-- The above URL is 404 as of April 24, 2023 -->

   **Définition d’index de propriété Lucene générée**

   ```xml
   - compatVersion = 2
   - type = "lucene"
   - async = "async"
   - jcr:primaryType = oak:QueryIndexDefinition
       + indexRules
       + myApp:AuthorModel
           + properties
           + firstName
               - name = "firstName"
               - propertyIndex = true
   ```

1. Déployez la définition d’index de propriété Lucene générée.

   Ajoutez la définition XML fournie par le générateur de définitions d’index Oak pour le nouvel index au projet AEM qui gère les définitions d’index Oak (n’oubliez pas de traiter les définitions d’index Oak comme du code, puisque le code en dépend).

   Déployez et testez le nouvel index en suivant le cycle de vie de développement logiciel d’AEM habituel et vérifiez que la requête correspond à l’index et qu’elle est performante.

   Lors du déploiement initial de cet index, AEM remplit l’index avec les données requises.

## À quel moment les requêtes de traversée et sans index sont-elles indiquées ? {#when-index-less-and-traversal-queries-are-ok}

Compte tenu de l’architecture de contenu flexible d’AEM, il est difficile de s’assurer que les structures de contenu n’évolueront pas au fil du temps pour atteindre des proportions inacceptables.

Assurez-vous donc que les index répondent aux requêtes, sauf si la combinaison des restrictions de type de nœud et de chemin d’accès garantit que **le nombre de nœuds parcourus ne sera jamais inférieur à 20.**

## Outils de développement de requêtes {#query-development-tools}

### Pris en charge par Adobe {#adobe-supported}

* **Débogueur Query Builder**

   * Interface utilisateur web destinée à exécuter des requêtes Query Builder et à générer le XPath connexe (à utiliser dans l’outil Expliquer la requête ou dans le Générateur de définitions d’index Oak).
   * Situé sur AEM à l’emplacement suivant : [/libs/cq/search/content/querydebug.html](http://localhost:4502/libs/cq/search/content/querydebug.html)

* **CRXDE Lite - Outil de requête**

   * Interface WebUI pour exécuter des requêtes XPath et JCR-SQL2.
   * Situé sur AEM à l’emplacement suivant : [/crx/de/index.jsp](http://localhost:4502/crx/de/index.jsp) > Outils > Requête…

* **[Expliquer la requête](/help/sites-administering/operations-dashboard.md#explain-query)**

   * Tableau de bord des opérations AEM qui fournit une explication détaillée (plan de requête, temps de requête et nombre de résultats) pour toute requête XPath ou JCR-SQL2.

* **[Requêtes lentes / les plus courantes](/help/sites-administering/operations-dashboard.md#query-performance)**

   * Tableau de bord des opérations AEM qui répertorie les requêtes lentes et populaires récentes exécutées sur AEM.

* **[Gestionnaire d’index](/help/sites-administering/operations-dashboard.md#the-index-manager)**

   * Interface WebUI des opérations AEM qui affiche les index sur l’instance AEM. Elle facilite la compréhension des index existants et peut être ciblée ou augmentée.

* **[Journalisation](/help/sites-administering/operations-dashboard.md#log-messages)**

   * Journalisation de Query Builder

      * `DEBUG @ com.day.cq.search.impl.builder.QueryImpl`

   * Journalisation de l’exécution des requêtes Oak

      * `DEBUG @ org.apache.jackrabbit.oak.query`

* **Configuration OSGi des paramètres du moteur de requête Apache Jackrabbit**

   * Configuration OSGi qui configure le comportement d’échec pour parcourir des requêtes.
   * Situé sur AEM à l’emplacement suivant : [/system/console/configMgr#org.apache.jackrabbit.oak.query.QueryEngineSettingsService](http://localhost:4502/system/console/configMgr#org.apache.jackrabbit.oak.query.QueryEngineSettingsService)

* **MBean JMX NodeCounter**

   * MBean JMX utilisé pour estimer le nombre de nœuds dans les arborescences de contenu dans AEM.
   * Situé sur AEM à l’emplacement suivant : [/system/console/jmx/org.apache.jackrabbit.oak%3Aname%3DnodeCounter%2Ctype%3DNodeCounter](http://localhost:4502/system/console/jmx/org.apache.jackrabbit.oak%3Aname%3DnodeCounter%2Ctype%3DNodeCounter)

### Prise en charge par la communauté {#community-supported}

* **Générateur de définitions d’index Oak sur`https://oakutils.appspot.com/generate/index`** <!-- The above URL is 404 as of April 24, 2023 -->

   * Générez l’index de propriété Lucene optimal à partir d’instructions de requête XPath ou JCR-SQL2.

* **[Module externe AEM Chrome](https://chrome.google.com/webstore/detail/aem-chrome-plug-in/ejdcnikffjleeffpigekhccpepplaode?hl=fr-FR)**

   * Extension de navigateur web Google Chrome qui expose des données de journal par demande, y compris les requêtes exécutées et leurs plans de requête, dans la console des outils de développement du navigateur.
   * [Sling Log Tracer 1.0.2+](https://sling.apache.org/downloads.cgi) doit être installé et activé sur AEM.
