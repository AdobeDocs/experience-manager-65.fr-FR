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
source-git-commit: f375b40c084ee363757b78c602091f38524b8b03
workflow-type: tm+mt
source-wordcount: '562'
ht-degree: 6%

---


# Topologies recommandées pour Communities {#recommended-topologies-for-communities}

Depuis AEM Communities 6.1, une approche unique a été adoptée pour la gestion du contenu généré par les utilisateurs (UGC) soumis par les visiteurs du site (membres) à partir de l’environnement de publication.

Cette approche est fondamentalement différente de la manière dont la plateforme AEM gère le contenu du site qui est généralement géré à partir de l’environnement d’auteur.

La plate-forme AEM utilise un magasin de noeuds qui reproduit le contenu du site de l’auteur à la publication, tandis qu’AEM Communities utilise un magasin commun unique pour UGC qui n’est jamais répliqué.

Pour le magasin UGC commun, il est nécessaire de choisir un fournisseur de ressources [d&#39;enregistrement (SRP)](working-with-srp.md). Les choix recommandés sont les suivants :

* [DSRP - Fournisseur de ressources d&#39;Enregistrement de données relationnelles](dsrp.md)
* [MSRP - Fournisseur de ressources d&#39;Enregistrement MongoDB](msrp.md)
* [ASRP - Fournisseur de ressources d&#39;Enregistrement d&#39;Adobe](asrp.md)

Une autre option SRP, [JSRP - JCR Enregistrement Resource Provider](jsrp.md), ne prend pas en charge un magasin UGC commun pour l’auteur et la publication d’environnements sur les deux accès.

Si un magasin commun est requis, les topologies suivantes sont recommandées.

>[!NOTE]
>
>Pour AEM Communities, [UGC n’est jamais répliqué](working-with-srp.md#ugc-never-replicated).
>
>Lorsque le déploiement n’inclut pas de magasin [](working-with-srp.md)commun, l’UGC n’est visible que sur l’instance de publication ou d’auteur AEM sur laquelle il a été saisi.


>[!NOTE]
>
>Pour plus d’informations sur la plateforme AEM, voir Déploiements [](../../help/sites-deploying/recommended-deploys.md) recommandés et [Présentation de la plateforme](../../help/sites-deploying/data-store-config.md)AEM.

## Pour la production {#for-production}

Il est essentiel de créer un magasin commun pour l&#39;UGC et, par conséquent, le déploiement sous-jacent dépend de sa capacité à soutenir un magasin commun.

Deux exemples :

1. Si le volume attendu de l’UGC est élevé et qu’une instance MongoDB locale est possible, le choix sera alors [MSRP](msrp.md).

1. Pour optimiser les performances du contenu de la page, le choix d’une batterie de [publication](../../help/sites-deploying/recommended-deploys.md#tarmk-farm) et d’un [ASRP](asrp.md) permettrait une mise à l’échelle optimale de l’UGC avec des opérations relativement simples.

Pour les deux cas, le déploiement peut être basé sur tout micronoyau OAK.

Pour choisir le magasin commun approprié, réfléchissez soigneusement aux [caractéristiques](working-with-srp.md#characteristics-of-srp-options) uniques de chacun.

Pour plus de détails sur les micro-kernals de chêne, consultez Déploiements [](../../help/sites-deploying/recommended-deploys.md)recommandés.

### Ferme de publication TarMK {#tarmk-publish-farm}

Lorsque la topologie est une batterie de publication, les sujets importants sont les suivants :

* [Synchronisation des utilisateurs](sync.md)
* [Gestion des utilisateurs et des groupes d’utilisateurs](users.md)

### Recommandé : DSRP, MSRP ou ASRP {#recommended-dsrp-msrp-or-asrp}

| MicroKernel | CONTENTREPOSITORY DU SITE | CONTENTREPOSITORY GÉNÉRÉ PAR L’UTILISATEUR | FOURNISSEUR DE RESSOURCES ENREGISTREMENTS | COMMON STORE |
|-------------|------------------------|----------------------------------|---------------------------|---------------|
| quelconque | JCR | MySQL | DSRP | Oui |
| quelconque | JCR | MongoDB | MSRP | Oui |
| quelconque | JCR | Stockage à la demande Adobe | ASRP | Oui |

### JSRP {#jsrp}


| Déploiement | CONTENTREPOSITORY DU SITE | CONTENTREPOSITORY GÉNÉRÉ PAR L’UTILISATEUR | FOURNISSEUR DE RESSOURCES ENREGISTREMENTS | COMMON STORE |
|----------------------|------------------------|----------------------------------|---------------------------|---------------------------------|
| Ferme TarMK (par défaut) | JCR | JCR | JSRP | Non |
| Grappe de chêne | JCR | JCR | JSRP | Yesfor publish environnement only |

## Pour le développement {#for-development}

Pour les environnements hors production, [JSRP](jsrp.md) simplifie la configuration d’un environnement de développement avec une instance d’auteur et une instance de publication.

Si vous choisissez [ASRP](asrp.md), [DSRP](dsrp.md) ou [MSRP](msrp.md) pour la production, il est également possible de mettre en place un environnement de développement similaire en utilisant un enregistrement à la demande Adobe ou MongoDB. Pour un exemple, reportez-vous à la section [HowTo Setup MongoDB for Demo](demo-mongo.md)(Configuration de MongoDB pour la démonstration).

## Références {#references}

* [Synchronisation des utilisateurs](sync.md)

   Traite de la synchronisation des données utilisateur entre les instances de batterie de publication.

* [Gestion des utilisateurs et des groupes d’utilisateurs](users.md)

   Parle des rôles des utilisateurs et des groupes d’utilisateurs dans les environnements d’auteur et de publication.

* Boutique [commune UGC](working-with-srp.md)

   Décrit l’enregistrement du contenu de la communauté distinct du contenu du site.

* [Stockages de noeuds et de données](../../help/sites-deploying/data-store-config.md)

   Essentiellement, le contenu du site est stocké dans un magasin de noeuds. Pour les ressources, une banque de données peut être configurée pour stocker des données binaires. Pour les communautés, un magasin commun doit être configuré pour sélectionner le SRP.

* [Éléments de stockage dans AEM 6.3](../../help/sites-deploying/storage-elements-in-aem-6.md)

   Décrit les deux mises en oeuvre d’enregistrement de noeud : Tar et MongoDB.
