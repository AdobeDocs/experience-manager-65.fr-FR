---
title: Configuration de MongoDB pour la démonstration
seo-title: Configuration de MongoDB pour la démonstration
description: Comment configurer MSRP pour une instance d’auteur et une instance de publication
seo-description: Comment configurer MSRP pour une instance d’auteur et une instance de publication
uuid: d2035a9e-f05c-4f90-949d-7cdae9646750
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 0b126218-b142-4d33-a28c-a91ab4fe99ac
role: Administrator
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '793'
ht-degree: 1%

---


# Comment configurer MongoDB pour la démonstration {#how-to-setup-mongodb-for-demo}

## Présentation {#introduction}

Ce didacticiel décrit comment configurer [MSRP](msrp.md) pour *une instance d&#39;auteur* et *une instance de publication*.

Avec cette configuration, le contenu de la communauté est accessible à partir des environnements d’auteur et de publication sans qu’il faille transférer ou inverser la réplication du contenu généré par l’utilisateur (UGC).

Cette configuration convient aux environnements *non-production* tels que le développement et/ou la démonstration.

**Un environnement  ** de production devrait :**

* Exécution de MongoDB avec un jeu de réplicas
* Utiliser SolrCloud
* Contenir plusieurs instances d’éditeur

## MongoDB {#mongodb}

### Installer MongoDB {#install-mongodb}

