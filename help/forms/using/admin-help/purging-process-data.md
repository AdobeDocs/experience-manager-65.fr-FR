---
title: Purge des données de processus
description: Les données de processus générées lors de l’appel d’un processus de longue durée peuvent devenir trop volumineuses, ce qui diminue les performances d’AEM Forms et utilise de l’espace disque inutilement. Découvrez comment purger les données de processus.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_the_aem_forms_database
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 0da59dbe-f050-4ee5-b74c-4380b3543b97
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: ht
source-wordcount: '187'
ht-degree: 100%

---

# Purge des données de processus {#purging-process-data}

Les données de processus générées lors de l’appel d’un processus de longue durée peuvent devenir trop volumineuses, ce qui diminue les performances d’AEM Forms et utilise de l’espace disque inutilement. Il est recommandé de purger les données de processus lorsque vous n’avez plus besoin des enregistrements. AEM Forms fournit plusieurs outils pour purger les données de processus :

* Vous pouvez utiliser la console d’administration pour effectuer une purge unique des enregistrements obsolètes liés à des processus de longue durée ou pour planifier des purges automatiques régulières. (Voir [Purge d’enregistrements de la base de données de Job Manager](/help/forms/using/admin-help/purge-records-job-manager-database.md#purge-records-from-the-job-manager-database)).
* Vous pouvez utiliser l’API Java AEM Forms et l’API de service web pour purger par programmation les données de processus de longue durée. (Voir « Purge des données de processus » dans [Programmation avec AEM Forms](https://www.adobe.com/go/learn_aemforms_programming_63_fr).)
* Utilisez l’outil approprié pour purger les processus basés sur le nom du processus et d’autres paramètres. Pour plus de détails, consultez le fichier « readme » de l’outil de purge de processus, situé dans *[aem_forms root]*\sdk\misc\Foundation\ProcessPurgeTool\ReadMe.txt.
