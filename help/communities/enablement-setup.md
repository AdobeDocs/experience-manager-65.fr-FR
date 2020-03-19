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
source-git-commit: d6c8bbb9aa763a2eb6660b6b6755aba75241e394

---


# Configuration initiale pour l&#39;activation {#initial-setup-for-enablement}

## Start Author and Publish Instances {#start-author-and-publish-instances}

Pour des raisons de développement et de démonstration, il sera nécessaire d’exécuter une instance d’auteur et une instance de publication.

Suivez les instructions de base de [prise en main](../../help/sites-deploying/deploy.md#getting-started) d’AEM, ce qui entraînera

* Auteur   sur [localhost:4502](http://localhost:4502/)
* Publier   sur [localhost:4503](http://localhost:4503/)

Pour les communautés AEM,

* L&#39;auteur  le  est pour

   * Développement de sites, de modèles, de composants, de ressources d’activation et de chemins d’apprentissage
   * Affectation de membres et de groupes de membres aux ressources d’activation et aux chemins d’apprentissage
   * Génération de rapports sur les affectations, les  et les publications
   *  d’administration et de configuration

*  de publication 

   * Formation/formation basée sur des sujets gérés par le Gestionnaire d&#39;activation
   * Commentaires et évaluation des ressources d’activation et des chemins d’apprentissage
   * Prise en contact avec les contacts de ressources

>[!NOTE]
>
>If not familiar with AEM, view the documentation on [basic handling](../../help/sites-authoring/basic-handling.md) and a [quick guide to authoring pages](../../help/sites-authoring/qg-page-authoring.md).

## Installer la dernière version des communautés {#install-latest-communities-release}

Ce didacticiel crée un site [communautaire d’](overview.md#enablement-community)activation. Pour vous assurer que le dernier Feature Pack est installé, consultez :

* [Dernières versions](deploy-communities.md#latest-releases)

Pour consulter un didacticiel qui crée un site [de communauté d’](overview.md#engagement-community)engagement, consultez [Prise en main des communautés](getting-started.md)AEM.

## Configuration des fonctionnalités d’activation {#configure-enablement-features}

Pour suivre ce didacticiel, il est nécessaire d’installer et de [configurer correctement l’activation](enablement.md), qui nécessite des produits tiers, tels que MySQL et FFmpeg.

## Configuration de Analytics {#configure-analytics}

Lorsque [Adobe Analytics est configuré pour le site](analytics.md)de la communauté, des informations supplémentaires sont disponibles dans les [rapports](reports.md) générés sur les ressources d’activation et les chemins d’apprentissage attribués aux membres de la communauté (apprenants).

## Configuration du courrier électronique pour les notifications {#configure-email-for-notifications}

La fonctionnalité de notifications, disponible par défaut pour tous les sites créés à l’aide de la `Communities Sites` console, fournit un de courrier électronique pour les notifications.

Ce qui est nécessaire, c&#39;est que le courrier électronique soit correctement configuré pour le site.

See [Configuring Email](email.md).

## Activation du service Tunnel {#enable-the-tunnel-service}

Lors de la création d’un site de la communauté dans le  de l’auteur, le service de tunnel permet de créer et de gérer des utilisateurs et des groupes d’utilisateurs enregistrés dans le de publication, d’attribuer des rôles aux membres de la communauté de confiance et d’affecter du contenu aux apprenants.

For more information see [Managing Users and User Groups](users.md).

Pour obtenir des instructions simples sur l’activation du service de tunnel, voir Service [de](deploy-communities.md#tunnel-service-on-author)tunnel.

## Création de balises de didacticiel {#create-tutorial-tags}

Créez des balises à utiliser pour les didacticiels d’interaction et d’activation, à l’aide de la balise   de `Tutorial`.

Utilisez la console [](../../help/sites-administering/tags.md#tagging-console) Balisage pour créer les balises suivantes :

* `Tutorial: Sports / Baseball`
* `Tutorial: Sports / Gymnastics`
* `Tutorial: Sports / Skiing`
* `Tutorial: Arts / Visual`
* `Tutorial: Arts / Auditory`
* `Tutorial: Arts / History`

![chlimage_1-417](assets/chlimage_1-417.png)

Suivez ensuite les instructions pour

1. [Définition des autorisations de balise](../../help/sites-administering/tags.md#setting-tag-permissions)
1. [Publication des balises](../../help/sites-administering/tags.md#publishing-tags)

Exemple de package de balises créé pour les didacticiels de prise en main des communautés AEM

[Obtenir le fichier](assets/communities_tutorialtags-10.zip)

## Créer des membres et des groupes d&#39;activation {#create-enablement-members-and-groups}

Pour un site de la communauté d&#39;activation, les du site ne doivent pas pouvoir s&#39; [auto-inscrire ni utiliser la connexion](sites-console.md#user-management)sociale.

Au lieu de cela, avec le service [tunnel](#enable-the-tunnel-service) activé, la console [](members.md) Membres est utilisée pour enregistrer de nouveaux membres dans le  de publication .

Dans ce didacticiel, trois membres sont créés dans le  de publication . Deux membres deviennent membres d’un groupe d’utilisateurs affecté à un parcours d’apprentissage, tandis que le troisième membre devient un contact de ressource d’activation.

Un quatrième utilisateur est créé dans l’ de l’auteur  et les rôles d’Administrateur des communautés et Gestionnaire d’activation de la communauté sont attribués.

>[!NOTE]
>
>Ces membres sont en cours de création avant la création du site de la communauté *du didacticiel* d&#39;activation.
>
>S’ils ont été créés par la suite, ils peuvent être ajoutés en tant que membres du groupe *de membres du* didacticiel d’activation pendant la création du membre.
>
>Au lieu de cela, plus tard, ils seront [affectés au groupe](enablement-create-site.md#assignuserstocommunityenablemembersgroup)de membres.

### Riley Taylor - Enrollee {#riley-taylor-enrollee}

[Créez un membre](members.md#create-new-member) qui sera ajouté à un groupe d’apprenants - le groupe de la classe de ski communautaire.

* **ID**: riley
* **Courriel**: riley.taylor@mailinator.com
* **Mot de passe** : password
* **Confirmer le mot de passe**: password
* **Prénom**: Riley
* **Nom**: Taylor

### Sidney Croft - Enrollee {#sidney-croft-enrollee}

[Créez un deuxième membre](members.md#create-new-member) qui sera ajouté au groupe Classe de ski communautaire.

* **ID**: sidney
* **Courriel**: sidney.croft@mailinator.com
* **Mot de passe** : password
* **Confirmer le mot de passe**: password
* **Prénom**: Sidney
* **Nom**: Croisement

### Quinn Harper - Ressource d&#39;activation Contact et modérateur {#quinn-harper-enablement-resource-contact-and-moderator}

[Créez un membre](members.md#create-new-member) qui sera ajouté au groupe de membres du site communautaire une fois le site créé. Cet abonnement permettra au membre d&#39;être affecté en tant que contact [de](resources.md#settings) ressource d&#39;activation lorsqu&#39;une ressource d&#39;activation est créée pour le site.

* **ID**: quinn
* **Courriel**: quinn.harper@mailinator.com
* **Mot de passe** : password
* **Confirmer le mot de passe**: password
* **Prénom**: Quinn
* **Nom**: Harper

### Ajouter un groupe d&#39;utilisateurs - Classe de ski de la communauté {#add-a-user-group-community-ski-class}

[Ajouter un nouveau groupe](members.md#create-new-group) nommé Community Ski Class.

* **ID**: community-ski-class
* **Nom**: Classe de ski communautaire
* **Description**: un groupe d&#39;exemples pour l&#39;affectation de ressources d&#39;activation
* **Ajouter Membres au groupe** &quot;ajouter&quot; :

   * riley
   * sidney

* Sélectionnez **[!UICONTROL Enregistrer]**

### Propriétés des classes de ski de communauté {#community-ski-class-properties}

![chlimage_1-418](assets/chlimage_1-418.png)

>[!NOTE]
>
>Pendant la création du site communautaire, les membres et groupes existants peuvent être ajoutés au groupe des membres du site.

## Rôle Administrateur de la communauté {#community-administrator-role}

Les membres du groupe Administrateurs de la communauté peuvent créer des sites communautaires, gérer des sites, gérer des membres (ils peuvent interdire les membres de la communauté) et modérer le contenu.

### Créer un utilisateur {#create-user}

Créez un utilisateur sur *l’auteur*, auquel est affecté le rôle Administrateur de la communauté :

* Sur l’instance d’auteur

   * For example, [http://localhost:4502/](http://localhost:4503/)

* Connexion avec droits d’administrateur

   * Par exemple, nom d’utilisateur &quot;admin&quot; / mot de passe &quot;admin&quot;

* Dans la console principale, accédez à **[!UICONTROL Outils, Opérations > Sécurité > Utilisateurs.]**
* Dans le menu **[!UICONTROL Modifier]** , sélectionnez **[!UICONTROL Ajouter Utilisateur]**

* Dans la `Create New User` boîte de dialogue, saisissez

   * **ID&amp;ast;**: sirius
   * **Adresse**&#x200B;électronique : sirius.nilson@mailinator.com
   * **Password&amp;ast;**: password
   * **Confirmer le mot de passe&amp;ast;**: password
   * **Prénom**: Sirius
   * **Nom&amp;ast;**: Nilson

### Affecter Sirius au groupe Administrateurs de la communauté {#assign-sirius-to-community-administrators-group}

Faites défiler jusqu’à `Add User to Groups`:

* Entrez &quot;C&quot; pour rechercher

   * Sélectionner `Community Administrators`
   * Sélectionner `Community Enablement Managers`

* Sélectionnez **[!UICONTROL Enregistrer]**

![chlimage_1-419](assets/chlimage_1-419.png)

