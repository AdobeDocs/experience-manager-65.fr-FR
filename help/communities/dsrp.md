---
title: DSRP - Fournisseur de ressources de stockage de la base de données relationnelle
description: Configurer AEM Communities pour utiliser une base de données relationnelle comme magasin commun
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
role: Admin
exl-id: 15b3a594-efde-4702-9233-232ba1c7e5b0
source-git-commit: f0dd1ac3ab9c17a8b331f5048d84ec97dd23924f
workflow-type: tm+mt
source-wordcount: '617'
ht-degree: 3%

---

# DSRP - Fournisseur de ressources de stockage de la base de données relationnelle {#dsrp-relational-database-storage-resource-provider}

## À propos de DSRP {#about-dsrp}

Lorsqu’AEM Communities est configuré pour utiliser une base de données relationnelle comme magasin commun, le contenu généré par l’utilisateur est accessible à partir de toutes les instances d’auteur et de publication sans avoir besoin de synchronisation ni de réplication.

Voir aussi [Caractéristiques des options SRP](working-with-srp.md#characteristics-of-srp-options) et [Topologies recommandées](topologies.md).

## Conditions requises {#requirements}

* [MySQL](#mysql-configuration), une base de données relationnelle.
* [Apache Solr](#solr-configuration), une plateforme de recherche.

>[!NOTE]
>
>La configuration de stockage par défaut est désormais stockée dans conf path(`/conf/global/settings/community/srpc/defaultconfiguration`) au lieu de `etc` path (`/etc/socialconfig/srpc/defaultconfiguration`). Il est conseillé de suivre le [étapes de migration](#zerodt-migration-steps) pour que les valeurs par défaut fonctionnent comme prévu.

## Configuration de la base de données relationnelle {#relational-database-configuration}

### Configuration MySQL {#mysql-configuration}

Une installation MySQL peut être partagée entre les fonctionnalités d&#39;activation et le magasin commun (DSRP) au sein d&#39;un même pool de connexions en utilisant des noms de base de données (schéma) différents et également des connexions différentes (server:port).

Pour plus d’informations sur l’installation et la configuration, voir [Configuration MySQL pour DSRP](dsrp-mysql.md).

### Configuration de Solr {#solr-configuration}

Une installation Solr peut être partagée entre le magasin de noeuds (Oak) et le magasin commun (SRP) à l’aide de différentes collections.

Si les collections Oak et SRP sont utilisées de manière intensive, un second Solr peut être installé pour des raisons de performances.

Pour les environnements de production, le mode SolrCloud offre de meilleures performances par rapport au mode autonome (une seule configuration Solr locale).

Pour plus d’informations sur l’installation et la configuration, voir [Configuration Solr pour SRP](solr.md).

### Sélectionner DSRP {#select-dsrp}

La variable [Console de configuration de stockage](srp-config.md) permet de sélectionner la configuration de stockage par défaut, qui identifie l’implémentation de la SRP à utiliser.

À l’auteur, pour accéder à la console Configuration de stockage

* Connexion avec droits d’administrateur
* Dans la **menu principal**

   * Sélectionner **[!UICONTROL Outils]** (dans le volet de gauche)
   * Sélectionner **[!UICONTROL Communautés]**
   * Sélectionner **[!UICONTROL Configuration de stockage]**

      * Par exemple, l’emplacement obtenu est le suivant : [http://localhost:4502/communities/admin/defaultsrp](http://localhost:4502/communities/admin/defaultsrp)

     >[!NOTE]
     >
     >La configuration de stockage par défaut est désormais stockée dans conf path(`/conf/global/settings/community/srpc/defaultconfiguration`) au lieu de `etc` path (`/etc/socialconfig/srpc/defaultconfiguration`). Il est conseillé de suivre le [étapes de migration](#zerodt-migration-steps) pour que les valeurs par défaut fonctionnent comme prévu.

  ![dsrp-config](assets/dsrp-config.png)

* Sélectionner **[!UICONTROL Fournisseur de ressources de stockage de base de données (DSRP)]**
* **Configuration de la base de données**

   * **[!UICONTROL Nom de la source de données JDBC]**

     Le nom donné à la connexion MySQL doit être identique à celui saisi dans [Configuration OSGi JDBC](dsrp-mysql.md#configurejdbcconnections)

     *default*: communautés

   * **[!UICONTROL Nom de la base de données]**

     Nom donné au schéma dans [init_schema.sql](dsrp-mysql.md#obtain-the-sql-script) script

     *default*: communautés

* **SolrConfiguration**

   * **[](https://solr.apache.org/guide/6_6/using-zookeeper-to-manage-configuration-files.html)Hôte Zookeeper**

     Laissez cette valeur vide si vous exécutez Solr à l’aide du ZooKeeper interne. Sinon, lorsque vous exécutez [Mode SolrCloud](solr.md#solrcloud-mode) avec un ZooKeeper externe, définissez cette valeur sur l’URI du ZooKeeper, comme *my.server.com:80*

     *default*: *&lt;blank>*

   * **[!UICONTROL URL de Solr]**

     *default*: https://127.0.0.1:8983/solr/

   * **[!UICONTROL Collection Solr]**

     *default*: collection1

* Sélectionnez **[!UICONTROL Envoyer]**.

### Pas de temps d’arrêt pour la migration des valeurs par défaut {#zerodt-migration-steps}

Pour vous assurer que la page par défaut s’affiche [http://localhost:4502/communities/admin/defaultsrp](http://localhost:4502/communities/admin/defaultsrp) fonctionne comme prévu, procédez comme suit :

1. Renommez le chemin à l’emplacement suivant : `/etc/socialconfig` to `/etc/socialconfig_old`, de sorte que la configuration du système revienne à jsrp (par défaut).
1. Accéder à la page default [http://localhost:4502/communities/admin/defaultsrp](http://localhost:4502/communities/admin/defaultsrp), où jsrp est configuré. Cliquez sur le bouton **[!UICONTROL submit]** afin que le nouveau noeud de configuration par défaut soit créé à l’adresse `/conf/global/settings/community/srpc`.
1. Suppression de la configuration par défaut créée `/conf/global/settings/community/srpc/defaultconfiguration`.
1. Copie de l’ancienne configuration `/etc/socialconfig_old/srpc/defaultconfiguration` à la place du noeud supprimé (`/conf/global/settings/community/srpc/defaultconfiguration`) à l’étape précédente.
1. Supprimer l’ancien `etc` node `/etc/socialconfig_old`.

## Publication de la configuration {#publishing-the-configuration}

DSRP doit être identifié comme le magasin commun sur toutes les instances d’auteur et de publication.

Pour rendre la configuration identique disponible dans l’environnement de publication :

* Sur l’auteur :

   * Accédez au **[!UICONTROL Outils]** > **[!UICONTROL Opérations]** > **[!UICONTROL Réplication]**
   * Double-cliquez **[!UICONTROL Activer l’arborescence]**
   * **Chemin de début**:

      * Accédez à `/etc/socialconfig/srpc/`

   * Assurez-vous que `Only Modified` n’est pas sélectionnée.
   * Sélectionner **[!UICONTROL Activer]**.

## Gestion des données utilisateur {#managing-user-data}

Pour plus d’informations sur *utilisateurs*, *profils utilisateur* et *groupes d’utilisateurs*, souvent entrées dans l’environnement de publication, consultez :

* [Synchronisation des utilisateurs](sync.md)
* [Gestion des utilisateurs et des groupes d’utilisateurs](users.md)

## Réindexation Solr pour DSRP {#reindexing-solr-for-dsrp}

Pour réindexer DSRP Solr, suivez la documentation de [réindexation MSRP](msrp.md#msrp-reindex-tool), toutefois, lors de la réindexation pour DSRP, utilisez plutôt cette URL : **/services/social/datastore/rdb/reindex**

Par exemple, une commande curl pour réindexer DSRP ressemblerait à ceci :

```shell
curl -u admin:password -X POST -F path=/ https://host:port/services/social/datastore/rdb/reindex
```
