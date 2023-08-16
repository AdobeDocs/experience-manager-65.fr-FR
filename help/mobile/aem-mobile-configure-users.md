---
title: Configuration des utilisateurs et des groupes d’utilisateurs
description: Consultez cette page pour comprendre les rôles utilisateur et comment configurer vos utilisateurs et groupes afin de prendre en charge la création et la gestion de votre application mobile On-Demand Services.
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: administering-on-demand-services-app
exl-id: 58b7d1b9-a851-442a-9d02-212cad8abbed
source-git-commit: 50d29c967a675db92e077916fb4adef6d2d98a1a
workflow-type: tm+mt
source-wordcount: '511'
ht-degree: 2%

---

# Configuration des utilisateurs et des groupes d’utilisateurs {#configure-your-users-and-user-groups}

>[!NOTE]
>
>Adobe recommande d’utiliser l’éditeur de SPA pour les projets qui nécessitent un rendu côté client basé sur la structure d’application d’une seule page (par exemple, React). [En savoir plus](/help/sites-developing/spa-overview.md).

Ce chapitre décrit les rôles utilisateur et comment configurer vos utilisateurs et groupes pour prendre en charge la création et la gestion de vos applications mobiles.

## Utilisateurs des applications AEM Mobile et administration des groupes {#aem-mobile-application-users-and-group-administration}

### Auteurs de contenu d’application AEM Mobile (groupe app-author) {#aem-mobile-application-content-authors-app-author-group}

Les membres du groupe app-author sont chargés de la création AEM contenu de l’application mobile, y compris les pages, le texte, les images et les vidéos.

#### Configuration de groupe - app-authors {#group-configuration-app-authors}

1. Créez un groupe d’utilisateurs appelé &quot;app-authors&quot; :

   Accédez au Admin Console utilisateur : [http://localhost:4502/libs/granite/security/content/groupadmin.html](http://localhost:4502/libs/granite/security/content/groupadmin.html)

   Dans la console du groupe d’utilisateurs, cliquez sur le bouton &quot;+&quot; pour créer un groupe.

   Définissez l’identifiant de ce groupe sur &quot;app-authors&quot; pour indiquer qu’il s’agit d’un type spécifique de groupe d’utilisateurs de création spécifique à la création d’applications mobiles dans AEM.

1. Ajouter un membre au groupe : Auteurs

   ![chlimage_1-167](assets/chlimage_1-167.png)

1. Maintenant que vous avez créé le groupe d’utilisateurs app-authors, vous pouvez ajouter des membres individuels de l’équipe à ce nouveau groupe par l’intermédiaire de la fonction [Admin Console utilisateur](http://localhost:4502/libs/granite/security/content/useradmin.md).

   ![chlimage_1-168](assets/chlimage_1-168.png)

1. Vous pouvez ajouter les éléments suivants au groupe d’auteurs de contenu AEM :

   (Lecture) activée

   * /app
   * /etc/clientlibs
   * /etc/designs
   * /etc/cloudservices/dps2015

### Groupe des administrateurs d’applications AEM Mobile (groupe app-admins) {#aem-mobile-application-administrators-group-app-admins-group}

Les membres du groupe app-admins peuvent créer du contenu d’application avec les mêmes autorisations que celles incluses avec app-authors. **ET** en outre, il est également chargé des tâches suivantes :

* Mise à jour OTA ContentSync de l’application intermédiaire, publication et effacement

>[!NOTE]
>
>Les autorisations déterminent la disponibilité de certaines actions de l’utilisateur dans le Centre de commandes des applications AEM.
>
>Notez que certaines options ne sont pas disponibles pour app-authors disponibles pour app-admins.

### Configuration de groupe - app-admins {#group-configuration-app-admins}

1. Créez un groupe appelé app-admins.
1. Ajoutez les groupes suivants à votre nouveau groupe app-admins :

   * auteurs de contenu
   * utilisateurs de workflow

   ![chlimage_1-169](assets/chlimage_1-169.png)

   >[!NOTE]
   >
   >workflow-users est requis pour la compilation à distance avec le service PhoneGap Build

1. Accédez au [Console Autorisations](http://localhost:4502/useradmin) et ajouter des autorisations pour administrer des services cloud

   * (Lecture, Modification, Création, Suppression, Réplication) sur /etc/cloudservices/mobilesservices

1. Dans la même console Autorisations, ajoutez des autorisations pour mettre à jour le contenu de l’application de manière intermédiaire, de publication et d’effacement.

   * (Lecture, Modification, Création, Suppression, Réplication) sur /etc/packages/mobileapp
   * (Lecture) sur /var/contentsync

   >[!NOTE]
   >
   >La réplication de package est utilisée pour publier les mises à jour d’application de l’instance d’auteur à l’instance de publication.

   >[!CAUTION]
   >
   >L’accès /var/contentsync est refusé en standard.
   >
   >Si vous omettez l’autorisation READ , les modules de mise à jour vides peuvent être créés et répliqués.

1. Ajoutez des membres à ce groupe selon les besoins.
1. Pour exporter du contenu ou le télécharger

   * (Lecture) sur /etc/contentsync pour accéder aux modèles d’exportation
   * (Lecture) sur /var pour la traversée du chemin en lecture
   * (Lecture, écriture, modification, suppression) sur /var/contentsync pour écrire, lire et nettoyer le contenu d’exportation mis en cache ContentSync

### Ressources supplémentaires {#additional-resources}

Pour en savoir plus sur les deux autres rôles et responsabilités dans la création d’une application AEM Mobile On-demand Services, consultez les ressources suivantes :

* [Développement de contenu AEM pour AEM Mobile On-demand Services](/help/mobile/aem-mobile-on-demand.md)
* [Création de contenu AEM pour l’application AEM Mobile On-demand Services](/help/mobile/mobile-apps-ondemand.md)
