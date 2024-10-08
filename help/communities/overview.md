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
source-wordcount: '1204'
ht-degree: 2%

---

# Présentation d’AEM Communities {#aem-communities-overview}

Adobe Experience Manager (AEM) Communities vous permet de créer rapidement un site de communauté sur site qui améliore les performances, améliore la gestion du site et encourage la conversion des visiteurs du site en membres de la communauté de grande valeur.

## Fonctions de communauté {#communities-features}

AEM Communities permet le développement d’une relation avec les visiteurs du site qui :

* **Informs** par le biais de blogs, de questions et réponses et de calendriers d’événements,
* Pendant que **obtient des insights** par le biais de forums, de commentaires et d’autres contenus de la communauté, souvent appelés contenu généré par l’utilisateur.
* Il permet la **modération** par les membres de confiance dans l’environnement Publish,
* **Connexion sociale** avec Twitter et Facebook,
* **Traduction en ligne** du contenu de la communauté,
* **Création de groupes communautaires** à partir du site de communauté publié,
* **Scoring** pour attribuer des badges,
* **Partage de fichiers**,
* **Notifications** et **Flux d’activités**,
* Permet à **tagging** (@mention) d’autres membres enregistrés dans le contenu généré par l’utilisateur d’attirer leur attention.

Les fonctionnalités de communauté peuvent être démontrées à l’aide de la [AEM Demo Machine](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki) disponible publiquement sur GitHub.com ou avec la nouvelle implémentation de référence `We.Retail`.

## Sites de la communauté {#community-sites}

Un site communautaire est un site AEM créé à l’aide d’un assistant simple qui génère un site web avec de nombreuses fonctionnalités courantes pré-câblées dans le site.

L&#39; [assistant de création de site](/help/communities/sites-console.md) :

