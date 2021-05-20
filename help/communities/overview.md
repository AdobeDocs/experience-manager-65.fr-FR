---
title: Présentation d’AEM Communities
seo-title: Présentation d’AEM Communities
description: Présentation des fonctionnalités et de la configuration d’AEM Communities
seo-description: Présentation des fonctionnalités et de la configuration d’AEM Communities
uuid: 14405847-36ae-4958-bdc6-d799ecd05f06
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 44374006-f711-4af8-a1fe-f89164f79581
docset: aem65
exl-id: d6243dff-a067-455c-a326-5f451f225efd
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1446'
ht-degree: 5%

---

# Présentation d’AEM Communities {#aem-communities-overview}

Adobe Experience Manager (AEM) Communities permet de créer rapidement un site de communauté local doté de performances et d’une gestion de sites améliorées, et qui encourage les visiteurs à devenir membres de la communauté.

<!--
Contact your account representative for information regarding licensing of AEM Communities as well as additional licensing for enablement features and Adobe Analytics.
-->

## Fonctions de communauté {#communities-features}

AEM Communities permet le développement d’une relation avec les visiteurs du site qui :

* **** Informations au moyen de blogs, de questions et réponses et de calendriers d’événements,
* Bien que **obtienne des informations** par le biais de forums, de commentaires et d’autres contenus de la communauté, souvent appelés contenu généré par l’utilisateur.
* Il permet la **modération** par les membres de confiance dans l’environnement de publication,
* **Connexion** à Social avec Twitter et Facebook,
* **Traduction en ligne** de contenu communautaire,
* **Création de groupes communautaires** à partir du site communautaire publié,
* **** Scoringto des badges de récompense,
* **Partage de fichiers**,
* **** Notifications et diffusions  **d&#39;activités**,
* Permet **le balisage** (@mention) aux autres membres enregistrés dans le contenu généré par l’utilisateur, pour attirer leur attention.
* Prend en charge la **navigation au clavier** sur les composants d’activation (par exemple, Lecture de catalogue et de cours, Affectations, Bibliothèque de fichiers).

Les fonctionnalités de communauté peuvent être démontrées à l’aide de [AEM Demo Machine](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki) disponible publiquement sur GitHub.com ou avec la nouvelle implémentation de référence We.Retail.

## Sites communautaires {#community-sites}

Un site communautaire est un site AEM créé à l’aide d’un assistant simple qui génère un site web avec de nombreuses fonctionnalités courantes pré-câblées dans le site.

[Assistant de création de site](/help/communities/sites-console.md) :

