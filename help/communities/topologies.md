---
title: Topologies recommandées pour Communities
seo-title: Topologies recommandées pour Communities
description: Comment aborder la gestion du contenu généré par l’utilisateur (UGC)
seo-description: Comment aborder la gestion du contenu généré par l’utilisateur (UGC)
uuid: 4bc1c423-0ba9-4f2e-b11c-4d6824f45641
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
content-type: reference
topic-tags: deploying
discoiquuid: 46f135de-a0bf-451d-bdcc-fb29188250aa
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Topologies recommandées pour Communities {#recommended-topologies-for-communities}

Depuis la version 6.1 des Communautés AEM, une approche unique a été adoptée pour la gestion du contenu généré par les utilisateurs (UGC) soumis par les visiteurs du site (membres) de l’environnement de publication.

Cette approche diffère fondamentalement de la manière dont la plateforme AEM gère le contenu du site généralement géré à partir de l’environnement d’auteur.

La plate-forme AEM utilise un magasin de noeuds qui répliquent le contenu du site de l’auteur à la publication, tandis que les communautés AEM utilisent un magasin commun unique pour l’UGC qui n’est jamais répliqué.

Pour le magasin UGC commun, il est nécessaire de choisir un fournisseur de ressources de [stockage (SRP)](working-with-srp.md). Les choix recommandés sont les suivants :

* [DSRP - Fournisseur de ressources de stockage de base de données relationnel](dsrp.md)
* [MSRP - Fournisseur de ressources de stockage MongoDB](msrp.md)
* [ASRP - Fournisseur de ressources de stockage Adobe](asrp.md)

Une autre option SRP, [JSRP - JCR Storage Resource Provider](jsrp.md), ne prend pas en charge un magasin UGC commun pour les environnements d’auteur et de publication pour les deux accès.

L’utilisation d’une boutique commune génère les topologies recommandées suivantes.

>[!NOTE]
>
>Pour les communautés AEM, [UGC n’est jamais répliqué](working-with-srp.md#ugc-never-replicated).
>
>Lorsque le déploiement n’inclut pas de magasin [](working-with-srp.md)commun, l’UGC est visible uniquement sur l’instance de publication ou d’auteur AEM sur laquelle il a été saisi.

>[!NOTE]
>
>Pour plus d’informations sur la plateforme AEM, voir Déploiements [recommandés et](../../help/sites-deploying/recommended-deploys.md) Présentation de la plateforme [](../../help/sites-deploying/data-store-config.md)AEM.

## Pour la production {#for-production}

Il est essentiel de créer un magasin commun pour l&#39;UGC, et le déploiement sous-jacent dépend donc de sa capacité à soutenir un magasin commun.

Deux exemples :

1) Si le volume attendu de l’UGC est élevé et qu’une instance MongoDB locale est possible, le choix sera [MSRP](msrp.md).

2) Pour des performances optimales pour le contenu de la page, le choix d’une batterie de [publication](../../help/sites-deploying/recommended-deploys.md#tarmk-farm) et d’un programme [ASRP](asrp.md) donnerait une mise à l’échelle optimale de l’UGC avec des opérations relativement simples.

Pour les deux, le déploiement peut être basé sur n&#39;importe quel micronoyau OAK.

Pour choisir le magasin commun approprié, réfléchissez soigneusement aux [caractéristiques](working-with-srp.md#characteristics-of-srp-options) uniques de chacun.

Pour plus d&#39;informations sur les microkernals d&#39;Oak, consultez Déploiements [recommandés](../../help/sites-deploying/recommended-deploys.md).

### Ferme de publication TarMK {#tarmk-publish-farm}

Lorsque la topologie est une batterie de publication, les sujets importants sont les suivants :

* [Synchronisation des utilisateurs](sync.md)
* [Gestion des utilisateurs et des groupes d’utilisateurs](users.md)

### Recommandé : DSRP, MSRP ou ASRP {#recommended-dsrp-msrp-or-asrp}

| MicroKernel | CONTENTREPOSITORY DU SITE | CONTENTREPOSITAIRE GÉNÉRÉ PAR L’UTILISATEUR | FOURNISSEUR DE RESSOURCES DE STOCKAGE | COMMON STORE |
|-------------|------------------------|----------------------------------|---------------------------|---------------|
| quelconque | JCR | MySQL | DSRP | Oui |
| quelconque | JCR | MongoDB | MSRP | Oui |
| quelconque | JCR | Stockage à la demande Adobe | ASRP | Oui |

### JSRP {#jsrp}


| Déploiement | CONTENTREPOSITORY DU SITE | CONTENTREPOSITAIRE GÉNÉRÉ PAR L’UTILISATEUR | FOURNISSEUR DE RESSOURCES DE STOCKAGE | COMMON STORE |
|----------------------|------------------------|----------------------------------|---------------------------|---------------------------------|
| Ferme TarMK (par défaut) | JCR | JCR | JSRP | Non |
| Grappe Oak | JCR | JCR | JSRP | Yesfor Publishing Environment uniquement |

## Pour le développement {#for-development}

Pour les environnements de non production, [JSRP](jsrp.md) simplifie la configuration d’un environnement de développement avec une instance d’auteur et une instance de publication.

Si vous choisissez [ASRP](asrp.md), [DSRP](dsrp.md) ou [MSRP](msrp.md) pour la production, il est également possible de configurer un environnement de développement similaire à l’aide du stockage à la demande Adobe ou de MongoDB. Pour obtenir un exemple, reportez-vous à la section [Comment configurer MongoDB pour la démonstration](demo-mongo.md).

## Références {#references}

* [Synchronisation des utilisateurs](sync.md)

   Parle de la synchronisation des données utilisateur entre les instances de batterie de publication.

* [Gestion des utilisateurs et des groupes d’utilisateurs](users.md)

   Parle des rôles des utilisateurs et des groupes d’utilisateurs dans les environnements de création et de publication.

* Boutique [commune UGC](working-with-srp.md)

   Décrit le stockage du contenu de la communauté séparé du contenu du site

* [Stockages de noeuds et de données](../../help/sites-deploying/data-store-config.md)

   Essentiellement, le contenu du site est stocké dans un magasin de noeuds. Pour les ressources, un magasin de données peut être configuré pour stocker des données binaires. Pour les communautés, un magasin commun doit être configuré pour sélectionner le SRP.

* [Éléments de stockage dans AEM 6.3](../../help/sites-deploying/storage-elements-in-aem-6.md)

   Décrit les implémentations de stockage sur deux noeuds : Tar et MongoDB.
