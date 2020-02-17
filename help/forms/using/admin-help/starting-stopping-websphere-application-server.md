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
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Démarrage et arrêt de WebSphere Application Server {#starting-and-stopping-websphere-application-server}

Plusieurs procédures nécessitent d’arrêter ou de démarrer l’instance de WebSphere sur laquelle vous souhaitez déployer les produits AEM forms. Si vous ne savez pas si le serveur d’applications a déjà été démarré, vous pouvez commencer par vérifier l’état de WebSphere Application Server.

## Affichage de l’état de WebSphere Application Server {#view-the-status-of-websphere-application-server}

1. From a command prompt, go to the *[appserver root]*/bin directory.
1. Saisissez la commande suivante en remplaçant *nom_serveur* par le nom de WebSphere Application Server :

   * (Windows) `serverStatus.bat`*server_name *
   * (Linux, UNIX) ./ `serverStatus.sh`*server_name *

## Démarrez WebSphere Application Server {#start-websphere-application-server}

1. From a command prompt, go to the *[appserver root]*/bin directory.
1. Saisissez la commande suivante en remplaçant *nom_serveur* par le nom de WebSphere Application Server :

   * (Windows) `startServer.bat`*server_name *
   * (Linux, UNIX) ./ `startServer.sh`*server_name *

## Arrêt de WebSphere Application Server {#stop-websphere-application-server}

1. From a command prompt, go to the *[appserver root]*/bin directory.
1. Saisissez la commande suivante en remplaçant *nom_serveur* par le nom de WebSphere Application Server :

   * (Windows) `stopServer.bat`*server_name *
   * (Linux, UNIX) ./ `stopServer.sh`*server_name *

