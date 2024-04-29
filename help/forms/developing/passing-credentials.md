---
title: Transmettre des informations d’identification à l’aide des en-têtes WS-security
description: Découvrez comment transmettre des informations d’identification à l’aide des en-têtes WS-security.
exl-id: 519d57ad-81ab-4caf-ae25-4390ae2eee13
solution: Experience Manager, Experience Manager Forms
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: ht
source-wordcount: '215'
ht-degree: 100%

---

# Transmettre des informations d’identification à l’aide des en-têtes WS-Security {#using-execute-script-service-aem-forms-jee-workbench}

Lors de l’appel d’un service AEM Forms on JEE à l’aide de services web, vous pouvez utiliser des en-têtes WS-Security pour transmettre des informations d’authentification du client requises par AEM Forms on JEE. WS-Security définit les extensions SOAP pour implémenter l’authentification du client, la confidentialité et l’intégrité des messages. Par conséquent, vous pouvez appeler les services AEM Forms on JEE lorsqu’AEM Forms on JEE est déployé en tant que serveur autonome ou dans un environnement de cluster.

La manière dont vous transmettez les en-têtes WS-Security à AEM Forms on JEE dépend de l’utilisation de classes Java générées par Axes ou d’un assemblage client .NET qui consomme la pile SOAP native d’un service.

>[!NOTE]
>
>À titre d’exemple d’appel d’un service à l’aide d’en-têtes WS-Security, cette rubrique chiffre un document PDF avec un mot de passe en appelant le service Encryption.

Ce document couvre les sujets suivants :

* Transmettre l’authentification du client à l’aide des classes Java générées par Axes

* Générer des fichiers de bibliothèque Axes requis pour appeler le service Encryption

* Appeler le service Encryption à l’aide d’un en-tête WS-Security

* Transmettre l’authentification du client à l’aide d’un assemblage client .NET

* Appeler le service Encryption à l’aide d’un en-tête WS-Security


## Conditions requises {#requirements}

Pour tirer le meilleur parti de ce document, vous devez maîtriser le logiciel AEM Forms on JEE.

>[!MORELIKETHIS]
>
>* [Transmettre des informations d’identification à l’aide des en-têtes WS-Security](assets/passing-credentials-using-ws-security-headers.pdf)
