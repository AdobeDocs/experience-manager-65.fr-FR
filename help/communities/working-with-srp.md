---
title: 'SRP -  de contenu de la communauté '
seo-title: 'SRP -  de contenu de la communauté '
description: A compter de la version 6.1 des Communautés AEM, le contenu généré par l’utilisateur est stocké dans un seul magasin commun fourni par un fournisseur de ressources   (SRP).
seo-description: A compter de la version 6.1 des Communautés AEM, le contenu généré par l’utilisateur est stocké dans un seul magasin commun fourni par un fournisseur de ressources   (SRP).
uuid: d45e03c4-378b-4510-a6a0-d48c8cb879d9
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 6f13b21a-f4ef-4889-9b8e-4da3f846fa35
docset: aem65
translation-type: tm+mt
source-git-commit: 2bcd098ae901070d5e50cd89d06c854884b4e461

---


# SRP -  de contenu de la communauté {#srp-community-content-storage}

## Présentation {#introduction}

A compter de la version 6.1 des Communautés AEM, le contenu généré par l’utilisateur est stocké dans un magasin commun unique fourni par un fournisseur de ressources  (SRP). Il existe plusieurs options SRP à partir desquelles choisir, telles que ASRP, MSRP et JSRP.

Contrairement aux versions précédentes, il n’existe pas de réplication inverse/avancée de l’UGC dans les instances AEM. Au lieu de cela, le protocole SRP rend l’UGC directement accessible pour créer, lire, mettre à jour et supprimer des opérations CRUD de toutes les instances d’auteur et de publication, à l’exception de JSRP.

