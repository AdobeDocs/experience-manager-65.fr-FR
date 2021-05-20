---
title: SRP - Stockage de contenu de la communauté
seo-title: SRP - Stockage de contenu de la communauté
description: Depuis AEM Communities 6.1, le contenu généré par l’utilisateur est stocké dans un seul magasin commun fourni par un fournisseur de ressources de stockage (SRP).
seo-description: Depuis AEM Communities 6.1, le contenu généré par l’utilisateur est stocké dans un seul magasin commun fourni par un fournisseur de ressources de stockage (SRP).
uuid: d45e03c4-378b-4510-a6a0-d48c8cb879d9
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 6f13b21a-f4ef-4889-9b8e-4da3f846fa35
docset: aem65
role: Administrator
exl-id: e29aae44-67be-43d2-8004-c986412d9e63
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '921'
ht-degree: 0%

---

# SRP - Stockage de contenu de la communauté {#srp-community-content-storage}

## Présentation {#introduction}

Depuis AEM Communities 6.1, le contenu généré par l’utilisateur est stocké dans un seul magasin commun fourni par un fournisseur de ressources de stockage (SRP). Il existe plusieurs options de SRP que vous pouvez sélectionner, telles que ASRP, MSRP et JSRP.

Contrairement aux versions précédentes, il n’existe pas de réplication inverse/transfert du contenu créé par l’utilisateur entre les instances AEM. Au lieu de cela, la SRP rend le contenu créé par l’utilisateur directement accessible pour les opérations CRUD (création, lecture, mise à jour et suppression) de toutes les instances d’auteur et de publication, à l’exception de JSRP.

