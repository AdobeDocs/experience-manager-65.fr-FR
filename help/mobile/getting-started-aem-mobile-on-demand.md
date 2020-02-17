---
title: AEM Mobile On-Demand
seo-title: AEM Mobile On-Demand
description: Le démarrage d'une nouvelle expérience d'application AEM Mobile requiert une cohésion des rôles avant d'être prêt pour la modification du contenu. Suivez cette page pour commencer à utiliser les services à la demande AEM Mobile.
seo-description: Le démarrage d'une nouvelle expérience d'application AEM Mobile requiert une cohésion des rôles avant d'être prêt pour la modification du contenu. Suivez cette page pour commencer à utiliser les services à la demande AEM Mobile.
uuid: 175c609d-3cb8-4a1b-bfea-278df272e500
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: introduction
content-type: reference
discoiquuid: dc6891cd-19cc-4dff-8bda-a41ed8af8bfb
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# AEM Mobile On-Demand{#aem-mobile-on-demand}

>[!NOTE]
>
>Adobe recommande d’utiliser l’éditeur d’application d’une seule page (SPA) pour les projets nécessitant un rendu côté client basé sur la structure SPA (par exemple, React). [En savoir plus](/help/sites-developing/spa-overview.md).

>[!NOTE]
>
>Si vous n&#39;utilisez pas AEM comme source de gestion de contenu, reportez-vous à l&#39;Aide [des services à la demande](https://helpx.adobe.com/digital-publishing-solution/topics.html)AEM Mobile.

AEM fournit plusieurs outils qui permettent d’intégrer du contenu dans les applications mobiles.

Le diagramme suivant illustre la manière dont les différents composants d&#39;AEM Mobile et des services à la demande s&#39;intègrent pour diffuser du contenu dans les applications mobiles.

L’application AEM Preflight peut être considérée comme un environnement de test permettant de prévisualiser l’application et le contenu avant sa publication ; tandis que l&#39;application AEM Mobile est la dernière à être créée pour la distribution.

>[!NOTE]
>
>Pour en savoir plus sur l&#39;application Preflight, reportez-vous à la page [Utilisation de l&#39;application](https://helpx.adobe.com/digital-publishing-solution/help/preflight-app.html) AEM Preflight dans l&#39;aide des services à la demande AEM Mobile.

![chlimage_1-171](assets/chlimage_1-171.png)

>[!NOTE]
>
>Dans le diagramme ci-dessus, l&#39;instance de publication AEM n&#39;est pas requise pour un scénario de déploiement type vers les services à la demande AEM Mobile.

## Démarrage d’une nouvelle application mobile {#starting-a-new-mobile-app}

AEM Mobile n&#39;est qu&#39;un pilier qui constitue la plate-forme AEM complète.

Le démarrage d&#39;une nouvelle expérience d&#39;application AEM Mobile requiert une cohésion des rôles avant d&#39;être prêt pour la modification du contenu. Les rôles suivants constituent un point de départ pour la création d&#39;une application AEM Mobile :

* **Administrateur**
* **Développeur**
* **Créateur**

>[!NOTE]
>
>Avant de travailler avec AEM Mobile et de suivre les étapes décrites dans ce guide de prise en main, les utilisateurs doivent connaître AEM. Learn the basics of AEM [here](/help/sites-deploying/deploy.md).

### Présentation du tableau de bord de l&#39;application AEM Mobile {#understanding-the-aem-mobile-application-dashboard}

Avant de comprendre les rôles et les responsabilités, l&#39;utilisateur doit posséder une connaissance approfondie d&#39; **AEM Mobile Control Center** ou du tableau de bord **de l&#39;** application. Cliquez [ici](/help/mobile/mobile-apps-ondemand-application-dashboard.md) pour une compréhension approfondie.

### Administrateur AEM {#aem-administrator}

Un administrateur ****** AEM est responsable de l&#39;ajout d&#39;une nouvelle application au catalogue AEM Mobile, soit en créant une nouvelle application à l&#39;aide de l&#39;assistant de création, soit en important une application existante. Les administrateurs AEM qui créent une nouvelle application à l&#39;aide de l&#39;assistant *de* création d&#39;AEM Mobile sélectionnent généralement l&#39;un des modèles d&#39;application souhaités, soit à partir des exemples de référence prêts à l&#39;emploi, soit (dans la plupart des cas) à partir d&#39;un modèle d&#39;application personnalisé créé par les développeurs *AEM.*

