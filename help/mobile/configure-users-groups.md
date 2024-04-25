---
title: Configuration des utilisateurs et des groupes d’utilisateurs
description: Consultez cette page pour comprendre les rôles utilisateur et comment configurer vos utilisateurs et groupes afin de prendre en charge la création et la gestion de vos applications mobiles.
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: administering-adobe-phonegap-enterprise
exl-id: 9f814204-8cd4-4ba9-9e25-3ff1b25c1955
solution: Experience Manager
feature: Mobile
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '614'
ht-degree: 5%

---

# Configuration des utilisateurs et des groupes d’utilisateurs {#configure-your-users-and-user-groups}

>[!NOTE]
>
>Adobe recommande d’utiliser l’éditeur SPA pour les projets nécessitant un rendu côté client, basé sur un framework, pour une application à une seule page (comme React). [En savoir plus](/help/sites-developing/spa-overview.md).

Ce chapitre décrit les rôles utilisateur et comment configurer vos utilisateurs et groupes pour prendre en charge la création et la gestion de vos applications mobiles.

## Utilisateurs des applications AEM Mobile et administration des groupes {#aem-mobile-application-users-and-group-administration}

Pour vous aider à organiser et à gérer le modèle d’autorisation pour les applications AEM, les deux groupes suivants sont disponibles :

* app-admins pour les administrateurs d’applications
* app-authors pour les auteurs d’applications

### Auteurs de contenu d’application AEM Mobile (groupe app-author) {#aem-mobile-application-content-authors-app-author-group}

Les membres du groupe app-author sont chargés de la création AEM contenu de l’application mobile, y compris les pages, le texte, les images et les vidéos.

#### Configuration de groupe - app-authors {#group-configuration-app-authors}

1. Créez un groupe d’utilisateurs appelé &quot;app-authors&quot; :

   Accédez au Admin Console utilisateur : [http://localhost:4502/libs/granite/security/content/groupadmin.html](http://localhost:4502/libs/granite/security/content/groupadmin.html)

   Dans la console du groupe d’utilisateurs, cliquez sur le bouton &quot;+&quot; pour créer un groupe.

   Définissez l’identifiant de ce groupe sur &quot;app-authors&quot; pour indiquer qu’il s’agit d’un type spécifique de groupe d’utilisateurs de création spécifique à la création d’applications mobiles dans AEM.

1. Ajouter un membre au groupe : Auteurs

   ![chlimage_1-18](assets/chlimage_1-18.png)

   Ajouter app-authors au groupe Auteurs

1. Maintenant que vous avez créé le groupe d’utilisateurs app-authors, vous pouvez ajouter des membres individuels de l’équipe à ce nouveau groupe par l’intermédiaire de la fonction [Admin Console utilisateur](http://localhost:4502/libs/granite/security/content/useradmin.md).

   ![chlimage_1-19](assets/chlimage_1-19.png)

   Modification des groupes d’utilisateurs

1. Accédez au [Console Autorisations](http://localhost:4502/useradmin) et ajouter des autorisations pour administrer des services cloud

   * (Lecture) sur /etc/cloudservices

   >[!NOTE]
   >
   >Les auteurs d’applications étendent le groupe content-authors (Auteurs) par défaut à partir d’AEM, de sorte qu’ils héritent de la possibilité de créer du contenu sous /content/phonegap

### Groupe des administrateurs d’applications AEM Mobile (groupe app-admins) {#aem-mobile-application-administrators-group-app-admins-group}

Les membres du groupe app-admins peuvent créer du contenu d’application avec les mêmes autorisations que celles incluses avec app-authors. **ET** en outre, il est également chargé des tâches suivantes :

* Configuration des services cloud PhoneGap Build et Adobe Mobile Services dans AEM
* Mise à jour OTA de synchronisation de contenu d’application intermédiaire, publication et effacement

>[!NOTE]
>
>Les autorisations déterminent la disponibilité de certaines actions de l’utilisateur dans le Centre de commandes des applications AEM.
>
>Notez que certaines options ne sont pas disponibles pour app-authors disponibles pour app-admins.

#### Configuration de groupe - app-admins {#group-configuration-app-admins}

1. Créez un groupe appelé app-admins.
1. Ajoutez les groupes suivants à votre nouveau groupe app-admins :

   * auteurs de contenu
   * utilisateurs de workflow

   ![chlimage_1-20](assets/chlimage_1-20.png)

1. Accédez au [Console Autorisations](http://localhost:4502/useradmin) et ajouter des autorisations pour administrer des services cloud

   * (Lecture, Modification, Création, Suppression, Réplication) sur /etc/cloudservices/mobilesservices
   * (Lecture, modification, création, suppression, réplication) sur /etc/cloudservices/phonegap-build

1. Dans la même console Autorisations, ajoutez des autorisations pour mettre à jour le contenu de l’application de manière intermédiaire, de publication et d’effacement.

   * (Lecture, Modification, Création, Suppression, Réplication) sur /etc/packages/mobileapp
   * (Lecture) sur /var/contentsync

   >[!NOTE]
   >
   >La réplication de package est utilisée pour publier les mises à jour d’application de l’instance d’auteur à l’instance de publication.

   >[!CAUTION]
   >
   >/var/contentsync est refusé d’usine.
   >
   >Si vous omettez l’autorisation READ , les modules de mise à jour vides peuvent être créés et répliqués.

1. Ajoutez des membres à ce groupe selon les besoins.

## Autorisations de mosaïque pour les tableaux de bord {#dashboard-tile-permissions}

Les mosaïques du tableau de bord peuvent afficher différentes actions en fonction des autorisations dont dispose l’utilisateur. La section suivante décrit les actions disponibles pour chaque mosaïque.

Outre ces autorisations, une action peut également être affichée/masquée en fonction de la configuration de l’application active. Par exemple, il n’y a aucun intérêt à exposer l’action &quot;Génération à distance&quot; si une configuration de cloud PhoneGap n’a pas été affectée à l’application. Ils sont répertoriés ci-dessous sous &quot;&quot;**Condition de configuration** sections &quot;.

### Mosaïque Gérer l’application {#manage-app-tile}

La mosaïque ne comporte actuellement aucune action nécessitant des autorisations. Toutefois, la page de détails de l’application comporte les actions suivantes :

* *Modifier* pour app-author et app-admin (déclencheur d’interface utilisateur - jcr:write - sur /content/phonegap/{suffix})
* *Télécharger* pour app-author et app-admin (Déclencheur d’interface utilisateur - sur /content/phonegap/{suffix})

L’image ci-dessous présente les options Télécharger et Modifier d’une application :

![chlimage_1-21](assets/chlimage_1-21.png)
