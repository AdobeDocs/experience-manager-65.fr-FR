---
title: Adobe Experience Manager Mobile On-Demand
description: Le démarrage d’une nouvelle expérience d’application mobile Adobe Experience Manager (AEM) nécessite une cohésion des rôles avant qu’elle ne soit prête pour la modification du contenu. Consultez cette page pour commencer à utiliser AEM services mobiles On-Demand.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: introduction
content-type: reference
exl-id: 4be199d8-963d-4807-b9bb-e23fa577c5f2
solution: Experience Manager
feature: Mobile
role: User
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '761'
ht-degree: 4%

---

# AEM Mobile On-Demand{#aem-mobile-on-demand}

>[!NOTE]
>
>Adobe recommande d’utiliser l’éditeur SPA pour les projets nécessitant un rendu côté client, basé sur un framework, pour une application à une seule page (comme React). [En savoir plus](/help/sites-developing/spa-overview.md).

>[!NOTE]
>
>Si vous n’utilisez pas Adobe Experience Manager (AEM) comme source de gestion de contenu, voir [Aide d’AEM Mobile On-demand Services](https://helpx.adobe.com/digital-publishing-solution/topics.html).

AEM fournit plusieurs outils qui vous permettent d&#39;intégrer votre contenu dans les applications mobiles.

Le diagramme suivant illustre la manière dont les différents composants d’AEM Mobile et des services à la demande s’assemblent pour diffuser du contenu vers les applications mobiles.

L’application AEM Preflight peut être considérée comme un environnement de test permettant de prévisualiser l’application et le contenu avant la publication, tandis que l’application AEM Mobile est l’application finale créée pour la distribution.

>[!NOTE]
>
>Pour en savoir plus sur l’application Preflight, voir [Utilisation de l’application AEM Preflight](https://helpx.adobe.com/digital-publishing-solution/help/preflight-app.html) dans l’aide d’AEM Mobile On-demand Services.

![chlimage_1-171](assets/chlimage_1-171.png)

>[!NOTE]
>
>Dans le diagramme ci-dessus, l’instance de publication AEM n’est pas requise pour un scénario de déploiement classique dans AEM Mobile On-demand Services.

## Démarrage d’une application mobile {#starting-a-new-mobile-app}

AEM Mobile n&#39;est qu&#39;un des piliers de la plateforme AEM complète.

Le démarrage d’une nouvelle expérience d’application AEM Mobile nécessite une cohésion des rôles avant qu’elle ne soit prête pour la modification du contenu. Les rôles suivants constituent un point de départ pour la création d’une application AEM Mobile :

* **Administrateur**
* **Développeur ou développeuse**
* **Auteur**

>[!NOTE]
>
>Avant de travailler avec AEM Mobile et de suivre les étapes décrites dans ce guide de prise en main, les utilisateurs doivent maîtriser AEM. Découvrez les principes de base d’AEM [here](/help/sites-deploying/deploy.md).

### Présentation du tableau de bord de l’application AEM Mobile {#understanding-the-aem-mobile-application-dashboard}

Avant de comprendre les rôles et les responsabilités, l’utilisateur doit posséder une connaissance approfondie de **Centre de contrôle AEM Mobile** ou le **Tableau de bord des applications**. Cliquez sur [here](/help/mobile/mobile-apps-ondemand-application-dashboard.md) pour une compréhension approfondie.

### Administration AEM {#aem-administrator}

Un ***Administrateur AEM*** est chargé d’ajouter une application au catalogue AEM Mobile, soit en créant une application à l’aide de l’assistant de création, soit en important une application existante. AEM administrateurs qui créent une application à l’aide d’AEM Mobile *assistant de création* sélectionnez généralement l’un des modèles d’application souhaités dans les exemples de référence d’usine de l’Adobe ou (généralement) un modèle d’application personnalisé créé par *AEM développeurs.*

Lors de la création d’une application à l’aide d’AEM Mobile On-demand Services, un administrateur d’AEM est responsable des tâches suivantes :

* [Configuration d’AEM Mobile](/help/mobile/aem-mobile-setup.md)
* [Configuration des utilisateurs et des groupes d’utilisateurs](/help/mobile/aem-mobile-configure-users.md)
* [Aperçu avec contrôle en amont](/help/mobile/aem-mobile-manage-ondemand-services.md)
* [Administration de Content Services](/help/mobile/developing-content-services.md)

Pour commencer à utiliser les rôles et responsabilités d’un administrateur, reportez-vous à la section [Administration de contenu pour l’utilisation d’AEM Mobile On-demand Services](/help/mobile/aem-mobile.md).

## AEM Développeur {#aem-developer}

Un **Développeur d’AEM** étend et crée des composants et des modèles web personnalisés pour permettre à l’ *auteur AEM* de créer des expériences mobiles belles et attrayantes. Ces modèles et composants sont non seulement optimisés pour l’application mobile, mais ils communiquent également avec l’appareil et le serveur AEM (tout serveur distant) aux points d’entrée du service omni-canal. AEM l’éditeur de contenu intégré est utilisé par *Auteurs d’AEM* pour créer des expériences riches et pertinentes au sein de l’application, y compris l’intégration au reste de Adobe Experience Cloud.

Un développeur d’AEM est responsable des tâches suivantes lors de la création d’une application à l’aide d’AEM Mobile On-demand Services :

* [Modèles et composants d’application](/help/mobile/app-templates-and-components1.md)
* [Mobile avec synchronisation de contenu](/help/mobile/mobile-ondemand-contentsync.md)
* [Propriétés du contenu et exportation de contenu](/help/mobile/on-demand-content-properties-exporting.md)
* [Développement d’AEM Mobile Content Services](/help/mobile/developing-content-services.md)

Pour commencer à utiliser les rôles et responsabilités des développeurs, voir [Développement de contenu AEM pour AEM Mobile On-demand Services](/help/mobile/aem-mobile-on-demand.md).

>[!NOTE]
>
>Un *AEM de développeur* ne démarre pas et ne se termine pas par le développement de modèles et de composants. Un *Développeur d’AEM* peut créer une application entièrement nouvelle plutôt que d’étendre simplement l’exemple d’implémentation de référence prêt à l’emploi.

## Instance de création AEM {#aem-author}

Un ***Auteur AEM* (ou *Marketer*)**utilise les modèles et composants développés ou prêts à l’emploi personnalisés pour ajouter et modifier des pages, faire glisser et déposer des composants et ajouter des médias de tous types à partir de la gestion des actifs numériques, y compris des images, des vidéos et des fragments de texte (fragments de contenu). AEM l’éditeur de contenu intégré est ensuite utilisé par *Auteurs d’AEM* pour créer des expériences riches et pertinentes au sein de l’application, y compris l’intégration au reste de Adobe Experience Cloud.

Un auteur AEM doit comprendre les rubriques suivantes, lors de la création d’une application à l’aide d’AEM Mobile On-demand Services :

* [Tableau de bord des applications AEM Mobile](/help/mobile/mobile-apps-ondemand-application-dashboard.md)
* [Actions de création et de configuration d’application](/help/mobile/mobile-apps-ondemand-application-create-configure-action.md)
* [Configuration du cloud](/help/mobile/mobile-on-demand-associating-an-on-demand-app-to-cloud-configuration.md)
* [Gestion du contenu](/help/mobile/mobile-apps-ondemand-manage-content-ondemand.md)
* [Présentation de Content Services](/help/mobile/develop-content-as-a-service.md)

Pour commencer à utiliser les rôles et responsabilités d’un auteur, voir [Création de contenu AEM pour l’application AEM Mobile On-demand Services](/help/mobile/mobile-apps-ondemand.md).

>[!NOTE]
>
>Un auteur AEM est également chargé de configurer les droits, de créer des cartes et des mises en page et d’envoyer des notifications push. En outre, pour plus d’informations sur les méthodes de création de contenu, la gestion des articles et des collections, la création de bannières, de cartes et de mises en page dans AEM Mobile, voir [Portail AEM Mobile On-Demand](https://helpx.adobe.com/digital-publishing-solution/topics.html#dynamicpod_reference_2).
