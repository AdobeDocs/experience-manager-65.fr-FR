---
title: Développement de communautés
seo-title: Developing Communities
description: Créez et personnalisez des fonctionnalités de la communauté telles que des forums, des groupes d’utilisateurs, etc.
seo-description: Create and customize community features such as forums, user groups, and more
uuid: 51dc54da-9090-4d36-adf9-72d5479062a5
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: fbfe8097-3c3f-4a05-97ad-1ce526362a26
exl-id: 3ed3768a-1b3c-45a1-a34c-61694cd407d9
source-git-commit: 4dbbcc41757843d3b2d5a3bbb2656ef587e83d2c
workflow-type: tm+mt
source-wordcount: '385'
ht-degree: 6%

---

# Développement de communautés  {#developing-communities}

## Présentation {#overview}

AEM Communities simplifie la création et la personnalisation de fonctionnalités de communauté telles que les forums, les groupes d’utilisateurs, les blogs, les questions et réponses, les calendriers, les commentaires, les révisions, le vote, les évaluations et les affectations. Ces fonctionnalités entraînent la saisie de contenu généré par l’utilisateur dans l’environnement de publication.

La fondation d’un [site communautaire](overview.md#communitiessites) est la valeur [structure des composants sociaux](scf.md) (SCF). La création d&#39;un site communautaire commence par la sélection d&#39;un [modèle de site communautaire](sites-console.md) qui est composé de [fonctions de communauté](functions.md).

Pour une présentation et des tutoriels de prise en main, rendez-vous sur :

* [Présentation d’AEM Communities](overview.md)
* [Prise en main d’AEM Communities](getting-started.md)

>[!NOTE]
> 
>Il est vivement recommandé de rester à jour avec la variable [dernières versions](deploy-communities.md#latest-releases).

## Déploiements recommandés {#recommended-deployments}

* [Stockage de contenu communautaire](working-with-srp.md): discute des choix de SRP disponibles pour un magasin commun UGC
* [Topologies recommandées pour les communautés](topologies.md): aborde les topologies en fonction du cas d’utilisation et du choix de la SRP

## Structure des composants sociaux {#social-component-framework}

* [Structure des composants sociaux](scf.md): présentation de la structure et des API.
* [Assistant de Handlebars SCF](handlebars-helpers.md): aide par défaut et comment écrire des aides personnalisées.
* [Personnalisation côté client](client-customize.md): personnalisation du code qui s’exécute dans le navigateur.
* [Personnalisation côté serveur](server-customize.md): personnalisation du code qui s’exécute sur le serveur.
* [Fournisseur de ressources de stockage (SRP)](srp.md): présentation du stockage de contenu de la communauté.
* [Consignes de codage](code-guide.md): directives, conseils et astuces.
* [Guide des composants de communauté](components-guide.md): outil de développement interactif.

## Notions fondamentales sur les composants, les fonctions et les fonctionnalités {#component-function-and-feature-essentials}

Les composants, fonctions et fonctionnalités d’AEM Communities fournissent les blocs de création pour [sites communautaires](sites-console.md).

* [Notions fondamentales sur les composants, les fonctions et les fonctionnalités](essentials.md)
* [Clientlibs des composants Communities](clientlibs.md)
* [Fonctions de la communauté](functions.md)
* [Modèles de groupe de communautés](tools-groups.md)
* [Modèles de site de communauté](sites.md)

## Membres de la communauté {#community-members}

* [Gestion des utilisateurs et des groupes d’utilisateurs](users.md)
* [Connexion aux réseaux sociaux avec Facebook et Twitter](social-login.md)

## Groupes communautaires {#community-groups}

[Groupes communautaires](overview.md#communitygroups) est le concept permettant aux membres de la communauté de former des sous-communautés au sein du site de la communauté. La création d’un groupe de communautés peut se produire dans l’environnement de publication ou de création.

* [Notions fondamentales sur les groupes de communautés](essentials-groups.md)
* [Fonction Groupes](functions.md#groups-function)
* [Modèles de groupe de communautés](tools-groups.md)
* [Gestion des utilisateurs et des groupes d’utilisateurs](users.md)
* [Groupes communautaires pour les auteurs](creating-groups.md)

## Gestion des données {#managing-data}

* [Principes de base de la SRP et du contenu généré par l’utilisateur](srp-and-ugc.md) - Méthodes et exemples de l’utilitaire SRP
* [Notions fondamentales sur les balises](tag.md) - possibilité pour les membres de la communauté de baliser le contenu généré par l’utilisateur et/ou les ressources d’activation cataloguées

## Tutoriels {#tutorials}

* [Tutoriels côté client](tutorials.md#client-side-customization)
* [Tutoriels côté serveur](tutorials.md#server-side-customization)
* [Instructions pratiques](tutorials.md#how-to-instructions)

## Résolution des problèmes {#troubleshooting}

* [Résolution des problèmes](troubleshooting.md)
* [Problèmes connus](/help/release-notes/release-notes.md)

## Documentation sur les communautés connexes {#related-communities-documentation}

* Visite [Déploiement de communautés](deploy-communities.md) pour en savoir plus sur les déploiements recommandés et la configuration du dispatcher.

* Visite [Administration des sites des communautés](administer-landing.md) pour en savoir plus sur la création d’un site communautaire, la configuration des modèles de site communautaire, la modération du contenu communautaire, la gestion des membres et la configuration des messages.

* Visite [Création de composants Communities](author-communities.md) pour savoir comment créer avec et configurer des composants Communities.