Vous trouverez ci-dessous les [caractéristiques de chaque option de SRP](#characteristics-of-srp-options), qui sont des informations cruciales pour le processus de décision lors du choix de la SRP appropriée et du [déploiement sous-jacent](/help/communities/topologies.md).

Pour plus d’informations sur l’utilisation de la SRP pour le contenu généré par l’utilisateur, voir [Présentation du fournisseur de ressources de stockage](/help/communities/srp.md).

>[!NOTE]
>
>La SRP s’applique uniquement au contenu de la communauté. Cela n’a aucune incidence sur l’emplacement de stockage du contenu du site ([node store](/help/sites-deploying/data-store-config.md)) et n’affecte pas la gestion sécurisée de l’enregistrement des utilisateurs, des profils utilisateur et des groupes d’utilisateurs entre les instances d’AEM (voir aussi [Gestion des données utilisateur](#managing-user-data)).

>[!CAUTION]
>
>À compter de la version AEM 6.1, le contenu généré par l’utilisateur n’est jamais répliqué ](#ugc-never-replicated).[
>
>Lorsque le déploiement n’inclut pas de magasin commun, tel que la topologie [JSRP](/help/communities/topologies.md#jsrp) par défaut, le contenu généré par l’utilisateur n’est visible que sur l’instance de publication ou d’auteur AEM sur laquelle il a été saisi. Ce n’est que si la topologie inclut une grappe de publication que le contenu généré par l’utilisateur sera visible sur n’importe quelle instance de publication.

## Caractéristiques des options SRP {#characteristics-of-srp-options}

[ASRP - Fournisseur de ressources de stockage d’Adobe](/help/communities/asrp.md)

Avec cette option, le contenu créé par l’utilisateur est conservé à distance dans un service cloud hébergé et géré par Adobe. Il nécessite une licence supplémentaire et l’utilisation d’un gestionnaire de compte pour configurer le compte pour cette licence spécifique. ASRP requiert :

* Service cloud associé fourni et pris en charge par Adobe pour stocker le contenu de la communauté.
* Choix d’un centre de données dans une zone géographique spécifique (États-Unis, EMEA, APAC).

* Tous les accès programmatiques au contenu généré par l’utilisateur sont effectués par le biais de l’API SRP.

ASRP convient :

* Pour la ferme de publication TarMK.
* Lorsqu’il n’y a aucune intention d’investir dans le stockage local.

>[!NOTE]
>
>Le téléchargement des pièces jointes aux publications (ou commentaires) dans ASRP est limité à 50 Mo.

[MSRP - Fournisseur de ressources de stockage MongoDB](/help/communities/msrp.md)

Avec cette option, le contenu généré par l’utilisateur est conservé directement dans une instance MongoDB locale.

MSRP requiert :

* Une installation locale sous licence de MongoDB pour stocker le contenu de la communauté.
* Une installation locale d’Apache Solr.
* Tous les accès programmatiques au contenu généré par l’utilisateur sont effectués par le biais de l’API SRP.

ASRP convient :

* Pour une ferme de publication TarMK existante.
* Pour une grappe MongoMK ou RdbMK.
* En cas d’attente de grands volumes de contenu de communauté.

[DSRP - Fournisseur de ressources de stockage de la base de données relationnelle](/help/communities/dsrp.md)

Avec cette option, le contenu généré par l’utilisateur est conservé directement dans une instance de base de données MySQL locale.

DSRP requiert :

* Une installation locale de MySQL pour stocker le contenu de la communauté.
* Une installation locale d’Apache Solr.
* Tous les accès programmatiques au contenu généré par l’utilisateur sont effectués par le biais de l’API SRP.

DSRP convient :

* Pour une ferme de publication TarMK existante.
* Pour une grappe MongoMK ou RdbMK.
* En cas d’attente de grands volumes de contenu de communauté.

[JSRP - Fournisseur de ressources de stockage JCR](/help/communities/jsrp.md)

Avec l’option par défaut, il n’y a pas de boutique courante. Le contenu généré par l’utilisateur n’est conservé que dans le même référentiel JCR que l’instance AEM dans laquelle il a été saisi.

JSRP:

* Stocke le contenu de la communauté dans le référentiel JCR de l’instance d’auteur ou de publication AEM à laquelle il a été publié.
* Nécessite l’accès programmatique au contenu généré par l’utilisateur via l’API SRP.
* Nécessite un cluster de publication si plusieurs instances de publication sont déployées (il n’existe aucun mécanisme de réplication entre les instances de publication dans une ferme TarMK).
* la modération est effectuée uniquement dans l’environnement de publication (il n’existe aucun mécanisme de réplication inverse/transfert entre l’auteur et la publication).
* Il est préférable pour le développement, les démonstrations et la formation.

## Configuration de la SRP {#configuring-srp}

La spécification de l’option de stockage par défaut, en fonction du déploiement sous-jacent, est effectuée via la [console Configuration de stockage](/help/communities/srp-config.md).

Pour plus d’informations sur la configuration de chaque option, voir :

* [ASRP - Fournisseur de ressources de stockage d’Adobe](/help/communities/asrp.md)
* [MSRP - Fournisseur de ressources de stockage MongoDB](/help/communities/msrp.md)
* [DSRP - Fournisseur de ressources de stockage de la base de données relationnelle](/help/communities/dsrp.md)
* [JSRP - Fournisseur de ressources de stockage JCR](/help/communities/jsrp.md)

Si aucune option de stockage n’est activement sélectionnée, JSRP est activé par défaut.

## Informations supplémentaires {#additional-information}

### UGC jamais répliqué {#ugc-never-replicated}

Dans l’environnement de création, un auteur crée du contenu de page et le réplique dans l’environnement de publication. Lorsqu’une page comprend une fonction AEM Communities interactive (commentaires, révisions, forum, blog ou Q&amp;R, par exemple), l’interaction des membres (connectés aux visiteurs du site) sur une instance de publication génère du contenu généré par l’utilisateur (UGC) entré dans l’environnement de publication.

Auparavant, ce contenu de communauté était répliqué par inverse vers les instances d’auteur et répliqué par l’auteur vers les instances de publication. Il était problématique de maintenir la cohérence entre les instances AEM avec la réplication inverse et vers l’avant.

À partir d’AEM Communities 6.1, le besoin de réplication du contenu créé par l’utilisateur a été éliminé en utilisant le stockage partagé pour le contenu créé par l’utilisateur, comme décrit ci-dessus.

Bien que le contenu du site soit répliqué, le contenu généré par l’utilisateur n’est jamais répliqué.

### Gestion des données utilisateur {#managing-user-data}

Les [*utilisateurs*, *groupes d’utilisateurs* et les *profils d’utilisateurs*](/help/communities/users.md) sont également intéressants pour les communautés. Ces données liées à l’utilisateur, lorsqu’elles sont créées et mises à jour dans l’environnement de publication, doivent être mises à la disposition d’autres instances de publication lorsque la topologie est une [ferme de publication](/help/sites-deploying/recommended-deploys.md#tarmk-farm).

Depuis AEM Communities 6.1, les données liées à l’utilisateur sont synchronisées à l’aide de la distribution Sling plutôt que de la réplication. Pour plus d’informations, voir [Synchronisation des utilisateurs](/help/communities/sync.md).

### Mise à niveau vers AEM Communities 6.5 {#upgrading-to-aem-communities}

Lors de la mise à niveau vers AEM 6.5 Communities, si du contenu créé par l’utilisateur préexistant doit être conservé, des étapes doivent être prises selon que la communauté AEM 5.6.1 ou 6.0 a utilisé le stockage Adobe à la demande ou le stockage on-premise du contenu créé par l’utilisateur.

Pour plus d’informations, voir [Mise à niveau vers AEM Communities 6.5](/help/communities/upgrade.md).
