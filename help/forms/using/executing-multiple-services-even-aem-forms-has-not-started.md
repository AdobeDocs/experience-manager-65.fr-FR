---
title: L’exécution de plusieurs services malgré AEM Forms n’a pas commencé.
description: Même si AEM Forms n’a pas entièrement démarré, il traite plusieurs services.
source-git-commit: 6b24067c1808475044a612f21d5d4d2793c13e17
workflow-type: tm+mt
source-wordcount: '97'
ht-degree: 4%

---

# L’exécution de plusieurs services malgré AEM Forms n’a pas entièrement démarré{#steps-to-resolve-error-after-installing-service-pack}


## Problème {#issue}

Lorsque l’utilisateur redémarre AEM Forms, les processus d’appel actuels continuent, tels que le rendu des documents du PDF, etc. Le redémarrage du serveur AEM Forms n’est alors pas correct.

## Application {#applies-to}

La solution s’applique au serveur AEM Forms on JEE et à AEM Forms on OSGi Server.

## Solution {#solution}

Pour résoudre le problème, les utilisateurs ajoutent un argument . `Dcom.adobe.livecycle.dsc.deferServiceStart=true` to [fichier batch](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/deploying/command-line-start-and-stop.html#windows-platform-start-bat-script-example) au démarrage du serveur.





