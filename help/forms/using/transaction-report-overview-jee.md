---
title: Présentation des rapports de transaction pour AEM Forms on JEE
description: Conservez un décompte de tous les formulaires envoyés, rendus, documents convertis dans un format à un autre, etc.
feature: Transaction Reports
exl-id: 77e95631-6b0d-406e-a1b8-78f8d9cceb63
role: Admin, User, Developer
solution: "Experience Manager, Experience Manager Forms"
source-git-commit: 9f59606bb58b9e90f07bd22e89f3213afb54a697
workflow-type: tm+mt
source-wordcount: '529'
ht-degree: 2%

---

# Activation et affichage des rapports de transaction pour AEM Forms on JEE {#transaction-reports-overview}

<!--Transaction reports in AEM Forms on JEE let you keep a count of all transactions taken place on your AEM Forms deployment. The objective is to provide information about product usage and helps business stakeholders understand their digital processing volumes. Examples of a transaction include:

* Submission of a document
* Rendition of a document
* Conversion of a document from one file format to another 

For more information on what is considered a transaction, see [Billable APIs](../../forms/using/transaction-reports-billable-apis-jee.md). Transaction log helps you to gain information about the number of documents submitted, rendered, and converted.-->

## Activation des rapports de transaction {#enable-transaction-reporting}

Par défaut, l’enregistrement de transaction est désactivé. Pour activer le reporting des transactions, procédez comme suit :

1. Accédez au `/adminui` sur votre instance AEM Forms on JEE, par exemple : `http://10.14.18.10:8080/adminui`.
1. Connexion en tant que **Administrateur**.
1. Accédez à **Paramètres** > **Paramètres de Core System** > **Configurations**.
1. Cochez la case pour **Activation des rapports de transaction** et **Enregistrer** les paramètres.

   ![sample-transaction-report-jee](assets/enable-transaction-jee.png)

1. Redémarrez le serveur.
1. Outre les modifications apportées au serveur, vous devez mettre à jour le `adobe-livecycle-client.jar` dans votre projet, si vous utilisez le même.

