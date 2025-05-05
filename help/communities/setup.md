---
title: Configuration initiale
description: Découvrez comment configurer initialement Adobe Experience Manager Communities.
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: introduction
content-type: reference
exl-id: 6bda0f09-7ae5-4540-b035-9dd249ac3186
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '684'
ht-degree: 2%

---

# Configuration initiale {#initial-setup}

## Démarrage des instances de création et de Publish {#start-author-and-publish-instances}

À des fins de développement et de démonstration, il est nécessaire d’exécuter une instance de création et une instance de publication.

Pour ce faire, suivez les instructions de base de Adobe Experience Manager (AEM) [Prise en main](../../help/sites-deploying/deploy.md#getting-started) , qui se traduisent par ce qui suit :

* Environnement de création sur [localhost:4502](http://localhost:4502/)
* Environnement Publish sur [localhost:4503](http://localhost:4503/)

Pour AEM Communities,

* L’environnement de création est destiné à :

   * Développement de sites, modèles et composants.
   * Tâches administratives et de configuration.

* L’environnement Publish est destiné à :

   * Expérience de la communauté à publier et modérer du contenu.
   * Création de groupes communautaires, de membres et de groupes de membres.

>[!NOTE]
>
>Si vous ne connaissez pas AEM, consultez la documentation sur la [gestion de base](../../help/sites-authoring/basic-handling.md) et un [ guide rapide sur la création de pages](../../help/sites-authoring/qg-page-authoring.md).

## Installation de la dernière version de Communities {#install-latest-communities-release}

Ce tutoriel crée un [site de la communauté d’engagement](overview.md#engagement-community) et est basé sur AEM Communities 6.2 Feature Pack version 1.10.

Pour vous assurer que le dernier Feature Pack est installé, rendez-vous sur :

* [Dernières versions](deploy-communities.md#latest-releases)

## Configurer Analytics {#configure-analytics}

Lorsque [Adobe Analytics est configuré pour le site de la communauté](analytics.md), des informations sur l’activité de la communauté sont disponibles, qui améliorent l’expérience du membre de la communauté et fournissent des commentaires aux administrateurs du site.

L’intégration à Adobe Analytics est facultative.

## Configuration du courrier électronique pour les notifications {#configure-email-for-notifications}

La fonctionnalité de notifications, disponible par défaut pour tous les sites créés à l’aide de la console `Communities Sites`, fournit un canal de courrier électronique pour les notifications.

Il est nécessaire de configurer correctement les emails pour le site.

Voir [Configuration du courrier électronique](email.md).

## Activation du service Tunnel {#enable-the-tunnel-service}

Lors de la création d’un site de communauté dans l’environnement de création, le service tunnel permet d’affecter des rôles aux membres de communauté approuvés enregistrés dans l’environnement Publish. Le service tunnel permet également d’accéder aux membres de la communauté à partir des [consoles Membres et Groupes](members.md) dans l’environnement de création.

La convention est destinée aux membres et aux groupes de membres créés dans l’environnement Publish pour *et non* être recréés dans l’environnement de création. Pour plus d’informations, voir [Gestion des utilisateurs et des groupes d’utilisateurs](users.md).

Pour obtenir des instructions simples afin d’activer le service de tunnel sur une instance **Author**, voir [service de tunnel](deploy-communities.md#tunnel-service-on-author).

## Rôle d’administrateur de la communauté {#community-administrator-role}

Les membres du groupe Administrateurs de la communauté peuvent créer des sites de la communauté, gérer les sites, gérer les membres (ils peuvent interdire les membres de la communauté) et modérer le contenu.

### Créer un utilisateur {#create-user}

Créez un utilisateur sur *author*, auquel est affecté le rôle d’administrateur de la communauté :

* Sur l’instance d’auteur

   * Par exemple, [http://localhost:4502/](http://localhost:4503/)

* Connexion avec droits d’administrateur

   * Par exemple, nom d’utilisateur &quot;admin&quot; / mot de passe &quot;admin&quot;

* Dans la console principale, accédez à **[!UICONTROL Outils]** > **[!UICONTROL Opérations]** > **[!UICONTROL Sécurité]** > **[!UICONTROL Utilisateurs]**.
* Dans le menu **Modifier**, sélectionnez **[!UICONTROL Ajouter un utilisateur]**

* Dans la boîte de dialogue `Create New User`, saisissez :

   * **[!UICONTROL ID]** : sirius
   * **[!UICONTROL Adresse électronique]** : sirius.nilson@mailinator.com
   * **[!UICONTROL Mot de passe]** : password
   * **[!UICONTROL Confirmer le mot de passe&ast;]** : password
   * **[!UICONTROL Prénom]** : Sirius
   * **[!UICONTROL Nom]** : Nilson

### Affecter Sirius au groupe Administrateurs de la communauté {#assign-sirius-to-community-administrators-group}

Faites défiler l’écran jusqu’à `Add User to Groups` :

* Saisissez &quot;C&quot; pour effectuer la recherche.

   * Sélectionnez `Community Administrators`.
   * Sélectionnez `Community Enablement Managers`.

* Sélectionnez **[!UICONTROL Enregistrer]**.

![create-user](assets/create-user.png)

## Activation de la connexion aux réseaux sociaux {#enable-social-login}

Avant de pouvoir utiliser des versions de démonstration de la connexion sociale avec Facebook et Twitter, il est nécessaire de

1. Installez un pack de correctifs ou le [dernier pack de fonctionnalités](deploy-communities.md#latestfeaturepack) (pour les modifications de l’API Facebook de mars 2017).
1. [Activez le fournisseur OAuth](social-login.md#adobe-granite-oauth-authentication-handler) dans l’environnement de publication.

Pour les serveurs de production, il est nécessaire de créer les services cloud nécessaires pour fournir une connexion sociale.

Voir [Connexion sociale avec Facebook et Twitter](social-login.md).

## Créer des balises de tutoriel {#create-tutorial-tags}

Créez des balises pour pouvoir les utiliser pour les tutoriels d’engagement, à l’aide de l’espace de noms de balise `Tutorial`.

Utilisez la [console Balisage](../../help/sites-administering/tags.md#tagging-console) pour créer les balises suivantes :

* `Tutorial: Sports / Baseball`
* `Tutorial: Sports / Gymnastics`
* `Tutorial: Sports / Skiing`
* `Tutorial: Arts / Visual`
* `Tutorial: Arts / Auditory`
* `Tutorial: Arts / History`

![tutorial-tags](assets/tutorial-tags.png)

Suivez ensuite les instructions pour :

1. [Définissez les autorisations de balise](../../help/sites-administering/tags.md#setting-tag-permissions).
1. [Publish les balises](../../help/sites-administering/tags.md#publishing-tags).

Exemple de package de balises créées pour les Tutorials de prise en main d’AEM Communities

[Obtenir le fichier](assets/tutorial_tags-v63.zip)

## MongoDB pour le magasin commun UGC {#mongodb-for-ugc-common-store}

Il est recommandé, mais facultatif, de définir [MSRP](msrp.md) (MongoDB) comme [ boutique commune](working-with-srp.md) afin de bénéficier de la flexibilité de modération de tous les UGC dans les environnements de publication et/ou de création.

Pour plus d’informations, voir [Comment configurer MongoDB pour la démonstration](demo-mongo.md).

Par défaut, l’installation des instances d’AEM de création et de publication entraîne le stockage du contenu généré par l’utilisateur dans le [stockage Tar JCR](../../help/sites-deploying/platform.md), accessible à l’aide de [JSRP](jsrp.md). JSRP n’est pas un magasin courant, ce qui signifie que le contenu créé par l’utilisateur n’est visible que sur l’instance sur laquelle il a été saisi. En règle générale, le contenu généré par l’utilisateur est saisi sur une instance de publication et ne sera pas visible dans l’environnement de création, ce qui entraîne la nécessité pour toutes les tâches de modération d’utiliser l’instance de publication.
