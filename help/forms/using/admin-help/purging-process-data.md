---
title: Purge des données de processus
seo-title: Purge des données de processus
description: Les données générées lors de l’appel d’un processus de longue durée peuvent occuper un espace considérable, réduisant les performances d’AEM forms et monopolisant un espace disque superflu. Découvrez comment vous pouvez purger des données de processus.
seo-description: Les données générées lors de l’appel d’un processus de longue durée peuvent occuper un espace considérable, réduisant les performances d’AEM forms et monopolisant un espace disque superflu. Découvrez comment vous pouvez purger des données de processus.
uuid: 2f04452c-71c6-452c-88c2-7560d35e7dec
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_the_aem_forms_database
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 3157bb92-4b07-40f2-be4c-8f5807f9a380
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Purge des données de processus {#purging-process-data}

Les données générées lors de l’appel d’un processus de longue durée peuvent occuper un espace considérable, réduisant les performances d’AEM forms et monopolisant un espace disque superflu. Il est recommandé de purger ces données de processus lorsque des enregistrements ne sont plus nécessaires. AEM forms fournit plusieurs outils pour purger ces données :

* Vous pouvez utiliser Administration Console pour effectuer une purge individuelle des enregistrements obsolètes liés à des processus de longue durée ou planifier des purges automatiques régulières (voir [Purge d’enregistrements de la base de données de Job Manager](/help/forms/using/admin-help/purge-records-job-manager-database.md#purge-records-from-the-job-manager-database)).
* Vous pouvez utiliser l’API Java AEM forms et l’API du service Web pour purger automatiquement les données liées à des processus de longue durée (Consultez la section « Purge des données de processus » dans [Programmation avec AEM Forms](https://www.adobe.com/go/learn_aemforms_programming_63).)
* Utilisez l’outil approprié pour purger les processus basés sur le nom du processus et d’autres paramètres. For details, see the process purge tool readme file, located in *[aem_forms root]*\sdk\misc\Foundation\ProcessPurgeTool\ReadMe.txt.

