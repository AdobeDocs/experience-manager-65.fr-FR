---
title: Indexation par l’intermédiaire du fichier Jar d’Oak-run
description: Découvrez comment effectuer l’indexation via le fichier Jar exécuté par Oak.
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: deploying
exl-id: dcec8c1b-13cc-486c-b1a4-62e6eb3184ad
source-git-commit: b9c164321baa3ed82ae87a97a325fcf0ad2f6ca0
workflow-type: tm+mt
source-wordcount: '906'
ht-degree: 41%

---

# Indexation par l’intermédiaire du fichier Jar d’Oak-run {#indexing-via-the-oak-run-jar}

Oak-run prend en charge tous les cas d’utilisation d’indexation sur la ligne de commande sans avoir à opérer au niveau JMX. Les avantages de l’approche oak-run sont les suivants :

1. Il s’agit d’un nouvel ensemble d’outils d’indexation pour AEM 6.4.
1. Il réduit la durée de réindexation, ce qui a un effet bénéfique sur les délais de réindexation des référentiels de grande taille.
1. Il réduit la consommation des ressources au cours de la réindexation dans AEM, ce qui se traduit par de meilleures performances du système pour d’autres activités AEM.
1. Oak-run fournit une prise en charge hors bande : Si les conditions de production ne vous permettent pas d’exécuter la réindexation sur les instances de production, un environnement cloné peut être utilisé pour la réindexation afin d’éviter un impact critique sur les performances.

Vous trouverez ci-dessous une liste de cas d’utilisation pouvant être utilisés lors de l’exécution d’opérations d’indexation via le `oak-run` outil.

## Contrôles de cohérence d’index {#indexconsistencychecks}

