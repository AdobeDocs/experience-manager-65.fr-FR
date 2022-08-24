---
title: Purge des données de processus
seo-title: Purging process data
description: Les données générées lors de l’appel d’un processus de longue durée peuvent occuper un espace considérable, réduisant les performances d’AEM forms et monopolisant un espace disque superflu. Découvrez comment vous pouvez purger des données de processus.
seo-description: Process data that is generated when a long-lived process is invoked can become too large, resulting in lower AEM forms performance and the use of unnecessary disk space. See how you can purge process data.
uuid: 2f04452c-71c6-452c-88c2-7560d35e7dec
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_the_aem_forms_database
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 3157bb92-4b07-40f2-be4c-8f5807f9a380
exl-id: 0da59dbe-f050-4ee5-b74c-4380b3543b97
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '194'
ht-degree: 100%

---

# Purge des données de processus {#purging-process-data}

Les données générées lors de l’appel d’un processus de longue durée peuvent occuper un espace considérable, réduisant les performances d’AEM forms et monopolisant un espace disque superflu. Il est recommandé de purger ces données de processus lorsque des enregistrements ne sont plus nécessaires. AEM forms fournit plusieurs outils pour purger ces données :

* Vous pouvez utiliser Administration Console pour effectuer une purge individuelle des enregistrements obsolètes liés à des processus de longue durée ou planifier des purges automatiques régulières (voir [Purge d’enregistrements de la base de données de Job Manager](/help/forms/using/admin-help/purge-records-job-manager-database.md#purge-records-from-the-job-manager-database)).
* Vous pouvez utiliser l’API Java AEM forms et l’API du service Web pour purger automatiquement les données liées à des processus de longue durée (Consultez la section « Purge des données de processus » dans [Programmation avec AEM Forms](https://www.adobe.com/go/learn_aemforms_programming_63_fr).)
* Utilisez l’outil approprié pour purger les processus basés sur le nom du processus et d’autres paramètres. Pour plus de détails, consultez le fichier « readme » de l’outil de purge de processus, situé dans *[racine aem_forms]*\sdk\misc\Foundation\ProcessPurgeTool\ReadMe.txt.
