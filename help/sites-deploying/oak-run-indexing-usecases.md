---
title: Indexation du fichier Oak-run.jar – Scénarios d’utilisation
seo-title: Indexation du fichier Oak-run.jar – Scénarios d’utilisation
description: Découvrez les différents scénarios d’utilisation pour procéder à l’indexation à l’aide de l’outil Oak-run.
seo-description: Découvrez les différents scénarios d’utilisation pour procéder à l’indexation à l’aide de l’outil Oak-run.
uuid: 3c50080d-1e0d-4886-8d37-269f06881eb4
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: deploying
discoiquuid: 084075b8-826d-4f27-9342-35f33368f24f
noindex: true
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '1392'
ht-degree: 88%

---


# Indexation du fichier Oak-run.jar – Scénarios d’utilisation{#oak-run-jar-indexing-use-cases}

Oak-run prend en charge tous les scénarios d’indexation sur la ligne de commande, sans qu’il faille orchestrer l’exécution de ces scénarios par le biais de la console JMX d’AEM.

Les principaux avantages de l&#39;utilisation de l&#39;approche de commande de l&#39;index oak-run.jar pour la gestion des index Oak sont les suivants :

1. La commande Oak-run index fournit un nouvel ensemble d&#39;outils d&#39;indexation pour AEM 6.4.
1. Oak-run réduit la durée de réindexation, ce qui a un effet bénéfique sur les délais de réindexation des référentiels de grande taille.
1. Oak-run réduit la consommation des ressources au cours de la réindexation dans AEM, ce qui se traduit par de meilleures performances globales du système.
1. Oak-run fournit une réindexation hors-bande. Cette méthode prend en charge les situations dans lesquelles un environnement de production doit être disponible. Aucune maintenance ou période d’indisponibilité normalement requise pour la réindexation n’est tolérée.

Les sections suivantes fournissent des échantillons de commande. La commande d’index oak-run prend en charge toutes les configurations NodeStore et BlobStore. Les exemples fournis ci-dessous concernent les configurations avec FileDataStore et SegmentNodeStore.

## Cas d’utilisation 1 – Contrôle de cohérence de l’index {#usercase1indexconsistencycheck}

Il s’agit d’un cas d’utilisation lié à l’altération d’index. Dans certains cas, il s’avérait impossible de déterminer les index qui étaient altérés. C’est pourquoi Adobe a développé des outils qui :

1. effectuent des contrôles de cohérence sur tous les index, et génèrent un rapport sur les index valides et non valides ;
1. peuvent être utilisés même si AEM n’est pas accessible ;
1. sont faciles à utiliser.

Checking for corrupt indexes can be performed via `--index-consistency-check` operation:

```shell
java -jar oak-run*.jar index --fds-path=/path/to/datastore  /path/to/segmentstore/ --index-consistency-check
```

This will generate a report in `indexing-result/index-consistency-check-report.txt`. Vous trouverez, ci-dessous, un exemple de rapport :

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

Cet outil peut à présent être utilisé par le service d’assistance et l’administrateur système pour déterminer rapidement les index qui sont altérés, puis les réindexer.

## Cas d’utilisation 2 – Statistiques sur les index {#usecase2indexstatistics}

Pour diagnostiquer certains des cas relatifs aux performances des requêtes, Adobe nécessitait généralement une définition d’index existante ; des statistiques sur les requêtes provenant de la configuration du client. Jusqu’à présent, ces informations étaient disséminées sur plusieurs ressources. Pour faciliter le dépannage, Adobe a créé des outils qui :

1. vident toute la définition d’index présente sur le système dans un seul fichier JSON ;

1. vident les statistiques importantes des index existants ;

1. vident le contenu de l’index en vue d’une analyse hors ligne ;

1. peuvent être utilisés même si AEM n’est pas accessible.

Les opérations ci-dessus peuvent désormais être effectuées par le biais des commandes d’index d’opération suivantes :

* `--index-info` - Collecte et vidage de diverses statistiques relatives aux index

* `--index-definitions` - Collecte et vidage des définitions d&#39;index

* `--index-dump` - Extrait le contenu de l&#39;index

Vous trouverez, ci-dessous, un exemple d’utilisation pratique des commandes :

```shell
java -jar oak-run*.jar index --fds-path=/path/to/datastore  /path/to/segmentstore/ --index-info --index-definitions --index-dump
```

The reports would be generated in `indexing-result/index-info.txt` and `indexing-result/index-definitions.json`

Les mêmes informations sont, en outre, disponibles via la console web et font partie du fichier zip de vidage de la configuration. Elles sont accessibles à l’emplacement suivant :

