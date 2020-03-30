---
title: Fichiers journaux
seo-title: Fichiers journaux
description: Les événements, comme les erreurs d’exécution ou de démarrage, sont enregistrés dans les fichiers journaux du serveur d’applications, que vous pouvez ouvrir à l’aide d’un éditeur de texte.
seo-description: Les événements, comme les erreurs d’exécution ou de démarrage, sont enregistrés dans les fichiers journaux du serveur d’applications, que vous pouvez ouvrir à l’aide d’un éditeur de texte.
uuid: 6ed9fdcd-ff02-4b35-893f-09261a6a557a
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_aem_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: cf140483-470f-4bff-8870-304207508aab
translation-type: tm+mt
source-git-commit: 317fadfe48724270e59644d2ed9a90fbee95cf9f

---


# Fichiers journaux {#log-files}

Les événements, comme les erreurs d’exécution ou de démarrage, sont enregistrés dans les fichiers journaux du serveur d’applications. Ces fichiers peuvent vous aider à diagnostiquer les éventuels problèmes rencontrés lors du déploiement sur le serveur d’applications. Vous pouvez les ouvrir dans un éditeur de texte.

(JBoss) Les fichiers journaux suivants se trouvent dans le `[appserver root]/server/'server'/log` répertoire :

* boot.log
* server.log.*[aaaa-mm-jj]*
* server.log

(WebLogic) Les fichiers journaux de domaine se trouvent dans le `[appserverdomain]` répertoire et les fichiers journaux de serveur dans le `[appserverdomain]/servers/[appserver name]/logs` répertoire :

* `access.log`
* `[appserver name].log`
* `[appserver name].out.[incremental number]`

(WebSphere) Les fichiers journaux suivants se trouvent dans le `[appserver root]/profiles/default/logs/[appserver name]` répertoire :

* SystemErr.log
* SystemOut.log
* StartServer.log

