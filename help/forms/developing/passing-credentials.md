---
title: Comment transmettre des informations d’identification à l’aide des en-têtes de sécurité du service Web ?
description: Découvrez comment transmettre des informations d’identification à l’aide des en-têtes WS-security
source-git-commit: 9b118ef4f852e3df1e717bb27b9be272caeb0456
workflow-type: tm+mt
source-wordcount: '219'
ht-degree: 0%

---

# Transmission des informations d’identification à l’aide des en-têtes WS-Security {#using-execute-script-service-aem-forms-jee-workbench}

Lors de l’appel d’un service AEM Forms on JEE à l’aide de services web, vous pouvez utiliser des en-têtes WS-Security pour transmettre des informations d’authentification du client requises par AEM Forms on JEE. WS-Security définit les extensions SOAP pour mettre en oeuvre l’authentification du client, la confidentialité des messages et l’intégrité des messages. Par conséquent, vous pouvez appeler les services AEM Forms on JEE lorsqu’AEM Forms on JEE est déployé en tant que serveur autonome ou dans un environnement en grappe.

La manière dont vous transmettez les en-têtes WS-Security à AEM Forms on JEE dépend de l’utilisation de classes Java générées par Axes ou d’un assemblage client .NET qui consomme la pile SOAP native d’un service.

>[!NOTE]
>
>À titre d’exemple d’appel d’un service à l’aide d’en-têtes WS-Security, cette rubrique chiffre un document PDF avec un mot de passe en appelant le service Encryption.

Ce document couvre les sujets suivants :

* Transmission de l’authentification du client à l’aide des classes Java générées par Axes

* Génération des fichiers de bibliothèque Axes requis pour appeler le service Encryption

* Appel du service Encryption à l’aide d’un en-tête WS-Security

* Transmission de l&#39;authentification du client à l&#39;aide d&#39;un assemblage client .NET

* Appel du service Encryption à l’aide d’un en-tête WS-Security


## Conditions requises {#requirements}

Pour tirer le meilleur parti de ce document, vous devez maîtriser le logiciel AEM Forms on JEE.

>[!MORELIKETHIS]
>
>* [Transmission des informations d’identification à l’aide des en-têtes WS-Security](assets/passing-credentials-using-ws-security-headers.pdf)


