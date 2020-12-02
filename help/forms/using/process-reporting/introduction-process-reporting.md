---
title: Présentation du Rapports de processus
seo-title: Présentation du Rapports de processus
description: Introduction et fonctionnalités clés du Rapports de processus AEM Forms on JEE
seo-description: Introduction et fonctionnalités clés du Rapports de processus AEM Forms on JEE
uuid: a7f2455b-1b09-41a7-817b-e2e7a1ff9936
content-type: reference
topic-tags: process-reporting
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 4e83ed7b-3f48-4bf6-be4c-89f79949c1df
docset: aem65
translation-type: tm+mt
source-git-commit: 56c6cfd437ef185336e81373bd5f758205b96317
workflow-type: tm+mt
source-wordcount: '309'
ht-degree: 0%

---


# Présentation du Rapports de processus {#introduction-to-process-reporting}

![processus-rapports](assets/process-reporting.png)

Le Rapports de processus est un outil basé sur un navigateur que vous utilisez pour créer et vue des rapports sur les processus et tâches AEM Forms.

Le Rapports de processus fournit un ensemble de rapports prêts à l’emploi qui vous permettent de filtrer, de vue des informations sur les processus à long terme, la durée du processus et le volume de processus.

De plus, Process Rapports fournit une interface permettant d’exécuter des requêtes ad hoc et d’intégrer des vues de rapports personnalisées dans l’interface utilisateur de Process Rapports.

Pour la liste des navigateurs pris en charge, voir [Plateformes prises en charge par AEM Forms](/help/forms/using/aem-forms-jee-supported-platforms.md).

Le Rapports de processus repose sur des modules qui :

* Lire les données de processus de la base de données AEM Forms
* Publier les données de processus dans un référentiel de Rapports de processus incorporé
* Fournit une interface utilisateur basée sur un navigateur pour les rapports de vue

## Fonctionnalités clés {#key-capabilities}

### Rapports permanent {#always-on-reporting}

![gestion de site](assets/site-management.png)

Vue de la liste des processus à exécution longue, des graphiques de durée de traitement et exécution de requêtes personnalisées à l’aide de filtres.

Le Rapports de processus offre également la possibilité d’exporter le rapport et les données de requête au format CSV.

### Rapports ad hoc {#adhoc-reports}

![impression et couleur](assets/print-&-colour.png)

Utilisez des filtres pour obtenir une vue spécifique de vos données.

Vous pouvez rechercher des processus ou des tâches par ID, durée, début et dates de fin, initiateur de processus, etc.

Vous pouvez combiner plusieurs filtres pour créer des rapports spécifiques.

Vous pouvez ensuite enregistrer les filtres de rapports pour qu’ils s’exécutent à une date ou une heure ultérieure.

### Historique des processus/Tâches {#process-task-history}

![gestion de fichiers](assets/file-management.png)

Les serveurs AEM Forms exécutent de nombreux processus en parallèle. Ces processus continuent de passer d’un état à l’autre. En publiant les données Forms dans le référentiel Process Rapports à intervalles réguliers, Process Rapports conserve les informations de transition sur les processus en cours d’exécution dans AEM Forms.

### Contrôle d’accès {#access-control-br}

![sans titre](assets/untitled.png)

La création de rapports sur les processus permet d’accéder à l’interface utilisateur en fonction des autorisations.

Cela signifie que seuls les utilisateurs disposant d’autorisations d’rapports ont accès à l’interface utilisateur de Process Rapports.
