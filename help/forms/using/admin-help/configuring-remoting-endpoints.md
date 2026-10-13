---
title: Configuration des points d’entrée Remoting
description: Découvrez comment configurer des points d’entrée Remoting. Ce document explique comment permettre à une application créée avec Flex d’appeler le service à l’aide d’AEM Forms Remoting.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/managing_endpoints
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 891d7d75-555a-46c6-a8a0-d5238b48bc79
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
source-wordcount: '139'
ht-degree: 100%
---
# Configurer des points d’entrée Remoting {#configuring-remoting-endpoints}

Un point d’entrée Remoting permet à une application créée avec Flex d’appeler le service à l’aide d’AEM Forms Remoting (obsolète pour AEM Forms). Un point d’entrée Remoting est automatiquement créé pour chaque service activé. Une destination Flex possède le même nom que le point d’entrée créé, et les clientes et clients Flex peuvent créer des objets à distance qui pointent vers cette destination pour appeler des opérations dans le service approprié.

## Paramètres des points d’entrée Remoting {#remoting-endpoint-settings}

**Méthode d’authentification du client Flex :** indique le type de réponse que le serveur renvoie au client lorsque la sécurité du service appelé est activée, l’opération appelée ne prend pas en charge les appels anonymes et le client parvient à se connecter sans informations d’identification ou avec des informations d’identification non valides.
