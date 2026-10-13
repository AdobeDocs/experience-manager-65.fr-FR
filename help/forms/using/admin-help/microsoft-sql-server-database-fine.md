---
title: 'Base de données SQL Server : réglage précis de la configuration'
description: Découvrez comment vous pouvez affiner la configuration de votre base de données Microsoft SQL Server.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_the_aem_forms_database
products: SG_EXPERIENCEMANAGER/6.5/FORMS, SG_AEMFORMS
exl-id: 9c570827-86e2-47d5-b8ae-66c0767bff2e
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
source-wordcount: '299'
ht-degree: 100%
---
# Base de données SQL Server : réglage précis de la configuration {#microsoft-sql-server-database-fine-tuning-the-configuration}

Lorsque vous utilisez Microsoft SQL Server, vous devez modifier les paramètres de configuration par défaut. Cliquez avec le bouton droit de la souris sur le serveur local dans Oracle Enterprise Manager pour accéder à la boîte de dialogue des propriétés.

## Paramètres de mémoire {#memory-settings}

Augmentez autant que possible l’allocation de mémoire minimale. Si la base de données est exécutée sur un ordinateur différent, utilisez l’intégralité de la mémoire. Les paramètres par défaut affectent relativement peu de mémoire, ce qui réduit les performances sur presque toutes les bases de données. Dans un environnement de production, affectez autant de mémoire que possible.

## Paramètres de processeur {#processor-settings}

Modifiez les paramètres de processeur et, surtout, cochez la case Forcer la priorité de SQL Server sous Windows, de sorte que le serveur exploite autant de cycles que possible. Le paramètre Utiliser les fibres Windows NT est moins important, mais vous pouvez également le sélectionner.

## Paramètres de base de données {#database-settings}

Modifiez les paramètres de la base de données. Le paramètre le plus important est Intervalle de récupération, qui spécifie le délai d’attente maximal après un blocage. Le paramètre par défaut est d’une minute. L’augmentation de ce délai (entre 5 et 15 minutes) améliore les performances en donnant plus de temps au serveur pour écrire dans les fichiers de la base de données les changements stockés dans le journal de la base de données.

>[!NOTE]
>
>Ce paramètre n’affecte pas le comportement transactionnel, car il ne fait que modifier la longueur de relecture du fichier journal qui doit être effectuée au démarrage.

Augmentez autant que possible l’espace alloué au journal et au fichier de données, pour qu’il soit supérieur à la base de données initiale. Essayez de calculer la croissance de la base de données sur une année. Dans l’idéal, le fichier journal et le fichier de données se trouvent dans un espace contigu de manière à ce que les données ne soient pas fragmentées sur tout le disque.
