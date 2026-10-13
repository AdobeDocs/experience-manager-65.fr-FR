---
title: Échec de la sauvegarde de la base de données lors de la mise à niveau vers 6.5.12.0 pour MySQL.
description: Lorsqu’un utilisateur effectue une mise à niveau vers Experience Manager 6.5.12.0 et clique sur « Mettre à niveau MySQL », le gestionnaire de configuration ne parvient pas à sauvegarder la base de données Experience Manager Forms précédente.
exl-id: 1af000fa-439b-4ffd-8b5a-3ba45f0c524c
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,AEM Forms on JEE
role: User, Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: 94663796-0ee7-58b9-84f4-b425ebb69e83
    internal-label: AEM Forms on JEE
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
source-wordcount: '102'
ht-degree: 15%
---
# Échec de la sauvegarde de la base de données lors de la mise à niveau vers la version 6.5.12.0 pour MySQL. {#issue}

Lorsque l’utilisateur effectue une mise à niveau vers Experience Manager 6.5.12.0 et clique sur « Mettre à niveau MySQL », le gestionnaire de configuration ne parvient pas à sauvegarder la base de données Experience Manager Forms précédente, le message d’erreur suivant apparaît :

`Failed to backup the previous Adobe Experience Manager Forms Database`


## Application {#applies-to}

* Experience Manager 6.5 Forms

## Solution {#solution}

Pour résoudre ce problème, augmentez la taille max_packet_size de la base de données sur 100 Mo ou, comme l’exige le fichier my.ini situé à l’emplacement {AEM_HOME}/mysql.