Voici les [caractéristiques de chaque option](#characteristics-of-srp-options)de PRS, qui est une information essentielle pour le processus décisionnel lors du choix du PRS approprié et du déploiement [](/help/communities/topologies.md)sous-jacent.

Pour plus d&#39;informations sur l&#39;utilisation de SRP pour l&#39;UGC, reportez-vous à la page Présentation [](/help/communities/srp.md)des des fournisseurs de ressources.

>[!NOTE]
>
>SRP s’applique uniquement au contenu de la communauté. Elle n’affecte pas l’emplacement de stockage du contenu du site (magasin[de](/help/sites-deploying/data-store-config.md)noeuds) et n’affecte pas la gestion sécurisée de l’enregistrement des utilisateurs, des  d’utilisateurs et des groupes d’utilisateurs entre les instances AEM (voir aussi [Gestion des données](#managing-user-data)utilisateur).


>[!CAUTION]
>
>Depuis AEM 6.1, [UGC n’est jamais répliqué](#ugc-never-replicated).
>
>Lorsque le déploiement n’inclut pas de magasin commun, tel que la topologie [JSRP](/help/communities/topologies.md#jsrp) par défaut, l’UGC n’est visible que sur l’instance de publication ou d’auteur AEM sur laquelle il a été saisi. L’UGC n’est visible sur aucune instance de publication que si la topologie inclut une grappe de publication.


## Caractéristiques des options SRP {#characteristics-of-srp-options}

[ASRP - Fournisseur de ressources Adobe](/help/communities/asrp.md)

Avec cette option, l’UGC est conservé à distance dans un service cloud hébergé et géré par Adobe. Il nécessite une licence supplémentaire et l’aide d’un gestionnaire de compte pour configurer le compte pour cette licence spécifique. ASRP requiert :

* Service cloud associé fourni et pris en charge par Adobe pour stocker le contenu de la communauté.
* Choix d’un centre de données dans une zone géographique spécifique (Etats-Unis, EMEA, APAC).

* Tous les accès programmatiques à l’UGC doivent être effectués via l’API SRP.

ASRP convient :

* Pour la batterie de publication TarMK.
* Quand il n&#39;y a pas d&#39;intention d&#39;investir dans les  locaux .

>[!NOTE]
>
>Le téléchargement de pièces jointes vers des publications (ou commentaires) dans ASRP est limité à 50 Mo.


[MSRP - MongoDB  fournisseur de ressources](/help/communities/msrp.md)

Avec cette option, l’UGC est conservé directement dans une instance MongoDB locale.

Le MSRP requiert :

* Installation locale sous licence de MongoDB pour stocker le contenu de la communauté.
* Une installation locale d&#39;Apache Solr.
* Tous les accès programmatiques à l’UGC doivent être effectués via l’API SRP.

ASRP convient :

* Pour une batterie de publication TarMK existante.
* Pour une grappe MongoMK ou RdbMK.
* Lorsque vous vous attendez à de gros volumes de contenu de la communauté.

[DSRP - Base de données relationnelle   fournisseur de ressources](/help/communities/dsrp.md)

Avec cette option, l’UGC est conservé directement dans une instance locale de base de données MySQL.

Le DSRP requiert :

* Installation locale de MySQL pour stocker le contenu de la communauté.
* Une installation locale d&#39;Apache Solr.
* Tous les accès programmatiques à l’UGC doivent être effectués via l’API SRP.

Le DSRP convient :

* Pour une batterie de publication TarMK existante.
* Pour une grappe MongoMK ou RdbMK.
* Lorsque vous vous attendez à de gros volumes de contenu de la communauté.

[JSRP - JCR  fournisseur de ressources](/help/communities/jsrp.md)

Avec l’option par défaut, il n’existe aucun magasin commun. L’UGC est conservé uniquement dans le même référentiel JCR que l’instance AEM dans laquelle il a été saisi.

JSRP:

* Stocke le contenu de la communauté dans le référentiel JCR de l’instance d’auteur ou de publication AEM à laquelle il a été publié.
* Nécessite que tous les accès programmatiques à l’UGC soient effectués via l’API SRP.
* Nécessite une grappe de publication si plusieurs instances de publication sont déployées (il n’existe aucun mécanisme de réplication parmi les instances de publication dans une batterie TarMK).
* la modération est exécutée uniquement dans le  de publication  (il n’existe aucun mécanisme de réplication inverse/transfert entre l’auteur et la publication).
* Il est préférable pour le développement, les démonstrations et la formation.

## Configuration de SRP {#configuring-srp}

La spécification de l’option de  de  par défaut, basée sur le déploiement sous-jacent, est effectuée via la console [Configuration de](/help/communities/srp-config.md).

Pour plus d’informations sur la configuration de chaque option, voir :

* [ASRP - Fournisseur de ressources Adobe](/help/communities/asrp.md)
* [MSRP - MongoDB  fournisseur de ressources](/help/communities/msrp.md)
* [DSRP - Base de données relationnelle   fournisseur de ressources](/help/communities/dsrp.md)
* [JSRP - JCR  fournisseur de ressources](/help/communities/jsrp.md)

Si aucune option   n’est activement sélectionnée, JSRP est activé par défaut.

## Informations supplémentaires {#additional-information}

### UGC jamais répliqué {#ugc-never-replicated}

Dans le de l’auteur  , un auteur crée le contenu de la page et le duplique dans le de publication . Lorsqu’une page comprend une fonctionnalité interactive des communautés AEM, telle que des commentaires, des révisions, un forum, un blog ou QnA, l’interaction des membres (connectés dans des de site) sur une instance de publication génère le contenu généré par l’utilisateur (UGC) saisi dans le  de publication .

Auparavant, ce contenu de la communauté était répliqué de manière inversée aux instances d’auteur et répliqué par l’auteur aux instances de publication. Il était problématique de maintenir la cohérence entre les instances AEM avec la réplication inverse et avancée.

À partir de la version 6.1 des Communautés AEM, le besoin de réplication de l’UGC a été éliminé grâce à l’utilisation d’un  partagé pour l’UGC, comme décrit ci-dessus.

Bien que le contenu du site soit répliqué, UGC n’est jamais répliqué.

### Gestion des données utilisateur {#managing-user-data}

Les [*utilisateurs *, les groupes d’* utilisateurs et les ***](/help/communities/users.md)utilisateurs présentent également un intérêt pour CommunitIes. Ces données utilisateur, lorsqu’elles sont créées et mises à jour dans le  de publication , doivent être mises à la disposition des autres instances de publication lorsque la topologie est une batterie de[publication](/help/sites-deploying/recommended-deploys.md#tarmk-farm).

Depuis la version 6.1 des communautés AEM, les données liées aux utilisateurs sont synchronisées à l’aide de la distribution Sling au lieu de la réplication. Pour plus d’informations, consultez Synchronisation [des](/help/communities/sync.md)utilisateurs.

### Upgrading to AEM Communities 6.5 {#upgrading-to-aem-communities}

Lors de la mise à niveau vers les communautés AEM 6.5, si l’UGC préexistant doit être conservé, des étapes doivent être effectuées selon que la communauté AEM 5.6.1 ou AEM 6.0 a utilisé les  à la demande Adobe   ou les  sur site de l’UGC.

Pour plus d’informations, consultez [Mise à niveau vers AEM Communities 6.5](/help/communities/upgrade.md).
