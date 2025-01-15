---
title: Adobe Experience Manager Mobile On-Demand
description: Le démarrage d’une nouvelle expérience d’application mobile Adobe Experience Manager (AEM) nécessite une cohésion des rôles avant d’être prêt pour la modification de contenu. Consultez cette page pour commencer à utiliser les services mobiles On-Demand d’AEM.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: introduction
content-type: reference
exl-id: 4be199d8-963d-4807-b9bb-e23fa577c5f2
solution: Experience Manager
feature: Mobile
role: User
source-git-commit: 2dae56dc9ec66f1bf36bbb24d6b0315a5f5040bb
workflow-type: tm+mt
source-wordcount: '740'
ht-degree: 1%

---

# AEM Mobile On-Demand{#aem-mobile-on-demand}

{{ue-over-mobile}}

>[!NOTE]
>
>Si vous n’utilisez pas Adobe Experience Manager (AEM) comme source de gestion de contenu, consultez l’[Aide d’AEM Mobile On-demand Services](https://helpx.adobe.com/digital-publishing-solution/topics.html).

AEM propose plusieurs outils permettant d’intégrer des contenus dans des applications mobiles.

Le diagramme suivant illustre la manière dont les différents composants d’AEM Mobile et des services à la demande s’intègrent pour diffuser du contenu aux applications mobiles.

L’application AEM Preflight peut être considérée comme un environnement de test pour prévisualiser l’application et le contenu avant sa publication, tandis que l’application AEM Mobile est la dernière application créée pour la distribution.

>[!NOTE]
>
>Pour en savoir plus sur l’application de contrôle en amont, voir [Utilisation de l’application de contrôle en amont AEM](https://helpx.adobe.com/digital-publishing-solution/help/preflight-app.html) dans l’aide d’AEM Mobile On-demand Services.

![chlimage_1-171](assets/chlimage_1-171.png)

>[!NOTE]
>
>Dans le diagramme ci-dessus, l’instance AEM Publish n’est pas nécessaire pour un scénario de déploiement standard d’AEM Mobile On-demand Services.

## Démarrage d’une nouvelle application mobile {#starting-a-new-mobile-app}

AEM Mobile n’est qu’un pilier de la plateforme AEM dans son ensemble.

Le démarrage d’une nouvelle expérience d’application AEM Mobile requiert une cohésion des rôles avant d’être prêt pour la modification du contenu. Les rôles ci-dessous servent de point de départ pour créer une application AEM Mobile :

* **Administrateur**
* **Développeur ou développeuse**
* **Auteur**

>[!NOTE]
>
>Avant de travailler avec AEM Mobile et de suivre les étapes de ce guide de prise en main, les utilisateurs doivent connaître AEM. Découvrez les principes de base d’AEM [ici](/help/sites-deploying/deploy.md).

### Présentation du tableau de bord de l’application AEM Mobile {#understanding-the-aem-mobile-application-dashboard}

Avant de comprendre les rôles et les responsabilités, l’utilisateur doit posséder des connaissances approfondies du **Centre de contrôle AEM Mobile** ou du **Tableau de bord de l’application**. Cliquez [ici](/help/mobile/mobile-apps-ondemand-application-dashboard.md) pour une compréhension approfondie.

### Administration AEM {#aem-administrator}

Un ***administrateur AEM*** est chargé d’ajouter une application au catalogue AEM Mobile, soit en créant une application à l’aide de l’assistant de création, soit en important une application existante. Les administrateurs AEM qui créent une application à l’aide de l’assistant de création d’AEM Mobile *assistant* sélectionnent généralement l’un des modèles d’application souhaités parmi les exemples de référence prêts à l’emploi d’Adobe ou (généralement) un modèle d’application personnalisé créé par *les développeurs AEM.*

Un administrateur AEM est chargé des tâches suivantes lors de la création d’une application à l’aide d’AEM Mobile On-demand Services :

* [Configuration d’AEM Mobile](/help/mobile/aem-mobile-setup.md)
* [Configuration des utilisateurs et des groupes d’utilisateurs](/help/mobile/aem-mobile-configure-users.md)
* [Aperçu avec contrôle en amont](/help/mobile/aem-mobile-manage-ondemand-services.md)
* [Administration de Content Services](/help/mobile/developing-content-services.md)

Pour commencer à connaître les rôles et responsabilités d’un administrateur, voir [Administration de contenu pour utiliser AEM Mobile On-demand Services](/help/mobile/aem-mobile.md).

## Développeur AEM {#aem-developer}

Un **développeur AEM** étend et crée des modèles et des composants web personnalisés pour permettre à l’*auteur AEM* de créer des expériences mobiles attrayantes et magnifiques. Ces modèles et composants ne sont pas seulement optimisés pour le monde des applications mobiles. Ils communiquent également à l’appareil et au serveur AEM (tout serveur distant) aux points d’entrée de service omnicanal. L’éditeur de contenu intégré d’AEM est utilisé par les *auteurs AEM* pour créer des expériences riches et pertinentes dans l’application, y compris l’intégration au reste du Adobe Experience Cloud.

Un développeur AEM est chargé des tâches suivantes lors de la création d’une application à l’aide d’AEM Mobile On-demand Services :

* [Modèles et composants d’application](/help/mobile/app-templates-and-components1.md)
* [Mobile avec synchronisation de contenu](/help/mobile/mobile-ondemand-contentsync.md)
* [Propriétés du contenu et exportation de contenu](/help/mobile/on-demand-content-properties-exporting.md)
* [Développement d’AEM Mobile Content Services](/help/mobile/developing-content-services.md)

Pour connaître les rôles et responsabilités des développeurs, reportez-vous à la section [Développement de contenu AEM pour AEM Mobile On-demand Services](/help/mobile/aem-mobile-on-demand.md).

>[!NOTE]
>
>Un rôle de développeur *AEM* ne commence pas et ne se termine pas par le développement de modèles et de composants. Un *développeur ou une développeuse AEM* peut créer une application entièrement nouvelle plutôt que simplement étendre l’exemple d’implémentation de référence prêt à l’emploi.

## Instance de création AEM {#aem-author}

Un ***auteur AEM* (ou un *spécialiste marketing*)**utilise les modèles et composants personnalisés développés ou prêts à l’emploi pour ajouter et modifier des pages, faire glisser et déposer des composants et ajouter des médias de tous types à partir de la gestion des ressources numériques, y compris des images, des vidéos et des fragments de texte (fragments de contenu). L’éditeur de contenu intégré d’AEM est ensuite utilisé par les *auteurs AEM* pour créer des expériences riches et pertinentes dans l’application, y compris l’intégration au reste du Adobe Experience Cloud.

Un auteur AEM doit comprendre les rubriques suivantes lors de la création d’une application à l’aide d’AEM Mobile On-demand Services :

* [Tableau de bord de l’application AEM Mobile](/help/mobile/mobile-apps-ondemand-application-dashboard.md)
* [Actions de création et de configuration d’application](/help/mobile/mobile-apps-ondemand-application-create-configure-action.md)
* [Configuration du cloud](/help/mobile/mobile-on-demand-associating-an-on-demand-app-to-cloud-configuration.md)
* [Gestion de contenu](/help/mobile/mobile-apps-ondemand-manage-content-ondemand.md)
* [Présentation de Content Services](/help/mobile/develop-content-as-a-service.md)

Pour commencer à connaître les rôles et responsabilités d’un auteur, reportez-vous à la section [ Création de contenu AEM pour l’application AEM Mobile On-demand Services ](/help/mobile/mobile-apps-ondemand.md).

>[!NOTE]
>
>Un auteur AEM est également responsable de la configuration des droits, de la création des cartes et des mises en page, ainsi que de l’envoi des notifications push. Pour plus d’informations sur les méthodes de création de contenu, de gestion d’articles et de collections, de création de bannières, de cartes et de mises en page dans AEM Mobile, consultez [Portail On-Demand AEM Mobile](https://helpx.adobe.com/digital-publishing-solution/topics.html#dynamicpod_reference_2).
