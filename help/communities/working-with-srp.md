---
title: SRP - Stockage de contenu communautaire
seo-title: SRP - Stockage de contenu communautaire
description: Depuis la version 6.1 des Communautés AEM, le contenu généré par l’utilisateur est stocké dans un seul magasin commun fourni par un fournisseur de ressources de stockage (SRP).
seo-description: Depuis la version 6.1 des Communautés AEM, le contenu généré par l’utilisateur est stocké dans un seul magasin commun fourni par un fournisseur de ressources de stockage (SRP).
uuid: d45e03c4-378b-4510-a6a0-d48c8cb879d9
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 6f13b21a-f4ef-4889-9b8e-4da3f846fa35
docset: aem65
translation-type: tm+mt
source-git-commit: 70e6f2d8366456e5091b7b775dc40914948921ab

---


# SRP - Stockage de contenu communautaire{#srp-community-content-storage}

## Présentation {#introduction}

Depuis la version 6.1 des Communautés AEM, le contenu généré par l’utilisateur est stocké dans un seul magasin commun fourni par un fournisseur de ressources de stockage (SRP). Il existe plusieurs options SRP à partir desquelles choisir, telles que ASRP, MSRP et JSRP.

Contrairement aux versions précédentes, il n’existe pas de réplication inverse/avancée de l’UGC dans les instances AEM. Au lieu de cela, le protocole SRP rend l’UGC directement accessible pour créer, lire, mettre à jour et supprimer des opérations CRUD de toutes les instances d’auteur et de publication, à l’exception de JSRP.

