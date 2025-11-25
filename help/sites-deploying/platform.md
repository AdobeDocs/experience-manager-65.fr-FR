---
title: Présentation de la plateforme AEM
description: Découvrez la plateforme AEM et ses composants les plus importants, notamment l’installation et le déploiement d’Adobe Experience Manager 6.5 et son architecture, y compris le déploiement cloud d’Adobe Managed Services.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
legacypath: /content/docs/en/aem/6-0/deploy/upgrade/introduction-to-oak
exl-id: 8ee5f4ff-648d-45ea-a51e-894cd4385e62
solution: Experience Manager, Experience Manager Sites
feature: Deploying
role: Developer
source-git-commit: 07289e891399a78568dcac957bc089cc08c7898c
workflow-type: tm+mt
source-wordcount: '776'
ht-degree: 100%

---


# Présentation de la plateforme AEM{#introduction-to-the-aem-platform}

La plateforme AEM dans AEM 6 est basée sur Apache Jackrabbit Oak.

Apache Jackrabbit Oak vise à implémenter un référentiel de contenu hiérarchique évolutif et performant pour l’utiliser comme fondation des sites web modernes de classe mondiale et d’autres applications de contenu exigeantes.

Il succède à Jackrabbit 2 et il est utilisé par AEM 6 comme structure par défaut pour son référentiel de contenu, CRX.

## Principes et objectifs de conception {#design-principles-and-goals}

Oak met en oeuvre les spécifications [JSR-283](https://jcp.org/en/jsr/detail?id=283) (JCR 2.0). Ses principaux objectifs de conception sont les suivants :

* Meilleure prise en charge des référentiels volumineux
* Plusieurs nœuds de cluster répartis pour une haute disponibilité
* Meilleures performances
* Prise en charge de nombreux nœuds enfants et de niveaux de contrôle d’accès

## Concept de l’architecture {#architecture-concept}

![chlimage_1-84](assets/chlimage_1-84.png)

### Stockage {#storage}

Le but de la couche de stockage est de :

* Mettre en œuvre un modèle d’arborescence
* Rendre possible l’alimentation du stockage
* Fournir un mécanisme de mise en cluster

### Oak Core {#oak-core}

Oak Core ajoute plusieurs couches à la couche de stockage :

* Contrôles de niveau d’accès
* Recherche et indexation
* Observation

### Oak JCR {#oak-jcr}

L’objectif principal de Oak JCR est de transformer la sémantique JCR en opérations arborescentes. Il est aussi chargé des éléments suivants :

* Mise en œuvre de l’API JCR
* Contenir des hooks de validation qui mettent en œuvre des contraintes JCR

En outre, les implémentations non Java sont désormais possibles et font partie du concept Oak JCR.

## Présentation du stockage {#storage-overview}

La couche de stockage Oak fournit une couche d’abstraction pour le stockage réel du contenu.

Actuellement, il existe deux implémentations du stockage disponibles dans AEM 6 : le **stockage tar** et le **stockage MongoDB**.

### Stockage Tar {#tar-storage}

Le stockage Tar utilise des fichiers TAR. Il stocke le contenu sous la forme de différents types d’enregistrements dans des segments plus volumineux. Les journaux sont utilisés pour effectuer le suivi de l’état le plus récent du référentiel.

Il repose sur plusieurs principes de conception clés :

* **Segments non modifiables**

Le contenu est stocké dans des segments d’une taille maximale de 256 Ko. Ils sont inaltérables, ce qui permet de mettre en cache les segments utilisés fréquemment et de réduire les erreurs système susceptibles de compromettre le référentiel.

Chaque segment est identifié par un identifiant unique (UUID) et contient un sous-ensemble continu de l’arborescence de contenu. En outre, les segments peuvent référencer d’autres contenus. Chaque segment conserve une liste des UUID des autres segments référencés.

* **Localité**

Les enregistrements associés tels qu’un nœud et ses enfants immédiats sont stockés dans le même segment. Cela permet de rechercher rapidement le référentiel et d’éviter la plupart des pertes de cache pour les clients et clientes standard qui accèdent à plusieurs nœuds associés par session.

* **Compacité**

La mise en forme des enregistrements est optimisée pour la taille afin de réduire les coûts d’E/S et d’intégrer le plus de contenu possible dans les caches.

### Stockage Mongo {#mongo-storage}

Le stockage MongoDB utilise MongoDB pour le partage et la mise en grappe. L’arborescence du référentiel est conservée dans une base de données MongoDB où chaque nœud est un document distinct.

Il a plusieurs particularités :

* Révisions

Pour chaque mise à jour (validation) du contenu, une nouvelle révision est créée. Une révision est essentiellement une chaîne composée de trois éléments :

1. Une date et heure dérivées de l’heure du système de la machine sur laquelle elles ont été générées.
1. Un compteur pour distinguer les révisions créées avec la même date et heure.
1. L’identifiant du nœud du cluster dans lequel la révision a été créée.

* Branches

Les branches sont prises en charge, ce qui permet aux clients d’organiser plusieurs modifications et de les rendre visibles avec un seul appel de fusion.

* Documents précédents

Le stockage MongoDB ajoute des données à un document à chaque modification. Cependant, il supprime uniquement les données si un nettoyage est explicitement déclenché. Les anciennes données sont déplacées lorsqu’un certain seuil est atteint. Les documents précédents ne contiennent que des données non modifiables, ce qui signifie qu’ils ne contiennent que des révisions validées et fusionnées.

* Métadonnées du nœud de cluster

Les données relatives aux nœuds de cluster actifs et inactifs sont conservées dans la base de données afin de faciliter les opérations de cluster.

Une configuration en cluster AEM typique avec un stockage MongoDB :

![chlimage_1-85](assets/chlimage_1-85.png)

## Qu’est-ce qui diffère de Jackrabbit 2 ? {#what-is-different-from-jackrabbit}

Oak étant rétrocompatible avec la norme JCR 1.0, il n’y a pratiquement aucune modification au niveau de l’utilisation. Cependant, il existe des différences notables dont vous devez tenir compte lors de la configuration d’une installation d’AEM basée sur Oak :

* Oak ne crée pas automatiquement d’index. Par conséquent, les index personnalisés doivent être créés si nécessaire.
* Contrairement à Jackrabbit 2 où les sessions reflètent toujours le dernier état du référentiel, avec Oak, une session reflète une vue stable du référentiel à partir du moment où la session a été acquise. Cette situation est due au modèle MVCC sur lequel Oak est basé.
* Les frères de même nom (SNS) ne sont pas pris en charge dans Oak.

## Autre documentation liée aux plateformes {#other-platform-related-documentation}

Pour plus d’informations sur la plateforme AEM, consultez également les articles ci-dessous :

* [Configuration des entrepôts de nœuds et des magasins de données dans AEM 6](/help/sites-deploying/data-store-config.md)
* [Requêtes et indexation Oak](/help/sites-deploying/queries-and-indexing.md)
* [Éléments de stockage dans AEM 6](/help/sites-deploying/storage-elements-in-aem-6.md)
* [AEM avec MongoDB](/help/sites-deploying/aem-with-mongodb.md)
