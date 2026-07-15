---
title: Présentation d’AEM Communities
description: Découvrez les principes de base des fonctionnalités et de la configuration de Adobe Experience Manager Communities.
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
docset: aem65
exl-id: d6243dff-a067-455c-a326-5f451f225efd
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '1331'
ht-degree: 1%

---

# Présentation d’AEM Communities {#aem-communities-overview}

Les communautés Adobe Experience Manager (AEM) vous permettent de créer rapidement un site communautaire on-premise qui a amélioré les performances, amélioré la gestion du site et encourage la conversion des visiteurs du site en membres précieux de la communauté.

## Fonctionnalités de Communities {#communities-features}

AEM Communities permet de développer une relation avec les visiteurs du site, ce qui :

* **informe** par le biais de blogs, de questions-réponses et de calendriers d’événements,
* Tout en **obtenant des informations** par le biais de forums, de commentaires et d’autres contenus de communauté, souvent appelés contenu créé par l’utilisateur ou l’utilisatrice (UGC).
* Il permet la **modération** par des membres de confiance dans l’environnement de publication,
* **Connexion sociale** avec Twitter et Facebook,
* **traduction en ligne** du contenu de la communauté,
* **création de groupes communautaires** à partir du site communautaire publié,
* **Notation** pour attribuer des badges,
* **Partage de fichiers**
* **Notifications** et **flux d’activités**,
* Permet **balisage** (@mention) aux autres membres enregistrés dans le contenu créé par l’utilisateur d’attirer leur attention.

Les fonctionnalités de Communities peuvent être démontrées à l’aide de la [machine de démonstration d’](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki) disponible publiquement sur GitHub.com ou avec la nouvelle implémentation de référence de `We.Retail`.

## Sites de la communauté {#community-sites}

Un site communautaire est un site AEM créé à l’aide d’un simple assistant qui génère un site web avec de nombreuses fonctionnalités courantes pré-connectées dans le site.

L&#39;assistant [ création de site ](/help/communities/sites-console.md) :