Voici les [caractéristiques de chaque option](#characteristics-of-srp-options)de PRS, qui est une information essentielle pour le processus décisionnel lors du choix du PRS approprié et du déploiement [](/help/communities/topologies.md)sous-jacent.

Pour plus d&#39;informations sur l&#39;utilisation de SRP pour l&#39;UGC, consultez Présentation [du fournisseur de ressources de](/help/communities/srp.md)stockage.

>[!NOTE]
>
>SRP s’applique uniquement au contenu de la communauté. Elle n’affecte pas l’emplacement de stockage du contenu du site (magasin[de](/help/sites-deploying/data-store-config.md)noeuds) et n’affecte pas la gestion sécurisée de l’enregistrement des utilisateurs, des profils utilisateur et des groupes d’utilisateurs entre les instances AEM (voir aussi [Gestion des données](#managing-user-data)utilisateur).

>[!CAUTION]
>
>Depuis AEM 6.1, [UGC n’est jamais répliqué](#ugc-never-replicated).
>
>Lorsque le déploiement n’inclut pas de magasin commun, tel que la topologie [JSRP](/help/communities/topologies.md#jsrp) par défaut, l’UGC n’est visible que sur l’instance de publication ou d’auteur AEM sur laquelle il a été saisi. L’UGC n’est visible sur aucune instance de publication que si la topologie inclut une grappe de publication.

## Caractéristiques des options SRP {#characteristics-of-srp-options}

[ASRP - Fournisseur](/help/communities/asrp.md)de ressources de stockage Adobe Avec cette option, l’UGC est conservé à distance dans un service de cloud hébergé et géré par Adobe. Il nécessite une licence supplémentaire et l’aide d’un gestionnaire de compte pour configurer le compte pour cette licence spécifique. ASRP requiert :

* Service cloud associé fourni et pris en charge par Adobe pour stocker le contenu de la communauté.
* Choix d’un centre de données dans une zone géographique spécifique (Etats-Unis, EMEA, APAC).

* Tous les accès programmatiques à l’UGC doivent être effectués via l’API SRP.

ASRP convient :

* pour la batterie de publication TarMK.
* lorsqu&#39;il n&#39;y a aucune intention d&#39;investir dans le stockage local.

>[!NOTE]
>
>Le téléchargement de pièces jointes vers des publications (ou commentaires) dans ASRP est limité à 50 Mo.

[MSRP - Fournisseur](/help/communities/msrp.md)de ressources de stockage MongoDB Avec cette option, l’UGC est conservé directement dans une instance MongoDB locale.

Le MSRP requiert :

* Installation locale sous licence de MongoDB pour stocker le contenu de la communauté.
* Une installation locale d&#39;Apache Solr.
* Tous les accès programmatiques à l’UGC doivent être effectués via l’API SRP.

ASRP convient :

* Pour une batterie de publication TarMK existante.
* Pour une grappe MongoMK ou RdbMK.
* Lorsque vous vous attendez à de gros volumes de contenu de la communauté.

[DSRP - Fournisseur](/help/communities/dsrp.md)de ressources de stockage de base de données relationnelles Avec cette option, l’UGC est conservé directement dans une instance de base de données MySQL locale.

Le DSRP requiert :

* Installation locale de MySQL pour stocker le contenu de la communauté.
* Une installation locale d&#39;Apache Solr.
* Tous les accès programmatiques à l’UGC doivent être effectués via l’API SRP.

Le DSRP convient :

* Pour une batterie de publication TarMK existante.
* Pour une grappe MongoMK ou RdbMK.
* Lorsque vous vous attendez à de gros volumes de contenu de la communauté.

[JSRP - Fournisseur](/help/communities/jsrp.md)de ressources de stockage JCR Avec l’option par défaut, il n’existe aucun magasin commun. L’UGC est conservé uniquement dans le même référentiel JCR que l’instance AEM dans laquelle il a été saisi.

JSRP:

* Stocke le contenu de la communauté dans le référentiel JCR de l’instance d’auteur ou de publication AEM à laquelle il a été publié.
* Nécessite que tous les accès programmatiques à l’UGC soient effectués via l’API SRP.
* Nécessite une grappe de publication si plusieurs instances de publication sont déployées (il n’existe aucun mécanisme de réplication parmi les instances de publication dans une batterie TarMK).
* la modération est exécutée uniquement dans l’environnement de publication (il n’existe aucun mécanisme de réplication inverse/transfert entre l’auteur et la publication).
* Il est préférable pour le développement, les démonstrations et la formation.

## Configuration de SRP {#configuring-srp}

La spécification de l&#39;option de stockage par défaut, en fonction du déploiement sous-jacent, est effectuée via la console [Configuration du](/help/communities/srp-config.md)stockage.

Pour plus d’informations sur la configuration de chaque option, voir :

* [ASRP - Fournisseur de ressources de stockage Adobe](/help/communities/asrp.md)
* [MSRP - Fournisseur de ressources de stockage MongoDB](/help/communities/msrp.md)
* [DSRP - Fournisseur de ressources de stockage de base de données relationnel](/help/communities/dsrp.md)
* [JSRP - Fournisseur de ressources de stockage JCR](/help/communities/jsrp.md)

Si aucune option de stockage n’est activement sélectionnée, JSRP est activé par défaut.

## Informations supplémentaires {#additional-information}

### UGC jamais répliqué {#ugc-never-replicated}

Dans l’environnement de création, un auteur crée du contenu de page et le répliquera dans l’environnement de publication. Lorsqu’une page comprend une fonction interactive Communautés AEM (commentaires, révisions, forum, blog ou QnA, par exemple), l’interaction des membres (connectés aux visiteurs du site) sur une instance de publication génère l’entrée de contenu généré par l’utilisateur dans l’environnement de publication.

Auparavant, ce contenu de la communauté était répliqué de manière inversée aux instances d’auteur et répliqué par l’auteur aux instances de publication. Il était problématique de maintenir la cohérence entre les instances AEM avec la réplication inverse et avancée.

À partir de la version 6.1 des Communautés AEM, le besoin de réplication de l’UGC a été éliminé en utilisant le stockage partagé pour l’UGC, comme décrit ci-dessus.

Bien que le contenu du site soit répliqué, UGC n’est jamais répliqué.

### Gestion des données utilisateur {#managing-user-data}

Les [*utilisateurs *, les groupes d’* utilisateurs et les profils *d’**](/help/communities/users.md)utilisateurs présentent également un intérêt pour CommunitIes. Ces données utilisateur, lorsqu’elles sont créées et mises à jour dans l’environnement de publication, doivent être mises à la disposition des autres instances de publication lorsque la topologie est une batterie de[publication](/help/sites-deploying/recommended-deploys.md#tarmk-farm).

Depuis la version 6.1 des communautés AEM, les données liées aux utilisateurs sont synchronisées à l’aide de la distribution Sling au lieu de la réplication. Pour plus d’informations, consultez Synchronisation [des](/help/communities/sync.md)utilisateurs.

### Upgrading to AEM Communities 6.5 {#upgrading-to-aem-communities}

Lors de la mise à niveau vers les communautés AEM 6.5, si l’UGC préexistant doit être conservé, des étapes doivent être effectuées selon que la communauté AEM 5.6.1 ou AEM 6.0 utilise le stockage à la demande Adobe ou le stockage sur site de l’UGC.

Pour plus d’informations, consultez [Mise à niveau vers AEM Communities 6.5](/help/communities/upgrade.md).
