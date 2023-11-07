---
title: Purge des données de processus
seo-title: Purging process data
description: Les données de processus générées lors de l’appel d’un processus de longue durée peuvent devenir trop volumineuses, ce qui entraîne des performances d’AEM forms plus faibles et une utilisation d’espace disque inutile. Découvrez comment purger les données de processus.
seo-description: Process data that is generated when a long-lived process is invoked can become too large, resulting in lower AEM forms performance and the use of unnecessary disk space. See how you can purge process data.
uuid: 2f04452c-71c6-452c-88c2-7560d35e7dec
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_the_aem_forms_database
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 3157bb92-4b07-40f2-be4c-8f5807f9a380
exl-id: 0da59dbe-f050-4ee5-b74c-4380b3543b97
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '193'
ht-degree: 6%

---

# Purge des données de processus {#purging-process-data}

Les données de processus générées lors de l’appel d’un processus de longue durée peuvent devenir trop volumineuses, ce qui entraîne des performances d’AEM forms plus faibles et une utilisation d’espace disque inutile. Il est recommandé de purger les données de processus lorsque les enregistrements ne sont plus nécessaires. AEM forms offre plusieurs moyens de purger les données de processus :

* Vous pouvez utiliser Administration Console pour effectuer une purge unique des enregistrements obsolètes liés à des processus de longue durée ou pour planifier des purges automatiques régulières. (Voir [Purge des enregistrements de la base de données de Job Manager](/help/forms/using/admin-help/purge-records-job-manager-database.md#purge-records-from-the-job-manager-database).)
* Vous pouvez utiliser l’API Java d’AEM forms et l’API de service Web pour purger par programmation les données de processus liées à des processus de longue durée. (Voir &quot;Purge des données de processus&quot; dans [Programmation avec les AEM forms](https://www.adobe.com/go/learn_aemforms_programming_63_fr).)
* Utilisez l’outil de purge de processus pour purger les processus en fonction du nom du processus et d’autres paramètres. Pour plus d’informations, voir le fichier Lisez-moi de l’outil de purge de processus, dans *[racine aem_forms]*\sdk\misc\Foundation\ProcessPurgeTool\ReadMe.txt.