>[!NOTE]
>
>Pour plus d’informations sur ce scénario, voir [Cas d’utilisation 1 - Contrôle de cohérence de l’index](/help/sites-deploying/oak-run-indexing-usecases.md#usercase1indexconsistencycheck).

* `oak-run.jar`détermine rapidement si les index Lucene Oak sont corrompus.
* Il est recommandé de lancer l’exécution sur une instance AEM en cours d’utilisation pour les niveaux de contrôle de cohérence 1 et 2.

![Contrôles de cohérence d’index](assets/screen_shot_2017-12-14at135758.png)

## Statistiques d’index {#indexstatistics}

>[!NOTE]
>
>Pour plus d’informations sur ce scénario, voir [Cas d’utilisation 2 - Statistiques des index](/help/sites-deploying/oak-run-indexing-usecases.md#usecase2indexstatistics)

* `oak-run.jar` vide toutes les définitions d’index, les statistiques d’index importantes et le contenu de l’index pour l’analyse hors ligne.
* Son exécution est recommandée sur une instance AEM en cours d’utilisation.

![image2017-12-19_9-47-40](assets/image2017-12-19_9-47-40.png)

## Arborescence de décision de la méthode de réindexation {#reindexingapproachdecisiontree}

Ce diagramme illustre une arborescence de décision concernant l’utilisation des diverses méthodes de réindexation.

![oak_-_reindexingwithoak-run](assets/oak_-_reindexingwithoak-run.png)

## Réindexation de MongoMK / RDMBMK {#reindexingmongomk}

>[!NOTE]
>
>Pour plus d’informations sur ce scénario, voir [Cas d’utilisation 3 - Réindexation](/help/sites-deploying/oak-run-indexing-usecases.md#usecase3reindexing).

### Pré-extraction de texte pour SegmentNodeStore et DocumentNodeStore {#textpre-extraction}

[pré-extraction de texte](/help/sites-deploying/best-practices-for-queries-and-indexing.md#how-to-perform-text-pre-extraction) (une fonctionnalité qui existe avec AEM 6.3) peut être utilisée pour réduire le temps de réindexation. La pré-extraction de texte peut être utilisée avec toutes les méthodes de réindexation.

Selon le `oak-run.jar` l’approche d’indexation. Il y aura différentes étapes de chaque côté de l’étape Réindexer dans le diagramme ci-dessous.

![Pré-extraction de texte pour SegmentNodeStore et DocumentNodeStore](assets/4.png)

>[!NOTE]
>
>Orange indique les activités pour lesquelles AEM doit se trouver dans une fenêtre de maintenance.

### Réindexation en ligne pour MongoMK ou RDBMK à l’aide du fichier oak-run.jar {#onlinere-indexingformongomk}

>[!NOTE]
>
>Pour plus d’informations sur ce scénario, voir [Réindexation - DocumentNodeStore](/help/sites-deploying/oak-run-indexing-usecases.md#reindexdocumentnodestore).

Il s’agit de la méthode recommandée pour réindexer les installations AEM MongoMK (et RDBMK). Aucune autre méthode ne doit être utilisée.

Exécutez ce processus uniquement sur une seule instance AEM de la grappe.

![Réindexation en ligne pour MongoMK ou RDBMK à l’aide du fichier oak-run.jar](assets/5.png)

## Réindexation de TarMK {#re-indexingtarmk}

>[!NOTE]
>
>Pour plus d’informations sur ce scénario, voir [Réindexation - SegmentNodeStore](/help/sites-deploying/oak-run-indexing-usecases.md#reindexsegmentnodestore).

* **Observations relatives à Cold Standby (TarMK)**

   * Il n&#39;y a pas de considérations particulières à prendre en compte pour le Secondaire froid; les modifications de synchronisation des instances Secondaires à froid sont identiques à celles d’habitude.

* **Fermes de publication AEM (les fermes de publication AEM doivent toujours être TarMK)**

   * Pour la batterie de serveurs de publication, elle doit être effectuée pour l’ensemble OU exécuter les étapes sur une seule publication, puis cloner la configuration pour d’autres (en prenant toutes les précautions habituelles lors du clonage d’instances AEM ; sling.id - doit pointer vers quelque chose ici)

### Réindexation en ligne pour TarMK {#onlinere-indexingfortarmk}

>[!NOTE]
>
>Pour plus d’informations sur ce scénario, voir [Réindexation en ligne - SegmentNodeStore](/help/sites-deploying/oak-run-indexing-usecases.md#onlinereindexsegmentnodestore).

Il s’agit de la méthode utilisée avant l’introduction des nouvelles fonctionnalités d’indexation du fichier oak-run.jar. Pour ce faire, définissez la variable `reindex=true` sur l’index Oak.

Cette approche peut être utilisée si les effets sur le temps et les performances à indexer sont acceptables pour le client. C’est souvent le cas pour les installations AEM de petite et moyenne taille.

![Réindexation en ligne pour TarMK](assets/6.png)

### Réindexation en ligne de TarMK à l’aide du fichier oak-run.jar {#onlinere-indexingtarmkusingoak-run-jar}

>[!NOTE]
>
>Pour obtenir des informations détaillées sur ce scénario, consultez la section [Réindexation en ligne – SegmentNodeStore – L’instance AEM est en cours d’exécution](/help/sites-deploying/oak-run-indexing-usecases.md#onlinereindexsegmentnodestoretheaeminstanceisrunning).

La réindexation en ligne de TarMK à l’aide du fichier oak-run.jar est plus rapide que la [Réindexation en ligne pour TarMK](#onlinere-indexingfortarmk) décrite ci-dessus. Cependant, elle exige également d’être exécutée au cours d’une fenêtre de maintenance, en sachant que cette fenêtre sera plus étroite. Son exécution s’accompagne, en outre, d’étapes supplémentaires.

>[!NOTE]
>
>La couleur orange indique les opérations au cours desquelles AEM doit être exécuté au cours d’une session de maintenance.

![Réindexation en ligne de TarMK à l’aide du fichier oak-run.jar](assets/7.png)

### Réindexation hors ligne de TarMK à l’aide du fichier oak-run.jar {#offlinere-indexingtarmkusingoak-run-jar}

>[!NOTE]
>
>Pour plus d’informations sur ce scénario, voir [Réindexation en ligne - SegmentNodeStore - L’instance AEM est arrêtée](/help/sites-deploying/oak-run-indexing-usecases.md#onlinereindexsegmentnodestoreaeminstanceisdown).

La réindexation hors ligne de TarMK est la méthode de réindexation la plus simple basée sur le fichier `oak-run.jar`, en ce sens qu’elle ne nécessite qu’un seul commentaire `oak-run.jar`. Toutefois, l’instance AEM doit être arrêtée.

>[!NOTE]
>
>Rouge indique les opérations où AEM doit être arrêté.

![Réindexation hors ligne de TarMK à l’aide du fichier oak-run.jar](assets/8.png)

### Réindexation hors-bande de TarMK à l’aide du fichier oak-run.jar  {#out-of-bandre-indexingtarmkusingoak-run-jar}

>[!NOTE]
>
>Pour obtenir des informations détaillées sur ce scénario, voir [Réindexation hors-bande – SegmentNodeStore](/help/sites-deploying/oak-run-indexing-usecases.md#outofbandreindexsegmentnodestore).

La réindexation hors-bande réduit l’impact de la réindexation sur les instances AEM en cours d’utilisation.

>[!NOTE]
>
>Rouge indique les opérations où AEM peut être arrêté.

![Réindexation hors-bande de TarMK à l’aide du fichier oak-run.jar](assets/9.png)

## Mise à jour des définitions d’indexation {#updatingindexingdefinitions}

>[!NOTE]
>
>Pour obtenir des informations détaillées sur ce scénario, consultez le [Cas d’utilisation 4 – Mise à jour des définitions d’indexation](/help/sites-deploying/oak-run-indexing-usecases.md#usecase4updatingindexdefinitions).

### Création et mise à jour des définitions d’index sur TarMK à l’aide d’ACS Ensure Index {#creatingandupdatingindexdefinitionsontarmkusingacsensureindex}

>[!NOTE]
>
>ACS Ensure Index est un projet pris en charge par la communauté et n’est pas pris en charge par la prise en charge des Adobes.

Cela vous permet d’envoyer une définition d’index via un package de contenu, ce qui se traduit, par la suite, par la possibilité d’effectuer une réindexation en définissant l’indicateur de réindexation sur `true`. Cela fonctionne avec les plus petites configurations pour lesquelles la réindexation est de courte durée.

Pour plus d’informations, voir [Documentation d’ACS Ensure Index](https://adobe-consulting-services.github.io/acs-aem-commons/features/ensure-oak-index/index.html) pour plus d’informations.

### Création et mise à jour des définitions d’index sur TarMK à l’aide du fichier oak-run.jar {#creatingandupdatingindexdefinitionsontarmkusingoak-run-jar}

Si l’impact sur le temps ou les performances de la réindexation à l’aide de la variable non-`oak-run.jar` est trop élevée, les méthodes suivantes `oak-run.jar` Une approche basée sur peut être utilisée pour importer et réindexer des définitions d’index Lucene dans une installation AEM basée sur TarMK.

![Création et mise à jour des définitions d’index sur TarMK à l’aide du fichier oak-run.jar](assets/10.png)

### Création et mise à jour des définitions d’index sur MongoMK à l’aide du fichier oak-run.jar {#creatingandupdatingindexdefinitionsonmonogmkusingoak-run-jar}

Si l’impact sur le temps ou les performances de la réindexation à l’aide de la variable non-`oak-run.jar` est trop élevée, les méthodes suivantes `oak-run.jar` Une approche basée sur peut être utilisée pour importer et réindexer des définitions d’index Lucene dans des installations d’AEM basées sur MongoMK.

![Création et mise à jour des définitions d’index sur MongoMK à l’aide du fichier oak-run.jar](assets/11.png)
