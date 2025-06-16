---
title: Requêtes et indexation Oak
description: Découvrez comment configurer des index dans Adobe Experience Manager (AEM) 6.5.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: deploying
legacypath: /content/docs/en/aem/6-0/deploy/upgrade/queries-and-indexing
feature: Configuring
exl-id: d9ec7728-84f7-42c8-9c80-e59e029840da
solution: Experience Manager, Experience Manager Sites
role: Admin
source-git-commit: eeeb31d81c22f8dace7a170953bf45a709f5ac73
workflow-type: ht
source-wordcount: '3051'
ht-degree: 100%

---

# Requêtes et indexation Oak{#oak-queries-and-indexing}

>[!NOTE]
>
>Cet article traite de la configuration des index dans AEM 6. Pour connaître les bonnes pratiques sur l’optimisation des requêtes et l’indexation des performances, consultez les [Bonnes pratiques relatives aux requêtes et à l’indexation](/help/sites-deploying/best-practices-for-queries-and-indexing.md).

## Présentation {#introduction}

Contrairement à Jackrabbit 2, Oak n’indexe pas le contenu par défaut. Les index personnalisés doivent être créés si nécessaire, tout comme avec les bases de données relationnelles traditionnelles. S’il n’existe aucun index pour une requête spécifique, il est possible que de nombreux nœuds soient parcourus. La requête peut encore fonctionner, mais elle est probablement lente.

Si Oak rencontre une requête sans index, un message de journal de niveau AVERTISSEMENT est imprimé :

```xml
*WARN* Traversed 1000 nodes with filter Filter(query=select ...) consider creating an index or changing the query
```

## Langages de requête pris en charge {#supported-query-languages}

Le moteur de requête Oak prend en charge les langages suivants :

* XPath (recommandé)
* SQL-2
* SQL (obsolète)
* JQOM

## Types d’indexeur et calcul des coûts {#indexer-types-and-cost-calculation}

Le back-end basé sur Apache Oak permet à différents indexeurs d’être connectés au référentiel.

Un indexeur est un **Index de propriété**, pour lequel la définition d’index est stockée dans le référentiel directement.

Les implémentations d’**Apache Lucene** et **Solr** sont également disponibles par défaut, et prennent en charge l’indexation du texte intégral.

L’**indexation transversale** est utilisé si aucun autre indexeur n’est disponible. Cela signifie que le contenu n’est pas indexé et que les nœuds de contenu sont parcourus pour trouver des correspondances avec la requête.

Si plusieurs indexeurs sont disponibles pour une requête, chaque indexeur disponible estime le coût d’exécution de la requête. Oak choisit ensuite l’indexeur avec le coût estimé le plus faible.

![chlimage_1-148](assets/chlimage_1-148.png)

Le diagramme ci-dessus est une représentation de haut niveau du mécanisme d’exécution de requête d’Apache Oak.

Tout d’abord, la requête est analysée dans une arborescence de syntaxe abstraite. Ensuite, la requête est vérifiée et transformée en SQL-2, qui est le langage natif des requêtes Oak.

Ensuite, chaque index est consulté pour estimer le coût de la requête. Une fois terminé, les résultats de l’index le moins cher sont récupérés. Enfin, les résultats sont filtrés, à la fois pour s’assurer que l’utilisateur ou l’utilisatrice actuelle a un accès en lecture au résultat et que le résultat correspond à la requête complète.

## Configurer les index {#configuring-the-indexes}

