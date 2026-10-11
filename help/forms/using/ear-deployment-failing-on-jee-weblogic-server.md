---
title: Échec du déploiement des fichiers EAR sur JEE WebLogic Server
seo-title: EAR Deployment failing on JEE Weblogic Server
description: Procédure de résolution de l’échec du déploiement des fichiers EAR sur JEE WebLogic Server
exl-id: 109d9182-5e3f-477e-9417-abc83d5ea3bc
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e14eb250-3c22-4a07-9061-a78112b2b826
    internal-label: Experience Manager 6.5
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '98'
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
