---
title: Configurer des points d’entrée Remoting
description: Découvrez comment configurer des points de fin distants. Ce document explique comment permettre à l’application créée avec Flex d’appeler le service à l’aide de AEM forms Remoting.
uuid: 4d4f9274-dcae-4b9f-975a-575376c2f89c
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/managing_endpoints
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: aab9d622-d76b-4100-9ca6-e5b86f543381
exl-id: 891d7d75-555a-46c6-a8a0-d5238b48bc79
source-git-commit: 6caf3ef4a00275f0f73be52b6a9ccba77d277f1a
workflow-type: tm+mt
source-wordcount: '139'
ht-degree: 36%

---

# Configurer des points d’entrée Remoting {#configuring-remoting-endpoints}

Un point de fin Remoting permet à une application créée avec Flex d’appeler le service en utilisant (obsolète pour les AEM forms) AEM forms Remoting. Un point de fin Remoting est automatiquement créé pour chaque service activé. Une destination Flex qui porte le même nom que le point de terminaison est créée et les clients Flex peuvent créer des objets distants qui pointent vers cette destination pour appeler des opérations sur le service approprié.

## Paramètres des points d’entrée Remoting {#remoting-endpoint-settings}

**Méthode d’authentification du client Flex :** indique le type de réponse que le serveur renvoie au client lorsque la sécurité du service appelé est activée, l’opération appelée ne prend pas en charge les appels anonymes et le client parvient à se connecter sans informations d’identification ou avec des informations d’identification non valides.
