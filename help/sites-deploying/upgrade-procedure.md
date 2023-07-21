---
title: Procédure de mise à niveau
description: Découvrez la procédure de mise à niveau d’Adobe Experience Manager (AEM).
contentOwner: sarchiz
topic-tags: upgrading
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
docset: aem65
targetaudience: target-audience upgrader
feature: Upgrading
exl-id: 5242600c-2281-46f9-a347-d985b4e319b3
source-git-commit: a56d5121a6ce11b42a6c30dae9e479564d16af27
workflow-type: tm+mt
source-wordcount: '815'
ht-degree: 21%

---

# Procédure de mise à niveau {#upgrade-procedure}

>[!NOTE]
>
>La mise à niveau nécessite un temps d’arrêt pour le niveau Auteur, car la plupart des mises à niveau d’Adobe Experience Manager (AEM) sont effectuées sur place. En suivant ces bonnes pratiques, vous pouvez réduire ou éliminer le temps d’arrêt du niveau Publication.

Lors de la mise à niveau de vos environnements AEM, vous devez tenir compte des différences d’approche entre la mise à niveau des environnements de création ou de publication afin de minimiser les temps d’arrêt pour vos auteurs et vos utilisateurs finaux. Cette page décrit la procédure de haut niveau pour mettre à niveau une topologie AEM en cours d’exécution sur une version d’AEM 6.x. Comme le processus diffère entre les niveaux de création et de publication, ainsi que les déploiements basés sur Mongo et TarMK, chaque niveau et micro-noyau a été répertorié dans une section distincte. Lors de l’exécution de votre déploiement, Adobe recommande d’abord de mettre à niveau votre environnement de création, de déterminer la réussite, puis de passer aux environnements de publication.

<!--
>[!IMPORTANT]
>
>The downtime during the upgrade can be significally reduced by indexing the repository before performing the upgrade. For more information, see [Using Offline Reindexing To Reduce Downtime During an Upgrade](/help/sites-deploying/upgrade-offline-reindexing.md)
-->

## Niveau de création TarMK {#tarmk-author-tier}

### Démarrage de la topologie {#starting-topology}

La topologie utilisée pour cette section consiste en un serveur d’auteur s’exécutant sur TarMK avec un Secondaire Cold. La réplication se produit du serveur d’auteur à la ferme de publication TarMK. Bien qu’elle ne soit pas illustrée ici, cette approche peut également être utilisée pour les déploiements qui utilisent le déchargement. Veillez à mettre à niveau ou à recréer l’instance de déchargement sur la nouvelle version après avoir désactivé les agents de réplication sur l’instance d’auteur et avant de les réactiver.

![tarmk_starting_topology](assets/tarmk_starting_topology.jpg)

### Préparation de la mise à niveau {#upgrade-preparation}

![upgrade-preparation-author](assets/upgrade-preparation-author.png)

1. Arrêtez la création de contenu..

1. Arrêtez l’instance Secondaire.

1. Désactivez les agents de réplication sur l’auteur.

1. Exécutez la variable [tâches de maintenance préalables à la mise à niveau](/help/sites-deploying/pre-upgrade-maintenance-tasks.md).

### Exécution de la mise à niveau {#upgrade-execution}

![execute_upgrade](assets/execute_upgrade.jpg)

1. Exécutez la [mise à niveau sur place](/help/sites-deploying/in-place-upgrade.md)..
1. Mise à jour du module Dispatcher *si nécessaire*.

1. Le contrôle qualité valide la mise à niveau.

1. Arrêtez l’instance d’auteur.

### En cas de réussite {#if-successful}

![if_successful](assets/if_successful.jpg)

1. Copiez l’instance mise à niveau pour créer un Secondaire Cold.

1. Démarrez l’instance d’auteur.

1. Démarrez l’instance de secours.

### En cas d’échec (restauration) {#if-unsuccessful-rollback}

![restauration](assets/rollback.jpg)

1. Démarrez l’instance Cold Standby en tant que nouvelle instance principale..

1. Recréez l’environnement de création depuis l’instance Cold Standby.

## Grappe d’auteurs MongoMK {#mongomk-author-cluster}

### Démarrage de la topologie {#starting-topology-1}

La topologie supposée de cette section est constituée d’un cluster d’auteur MongoMK avec au moins deux instances d’auteur AEM, prises en charge par au moins deux bases de données MongoMK. Toutes les instances d’auteur partagent une banque de données. Ces étapes doivent s’appliquer aux entrepôts de données S3 et File. La réplication se produit des serveurs d’auteur à la ferme de publication TarMK.

![mongo-topology](assets/mongo-topology.jpg)

### Préparation de la mise à niveau {#upgrade-preparation-1}

![mongo-upgrade_prep](assets/mongo-upgrade_prep.jpg)

