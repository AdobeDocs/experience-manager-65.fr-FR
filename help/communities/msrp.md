---
title: 'MSRP - MongoDB  fournisseur de ressources '
seo-title: 'MSRP - MongoDB  fournisseur de ressources '
description: Configuration des communautés AEM pour utiliser une base de données relationnelle comme magasin commun
seo-description: Configuration des communautés AEM pour utiliser une base de données relationnelle comme magasin commun
uuid: 9fc06d4f-a60f-4ce3-8586-bcc836aa7de6
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 048f7b30-20c3-4567-bd32-38cf2643cf39
translation-type: tm+mt
source-git-commit: f7e5afe46100db7837647ac89aaf58cf101143b0

---


# MSRP - MongoDB  fournisseur de ressources {#msrp-mongodb-storage-resource-provider}

## A propos de MSRP {#about-msrp}

Lorsque les communautés AEM sont configurées pour utiliser MSRP comme magasin commun, le contenu généré par l’utilisateur (UGC) est accessible à partir de toutes les instances d’auteur et de publication sans avoir besoin de synchronisation ni de réplication.

Voir aussi [Caractéristiques des options](working-with-srp.md#characteristics-of-srp-options) SRP et Topologies [](topologies.md)recommandées.

## Conditions requises {#requirements}

* [MongoDB](https://www.mongodb.org/):

   * Version 2.6 ou ultérieure
   * Pas besoin de configurer les mongos ou le partage
   * Recommandez vivement l&#39;utilisation d&#39;un jeu de [réplicas](#mongoreplicaset)
   * Peut s’exécuter sur le même hôte qu’AEM ou à distance

* [Apache Solr](https://lucene.apache.org/solr/):

   * Version 4.10 ou version 5
   * Le solaire requiert Java 1.7 ou version ultérieure
   * Aucun service requis
   * Choix des modes d’exécution :
      * Mode autonome
      * [Mode](solr.md#solrcloud-mode) SolrCloud (recommandé pour les  de production )
   * Choix de la recherche multilingue (MLS)
      * [Installation de Standard MLS](solr.md#installing-standard-mls)
      * [Installation de MLS avancé](solr.md#installing-advanced-mls)

## MongoDB Configuration {#mongodb-configuration}

### Sélectionner MSRP {#select-msrp}

La console [de configuration de  de](srp-config.md) permet de sélectionner la configuration de par défaut, qui identifie l&#39;implémentation de SRP à utiliser.

Sur l’auteur, pour accéder à la console de configuration  du  :

* Dans la navigation globale, sélectionnez **[!UICONTROL Outils]** > **[!UICONTROL Communautés]** > **[!UICONTROL configuration]**.

![chlimage_1-28](assets/chlimage_1-28.png)

* Select **[!UICONTROL MongoDB Storage Resource Provider (MSRP)]**
* **[!UICONTROL Configuration de mongoDB]**

   * **[!UICONTROL URI de mongoDB]**

      *default*: mongodb://localhost/?maxPoolSize=10&amp;waitQueueMultiple=5&amp;readPreference=secondaryPreferred

   * **[!UICONTROL Base de données mongoDB]**

      *default*: communautés

   * **[!UICONTROL Collection UGC mongoDB]**

      *default*: contenu

   * **[!UICONTROL Collection de pièces jointes mongoDB]**

      *default*: pièces jointes

* **[!UICONTROL SolrConfiguration]**

   * **[](https://cwiki.apache.org/confluence/display/solr/Using+ZooKeeper+to+Manage+Configuration+Files)Hôte Zookeeper **

      Lors de l’exécution en mode [](solr.md#solrcloud-mode) SolrCloud avec un ZooKeeper externe, définissez cette valeur sur `HOST:PORT` pour le ZooKeeper, par exemple *my.server.com:2181.*

      Pour un ensemble ZooKeeper, saisissez `HOST:PORT` des valeurs séparées par des virgules, telles que *host1:2181,host2:2181.*

      Laissez ce champ vide si vous exécutez Solr en mode autonome à l’aide de ZooKeeper interne.
      *Valeur par défaut*: *&lt;blank>*

      * **[!UICONTROL URL]**solaire URL utilisée pour communiquer avec Solr en mode autonome.
Laissez ce champ vide si vous êtes en mode SolrCloud.
         *Valeur par défaut*: https://127.0.0.1:8983/solr/

      * **[!UICONTROL Collection]**Solr Nom de la collection Solr.
         *Valeur par défaut*: collection1

* Sélectionnez **[!UICONTROL Envoyer]**

>[!NOTE]
>
>La base de données mongoDB, qui prend par défaut le nom `communities`, ne doit pas être définie sur le nom d’une base de données utilisée pour les magasins de [noeuds ou les magasins](../../help/sites-deploying/data-store-config.md)de données (binaires). Reportez-vous également à la page [Eléments  dans AEM 6.5](../../help/sites-deploying/storage-elements-in-aem-6.md).


### Jeu de réplicas MongoDB {#mongodb-replica-set}

Pour le  de production , il est vivement recommandé de configurer un jeu de réplicas, un cluster de serveurs MongoDB qui implémente la réplication maître-esclave et le basculement automatisé.

Pour en savoir plus sur les jeux de réplicas, consultez la documentation de [réplication](https://docs.mongodb.org/manual/replication/) de MongoDB.

Pour travailler avec des jeux de réplicas et apprendre à définir des connexions entre des applications et des instances MongoDB, consultez la documentation [Connection String URI Format](https://docs.mongodb.org/manual/reference/connection-string/) .

#### Exemple d’URL pour la connexion à un jeu de réplicas {#example-url-for-connecting-to-a-replica-set}

```shell
# Example url for:
# servers "mongoserver1", "mongoserver2", "mongoserver3"
# replica set 'rs0'
# port numbers only necessary if not default port 27017
mongodb://mongoserver1:<mongoport1>,mongoserver2:<mongoport2>,mongoserver3:<mongoport3>/?replicaSet=rs0&maxPoolSize=100&waitQueueMultiple=50&readPreference=secondaryPreferred
```

## Configuration de Solr {#solr-configuration}

Une installation Solr peut être partagée entre le magasin de noeuds (Oak) et le magasin commun (MSRP) à l’aide de différentes collections.

Si les collections Oak et MSRP sont utilisées de manière intensive, un second Solr peut être installé pour des raisons de performances.

Pour les  de production , le mode [](solr.md#solrcloud-mode) SolrCloud offre des performances améliorées par rapport au mode autonome (une configuration Solr locale unique).

Pour plus d’informations sur la configuration, voir Configuration [Solr pour SRP](solr.md).

### Mise à niveau {#upgrading}

Si une mise à niveau à partir d’une version antérieure configurée avec MSRP, vous devez effectuer les opérations suivantes :

1. Effectuer la [mise à niveau vers les communautés AEM](upgrade.md)
1. Installation de nouveaux fichiers de configuration Solr
   * Pour MLS [standard](solr.md#installing-standard-mls)
   * Pour les MLS [avancés](solr.md#installing-advanced-mls)
1. Réindexer l&#39;outil de réindexation [MSRP de la section MSRP](#msrp-reindex-tool)

## Publication de la configuration {#publishing-the-configuration}

MSRP doit être identifié comme le magasin commun sur toutes les instances d’auteur et de publication.

Pour rendre la configuration identique disponible dans le  de publication , connectez-vous à votre instance d’auteur et procédez comme suit :

* Dans le menu principal, sélectionnez **[!UICONTROL Outils]** > **[!UICONTROL Opérations]** > **[!UICONTROL Réplication]**.
* Sélectionner **[!UICONTROL Activer l&#39;arborescence]**
* **[!UICONTROL Chemin de début]**:
   * Naviguer jusqu’à `/etc/socialconfig/srpc/`
* Sélectionner **[!UICONTROL Activer]**

## Gestion des données utilisateur {#managing-user-data}

Pour plus d’informations sur les *utilisateurs*, les *des* utilisateurs et les groupes *d’* utilisateurs, souvent saisis dans le  de publication, consultez la page

* [Synchronisation des utilisateurs](sync.md)
* [Gestion des utilisateurs et des groupes d’utilisateurs](users.md)

## Outil Réindexation MSRP {#msrp-reindex-tool}

Il existe un point de terminaison HTTP pour la réindexation de Solr pour MSRP lors de l’installation de nouveaux fichiers de configuration ou de la réparation d’un index Solr endommagé.

Avec cet outil, MongoDB est la source de *vérité* pour MSRP ; les sauvegardes ne doivent être effectuées que sur MongoDB.

L&#39;arborescence UGC entière peut être réindexée, ou seulement une sous-arborescence spécifique, comme spécifié par le paramètre *path *data.

Cet outil peut être exécuté à partir de la ligne de commande à l’aide de cURL ou de tout autre outil HTTP.

Lors de la réindexation, il existe un compromis entre la mémoire et les performances contrôlées par le paramètre de données *batchSize *qui spécifie le nombre d’enregistrements UGC réindexés par lot.

Une valeur par défaut raisonnable est 5000 :

* Si la mémoire est un problème, spécifiez un nombre plus petit.
* Si la vitesse est un problème, spécifiez un nombre plus élevé pour augmenter la vitesse.

### Exécution de l’outil de réindexation MSRP à l’aide de la commande cURL {#running-msrp-reindex-tool-using-curl-command}

La commande cURL suivante montre ce qui est nécessaire pour qu’une requête HTTP puisse réindexer l’UGC stockée dans MSRP.

Le format de base est le suivant :

cURL -u *connexion* -d *données* *reindex-url*

*signature* = administrator-id:passwordPar exemple : admin:admin

*data* = &quot;batchSize=*size*&amp;path=*path&quot;*

*size* = nombre d’entrées UGC à réindexer par opération`/content/usergenerated/asi/mongo/`

*chemin* = emplacement racine de l’arborescence de l’UGC à réindexer

* Pour réindexer tout UGC, spécifiez la valeur de la `asipath`propriété de
   `/etc/socialconfig/srpc/defaultconfiguration`
* Pour limiter l’index à un élément UGC, spécifiez une sous-arborescence de `asipath`

*reindex-url* = point de terminaison de la réindexation de SRP`http://localhost:4503/services/social/datastore/mongo/reindex`

>[!NOTE]
>
>Si vous [réindexez DSRP Solr](dsrp.md), l’URL est **/services/social/datastore/rdb/reindex.**


### Exemple de réindexation MSRP {#msrp-reindex-example}

```shell
curl -s -u admin:admin -d 'batchSize=10000&path=/content/usergenerated/asi/mongo/' http://localhost:4503/services/social/datastore/mongo/reindex
```

## Démonstration du protocole MSRP {#how-to-demo-msrp}

Pour configurer MSRP pour une démonstration ou un  de développement , reportez-vous à la section [Procédure de configuration de MongoDB pour la démonstration](demo-mongo.md).

## Résolution des incidents {#troubleshooting}

### UGC invisible dans MongoDB {#ugc-not-visible-in-mongodb}

Assurez-vous que MSRP a été configuré comme fournisseur par défaut en vérifiant la configuration de l’option de  de . Par défaut, le fournisseur de ressources   est JSRP.

Sur toutes les instances d’AEM de création et de publication, consultez de nouveau la console [](srp-config.md) de configuration  ou vérifiez le référentiel AEM :

* Dans JCR, if [/etc/socialconfig](http://localhost:4502/crx/de/index.jsp#/etc/socialconfig/)

   * Ne contient pas de noeud [srpc](http://localhost:4502/crx/de/index.jsp#/etc/socialconfig/srpc) , cela signifie que le fournisseur de  de  est JSRP.
   * Si le noeud srpc existe et contient la configuration [par](http://localhost:4502/crx/de/index.jsp#/etc/socialconfig/srpc/defaultconfiguration)défaut du noeud, les propriétés de la configuration par défaut doivent définir MSRP comme fournisseur par défaut.

### UGC disparaît après la mise à niveau {#ugc-disappears-after-upgrade}

Si une mise à niveau à partir d’un site AEM Communities 6.0 existant, tout fichier UGC préexistant doit être converti en fonction de la structure requise pour l’API [SRP](srp.md) après la mise à niveau vers AEM Communities 6.3.

Un outil open source est disponible sur GitHub à cette fin :

* [Outil de migration UGC des communautés AEM](https://github.com/Adobe-Marketing-Cloud/communities-ugc-migration)

L’outil de migration peut être personnalisé pour exporter l’UGC des versions antérieures des communautés sociales AEM en vue de l’importer dans les communautés AEM 6.1 ou une version ultérieure.

### Erreur - champ non défini provider_id {#error-undefined-field-provider-id}

Si l’erreur suivante est affichée dans les journaux, cela indique que le fichier  Solr n’est pas correctement configuré.

#### JsonMappingException : provider_id de champ non défini {#jsonmappingexception-undefined-field-provider-id}

```xml
Caused by: com.fasterxml.jackson.databind.JsonMappingException: undefined field provider_id
at com.fasterxml.jackson.databind.ser.DefaultSerializerProvider.serializeValue(DefaultSerializerProvider.java:129)
at com.fasterxml.jackson.databind.ObjectMapper.writeValue(ObjectMapper.java:1819)
at com.adobe.cq.social.scf.core.BaseSocialComponent.toJSONString(BaseSocialComponent.java:196)
... 124 common frames omitted
```

Pour résoudre l’erreur, suivez les instructions d’ [installation de Standard MLS](solr.md#installing-standard-mls)et assurez-vous que :

* Les fichiers de configuration XML ont été copiés à l’emplacement Solr approprié.
* Solr a été redémarré après que les nouveaux fichiers de configuration ont remplacé les fichiers existants.

### Échec de la connexion sécurisée à MongoDB {#secure-connection-to-mongodb-fails}

Si une tentative d’établissement d’une connexion sécurisée au serveur MongoDB échoue en raison d’une définition de classe manquante, il est nécessaire de mettre à jour le lot de pilotes MongoDB, `mongo-java-driver`, disponible à partir du référentiel Maven public.

1. Téléchargez le pilote à partir de [https://search.maven.org/#artifactdetails%7Corg.mongodb%7Cmongo-java-driver%7C2.13.2%7Cjar](https://search.maven.org/#artifactdetails%7Corg.mongodb%7Cmongo-java-driver%7C2.13.2%7Cjar) (version 2.13.2 ou ultérieure).
1. Copiez le lot dans le dossier &quot;crx-quickstart/install&quot; pour une instance AEM.
1. Redémarrez l’instance AEM.

## Ressources {#resources}

* [AEM avec MongoDB](../../help/sites-deploying/aem-with-mongodb.md)
* [Documentation MongoDB](https://docs.mongodb.org/)

