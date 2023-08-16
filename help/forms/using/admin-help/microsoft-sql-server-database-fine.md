---
title: "Base de données SQL Server\_: réglage précis de la configuration"
description: Découvrez comment affiner la configuration de votre base de données Microsoft SQL Server.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_the_aem_forms_database
products: SG_EXPERIENCEMANAGER/6.5/FORMS, SG_AEMFORMS
exl-id: 9c570827-86e2-47d5-b8ae-66c0767bff2e
source-git-commit: 10227bcfcfd5a9b0f126fee74dce6ec7842f5e95
workflow-type: tm+mt
source-wordcount: '293'
ht-degree: 4%

---

# Base de données SQL Server : réglage précis de la configuration {#microsoft-sql-server-database-fine-tuning-the-configuration}

Lorsque vous utilisez Microsoft SQL Server, vous devez modifier les paramètres de configuration par défaut. Cliquez avec le bouton droit sur le serveur local dans Oracle Enterprise Manager pour accéder à la boîte de dialogue des propriétés.

## Paramètres de mémoire {#memory-settings}

Remplacez l’allocation de mémoire minimale par un nombre aussi grand que possible. Si la base de données est exécutée sur un ordinateur distinct, utilisez toute la mémoire. Les paramètres par défaut n’allouent pas de manière agressive la mémoire, ce qui nuit aux performances sur presque toutes les bases de données. Vous devez être plus agressif dans l’allocation de mémoire sur les machines de production.

## Paramètres du processeur {#processor-settings}

Modifiez les paramètres du processeur et, surtout, cochez la case Renforcer la priorité SQL Server sous Windows afin que le serveur utilise autant de cycles que possible. Le paramètre Utiliser les fibres NT est moins important, mais vous pouvez également le sélectionner.

## Paramètres de base de données {#database-settings}

Modifiez les paramètres de la base de données. Le paramètre le plus important est l’ Intervalle de récupération , qui spécifie le temps maximal d’attente de récupération après un blocage. Le paramètre par défaut est d’une minute. L’utilisation d’une valeur plus élevée, comprise entre 5 et 15 minutes, améliore les performances car elle donne au serveur plus de temps pour écrire les modifications du journal de base de données dans les fichiers de base de données.

>[!NOTE]
>
>Ce paramètre ne compromet pas le comportement transactionnel, car il ne modifie que la longueur de relecture du fichier journal qui doit être effectuée au démarrage.

Définissez la taille d’ espace alloué pour le journal et le fichier de données sur une taille beaucoup plus grande que la base de données initiale. Tenez compte de la croissance de la base de données sur une année. Idéalement, le journal et les fichiers de données sont alloués de manière contiguë afin que les données ne soient pas fragmentées sur tout le disque.
