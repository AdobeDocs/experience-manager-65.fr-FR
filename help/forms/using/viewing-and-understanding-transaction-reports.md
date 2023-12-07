---
title: Afficher et comprendre les rapports de transaction
description: Utilisez les rapports de transaction pour prendre une décision éclairée sur l’utilisation du produit et rééquilibrer les investissements en matériel et en logiciels.
topic-tags: forms-manager
products: SG_EXPERIENCEMANAGER/6.5/FORMS
docset: aem65
exl-id: 3c7cbe1f-ac81-4df9-96b2-662cbc5f2075
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '861'
ht-degree: 100%

---

# Afficher et comprendre les rapports de transaction{#viewing-and-understanding-transaction-reports}

Les rapports de transaction vous permettent de capturer et de suivre le nombre de formulaires envoyés, de documents traités et de documents rendus. L’objectif derrière le suivi de ces transactions est de prendre une décision éclairée concernant l’utilisation du produit et de réévaluer les investissements en matériel et en logiciels. Pour plus d’informations, voir [Présentation des rapports sur les transactions AEM Forms](../../forms/using/transaction-reports-overview.md).

## Configurer des rapports de transaction  {#setting-up-transaction-reports}

La fonction Rapports de transaction est disponible dans le cadre du package complémentaire d’AEM Forms. Pour plus d’informations sur l’installation du package complémentaire sur toutes les instances de création et de publication, voir [Installer et configurer AEM Forms](/help/forms/using/installing-configuring-aem-forms-osgi.md). Une fois que vous avez installé le package complémentaire AEM Forms, procédez comme suit :

* Activer la réplication inverse sur toutes les instances de publication
* Activer les rapports de transactions
* Fournir des droits pour afficher un rapport de transaction
* (Facultatif) Configurer la période de purge des transactions et des boîtes d’envoi [](/help/forms/using/installing-configuring-aem-forms-osgi.md)

>[!NOTE]
>
>* Les rapports de transaction AEM Forms ne prennent pas en charge les topologies contenant uniquement des instances de publication.
>* Avant d’utiliser les rapports de transaction, assurez-vous que la réplication inverse est activée pour toutes les instances de publication.
>* Les données de transaction sont répliquées à l’inverse d’une instance de publication vers une instance de création ou de traitement correspondante. L’instance de création ou de traitement ne peut pas répliquer davantage les données vers une autre instance.
>

### Activer la réplication inverse sur toutes les instances de publication {#enable-reverse-replication-on-all-the-publish-instances}

Les rapports de transactions utilisent la réplication inverse pour consolider le nombre de transactions entre les instances de publication et les instances de création. Configurez la réplication inverse sur toutes les instances de publication. Pour obtenir des instructions détaillées sur la configuration de la réplication inverse, voir [réplication](/help/sites-deploying/replication.md).

### Activer les rapports de transactions {#enable-transaction-reports}

Les rapports de transaction sont désactivés par défaut. Vous pouvez activer les rapports à partir de la console web AEM. Pour activer les rapports de transaction dans un environnement AEM Forms, effectuez les opérations suivantes sur toutes les instances de création et de publication :

1. Connectez-vous à votre instance AEM en tant qu’administrateur. Accédez à **Outils** > **Opérations** > **Console web**.
1. Recherchez et ouvrez le service **Rapports de transactions de Forms**.
1. Cochez la case Enregistrer les transactions. Cliquez sur **Enregistrer**.

   Répétez les étapes 1 à 3 sur toutes les instances de création et de publication.

### Fournir des droits pour afficher un rapport de transaction {#provide-rights-to-view-a-transaction-report}

Seuls les membres du groupe administrateur-fd peuvent voir les rapports des transactions. Pour permettre à un utilisateur de consulter les rapports de transaction, faites de ces utilisateurs des membres du groupe fd-administrator. Pour plus d’informations sur la façon de faire d’un utilisateur un membre d’un groupe AEM, voir [Administration des utilisateurs, des groupes et des droits d’accès](/help/sites-administering/user-group-ac-admin.md).

### (Facultatif) Configurer la période de purge des transactions et des boîtes d’envoi {#optional-configure-transaction-flush-period-and-outboxes}

