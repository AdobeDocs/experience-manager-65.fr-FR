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
exl-id: 23a65be4-3277-4c73-9189-a9b4d7be73cd
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '144'
ht-degree: 73%

---

# Fichiers journaux {#log-files}

Les événements, comme les erreurs d’exécution ou de démarrage, sont enregistrés dans les fichiers journaux du serveur d’applications. Ces fichiers peuvent vous aider à diagnostiquer les éventuels problèmes rencontrés lors du déploiement sur le serveur d’applications. Vous pouvez les ouvrir dans un éditeur de texte.

(JBoss) Les fichiers journaux suivants se trouvent dans le répertoire `[appserver root]/server/'server'/log` :

* boot.log
* server.log.*[aaaa-mm-jj]*
* server.log

(WebLogic) Les fichiers journaux de domaine se trouvent dans le répertoire `[appserverdomain]` et les fichiers journaux du serveur dans le répertoire `[appserverdomain]/servers/[appserver name]/logs` :

* `access.log`
* `[appserver name].log`
* `[appserver name].out.[incremental number]`

(WebSphere) Les fichiers journaux suivants se trouvent dans le répertoire `[appserver root]/profiles/default/logs/[appserver name]` :

* SystemErr.log
* SystemOut.log
* StartServer.log
