---
title: SRP - Stockage de contenu de la communauté
description: Depuis AEM Communities 6.1, le contenu créé par l’utilisateur est stocké dans un magasin commun unique fourni par un fournisseur de ressources de stockage (SRP)
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
docset: aem65
role: Admin
exl-id: e29aae44-67be-43d2-8004-c986412d9e63
solution: Experience Manager
feature: Communities
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
feature_v2:
  - id: b013f126-a97e-52d1-9f79-cb5bbb12114e
    internal-label: Communities
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
source-git-commit: 751e1826ed53df7522418e50a206f0fe622256a4
workflow-type: tm+mt
source-wordcount: '912'
ht-degree: 0%
---
# SRP - Stockage de contenu de la communauté {#srp-community-content-storage}

## Présentation {#introduction}

Depuis AEM Communities 6.1, le contenu créé par l’utilisateur est stocké dans un magasin commun unique fourni par un fournisseur de ressources de stockage (SRP). Il existe plusieurs options SRP parmi lesquelles choisir, telles que ASRP, MSRP et JSRP.

Contrairement aux versions précédentes, il n’existe aucune réplication inverse/directe du contenu créé par l’utilisateur sur les instances AEM. Au lieu de cela, le SRP rend le contenu créé par l’utilisateur directement accessible pour les opérations de création, de lecture, de mise à jour et de suppression (CRUD) de toutes les instances de création et de publication, à l’exception de JSRP.

