---
title: Configuration des points de fin Remoting
seo-title: Configuration des points de fin Remoting
description: Découvrez comment configurer des points de fin Remoting.
seo-description: Découvrez comment configurer des points de fin Remoting.
uuid: 4d4f9274-dcae-4b9f-975a-575376c2f89c
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/managing_endpoints
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: aab9d622-d76b-4100-9ca6-e5b86f543381
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '129'
ht-degree: 67%

---


# Configuration des points de fin Remoting {#configuring-remoting-endpoints}

Un point de fin Remoting permet à une application créée avec Flex d’appeler le service qui utilise AEM forms Remoting (obsolète pour AEM forms). Un point de fin Remoting est automatiquement créé pour chaque service activé. Une destination Flex portant le même nom que le point de fin est créée, ce qui permet aux clients Flex de créer des objets distants pointant vers cette destination afin d’appeler des opérations sur le service adéquat.

## Paramètres des points de fin Remoting {#remoting-endpoint-settings}

**Méthode d’authentification du client Flex :** détermine le type de réponse que le serveur renvoie au client lorsque la sécurité du service appelé est activée, l’opération appelée ne prend pas en charge les appels anonymes et le client transmet des informations d’identification non valides ou non valides.
