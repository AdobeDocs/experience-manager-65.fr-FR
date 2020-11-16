---
title: Configuration d’utilisateurs et de groupes d’utilisateurs
seo-title: Configuration d’utilisateurs et de groupes d’utilisateurs
description: Suivez cette page pour comprendre les rôles d'utilisateur et comment configurer vos utilisateurs et groupes pour prendre en charge la création et la gestion de votre application de services à la demande mobile.
seo-description: Suivez cette page pour comprendre les rôles d'utilisateur et comment configurer vos utilisateurs et groupes pour prendre en charge la création et la gestion de votre application de services à la demande mobile.
uuid: 461e1725-41dd-4883-92b9-a7e175660401
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: administering-on-demand-services-app
discoiquuid: c3c73e67-7f85-4308-b4cd-1b42d4f3f2d9
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '549'
ht-degree: 53%

---


# Configuration d’utilisateurs et de groupes d’utilisateurs {#configure-your-users-and-user-groups}

>[!NOTE]
>
>Adobe recommande d’utiliser l’éditeur d’application d’une seule page (SPA) pour les projets nécessitant un rendu côté client basé sur la structure SPA (par exemple, React). [En savoir plus](/help/sites-developing/spa-overview.md).

Ce chapitre décrit les rôles utilisateur et comment configurer vos utilisateurs et groupes pour qu’ils prennent en charge la création et la gestion de vos applications mobiles.

## Utilisateurs de l’application AEM Mobile et administration des groupes {#aem-mobile-application-users-and-group-administration}

### Développeurs de contenu d’application AEM Mobile (groupe app-author) {#aem-mobile-application-content-authors-app-author-group}

Les membres du groupe d’auteurs d’applications sont chargés de créer AEM contenu d’applications mobiles, y compris des pages, du texte, des images et des vidéos.

#### Configuration du groupe - app-authors {#group-configuration-app-authors}

1. Créez un groupe d’utilisateurs appelé « app-authors » :

   Navigate to the User Admin Console: [http://localhost:4502/libs/granite/security/content/groupadmin.html](http://localhost:4502/libs/granite/security/content/groupadmin.html)

   Dans la console des groupes d’utilisateurs, sélectionnez le bouton « + » pour créer un groupe.

   Définissez l’ID de ce groupe sur « app-authors » pour indiquer qu’il s’agit d’un type précis de groupe d’utilisateurs-auteurs qui est spécifique au développement d’applications mobiles dans AEM.

1. Ajouter un membre au groupe : Auteurs

   ![chlimage_1-167](assets/chlimage_1-167.png)

1. Maintenant que vous avez créé le groupe d’utilisateurs app-authors, vous pouvez lui ajouter d’autres membres dans la [console d’administration des utilisateurs](http://localhost:4502/libs/granite/security/content/useradmin.md).

   ![chlimage_1-168](assets/chlimage_1-168.png)

1. Les éléments suivants vous permettent d’ajouter AEM groupe d’auteurs de contenu :

   (Lecture) sur

   * /propriétés d’objet
   * /etc/clientlibs
   * /etc/designs
   * /etc/cloudservices/dps2015

### Groupe Administrateurs d’application AEM Mobile (groupe app-admins) {#aem-mobile-application-administrators-group-app-admins-group}

Members of the app-admins group can author application content with the same permissions included with app-authors **AND** in addition are also responsible for:

* La mise à jour, la publication et la suppression des mises à jour ContentSync OTA d’application

>[!NOTE]
>
>Les autorisations déterminent la disponibilité de certaines actions utilisateur dans le centre de commande d’applications AEM.
>
>Vous remarquerez que certaines options ne sont pas disponibles pour le groupe app-authors, mais le sont pour app-admins.

### Configuration du groupe - app-admins {#group-configuration-app-admins}

1. Créez un groupe appelé app-admins.
1. Ajoutez les groupes suivants à votre nouveau groupe app-admins :

   * content-authors
   * workflow-users

   ![chlimage_1-169](assets/chlimage_1-169.png)

   >[!NOTE]
   >
   >Des autorisations workflow-users sont nécessaires pour la compilation à distance avec le service PhoneGap Build.

1. Navigate to the [Permissions console](http://localhost:4502/useradmin) and add permissions to administer cloudservices

   * (lire, modifier, créer, supprimer, répliquer) sur /etc/cloudservices/mobileservices

1. Dans la console Autorisations, ajoutez des autorisations pour mettre en attente, modifier et supprimer les mises à jour du contenu de l’application,

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
1. Pour exporter du contenu ou le télécharger

   * (Lecture) sur /etc/contentsync pour accéder aux modèles d&#39;exportation
   * (Lecture) sur /var à pour la traversée de chemin en lecture
   * (Lu, Écrire, Modifier, Supprimer) sur /var/contentsync pour écrire, lire et nettoyer le contenu d’exportation en mémoire cache de ContentSync

### Ressources supplémentaires {#additional-resources}

Pour en savoir plus sur les deux autres rôles et responsabilités de création d’une application AEM Mobile On-demand Services, consultez les ressources suivantes :

* [Développement de contenu AEM pour AEM Mobile On-demand Services](/help/mobile/aem-mobile-on-demand.md)
* [Création de contenu AEM pour une application AEM Mobile On-demand Services](/help/mobile/mobile-apps-ondemand.md)
