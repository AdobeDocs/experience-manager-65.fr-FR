---
title: Fonctionnement de Process Reporting
seo-title: How Process Reporting Works
description: Description des services qui constituent Process Reporting d’AEM Forms on JEE et présentation de l’interface utilisateur de Process Reporting
seo-description: Description of the services that make up the AEM Forms on JEE Process Reporting and an introduction to the Process Reporting UI
uuid: 4631b734-a679-495c-a708-2348bf22c1f7
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: process-reporting
discoiquuid: a1af9920-5d2a-462f-bdee-ccec4c047c5b
source-git-commit: 56c6cfd437ef185336e81373bd5f758205b96317
workflow-type: ht
source-wordcount: '345'
ht-degree: 100%

---


# Fonctionnement de Process Reporting {#how-process-reporting-works}

Process Reporting est le module de création de rapports d’AEM Forms on JEE.

Process Reporting vous permet d’exécuter des rapports sur les processus et les tâches AEM Forms.

Process Reporting utilise le référentiel Process Reporting incorporé pour publier les données de Forms. Il utilise ensuite ces données pour exécuter des rapports.

Process Reporting se compose des modules suivants :

* [Service ProcessDataPublisher](/help/forms/using/process-reporting/process-reporting-architecture.md#p-processdatapublisher-service-br-p)
* [Service ProcessDataStorage](/help/forms/using/process-reporting/process-reporting-architecture.md#p-processdatastorageprovider-service-br-p)
* [Service OSGi](/help/forms/using/process-reporting/process-reporting-architecture.md#p-osgi-service-br-p)
* [Service QueryDataServlet](/help/forms/using/process-reporting/process-reporting-architecture.md#p-querydataservlet-service-br-p)
* [Interface utilisateur de Process Reporting](/help/forms/using/process-reporting/process-reporting-architecture.md#p-process-reporting-user-interface-br-p)

## Architecture de Process Reporting {#process-reporting-architecture-br}

![processreportingarchitarchitecture](assets/processreportingarchitecture.png)

## Modules de Process Reporting {#process-reporting-modules}

### Service ProcessDataPublisher {#processdatapublisher-service-br}

Le serveur ProcessDataPublisher s’exécute régulièrement sur la base de données d’AEM Forms et extrait les données qui ont changé depuis la dernière exécution du service. Il publie ensuite les données dans le service Process Data Storage.

Pour plus d’informations sur la configuration du service, voir [Configuration du service ProcessDataPublisher](/help/forms/using/process-reporting/install-start-process-reporting.md#p-reportconfiguration-service-p).

### Service ProcessDataStorageProvider {#processdatastorageprovider-service-br}

Le service ProcessDataStorageProvider reçoit les données de processus du service ProcessDataPublisher et enregistre les données dans le référentiel Process Reporting.

Pour plus d’informations sur la configuration du service, voir [Configuration du service ProcessDataStorageProvider](/help/forms/using/process-reporting/install-start-process-reporting.md#p-to-configure-the-process-reporting-repository-locations-p).

### Service OSGi {#osgi-service-br}

Le service QueryDataServlet utilise ce service pour obtenir les données de rapport du référentiel Process Reporting.

### Service QueryDataServlet {#querydataservlet-service-br}

Le service QueryDataServlet accepte les requêtes de l’interface utilisateur de Process Reporting.

Le service utilise ensuite les services OSGi pour obtenir les données de rapport appropriées. Il traite les données et renvoie les données à l’interface utilisateur.

### Interface utilisateur de Process Reporting {#process-reporting-user-interface-br}

L’interface utilisateur de Process Reporting est une interface web basée sur un navigateur. Vous utilisez cette interface pour afficher les informations sur les processus et les tâches publiées à partir de la base de données d’AEM Forms.

### Service QueryDataServlet {#querydataservlet-service-br-1}

Le service QueryDataServlet accepte les requêtes de l’interface utilisateur de Process Reporting.

Le service utilise ensuite les services OSGi pour obtenir les données de rapport appropriées. Il traite les données et renvoie les données à l’interface utilisateur.

### Rapports personnalisés {#custom-reports-br}

Vous pouvez créer des rapports personnalisés et les afficher dans l’onglet Rapports personnalisés de l’interface utilisateur de Process Reporting.

Pour connaître les étapes de création d’un rapport personnalisé, voir la section Pour créer un rapport personnalisé dans l’article [Rapports personnalisés dans Process Reporting](/help/forms/using/process-reporting/process-reporting-custom-reports.md).
