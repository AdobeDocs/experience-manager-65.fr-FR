---
title: Configuration des points d’entrée Remoting
description: Découvrez comment configurer des points d’entrée Remoting. Ce document explique comment permettre à l’application créée avec Flex d’appeler le service à l’aide d’AEM Forms Remoting.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/managing_endpoints
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 891d7d75-555a-46c6-a8a0-d5238b48bc79
solution: Experience Manager, Experience Manager Forms
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '139'
ht-degree: 100%

---

# Configurer des points d’entrée Remoting {#configuring-remoting-endpoints}

Un point d’entrée Remoting permet à une application créée avec Flex dʼappeler le service qui utilise AEM Forms Remoting (obsolète pour AEM Forms). Un point d’entrée Remoting est automatiquement créé pour chaque service activé. Une destination Flex possède le même nom que le point d’entrée créé, et les clientes et clients Flex peuvent créer des objets à distance qui pointent vers cette destination pour appeler des opérations dans le service approprié.

## Paramètres des points d’entrée Remoting {#remoting-endpoint-settings}

**Méthode d’authentification du client Flex :** indique le type de réponse que le serveur renvoie au client lorsque la sécurité du service appelé est activée, l’opération appelée ne prend pas en charge les appels anonymes et le client parvient à se connecter sans informations d’identification ou avec des informations d’identification non valides.
