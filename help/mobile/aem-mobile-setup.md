---
title: Configuration d’AEM Mobile
seo-title: AEM Mobile SetUp
description: Consultez cette page pour configurer AEM Mobile et permettre ainsi à l’utilisateur de créer et de gérer le contenu dans AEM. Cette page fournit des informations sur l’intégration de l’instance AEM avec le ou les comptes et projets AEM Mobile On-demand Services basés sur le cloud.
seo-description: Follow this page for setting up AEM Mobile and thus allowing the user to create and manage the content within AEM. This page provides information on integrating the AEM instance with the cloud-based AEM Mobile On-Demand Services account and project(s).
uuid: 03bf5b56-7750-4f76-b079-43761367655a
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: administering-on-demand-services-app
discoiquuid: 393cf504-917e-4bf6-9a8b-b7a5bd862c65
exl-id: 0ead982d-2315-4947-b762-596aa2aa42a1
source-git-commit: 259f257964829b65bb71b5a46583997581a91a4e
workflow-type: tm+mt
source-wordcount: '929'
ht-degree: 2%

---

# Configuration d’AEM Mobile{#aem-mobile-setup}

>[!NOTE]
>
>Adobe recommande d’utiliser l’éditeur de SPA pour les projets qui nécessitent un rendu côté client basé sur la structure d’application d’une seule page (par exemple, React). [En savoir plus](/help/sites-developing/spa-overview.md).

>[!CAUTION]
>
>Les clients AEM Mobile Apps existants qui migrent d’AEM 6.2 ou 6.3 vers AEM 6.5 peuvent continuer à utiliser les applications AEM Mobile en téléchargeant un module à partir de PackageShare. Toutefois, les nouvelles installations d’AEM 6.5 ne prendront pas en charge la fonctionnalité des applications AEM Mobile.

Pour utiliser AEM afin de produire du contenu pour les applications AEM Mobile, vous devez intégrer l’instance AEM au compte et aux projets AEM Mobile On-demand Services basés sur le cloud.

Suivez ces étapes pour configurer AEM Mobile et permettre ainsi à l’utilisateur de créer et de gérer le contenu dans AEM.

## Approvisionnement d’AEM Mobile {#aem-mobile-provisioning}

Pour commencer à configurer AEM Mobile, vous devez :

* **Demande d’une clé API**: Pour accéder à l&#39;API On-Demand Services, vous devez demander une clé API. Pour demander la clé d’API, renseignez la variable [PDF form](https://helpx.adobe.com/digital-publishing-solution/help/aem-mobile-end-of-life-faq.html). Envoyez le formulaire complété au support Adobe Developer : [wwds@adobe.com](mailto:wwds@adobe.com)

* **Génération de l’ID de périphérique et du jeton de périphérique**: Une fois que vous avez reçu votre clé API, vous pouvez générer l’identifiant de l’appareil et le jeton de l’appareil. Accédez à `https://aex.aemmobile.adobe.com` et procédez comme suit :

   * Fournir la clé API
   * Connectez-vous à un projet Adobe ID que vous avez ajouté à un projet AEM Mobile avec les autorisations suivantes (voir les étapes ci-dessous pour créer un projet).

      * Administration > Gérer les projets et les utilisateurs
      * Contenu > Ajouter et modifier du contenu, supprimer du contenu, afficher du contenu, publier du contenu

Si toutes les conditions sont remplies, un identifiant de périphérique et un jeton de périphérique sont générés.

