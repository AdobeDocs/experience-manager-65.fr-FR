---
title: "DB2&reg; base de données : exécution d’un processus hebdomadaire"
description: Découvrez comment améliorer les performances de votre base de données AEM Forms DB2&reg;.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_the_aem_forms_database
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: ca2cfe35-b602-4ef8-b4e3-af846105d4de
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: tm+mt
source-wordcount: '148'
ht-degree: 23%

---

# Base de données DB2® : exécution d’un processus hebdomadaire{#db-database-running-a-process-weekly}

Si votre base de données AEM Forms DB2® commence à s’exécuter lentement, l’exécution hebdomadaire du processus suivant peut améliorer ses performances :

1. Démarrez DB2® Control Center :

   (Windows) Sélectionnez Démarrer > Programmes > IBM® DB2® > Outils d’administration générale > Centre de contrôle.

   (Linux® et UNIX®) À partir d’une invite de commande, saisissez la variable `db2jcc` .

1. Dans l’arborescence d’objets DB2® Control Center, cliquez sur All Databases.
1. Cliquez sur la base de données que vous avez créée pour AEM Forms, puis sur le dossier Tables .
1. Sélectionnez toutes les tables de base de données dans le volet de contenu, cliquez dessus avec le bouton droit, puis sélectionnez Exécuter les statistiques.
1. Accédez à Statistics > Index Statistics.
1. Sélectionnez Collect Statistics For All Indexes, puis Collect Statistics For Indexes With Extended Detailed Statistics et cliquez sur OK.

Un message s’affiche une fois le processus terminé. Fermez le message.
