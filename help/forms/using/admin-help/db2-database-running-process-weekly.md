---
title: '« Base de données DB2® : exécution d’un processus hebdomadaire »'
description: Découvrez comment vous pouvez améliorer la performance de votre base de données AEM Forms DB2®.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_the_aem_forms_database
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: ca2cfe35-b602-4ef8-b4e3-af846105d4de
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: ht
source-wordcount: '148'
ht-degree: 100%

---

# Base de données DB2® : exécution d’un processus hebdomadaire{#db-database-running-a-process-weekly}

Si votre base de données DB2® AEM Forms commence à s’exécuter lentement, l’exécution hebdomadaire du processus suivant peut améliorer ses performances :

1. Démarrez DB2® Control Center :

   (Windows) Sélectionnez Démarrer > Programmes > IBM® DB2® > Outils d’administration générale > Centre de contrôle.

   (Linux® et UNIX®) Ouvrez une invite de commande et saisissez la commande `db2jcc`.

1. Dans l’arborescence d’objets du centre de contrôle DB2®, cliquez sur Toutes les bases de données.
1. Cliquez sur la base de données que vous avez créée pour AEM Forms, puis sur le dossier Tableaux.
1. Sélectionnez tous les tableaux de base de données dans le volet de contenu, cliquez dessus avec le bouton droit et sélectionnez Statistiques d’exécution.
1. Accédez à Statistics > Index Statistics.
1. Sélectionnez Collect Statistics For All Indexes, puis Collect Statistics For Indexes With Extended Detailed Statistics et cliquez sur OK.

Un message s’affiche une fois le processus terminé. Fermez le message.
