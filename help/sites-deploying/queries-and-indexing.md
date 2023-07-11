---
title: Requêtes et indexation Oak
description: Découvrez comment configurer des index dans AEM.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: deploying
legacypath: /content/docs/en/aem/6-0/deploy/upgrade/queries-and-indexing
feature: Configuring
exl-id: d9ec7728-84f7-42c8-9c80-e59e029840da
source-git-commit: b9c164321baa3ed82ae87a97a325fcf0ad2f6ca0
workflow-type: tm+mt
source-wordcount: '2619'
ht-degree: 35%

---

# Requêtes et indexation Oak{#oak-queries-and-indexing}

>[!NOTE]
>
>Cet article traite de la configuration des index dans AEM 6. Pour connaître les bonnes pratiques sur l’optimisation des requêtes et l’indexation des performances, consultez les [Bonnes pratiques relatives aux requêtes et à l’indexation](/help/sites-deploying/best-practices-for-queries-and-indexing.md).

## Présentation {#introduction}

Contrairement à Jackrabbit 2, Oak n’indexe pas le contenu par défaut. Les index personnalisés doivent être créés si nécessaire, tout comme avec les bases de données relationnelles traditionnelles. S’il n’existe aucun index pour une requête spécifique, il est possible que de nombreux noeuds soient parcourus. La requête peut encore fonctionner, mais elle est probablement assez lente.

Si Oak rencontre une requête sans index, un message de journal de niveau AVERTISSEMENT est imprimé :

```xml
*WARN* Traversed 1000 nodes with filter Filter(query=select ...) consider creating an index or changing the query
```

## Langues de requête prises en charge {#supported-query-languages}

Le moteur de requête Oak prend en charge les langues suivantes :

* XPath (recommandé)
* SQL-2
* SQL (obsolète)
* JQOM

## Types d’indexeur et calcul des coûts {#indexer-types-and-cost-calculation}

Le serveur principal basé sur Apache Oak permet à différents indexeurs d’être connectés au référentiel.

Un indexeur est le **Index de propriété**, pour laquelle la définition d’index est stockée dans le référentiel lui-même.

Les implémentations d’**Apache Lucene** et **Solr** sont également disponibles par défaut, et prennent en charge l’indexation du texte intégral.

L’**indexation transversale** est utilisé si aucun autre indexeur n’est disponible. Cela signifie que le contenu n’est pas indexé et que les noeuds de contenu sont parcourus pour trouver des correspondances avec la requête.

Si plusieurs indexeurs sont disponibles pour une requête, chaque indexeur disponible estime le coût d’exécution de la requête. Oak choisit ensuite l’indexeur avec le coût estimé le plus faible.

![chlimage_1-148](assets/chlimage_1-148.png)

Le diagramme ci-dessus est une représentation de haut niveau du mécanisme d’exécution de requête d’Apache Oak.

Tout d’abord, la requête est analysée dans une arborescence de syntaxe abstraite. Ensuite, la requête est vérifiée et transformée en SQL-2, qui est la langue native des requêtes Oak.

Ensuite, chaque index est consulté pour estimer le coût de la requête. Une fois terminé, les résultats de l’index le moins cher sont récupérés. Enfin, les résultats sont filtrés, à la fois pour s’assurer que l’utilisateur actuel a un accès en lecture au résultat et que le résultat correspond à la requête complète.

## Configuration des index {#configuring-the-indexes}

