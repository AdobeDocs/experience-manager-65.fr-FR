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

Pour ce faire, suivez les instructions de base AEM [Prise en main](../../help/sites-deploying/deploy.md#getting-started), qui se traduiront par :

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
>Si l&#39;AEM n&#39;est pas familier, vue la documentation sur la [gestion de base](../../help/sites-authoring/basic-handling.md) et un [guide rapide de création de pages](../../help/sites-authoring/qg-page-authoring.md).

## Installer la dernière version des communautés {#install-latest-communities-release}

Ce didacticiel crée un [site de la communauté d’engagement](overview.md#engagement-community) et est basé sur AEM Communities 6.2 Feature Pack version 1.10.

Pour vous assurer que le dernier Feature Pack est installé, visitez :

* [Dernières versions](deploy-communities.md#latest-releases)

Pour consulter un didacticiel qui crée un [site de la communauté d&#39;activation](overview.md#enablement-community), visitez [Prise en main d&#39;AEM Communities pour l&#39;activation](getting-started-enablement.md).

## Configuration de Analytics {#configure-analytics}

Lorsque [Adobe Analytics est configuré pour le site communautaire](analytics.md), des informations sur l&#39;activité de la communauté sont disponibles qui améliorent l&#39;expérience des membres de la communauté et fournissent des commentaires aux administrateurs du site.

L’intégration à Adobe Analytics est facultative.

## Configurer le courrier électronique pour les notifications {#configure-email-for-notifications}

La fonction de notifications, disponible par défaut pour tous les sites créés à l&#39;aide de la console `Communities Sites`, fournit un canal électronique pour les notifications.

Il est nécessaire que le courrier électronique soit correctement configuré pour le site.

Voir [Configuration du courrier électronique](email.md).

## Activer le service de tunnel {#enable-the-tunnel-service}

Lors de la création d’un site communautaire dans l’environnement d’auteur, le service tunnel permet d’attribuer des rôles aux membres de la communauté de confiance enregistrés dans l’environnement de publication. Le service tunnel permet également d&#39;accéder aux membres de la communauté à partir des consoles [Membres et groupes](members.md) de l&#39;environnement auteur.

La convention est destinée aux membres et aux groupes de membres créés dans l’environnement de publication pour *ne pas* être recréés dans l’environnement d’auteur. Pour plus d’informations, voir [Gestion des utilisateurs et des groupes d’utilisateurs](users.md).

Pour obtenir des instructions simples pour activer le service de tunnel sur une instance **author**, voir [Tunnel Service](deploy-communities.md#tunnel-service-on-author).

## Rôle Administrateur de la communauté {#community-administrator-role}

Les membres du groupe Administrateurs de la communauté peuvent créer des sites communautaires, gérer des sites, gérer des membres (ils peuvent interdire les membres de la communauté) et modérer le contenu.

### Créer un utilisateur {#create-user}

Créez un utilisateur sur *author*, auquel est affecté le rôle Administrateur de la communauté :

* Sur l’instance d’auteur

   * Par exemple, [http://localhost:4502/](http://localhost:4503/)

* Connexion avec droits d’administrateur

   * Par exemple, nom d’utilisateur &quot;admin&quot; / mot de passe &quot;admin&quot;

* Dans la console principale, accédez à **[!UICONTROL Outils]** > **[!UICONTROL Opérations]** > **[!UICONTROL Sécurité]** > **[!UICONTROL Utilisateurs]**.
* Dans le menu **Modifier**, sélectionnez **[!UICONTROL Ajouter l&#39;utilisateur]**.

* Dans la boîte de dialogue `Create New User`, saisissez :

   * **[!UICONTROL ID]** : sirius
   * **[!UICONTROL Adresse]** électronique : sirius.nilson@mailinator.com
   * **[!UICONTROL Mot de passe]** : password
   * **[!UICONTROL Confirmer le mot de passe&amp;ast;]** : password
   * **[!UICONTROL Prénom]** : Sirius
   * **[!UICONTROL Nom]** : Nilson

### Affecter Sirius au groupe Administrateurs de la communauté {#assign-sirius-to-community-administrators-group}

Faites défiler jusqu&#39;à `Add User to Groups` :

* Entrer &quot;C&quot; pour effectuer la recherche

   * Sélectionner `Community Administrators`
   * Sélectionner `Community Enablement Managers`

* Sélectionnez **[!UICONTROL Enregistrer]**.

![create-user](assets/create-user.png)

## Activer la connexion aux réseaux sociaux {#enable-social-login}

Avant de pouvoir utiliser les versions de démonstration de la connexion sociale avec Facebook et Twitter, il est nécessaire de

1. Installez un pack de correctifs ou [dernier pack de fonctionnalités](deploy-communities.md#latestfeaturepack) (pour les modifications de l’API Facebook de mars 2017).
1. [Activez le ](social-login.md#adobe-granite-oauth-authentication-handler) fournisseur OAuth dans l’environnement de publication.

Pour les serveurs de production, il est nécessaire de créer les services cloud nécessaires pour fournir une connexion sociale.

Voir [Connexion aux réseaux sociaux avec Facebook et Twitter](social-login.md).

## Créer des balises de didacticiel {#create-tutorial-tags}

Créez des balises à utiliser pour les didacticiels d’interaction et d’activation, à l’aide de l’espace de nommage de balises `Tutorial`.

Utilisez la [console Balisage](../../help/sites-administering/tags.md#tagging-console) pour créer les balises suivantes :

* `Tutorial: Sports / Baseball`
* `Tutorial: Sports / Gymnastics`
* `Tutorial: Sports / Skiing`
* `Tutorial: Arts / Visual`
* `Tutorial: Arts / Auditory`
* `Tutorial: Arts / History`

![tutorial-tags](assets/tutorial-tags.png)

Suivez ensuite les instructions pour :

1. [Définissez les autorisations](../../help/sites-administering/tags.md#setting-tag-permissions) de balise.
1. [Publiez les balises](../../help/sites-administering/tags.md#publishing-tags).

Exemple de package de balises créées pour les Tutorials de prise en main AEM Communities

[Obtenir le fichier](assets/tutorial_tags-v63.zip)

## MongoDB pour UGC Common Store {#mongodb-for-ugc-common-store}

Il est recommandé, mais facultatif, de définir [MSRP](msrp.md) (MongoDB) comme [magasin commun](working-with-srp.md) pour bénéficier de la souplesse de modération de tous les UGC des environnements de publication et/ou d’auteur.

Pour obtenir des instructions, consultez [Comment configurer MongoDB pour la démonstration](demo-mongo.md).

Par défaut, l’installation des instances d’auteur et de publication AEM le contenu généré par l’utilisateur (UGC) est stocké dans [enregistrement Tar JCR](../../help/sites-deploying/platform.md) accessible à l’aide de [JSRP](jsrp.md). JSRP n’est pas un magasin courant, ce qui signifie que l’UGC n’est visible que sur l’instance sur laquelle il a été saisi. En règle générale, l’UGC est saisi sur une instance de publication et n’est pas visible dans l’environnement d’auteur, de sorte que toutes les tâches de modération doivent utiliser l’instance de publication.