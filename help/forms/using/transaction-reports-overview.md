---
title: Présentation des rapports sur les transactions
seo-title: Présentation des rapports sur les transactions
description: Conserver le décompte de tous les formulaires envoyés, les communications interactives rendues, les Documents convertis en un autre format, etc.
seo-description: Conserver le décompte de tous les formulaires envoyés, les communications interactives rendues, les Documents convertis en un autre format, etc.
uuid: 2c3dc1f3-5bbf-4aab-aa84-7aef5aabadf6
topic-tags: forms-manager
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: b2c09e6b-a1d8-4b30-af2c-988442a3a986
docset: aem65
translation-type: tm+mt
source-git-commit: 8f90dc4865126d52e04effc9197ef7145b1a167e
workflow-type: tm+mt
source-wordcount: '573'
ht-degree: 0%

---


# Présentation des rapports sur les transactions{#transaction-reports-overview}

## Présentation {#introduction}

Les rapports de transactions à AEM Forms vous permettent de conserver le décompte de toutes les transactions effectuées depuis une date spécifiée dans votre déploiement AEM Forms. L&#39;objectif est de fournir des informations sur l&#39;utilisation des produits et d&#39;aider les parties prenantes à comprendre leurs volumes de traitement numérique. Voici quelques exemples d’une transaction :

* Envoi d’un formulaire adaptatif, d’un formulaire HTML5 ou d’un jeu de formulaires
* Rendu d&#39;une version imprimée ou Web d&#39;une communication interactive
* Conversion d’un document d’un format de fichier à un autre

Pour plus d&#39;informations sur ce qui est considéré comme une transaction, consultez API [](../../forms/using/transaction-reports-billable-apis.md)facturables.

L’enregistrement de transaction est désactivé par défaut. Vous pouvez [activer l&#39;enregistrement](../../forms/using/viewing-and-understanding-transaction-reports.md#setting-up-transaction-reports) des transactions à partir de AEM console Web. Vous pouvez vue des rapports de transactions sur les instances d’auteur, de traitement ou de publication. Vue des rapports de transactions sur les instances d&#39;auteur ou de traitement pour une somme agrégée de toutes les transactions. Les transactions de vue génèrent des rapports sur les instances de publication pour comptabiliser toutes les transactions qui ont lieu uniquement sur cette instance de publication à partir de laquelle l&#39;état est exécuté.

Ne créez pas de contenu (créez des formulaires adaptatifs, des communications interactives, des thèmes et d’autres activités de création) et de documents de processus (utilisez des workflows, des services de document et d’autres activités de traitement) sur la même instance AEM. Conservez l’enregistrement de transaction désactivé pour les serveurs AEM Forms utilisés pour créer du contenu. Activez l’enregistrement des transactions pour les serveurs AEM Forms utilisés pour traiter les documents.

![sample-transaction-report-author-1](assets/sample-transaction-report-author-1.png)

Une transaction reste dans la mémoire tampon pendant une période spécifiée (durée de la mémoire tampon de vidage + temps de réplication inverse). Par défaut, il faut environ 90 secondes pour que le nombre de transactions se reflète dans l&#39;état de la transaction.

Les actions telles que l’envoi d’un formulaire PDF, l’utilisation de l’interface utilisateur de l’agent pour prévisualisation une communication interactive ou l’utilisation de méthodes d’envoi de formulaire non standard ne sont pas comptabilisées comme des transactions. AEM Forms fournit une API pour enregistrer ces transactions. Appelez l’API depuis vos implémentations personnalisées pour enregistrer une transaction.

## Topologie prise en charge {#supported-topology}

Les rapports de transactions sont disponibles uniquement sur AEM Forms sur l’environnement OSGi. Il prend en charge les topologies auteur-publication, auteur-traitement-publication et de traitement uniquement. For example topologies, see [Architecture and deployment topologies for AEM Forms](../../forms/using/transaction-reports-overview.md).

Le nombre de transactions est répliqué inversement d’instances de publication à des instances d’auteur ou de traitement. Une topologie indicative auteur-publication s’affiche ci-dessous :

![simple-auteur-publication-topologie](assets/simple-author-publish-topology.png)

>[!NOTE]
>
>Les rapports de transactions AEM Forms ne prennent pas en charge les topologies qui contiennent uniquement des instances de publication.

### Instructions relatives à l&#39;utilisation des rapports de transactions {#guidelines-for-using-transaction-reports}

* Désactiver les rapports de transactions sur toutes les instances d’auteur en tant que rapports sur les instances d’auteur inclut les transactions enregistrées lors de la création d’activités.
* Activez l’option **Afficher les transactions de publication uniquement** sur l’instance d’auteur pour vue les transactions cumulatives de toutes les instances de publication. Vous pouvez également vue des rapports de transactions sur chaque instance de publication pour les transactions réelles sur cette instance de publication uniquement.
* N’utilisez pas les instances d’auteur pour exécuter des workflows et traiter des documents.
* Avant d’utiliser le rapports de transaction, si vous disposez d’une stratégie avec les serveurs de publication, assurez-vous que la réplication inversée est activée pour toutes les instances de publication.
* Les données de transaction sont répliquées de manière inversée d’une instance de publication à une instance d’auteur ou de traitement correspondante uniquement. L’auteur ou l’instance de traitement ne peut pas répliquer davantage les données vers une autre instance. Par exemple, si vous disposez de la topologie author-processing-publish, les données de transaction agrégées sont répliquées uniquement sur l’instance de traitement.

## Related Articles {#related-articles}

* [Affichage et compréhension des rapports sur les transactions](../../forms/using/viewing-and-understanding-transaction-reports.md)
* [API facturables des rapports de transaction](../../forms/using/transaction-reports-billable-apis.md)
* [Enregistrer une transaction pour les implémentations personnalisées](/help/forms/using/record-transaction-custom-implementation.md)

