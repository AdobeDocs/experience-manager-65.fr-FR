---
title: Fichiers journaux
description: Les événements, comme les erreurs d’exécution ou de démarrage, sont enregistrés dans les fichiers journaux du serveur d’applications, que vous pouvez ouvrir à l’aide d’un éditeur de texte.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_aem_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 23a65be4-3277-4c73-9189-a9b4d7be73cd
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: ht
source-wordcount: '115'
ht-degree: 100%

---

# Fichiers journaux {#log-files}

Les événements tels que les erreurs d’exécution ou de démarrage sont enregistrés dans les fichiers journaux du serveur d’applications. Si vous rencontrez des problèmes lors du déploiement sur le serveur d’applications, vous pouvez utiliser les fichiers journaux pour vous aider à identifier le problème. Vous pouvez ouvrir les fichiers journaux à l’aide de n’importe quel éditeur de texte.

(JBoss) Les fichiers journaux suivants se trouvent dans le répertoire `[appserver root]/server/'server'/log` :

* boot.log
* server.log.*[aaaa-mm-jj]*
* server.log

(WebLogic) Les fichiers journaux du domaine sont dans le répertoire `[appserverdomain]` et ceux du serveur se trouvent dans le répertoire `[appserverdomain]/servers/[appserver name]/logs` :

* `access.log`
* `[appserver name].log`
* `[appserver name].out.[incremental number]`

(WebSphere) Les fichiers journaux suivants se trouvent dans le répertoire `[appserver root]/profiles/default/logs/[appserver name]` :

* SystemErr.log
* SystemOut.log
* StartServer.log
