---
title: Purge de version
seo-title: Version Purging
description: Cet article décrit les options disponibles pour la purge de version.
seo-description: This article describes the available options for version purging.
uuid: a9fa25c7-e60e-4665-a726-99af9aac8f70
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: configuring
content-type: reference
discoiquuid: fb4d7337-7b94-430b-80d2-f1754f823c2b
docset: aem65
feature: Configuring
exl-id: 6f0b1951-bdda-475f-b6c0-bc18de082b7c
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '728'
ht-degree: 68%

---

# Purge de version{#version-purging}

Durant l’installation standard, AEM crée une version de page ou de nœud lorsque la page est activée après la mise à jour du contenu. 

>[!NOTE]
>
>Si aucune modification de contenu n’est effectuée, vous verrez un message affirmant que la page a été activée, cependant aucune nouvelle version ne sera créée.

Vous pouvez créer des versions supplémentaires sur demande à l’aide de l’onglet **Versions** du sidekick. Ces versions sont stockées dans le référentiel et peuvent être restaurées si nécessaire. 

Ces versions n’étant jamais purgées, la taille du référentiel va continuer d’augmenter et devra être gérée.

AEM est livré avec divers mécanismes vous permettant de gérer le référentiel :

* Le [gestionnaire de versions](#version-manager) Il peut être installé pour supprimer les anciennes versions lorsque de nouvelles versions sont créées. 

* L’outil [Purger les versions](/help/sites-deploying/monitoring-and-maintaining.md#purgeversionstool) sert en partie à  surveiller et à maintenir le référentiel.
 Il vous permet d’intervenir et de supprimer les anciennes versions d’un nœud ou d’une hiérarchie de nœuds, en fonction des paramètres suivants :

   * Le nombre maximal de versions à conserver dans le référentiel.
Une fois ce nombre dépassé, la version la plus ancienne est supprimée.

   * L’âge maximal des versions conservées dans le référentiel.  Lorsque l’âge d’une version dépasse cette valeur, elle est purgée du référentiel. 

* la valeur [Tâche de maintenance de purge de version](/help/sites-administering/operations-dashboard.md#automated-maintenance-tasks). Vous pouvez planifier la tâche de maintenance Purge de version pour supprimer automatiquement les anciennes versions. Par conséquent, cela réduit la nécessité d’utiliser manuellement les outils de purge de version.

>[!CAUTION]
>
>Pour optimiser la taille du référentiel, vous devez exécuter la tâche Purge de version fréquemment. La tâche doit être planifiée en dehors des heures de bureau lorsque le trafic est limité.

## Gestionnaire de versions {#version-manager}

En plus de la purge explicite via l’outil de purge, le gestionnaire de versions peut être configuré pour purger d’anciennes versions lorsque de nouvelles versions sont créées.

Pour configurer le gestionnaire de versions, procédez comme suit : [création d’une configuration](/help/sites-deploying/configuring-osgi.md) pour :

`PID com.day.cq.wcm.core.impl.VersionManagerImpl`

Les options suivantes sont disponibles :

* `versionmanager.createVersionOnActivation` (booléen, valeur par défaut : true) Indique s’il faut créer une version lorsque les pages sont activées.
Une version est créée sauf si l’agent de réplication est configuré pour supprimer la création de versions, qui est honorée par le gestionnaire de versions.
Une version n’est créée que si l’activation se produit sur un chemin contenu dans `versionmanager.ivPaths` (voir ci-dessous).

* `versionmanager.ivPaths`(Chaîne)[], par défaut : `{"/"}`) Spécifie les chemins d’accès sur lesquels les versions sont implicitement créées lors de l’activation si `versionmanager.createVersionOnActivation` est définie sur true.

* `versionmanager.purgingEnabled` (booléen, valeur par défaut : false) Définit si la purge doit être activée ou non lors de la création de versions.

* `versionmanager.purgePaths` (Chaîne)[], par défaut : {&quot;/content&quot;}) Spécifie les chemins d’accès pour purger les versions lors de la création de nouvelles versions.

* `versionmanager.maxAgeDays` (int, valeur par défaut : 30) Lors de la purge de version, toute version antérieure à la valeur configurée est supprimée. Si la valeur est inférieure à 1, la purge ne sera pas effectuée en fonction de l’âge de la version.

* `versionmanager.maxNumberVersions` (int, valeur par défaut 5) Lors de la purge de version, toute version antérieure à la n-ème version la plus récente est supprimée. Si la valeur est inférieure à 1, la purge n’est pas effectuée en fonction du nombre de versions.

* `versionmanager.minNumberVersions` (int, valeur par défaut 0) Nombre minimum de versions qui seront conservées, indépendamment de l’âge. Si cette valeur est définie sur une valeur inférieure à 1, aucun nombre minimum de versions n’est conservé.

>[!NOTE]
>
>Il n’est pas recommandé de conserver un grand nombre de versions dans le référentiel. Par conséquent, lors de la configuration de l’opération de purge de version, veillez à ne pas exclure un trop grand nombre de versions de la purge, faute de quoi la taille du référentiel ne sera pas correctement optimisée. Si vous conservez un grand nombre de versions en raison des besoins de l’entreprise, contactez l’assistance Adobe pour trouver d’autres moyens d’optimiser la taille du référentiel.

### Combinaison d’options de conservation {#combining-retention-options}

Les options définissant la manière dont les versions doivent être conservées ( `maxAgeDays`, `maxNumberVersions`, `minNumberVersions`), peut être combiné selon vos besoins.

Par exemple, en définissant le nombre maximum de versions à conserver ET la version la plus ancienne à conserver :

* Configuration:

   * `maxNumberVersions` = 7

   * `maxAgeDays` = 30

* Avec :

   * 10 versions créées dans les 60 derniers jours
   * 3 de ces versions créées dans les 30 derniers jours 

* Ce qui signifie que :

   * les 3 dernières versions seront conservées 

Par exemple, en définissant les nombres maximum ET minimum de versions à conserver ET la version la plus ancienne à conserver :

* Configuration:

   * `maxNumberVersions` = 3
   * `maxAgeDays` = 30
   * `minNumberVersions` = 3

* Avec :

   * 5 versions créées il y a 60 jours

* Ce qui signifie que :

   * 3 versions seront conservées

## Outil de purge des versions {#purge-versions-tool}

L’outil de [purge des versions](/help/sites-deploying/monitoring-and-maintaining.md#purgeversionstool) est conçu pour la purge des versions d’un nœud ou d’une hiérarchie de nœuds dans votre référentiel. Son principal objectif est de vous aider à réduire la taille du référentiel en supprimant les anciennes versions de vos nœuds. 
