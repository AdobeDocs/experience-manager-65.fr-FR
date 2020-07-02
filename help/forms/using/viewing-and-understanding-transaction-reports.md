---
title: Affichage et compréhension des rapports de transactions
seo-title: Affichage et compréhension des rapports de transactions
description: Utilisez les rapports de transactions pour prendre une décision éclairée sur l'utilisation des produits et rééquilibrer les investissements en matériel et en logiciels.
seo-description: Utilisez les rapports de transactions pour prendre une décision éclairée sur l'utilisation des produits et rééquilibrer les investissements en matériel et en logiciels.
uuid: 56d9f01d-4778-47c9-bbb2-6650a73a3f59
topic-tags: forms-manager
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: c04c488b-73f3-49ba-9e89-f97497965757
docset: aem65
translation-type: tm+mt
source-git-commit: 4ee3b99a3f0a5d37441eee76c3ec747afcf2e32e
workflow-type: tm+mt
source-wordcount: '857'
ht-degree: 0%

---


# Affichage et compréhension des rapports de transactions{#viewing-and-understanding-transaction-reports}

Les rapports de transactions vous permettent de capturer et de suivre le nombre de formulaires envoyés, de documents traités et de documents rendus. L&#39;objectif du suivi de ces transactions est de prendre une décision éclairée sur l&#39;utilisation des produits et de rééquilibrer les investissements en matériel et en logiciels. Pour plus d&#39;informations, consultez Présentation [des rapports sur les transactions](../../forms/using/transaction-reports-overview.md)AEM Forms.

## Configuration des rapports de transactions  {#setting-up-transaction-reports}

La fonctionnalité de rapports de transactions est disponible dans le module complémentaire AEM Forms. Pour plus d’informations sur l’installation du module complémentaire sur toutes les instances d’auteur et de publication, voir [Installation et configuration d’AEM Forms](/help/forms/using/installing-configuring-aem-forms-osgi.md). Une fois le module complémentaire AEM Forms installé, procédez comme suit :

* Activation de la réplication inverse sur toutes les instances de publication
* Activer les rapports de transaction
* Attribuer des droits à la vue d&#39;un rapport de transaction
* (Facultatif) Configuration de la période de vidage des transactions et des boîtes d&#39;envoi [](/help/forms/using/installing-configuring-aem-forms-osgi.md)

>[!NOTE]
>
>* Les rapports de transactions AEM Forms ne prennent pas en charge les topologies qui contiennent uniquement des instances de publication.
>* Avant d’utiliser le rapports de transaction, assurez-vous que la réplication inverse est activée pour toutes les instances de publication.
>* Les données de transaction sont répliquées de manière inversée d’une instance de publication à une instance d’auteur ou de traitement correspondante uniquement. L’auteur ou l’instance de traitement ne peut pas répliquer davantage les données vers une autre instance.

>



### Activation de la réplication inverse sur toutes les instances de publication {#enable-reverse-replication-on-all-the-publish-instances}

Les rapports de transactions utilisent la réplication inverse pour consolider le nombre de transactions entre les instances de publication et les instances d’auteur. Configurez la réplication inverse sur toutes les instances de publication. Pour obtenir des instructions détaillées sur la configuration de la réplication inverse, voir [réplication](/help/sites-deploying/replication.md).

### Activer les rapports de transaction {#enable-transaction-reports}

Les rapports de transactions sont désactivés par défaut. Vous pouvez activer les rapports à partir de la console Web AEM. pour activer les rapports de transactions dans un environnement AEM Forms, effectuez les étapes suivantes sur toutes les instances d’auteur et de publication :

1. Connectez-vous à une instance AEM en tant qu’administrateur. Accédez à **Outils** > **Opérations** > Console **** Web.
1. Recherchez et ouvrez le service de Rapports **de transactions de** formulaires.
1. Cochez la case Enregistrer les transactions. Cliquez sur **Enregistrer**.

   Répétez les étapes 1 à 3 sur toutes les instances d’auteur et de publication.

### Attribuer des droits à la vue d&#39;un rapport de transaction {#provide-rights-to-view-a-transaction-report}

Seuls les membres du groupe fd-administrator peuvent vue des rapports de transactions. Pour permettre à un utilisateur de vue des rapports de transactions, faites en sorte que les utilisateurs soient membres du groupe fd-administrator. Pour plus d’informations sur la façon de faire d’un utilisateur un membre d’un groupe AEM, voir Administration [des droits d’accès, d’](/help/sites-administering/user-group-ac-admin.md)utilisateur et de groupe.

