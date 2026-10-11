---
title: Démarrer et arrêter WebSphere Application Server
description: Plusieurs procédures nécessitent d’arrêter ou de démarrer l’instance de WebSphere sur laquelle vous souhaitez déployer les produits AEM Forms. Ce document décrit comment démarrer et arrêter WebSphere Application Server.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_the_application_server
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 1a4e8f20-0644-4c96-9f52-f7a59521eac9
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
source-wordcount: '180'
ht-degree: 95%
---
# Démarrer et arrêter WebSphere Application Server {#starting-and-stopping-websphere-application-server}

Plusieurs procédures nécessitent d’arrêter ou de démarrer l’instance de WebSphere sur laquelle vous souhaitez déployer les produits AEM Forms. Si vous ne savez pas si le serveur d’applications a démarré, vous pouvez d’abord afficher le statut de WebSphere Application Server.

## Afficher le statut de WebSphere Application Server {#view-the-status-of-websphere-application-server}

1. À partir d’une invite de commande, accédez au répertoire `[appserver root]/bin`.
1. Saisissez la commande suivante en remplaçant *nom_serveur* par le nom de WebSphere Application Server :

   * (Windows) `serverStatus.bat`*nom_serveur*
   * (Linux, UNIX) ./ `serverStatus.sh`*nom_serveur*

## Démarrer WebSphere Application Server {#start-websphere-application-server}

1. À partir d’une invite de commande, accédez au répertoire `[appserver root]/bin`.
1. Saisissez la commande suivante en remplaçant *nom_serveur* par le nom de WebSphere Application Server :

   * (Windows) `startServer.bat`*nom_serveur*
   * (Linux, UNIX) ./ `startServer.sh`*nom_serveur*

## Arrêt de WebSphere Application Server {#stop-websphere-application-server}

1. À partir d’une invite de commande, accédez au répertoire `[appserver root]/bin`.
1. Saisissez la commande suivante en remplaçant *nom_serveur* par le nom de WebSphere Application Server :

   * (Windows) `stopServer.bat`*nom_serveur*
   * (Linux, UNIX) ./ `stopServer.sh`*nom_serveur*
