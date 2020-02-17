---
title: DSRP - Fournisseur de ressources de stockage de base de données relationnel
seo-title: DSRP - Fournisseur de ressources de stockage de base de données relationnel
description: Configuration des communautés AEM pour utiliser une base de données relationnelle comme magasin commun
seo-description: Configuration des communautés AEM pour utiliser une base de données relationnelle comme magasin commun
uuid: f364e7da-ee54-4ab2-a630-7ec9239005ac
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: d23acb18-6761-4290-9e7a-a434582791bd
translation-type: tm+mt
source-git-commit: b7c790681034e9950aa43738310f7af8b1dd0085

---


# DSRP - Fournisseur de ressources de stockage de base de données relationnel {#dsrp-relational-database-storage-resource-provider}

## A propos de DSRP {#about-dsrp}

Lorsque les communautés AEM sont configurées pour utiliser une base de données relationnelle comme magasin commun, le contenu généré par l’utilisateur (UGC) est accessible à partir de toutes les instances d’auteur et de publication sans avoir besoin de synchronisation ni de réplication.

Voir aussi [Caractéristiques des options](working-with-srp.md#characteristics-of-srp-options) SRP et Topologies [](topologies.md)recommandées.

## Conditions requises {#requirements}

* [MySQL](#mysql-configuration), une base de données relationnelle
* [Apache Solr](#solr-configuration), une plateforme de recherche

>[!NOTE]
>
>La configuration de stockage par défaut est maintenant stockée dans conf path(`/conf/global/settings/community/srpc/defaultconfiguration`) au lieu de etc path (`/etc/socialconfig/srpc/defaultconfiguration`). Nous vous conseillons de suivre les étapes [de](#zerodt-migration-steps) migration pour que la variable defaultsrp fonctionne comme prévu.


## Configuration de la base de données relationnelle {#relational-database-configuration}

### Configuration MySQL {#mysql-configuration}

Une installation MySQL peut être partagée entre les fonctionnalités d’activation et le magasin commun (DSRP) dans le même pool de connexions en utilisant des noms de base de données (schéma) différents et des connexions différentes (serveur:port).

Pour plus d’informations sur l’installation et la configuration, voir Configuration [MySQL pour DSRP](dsrp-mysql.md).

### Configuration de Solr {#solr-configuration}

Une installation Solr peut être partagée entre le magasin de noeuds (Oak) et le magasin commun (SRP) en utilisant différentes collections.

Si les collections Oak et SRP sont utilisées de manière intensive, un second Solr peut être installé pour des raisons de performances.

Pour les environnements de production, le mode SolrCloud offre des performances améliorées par rapport au mode autonome (une configuration Solr locale unique).

Pour plus d’informations sur l’installation et la configuration, voir Configuration [Solr pour SRP](solr.md).

### Sélectionner DSRP {#select-dsrp}

La console [Configuration du](srp-config.md) stockage permet de sélectionner la configuration de stockage par défaut, qui identifie l&#39;implémentation de SRP à utiliser.

A l’auteur, pour accéder à la console Configuration du stockage

* Connexion avec droits d’administrateur
* Dans le menu **principal**

   * Sélectionnez **[!UICONTROL Outils]** (dans le volet de gauche).
   * Sélectionner **[!UICONTROL des communautés]**
   * Sélectionner la configuration **[!UICONTROL de stockage]**

      * Par exemple, l’emplacement obtenu est : [http://localhost:4502/communities/admin/defaultsrp](http://localhost:4502/communities/admin/defaultsrp)
      >[!NOTE]
      >
      >La configuration de stockage par défaut est maintenant stockée dans conf path(`/conf/global/settings/community/srpc/defaultconfiguration`) au lieu de etc path (`/etc/socialconfig/srpc/defaultconfiguration`). Nous vous conseillons de suivre les étapes [de](#zerodt-migration-steps) migration pour que la variable defaultsrp fonctionne comme prévu.

![chlimage_1-128](assets/chlimage_1-128.png)

* Select **[!UICONTROL Database Storage Resource Provider (DSRP)]**
* **Configuration de la base de données**

   * **[!UICONTROL Nom de la source de données JDBC]**

      Le nom donné à la connexion MySQL doit être identique à celui entré dans la configuration OSGi [JDBC.](dsrp-mysql.md#configurejdbcconnections)

      *default*: communautés

   * **[!UICONTROL le nom de la base de données ;]**

      Nom donné au schéma dans le script [init_schema.sql](dsrp-mysql.md#obtain-the-sql-script)

      *default*: communautés

* **SolrConfiguration**

   * **[](https://cwiki.apache.org/confluence/display/solr/Using+ZooKeeper+to+Manage+Configuration+Files)Hôte Zookeeper **

      Laissez cette valeur vide si vous exécutez Solr à l’aide de ZooKeeper interne. Sinon, lors de l’exécution en mode [](solr.md#solrcloud-mode) SolrCloud avec un ZooKeeper externe, définissez cette valeur sur l’URI du ZooKeeper, par exemple *my.server.com:80.*

      *default*: *&lt;blank>*

   * **[!UICONTROL URL de Solr]**

      *default*: https://127.0.0.1:8983/solr/

   * **[!UICONTROL Collection Solr]**

      *default*: collection1

* Sélectionnez **[!UICONTROL Envoyer]**.

### Etapes de migration sans temps d’arrêt pour les valeurs par défaut {#zerodt-migration-steps}

Pour vous assurer que la page par défaut [http://localhost:4502/communities/admin/defaultsrp](http://localhost:4502/communities/admin/defaultsrp) fonctionne comme prévu :

1. Renommez le chemin d’accès `/etc/socialconfig` à `/etc/socialconfig_old`, de sorte que la configuration du système revienne à jsrp(par défaut).
1. Accédez à la page par défaut [http://localhost:4502/communities/admin/defaultsrp](http://localhost:4502/communities/admin/defaultsrp), où jsrp est configuré. Cliquez sur le bouton **[!UICONTROL Envoyer]** pour créer un nouveau noeud de configuration par défaut `/conf/global/settings/community/srpc`.
1. Supprimez la configuration par défaut créée `/conf/global/settings/community/srpc/defaultconfiguration`.
1. Copiez l’ancienne configuration `/etc/socialconfig_old/srpc/defaultconfiguration` à la place du noeud supprimé (`/conf/global/settings/community/srpc/defaultconfiguration`) à l’étape précédente.
1. Supprimez l’ancien noeud etc `/etc/socialconfig_old`.

## Publication de la configuration {#publishing-the-configuration}

DSRP doit être identifié comme le magasin commun sur toutes les instances d’auteur et de publication.

Pour rendre la configuration identique disponible dans l’environnement de publication :

* Sur l&#39;auteur :

   * Accédez au menu principal à **[!UICONTROL Outils > Opérations > Réplication.]**
   * Double-cliquez sur **Activer l’arborescence **
   * **Chemin de début:**

      * Naviguer jusqu’à `/etc/socialconfig/srpc/`
   * Vérifier que `Only Modified` n’est pas sélectionné.
   * Sélectionner **[!UICONTROL Activer]**


## Gestion des données utilisateur {#managing-user-data}

Pour plus d’informations sur les *utilisateurs*, les profils ** utilisateur et les groupes *d’* utilisateurs, souvent entrés dans l’environnement de publication, consultez la page

* [Synchronisation des utilisateurs](sync.md)
* [Gestion des utilisateurs et des groupes d’utilisateurs](users.md)

## Réindexation Solr pour DSRP {#reindexing-solr-for-dsrp}

Pour réindexer DSRP Solr, suivez la documentation relative à la [réindexation MSRP](msrp.md#msrp-reindex-tool). Toutefois, lors de la réindexation pour DSRP, utilisez plutôt cette URL : **/services/social/datastore/rdb/reindex**

Par exemple, une commande curl pour réindexer DSRP se présenterait comme suit :

```shell
curl -u admin:password -X POST -F path=/ https://host:port/services/social/datastore/rdb/reindex
```

