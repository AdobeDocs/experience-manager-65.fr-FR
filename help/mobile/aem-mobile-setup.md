---
title: Configuration d'AEM Mobile
seo-title: Configuration d'AEM Mobile
description: Suivez cette page pour configurer AEM Mobile et permettre ainsi à l'utilisateur de créer et de gérer le contenu dans AEM. Cette page fournit des informations sur l'intégration de l'instance AEM avec le compte et les projets AEM Mobile On-Demand Services basés sur le cloud.
seo-description: Suivez cette page pour configurer AEM Mobile et permettre ainsi à l'utilisateur de créer et de gérer le contenu dans AEM. Cette page fournit des informations sur l'intégration de l'instance AEM avec le compte et les projets AEM Mobile On-Demand Services basés sur le cloud.
uuid: 03bf5b56-7750-4f76-b079-43761367655a
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: administering-on-demand-services-app
discoiquuid: 393cf504-917e-4bf6-9a8b-b7a5bd862c65
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Configuration d&#39;AEM Mobile{#aem-mobile-setup}

>[!NOTE]
>
>Adobe recommande d’utiliser l’éditeur d’application d’une seule page (SPA) pour les projets nécessitant un rendu côté client basé sur la structure SPA (par exemple, React). [En savoir plus](/help/sites-developing/spa-overview.md).

>[!CAUTION]
>
>Les clients AEM Mobile Apps qui migrent d&#39;AEM 6.2 ou 6.3 vers AEM 6.5 peuvent continuer à utiliser les applications AEM Mobile en téléchargeant un [package depuis PackageShare](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq640/compatpack/aem-mobile-package). Toutefois, les nouvelles installations d&#39;AEM 6.5 ne prendront pas en charge la fonctionnalité des applications AEM Mobile.

Pour utiliser AEM pour produire du contenu pour les applications AEM Mobile, vous devez intégrer l&#39;instance AEM au compte et aux projets d&#39;AEM Mobile On-Demand Services basés sur le cloud.

Suivez ces étapes pour configurer AEM Mobile et permettre ainsi à l&#39;utilisateur de créer et de gérer le contenu dans AEM.

## Approvisionnement AEM Mobile {#aem-mobile-provisioning}

Pour commencer à configurer AEM Mobile, vous devez :

* **Demander une clé** d&#39;API : Pour accéder à l&#39;interface On-Demand Services API, vous devez demander une clé d&#39;API. Pour demander la clé d’API, complétez le formulaire [](https://helpx.adobe.com/digital-publishing-solution/help/integrating-dps.html)PDF. Envoyez le formulaire rempli au Support aux développeurs Adobe : [wwds@adobe.com](mailto:wwds@adobe.com)

* **Générer l&#39;ID de périphérique et le jeton** de périphérique : Une fois que vous avez reçu votre clé d’API, vous pouvez générer l’ID de périphérique et le jeton de périphérique. Accédez à [https://aex.aemmobile.adobe.com](https://aex.aemmobile.adobe.com/) et procédez comme suit :

   * Fournir la clé d&#39;API
   * Connectez-vous avec un ID Adobe que vous avez ajouté à un projet AEM Mobile avec les autorisations suivantes (voir les étapes ci-dessous pour créer le projet).

      * Administration > Gérer les projets et les utilisateurs
      * Contenu > Ajouter et modifier du contenu, supprimer du contenu, afficher du contenu, publier du contenu

Si toutes les conditions sont remplies, un ID de périphérique et un jeton de périphérique sont générés.

>[!NOTE]
>
>L&#39;ID Adobe requis doit être autorisé à accéder à un projet AEM Mobile. Reportez-vous à la page Administration de [comptes pour AEM Mobile](https://helpx.adobe.com/digital-publishing-solution/help/account-admin-dps.html) dans l&#39;aide en ligne.

## Création de projets pour AEM Mobile {#creating-projects-for-aem-mobile}

Lorsque vous créez un projet, vous spécifiez des paramètres pour toute plateforme ciblée : iOS, Android, Windows et lecteur web pour ordinateur. La plupart des paramètres de projet que vous spécifiez affectent le comportement de l’application.

Pour créer un projet, vous devez vous connecter au portail des services à la demande à l’aide d’un Adobe ID doté du rôle Administrateur principal. Pour modifier un projet, vous devez disposer d’un rôle Administrateur principal ou d’un rôle utilisateur doté de l’autorisation **Gérer les projets et les utilisateurs** .

