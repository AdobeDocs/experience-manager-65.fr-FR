---
title: Purge des données de processus
description: Les données de processus générées lors de l’appel d’un processus de longue durée peuvent devenir trop volumineuses, ce qui diminue les performances d’AEM Forms et utilise de l’espace disque inutilement. Découvrez comment purger les données de processus.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/maintaining_the_aem_forms_database
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 0da59dbe-f050-4ee5-b74c-4380b3543b97
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
source-wordcount: '207'
ht-degree: 100%
---
# Purge des données de processus {#purging-process-data}

>[!NOTE]
> 
> Vérifiez que l’utilisateur ou l’utilisatrice dispose de droits d’administration pour accéder à la console d’administration.

Les données de processus générées lors de l’appel d’un processus de longue durée peuvent devenir trop volumineuses, ce qui diminue les performances d’AEM Forms et utilise de l’espace disque inutilement. Il est recommandé de purger les données de processus lorsque vous n’avez plus besoin des enregistrements. AEM Forms fournit plusieurs moyens de purger les données de processus :

* Vous pouvez utiliser la console d’administration pour effectuer une purge unique des enregistrements obsolètes liés à des processus de longue durée ou pour planifier des purges automatiques régulières. (Voir [Purge d’enregistrements de la base de données de Job Manager](/help/forms/using/admin-help/purge-records-job-manager-database.md#purge-records-from-the-job-manager-database)).
* Vous pouvez utiliser l’API Java AEM Forms et l’API de service web pour purger par programmation les données de processus liées à des processus de longue durée. (Voir « Purge des données de processus » dans [Programmation avec AEM Forms](https://www.adobe.com/go/learn_aemforms_programming_63_fr).)
* Utilisez l’outil de purge des processus pour purger les processus en fonction du nom du processus et d’autres paramètres. Pour plus de détails, consultez le fichier « readme » de l’outil de purge de processus, situé dans *[aem_forms root]*\sdk\misc\Foundation\ProcessPurgeTool\ReadMe.txt.
