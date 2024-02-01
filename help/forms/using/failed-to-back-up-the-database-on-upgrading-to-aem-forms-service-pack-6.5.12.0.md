---
title: Échec de la sauvegarde de la base de données lors de la mise à niveau vers la version 6.5.12.0 pour MySQL.
description: Lorsqu’un utilisateur effectue une mise à niveau vers Experience Manager 6.5.12.0 et clique sur "Mettre à niveau MySQL", le gestionnaire de configuration ne parvient pas à sauvegarder la base de données Experience Manager Forms précédente.
source-git-commit: bf974331157e21b28c0daa5b878ac927ce5a2304
workflow-type: tm+mt
source-wordcount: '106'
ht-degree: 6%

---

# Échec de la sauvegarde de la base de données lors de la mise à niveau vers la version 6.5.12.0 pour MySQL (#issue)

Lorsqu’un utilisateur effectue une mise à niveau vers Experience Manager 6.5.12.0 et clique sur &quot;Mettre à niveau MySQL&quot;, le gestionnaire de configuration ne parvient pas à sauvegarder la base de données Experience Manager Forms précédente. L’erreur s’affiche :

`Failed to backup the previous Adobe Experience Manager Forms Database`


## Application {#applies-to}

* Formulaires avec Experience Manager 6.5

## Solution {#solution}

Pour résoudre ce problème, augmentez la taille max_packet_size de la base de données à 100 M ou selon les besoins dans le fichier my.ini situé à l’adresse {AEM_HOME}/mysql.
