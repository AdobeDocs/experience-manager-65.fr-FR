---
title: Démarrage et arrêt de WebSphere Application Server
seo-title: Démarrage et arrêt de WebSphere Application Server
description: Plusieurs procédures nécessitent d’arrêter ou de démarrer l’instance de WebSphere sur laquelle vous souhaitez déployer les produits AEM forms. Ce document explique le démarrage et l’arrêt de WebSphere Application Server.
seo-description: Plusieurs procédures nécessitent d’arrêter ou de démarrer l’instance de WebSphere sur laquelle vous souhaitez déployer les produits AEM forms. Ce document explique le démarrage et l’arrêt de WebSphere Application Server.
uuid: e0373197-aa57-4087-933d-92a86840a11a
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_the_application_server
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: bcd16691-67ab-4694-9e6b-c9d3e0c7bf0b
translation-type: tm+mt
source-git-commit: 67ea825215d1ca7cc2e350ed1c128c3146de45ec
workflow-type: tm+mt
source-wordcount: '227'
ht-degree: 82%

---


# Démarrage et arrêt de WebSphere Application Server {#starting-and-stopping-websphere-application-server}

Plusieurs procédures nécessitent d’arrêter ou de démarrer l’instance de WebSphere sur laquelle vous souhaitez déployer les produits AEM forms. Si vous ne savez pas si le serveur d’applications a déjà été démarré, vous pouvez commencer par vérifier l’état de WebSphere Application Server.

## Affichage de l’état de WebSphere Application Server {#view-the-status-of-websphere-application-server}

1. Ouvrez une invite de commande et accédez au répertoire `[appserver root]/bin`.
1. Saisissez la commande suivante en remplaçant *nom_serveur* par le nom de WebSphere Application Server :

   * (Windows) `serverStatus.bat`*nom_serveur*
   * (Linux, UNIX) ./ `serverStatus.sh`*nom_serveur*

## Démarrez WebSphere Application Server {#start-websphere-application-server}

1. Ouvrez une invite de commande et accédez au répertoire `[appserver root]/bin`.
1. Saisissez la commande suivante en remplaçant *nom_serveur* par le nom de WebSphere Application Server :

   * (Windows) `startServer.bat`*nom_serveur*
   * (Linux, UNIX) ./ `startServer.sh`*nom_serveur*

## Arrêt de WebSphere Application Server {#stop-websphere-application-server}

1. Ouvrez une invite de commande et accédez au répertoire `[appserver root]/bin`.
1. Saisissez la commande suivante en remplaçant *nom_serveur* par le nom de WebSphere Application Server :

   * (Windows) `stopServer.bat`*nom_serveur*
   * (Linux, UNIX) ./ `stopServer.sh`*nom_serveur*

