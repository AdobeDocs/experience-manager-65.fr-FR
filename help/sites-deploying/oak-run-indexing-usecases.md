---
title: Indexation du fichier Oak-run.jar – Scénarios d’utilisation
description: Découvrez les différents cas d’utilisation pour effectuer une indexation avec l’outil Oak-run.
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: deploying
noindex: true
exl-id: d25e3070-080a-4594-8fdb-9f09164135fc
solution: Experience Manager, Experience Manager Sites
feature: Deploying
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '1380'
ht-degree: 100%

---

# Indexation du fichier Oak-run.jar – Scénarios d’utilisation{#oak-run-jar-indexing-use-cases}

Oak-run prend en charge tous les scénarios d’indexation sur la ligne de commande, sans qu’il faille orchestrer l’exécution de ces scénarios par le biais de la console JMX d’AEM.

Les principaux avantages liés à l’utilisation de la commande d’index oak-run.jar pour la gestion des index Oak sont les suivants :

1. La commande d’index Oak-run fournit un nouvel ensemble d’outils d’indexation pour AEM 6.4.
1. Oak-run diminue le temps de réindexation, ce qui réduit le délai de réindexation sur des référentiels plus volumineux.
1. Oak-run réduit la consommation de ressources lors de la réindexation dans AEM, ce qui entraîne de meilleures performances globales du système.
1. Oak-run fournit une réindexation hors bande, prenant en charge les situations dans lesquelles la production doit être disponible et ne peut pas tolérer la maintenance ou les temps d&#39;arrêt autrement nécessaires à la réindexation.

Les sections ci-dessous fournissent des exemples de commandes. La commande d’index Oak-run prend en charge toutes les configurations NodeStore et BlobStore. Les exemples fournis ci-dessous concernent des configurations comportant FileDataStore et SegmentNodeStore.

## Cas d’utilisation 1 – Vérification de cohérence d’index {#usercase1indexconsistencycheck}

Il s’agit d’un cas d’utilisation lié à la corruption d’index. Parfois, il n’était pas possible de déterminer lesquels des index étaient corrompus. Par conséquent, Adobe a fourni des outils offrant les fonctionnalités suivantes :

1. Cette méthode effectue des contrôles de cohérence sur tous les index et génère un rapport sur les index valides et non valides.
1. Les fonctionnalités peuvent être utilisées même si AEM n’est pas accessible.
1. Cette méthode est facile à utiliser.

La recherche d’index corrompus peut être effectuée au moyen de l’opération `--index-consistency-check` :

```shell
java -jar oak-run*.jar index --fds-path=/path/to/datastore  /path/to/segmentstore/ --index-consistency-check
```

Cette opération génère un rapport dans `indexing-result/index-consistency-check-report.txt`. Voir ci-dessous pour un exemple de rapport :

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

Cet outil peut désormais être utilisé par l’assistance et l’administrateur ou l’administratrice système pour déterminer rapidement quels index sont corrompus, puis les réindexer.

## Cas d’utilisation 2 – Statistiques d’index {#usecase2indexstatistics}

Pour diagnostiquer certains cas liés aux performances des requêtes, Adobe avait souvent besoin d’une définition d’index existante et de statistiques liées à l’index provenant de la configuration du client ou de la cliente. Jusqu’à présent, ces informations étaient dispersées sur plusieurs ressources. Pour faciliter le dépannage, Adobe a créé des outils qui :

1. vident toute la définition d’index présente sur le système dans un seul fichier JSON ;

1. vident les statistiques importantes des index existants ;

1. vident le contenu de l’index en vue d’une analyse hors ligne ;

1. peuvent être utilisés même si AEM n’est pas accessible.

Les opérations ci-dessus peuvent désormais être effectuées par le biais des commandes d’index d’opération suivantes :

* `--index-info` : collecte et vide diverses statistiques liées aux index.

* `--index-definitions` : collecte et vide des définitions d’index.

* `--index-dump` : vide le contenu de l’index.

Vous trouverez, ci-dessous, un exemple d’utilisation pratique des commandes :

```shell
java -jar oak-run*.jar index --fds-path=/path/to/datastore  /path/to/segmentstore/ --index-info --index-definitions --index-dump
```

Les rapports sont générés dans `indexing-result/index-info.txt` et dans `indexing-result/index-definitions.json`

De plus, les mêmes détails sont fournis via la console web et font partie du fichier zip de configuration. Ils se trouvent à l’emplacement suivant :

`https://serverhost:serverport/system/console/status-oak-index-defn`

### Avantages {#uc2benefits}

