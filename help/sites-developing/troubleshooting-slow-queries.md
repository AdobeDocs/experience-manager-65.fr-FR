---
title: Résolution des problèmes de lenteur des requêtes
seo-title: Résolution des problèmes de lenteur des requêtes
description: 'null'
seo-description: 'null'
uuid: ad09546a-c049-44b2-99a3-cb74ee68f040
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: c01e42ff-e338-46e6-a961-131ef943ea91
translation-type: tm+mt
source-git-commit: 6d8680bcfb03197ac33bc7efb0e40796e38fef20
workflow-type: tm+mt
source-wordcount: '2267'
ht-degree: 69%

---


# Résolution des problèmes de lenteur des requêtes{#troubleshooting-slow-queries}

## Classifications des requêtes lentes {#slow-query-classifications}

Dans AEM, les requêtes lentes sont classées dans 3 catégories principales, suivant le degré de gravité :

1. **Requêtes sans index**

   * Requêtes qui **ne sont pas** résolues sur un index et qui parcourent le contenu du JCR pour collecter des résultats

1. **Requêtes mal limitées**

   * Requêtes qui sont résolues sur un index, mais qui doivent parcourir toutes les entrées d’index pour collecter des résultats

1. **Requêtes avec jeu de résultats volumineux**

   * Requêtes qui renvoient un très grand nombre de résultats

