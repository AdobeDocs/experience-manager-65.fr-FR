---
title: DSRP - Fournisseur de ressources d'Enregistrement de données relationnelles
seo-title: DSRP - Fournisseur de ressources d'Enregistrement de données relationnelles
description: Configurer AEM Communities pour utiliser une base de données relationnelle comme magasin commun
seo-description: Configurer AEM Communities pour utiliser une base de données relationnelle comme magasin commun
uuid: f364e7da-ee54-4ab2-a630-7ec9239005ac
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: d23acb18-6761-4290-9e7a-a434582791bd
translation-type: tm+mt
source-git-commit: f375b40c084ee363757b78c602091f38524b8b03
workflow-type: tm+mt
source-wordcount: '648'
ht-degree: 3%

---


# DSRP - Fournisseur de ressources d&#39;Enregistrement de données relationnelles {#dsrp-relational-database-storage-resource-provider}

## A propos de DSRP {#about-dsrp}

Lorsque AEM Communities est configuré pour utiliser une base de données relationnelle en tant que magasin commun, le contenu généré par l’utilisateur est accessible à partir de toutes les instances d’auteur et de publication sans avoir besoin de synchronisation ni de réplication.

Voir aussi [Caractéristiques des options](working-with-srp.md#characteristics-of-srp-options) SRP et Topologies [](topologies.md)recommandées.

## Conditions requises {#requirements}

* [MySQL](#mysql-configuration), une base de données relationnelle.
* [Apache Solr](#solr-configuration), une plateforme de recherche.

>[!NOTE]
>
>La configuration par défaut de l&#39;enregistrement est maintenant stockée dans conf path(`/conf/global/settings/community/srpc/defaultconfiguration`) au lieu de etc path (`/etc/socialconfig/srpc/defaultconfiguration`). Il est conseillé de suivre les étapes [de](#zerodt-migration-steps) migration pour que les paramètres par défaut fonctionnent comme prévu.

## Configuration de la base de données relationnelle {#relational-database-configuration}

### Configuration MySQL {#mysql-configuration}

Une installation MySQL peut être partagée entre les fonctions d&#39;activation et le magasin commun (DSRP) dans le même pool de connexions en utilisant des noms de base de données (schéma) différents et aussi des connexions différentes (serveur:port).

Pour plus d’informations sur l’installation et la configuration, voir Configuration [MySQL pour DSRP](dsrp-mysql.md).

### Configuration de Solr {#solr-configuration}

Une installation Solr peut être partagée entre le magasin de noeuds (Oak) et le magasin commun (SRP) en utilisant différentes collections.

Si les deux collections Oak et SRP sont utilisées de façon intensive, un second Solr peut être installé pour des raisons de performances.

Pour les environnements de production, le mode SolrCloud offre de meilleures performances par rapport au mode autonome (une seule configuration Solr locale).

Pour plus d’informations sur l’installation et la configuration, voir Configuration [Solr pour SRP](solr.md).

### Sélectionner DSRP {#select-dsrp}

La console [Configuration de l&#39;](srp-config.md) Enregistrement permet de sélectionner la configuration d&#39;enregistrement par défaut, qui identifie l&#39;implémentation de SRP à utiliser.

Sur l’auteur, pour accéder à la console de configuration de l’Enregistrement

* Connexion avec droits d’administrateur
* Dans le menu **principal**

   * Sélectionnez **[!UICONTROL Outils]** (dans le volet de gauche).
   * Sélectionner **[!UICONTROL des communautés]**
   * Sélectionner la configuration **[!UICONTROL d&#39;Enregistrement]**

      * Par exemple, l’emplacement obtenu est : [http://localhost:4502/communities/admin/defaultsrp](http://localhost:4502/communities/admin/defaultsrp)
      >[!NOTE]
      >
      >La configuration par défaut de l&#39;enregistrement est maintenant stockée dans conf path(`/conf/global/settings/community/srpc/defaultconfiguration`) au lieu de etc path (`/etc/socialconfig/srpc/defaultconfiguration`). Il est conseillé de suivre les étapes [de](#zerodt-migration-steps) migration pour que les paramètres par défaut fonctionnent comme prévu.
   ![dsrp-config](assets/dsrp-config.png)

* Select **[!UICONTROL Database Storage Resource Provider (DSRP)]**
* **Configuration de la base de données**

   * **[!UICONTROL Nom de la source de données JDBC]**

      Le nom donné à la connexion MySQL doit être identique à celui entré dans la configuration [JDBC OSGi.](dsrp-mysql.md#configurejdbcconnections)

      *par défaut*: communautés

   * **[!UICONTROL le nom de la base de données ;]**

      Nom donné au schéma dans [le script init_schéma.sql](dsrp-mysql.md#obtain-the-sql-script)

      *par défaut*: communautés

* **SolrConfiguration**

   * **[](https://cwiki.apache.org/confluence/display/solr/Using+ZooKeeper+to+Manage+Configuration+Files)Hôte Zookeeper**

      Laissez cette valeur vide si Solr est exécuté à l’aide du ZooKeeper interne. Sinon, lorsque vous exécutez en mode [](solr.md#solrcloud-mode) SolrCloud avec un ZooKeeper externe, définissez cette valeur sur l’URI du ZooKeeper, par exemple *my.server.com:80.*

      *par défaut*: *&lt;blank>*

   * **[!UICONTROL URL de Solr]**

      *par défaut*: https://127.0.0.1:8983/solr/

   * **[!UICONTROL Collection Solr]**

      *par défaut*: collection1

* Sélectionnez **[!UICONTROL Envoyer]**.

### Étapes de migration sans interruption de service pour le rtp par défaut {#zerodt-migration-steps}

Pour vous assurer que la page http://localhost:4502/communities/admin/defaultsrp [](http://localhost:4502/communities/admin/defaultsrp) fonctionne comme prévu par défaut, procédez comme suit :

1. Renommez le chemin d’accès `/etc/socialconfig` à `/etc/socialconfig_old`, de sorte que la configuration du système revienne à jsrp(par défaut).
1. Accédez à la page par défaut [http://localhost:4502/communities/admin/defaultsrp](http://localhost:4502/communities/admin/defaultsrp), où jsrp est configuré. Cliquez sur le bouton **[!UICONTROL Envoyer]** pour créer un nouveau noeud de configuration par défaut `/conf/global/settings/community/srpc`.
1. Supprimez la configuration par défaut créée `/conf/global/settings/community/srpc/defaultconfiguration`.
1. Copiez l’ancienne configuration `/etc/socialconfig_old/srpc/defaultconfiguration` à la place du noeud supprimé (`/conf/global/settings/community/srpc/defaultconfiguration`) à l’étape précédente.
1. Supprimez l’ancien noeud etc `/etc/socialconfig_old`.

## Publication de la configuration {#publishing-the-configuration}

DSRP doit être identifié comme le magasin commun sur toutes les instances d’auteur et de publication.

Pour rendre la configuration identique disponible dans l’environnement de publication :

* Sur l&#39;auteur :

   * Accédez au menu principal à **[!UICONTROL Outils]** > **[!UICONTROL Opérations]** > **[!UICONTROL Réplication.]**
   * Double-cliquez sur **[!UICONTROL Activer l’arborescence]**
   * **Chemin de début**:

      * Naviguer jusqu’à `/etc/socialconfig/srpc/`
   * Assurez-vous que `Only Modified` l’option n’est pas sélectionnée.
   * Sélectionnez **[!UICONTROL Activer]**.


## Gestion des données utilisateur {#managing-user-data}

Pour plus d’informations sur *les utilisateurs*, les profils ** utilisateur et les groupes *d’* utilisateurs, souvent saisis dans l’environnement de publication, consultez la page :

* [Synchronisation des utilisateurs](sync.md)
* [Gestion des utilisateurs et des groupes d’utilisateurs](users.md)

## Réindexation du Solr pour DSRP {#reindexing-solr-for-dsrp}

Pour réindexer DSRP Solr, suivez la documentation relative à la [réindexation du MSRP](msrp.md#msrp-reindex-tool). Cependant, lors de la réindexation pour le DSRP, utilisez plutôt cette URL : **/services/social/datastore/rdb/reindex**

Par exemple, une commande curl pour réindexer DSRP ressemblerait à ceci :

```shell
curl -u admin:password -X POST -F path=/ https://host:port/services/social/datastore/rdb/reindex
```

