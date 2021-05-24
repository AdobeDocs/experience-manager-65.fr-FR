---
title: Bonnes pratiques MSM
seo-title: Bonnes pratiques MSM
description: Découvrez les meilleures pratiques compilées par les équipes d’ingénierie et de recherche d’Adobe pour vous aider à maîtriser le Multi Site Manager (MSM) AEM.
seo-description: Découvrez les meilleures pratiques compilées par les équipes d’ingénierie et de recherche d’Adobe pour vous aider à maîtriser le Multi Site Manager (MSM) AEM.
uuid: cbb598bb-ec8f-4985-97af-7c87f5891c66
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: site-features, best-practices
content-type: reference
discoiquuid: 04344537-7485-40a9-ad14-804ba448f1e2
feature: Multi Site Manager
exl-id: 3fedc1ba-64f5-4fbe-9ee5-9b96b75dda58
source-git-commit: cb4b0cb60b8709beea3da70495a15edc8c4831b8
workflow-type: tm+mt
source-wordcount: '1667'
ht-degree: 69%

---

# Bonnes pratiques MSM{#msm-best-practices}

## Général {#general}

MSM est une structure configurable pour automatiser le déploiement de contenu. Les mises en œuvre impliquent souvent des parties importantes d’un site web, ainsi que plusieurs organisations et zones géographiques. Il est donc vivement recommandé de planifier les mises en œuvre MSM avec autant d’attention que lorsque vous planifiez votre site web :

* **Planifiez la structure et les flux de contenu** avec soin avant de commencer la mise en œuvre.
* **Veillez à ce que le nombre de Live Copies reste minimal.** Le traitement des Live Copies est une tâche gourmande en ressources. Plus il existe de Live Copies dans votre système, plus les performances peuvent être affectées : depuis le traitement des index de Live Copy internes, sur les opérations de Live Copy telles que les déploiements, jusqu’aux opérations de l’interface utilisateur telles que l’affichage des relations de Live Copy dans le rail de références d’administration des sites . La bonne pratique consiste à créer des Live Copies de sites ou de branches d’un site, où les relations de Live Copy sont héritées des pages du site ou de la branche. Évitez de créer des Live Copies individuelles pour les pages d’un site ou d’une branche lorsque la structure entière peut être transformée en Live Copy.
* **Personnalisez autant que nécessaire, mais le moins possible.** Bien que MSM prenne en charge un haut degré de personnalisation (par exemple, des configurations de déploiement), la meilleure pratique pour les performances, la fiabilité et la mise à niveau de votre site web est généralement de minimiser la personnalisation.
* Établissez un modèle de **gouvernance** dès le début et formez les utilisateurs en conséquence, afin de garantir la réussite. Une bonne pratique du point de vue de la gouvernance consiste à **minimiser l’autorité des producteurs de contenu locaux** pour allouer/connecter du contenu à d’autres utilisateurs locaux et à leurs Live Copies respectives. Cela est dû au fait que les héritages par enchaînement non gouvernés peuvent considérablement augmenter la complexité d’une structure MSM et dégrader ses performances et sa stabilité.

* Une fois qu’un plan existe pour votre structure, vos flux de contenu, l’automatisation et la gouvernance : **prototypez et testez minutieusement votre système**, avant de commencer la mise en oeuvre en direct.
* Gardez à l’esprit que les **intégrateurs système de premier plan et les consultants Adobe** possèdent une expérience approfondie dans la planification et la mise en œuvre de l’automatisation de contenu avec MSM. Ils peuvent donc vous aider lors du lancement de votre projet MSM et tout au long de sa mise en œuvre.

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



## Configurations de plan directeur et de sources Live Copy {#live-copy-sources-and-blueprint-configurations}