>[!NOTE]
>
>Pour un référentiel de grande taille, créer un index est une opération qui demande beaucoup de temps. Cela vaut aussi bien pour la création initiale d’un index que pour la réindexation (reconstruction d’un index après avoir modifié la définition). Consultez également les sections [Résolution des problèmes liés aux index Oak](/help/sites-deploying/troubleshooting-oak-indexes.md) et [Empêcher une réindexation lente](/help/sites-deploying/troubleshooting-oak-indexes.md#preventing-slow-re-indexing).

Si une réindexation s’avère nécessaire dans des référentiels volumineux, en particulier lorsque vous utilisez MongoDB et des index en texte intégral, pensez à recourir à la pré-extraction de texte, ainsi qu’à utiliser la commande oak-run pour générer l’index initial et procéder à la réindexation.

Les index sont configurés en tant que nœuds dans le référentiel sous le nœud **Oak:index**.

Le type du nœud d’index doit être **oak:QueryIndexDefinition.** Plusieurs options de configuration sont disponibles pour chaque indexeur en tant que propriétés de nœud. Pour plus d’informations, voir les détails de configuration pour chaque type d’indexeur ci-dessous.

### Index de propriété {#the-property-index}

L’index de propriété s’avère utile pour les requêtes qui ont des contraintes de propriété, mais qui ne sont pas en texte intégral. Il peut être configuré en suivant la procédure ci-dessous :

1. Ouvrez CRXDE en accédant à `http://localhost:4502/crx/de/index.jsp`.
1. Créez un nœud sous **oak:index**.
1. Nommez le nœud **PropertyIndex**, puis définissez le type de nœud sur **oak:QueryIndexDefinition**.
1. Définissez les propriétés suivantes pour le nouveau nœud :

   * **Type :**  `property` (de type String)
   * **propertyNames :** `jcr:uuid` (de type Nom)

   Cet exemple particulier indexe la propriété `jcr:uuid`, dont la tâche est de présenter l’UUID (universally unique identifier, identifiant universel unique) du nœud associé.

1. Enregistrez les modifications.

L’index de propriété comporte les options de configuration suivantes :

* La propriété **type** spécifie le type d’index. Dans ce cas, il doit être défini sur **property**.

* La propriété **propertyNames** indique la liste des propriétés qui seront stockées dans l’index. En cas d’absence, le nom du nœud est utilisé comme valeur de référence de nom de propriété. Dans cet exemple, la propriété **jcr:uuid** dont la tâche est d’exposer l’identifiant unique (UUID) de son nœud est ajouté à l’index.

* L’indicateur **unique**, qui, défini sur **true**, ajoute une limite d’unicité à l’index de propriété.

* La propriété **declaringNodeTypes** vous permet de spécifier un certain type de nœud que l’index appliquera uniquement.
* L’indicateur **Réindexation**, si défini sur **true**, déclenchera une réindexation de l’ensemble du contenu.

### Index ordonné {#the-ordered-index}

L’index ordonné est une extension de l’index de propriété. Cependant, il est désormais obsolète. Les index de ce type doivent être remplacés par l’[index de propriété Lucene](#the-lucene-property-index).

### Index de texte intégral Lucene {#the-lucene-full-text-index}

L’indexeur de texte intégral basé sur Apache Lucene est disponible dans AEM 6.

Si un index de recherche en texte intégral est configuré, toutes les requêtes ayant une condition de texte intégral l’utilisent, quelles que soient les autres conditions indexées et les restrictions de chemin d’accès.

Si aucun index de recherche en texte intégral n’est configuré, les requêtes avec des conditions de texte intégral ne fonctionneront pas comme prévu.

Étant donné que l’index est mis à jour par le biais d’un thread asynchrone d’arrière-plan, certaines recherches en texte intégral ne seront pas disponibles pendant une courte durée, jusqu’à ce que les processus d’arrière-plan soient terminés.

Vous pouvez configurer un index de recherche en texte intégral Lucene en suivant la procédure ci-dessous :

1. Ouvrez CRXDE et créez un nœud sous **oak:index**.
1. Nommez le nœud **LuceneIndex** et définissez le type de nœud sur **oak:QueryIndexDefinition**.
1. Ajoutez les propriétés suivantes au nœud :

   * **type :**  `lucene` (de type String)
   * **async :**  `async` (de type String)

1. Enregistrez les modifications.

L’index Lucene comporte les options de configuration suivantes :

* La propriété **type** qui spécifie le type d’index qui doit être défini sur **lucene**.
* La propriété **async** qui doit être définie sur **async**. Le processus de mise à jour de l’index est ainsi envoyé à un thread d’arrière-plan.
* La propriété **includePropertyTypes** qui définit le sous-ensemble des types de propriétés inclus dans l’index.
* La propriété **excludePropertyNames**, qui définit une liste de noms de propriété (les propriétés qui doivent être exclues de l’index).
* L’indicateur **Réindexation**, si défini sur **true**, déclenchera une réindexation de l’ensemble du contenu.

### Présentation de la recherche en texte intégral {#understanding-fulltext-search}

La documentation de cette section s’applique à Apache Lucene, Elasticsearch, ainsi qu’aux index en texte intégral, par exemple PostgreSQL, SQLite, MySQL. L’exemple suivant concerne AEM/Oak/Lucene.

<b>Données à indexer</b>

Les données qui doivent être indexées constituent le point de départ. Prenez les documents suivants comme exemple :

| <b>ID du document</b> | <b>Chemin</b> | <b>Texte intégral</b> |
| --- | --- | --- |
| 100 | /content/rubik | « Rubik est une marque finlandaise. » |
| 200 | /content/rubiksCube | « Le Rubik&#39;s Cube a été inventé en 1974. » |
| 300 | /content/cube | « Un cube est un objet à 3 dimensions. » |


<b>Index inversé</b>

Le mécanisme d’indexation divise le texte intégral en termes appelés « jetons » et crée un index appelé « index inversé ». Cet index contient la liste des documents où il apparaît pour chaque terme.

Les termes courants et courts (également appelés « mots vides »), ne sont pas indexés. Tous les jetons sont convertis en minuscules et la recherche de radical est appliquée.

Les caractères spéciaux tels que *« - »* ne sont pas indexés.

| <b>Jeton</b> | <b>ID de document</b> |
| --- | --- |
| 194 | ..., 200,... |
| marque | ..., 100,... |
| cube | ..., 200, 300,... |
| dimension | 300 |
| terminer | ..., 100,... |
| inventer | 200 |
| objet | ..., 300,... |
| rubik | ..., 100, 200,... |

La liste des documents est triée. Le tri est pratique lors de l’interrogation.

<b>Recherche en cours</b>

Vous trouverez ci-dessous un exemple de requête. Notez que tous les caractères spéciaux (tels que *&#39;*) ont été remplacés par un espace :

```
/jcr:root/content//element(\*; cq:Page)`[` jcr:contains('Rubik s Cube')`]`
```

Les termes sont transformés en jetons et filtrés de la même manière que lors de l’indexation (les termes d’un seul caractère sont supprimés, par exemple). Dans ce cas, la recherche porte donc sur :

```
+:fulltext:rubik +:fulltext:cube
```

L’index consulte la liste des documents pour ces termes. Si les documents sont nombreux, la listes peut être volumineuse. Par exemple, supposons qu’elle contienne les éléments suivants :


| <b>Jeton</b> | <b>ID de document</b> |
| --- | --- |
| rubik | 10, 100, 200, 1000 |
| cube | 30, 200, 300, 2000 |


Lucene passe d’une liste à l’autre (ou examine les listes `n` en alternance lors de la recherche des termes `n`) :

* La lecture de « rubik » permet d’obtenir la première entrée : il trouve 10
* La lecture de « cube » permet d’obtenir la première entrée `>` = 10. 10 est introuvable, le suivant est 30.
* La lecture de « rubik » permet d’obtenir la première entrée `>` = 30 : 100.
* La lecture de « cube » permet d’obtenir la première entrée `>` = 100 : 200.
* La lecture de « rubik » permet d’obtenir la première entrée `>` = 200. 200 trouvé. Le document 200 correspond donc aux deux termes. Cela est mémorisé.
* La lecture de « rubik » permet d&#39;’obtenir l’entrée suivante : 1000.
* La lecture de « cube » permet d’obtenir la première entrée `>` = 1000 : 2000.
* La lecture de « rubik » permet d’obtenir la première entrée `>` = 2000 : fin de la liste.
* Vous pouvez arrêter la recherche.

Le seul document qui contient les deux termes est 200, comme dans l’exemple ci-dessous :

| 200 | /content/rubiksCube | « Le Rubik&#39;s Cube a été inventé en 1974. » |
| --- | --- | --- |

Lorsque plusieurs entrées sont trouvées, elles sont triées par score.

>[!NOTE]
>
>Le mécanisme de recherche décrit dans cette section utilise l’indexation Lucene, et non une correspondance partielle comme la commande Linux `grep`.

### Index de propriété Lucene {#the-lucene-property-index}

Depuis **Oak 1.0.8**, Lucene permet de créer des index qui impliquent des contraintes de propriété qui ne sont pas du texte intégral.

Pour obtenir un index de propriété Lucene, la propriété **fulltextEnabled** doit toujours être définie sur false.

Prenez l’exemple de requête suivant :

```xml
select * from [nt:base] where [alias] = '/admin'
```

Pour définir un index de propriété Lucene pour la requête ci-dessus, vous pouvez ajouter la définition suivante en créant un nœud sous **`oak:index`:**.

* **Nom :** `LucenePropertyIndex`
* **Type :** `oak:QueryIndexDefinition`

Une fois que le nœud a été créé, ajoutez les propriétés suivantes :

* **type :**

  ```xml
  lucene (of type String)
  ```

* **async :**

  ```xml
  async (of type String)
  ```

* **fulltextEnabled :**

  ```xml
  false (of type Boolean)
  ```

* **includePropertyNames :** `["alias"] (of type String)`

>[!NOTE]
>
>Par rapport à l’index standard de propriété, l’index de propriété Lucene est toujours configuré en mode asynchrone. Par conséquent, les résultats renvoyés par l’index peuvent ne pas toujours refléter la version la plus récente du référentiel.

>[!NOTE]
>
>Pour obtenir des informations plus détaillées sur l’index de propriété Lucene, reportez-vous à la page de documentation [Oak Lucene Apache Jackrabbit](https://jackrabbit.apache.org/oak/docs/query/lucene.html).

### Analyseurs Lucene {#lucene-analyzers}

Depuis la version 1.2.0, Oak prend en charge les analyseurs Lucene.

Les analyseurs sont utilisés lorsqu’un document est indexé et au moment de la requête. Un analyseur examine le texte des champs et génère un flux de jeton. Les analyseurs Lucene se composent d’une série de classes de générateurs de jetons et de filtres.

Les analyseurs peuvent être configurées par l’intermédiaire du nœud `analyzers` (de type `nt:unstructured`), à l’intérieur de la définition `oak:index`.

L’analyseur par défaut pour un index est configuré dans l’enfant `default`du nœud des analyseurs.

![chlimage_1-149](assets/chlimage_1-149.png)

>[!NOTE]
>
>Pour obtenir la liste des analyseurs disponibles, consultez la documentation de l’API de votre version Lucene.

#### Spécification directe de la classe d’analyseur {#specifying-the-analyzer-class-directly}

Si vous souhaitez utiliser un analyseur prêt à l’emploi, vous pouvez le configurer comme suit :

1. Localisez l’index avec lequel vous souhaitez utiliser l’analyseur sous le nœud `oak:index`.

1. Dans l’index, créez un nœud enfant appelé `default` de type `nt:unstructured`.

1. Ajoutez une propriété au nœud par défaut avec les propriétés suivantes :

   * **Nom :** `class`
   * **Type :** `String`
   * **Valeur :** `org.apache.lucene.analysis.standard.StandardAnalyzer`

   La valeur est le nom de la classe d’analyseur que vous souhaitez utiliser.

   Vous pouvez également définir l’analyseur à utiliser avec une version spécifique de Lucene à l’aide de la propriété de chaîne `luceneMatchVersion` facultative. Une syntaxe valide à utiliser avec Lucene 4.7 serait :

   * **Nom :** `luceneMatchVersion`
   * **Type :** `String`
   * **Valeur :** `LUCENE_47`

   Si `luceneMatchVersion` n’est pas spécifié, Oak utilise la version Lucene avec laquelle il est fourni.

1. Si vous souhaitez ajouter un fichier de mots vides aux configurations de l’analyseur, vous pouvez créer un nœud sous le nœud `default` avec les propriétés suivantes :

   * **Nom :** `stopwords`
   * **Type :** `nt:file`

#### Création d’analyseurs par composition {#creating-analyzers-via-composition}

Les analyseurs peuvent également être composés en fonction de `Tokenizers`, `TokenFilters` et `CharFilters`. Vous pouvez effectuer cette opération en spécifiant un analyseur et en créant des nœuds enfants de ces générateurs de jetons et filtres facultatifs, qui seront appliqués dans l’ordre indiqué. Consultez également [https://cwiki.apache.org/confluence/display/solr/AnalyzersTokenizersTokenFilters#Specifying_an_Analyzer_in_the_schema](https://cwiki.apache.org/confluence/display/solr/AnalyzersTokenizersTokenFilters#Specifying_an_Analyzer_in_the_schema)

Prenez cette structure de nœud comme exemple :

* **Nom :** `analyzers`

   * **Nom :** `default`

      * **Nom :** `charFilters`
      * **Type :** `nt:unstructured`

         * **Nom :** `HTMLStrip`
         * **Nom :** `Mapping`

      * **Nom :** `tokenizer`

         * **Nom de la propriété :** `name`

            * **Type :** `String`
            * **Valeur :** `Standard`

      * **Nom :** `filters`
      * **Type :** `nt:unstructured`

         * **Nom :** `LowerCase`
         * **Nom :** `Stop`

            * **Nom de la propriété :** `words`

               * **Type :** `String`
               * **Valeur :** `stop1.txt, stop2.txt`

            * **Nom :** `stop1.txt`

               * **Type :** `nt:file`

            * **Nom :** `stop2.txt`

               * **Type :** `nt:file`

Les noms des filtres, charFilters et générateurs de jetons sont formés en supprimant les suffixes d’usine. Ainsi :

* `org.apache.lucene.analysis.standard.StandardTokenizerFactory` devient `standard` ;

* `org.apache.lucene.analysis.charfilter.MappingCharFilterFactory` devient `Mapping` ;

* `org.apache.lucene.analysis.core.StopFilterFactory` devient `Stop` ;

Tout paramètre de configuration requis pour la fabrique est spécifié en tant que propriété du nœud en question.

Dans des cas tels que le chargement de mots vides où le contenu des fichiers externes doit être chargé, le contenu peut être diffusé en créant un nœud enfant de type `nt:file` pour le fichier en question.

### Index Solr {#the-solr-index}

L’index Solr est dédié à la recherche en texte intégral, mais il peut également être utilisé pour indexer la recherche par chemin, restrictions de propriété et restrictions de type principal. Cela signifie que l’index Solr dans Oak peut être utilisé pour n’importe quel type de requête JCR.

L’intégration dans AEM se fait au niveau du référentiel, de sorte que Solr est l’un des index possibles qui peuvent être utilisés dans Oak, la nouvelle implémentation du référentiel fournie avec AEM.

Il peut être configuré pour fonctionner en tant que serveur distant avec l’instance AEM.

### Configuration d’AEM avec un seul serveur distant Solr {#configuring-aem-with-a-single-remote-solr-server}

AEM peut également être configuré pour travailler avec une instance de serveur distant Solr :

1. Téléchargez et procédez à l’extraction de la dernière version de Solr. Pour plus d’informations sur la procédure à suivre, consultez la [documentation sur l’installation d’Apache Solr](https://solr.apache.org/guide/6_6/installing-solr.html).
1. Créez à présent deux partitionnements Solr. Pour ce faire, vous devez créer des dossiers pour chaque partition dans le dossier dans lequel Solr a été décompressé :

   * Pour la première partition, créez le dossier :

   `<solrunpackdirectory>\aemsolr1\node1`

   * Pour la seconde partition, créez le dossier :

   `<solrunpackdirectory>\aemsolr2\node2`

1. Recherchez un exemple d’instance dans le package Solr. Cet environnement se situe dans un dossier nommé « `example` », à la racine du package.
1. Copiez les dossiers suivants de l’exemple d’instance vers les deux dossiers des partitions (`aemsolr1\node1` et `aemsolr2\node2`) :

   * `contexts`
   * `etc`
   * `lib`
   * `resources`
   * `scripts`
   * `solr-webapp`
   * `webapps`
   * `start.jar`

1. Créez un dossier appelé « `cfg` » dans chacun des deux dossiers des partitions.
1. Définissez vos fichiers de configuration Solr et Zookeeper dans les dossiers nouvellement créés `cfg`.

   >[!NOTE]
   >
   >Pour plus d’informations sur la configuration de Solr et ZooKeeper, consultez la [documentation sur la configuration de Solr](https://cwiki.apache.org/confluence/display/solr/ConfiguringSolr) et le [Guide de prise en main pour ZooKeeper](https://zookeeper.apache.org/doc/r3.1.2/zookeeperStarted.html).

1. Démarrez la première partition avec la prise en charge de ZooKeeper en accédant à `aemsolr1\node1` et en exécutant la commande suivante :

   ```xml
   java -Xmx2g -Dbootstrap_confdir=./cfg/oak/conf -Dcollection.configName=myconf -DzkRun -DnumShards=2 -jar start.jar
   ```

1. Démarrez la deuxième partition en accédant à `aemsolr2\node2` et en exécutant la commande suivante :

   ```xml
   java -Xmx2g -Djetty.port=7574 -DzkHost=localhost:9983 -jar start.jar
   ```

1. Une fois les deux partitions démarrées, vérifiez que tout est en état de marche en vous connectant à l’interface à l’adresse `http://localhost:8983/solr/#/`.
1. Démarrez AEM et accédez à la console web à l’adresse `http://localhost:4502/system/console/configMgr`.
1. Définissez la configuration suivante dans la **configuration du serveur distant Solr Oak** :

   * URL HTTP Solr : `http://localhost:8983/solr/`

1. Sélectionnez **Solr distant** dans la liste déroulante sous le fournisseur de serveurs **Oak Solr**.

1. Accédez à CRXDE et connectez-vous en tant qu’administrateur ou administratrice.
1. Créez un nœud appelé **solrIndex** sous **oak:index** et définissez les propriétés suivantes :

   * **type :** solr (de type Chaîne)
   * **async :** async (de type Chaîne)
   * **reindex :** true (de type booléen)

1. Enregistrez les modifications.

#### Configuration recommandée pour Solr {#recommended-configuration-for-solr}

Vous trouverez ci-dessous un exemple de configuration de base adaptée aux trois déploiements Solr décrits dans cet article. Il s’adapte aux index de propriété dédiés qui sont déjà présents dans AEM et ne doit pas être utilisé avec d’autres applications.

Pour l’utiliser correctement, vous devez placer le contenu de l’archive directement dans le répertoire de base Solr. Dans le cas de déploiements avec plusieurs nœuds, il doit être placé directement sous le dossier racine de chaque nœud.

Fichiers de configuration recommandés pour Solr

[Obtenir le fichier](assets/recommended-conf.zip)

### Outils d’indexation AEM {#aem-indexing-tools}

AEM 6.1 intègre également deux outils d’indexation présents dans AEM 6.0 dans le cadre de l’ensemble d’outils d’Adobe Consulting Services Commons :

1. **Expliquer la requête**, un outil conçu pour aider les administrateurs et les administratrices à comprendre le mode d’exécution des requêtes ;
1. **Oak Index Manager**, une interface utilisateur web pour la maintenance des index existants.

Vous pouvez maintenant y accéder à partir de l’écran de bienvenue d’AEM, sous **Outils - Opérations - Tableau de bord - Diagnostic**.

Pour plus d’informations sur leur utilisation, consultez la [documentation du tableau de bord des opérations](/help/sites-administering/operations-dashboard.md).

#### Créer des index de propriété au moyen d’OSGi {#creating-property-indexes-via-osgi}

Le package ACS Commons expose également les configurations OSGi qui peuvent être utilisées pour créer des index de propriété.

Vous pouvez y accéder à partir de la console web en recherchant « **Ensure Oak Property Index** ».

![chlimage_1-150](assets/chlimage_1-150.png)

### Résolution des problèmes d’indexation {#troubleshooting-indexing-issues}

Des situations peuvent entraîner l’exécution lente des requêtes et un temps lent de réponse général du système.

Cette section présente un ensemble de recommandations sur la marche à suivre pour trouver la cause de ces problèmes et présente des conseils sur la manière d’y remédier.

#### Obtenir des informations de débogage pour l’analyse {#preparing-debugging-info-for-analysis}

La façon la plus simple d’obtenir les informations requises pour la requête en cours d’exécution est via l’[outil Explain Query](/help/sites-administering/operations-dashboard.md#explain-query). Vous pouvez ainsi collecter des informations précises nécessaires au débogage d’une requête lente, sans avoir à consulter les informations des journaux. Cette méthode est préférable si vous connaissez la requête qui est en cours de débogage.

Si cela n’est pas possible pour une raison quelconque, vous pouvez rassembler les journaux d’indexation dans un seul fichier pour résoudre votre problème.

#### Activer la journalisation {#enable-logging}

Pour activer la journalisation, vous devez activer les journaux de niveau **DEBUG** pour les catégories relatives à l’indexation et aux requêtes Oak. Ces catégories sont les suivantes :

* org.apache.jackrabbit.oak.plugins.index
* org.apache.jackrabbit.oak.query
* com.day.cq.search

La catégorie **com.day.cq.search** ne s’applique que si vous utilisez l’utilitaire QueryBuilder fourni par AEM.

>[!NOTE]
>
>Il est important que les journaux ne soient définis sur DEBUG que pendant la durée d’exécution de la requête que vous souhaitez résoudre. Sinon, un grand nombre d’événements sont générés dans les journaux au fil du temps. Pour cette raison, une fois que les journaux requis sont collectés, basculez vers la journalisation au niveau INFO pour les catégories mentionnées ci-dessus.

Vous pouvez activer la journalisation en procédant comme suit :

1. Pointez votre navigateur sur `https://serveraddress:port/system/console/slinglog`.
1. Cliquez sur le bouton **Ajouter un nouvel enregistreur** dans la partie inférieure de la console.
1. Dans la ligne que vous venez de créer, ajoutez les catégories mentionnées ci-dessus. Vous pouvez utiliser le signe **+** pour ajouter plus d’une catégorie à un seul journal.
1. Sélectionnez **DEBUG** dans la liste déroulante **Niveau de journal**.
1. Définissez le fichier de sortie sur `logs/queryDebug.log`. Cela corrélera tous les événements DEBUG dans un seul fichier journal.
1. Exécutez la requête ou effectuez le rendu de la page qui utilise la requête que vous souhaitez déboguer.
1. Une fois que vous avez exécuté la requête, revenez à la console de journalisation et modifiez le niveau du journal nouvellement créé en le passant sur **INFO**.

#### Configuration de l’index {#index-configuration}

La configuration de l’index influence largement la manière dont la requête est évaluée. Il est important de faire analyser la configuration de l’index ou de l’envoyer à l’assistance. Vous pouvez obtenir la configuration sous la forme d’un package de contenu ou un rendu JSON.

En règle générale, la configuration d’indexation est stockée sous le nœud `/oak:index` dans CRXDE. Vous pouvez obtenir la version JSON à l’adresse :

`https://serveraddress:port/oak:index.tidy.-1.json`

Si l’index est configuré à un autre emplacement, modifiez le chemin en conséquence.

#### Sortie de MBeans {#mbean-output}

Il est parfois utile de fournir la sortie des MBeans liés à l’index pour le débogage. Vous pouvez le faire en procédant comme suit :

1. Accédez à la console JMX à l’adresse :
   `https://serveraddress:port/system/console/jmx`

1. Recherchez les MBeans suivants :

   * Statistiques d’index Lucene
   * Statistiques de prise en charge de CopyOnRead
   * Statistiques de requête Oak
   * IndexStats

1. Cliquez sur chacun des MBeans pour obtenir des statistiques de performances. Créez une copie d’écran ou notez-les au cas où un envoi au service d’assistance serait nécessaire.

Vous pouvez également obtenir la variante JSON de ces statistiques en accédant aux URL suivantes :

* `https://serveraddress:port/system/sling/monitoring/mbeans/org/apache/jackrabbit/oak/%2522LuceneIndex%2522.tidy.-1.json`
* `https://serveraddress:port/system/sling/monitoring/mbeans/org/apache/jackrabbit/oak/%2522LuceneIndex%2522.tidy.-1.json`
* `https://serveraddress:port/system/sling/monitoring/mbeans/org/apache/jackrabbit/oak/%2522LuceneIndex%2522.tidy.-1.json`
* `https://serveraddress:port/system/sling/monitoring/mbeans/org/apache/jackrabbit/oak/%2522LuceneIndex%2522.tidy.-1.json`

Vous pouvez également fournir une sortie JMX consolidée via `https://serveraddress:port/system/sling/monitoring/mbeans/org/apache/jackrabbit/oak.tidy.3.json`. Cela inclut tous les détails liés à MBean Oak au format JSON.

#### Autres détails {#other-details}

Vous pouvez rassembler des informations supplémentaires pour résoudre le problème, telles que :

1. Version Oak sur laquelle votre instance s’exécute. Vous pouvez l’afficher en ouvrant CRXDE et en affichant la version dans le coin inférieur droit de la page d’accueil ou en vérifiant la version du lot `org.apache.jackrabbit.oak-core`.
1. La sortie du débogueur QueryBuilder de la requête posant problème. Le débogueur est accessible à l’adresse : `https://serveraddress:port/libs/cq/search/content/querydebug.html`.
