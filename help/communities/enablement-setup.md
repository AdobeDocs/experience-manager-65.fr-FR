---
title: Configuration initiale pour l'activation
seo-title: Configuration initiale
description: Configuration initiale pour l'activation
seo-description: Configuration initiale pour l'activation
uuid: 873ec41d-c088-41d9-a535-de5300661de6
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: introduction
content-type: reference
discoiquuid: f2ac3d66-cc79-498f-83fb-dd96feb88de2
translation-type: tm+mt
source-git-commit: f375b40c084ee363757b78c602091f38524b8b03
workflow-type: tm+mt
source-wordcount: '866'
ht-degree: 2%

---


# Configuration initiale pour l&#39;activation {#initial-setup-for-enablement}

## Instances d’auteur et de publication de début {#start-author-and-publish-instances}

Pour des raisons de développement et de démonstration, il sera nécessaire d’exécuter un auteur et une instance de publication.

Suivez les instructions de base AEM [Prise en main](../../help/sites-deploying/deploy.md#getting-started) qui se traduiront par

* Environnement de l’auteur sur [localhost:4502](http://localhost:4502/)
* Publier l’environnement sur [localhost:4503](http://localhost:4503/)

Pour AEM Communities,

* L&#39;environnement de l&#39;auteur est destiné à :

   * Développement de sites, de modèles, de composants, de ressources d’activation et de chemins d’apprentissage.
   * Affectation de membres et de groupes de membres aux ressources d’activation et aux chemins d’apprentissage.
   * Génération de rapports sur les affectations, les vues et les publications.
   * Tâches d’administration et de configuration.

* L’environnement de publication est destiné à :

   * Apprentissage/formation basés sur des rubriques gérées par le Gestionnaire d&#39;activation.
   * Commentaires et évaluation des ressources d’activation et des chemins d’apprentissage.
   * Se mettre en contact avec les contacts de la ressource.

>[!NOTE]
>
>Si l&#39;AEM n&#39;est pas familier, vue la documentation sur la [gestion de base](../../help/sites-authoring/basic-handling.md) et un [guide rapide de création de pages](../../help/sites-authoring/qg-page-authoring.md).

## Installer la dernière version des communautés {#install-latest-communities-release}

Ce didacticiel crée un [site communautaire d&#39;activation](overview.md#enablement-community). Pour vous assurer que le dernier Feature Pack est installé, visitez :

* [Dernières versions](deploy-communities.md#latest-releases)

Pour consulter un didacticiel qui crée un [site de la communauté d’engagement](overview.md#engagement-community), visitez [Prise en main de AEM Communities](getting-started.md).

## Configurer les fonctionnalités d&#39;activation {#configure-enablement-features}

Pour suivre ce didacticiel, il est nécessaire d&#39;installer et de [configurer correctement l&#39;activation](enablement.md), ce qui nécessite des produits tiers, tels que MySQL et FFmpeg.

## Configuration de Analytics {#configure-analytics}

Lorsque [Adobe Analytics est configuré pour le site communautaire](analytics.md), des informations supplémentaires sont disponibles dans les [rapports](reports.md) générés sur les ressources d’activation et les chemins d’apprentissage attribués aux membres de la communauté (apprenants).

## Configurer le courrier électronique pour les notifications {#configure-email-for-notifications}

La fonction de notifications, disponible par défaut pour tous les sites créés à l&#39;aide de la console `Communities Sites`, fournit un canal électronique pour les notifications.

Il est nécessaire que le courrier électronique soit correctement configuré pour le site.

Voir [Configuration du courrier électronique](email.md).

## Activer le service de tunnel {#enable-the-tunnel-service}

Lors de la création d’un site communautaire dans l’environnement d’auteur, le service de tunnel permet de créer et de gérer des utilisateurs et des groupes d’utilisateurs enregistrés dans l’environnement de publication (membres), d’attribuer des rôles aux membres de la communauté de confiance et d’affecter du contenu aux apprenants.

Pour plus d’informations, voir [Gestion des utilisateurs et des groupes d’utilisateurs](users.md).

Pour obtenir des instructions simples pour activer le service de tunnel, voir [Tunnel Service](deploy-communities.md#tunnel-service-on-author).

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

1. [Définir les autorisations de balise](../../help/sites-administering/tags.md#setting-tag-permissions)
1. [Publication des balises](../../help/sites-administering/tags.md#publishing-tags)

Exemple de package de balises créées pour les Tutorials de prise en main AEM Communities

[Obtenir le fichier](assets/communities_tutorialtags-10.zip)

## Créer des membres et des groupes d&#39;activation {#create-enablement-members-and-groups}

Pour un site de la communauté d&#39;activation, les visiteurs du site ne doivent pas être en mesure de [s&#39;inscrire eux-mêmes ni d&#39;utiliser la connexion sociale](sites-console.md#user-management).

À la place, avec le service [tunnel](#enable-the-tunnel-service) activé, la console [Membres](members.md) est utilisée pour enregistrer de nouveaux membres dans l’environnement de publication.

Dans ce didacticiel, trois membres sont créés dans l’environnement de publication. Deux membres deviennent membres d’un groupe d’utilisateurs affecté à un parcours d’apprentissage, tandis que le troisième membre devient un contact de ressources d’activation.

Un quatrième utilisateur est créé dans l’environnement d’auteur et se voit attribuer les rôles d’administrateur des communautés et de gestionnaire d’activation des communautés.

>[!NOTE]
>
>Ces membres sont en cours de création avant la création du *site communautaire du didacticiel d’activation*.
>
>S’ils ont été créés par la suite, ils peuvent être ajoutés en tant que membres du groupe de membres *Didacticiel d’activation* au cours de la création du membre.
>
>Par la suite, ils seront [affectés au groupe de membres](enablement-create-site.md#assignuserstocommunityenablemembersgroup).

### Riley Taylor - Enrollee {#riley-taylor-enrollee}

[Créez un ](members.md#create-new-member) membre qui sera ajouté à un groupe d&#39;apprenants - le groupe de cours de ski communautaire.

* **ID** : riley
* **Courriel** : riley.taylor@mailinator.com
* **Mot de passe** : password
* **Confirmer le mot de passe** : password
* **Prénom** : Riley
* **Nom** : Taylor

### Sidney Croft - Enrollee {#sidney-croft-enrollee}

[Créez un second ](members.md#create-new-member) membre qui sera ajouté au groupe de la classe de ski communautaire.

* **ID** : annexe
* **Courriel** : sidney.croft@mailinator.com
* **Mot de passe** : password
* **Confirmer le mot de passe** : password
* **Prénom** : Sidney
* **Nom** : Croisement

### Quinn Harper - Ressource d&#39;activation Contact et modérateur {#quinn-harper-enablement-resource-contact-and-moderator}

[Créez un ](members.md#create-new-member) membre qui sera ajouté au groupe de membres du site communautaire une fois le site créé. Cette adhésion permet au membre d&#39;être affecté en tant qu&#39;activation [Contact ressource](resources.md#settings) lorsqu&#39;une ressource d&#39;activation est créée pour le site.

* **ID** : quinn
* **Courriel** : quinn.harper@mailinator.com
* **Mot de passe** : password
* **Confirmer le mot de passe** : password
* **Prénom** : Quinn
* **Nom** : Harper

### Ajouter un groupe d&#39;utilisateurs - Classe de ski communautaire {#add-a-user-group-community-ski-class}

[Ajoutez un nouveau ](members.md#create-new-group) groupe nommé Community Ski Class.

* **ID** : community-ski-class
* **Nom** : Classe de ski communautaire
* **Description** : un groupe d&#39;exemples pour l&#39;affectation de ressources d&#39;activation
* **Ajouter les membres au groupe**  &quot;ajouter&quot; :

   * riley
   * annexe

* Sélectionnez **[!UICONTROL Enregistrer]**

### Propriétés de la classe de ski de communauté {#community-ski-class-properties}

![ski-class-properties](assets/ski-class-properties.png)

>[!NOTE]
>
>Pendant la création du site communautaire, les membres et les groupes existants peuvent être ajoutés au groupe de membres du site communautaire.

## Rôle Administrateur de la communauté {#community-administrator-role}

Les membres du groupe Administrateurs de la communauté peuvent créer des sites communautaires, gérer des sites, gérer des membres (ils peuvent interdire les membres de la communauté) et modérer le contenu.

### Créer un utilisateur {#create-user}

Créez un utilisateur sur *author*, auquel est affecté le rôle Administrateur de la communauté :

* Sur l’instance d’auteur

   * Par exemple, [http://localhost:4502/](http://localhost:4503/)

* Connexion avec droits d’administrateur

   * Par exemple, nom d’utilisateur &quot;admin&quot; / mot de passe &quot;admin&quot;

* Dans la console principale, accédez à **[!UICONTROL Outils]** > **[!UICONTROL Opérations]** > **[!UICONTROL Sécurité]** > **[!UICONTROL Utilisateurs]**.
* Dans le menu **[!UICONTROL Modifier]**, sélectionnez **[!UICONTROL Ajouter l&#39;utilisateur]**.

* Dans la boîte de dialogue `Create New User`, saisissez :

   * **ID&amp;ast;** : sirius
   * **Adresse** électronique : sirius.nilson@mailinator.com
   * **Password&amp;ast;** : password
   * **Confirmer le mot de passe&amp;ast;** : password
   * **Prénom** : Sirius
   * **Nom&amp;ast;** : Nilson

### Affecter Sirius au groupe Administrateurs de la communauté {#assign-sirius-to-community-administrators-group}

Faites défiler jusqu&#39;à `Add User to Groups` :

* Entrer &quot;C&quot; pour effectuer la recherche

   * Sélectionner `Community Administrators`
   * Sélectionner `Community Enablement Managers`

* Sélectionnez **[!UICONTROL Enregistrer]**

![admin-role](assets/admin-role.png)

