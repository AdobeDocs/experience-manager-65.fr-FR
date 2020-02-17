---
title: Présentation de Health Monitor
seo-title: Présentation de Health Monitor
description: Ce document fournit une présentation de Health Monitor et des détails sur la manière dont vous pouvez y accéder.
seo-description: Ce document fournit une présentation de Health Monitor et des détails sur la manière dont vous pouvez y accéder.
uuid: 5934fd2d-80a5-4c6d-b3ee-882c2865705b
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/health_monitor
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: c303e967-944d-40b0-96ca-f91e2f42a0d0
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Présentation de Health Monitor {#overview-of-health-monitor}

Health Monitor fournit des informations essentielles sur le système AEM forms, telles que des informations sur le serveur, l’utilisation de la mémoire ou encore l’utilisation du processeur. Il fournit également les statistiques Work Manager, telles que le nombre de tâches dans la file d’attente ainsi que leur état. Vous pouvez effectuer les tâches suivantes à l’aide Health Monitor :

* vérification du bon fonctionnement du système ;
* affichage d’informations pour aider à diagnostiquer les problèmes système dès leur apparition ;
* réalisation d’opérations sur des éléments de travail ou des tâches affichant des problèmes ;
* purge d’enregistrements obsolètes de la base de données de Job Manager.

La page Health Monitor d’Administration Console se compose de trois onglets :

* L’onglet Système affiche des graphiques de contrôle des ressources ainsi que des informations sur le serveur Forms (ou sur le nœud dans un environnement en grappe) (voir [Affichage des informations du système](/help/forms/using/admin-help/view-system-information.md#view-system-information)).
* L’onglet Work Manager affiche les données liées à Work Manager, comme le nombre de tâches dans la file d’attente de Work Manager. Vous pouvez filtrer les informations en utilisant différents critères ou gérer des tâches individuelles en utilisant les outils d’opération (voir [Affichage des statistiques relatives à Work Manager](/help/forms/using/admin-help/view-statistics-related-manager.md#view-statistics-related-to-work-manager)).
* L’onglet Planificateur de purge de travaux vous permet de purger les enregistrements obsolètes de la base de données de Job Manager (voir [Purge d’enregistrements de la base de données de Job Manager](/help/forms/using/admin-help/purge-records-job-manager-database.md#purge-records-from-the-job-manager-database)).

La page Web Health Monitor est renseignée avec des statistiques collectées via une API Gemfire. Cette API détecte automatiquement tous les nœuds d’une grappe. Elle résout également les problèmes de sécurité qui surviennent lors de la collecte de statistiques derrière des serveurs proxy ou des services d’équilibrage de charge. Des options Java sont proposées pour affiner Health Monitor, réduisant l’incidence sur les performances de votre environnement AEM forms (voir [Réglage précis des performances d’Health Monitor](/help/forms/using/admin-help/fine-tuning-health-monitor-performance.md#fine-tuning-health-monitor-performance)).

**Accès à Health Monitor**

1. Dans l’angle supérieur droit de la page d’Administration Console, cliquez sur Health Monitor.

