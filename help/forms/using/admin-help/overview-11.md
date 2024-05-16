---
title: Présentation de Health Monitor
description: Ce document présente une vue d’ensemble de Health Monitor et donne des informations sur la manière dont vous pouvez y accéder.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/health_monitor
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 05f8b430-141e-4921-98b1-a0d8f636e478
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: ht
source-wordcount: '296'
ht-degree: 100%

---

# Présentation de Health Monitor {#overview-of-health-monitor}

Health Monitor fournit des informations critiques sur le système d’AEM Forms telles que des informations sur le serveur, l’utilisation de la mémoire et l’utilisation du processeur. Il fournit également les statistiques Work Manager, telles que le nombre de tâches dans la file d’attente ainsi que leur état. Health Monitor vous permet d’effectuer les tâches suivantes :

* Vérification du bon fonctionnement du système ;
* Affichage d’informations permettant de diagnostiquer les problèmes système au fur et à mesure qu’ils se produisent.
* Exécution d’opérations sur des tâches présentant des problèmes.
* Purge d’enregistrements obsolètes de la base de données de Job Manager.

La page Health Monitor de la console d’administration comporte trois onglets :

* L’onglet Système affiche des graphiques de contrôle des ressources ainsi que des informations sur le serveur Forms Server (ou le nœud dans un environnement organisé en cluster). (Voir [Affichage des informations du système](/help/forms/using/admin-help/view-system-information.md#view-system-information)).
* L’onglet Work Manager affiche les données qui y sont liées, telles que le nombre de tâches dans la file d’attente de Work Manager. Vous pouvez filtrer les informations à l’aide de différents critères ou gérer des tâches individuelles à l’aide des outils d’opération. (Voir [Affichage des statistiques relatives à Work Manager](/help/forms/using/admin-help/view-statistics-related-manager.md#view-statistics-related-to-work-manager)).
* L’onglet Planificateur de purge de travaux vous permet de purger les enregistrements obsolètes de la base de données de Job Manager. (Voir [Purge d’enregistrements de la base de données de Job Manager](/help/forms/using/admin-help/purge-records-job-manager-database.md#purge-records-from-the-job-manager-database)).

La page Web Health Monitor est renseignée avec les statistiques collectées via une API Gemfire. Cette API détecte automatiquement tous les nœuds d’un cluster. Elle résout également les problèmes de sécurité qui se produisent lors de la collecte de statistiques depuis des serveurs proxy ou des équilibreurs de charge. Des options Java sont proposées pour affiner Health Monitor, réduisant l’incidence sur les performances de votre environnement AEM forms. (Voir [Réglage précis des performances de Health Monitor](/help/forms/using/admin-help/fine-tuning-health-monitor-performance.md#fine-tuning-health-monitor-performance)).

**Accès à Health Monitor**

1. Dans la console d’administration, cliquez sur Health Monitor dans le coin supérieur droit de la page.
