---
title: Le serveur AEM Forms commence à traiter les documents avant même que tous les services ne soient opérationnels et en cours d’exécution.
description: Le serveur AEM Forms commence à traiter les documents avant même que tous les services ne soient opérationnels et en cours d’exécution sur le serveur JEE et le serveur OSGi.
exl-id: 1a1bc1cb-e0ce-49a0-9b05-ae59f900cfb2
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: 9f59606bb58b9e90f07bd22e89f3213afb54a697
workflow-type: tm+mt
source-wordcount: '111'
ht-degree: 100%

---

# Le serveur AEM Forms commence à traiter les documents avant même que tous les services ne soient opérationnels et en cours d’exécution.{#aem-forms-server-start-processing-documents-even-if-it-is-not-fully-up}

## Problème {#issue}

<!--When user restarts AEM Forms server, the current calling processes or services still continue such as rendering PDF documents and more. It causes the restart of the AEM Forms server to not startup correctly.-->

Avant que le serveur AEM Forms ne soit pleinement opérationnel et que toutes les applications ne soient opérationnelles et en cours d’exécution, le serveur AEM Forms commence à traiter les documents.


## Application {#applies-to}

La solution s’applique au serveur AEM Forms on JEE et au serveur AEM Forms on OSGi.

## Solution {#solution}

Pour résoudre le problème, ajoutez un argument `Dcom.adobe.livecycle.dsc.deferServiceStart=true` au [fichier de commandes](https://experienceleague.adobe.com/fr/docs/experience-manager-65/content/implementing/deploying/deploying/command-line-start-and-stop#windows-platform-start-bat-script-example) au démarrage du serveur.
