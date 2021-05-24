---
title: Utilisation de la réindexation hors ligne pour réduire les temps d’arrêt pendant une mise à niveau
description: Découvrez comment utiliser la méthodologie de réindexation hors ligne pour réduire le temps d’arrêt du système lors d’une mise à niveau d’AEM.
contentOwner: sarchiz
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: upgrading
content-type: reference
feature: Mise à niveau
exl-id: 85bc041e-0ab1-42de-8bcc-c98a175d7494
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1344'
ht-degree: 1%

---

# Utilisation de la réindexation hors ligne pour réduire les temps d’arrêt lors d’une mise à niveau {#offline-reindexing-to-reduce-downtime-during-upgrades}

## Présentation {#introduction}

L’un des principaux défis de la mise à niveau d’Adobe Experience Manager est le temps d’arrêt associé à l’environnement de création lorsqu’une mise à niveau statique est effectuée. Les auteurs de contenu ne pourront pas accéder à l’environnement au cours d’une mise à niveau. Il est donc souhaitable de réduire le temps nécessaire à la mise à niveau. Pour les référentiels volumineux, en particulier les projets AEM Assets, qui disposent généralement de grands entrepôts de données et d’un niveau élevé de chargement de ressources par heure, la réindexation des index Oak prend un pourcentage significatif du temps de mise à niveau.