>[!NOTE]
>
>Pour un référentiel de grande taille, créer un index est une opération qui demande beaucoup de temps. Cela est vrai pour la création initiale d’un index et pour la réindexation (reconstruction d’un index après modification de la définition). Voir aussi [Dépannage des index Oak](/help/sites-deploying/troubleshooting-oak-indexes.md) et [Prévention d’une réindexation lente](/help/sites-deploying/troubleshooting-oak-indexes.md#preventing-slow-re-indexing).

Si la réindexation est nécessaire dans les référentiels volumineux, en particulier lorsque vous utilisez MongoDB et pour les index de texte intégral, envisagez la pré-extraction de texte et l’utilisation de oak-run pour créer l’index initial et réindexer.

Les index sont configurés en tant que noeuds dans le référentiel sous **Oak:index** noeud .

Le type du noeud d’index doit être **oak:QueryIndexDefinition.** Plusieurs options de configuration sont disponibles pour chaque indexeur en tant que propriétés de noeud. Pour plus d’informations, voir les détails de configuration pour chaque type d’indexeur ci-dessous.

### Index de propriété {#the-property-index}

L’index de propriété est utile pour les requêtes qui ont des contraintes de propriété, mais qui ne sont pas en texte intégral. Il peut être configuré en suivant la procédure ci-dessous :

1. Ouvrez CRXDE en accédant à `http://localhost:4502/crx/de/index.jsp`.
1. Créez un noeud sous **oak:index**
1. Nommez le noeud **PropertyIndex**, puis définissez le type de noeud sur **oak:QueryIndexDefinition**
1. Définissez les propriétés suivantes pour le nouveau noeud :

   * **Type :**  `property` (de type String)
   * **propertyNames :** `jcr:uuid` (de type Nom)

   Cet exemple particulier indexe la variable `jcr:uuid` dont la tâche est d’exposer l’identifiant unique universelle (UUID) du noeud auquel il est associé.

1. Enregistrez les modifications.

L’index de propriété comporte les options de configuration suivantes :

* Le **type** spécifie le type d’index. Dans ce cas, il doit être défini sur **property**

* Le **propertyNames** indique la liste des propriétés qui seront stockées dans l’index. En cas d’absence, le nom du noeud est utilisé comme valeur de référence de nom de propriété. Dans cet exemple, la variable **jcr:uuid** dont la tâche est d’exposer l’identifiant unique (UUID) de son noeud est ajouté à l’index.

* L’indicateur **unique**, qui, défini sur **true**, ajoute une limite d’unicité à l’index de propriété.

* Le **déclarationNodeTypes** permet de spécifier un certain type de noeud auquel l’index s’appliquera uniquement.
* Le **reindex** qui, s’il est défini sur **true**, déclenche une réindexation complète du contenu.

### Index ordonné {#the-ordered-index}

L’index trié est une extension de l’index Propriété. Cependant, elle a été abandonnée. Les index de ce type doivent être remplacés par le [Index de propriété Lucene](#the-lucene-property-index).

### Index de texte intégral Lucene {#the-lucene-full-text-index}

L’indexeur de texte intégral basé sur Apache Lucene est disponible dans AEM 6.

Si un index de texte intégral est configuré, toutes les requêtes ayant une condition de texte intégral utilisent l’index de texte intégral, qu’il existe d’autres conditions indexées ou non, qu’il y ait une restriction de chemin.

Si aucun index de texte intégral n’est configuré, les requêtes avec des conditions de texte intégral ne fonctionneront pas comme prévu.

Comme l’index est mis à jour via un thread d’arrière-plan asynchrone, certaines recherches de texte intégral ne sont pas disponibles pendant une petite période de temps jusqu’à ce que les processus d’arrière-plan soient terminés.

Vous pouvez configurer un index de texte intégral Lucene en suivant la procédure ci-dessous :

1. Ouvrez CRXDE et créez un noeud sous **oak:index**.
1. Nommez le noeud **LuceneIndex** et définissez le type de noeud sur **oak:QueryIndexDefinition**
1. Ajoutez les propriétés suivantes au nœud :

   * **type :**  `lucene` (de type String)
   * **async :**  `async` (de type String)

1. Enregistrez les modifications.

L’index Lucene présente les options de configuration suivantes :

* Le **type** qui spécifie le type d’index doit être défini sur **lucene**
* Le **async** qui doit être définie sur **async**. Cela envoie le processus de mise à jour de l’index à un thread d’arrière-plan.
* Le **includePropertyTypes** qui définit le sous-ensemble des types de propriétés inclus dans l’index.
* Le **excludePropertyNames** qui définit une liste de noms de propriétés - propriétés qui doivent être exclues de l’index.
* Le **reindex** Indicateur qui, lorsqu’il est défini sur **true**, déclenche une réindexation complète du contenu.

### Index de propriété Lucene {#the-lucene-property-index}

Depuis **Oak 1.0.8**, Lucene peut être utilisé pour créer des index qui impliquent des contraintes de propriété qui ne sont pas du texte intégral.

Pour obtenir un index de propriété Lucene, la variable **fulltextEnabled** doit toujours être définie sur false.

Considérez l’exemple de requête suivant :

```xml
select * from [nt:base] where [alias] = '/admin'
```

Pour définir un index de propriété Lucene pour la requête ci-dessus, vous pouvez ajouter la définition suivante en créant un noeud sous **oak:index:**

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
>Par rapport à l’index standard de propriété, l’index de propriété Lucene est toujours configuré en mode asynchrone. Par conséquent, les résultats renvoyés par l’index peuvent ne pas toujours refléter l’état le plus récent du référentiel.

>[!NOTE]
>
>Pour obtenir des informations plus détaillées sur l’index de propriété Lucene, reportez-vous à la page de documentation [Oak Lucene Apache Jackrabbit](https://jackrabbit.apache.org/oak/docs/query/lucene.html).

### Analyseurs Lucene {#lucene-analyzers}

Depuis la version 1.2.0, Oak prend en charge les analyseurs Lucene.

Les analyseurs sont utilisés lorsqu’un document est indexé et au moment de la requête. Un analyseur examine le texte des champs et génère un flux de jeton. Les analyseurs Lucene se composent d’une série de classes de jetons et de filtres.

Les analyseurs peuvent être configurées par l’intermédiaire du nœud `analyzers` (de type `nt:unstructured`), à l’intérieur de la définition `oak:index`.

L’analyseur par défaut pour un index est configuré dans l’enfant `default`du nœud des analyseurs.

![chlimage_1-149](assets/chlimage_1-149.png)

>[!NOTE]
>
>Pour obtenir la liste des analyseurs disponibles, consultez la documentation de l’API de la version Lucene que vous utilisez.

#### Spécification directe de la classe Analyzer {#specifying-the-analyzer-class-directly}

Si vous souhaitez utiliser un analyseur prêt à l’emploi, vous pouvez le configurer comme suit :

1. Recherchez l’index avec lequel vous souhaitez utiliser l’analyseur sous le `oak:index` noeud .

1. Dans l’index, créez un nœud enfant appelé `default` de type `nt:unstructured`.

1. Ajoutez une propriété au nœud par défaut avec les propriétés suivantes :

   * **Nom :** `class`
   * **Type :** `String`
   * **Valeur :** `org.apache.lucene.analysis.standard.StandardAnalyzer`

   La valeur est le nom de la classe d’analyseur que vous souhaitez utiliser.

   Vous pouvez également définir l’analyseur à utiliser avec une version spécifique de Lucene à l’aide de l’option `luceneMatchVersion` propriété de chaîne. Une syntaxe valide pour l’utiliser avec Lucene 4.7 serait :

   * **Nom :** `luceneMatchVersion`
   * **Type :** `String`
   * **Valeur :** `LUCENE_47`

   If `luceneMatchVersion` n’est pas fourni, Oak utilise la version de Lucene avec laquelle il est fourni.

1. Si vous souhaitez ajouter un fichier stopwords aux configurations de l’analyseur, vous pouvez créer un noeud sous `default` l’une avec les propriétés suivantes :

   * **Nom :** `stopwords`
   * **Type :** `nt:file`

#### Création d’analyseurs via la composition {#creating-analyzers-via-composition}

Les analyseurs peuvent également être classés en fonction de `Tokenizers`, `TokenFilters` et `CharFilters`. Vous pouvez effectuer cette opération en spécifiant un programme d’analyse et en créant des nœuds enfants de ces jetons et filtres facultatifs, qui seront appliqués dans l’ordre indiqué. Consultez également [https://wiki.apache.org/solr/AnalyzersTokenizersTokenFilters#Specifying_an_Analyzer_in_the_schema](https://wiki.apache.org/solr/AnalyzersTokenizersTokenFilters#Specifying_an_Analyzer_in_the_schema)

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

Le nom des filtres, charFilters et jetons est formé en supprimant les suffixes d’usine. Ainsi :

* `org.apache.lucene.analysis.standard.StandardTokenizerFactory` devient `standard` ;

* `org.apache.lucene.analysis.charfilter.MappingCharFilterFactory` devient `Mapping` ;

* `org.apache.lucene.analysis.core.StopFilterFactory` devient `Stop`.

Tout paramètre de configuration requis pour la fabrique est spécifié en tant que propriété du nœud en question.

Dans des cas tels que le chargement de mots vides quand le contenu des fichiers externes doit être chargé, le contenu peut être diffusé en créant un nœud enfant `nt:file` pour le fichier en question.

### L’index Solr {#the-solr-index}

L’index Solr a pour objectif la recherche en texte intégral, mais il peut également être utilisé pour indexer la recherche par chemin, par restrictions de propriété et par restrictions de type Principal. Cela signifie que l’index Solr dans Oak peut être utilisé pour n’importe quel type de requête JCR.

L’intégration dans AEM se fait au niveau du référentiel, de sorte que Solr soit l’un des index possibles qui peut être utilisé dans Oak, la nouvelle implémentation du référentiel fournie avec AEM.

Il peut être configuré pour fonctionner en tant que serveur distant avec l’instance AEM.

### Configuration d’AEM avec un seul serveur distant Solr {#configuring-aem-with-a-single-remote-solr-server}

AEM peut également être configuré pour travailler avec une instance de serveur distant Solr :

1. Téléchargez et extrayez la dernière version de Solr. Pour plus d’informations sur la procédure à suivre, voir [Documentation d’installation Apache Solr](https://cwiki.apache.org/confluence/display/solr/Installing+Solr).
1. Maintenant, créez deux éclats Solr. Pour ce faire, vous devez créer des dossiers pour chaque partition dans le dossier dans lequel Solr a été décompressé :

   * Pour la première partition, créez le dossier :

   `<solrunpackdirectory>\aemsolr1\node1`

   * Pour la seconde partition, créez le dossier :

   `<solrunpackdirectory>\aemsolr2\node2`

1. Recherchez un exemple d’instance dans le package Solr. Il se trouve dans un dossier appelé &quot; `example`&quot; dans la racine du module.
1. Copiez les dossiers suivants de l’instance d’exemple vers les deux dossiers des partitions (`aemsolr1\node1` et `aemsolr2\node2`) :

   * `contexts`
   * `etc`
   * `lib`
   * `resources`
   * `scripts`
   * `solr-webapp`
   * `webapps`
   * `start.jar`

1. Créez un dossier appelé &quot; `cfg`&quot; dans chacun des deux dossiers de partage.
1. Définissez vos fichiers de configuration Solr et Zookeeper dans les dossiers nouvellement créés `cfg`.

   >[!NOTE]
   >
   >Pour plus d’informations sur la configuration de Solr et ZooKeeper, consultez la [documentation sur la configuration de Solr](https://wiki.apache.org/solr/ConfiguringSolr) et le [Guide de prise en main pour ZooKeeper](https://zookeeper.apache.org/doc/r3.1.2/zookeeperStarted.html).

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

1. Choisir **Remote Solr** dans la liste déroulante sous **Oak Solr** fournisseur de serveur.

1. Accédez à CRXDE et connectez-vous en tant qu’administrateur.
1. Créez un noeud appelé **solrIndex** under **oak:index** et définissez les propriétés suivantes :

   * **type :** solr (de type Chaîne)
   * **async :** async (de type Chaîne)
   * **reindex :** true (de type booléen)

1. Enregistrez les modifications.

#### Configuration recommandée pour Solr {#recommended-configuration-for-solr}

Vous trouverez ci-dessous un exemple de configuration de base qui peut être utilisée avec les trois déploiements Solr décrits dans cet article. Il s’adapte aux index de propriété dédiés qui sont déjà présents dans AEM et ne doivent pas être utilisés avec d’autres applications.

Pour l’utiliser correctement, vous devez placer le contenu de l’archive directement dans le répertoire d’accueil Solr. Dans le cas de déploiements avec plusieurs nœuds, il doit être placé directement sous le dossier racine de chaque nœud.

Fichiers de configuration recommandés pour Solr

[Obtenir le fichier](assets/recommended-conf.zip)

### Outils d’indexation AEM {#aem-indexing-tools}

AEM 6.1 intègre également deux outils d’indexation présents dans AEM 6.0 dans le cadre de l’ensemble d’outils d’Adobe Consulting Services Commons :

1. **Expliquer la requête**, un outil conçu pour aider les administrateurs à comprendre le mode d’exécution des requêtes ;
1. **Oak Index Manager**, une interface utilisateur web pour la maintenance des index existants.

Vous pouvez désormais les atteindre en accédant à **Outils - Opérations - Tableau de bord - Diagnostic** dans l’écran de bienvenue d’AEM.

Pour plus d’informations sur leur utilisation, voir [Documentation du tableau de bord des opérations](/help/sites-administering/operations-dashboard.md).

#### Création d’index de propriété via OSGi {#creating-property-indexes-via-osgi}

Le package ACS Commons expose également les configurations OSGi qui peuvent être utilisées pour créer des index de propriété.

Vous pouvez y accéder à partir de la console web en recherchant &quot;**Vérification de l’index de propriété Oak**&quot;.

![chlimage_1-150](assets/chlimage_1-150.png)

### Résolution des problèmes d’indexation {#troubleshooting-indexing-issues}

Des situations peuvent survenir lorsque l’exécution des requêtes prend du temps et que le temps de réponse général du système est lent.

Cette section présente un ensemble de recommandations sur ce qui doit être fait pour déterminer la cause de ces problèmes et des conseils sur la manière de les résoudre.

#### Préparation des informations de débogage pour l’analyse {#preparing-debugging-info-for-analysis}

La façon la plus simple d’obtenir les informations requises pour la requête en cours d’exécution est via l’[outil Explain Query](/help/sites-administering/operations-dashboard.md#explain-query). Vous pouvez ainsi collecter les informations précises nécessaires au débogage d’une requête lente sans avoir à consulter les informations du niveau du journal. Cette méthode est préférable si vous connaissez la requête qui est en cours de débogage.

Si cela n’est pas possible pour une raison quelconque, vous pouvez rassembler les logs d’indexation dans un seul fichier et les utiliser pour résoudre votre problème particulier.

#### Activation de la journalisation {#enable-logging}

Pour activer la journalisation, vous devez activer **DEBUG** des logs de niveau pour les catégories relatives à l’indexation et aux requêtes Oak. Ces catégories sont les suivantes :

* org.apache.jackrabbit.oak.plugins.index
* org.apache.jackrabbit.oak.query
* com.day.cq.search

Le **com.day.cq.search** ne s’applique que si vous utilisez l’utilitaire QueryBuilder fourni par AEM.

>[!NOTE]
>
>Il est important que les journaux ne soient définis sur DEBUG que pendant la durée d’exécution de la requête que vous souhaitez résoudre. Dans le cas contraire, un grand nombre d’événements sont générés dans les journaux au fil du temps. Pour cette raison, une fois que les journaux requis sont collectés, basculez vers la journalisation au niveau INFO pour les catégories mentionnées ci-dessus.

Vous pouvez activer la journalisation en procédant comme suit :

1. Pointez votre navigateur sur `https://serveraddress:port/system/console/slinglog`.
1. Cliquez sur le bouton **Ajouter un nouvel enregistreur** dans la partie inférieure de la console.
1. Dans la ligne que vous venez de créer, ajoutez les catégories mentionnées ci-dessus. Vous pouvez utiliser le signe **+** pour ajouter plus d’une catégorie à un seul journal.
1. Choisir **DEBUG** de la **Niveau de journal** liste déroulante.
1. Définissez le fichier de sortie sur `logs/queryDebug.log`. Cela met en corrélation tous les événements DEBUG dans un seul fichier journal.
1. Exécutez la requête ou effectuez le rendu de la page qui utilise la requête que vous souhaitez déboguer.
1. Une fois que vous avez exécuté la requête, revenez à la console de journalisation et modifiez le niveau du journal nouvellement créé en le passant sur **INFO**.

#### Configuration de l’index {#index-configuration}

La manière dont la requête est évaluée est largement affectée par la configuration de l’index. Il est important de faire analyser la configuration de l’index ou de l’envoyer à la prise en charge. Vous pouvez obtenir la configuration sous la forme d’un module de contenu ou un rendu JSON.

En règle générale, la configuration d’indexation est stockée sous le `/oak:index` dans CRXDE, vous pouvez obtenir la version JSON à l’adresse :

`https://serveraddress:port/oak:index.tidy.-1.json`

Si l’index est configuré à un autre emplacement, modifiez le chemin en conséquence.

#### Sortie MBean {#mbean-output}

Il est parfois utile de fournir la sortie des MBeans liés à l’index pour le débogage. Vous pouvez le faire en procédant comme suit :

1. Accédez à la console JMX à l’adresse :
   `https://serveraddress:port/system/console/jmx`

1. Recherchez les MBeans suivants :

   * Statistiques de l’index Lucene
   * Statistiques de prise en charge de CopyOnRead
   * Statistiques de requête Oak
   * IndexStats

1. Cliquez sur chacun des MBeans pour obtenir les statistiques de performances. Créez une capture d’écran ou notez-les au cas où vous devez les envoyer au service d’assistance.

Vous pouvez également obtenir la variante JSON de ces statistiques en accédant aux URL suivantes :

* `https://serveraddress:port/system/sling/monitoring/mbeans/org/apache/jackrabbit/oak/%2522LuceneIndex%2522.tidy.-1.json`
* `https://serveraddress:port/system/sling/monitoring/mbeans/org/apache/jackrabbit/oak/%2522LuceneIndex%2522.tidy.-1.json`
* `https://serveraddress:port/system/sling/monitoring/mbeans/org/apache/jackrabbit/oak/%2522LuceneIndex%2522.tidy.-1.json`
* `https://serveraddress:port/system/sling/monitoring/mbeans/org/apache/jackrabbit/oak/%2522LuceneIndex%2522.tidy.-1.json`

Vous pouvez également fournir une sortie JMX consolidée via `https://serveraddress:port/system/sling/monitoring/mbeans/org/apache/jackrabbit/oak.tidy.3.json`. Cela inclut tous les détails liés à MBean Oak au format JSON.

#### Autres détails {#other-details}

Vous pouvez rassembler des informations supplémentaires pour résoudre le problème, telles que :

1. Version Oak sur laquelle votre instance s’exécute. Vous pouvez l’afficher en ouvrant CRXDE et en affichant la version dans le coin inférieur droit de la page d’accueil ou en vérifiant la version du lot `org.apache.jackrabbit.oak-core`.
1. La sortie du débogueur QueryBuilder de la requête posant problème. Le débogueur est accessible à l’adresse : `https://serveraddress:port/libs/cq/search/content/querydebug.html`.
