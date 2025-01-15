---
title: Configuration d’AEM Mobile
description: Consultez cette page pour configurer AEM Mobile et permettre ainsi à l’utilisateur de créer et de gérer le contenu dans Adobe Experience Manager (AEM). Cette page fournit des informations sur l’intégration de l’instance AEM au compte et aux projets AEM Mobile On-demand Services basés sur le cloud.
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: administering-on-demand-services-app
exl-id: 0ead982d-2315-4947-b762-596aa2aa42a1
solution: Experience Manager
feature: Mobile
role: Admin
source-git-commit: 2dae56dc9ec66f1bf36bbb24d6b0315a5f5040bb
workflow-type: tm+mt
source-wordcount: '889'
ht-degree: 1%

---

# Configuration d’AEM Mobile{#aem-mobile-setup}

{{ue-over-mobile}}

>[!CAUTION]
>
>Les clients d’applications mobiles Adobe Experience Manager (AEM) existantes effectuant une migration d’AEM 6.2 ou 6.3 vers AEM 6.5 peuvent continuer à utiliser les applications AEM Mobile en téléchargeant un package à partir du partage de packages. Toutefois, les nouvelles installations d’AEM 6.5 ne prennent pas en charge les fonctionnalités des applications AEM Mobile.

Pour utiliser AEM afin de produire du contenu pour les applications AEM Mobile, vous devez intégrer l’instance AEM au compte et aux projets AEM Mobile On-demand Services basés sur le cloud.

Pour configurer AEM Mobile et permettre à l’utilisateur de créer et de gérer le contenu dans AEM, procédez comme suit.

## Approvisionnement d’AEM Mobile {#aem-mobile-provisioning}

Pour commencer à configurer AEM Mobile, vous devez :

