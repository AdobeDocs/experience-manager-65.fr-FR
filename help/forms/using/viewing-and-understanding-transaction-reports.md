---
title: Affichage et compréhension des rapports de transaction
seo-title: Affichage et compréhension des rapports de transaction
description: Utilisez les rapports de transaction pour prendre une décision éclairée sur l'utilisation du produit et rééquilibrer les investissements dans le matériel et les logiciels.
seo-description: Utilisez les rapports de transaction pour prendre une décision éclairée sur l'utilisation du produit et rééquilibrer les investissements dans le matériel et les logiciels.
uuid: 56d9f01d-4778-47c9-bbb2-6650a73a3f59
topic-tags: forms-manager
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: c04c488b-73f3-49ba-9e89-f97497965757
docset: aem65
translation-type: tm+mt
source-git-commit: 317fadfe48724270e59644d2ed9a90fbee95cf9f

---


# Affichage et compréhension des rapports de transaction{#viewing-and-understanding-transaction-reports}

Les rapports de transaction vous permettent de capturer et de suivre le nombre de formulaires envoyés, de  traités et de  générés. L&#39;objectif du suivi de ces transactions est de prendre une décision éclairée sur l&#39;utilisation des produits et de rééquilibrer les investissements dans le matériel et les logiciels. Pour plus d’informations, voir Présentation [des rapports de transactions](../../forms/using/transaction-reports-overview.md)AEM Forms.

## Configuration des rapports de transaction {#setting-up-transaction-reports}

La fonctionnalité de rapports de transaction est disponible dans le cadre du module complémentaire AEM Forms. Pour plus d’informations sur l’installation du module complémentaire sur toutes les instances d’auteur et de publication, voir [Installation et configuration d’AEM Forms](/help/forms/using/installing-configuring-aem-forms-osgi.md). Une fois le module complémentaire AEM Forms installé, procédez comme suit :

* Activer la réplication inverse sur toutes les instances de publication
* Activer les rapports de transaction
* Fournir des droits  un rapport de transaction
* (Facultatif) Configuration de la période de vidage des transactions et des boîtes d’envoi [](/help/forms/using/installing-configuring-aem-forms-osgi.md)

>[!NOTE]
>
>* Les rapports de transaction AEM Forms ne prennent pas en charge les topologies qui contiennent uniquement des instances de publication.
>* Avant d’utiliser les  de transaction, assurez-vous que la réplication inverse est activée pour toutes les instances de publication.
>* Les données de transaction sont répliquées inversement d’une instance de publication à une instance d’auteur ou de traitement correspondante uniquement. L’auteur ou l’instance de traitement ne peut pas répliquer davantage les données vers une autre instance.
>



### Activer la réplication inverse sur toutes les instances de publication {#enable-reverse-replication-on-all-the-publish-instances}

Les rapports de transaction utilisent la réplication inverse pour consolider le nombre de transactions entre les instances de publication et les instances d’auteur. Configurez la réplication inverse sur toutes les instances de publication. Pour obtenir des instructions détaillées sur la configuration de la réplication inverse, voir [Réplication](/help/sites-deploying/replication.md).

### Activer les rapports de transaction {#enable-transaction-reports}

Les rapports de transaction sont désactivés par défaut. Vous pouvez activer les rapports à partir de la console Web AEM. pour activer les rapports de transaction dans un AEM Forms , effectuez les étapes suivantes sur toutes les instances d’auteur et de publication :

1. Connectez-vous à une instance AEM en tant qu’administrateur. Accédez à **Outils** > **Opérations** > Console **** Web.
1. Recherchez et ouvrez le service de transaction de **formulaires** .
1. Cochez la case Enregistrer les transactions. Cliquez sur **Enregistrer**.

   Répétez les étapes 1 à 3 sur toutes les instances d’auteur et de publication.

### Fournir des droits  un rapport de transaction {#provide-rights-to-view-a-transaction-report}

Seuls les membres du groupe fd-administrator peuvent des rapports de transaction. Pour permettre à un utilisateur de des rapports de transaction, faites en sorte que les utilisateurs soient membres du groupe fd-administrator. Pour plus d’informations sur la façon de faire d’un utilisateur un membre d’un groupe AEM, voir Administration [des droits d’](/help/sites-administering/user-group-ac-admin.md)utilisateur, de groupe et d’accès.

