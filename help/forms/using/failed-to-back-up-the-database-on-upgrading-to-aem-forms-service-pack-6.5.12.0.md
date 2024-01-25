---
title: Échec de la sauvegarde de la base de données précédente sur AEM Forms 6.5.12.0.
description: Lorsqu’un utilisateur effectue une mise à niveau vers Experience Manager 6.5.12.0 et clique sur "Mettre à niveau MySQL", le gestionnaire de configuration ne parvient pas à sauvegarder la base de données Experience Manager Forms précédente.
source-git-commit: d232bfdad7b8413eb015f6fe5dd3442cebf1001d
workflow-type: tm+mt
source-wordcount: '98'
ht-degree: 7%

---

# Problème (#issue)

Lorsqu’un utilisateur effectue une mise à niveau vers Experience Manager 6.5.12.0 et clique sur &quot;Mettre à niveau MySQL&quot;, le gestionnaire de configuration ne parvient pas à sauvegarder la base de données Experience Manager Forms précédente. L’erreur s’affiche :

`Failed to backup the previous Adobe Experience Manager Forms Database`


## Application {#applies-to}

* Formulaires avec Experience Manager 6.5

## Solution {#solution}

Pour résoudre ce problème, augmentez la taille max_packet_size de la base de données à 100 M ou selon les besoins dans le fichier my.ini situé à l’adresse {AEM_HOME}/mysql.