### (Facultatif) Configuration de la période de vidage des transactions et des boîtes d&#39;envoi {#optional-configure-transaction-flush-period-and-outboxes}

Les transactions sont mises en cache en mémoire avant d’être stockées dans le référentiel. Par défaut, la période de mise en cache (période de vidage des transactions) est définie sur 60 secondes. Effectuez les étapes suivantes pour modifier la période de mise en cache par défaut :

1. Connectez-vous aux instances d’auteur en tant qu’administrateur. Accédez à **Outils** > **Opérations** > Console **** Web.
1. Recherchez et ouvrez le service Fournisseur **d’Enregistrement de référentiel de transactions de** formulaires.
1. Indiquez le nombre de secondes dans le champ Période **de vidage des** mouvements. Cliquez sur **Enregistrer**.

La réplication inverse copie les données de transaction dans la boîte d&#39;envoi par défaut des instances d&#39;auteur. Vous pouvez placer les données de transaction dans une boîte d’envoi personnalisée. Effectuez les étapes suivantes pour spécifier une boîte d’envoi personnalisée :

1. Connectez-vous aux instances d’auteur en tant qu’administrateur. Accédez à **Outils** > **Opérations** > Console **** Web.
1. Recherchez et ouvrez le service Fournisseur **d’Enregistrement de référentiel de transactions de** formulaires.
1. Spécifiez le nom de la boîte d&#39;envoi personnalisée dans le champ **Boîtes** d&#39;envoi. Cliquez sur **Enregistrer**. Une boîte d’envoi portant le nom spécifié est créée sur toutes les instances d’auteur.

## Affichage de l&#39;état des transactions {#viewing-the-transaction-report}

Vous pouvez vue des rapports de transactions sur les instances d’auteur ou de publication. Le rapport de transaction sur l’instance d’auteur fournit une somme agrégée de toutes les transactions qui ont lieu sur les instances d’auteur et de publication configurées. Le rapport de transaction sur l’instance de publication fournit un décompte des transactions qui ont lieu uniquement sur l’instance de publication sous-jacente. Effectuez les étapes suivantes pour vue du rapport :

1. Log in to the AEM Forms server at `https://[hostname]:'port'`.
1. Accédez à **Outils** > **Formulaires**>**Rapport** de transactions de Vue.

## Présentation du rapport {#understanding-the-report}

Les AEM Forms affichent les rapports de transactions depuis la date configurée, comme le montre un rapport récapitulatif ci-dessous :

![exemple-transaction-rapport-auteur](assets/sample-transaction-report-author.png)

* Utilisez les options **Réinitialiser la date à aujourd&#39;hui** pour réinitialiser les enregistrements de transaction. Lorsque vous réinitialisez la date à aujourd’hui, tous les enregistrements de transaction précédents sont perdus. Lorsque vous réinitialisez la date sur une instance d’auteur, la modification n’affecte pas les rapports de transaction sur les instances de publication et à l’inverse.
* Utilisez l’option **Afficher les transactions des instances** Publier uniquement pour vue toutes les transactions qui se sont produites uniquement sur l’instance de publication ou la batterie de publication configurée.
* Utilisez les catégories : **Document traité**, **Documents rendus** et **formulaires envoyés** à la vue des transactions correspondantes. Pour connaître le type de transactions comptabilisées dans ces catégories, voir API [de rapports de transactions](../../forms/using/transaction-reports-billable-apis.md)facturables.

## Journaux des rapports de transactions de Vue {#view-transaction-reporting-logs}

Le rapports des transactions place toutes les informations affichées dans le rapport et d’autres informations dans les journaux. Les informations fournies dans les journaux sont utiles aux utilisateurs avancés. Par exemple, les journaux divisent les transactions en plusieurs catégories granulaires par rapport à trois catégories consolidées affichées dans l&#39;état. Les journaux sont disponibles dans le `error.log` fichier situé dans le `/crx-repository/logs/` répertoire. Les journaux sont disponibles même si vous n’activez pas les rapports de transaction à partir de la console Web AEM.

## Related Articles {#related-articles}

* [Présentation des rapports sur les transactions](../../forms/using/transaction-reports-overview.md)
* [API facturables des rapports de transaction](../../forms/using/transaction-reports-billable-apis.md)
* [Enregistrer une transaction pour les implémentations personnalisées](/help/forms/using/record-transaction-custom-implementation.md)

