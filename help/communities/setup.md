---
title: Configuration initiale
seo-title: Configuration initiale
description: Configuration des communautés
seo-description: Configuration des communautés
uuid: c53d280c-c5ae-47cf-8038-f0dea68e15ff
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: introduction
content-type: reference
discoiquuid: 0d462ad1-5619-4bb6-9609-bc8987c40a0c
translation-type: tm+mt
source-git-commit: f375b40c084ee363757b78c602091f38524b8b03
workflow-type: tm+mt
source-wordcount: '697'
ht-degree: 2%

---


# Configuration initiale {#initial-setup}

## Instances d’auteur et de publication de début {#start-author-and-publish-instances}

À des fins de développement et de démonstration, il sera nécessaire d’exécuter une instance d’auteur et une instance de publication.

Pour ce faire, suivez les instructions de base AEM [Prise en main](../../help/sites-deploying/deploy.md#getting-started) , qui se traduiront par :

* Environnement de l’auteur sur [localhost:4502](http://localhost:4502/)
* Publier l’environnement sur [localhost:4503](http://localhost:4503/)

Pour AEM Communities,

* L&#39;environnement de l&#39;auteur est destiné à :

   * Développement de sites, de modèles et de composants.
   * Tâches d’administration et de configuration.

* L’environnement de publication est destiné à :

   * Expérience de la communauté à publier et modérer du contenu.
   * Créer des groupes communautaires, des membres et des groupes de membres.

>[!NOTE]
>
>If not familiar with AEM, view the documentation on [basic handling](../../help/sites-authoring/basic-handling.md) and a [quick guide to authoring pages](../../help/sites-authoring/qg-page-authoring.md).

## Installer la dernière version des communautés {#install-latest-communities-release}

Ce didacticiel crée un site [communautaire d’](overview.md#engagement-community) engagement et est basé sur AEM Communities 6.2 Feature Pack version 1.10.

Pour vous assurer que le dernier Feature Pack est installé, visitez :

* [Dernières versions](deploy-communities.md#latest-releases)

Pour consulter un didacticiel qui crée un site [communautaire d’](overview.md#enablement-community)activation, consultez [Prise en main de AEM Communities pour l’activation](getting-started-enablement.md).

## Configuration de Analytics {#configure-analytics}

Lorsque [Adobe Analytics est configuré pour le site](analytics.md)communautaire, des informations sur l&#39;activité de la communauté sont disponibles, ce qui améliore l&#39;expérience des membres de la communauté et fournit des commentaires aux administrateurs du site.

L’intégration à Adobe Analytics est facultative.

## Configurer le courrier électronique pour les notifications {#configure-email-for-notifications}

La fonction de notifications, disponible par défaut pour tous les sites créés à l’aide de la `Communities Sites` console, fournit un canal électronique pour les notifications.

Il est nécessaire que le courrier électronique soit correctement configuré pour le site.

See [Configuring Email](email.md).

## Activation du service de tunnel {#enable-the-tunnel-service}

Lors de la création d’un site communautaire dans l’environnement d’auteur, le service tunnel permet d’attribuer des rôles aux membres de la communauté de confiance enregistrés dans l’environnement de publication. Le service tunnel permet également d&#39;accéder aux membres de la communauté à partir des consoles [](members.md) Membres et Groupes de l&#39;environnement auteur.

La convention permet aux membres et aux groupes de membres créés dans l’environnement de publication de *ne pas* être recréés dans l’environnement d’auteur. For more information see [Managing Users and User Groups](users.md).

Pour obtenir des instructions simples sur l’activation du service de tunnel sur une instance d’ **auteur** , voir Service [de](deploy-communities.md#tunnel-service-on-author)tunnel.

## Rôle Administrateur de la communauté {#community-administrator-role}

Les membres du groupe Administrateurs de la communauté peuvent créer des sites communautaires, gérer des sites, gérer des membres (ils peuvent interdire les membres de la communauté) et modérer le contenu.

### Créer un utilisateur {#create-user}

Créez un utilisateur sur *l’auteur*, auquel est affecté le rôle Administrateur de la communauté :

* Sur l’instance d’auteur

   * For example, [http://localhost:4502/](http://localhost:4503/)

* Connexion avec droits d’administrateur

   * Par exemple, nom d’utilisateur &quot;admin&quot; / mot de passe &quot;admin&quot;

* Dans la console principale, accédez à **[!UICONTROL Outils]** > **[!UICONTROL Opérations]** > **[!UICONTROL Sécurité]** > **[!UICONTROL Utilisateurs.]**
* Dans le menu **Modifier** , sélectionnez **[!UICONTROL Ajouter un utilisateur.]**

* Dans la `Create New User` boîte de dialogue, saisissez :

   * **[!UICONTROL ID]**: sirius
   * **[!UICONTROL Adresse]**&#x200B;électronique : sirius.nilson@mailinator.com
   * **[!UICONTROL Mot de passe]** : password
   * **[!UICONTROL Confirmer le mot de passe&amp;ast;]**: password
   * **[!UICONTROL Prénom]**: Sirius
   * **[!UICONTROL Nom]**: Nilson

### Affecter le sirius au groupe Administrateurs de la communauté {#assign-sirius-to-community-administrators-group}

Faites défiler la page jusqu&#39;à `Add User to Groups`:

* Entrer &quot;C&quot; pour effectuer la recherche

   * Sélectionner `Community Administrators`
   * Sélectionner `Community Enablement Managers`

* Sélectionnez **[!UICONTROL Enregistrer]**.

![create-user](assets/create-user.png)

## Activer la connexion aux réseaux sociaux {#enable-social-login}

Avant de pouvoir utiliser les versions de démonstration de la connexion sociale avec Facebook et Twitter, il est nécessaire de

1. Installez un pack de correctifs ou le [dernier pack de fonctionnalités](deploy-communities.md#latestfeaturepack) (pour les modifications apportées à l’API Facebook en mars 2017).
1. [Activez le fournisseur](social-login.md#adobe-granite-oauth-authentication-handler) OAuth dans l’environnement de publication.

Pour les serveurs de production, il est nécessaire de créer les services cloud nécessaires pour fournir une connexion sociale.

Voir Connexion [aux réseaux sociaux avec Facebook et Twitter](social-login.md).

## Création de balises de didacticiel {#create-tutorial-tags}

Créez des balises à utiliser pour les didacticiels d’interaction et d’activation, à l’aide de l’espace de nommage de balises de `Tutorial`.

Utilisez la console [](../../help/sites-administering/tags.md#tagging-console) Balisage pour créer les balises suivantes :

* `Tutorial: Sports / Baseball`
* `Tutorial: Sports / Gymnastics`
* `Tutorial: Sports / Skiing`
* `Tutorial: Arts / Visual`
* `Tutorial: Arts / Auditory`
* `Tutorial: Arts / History`

![tutorial-tags](assets/tutorial-tags.png)

Suivez ensuite les instructions pour :

1. [Définissez les autorisations](../../help/sites-administering/tags.md#setting-tag-permissions)de balise.
1. [Publiez les balises](../../help/sites-administering/tags.md#publishing-tags).

Exemple de package de balises créées pour les Tutorials de prise en main AEM Communities

[Obtenir le fichier](assets/tutorial_tags-v63.zip)

## MongoDB pour le magasin commun UGC {#mongodb-for-ugc-common-store}

Il est recommandé, mais facultatif, de définir [MSRP](msrp.md) (MongoDB) comme magasin [](working-with-srp.md) commun afin de pouvoir modérer tous les UGC des environnements de publication et/ou d’auteur.

Pour obtenir des instructions, consultez [Comment configurer MongoDB pour la démonstration](demo-mongo.md).

Par défaut, l’installation des instances d’auteur et de publication AEM le contenu généré par l’utilisateur (UGC) est stocké dans l’enregistrement [Tar](../../help/sites-deploying/platform.md) JCR accessible à l’aide de [JSRP](jsrp.md). JSRP n’est pas un magasin courant, ce qui signifie que l’UGC n’est visible que sur l’instance sur laquelle il a été saisi. En règle générale, l’UGC est saisi sur une instance de publication et n’est pas visible dans l’environnement d’auteur, de sorte que toutes les tâches de modération doivent utiliser l’instance de publication.