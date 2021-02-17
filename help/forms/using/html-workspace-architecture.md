---
title: Architecture de l’espace de travail AEM Forms
seo-title: Architecture de l’espace de travail AEM Forms
description: Informations conceptuelles et présentation de l’architecture de l’espace de travail LiveCycle AEM Forms.
seo-description: Informations conceptuelles et présentation de l’architecture de l’espace de travail LiveCycle AEM Forms.
uuid: e1a48452-ed44-4ea7-ba38-d961c8faafa5
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: c3a312fb-f684-477d-916d-2d3c99aa7607
translation-type: tm+mt
source-git-commit: 56c6cfd437ef185336e81373bd5f758205b96317
workflow-type: tm+mt
source-wordcount: '235'
ht-degree: 81%

---


# Architecture de l’espace de travail AEM Forms {#aem-forms-workspace-architecture}

L’espace de travail AEM Forms est une application Web hébergée sur CRX™. Lorsque l’espace de travail est ouvert dans un navigateur, une ressource CRX est appelée et l’application est rendue en tant que page HTML dans le navigateur.

L’application accède au serveur AEM Forms sur les points d’extrémité REST pour effectuer les opérations suivantes :

* récupérer les tâches de l’utilisateur, les points de départ des processus, l’historique des processus et les informations sur l’utilisateur ;
* effectuer des actions sur des tâches ;
* interroger les tâches dans la base de données ;
* mettre à jour les préférences de l’utilisateur, etc.

Le serveur AEM Forms accède à la base de données AEM Forms sur JDBC. La base de données sauvegarde les tâches, les processus et leurs instances, les utilisateurs ainsi que les informations associées.

L’espace de travail AEM Forms est conçu en composants modulaires JavaScript™ qui peuvent être personnalisés individuellement et réutilisés dans d’autres applications Web. Les composants sont basés sur BackBone, une bibliothèque JavaScript qui fournit une structure aux applications Web. Un article détaillé présentant l’interaction des composants avec BackBone est disponible [ici](/help/forms/using/backbone-interaction.md). L’organisation des composants dans la structure de dossier de CRX est présentée dans [cet](/help/forms/using/folder-structure.md) article.

Packages fournis pour l’espace de travail AEM Forms :

* `adobe-lc-workspace-pkg-<version>.zip` : il s’agit du package CRX, c’est-à-dire qu’il peut être déployé dans CRX en utilisant Package Manager.
* `adobe-lc-workspace-<version>-src.zip`: Il s’agit d’une archive qui contient le code complet de l’espace de travail AEM Forms et des scripts pour créer les packs de déploiement (Ship, Debug et Dev).
