---
title: Tableau de bord des applications AEM Mobile
description: Vous pouvez gérer le contenu de votre application et de votre application mobile à partir du tableau de bord de l’application AEM Mobile ou du centre de contrôle. Consultez cette page pour en savoir plus.
contentOwner: User
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/MOBILE
topic-tags: authoring-on-demand-services-app
exl-id: daafc8b8-3c01-4c97-a14b-f1b706600249
solution: Experience Manager
feature: Mobile
role: User
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '603'
ht-degree: 9%

---

# Tableau de bord des applications AEM Mobile {#aem-mobile-application-dashboard}

>[!NOTE]
>
>Adobe recommande d’utiliser l’éditeur SPA pour les projets nécessitant un rendu côté client, basé sur un framework, pour une application à une seule page (comme React). [En savoir plus](/help/sites-developing/spa-overview.md).

Vous pouvez gérer le contenu de votre application et de votre application mobile à partir du tableau de bord de l’application AEM Mobile ou du centre de contrôle.

Vous pouvez parcourir chaque mosaïque du Centre de contrôle pour afficher ou modifier les détails en cliquant sur &quot;...&quot; dans le coin inférieur droit.

![chlimage_1-54](assets/chlimage_1-54.png)

>[!NOTE]
>
>Vous pouvez réorganiser l’ordre des mosaïques en cliquant sur l’icône de capture de la mosaïque (9 points en haut à gauche). Le changement de commande est spécifique à l’utilisateur, différent pour les utilisateurs individuels.

La gestion du contenu des applications nécessite un effort collectif des développeurs, des auteurs de contenu et des administrateurs. Les auteurs manipulent les pages, qui sont à leur tour basées sur des modèles et des composants générés par les développeurs d’applications.

Enfin, les administrateurs publient stratégiquement le contenu de l’application mis à jour.

## Mosaïque Gérer l’application {#the-manage-app-tile}

La mosaïque **Gérer l’application** affiche les informations d’application disponibles :

* Titre
* Description
* Icône
* Date de dernière modification
* Dernière modification par

![chlimage_1-55](assets/chlimage_1-55.png)

## Mosaïque Gérer la connexion {#the-manage-connection-tile}

La mosaïque **Gérer la connexion** affiche les informations de connexion AEM Mobile On-demand Services :

* Nom de la configuration de la publicité
* Nom et identifiant du projet
* État de la connexion

>[!NOTE]
>
>Cliquez sur l’engrenage en haut à droite pour configurer une configuration cloud Mobile On-Demand.
>
>Voir [Configuration de Mobile On-Demand Services](/help/mobile/mobile-on-demand-associating-an-on-demand-app-to-cloud-configuration.md) pour plus d’informations.

![chlimage_1-56](assets/chlimage_1-56.png)

## Gestion des entités {#managing-entities}

Ces trois mosaïques fournissent un aperçu de l’état du contenu d’une application :

* **bannières**
* **articles**
* **collections**

Chaque mosaïque peut être développée pour fournir une vue de liste plus détaillée en cliquant sur les points de suspension (..) dans le coin inférieur droit. Ces vues de liste offrent un autre moyen d’accéder aux actions courantes de Mobile On Demand, telles que la suppression, le chargement et la modification des propriétés.

### Mosaïque Gestion des bannières {#the-manage-banners-tile}

La mosaïque **Gérer les bannières** vous permet de gérer le contenu d’une bannière. Les informations suivantes s’affichent pour une bannière :

* image
* **TITLE** : nom de la bannière
* **MODIFIED** : dernière modification dans AEM
* **UPLOADED** : dernier téléchargé à partir d’AEM
* **PUBLISHED** : dernier formulaire de demande publié AEM
* **SOURCE** : source (AEM locale ou distante de Mobile On Demand)

L’image suivante montre la mosaïque **Gérer les bannières** dans le tableau de bord de l’application AEM Mobile :

![chlimage_1-57](assets/chlimage_1-57.png)

>[!NOTE]
>
>Voir **[Gestion des bannières](/help/mobile/mobile-on-demand-managing-banners.md)** pour créer, supprimer ou mettre à jour les bannières.

### Mosaïque Gestion des articles {#the-manage-articles-tile}

La mosaïque **Gérer les articles** vous permet de gérer le contenu d’un article. Les informations suivantes s’affichent pour un article :

* image
* **TITLE** : nom de l’article
* **MODIFIED** : dernière modification dans AEM
* **UPLOADED** : dernier téléchargé à partir d’AEM
* **PUBLISHED** : dernier formulaire de demande publié AEM
* **SOURCE** : source (AEM locale ou distante de Mobile On Demand)

L’image suivante montre la mosaïque **Gérer les articles** dans le tableau de bord de l’application AEM Mobile :

![chlimage_1-58](assets/chlimage_1-58.png)

>[!NOTE]
>
>Voir [**Gestion des articles**](/help/mobile/mobile-on-demand-managing-articles.md) pour créer, supprimer ou mettre à jour des articles.

### Mosaïque Gérer les collections {#the-manage-collections-tile}

La mosaïque **Gérer les collections** vous permet de gérer le contenu d’une collection. Les informations suivantes s’affichent pour une collection :

* image
* **TITLE** : nom de la collection
* **MODIFIED** : dernière modification dans AEM
* **UPLOADED** : dernier téléchargé à partir d’AEM
* **PUBLISHED** : dernier formulaire de demande publié AEM
* **SOURCE** : source (AEM locale ou distante de Mobile On Demand)

L’image suivante montre la mosaïque **Gérer les collections** dans le tableau de bord de l’application AEM Mobile :

![chlimage_1-59](assets/chlimage_1-59.png)

>[!NOTE]
>
>Voir **[Gestion des collections](/help/mobile/mobile-on-demand-managing-collections.md)** pour créer, supprimer ou mettre à jour des collections.

### Les étapes suivantes {#the-next-steps}

Une fois que vous connaissez le tableau de bord de l’application, consultez les ressources suivantes pour créer une application mobile :

* [Actions de création et de configuration d’application](/help/mobile/mobile-apps-ondemand-application-create-configure-action.md)
* [Association d’une application On-Demand à une configuration cloud](/help/mobile/mobile-on-demand-associating-an-on-demand-app-to-cloud-configuration.md)
* [Actions de gestion de contenu](/help/mobile/mobile-apps-ondemand-manage-content-ondemand.md)

### Ressources supplémentaires {#additional-resources}

Pour en savoir plus sur les rôles et les responsabilités d’un administrateur et d’un développeur, consultez les ressources ci-dessous :

* [Développement de contenu AEM pour AEM Mobile On-demand Services](/help/mobile/aem-mobile-on-demand.md)
* [Administration de contenu pour l’utilisation d’AEM Mobile On-demand Services](/help/mobile/aem-mobile.md)
