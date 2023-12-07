---
title: Présentation de Health Monitor
description: Ce document présente l’aperçu du moniteur d’intégrité et fournit des détails sur la manière dont vous pouvez y accéder.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/health_monitor
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 05f8b430-141e-4921-98b1-a0d8f636e478
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '296'
ht-degree: 2%

---

# Présentation de Health Monitor {#overview-of-health-monitor}

Health Monitor fournit des informations critiques sur le système AEM forms, telles que des informations sur le serveur, l’utilisation de la mémoire et l’utilisation du processeur. Vous pouvez également accéder aux statistiques de Work Manager, telles que le nombre de tâches dans la file d’attente et leur état. Vous pouvez effectuer les tâches suivantes à l’aide de Health Monitor :

* Vérifiez que votre système fonctionne correctement.
* Affichage des informations pour aider à diagnostiquer les problèmes système au fur et à mesure qu’ils se produisent
* Exécution d’opérations sur des tâches présentant des problèmes
* Purge des enregistrements obsolètes de la base de données de Job Manager

La page Health Monitor d’Administration Console comporte trois onglets :

* L’onglet Système affiche des graphiques de surveillance des ressources et des informations sur le serveur Forms (ou le noeud dans un environnement en grappe). (Voir [Affichage des informations du système](/help/forms/using/admin-help/view-system-information.md#view-system-information).)
* L’onglet Work Manager affiche les données liées à Work Manager, telles que le nombre de tâches dans la file d’attente de Work Manager. Vous pouvez filtrer les informations à l’aide de différents critères ou gérer des tâches individuelles à l’aide des outils d’opération. (Voir [Affichage des statistiques relatives à Work Manager](/help/forms/using/admin-help/view-statistics-related-manager.md#view-statistics-related-to-work-manager).)
* L’onglet Planificateur de purge de tâche permet de purger les enregistrements obsolètes de la base de données de Job Manager. (Voir [Purge des enregistrements de la base de données de Job Manager](/help/forms/using/admin-help/purge-records-job-manager-database.md#purge-records-from-the-job-manager-database).)

La page web Health Monitor est renseignée avec les statistiques collectées via une API Gemfire. Cette API détecte automatiquement tous les noeuds d’une grappe. Elle résout également les problèmes de sécurité qui se produisent lors de la collecte de statistiques depuis des serveurs proxy ou des équilibreurs de charge. Des options Java sont disponibles pour affiner Health Monitor, réduisant ainsi l’impact sur les performances de votre environnement AEM forms. (Voir [Réglage précis des performances de Health Monitor](/help/forms/using/admin-help/fine-tuning-health-monitor-performance.md#fine-tuning-health-monitor-performance).)

**Accès à Health Monitor**

1. Dans Administration Console, cliquez sur Health Monitor dans le coin supérieur droit de la page.
