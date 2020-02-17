---
title: '"Base de données DB2 : exécution d’un processus hebdomadaire"'
seo-title: '"Base de données DB2 : exécution d’un processus hebdomadaire"'
description: Découvrez comment vous pouvez améliorer la performance de votre base de données AEM Forms DB2.
seo-description: Découvrez comment vous pouvez améliorer la performance de votre base de données AEM Forms DB2.
uuid: 36070087-c250-41df-a841-aa922e777697
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_the_aem_forms_database
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: fc0e8183-5d50-4fc0-997a-5f3168ba0d70
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Base de données DB2 : exécution d’un processus hebdomadaire{#db-database-running-a-process-weekly}

Si la base de données AEM forms DB2 montre des signes de ralentissement, effectuez la procédure suivante chaque semaine pour améliorer ses performances :

1. Démarrez DB2 Control Center :

   (Windows) Sélectionnez Démarrer > Programmes > IBM DB2 > General Administration Tools > Control Center.

   (Linux et UNIX) Ouvrez une invite de commande et saisissez la commande `db2jcc`.

1. Dans l’arborescence de DB2 Control Center, cliquez sur All Databases.
1. Cliquez sur la base de données que vous avez créée pour AEM forms et cliquez sur Tables.
1. Sélectionnez toutes les tables de base de données dans le volet de contenu, puis cliquez sur celles-ci avec le bouton droit de la souris et sélectionnez Run Statistics.
1. Accédez à Statistics > Index Statistics.
1. Sélectionnez Collect Statistics For All Indexes, puis Collect Statistics For Indexes With Extended Detailed Statistics et enfin sur OK.

Un message apparaît une fois le processus terminé. Fermez le message.
