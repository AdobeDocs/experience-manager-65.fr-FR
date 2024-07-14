---
title: Échec de la sauvegarde de la base de données lors de la mise à niveau vers la version 6.5.12.0 pour MySQL.
description: Lorsqu’un utilisateur ou une utilisatrice effectue une mise à niveau vers Experience Manager 6.5.12.0 et clique sur « Mettre à niveau MySQL », le gestionnaire de configuration ne parvient pas à sauvegarder la base de données Experience Manager Forms précédente.
exl-id: 1af000fa-439b-4ffd-8b5a-3ba45f0c524c
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,AEM Forms on JEE
role: User, Developer
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '105'
ht-degree: 100%

---

# Échec de la sauvegarde de la base de données lors de la mise à niveau vers la version 6.5.12.0 pour MySQL {#issue}

Lorsqu’un utilisateur ou une utilisatrice effectue une mise à niveau vers Experience Manager 6.5.12.0 et clique sur « Mettre à niveau MySQL », le gestionnaire de configuration ne parvient pas à sauvegarder la base de données Experience Manager Forms précédente. L’erreur suivante s’affiche :

`Failed to backup the previous Adobe Experience Manager Forms Database`


## Application {#applies-to}

* Experience Manager 6.5 Forms

## Solution {#solution}

Pour résoudre le problème, augmentez la taille max_packet_size de la base de données à 100 Mo ou selon les besoins dans le fichier my.ini situé à l’emplacement {AEM_HOME}/mysql.