>[!NOTE]
>
>Pour en savoir plus sur la création de projets dans AEM Mobile, cliquez [ici](https://helpx.adobe.com/digital-publishing-solution/help/creating-projects.html).

## Configuration d&#39;un connecteur AEM Mobile {#configuring-an-aem-mobile-connector}

La configuration d’AEM implique les étapes suivantes pour la configuration du connecteur. Une fois la configuration du connecteur AEM Mobile terminée, l&#39;utilisateur peut configurer des groupes d&#39;utilisateurs et des autorisations.

Le connecteur à la demande d&#39;AEM Mobile permet de lier le contenu géré d&#39;AEM Mobile aux services à la demande d&#39;Adobe Experience Manager Mobile. Cela permet aux auteurs de contenu de créer et de gérer du contenu pour les applications mobiles à l&#39;aide des outils d&#39;AEM, tout en utilisant les services à la demande d&#39;AEM Mobile pour une distribution aisée du contenu mobile.

>[!NOTE]
>
>Il s’agit d’une étape unique de configuration de l’instance AEM.

### Configuration du client AEM Mobile On-Demand Services {#configuring-aem-mobile-on-demand-services-client}

Vous devez suivre les étapes de configuration pour que les intégrations AEM Mobile fonctionnent correctement.

1. Accéder à la configuration du service OSGI

   1. AEM > Outils > Opérations > Console Web
   1. Recherchez ou faites défiler ***Experience Manager Mobile On-Demand Services Client (anciennement Adobe Digital Publishing Solution Client).***

1. Modifier le client ***Experience Manager Mobile On-Demand Services***

   1. **(obligatoire)** Entrez les champs obligatoires :

      1. ID client.
      1. Secret client.
   1. **(Facultatif)** Modifiez les valeurs existantes.


1. Enregistrez les modifications.
1. Voici un exemple de configuration :

![chlimage_1-53](assets/chlimage_1-53.png)

### Configuration d&#39;AEM Mobile On-Demand Services CloudService {#configuring-aem-mobile-on-demand-services-cloudservice}

1. Accès aux services Cloud

   1. AEM > Outils > Déploiement > [CloudServices](http://localhost:4502/libs/cq/core/content/tools/cloudservices.html). Recherchez ou faites défiler ***Adobe Experience Manager Mobile On-Demand Services***

1. Sélectionnez ***Configurer maintenant*** ou ***Afficher les configurations*** et sélectionnez l’icône Ajouter une nouvelle configuration.

1. Créer une configuration

   1. Entrez un titre et un nom
   1. Entrer l&#39;ID de périphérique
   1. Entrer le jeton du périphérique
   1. Sélectionnez ***Tester la configuration*** du périphérique pour valider les valeurs saisies
   1. Sélectionner OK

## Ajout des rôles utilisateur d&#39;AEM Mobile et attribution des autorisations {#adding-aem-mobile-user-roles-and-assigning-permissions}

Après avoir créé un projet, vous devez créer des rôles et accorder l’accès aux utilisateurs. Seuls les administrateurs principaux peuvent créer et modifier des rôles. Lorsque vous créez un rôle, vous activez des fonctionnalités (ou des autorisations) pour les utilisateurs auxquels ces autorisations sont attribuées. Par exemple, vous pouvez créer un rôle qui inclut des autorisations pour la création d’applications et un autre qui inclut des autorisations pour la création et la publication de contenu.

Dans le développement d&#39;applications AEM Mobile, il existe trois rôles différents :

* Administrator
* Développeur
* Création

Pour plus d&#39;informations sur la création de rôles avec différentes autorisations, comme pour la création d&#39;applications ou pour la création et la publication de contenu, cliquez sur [Création de rôles utilisateur et Accès](https://helpx.adobe.com/digital-publishing-solution/help/account-admin-dps.html) dans l&#39;aide d&#39;AEM Mobile.

>[!NOTE]
>
>La gestion du contenu d’une application requiert un effort collectif de la part des développeurs, des auteurs de contenu et des administrateurs. Les auteurs manipulent les pages, qui sont à leur tour basées sur les modèles et les composants générés par les développeurs d’applications. Enfin, les administrateurs publient stratégiquement le contenu de l’application mis à jour. La configuration des groupes AEM et des autorisations définit leurs rôles dans le tableau de bord de l’application ou dans le centre de contrôle.
>
>Pour plus d&#39;informations sur le tableau de bord AEM Mobile, cliquez [ici](/help/mobile/mobile-apps-ondemand-application-dashboard.md).

Une fois que vous avez créé des rôles avec des autorisations différentes, comme pour la création d’applications ou pour la création et la publication de contenu, voir [**Configuration de vos utilisateurs et groupes **](/help/mobile/aem-mobile-configure-users.md)d’utilisateurs pour configurer vos utilisateurs et groupes afin qu’ils prennent en charge la création et la gestion de vos applications mobiles.

### Ressources supplémentaires {#additional-resources}

Pour en savoir plus sur les deux autres rôles et responsabilités de création d&#39;une application de services à la demande AEM Mobile, reportez-vous aux ressources suivantes :

* [Développement de contenu AEM pour les services à la demande AEM Mobile](/help/mobile/aem-mobile-on-demand.md)
* [Création de contenu AEM pour l&#39;application AEM Mobile On-Demand Services](/help/mobile/mobile-apps-ondemand.md)

>[!NOTE]
>
>Pour prévisualiser le contenu de l’application, y compris les pages de navigation et les articles, voir [Aperçu avec contrôle en amont](/help/mobile/aem-mobile-manage-ondemand-services.md).
