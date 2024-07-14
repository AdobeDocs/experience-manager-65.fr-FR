---
title: Développement de communautés
description: Créez et personnalisez des fonctionnalités de la communauté telles que des forums, des groupes d’utilisateurs, etc.
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: 3ed3768a-1b3c-45a1-a34c-61694cd407d9
solution: Experience Manager
feature: Communities
role: Developer
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '390'
ht-degree: 5%

---

# Développement de communautés  {#developing-communities}

## Vue d’ensemble {#overview}

Adobe Experience Manager (AEM) Communities simplifie la création et la personnalisation de fonctionnalités de communauté telles que les forums, les groupes d’utilisateurs, les blogs, les questions et réponses, les calendriers, les commentaires, les révisions, le vote, les évaluations et les affectations. Ces fonctionnalités entraînent la saisie de contenu généré par l’utilisateur dans l’environnement de publication.

La fondation d&#39;un [site communautaire](overview.md#communitiessites) est le [framework de composant social](scf.md) (SCF). La création d’un site communautaire commence par la sélection d’un [modèle de site communautaire](sites-console.md) composé de [ fonctions communautaires](functions.md).

Pour une présentation et des tutoriels de prise en main, rendez-vous sur :

* [Présentation d’AEM Communities](overview.md)
* [Prise en main d’AEM Communities](getting-started.md)

>[!NOTE]
> 
>Il est vivement recommandé de rester à jour avec les [dernières versions](deploy-communities.md#latest-releases).

## Déploiements recommandés {#recommended-deployments}

* [Stockage de contenu de la communauté](working-with-srp.md) : aborde les choix disponibles du fournisseur de ressources sociales (SRP) pour un magasin commun UGC.
* [Topologies recommandées pour Communities](topologies.md) : aborde les topologies en fonction du cas d’utilisation et du choix de la SRP.

## Structure des composants sociaux {#social-component-framework}

* [Social Component Framework](scf.md) : présentation de la structure et des API.
* [Aide-mémoire SCF](handlebars-helpers.md) : aide par défaut et comment écrire des assistants personnalisés.
* [Personnalisation côté client](client-customize.md) : personnalisation du code qui s’exécute dans le navigateur.
* [Personnalisation côté serveur](server-customize.md) : personnalisation du code qui s’exécute sur le serveur.
* [Storage Resource Provider (SRP)](srp.md) : présentation du stockage de contenu de communauté.
* [Directives de codage](code-guide.md) : instructions, conseils et astuces.
* [Guide des composants de la communauté](components-guide.md) : outil de développement interactif.

## Principes fondamentaux des composants, fonctions et fonctionnalités {#component-function-and-feature-essentials}

Les composants, fonctions et fonctionnalités d’AEM Communities fournissent les blocs de création pour les [sites de la communauté](sites-console.md).

* [Notions fondamentales sur les composants, les fonctions et les fonctionnalités](essentials.md)
* [Clientlibs des composants Communities](clientlibs.md)
* [Fonctions de la communauté](functions.md)
* [Modèles de groupe de communautés](tools-groups.md)
* [Modèles de site de communauté](sites.md)

## Membres de la communauté {#community-members}

* [Gestion des utilisateurs et des groupes d’utilisateurs](users.md)
* [Connexion à Social avec Facebook et Twitter](social-login.md)

## Groupes communautaires {#community-groups}

Les [groupes de communautés](overview.md#communitygroups) sont le concept permettant aux membres de la communauté de former des sous-communautés au sein du site de la communauté. La création d’un groupe de communautés peut se produire dans l’environnement de publication ou de création.

* [Notions fondamentales sur les groupes de communautés](essentials-groups.md)
* [Fonction Groupes](functions.md#groups-function)
* [Modèles de groupe de communautés](tools-groups.md)
* [Gestion des utilisateurs et des groupes d’utilisateurs](users.md)
* [Groupes communautaires pour les auteurs](creating-groups.md)

## Gestion des données {#managing-data}

* [Essentials SRP et UGC](srp-and-ugc.md) - Exemples et méthodes d’utilitaire d’API SRP
* [Notions fondamentales sur les balises](tag.md) : possibilité pour les membres de la communauté de baliser le contenu généré par l’utilisateur et/ou les ressources d’activation cataloguées.

## Tutoriels {#tutorials}

* [Tutoriels côté client](tutorials.md#client-side-customization)
* [Tutoriels côté serveur](tutorials.md#server-side-customization)
* [Instructions pratiques](tutorials.md#how-to-instructions)

## Résolution des problèmes {#troubleshooting}

* [Résolution des problèmes](troubleshooting.md)
* [Problèmes connus](/help/release-notes/release-notes.md)

## Documentation sur les communautés connexes {#related-communities-documentation}

* Consultez [Déploiement de communautés](deploy-communities.md) pour en savoir plus sur les déploiements recommandés et la configuration de Dispatcher.

* Consultez [Administration de sites de communautés](administer-landing.md) pour en savoir plus sur la création d’un site de communauté, la configuration de modèles de site de communauté, la modération du contenu de communauté, la gestion des membres et la configuration de la messagerie.

* Visitez la page [Création de composants de communautés](author-communities.md) pour apprendre à créer et configurer des composants de communautés.