### (Facultatif) Configuration de la période de vidage des transactions et des boîtes d’envoi {#optional-configure-transaction-flush-period-and-outboxes}

Les transactions sont mises en cache en mémoire avant d’être stockées dans le référentiel. Par défaut, la période de mise en cache (période de vidage des transactions) est définie sur 60 secondes. Effectuez les étapes suivantes pour modifier la période de mise en cache par défaut :

1. Connectez-vous aux instances d’auteur en tant qu’administrateur. Accédez à **Outils** > **Opérations** > Console **** Web.
1. Recherchez et ouvrez le référentiel de transactions de **formulaires  le service  fournisseur** de.
1. Indiquez le nombre de secondes dans le champ Période **de vidage des** transactions. Cliquez sur **Enregistrer**.

La réplication inverse copie les données de transaction dans la boîte d’envoi par défaut des instances d’auteur. Vous pouvez placer les données de transaction dans une boîte d’envoi personnalisée. Effectuez les étapes suivantes pour spécifier une boîte d’envoi personnalisée :

1. Connectez-vous aux instances d’auteur en tant qu’administrateur. Accédez à **Outils** > **Opérations** > Console **** Web.
1. Recherchez et ouvrez le référentiel de transactions de **formulaires  le service  fournisseur** de.
1. Indiquez le nom de la boîte d’envoi personnalisée dans le champ **Outboxes** . Cliquez sur **Enregistrer**. Une boîte de réception portant le nom spécifié est créée sur toutes les instances d’auteur.

## Affichage du rapport de transaction {#viewing-the-transaction-report}

Vous pouvez des rapports de transaction sur des instances d’auteur ou de publication. Le rapport de transaction sur l’instance d’auteur fournit une somme agrégée de toutes les transactions qui ont lieu sur les instances d’auteur et de publication configurées. Le rapport de transaction sur l’instance de publication indique le nombre de transactions qui ont lieu uniquement sur l’instance de publication sous-jacente. Effectuez les étapes suivantes pour  le rapport :

1. Log in to the AEM Forms server at `https://[hostname]:'port'`.
1. Accédez à **Outils** > **Formulaires**>**Rapport de transaction des**.

## Présentation du rapport {#understanding-the-report}

AEM Forms affiche les rapports de transaction depuis la date configurée, comme illustré dans un rapport récapitulatif ci-dessous :

![sample-transaction-report-author](assets/sample-transaction-report-author.png)

* Utilisez les options **Réinitialiser la date à aujourd’hui** pour réinitialiser les enregistrements de transaction. Lorsque vous redéfinissez la date sur aujourd’hui, tous les enregistrements de transaction précédents sont perdus. Lorsque vous réinitialisez la date sur une instance d’auteur, la modification n’affecte pas les rapports de transaction sur les instances de publication et inversement.
* Utilisez l’option **Afficher les transactions des instances** de publication uniquement pour toutes les transactions qui se sont produites uniquement sur l’instance de publication ou la batterie de publication configurée.
* Utilisez le  de :  **traité**, **rendu** et **formulaires envoyés** à des transactionscorrespondantes. Pour connaître le type de transactions comptabilisées dans ces  de, voir API [Rapports de transactions](../../forms/using/transaction-reports-billable-apis.md)facturables.

## Journaux de de transaction  de transactions {#view-transaction-reporting-logs}

Le de transactions place toutes les informations affichées dans le rapport et d’autres informations dans les journaux. Les informations fournies dans les journaux sont utiles aux utilisateurs avancés. Par exemple, les journaux divisent les transactions en plusieurs  granulaires par rapport à trois  consolidées affichées dans le rapport. Les journaux se trouvent à l’adresse /crx-quickstart/logs/aem-forms-transaction.log.

## Related Articles {#related-articles}

* [Aperçu des rapports de transaction](../../forms/using/transaction-reports-overview.md)
* [API facturables des rapports de transaction](../../forms/using/transaction-reports-billable-apis.md)
* [Enregistrement d’une transaction pour des implémentations personnalisées](/help/forms/using/record-transaction-custom-implementation.md)