* Téléchargez MongoDB depuis [https://www.mongodb.org/](https://www.mongodb.org/)

   * Choix du système d’exploitation :

      * Linux
      * Mac 10.8
      * Windows 7
   * Choix de la version :

      * Utilisez au minimum la version 2.6.


* Configuration de base

   * Suivez les instructions d’installation de MongoDB.
   * Configurer pour mongod :

      * Pas besoin de configurer les mongos ou le partage.
   * Le dossier MongoDB installé sera appelé &lt;mongo-install>.
   * Le chemin d&#39;accès au répertoire de données défini sera appelé &lt;mongo-dbpath>.


* MongoDB peut s&#39;exécuter sur le même hôte que AEM ou à distance.

### Début MongoDB {#start-mongodb}

* &lt;mongo-install>/bin/mongod —dbpath  &lt;mongo-dbpath>

Ceci début un serveur MongoDB à l’aide du port par défaut 27017.

* Pour Mac, augmentez ulimit avec l’arg de début &quot;ulimit -n 2048&quot;.

>[!NOTE]
>
>Si MongoDB est démarré *après* AEM, **redémarrez** toutes les instances **AEM** afin qu’elles se connectent correctement à MongoDB.

### Option de production de démonstration : Configurer le jeu de Secondaires MongoDB {#demo-production-option-setup-mongodb-replica-set}

Les commandes suivantes constituent un exemple de configuration d’un jeu de réplicas avec 3 noeuds sur localhost :

* `bin/mongod --port 27017 --dbpath data --replSet rs0&`
* `bin/mongo`

   * `cfg = {"_id": "rs0","version": 1,"members": [{"_id": 0,"host": "127.0.0.1:27017"}]}`
   * `rs.initiate(cfg)`

* `bin/mongod --port 27018 --dbpath data1 --replSet rs0&`
* `bin/mongod --port 27019 --dbpath data2 --replSet rs0&`
* `bin/mongo`

   * `rs.add("127.0.0.1:27018")`
   * `rs.add("127.0.0.1:27019")`
   * `rs.status()`

## Solr {#solr}

### Installer Solr {#install-solr}

* Téléchargez Solr à partir de [Apache Lucene](https://archive.apache.org/dist/lucene/solr/) :

   * Adapté à tous les systèmes d’exploitation.
   * Solr version 7.0.
   * Le solaire requiert Java 1.7 ou version ultérieure.

* Configuration de base

   * Suivez l&#39;exemple de configuration Solr.
   * Aucun service n&#39;est nécessaire.
   * Le dossier Solr installé sera appelé &lt;solr-install>.

### Configurer Solr pour AEM Communities {#configure-solr-for-aem-communities}

Pour configurer une collection Solr pour MSRP pour la démonstration, deux décisions doivent être prises (sélectionnez les liens vers la documentation principale pour plus de détails) :

1. Exécutez Solr en mode autonome ou [SolrCloud ](msrp.md#solrcloudmode).
1. Installez [standard](msrp.md#installingstandardmls) ou [recherche avancée](msrp.md#installingadvancedmls) multilingue (MLS).

### Solr autonome {#standalone-solr}

La méthode d&#39;exécution de Solr peut varier en fonction de la version et du mode d&#39;installation. Le [guide de référence Solr](https://archive.apache.org/dist/lucene/solr/ref-guide/) est la documentation faisant autorité.

Pour simplifier, en utilisant la version 4.10 comme exemple, début Solr en mode autonome :

* cd à &lt;solrinstall>/example
* java -jar début.jar

Ceci début un serveur HTTP Solr en utilisant le port par défaut 8983. Vous pouvez accéder à la console Solr pour obtenir une console Solr à des fins de test.

* console Solr par défaut : [http://localhost:8983/solr/](http://localhost:8983/solr/)

>[!NOTE]
>
>Si Solr Console n&#39;est pas disponible, vérifiez les journaux sous &lt;solrinstall>/example/logs. Vérifiez si SOLR tente de se lier à un nom d’hôte spécifique qui ne peut pas être résolu (ex. &quot;user-macbook-pro&quot;).
Si c&#39;est le cas, mettez à jour le fichier etc/hosts avec une nouvelle entrée pour ce nom d&#39;hôte (par exemple, 127.0.0.1 user-macbook-pro) et Solr sera correctement début.

### SolrCloud {#solrcloud}

Pour exécuter une configuration solrCloud de base (pas de production), début solr avec :

* `java -Dbootstrap_confdir=./solr/collection1/conf -Dbootstrap_conf=true -DzkRun -jar start.jar`

## Identifier MongoDB comme magasin commun {#identify-mongodb-as-common-store}

Lancez les instances d’auteur et de publication AEM, si nécessaire.

Si l&#39;AEM était en cours d&#39;exécution avant le démarrage de MongoDB, les instances AEM devront être redémarrées.

Suivez les instructions de la page de documentation principale : [MSRP - MongoDB Common Store](msrp.md)

## Test {#test}

Pour tester et vérifier le magasin commun MongoDB, publiez un commentaire sur l’instance de publication et vue-le sur l’instance d’auteur, ainsi que la vue de l’UGC dans MongoDB et Solr :

1. Sur l’instance de publication, accédez à la page [Community Components Guide](http://localhost:4503/content/community-components/en/comments.html) et sélectionnez le composant Commentaires.
1. Connectez-vous pour publier un commentaire :
1. Saisissez du texte dans la zone de saisie du commentaire, puis cliquez sur **[!UICONTROL Publier]**.

   ![post-commentaire](assets/post-comment.png)

1. Il vous suffit de vue le commentaire sur l’[instance d’auteur](http://localhost:4502/content/community-components/en/comments.html) (probablement encore connecté en tant qu’administrateur / administrateur).

   ![vue-commentaire](assets/view-comment.png)

   Remarque : Bien qu’il existe des noeuds JCR sous le *asipath* sur l’auteur, il s’agit de la structure SCF. L’UGC réel n’est pas dans le JCR, mais dans la MongoDB.

1. Vue de l’UGC dans mongodb **[!UICONTROL Communautés]** > **[!UICONTROL Collections]** > **[!UICONTROL Contenu]**

   ![ugc-content](assets/ugc-content.png)

1. Vue de l&#39;UGC à Solr :

   * Accédez au tableau de bord Solr : [http://localhost:8983/solr/](http://localhost:8983/solr/).
   * Utilisateur `core selector` à sélectionner `collection1`.
   * Sélectionner `Query`.
   * Sélectionner `Execute Query`.

   ![ugc-solr](assets/ugc-solr.png)

## Résolution des incidents {#troubleshooting}

### Aucun UGC n&#39;apparaît {#no-ugc-appears}

1. Assurez-vous que MongoDB est installé et s’exécute correctement.

1. Assurez-vous que MSRP a été configuré comme fournisseur par défaut :

   * Sur toutes les instances d’AEM auteur et de publication, consultez de nouveau la [console de configuration d’Enregistrement](srp-config.md) ou vérifiez le référentiel AEM :

   * Dans JCR, si [/etc/socialconfig](http://localhost:4502/crx/de/index.jsp#/etc/socialconfig/) ne contient pas de noeud [srpc](http://localhost:4502/crx/de/index.jsp#/etc/socialconfig/srpc), cela signifie que le fournisseur d’enregistrement est JSRP.
   * Si le noeud srpc existe et contient le noeud [defaultconfiguration](http://localhost:4502/crx/de/index.jsp#/etc/socialconfig/srpc/defaultconfiguration), les propriétés de la configuration par défaut doivent définir MSRP comme fournisseur par défaut.

1. Assurez-vous que l&#39;AEM a été redémarré après avoir sélectionné MSRP.
