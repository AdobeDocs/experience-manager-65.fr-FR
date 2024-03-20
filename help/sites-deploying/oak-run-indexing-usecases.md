---
title: Indexation du fichier Oak-run.jar – Scénarios d’utilisation
description: Découvrez les différents cas d’utilisation de l’indexation à l’aide de l’outil exécuté par Oak.
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: deploying
noindex: true
exl-id: d25e3070-080a-4594-8fdb-9f09164135fc
solution: Experience Manager, Experience Manager Sites
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '1380'
ht-degree: 26%

---

# Indexation du fichier Oak-run.jar – Scénarios d’utilisation{#oak-run-jar-indexing-use-cases}

Oak-run prend en charge les cas d’utilisation d’indexation sur la ligne de commande sans avoir à orchestrer l’exécution de ces cas d’utilisation par le biais de la console JMX AEM.

Les principaux avantages liés à l’utilisation de la commande d’index oak-run.jar pour la gestion des index Oak sont les suivants :

1. La commande d’index Oak-run fournit un nouveau jeu d’outils d’indexation pour AEM 6.4.
1. Oak-run réduit la durée de réindexation, ce qui réduit les temps de réindexation sur les référentiels plus volumineux.
1. Oak-run réduit la consommation de ressources lors de la réindexation dans AEM, ce qui se traduit par de meilleures performances globales du système.
1. Oak-run fournit une réindexation hors-bande, ce qui prend en charge les situations où la production doit être disponible et ne peut pas tolérer de maintenance ou de temps d’arrêt autrement requis pour la réindexation.

Les sections ci-dessous fournissent des exemples de commandes. La commande d’index Oak-run prend en charge toutes les configurations NodeStore et BlobStore. Les exemples fournis ci-dessous concernent les configurations avec FileDataStore et SegmentNodeStore.

## Cas d’utilisation 1 - Contrôle de cohérence de l’index {#usercase1indexconsistencycheck}

Il s’agit d’un cas d’utilisation lié à la corruption d’index. Parfois, il n&#39;était pas possible de déterminer les index corrompus. Par conséquent, Adobe a fourni des outils qui :

1. Cette méthode effectue des contrôles de cohérence sur tous les index et génère un rapport sur les index valides et non valides.
1. Les fonctionnalités peuvent être utilisées même si AEM n’est pas accessible.
1. Cette méthode est facile à utiliser.

La vérification des index corrompus peut être effectuée au moyen de `--index-consistency-check` operation :

```shell
java -jar oak-run*.jar index --fds-path=/path/to/datastore  /path/to/segmentstore/ --index-consistency-check
```

Cela génère un rapport dans `indexing-result/index-consistency-check-report.txt`. Voir ci-dessous un exemple de rapport :

```
Valid indexes :
        - /content/oak:index/enablementResourceName
        - /oak:index/cqProjectLucene
        - /oak:index/cqTagLucene
        - /oak:index/lucene
        - /oak:index/ntBaseLucene
        - /oak:index/socialLucene
    Invalid indexes :
        - /oak:index/atDamIndex
        - /oak:index/atIndex
        - /oak:index/cqPageLucene
        - /oak:index/damAssetLucene
        - /oak:index/groups
        - /oak:index/slingeventJob
        - /oak:index/users
        - /oak:index/workflowDataLucene
    Ignored indexes as these are not of type lucene:
        - /oak:index/acPrincipalName
        - /oak:index/active
```

### Avantages {#uc1benefits}

Cet outil peut désormais être utilisé par l’assistance et l’administrateur système pour déterminer rapidement les index corrompus, puis les réindexer.

## Cas d’utilisation 2 - Statistiques des index {#usecase2indexstatistics}

Pour diagnostiquer certains cas concernant l’Adobe des performances des requêtes, une définition d’index existante était souvent requise, ainsi que des statistiques liées à l’index issues de la configuration du client. Jusqu&#39;à présent, ces informations ont été réparties sur plusieurs ressources. Pour faciliter le dépannage, Adobe a créé des outils qui :

1. videz toutes les définitions d’index présentes dans le système dans un seul fichier JSON ;

1. vident les statistiques importantes des index existants ;

1. vident le contenu de l’index en vue d’une analyse hors ligne ;

1. Est utilisable même si AEM n’est pas accessible

Les opérations ci-dessus peuvent désormais être effectuées à l’aide des commandes d’index d’opération suivantes :

* `--index-info` : collecte et vide diverses statistiques liées aux index.

* `--index-definitions` : collecte et vide des définitions d’index.

* `--index-dump` : vide le contenu de l’index.

Vous trouverez, ci-dessous, un exemple d’utilisation pratique des commandes :

```shell
java -jar oak-run*.jar index --fds-path=/path/to/datastore  /path/to/segmentstore/ --index-info --index-definitions --index-dump
```

