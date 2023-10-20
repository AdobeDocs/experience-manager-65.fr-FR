---
title: Sites de communautés
description: Découvrez les principes de base des communautés Adobe Experience Manager (AEM) pour administrer les utilisateurs qui connaissent déjà ses fonctions de base.
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
role: Admin
exl-id: e3ffc73e-2bc5-492d-b64b-750cc7d8ab9b
source-git-commit: f03d0ab9d0f491441378e16e1590d33651f064b5
workflow-type: tm+mt
source-wordcount: '449'
ht-degree: 5%

---

# Sites de communautés {#communities-sites}

Cette section s’adresse à ceux qui gèrent AEM Communities et se familiarisent avec les fonctionnalités d’AEM Communities.

## Vue d’ensemble {#overview}

Pour une présentation et des tutoriels de prise en main, rendez-vous sur :

* [Présentation d’AEM Communities](overview.md)
* [Prise en main d’AEM Communities](getting-started.md)

## Rubriques d’administration et de configuration {#administration-and-configuration-topics}

### Création et gestion de sites communautaires {#communities-site-creation-and-management}

* Communautés [consoles](consoles.md)

   * [Sites](sites-console.md)

      * [Groupes (sous-communautés)](groups.md)

   * [Modération](moderation.md)
   * [Gestion des membres et des groupes](members.md)
   * [Rapports](reports.md)

* Communautés [*outils*](tools.md):

   * [Modèles de site](sites.md)
   * [Modèles de groupe](tools-groups.md)
   * [Fonctions de la communauté](functions.md)
   * [Configuration du stockage](srp-config.md)
   * [Guide du composant](components-guide.md)
   * [Badges](badges.md)


### Contenu généré par l&#39;utilisateur {#user-generated-content}

L’une des principales fonctionnalités d’AEM Communities est la génération de contenu généré par les utilisateurs par les visiteurs connectés sur le site (membres). Pour en savoir plus sur l’utilisation du contenu créé par l’utilisateur, rendez-vous sur :

* [Magasin UGC commun](working-with-srp.md): choix de la SRP pour le stockage partagé du contenu créé par l’utilisateur
* [Modération du contenu créé par l’utilisateur](moderate-ugc.md): les membres approuvés peuvent modérer le contenu généré par l’utilisateur en masse ou en contexte.
* [Balisage UGC](tag-ugc.md): fonctionnalités peuvent être configurées pour permettre aux membres de baliser le contenu.
* [Traduire le contenu généré par l’utilisateur](translate-ugc.md): fonctionnalités peuvent être configurées pour traduire tout le contenu généré par les utilisateurs ou permettre aux membres de traduire les publications sélectionnées
* [Configuration Analytics](analytics.md): activation d’Adobe Analytics pour créer des rapports sur diverses mesures concernant l’activité des membres

### Membres de la communauté {#community-members}

* [Gestion des utilisateurs et des groupes d’utilisateurs](users.md): détails des membres de la communauté et des groupes de membres, y compris les membres privilégiés.
* [Limites de contribution](limits.md): possibilité de limiter la publication par les nouveaux membres.
* [Service Tunnel](deploy-communities.md#tunnel-service-on-author): permet d’accéder aux membres et aux groupes de membres côté publication à partir de l’environnement de création.
* [Consoles Membres et Groupes](members.md): permet de créer et de gérer des membres et des groupes de membres côté publication à partir de l’environnement de création.
* [Synchronisation des utilisateurs](sync.md): pour synchroniser les membres et les groupes de membres sur plusieurs instances de publication.
* [Connexion à Social avec Facebook et Twitter](social-login.md): possibilité pour les visiteurs du site de devenir membres de la communauté à l’aide de leurs informations d’identification Facebook ou Twitter.
* [Notation et badges](implementing-scoring.md): possibilité d’attribuer des badges pour identifier les rôles d’un membre et d’obtenir des badges grâce à sa participation à la communauté.
* [Notifications](notifications.md): possibilité pour les membres d’être informés de l’activité qu’ils suivent.
* [Abonnements](subscriptions.md): possibilité pour les membres d’interagir avec la communauté à l’aide de courriers électroniques externes.
* [Messagerie](messaging.md): possibilité pour les membres d’interagir avec la communauté à l’aide de messages internes.

### Déploiement {#deployment}

La section Déploiement contient des informations spécifiques à AEM Communities.

La nature de l’utilisation du contenu de la communauté influence la structure du déploiement :

* [Topologies recommandées pour Communities](topologies.md)

Il est important d’installer la dernière version de Communities sur la plateforme AEM :

* [Dernier Feature Pack Communities](deploy-communities.md#latestfeaturepack)

Consultez la page de déploiement pour obtenir d’autres informations spécifiques à Communities, telles que [Mise à niveau](upgrade.md), [Dispatcher](dispatcher.md), et [Réplication](deploy-communities.md#replication-agents-on-author).

## Documentation sur les communautés connexes {#related-communities-documentation}

* Visite [Déploiement de communautés](deploy-communities.md) où vous pouvez en savoir plus sur les déploiements recommandés.

* Visite [Développement de communautés](communities.md) où vous pouvez en savoir plus sur la structure de composants sociaux (SCF) et la personnalisation des composants et fonctionnalités de Communities.

* Visite [Création de composants Communities](author-communities.md) où vous pouvez apprendre à créer avec et configurer des composants Communities.
