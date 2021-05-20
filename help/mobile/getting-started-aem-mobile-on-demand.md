---
title: AEM Mobile On-Demand
seo-title: AEM Mobile On-Demand
description: Le démarrage d’une nouvelle expérience d’application AEM Mobile nécessite une cohésion des rôles avant qu’elle ne soit prête pour la modification du contenu. Consultez cette page pour commencer à utiliser AEM services mobiles On-Demand.
seo-description: Le démarrage d’une nouvelle expérience d’application AEM Mobile nécessite une cohésion des rôles avant qu’elle ne soit prête pour la modification du contenu. Consultez cette page pour commencer à utiliser AEM services mobiles On-Demand.
uuid: 175c609d-3cb8-4a1b-bfea-278df272e500
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: introduction
content-type: reference
discoiquuid: dc6891cd-19cc-4dff-8bda-a41ed8af8bfb
exl-id: 4be199d8-963d-4807-b9bb-e23fa577c5f2
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '804'
ht-degree: 5%

---

# AEM Mobile On-Demand{#aem-mobile-on-demand}

>[!NOTE]
>
>Adobe recommande d’utiliser l’éditeur d’application d’une seule page (SPA) pour les projets nécessitant un rendu côté client basé sur la structure SPA (par exemple, React). [En savoir plus](/help/sites-developing/spa-overview.md).

