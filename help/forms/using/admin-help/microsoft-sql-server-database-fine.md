---
title: '"Base de données SQL Server : réglage précis de la configuration"'
seo-title: '"Base de données SQL Server : réglage précis de la configuration"'
description: Découvrez comment vous pouvez affiner la configuration de votre base de données Microsoft SQL Server.
seo-description: Découvrez comment vous pouvez affiner la configuration de votre base de données Microsoft SQL Server.
uuid: 2d618aab-3c67-4edb-a28f-a20904689e6f
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_the_aem_forms_database
products: SG_EXPERIENCEMANAGER/6.5/FORMS, SG_AEMFORMS
discoiquuid: 70559a94-42ea-411a-a32f-5f38bc17ff96
translation-type: tm+mt
source-git-commit: a929252a13f66da8ac3e52aea0655b12bdd1425f
workflow-type: tm+mt
source-wordcount: '315'
ht-degree: 100%

---


# Base de données SQL Server : réglage précis de la configuration {#microsoft-sql-server-database-fine-tuning-the-configuration}

Lorsque vous utilisez Microsoft SQL Server, vous pouvez modifier les paramètres de configuration par défaut. Cliquez avec le bouton droit de la souris sur le serveur local dans Oracle Enterprise Manager pour accéder à la boîte de dialogue des propriétés.

## Paramètres de mémoire {#memory-settings}

Augmentez autant que possible l’allocation de mémoire minimale. Si la base de données est exécutée sur un ordinateur différent, utilisez l’intégralité de la mémoire. Les paramètres par défaut affectent relativement peu de mémoire, ce qui réduit les performances dans presque tous les cas. Dans un environnement de production, affectez autant de mémoire que possible.

## Paramètres de processeur {#processor-settings}

Modifiez les paramètres de processeur et, surtout, cochez la case Forcer la priorité de SQL Server sous Windows, de sorte que le serveur exploite autant de cycles que possible. Le paramètre Utiliser les fibres Windows NT est moins important, mais vous pouvez également le sélectionner.

## Paramètres de base de données {#database-settings}

Modifiez les paramètres de base de données. Le paramètre le plus important est Intervalle de récupération, qui spécifie le délai d’attente maximal après un blocage. Le paramètre par défaut est d’une minute. L’augmentation de ce délai (entre 5 et 15 minutes) améliore les performances en donnant plus de temps au serveur pour écrire dans les fichiers de la base de données les changements stockés dans le journal de la base de données.

>[!NOTE]
>
>Ce paramètre n’affecte pas la gestion des transactions car il ne fait que modifier la longueur de relecture du fichier journal qui doit être effectuée au démarrage.

Augmentez autant que possible l’espace alloué au journal et au fichier de données, pour qu’il soit supérieur à la base de données initiale. Essayez de calculer la croissance de la base de données sur une année. Dans l’idéal, le fichier journal et le fichier de données se trouvent dans un espace contigu de manière à ce que les données ne soient pas fragmentées sur tout le disque.
