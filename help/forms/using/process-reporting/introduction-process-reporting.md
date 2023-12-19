---
title: Présentation de Process Reporting
description: Présentation et principales fonctionnalités de Process Reporting d’AEM Forms on JEE
content-type: reference
topic-tags: process-reporting
products: SG_EXPERIENCEMANAGER/6.5/FORMS
docset: aem65
exl-id: 674d28dc-7353-49de-9e12-b1998e1509c7
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '294'
ht-degree: 93%

---

# Présentation de Process Reporting{#introduction-to-process-reporting}

![process-reporting](assets/process-reporting.png)

Process Reporting est un outil de navigateur que vous utilisez pour créer et afficher des rapports sur les processus et tâches AEM Forms.

Process Reporting fournit un ensemble de rapports d’usine qui vous permettent de filtrer et d’afficher des informations sur les processus à long terme, la durée de processus et le volume de workflows.

En outre, Process Reporting fournit une interface permettant d’exécuter des requêtes ad hoc et d’intégrer des vues de rapports personnalisées dans son interface utilisateur.

Pour obtenir la liste des navigateurs pris en charge, voir [Plateformes prises en charge par AEM Forms](/help/forms/using/aem-forms-jee-supported-platforms.md).

Process Reporting est construit sur des modules qui permettent de :

* Lire les données de processus de la base de données AEM Forms.
* Publier des données de processus dans un référentiel Process Reporting incorporé.
* Fournir une interface utilisateur de navigateur pour afficher les rapports.

## Fonctionnalités essentielles {#key-capabilities}

### Création de rapports permanents {#always-on-reporting}

![site-management](assets/site-management.png)

Affichez la liste des processus à long terme, des graphiques de durée de processus et exécutez des requêtes personnalisées à l’aide de filtres.

Process Reporting offre également la possibilité d’exporter le rapport et les données de requête au format CSV.

### Rapports ad hoc {#adhoc-reports}

![print-&amp;-colour](assets/print-&-colour.png)

Utilisez des filtres pour obtenir une vue spécifique des données.

Vous pouvez rechercher des processus ou des tâches par identifiant, durée, dates de début et de fin, initiateur de processus, etc.

Vous pouvez combiner plusieurs filtres pour créer des rapports spécifiques.

Vous pouvez ensuite enregistrer les filtres de rapport pour les exécuter à une date ou une heure ultérieure.

### Historique des processus/tâches {#process-task-history}

![file-management](assets/file-management.png)

Les serveurs AEM Forms exécutent de nombreux processus en parallèle. Ces processus continuent de passer d’un statut à un autre. En publiant des données Forms dans le référentiel Process Reporting à intervalles réguliers, Process Reporting conserve les informations de transition sur les processus en cours d’exécution dans AEM Forms.

### Contrôle d’accès {#access-control-br}

![untitled](assets/untitled.png)

Process Reporting permet d’accéder à l’interface utilisateur en fonction des autorisations.

Cela signifie que seuls les utilisateurs disposant d’autorisations de création de rapports ont accès à l’interface utilisateur Process Reporting.
