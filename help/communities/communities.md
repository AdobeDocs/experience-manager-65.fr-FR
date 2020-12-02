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
translation-type: tm+mt
source-git-commit: f375b40c084ee363757b78c602091f38524b8b03
workflow-type: tm+mt
source-wordcount: '406'
ht-degree: 10%

---


# Communautés en développement {#developing-communities}

## Présentation {#overview}

AEM Communities simplifie la création et la personnalisation de fonctionnalités de la communauté telles que les forums, les groupes d’utilisateurs, les blogs, les questions et réponses, les calendriers, les commentaires, les commentaires, les votes, les évaluations et les affectations. Ces fonctions entraînent la saisie de contenu généré par l’utilisateur (UGC) dans l’environnement de publication.

La base d&#39;un [site communautaire](overview.md#communitiessites) est le [cadre de composants sociaux](scf.md) (SCF). La création d&#39;un site communautaire commence par la sélection d&#39;un [modèle de site communautaire](sites-console.md) composé de [fonctions communautaires](functions.md).

Pour une présentation et des didacticiels de prise en main, visitez :

* [Présentation d’AEM Communities](overview.md)
* [Prise en main d’AEM Communities](getting-started.md)
* [Prise en main d’AEM Communities pour l’activation](getting-started-enablement.md)

>[!NOTE]
> 
>Il est vivement recommandé de rester à jour avec les [dernières versions](deploy-communities.md#latest-releases).

## Déploiements recommandés {#recommended-deployments}

* [Enregistrement](working-with-srp.md) de contenu de la communauté : décrit les options SRP disponibles pour un magasin commun UGC
* [Topologies recommandées pour les communautés](topologies.md) : aborde les topologies en fonction du cas d’utilisation et du choix SRP

## Cadre des composants sociaux {#social-component-framework}

* [Cadre](scf.md) des composants sociaux : présentation de la structure et des API.
* [Aide](handlebars-helpers.md) des barres d&#39;outils SCF : aide par défaut et comment écrire des aides personnalisées.
* [Personnalisation](client-customize.md) côté client : personnalisation du code qui s’exécute dans le navigateur.
* [Personnalisation](server-customize.md) côté serveur : personnalisation du code s’exécutant sur le serveur.
* [Fournisseur de ressources d&#39;Enregistrement (SRP)](srp.md) : aperçu de l’enregistrement de contenu de la communauté.
* [Instructions](code-guide.md) de codage : directives, conseils et astuces.
* [Guide](components-guide.md) des composants de la communauté : outil de développement interactif.

## Composants, fonctions et caractéristiques essentielles {#component-function-and-feature-essentials}

Les composants, fonctions et fonctionnalités AEM Communities constituent les éléments de base des [sites communautaires](sites-console.md).

* [Composants, fonctions et caractéristiques essentielles](essentials.md)
* [Clientlibs pour les composants Communities](clientlibs.md)
* [Fonctions de la communauté](functions.md)
* [Modèles de groupe de communautés](tools-groups.md)
* [Modèles de site de communauté](sites.md)

## Membres de la communauté {#community-members}

* [Gestion des utilisateurs et des groupes d’utilisateurs](users.md)
* [Connexion aux réseaux sociaux avec Facebook et Twitter](social-login.md)

## Groupes communautaires {#community-groups}

[Les ](overview.md#communitygroups) regroupements communautaires constituent le concept permettant aux membres de la communauté de former des sous-communautés au sein du site communautaire. La création d’un groupe communautaire peut se produire dans l’environnement de publication ou d’auteur.

* [Groupe communautaire Essentials](essentials-groups.md)
* [Fonction Groupes](functions.md#groups-function)
* [Modèles de groupe de communautés](tools-groups.md)
* [Gestion des utilisateurs et des groupes d’utilisateurs](users.md)
* [Groupes communautaires pour les auteurs](creating-groups.md)

## Gestion des données {#managing-data}

* [SRP et UGC Essentials](srp-and-ugc.md)  - Exemples et méthodes d&#39;utilitaire SRP API
* [Tag Essentials](tag.md)  : capacité des membres de la communauté à baliser les ressources d&#39;activation de l&#39;UGC et/ou cataloguées

## Tutoriels {#tutorials}

* [Didacticiels client](tutorials.md#client-side-customization)
* [Didacticiels côté serveur](tutorials.md#server-side-customization)
* [Instructions pratiques](tutorials.md#how-to-instructions)

## Dépannage {#troubleshooting}

* [Résolution des incidents](troubleshooting.md)
* [Problèmes connus](/help/release-notes/known-issues.md)

## Documentation sur les communautés associée {#related-communities-documentation}

* Visitez [Déploiement de communautés](deploy-communities.md) pour en savoir plus sur les déploiements recommandés et la configuration du répartiteur.

* Visitez [Administration des sites des communautés](administer-landing.md) pour en savoir plus sur la création d&#39;un site de la communauté, la configuration des modèles de site de la communauté, la modération du contenu de la communauté, la gestion des membres et la configuration des messages.

* Visitez [Création de composants de communautés](author-communities.md) pour savoir comment créer et configurer des composants de communautés.

