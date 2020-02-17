---
title: Sites de communautés
seo-title: Sites de communautés
description: Présentation de la documentation des communautés AEM
seo-description: Présentation de la documentation des communautés AEM
uuid: 9842ce6c-1af8-4b27-b199-07410e797ab2
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 8799386a-c3b8-43cf-9f71-580ff2a81abc
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Communities Sites {#communities-sites}

Cette section s’adresse aux personnes qui gèrent les communautés AEM et qui se familiarisent avec les fonctionnalités des communautés AEM.

## Présentation {#overview}

Pour obtenir une présentation et des didacticiels de prise en main, visitez :

* [Présentation d’AEM Communities](overview.md)
* [Prise en main d’AEM Communities](getting-started.md)
* [Prise en main d’AEM Communities pour l’activation](getting-started-enablement.md)

## Rubriques d’administration et de configuration {#administration-and-configuration-topics}

### Collectivités Création et gestion de sites {#communities-site-creation-and-management}

* Consoles [de communautés](consoles.md)

   * [Sites](sites-console.md)

      * [Groupes (sous-communautés)](groups.md)
   * [Modération](moderation.md)
   * [Gestion des membres et des groupes](members.md)
   * [Ressources d&#39;activation](resources.md)
   * [Rapports](reports.md)


* Outils [*de communautés *](tools.md):

   * [Modèles de site](sites.md)
   * [Modèles de groupe](tools-groups.md)
   * [Fonctions de la communauté](functions.md)
   * [Configuration du stockage](srp-config.md)
   * [Guide du composant](components-guide.md)
   * [Badges](badges.md)


### Contenu généré par l&#39;utilisateur {#user-generated-content}

L’une des principales fonctionnalités des communautés AEM est la génération de contenu généré par les utilisateurs (UGC) par les visiteurs (membres) du site connectés. Pour en savoir plus sur l&#39;utilisation de l&#39;UGC, visitez :

* [Magasin](working-with-srp.md)UGC commun : choix du SRP pour le stockage partagé de l&#39;UGC
* [Modération de l’UGC](moderate-ugc.md): les membres de confiance peuvent modérer les CU en bloc ou dans le contexte
* [Balisage UGC](tag-ugc.md): fonctionnalités peuvent être configurées pour permettre aux membres de baliser le contenu
* [Traduction de l’UGC](translate-ugc.md): peut être configurée pour traduire toutes les UGC ou permettre aux membres de traduire les publications sélectionnées
* [Configuration](analytics.md)d’Analytics : activation d’Adobe Analytics pour la création de rapports sur diverses mesures concernant l’activité des membres

### Membres de la communauté {#community-members}

* [Gestion des utilisateurs et des groupes](users.md)d’utilisateurs : détails sur les membres de la communauté et les groupes membres, y compris les membres privilégiés
* [Limites](limits.md)des contributions : capacité de limiter la publication par les nouveaux membres
* [Service](deploy-communities.md#tunnel-service-on-author)tunnel : permet d’accéder aux membres et aux groupes de membres côté publication depuis l’environnement d’auteur
* [Consoles Membres et Groupes](members.md): permet de créer et de gérer des membres et des groupes de membres côté publication à partir de l’environnement d’auteur
* [Synchronisation](sync.md)utilisateur : pour synchroniser des membres et des groupes de membres sur plusieurs instances de publication
* [Connexion aux réseaux sociaux avec Facebook et Twitter](social-login.md): possibilité pour les visiteurs du site de devenir membres de la communauté à l’aide de leurs identifiants Facebook ou Twitter
* [Score et insignes](implementing-scoring.md): capacité d&#39;attribuer des badges pour déterminer le ou les rôles d&#39;un membre et pour que les membres obtiennent des badges en participant à la collectivité
* [Notifications](notifications.md): capacité pour les membres d&#39;être informés de l&#39;activité qu&#39;ils suivent
* [Abonnements](subscriptions.md): capacité des membres à interagir avec la communauté à l’aide de courriers électroniques externes
* [Messagerie](messaging.md): capacité des membres à interagir avec la communauté à l&#39;aide de messages internes

### Fonctionnalités d’activation {#enablement-features}

* [Configuration de l&#39;activation](enablement.md): informations nécessaires pour configurer correctement les fonctions d&#39;activation
* [Configuration](analytics.md)d’Analytics : informations nécessaires pour activer les fonctionnalités d’Adobe Analytics pour les communautés
* [Ressources](tag-resources.md)d&#39;activation du balisage : nécessaire à la création de catalogues d’activation

### Déploiement {#deployment}

La section de déploiement contient des informations spécifiques aux communautés AEM.

La nature de l&#39;utilisation du contenu communautaire influe sur la structure du déploiement :

* [Topologies recommandées pour Communities](topologies.md)

Il est important d’installer la dernière version des Communautés sur la plateforme AEM :

* [Pack de fonctionnalités des dernières communautés](deploy-communities.md#latestfeaturepack)

Consultez la page de déploiement pour obtenir des informations spécifiques à d’autres communautés, telles que [Mise à niveau](upgrade.md), [Répartiteur](dispatcher.md) et [Réplication](deploy-communities.md#replication-agents-on-author).

## Documentation sur les communautés associée {#related-communities-documentation}

* Visit [Deploying Communities](deploy-communities.md) to learn about recommended deployments.

* Visit [Developing Communities](communities.md) to learn about the social component framework (SCF) and customizing Communities components and features.

* Visitez [Création de composants](author-communities.md) de communautés pour apprendre à créer et à configurer des composants de communautés.