* **Demander une clé API** : pour accéder à l’API On-Demand Services, vous devez demander une clé API. Pour demander la clé API, remplissez le formulaire de PDF [](https://helpx.adobe.com/digital-publishing-solution/help/aem-mobile-end-of-life-faq.html). Envoyez le formulaire rempli au support Adobe Developer : [wwds@adobe.com](mailto:wwds@adobe.com)

* **Générer l’ID d’appareil et le jeton d’appareil** : une fois que vous avez reçu votre clé API, vous pouvez générer l’ID d’appareil et le jeton d’appareil. Accédez à `https://aex.aemmobile.adobe.com` et procédez comme suit :

   * Fournir la clé API
   * Connectez-vous avec un Adobe ID que vous avez ajouté à un projet AEM Mobile avec les autorisations suivantes (voir les étapes ci-dessous pour créer un projet)

      * Administration > Gérer les projets et les utilisateurs
      * Contenu > Ajouter et modifier du contenu, Supprimer du contenu, Afficher du contenu, Contenu Publish

Si toutes les conditions sont remplies, un identifiant d’appareil et un jeton d’appareil sont générés.

>[!NOTE]
>
>L’Adobe ID nécessaire doit se voir accorder l’accès sur un projet AEM Mobile. Voir [Administration des comptes pour AEM Mobile](https://helpx.adobe.com/digital-publishing-solution/help/aem-mobile-end-of-life-faq.html) dans l’aide en ligne.

## Création de projets pour AEM Mobile {#creating-projects-for-aem-mobile}

Lorsque vous créez un projet, vous spécifiez des paramètres pour toute plateforme que vous ciblez : iOS, Android™, Windows et la visionneuse Web de bureau. La plupart des paramètres de projet que vous spécifiez affectent le comportement de l’application.

Pour créer un projet, vous devez vous connecter au portail Services à la demande à l’aide d’un Adobe ID doté d’un rôle d’administrateur de Principal. La modification d’un projet nécessite un rôle d’administrateur de Principal ou un rôle utilisateur avec une autorisation **Gérer les projets et les utilisateurs**.

>[!NOTE]
>
>Pour en savoir plus sur la création de projets dans AEM Mobile, cliquez [ici](https://helpx.adobe.com/digital-publishing-solution/help/creating-projects.html).

## Configuration d’un connecteur AEM Mobile {#configuring-an-aem-mobile-connector}

La configuration d’AEM implique les étapes suivantes pour configurer le connecteur. Une fois la configuration du connecteur AEM Mobile terminée, l’utilisateur peut configurer des groupes d’utilisateurs et des autorisations.

Le connecteur On-Demand AEM Mobile est utilisé pour lier le contenu géré par AEM Mobile aux services On-Demand Adobe Experience Manager Mobile. Cela permet aux auteurs de contenu de créer et de gérer du matériel pour les applications mobiles à l’aide des outils AEM, tout en utilisant les services On-Demand d’AEM Mobile pour une distribution facile du contenu mobile.

>[!NOTE]
>
>Il s’agit d’une étape unique pour configurer l’instance AEM.

### Configuration du client AEM Mobile On-demand Services {#configuring-aem-mobile-on-demand-services-client}

Suivez les étapes de configuration pour que les intégrations AEM Mobile fonctionnent correctement.

1. Accéder à la configuration du service OSGI

   1. AEM > Outils > Opérations > Console Web
   1. Faites défiler ou recherchez ***Client de services à la demande mobile Experience Manager (était un client de solution de publication numérique d’Adobe)***

1. Modifier ***Client de services à la demande Mobile Experience Manager***

   1. **(Obligatoire)** Renseignez les champs obligatoires :

      1. Identifiant du client.
      1. Secret client.

   1. **(Facultatif)** Modifiez les valeurs existantes.

1. Enregistrez les modifications.
1. Voici un exemple de configuration :

![chlimage_1-53](assets/chlimage_1-53.png)

### Configuration d’AEM Mobile On-demand Services Cloud Service {#configuring-aem-mobile-on-demand-services-cloudservice}

1. Accédez au Cloud Service.

   1. AEM > Outils > Déploiement > [CloudServices](http://localhost:4502/libs/cq/core/content/tools/cloudservices.html). Faites défiler l’écran ou recherchez ***Services à la demande Adobe Experience Manager Mobile***

1. Sélectionnez ***Configurer maintenant*** ou ***Afficher les configurations*** et sélectionnez l’icône d’ajout de configuration.

1. Création d’une configuration

   1. Saisir un titre et un nom
   1. Saisir l’ID de l’appareil
   1. Saisir le jeton de l’appareil
   1. Sélectionnez ***Tester la configuration de l’appareil*** afin de valider les valeurs saisies
   1. Sélectionner OK

## Ajout de rôles utilisateur AEM Mobile et attribution d’autorisations {#adding-aem-mobile-user-roles-and-assigning-permissions}

Après avoir créé un projet, vous devez créer des rôles et accorder l’accès aux utilisateurs. Seuls les administrateurs de Principal peuvent créer et modifier des rôles. Lorsque vous créez un rôle, vous activez des fonctionnalités (ou des autorisations) pour les utilisateurs et utilisatrices auxquels ces autorisations sont attribuées. Par exemple, vous pouvez créer un rôle qui inclut des autorisations pour la création d’applications et un autre qui inclut des autorisations pour la création et la publication de contenu.

Dans le développement d’applications AEM Mobile, trois rôles différents existent :

* Administrateur
* Développeur ou développeuse
* Création

Pour plus d’informations sur la création de rôles avec différentes autorisations, telles que la création d’applications ou la création et la publication de contenu, cliquez sur [Création de rôles utilisateur et octroi de l’accès](https://helpx.adobe.com/digital-publishing-solution/help/account-admin-dps.html) dans l’aide d’AEM Mobile.

>[!NOTE]
>
>La gestion du contenu de l’application nécessite un effort collectif de la part des développeurs, des auteurs de contenu et des administrateurs. Les auteurs manipulent les pages, qui sont à leur tour basées sur des modèles et des composants générés par les développeurs d’applications. Enfin, les administrateurs publient stratégiquement le contenu de l’application mise à jour. La configuration des groupes et des autorisations AEM définit leurs rôles dans le tableau de bord de l’application ou le Centre de contrôle.
>
>Voir [Tableau de bord AEM Mobile](/help/mobile/mobile-apps-ondemand-application-dashboard.md).

Lorsque vous avez terminé de créer des rôles avec des autorisations différentes, par exemple pour la création d’applications ou pour la création et la publication de contenu, consultez [**Configuration de vos utilisateurs et groupes d’utilisateurs**](/help/mobile/aem-mobile-configure-users.md). Cela peut vous aider à configurer vos utilisateurs et groupes pour prendre en charge la création et la gestion de vos applications mobiles.

### Ressources supplémentaires {#additional-resources}

Pour en savoir plus sur les deux autres rôles et responsabilités liés à la création d’une application AEM Mobile On-demand Services, consultez les ressources suivantes :

* [Développement de contenu AEM pour AEM Mobile On-demand Services](/help/mobile/aem-mobile-on-demand.md)
* [Création de contenu AEM pour l’application AEM Mobile On-demand Services](/help/mobile/mobile-apps-ondemand.md)

>[!NOTE]
>
>Pour prévisualiser le contenu de l’application, y compris les pages de navigation et les articles, consultez [Aperçu avec contrôle en amont](/help/mobile/aem-mobile-manage-ondemand-services.md).
