---
title: Sites de communautés
description: Découvrez les principes de base des communautés Adobe Experience Manager (AEM) pour les administrateurs qui connaissent déjà ses fonctionnalités de base.
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
role: Admin
exl-id: e3ffc73e-2bc5-492d-b64b-750cc7d8ab9b
solution: Experience Manager
feature: Communities
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '453'
ht-degree: 5%
---
# Sites de communautés {#communities-sites}

Cette section est destinée aux personnes qui administrent AEM Communities et qui supposent être familières avec les fonctionnalités d’AEM Communities.

## Vue d’ensemble {#overview}

Pour obtenir un aperçu et des tutoriels de prise en main, rendez-vous sur :

* [Présentation d’AEM Communities](overview.md)
* [Prise en main d’AEM Communities](getting-started.md)

## Rubriques Administration et configuration {#administration-and-configuration-topics}

### Création et gestion de sites Communities {#communities-site-creation-and-management}

* Communities [consoles](consoles.md)

  * [Sites](sites-console.md)

    * [Groupes (sous-communautés)](groups.md)

  * [Modération](moderation.md)
  * [Gestion des membres et des groupes](members.md)
  * [Rapports](reports.md)

* Communities [*outils*](tools.md) :

  * [Modèles de site](sites.md)
  * [Modèles de groupe](tools-groups.md)
  * [Fonctions de la communauté](functions.md)
  * [Configuration du stockage](srp-config.md)
  * [Guide du composant](components-guide.md)
  * [Badges](badges.md)


### Contenu généré par l&#39;utilisateur {#user-generated-content}

L’une des principales fonctionnalités d’AEM Communities est la génération de contenu créé par l’utilisateur (UGC) par les visiteurs (membres) du site connectés. Pour en savoir plus sur l’utilisation du contenu créé par l’utilisateur, rendez-vous sur :

* [Common UGC Store](working-with-srp.md) : choix du SRP pour le stockage partagé du contenu créé par l’utilisateur
* [Modération du contenu créé par l’utilisateur](moderate-ugc.md) : les membres approuvés peuvent modérer le contenu créé par l’utilisateur en bloc ou en contexte
* [Balisage du contenu créé par l’utilisateur](tag-ugc.md) : les fonctionnalités peuvent être configurées pour permettre aux membres de baliser le contenu
* [Traduction du contenu créé par l’utilisateur](translate-ugc.md) : les fonctionnalités peuvent être configurées pour traduire tout le contenu créé par l’utilisateur ou permettre aux membres de traduire les publications sélectionnées
* [Configuration d’Analytics](analytics.md) : activation d’Adobe Analytics pour créer des rapports sur diverses mesures concernant l’activité des membres

### Membres de la communauté {#community-members}

* [Gestion des utilisateurs et des groupes d’utilisateurs](users.md) : informations sur les membres de la communauté et les groupes de membres, y compris les membres privilégiés.
* [Limites de contribution](limits.md) : capacité à limiter la validation par les nouveaux membres.
* [Service Tunnel](deploy-communities.md#tunnel-service-on-author) : permet d’accéder aux membres et aux groupes de membres côté publication à partir de l’environnement de création.
* [consoles Membres et groupes](members.md) : permet de créer et de gérer des membres et des groupes de membres côté publication à partir de l’environnement de création.
* [Synchronisation des utilisateurs](sync.md) : pour synchroniser les membres et les groupes de membres sur plusieurs instances de publication.
* [Social Connectez-vous avec Facebook et Twitter](social-login.md) : possibilité pour les visiteurs du site de devenir membres de la communauté en utilisant leurs identifiants Facebook ou Twitter.
* [Notation et pastilles](implementing-scoring.md) : possibilité pour les pastilles d&#39;être attribuées pour identifier les rôles d&#39;un membre et pour les membres de gagner des pastilles grâce à leur participation à la communauté.
* [Notifications](notifications.md) : possibilité pour les membres d&#39;être avertis de l&#39;activité qu&#39;ils suivent.
* [Abonnements](subscriptions.md) : possibilité pour les membres d’interagir avec la communauté à l’aide d’un e-mail externe.
* [Messagerie](messaging.md) : capacité des membres à interagir avec la communauté à l’aide de messages internes.

### Déploiement {#deployment}

La section Déploiement contient des informations spécifiques à AEM Communities.

La nature de l’utilisation du contenu de la communauté influence la structure du déploiement :

* [Topologies recommandées pour Communities](topologies.md)

Il est important d’installer la version la plus récente de Communities sur la plateforme d’AEM :

* [Dernier Feature Pack Pour Communities](deploy-communities.md#latestfeaturepack)

Voir la page de déploiement pour d’autres informations spécifiques aux communautés, telles que [Mise à niveau](upgrade.md), [Dispatcher](dispatcher.md) et [Réplication](deploy-communities.md#replication-agents-on-author).

## Documentation sur les communautés associées {#related-communities-documentation}

* Consultez [Déploiement de communautés](deploy-communities.md) où vous trouverez des informations sur les déploiements recommandés.

* Consultez [Développement de communautés](communities.md) où vous pouvez en savoir plus sur le framework de composants sociaux (SCF) et sur la personnalisation des composants et fonctionnalités de communautés.

* Consultez [Création de composants de communautés](author-communities.md) où vous pouvez apprendre à créer avec des composants de communautés et à les configurer.
