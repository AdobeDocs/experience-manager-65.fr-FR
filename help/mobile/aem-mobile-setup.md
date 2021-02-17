---
title: Configuration AEM Mobile
seo-title: Configuration AEM Mobile
description: Suivez cette page pour configurer AEM Mobile et permettre ainsi à l’utilisateur de créer et de gérer le contenu dans AEM. Cette page fournit des informations sur l’intégration de l’instance AEM au compte AEM Mobile On-demand Services et aux projets basés sur le cloud.
seo-description: Suivez cette page pour configurer AEM Mobile et permettre ainsi à l’utilisateur de créer et de gérer le contenu dans AEM. Cette page fournit des informations sur l’intégration de l’instance AEM au compte AEM Mobile On-demand Services et aux projets basés sur le cloud.
uuid: 03bf5b56-7750-4f76-b079-43761367655a
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: administering-on-demand-services-app
discoiquuid: 393cf504-917e-4bf6-9a8b-b7a5bd862c65
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '990'
ht-degree: 4%

---


# Configuration AEM Mobile{#aem-mobile-setup}

>[!NOTE]
>
>Adobe recommande d’utiliser l’éditeur d’application d’une seule page (SPA) pour les projets nécessitant un rendu côté client basé sur la structure SPA (par exemple, React). [En savoir plus](/help/sites-developing/spa-overview.md).