* Assemble les fonctionnalités du site, en fonction du [ modèle de site communautaire](/help/communities/sites.md) sélectionné, à savoir :

   * créé à partir des [fonctions de communauté](#community-functions)
   * fonction facultative [groupes de communautés](#communitygroups)

* Utilise les paramètres à configurer :

   * modération
   * login
   * traduction

* Fournit les fonctionnalités essentielles :

   * Responsive design : utilise les [thèmes de Bootstrap de Twitter](https://getbootstrap.com)

   * Connexion : auto-inscription, [connexion sociale](/help/communities/social-login.md), profils utilisateur

      * Notifications :
les membres voient les événements qui les intéressent et le contenu généré par l’utilisateur où ils sont [@mentioned](/help/communities/overview.md#mentionssupport).

      * Messagerie : les membres peuvent envoyer ou recevoir des messages sur le site de la communauté.
      * Recherche : possibilité de rechercher dans le site de la communauté.
      * Changement de langue : possibilité de sélectionner une langue pour un [site multilingue](/help/sites-administering/translation.md).

      * Administration : accès pour les membres autorisés afin de modérer et de gérer les utilisateurs sur le site de la communauté.

* Élimine de nombreuses étapes de création au niveau de la page :

   * Marque : téléchargement facultatif d’une image de bannière à afficher sur toutes les pages du site de la communauté
   * Menu de navigation : les liens de navigation sont fournis pour les fonctionnalités incluses dans le modèle de site de la communauté.

Pour découvrir la facilité de création rapide d’un site communautaire, consultez la page [Prise en main d’AEM Communities](/help/communities/getting-started.md).

## Persistance du contenu communautaire {#community-content-persistence}

Pour améliorer les performances et la synchronisation du contenu de la communauté, AEM Communities nécessite un magasin commun spécifique au contenu généré par l’utilisateur (UGC) partagé entre toutes les instances d’AEM (auteur et publication).

Le contenu de la communauté est facilement accessible par le biais du fournisseur de ressources de stockage (SRP), qui fournit une couche pour séparer l’accès de la topologie sous-jacente et prend en charge un magasin commun pour le contenu généré par l’utilisateur.

Pour en savoir plus sur la persistance du contenu de la communauté et les déploiements recommandés, voir :

* [Stockage de contenu de la communauté](/help/communities/working-with-srp.md) : aborde les options de stockage SRP disponibles pour le contenu généré par l’utilisateur.
* [Topologies recommandées](/help/communities/topologies.md) : aborde les topologies en fonction du cas d’utilisation et du choix de la SRP.
* [Mise à niveau vers AEM 6.5 Communities](/help/communities/upgrade.md)—fournit des informations utiles sur le contenu créé par l’utilisateur lors du passage à AEM 6.5.

## Consoles Communities {#communities-consoles}

Dans l’environnement de création, la console de navigation globale permet d’accéder à la [console Communautés](/help/communities/consoles.md), qui contient :

* La console [Sites](/help/communities/sites-console.md)

   * Création de site
   * Modification du site
   * Gestion de site
   * Console [Groupes communautaires](/help/communities/groups.md)

* Console [Modération](/help/communities/moderation.md)

   * Interface utilisateur de modération en bloc courante pour les environnements de création et de Publish.
   * Nouveaux critères de filtrage.

* Consoles de gestion [Membres et groupes](/help/communities/members.md)

   * Permet de créer et de gérer des utilisateurs (membres) côté publication à partir de l’environnement de création.
   * Permet d&#39;interdire les membres.
   * Permet de créer et de gérer des groupes d’utilisateurs (groupes de membres) côté publication à partir de l’environnement de création.

* Console [Rapports](/help/communities/reports.md)

   * Vous permet de générer des rapports sur les affectations, les publications et les vues.

La console d’outils globale permet d’accéder aux outils Communities suivants :

* Console [Modèles de site](/help/communities/tools.md#sitetemplatesconsole)

   * Créez et gérez des modèles de site de communauté.

* Console [Modèles de groupe](/help/communities/tools.md#grouptemplatesconsole)

   * Créez et gérez des modèles de groupe de communautés.

* Console [Fonctions de communauté](/help/communities/tools.md#communityfunctionsconsole)

   * Créez et gérez des fonctions de communauté.

* Console [Configuration de stockage](/help/communities/tools.md#storageconfiguratonconsole)

   * Sélectionnez et configurez le [magasin commun](/help/communities/working-with-srp.md) pour le site.

* [Guide du composant](/help/communities/components-guide.md)

   * Un exemple de site, [Composants de la communauté](https://localhost:4502/editor.html/content/community-components/en.html) fournit un exemple de tous les composants de la communauté avec leur configuration par défaut et la possibilité de les tester.

## Modèles de site de communauté {#community-site-templates}

La création d’un site de communauté est basée sur la sélection d’un modèle de site de communauté afin de configurer rapidement un site de communauté indépendant de tout exemple de site.

Un modèle de site de communauté, composé de fonctions de communauté et de modèles de groupe de communautés, fournit la structure d’un site de communauté. Il comprend les fonctionnalités de connexion, de profil utilisateur, de messagerie, de menu du site, de recherche, de thème et de marque.

Voir la [console Modèles de site](/help/communities/sites.md).

## Fonctions de la communauté {#community-functions}

Les caractéristiques attendues d’une expérience communautaire sont bien connues. Avec AEM Communities, ces fonctionnalités sont disponibles sous la forme de blocs de création, appelés fonctions de communauté.

Les fonctions de communauté sont des pages d’AEM normales qui comprennent des composants connectés dans une fonctionnalité facilement intégrée à un modèle de site de communauté.

Voir la [console des fonctions de la communauté](/help/communities/functions.md).

## Groupes communautaires et modèles de groupe {#community-groups-and-group-templates}

La fonctionnalité de groupes de communautés permet à une sous-communauté d’être créée dynamiquement dans un site de communauté par des utilisateurs autorisés et des membres de la communauté à partir des environnements de création et de publication.

Dans l’environnement de création, les groupes de communautés (sous-communautés) peuvent être créés dans un site de communauté existant ou imbriqués dans un groupe existant, lorsque la structure du modèle contient la [fonction Groupes](/help/communities/functions.md#groups-function).

La création d’un groupe de communautés nécessite la sélection d’un modèle de groupe de communautés qui fournit la conception des pages de groupe de communautés. Lorsqu’une fonction Groupes est ajoutée à une structure de modèle, elle est configurée pour spécifier un modèle de groupe ou pour offrir un choix de modèles au moment de la création d’un groupe de communautés.

Voir également :

* [Console Groupes de sites](/help/communities/groups.md) pour créer des sous-communautés dans l’environnement de création.
* [Console Modèles de groupe](/help/communities/tools-groups.md) pour créer des structures de site pour les groupes.
* [Prise en main d’AEM Communities](/help/communities/getting-started.md) pour obtenir un tutoriel sur la création rapide d’un site communautaire comprenant des groupes imbriqués.

## Composants de la communauté {#community-components}

Les [composants de communauté](/help/communities/author-communities.md) à partir desquels un site de communauté est créé peuvent être utilisés pour ajouter des fonctionnalités de communauté à n’importe quel site AEM.

Le [guide des composants de la communauté](/help/communities/components-guide.md) est disponible pour l’exploration interactive des composants.

## Communauté d’engagement {#engagement-community}

Une communauté d’engagement est un site communautaire axé sur l’interaction entre les clients et leur permettant d’informer, de solliciter des commentaires et d’interagir en tant que membres de la communauté.

Les caractéristiques d’une communauté d’engagement peuvent être les suivantes :

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
* Rapports Analytics

Pour découvrir la facilité de création rapide d’une communauté d’engagement, consultez la page [Prise en main d’AEM Communities](/help/communities/getting-started.md).

## AEM Demo Machine {#aem-demo-machine}

La [AEM Demo Machine](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine) gère et exécute des démonstrations pour AEM [Sites](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Scenario%20Sites), [Assets](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Scenario%20Assets), [Communities](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Scenario%20Communities), [Apps](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Scenario%20Apps) et [Forms](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Scenario%20Forms), qui nécessitent souvent plus de configuration que de simplement lancer une instance QuickStart. AEM Demo Machine configure une [infrastructure](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Infrastructure) supplémentaire comme MongoDB, Solr, MySQL, FFmpeg et les serveurs de messagerie.

La machine de démonstration AEM comprend :

* Une [interface utilisateur graphique](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/User%20Interface).
* Scripts Apache ANT avec [properties](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Properties) et [cibles](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Command%20Line) configurables.

* Packages à installer.

AEM Demo Machine a été testé avec succès avec CQ 5.5, CQ 5.6.1, AEM 6.0, AEM 6.1, 6.2, 6.3 et 6.4 sous Windows, macOS et Linux®.

AEM Demo Machine nécessite une licence AEM valide.

>[!NOTE]
>
>Affichez une [présentation vidéo](https://www.youtube.com/watch?v=zEE_zkR9fVQ&amp;feature=youtu.be) sur la AEM Demo Machine (13:26).

## Documentation AEM Communities {#aem-communities-documentation}

* Visitez [Déploiement de communautés](deploy-communities.md) où vous pouvez en savoir plus sur les déploiements recommandés.
* Visitez [Administration de sites de communautés](administer-landing.md) où vous pouvez en savoir plus sur la création d’un site de communauté, l’ajout de groupes de communautés, la configuration de modèles de site de communauté, la modération de contenu de communauté, la gestion des membres, le balisage, les notifications, la notation et les badges.
* Consultez [Développement de communautés](communities.md) où vous pouvez en savoir plus sur la structure de composants sociaux (SCF) et la personnalisation des composants et fonctionnalités de communautés.
* Visitez la page [Création de composants de communautés](author-communities.md) où vous pouvez apprendre à créer et configurer des composants de communautés.