N’oubliez pas qu’une Live Copy peut être créée avec des [pages ordinaires](/help/sites-administering/msm-livecopy.md#creating-a-live-copy-of-a-page) ou une [configuration de plan directeur](/help/sites-administering/msm-livecopy.md#creating-a-live-copy-of-a-site-from-a-blueprint-configuration). Les deux cas d’utilisation sont valides.

Les avantages de l’utilisation d’une configuration de plan directeur sont qu’elle :

* Autoriser l’auteur à utiliser l’option **Déploiement** sur un plan directeur pour (explicitement) pousser les modifications vers les Live Copies qui héritent de ce plan directeur.
* Autoriser l’auteur à utiliser **Créer un site** ; cela permet à l’utilisateur de sélectionner facilement des langues et de configurer la structure de la Live Copy.
* définit une configuration de déploiement par défaut pour les Live Copies partageant une relation avec le plan directeur.

Dans le cas où aucune configuration de plan directeur n’est référencée, les déploiements peuvent uniquement être lancés à partir des Live Copies elles-mêmes, en extrayant essentiellement le contenu de la source.

Lors de la création d’un site avec une Live Copy, il est pratique de créer des configurations de plan directeur pour garantir la disponibilité du jeu complet de fonctions MSM.

>[REMARQUE!]
>
> Notez que les groupes d’utilisateurs fermés dans l’onglet Autorisations ne peuvent pas être déployés sur des Live Copies à partir de plans directeurs. Veuillez en tenir compte lors de la configuration de Live Copy.

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

* Lors de la [création d’une Live Copy](/help/sites-administering/msm-livecopy.md#creating-a-live-copy-of-a-page)

   Cela peut être considéré comme l’approche plus générique, qui vous permet de créer des Live Copies à partir de n’importe quelle page. La structure de contenu d’une Live Copy correspond exactement à la source.

* Quand [créer un site](/help/sites-administering/msm-livecopy.md#creating-a-live-copy-of-a-site-from-a-blueprint-configuration)

   Il s’agit d’une approche plus spécialisée, principalement pour la création de sites web avec une structure multilingue.

Voici quelques points à garder à l’esprit lors de la création d’un site :

* Pour créer un site, vous avez besoin d’une [configuration de plan directeur](/help/sites-administering/msm-livecopy.md#managing-blueprint-configurations).
* Pour permettre la sélection des chemins de langue afin de créer un site, les racines de langue correspondantes doivent exister dans le plan directeur (source).
* Une fois qu’un [nouveau site a été créé en tant que Live Copy](/help/sites-administering/msm-livecopy.md#creating-a-live-copy-of-a-site-from-a-blueprint-configuration) (à l’aide de **Créer**, puis **Site**), les deux premiers niveaux de cette Live Copy sont *superficiel*. Les enfants de la page n’appartiennent pas à la relation activée, mais un déploiement descend toujours si une relation activée correspondant au déclencheur est détectée.

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

* **** La création de pages dans un plan directeur entraîne la création de pages correspondantes dans des Live Copies après déploiement avec la configuration de déploiement standard.

* **** La suppression de pages dans un plan directeur entraîne la suppression des pages correspondantes des Live Copies après déploiement avec la configuration de déploiement standard.

* **** Le déplacement de pages dans un plan directeur  **** n’entraîne pas le déplacement des pages correspondantes dans des Live Copies après déploiement avec la configuration de déploiement standard :

   * La raison de ce comportement est que le déplacement d’une page comprend implicitement une suppression de page. Cela peut provoquer un comportement inattendu lors de la publication, la suppression des pages sur l’instance de création désactivant automatiquement le contenu correspondant sur l’instance de publication. Cela peut également avoir des répercussions sur les éléments associés, comme les liens, les signets, etc.
   * L’héritage de contenu dans les pages de Live Copy respectives est mis à jour pour refléter le nouvel emplacement de leurs sources dans le plan directeur.
   * Pour réaliser pleinement un déplacement de page d’un plan directeur vers des Live Copies, tenez compte des bonnes pratiques suivantes :

>[!NOTE]
>
>Cela fonctionne uniquement avec le déclencheur [Au déploiement](https://helpx.adobe.com/experience-manager/6-3/sites/administering/using/msm-sync.html#rollout-triggers).

* Créez une configuration de déploiement personnalisée:

   * Cette nouvelle configuration doit inclure l’action:

      `PageMoveAction`

      N’ajoutez pas d’autres actions à cette configuration.

* Placez la nouvelle configuration:

   * Pour déployer entièrement le déplacement de page, tout en supprimant les pages respectives à leur ancien emplacement dans la Live Copy :

      * Placez la configuration que vous venez de créer avant la configuration de déploiement standard.

         La configuration de déploiement standard se charge de supprimer les pages de leur ancien emplacement.
   * Pour déployer le déplacement de la page tout en conservant les pages respectives à leur ancien emplacement dans les Live Copies (en dupliquant essentiellement le contenu) :

      * Placez la configuration que vous venez de créer après la configuration de déploiement standard.

         Cela permet de s’assurer qu’aucun contenu n’est supprimé dans la Live Copy ou désactivé de la publication.


## Personnalisation des déploiements {#customizing-rollouts}

Les configurations de déploiement MSM sont fortement personnalisables. Vous devez savoir que l’automatisation des déploiements peut avoir des conséquences importantes. Il est recommandé de planifier avec une *grande* attention par exemple les opérations suivantes :

* l’automatisation des déploiements ; par exemple, avec [onModify triggers](#onmodify),
* la personnalisation des [propriétés/types de nœuds](#node-types-properties) ;
* démarrer les workflows suivants,
* et/ou activation de contenu dans le cadre de déploiements.

### onModify {#onmodify}

Lorsque vous utilisez le [déclencheur de déploiement](/help/sites-administering/msm-sync.md#rollout-triggers) `onModify`, vous devez prendre en compte les points suivants :

* L’automatisation des déploiements avec des déclencheurs `onModify` peut avoir un impact négatif sur les performances de création, car ils déclenchent des déploiements après chaque modification de page.**

* Le résultat du déploiement peut différer du résultat attendu pour les raisons suivantes :

   * Vous ne pouvez pas spécifier l’ordre des événements de modification résultants.
   * L’architecture basée sur les événements ne peut pas garantir la séquence des événements transmise au gestionnaire de déploiements.

* L’utilisation d’une telle configuration de déploiement est susceptible d’entraîner des conflits de validation en cas de mises à jour simultanées de la même ressource.

Par conséquent, il est recommandé de *n’utiliser* que les déclencheurs `onModify` si les avantages du lancement du déploiement automatique l’emportent sur les problèmes de performances potentiels.

### Types/propriétés de nœuds {#node-types-properties}

N’oubliez pas les points suivants :

* En plus de personnaliser les actions de déploiement, MSM vous permet de personnaliser les propriétés des nœuds qui sont déployés. La [configuration OSGi MSM vous permet d’exclure des types de nœuds](/help/sites-administering/msm-sync.md#excluding-properties-and-node-types-from-synchronization) de la copie de la source vers la Live Copy.

## Informations supplémentaires {#further-information}

La présente section et les pages suivantes abordent les questions connexes :

* [Création et synchronisation de Live Copies](/help/sites-administering/msm-livecopy.md)
* [Console Aperçu de Live Copy](/help/sites-administering/msm-livecopy-overview.md)
* [Configuration de la synchronisation des Live Copies](/help/sites-administering/msm-sync.md)
* [Conflits de déploiement de MSM](/help/sites-administering/msm-rollout-conflicts.md)
