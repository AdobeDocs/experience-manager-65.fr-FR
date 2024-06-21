---
title: Architecture de l’espace de travail AEM Forms
description: Informations conceptuelles et vue d’ensemble de l’architecture de l’espace de travail AEM Forms LiveCycle.
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
exl-id: c6f216d4-781c-4356-b9f0-3324903a28e7
solution: Experience Manager, Experience Manager Forms
feature: HTML5 Forms, Adaptive Forms
role: User, Developer
source-git-commit: e821be5233fd5f6688507096790d219d25903892
workflow-type: tm+mt
source-wordcount: '219'
ht-degree: 100%

---

# Architecture de l’espace de travail AEM Forms {#aem-forms-workspace-architecture}

L’espace de travail AEM Forms est une application web hébergée sur CRX™. Lorsque l’espace de travail est ouvert dans un navigateur, une ressource CRX est appelée et l’application est rendue en tant que page HTML dans le navigateur.

L’application accède au serveur AEM Forms sur les points d’entrée REST pour effectuer les opérations suivantes :

* Récupérer des tâches utilisateur, des points de départ de processus, l’historique des processus et des informations sur l’utilisateur ou l’utilisatrice
* Exécuter une action sur les tâches
* Interroger les tâches dans la base de données
* Mettre à jour des préférences utilisateur, etc.

Le serveur AEM Forms accède à la base de données AEM Forms via JDBC. La base de données conserve les tâches, les processus et leurs instances, les utilisateurs et utilisatrices et les informations associées.

L’espace de travail AEM Forms est constitué de composants modulaires JavaScript™ qui peuvent être personnalisés individuellement et réutilisés dans d’autres applications web. Les composants sont basés sur BackBone, une bibliothèque JavaScript qui fournit une structure aux applications web. Un article détaillé décrivant l’interaction des composants avec BackBone est disponible [ici](/help/forms/using/backbone-interaction.md). L’organisation des composants dans la structure de dossiers CRX est présentée dans [cet](/help/forms/using/folder-structure.md) article.

Packages fournis pour l’espace de travail AEM Forms :

* `adobe-lc-workspace-pkg-<version>.zip` : il s’agit du package CRX, c’est-à-dire qu’il peut être déployé dans CRX en utilisant Package Manager.
* `adobe-lc-workspace-<version>-src.zip` : il s’agit d’un fichier d’archive contenant le code complet de l’espace de travail AEM Forms et les scripts permettant de créer les packages de déploiement (Ship, Debug et Dev).
