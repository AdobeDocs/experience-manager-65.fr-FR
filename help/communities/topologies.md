---
title: Topologies recommandées pour Communities
description: Comment aborder la gestion du contenu généré par l’utilisateur
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
content-type: reference
topic-tags: deploying
exl-id: b6658330-d862-44e3-aac0-824fb91cd087
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '548'
ht-degree: 6%

---

# Topologies recommandées pour Communities {#recommended-topologies-for-communities}

Depuis AEM Communities 6.1, une approche unique a été adoptée pour gérer le contenu généré par les utilisateurs (UGC) envoyé par les visiteurs du site (membres) à partir de l’environnement de publication.

Cette approche diffère fondamentalement de la manière dont la plateforme AEM gère le contenu du site généralement géré à partir de l’environnement de création.

La plateforme AEM utilise un magasin de noeuds qui reproduit le contenu du site de l’auteur à la publication, tandis qu’AEM Communities utilise un seul magasin commun pour le contenu généré par l’utilisateur qui n’est jamais répliqué.

Pour le magasin UGC commun, il est nécessaire de choisir un [fournisseur de ressources de stockage (SRP)](working-with-srp.md). Les choix recommandés sont les suivants :

* [DSRP - Fournisseur de ressources de stockage de la base de données relationnelle](dsrp.md)
* [MSRP - Fournisseur de ressources de stockage MongoDB](msrp.md)
* [ASRP - Fournisseur de ressources de stockage d’Adobe](asrp.md)

une autre option de SRP, [JSRP - Fournisseur de ressources de stockage JCR](jsrp.md), ne prend pas en charge un magasin UGC commun pour les environnements de création et de publication à accès simultané.

L’exigence d’un magasin commun entraîne les topologies recommandées suivantes.

>[!NOTE]
>
>Pour AEM Communities, [Le contenu généré par l’utilisateur n’est jamais répliqué](working-with-srp.md#ugc-never-replicated).
>
>Lorsque le déploiement n’inclut pas une [magasin commun](working-with-srp.md), le contenu généré par l’utilisateur ne sera visible que sur l’instance de publication ou d’auteur AEM sur laquelle il a été saisi.
>

>[!NOTE]
>
>Pour plus d’informations sur la plateforme AEM, voir [Déploiements recommandés](../../help/sites-deploying/recommended-deploys.md) et [Présentation de la plateforme AEM](../../help/sites-deploying/data-store-config.md).

## Pour la production {#for-production}

La création d’un magasin commun pour le contenu généré par l’utilisateur est essentielle, de sorte que le déploiement sous-jacent dépend de sa capacité à prendre en charge un magasin commun.

Deux exemples :

1. Si le volume attendu du contenu créé par l’utilisateur est élevé et qu’une instance MongoDB locale est possible, le choix serait [MSRP](msrp.md).

1. Pour des performances optimales du contenu de la page, le choix d’un [batterie de publication](../../help/sites-deploying/recommended-deploys.md#tarmk-farm) et [ASRP](asrp.md) offre une mise à l’échelle optimale du contenu généré par l’utilisateur avec des opérations relativement simples.

Pour les deux, le déploiement peut être basé sur n’importe quel micronoyau OAK.

Pour choisir le magasin commun approprié, considérez soigneusement l’événement [caractéristiques](working-with-srp.md#characteristics-of-srp-options) de chacun.

Pour plus d’informations sur les microkernals Oak, voir [Déploiements recommandés](../../help/sites-deploying/recommended-deploys.md).

### Ferme de publication TarMK {#tarmk-publish-farm}

Lorsque la topologie est une ferme de publication, les sujets importants sont les suivants :

* [Synchronisation des utilisateurs](sync.md)
* [Gestion des utilisateurs et des groupes d’utilisateurs](users.md)

### Recommandé : DSRP, MSRP ou ASRP {#recommended-dsrp-msrp-or-asrp}

| MicroKernel | CONTENTREPOSITORY DU SITE | CONTENTREPOSITORY GÉNÉRÉ PAR L’UTILISATEUR | FOURNISSEUR DE RESSOURCES DE STOCKAGE | COMMON STORE |
|-------------|------------------------|----------------------------------|---------------------------|---------------|
| quelconque | JCR | MySQL | DSRP | Oui |
| quelconque | JCR | MongoDB | MSRP | Oui |
| quelconque | JCR | Adobe du stockage sur demande | ASRP | Oui |

### JSRP {#jsrp}


| Déploiement | CONTENTREPOSITORY DU SITE | CONTENTREPOSITORY GÉNÉRÉ PAR L’UTILISATEUR | FOURNISSEUR DE RESSOURCES DE STOCKAGE | COMMON STORE |
|----------------------|------------------------|----------------------------------|---------------------------|---------------------------------|
| Ferme TarMK (par défaut) | JCR | JCR | JSRP | Non |
| Grappe Oak | JCR | JCR | JSRP | Yesfor Publish uniquement |

## Pour le développement {#for-development}

Pour les environnements hors production, [JSRP](jsrp.md) simplifie la configuration d’un environnement de développement avec une instance d’auteur et une instance de publication.

Si vous choisissez [ASRP](asrp.md), [DSRP](dsrp.md) ou [MSRP](msrp.md) pour la production, il est également possible de configurer un environnement de développement similaire à l’aide du stockage à la demande Adobe ou de MongoDB. Pour consulter un exemple, reportez-vous à la section [Comment configurer MongoDB pour la démonstration](demo-mongo.md).

## Références {#references}

* [Synchronisation des utilisateurs](sync.md)

  Décrit la synchronisation des données utilisateur entre les instances de fermes de publication.

* [Gestion des utilisateurs et des groupes d’utilisateurs](users.md)

  Discute des rôles des utilisateurs et des groupes d’utilisateurs dans les environnements de création et de publication.

* UGC [magasin commun](working-with-srp.md)

  Décrit le stockage du contenu de la communauté distinct du contenu du site.

* [Magasins de noeuds et entrepôts de données](../../help/sites-deploying/data-store-config.md)

  Fondamentalement, le contenu du site est stocké dans un magasin de noeuds. Pour Assets, un entrepôt de données peut être configuré pour stocker des données binaires. Pour Communities, un magasin commun doit être configuré pour sélectionner la SRP.

* [Éléments de stockage](../../help/sites-deploying/storage-elements-in-aem-6.md)

  Décrit les deux implémentations de stockage de noeuds : Tar et MongoDB.
