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
source-git-commit: 6d425dcec4fab19243be9acb41c25b531a84ea74

---


# Configuration initiale {#initial-setup}

## Start Author and Publish Instances {#start-author-and-publish-instances}

À des fins de développement et de démonstration, il sera nécessaire d’exécuter une instance d’auteur et une instance de publication.

Pour ce faire, suivez les instructions de base de [prise en main](../../help/sites-deploying/deploy.md#getting-started) d’AEM, qui se traduiront par :

* Auteur   sur [localhost:4502](http://localhost:4502/)
* Publier   sur [localhost:4503](http://localhost:4503/)

Pour les communautés AEM,

* L&#39;auteur   est pour :

   * Développement de sites, de modèles et de composants.
   *  d’administration et de configuration.

*  de publication  pour :

   * Expérience communautaire de publication et de modération de contenu.
   * Création de groupes communautaires, de membres et de groupes de membres.

>[!NOTE]
>
>If not familiar with AEM, view the documentation on [basic handling](../../help/sites-authoring/basic-handling.md) and a [quick guide to authoring pages](../../help/sites-authoring/qg-page-authoring.md).


## Installer la dernière version des communautés {#install-latest-communities-release}

Ce didacticiel crée un site [communautaire d’](overview.md#engagement-community) engagement et est basé sur la version 1.10 du Feature Pack AEM Communities 6.2.

Pour vous assurer que le dernier Feature Pack est installé, consultez :

* [Dernières versions](deploy-communities.md#latest-releases)

Pour consulter un didacticiel qui crée un site [communautaire d’](overview.md#enablement-community)activation, consultez [Prise en main des communautés AEM pour l’activation](getting-started-enablement.md).

## Configuration de Analytics {#configure-analytics}

Lorsque [Adobe Analytics est configuré pour le site](analytics.md)de la communauté, des informations sur les  de la communauté sont disponibles, ce qui améliore l’expérience des membres de la communauté et fournit des commentaires aux administrateurs du site.

L’intégration à Adobe Analytics est facultative.

## Configuration du courrier électronique pour les notifications {#configure-email-for-notifications}

La fonctionnalité de notifications, disponible par défaut pour tous les sites créés à l’aide de la `Communities Sites` console, fournit un de courrier électronique pour les notifications.

Ce qui est nécessaire, c&#39;est que le courrier électronique soit correctement configuré pour le site.

See [Configuring Email](email.md).

## Activation du service Tunnel {#enable-the-tunnel-service}

Lors de la création d’un site communautaire dans l’auteur  , le service tunnel permet d’attribuer des rôles aux membres de la communauté de confiance enregistrés dans le de publication . Le service tunnel permet également d&#39;accéder aux membres de la communauté à partir des consoles [](members.md) Membres et Groupes de l&#39;auteur  .

La convention permet aux membres et aux groupes de membres créés dans le  de publication de ne *pas* être recréés dans le de l’auteur . For more information see [Managing Users and User Groups](users.md).

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
* Dans le menu **Modifier **, sélectionnez**[!UICONTROL Ajouter Utilisateur ]**

* Dans la `Create New User` boîte de dialogue, saisissez :

   * **[!UICONTROL ID]**: sirius
   * **[!UICONTROL Adresse]**&#x200B;électronique : sirius.nilson@mailinator.com
   * **[!UICONTROL Mot de passe]** : password
   * **[!UICONTROL Confirmer le mot de passe&amp;ast;]**: password
   * **[!UICONTROL Prénom]**: Sirius
   * **[!UICONTROL Nom]**: Nilson

### Affecter Sirius au groupe Administrateurs de la communauté {#assign-sirius-to-community-administrators-group}

Faites défiler jusqu’à `Add User to Groups`:

* Entrez &quot;C&quot; pour rechercher

   * Sélectionner `Community Administrators`
   * Sélectionner `Community Enablement Managers`

* Sélectionnez **[!UICONTROL Enregistrer]**.

![chlimage_1-301](assets/chlimage_1-301.png)

## Activer la connexion aux réseaux sociaux {#enable-social-login}

Avant d’utiliser les versions de démonstration de la connexion sociale avec Facebook et Twitter, vous devez

1. Installez un pack de correctifs ou le [dernier pack](deploy-communities.md#latestfeaturepack) de fonctionnalités (pour les modifications de l’API Facebook de mars 2017).
1. [Activez le fournisseur](social-login.md#adobe-granite-oauth-authentication-handler) OAuth dans le  de publication .

Pour les serveurs de production, il est nécessaire de créer les services Cloud nécessaires pour fournir une connexion sociale.

Voir Connexion [aux réseaux sociaux avec Facebook et Twitter](social-login.md).

## Création de balises de didacticiel {#create-tutorial-tags}

Créez des balises à utiliser pour les didacticiels d’interaction et d’activation, à l’aide de la balise   de `Tutorial`.

Utilisez la console [](../../help/sites-administering/tags.md#tagging-console) Balisage pour créer les balises suivantes :

* `Tutorial: Sports / Baseball`
* `Tutorial: Sports / Gymnastics`
* `Tutorial: Sports / Skiing`
* `Tutorial: Arts / Visual`
* `Tutorial: Arts / Auditory`
* `Tutorial: Arts / History`

![chlimage_1-302](assets/chlimage_1-302.png)

Suivez ensuite les instructions pour :

1. [Définissez les autorisations](../../help/sites-administering/tags.md#setting-tag-permissions)de balise.
1. [Publiez les balises](../../help/sites-administering/tags.md#publishing-tags).

Exemple de package de balises créé pour les didacticiels de prise en main des communautés AEM

[Obtenir le fichier](assets/tutorial_tags-v63.zip)

## MongoDB pour le magasin commun UGC {#mongodb-for-ugc-common-store}

Il est recommandé, mais facultatif, de définir [MSRP](msrp.md) (MongoDB) comme magasin [](working-with-srp.md) commun afin de bénéficier de la souplesse de modération de tous les UGC, qu’ils soient publiés ou  auteurs .

Pour obtenir des instructions, consultez [Comment configurer MongoDB pour la démonstration](demo-mongo.md).

Par défaut, l’installation des instances d’auteur et de publication d’AEM entraîne le stockage du contenu généré par l’utilisateur (UGC) dans le Tar [JCR](../../help/sites-deploying/platform.md) accessible à l’aide de [JSRP](jsrp.md). JSRP n’est pas un magasin commun, ce qui signifie que l’UGC n’est visible que sur l’instance sur laquelle il a été saisi. En règle générale, l’UGC est saisi sur une instance de publication et ne serait pas visible dans le  de l’auteur , ce qui entraînait l’utilisation de l’instance de publication par tous les de modération.