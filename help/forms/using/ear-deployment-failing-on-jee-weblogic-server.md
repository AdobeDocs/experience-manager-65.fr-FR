---
title: Échec du déploiement des fichiers EAR sur JEE WebLogic Server
description: Procédure de résolution de l’échec du déploiement des fichiers EAR sur JEE WebLogic Server
exl-id: b87a9eee-ee56-4dca-b4a3-a42c91db0b4f
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
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
