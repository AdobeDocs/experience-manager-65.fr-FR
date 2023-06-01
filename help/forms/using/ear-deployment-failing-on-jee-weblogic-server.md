---
title: Échec du déploiement des fichiers EAR sur JEE WebLogic Server
seo-title: EAR Deployment failing on JEE Weblogic Server
description: Procédure de résolution de l’échec du déploiement des fichiers EAR sur JEE WebLogic Server
seo-description: Steps to resolve EAR Deployment failing on JEE Weblogic Server
source-git-commit: 45bb54a2666c2c196a8fb52795a7f428aa751e4d
workflow-type: tm+mt
source-wordcount: '103'
ht-degree: 10%

---


# Échec du déploiement des fichiers EAR sur JEE WebLogic Server {#ear-deployment-failing-on-jee-weblogic-server}

## Problème {#issue}

Lorsqu’un utilisateur tente de déployer la variable `adobe-livecycle-weblogic.ear`, la variable `Null Pointer` exception est rencontrée .

## Application {#applies-to}

Cette solution s’applique aux éléments suivants :

* AEM Forms sur le serveur WebLogic JEE version 12.2.1.x.

## Solution {#solution}

Pour résoudre ce problème, procédez comme suit :

1. Accédez au `<domain_home>\bin` répertoire du serveur WebLogic JEE installé.

1. Modifiez la variable `setDomainEnv.cmd` ou `setDomainEnv.sh` en tant que `applicable`.

1. Recherchez la dernière occurrence de `JAVA_OPTS` et ajouter `-DANTLR_USE_DIRECT_CLASS_LOADING=true` à lui. Par exemple, la chaîne mise à jour s’affiche comme suit :

       set `JAVA_OPTIONS=%JAVA_OPTIONS% -DANTLR_USE_DIRECT_CLASS_LOADING=true`
   
1. Enregistrez les modifications.


