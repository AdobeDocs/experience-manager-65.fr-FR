---
title: Purge des données de processus
description: Les données de processus générées lors de l’appel d’un processus de longue durée peuvent devenir trop volumineuses, ce qui entraîne des performances d’AEM forms plus faibles et une utilisation d’espace disque inutile. Découvrez comment purger les données de processus.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_the_aem_forms_database
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 0da59dbe-f050-4ee5-b74c-4380b3543b97
solution: Experience Manager, Experience Manager Forms
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '187'
ht-degree: 3%

---

# Purge des données de processus {#purging-process-data}

Les données de processus générées lors de l’appel d’un processus de longue durée peuvent devenir trop volumineuses, ce qui entraîne des performances d’AEM forms plus faibles et une utilisation d’espace disque inutile. Il est recommandé de purger les données de processus lorsque les enregistrements ne sont plus nécessaires. AEM forms offre plusieurs moyens de purger les données de processus :

* Vous pouvez utiliser Administration Console pour effectuer une purge unique des enregistrements obsolètes liés à des processus de longue durée ou pour planifier des purges automatiques régulières. (Voir [Purge des enregistrements de la base de données de Job Manager](/help/forms/using/admin-help/purge-records-job-manager-database.md#purge-records-from-the-job-manager-database).)
* Vous pouvez utiliser l’API Java d’AEM forms et l’API de service Web pour purger par programmation les données de processus liées à des processus de longue durée. (Voir &quot;Purge des données de processus&quot; dans [Programmation avec les AEM forms](https://www.adobe.com/go/learn_aemforms_programming_63_fr).)
* Utilisez l’outil de purge de processus pour purger les processus en fonction du nom du processus et d’autres paramètres. Pour plus d’informations, voir le fichier Lisez-moi de l’outil de purge de processus, dans *[racine aem_forms]*\sdk\misc\Foundation\ProcessPurgeTool\ReadMe.txt.
