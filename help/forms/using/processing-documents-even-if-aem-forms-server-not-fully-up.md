---
title: AEM Forms Server démarre le traitement des documents avant même que tous les services ne soient en cours d’exécution.
description: AEM Forms Server démarre le traitement des documents avant même que tous les services ne soient opérationnels sur le serveur JEE et le serveur OSGi.
exl-id: 1a1bc1cb-e0ce-49a0-9b05-ae59f900cfb2
solution: Experience Manager, Experience Manager Forms
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '111'
ht-degree: 3%

---

# AEM Forms Server démarre le traitement des documents avant même que tous les services ne soient opérationnels.{#aem-forms-server-start-processing-documents-even-if-it-is-not-fully-up}

## Problème {#issue}

<!--When user restarts AEM Forms server, the current calling processes or services still continue such as rendering PDF documents and more. It causes the restart of the AEM Forms server to not startup correctly.-->

Avant que le serveur AEM Forms ne soit entièrement opérationnel et que toutes les applications soient en cours d’exécution, le serveur AEM Forms commence à traiter les documents.


## Application {#applies-to}

La solution s’applique au serveur AEM Forms on JEE et à AEM Forms on OSGi Server.

## Solution {#solution}

Pour résoudre le problème, ajoutez un argument . `Dcom.adobe.livecycle.dsc.deferServiceStart=true` à la fonction [fichier batch](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/deploying/command-line-start-and-stop.html#windows-platform-start-bat-script-example) au démarrage du serveur.
