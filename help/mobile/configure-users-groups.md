---
title: Configuration d’utilisateurs et de groupes d’utilisateurs
seo-title: Configuration d’utilisateurs et de groupes d’utilisateurs
description: Suivez cette page pour comprendre les rôles d’utilisateur et comment configurer vos utilisateurs et groupes afin de prendre en charge la création et la gestion de vos applications mobiles.
seo-description: Suivez cette page pour comprendre les rôles d’utilisateur et comment configurer vos utilisateurs et groupes afin de prendre en charge la création et la gestion de vos applications mobiles.
uuid: 55cea2b3-d7e6-4174-92b3-ee97e46b59c4
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: administering-adobe-phonegap-enterprise
discoiquuid: 167f3bd9-7dbc-4e6b-9868-3ee53935641b
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '666'
ht-degree: 51%

---


# Configuration d’utilisateurs et de groupes d’utilisateurs {#configure-your-users-and-user-groups}

>[!NOTE]
>
>Adobe recommande d’utiliser l’éditeur d’application d’une seule page (SPA) pour les projets nécessitant un rendu côté client basé sur la structure SPA (par exemple, React). [En savoir plus](/help/sites-developing/spa-overview.md).

Ce chapitre décrit les rôles utilisateur et comment configurer vos utilisateurs et groupes pour qu’ils prennent en charge la création et la gestion de vos applications mobiles.

## Utilisateurs de l’application AEM Mobile et administration des groupes {#aem-mobile-application-users-and-group-administration}

Pour aider à organiser et à gérer le modèle d’autorisation pour les applications AEM, les deux groupes suivants sont disponibles :

* administrateurs d’applications pour les administrateurs d’applications
* créateurs d’applications pour les auteurs d’applications

### Développeurs de contenu d’application AEM Mobile (groupe app-author) {#aem-mobile-application-content-authors-app-author-group}

Les membres du groupe d’auteurs d’applications sont chargés de créer AEM contenu d’applications mobiles, y compris des pages, du texte, des images et des vidéos.

#### Configuration du groupe - app-authors {#group-configuration-app-authors}

1. Créez un groupe d’utilisateurs appelé « app-authors » :

   Navigate to the User Admin Console: [http://localhost:4502/libs/granite/security/content/groupadmin.html](http://localhost:4502/libs/granite/security/content/groupadmin.html)

   Dans la console des groupes d’utilisateurs, sélectionnez le bouton « + » pour créer un groupe.

   Définissez l’ID de ce groupe sur « app-authors » pour indiquer qu’il s’agit d’un type précis de groupe d’utilisateurs-auteurs qui est spécifique au développement d’applications mobiles dans AEM.

1. Ajouter un membre au groupe : Auteurs

   ![chlimage_1-18](assets/chlimage_1-18.png)

   Ajouter les auteurs d’applications au groupe Auteurs

1. Maintenant que vous avez créé le groupe d’utilisateurs app-authors, vous pouvez lui ajouter d’autres membres dans la [console d’administration des utilisateurs](http://localhost:4502/libs/granite/security/content/useradmin.md).

   ![chlimage_1-19](assets/chlimage_1-19.png)

   Modifier des groupes d’utilisateurs

1. Navigate to the [Permissions console](http://localhost:4502/useradmin) and add permissions to administer cloudservices

   * (Lire) sur /etc/cloudservices
   >[!NOTE]
   >
   >Les auteurs d’applications étendent le groupe d’auteurs de contenu (auteurs) par défaut de l’AEM, héritant ainsi de la possibilité de créer du contenu sous /content/phonegap

### Groupe Administrateurs d’application AEM Mobile (groupe app-admins) {#aem-mobile-application-administrators-group-app-admins-group}

Members of the app-admins group can author application content with the same permissions included with app-authors **AND** in addition are also responsible for:

* La configuration des services cloud PhoneGap Build et Adobe Mobile Services dans AEM
* Mises à jour OTA de synchronisation de contenu de l’application d’évaluation, de publication et d’effacement

>[!NOTE]
>
>Les autorisations déterminent la disponibilité de certaines actions utilisateur dans le centre de commande d’applications AEM.
>
>Vous remarquerez que certaines options ne sont pas disponibles pour le groupe app-authors, mais le sont pour app-admins.

#### Configuration du groupe - app-admins {#group-configuration-app-admins}

1. Créez un groupe appelé app-admins.
1. Ajoutez les groupes suivants à votre nouveau groupe app-admins :

   * content-authors
   * workflow-users

   ![chlimage_1-20](assets/chlimage_1-20.png)

1. Navigate to the [Permissions console](http://localhost:4502/useradmin) and add permissions to administer cloudservices

   * (lire, modifier, créer, supprimer, répliquer) sur /etc/cloudservices/mobileservices
   * (lire, modifier, créer, supprimer, répliquer) sur /etc/cloudservices/phonegap-build

1. Dans la même console Permissions, ajoutez des autorisations pour l’affichage, la publication et l’effacement des mises à jour du contenu de l’application.

   * (lire, modifier, créer, supprimer, répliquer) sur /etc/packages/mobileapp
   * (lire) sur /var/contentsync

   >[!NOTE]
   >
   >La réplication de package sert à publier des mises à jour d’application de l’instance de création vers l’instance de publication

   >[!CAUTION]
   >
   >/var/contentsync est par défaut refusé.
   >
   >L’omission du droit en lecture peut entraîner la création et la réplication de packages de mise à jour vides.

1. Ajoutez des membres à ce groupe selon les besoins

## Autorisations de la mosaïque Tableau de bord {#dashboard-tile-permissions}

Les mosaïques Tableau de bord peuvent présenter différentes actions selon les droits de l’utilisateur. Le document suivant décrit les actions disponibles pour chaque mosaïque.

Outre ces autorisations, une action peut également être affichée/masquée selon la façon dont l’application est configurée. Par exemple, il n&#39;y a aucun intérêt à exposer l&#39;action &quot;Génération à distance&quot; si une configuration de cloud PhoneGap n&#39;a pas été affectée à l&#39;application. These will be listed below under &#39;**Configuration Condition**&#39; sections.

### Mosaïque Gestion de l’application {#manage-app-tile}

La mosaïque ne présente actuellement aucune action nécessitant des autorisations. Toutefois, la page de détails de l’application propose les actions suivantes:

* *Modification* pour app-author et app-admin (Déclencheur de l’interface utilisateur - jcr:write - on /content/phonegap/{suffix})
* *Téléchargement* pour app-author et app-admin (déclencheur de l’interface utilisateur - sur /content/phonegap/{suffix})

L’image ci-dessous présente les options de téléchargement et de modification pour une application :

![chlimage_1-21](assets/chlimage_1-21.png)