Cette section décrit comment utiliser l’outil exécuté par Oak pour réindexer le référentiel **avant** d’effectuer la mise à niveau, réduisant ainsi le temps d’arrêt pendant la mise à niveau réelle. Les étapes présentées peuvent être appliquées aux index [Lucene](https://jackrabbit.apache.org/oak/docs/query/lucene.html) pour les versions AEM 6.4 et ultérieures.

## Présentation {#overview}

De nouvelles versions de l’AEM introduisent des modifications dans les définitions d’index Oak au fur et à mesure que l’ensemble de fonctionnalités est développé. Les modifications apportées aux index Oak forcent la réindexation lors de la mise à niveau de l’instance AEM. La réindexation coûte cher pour les déploiements de ressources, car le texte des ressources (par exemple, le texte dans le fichier pdf) est extrait et indexé. Avec les référentiels MongoMK, les données sont conservées sur le réseau, ce qui augmente encore le temps nécessaire à la réindexation.

Le problème rencontré par la plupart des clients lors d’une mise à niveau est la réduction du temps d’arrêt. La solution consiste à **ignorer** l’activité de réindexation pendant la mise à niveau. Pour ce faire, créez les index **antérieurs** pour effectuer la mise à niveau, puis importez-les simplement pendant la mise à niveau.

## Approche {#approach}

![offline-reindexing-upgrade-text-extraction](assets/offline-reindexing-upgrade-process.png)

L’idée est de créer l’index avant la mise à niveau, par rapport aux définitions d’index de la version d’AEM cible à l’aide de l’outil [Oak-run](/help/sites-deploying/indexing-via-the-oak-run-jar.md). Le diagramme ci-dessus montre l’approche de réindexation hors ligne.

En outre, il s’agit de l’ordre des étapes décrit dans l’approche :

1. Le texte des binaires est extrait en premier.
2. Les définitions d’index cible sont créées.
3. Les index hors ligne sont créés.
4. Les index sont ensuite importés pendant le processus de mise à niveau.

### Extraction de texte {#text-extraction}

Pour activer l’indexation complète dans AEM, le texte des fichiers binaires tels que PDF est extrait et ajouté à l’index. Il s’agit généralement d’une étape coûteuse du processus d’indexation. L’extraction de texte est une étape d’optimisation recommandée, en particulier pour la réindexation des référentiels de ressources, car ils stockent un grand nombre de fichiers binaires.

![offline-reindexing-upgrade-text-extraction](assets/offline-reindexing-upgrade-text-extraction.png)

Le texte des fichiers binaires stockés dans le système peut être extrait à l’aide de cet outil oak-run avec la bibliothèque tika. Un clone des systèmes de production peut être pris avant la mise à niveau et peut être utilisé pour ce processus d’extraction de texte. Ce processus crée ensuite l’entrepôt de texte en procédant comme suit :

**1. Parcourir le référentiel et rassembler les détails des binaires**

Cette étape génère un fichier CSV contenant un ensemble de binaires, un chemin d’accès et un ID d’objet blob.

Exécutez la commande ci-dessous à partir du répertoire à partir duquel vous souhaitez créer l’index. L’exemple ci-dessous suppose que le répertoire racine du référentiel.

```
java java -jar oak-run.jar tika <nodestore path> --fds-path <datastore path> --data-file text-extraction/oak-binary-stats.csv --generate
```

Où `nodestore path` est `mongo_ur` ou `crx-quickstart/repository/segmentstore/`

Utilisez le paramètre `--fake-ds-path=temp` au lieu de `–fds-path` pour accélérer le processus.

**2. Réutilisation du magasin de texte binaire disponible dans l’index existant**

Extrayez les données d’index du système existant et extrayez le magasin de texte.

Vous pouvez vider les données d’index existantes à l’aide de la commande suivante :

```
java -jar oak-run.jar index <nodestore path> --fds-path=<datastore path> --index-dump
```

Où `nodestore path` est `mongo_ur` ou `crx-quickstart/repository/segmentstore/`

Ensuite, utilisez le vidage d’index ci-dessus pour renseigner le magasin :

```
java -jar oak-run.jar tika --data-file text-extraction/oak-binary-stats.csv --store-path text-extraction/store --index-dir ./indexing-result/index-dumps/<oak-index-name>/data populate
```

Où `oak-index-name` est le nom de l’index de texte intégral, par exemple &quot;lucene&quot;.

**3. Exécutez le processus d’extraction de texte à l’aide de la bibliothèque tika pour les fichiers binaires manqués à l’étape** ci-dessus.

```
java -cp oak-run.jar:tika-app-1.21.jar org.apache.jackrabbit.oak.run.Main tika --data-file text-extraction/oak-binary-stats.csv --store-path text-extraction/store --fds-path <datastore path> extract
```

Où `datastore path` est le chemin d’accès à l’entrepôt de données binaire.

Le magasin de texte créé peut être mis à jour et réutilisé pour les scénarios de réindexation à l’avenir.

Pour plus d’informations sur le processus d’extraction de texte, consultez la [documentation Oak-run](https://jackrabbit.apache.org/oak/docs/query/pre-extract-text.html).

### Réindexation hors ligne {#offline-reindexing}

![offline-reindexing-upgrade-offline-reindexing](assets/offline-reindexing-upgrade-offline-reindexing.png)

Créez l’index Lucene hors ligne avant la mise à niveau. Si vous utilisez MongoMK, il est recommandé de l’exécuter directement sur l’un des noeuds MongoMk, car cela évite la surcharge du réseau.

Pour créer l’index hors ligne, procédez comme suit :

**1. Générer des définitions d’index Oak Lucene pour la version d’AEM cible**

Supprimez les définitions d’index existantes. Les définitions d’index qui ont fait l’objet de modifications ont été générées à l’aide du lot de référentiel Granite Adobe de la version AEM cible et de oak-run.

Pour vider la définition d&#39;index de l&#39;instance d&#39;AEM **source**, exécutez la commande suivante :

>[!NOTE]
>
>Pour plus de détails sur les définitions des index de dumping, consultez la [documentation Oak](https://jackrabbit.apache.org/oak/docs/query/oak-run-indexing.html#async-index-data).

```
java -jar oak-run.jar index --fds-path <datastore path> <nodestore path> --index-definitions
```

Où `datastore path` et `nodestore path` proviennent de l’instance d’AEM **source**.

Ensuite, générez des définitions d’index à partir de la version d’AEM **target** à l’aide du lot de référentiel Granite de la version cible.

```
java -cp oak-run.jar:bundle-com.adobe.granite.repository.jar org.apache.jackrabbit.oak.index.IndexDefinitionUpdater --in indexing-definitions_source.json --out merge-index-definitions_target.json --initializer com.adobe.granite.repository.impl.GraniteContent
```

>[!NOTE]
>
> Le processus de création de la définition d’index ci-dessus est pris en charge uniquement à partir de la version `oak-run-1.12.0` et les versions ultérieures. Le ciblage est effectué à l’aide du lot de référentiel Granite `com.adobe.granite.repository-x.x.xx.jar`.

Les étapes ci-dessus créent un fichier JSON appelé `merge-index-definitions_target.json` qui est la définition d’index.

**2. Créez un point de contrôle dans le référentiel**

Créez un point de contrôle dans l’instance d’AEM de production **source** avec une durée de vie longue. Cela doit être effectué avant de cloner le référentiel.

Via la console JMX située à `http://serveraddress:serverport/system/console/jmx`, accédez à `CheckpointMBean` et créez un point de contrôle avec une durée de vie suffisante (par exemple, 200 jours). Pour ce faire, appelez `CheckpointMBean#createCheckpoint` avec `17280000000` comme argument de la durée de vie en millisecondes.

Une fois cette opération effectuée, copiez l’identifiant de point de contrôle nouvellement créé et validez la durée de vie à l’aide de JMX `CheckpointMBean#listCheckpoints`.

>[!NOTE]
>
> Ce point de contrôle sera supprimé lorsque l’index sera importé ultérieurement.

Pour plus d’informations, consultez [Création de points de contrôle](https://jackrabbit.apache.org/oak/docs/query/oak-run-indexing.html#out-of-band-create-checkpoint) dans la documentation Oak.

**Exécution de l’indexation hors ligne pour les définitions d’index générées**

La réindexation Lucene peut être effectuée hors ligne à l’aide de oak-run. Ce processus crée des données d’index dans le disque sous `indexing-result/indexes`. Il n’écrit **pas** dans le référentiel et ne nécessite donc pas l’arrêt de l’instance AEM en cours d’exécution. La banque de texte créée est intégrée à ce processus :

```
java -Doak.indexer.memLimitInMB=500 -jar oak-run.jar index <nodestore path> --reindex --doc-traversal-mode --checkpoint <checkpoint> --fds-path <datastore path> --index-definitions-file merge-index-definitions_target.json --pre-extracted-text-dir text-extraction/store

Sample <checkpoint> looks like r16c85700008-0-8
—fds-path: path to data store.
--pre-extracted-text-dir: Directory of pre-extracted text.
merge-index-definitions_target: JSON file having merged definitions for the target AEM instance. indexes in this file will be re-indexed.
```

L’utilisation du paramètre `--doc-traversal-mode` est pratique avec les installations MongoMK, car elle améliore considérablement le temps de réindexation en mettant en file d’attente le contenu du référentiel dans un fichier plat local. Toutefois, il nécessite un espace disque supplémentaire deux fois plus grand que le référentiel.

Dans le cas de MongoMK, ce processus peut être accéléré si cette étape est exécutée dans une instance plus proche de l’instance MongoDB. Si elle est exécutée sur le même ordinateur, la surcharge réseau peut être évitée.

Vous trouverez des détails techniques supplémentaires dans la [documentation oak-run pour l’indexation ](https://jackrabbit.apache.org/oak/docs/query/oak-run-indexing.html).

### Importer des index {#importing-indexes}

Avec AEM 6.4 et les versions plus récentes, AEM dispose de la fonctionnalité intégrée d’import des index à partir du disque sur la séquence de démarrage. Le dossier `<repository>/indexing-result/indexes` est surveillé pour détecter la présence de données d’index au démarrage. Vous pouvez copier l’index précréé à l’emplacement ci-dessus pendant le processus de mise à niveau [](in-place-upgrade.md#performing-the-upgrade) avant de commencer avec la nouvelle version du fichier jar d’AEM **target**. AEM l’importe dans le référentiel et supprime le point de contrôle correspondant du système. Ainsi, une réindexation est complètement évitée.

## Autres conseils et dépannage {#troubleshooting}

Vous trouverez ci-dessous quelques conseils utiles et des instructions de dépannage.

### Réduction de l’impact sur le système de production en direct {#reduce-the-impact-on-the-live-production-system}

Il est recommandé de cloner le système de production et de créer l’index hors ligne à l’aide du clone. Cela élimine tout impact potentiel sur le système de production. Toutefois, le point de contrôle requis pour importer l’index doit être présent dans le système de production. Il est donc essentiel de créer un point de contrôle avant de prendre le clone.

### Préparation d’un runbook et d’une exécution d’évaluation {#prepare-a-runbook-and-trial-run}

Il est recommandé de préparer un [runbook](https://docs.adobe.com/content/help/en/experience-manager-65/deploying/upgrading/upgrade-planning.html#building-the-upgrade-and-rollback-runbook) et d’effectuer quelques tests avant d’exécuter la mise à niveau en production.

### Mode Doc Traversal Avec Indexation Hors Ligne {#doc-traversal-mode-with-offline-indexing}

L’indexation hors ligne nécessite plusieurs traversées de l’ensemble du référentiel. Avec les installations MongoMK, le référentiel est accessible sur le réseau, ce qui a un impact sur les performances du processus d’indexation. Une option consiste à exécuter le processus d’indexation hors ligne sur la réplique MongoDB elle-même, ce qui élimine la surcharge réseau. Une autre option est l’utilisation du mode de traversée de documents.

Le mode de traversée de documents peut être appliqué en ajoutant le paramètre de ligne de commande `—doc-traversal` à la commande oak-run pour l’indexation hors ligne. Ce mode met en file d’attente une copie de l’ensemble du référentiel dans le disque local en tant que fichier plat et l’utilise pour exécuter l’indexation.
