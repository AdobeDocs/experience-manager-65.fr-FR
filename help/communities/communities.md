---
title: Communautés en développement
description: Créez et personnalisez des fonctionnalités de communauté telles que des forums, des groupes d’utilisateurs, etc.
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: 3ed3768a-1b3c-45a1-a34c-61694cd407d9
solution: Experience Manager
feature: Communities
role: Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
feature_v2:
  - id: b013f126-a97e-52d1-9f79-cb5bbb12114e
    internal-label: Communities
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '399'
ht-degree: 5%
---
# Communautés en développement  {#developing-communities}

## Vue d’ensemble {#overview}

Les communautés Adobe Experience Manager (AEM) simplifient la création et la personnalisation de fonctionnalités de communauté telles que les forums, les groupes d’utilisateurs, les blogs, les questions/réponses, les calendriers, les commentaires, les révisions, les votes, les évaluations et les affectations. Grâce à ces fonctionnalités, le contenu créé par l’utilisateur est saisi dans l’environnement de publication.

La base d’un [site communautaire](overview.md#communitiessites) est le [cadre des composants sociaux](scf.md) (SCF). La création d’un site communautaire commence par la sélection d’un [modèle de site communautaire](sites-console.md) composé de [fonctions de communauté](functions.md).

Pour obtenir un aperçu et des tutoriels de prise en main, rendez-vous sur :

* [Présentation d’AEM Communities](overview.md)
* [Prise en main d’AEM Communities](getting-started.md)

>[!NOTE]
> 
>Il est vivement recommandé de se tenir à jour avec les [dernières versions](deploy-communities.md#latest-releases).

## Déploiements recommandés {#recommended-deployments}

* [Stockage de contenu de la communauté](working-with-srp.md) : décrit les choix disponibles pour le fournisseur de ressources sociales (SRP) pour un magasin commun de contenu créé par l’utilisateur
* [Topologies recommandées pour Communities](topologies.md) : décrit les topologies en fonction du cas d’utilisation et du choix du SRP.

## Structure des composants sociaux {#social-component-framework}

* [Social Component Framework](scf.md) : présentation du framework et des API.
* [Assistant Handlebars SCF](handlebars-helpers.md) : assistants par défaut et comment écrire des assistants personnalisés.
* [Personnalisation côté client](client-customize.md) : personnalisation du code qui s’exécute dans le navigateur.
* [Personnalisation côté serveur](server-customize.md) : personnalisation du code qui s’exécute sur le serveur.
* [Fournisseur de ressources de stockage (SRP)](srp.md) : présentation du stockage de contenu de la communauté.
* [Directives de codage](code-guide.md) : directives, conseils et astuces.
* [Guide des composants de communauté](components-guide.md) : outil de développement interactif.

## Principes fondamentaux des composants, des fonctions et des fonctionnalités {#component-function-and-feature-essentials}

Les composants, fonctions et fonctions d’AEM Communities constituent les éléments de base des [sites de la communauté](sites-console.md).

* [Principes fondamentaux des composants, des fonctions et des fonctionnalités](essentials.md)
* [Bibliothèques clientes pour les composants de Communities](clientlibs.md)
* [Fonctions de la communauté](functions.md)
* [Modèles de groupe de communautés](tools-groups.md)
* [Modèles de site de communauté](sites.md)

## Membres de la communauté {#community-members}

* [Gestion des utilisateurs et des groupes d’utilisateurs](users.md)
* [Connexion sociale avec Facebook et Twitter](social-login.md)

## Groupes communautaires {#community-groups}

Les [groupes communautaires](overview.md#communitygroups) sont le concept qui permet aux membres de la communauté de former des sous-communautés au sein du site communautaire. La création d’un groupe de communautés peut avoir lieu dans l’environnement de publication ou de création.

* [Principes de base du groupe de la communauté](essentials-groups.md)
* [Fonction de groupes](functions.md#groups-function)
* [Modèles de groupe de communautés](tools-groups.md)
* [Gestion des utilisateurs et des groupes d’utilisateurs](users.md)
* [Groupes de communautés pour les auteurs](creating-groups.md)

## Gestion des données {#managing-data}

* [SRP et UGC Essentials](srp-and-ugc.md) - Méthodes et exemples d’utilitaires d’API SRP
* [Tag Essentials](tag.md) - possibilité pour les membres de la communauté de baliser le contenu créé par l’utilisateur et/ou les ressources d’activation cataloguées

## Tutoriels {#tutorials}

* [Tutoriels côté client](tutorials.md#client-side-customization)
* [Tutoriels côté serveur](tutorials.md#server-side-customization)
* [Instructions Pratiques](tutorials.md#how-to-instructions)

## Résolution des problèmes {#troubleshooting}

* [Résolution des problèmes](troubleshooting.md)
* [Problèmes connus](/help/release-notes/release-notes.md)

## Documentation sur les communautés associées {#related-communities-documentation}

* Consultez [Déploiement de communautés](deploy-communities.md) pour en savoir plus sur les déploiements recommandés et la configuration de Dispatcher.

* Consultez [Administration de sites de communautés](administer-landing.md) pour en savoir plus sur la création d’un site communautaire, la configuration de modèles de site communautaire, la modération du contenu de la communauté, la gestion des membres et la configuration des messages.

* Consultez [Création de composants de communautés](author-communities.md) pour savoir comment créer avec les composants de communautés et les configurer.
