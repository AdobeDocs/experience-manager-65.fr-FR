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

* Soigneusement **planifier la structure et les flux de contenu** avant de commencer la mise en oeuvre.
* **Personnalisez autant que nécessaire, mais le moins possible.** Bien que MSM prenne en charge un haut degré de personnalisation (par exemple, les configurations de déploiement), la meilleure pratique pour les performances, la fiabilité et la mise à niveau de votre site Web consiste à minimiser la personnalisation.
* Établir rapidement un modèle de **gouvernance** et former les utilisateurs en conséquence afin d&#39;assurer la réussite. Une bonne pratique d&#39;un point de vue de gouvernance consiste à **réduire au minimum l&#39;autorité dont disposent les producteurs de contenu locaux** pour allouer/connecter du contenu à d&#39;autres utilisateurs locaux et leurs copies en direct respectives. En effet, les héritages enchaînés et non gouvernés peuvent considérablement accroître la complexité d&#39;une structure de gestion multivariée et compromettre ses performances et sa fiabilité.

* Une fois qu&#39;un plan existe pour votre structure, vos flux de contenu, l&#39;automatisation et la gouvernance : **prototype et testez minutieusement votre système**, avant de commencer la mise en oeuvre.
* Gardez à l&#39;esprit que **Adobe Consulting et les principaux intégrateurs système** ont une expérience approfondie de la planification et de l&#39;implémentation de l&#39;automatisation du contenu avec MSM, afin qu&#39;ils puissent vous aider à la fois à démarrer votre projet MSM et tout au long de sa mise en oeuvre.

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

* Permettre à l&#39;auteur d&#39;utiliser l&#39;option **Déploiement** sur un plan directeur pour (explicitement) pousser les modifications à des copies dynamiques qui héritent de ce plan.
* Autoriser l’auteur à utiliser **Créer un site**; cela permet à l’utilisateur de sélectionner facilement les langues et de configurer la structure de la copie dynamique.
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

* Lorsque [créer une Live Copy](/help/sites-administering/msm-livecopy.md#creating-a-live-copy-of-a-page)

   Il peut s’agir de l’approche la plus générique, qui vous permet de créer des copies dynamiques à partir de n’importe quelle page. La structure de contenu d’une Live Copy correspond exactement à la source.

* Lorsque [créer un site](/help/sites-administering/msm-livecopy.md#creating-a-live-copy-of-a-site-from-a-blueprint-configuration)

   Il s&#39;agit d&#39;une approche plus spécialisée, principalement pour la création de sites Web à structure multilingue.

Voici quelques points à garder à l’esprit lors de la création d’un site :

* Pour créer un nouveau site, vous devez disposer d&#39;une configuration de plan directeur [](/help/sites-administering/msm-livecopy.md#managing-blueprint-configurations).
* Pour permettre la sélection des chemins de langue à créer dans un nouveau site, les racines de langue correspondantes doivent exister dans le plan directeur (source).
* Une fois qu&#39;un [nouveau site a été créé en tant que copie dynamique](/help/sites-administering/msm-livecopy.md#creating-a-live-copy-of-a-site-from-a-blueprint-configuration) (en utilisant **Créer**, puis **Site**), les deux premiers niveaux de cette copie dynamique sont *peu profonds*. Les enfants de la page n’appartiennent pas à la relation activée, mais un déploiement descend toujours si une relation activée correspondant au déclencheur est détectée.

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

* **La** création de pages dans un plan directeur entraîne la création de pages correspondantes dans des copies dynamiques après le déploiement avec la configuration de déploiement standard.

* **La** suppression de pages dans un plan directeur entraîne la suppression des pages correspondantes des copies dynamiques après le déploiement avec la configuration de déploiement standard.

* **Le** déplacement de pages dans un plan directeur  **** n&#39;entraîne pas le déplacement de pages correspondantes dans des copies dynamiques après le déploiement avec la configuration de déploiement standard :

   * La raison de ce comportement est que le déplacement d’une page comprend implicitement une suppression de page. Cela peut provoquer un comportement inattendu lors de la publication, la suppression des pages sur l’instance de création désactivant automatiquement le contenu correspondant sur l’instance de publication. Cela peut également avoir des répercussions sur les éléments associés, comme les liens, les signets, etc.
   * L’héritage de contenu dans les pages de Live Copy respectives est mis à jour pour refléter le nouvel emplacement de leurs sources dans le plan directeur.
   * Pour réaliser pleinement le déplacement d’une page d’un plan directeur vers des copies en direct, tenez compte des bonnes pratiques suivantes :

>[!NOTE]
>
>Cela fonctionne uniquement avec le déclencheur [Au déploiement](https://helpx.adobe.com/experience-manager/6-3/sites/administering/using/msm-sync.html#rollout-triggers).

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

* automatisation des déploiements ; par exemple, avec [onModify triggers](#onmodify),
* la personnalisation des [propriétés/types de nœuds](#node-types-properties) ;
* commençant les workflows suivants,
* et/ou activation de contenu dans le cadre de déploiements.

### onModify {#onmodify}

Lorsque vous utilisez le [déclencheur de déploiement](/help/sites-administering/msm-sync.md#rollout-triggers) `onModify`, vous devez prendre en compte les points suivants :

* L’automatisation des déploiements avec des déclencheurs `onModify` peut avoir un impact négatif sur les performances de création, car elles déclenchent des déploiements après *chaque modification de page*.

* Le résultat du déploiement peut différer du résultat attendu pour les raisons suivantes :

   * Vous ne pouvez pas spécifier l’ordre des événements de modification résultants.
   * L’architecture basée sur les événements ne peut pas garantir la séquence des événements transmise au gestionnaire de déploiements.

* L’utilisation d’une telle configuration de déploiement est susceptible d’entraîner des conflits de validation en cas de mises à jour simultanées de la même ressource.

Par conséquent, il est recommandé de *n&#39;utiliser* que les déclencheurs `onModify` si les avantages du lancement automatique du déploiement l&#39;emportent sur les éventuels problèmes de performances.

### Types/propriétés de nœuds {#node-types-properties}

N’oubliez pas les points suivants :

* Outre la personnalisation des actions de déploiement, MSM vous permet également de personnaliser les propriétés de noeud en cours de déploiement. La [configuration OSGi MSM vous permet d’exclure des types de nœuds](/help/sites-administering/msm-sync.md#excluding-properties-and-node-types-from-synchronization) de la copie de la source vers la Live Copy.

## Informations supplémentaires {#further-information}

La présente section et les pages suivantes abordent les questions connexes :

* [Création et synchronisation de Live Copies](/help/sites-administering/msm-livecopy.md)
* [Console Aperçu de la Live Copy](/help/sites-administering/msm-livecopy-overview.md)
* [Configuration de la synchronisation des Live Copies](/help/sites-administering/msm-sync.md)
* [Conflits de déploiement dans MSM](/help/sites-administering/msm-rollout-conflicts.md)

