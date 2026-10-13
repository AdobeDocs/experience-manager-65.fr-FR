---
title: 'DB2&reg ; base de données : exécution d''un processus hebdomadaire'
description: Découvrez comment améliorer les performances de votre base de données AEM Forms DB2&reg;.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_the_aem_forms_database
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: ca2cfe35-b602-4ef8-b4e3-af846105d4de
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
source-wordcount: '149'
ht-degree: 85%
---
# Base de données DB2® : exécution d’un processus hebdomadaire{#db-database-running-a-process-weekly}

Si votre base de données DB2® AEM Forms commence à s’exécuter lentement, l’exécution hebdomadaire du processus suivant peut améliorer ses performances :

1. Démarrez DB2® Control Center :

   (Windows) Sélectionnez Démarrer > Programmes > IBM® DB2® > Outils d’administration générale > Centre de contrôle.

   (Linux® et UNIX®) Ouvrez une invite de commande et saisissez la commande `db2jcc`.

1. Dans l’arborescence d’objets du centre de contrôle DB2®, cliquez sur Toutes les bases de données.
1. Cliquez sur la base de données que vous avez créée pour AEM Forms, puis sur le dossier Tables.
1. Sélectionnez tous les tableaux de base de données dans le volet de contenu, cliquez dessus avec le bouton droit et sélectionnez Statistiques d’exécution.
1. Accédez à Statistics > Index Statistics.
1. Sélectionnez Collect Statistics For All Indexes, puis Collect Statistics For Indexes With Extended Detailed Statistics et cliquez sur OK.

Un message s’affiche une fois le processus terminé. Fermez le message.
