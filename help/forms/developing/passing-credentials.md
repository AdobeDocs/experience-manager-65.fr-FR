---
title: Transmettre des informations d’identification à l’aide des en-têtes WS-security
description: Découvrez comment transmettre des informations d’identification à l’aide des en-têtes WS-security.
exl-id: 519d57ad-81ab-4caf-ae25-4390ae2eee13
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,Document Security
role: User, Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: 50158d81-1c06-57f7-8bd7-e8ff76a93f85
    internal-label: Document Security
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
source-wordcount: '228'
ht-degree: 100%
---
# Transmettre des informations d’identification à l’aide des en-têtes WS-Security {#using-execute-script-service-aem-forms-jee-workbench}

Lors de l’appel d’un service AEM Forms on JEE à l’aide de services web, vous pouvez utiliser des en-têtes WS-Security pour transmettre des informations d’authentification du client requises par AEM Forms on JEE. WS-Security définit les extensions SOAP pour mettre en œuvre l’authentification du client ou de la cliente, la confidentialité et l’intégrité des messages. Par conséquent, vous pouvez appeler les services AEM Forms on JEE lorsqu’AEM Forms on JEE est déployé en tant que serveur autonome ou dans un environnement de cluster.

La manière dont vous transmettez les en-têtes WS-Security à AEM Forms on JEE dépend de l’utilisation de classes Java générées par Axis ou d’un assemblage client .NET qui consomme la pile SOAP native d’un service.

>[!NOTE]
>
>À titre d’exemple d’appel d’un service à l’aide d’en-têtes WS-Security, cette rubrique chiffre un document PDF avec un mot de passe en appelant le service de chiffrement.

Ce document couvre les sujets suivants :

* Transmettre l’authentification du client à l’aide des classes Java générées par Axis

* Générer des fichiers de bibliothèque Axis requis pour appeler le service de chiffrement

* Appeler le service de chiffrement à l’aide d’un en-tête WS-Security

* Transmettre l’authentification du client à l’aide d’un assemblage client .NET

* Appeler le service de chiffrement à l’aide d’un en-tête WS-Security


## Conditions requises {#requirements}

Pour tirer le meilleur parti de ce document, vous devez maîtriser le logiciel AEM Forms on JEE.

>[!MORELIKETHIS]
>
>* [Transmettre des informations d’identification à l’aide des en-têtes WS-Security](assets/passing-credentials-using-ws-security-headers.pdf)
