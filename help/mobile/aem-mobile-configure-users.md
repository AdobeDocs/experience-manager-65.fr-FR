---
title: Configuration des utilisateurs et des groupes d’utilisateurs
description: Consultez cette page pour comprendre les rôles des utilisateurs et la configuration des utilisateurs et des groupes afin de prendre en charge la création et la gestion de votre application de services On-Demand mobile.
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: administering-on-demand-services-app
exl-id: 58b7d1b9-a851-442a-9d02-212cad8abbed
solution: Experience Manager
feature: Mobile
role: Admin
source-git-commit: 2dae56dc9ec66f1bf36bbb24d6b0315a5f5040bb
workflow-type: tm+mt
source-wordcount: '473'
ht-degree: 2%

---

# Configuration des utilisateurs et des groupes d’utilisateurs {#configure-your-users-and-user-groups}

{{ue-over-mobile}}

Ce chapitre décrit les rôles utilisateur et la configuration de vos utilisateurs et groupes pour prendre en charge la création et la gestion de vos applications mobiles.

## Administration des utilisateurs et des groupes de l’application AEM Mobile {#aem-mobile-application-users-and-group-administration}

### Auteurs de contenu d’application AEM Mobile (groupe app-author) {#aem-mobile-application-content-authors-app-author-group}

Les membres du groupe app-author sont chargés de la création du contenu de l’application mobile AEM, notamment des pages, du texte, des images et des vidéos.

#### Configuration de groupe - app-authors {#group-configuration-app-authors}

1. Créez un groupe d’utilisateurs appelé « app-authors » :

   Accédez à l’Admin Console utilisateur : [http://localhost:4502/libs/granite/security/content/groupadmin.html](http://localhost:4502/libs/granite/security/content/groupadmin.html)

   Dans la console Groupe d’utilisateurs , sélectionnez le bouton « + » pour créer un groupe.

   Définissez l’identifiant de ce groupe sur « app-authors » pour indiquer qu’il s’agit d’un type spécifique de groupe d’utilisateurs de création spécifique à la création d’applications mobiles dans AEM.

1. Ajouter un membre au groupe : Auteurs

   ![chlimage_1-167](assets/chlimage_1-167.png)

1. Maintenant que vous avez créé le groupe d’utilisateurs app-authors, vous pouvez ajouter des membres d’équipe individuels à ce nouveau groupe via l’[Admin Console utilisateur](http://localhost:4502/libs/granite/security/content/useradmin.md).

   ![chlimage_1-168](assets/chlimage_1-168.png)

1. Ce qui suit vous permet d’ajouter au groupe de créateurs de contenu AEM :

   (Lecture) le

   * /app
   * /etc/clientlibs
   * /etc/designs
   * /etc/cloudservices/dps2015

### Groupe d’administrateurs de l’application AEM Mobile (groupe app-admins) {#aem-mobile-application-administrators-group-app-admins-group}

Les membres du groupe app-admins peuvent créer du contenu d’application avec les mêmes autorisations que celles incluses dans app-authors **ET**. Ils sont également responsables des éléments suivants :

* Évaluation, publication et effacement des mises à jour OTA ContentSync de l’application

>[!NOTE]
>
>Les autorisations déterminent la disponibilité de certaines actions utilisateur dans le centre de commande de l’application AEM.
>
>Notez que certaines options ne sont pas disponibles pour les auteurs d’applications qui sont disponibles pour les administrateurs d’applications.

### Configuration du groupe - app-admins {#group-configuration-app-admins}

1. Créez un groupe appelé app-admins.
1. Ajoutez les groupes suivants à votre nouveau groupe app-admins :

   * auteurs de contenu
   * utilisateurs de workflow

   ![chlimage_1-169](assets/chlimage_1-169.png)

   >[!NOTE]
   >
   >les utilisateurs de workflow sont requis pour créer à distance avec le service PhoneGap Build

1. Accédez à la [console Autorisations](http://localhost:4502/useradmin) et ajoutez des autorisations pour administrer les services cloud

   * (Lecture, modification, création, suppression, réplication) sur /etc/cloudservices/mobileservices

1. Sur la même console Autorisations, ajoutez des autorisations d’évaluation, de publication et d’effacement des mises à jour de contenu d’application.

   * (Lecture, modification, création, suppression, réplication) sur /etc/packages/mobileapp
   * (Lecture) sous /var/contentsync

   >[!NOTE]
   >
   >La réplication de package est utilisée pour publier les mises à jour d’application de l’instance d’auteur vers l’instance de publication

   >[!CAUTION]
   >
   >L’accès à /var/contentsync est refusé par défaut.
   >
   >L’omission de l’autorisation LECTURE peut entraîner la création et la réplication de packages de mise à jour vides.

1. Ajoutez des membres à ce groupe si nécessaire.
1. Pour exporter du contenu ou le charger

   * (Lecture) sur /etc/contentsync pour accéder aux modèles d’exportation.
   * (Lecture) sous /var vers le parcours en lecture
   * (Lecture, écriture, modification, suppression) sur /var/contentsync pour écrire, lire et nettoyer le contenu d’exportation mis en cache de ContentSync.

### Ressources supplémentaires {#additional-resources}

Pour en savoir plus sur les deux autres rôles et responsabilités liés à la création d’une application AEM Mobile On-demand Services, consultez les ressources suivantes :

* [Développement de contenu AEM pour AEM Mobile On-demand Services](/help/mobile/aem-mobile-on-demand.md)
* [Création de contenu AEM pour l’application AEM Mobile On-demand Services](/help/mobile/mobile-apps-ondemand.md)