Les deux premières classifications de requêtes (sans index et faiblement restreintes) sont lentes, car elles forcent le moteur de requête Oak à inspecter chaque résultat **potentiel** (noeud de contenu ou entrée d&#39;index) pour identifier celui qui appartient au jeu de résultats **réel**.

Le fait d’inspecter chaque résultat potentiel est désigné sous le nom de traversée.

Chaque résultat potentiel devant être inspecté, le coût lié à l’identification du jeu de résultats réel augmente de façon linéaire avec le nombre de résultats potentiels.

L’ajout de restrictions de requête et l’optimisation des index permettent de stocker les données d’index dans un format optimisé, ce qui se traduit par une récupération rapide des résultats. En outre, cela réduit la nécessité de recourir à une inspection linéaire des jeux de résultats potentiels, voire permet de s’en passer complètement.

Par défaut, dans AEM 6.3, lorsqu’une traversée de 100 000 est atteinte, la requête échoue et génère une exception. Cette limite n&#39;existe pas par défaut dans AEM versions antérieures à AEM 6.3, mais peut être définie via les paramètres du moteur de Requête Apache Jackrabbit OSGi configuration et QueryEngineSettings JMX bean (property LimitReads).

### Détection des requêtes sans index {#detecting-index-less-queries}

#### Pendant le développement {#during-development}

Expliquer **toutes** requêtes et s&#39;assurer que leurs plans de requête ne contiennent pas les **/&amp;ast; traverse** explication en eux. Exemple de plan de requête de traversée :

* **PLAN :** `[nt:unstructured] as [a] /* traverse "/content//*" where ([a].[unindexedProperty] = 'some value') and (isdescendantnode([a], [/content])) */`

#### Après le déploiement {#post-deployment}

* Contrôlez le journal `error.log` à la recherche de requêtes de traversée sans index :

   * `*INFO* org.apache.jackrabbit.oak.query.QueryImpl Traversal query (query without index) ... ; consider creating and index`
   * Ce message n’est consigné que si aucun index n’est disponible et si la requête traverse potentiellement de nombreux nœuds. Les messages ne sont pas consignés si un index est disponible, mais que la quantité à traverser est faible et, par conséquent, rapide.

* Visitez la console d&#39;opérations [Performance de Requête](/help/sites-administering/operations-dashboard.md#query-performance) et [Expliquez](/help/sites-administering/operations-dashboard.md#explain-query) les requêtes lentes à la recherche de traversées ou sans explication de requête d&#39;index.

### Détection des requêtes mal limitées {#detecting-poorly-restricted-queries}

#### Pendant le développement {#during-development-1}

Expliquez toutes les requêtes et assurez-vous qu’elles sont résolues sur un index optimisé afin de correspondre aux restrictions de propriété de la requête.

* Dans une couverture de plan de requête idéale, `indexRules` est défini pour toutes les restrictions de propriété et, au minimum, pour les restrictions de propriété les plus strictes de la requête.
* Les requêtes qui trient les résultats doivent être résolues sur un index de propriété Lucene avec des règles d’index pour les propriétés de tri qui définissent `orderable=true.`.

#### Par exemple, la valeur par défaut `cqPageLucene` n’a pas de règle d’index pour `jcr:content/cq:tags` {#for-example-the-default-cqpagelucene-does-not-have-an-index-rule-for-jcr-content-cq-tags}

Avant d’ajouter la règle d’index cq:tags

* **Règle d’index cq:tags**

   * N’existe pas en version prête à l’emploi.

* **Requête Query Builder**

   ```js
   type=cq:Page
   property=jcr:content/cq:tags
   property.value=my:tag
   ```

* **Plan de requête**

   `[cq:Page] as [a] /* lucene:cqPageLucene(/oak:index/cqPageLucene) *:* where [a].[jcr:content/cq:tags] = 'my:tag' */`

Cette requête est résolue sur l’index `cqPageLucene`. Cependant, étant donné qu’il n’existe pas de règle d’index de propriété pour `jcr:content` ou `cq:tags`, lorsque cette restriction est évaluée, chaque enregistrement de l’index `cqPageLucene` est vérifié afin de déterminer une correspondance. Cela signifie que si l’index contient un million de nœuds `cq:Page`, un million d’enregistrements sont vérifiés pour déterminer le jeu de résultats.

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

L&#39;ajout de indexRule pour `jcr:content/cq:tags` dans l&#39;index `cqPageLucene` permet de stocker les données `cq:tags` de façon optimisée.

Lorsqu&#39;une requête avec la restriction `jcr:content/cq:tags` est exécutée, l&#39;index peut rechercher les résultats par valeur. Cela signifie que si 100 nœuds `cq:Page` ont `myTagNamespace:myTag` comme valeur, seuls ces 100 résultats sont renvoyés. Les 999 000 autres résultats sont exclus des contrôles de restriction, ce qui améliore les performances d’un facteur 10 000.

Il va sans dire que des restrictions de requête supplémentaires réduisent les jeux de résultats éligibles et améliorent encore l’optimisation des requêtes.

De même, en l&#39;absence d&#39;une règle d&#39;index supplémentaire pour la propriété `cq:tags`, même une requête de texte intégral avec une restriction sur `cq:tags` ne fonctionnerait pas correctement car les résultats de l&#39;index retourneraient toutes les correspondances de texte intégral. La restriction sur les balises cq:tags sera ensuite filtrée.

Les listes de contrôle d’accès constituent une autre cause de filtrage post index. Bien souvent, il n’en est pas tenu compte en cours de développement. Tâchez de vous assurer que la requête ne renvoie pas de chemins d’accès auxquels l’utilisateur risque ne pas avoir accès. En règle générale, cela passe par une meilleure structure de contenu, ainsi que la définition d’une restriction de chemin d’accès appropriée sur la requête.

Pour déterminer si l&#39;index Lucene retourne de nombreux résultats pour renvoyer un très petit sous-ensemble en tant que résultat de requête, il est utile d&#39;activer les journaux DEBUG pour `org.apache.jackrabbit.oak.plugins.index.lucene.LucenePropertyIndex` et de voir combien de documents sont chargés à partir de l&#39;index. Le nombre de résultats finaux par rapport au nombre de documents chargés ne devrait pas être disproportionné. Pour plus d’informations, voir [Journalisation](/help/sites-deploying/configure-logging.md).

#### Après le déploiement {#post-deployment-1}

* Surveillez `error.log` pour les requêtes de traversée :

   * `*WARN* org.apache.jackrabbit.oak.spi.query.Cursors$TraversingCursor Traversed ### nodes ... consider creating an index or changing the query`

* Visitez la console d&#39;opérations [Performance de la Requête](/help/sites-administering/operations-dashboard.md#query-performance) et [Expliquez](/help/sites-administering/operations-dashboard.md#explain-query) les requêtes lentes à la recherche de plans de requête qui ne résolvent pas les restrictions de propriété de requête aux règles de propriété d&#39;index.

### Détection des requêtes avec jeu de résultats volumineux {#detecting-large-result-set-queries}

#### Pendant le développement {#during-development-2}

Définissez des seuils bas pour oak.queryLimitInMemory (par exemple, 10000) et oak.queryLimitReads (par exemple, 5000) et optimisez les requêtes coûteuses lorsque vous obtenez une exception UnsupportedOperationException indiquant que la requête lit plus de x nœuds... (The query read more than x nodes...).

Cela permet d’éviter les requêtes gourmandes en ressources (c’est-à-dire non soutenues par un index ou soutenues par un index moins étendu). Par exemple, une requête qui lit 1 million de nœuds générerait un grand nombre d’E/S et aurait un impact négatif sur les performances globales de l’application. Par conséquent, toute requête qui échoue en raison des limites ci-dessus doit être analysée et optimisée.

#### Après le déploiement {#post-deployment-2}

* Surveillez les journaux à la recherche de requêtes déclenchant une traversée de grands noeuds ou une consommation importante de mémoire de tas : &quot;

   * `*WARN* ... java.lang.UnsupportedOperationException: The query read or traversed more than 100000 nodes. To avoid affecting other tasks, processing was stopped.`
   * Optimisez la requête afin de réduire le nombre de nœuds parcourus transversalement.

* Surveillez les journaux à la recherche de requêtes déclenchant une consommation importante de mémoire de tas :

   * `*WARN* ... java.lang.UnsupportedOperationException: The query read more than 500000 nodes in memory. To avoid running out of memory, processing was stopped`
   * Optimisez la requête pour réduire la consommation de mémoire de tas.

Pour AEM versions 6.0 à 6.2, vous pouvez régler le seuil de traversée des noeuds au moyen de paramètres JVM dans le script d’début AEM afin d’éviter que les requêtes volumineuses ne surchargent l’environnement. Les valeurs recommandées sont les suivantes :

* `-Doak.queryLimitInMemory=500000`
* `-Doak.queryLimitReads=100000`

Dans AEM 6.3, les 2 paramètres ci-dessus sont préconfigurés par défaut et peuvent être modifiés dans les paramètres OSGi QueryEngineSettings.

Plus d&#39;informations disponibles sous : [https://jackrabbit.apache.org/oak/docs/query/query-engine.html#Slow_Queries_and_Read_Limits](https://jackrabbit.apache.org/oak/docs/query/query-engine.html#Slow_Queries_and_Read_Limits)

## Optimisation des performances des requêtes {#query-performance-tuning}

S’agissant de l’optimisation des performances des requêtes dans AEM, la devise est :

**« Plus il y a de restrictions, mieux c’est ! »**

Voici un aperçu des réglages recommandés pour garantir les performances des requêtes. Commencez par optimiser la requête, qui est une opération plus discrète, puis, si nécessaire, optimisez les définitions d’index.

### Réglage de l’instruction de requête  {#adjusting-the-query-statement}

AEM prend en charge les langages de requête suivants :

* Query Builder
* JCR-SQL2
* XPath

Query Builder est utilisé dans l’exemple suivant, car il s’agit du langage de requête employé le plus couramment par les développeurs AEM. Cependant, les mêmes principes s’appliquent également à JCR-SQL2 et XPath.

1. Ajoutez une restriction de type de nœud, de sorte que la requête soit résolue sur un index de propriété Lucene existant.

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

   La définition de `type=cq:Page` limite cette requête aux seuls noeuds `cq:Page` et résout la requête à l&#39;AEM cqPageLucene, en limitant les résultats à un sous-ensemble de noeuds (seulement `cq:Page` noeuds) en AEM.

1. Réglez la restriction de type de nœud de la requête, de sorte que cette dernière soit résolue sur un index de propriété Lucene existant.

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

   `nt:hierarchyNode` est le type de noeud parent de  `cq:Page`, et en supposant qu’ `jcr:content/contentType=article-page` il ne soit appliqué qu’aux  `cq:Page` noeuds via notre application personnalisée, cette requête ne renvoie que  `cq:Page` les noeuds où  `jcr:content/contentType=article-page`. Il s’agit toutefois d’une restriction sous-optimale, pour les raisons suivantes :

   * Un autre noeud hérite de `nt:hierarchyNode` (ex. `dam:Asset`) ajoutant inutilement à l&#39;ensemble des résultats potentiels.
   * Il n&#39;existe aucun index fourni par l&#39;AEM pour `nt:hierarchyNode`, mais il existe un index fourni pour `cq:Page`.
   Le fait de définir `type=cq:Page` limite cette requête aux seuls nœuds `cq:Page` et résout la requête sur l’index cqPageLucene d’AEM, ce qui limite les résultats à un sous-ensemble de nœuds (uniquement les nœuds cq:Page) dans AEM.

1. Vous pouvez également ajuster la ou les restrictions de propriété afin que la requête se résolve à un index de propriétés existant.

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

   La modification de la restriction de propriété de `jcr:content/contentType` (valeur personnalisée) à la propriété bien connue `sling:resourceType` permet à la requête de résoudre l&#39;index de propriété `slingResourceType` qui indexe tout le contenu par `sling:resourceType`.

   Les index de propriété (contrairement aux index de propriété Lucene) conviennent mieux lorsque la requête ne fait pas de distinction par type de nœud et qu’une seule restriction de propriété domine le jeu de résultats.

1. Ajoutez la restriction de chemin la plus stricte possible à la requête. Par exemple, préférez `/content/my-site/us/en` à `/content/my-site` ou `/content/dam` à `/`.

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

   L&#39;extension de la restriction de chemin de `path=/content`à `path=/content/my-site/us/en` permet aux index de réduire le nombre d&#39;entrées d&#39;index à inspecter. Lorsque la requête peut très bien restreindre le chemin, au-delà de `/content` ou `/content/dam`, assurez-vous que l&#39;index a `evaluatePathRestrictions=true`.

   L&#39;utilisation de `evaluatePathRestrictions` augmente la taille de l&#39;index.

1. Si possible, évitez d’utiliser des fonctions/opérations de requête telles que `LIKE` et `fn:XXXX`, car leur coût évolue en fonction du nombre de résultats basés sur une restriction.

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

   La condition LIKE est lente à être évaluée, car aucun index ne peut être utilisé si le texte début avec un caractère générique (&quot;%...&#39;). La condition jcr:contains autorise un index en texte intégral et est, de ce fait, à privilégier. Pour cela, l&#39;index de propriétés Lucene résolu doit avoir indexRule pour `jcr:content/contentType` avec `analayzed=true`.

   L&#39;utilisation de fonctions de requête telles que `fn:lowercase(..)` peut s&#39;avérer plus difficile à optimiser, car il n&#39;existe pas d&#39;équivalents plus rapides (en dehors de configurations d&#39;analyseur d&#39;index plus complexes et intrusives). Il est préférable d’identifier d’autres restrictions d’étendue afin d’améliorer les performances globales des requêtes, ce qui exige que les fonctions s’exécutent sur le plus petit jeu possible de résultats potentiels.

1. ***Ce réglage est spécifique à Query Builder et ne s’applique pas à JCR-SQL2 ni à XPath.***

   Utilisez le paramètre [guessTotal de Query Builder](/help/sites-developing/querybuilder-api.md#using-p-guesstotal-to-return-the-results) si le jeu complet de résultats n’est **pas** nécessaire immédiatement.

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
   Dans les cas où l&#39;exécution de la requête est rapide mais où le nombre de résultats est élevé, p. `guessTotal` est une optimisation essentielle pour les requêtes du créateur de Requêtes.

   Le paramètre `p.guessTotal=100` indique à Query Builder de ne collecter que les 100 premiers résultats et de définir un indicateur booléen pour signaler l’existence d’au moins un résultat supplémentaire (sans calculer toutefois ce nombre, car cela entraînerait un ralentissement des performances). Cette optimisation donne d’excellents résultats pour la pagination ou le chargement infini, deux scénarios dans lesquels seul un sous-ensemble de résultats est affiché de manière incrémentielle.

## Optimisation d’un index existant  {#existing-index-tuning}

1. Si la requête optimale est résolue sur un index de propriété, il n’y a rien d’autre à faire, dans la mesure où les index de ce type présentent des capacités de réglage minimales.
1. Dans le cas contraire, la requête doit se résoudre en un index de propriétés Lucene. Si aucun index ne peut être résolu, passez à la création d’un index.
1. Le cas échéant, convertissez la requête au format XPath ou JCR-SQL2.

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

1. Fournissez le XPath (ou JCR-SQL2) au [Générateur de définitions d’index en Oak](https://oakutils.appspot.com/generate/index) afin de générer la définition d’index de propriété Lucene optimisée.

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

1. Fusionnez manuellement la définition générée dans l’index de propriétés Lucene existant de manière additive. Veillez à ne pas supprimer les configurations existantes, car elles peuvent être utilisées pour accomplir d’autres requêtes.

   1. Définissez l’index de propriété Lucene existant qui couvre cq:Page (à l’aide du gestionnaire d’index). Dans ce cas, `/oak:index/cqPageLucene`.
   1. Identifiez le delta de configuration entre la définition d’index optimisée (étape n° 4) et l’index existant (/oak:index/cqPageLucene), puis ajoutez les configurations manquantes depuis l’index optimisé à la définition d’index existante.
   1. Conformément aux meilleures pratiques en matière de réindexation d’AEM, une actualisation ou une réindexation est acceptable, selon que le contenu existant est affecté par cette modification de configuration d’index.

## Créer un nouvel index {#create-a-new-index}

1. Vérifiez que la requête n’est pas résolue sur un index de propriété Lucene existant. Si tel est le cas, consultez la section précédente traitant de l’optimisation d’un index existant.
1. Le cas échéant, convertissez la requête au format XPath ou JCR-SQL2.

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

1. Fournissez le XPath (ou JCR-SQL2) au [Générateur de définitions d’index en Oak](https://oakutils.appspot.com/generate/index) afin de générer la définition d’index de propriété Lucene optimisée.

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

   Ajoutez la définition XML fournie par le Générateur de définitions d’index en Oak du nouvel index au projet AEM qui gère les définitions d’index Oak (pour rappel, traitez les définitions d’index Oak comme du code, car le code dépend de celles-ci).

   Déployez et testez le nouvel index suivant le cycle de vie de développement habituel des logiciels AEM. Vérifiez également que la requête est résolue sur l’index et qu’elle est performante.

   Lors du déploiement initial de cet index, AEM va le remplir avec les données requises.

## Quand les requêtes sans index et de traversée sont-elles compatibles ? {#when-index-less-and-traversal-queries-are-ok}

Compte tenu de l’architecture de contenu flexible d’AEM, il est difficile d’affirmer que les structures de contenu n’évolueront pas au fil du temps pour atteindre des proportions inacceptables.

Par conséquent, assurez-vous que les index satisfont aux requêtes, sauf si la combinaison de la restriction de chemin et de la restriction de type nodetype garantit que **moins de 20 noeuds sont jamais traversés.**

## Outils de développement de requêtes {#query-development-tools}

### Prise en charge par Adobe {#adobe-supported}

* **Débogueur Query Builder**

   * Interface utilisateur web destinée à exécuter des requêtes Query Builder et à générer le XPath connexe (à utiliser dans l’outil Expliquer la requête ou dans le Générateur de définitions d’index en Oak).
   * Situé sur AEM à [/libs/cq/search/content/querydebug.html](http://localhost:4502/libs/cq/search/content/querydebug.html)

* **CRXDE LITE : outil de requête**

   * Interface utilisateur web destinée à exécuter des requêtes XPath et JCR-SQL2.
   * Situé sur l’AEM à l’adresse [/crx/de/index.jsp](http://localhost:4502/crx/de/index.jsp) > Outils > Requête...

* **[Expliquer la requête](/help/sites-administering/operations-dashboard.md#explain-query)**

   * Tableau de bord des opérations AEM qui fournit une explication détaillée (plan de requête, durée de la requête et nombre de résultats) pour toute requête XPATH ou JCR-SQL2 donnée.

* **[Requêtes lentes/les plus courantes](/help/sites-administering/operations-dashboard.md#query-performance)**

   * Tableau de bord des opérations AEM répertoriant les requêtes lentes et les requêtes les plus courantes exécutées sur AEM.

* **[Gestionnaire d’index](/help/sites-administering/operations-dashboard.md#the-index-manager)**

   * Interface utilisateur des opérations AEM qui affiche les index sur l’instance AEM ; cela permet d’identifier plus facilement les index qui existent déjà, qui peuvent être ciblés ou augmentés.

* **[Journalisation](/help/sites-administering/operations-dashboard.md#log-messages)**

   * Journalisation de Query Builder

      * `DEBUG @ com.day.cq.search.impl.builder.QueryImpl`
   * Journalisation de l’exécution des requêtes Oak

      * `DEBUG @ org.apache.jackrabbit.oak.query`


* **Configuration OSGi des paramètres du moteur de requête Apache Jackrabbit**

   * Configuration OSGi qui configure le comportement d’échec pour les requêtes de traversée.
   * Situé sur AEM à [/system/console/configMgr#org.apache.jackrabbit.oak.requête.QueryEngineSettingsService](http://localhost:4502/system/console/configMgr#org.apache.jackrabbit.oak.query.QueryEngineSettingsService)

* **Mbean JMX NodeCounter**

   * MBean JMX utilisé pour estimer le nombre de nœuds des arborescences de contenu dans AEM.
   * Situé sur l&#39;AEM à l&#39;adresse [/system/console/jmx/org.apache.jackrabbit.oak%3Aname%3DnodeCounter%2Ctype%3DNodeCounter](http://localhost:4502/system/console/jmx/org.apache.jackrabbit.oak%3Aname%3DnodeCounter%2Ctype%3DNodeCounter)

### Prise en charge par la communauté {#community-supported}

* **[Générateur de définitions d’index Oak](https://oakutils.appspot.com/generate/index)**

   * Générez l’index de propriété Lucene optimal à partir d’instructions de requête XPath ou JCR-SQL2.

* **[Module externe AEM Chrome](https://chrome.google.com/webstore/detail/aem-chrome-plug-in/ejdcnikffjleeffpigekhccpepplaode?hl=en-US)**

   * Extension de navigateur web Google Chrome qui expose des données de journal par demande, y compris les requêtes exécutées et leurs plans de requête, dans la console des outils de développement du navigateur.
   * [Sling Log Tracer 1.0.2+](https://sling.apache.org/downloads.cgi) doit être installé et activé sur AEM.
