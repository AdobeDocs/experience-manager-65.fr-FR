---
title: Présentation d’AEM Communities
seo-title: Présentation d’AEM Communities
description: Présentation des fonctionnalités et de la configuration des communautés AEM
seo-description: Présentation des fonctionnalités et de la configuration des communautés AEM
uuid: 14405847-36ae-4958-bdc6-d799ecd05f06
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 44374006-f711-4af8-a1fe-f89164f79581
docset: aem65
translation-type: tm+mt
source-git-commit: 70e6f2d8366456e5091b7b775dc40914948921ab

---


# Présentation d’AEM Communities{#aem-communities-overview}

Adobe Experience Manager (AEM) Communities permet de créer rapidement un site de communauté local doté de performances et d’une gestion de sites améliorées, et qui encourage les visiteurs à devenir membres de la communauté.

Contactez votre gestionnaire de compte pour plus d’informations sur la licence des communautés AEM, ainsi que sur les licences supplémentaires pour les fonctionnalités d’activation et Adobe Analytics.

## Fonctionnalités des communautés {#communities-features}

Les communautés AEM permettent le développement d’une relation avec les visiteurs du site, qui :

* **informe** par le biais de blogs, de questions et réponses et de calendriers d’événements,
* pendant que **vous obtenez des informations **via des forums, des commentaires et d’autres contenus de la communauté, souvent appelés contenu généré par l’utilisateur (UGC).
* Il permet** la modération **par les membres de confiance dans l’environnement de publication,
* **connexion sociale **avec Twitter et Facebook,
* **traduction** en ligne de contenu communautaire,
* **création de groupes communautaires **à partir du site communautaire publié,
* **notation **pour attribuer des badges,
* **partage** de fichiers,
* **notifications **et flux **d’** activité,

* permet au **balisage** (@mentions) d’autres membres enregistrés dans le contenu généré par l’utilisateur, d’attirer leur attention.
* Prend en charge la navigation **par** clavier sur les composants d’activation (par exemple, Lecture de catalogue et de cours, Affectations, Bibliothèque de fichiers).

Les fonctionnalités des communautés peuvent être démontrées à l’aide de la machine [de démonstration](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki) AEM disponible publiquement sur GitHub.com ou avec la nouvelle implémentation de référence We.Retail.

## Sites communautaires {#community-sites}

Un site communautaire est un site AEM créé à l’aide d’un assistant simple qui génère un site Web avec de nombreuses fonctionnalités courantes pré-connectées au site.

Assistant [de création de](/help/communities/sites-console.md)site :