Les rapports sont générés dans `indexing-result/index-info.txt` et dans `indexing-result/index-definitions.json`

En outre, les mêmes détails sont fournis par le biais de la console web et feraient partie du fichier zip de vidage de configuration. Ils sont accessibles à l’emplacement suivant :

`https://serverhost:serverport/system/console/status-oak-index-defn`

### Avantages {#uc2benefits}

Cet outil permet de collecter rapidement tous les détails requis relatifs aux problèmes d’indexation ou de requête et de réduire le temps consacré à l’extraction de ces informations.

## Cas d’utilisation 3 - Réindexation {#usecase3reindexing}

Selon le [scénarios](https://jackrabbit.apache.org/oak/docs/query/indexing.html#reindexing), la réindexation doit parfois être effectuée. Actuellement, la réindexation est effectuée en définissant la variable `reindex` indicateur pour `true` dans le noeud de définition d’index au moyen de CRXDE ou de l’interface utilisateur du gestionnaire d’index. Une fois l’indicateur défini, la réindexation est effectuée de manière asynchrone.

Certains points à noter concernant la réindexation :

* La réindexation s’avère beaucoup plus lente sur les configurations `DocumentNodeStore` que sur les configurations `SegmentNodeStore` dans lesquelles tout le contenu est local.

* Avec la conception actuelle, lorsque la réindexation se produit, l’indexeur asynchrone est bloqué et tous les autres index asynchrones deviennent obsolètes et ne sont pas mis à jour pendant l’indexation. Pour cette raison, si le système est en cours d’utilisation, les utilisateurs peuvent ne pas voir les résultats à jour ;
* La réindexation implique la traversée de l’ensemble du référentiel, ce qui peut faire peser une charge importante sur la configuration AEM et, partant, avoir une incidence sur l’expérience utilisateur.
* Dans le cas d’une installation `DocumentNodeStore` dans laquelle la réindexation peut prendre un temps considérable, si la connexion à la base de données Mongo échoue en plein milieu de l’opération, l’indexation doit être relancée depuis le début.

* Parfois, la réindexation peut prendre du temps en raison de l’extraction de texte. Ceci est spécifique aux configurations qui contiennent de nombreux fichiers de PDF, où le temps passé sur l’extraction de texte peut avoir une incidence sur le temps d’indexation.

Pour atteindre ces objectifs, l’outil d’index oak-run prend en charge différents modes de réindexation qui peuvent être utilisés selon les besoins. La commande d’index oak-run offre les avantages suivants :

* **Réindexation hors-bande** : la réindexation oak-run peut être effectuée séparément d’une configuration AEM en cours d’exécution, ce qui réduit l’impact sur l’instance AEM en cours d’utilisation.

* **Réindexation hors ligne** - La réindexation a lieu sans impact sur les opérations d’indexation. Cela signifie que le moteur d’indexation asynchrone peut continuer à indexer d’autres index.

* **Réindexation simplifiée pour les installations** : pour les installations `DocumentNodeStore`, la réindexation peut être réalisée avec une seule commande, ce qui garantit une exécution optimale.

* **Prise en charge de la mise à jour des définitions d’index et de l’ajout de nouvelles définitions d’index**

### Réindexation – DocumentNodeStore {#reindexdocumentnodestore}

Pour `DocumentNodeStore` La réindexation des installations peut être effectuée au moyen d’une seule commande oak-run :

```shell
java -jar oak-run*.jar index --reindex --index-paths=/oak:index/lucene --read-write --fds-path=/path/to/datastore mongodb://server:port/aem
```

Les avantages suivants sont proposés :

* Impact minimal sur l’exécution des instances AEM. La plupart des lectures peuvent être effectuées à partir de serveurs secondaires et l’exécution des caches d’AEM n’est pas affectée en raison de la traversée requise pour la réindexation.
* Les utilisateurs peuvent également fournir un fichier JSON d’un index nouveau ou mis à jour au moyen de l’option `--index-definitions-file` .

### Réindexation – SegmentNodeStore {#reindexsegmentnodestore}

Pour les installations `SegmentNodeStore`, la réindexation peut être effectuée de l’une des façons suivantes :

#### Réindexation en ligne – SegmentNodeStore {#onlinereindexsegmentnodestore}

Suivez la méthode établie où la réindexation est effectuée au moyen de la définition de `reindex` Indicateur.

#### Réindexation en ligne – SegmentNodeStore – L’instance AEM est en cours d’exécution. {#onlinereindexsegmentnodestoretheaeminstanceisrunning}

Pour `SegmentNodeStore` installations, un seul processus peut accéder aux fichiers de segments en mode lecture-écriture. Pour cette raison, certaines opérations dans l’indexation exécutée par Oak nécessitent des étapes manuelles supplémentaires.

Cela impliquerait les éléments suivants :

1. Texte de l’étape
1. Connectez-vous au `oak-run` dans le même référentiel que celui utilisé par AEM en mode lecture seule et en réalisant l’indexation. Voici un exemple de la manière d’y parvenir :

   ```shell
   java -jar oak-run-1.7.6.jar index --fds-path=/Users/dhasler/dev/cq/quickstart/target/crx-quickstart/repository/datastore/ --checkpoint 26b7da38-a699-45b2-82fb-73aa2f9af0e2 --reindex --index-paths=/oak:index/lucene /Users/dhasler/dev/cq/quickstart/target/crx-quickstart/repository/segmentstore/
   ```

1. Enfin, importez les fichiers d’index créés à l’aide de la fonction `IndexerMBean#importIndex` à partir du chemin où oak-run a enregistré les fichiers d’indexation après avoir exécuté la commande ci-dessus.

Dans ce scénario, il n’est pas nécessaire d’arrêter le serveur AEM ni de configurer une nouvelle instance. Cependant, comme l’indexation implique la traversée de l’ensemble du référentiel, elle augmenterait la charge d’E/S sur l’installation, ce qui aurait un impact négatif sur les performances d’exécution.

#### Réindexation en ligne - SegmentNodeStore - L’instance AEM est arrêtée {#onlinereindexsegmentnodestoreaeminstanceisdown}

Pour `SegmentNodeStore` installations, la réindexation peut être effectuée au moyen d’une seule commande oak-run. Toutefois, l’instance AEM doit être arrêtée.

Vous pouvez déclencher la réindexation à l’aide de la commande suivante :

```shell
java -jar oak-run*.jar index --reindex --index-paths=/oak:index/lucene --read-write --fds-path=/path/to/datastore  /path/to/segmentstore/
```

La différence entre cette approche et celle expliquée ci-dessus est que la création de points de contrôle et l’importation d’index sont effectués automatiquement. L&#39;inconvénient, c&#39;est que AEM doit être en panne pendant le processus.

#### Réindexation hors bande - SegmentNodeStore {#outofbandreindexsegmentnodestore}

Dans ce cas pratique, vous pouvez effectuer une réindexation sur une configuration clonée afin de minimiser l’impact sur l’instance AEM en cours d’exécution :

1. Créez un point de contrôle au moyen d’une opération JMX. Pour ce faire, vous pouvez accéder à la [Console JMX](/help/sites-administering/jmx-console.md) et rechercher `CheckpointManager`. Cliquez ensuite sur le bouton **createCheckpoint(long p1)** en utilisant une valeur d’expiration élevée en secondes (par exemple, **2592000**).
1. Copiez le dossier `crx-quickstart` sur un nouvel ordinateur.
1. Effectuez la réindexation au moyen de la commande d’index oak-run

1. Copiez les fichiers d’index générés sur le serveur AEM.

1. Importez les fichiers d’index au moyen de JMX.

Dans ce cas pratique, on suppose que l’entrepôt de données est accessible sur une autre instance, ce qui peut ne pas être possible si `FileDataStore` est placé sur une solution de stockage dans le cloud telle qu’EBS. Cela exclut le scénario dans lequel `FileDataStore` est également cloné. Si la définition d’index n’effectue pas d’indexation du texte intégral, il n’est pas nécessaire d’accéder à `DataStore`.

## Cas d’utilisation 4 – Mise à jour des définitions d’index {#usecase4updatingindexdefinitions}

Actuellement, vous pouvez envoyer les modifications de définition d’index par le biais de [Index ACS Ensure](https://adobe-consulting-services.github.io/acs-aem-commons/features/ensure-oak-index/index.html) module. Cela permet d’expédier les définitions d’index par le biais d’un module de contenu qui nécessite ensuite une réindexation en définissant la variable `reindex` indicateur pour `true`.

Cela fonctionne bien pour les installations plus petites où la réindexation ne prend pas beaucoup de temps. Toutefois, pour les référentiels volumineux, la réindexation s’effectue dans un délai considérablement plus long. Dans ce cas, nous pouvons désormais utiliser l’outil d’index oak-run.

Oak-run prend désormais en charge la fourniture de définitions d’index au format JSON et la création d’index en mode hors bande où aucune modification n’est effectuée sur une instance en direct.

Le processus à prendre en compte pour ce cas pratique est le suivant :

1. Un développeur met à jour les définitions d’index sur une instance locale, puis génère un fichier JSON de définition d’index au moyen de l’option `--index-definitions` option

1. Le fichier JSON mis à jour est ensuite donné à l’équipe d’administration système.
1. Celle-ci suit la méthode hors-bande et prépare l’index sur une autre installation.
1. Une fois cette opération terminée, les fichiers d’index générés sont importés sur une installation AEM en cours d’exécution.