Vous trouverez ci-dessous les [caractéristiques de chaque option de SRP](#characteristics-of-srp-options), qui constituent des informations cruciales pour le processus de décision lors du choix du SRP approprié et du [déploiement sous-jacent](/help/communities/topologies.md).

Pour plus d’informations sur l’utilisation de SRP pour le contenu créé par l’utilisateur, consultez [Présentation du fournisseur de ressources de stockage](/help/communities/srp.md).

>[!NOTE]
>
>SRP s’applique uniquement au contenu de la communauté. Elle n’a aucune incidence sur l’emplacement de stockage du contenu du site ([magasin de nœuds](/help/sites-deploying/data-store-config.md)) et n’affecte pas la gestion sécurisée de l’enregistrement des utilisateurs, des profils utilisateur et des groupes d’utilisateurs entre les instances AEM (voir également [Gestion des données utilisateur](#managing-user-data)).

>[!CAUTION]
>
>Depuis AEM 6.1, [le contenu créé par l’utilisateur n’est jamais répliqué](#ugc-never-replicated).
>
>Lorsque le déploiement n’inclut pas de magasin commun, comme la topologie [JSRP](/help/communities/topologies.md#jsrp) par défaut, le contenu créé par l’utilisateur n’est visible que sur l’instance de publication ou d’auteur AEM sur laquelle il a été saisi. Le contenu créé par l’utilisateur n’est visible sur aucune instance de publication que si la topologie inclut un cluster de publication.

## Caractéristiques des options SRP {#characteristics-of-srp-options}

[ASRP - Fournisseur de ressources de stockage Adobe](/help/communities/asrp.md)

Avec cette option, le contenu créé par l’utilisateur est conservé à distance dans un service cloud hébergé et géré par Adobe. Vous avez besoin d’une licence supplémentaire et de travailler avec un représentant de compte pour configurer le compte pour cette licence spécifique. ASRP requiert :

* Service cloud associé fourni et pris en charge par Adobe pour stocker le contenu de la communauté.
* Choix d’un centre de données dans une zone géographique spécifique (États-Unis, EMEA, APAC).

* Tous les accès programmatiques au contenu créé par l’utilisateur s’effectuent via l’API SRP.

ASRP convient :

* Pour la ferme de publication TarMK.
* Lorsqu’il n’y a aucune intention d’investir dans le stockage local.

>[!NOTE]
>
>Le chargement des pièces jointes aux publications (ou commentaires) dans ASRP est limité à 50 Mo.

[MSRP - Fournisseur de ressources de stockage MongoDB](/help/communities/msrp.md)

Avec cette option, le contenu créé par l’utilisateur est conservé directement dans une instance MongoDB locale.

MSRP requiert :

* Une installation sous licence locale de MongoDB pour stocker le contenu de la communauté.
* Une installation locale d’Apache Solr.
* Tous les accès programmatiques au contenu créé par l’utilisateur s’effectuent via l’API SRP.

ASRP convient :

* Pour une ferme de publication TarMK existante.
* Pour un cluster MongoMK ou RdbMK.
* Lorsque vous prévoyez d’importants volumes de contenu de la communauté .

[DSRP - Fournisseur de ressources de stockage de base de données relationnelle](/help/communities/dsrp.md)

Avec cette option, le contenu créé par l’utilisateur est conservé directement dans une instance de base de données MySQL locale.

DSRP requiert :

* Une installation locale de MySQL pour stocker le contenu de la communauté.
* Une installation locale d’Apache Solr.
* Tous les accès programmatiques au contenu créé par l’utilisateur s’effectuent via l’API SRP.

DSRP convient :

* Pour une ferme de publication TarMK existante.
* Pour un cluster MongoMK ou RdbMK.
* Lorsque vous prévoyez d’importants volumes de contenu de la communauté .

[JSRP - Fournisseur de ressources de stockage JCR](/help/communities/jsrp.md)

Avec l’option par défaut, il n’existe pas de magasin commun. Le contenu créé par l’utilisateur est conservé uniquement dans le même référentiel JCR que l’instance AEM dans laquelle il a été saisi.

JSRP :

* Stocke le contenu de la communauté dans le référentiel JCR de l’instance de création ou de publication AEM sur laquelle il a été publié.
* Nécessite que tous les accès programmatiques au contenu créé par l’utilisateur soient effectués via l’API SRP.
* Nécessite un cluster de publication si plusieurs instances de publication sont déployées (il n’existe aucun mécanisme de réplication entre les instances de publication dans une ferme TarMK).
* la modération n’est effectuée que dans l’environnement de publication (il n’existe aucun mécanisme de réplication inverse/direct entre l’instance de création et celle de publication).
* Idéal pour le développement, les démonstrations et la formation.

## Configuration de SRP {#configuring-srp}

La spécification de l’option de stockage par défaut, en fonction du déploiement sous-jacent, s’effectue via la [console de configuration de stockage](/help/communities/srp-config.md).

Pour les détails de configuration de chaque option, voir :

* [ASRP - Fournisseur de ressources de stockage Adobe](/help/communities/asrp.md)
* [MSRP - Fournisseur de ressources de stockage MongoDB](/help/communities/msrp.md)
* [DSRP - Fournisseur de ressources de stockage de base de données relationnelle](/help/communities/dsrp.md)
* [JSRP - Fournisseur de ressources de stockage JCR](/help/communities/jsrp.md)

Si aucune option de stockage n’est sélectionnée, JSRP est activé par défaut.

## Informations supplémentaires {#additional-information}

### Contenu créé par l’utilisateur jamais répliqué {#ugc-never-replicated}

Dans l’environnement de création, un auteur crée du contenu de page et le réplique dans l’environnement de publication. Lorsqu’une page comprend une fonctionnalité AEM Communities interactive, telle que des commentaires, des révisions, un forum, un blog ou un QnA, l’interaction des membres (visiteurs du site connectés) sur une instance de publication entraîne la saisie de contenu généré par l’utilisateur dans l’environnement de publication.

Auparavant, ce contenu de communauté était répliqué par inverse sur les instances de création et de création répliqué sur les instances de publication. Le maintien de la cohérence entre les instances AEM avec la réplication inverse et directe posait problème.

Depuis AEM Communities 6.1, la réplication du contenu créé par l’utilisateur n’est plus nécessaire. Le stockage partagé du contenu créé par l’utilisateur a été utilisé, comme décrit ci-dessus.

Lorsque le contenu du site est répliqué, le contenu créé par l’utilisateur n’est jamais répliqué.

### Gestion des données utilisateur {#managing-user-data}

Les CommunityIes s’intéressent également aux [*utilisateurs*, *groupes d’utilisateurs* et *profils d’utilisateurs*](/help/communities/users.md). Ces données utilisateur, lorsqu’elles sont créées et mises à jour dans l’environnement de publication, doivent être mises à la disposition d’autres instances de publication lorsque la topologie consiste en une [&#x200B; ferme de publication &#x200B;](/help/sites-deploying/recommended-deploys.md#tarmk-farm).

Depuis AEM Communities 6.1, les données utilisateur sont synchronisées à l’aide de la distribution Sling au lieu de la réplication. Pour plus d’informations, consultez [Synchronisation des utilisateurs](/help/communities/sync.md).

### Mise à niveau vers AEM Communities 6.5 {#upgrading-to-aem-communities}

Lors de la mise à niveau vers AEM 6.5 Communities, si du contenu créé par l’utilisateur préexistant doit être conservé, des mesures doivent être prises selon que la communauté AEM 5.6.1 ou AEM 6.0 a utilisé le stockage à la demande d’Adobe ou le stockage sur site du contenu créé par l’utilisateur.

Pour plus d’informations, consultez [Mise à niveau vers AEM Communities 6.5](/help/communities/upgrade.md).
