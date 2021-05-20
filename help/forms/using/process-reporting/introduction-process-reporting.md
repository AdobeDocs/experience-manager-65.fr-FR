---
title: Présentation des rapports de processus
seo-title: Présentation des rapports de processus
description: Présentation et principales fonctionnalités des rapports de processus d’AEM Forms on JEE
seo-description: Présentation et principales fonctionnalités des rapports de processus d’AEM Forms on JEE
uuid: a7f2455b-1b09-41a7-817b-e2e7a1ff9936
content-type: reference
topic-tags: process-reporting
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 4e83ed7b-3f48-4bf6-be4c-89f79949c1df
docset: aem65
exl-id: 674d28dc-7353-49de-9e12-b1998e1509c7
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '309'
ht-degree: 0%

---

# Introduction aux rapports de processus{#introduction-to-process-reporting}

![process-reporting](assets/process-reporting.png)

Process Reporting est un outil de navigateur que vous utilisez pour créer et afficher des rapports sur les processus et tâches AEM Forms.

La création de rapports de processus fournit un ensemble de rapports d’usine qui vous permettent de filtrer, d’afficher des informations sur les processus à long terme, la durée de processus et le volume de workflow.

En outre, Process Reporting fournit une interface permettant d’exécuter des requêtes ad hoc et d’intégrer des vues de rapports personnalisées dans l’interface utilisateur Process Reporting.

Pour obtenir la liste des navigateurs pris en charge, voir [Plateformes prises en charge par AEM Forms](/help/forms/using/aem-forms-jee-supported-platforms.md).

Les rapports de processus sont construits sur des modules qui :

* Lire les données de processus de la base de données AEM Forms
* Publication de données de processus dans un référentiel de création de rapports de processus incorporé
* Fournit une interface utilisateur de navigateur pour afficher les rapports.

## Fonctionnalités clés {#key-capabilities}

### Création de rapports &quot;toujours&quot; {#always-on-reporting}

![gestion de site](assets/site-management.png)

Affichez la liste des processus à long terme, des graphiques de durée de processus et exécutez des requêtes personnalisées à l’aide de filtres.

Les rapports de processus offrent également la possibilité d’exporter le rapport et les données de requête au format CSV.

### Rapports ad hoc {#adhoc-reports}

![print-&amp;-color](assets/print-&-colour.png)

Utilisez des filtres pour obtenir une vue spécifique de vos données.

Vous pouvez rechercher des processus ou des tâches par identifiant, durée, dates de début et de fin, initiateur de processus, etc.

Vous pouvez combiner plusieurs filtres pour créer des rapports spécifiques.

Vous pouvez ensuite enregistrer les filtres de rapport pour les exécuter à une date ou une heure ultérieure.

### Historique des processus/tâches {#process-task-history}

![gestion de fichiers](assets/file-management.png)

Les serveurs AEM Forms exécutent de nombreux processus en parallèle. Ces processus continuent de passer d’un état à un autre. En publiant des données Forms dans le référentiel Process Reporting à intervalles réguliers, Process Reporting conserve les informations de transition sur les processus en cours d’exécution dans AEM Forms.

### Contrôle d’accès {#access-control-br}

![sans titre](assets/untitled.png)

La création de rapports sur les processus permet d’accéder à l’interface utilisateur en fonction des autorisations.

Cela signifie que seuls les utilisateurs disposant d’autorisations de création de rapports ont accès à l’interface utilisateur Process Reporting.