>[!CAUTION]
>
>Les clients AEM Mobile Apps qui migrent de AEM 6.2 ou 6.3 vers AEM 6.5 peuvent continuer à utiliser les AEM Mobile Apps en téléchargeant un package [à partir de PackageShare](https://www.adobeaemcloud.com/content/marketplace/marketplaceProxy.html?packagePath=/content/companies/public/adobe/packages/cq640/compatpack/aem-mobile-package). Cependant, les nouvelles installations d&#39;AEM 6.5 ne prendront pas en charge la fonctionnalité des applications AEM Mobile.

Pour utiliser l’AEM pour produire du contenu pour les applications AEM Mobile, vous devez intégrer l’instance AEM au compte et au projet AEM Mobile On-demand Services basés sur le cloud.

Suivez ces étapes pour configurer AEM Mobile et permettre ainsi à l’utilisateur de créer et de gérer le contenu dans AEM.

## Approvisionnement AEM Mobile {#aem-mobile-provisioning}

Pour commencer à configurer AEM Mobile, vous devez :

* **Demander une clé** d&#39;API : Pour accéder à l&#39;interface On-Demand Services API, vous devez demander une clé d&#39;API. Pour demander la clé d&#39;API, remplissez le [formulaire PDF](https://helpx.adobe.com/digital-publishing-solution/help/integrating-dps.html). Envoyez le formulaire rempli au Support aux développeurs d&#39;Adobes : [wwds@adobe.com](mailto:wwds@adobe.com)

* **Générer l&#39;ID de périphérique et le jeton** de périphérique : Une fois que vous avez reçu votre clé d’API, vous pouvez générer l’ID de périphérique et le jeton de périphérique. Accédez à [https://aex.aemmobile.adobe.com](https://aex.aemmobile.adobe.com/) et procédez comme suit :

   * Fournir la clé d&#39;API
   * Connectez-vous avec une Adobe ID que vous avez ajoutée à un projet AEM Mobile avec les autorisations suivantes (voir les étapes ci-dessous pour créer un projet).

      * Administration > Gérer les projets et les utilisateurs
      * Contenu > Ajouter et modifier du contenu, supprimer du contenu, Vue du contenu, publier du contenu

Si toutes les conditions sont remplies, un ID de périphérique et un jeton de périphérique sont générés.

>[!NOTE]
>
>L&#39;Adobe ID doit avoir accès à un projet AEM Mobile. Voir [Administration de comptes pour AEM Mobile](https://helpx.adobe.com/digital-publishing-solution/help/account-admin-dps.html) dans l’aide en ligne.

## Création de projets pour AEM Mobile {#creating-projects-for-aem-mobile}

Lorsque vous créez un projet, vous spécifiez des paramètres pour toute plateforme que vous ciblez : iOS, Android, Windows et lecteur web pour ordinateur. La plupart des paramètres de projet que vous spécifiez affectent le comportement de l’application.

Pour créer un projet, vous devez vous connecter au portail des services à la demande à l&#39;aide d&#39;une Adobe ID dotée d&#39;un rôle d&#39;administrateur de Principal. La modification d’un projet requiert soit un rôle d’administrateur de Principal, soit un rôle d’utilisateur doté de l’autorisation **Gérer les projets et les utilisateurs**.

>[!NOTE]
>
>Pour en savoir plus sur la création de projets en AEM Mobile, cliquez [ici](https://helpx.adobe.com/digital-publishing-solution/help/creating-projects.html).

## Configuration d’un connecteur AEM Mobile {#configuring-an-aem-mobile-connector}

La configuration AEM implique les étapes suivantes pour la configuration du connecteur. Une fois la configuration du connecteur AEM Mobile terminée, l’utilisateur peut configurer des groupes d’utilisateurs et des autorisations.

Le connecteur AEM Mobile On-Demand est utilisé pour lier le contenu géré AEM Mobile aux services On-Demand d’Adobe Experience Manager Mobile. Cela permet aux créateurs de contenu de créer et de gérer du contenu pour les applications mobiles à l’aide des outils d’AEM, tout en utilisant les services à la demande d’AEM Mobile pour une distribution facile du contenu mobile.

>[!NOTE]
>
>Il s’agit d’une étape unique de configuration de l’instance AEM.

### Configuration du client AEM Mobile On-demand Services {#configuring-aem-mobile-on-demand-services-client}

Vous devez exécuter les étapes de configuration pour que les intégrations AEM Mobile fonctionnent correctement.

1. Accéder à la configuration du service OSGI

   1. AEM > Outils > Opérations > Console Web
   1. Recherchez ***Experience Manager Mobile On-Demand Services Client (anciennement Adobe Digital Publishing Solution Client)***

1. Modifier ***Client des services à la demande pour mobile Experience Manager***

   1. **(obligatoire)** Saisissez les champs obligatoires :

      1. ID client.
      1. Secret client.
   1. **(Facultatif)** Modifiez les valeurs existantes.


1. Enregistrez les modifications.
1. Voici un exemple de configuration :

![chlimage_1-53](assets/chlimage_1-53.png)

### Configuration de AEM Mobile On-demand Services CloudService {#configuring-aem-mobile-on-demand-services-cloudservice}

1. Aller en Cloud Services

   1. AEM > Outils > Déploiement > [CloudServices](http://localhost:4502/libs/cq/core/content/tools/cloudservices.html). Recherchez ***Adobe Experience Manager Mobile On-Demand Services*** dans le menu déroulant.

1. Sélectionnez ***Configurer maintenant*** ou ***Afficher les configurations*** et sélectionnez l&#39;icône Ajouter une nouvelle configuration.

1. Créer une configuration

   1. Saisissez un titre et un nom
   1. Entrer l&#39;ID de périphérique
   1. Entrer le jeton de périphérique
   1. Sélectionnez ***Test de la configuration du périphérique*** pour valider les valeurs saisies.
   1. Sélectionner OK

## Ajouter les rôles utilisateur AEM Mobile et attribuer des autorisations {#adding-aem-mobile-user-roles-and-assigning-permissions}

Après avoir créé un projet, vous devez créer des rôles et accorder l’accès aux utilisateurs. Seuls les administrateurs de Principal peuvent créer et modifier des rôles. Lorsque vous créez un rôle, vous activez des fonctionnalités (ou autorisations) pour les utilisateurs auxquels ces autorisations sont attribuées. Par exemple, vous pouvez créer un rôle qui inclut des autorisations pour la création d’applications et un autre rôle qui inclut des autorisations pour la création et la publication de contenu.

Dans le développement d’applications AEM Mobile, il existe trois rôles différents :

* Administrator
* Développeur
* Création

Pour plus d’informations sur la création de rôles avec différentes autorisations, par exemple pour la création d’applications ou pour la création et la publication de contenu, cliquez sur [Création de rôles utilisateur et octroi d’accès](https://helpx.adobe.com/digital-publishing-solution/help/account-admin-dps.html) dans l’aide AEM Mobile.

>[!NOTE]
>
>La gestion du contenu d’une application requiert un effort collectif des développeurs, des auteurs de contenu et des administrateurs. Les auteurs manipulent les pages, lesquelles reposent à leur tour sur des modèles et des composants générés par les développeurs d’applications. Enfin, les administrateurs publient stratégiquement le contenu de l’application mis à jour. La configuration de groupes AEM et d’autorisations définit leurs rôles dans le Tableau de bord de l’application ou dans Control Center.
>
>Pour plus d’informations sur le Tableau de bord AEM Mobile, cliquez [ici](/help/mobile/mobile-apps-ondemand-application-dashboard.md).

Une fois les rôles créés avec différentes autorisations, par exemple pour la création d’applications ou pour la création et la publication de contenu, voir [**Configurer vos groupes d’utilisateurs et d’utilisateurs**](/help/mobile/aem-mobile-configure-users.md) pour configurer vos utilisateurs et groupes afin qu’ils prennent en charge la création et la gestion de vos applications mobiles.

### Ressources supplémentaires {#additional-resources}

Pour en savoir plus sur les deux autres rôles et responsabilités de création d’une application AEM Mobile On-demand Services, consultez les ressources suivantes :

* [Développement de contenu AEM pour AEM Mobile On-demand Services](/help/mobile/aem-mobile-on-demand.md)
* [Création de contenu AEM pour une application AEM Mobile On-demand Services](/help/mobile/mobile-apps-ondemand.md)

>[!NOTE]
>
>Pour prévisualisation du contenu de l’application, y compris les pages de navigation et les articles, voir [Prévisualisation avec contrôle en amont](/help/mobile/aem-mobile-manage-ondemand-services.md).