Un administrateur AEM est responsable des tâches suivantes lors de la création d&#39;une application à l&#39;aide des services à la demande AEM Mobile :

* [Configuration d&#39;AEM Mobile](/help/mobile/aem-mobile-setup.md)
* [Configuration des utilisateurs et des groupes d’utilisateurs](/help/mobile/aem-mobile-configure-users.md)
* [Aperçu avec contrôle en amont](/help/mobile/aem-mobile-manage-ondemand-services.md)
* [Administration de Content Services](/help/mobile/developing-content-services.md)

Pour commencer avec les rôles et responsabilités d&#39;un administrateur, voir [Administration du contenu pour utiliser les services](/help/mobile/aem-mobile.md)à la demande AEM Mobile.

## Développeur AEM {#aem-developer}

Un développeur **AEM** étend et crée des modèles Web et des composants personnalisés pour permettre à *AEM Author *de créer de belles expériences mobiles attrayantes. Ces modèles et composants ne sont pas seulement optimisés pour l’univers des applications mobiles ; mais communiquez avec le périphérique et le serveur AEM (tout serveur distant) pour obtenir des points de terminaison de service omni-channel. L’éditeur de contenu intégré d’AEM est utilisé par les auteurs *d’* AEM pour créer des expériences riches et pertinentes au sein de l’application, y compris l’intégration au reste d’Adobe Marketing Cloud.

Un développeur AEM est responsable des tâches suivantes lors de la création d&#39;une application à l&#39;aide des services à la demande AEM Mobile :

* [Modèles d’application et composants](/help/mobile/app-templates-and-components1.md)
* [Mobile avec Content Sync](/help/mobile/mobile-ondemand-contentsync.md)
* [Propriétés du contenu et exportation de contenu](/help/mobile/on-demand-content-properties-exporting.md)
* [Développement d&#39;AEM Mobile Content Services](//help/mobile/developing-content-services.md)

Pour vous familiariser avec les rôles et responsabilités des développeurs, reportez-vous à la page [Développement de contenu AEM pour les services](/help/mobile/aem-mobile-on-demand.md)à la demande AEM Mobile.

>[!NOTE]
>
>Le rôle *d’un développeur* AEM ne commence pas et ne se termine pas par le développement de modèles et de composants. Un développeur *AEM* peut créer une application entièrement nouvelle au lieu de simplement étendre l’exemple d’implémentation de référence prêt à l’emploi.

## Auteur AEM {#aem-author}

Un ***AEM Author *(ou*Marketer *)**utilise les modèles et composants personnalisés développés ou prêts à l’emploi pour ajouter et modifier des pages, faire glisser et déposer des composants et ajouter des supports de tous types à partir du DAM, y compris des images, des vidéos et des fragments de texte (fragments de contenu). L’éditeur de contenu intégré d’AEM est ensuite utilisé par les auteurs*d’*AEM pour créer des expériences riches et pertinentes au sein de l’application, y compris l’intégration au reste d’Adobe Marketing Cloud.

Un auteur AEM doit comprendre les rubriques suivantes, lors de la création d&#39;une application à l&#39;aide des services à la demande AEM Mobile :

* [Tableau de bord des applications AEM Mobile](/help/mobile/mobile-apps-ondemand-application-dashboard.md)
* [Actions de création et de configuration d’application](/help/mobile/mobile-apps-ondemand-application-create-configure-action.md)
* [Configuration du cloud](/help/mobile/mobile-on-demand-associating-an-on-demand-app-to-cloud-configuration.md)
* [Gestion du contenu](/help/mobile/mobile-apps-ondemand-manage-content-ondemand.md)
* [Présentation de Content Services](/help/mobile/develop-content-as-a-service.md)

Pour commencer avec les rôles et responsabilités d&#39;un auteur, reportez-vous à la page [Création de contenu AEM pour l&#39;application](/help/mobile/mobile-apps-ondemand.md)AEM Mobile On-Demand Services.

>[!NOTE]
>
>Un auteur AEM est également chargé de configurer les droits, de créer des cartes et des mises en page et d’envoyer des notifications Push. Pour plus d&#39;informations sur les méthodes de création de contenu, gestion des articles et des collections; création de bannières, de cartes et de mises en page dans AEM Mobile, reportez-vous à [AEM Mobile On-Demand Portal](https://helpx.adobe.com/digital-publishing-solution/topics.html#dynamicpod_reference_2).

