---
title: Développement de communautés
seo-title: Développement de communautés
description: Créez et personnalisez des fonctionnalités de la communauté telles que des forums, des groupes d’utilisateurs, etc.
seo-description: Créez et personnalisez des fonctionnalités de la communauté telles que des forums, des groupes d’utilisateurs, etc.
uuid: 51dc54da-9090-4d36-adf9-72d5479062a5
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: fbfe8097-3c3f-4a05-97ad-1ce526362a26
exl-id: 3ed3768a-1b3c-45a1-a34c-61694cd407d9
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '406'
ht-degree: 10%

---

# Développement de communautés {#developing-communities}

## Présentation {#overview}

AEM Communities simplifie la création et la personnalisation de fonctionnalités de communauté telles que les forums, les groupes d’utilisateurs, les blogs, les questions et réponses, les calendriers, les commentaires, les révisions, le vote, les évaluations et les affectations. Ces fonctionnalités entraînent la saisie de contenu généré par l’utilisateur dans l’environnement de publication.

La base d’un [site communautaire](overview.md#communitiessites) est la [structure de composants sociaux](scf.md) (SCF). La création d’un site communautaire commence par la sélection d’un [modèle de site communautaire](sites-console.md) composé de [fonctions communautaires](functions.md).

Pour une présentation et des tutoriels de prise en main, rendez-vous sur :

* [Présentation d’AEM Communities](overview.md)
* [Prise en main d’AEM Communities](getting-started.md)
* [Prise en main d’AEM Communities pour l’activation](getting-started-enablement.md)

>[!NOTE]
> 
>Il est vivement recommandé de rester à jour avec les [dernières versions](deploy-communities.md#latest-releases).

## Déploiements recommandés {#recommended-deployments}

* [Stockage de contenu de la communauté](working-with-srp.md) : discute des choix de SRP disponibles pour un magasin commun UGC
* [Topologies recommandées pour les communautés](topologies.md) : aborde les topologies en fonction du cas d’utilisation et du choix de la SRP

## Structure des composants sociaux {#social-component-framework}

* [Structure des composants sociaux](scf.md) : présentation de la structure et des API.
* [Aide-mémoire SCF](handlebars-helpers.md) : aide par défaut et comment écrire des aides personnalisées.
* [Personnalisation côté client](client-customize.md) : personnalisation du code qui s’exécute dans le navigateur.
* [Personnalisation côté serveur](server-customize.md) : personnalisation du code qui s’exécute sur le serveur.
* [Fournisseur de ressources de stockage (SRP)](srp.md) : présentation du stockage de contenu de la communauté.
* [Consignes de codage](code-guide.md) : directives, conseils et astuces.
* [Guide](components-guide.md) des composants de communauté : outil de développement interactif.

## Notions fondamentales sur les composants, les fonctions et les fonctionnalités {#component-function-and-feature-essentials}

Les composants, fonctions et fonctionnalités d’AEM Communities fournissent les blocs de création des [sites de communauté](sites-console.md).

* [Notions fondamentales sur les composants, les fonctions et les fonctionnalités](essentials.md)
* [Clientlibs des composants Communities](clientlibs.md)
* [Fonctions de la communauté](functions.md)
* [Modèles de groupe de communautés](tools-groups.md)
* [Modèles de site de communauté](sites.md)

## Membres de la communauté {#community-members}

* [Gestion des utilisateurs et des groupes d’utilisateurs](users.md)
* [Connexion aux réseaux sociaux avec Facebook et Twitter](social-login.md)

## Groupes communautaires {#community-groups}

[Le ](overview.md#communitygroups) regroupement communautaire consiste à permettre aux membres de la communauté de former des sous-communautés au sein du site communautaire. La création d’un groupe de communautés peut se produire dans l’environnement de publication ou de création.

* [Notions fondamentales sur les groupes de communautés](essentials-groups.md)
* [Fonction Groupes](functions.md#groups-function)
* [Modèles de groupe de communautés](tools-groups.md)
* [Gestion des utilisateurs et des groupes d’utilisateurs](users.md)
* [Groupes communautaires pour les auteurs](creating-groups.md)

## Gestion des données {#managing-data}

* [Principes de base de la SRP et de l’UGC](srp-and-ugc.md)  : méthodes et exemples de l’utilitaire de SRP
* [Notions fondamentales sur les balises](tag.md)  : possibilité pour les membres de la communauté de baliser le contenu généré par l’utilisateur et/ou les ressources d’activation cataloguées.

## Tutoriels {#tutorials}

* [Tutoriels côté client](tutorials.md#client-side-customization)
* [Tutoriels côté serveur](tutorials.md#server-side-customization)
* [Instructions pratiques](tutorials.md#how-to-instructions)

## Résolution des problèmes {#troubleshooting}

* [Résolution des problèmes](troubleshooting.md)
* [Problèmes connus](/help/release-notes/known-issues.md)

## Documentation sur les communautés associée {#related-communities-documentation}

* Visitez [Déploiement de communautés](deploy-communities.md) pour en savoir plus sur les déploiements recommandés et la configuration du Dispatcher.

* Consultez [Administration des sites communautaires](administer-landing.md) pour en savoir plus sur la création d’un site communautaire, la configuration des modèles de site communautaire, la modération du contenu communautaire, la gestion des membres et la configuration de la messagerie.

* Consultez la section [Création de composants de communautés](author-communities.md) pour savoir comment créer et configurer des composants de communautés.
