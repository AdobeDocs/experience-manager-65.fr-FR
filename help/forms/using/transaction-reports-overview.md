---
title: Présentation des rapports de transaction
description: Tenez le compte de tous les formulaires envoyés, les communications interactives générées, les documents convertis dans un autre format, etc.
topic-tags: forms-manager
products: SG_EXPERIENCEMANAGER/6.5/FORMS
docset: aem65
feature: Transaction Reports
exl-id: bb812614-f4d8-4f57-bea2-8f7d31457039
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: tm+mt
source-wordcount: '476'
ht-degree: 100%

---

# Rapports de transaction pour AEM Forms sur OSGi {#transaction-reports-overview}

<!--## Introduction {#introduction}

Transaction reports in AEM Forms let you keep a count of all transactions taken place since a specified date on your AEM Forms deployment. The objective is to provide information about product usage and help business stakeholders understand their digital processing volumes. Examples of a transaction include:

* Submission of an adaptive form, an HTML5 Form, or a form set
* Rendition of a print or a web version of an interactive communication
* Conversion of a document from one file format to another

For more information on what is considered a transaction, see [Billable APIs](../../forms/using/transaction-reports-billable-apis.md).-->

L’enregistrement des transactions est désactivé par défaut. Vous pouvez [activer l’enregistrement des transactions](../../forms/using/viewing-and-understanding-transaction-reports.md#setting-up-transaction-reports) à partir de la console web d’AEM. Vous pouvez afficher les rapports de transaction sur les instances de création, de traitement ou de publication. Affichez les rapports de transaction sur les instances de création ou de traitement pour obtenir un total combiné de toutes les transactions. Affichez les rapports de transaction sur les instances de publication pour connaître le nombre de toutes les transactions qui ont lieu uniquement sur cette instance de publication à partir de laquelle le rapport est exécuté.

Ne créez pas de contenu (créez des formulaires adaptatifs, des communications interactives, des thèmes et d’autres activités de création) et traitez des documents (utilisez des workflows, des services de document et d’autres activités de traitement) sur la même instance d’AEM. Conservez l’enregistrement des transactions désactivé pour les serveurs AEM Forms utilisés pour créer du contenu. Conservez l’enregistrement des transactions activé pour les serveurs AEM Forms utilisés pour traiter les documents.

![sample-transaction-report-author-1](assets/sample-transaction-report-author-1.png)

Une transaction reste dans la mémoire tampon pendant une période spécifiée (durée de la mémoire tampon de purge + temps de réplication inverse). Par défaut, le comptage des transactions prend environ 90 secondes pour figurer dans le rapport de transaction.

Les actions telles que l’envoi d’un formulaire de PDF, l’utilisation de l’interface utilisateur de l’agent pour prévisualiser une communication interactive ou l’utilisation de méthodes d’envoi de formulaire non standard ne sont pas comptabilisées comme des transactions. AEM Forms fournit une API pour enregistrer ces transactions. Appelez l’API à partir de vos implémentations personnalisées pour enregistrer une transaction.

## Topologie prise en charge {#supported-topology}

Les rapports de transaction sont disponibles uniquement sur AEM Forms dans l’environnement OSGi. Il prend en charge les topologies de création-publication, de création-traitement-publication et de traitement uniquement. Pour plus d’informations sur les topologies, voir [Architecture et topologies de déploiement pour AEM Forms](../../forms/using/transaction-reports-overview.md).

Le nombre de transactions est répliqué par inverse des instances de publication vers les instances de création ou de traitement. Une topologie de création-publication indicative est affichée ci-dessous :

![simple-author-publish-topology](assets/simple-author-publish-topology.png)

>[!NOTE]
>
>Les rapports de transaction AEM Forms ne prennent pas en charge les topologies qui contiennent uniquement des instances de publication.

### Instructions relatives à l’utilisation des rapports de transaction {#guidelines-for-using-transaction-reports}

* Désactivez les rapports de transaction sur toutes les instances de création, car les rapports sur les instances de création incluent les transactions enregistrées lors des activités de création.
* Activez l’option **Afficher les transactions de publication uniquement** sur l’instance de création pour afficher les transactions cumulées de toutes les instances de publication. Vous pouvez également afficher des rapports de transaction sur chaque instance de publication pour les transactions réelles sur cette instance de publication uniquement.
* N’utilisez pas d’instances de création pour exécuter des workflows et traiter des documents.
* Avant d’utiliser la création de rapports de transaction, si vous disposez d’une stratégie avec les serveurs de publication, assurez-vous que la réplication inverse est activée pour toutes les instances de publication.
* Les données de transaction sont répliquées à l’inverse d’une instance de publication vers une instance de création ou de traitement correspondante. L’instance de création ou de traitement ne peut pas répliquer davantage les données vers une autre instance. Par exemple, si vous disposez d’une topologie création-traitement-publication, les données de transaction agrégées sont répliquées uniquement vers l’instance de traitement.

## Articles connexes {#related-articles}

* [Afficher et comprendre un rapport de transaction pour AEM Forms sur OSGi](../../forms/using/viewing-and-understanding-transaction-reports.md)
* [API facturables pour les rapports de transaction pour AEM Forms sur OSGi](../../forms/using/transaction-reports-billable-apis.md)
* [Enregistrer une transaction pour les implémentations personnalisées pour AEM Forms sur OSGi](/help/forms/using/record-transaction-custom-implementation.md)
