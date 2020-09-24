---
title: Meilleures pratiques MSM
seo-title: Meilleures pratiques MSM
description: Découvrez les meilleures pratiques compilées par les équipes d’ingénierie et de recherche d’Adobe pour vous aider à maîtriser le Multi Site Manager (MSM) AEM.
seo-description: Découvrez les meilleures pratiques compilées par les équipes d’ingénierie et de recherche d’Adobe pour vous aider à maîtriser le Multi Site Manager (MSM) AEM.
uuid: cbb598bb-ec8f-4985-97af-7c87f5891c66
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: site-features, best-practices
content-type: reference
discoiquuid: 04344537-7485-40a9-ad14-804ba448f1e2
translation-type: tm+mt
source-git-commit: a929252a13f66da8ac3e52aea0655b12bdd1425f
workflow-type: tm+mt
source-wordcount: '1530'
ht-degree: 63%

---


# Meilleures pratiques MSM{#msm-best-practices}

## Général {#general}

MSM est une structure configurable pour automatiser le déploiement de contenu. Les mises en œuvre impliquent souvent des parties importantes d’un site web, ainsi que plusieurs organisations et zones géographiques. Il est donc vivement recommandé de planifier les mises en œuvre MSM avec autant d’attention que lorsque vous planifiez votre site web :

* Carefully **plan structure and content flows** before starting implementation.
* **Personnalisez autant que nécessaire, mais le moins possible.** Bien que MSM prenne en charge un haut degré de personnalisation (par exemple, les configurations de déploiement), la meilleure pratique pour les performances, la fiabilité et la mise à niveau de votre site Web consiste à minimiser la personnalisation.
* Establish a **governance** model early, and train users accordingly, to ensure success. A best practice from a governance point of view is to **minimize the authority that local content producers have** to allocate/connect content to other local users and their respective live copies. En effet, les héritages enchaînés et non gouvernés peuvent considérablement accroître la complexité d&#39;une structure de gestion multivariée et compromettre ses performances et sa fiabilité.

* Once a plan exists for your structure, content flows, automation and governance - **prototype and thoroughly test your system**, before starting live implementation.
* Keep in mind that **Adobe Consulting and leading System Integrators** have deep experience planning and implementing content automation with MSM, so they can help you both get started with your MSM project and throughout its entire implementation.