* Assemble les fonctionnalités du site, en fonction du [modèle de site de la communauté](/help/communities/sites.md) sélectionné, qui est :

   * construit à partir de [fonctions de la communauté](#community-functions)
   * fonctionnalité facultative [groupes de la communauté](#communitygroups)

* Utilise les paramètres pour configurer :

   * modération
   * connexion
   * traduction

* Fournit des fonctionnalités essentielles :

   * Responsive design : utilise [thèmes Twitter Bootstrap](https://getbootstrap.com)

   * Connexion : auto-inscription, [connexion au réseau social](/help/communities/social-login.md), profils utilisateur

      * Notifications:
les membres voient les événements qui les concernent et le contenu généré par l&#39;utilisateur où ils se trouvent [](/help/communities/overview.md#mentionssupport).

      * Messages : les membres peuvent envoyer ou recevoir des messages sur le site de la communauté.
      * Recherche : possibilité de rechercher dans le site de la communauté.
      * Changement de langue : possibilité de sélectionner une langue pour un [site multilingue](/help/sites-administering/translation.md).

      * Administration : accès pour les membres autorisés à modérer et gérer les utilisateurs au sein du site de la communauté.

* Élimine de nombreuses étapes de création au niveau de la page :

   * Image de marque : chargement facultatif d’une image de bannière à afficher sur toutes les pages du site de la communauté
   * Menu de navigation : des liens de navigation sont fournis pour les fonctionnalités incluses dans le modèle de site de la communauté.

Pour découvrir la facilité de création rapide d’un site communautaire, consultez [Prise en main d’AEM Communities](/help/communities/getting-started.md).

## Persistance du contenu de la communauté {#community-content-persistence}

Pour améliorer les performances et la synchronisation du contenu de la communauté, AEM Communities a besoin d’un magasin commun conçu spécifiquement pour le contenu créé par l’utilisateur (UGC) partagé entre toutes les instances AEM (création et publication).

Le contenu de la communauté est facilement accessible via le fournisseur de ressources de stockage (SRP), qui fournit une couche pour séparer l’accès de la topologie sous-jacente et prend en charge un magasin commun pour le contenu créé par l’utilisateur.

Pour en savoir plus sur la persistance du contenu de la communauté et les déploiements recommandés, voir :

* [Community Content Storage](/help/communities/working-with-srp.md) : présente les options de stockage SRP disponibles pour le contenu créé par l’utilisateur.
* [Topologies recommandées](/help/communities/topologies.md) : présente les topologies en fonction du cas d’utilisation et du choix du SRP.
* [Mise à niveau vers AEM 6.5 Communities](/help/communities/upgrade.md) : fournit des informations utiles sur le contenu créé par l’utilisateur lors du passage à AEM 6.5.

## Consoles Communities {#communities-consoles}

Dans l’environnement de création, la console de navigation globale permet d’accéder à la [console Communities](/help/communities/consoles.md), qui contient les éléments suivants :

* La console [Sites](/help/communities/sites-console.md)

   * Création de site
   * Modification du site
   * Gestion de site
   * Console [Groupes de la communauté](/help/communities/groups.md)

* Console [Modération](/help/communities/moderation.md)

   * Interface utilisateur commune de modération en bloc pour les environnements de création et de publication.
   * Nouveaux critères de filtrage.

* Consoles de gestion [Membres et groupes](/help/communities/members.md)

   * Permet de créer et de gérer des utilisateurs (membres) côté publication à partir de l’environnement de création.
   * Permet d&#39;interdire les membres.
   * Permet de créer et de gérer des groupes d’utilisateurs côté publication (groupes membres) à partir de l’environnement de création.

* Console [Rapports](/help/communities/reports.md)

   * Permet de générer des rapports sur les affectations, les publications et les vues.

La console Outils globaux permet d’accéder aux outils de communautés suivants :

* Console [ Modèles de site ](/help/communities/tools.md#sitetemplatesconsole)

   * Créer et gérer des modèles de site de la communauté.

* Console [Modèles de groupe](/help/communities/tools.md#grouptemplatesconsole)

   * Créez et gérez des modèles de groupes communautaires.

* Console [Fonctions de la communauté](/help/communities/tools.md#communityfunctionsconsole)

   * Créer et gérer des fonctions de communauté.

* Console [Configuration de stockage](/help/communities/tools.md#storageconfiguratonconsole)

   * Sélectionnez et configurez le [magasin commun](/help/communities/working-with-srp.md) pour le site.

* [Guide du composant](/help/communities/components-guide.md)

   * Un exemple de site, [Composants de communauté](https://localhost:4502/editor.html/content/community-components/en.html) fournit un exemple de tous les composants de communauté avec leur configuration par défaut et la possibilité de les tester.

## Modèles de site de communauté {#community-site-templates}

La création d’un site communautaire repose sur la sélection d’un modèle de site communautaire pour configurer rapidement un site communautaire indépendant de tout exemple de site.

Un modèle de site communautaire, composé de fonctions de communauté et de modèles de groupe communautaire, fournit la structure d’un site communautaire. Cela inclut les fonctionnalités de connexion, de profils utilisateur, de messagerie, de menu de site, de recherche, de thème et de branding.

Voir la [console Modèles de site](/help/communities/sites.md).

## Fonctions de la communauté {#community-functions}

Les caractéristiques attendues d’une expérience communautaire sont bien connues. Avec AEM Communities, ces fonctionnalités sont disponibles sous la forme de blocs de création, connus sous le nom de fonctions de communauté.

Les fonctions de communauté sont des pages AEM normales. Elles comprennent des composants connectés dans une fonctionnalité qui est facilement incorporée dans un modèle de site de communauté.

Voir la [console Fonctions de la communauté](/help/communities/functions.md).

## Groupes de la communauté et modèles de groupe {#community-groups-and-group-templates}

La fonctionnalité de groupes de communautés permet à une sous-communauté d’être créée dynamiquement dans un site communautaire par des utilisateurs autorisés et des membres de la communauté des environnements de création et de publication.

À partir de l’environnement de création, des groupes de communautés (sous-communautés) peuvent être créés dans un site de communauté existant ou imbriqués dans un groupe existant, lorsque la structure du modèle contient la fonction [Groups](/help/communities/functions.md#groups-function).

La création d’un groupe de la communauté nécessite la sélection d’un modèle de groupe de la communauté qui fournit la conception des pages du groupe de la communauté. Lorsqu’une fonction Groupes est ajoutée à une structure de modèle, elle est configurée pour spécifier un modèle de groupe ou pour fournir un choix de modèles au moment de la création d’un groupe de la communauté.

Voir également :

* [Console Groupes de sites](/help/communities/groups.md) pour créer des sous-communautés dans l’environnement de création.
* [Console Modèles de groupe](/help/communities/tools-groups.md) pour créer des structures de site pour des groupes.
* [Prise en main d’AEM Communities](/help/communities/getting-started.md) pour un tutoriel sur la création rapide d’un site communautaire comprenant des groupes imbriqués.

## Composants de communauté {#community-components}

Les [composants de communauté](/help/communities/author-communities.md) à partir desquels un site de communauté est créé peuvent être utilisés pour ajouter des fonctions de communautés à n’importe quel site AEM.

Le [guide des composants de la communauté](/help/communities/components-guide.md) est disponible pour une exploration interactive des composants.

## Communauté d’engagement {#engagement-community}

Une communauté d’engagement est un site communautaire axé sur l’engagement des clients pour informer, solliciter des commentaires et permettre aux clients d’interagir en tant que membres de la communauté.

Les caractéristiques d’une communauté d’engagement peuvent inclure :

* Connexion
* Message
* Forums
* Commentaires
* Révisions
* Évaluations
* Votant
* Blogs
* Groupes
* Calendriers
* Traduction
* Modération
* Notifications
* Notation et badges
* Création de rapports Analytics

Pour découvrir la facilité de création rapide d’une communauté d’engagement, consultez [Prise en main d’AEM Communities](/help/communities/getting-started.md).

## Machine de démonstration AEM {#aem-demo-machine}

La [machine de démonstration ](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine) gère et exécute des démonstrations pour AEM [Sites](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Scenario%20Sites), [Assets](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Scenario%20Assets), [Communities](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Scenario%20Communities), [Apps](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Scenario%20Apps) et [Forms](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Scenario%20Forms), qui nécessitent souvent plus de configuration que le simple lancement d’une instance QuickStart. La machine de démonstration d’AEM configure d’autres [infrastructures](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Infrastructure) telles que MongoDB, Solr, MySQL, FFmpeg et des serveurs de messagerie.

La machine de démonstration AEM comprend :

* Une [interface utilisateur graphique](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/User%20Interface).
* Scripts ANT Apache avec [propriétés](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Properties) et [cibles](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Command%20Line) configurables.

* Packages à installer.

La machine de démonstration AEM a été testée avec succès avec CQ 5.5, CQ 5.6.1, AEM 6.0, AEM 6.1, AEM 6.2, AEM 6.3 et AEM 6.4 sous Windows, macOS et Linux®.

La machine de démonstration AEM nécessite une licence AEM valide.

>[!NOTE]
>
>Regardez une [vidéo d’introduction](https://www.youtube.com/watch?v=zEE_zkR9fVQ&feature=youtu.be) à la machine de démonstration AEM (13:26).

## Documentation AEM Communities {#aem-communities-documentation}

* Consultez [Déploiement de communautés](deploy-communities.md) où vous trouverez des informations sur les déploiements recommandés.
* Rendez-vous sur la page [Administration des sites de communautés](administer-landing.md) pour en savoir plus sur la création d’un site communautaire, l’ajout de groupes communautaires, la configuration de modèles de site communautaire, la modération du contenu de la communauté, la gestion des membres, le balisage, les notifications, la notation et les badges.
* Consultez [Développement de communautés](communities.md) où vous pouvez en savoir plus sur le framework de composants sociaux (SCF) et sur la personnalisation des composants et fonctionnalités de communautés.
* Consultez [Création de composants de communautés](author-communities.md) où vous pouvez apprendre à créer avec des composants de communautés et à les configurer.
