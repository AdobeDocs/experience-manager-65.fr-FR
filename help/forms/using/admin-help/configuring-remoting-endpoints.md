---
title: Configurer des points d’entrée Remoting
description: Découvrez comment configurer des points de fin distants. Ce document explique comment permettre à l’application créée avec Flex d’appeler le service à l’aide de AEM forms Remoting.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/managing_endpoints
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 891d7d75-555a-46c6-a8a0-d5238b48bc79
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '139'
ht-degree: 36%

---

# Configurer des points d’entrée Remoting {#configuring-remoting-endpoints}

Un point de fin Remoting permet à une application créée avec Flex d’appeler le service en utilisant (obsolète pour les AEM forms) AEM forms Remoting. Un point de fin Remoting est automatiquement créé pour chaque service activé. Une destination Flex qui porte le même nom que le point de terminaison est créée et les clients Flex peuvent créer des objets distants qui pointent vers cette destination pour appeler des opérations sur le service approprié.

## Paramètres des points d’entrée Remoting {#remoting-endpoint-settings}

**Méthode d’authentification du client Flex :** indique le type de réponse que le serveur renvoie au client lorsque la sécurité du service appelé est activée, l’opération appelée ne prend pas en charge les appels anonymes et le client parvient à se connecter sans informations d’identification ou avec des informations d’identification non valides.
