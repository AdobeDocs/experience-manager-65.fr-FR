---
title: Fonctionnement des rapports de traitement
seo-title: Fonctionnement des rapports de traitement
description: Description des services qui constituent les rapports de processus d’AEM Forms on JEE et présentation de l’interface utilisateur des rapports de processus
seo-description: Description des services qui constituent les rapports de processus d’AEM Forms on JEE et présentation de l’interface utilisateur des rapports de processus
uuid: 37e31985-088a-4ef6-ba57-10a01597a873
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: process-reporting
discoiquuid: a6ff50df-273d-48f7-b0c6-0e69e900b97f
docset: aem65
exl-id: 66dfac36-5b7e-40be-9921-efa9f2a9521c
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '385'
ht-degree: 1%

---

# Fonctionnement des rapports de traitement{#how-process-reporting-works}

Process Reporting est le module de création de rapports d’AEM Forms on JEE.

Les rapports de processus vous permettent d’exécuter des rapports sur les processus et les tâches AEM Forms.

La création de rapports de processus utilise le référentiel de création de rapports de processus incorporé pour publier les données Forms. Il utilise ensuite ces données pour exécuter des rapports.

Les rapports de processus se composent des modules suivants :

* [Service ProcessDataPublisher](#processdatapublisher-service-br-p)
* [Service ProcessDataStorage](#processdatastorageprovider-service-br-p)
* [Service OSGi](#osgi-service-br-p)
* [Servlet Query Data](#querydataservlet-service-br-p)
* [Interface utilisateur des rapports de processus](#process-reporting-user-interface-br-p)

## Architecture des rapports de processus {#process-reporting-architecture-br}

![processreportingarchitarchitecture](assets/processreportingarchitecture.png)

## Modules de reporting de processus {#process-reporting-modules}

### Service ProcessDataPublisher {#processdatapublisher-service-br}

Le serveur ProcessDataPublisher s’exécute régulièrement sur la base de données AEM Forms et extrait les données qui ont changé depuis la dernière exécution du service. Il publie ensuite les données dans le service Process Data Storage.

Pour plus d’informations sur la configuration du service, voir [Configuration du service ProcessDataPublisher](/help/forms/using/process-reporting/install-start-process-reporting.md#p-reportconfiguration-service-p).

### Service ProcessDataStorageProvider {#processdatastorageprovider-service-br}

Le service ProcessDataStorageProvider reçoit les données de processus du service ProcessDataPublisher et enregistre les données dans le référentiel Process Reporting.

Pour plus d’informations sur la configuration du service, voir [Configuration du service ProcessDataStorageProvider](/help/forms/using/process-reporting/install-start-process-reporting.md#p-to-configure-the-process-reporting-repository-locations-p).

### Service OSGi {#osgi-service-br}

QueryDataServlet utilise ce service pour obtenir les données de rapport du référentiel Process Reporting.

### Service QueryDataServlet {#querydataservlet-service-br}

Le service QueryDataServlet accepte les requêtes de l’interface utilisateur Process Reporting.

Le service utilise ensuite les services OSGi pour obtenir les données de rapport appropriées, traite les données et renvoie les données à l’interface utilisateur.

### Interface utilisateur des rapports de processus {#process-reporting-user-interface-br}

L’interface utilisateur Process Reporting est une interface Web basée sur un navigateur. Vous utilisez cette interface pour afficher les informations sur les processus et les tâches publiées à partir de la base de données AEM Forms.

Pour une présentation de l’interface utilisateur Process Reporting, voir [Interface utilisateur Process Reporting](/help/forms/using/process-reporting/introduction-process-reporting.md).

### Service QueryDataServlet {#querydataservlet-service-br-1}

Le service QueryDataServlet accepte les requêtes de l’interface utilisateur Process Reporting.

Le service utilise ensuite les services OSGi pour obtenir les données de rapport appropriées, traite les données et renvoie les données à l’interface utilisateur.

### Rapports personnalisés {#custom-reports-br}

Vous pouvez créer vos propres rapports personnalisés et les afficher dans l’onglet Rapports personnalisés de l’interface utilisateur Process Reporting.

Pour connaître les étapes de création d’un rapport personnalisé, voir Création d’un rapport personnalisé dans l’article [Rapports personnalisés dans les rapports de processus](/help/forms/using/process-reporting/process-reporting-custom-reports.md).
