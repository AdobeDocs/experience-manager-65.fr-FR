---
title: Topologies recommandées pour Communities
description: Approche de la gestion du contenu généré par l’utilisateur (UGC)
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
content-type: reference
topic-tags: deploying
exl-id: b6658330-d862-44e3-aac0-824fb91cd087
solution: Experience Manager
feature: Communities
role: Admin
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '552'
ht-degree: 6%
---
# Topologies recommandées pour Communities {#recommended-topologies-for-communities}

Depuis AEM Communities 6.1, une approche unique a été adoptée pour gérer le contenu généré par l’utilisateur (UGC) envoyé par les visiteurs du site (membres) à partir de l’environnement de publication.

Cette approche est fondamentalement différente de la façon dont la plateforme AEM gère le contenu du site qui est généralement géré à partir de l’environnement de création.

La plateforme AEM utilise un magasin de nœuds qui réplique le contenu du site de l’instance de création vers l’instance de publication, tandis qu’AEM Communities utilise un magasin unique et commun pour le contenu créé par l’utilisateur qui n’est jamais répliqué.

Pour le magasin UGC commun, il est nécessaire de choisir un [fournisseur de ressources de stockage (SRP)](working-with-srp.md). Les choix recommandés sont les suivants :

* [DSRP - Fournisseur de ressources de stockage de base de données relationnelle](dsrp.md)
* [MSRP - Fournisseur de ressources de stockage MongoDB](msrp.md)
* [ASRP - Fournisseur de ressources de stockage Adobe](asrp.md)

Une autre option SRP, [JSRP - Fournisseur de ressources de stockage JCR](jsrp.md), ne prend pas en charge un magasin UGC commun pour les environnements de création et de publication auxquels accéder.

La nécessité d’un magasin commun se traduit par les topologies recommandées suivantes.

>[!NOTE]
>
>Pour AEM Communities, [le contenu créé par l’utilisateur n’est jamais répliqué](working-with-srp.md#ugc-never-replicated).
>
>Lorsque le déploiement n’inclut pas de [magasin commun](working-with-srp.md), le contenu créé par l’utilisateur n’est visible que sur l’instance de publication ou d’auteur AEM sur laquelle il a été saisi.
>

>[!NOTE]
>
>Pour plus d’informations sur la plateforme AEM, voir [Déploiements recommandés](../../help/sites-deploying/recommended-deploys.md) et [Présentation de la plateforme AEM](../../help/sites-deploying/data-store-config.md).

## Pour la production {#for-production}

La création d’un magasin commun pour le contenu créé par l’utilisateur est essentielle. Le déploiement sous-jacent dépend donc de sa capacité à prendre en charge un magasin commun.

Deux exemples :

1. Si le volume attendu de contenu créé par l’utilisateur est élevé et qu’une instance MongoDB locale est possible, le choix sera [MSRP](msrp.md).

1. Pour des performances optimales pour le contenu des pages, le choix d’une [ferme de publication](../../help/sites-deploying/recommended-deploys.md#tarmk-farm) et d’un [ASRP](asrp.md) permettrait une mise à l’échelle optimale du contenu créé par l’utilisateur avec des opérations relativement simples.

Pour les deux, le déploiement peut être basé sur n’importe quel micro-noyau OAK.

Pour choisir le magasin commun approprié, prenez soigneusement en compte les [caractéristiques](working-with-srp.md#characteristics-of-srp-options) uniques de chacun.

Pour plus d’informations sur les micro-noyaux Oak, consultez [Déploiements recommandés](../../help/sites-deploying/recommended-deploys.md).

### Ferme de publication TarMK {#tarmk-publish-farm}

Lorsque la topologie consiste en une ferme de publication, les sujets pertinents sont les suivants :

* [Synchronisation des utilisateurs](sync.md)
* [Gestion des utilisateurs et des groupes d’utilisateurs](users.md)

### Recommandé : DSRP, MSRP ou ASRP {#recommended-dsrp-msrp-or-asrp}

| MicroKernel | RÉFÉRENTIEL DE CONTENU DU SITE | RÉFÉRENTIEL DE CONTENU GÉNÉRÉ PAR L’UTILISATEUR | FOURNISSEUR DE RESSOURCES DE STOCKAGE | MAGASIN COMMUN |
|-------------|------------------------|----------------------------------|---------------------------|---------------|
| quelconque | JCR | MySQL | DSRP | Oui |
| quelconque | JCR | MongoDB | MSRP | Oui |
| quelconque | JCR | Stockage à la demande d’Adobe | ASRP | Oui |

### JSRP {#jsrp}


| Déploiement | RÉFÉRENTIEL DE CONTENU DU SITE | RÉFÉRENTIEL DE CONTENU GÉNÉRÉ PAR L’UTILISATEUR | FOURNISSEUR DE RESSOURCES DE STOCKAGE | MAGASIN COMMUN |
|----------------------|------------------------|----------------------------------|---------------------------|---------------------------------|
| Batterie de serveurs TarMK (par défaut) | JCR | JCR | JSRP | Non |
| Cluster Oak | JCR | JCR | JSRP | Oui pour l’environnement de publication uniquement |

## Pour le développement {#for-development}

Pour les environnements hors production, [JSRP](jsrp.md) simplifie la configuration d’un environnement de développement avec une instance de création et une instance de publication.

Si vous choisissez [ASRP](asrp.md), [DSRP](dsrp.md) ou [MSRP](msrp.md) pour la production, il est également possible de configurer un environnement de développement similaire à l’aide du stockage à la demande d’Adobe ou de MongoDB. Pour obtenir un exemple, consultez [Comment configurer MongoDB pour la démonstration](demo-mongo.md).

## Références {#references}

* [Synchronisation des utilisateurs](sync.md)

  Décrit la synchronisation des données utilisateur entre les instances de batterie de publication.

* [Gestion des utilisateurs et des groupes d’utilisateurs](users.md)

  Décrit les rôles des utilisateurs et des groupes d’utilisateurs dans les environnements de création et de publication.

* UGC [magasin commun](working-with-srp.md)

  Décrit le stockage du contenu de la communauté séparément du contenu du site.

* [Magasins de nœuds et de données](../../help/sites-deploying/data-store-config.md)

  En gros, le contenu du site est stocké dans un magasin de nœuds. Pour Assets, un entrepôt de données peut être configuré pour stocker des données binaires. Pour Communities, un magasin commun doit être configuré pour sélectionner le SRP.

* [Éléments de stockage](../../help/sites-deploying/storage-elements-in-aem-6.md)

  Décrit les deux implémentations de stockage de nœud : Tar et MongoDB.