Les transactions sont mises en cache en mémoire avant d’être stockées dans le référentiel. Le processus est suivi pour s’assurer qu’il n’y a pas d’écritures fréquentes dans le référentiel. Par défaut, la période de mise en cache (période de purge des transactions) est définie sur 60 secondes. Vous pouvez modifier la période par défaut en fonction de votre environnement. Effectuez les opérations suivantes pour modifier la période de mise en cache par défaut :

1. Connectez-vous aux instances de création en tant qu’administrateur. Accédez à **Outils** > **Opérations** > **Console web**.
1. Recherchez et ouvrez le service **Fournisseur de stockage du référentiel de transactions Forms**.
1. Spécifiez le nombre de secondes dans le champ **Période de purge des transactions**. Cliquez sur **Enregistrer**.

La réplication inverse copie les données de transaction dans la boîte d’envoi par défaut des instances de création. Vous pouvez placer les données de transaction dans une boîte d’envoi personnalisée. Pour définir une boîte d’envoi personnalisée, procédez comme suit :

1. Connectez-vous aux instances de création en tant qu’administrateur. Accédez à **Outils** > **Opérations** > **Console web**.
1. Recherchez et ouvrez le service **Forms Transaction Repository Storage Provider**.
1. Indiquez le nom de la boîte d’envoi personnalisée le champ **Boîtes dʼenvoi**. Cliquez sur **Enregistrer**. Une boîte d’envoi du nom spécifié est créée sur toutes les instances d’auteur.

## Afficher le rapport de transaction {#viewing-the-transaction-report}

Vous pouvez afficher les rapports de transaction sur les instances d’auteur ou de publication. Le rapport de transaction sur l’instance d’auteur fournit une somme agrégée de toutes les transactions qui ont lieu sur les instances d’auteur et de publication configurées. Le rapport de transaction sur l’instance de publication fournit un décompte des transactions qui ont lieu uniquement sur l’instance de publication sous-jacente. Pour afficher le rapport, procédez comme suit :

1. Connectez-vous au serveur AEM Forms à lʼadresse `https://[hostname]:'port'`.
1. Accédez à **Outils** > **Forms** > **Afficher le rapport de transaction**.

## Comprendre le rapport {#understanding-the-report}

AEM Forms affiche les rapports de transaction depuis la date configurée, comme illustré dans le rapport récapitulatif ci-dessous :

![sample-transaction-report-author](assets/sample-transaction-report-author.png)

* Utilisez les options **Réinitialiser la date à aujourd’hui** pour réinitialiser les enregistrements de transactions. Lorsque vous réinitialisez la date à aujourd’hui, tous les enregistrements des transactions précédentes sont perdus. Lorsque vous réinitialisez la date sur une instance d’auteur, la modification n’affecte pas les rapports de transaction sur les instances de publication et inversement.
* Utilisez lʼoption **Afficher les transactions des seules instances de publication** pour afficher toutes les transactions qui se sont produites uniquement sur l’instance de publication ou la batterie de publication configurée.
* Pour afficher les transactions correspondantes, utilisez les catégories suivantes : **Document traité**, **Documents restitués** et **Formulaires envoyés**. Pour plus dʼinformations sur le type de transactions comptabilisées dans ces catégories, consultez la section [API de rapports de transactions facturables](../../forms/using/transaction-reports-billable-apis.md).

## Afficher les journaux de rapports de transactions {#view-transaction-reporting-logs}

Le rapport de transaction consigne toutes les informations affichées dans le rapport, ainsi que certaines informations supplémentaires, dans les journaux. Les informations contenues dans les journaux sont utiles pour les utilisateurs avancés. Par exemple, les journaux divisent les transactions en plusieurs catégories granulaires, au lieu des trois catégories consolidées du rapport. Les journaux sont disponibles dans le fichier `error.log` du répertoire `/crx-repository/logs/`. Les journaux sont disponibles même si vous n’activez pas les rapports de transaction depuis la console web AEM.

## Articles connexes {#related-articles}

* [Présentation des rapports de transaction](../../forms/using/transaction-reports-overview.md)
* [API de rapports de transactions facturables](../../forms/using/transaction-reports-billable-apis.md)
* [Enregistrer une transaction pour les implémentations personnalisées](/help/forms/using/record-transaction-custom-implementation.md)
