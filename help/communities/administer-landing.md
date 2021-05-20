---
title: Sites Communities
seo-title: Sites Communities
description: Présentation de la documentation AEM Communities
seo-description: Présentation de la documentation AEM Communities
uuid: 9842ce6c-1af8-4b27-b199-07410e797ab2
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 8799386a-c3b8-43cf-9f71-580ff2a81abc
role: Administrator
exl-id: e3ffc73e-2bc5-492d-b64b-750cc7d8ab9b
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '478'
ht-degree: 9%

---

# Sites Communities {#communities-sites}

Cette section s’adresse à ceux qui gèrent AEM Communities et se familiarisent avec les fonctionnalités d’AEM Communities.

## Présentation {#overview}

Pour une présentation et des tutoriels de prise en main, rendez-vous sur :

* [Présentation d’AEM Communities](overview.md)
* [Prise en main d’AEM Communities](getting-started.md)
* [Prise en main d’AEM Communities pour l’activation](getting-started-enablement.md)

## Rubriques d’administration et de configuration {#administration-and-configuration-topics}

### Création et gestion du site des communautés {#communities-site-creation-and-management}

* Communautés [consoles](consoles.md)

   * [Sites](sites-console.md)

      * [Groupes (sous-communautés)](groups.md)
   * [Modération](moderation.md)
   * [Gestion des membres et des groupes](members.md)
   * [Ressources d’activation](resources.md)
   * [Rapports](reports.md)


* Communities [*tools*](tools.md) :

   * [Modèles de site](sites.md)
   * [Modèles de groupe](tools-groups.md)
   * [Fonctions de la communauté](functions.md)
   * [Stockage   Configuration](srp-config.md)
   * [Guide du composant](components-guide.md)
   * [Badges](badges.md)


### Contenu généré par l&#39;utilisateur {#user-generated-content}

L’une des principales fonctionnalités d’AEM Communities est la génération de contenu généré par les utilisateurs par les visiteurs connectés sur le site (membres). Pour en savoir plus sur l’utilisation du contenu créé par l’utilisateur, rendez-vous sur :

* [Magasin UGC commun](working-with-srp.md) : choix de la SRP pour le stockage partagé du contenu créé par l’utilisateur
* [Modération du contenu généré par l’utilisateur](moderate-ugc.md) : Les membres approuvés peuvent modérer le contenu généré par l’utilisateur en bloc ou en contexte.
* [Balisage du contenu généré par l’utilisateur](tag-ugc.md) : fonctions pouvant être configurées pour permettre aux membres de baliser le contenu
* [Traduction du contenu généré par l’utilisateur](translate-ugc.md) : fonctionnalités peuvent être configurées pour traduire tout le contenu généré par les utilisateurs ou permettre aux membres de traduire les publications sélectionnées
* [Configuration d’Analytics](analytics.md) : activation d’Adobe Analytics pour créer des rapports sur diverses mesures concernant l’activité des membres

### Membres de la communauté {#community-members}

* [Gestion des utilisateurs et des groupes d’utilisateurs](users.md) : détails des membres de la communauté et des groupes de membres, y compris les membres privilégiés.
* [Limites de contribution](limits.md) : capacité de limiter la publication par les nouveaux membres.
* [Service Tunnel](deploy-communities.md#tunnel-service-on-author) : permet d’accéder aux membres et aux groupes de membres côté publication à partir de l’environnement de création.
* [Consoles Membres et Groupes](members.md) : permet de créer et de gérer des membres et des groupes de membres côté publication à partir de l’environnement de création.
* [Synchronisation des utilisateurs](sync.md) : pour synchroniser les membres et les groupes de membres sur plusieurs instances de publication.
* [Connexion de réseau social avec Facebook et Twitter](social-login.md) : possibilité pour les visiteurs du site de devenir membres de la communauté à l’aide de leurs informations d’identification Facebook ou Twitter.
* [Notation et badges](implementing-scoring.md) : la capacité d’attribuer des badges pour identifier le(s) rôle(s) d’un membre et de gagner des badges grâce à sa participation à la communauté.
* [Notifications](notifications.md) : possibilité pour les membres d’être informés de l’activité qu’ils suivent.
* [Abonnements](subscriptions.md) : possibilité pour les membres d’interagir avec la communauté à l’aide de courriers électroniques externes.
* [Messagerie](messaging.md) : possibilité pour les membres d’interagir avec la communauté à l’aide de messages internes.

### Fonctionnalités d’activation {#enablement-features}

* [Configuration de l’activation](enablement.md) : informations nécessaires pour configurer correctement les fonctions d’activation.
* [Configuration d’Analytics](analytics.md) : informations nécessaires pour activer les fonctionnalités Adobe Analytics for Communities.
* [Balisage des ressources d’activation](tag-resources.md) : nécessaire pour créer des catalogues d’activation.

### Déploiement {#deployment}

La section Déploiement contient des informations spécifiques à AEM Communities.

La nature de l’utilisation du contenu de la communauté influence la structure du déploiement :

* [Topologies recommandées pour Communities](topologies.md)

Il est important d’installer la dernière version de Communities sur la plateforme AEM :

* [Dernier Feature Pack Communities](deploy-communities.md#latestfeaturepack)

Consultez la page de déploiement pour obtenir d’autres informations spécifiques à Communities, telles que la [mise à niveau](upgrade.md), [Dispatcher](dispatcher.md) et la [réplication](deploy-communities.md#replication-agents-on-author).

## Documentation sur les communautés associée {#related-communities-documentation}

* Visitez [Déploiement de communautés](deploy-communities.md) pour en savoir plus sur les déploiements recommandés.

* Visitez [Développement de communautés](communities.md) pour en savoir plus sur la structure de composants sociaux (SCF) et la personnalisation des composants et fonctionnalités de communautés.

* Consultez la section [Création de composants de communautés](author-communities.md) pour savoir comment créer et configurer des composants de communautés.