`https://serverhost:serverport/system/console/status-oak-index-defn`

### Avantages {#uc2benefits}

Cet outil permet de collecter rapidement toutes les informations requises concernant les problèmes d’indexation ou de requête, et de réduire le temps consacré à l’extraction de ces informations.

## Cas d’utilisation 3 – Réindexation {#usecase3reindexing}

En fonction des [scénarios](https://jackrabbit.apache.org/oak/docs/query/indexing.html#reindexing), une réindexation doit être effectuée dans certains cas. Currently the reindexing is done by setting the `reindex` flag to `true` in the index definition node via CRXDE or via the Index Manager user interface. Une fois cet indicateur défini, la réindexation s’opère de façon asynchrone.

Quelques observations concernant la réindexation :

* La réindexation s’avère beaucoup plus lente sur les configurations `DocumentNodeStore` que sur les configurations `SegmentNodeStore` dans lesquelles tout le contenu est local.

* Avec la conception actuelle, la situation est la suivante : pendant la réindexation, le moteur d’indexation asynchrone est bloqué, et tous les autres index deviennent obsolètes et ne sont plus mis à jour pendant la durée de l’indexation. Par conséquent, si le système est en cours d’utilisation, il se peut que les utilisateurs n’aient pas accès à des résultats actualisés.
* La réindexation implique la traversée de l’ensemble du référentiel, ce qui peut faire peser une charge importante sur la configuration AEM et, partant, avoir une incidence sur l’expérience utilisateur.
* Dans le cas d’une installation `DocumentNodeStore` dans laquelle la réindexation peut prendre un temps considérable, si la connexion à la base de données Mongo échoue en plein milieu de l’opération, l’indexation doit être relancée depuis le début.

* Dans certains cas, la réindexation peut prendre un certain temps en raison de l’extraction de texte. Cela concerne tout particulièrement les configurations comprenant un grand nombre de fichiers PDF, où le temps consacré à l’extraction de texte peut avoir une incidence sur la durée d’indexation.

Pour répondre à ces objectifs, les outils d’index oak-run prennent en charge différents modes de réindexation qui peuvent être utilisés suivant les besoins. La commande d’index oak-run offre les avantages suivants :

* **Réindexation hors-bande** : la réindexation oak-run peut être effectuée séparément d’une configuration AEM en cours d’exécution, ce qui réduit l’impact sur l’instance AEM en cours d’utilisation.

* **Réindexation hors-piste** : la réindexation s’effectue sans que cela n’ait d’incidence sur les opérations d’indexation. Cela signifie que le moteur d’indexation asynchrone peut continuer à indexer d’autres index.

* **Réindexation simplifiée pour les installations** : pour les installations `DocumentNodeStore`DocumentNodeStore, la réindexation peut être réalisée avec une seule commande, ce qui garantit une exécution optimale.

* **Prise en charge de la mise à jour des définitions d’index et de l’ajout de nouvelles définitions d’index.**

### Réindexation – DocumentNodeStore {#reindexdocumentnodestore}

Pour les installations `DocumentNodeStore`, la réindexation peut être effectuée au moyen d’une seule commande oak-run:

```shell
java -jar oak-run*.jar index --reindex --index-paths=/oak:index/lucene --read-write --fds-path=/path/to/datastore mongodb://server:port/aem
```

Cela présente les avantages suivants :

* Incidence minimale sur les instances AEM en cours d’exécution. La plupart des lectures peuvent être effectuées à partir de serveurs secondaires et les activités de traversée requises pour la réindexation n’ont pas de répercussions négatives sur les caches AEM en cours d’exécution.
* Users can also provide a JSON of a new or updated index via the `--index-definitions-file` option.

### Réindexation – SegmentNodeStore {#reindexsegmentnodestore}

Pour les installations `SegmentNodeStore`, la réindexation peut être effectuée de l’une des façons suivantes :

#### Réindexation en ligne – SegmentNodeStore {#onlinereindexsegmentnodestore}

Follow the established way where reindexing is done via setting `reindex` flag.

#### Réindexation en ligne – SegmentNodeStore – L’instance AEM est en cours d’exécution {#onlinereindexsegmentnodestoretheaeminstanceisrunning}

Dans le cas des installations `SegmentNodeStore`, un seul processus peut accéder à des fichiers de segment en mode lecture/écriture. C’est la raison pour laquelle d’autres tâches manuelles doivent être effectuées avec certaines opérations de l’indexation oak-run.

Ces tâches sont notamment les suivantes :

1. Texte de l’étape
1. Connectez `oak-run` au même référentiel que celui utilisé par AEM en mode lecture seule et procédez à l’indexation. Voici un exemple de commande à exécuter pour réaliser cette opération :

   ```shell
   java -jar oak-run-1.7.6.jar index --fds-path=/Users/dhasler/dev/cq/quickstart/target/crx-quickstart/repository/datastore/ --checkpoint 26b7da38-a699-45b2-82fb-73aa2f9af0e2 --reindex --index-paths=/oak:index/lucene /Users/dhasler/dev/cq/quickstart/target/crx-quickstart/repository/segmentstore/
   ```

1. Pour terminer, importez les fichiers d’index créés au moyen de l’opération `IndexerMBean#importIndex` à partir de l’emplacement où oak-run a enregistré les fichiers d’indexation après avoir exécuté la commande ci-dessus.

Dans ce cas, il n’est pas nécessaire d’arrêter le serveur AEM, ni de provisionner une nouvelle instance. Cependant, comme l’indexation implique la traversée de l’ensemble du référentiel, cela augmentera la charge d’E/S sur l’installation, ce qui aura des répercussions négatives sur les performances d’exécution.

#### Réindexation en ligne – SegmentNodeStore – L’instance AEM est arrêtée {#onlinereindexsegmentnodestoreaeminstanceisdown}

Pour les installations `SegmentNodeStore`, la réindexation peut être effectuée au moyen d’une seule commande oak-run. Cependant, l’instance AEM doit être arrêtée.

Vous pouvez déclencher la réindexation à l’aide de la commande suivante :

```shell
java -jar oak-run*.jar index --reindex --index-paths=/oak:index/lucene --read-write --fds-path=/path/to/datastore  /path/to/segmentstore/
```

À la différence de la méthode décrite ci-dessus, la création du point de contrôle et l’importation de l’index sont, dans ce cas, effectuées automatiquement. L’inconvénient est qu’AEM doit être arrêté pendant le processus.

#### Réindexation hors-bande – SegmentNodeStore {#outofbandreindexsegmentnodestore}

Dans ce scénario, vous pouvez effectuer la réindexation sur une configuration clonée afin de réduire l’impact sur l’instance AEM en cours d’exécution :

1. Créez le point de contrôle au moyen d’une opération JMX. Pour ce faire, vous pouvez accéder à la [Console JMX](/help/sites-administering/jmx-console.md) et rechercher `CheckpointManager`. Then, click on the **createCheckpoint(long p1)** operation using a high value for expiration in seconds (for example, **2592000**).
1. Copy the `crx-quickstart` folder to a new machine
1. Effectuez la réindexation via la commande d’index oak-run.

1. Copiez les fichiers d’index générés sur le serveur AEM.

1. Importez les fichiers d’index via JMX.

Dans ce scénario d’utilisation, on part du principe que l’entrepôt de données est accessible sur une autre instance, ce qui peut s’avérer impossible si `FileDataStore` est placé sur une solution de stockage cloud telle qu’EBS. Cela exclut le scénario dans lequel `FileDataStore` est également cloné. Si la définition d’index n’effectue pas d’indexation du texte intégral, il n’est pas nécessaire d’accéder à `DataStore`.

## Cas d’utilisation 4 – Mise à jour des définitions d’index {#usecase4updatingindexdefinitions}

Actuellement, vous pouvez envoyer des modifications de définition d’index via le module [ACS Ensure Index](https://adobe-consulting-services.github.io/acs-aem-commons/features/ensure-oak-index/index.html). Cela permet d’envoyer les définitions d’index via le module de contenu, ce qui exigera, par la suite, que la réindexation soit effectuée en définissant l’indicateur `reindex` sur `true`.

Cela donne de bons résultats avec les plus petites installations pour lesquelles la réindexation est de courte durée. Cependant, pour les référentiels très volumineux, la réindexation prendra beaucoup plus de temps. Dans ce cas, il est désormais possible d’utiliser l’outil d’indexation oak-run.

Oak-run permet à présent de fournir des définitions d’index au format JSON et de créer l’index en mode hors-bande dans lequel aucune modification n’est effectuée sur une instance dynamique.

Le processus dont vous devez tenir compte pour ce scénario d’utilisation est le suivant :

1. A developer would update the index definitions on a local instance and then generate an index definition JSON file via the `--index-definitions` option

1. Le fichier JSON mis à jour est ensuite donné à l’administrateur système.
1. L’administrateur système suit la méthode hors-bande et prépare l’index sur une autre installation.
1. Une fois cette opération terminée, les fichiers d’index générés seront importés sur une installation AEM active.