<!--
* You can [enable transaction recording](../../forms/using/viewing-and-understanding-transaction-reports.md#setting-up-transaction-reports) from AEM Web Console. view transaction reports on author, processing, or publish instances. View transaction reports on author or processing instances for an aggregated sum of all transactions. View transaction reports on the publish instances for a count of all transactions that take place only on that publish instance from where the report is run.
-->

<!--Do not author content (Create adaptive forms, interactive communication, themes, and other authoring activities) and process documents (Use workflows, document services, and other processing activities) on the same AEM instance. Keep the transaction recording disabled for AEM Forms servers used to author content. Keep the transaction recording enabled for AEM Forms servers used to process documents.-->

## Affichage du rapport de transaction {#view-transaction-report}

Lorsque vous activez la création de rapports de transaction, les informations sur les comptes de transaction sont accessibles via la variable [rapport des transactions via le tableau de bord](#transaction-report-dashboard) et une [rapport de transaction via un fichier journal](#transaction-report-logfile). Les deux sont expliquées ci-dessous :

### Rapport des transactions via un tableau de bord {#transaction-report-dashboard}

Le rapport sur les transactions, accessible par le biais d’un tableau de bord, indique le nombre total de transactions pour chaque type de transaction. Par exemple, vous obtenez des informations sur le nombre total de formulaires rendus, convertis et envoyés, comme illustré dans l’image. Pour obtenir le rapport de transaction :

1. Accédez au `/adminui` sur votre instance AEM Forms on JEE, par exemple : `http://10.13.15.08:8080/adminui`.
1. Connexion en tant que **Administrateur**.
1. Cliquez sur Health Monitor.
1. Accédez à **Reporter les transactions** , cliquez sur **Calculer le total des transactions**, vous voyez maintenant qu’un graphique circulaire représente le nombre de PDF forms (envoyés, rendus ou convertis).

![sample-transaction-report-jee](assets/transaction-piechart.png)


### Rapport de transaction via un fichier journal {#transaction-report-logfile}

Le rapport des transactions via un fichier journal fournit des informations détaillées sur chaque transaction. Pour accéder aux journaux des transactions, suivez le chemin du contexte relatif au démarrage du serveur. Les transactions sont capturées dans un fichier journal distinct. `transaction_log.log` par défaut. La variable **chemin du fichier** est relatif au contexte de démarrage du serveur. Le chemin par défaut des différents serveurs est indiqué ci-dessous :

```
For Jboss Turnkey:
"<AEM_Forms_Installation>/jboss/bin/transaction_log.log"

For IBM Websphere: 
"<IBM_WAS_Profile_path>/transaction_log.log"

For Oracle Weblogic:
"<Weblogic_Domain_path>/transaction_log.log"

For Jboss Cluster:
"<Jboss home>/transaction_log.log"
```

Exemple d&#39;enregistrement de transaction d&#39;exemple :
`[2024-02-28 06:11:27] [INFO] TransactionRecord{service='GeneratePDFService', operation='HtmlFileToPDF', internalService='GeneratePDFService', internalOperation='HtmlFileToPDF', transactionOperationType='CONVERT', transactionCount=1, elapsedTime=1906, transactionDate=Wed Feb 28 06:11:25 UTC 2024}`

#### Enregistrement de transaction {#transaction-record-structure-jee}

La structure du journal des transactions définit la manière dont chaque transaction est enregistrée au moyen de ses différents paramètres, tels que le service, l’opération, le type de transaction, etc. Chacun d&#39;eux est présenté en détail ci-dessous. La structure de l&#39;enregistrement de transaction est la suivante :

```
TransactionRecord
{
    service='...', 
    operation='...', 
    internalService='...', 
    internalOperation='...', 
    transactionOperationType='...', 
    transactionCount=..., 
    elapsedTime=..., 
    transactionDate=...
}
```

* **service**: nom du service.
* **operation**: nom de l’opération.
* **internalService**: nom de l’appel en cas d’appel interne, identique au nom du service.
* **internalOperation**: nom de l’appel dans lequel se trouve un appel interne, sinon identique au nom de l’opération.
* **transactionOperationType**: type de transaction (envoi, rendu, conversion).
* **transactionCount**: Nombre total de transactions.
* **elapsedTime**: temps entre le lancement de l’appel et la réponse reçue.
* **transactionDate**: horodatage indiquant le moment où le service a été appelé.

**Exemple de journal des transactions**:

```
[2024-02-14 14:23:25] [INFO] TransactionRecord
{
    service='BarcodedFormsService', 
    operation='decode', 
    internalService='BarcodedFormsService', 
    internalOperation='decode', 
    transactionOperationType='CONVERT', 
    transactionCount=1, 
    elapsedTime=47405, 
    transactionDate=Wed Feb 14 14:22:37 UTC 2024
}
```

## Fréquence d’enregistrement des transactions {#transaction-recording-frequency}

<!--Transaction persistence involves updating the total transaction count for SUBMIT, CONVERT, and RENDER operations on the server periodically: -->

La fréquence d’enregistrement des transactions est déterminée par les opérations de mise à jour sur le serveur pour chaque formulaire qui est envoyé, rendu ou converti avec succès.

* Dans **tableau de bord**, le nombre de transactions est mis à jour régulièrement, la valeur par défaut est de 1 minute. Vous pouvez mettre à jour la fréquence en définissant la propriété système à l’adresse `"com.adobe.idp.dsc.transaction.recordFrequency"`. Par exemple, sur AEM Forms pour JEE sur JBoss®, ajoutez `-Dcom.adobe.idp.dsc.transaction.recordFrequency=5` in `JAVA_OPTS` pour définir la fréquence de mise à jour sur 5 minutes.

* Dans **logs de transaction**, la mise à jour de chaque transaction se produit instantanément lorsqu’un formulaire est envoyé, rendu ou converti avec succès.

<!-- A transaction remains in the buffer for a specified period (Flush Buffer time + Reverse replication time). By default, it takes approximately 90 seconds for the transaction count to reflect in the transaction report.

Actions like submitting a PDF Form, using Agent UI to preview an interactive communication, or using non-standard form submission methods are not accounted as transactions. AEM Forms provides an API to record such transactions. Call the API from your custom implementations to record a transaction.

## Supported Topology {#supported-topology}

Transaction reports are available only on AEM Forms on OSGi environment. It supports author-publish, author-processing-publish, and only processing topologies. For example, topologies, see [Architecture and deployment topologies for AEM Forms](../../forms/using/transaction-reports-overview.md).

The transaction count is reverse replicated from publish instances to author or processing instances. An indicative author-publish topology is displayed below:

![simple-author-publish-topology](assets/simple-author-publish-topology.png)

>[!NOTE]
>
>AEM Forms transaction reports does not support topologies that contain only publish instances.

### Guidelines for using transaction reports {#guidelines-for-using-transaction-reports}

* Disable transaction reports on all author instances as reports on author instances includes transactions registered during authoring activities.
* Enable the **Show transactions from publish only** option on the author instance to view cumulative transactions from all publish instances. You can also view transaction reports on each publish instance for actual transactions on that particular publish instance only.
* Do not use author instances to run workflows and process documents.
* Before using transaction reporting, if you are have a toplogy with publish servers, ensure that the reverse replication is enabled for all the publish instances.
* Transaction data is reverse-replicated from a publish instance to only corresponding author or processing instance. The author or processing instance cannot further replicate data to another instance. For example, if you have author-processing-publish topology, aggregated transaction data is replicated only to the processing instance.-->

## Articles connexes {#related-articles}

* [Liste des API facturables pour AEM Forms on JEE](../../forms/using/transaction-reports-billable-apis-jee.md)
* [Enregistrement d’une transaction pour les API de composant personnalisées pour AEM Forms on JEE](/help/forms/using/record-transaction-custom-component-jee.md)
