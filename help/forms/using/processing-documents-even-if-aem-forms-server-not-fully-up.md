---
title: Le serveur AEM Forms commence à traiter les documents avant même que tous les services ne soient opérationnels et en cours d’exécution.
description: Le serveur AEM Forms commence à traiter les documents avant même que tous les services ne soient opérationnels et en cours d’exécution sur le serveur JEE et le serveur OSGi.
exl-id: 1a1bc1cb-e0ce-49a0-9b05-ae59f900cfb2
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
source-wordcount: '129'
ht-degree: 100%
---
# Le serveur AEM Forms commence à traiter les documents avant même que tous les services ne soient opérationnels et en cours d’exécution.{#aem-forms-server-start-processing-documents-even-if-it-is-not-fully-up}

## Problème {#issue}

<!--When user restarts AEM Forms server, the current calling processes or services still continue such as rendering PDF documents and more. It causes the restart of the AEM Forms server to not startup correctly.-->

Avant que le serveur AEM Forms ne soit pleinement opérationnel et que toutes les applications ne soient opérationnelles et en cours d’exécution, le serveur AEM Forms commence à traiter les documents.


## Application {#applies-to}

La solution s’applique à AEM Forms sur le serveur JEE et à AEM Forms sur le serveur OSGi.

## Solution {#solution}

Pour résoudre le problème, ajoutez un argument `Dcom.adobe.livecycle.dsc.deferServiceStart=true` au [fichier de commandes](https://experienceleague.adobe.com/fr/docs/experience-manager-65/content/implementing/deploying/deploying/command-line-start-and-stop#windows-platform-start-bat-script-example) au démarrage du serveur.
