---
title: Présentation de Health Monitor
description: Ce document présente une vue d’ensemble de Health Monitor et donne des informations sur la manière dont vous pouvez y accéder.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/health_monitor
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 05f8b430-141e-4921-98b1-a0d8f636e478
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: e72c079d-d036-46d5-b43d-29b276a174c2
    internal-label: Authoring and publishing content
subfeature_v2:
  - id: a26f372d-6d7c-452b-81df-594dd4365ae1
    internal-label: Adaptive Forms
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '299'
ht-degree: 100%
---
# Présentation de Health Monitor {#overview-of-health-monitor}

Health Monitor fournit des informations critiques sur le système d’AEM Forms telles que des informations sur le serveur, l’utilisation de la mémoire et l’utilisation du processeur. Il fournit également des statistiques Work Manager, telles que le nombre d’éléments de travail ou de tâches dans la file d’attente ainsi que leur état. Health Monitor vous permet d’effectuer les tâches suivantes :

* Vérifier le bon fonctionnement du système
* Affichage d’informations permettant de diagnostiquer les problèmes système au fur et à mesure qu’ils se produisent.
* Exécution d’opérations sur des tâches ou des traitements présentant des problèmes.
* Purge d’enregistrements obsolètes de la base de données de Job Manager.

La page Health Monitor de la console d’administration comporte trois onglets :

* L’onglet Système affiche des graphiques de contrôle des ressources ainsi que des informations sur le Serveur Formulaires (ou le nœud dans un environnement organisé en cluster). (Voir [Affichage des informations du système](/help/forms/using/admin-help/view-system-information.md#view-system-information)).
* L’onglet Work Manager affiche les données qui y sont liées, telles que le nombre de tâches dans la file d’attente de Work Manager. Vous pouvez filtrer les informations à l’aide de différents critères ou gérer des tâches individuelles à l’aide des outils d’opération. (Voir [Affichage des statistiques relatives à Work Manager](/help/forms/using/admin-help/view-statistics-related-manager.md#view-statistics-related-to-work-manager)).
* L’onglet Planificateur de purge de travaux vous permet de purger les enregistrements obsolètes de la base de données de Job Manager. (Voir [Purge d’enregistrements de la base de données de Job Manager](/help/forms/using/admin-help/purge-records-job-manager-database.md#purge-records-from-the-job-manager-database)).

La page web Health Monitor est renseignée avec les statistiques collectées via une API Gemfire. Cette API détecte automatiquement tous les nœuds d’un cluster. Elle résout également les problèmes de sécurité qui se produisent lors de la collecte de statistiques depuis des serveurs proxy ou des équilibreurs de charge. Des options Java sont proposées pour affiner Health Monitor, réduisant l’incidence sur les performances de votre environnement AEM Forms. (Voir [Réglage précis des performances de Health Monitor](/help/forms/using/admin-help/fine-tuning-health-monitor-performance.md#fine-tuning-health-monitor-performance)).

**Accès à Health Monitor**

1. Dans la console d’administration, cliquez sur Health Monitor dans le coin supérieur droit de la page.