* assemble les fonctionnalités du site, en fonction du modèle [de site](/help/communities/sites.md) communautaire sélectionné, qui est :

   * construit à partir de fonctions [communautaires](#community-functions)
   * fonction facultative des groupes [de](#communitygroups) communauté

* utilise les paramètres pour configurer :

   * modération
   * Connexion
   * traduction

* fournit les fonctionnalités essentielles :

   * conception adaptée :
utilise les thèmes [Twitter Bootstrap](https://getbootstrap.com)

   * login :
auto-inscription, connexion [](/help/communities/social-login.md)sociale, profils utilisateur

   * notifications :
les membres voient les événements qui les concernent et le contenu généré par l’utilisateur où ils sont [@mentionnés](/help/communities/overview.md#mentionssupport).

   * messagerie :
les membres peuvent envoyer ou recevoir des messages sur le site communautaire
   * search :
capacité de recherche dans le site communautaire
   * changement de langue :
possibilité de sélectionner une langue pour un site [multilingue](/help/sites-administering/translation.md)

   * administration :
accès des membres autorisés à modérer et à gérer les utilisateurs du site communautaire

* élimine de nombreuses étapes de création au niveau de la page :

   * marque :
téléchargement facultatif d’une image de bannière à afficher sur toutes les pages du site de la communauté
   * menu de navigation :
des liens de navigation sont fournis pour les fonctionnalités incluses dans le modèle de site communautaire.

Pour découvrir la facilité de création rapide d’un nouveau site communautaire, consultez [Prise en main des communautés](/help/communities/getting-started.md)AEM.

## Persistance du contenu de la communauté {#community-content-persistence}

Pour améliorer les performances et la synchronisation du contenu de la communauté, les communautés AEM nécessitent un magasin commun spécifique pour le contenu généré par l’utilisateur (UGC) partagé entre toutes les instances AEM (auteur et publication).

Le contenu de la communauté est facilement accessible via le fournisseur de ressources de stockage (SRP), qui fournit une couche pour séparer l&#39;accès de la topologie sous-jacente et prend en charge un magasin commun pour l&#39;UGC.

Pour en savoir plus sur la persistance du contenu de la communauté et les déploiements recommandés, voir :

* [Community Content Storage](/help/communities/working-with-srp.md), qui présente les options de stockage SRP disponibles pour UGC.
* [Topologies](/help/communities/topologies.md)recommandées, qui traite des topologies en fonction du cas d’utilisation et du choix du SRP.
* [Mise à niveau vers les communautés](/help/communities/upgrade.md)AEM 6.5, qui fournit des informations utiles sur l’UGC lors du passage à AEM 6.5.

## Console Communautés {#communities-consoles}

Dans l’environnement de création, la console de navigation globale permet d’accéder à la console [](/help/communities/consoles.md)Communautés, qui contient :

* La console [Sites](/help/communities/sites-console.md)

   * création de site
   * modification du site
   * gestion du site
   * [Console Groupes](/help/communities/groups.md) de communautés

* [Console Modération](/help/communities/moderation.md)

   * interface utilisateur commune de modération en bloc pour les environnements de création et de publication
   * nouveaux critères de filtrage

* [Consoles de gestion des membres et des groupes](/help/communities/members.md)

   * permet de créer et de gérer des utilisateurs côté publication (membres) à partir de l’environnement d’auteur
   * permet d&#39;interdire les membres
   * permet de créer et de gérer des groupes d’utilisateurs côté publication (groupes de membres) à partir de l’environnement d’auteur.

* [Console Rapports](/help/communities/reports.md)

   * permet de générer des rapports sur les affectations, les publications et les vues

* [Console Ressources](/help/communities/resources.md)

   * permet de créer des ressources d’activation et des chemins d’apprentissage
   * donne accès aux rapports sur les ressources d’activation et les chemins d’apprentissage

La console d’outils globale donne accès aux outils de communautés suivants :

* [Console Modèles](/help/communities/tools.md#sitetemplatesconsole) de site

   * créer et gérer des modèles de site communautaire

* [Console Modèles](/help/communities/tools.md#grouptemplatesconsole) de groupe

   * créer et gérer des modèles de groupes de communautés

* [Console Fonctions](/help/communities/tools.md#communityfunctionsconsole) de la communauté

   * créer et gérer les fonctions de la communauté

* [Console de configuration](/help/communities/tools.md#storageconfiguratonconsole) du stockage

   * sélectionner et configurer la boutique [](/help/communities/working-with-srp.md) commune pour le site ;

* [Guide du composant](/help/communities/components-guide.md)

   * un exemple de site, Composants [de la](https://localhost:4502/editor.html/content/community-components/en.html)communauté, qui fournit un échantillon de tous les composants de la communauté avec leur configuration par défaut et la possibilité de les tester

## Modèles de site de communauté {#community-site-templates}

La création d&#39;un site communautaire est basée sur la sélection d&#39;un modèle de site communautaire afin de configurer rapidement un site communautaire indépendant de tout exemple de site.

Un modèle de site de la communauté, composé de fonctions de la communauté et de modèles de groupes de la communauté, fournit la structure d’un site de la communauté, y compris les identifiants de connexion, les profils utilisateur, la messagerie, le menu du site, la recherche, le thème et les fonctionnalités de marque.

Voir la console [Modèles de](/help/communities/sites.md)site.

## Fonctions de la communauté {#community-functions}

Les caractéristiques attendues d&#39;une expérience communautaire sont bien connues. Avec les communautés AEM, ces fonctionnalités sont disponibles sous forme de blocs de création, appelés fonctions de communauté.

Les fonctions de la communauté sont des pages AEM normales qui comprennent des composants reliés entre eux dans une fonctionnalité facilement intégrée dans un modèle de site de la communauté.

See the [Community Functions console](/help/communities/functions.md).

## Groupes de communautés et modèles de groupes {#community-groups-and-group-templates}

La fonctionnalité des groupes communautaires permet à une sous-communauté d’être créée dynamiquement dans un site communautaire par des utilisateurs autorisés et des membres de la communauté provenant des environnements d’auteur et de publication.

Dans l’environnement de l’auteur, des groupes communautaires (sous-communautés) peuvent être créés dans un site communautaire existant ou imbriqués dans un groupe existant, lorsque la structure du modèle contient la fonction [](/help/communities/functions.md#groups-function)Groupes.

La création d&#39;un groupe communautaire nécessite la sélection d&#39;un modèle de groupe communautaire qui fournit la conception des pages de groupe communautaire. Lorsqu’une fonction Groupes est ajoutée à une structure de modèle, elle est configurée pour spécifier un modèle de groupe ou pour fournir un choix de modèles au moment de la création d’un nouveau groupe de communauté.

Voir également:

* [Console](/help/communities/groups.md) Groupes de sites pour la création de sous-communautés dans l’environnement de création
* [Console](/help/communities/tools-groups.md) Modèles de groupe pour la création de la structure du site pour les groupes
* [Pour commencer avec les communautés](/help/communities/getting-started.md) AEM pour obtenir un didacticiel sur la création rapide d’un site communautaire incluant des groupes imbriqués

## Composants communautaires {#community-components}

Les composants [de](/help/communities/author-communities.md) la communauté à partir desquels un site communautaire est créé peuvent être utilisés pour ajouter des fonctionnalités de communautés à tout site AEM.

Le guide [des composants](/help/communities/components-guide.md) communautaires est disponible pour l’exploration interactive des composants.

## Types de communautés {#types-of-communities}

### Communauté d’engagement {#engagement-community}

Une communauté d’engagement est un site communautaire axé sur l’engagement des clients à informer, à solliciter des commentaires et à permettre aux clients d’interagir en tant que membres de la communauté.

Les caractéristiques d&#39;une communauté d&#39;engagement peuvent être les suivantes :

* Connexion
* messagerie
* forums
* Commentaires
* Révisions
* évaluations
* Votant
* blogs
* groupes ;
* calendriers
* traduction
* modération
* notifications
* notation et badges
* rapports d’analyse

Pour découvrir la facilité de création rapide d’une nouvelle communauté d’engagement, consultez [Prise en main des communautés](/help/communities/getting-started.md)AEM.

### Communauté d&#39;activation {#enablement-community}

Une communauté d’activation est un site communautaire qui comprend des fonctionnalités d’apprentissage en ligne.

Les caractéristiques d’une communauté d’activation peuvent être les suivantes :

* toutes les caractéristiques d&#39;une communauté [d&#39;engagement](#engagement-community)
* possibilité d’affecter du contenu et des ressources d’apprentissage aux membres et aux groupes de membres
* prend en charge le contenu SCORM, comme les questionnaires et les tests
* suivi des affectations terminées
* accès aux rapports et analyses
* la possibilité d’avoir une conversation sur une ressource d’apprentissage par le biais de forums, de messages, de commentaires et d’évaluations

Une communauté d&#39;activation peut être créée lorsque le module complémentaire [d&#39;activation est configuré](/help/communities/enablement.md), ce qui nécessite une licence supplémentaire pour une utilisation dans un environnement de production. Un site de la communauté d&#39;activation inclura la fonction [](#community-functions)assignations.

Pour découvrir la facilité de création d’une nouvelle communauté d’activation, consultez [Prise en main des communautés AEM pour l’activation](/help/communities/getting-started-enablement.md).

## Machine de démonstration AEM {#aem-demo-machine}

La machine [de démonstration](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine) AEM gère et exécute des démos pour les [sites](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Scenario%20Sites)AEM, les [ressources](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Scenario%20Assets)[, les communautés, les applications et lesForms, qui nécessitent souvent plus de configuration que de simplement lancer une instance QuickStart. ](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Scenario%20Communities)[](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Scenario%20Apps)[](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Scenario%20Forms) La machine de démonstration AEM installera une [infrastructure](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Infrastructure) supplémentaire telle que MongoDB, Solr, MySQL, FFmpeg et les serveurs de messagerie.

La machine de démonstration AEM comprend :

* une interface utilisateur [graphique](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/User%20Interface)
* Scripts Apache ANT avec [propriétés](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Properties) et [cibles configurables](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Command%20Line)

* packages à installer

La machine de démonstration AEM a été testée avec succès avec CQ 5.5, CQ 5.6.1, AEM 6.0, AEM 6.1, AEM 6.2, AEM 6.3 et AEM 6.4 sous Windows, MacOS et Linux.

La machine de démonstration AEM requiert une licence AEM valide.

>[!NOTE]
>
>Visionnez une présentation [](https://www.youtube.com/watch?v=zEE_zkR9fVQ&feature=youtu.be) vidéo sur la machine de démonstration AEM (13:26).

## Documentation des communautés AEM {#aem-communities-documentation}

* Visit [Deploying Communities](/help/communities/deploy-communities.md) to learn about recommended deployments.
* Visitez [Administration des sites](/help/communities/administer-landing.md) des communautés pour en savoir plus sur la création d’un site communautaire, l’ajout de groupes communautaires, la configuration de modèles de site communautaire, la modération du contenu communautaire, la gestion des membres, le balisage, les notifications, la notation et les badges.
* Visit [Developing Communities](/help/communities/communities.md) to learn about the social component framework (SCF) and customizing Communities components and features.
* Visitez [Création de composants](/help/communities/author-communities.md) de communautés pour apprendre à créer et à configurer des composants de communautés.

