---
title: MSRP - Fournisseur de ressources d'Enregistrement MongoDB
seo-title: MSRP - Fournisseur de ressources d'Enregistrement MongoDB
description: Configurer AEM Communities pour utiliser une base de données relationnelle comme magasin commun
seo-description: Configurer AEM Communities pour utiliser une base de données relationnelle comme magasin commun
uuid: 9fc06d4f-a60f-4ce3-8586-bcc836aa7de6
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 048f7b30-20c3-4567-bd32-38cf2643cf39
translation-type: tm+mt
source-git-commit: f375b40c084ee363757b78c602091f38524b8b03
workflow-type: tm+mt
source-wordcount: '1209'
ht-degree: 3%

---


# MSRP - Fournisseur de ressources d&#39;Enregistrement MongoDB {#msrp-mongodb-storage-resource-provider}

## A propos de MSRP {#about-msrp}

Lorsque AEM Communities est configuré pour utiliser MSRP comme magasin commun, le contenu généré par l’utilisateur est accessible à partir de toutes les instances d’auteur et de publication sans avoir à effectuer de synchronisation ni de réplication.

Voir aussi [Caractéristiques des options](working-with-srp.md#characteristics-of-srp-options) SRP et Topologies [](topologies.md)recommandées.

## Conditions requises {#requirements}

* [MongoDB](https://www.mongodb.org/):

   * Version 2.6 ou ultérieure
   * Pas besoin de configurer les mongos ou le partage
   * Recommander fortement l&#39;utilisation d&#39;un jeu de [réplicas](#mongoreplicaset)
   * Peut s’exécuter sur le même hôte que AEM ou à distance

* [Apache Solr](https://lucene.apache.org/solr/):

   * Solr version 7.0
   * Le serveur requiert Java 1.7 ou version ultérieure
   * Aucun service requis
   * Choix des modes d&#39;exécution :
      * Mode autonome
      * [Mode](solr.md#solrcloud-mode) SolrCloud (recommandé pour les environnements de production)
   * Choix de la recherche multilingue (MLS) :
      * [Installation de MLS standard](solr.md#installing-standard-mls)
      * [Installation de MLS avancé](solr.md#installing-advanced-mls)

## MongoDB Configuration {#mongodb-configuration}

### Sélectionner MSRP {#select-msrp}

La console [Configuration de l&#39;](srp-config.md) Enregistrement permet de sélectionner la configuration d&#39;enregistrement par défaut, qui identifie l&#39;implémentation de SRP à utiliser.

Sur author, pour accéder à la console de configuration d’Enregistrement :

* Dans la navigation globale, sélectionnez **[!UICONTROL Outils]** > **[!UICONTROL Communautés]** > Configuration **[!UICONTROL de l’]** Enregistrement.

![msrp](assets/msrp.png)

* Select **[!UICONTROL MongoDB Storage Resource Provider (MSRP)]**
* **[!UICONTROL Configuration de mongoDB]**

   * **[!UICONTROL URI de mongoDB]**

      *par défaut*: mongodb://localhost/?maxPoolSize=10&amp;waitQueueMultiple=5&amp;readPreference=secondaryPreferred

   * **[!UICONTROL Base de données mongoDB]**

      *par défaut*: communautés

   * **[!UICONTROL Collection UGC mongoDB]**

      *par défaut*: content

   * **[!UICONTROL Collection de pièces jointes mongoDB]**

      *par défaut*: pièces jointes

* **[!UICONTROL SolrConfiguration]**

   * **[](https://cwiki.apache.org/confluence/display/solr/Using+ZooKeeper+to+Manage+Configuration+Files)Hôte Zookeeper**

      Lors de l’exécution en mode [](solr.md#solrcloud-mode) SolrCloud avec un ZooKeeper externe, définissez cette valeur sur la valeur `HOST:PORT` pour le ZooKeeper, telle que *my.server.com:2181.*

      Pour un ensemble ZooKeeper, saisissez des `HOST:PORT` valeurs séparées par des virgules, telles que *host1:2181,host2:2181.*

      Laissez vide si Solr est exécuté en mode autonome à l’aide du ZooKeeper interne.
      *Par défaut*: *&lt;blank>*

      * **[!UICONTROL URL]**solaire URL utilisée pour communiquer avec Solr en mode autonome.
Laissez vide si vous exécutez en mode SolrCloud.

         *Par défaut*: https://127.0.0.1:8983/solr/

      * **[!UICONTROL Collection]**Solr Nom de la collection Solr.

         *Par défaut*: collection1

* Sélectionnez **[!UICONTROL Envoyer]**

>[!NOTE]
>
>La base de données mongoDB, dont le nom par défaut `communities`est le nom, ne doit pas être définie sur le nom d’une base de données utilisée pour les magasins de [noeuds ou les magasins de données (binaires)](../../help/sites-deploying/data-store-config.md). Voir aussi [Enregistrement Elements dans AEM 6.5](../../help/sites-deploying/storage-elements-in-aem-6.md).

### Jeu de Secondaires MongoDB {#mongodb-replica-set}

Pour l’environnement de production, il est fortement recommandé de configurer un jeu de réplicas, un cluster de serveurs MongoDB qui implémente la réplication Principale-secondaire et le basculement automatisé.

Pour en savoir plus sur les jeux de réplicas, consultez la documentation sur la [réplication](https://docs.mongodb.org/manual/replication/) de MongoDB.

Pour utiliser des jeux de réplicas et apprendre à définir des connexions entre les applications et les instances MongoDB, consultez la documentation sur le format [URI de chaîne de](https://docs.mongodb.org/manual/reference/connection-string/) connexion de MongoDB.

#### Exemple d’URL pour la connexion à un jeu de Secondaires  {#example-url-for-connecting-to-a-replica-set}

```shell
# Example url for:
# servers "mongoserver1", "mongoserver2", "mongoserver3"
# replica set 'rs0'
# port numbers only necessary if not default port 27017
mongodb://mongoserver1:<mongoport1>,mongoserver2:<mongoport2>,mongoserver3:<mongoport3>/?replicaSet=rs0&maxPoolSize=100&waitQueueMultiple=50&readPreference=secondaryPreferred
```

## Configuration de Solr {#solr-configuration}

Une installation Solr peut être partagée entre le magasin de noeuds (Oak) et le magasin commun (MSRP) en utilisant différentes collections.

Si les deux collections Oak et MSRP sont utilisées de façon intensive, un second Solr peut être installé pour des raisons de performances.

Pour les environnements de production, le mode [](solr.md#solrcloud-mode) SolrCloud offre de meilleures performances par rapport au mode autonome (une seule configuration Solr locale).

Pour plus d&#39;informations sur la configuration, reportez-vous à la section Configuration [solaire pour SRP](solr.md).

### Mise à niveau {#upgrading}

Si la mise à niveau à partir d’une version antérieure configurée avec MSRP, il sera nécessaire de :

1. Effectuer la [mise à niveau vers AEM Communities](upgrade.md)
1. Installer de nouveaux fichiers de configuration Solr
   * Pour MLS [standard](solr.md#installing-standard-mls)
   * Pour MLS [avancé](solr.md#installing-advanced-mls)
1. Réindexer l&#39;outil de réindexation de la section [MSRP MSRP](#msrp-reindex-tool)

## Publication de la configuration {#publishing-the-configuration}

MSRP doit être identifié comme le magasin commun sur toutes les instances d’auteur et de publication.

Pour rendre la configuration identique disponible dans l’environnement de publication, connectez-vous à votre instance d’auteur et procédez comme suit :

* Dans le menu principal, sélectionnez **[!UICONTROL Outils]** > **[!UICONTROL Opérations]** > **[!UICONTROL Réplication]**.
* Sélectionner **[!UICONTROL Activer l&#39;arborescence]**
* **[!UICONTROL Chemin de début]**:
   * Naviguer jusqu’à `/etc/socialconfig/srpc/`
* Sélectionner **[!UICONTROL Activer]**

## Gestion des données utilisateur {#managing-user-data}

Pour plus d’informations sur *les utilisateurs*, les profils ** utilisateur et les groupes *d’* utilisateurs, souvent saisis dans l’environnement de publication, consultez la page

* [Synchronisation des utilisateurs](sync.md)
* [Gestion des utilisateurs et des groupes d’utilisateurs](users.md)

## Outil de réindexation MSRP {#msrp-reindex-tool}

Il existe un point de terminaison HTTP pour la réindexation de Solr pour MSRP lors de l&#39;installation de nouveaux fichiers de configuration ou de la réparation d&#39;un index Solr endommagé.

Avec cet outil, MongoDB est la source de *vérité* pour MSRP ; les sauvegardes ne doivent être effectuées que sur MongoDB.

L&#39;arbre UGC entier peut être réindexé, ou seulement une sous-arborescence spécifique, comme spécifié par le paramètre *path *data.

Cet outil peut être exécuté à partir de la ligne de commande à l&#39;aide de cURL ou de tout autre outil HTTP.

Lors de la réindexation, il existe un compromis entre la mémoire et les performances contrôlées par le paramètre de données *batchSize *qui spécifie le nombre d&#39;enregistrements UGC réindexés par lot.

La valeur par défaut raisonnable est 5000 :

* Si la mémoire pose problème, indiquez un nombre inférieur.
* Si la vitesse est un problème, indiquez un nombre plus élevé pour augmenter la vitesse.

### Exécution de l’outil de réindexation MSRP à l’aide de la commande cURL {#running-msrp-reindex-tool-using-curl-command}

La commande cURL suivante indique ce qui est nécessaire pour qu’une requête HTTP puisse réindexer l’UGC stockée dans MSRP.

Le format de base est le suivant :

cURL -u *signature* -d *data* *reindex-url*

*signature* = administrator-id:passwordPar exemple : admin:admin

*data* = &quot;batchSize=*size*&amp;path=*path&quot;*

*taille* = nombre d&#39;entrées UGC à réindexer par opération
`/content/usergenerated/asi/mongo/`

*chemin* = emplacement racine de l&#39;arborescence de l&#39;UGC à réindexer

* Pour réindexer tous les fichiers UGC, spécifiez la valeur de la `asipath`propriété de
   `/etc/socialconfig/srpc/defaultconfiguration`
* Pour limiter l’index à certains UGC, spécifiez une sous-arborescence de `asipath`

*reindex-url* = point de terminaison de la réindexation de SRP
`http://localhost:4503/services/social/datastore/mongo/reindex`

>[!NOTE]
>
>Si vous [réindexez DSRP Solr](dsrp.md), l’URL est **/services/social/datastore/rdb/reindex.**

### Exemple de réindexation MSRP {#msrp-reindex-example}

```shell
curl -s -u admin:admin -d 'batchSize=10000&path=/content/usergenerated/asi/mongo/' http://localhost:4503/services/social/datastore/mongo/reindex
```

## Démonstration de MSRP {#how-to-demo-msrp}

Pour configurer MSRP pour une démonstration ou un environnement de développement, voir [Procédure de configuration de MongoDB pour la démonstration](demo-mongo.md).

## Résolution des incidents {#troubleshooting}

### UGC invisible dans MongoDB {#ugc-not-visible-in-mongodb}

Assurez-vous que MSRP a été configuré comme fournisseur par défaut en vérifiant la configuration de l’option enregistrement. Par défaut, le fournisseur de ressources d’enregistrement est JSRP.

Sur toutes les instances d’AEM création et de publication, consultez de nouveau la console [Configuration de l’](srp-config.md) Enregistrement ou vérifiez le référentiel AEM :

* Dans JCR, si [/etc/socialconfig](http://localhost:4502/crx/de/index.jsp#/etc/socialconfig/)

   * Ne contient pas de noeud [srpc](http://localhost:4502/crx/de/index.jsp#/etc/socialconfig/srpc) , cela signifie que le fournisseur d’enregistrements est JSRP.
   * Si le noeud srpc existe et contient la configuration [par](http://localhost:4502/crx/de/index.jsp#/etc/socialconfig/srpc/defaultconfiguration)défaut du noeud, les propriétés de la configuration par défaut doivent définir MSRP comme fournisseur par défaut.

### UGC disparaît après la mise à niveau {#ugc-disappears-after-upgrade}

Si une mise à niveau à partir d’un site AEM Communities 6.0 existant, tout fichier UGC préexistant doit être converti en fonction de la structure requise pour l’API [SRP](srp.md) après la mise à niveau vers AEM Communities 6.3.

Un outil open source est disponible sur GitHub à cet effet :

* [Outil de migration UGC AEM Communities](https://github.com/Adobe-Marketing-Cloud/communities-ugc-migration)

L’outil de migration peut être personnalisé pour exporter l’UGC à partir de versions antérieures d’AEM communautés sociales en vue de son importation dans AEM Communities 6.1 ou version ultérieure.

### Erreur - champ non défini provider_id {#error-undefined-field-provider-id}

Si l&#39;erreur suivante apparaît dans les journaux, cela indique que le fichier de schéma Solr n&#39;est pas correctement configuré.

#### JsonMappingException : provider_id de champ non défini {#jsonmappingexception-undefined-field-provider-id}

```xml
Caused by: com.fasterxml.jackson.databind.JsonMappingException: undefined field provider_id
at com.fasterxml.jackson.databind.ser.DefaultSerializerProvider.serializeValue(DefaultSerializerProvider.java:129)
at com.fasterxml.jackson.databind.ObjectMapper.writeValue(ObjectMapper.java:1819)
at com.adobe.cq.social.scf.core.BaseSocialComponent.toJSONString(BaseSocialComponent.java:196)
... 124 common frames omitted
```

Pour résoudre l’erreur, lorsque vous suivez les instructions d’ [installation de MLS](solr.md#installing-standard-mls)standard, veillez à :

* Les fichiers de configuration XML ont été copiés à l’emplacement Solr approprié.
* Solr a été redémarré après que les nouveaux fichiers de configuration ont remplacé les fichiers existants.

### Échec de la connexion sécurisée à MongoDB {#secure-connection-to-mongodb-fails}

Si une tentative d&#39;établir une connexion sécurisée au serveur MongoDB échoue en raison d&#39;une définition de classe manquante, il est nécessaire de mettre à jour le lot de pilotes MongoDB `mongo-java-driver`, disponible dans le référentiel public maven.

1. Téléchargez le pilote à partir de [https://search.maven.org/#artifactdetails%7Corg.mongodb%7Cmongo-java-driver%7C2.13.2%7Cjar](https://search.maven.org/#artifactdetails%7Corg.mongodb%7Cmongo-java-driver%7C2.13.2%7Cjar) (version 2.13.2 ou ultérieure).
1. Copiez le lot dans le dossier &quot;crx-quickstart/install&quot; pour une instance AEM.
1. Redémarrez l’instance AEM.

## Ressources {#resources}

* [AEM avec MongoDB](../../help/sites-deploying/aem-with-mongodb.md)
* [Documentation de MongoDB](https://docs.mongodb.org/)