>[!NOTE]
>
>Si vous n’utilisez pas AEM comme source de gestion de contenu, voir [Aide d’AEM Mobile On-demand Services](https://helpx.adobe.com/digital-publishing-solution/topics.html).

AEM fournit plusieurs outils qui permettent d’intégrer du contenu dans les applications mobiles.

Le diagramme suivant illustre la manière dont les différents composants d’AEM Mobile et des services à la demande s’assemblent pour diffuser du contenu vers les applications mobiles.

L’application AEM Preflight peut être considérée comme un environnement de test permettant de prévisualiser l’application et le contenu avant la publication. alors que l’application AEM Mobile est l’application finale créée pour la distribution.

>[!NOTE]
>
>Pour en savoir plus sur l’application Preflight, voir [Utilisation de l’application AEM Preflight](https://helpx.adobe.com/digital-publishing-solution/help/preflight-app.html) dans l’aide d’AEM Mobile On-demand Services.

![chlimage_1-171](assets/chlimage_1-171.png)

>[!NOTE]
>
>Dans le diagramme ci-dessus, l’instance de publication AEM n’est pas requise pour un scénario de déploiement classique dans AEM Mobile On-demand Services.

## Démarrage d’une nouvelle application mobile {#starting-a-new-mobile-app}

AEM Mobile n&#39;est qu&#39;un des piliers de la plateforme AEM complète.

Le démarrage d’une nouvelle expérience d’application AEM Mobile nécessite une cohésion des rôles avant qu’elle ne soit prête pour la modification du contenu. Les rôles suivants constituent un point de départ pour la création d’une application AEM Mobile :

* **Administrateur**
* **Développeur**
* **Auteur**

>[!NOTE]
>
>Avant de travailler avec AEM Mobile et de suivre les étapes décrites dans ce guide de prise en main, les utilisateurs doivent maîtriser AEM. Découvrez les principes de base d’AEM [ici](/help/sites-deploying/deploy.md).

### Présentation du tableau de bord de l’application AEM Mobile {#understanding-the-aem-mobile-application-dashboard}

Avant de comprendre les rôles et les responsabilités, l’utilisateur doit posséder une connaissance approfondie du **centre de contrôle AEM Mobile** ou du **tableau de bord de l’application**. Cliquez [ici](/help/mobile/mobile-apps-ondemand-application-dashboard.md) pour une compréhension approfondie.

### Administrateur AEM {#aem-administrator}

Un ***administrateur AEM*** est chargé d’ajouter une nouvelle application au catalogue AEM Mobile, soit en créant une application à l’aide de l’assistant de création, soit en important une application existante. AEM les administrateurs qui créent une application à l’aide de l’*assistant de création AEM Mobile* sélectionnent généralement l’un des modèles d’application souhaités, soit parmi nos exemples de référence prêts à l’emploi, soit (dans la plupart des cas) un modèle d’application personnalisé créé par *AEM développeurs.*

Lors de la création d’une application à l’aide d’AEM Mobile On-demand Services, un administrateur AEM est responsable des tâches suivantes :

* [Configuration d’AEM Mobile](/help/mobile/aem-mobile-setup.md)
* [Configuration des utilisateurs et des groupes d’utilisateurs](/help/mobile/aem-mobile-configure-users.md)
* [Aperçu avec contrôle en amont](/help/mobile/aem-mobile-manage-ondemand-services.md)
* [Administration de Content Services](/help/mobile/developing-content-services.md)

Pour commencer à utiliser les rôles et responsabilités d’un administrateur, voir [Administration de contenu pour utiliser AEM Mobile On-demand Services](/help/mobile/aem-mobile.md).

## AEM Développeur {#aem-developer}

Un **AEM développeur** étend et crée des modèles web et des composants personnalisés pour permettre à l’ *auteur AEM* de créer des expériences mobiles belles et attrayantes. Ces modèles et composants ne sont pas seulement optimisés pour le monde des applications mobiles ; mais communiquez à la fois à l’appareil et au serveur AEM (tout serveur distant) aux points d’entrée du service omni-canal. L’AEM éditeur de contenu intégré est utilisé par les *auteurs AEM* pour créer des expériences riches et pertinentes au sein de l’application, y compris l’intégration au reste de Adobe Marketing Cloud.

Un développeur d’AEM est responsable des tâches suivantes lors de la création d’une application à l’aide d’AEM Mobile On-demand Services :

* [Modèles et composants d’application](/help/mobile/app-templates-and-components1.md)
* [Mobile avec synchronisation de contenu](/help/mobile/mobile-ondemand-contentsync.md)
* [Propriétés du contenu et exportation de contenu](/help/mobile/on-demand-content-properties-exporting.md)
* [Développement d’AEM Mobile Content Services](/help/mobile/developing-content-services.md)

Pour commencer à utiliser les rôles et responsabilités des développeurs, voir [Développement de contenu AEM pour AEM Mobile On-demand Services](/help/mobile/aem-mobile-on-demand.md).

>[!NOTE]
>
>Un rôle *AEM de développeur* ne commence pas et ne se termine pas par le développement de modèles et de composants. Un *AEM développeur* peut créer une application entièrement nouvelle plutôt que d’étendre simplement l’exemple d’implémentation de référence prêt à l’emploi.

## Auteur AEM {#aem-author}

Un ***auteur AEM* (ou *marketeur*)**utilise les modèles et composants développés ou prêts à l’emploi personnalisés pour ajouter et modifier des pages, faire glisser des composants et ajouter des supports de tous types à partir de la gestion des actifs numériques, y compris des images, des vidéos et des fragments de texte (fragments de contenu). AEM éditeur de contenu intégré est ensuite utilisé par les *auteurs AEM* pour créer des expériences riches et pertinentes au sein de l’application, y compris l’intégration au reste de Adobe Marketing Cloud.

Un auteur AEM doit comprendre les rubriques suivantes, lors de la création d’une application à l’aide d’AEM Mobile On-demand Services :

* [Tableau de bord des applications AEM Mobile](/help/mobile/mobile-apps-ondemand-application-dashboard.md)
* [Actions de création et de configuration d’application](/help/mobile/mobile-apps-ondemand-application-create-configure-action.md)
* [Configuration du cloud](/help/mobile/mobile-on-demand-associating-an-on-demand-app-to-cloud-configuration.md)
* [Gestion du contenu](/help/mobile/mobile-apps-ondemand-manage-content-ondemand.md)
* [Présentation de Content Services](/help/mobile/develop-content-as-a-service.md)

Pour commencer à utiliser les rôles et responsabilités d’un auteur, voir [Création AEM contenu pour l’application AEM Mobile On-demand Services](/help/mobile/mobile-apps-ondemand.md).

>[!NOTE]
>
>Un auteur AEM est également chargé de configurer les droits, de créer des cartes et des mises en page et d’envoyer des notifications push. En outre, pour plus d’informations sur les méthodes de création de contenu ; la gestion des articles et collections ; pour créer des bannières, des cartes et des mises en page dans AEM Mobile, voir [Portail à la demande AEM Mobile](https://helpx.adobe.com/digital-publishing-solution/topics.html#dynamicpod_reference_2).
