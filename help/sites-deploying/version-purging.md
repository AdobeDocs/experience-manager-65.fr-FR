---
title: Purge de version
description: Cet article décrit les options disponibles pour la purge de version.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: configuring
content-type: reference
docset: aem65
feature: Configuring
exl-id: 6f0b1951-bdda-475f-b6c0-bc18de082b7c
solution: Experience Manager, Experience Manager Sites
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '732'
ht-degree: 81%

---

# Purge de version{#version-purging}

Dans une installation standard, Adobe Experience Manager (AEM) crée une version d’une page ou d’un nœud lorsque vous activez une page après la mise à jour du contenu.

>[!NOTE]
>
>Si le contenu n’est pas modifié, un message s’affiche indiquant que la page a été activée, mais qu’aucune nouvelle version n’est créée.

Vous pouvez créer des versions supplémentaires sur demande à l’aide de l’onglet **Contrôle de version** du sidekick. Ces versions sont stockées dans le référentiel et peuvent être restaurées si nécessaire.

Ces versions ne sont jamais purgées. La taille du référentiel augmente au fil du temps et doit donc être gérée.

AEM est fourni avec divers mécanismes pour vous aider à gérer votre référentiel :

* le [Gestionnaire de versions](#version-manager)
Cette option peut être configurée pour purger les anciennes versions lorsque de nouvelles versions sont créées.

* l’outil [&#x200B; Purger les versions &#x200B;](/help/sites-deploying/monitoring-and-maintaining.md#purgeversionstool)
Il est utilisé dans le cadre de la surveillance et de la maintenance de votre référentiel.
Il vous permet d’intervenir et de supprimer les anciennes versions d’un nœud ou d’une hiérarchie de nœuds, en fonction des paramètres suivants :

  * Le nombre maximal de versions à conserver dans le référentiel.
    Une fois ce nombre dépassé, la version la plus ancienne est supprimée.

  * L’âge maximal des versions conservées dans le référentiel.
    Lorsque l’âge d’une version dépasse cette valeur, elle est purgée du référentiel.

* La [tâche de maintenance Purge de version](/help/sites-administering/operations-dashboard.md#automated-maintenance-tasks). Vous pouvez planifier la tâche de maintenance Purge de version pour supprimer automatiquement les anciennes versions. Ainsi, cela réduit la nécessité d’utiliser manuellement les outils de purge de version.

>[!CAUTION]
>
>Pour optimiser la taille du référentiel, vous devez exécuter la tâche de purge des versions fréquemment. La tâche doit être planifiée en dehors des heures de bureau lorsqu’il y a un trafic limité.

## Gestionnaire de versions {#version-manager}

Outre la purge explicite à l’aide de l’outil dédié, le gestionnaire de versions peut être configuré pour purger les anciennes versions lors de la création de nouvelles versions.

Pour installer le gestionnaire de versions, [créez une configuration](/help/sites-deploying/configuring-osgi.md) pour :

`PID com.day.cq.wcm.core.impl.VersionManagerImpl`

Les options suivantes sont disponibles :

* `versionmanager.createVersionOnActivation` (booléen, valeur par défaut : true)
Indique s’il faut créer une version lorsque les pages sont activées.
Une version est créée sauf si l’agent de réplication est configuré pour supprimer la création de versions, qui est prise en charge par le gestionnaire de versions.
Une version est créée uniquement si l’activation s’effectue sur un chemin qui est contenu dans `versionmanager.ivPaths` (voir ci-dessous).

* `versionmanager.ivPaths`(String[], default: `{"/"}`)
Indique les chemins d’accès sur lesquels des versions sont créées implicitement lors de l’activation si `versionmanager.createVersionOnActivation` est défini sur true.

* `versionmanager.purgingEnabled` (booléen, valeur par défaut : false)
Définit s’il faut activer la purge lorsque de nouvelles versions sont créées.

* `versionmanager.purgePaths` (chaîne[], valeur par défaut : {« /content »})
Indique sur quels chemins d’accès purger les versions lorsque de nouvelles versions sont créées.

* `versionmanager.maxAgeDays` (int, valeur par défaut : 30)
Lors de la purge de version, toute version antérieure à la valeur configurée est supprimée. Si cette valeur est inférieure à 1, la purge n’est pas effectuée sur la base de l’âge de la version.

* `versionmanager.maxNumberVersions` (int, valeur par défaut 5)
Lors de la purge, toute version antérieure à la nième version la plus récente est supprimée. Si cette valeur est inférieure à 1, la purge n’est pas effectuée sur la base du nombre de versions.

* `versionmanager.minNumberVersions` (int, 0 par défaut)
Nombre minimum de versions à conserver, quel que soit l’âge. Si cette valeur est inférieure à 1, aucun nombre minimum de versions n’est conservé.

>[!NOTE]
>
>Il n’est pas recommandé de conserver de nombreuses versions dans le référentiel. Par conséquent, lors de la configuration de l’opération de purge de version, veillez à ne pas exclure un trop grand nombre de versions de la purge, faute de quoi la taille du référentiel ne sera pas correctement optimisée. Si vous conservez un grand nombre de versions en raison d’exigences métier, contactez l’assistance technique d’Adobe pour trouver d’autres moyens d’optimiser la taille du référentiel.

### Combinaison d’options de conservation {#combining-retention-options}

Les options qui définissent la manière dont les versions doivent être conservées (`maxAgeDays`, `maxNumberVersions`, `minNumberVersions`) peuvent être combinées en fonction de vos besoins.

Par exemple, lors de la définition du nombre maximal de versions à conserver ET de la version la plus ancienne à conserver :

* Configuration :

  * `maxNumberVersions` = 7

  * `maxAgeDays` = 30

* Avec :

  * Dix versions ont été créées au cours des 60 derniers jours.
  * Trois de ces versions ont été créées au cours des 30 derniers jours.

* Cela signifie que :

  * Les trois dernières versions sont conservées.

Par exemple, pour définir le nombre maximal ET minimal de versions à conserver ET définir la version la plus ancienne à conserver :

* Configuration :

  * `maxNumberVersions` = 3
  * `maxAgeDays` = 30
  * `minNumberVersions` = 3

* Avec :

  * Cinq versions ont été créées il y a 60 jours.

* Cela signifie que :

  * Trois versions sont conservées.

## Outil Purge de version {#purge-versions-tool}

L’outil [Purge de version](/help/sites-deploying/monitoring-and-maintaining.md#purgeversionstool) est destiné à purger les versions d’un nœud ou d’une hiérarchie de nœuds dans votre référentiel. Son objectif premier est de vous aider à réduire la taille de votre référentiel en supprimant les anciennes versions de vos nœuds.