* Assemble les fonctionnalités du site, en fonction du [modèle de site communautaire](/help/communities/sites.md) sélectionné, à savoir :

   * créée à partir des [fonctions de la communauté](#community-functions)
   * fonction facultative [groupes de communautés](#communitygroups)

* Utilise les paramètres à configurer :

   * modération
   * Connexion
   * traduction

* Fournit les fonctionnalités essentielles :

   * Responsive design : utilise [Thèmes du Bootstrap Twitter](https://getbootstrap.com)

   * Connexion : auto-inscription, [connexion sociale](/help/communities/social-login.md), profils utilisateur

      * Notifications :
les membres voient les événements qui les intéressent et le contenu généré par l’utilisateur où ils se trouvent [@mentioned](/help/communities/overview.md#mentionssupport).

      * Messagerie : les membres peuvent envoyer ou recevoir des messages sur le site de la communauté.
      * Rechercher : possibilité de rechercher dans le site de la communauté.
      * Changement de langue : possibilité de sélectionner une langue pour un [site multilingue](/help/sites-administering/translation.md).

      * Administration : accès pour les membres autorisés afin de modérer et de gérer les utilisateurs sur le site de la communauté.

* Élimine de nombreuses étapes de création au niveau de la page :

   * Marques : téléchargement facultatif d’une image de bannière à afficher sur toutes les pages du site de la communauté
   * Menu de navigation : des liens de navigation sont fournis pour les fonctionnalités incluses dans le modèle de site de la communauté.

Pour découvrir la facilité de création rapide d’un site communautaire, consultez la section [Prise en main d’AEM Communities](/help/communities/getting-started.md).

## Persistance du contenu de la communauté {#community-content-persistence}

Pour améliorer les performances et la synchronisation du contenu de la communauté, AEM Communities nécessite un magasin commun spécifique au contenu généré par l’utilisateur (UGC) partagé entre toutes les instances d’AEM (auteur et publication).

Le contenu de la communauté est facilement accessible par le biais du fournisseur de ressources de stockage (SRP), qui fournit une couche pour séparer l’accès de la topologie sous-jacente et prend en charge un magasin commun pour le contenu généré par l’utilisateur.

Pour en savoir plus sur la persistance du contenu de la communauté et les déploiements recommandés, voir :

* [Stockage de contenu de la communauté](/help/communities/working-with-srp.md), qui présente les options de stockage SRP disponibles pour le contenu généré par l’utilisateur.
* [Topologies recommandées](/help/communities/topologies.md), qui traite des topologies en fonction du cas d’utilisation et du choix de la SRP.
* [Mise à niveau vers AEM 6.5 Communities](/help/communities/upgrade.md), qui fournit des informations utiles sur le contenu généré par l’utilisateur lors du passage à AEM 6.5.

## Consoles Communities {#communities-consoles}

Dans l’environnement de création, la console de navigation globale permet d’accéder à la [console Communautés](/help/communities/consoles.md), qui contient :

* La console [Sites](/help/communities/sites-console.md)

   * Création de site
   * Modification du site
   * Gestion de site
   * [console ](/help/communities/groups.md) Groupes communautaires

* [Console Modération](/help/communities/moderation.md)

   * Interface utilisateur de modération en bloc courante pour les environnements de création et de publication.
   * Nouveaux critères de filtrage.

* [Consoles de gestion des membres et ](/help/communities/members.md) des groupes

   * Permet de créer et de gérer des utilisateurs (membres) côté publication à partir de l’environnement de création.
   * Permet d’interdire les membres.
   * Permet de créer et de gérer des groupes d’utilisateurs côté publication (groupes de membres) à partir de l’environnement de création.

* [](/help/communities/reports.md) Reportsconsole

   * Permet de générer des rapports sur les affectations, les publications et les vues.

* [](/help/communities/resources.md) ResourceConsole

   * Permet de créer des ressources d’activation et des parcours d’apprentissage.
   * Permet d’accéder aux rapports sur les ressources d’activation et les parcours de formation.

La console d’outils globale permet d’accéder aux outils Communities suivants :

* [Console ](/help/communities/tools.md#sitetemplatesconsole) Modèles du site

   * Créez et gérez des modèles de site de communauté.

* [Console ](/help/communities/tools.md#grouptemplatesconsole) Modèles de groupe

   * Créez et gérez des modèles de groupe de communautés.

* [console ](/help/communities/tools.md#communityfunctionsconsole) Fonctions de communauté

   * Créez et gérez des fonctions de communauté.

* [Storage ](/help/communities/tools.md#storageconfiguratonconsole) Configuration Console

   * Sélectionnez et configurez le [magasin commun](/help/communities/working-with-srp.md) pour le site.

* [Guide du composant](/help/communities/components-guide.md)

   * Un exemple de site, [Composants de la communauté](https://localhost:4502/editor.html/content/community-components/en.html), qui fournit un exemple de tous les composants de communauté avec leur configuration par défaut et la possibilité de les tester.

## Modèles de site de communauté {#community-site-templates}

La création d’un site de communauté est basée sur la sélection d’un modèle de site de communauté afin de configurer rapidement un site de communauté indépendant de tout exemple de site.

Un modèle de site de communauté, composé de fonctions de communauté et de modèles de groupe, fournit la structure d’un site de communauté, y compris les identifiants de connexion, les profils utilisateur, la messagerie, le menu du site, la recherche, le thème et les fonctionnalités de marque.

Voir la [console Modèles de site](/help/communities/sites.md).

## Fonctions de la communauté {#community-functions}

Les caractéristiques attendues d’une expérience communautaire sont bien connues. Avec AEM Communities, ces fonctionnalités sont disponibles sous la forme de blocs de création, appelés fonctions de communauté.

Les fonctions de communauté sont des pages d’AEM normales qui comprennent des composants connectés dans une fonctionnalité facilement intégrée à un modèle de site de communauté.

Voir la [console Fonctions de communauté](/help/communities/functions.md).

## Groupes communautaires et modèles de groupe {#community-groups-and-group-templates}

La fonctionnalité de groupes de communautés permet à une sous-communauté d’être créée dynamiquement dans un site de communauté par des utilisateurs autorisés et des membres de la communauté à partir des environnements de création et de publication.

Dans l’environnement de création, les groupes de communautés (sous-communautés) peuvent être créés dans un site de communauté existant ou imbriqués dans un groupe existant, lorsque la structure du modèle contient la [fonction Groupes](/help/communities/functions.md#groups-function).

La création d’un groupe de communautés nécessite la sélection d’un modèle de groupe de communautés qui fournit la conception des pages du groupe de communautés. Lorsqu’une fonction Groupes est ajoutée à une structure de modèle, elle est configurée pour spécifier un modèle de groupe ou pour offrir un choix de modèles au moment de la création d’un groupe de communautés.

Voir également :

* [Console Groupes de sites ](/help/communities/groups.md) pour la création de sous-communautés dans l’environnement de création.
* [Console Modèles de groupe ](/help/communities/tools-groups.md) permettant de créer une structure de site pour les groupes.
* [Prise en main d’AEM ](/help/communities/getting-started.md) communautés pour obtenir un tutoriel sur la création rapide d’un site communautaire comprenant des groupes imbriqués.

## Composants de la communauté {#community-components}

Les [composants de communauté](/help/communities/author-communities.md) à partir desquels un site de communauté est créé peuvent être utilisés pour ajouter des fonctionnalités de communauté à n’importe quel site AEM.

Le [guide des composants de communauté](/help/communities/components-guide.md) est disponible pour l’exploration interactive des composants.

## Types de communautés {#types-of-communities}

### Communauté d’engagement {#engagement-community}

Une communauté d’engagement est un site communautaire axé sur l’interaction entre les clients et leur permettant d’informer, de solliciter des commentaires et d’interagir en tant que membres de la communauté.

Les caractéristiques d’une communauté d’engagement peuvent être les suivantes :

* La connexion
* Message
* Forums
* Commentaires
* Révisions
* Evaluations
* Vote
* Blogs
* Groupes
* Calendriers
* Traduction
* Modération
* Notifications
* Notation et badges
* Rapports Analytics

Pour découvrir la facilité de création rapide d’une nouvelle communauté d’engagement, consultez la section [Prise en main d’AEM Communities](/help/communities/getting-started.md).

### Communauté d’activation {#enablement-community}

Une communauté d’activation est un site communautaire qui comprend des fonctionnalités d’apprentissage en ligne.

Les fonctionnalités d’une communauté d’activation peuvent être les suivantes :

* Toutes les fonctionnalités d’une [communauté d’engagement](#engagement-community).
* la capacité d’attribuer du contenu et de l’apprentissage. aux membres et aux groupes de membres.
* Prend en charge le contenu SCORM, comme les questionnaires et les tests.
* Suivi de la fin des affectations.
* Accès aux rapports et analyses.
* La possibilité d’avoir une conversation sur une ressource d’apprentissage par le biais de forums, de messages, de commentaires et d’évaluations.

Une communauté d’activation peut être créée lorsque le module complémentaire [Activation est configuré](/help/communities/enablement.md), ce qui nécessite des licences supplémentaires pour une utilisation dans un environnement de production. Un site de la communauté d’activation comprend la fonction [Affectations](#community-functions).

Pour découvrir la facilité de création d’une communauté d’activation, consultez la section [Prise en main d’AEM Communities pour l’activation](/help/communities/getting-started-enablement.md).

## AEM Demo Machine {#aem-demo-machine}

La [AEM Demo Machine](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine) gère et exécute des démonstrations pour AEM [Sites](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Scenario%20Sites), [Ressources](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Scenario%20Assets), [Communautés](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Scenario%20Communities), [Applications](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Scenario%20Apps) et [Forms](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Scenario%20Forms), qui nécessitent souvent plus qu’un simple lancement Instance QuickStart. AEM Demo Machine va configurer une infrastructure [supplémentaire](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Infrastructure) comme les serveurs MongoDB, Solr, MySQL, FFmpeg et de messagerie électronique.

La machine de démonstration AEM comprend :

* [Interface utilisateur graphique](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/User%20Interface).
* Scripts Apache ANT avec des [propriétés](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Properties) et [cibles](https://github.com/Adobe-Marketing-Cloud/aem-demo-machine/wiki/Command%20Line) configurables.

* Packages à installer.

AEM Demo Machine a été testé avec succès avec CQ 5.5, CQ 5.6.1, AEM 6.0, AEM 6.1, 6.2, 6.3 et 6.4 sous Windows, MacOS et Linux.

AEM Demo Machine nécessite une licence AEM valide.

>[!NOTE]
>
>Affichez une [introduction vidéo](https://www.youtube.com/watch?v=zEE_zkR9fVQ&amp;feature=youtu.be) à la machine de démonstration AEM (13:26).

## Documentation AEM Communities {#aem-communities-documentation}

* Visitez [Déploiement de communautés](deploy-communities.md) pour en savoir plus sur les déploiements recommandés.
* Consultez [Administration des sites communautaires](administer-landing.md) pour en savoir plus sur la création d’un site communautaire, l’ajout de groupes de communautés, la configuration de modèles de site communautaire, la modération de contenu communautaire, la gestion des membres, le balisage, les notifications, la notation et les badges.
* Visitez [Développement de communautés](communities.md) pour en savoir plus sur la structure de composants sociaux (SCF) et la personnalisation des composants et fonctionnalités de communautés.
* Consultez la section [Création de composants de communautés](author-communities.md) pour savoir comment créer et configurer des composants de communautés.