>[!NOTE]
>
>Des informations supplémentaires sur l’utilisation de MSM sont disponibles dans les articles de la base de connaissances :
>
>* [FAQ relative à MSM](https://helpx.adobe.com/fr/experience-manager/kb/index/msm_faq.html)
>* [Résolution des incidents liés à MSM](https://helpx.adobe.com/fr/experience-manager/kb/troubleshooting-aem-msm-issues.html)

>



>[!NOTE]
>
>Vous pouvez également utiliser le [composant Référence](/help/sites-authoring/default-components-foundation.md#reference) pour réutiliser une seule page ou un paragraphe. Gardez cependant à l’esprit que :
>
>* MSM est plus souple et permet un contrôle à granularité fine sur la nature du contenu synchronisé et le moment de synchronisation.
>* Il est désormais recommandé d’utiliser les [composants principaux](https://docs.adobe.com/content/help/fr-FR/experience-manager-core-components/using/introduction.html) plutôt que les composants de base.

>



## Sources de Live Copy et configurations de plan directeur {#live-copy-sources-and-blueprint-configurations}

N’oubliez pas qu’une Live Copy peut être créée avec des [pages ordinaires](/help/sites-administering/msm-livecopy.md#creating-a-live-copy-of-a-page) ou une [configuration de plan directeur](/help/sites-administering/msm-livecopy.md#creating-a-live-copy-of-a-site-from-a-blueprint-configuration). Les deux cas d’utilisation sont valides.

Les avantages de l’utilisation d’une configuration de plan directeur sont qu’elle :

* Allow the author to use the **Rollout** option on a blueprint - to (explicitly) push modifications to live copies that inherit from this blueprint.
* Allow the author to use **Create Site**; this allows the user to easily select languages and configure the structure of the live copy.
* définit une configuration de déploiement par défaut pour les Live Copies partageant une relation avec le plan directeur.

Dans le cas où aucune configuration de plan directeur n’est référencée, les déploiements peuvent uniquement être lancés à partir des Live Copies elles-mêmes, en extrayant essentiellement le contenu de la source.

Lors de la création d’un site avec une Live Copy, il est pratique de créer des configurations de plan directeur pour garantir la disponibilité du jeu complet de fonctions MSM.

## Composants et synchronisation de conteneur {#components-and-container-synchronization}

En général, la règle de déploiement dans MSM concernant la synchronisation des composants est la suivante :

* Les composants sont déployés en synchronisant toutes les ressources contenues dans le plan directeur.
* Les conteneurs synchronisent uniquement la ressource actuelle.

Cela signifie que les composants sont traités comme un agrégat et, dans un déploiement, le composant lui-même et tous ses enfants sont remplacés par ceux des plans directeurs. Cela signifie que si une ressource est ajoutée à un composant en local, elle sera perdue au profit du contenu du plan directeur lors du déploiement.

Pour prendre en charge l’imbrication des composants de façon à ce que les composants ajoutés localement soient conservés dans un déploiement, le composant doit être déclaré en tant que conteneur. Par exemple, le système de paragraphe (parsys) par défaut est déclaré en tant que conteneur afin qu’il puisse prendre en charge le contenu ajouté en local.

>[!NOTE]
>
>Ajoutez la propriété `cq:isContainer` au composant pour le désigner en tant que conteneur.

## Créer un site {#create-site}

Notez qu’AEM propose deux méthodes principales pour créer des Live Copies :

* When [creating a Live Copy](/help/sites-administering/msm-livecopy.md#creating-a-live-copy-of-a-page)

   Il peut s’agir de l’approche la plus générique, qui vous permet de créer des copies dynamiques à partir de n’importe quelle page. La structure de contenu d’une Live Copy correspond exactement à la source.

* Lors de la [création d&#39;un site](/help/sites-administering/msm-livecopy.md#creating-a-live-copy-of-a-site-from-a-blueprint-configuration)

   Il s&#39;agit d&#39;une approche plus spécialisée, principalement pour la création de sites Web à structure multilingue.

Voici quelques points à garder à l’esprit lors de la création d’un site :

* To create a new site, you need a [blueprint configuration](/help/sites-administering/msm-livecopy.md#managing-blueprint-configurations).
* Pour permettre la sélection des chemins de langue à créer dans un nouveau site, les racines de langue correspondantes doivent exister dans le plan directeur (source).
* Once a [new site has been created as a live copy](/help/sites-administering/msm-livecopy.md#creating-a-live-copy-of-a-site-from-a-blueprint-configuration) (using **Create**, then **Site**), the first two levels of this live copy are *shallow*. Les enfants de la page n’appartiennent pas à la relation activée, mais un déploiement descend toujours si une relation activée correspondant au déclencheur est détectée.

    Il permet d’éviter :

   * d’ajouter manuellement des langues dans le plan directeur (sous le premier niveau) ;
   * d’ajouter manuellement le contenu directement sous la racine de langue ;
   * de voir ce contenu transféré automatiquement vers la Live Copy au moment du déploiement.

## MSM et sites web multilingues {#msm-and-multilingual-websites}

MSM peut aider à la création de sites web multilingues de deux façons :

* Lors de la création de gabarits de langue

   * Bien que MSM lui-même **ne fournisse pas la traduction de contenu**, il peut être intégré à des connecteurs de traduction tiers qui proposent ce service. Veuillez noter que :

      * MSM vous permet d’annuler l’héritage au niveau des pages et/ou des composants. Cela évite de remplacer le contenu traduit (dans une Live Copy, avec le contenu pas encore traduit d’un plan directeur) lors du déploiement suivant.
      * Certains connecteurs de traduction tiers automatisent cette gestion des héritages MSM.

         Contactez votre prestataire de services de traduction pour plus d’informations.

      * Une autre méthode pour créer et traduire les gabarits de langue est d’utiliser des copies de langue conjointement à la structure d’intégration de traduction prête à l’emploi d’AEM.

* Lors du déploiement de contenu de gabarits de langue

   * Par exemple, du gabarit de langue française vers des sites spécifiques aux pays, par exemple, France/Français, Canada/Français, Suisse/Français.

Pour plus d’informations, voir [Traduction du contenu des sites multilingues](/help/sites-administering/translation.md) et [Meilleures pratiques de traduction](/help/sites-administering/tc-bp.md).

## Modifications de structure et déploiements {#structure-changes-and-rollouts}

Les modifications apportées à la structure du contenu dans un plan directeur/une arborescence source sont répercutées différemment dans une Live Copy. Cela dépend du type de modification :

* **La création** de nouvelles pages dans un plan directeur entraîne la création de pages correspondantes dans des copies dynamiques après le déploiement avec la configuration de déploiement standard.

* **La suppression** des pages d&#39;un plan directeur entraîne la suppression des pages correspondantes des copies dynamiques après le déploiement avec la configuration de déploiement standard.

* **Le déplacement** de pages dans un plan directeur **n&#39;entraîne pas** le déplacement des pages correspondantes en copies dynamiques après le déploiement avec la configuration de déploiement standard :

   * La raison de ce comportement est que le déplacement d’une page comprend implicitement une suppression de page. Cela peut provoquer un comportement inattendu lors de la publication, la suppression des pages sur l’instance de création désactivant automatiquement le contenu correspondant sur l’instance de publication. Cela peut également avoir des répercussions sur les éléments associés, comme les liens, les signets, etc.
   * L’héritage de contenu dans les pages de Live Copy respectives est mis à jour pour refléter le nouvel emplacement de leurs sources dans le plan directeur.
   * Pour réaliser pleinement le déplacement d’une page d’un plan directeur vers des copies en direct, tenez compte des bonnes pratiques suivantes :

>[!NOTE]
>
>This will work only with the [On Rollout trigger](https://helpx.adobe.com/experience-manager/6-3/sites/administering/using/msm-sync.html#rollout-triggers).

* Créez une configuration de déploiement personnalisée :

   * Cette nouvelle configuration doit inclure l’action suivante :

      `PageMoveAction`

      N’ajoutez pas d’autres actions à cette configuration.

* Placez la nouvelle configuration :

   * Pour déployer complètement le déplacement de la page, tout en supprimant les pages respectives à leur ancien emplacement dans la copie dynamique :

      * Placez la configuration que vous venez de créer avant la configuration de déploiement standard.

         La configuration de déploiement standard se charge de supprimer les pages de leur ancien emplacement.
   * Pour déployer le déplacement de la page tout en conservant les pages respectives à leur ancien emplacement dans les copies en direct (essentiellement en dupliquant le contenu) :

      * Placez la configuration que vous venez de créer après la configuration de déploiement standard.

         Ainsi, aucun contenu n’est supprimé dans la copie dynamique ou désactivé de la publication.


## Personnalisation des déploiements {#customizing-rollouts}

Les configurations de déploiement MSM sont fortement personnalisables. Vous devez savoir que l’automatisation des déploiements peut avoir des conséquences importantes. Il est recommandé de planifier avec une *grande* attention par exemple les opérations suivantes :

* automating rollouts; for example, with [onModify triggers](#onmodify),
* la personnalisation des [propriétés/types de nœuds](#node-types-properties) ;
* commençant les workflows suivants,
* et/ou activation de contenu dans le cadre de déploiements.

### onModify {#onmodify}

Lorsque vous utilisez le [déclencheur de déploiement](/help/sites-administering/msm-sync.md#rollout-triggers) `onModify`, vous devez prendre en compte les points suivants :

* Automating rollouts with `onModify` triggers may have a negative impact on authoring performance as they trigger rollouts after *every* page modification.

* Le résultat du déploiement peut différer du résultat attendu pour les raisons suivantes :

   * Vous ne pouvez pas spécifier l’ordre des événements de modification résultants.
   * L’architecture basée sur les événements ne peut pas garantir la séquence des événements transmise au gestionnaire de déploiements.

* L’utilisation d’une telle configuration de déploiement est susceptible d’entraîner des conflits de validation en cas de mises à jour simultanées de la même ressource.

Therefore, it is recommended that you *only* use `onModify` triggers if the benefits of automatic rollout initiation outweigh any potential performance issues.

### Types/propriétés de nœuds {#node-types-properties}

N’oubliez pas les points suivants :

* Outre la personnalisation des actions de déploiement, MSM vous permet également de personnaliser les propriétés de noeud en cours de déploiement. La [configuration OSGi MSM vous permet d’exclure des types de nœuds](/help/sites-administering/msm-sync.md#excluding-properties-and-node-types-from-synchronization) de la copie de la source vers la Live Copy.

## Informations supplémentaires {#further-information}

La présente section et les pages suivantes abordent les questions connexes :

* [Création et synchronisation de Live Copies](/help/sites-administering/msm-livecopy.md)
* [Console Aperçu de la Live Copy](/help/sites-administering/msm-livecopy-overview.md)
* [Configuration de la synchronisation des Live Copies](/help/sites-administering/msm-sync.md)
* [Conflits de déploiement dans MSM](/help/sites-administering/msm-rollout-conflicts.md)

