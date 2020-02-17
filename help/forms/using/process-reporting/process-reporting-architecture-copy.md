---
title: Fonctionnement de Process Reporting
seo-title: Fonctionnement de Process Reporting
description: Description des services qui composent la création de rapports de processus d’AEM Forms sur JEE et présentation de l’interface utilisateur de création de rapports de processus
seo-description: Description des services qui composent la création de rapports de processus d’AEM Forms sur JEE et présentation de l’interface utilisateur de création de rapports de processus
uuid: 4631b734-a679-495c-a708-2348bf22c1f7
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: process-reporting
discoiquuid: a1af9920-5d2a-462f-bdee-ccec4c047c5b
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Fonctionnement de Process Reporting {#how-process-reporting-works}

Process Reporting est le module de création de rapports d’AEM Forms sur JEE.

Process Reporting vous permet d’exécuter des rapports sur des processus et des tâches AEM Forms.

Process Reporting utilise le référentiel Process Reporting incorporé pour publier les données de Forms. Il utilise ensuite ces données pour exécuter des rapports.

Process Reporting se compose des modules suivants :

* [Service ProcessDataPublisher](/help/forms/using/process-reporting/process-reporting-architecture.md#p-processdatapublisher-service-br-p)
* [Service ProcessDataStorage](/help/forms/using/process-reporting/process-reporting-architecture.md#p-processdatastorageprovider-service-br-p)
* [Service OSGi](/help/forms/using/process-reporting/process-reporting-architecture.md#p-osgi-service-br-p)
* [servlet de données de requête](/help/forms/using/process-reporting/process-reporting-architecture.md#p-querydataservlet-service-br-p)
* [Interface utilisateur de Process Reporting](/help/forms/using/process-reporting/process-reporting-architecture.md#p-process-reporting-user-interface-br-p)

## Architecture des rapports de processus {#process-reporting-architecture-br}

![processreportingarchitecture](assets/processreportingarchitecture.png)

## Modules Process Reporting {#process-reporting-modules}

### Service ProcessDataPublisher {#processdatapublisher-service-br}

Le serveur ProcessDataPublisher s’exécute régulièrement sur la base de données AEM Forms et extrait les données qui ont changé depuis la dernière exécution du service. Il publie ensuite les données dans le service Process Data Storage.

Pour plus d’informations sur la configuration du service, voir [Configuration du service](/help/forms/using/process-reporting/install-start-process-reporting.md#p-reportconfiguration-service-p)ProcessDataPublisher.

### Service ProcessDataStorageProvider {#processdatastorageprovider-service-br}

Le service ProcessDataStorageProvider reçoit les données de processus du service ProcessDataPublisher et les enregistre dans le référentiel Process Reporting.

Pour plus d’informations sur la configuration du service, voir [Configuration du service](/help/forms/using/process-reporting/install-start-process-reporting.md#p-to-configure-the-process-reporting-repository-locations-p)ProcessDataStorageProvider.

### Service OSGi {#osgi-service-br}

Le servlet QueryDataServlet utilise ce service pour obtenir les données de création de rapports à partir du référentiel Process Reporting.

### Service QueryDataServlet {#querydataservlet-service-br}

Le service QueryDataServlet accepte les requêtes de l’interface utilisateur de Process Reporting.

Le service utilise ensuite les services OSGi pour obtenir les données de rapport appropriées, traiter les données et renvoyer les données à l’interface utilisateur.

### Interface utilisateur de Process Reporting {#process-reporting-user-interface-br}

L’interface utilisateur de Process Reporting est une interface Web basée sur un navigateur. Vous utilisez cette interface pour afficher les informations de processus et de tâche qui sont publiées à partir de la base de données AEM Forms.

### Service QueryDataServlet {#querydataservlet-service-br-1}

Le service QueryDataServlet accepte les requêtes de l’interface utilisateur de Process Reporting.

Le service utilise ensuite les services OSGi pour obtenir les données de rapport appropriées, traiter les données et renvoyer les données à l’interface utilisateur.

### Rapports personnalisés {#custom-reports-br}

Vous pouvez créer vos propres rapports personnalisés et les afficher dans l’onglet Rapports personnalisés de l’interface utilisateur Process Reporting.

Pour connaître les étapes de création d’un rapport personnalisé, voir Pour créer un rapport personnalisé dans l’article Rapports [personnalisés dans Process Reporting](/help/forms/using/process-reporting/process-reporting-custom-reports.md).

[Contacter le support technique](https://www.adobe.com/account/sign-in.supportportal.html)
