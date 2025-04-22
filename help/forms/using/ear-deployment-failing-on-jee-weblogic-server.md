---
title: Échec du déploiement des fichiers EAR sur JEE WebLogic Server
seo-title: EAR Deployment failing on JEE Weblogic Server
description: Procédure de résolution de l’échec du déploiement des fichiers EAR sur JEE WebLogic Server
source-git-commit: 05712cfcef1d9c37b7cd015133abaf6df0e351d2
workflow-type: tm+mt
source-wordcount: '97'
ht-degree: 100%

---


# Échec du déploiement des fichiers EAR sur JEE WebLogic Server {#ear-deployment-failing-on-jee-weblogic-server}

## Problème {#issue}

Lorsqu’un utilisateur ou une utilisatrice tente de déployer `adobe-livecycle-weblogic.ear`, l’exception `Null Pointer` est rencontrée.

## Application {#applies-to}

Cette solution s’applique aux éléments suivants :

* AEM Forms sur la version 12.2.1.x de JEE WebLogic Server.

## Solution {#solution}

Pour résoudre ce problème, procédez comme suit :

1. Accédez au répertoire `<domain_home>\bin` du JEE WebLogic Server installé.

1. Modifiez le fichier `setDomainEnv.cmd` ou `setDomainEnv.sh` comme `applicable`.

1. Recherchez la dernière occurrence de `JAVA_OPTS` et ajoutez-y `-DANTLR_USE_DIRECT_CLASS_LOADING=true`. Par exemple, la chaîne mise à jour s’affiche comme suit :

       set `JAVA_OPTIONS=%JAVA_OPTIONS% -DANTLR_USE_DIRECT_CLASS_LOADING=true`
   
1. Enregistrez les modifications.
