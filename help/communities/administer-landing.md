---
title: Sites des communautés
seo-title: Sites des communautés
description: Présentation de la documentation AEM Communities
seo-description: Présentation de la documentation AEM Communities
uuid: 9842ce6c-1af8-4b27-b199-07410e797ab2
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 8799386a-c3b8-43cf-9f71-580ff2a81abc
translation-type: tm+mt
source-git-commit: 2bd74d5e90aff1146de5c5a0dffd99fc7dd9031c
workflow-type: tm+mt
source-wordcount: '478'
ht-degree: 9%

---


# Communities Sites {#communities-sites}

Cette section s’adresse à ceux qui gèrent l’AEM Communities et se familiarisent avec les fonctionnalités de AEM Communities.

## Présentation {#overview}

Pour une présentation et des didacticiels de prise en main, visitez :

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


* [*Outils des communautés*](tools.md):

   * [Modèles de site](sites.md)
   * [Modèles de groupe](tools-groups.md)
   * [Fonctions de la communauté](functions.md)
   * [Configuration du stockage](srp-config.md)
   * [Guide du composant](components-guide.md)
   * [Badges](badges.md)


### Contenu généré par l&#39;utilisateur {#user-generated-content}

L’une des principales fonctionnalités d’AEM Communities est la génération de contenu généré par les utilisateurs (UGC) par des visiteurs (membres) du site signés. Pour en savoir plus sur l&#39;utilisation de l&#39;UGC, visitez :

* [Boutique](working-with-srp.md)UGC commune : choix du PRS pour l&#39;enregistrement partagé de l&#39;UGC
* [Modération de l&#39;UGC](moderate-ugc.md): les membres de confiance peuvent modérer les CU en bloc ou dans le contexte
* [Balisage UGC](tag-ugc.md): peut être configuré pour permettre aux membres de marquer le contenu
* [Traduction de l&#39;UGC](translate-ugc.md): peut être configuré pour traduire tous les UGC ou permettre aux membres de traduire les publications sélectionnées
* [Configuration](analytics.md)d’Analytics : activation de Adobe Analytics pour créer des rapports sur diverses mesures concernant l’activité des membres

### Membres de la communauté {#community-members}

* [Gestion des utilisateurs et des groupes](users.md)d’utilisateurs : des détails sur les membres de la communauté et les groupes de membres, y compris les membres privilégiés.
* [Limites](limits.md)des contributions : capacité de limiter la publication par les nouveaux membres.
* [Service](deploy-communities.md#tunnel-service-on-author)du tunnel : permet d’accéder aux membres et aux groupes de membres côté publication depuis l’environnement d’auteur.
* [Consoles](members.md)Membres et Groupes : permet de créer et de gérer des membres et des groupes de membres côté publication à partir de l’environnement d’auteur.
* [Synchronisation](sync.md)utilisateur : pour synchroniser des membres et des groupes de membres sur plusieurs instances de publication.
* [Connexion aux réseaux sociaux avec Facebook et Twitter](social-login.md): possibilité pour les visiteurs du site de devenir membres de la communauté à l’aide de leurs identifiants Facebook ou Twitter.
* [Scores et insignes](implementing-scoring.md): capacité d&#39;attribuer des badges pour identifier le ou les rôles d&#39;un membre et permettre aux membres d&#39;obtenir des badges en participant à la communauté.
* [Notifications](notifications.md): capacité pour les membres d&#39;être informés de l&#39;activité qu&#39;ils suivent.
* [Abonnements](subscriptions.md): capacité des membres à interagir avec la communauté à l’aide de courriers électroniques externes.
* [Messagerie](messaging.md): capacité des membres à interagir avec la communauté à l&#39;aide de messages internes.

### Fonctionnalités d’activation {#enablement-features}

* [Configuration de l&#39;activation](enablement.md): informations nécessaires pour configurer correctement les fonctions d’activation.
* [Configuration](analytics.md)d’Analytics : informations nécessaires pour activer les fonctionnalités Adobe Analytics for Communities.
* [Ressources](tag-resources.md)d&#39;activation du balisage : nécessaire pour créer des catalogues d’activation.

### Déploiement {#deployment}

La section de déploiement contient des informations spécifiques à AEM Communities.

La nature de l’utilisation du contenu communautaire influence la structure du déploiement :

* [Topologies recommandées pour Communities](topologies.md)

Il est important d’installer la version la plus récente des communautés sur la plateforme AEM :

* [Pack de fonctionnalités des dernières communautés](deploy-communities.md#latestfeaturepack)

Consultez la page de déploiement pour obtenir des informations spécifiques à d’autres communautés, telles que [Mise à niveau](upgrade.md), [Répartiteur et](dispatcher.md) Réplication [](deploy-communities.md#replication-agents-on-author).

## Documentation sur les communautés associée {#related-communities-documentation}

* Visit [Deploying Communities](deploy-communities.md) to learn about recommended deployments.

* Visit [Developing Communities](communities.md) to learn about the social component framework (SCF) and customizing Communities components and features.

* Visitez la page Composants [Communautés](author-communities.md) de création pour découvrir comment créer et configurer des composants Communautés.
