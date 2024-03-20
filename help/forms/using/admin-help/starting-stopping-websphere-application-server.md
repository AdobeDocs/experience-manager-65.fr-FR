---
title: Démarrer et arrêter WebSphere Application Server
description: Plusieurs procédures nécessitent l’arrêt ou le démarrage de l’instance de WebSphere sur laquelle vous souhaitez déployer AEM produits forms. Ce document explique comment démarrer et arrêter WebSphere Application Server.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_the_application_server
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 1a4e8f20-0644-4c96-9f52-f7a59521eac9
solution: Experience Manager, Experience Manager Forms
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '180'
ht-degree: 56%

---

# Démarrer et arrêter WebSphere Application Server {#starting-and-stopping-websphere-application-server}

Plusieurs procédures nécessitent l’arrêt ou le démarrage de l’instance de WebSphere sur laquelle vous souhaitez déployer AEM produits forms. Si vous ne savez pas si le serveur d’applications a démarré, vous pouvez d’abord afficher l’état de WebSphere Application Server.

## Affichage de l’état de WebSphere Application Server {#view-the-status-of-websphere-application-server}

1. À partir d’une invite de commande, accédez au répertoire `[appserver root]/bin`.
1. Saisissez la commande suivante en remplaçant *nom_serveur* par le nom de WebSphere Application Server :

   * (Windows) `serverStatus.bat`*nom_serveur*
   * (Linux, UNIX) ./ `serverStatus.sh`*nom_serveur*

## Démarrez WebSphere Application Server {#start-websphere-application-server}

1. À partir d’une invite de commande, accédez au répertoire `[appserver root]/bin`.
1. Saisissez la commande suivante en remplaçant *nom_serveur* par le nom de WebSphere Application Server :

   * (Windows) `startServer.bat`*nom_serveur*
   * (Linux, UNIX) ./ `startServer.sh`*nom_serveur*

## Arrêt de WebSphere Application Server {#stop-websphere-application-server}

1. À partir d’une invite de commande, accédez au répertoire `[appserver root]/bin`.
1. Saisissez la commande suivante en remplaçant *nom_serveur* par le nom de WebSphere Application Server :

   * (Windows) `stopServer.bat`*nom_serveur*
   * (Linux, UNIX) ./ `stopServer.sh`*nom_serveur*