>[!NOTE]
>
>L’accès à Adobe ID nécessaire doit être autorisé sur un projet AEM Mobile. Voir [Administration de comptes pour AEM Mobile](https://helpx.adobe.com/digital-publishing-solution/help/aem-mobile-end-of-life-faq.html) dans l’aide en ligne.

## Création de projets pour AEM Mobile {#creating-projects-for-aem-mobile}

Lorsque vous créez un projet, vous spécifiez les paramètres de toute plateforme que vous ciblez : Visionneuse web pour iOS, Android, Windows et bureau. La plupart des paramètres du projet que vous spécifiez affectent le comportement de l’application.

Pour créer un projet, vous devez vous connecter au portail des services à la demande à l’aide d’une Adobe ID dotée d’un rôle d’administrateur de Principal. La modification d’un projet nécessite un rôle d’administrateur de Principal ou un rôle d’utilisateur avec un **Gestion des projets et des utilisateurs** autorisation.

>[!NOTE]
>
>Pour en savoir plus sur la création de projets dans AEM Mobile, cliquez sur [here](https://helpx.adobe.com/digital-publishing-solution/help/creating-projects.html).

## Configuration d’un connecteur AEM Mobile {#configuring-an-aem-mobile-connector}

AEM configuration implique les étapes suivantes pour la configuration du connecteur. Une fois la configuration du connecteur AEM Mobile terminée, l’utilisateur peut configurer des groupes d’utilisateurs et des autorisations.

Le connecteur AEM Mobile On-Demand est utilisé pour lier le contenu géré AEM Mobile aux services On-Demand d’Adobe Experience Manager Mobile. Cela permet aux auteurs de contenu de créer et de gérer du contenu pour les applications mobiles à l’aide d’outils AEM, tout en utilisant les services On-Demand d’AEM Mobile pour une distribution facile du contenu mobile.

>[!NOTE]
>
>Il s’agit d’une étape unique pour configurer l’instance AEM.

### Configuration du client AEM Mobile On-demand Services {#configuring-aem-mobile-on-demand-services-client}

Pour que les intégrations AEM Mobile fonctionnent correctement, vous devez suivre les étapes de configuration.

1. Accès à la configuration du service OSGI

   1. AEM > Outils > Opérations > Console web
   1. Faites défiler ou recherchez ***Client Experience Manager Mobile On Demand Services (était le client Adobe Digital Publishing Solution)***

1. Modifier ***Client des services mobiles On-Demand Experience Manager***

   1. **(obligatoire)** Renseignez les champs requis :

      1. ID client.
      1. Secret client.

   1. **(Facultatif)** Modifiez les valeurs existantes.

1. Enregistrez les modifications.
1. Voici un exemple de configuration :

![chlimage_1-53](assets/chlimage_1-53.png)

### Configuration d’AEM Mobile On-demand Services Cloud Service {#configuring-aem-mobile-on-demand-services-cloudservice}

1. Accéder aux Cloud Services

   1. AEM > Outils > Déploiement > [Cloud Services](http://localhost:4502/libs/cq/core/content/tools/cloudservices.html). Faites défiler ou recherchez ***Adobe Experience Manager Mobile On-demand Services***

1. Sélectionner ***Configurer maintenant*** ou ***Afficher les configurations*** et sélectionnez l’icône ajouter une nouvelle configuration .

1. Création d’une configuration

   1. Saisissez un titre et un nom.
   1. Entrer dans l’ID de périphérique
   1. Saisie du jeton de périphérique
   1. Sélectionner ***Test de la configuration du périphérique*** pour valider les valeurs entrées
   1. Sélectionner OK

## Ajout de rôles utilisateur AEM Mobile et attribution d’autorisations {#adding-aem-mobile-user-roles-and-assigning-permissions}

Après avoir créé un projet, vous devez créer des rôles et accorder l’accès aux utilisateurs. Seuls les administrateurs de Principal peuvent créer et modifier des rôles. Lorsque vous créez un rôle, vous activez des fonctionnalités (ou autorisations) pour les utilisateurs auxquels ces autorisations sont affectées. Par exemple, vous pouvez créer un rôle qui inclut des autorisations pour la création d’applications et un autre qui inclut des autorisations pour la création et la publication de contenu.

Dans le développement d’applications AEM Mobile, trois rôles différents existent :

* Administrateur
* Développeur
* Création

Pour plus d’informations sur la création de rôles avec différentes autorisations, telles que pour la création d’applications ou la création et la publication de contenu, cliquez sur [Création de rôles utilisateur et octroi d’accès](https://helpx.adobe.com/digital-publishing-solution/help/account-admin-dps.html) dans l’aide d’AEM Mobile.

>[!NOTE]
>
>La gestion du contenu des applications nécessite un effort collectif des développeurs, des auteurs de contenu et des administrateurs. Les auteurs manipulent les pages, qui sont à leur tour basées sur des modèles et des composants générés par les développeurs d’applications. Enfin, les administrateurs publient stratégiquement le contenu de l’application mis à jour. La configuration des groupes AEM et des autorisations définit leurs rôles dans le tableau de bord de l’application ou dans le centre de contrôle.
>
>Pour plus d’informations sur le tableau de bord AEM Mobile, cliquez sur [here](/help/mobile/mobile-apps-ondemand-application-dashboard.md).

Une fois que vous avez créé des rôles avec différentes autorisations, telles que pour la création d’applications ou pour la création et la publication de contenu, reportez-vous à la section [**Configuration des utilisateurs et des groupes d’utilisateurs**](/help/mobile/aem-mobile-configure-users.md) pour configurer vos utilisateurs et groupes afin qu’ils prennent en charge la création et la gestion de vos applications mobiles.

### Ressources supplémentaires {#additional-resources}

Pour en savoir plus sur les deux autres rôles et responsabilités dans la création d’une application AEM Mobile On-demand Services, consultez les ressources suivantes :

* [Développement de contenu AEM pour AEM Mobile On-demand Services](/help/mobile/aem-mobile-on-demand.md)
* [Création de contenu AEM pour l’application AEM Mobile On-demand Services](/help/mobile/mobile-apps-ondemand.md)

>[!NOTE]
>
>Pour prévisualiser le contenu de l’application, y compris les pages de navigation et les articles, voir [Aperçu avec contrôle en amont](/help/mobile/aem-mobile-manage-ondemand-services.md).
