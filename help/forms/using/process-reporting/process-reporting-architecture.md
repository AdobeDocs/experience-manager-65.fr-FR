---
title: Fonctionnement du Rapports de traitement
seo-title: Fonctionnement du Rapports de traitement
description: Description des services qui composent le Rapports de processus AEM Forms on JEE et présentation de l’interface utilisateur du Rapports de processus
seo-description: Description des services qui composent le Rapports de processus AEM Forms on JEE et présentation de l’interface utilisateur du Rapports de processus
uuid: 37e31985-088a-4ef6-ba57-10a01597a873
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: process-reporting
discoiquuid: a6ff50df-273d-48f7-b0c6-0e69e900b97f
docset: aem65
translation-type: tm+mt
source-git-commit: 56c6cfd437ef185336e81373bd5f758205b96317
workflow-type: tm+mt
source-wordcount: '385'
ht-degree: 1%

---


# Fonctionnement du Rapports de traitement{#how-process-reporting-works}

Le Rapports de processus est le module de rapports du AEM Forms on JEE.

Le Rapports de processus vous permet d’exécuter des rapports sur les processus et tâches AEM Forms.

Le Rapports de processus utilise le référentiel de Rapports de processus incorporé pour publier les données Forms. Il utilise ensuite ces données pour exécuter des rapports.

Le Rapports de processus se compose des modules suivants :

* [Service ProcessDataPublisher](#processdatapublisher-service-br-p)
* [Service ProcessDataStorage](#processdatastorageprovider-service-br-p)
* [Service OSGi](#osgi-service-br-p)
* [servlet requête Data](#querydataservlet-service-br-p)
* [Interface utilisateur du Rapports de processus](#process-reporting-user-interface-br-p)

## Architecture du Rapports de processus {#process-reporting-architecture-br}

![processreportingarchitecture](assets/processreportingarchitecture.png)

## Modules de Rapports de processus {#process-reporting-modules}

### Service ProcessDataPublisher {#processdatapublisher-service-br}

Le serveur ProcessDataPublisher s&#39;exécute régulièrement sur la base de données AEM Forms et extrait les données qui ont changé depuis la dernière exécution du service. Il publie ensuite les données dans le service Process Data Enregistrement.

Pour plus d’informations sur la configuration du service, voir [Configuration du service](/help/forms/using/process-reporting/install-start-process-reporting.md#p-reportconfiguration-service-p)ProcessDataPublisher.

### Service ProcessDataStorageProvider {#processdatastorageprovider-service-br}

Le service ProcessDataStorageProvider reçoit les données de processus du service ProcessDataPublisher et les enregistre dans le référentiel Process Rapports.

Pour plus d’informations sur la configuration du service, voir [Configuration du service](/help/forms/using/process-reporting/install-start-process-reporting.md#p-to-configure-the-process-reporting-repository-locations-p)ProcessDataStorageProvider.

### Service OSGi {#osgi-service-br}

QueryDataServlet utilise ce service pour obtenir les données de rapports du référentiel de Rapports de processus.

### Service QueryDataServlet {#querydataservlet-service-br}

Le service QueryDataServlet accepte les requêtes provenant de l’interface utilisateur du Rapports de processus.

Le service utilise ensuite les services OSGi pour obtenir les données de rapports appropriées, traiter les données et renvoyer les données à l’interface utilisateur.

### Interface utilisateur du Rapports de processus {#process-reporting-user-interface-br}

L’interface utilisateur du Rapports de processus est une interface Web basée sur un navigateur. Cette interface vous permet d’accéder aux informations de processus de vue et de tâche publiées à partir de la base de données AEM Forms.

Pour une présentation de l’interface utilisateur du Rapports de processus, voir Interface [utilisateur du Rapports de](/help/forms/using/process-reporting/introduction-process-reporting.md)processus.

### Service QueryDataServlet {#querydataservlet-service-br-1}

Le service QueryDataServlet accepte les requêtes provenant de l’interface utilisateur du Rapports de processus.

Le service utilise ensuite les services OSGi pour obtenir les données de rapports appropriées, traiter les données et renvoyer les données à l’interface utilisateur.

### Rapports personnalisés {#custom-reports-br}

Vous pouvez créer vos propres rapports personnalisés et les afficher dans l’onglet Rapports personnalisés de l’interface utilisateur du Rapports de processus.

Pour connaître les étapes de création d&#39;un rapport personnalisé, voir Pour créer un rapport personnalisé dans l&#39;article Rapports [personnalisés dans le Rapports](/help/forms/using/process-reporting/process-reporting-custom-reports.md)de processus.
