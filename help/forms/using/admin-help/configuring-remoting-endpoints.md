---
title: Configurer des points de fin Remoting
seo-title: Configuring Remoting endpoints
description: Découvrez comment configurer des points de fin Remoting.
seo-description: Learn how to configure remoting endpoints.
uuid: 4d4f9274-dcae-4b9f-975a-575376c2f89c
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/managing_endpoints
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: aab9d622-d76b-4100-9ca6-e5b86f543381
exl-id: 891d7d75-555a-46c6-a8a0-d5238b48bc79
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: ht
source-wordcount: '120'
ht-degree: 100%

---

# Configurer des points de fin Remoting {#configuring-remoting-endpoints}

Un point de fin Remoting permet à une application créée avec Flex d’appeler le service qui utilise AEM forms Remoting (obsolète pour AEM forms). Un point de fin Remoting est automatiquement créé pour chaque service activé. Une destination Flex portant le même nom que le point de fin est créée, ce qui permet aux clients Flex de créer des objets distants pointant vers cette destination afin d’appeler des opérations sur le service adéquat.

## Paramètres des points d’entrée Remoting {#remoting-endpoint-settings}

**Méthode d’authentification du client Flex :** indique le type de réponse que le serveur renvoie au client lorsque la sécurité du service appelé est activée, l’opération appelée ne prend pas en charge les appels anonymes et le client parvient à se connecter sans informations d’identification ou avec des informations d’identification non valides.
