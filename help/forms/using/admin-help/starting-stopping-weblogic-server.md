---
title: Démarrage et arrêt de WebLogic Server
seo-title: Démarrage et arrêt de WebLogic Server
description: Plusieurs procédures nécessitent de démarrer ou d’arrêter l’instance de WebLogic Server sur laquelle vous souhaitez déployer les modules d’AEM forms. Ce document explique le démarrage et l’arrêt de WebLogic Server.
seo-description: Plusieurs procédures nécessitent de démarrer ou d’arrêter l’instance de WebLogic Server sur laquelle vous souhaitez déployer les modules d’AEM forms. Ce document explique le démarrage et l’arrêt de WebLogic Server.
uuid: 957787fe-4cea-4ecd-b49a-c33023c5c309
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_the_application_server
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: c908d064-6596-473a-b218-22a2496c83f7
source-git-commit: 317fadfe48724270e59644d2ed9a90fbee95cf9f
workflow-type: tm+mt
source-wordcount: '639'
ht-degree: 77%

---


# Démarrage et arrêt de WebLogic Server {#starting-and-stopping-weblogic-server}

Plusieurs procédures nécessitent de démarrer ou d’arrêter l’instance de WebLogic Server sur laquelle vous souhaitez déployer les modules d’AEM forms. Vérifiez que WebLogic Server est arrêté ou en cours d’exécution, selon la tâche que vous effectuez.

<table>
 <thead>
  <tr>
   <th><p>Activité</p></th>
   <th><p>Etat de WebLogic requis</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>Création d’un domaine WebLogic</p></td>
   <td><p>Arrêté</p></td>
  </tr>
  <tr>
   <td><p>Création d’un serveur géré WebLogic</p></td>
   <td><p>En cours d’exécution</p></td>
  </tr>
  <tr>
   <td><p>Augmentation du nombre de threads du serveur</p></td>
   <td><p>En cours d’exécution</p></td>
  </tr>
  <tr>
   <td><p>Déploiement des produits AEM forms</p></td>
   <td><p>En cours d’exécution</p></td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>Si vous exécutez WebLogic Server sous Red Hat® Enterprise Linux Advanced Server 4.0, définissez la variable d’environnement `LD_ASSUME_KERNEL` sur 2.4.19 à l’aide de la commande `export LD_ASSUME_KERNEL=2.4.19`. Exécutez ensuite WebLogic Server depuis le shell à partir duquel vous avez défini la variable d’environnement.

## Lancement de WebLogic Server {#start-weblogic-server}

1. Ouvrez une invite de commande et accédez à *[racine du serveur d’applications]*/user_projects/domains/*[domaine du serveur d’applications]*.
1. Saisissez la commande suivante :

   * (Windows) `startWebLogic.cmd`
   * (Linux, UNIX) ./ `startWebLogic.sh`

## Arrêt de WebLogic Server {#stop-weblogic-server}

1. Démarrez WebLogic Server Administration Console en saisissant `https://[host name]:7001/console` dans la ligne d’adresse d’un navigateur Web.
1. Connectez-vous en saisissant le nom d’utilisateur et le mot de passe utilisés lors de la création de cette configuration WebLogic, puis cliquez sur Log In.
1. Sous Change Center, cliquez sur Lock &amp; Edit.
1. Sous Domain Structure, cliquez sur Environment > Servers.
1. Cliquez sur AdminServer puis, dans le volet Setting for AdminServer, cliquez sur l’onglet Control.
1. Vérifiez que AdminServer est sélectionné dans le tableau Server Status, puis cliquez sur Shutdown.
1. Sélectionnez When work completes pour arrêter le serveur normalement ou Force Shutdown Now pour l’arrêter immédiatement sans achever les tâches en cours.
1. Dans le volet Server Life Cycle Assistant, cliquez sur Yes pour arrêter le serveur.

WebLogic Server Administration Console n’est plus accessible et l’invite de commande à partir de laquelle vous avez exécuté la commande start redevient disponible.

## Démarrage de WebLogic Administration Console  {#start-weblogic-administration-console}

1. Si WebLogic Admin Server n’est pas déjà en cours d’exécution, ouvrez une invite de commande, accédez au répertoire *[racine du serveur d’applications]\user_projects\domains\[nom du domaine]*, puis saisissez la commande suivante :

   * (Windows) `startWebLogic.cmd`
   * (Linux, UNIX) ./ `startWebLogic.sh`

1. Accédez à WebLogic Server Administration Console en saisissant `https://[host name]:[port]/console` dans la ligne d’adresse d’un navigateur Web, où *[port]* est le port d’écoute non sécurisé. Par défaut, la valeur de ce port est 7001.
1. Dans l’écran de connexion, saisissez le nom d’utilisateur et le mot de passe, puis cliquez sur Log In.

## Démarrage de Node Manager  {#start-node-manager}

1. Vérifiez que WebLogic Server est en cours d’exécution.
1. Ouvrez une nouvelle invite de commande et accédez à la *[racine du serveur d’applications]*/server/bin.
1. Saisissez la commande suivante :

   * (Windows) `startNodeManager.cmd`
   * (Linux, UNIX) `./startNodeManager.sh`

## Arrêt de Node Manager {#stop-node-manager}

Après avoir arrêté WebLogic Server, vous pouvez fermer l’invite de commande à partir de laquelle vous avez appelé Node Manager.

## Démarrage d’un serveur géré WebLogic  {#start-a-weblogic-managed-server}

>[!NOTE]
>
>cette tâche ne peut être effectuée qu’après avoir créé un domaine WebLogic et un serveur géré.

1. Assurez-vous que WebLogic Server et Node Manager sont en cours d’exécution.
1. Démarrez WebLogic Server Administration Console en saisissant `https://host name]:[port]`/console dans la ligne d’adresse d’un navigateur Web.
1. Sous Domain Structure, cliquez sur Environment > Servers.
1. Dans le volet de droite, cliquez sur l’onglet Configuration.
1. Sélectionnez le serveur géré que vous souhaitez démarrer.
1. Cliquez sur le bouton Start situé sous le serveur géré à démarrer.

## Arrêt d’ un serveur géré WebLogic  {#stop-a-weblogic-managed-server}

1. Démarrez WebLogic Server Administration Console en saisissant `https://`*[nom d’hôte]:[port ]*`/console` dans la ligne d’adresse d’un navigateur Web.
1. Sous Domain Structure, cliquez sur Environment > Servers.
1. Dans le volet de droite, cliquez sur l’onglet Configuration.
1. Sélectionnez le serveur géré que vous souhaitez arrêter.
1. Cliquez sur le bouton Shutdown situé sous le serveur géré à arrêter.
1. Sélectionnez When work completes pour arrêter le serveur normalement ou Force Shutdown Now pour l’arrêter immédiatement sans achever les tâches en cours.
1. Dans le volet Server Life Cycle Assistant, cliquez sur Yes pour arrêter le serveur.