Cet outil permet de collecter rapidement tous les détails requis liés aux problèmes d’indexation ou de requête et de réduire le temps passé à extraire ces informations.

## Cas d’utilisation 3 – Réindexation {#usecase3reindexing}

En fonction des [scénarios](https://jackrabbit.apache.org/oak/docs/query/indexing.html#reindexing), une réindexation doit être parfois effectuée. Actuellement, la réindexation s’effectue en définissant l’indicateur `reindex` sur `true` dans le nœud de définition d’index via CRXDE ou via l’interface utilisateur du Gestionnaire d’index. Une fois l’indicateur défini, la réindexation est effectuée de manière asynchrone.

Voici quelques points à noter autour de la réindexation :

* La réindexation s’avère beaucoup plus lente sur les configurations `DocumentNodeStore` que sur les configurations `SegmentNodeStore` dans lesquelles tout le contenu est local.

* Avec la conception actuelle, la situation est la suivante : pendant la réindexation, le moteur d’indexation asynchrone est bloqué, et tous les autres index deviennent obsolètes et ne sont plus mis à jour pendant la durée de l’indexation. Par conséquent, si le système est en cours d’utilisation, il se peut que les utilisateurs et utilisatrices n’aient pas accès à des résultats actualisés.
* La réindexation implique la traversée de l’ensemble du référentiel, ce qui peut faire peser une charge importante sur la configuration AEM et, partant, avoir une incidence sur l’expérience utilisateur.
* Dans le cas d’une installation `DocumentNodeStore` dans laquelle la réindexation peut prendre un temps considérable, si la connexion à la base de données Mongo échoue en plein milieu de l’opération, l’indexation doit être relancée depuis le début.

* Parfois, la réindexation peut prendre beaucoup de temps en raison de l’extraction de texte. Cela est spécifique aux configurations contenant de nombreux fichiers PDF, où le temps consacré à l’extraction de texte peut avoir un impact sur le temps d’indexation.

Pour atteindre ces objectifs, l’outil d’index oak-run prend en charge différents modes de réindexation qui peuvent être utilisés selon les besoins. La commande d’index oak-run offre les avantages suivants :

* **Réindexation hors-bande** : la réindexation oak-run peut être effectuée séparément d’une configuration AEM en cours d’exécution, ce qui réduit l’impact sur l’instance AEM en cours d’utilisation.

* **Réindexation hors-piste** : la réindexation s’effectue sans que cela n’ait d’incidence sur les opérations d’indexation. Cela signifie que le moteur d’indexation asynchrone peut continuer à indexer d’autres index.

* **Réindexation simplifiée pour les installations** : pour les installations `DocumentNodeStore`, la réindexation peut être réalisée avec une seule commande, ce qui garantit une exécution optimale.

* **Prise en charge de la mise à jour des définitions d’index et de l’ajout de nouvelles définitions d’index**

### Réindexation – DocumentNodeStore {#reindexdocumentnodestore}

Pour les installations `DocumentNodeStore`, la réindexation peut être effectuée au moyen d’une seule commande oak-run :

```shell
java -jar oak-run*.jar index --reindex --index-paths=/oak:index/lucene --read-write --fds-path=/path/to/datastore mongodb://server:port/aem
```

Cela offre les avantages suivants :

* Impact minimal sur l’exécution des instances AEM. La plupart des lectures peuvent être effectuées à partir de serveurs secondaires et les activités de traversée requises pour la réindexation n’ont pas de répercussions négatives sur les caches AEM en cours d’exécution.
* Les utilisateurs et utilisatrices peuvent également fournir un fichier JSON d’un index nouveau ou mis à jour par le biais de l’option `--index-definitions-file`.

### Réindexation – SegmentNodeStore {#reindexsegmentnodestore}

Pour les installations `SegmentNodeStore`, la réindexation peut être effectuée de l’une des façons suivantes :

#### Réindexation en ligne – SegmentNodeStore {#onlinereindexsegmentnodestore}

Suivez la méthode habituelle où la réindexation est effectuée en définissant l’indicateur `reindex`.

#### Réindexation en ligne – SegmentNodeStore – L’instance AEM est en cours d’exécution. {#onlinereindexsegmentnodestoretheaeminstanceisrunning}

Dans le cas des installations `SegmentNodeStore`, un seul processus peut accéder à des fichiers de segment en mode lecture/écriture. Pour cette raison, certaines opérations d’indexation oak-run nécessitent des étapes manuelles supplémentaires.

Cela impliquerait les opérations suivantes :

1. Texte de l’étape
1. Connectez `oak-run` au même référentiel que celui utilisé par AEM en mode lecture seule et procédez à l’indexation. Voici un exemple de commande à exécuter pour réaliser cette opération :

   ```shell
   java -jar oak-run-1.7.6.jar index --fds-path=/Users/dhasler/dev/cq/quickstart/target/crx-quickstart/repository/datastore/ --checkpoint 26b7da38-a699-45b2-82fb-73aa2f9af0e2 --reindex --index-paths=/oak:index/lucene /Users/dhasler/dev/cq/quickstart/target/crx-quickstart/repository/segmentstore/
   ```

1. Pour terminer, importez les fichiers d’index créés au moyen de l’opération `IndexerMBean#importIndex` à partir du chemin où oak-run a enregistré les fichiers d’indexation après avoir exécuté la commande ci-dessus.

Dans ce scénario, vous n’avez pas besoin d’arrêter le serveur AEM ni de configurer une nouvelle instance. Cependant, comme l’indexation implique la traversée de l’ensemble du référentiel, cela augmenterait la charge d’E/S sur l’installation, ce qui aurait un impact négatif sur les performances d’exécution.

#### Réindexation en ligne – SegmentNodeStore – L’instance AEM est arrêtée {#onlinereindexsegmentnodestoreaeminstanceisdown}

Pour les installations `SegmentNodeStore`, la réindexation peut être effectuée au moyen d’une seule commande oak-run. Toutefois, l’instance AEM doit être arrêtée.

Vous pouvez déclencher la réindexation avec la commande suivante :

```shell
java -jar oak-run*.jar index --reindex --index-paths=/oak:index/lucene --read-write --fds-path=/path/to/datastore  /path/to/segmentstore/
```

La différence entre cette approche et celle expliquée ci-dessus est que la création de points de contrôle et l&#39;importation d’index s’effectuent automatiquement. L’inconvénient est qu’AEM doit être arrêté pendant le processus.

#### Réindexation hors bande – SegmentNodeStore {#outofbandreindexsegmentnodestore}

Dans ce cas d’utilisation, vous pouvez effectuer une réindexation sur une configuration clonée pour minimiser l’impact sur l’instance AEM en cours d’exécution :

1. Créez un point de contrôle via une opération JMX. Pour ce faire, vous pouvez accéder à la [Console JMX](/help/sites-administering/jmx-console.md) et rechercher `CheckpointManager`. Cliquez ensuite sur l’opération **createCheckpoint(long p1)** avec une valeur d’expiration élevée, en secondes (par exemple, **2592000**).
1. Copiez le dossier `crx-quickstart` sur un nouvel ordinateur.
1. Effectuez une réindexation au moyen de la commande d’index oak-run.

1. Copiez les fichiers d’index générés sur le serveur AEM.

1. Importez les fichiers d’index via JMX.

Dans ce scénario d’utilisation, on part du principe que le magasin de données est accessible sur une autre instance, ce qui peut s’avérer impossible si `FileDataStore` est placé sur une solution de stockage cloud telle qu’EBS. Cela exclut le scénario dans lequel `FileDataStore` est également cloné. Si la définition d’index n’effectue pas d’indexation du texte intégral, il n’est pas nécessaire d’accéder à `DataStore`.

## Cas d’utilisation 4 – Mise à jour des définitions d’index {#usecase4updatingindexdefinitions}

Actuellement, vous pouvez envoyer des modifications de définition d’index via le package [ACS Ensure Index](https://adobe-consulting-services.github.io/acs-aem-commons/features/ensure-oak-index/index.html). Cela permet d’envoyer les définitions d’index au moyen du package de contenu, ce qui exigera, par la suite, que la réindexation soit effectuée en définissant l’indicateur `reindex` sur `true`.

Cela fonctionne bien sur des petites installations pour lesquelles la réindexation prend peu de temps. . Cependant, pour les référentiels volumineux, la réindexation est effectuée dans un délai considérablement plus long. Pour de tels cas, nous pouvons désormais utiliser l’outil d’indexation oak-run.

Oak-run prend désormais en charge la fourniture de définitions d’index au format JSON et la création d’index en mode hors bande où aucune modification n’est effectuée sur une instance active.

Le processus à prendre en compte pour ce cas d’utilisation est le suivant :

1. Un développeur ou une développeuse met à jour les définitions d’index sur une instance locale, puis génère un fichier JSON de définition d’index au moyen de l’option `--index-definitions`.

1. Le fichier JSON mis à jour est ensuite donné à l’équipe d’administration système.
1. Celle-ci suit la méthode hors-bande et prépare l’index sur une autre installation.
1. Une fois cette opération terminée, les fichiers d’index générés seront importés sur une installation AEM active.
