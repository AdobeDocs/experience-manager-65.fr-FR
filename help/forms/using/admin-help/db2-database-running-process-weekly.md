---
title: "Base de données DB2\_: exécution d’un processus hebdomadaire"
description: Découvrez comment vous pouvez améliorer la performance de votre base de données AEM Forms DB2.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_the_aem_forms_database
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: ca2cfe35-b602-4ef8-b4e3-af846105d4de
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '145'
ht-degree: 26%

---

# Base de données DB2 : exécution d’un processus hebdomadaire{#db-database-running-a-process-weekly}

Si votre base de données AEM forms DB2 commence à s’exécuter lentement, l’exécution hebdomadaire du processus suivant peut améliorer ses performances :

1. Démarrez DB2 Control Center :

   (Windows) Sélectionnez Démarrer > Programmes > IBM DB2 > General Administration Tools > Control Center.

   (Linux et UNIX) Ouvrez une invite de commande et saisissez la commande `db2jcc`.

1. Dans l’arborescence d’objets DB2 Control Center, cliquez sur All Databases.
1. Cliquez sur la base de données que vous avez créée pour AEM forms et cliquez sur le dossier Tables .
1. Sélectionnez toutes les tables de base de données dans le volet de contenu, cliquez dessus avec le bouton droit et sélectionnez Exécuter les statistiques.
1. Accédez à Statistiques > Statistiques des index.
1. Sélectionnez Collecter des statistiques pour tous les index, puis Collecter des statistiques pour les index avec des statistiques détaillées étendues et cliquez sur OK.

Un message s’affiche une fois le processus terminé. Fermez le message.
