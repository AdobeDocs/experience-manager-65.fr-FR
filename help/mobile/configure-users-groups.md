---
title: Configuration des utilisateurs et des groupes d’utilisateurs
description: Consultez cette page pour comprendre les rôles utilisateur et comment configurer vos utilisateurs et groupes afin de prendre en charge la création et la gestion de vos applications mobiles.
uuid: 55cea2b3-d7e6-4174-92b3-ee97e46b59c4
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: administering-adobe-phonegap-enterprise
discoiquuid: 167f3bd9-7dbc-4e6b-9868-3ee53935641b
exl-id: 9f814204-8cd4-4ba9-9e25-3ff1b25c1955
source-git-commit: f4b6eb2ded17ec641f23a1fc3b977ce77169c8a1
workflow-type: tm+mt
source-wordcount: '633'
ht-degree: 3%

---

# Configuration des utilisateurs et des groupes d’utilisateurs {#configure-your-users-and-user-groups}

>[!NOTE]
>
>Adobe recommande d’utiliser l’éditeur d’application d’une seule page (SPA) pour les projets nécessitant un rendu côté client basé sur la structure SPA (par exemple, React). [En savoir plus](/help/sites-developing/spa-overview.md).

Ce chapitre décrit les rôles utilisateur et comment configurer vos utilisateurs et groupes pour prendre en charge la création et la gestion de vos applications mobiles.

## Utilisateurs des applications AEM Mobile et administration des groupes {#aem-mobile-application-users-and-group-administration}

Pour organiser et gérer le modèle d’autorisation pour les applications AEM, les deux groupes suivants sont disponibles :

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

1. Maintenant que vous avez créé le groupe d’utilisateurs app-authors, vous pouvez ajouter des membres individuels de l’équipe à ce nouveau groupe par l’intermédiaire de la fonction [Console d’administration des utilisateurs](http://localhost:4502/libs/granite/security/content/useradmin.md).

   ![chlimage_1-19](assets/chlimage_1-19.png)

   Modification des groupes d’utilisateurs

1. Accédez au [Console Autorisations](http://localhost:4502/useradmin) et ajouter des autorisations pour administrer des services cloud

   * (Lecture) sur /etc/cloudservices
   >[!NOTE]
   >
   >Les auteurs d’applications étendent le groupe content-authors (Auteurs) par défaut à partir d’AEM héritant ainsi de la possibilité de créer du contenu sous /content/phonegap

### Groupe des administrateurs d’applications AEM Mobile (groupe app-admins) {#aem-mobile-application-administrators-group-app-admins-group}

Les membres du groupe app-admins peuvent créer du contenu d’application avec les mêmes autorisations que celles incluses avec app-authors. **ET** en outre, il est également chargé des tâches suivantes :

* Configuration des services cloud PhoneGap Build et Adobe Mobile Services dans AEM
* Mises à jour OTA de synchronisation de contenu d’application intermédiaire, de publication et d’effacement

>[!NOTE]
>
>Les autorisations déterminent la disponibilité de certaines actions de l’utilisateur dans le Centre de commandes des applications AEM.
>
>Vous remarquerez que certaines options ne sont pas disponibles pour les créateurs d’applications disponibles pour les administrateurs d’applications.

#### Configuration de groupe - app-admins {#group-configuration-app-admins}

1. Créez un groupe appelé app-admins.
1. Ajoutez les groupes suivants à votre nouveau groupe app-admins :

   * content-authors
   * utilisateurs de workflow

   ![chlimage_1-20](assets/chlimage_1-20.png)

1. Accédez au [Console Autorisations](http://localhost:4502/useradmin) et ajouter des autorisations pour administrer des services cloud

   * (Lecture, Modification, Création, Suppression, Réplication) sur /etc/cloudservices/mobilesservices
   * (Lecture, modification, création, suppression, réplication) sur /etc/cloudservices/phonegap-build

1. Dans la même console Autorisations, ajoutez des autorisations pour mettre en scène, publier et effacer les mises à jour du contenu de l’application.

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

## Autorisations de mosaïque pour les tableaux de bord {#dashboard-tile-permissions}

Les mosaïques du tableau de bord peuvent afficher différentes actions en fonction des autorisations dont dispose l’utilisateur. La section suivante décrit les actions disponibles pour chaque mosaïque.

Outre ces autorisations, une action peut également être affichée/masquée en fonction de la configuration de l’application active. Par exemple, il n’y a aucun intérêt à exposer l’action &quot;Génération à distance&quot; si une configuration de cloud PhoneGap n’a pas été affectée à l’application. Elles seront répertoriées ci-dessous sous &quot;&quot;.**Condition de configuration** sections &quot;.

### Mosaïque Gérer l’application {#manage-app-tile}

La mosaïque ne comporte actuellement aucune action nécessitant des autorisations. Toutefois, la page de détails de l’application comporte les actions suivantes :

* *Modifier* pour app-author et app-admin (interface utilisateur Trigger - jcr:write - sur /content/phonegap/{suffix})
* *Télécharger* pour app-author et app-admin (Déclencheur d’interface utilisateur - sur /content/phonegap/{suffix})

L’image ci-dessous présente les options Télécharger et Modifier d’une application :

![chlimage_1-21](assets/chlimage_1-21.png)