1. Arrêtez la création de contenu..
1. Cloner l’entrepôt de données à des fins de sauvegarde.
1. Arrêtez toutes les instances d’auteur AEM sauf une, votre Principal auteur.
1. Supprimez tous les noeuds MongoDB de l’ensemble de réplication, votre Principale instance Mongo.
1. Mettez à jour le `DocumentNodeStoreService.cfg` sur l’auteur Principal pour refléter votre jeu de réplications de membre unique.
1. Redémarrez l’auteur Principal pour vous assurer qu’il redémarre correctement.
1. Désactivez les agents de réplication sur l’auteur Principal.
1. Exécuter [tâches de maintenance préalables à la mise à niveau](/help/sites-deploying/pre-upgrade-maintenance-tasks.md) sur l’instance d’auteur Principale.
1. Si nécessaire, mettez à niveau MongoDB sur l’Principale instance Mongo vers la version 3.2 avec WiredTiger.

### Exécution de la mise à niveau {#Upgrade-execution-1}

![mongo-execution](assets/mongo-execution.jpg)

1. Exécutez une [mise à niveau sur place](/help/sites-deploying/in-place-upgrade.md) sur l’auteur principal..
1. Mise à jour de Dispatcher ou du module web *si nécessaire*.
1. Le contrôle qualité valide la mise à niveau.

### En cas de réussite {#if-successful-1}

![mongo-secondaries](assets/mongo-secondaries.jpg)

1. Créez de nouvelles instances d’auteur 6.5, connectées à votre instance de mise à niveau Mongo..

1. Recréez les noeuds MongoDB qui ont été supprimés de la grappe.

1. Mettez à jour le `DocumentNodeStoreService.cfg` pour refléter l’ensemble de réplication complet.

1. Redémarrez les instances d’auteur, une par une.

1. Supprimez les magasin de données clonés.

### En cas d’échec (restauration)  {#if-unsuccessful-rollback-2}

![mongo-rollback](assets/mongo-rollback.jpg)

1. Reconfigurez les instances d’auteur secondaires pour établir la connexion au magasin de données cloné..

1. Arrêtez l’instance Principale d’auteur mise à niveau.

1. Désactivez l’instance principale Mongo mise à niveau.

1. Démarrez les instances secondaires Mongo, l’une d’entre elles faisant office d’instance principale..

1. Configurez la variable `DocumentNodeStoreService.cfg` sur les instances d’auteur secondaires pour pointer vers l’ensemble de réplication des instances Mongo non encore mises à niveau.

1. Démarrez les instances d’auteur secondaires.

1. Nettoyez les instances d’auteur, le noeud Mongo et l’entrepôt de données mis à niveau.

## Ferme de publication TarMK {#tarmk-publish-farm}

### Ferme de publication TarMK {#tarmk-publish-farm-1}

La topologie supposée de cette section est composée de deux instances de publication TarMK, devant lesquelles les dispatchers sont eux-mêmes devancés par un équilibreur de charge. La réplication se produit du serveur de création à la ferme de publication TarMK.

![tarmk-pub-farmv5](assets/tarmk-pub-farmv5.png)

### Exécution de la mise à niveau {#upgrade-execution-2}

![upgrade-publish2](assets/upgrade-publish2.png)

1. Arrêtez le trafic de l’instance de publication 2 à l’équilibreur de charge..
1. Exécuter [maintenance avant la mise à niveau](/help/sites-deploying/pre-upgrade-maintenance-tasks.md) sur la publication 2.
1. Exécutez une [mise à niveau statique](/help/sites-deploying/in-place-upgrade.md) sur la publication 2.
1. Mise à jour de Dispatcher ou du module web *si nécessaire*.
1. Videz le cache de Dispatcher.
1. Le contrôle qualité valide la publication 2 via Dispatcher, derrière le pare-feu.
1. Arrêter la publication 2.
1. Copiez l’instance de publication 2.
1. Démarrez la publication 2.

### En cas de réussite {#if-successful-2}

![upgrade-publish1](assets/upgrade-publish1.png)

1. Activez le trafic vers l’instance de publication 2..
1. Arrêtez le trafic vers la publication 1.
1. Arrêtez l’instance de publication 1.
1. Remplacez l’instance de publication 1 par une copie de la publication 2.
1. Mise à jour de Dispatcher ou du module web *si nécessaire*.
1. Videz le cache de Dispatcher pour la publication 1.
1. Démarrez la publication 1.
1. Le contrôle qualité valide la publication 1 via Dispatcher, derrière le pare-feu.

### En cas d’échec (restauration) {#if-unsuccessful-rollback-1}

![pub_rollback](assets/pub_rollback.jpg)

1. Créez une copie de l’instance de publication 1..
1. Remplacez l’instance de publication 2 par une copie de la publication 1.
1. Videz le cache de Dispatcher pour la publication 2.
1. Démarrez la publication 2.
1. Le contrôle qualité valide la publication 2 via Dispatcher, derrière le pare-feu.
1. Activez le trafic vers la publication 2.

## Dernières étapes de mise à niveau {#final-upgrade-steps}

1. Activez le trafic vers l’instance de publication 1..
1. Le contrôle qualité procède à la validation finale à partir d’une URL publique.
1. Activez les agents de réplication à partir de l’environnement de création.
1. Reprenez la création de contenu.
1. Effectuez les [vérifications d’après mise à niveau](/help/sites-deploying/post-upgrade-checks-and-troubleshooting.md).

![final](assets/final.jpg)
