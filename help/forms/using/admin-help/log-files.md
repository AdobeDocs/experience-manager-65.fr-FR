---
title: Fichiers journaux
description: Les événements, comme les erreurs d’exécution ou de démarrage, sont enregistrés dans les fichiers journaux du serveur d’applications, que vous pouvez ouvrir à l’aide d’un éditeur de texte.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_aem_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 23a65be4-3277-4c73-9189-a9b4d7be73cd
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
source-wordcount: '118'
ht-degree: 97%
---
# Fichiers journaux {#log-files}

Les événements tels que les erreurs d’exécution ou de démarrage sont enregistrés dans les fichiers journaux du serveur d’applications. Si vous rencontrez des problèmes lors du déploiement sur le serveur d’applications, vous pouvez utiliser les fichiers journaux pour vous aider à identifier le problème. Vous pouvez ouvrir les fichiers journaux à l’aide de n’importe quel éditeur de texte.

(JBoss) Les fichiers journaux suivants se trouvent dans le répertoire `[appserver root]/server/'server'/log` :

* boot.log
* server.log.*[yyyy-mm-dd]*
* server.log

(WebLogic) Les fichiers journaux du domaine sont dans le répertoire `[appserverdomain]` et ceux du serveur se trouvent dans le répertoire `[appserverdomain]/servers/[appserver name]/logs` :

* `access.log`
* `[appserver name].log`
* `[appserver name].out.[incremental number]`

(WebSphere) Les fichiers journaux suivants se trouvent dans le répertoire `[appserver root]/profiles/default/logs/[appserver name]` :

* SystemErr.log
* SystemOut.log
* StartServer.log
