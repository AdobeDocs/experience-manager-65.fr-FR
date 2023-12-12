---
title: L’exécution de plusieurs services malgré AEM Forms n’a pas commencé.
description: Même si AEM Forms n’a pas entièrement démarré, il traite plusieurs services.
exl-id: 4ec40412-15b1-434b-a919-2cf23f48077c
source-git-commit: faa628ac4a4631564141f68f3efc9d69a67e5c40
workflow-type: tm+mt
source-wordcount: '96'
ht-degree: 4%

---

# L’exécution de plusieurs services malgré AEM Forms n’a pas entièrement démarré{#steps-to-resolve-error-after-installing-service-pack}


## Problème {#issue}

Lorsque l’utilisateur redémarre AEM Forms, les processus d’appel actuels continuent, tels que le rendu des documents du PDF, etc. Le redémarrage du serveur AEM Forms n’est alors pas correct.

## Application {#applies-to}

La solution s’applique au serveur AEM Forms on JEE et à AEM Forms on OSGi Server.

## Solution {#solution}

Pour résoudre le problème, ajoutez un argument . `Dcom.adobe.livecycle.dsc.deferServiceStart=true` to [fichier batch](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/deploying/command-line-start-and-stop.html#windows-platform-start-bat-script-example) au démarrage du serveur.
