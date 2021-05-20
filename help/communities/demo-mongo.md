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
exl-id: 7e257b34-a0f5-47db-b1a9-e26333c287d9
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '792'
ht-degree: 1%

---

# Configuration de MongoDB pour la démonstration {#how-to-setup-mongodb-for-demo}

## Présentation {#introduction}

Ce tutoriel explique comment configurer [MSRP](msrp.md) pour *une instance d’auteur* et *une instance de publication*.

Avec cette configuration, le contenu de la communauté est accessible à partir des environnements de création et de publication sans avoir à transférer ou à répliquer à l’envers le contenu généré par l’utilisateur.

Cette configuration est adaptée aux environnements *hors production* tels que le développement et/ou la démonstration.

**Un environnement  ** de production doit :**

* Exécution de MongoDB avec un jeu de réplications
* Utilisation de SolrCloud
* Contenir plusieurs instances d’éditeur

## MongoDB {#mongodb}

### Installer MongoDB {#install-mongodb}

* Téléchargez MongoDB à partir de [https://www.mongodb.org/](https://www.mongodb.org/)

   * Choix du système d’exploitation :

      * Linux
      * Mac 10.8
      * Windows 7
   * Choix de la version :

      * Utilisez au minimum la version 2.6.


* Configuration de base

   * Suivez les instructions d’installation de MongoDB.
   * Configuration pour mongod :

      * Il n’est pas nécessaire de configurer les mongos ou le partage.
   * Le dossier MongoDB installé est appelé &lt;mongo-install>.
   * Le chemin d’accès au répertoire de données défini sera appelé &lt;mongo-dbpath>.


* MongoDB peut s’exécuter sur le même hôte qu’AEM ou à distance.

### Démarrer MongoDB {#start-mongodb}

* &lt;mongo-install>/bin/mongod —dbpath  &lt;mongo-dbpath>

Cela démarrera un serveur MongoDB à l’aide du port par défaut 27017.

* Pour Mac, augmentez ulimit avec l’arg de démarrage &#39;ulimit -n 2048&#39;

>[!NOTE]
>
>Si MongoDB est démarré *après* AEM, **restart** toutes les instances **AEM** afin qu’elles se connectent correctement à MongoDB.

### Option de production de démonstration : Configuration d’un jeu de Secondaires MongoDB {#demo-production-option-setup-mongodb-replica-set}

Les commandes suivantes constituent un exemple de configuration d’un ensemble de réplication avec 3 noeuds sur localhost :

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
   * Solr requiert Java 1.7 ou version ultérieure.

* Configuration de base

   * Suivez &quot;exemple&quot; Configuration Solr.
   * Aucun service n’est nécessaire.
   * Le dossier Solr installé sera appelé &lt;solr-install>.

### Configuration de Solr pour AEM Communities {#configure-solr-for-aem-communities}

Pour configurer une collection Solr pour MSRP à des fins de démonstration, deux décisions doivent être prises (pour plus de détails, cliquez sur les liens vers la documentation principale) :

1. Exécutez Solr en mode autonome ou [SolrCloud ](msrp.md#solrcloudmode).
1. Installez [standard](msrp.md#installingstandardmls) ou [recherche avancée](msrp.md#installingadvancedmls) multilingue (MLS).

### Solr autonome {#standalone-solr}

La méthode d’exécution de Solr peut varier en fonction de la version et du mode d’installation. Le [guide de référence Solr](https://archive.apache.org/dist/lucene/solr/ref-guide/) est la documentation faisant autorité.

Pour plus de simplicité, à l’aide de la version 4.10, démarrez Solr en mode autonome :

* cd à &lt;solrinstall>/example
* java -jar start.jar

Cela lancera un serveur HTTP Solr en utilisant le port par défaut 8983. Vous pouvez accéder à la console Solr pour obtenir une console Solr à des fins de test.

* console Solr par défaut : [http://localhost:8983/solr/](http://localhost:8983/solr/)

>[!NOTE]
>
>Si la console Solr n’est pas disponible, vérifiez les journaux sous &lt;solrinstall>/example/logs. Vérifiez si SOLR tente de se lier à un nom d’hôte spécifique qui ne peut pas être résolu (par exemple : &quot;user-macbook-pro&quot;).
Si tel est le cas, mettez à jour le fichier etc/hosts avec une nouvelle entrée pour ce nom d’hôte (par exemple, 127.0.0.1 user-macbook-pro) et Solr démarrera correctement.

### SolrCloud {#solrcloud}

Pour exécuter une configuration solrCloud de base (et non de production), commencez solder par :

* `java -Dbootstrap_confdir=./solr/collection1/conf -Dbootstrap_conf=true -DzkRun -jar start.jar`

## Identifiez MongoDB en tant que magasin commun {#identify-mongodb-as-common-store}

Lancez les instances d’AEM de création et de publication, si nécessaire.

Si AEM était en cours d’exécution avant le démarrage de MongoDB, les instances AEM doivent être redémarrées.

Suivez les instructions de la page de documentation principale : [MSRP - MongoDB Common Store](msrp.md)

## Test {#test}

Pour tester et vérifier le magasin commun MongoDB, publiez un commentaire sur l’instance de publication et affichez-le sur l’instance d’auteur, ainsi que le contenu créé par l’utilisateur dans MongoDB et Solr :

1. Sur l’instance de publication, accédez à la page [Guide des composants de la communauté](http://localhost:4503/content/community-components/en/comments.html) et sélectionnez le composant Commentaires .
1. Connectez-vous pour publier un commentaire :
1. Saisissez du texte dans la zone de saisie du texte du commentaire, puis cliquez sur **[!UICONTROL Publier]**

   ![post-commentaire](assets/post-comment.png)

1. Consultez simplement le commentaire sur l’ [instance d’auteur](http://localhost:4502/content/community-components/en/comments.html) (probablement toujours connecté en tant qu’administrateur/administrateur).

   ![view-comment](assets/view-comment.png)

   Remarque : Bien qu’il existe des noeuds JCR sous *asipath* sur l’auteur, ils sont destinés à la structure SCF. Le contenu généré par l’utilisateur réel n’est pas dans JCR, mais dans MongoDB.

1. Affichez le contenu généré par l’utilisateur dans mongodb **[!UICONTROL Communities]** > **[!UICONTROL Collections]** > **[!UICONTROL Contenu]**

   ![ugc-content](assets/ugc-content.png)

1. Affichez le contenu généré par l’utilisateur dans Solr :

   * Accédez au tableau de bord Solr : [http://localhost:8983/solr/](http://localhost:8983/solr/).
   * Utilisateur `core selector` à sélectionner `collection1`.
   * Sélectionner `Query`.
   * Sélectionner `Execute Query`.

   ![ugc-solr](assets/ugc-solr.png)

## Résolution des problèmes {#troubleshooting}

### Aucun contenu généré par l’utilisateur n’apparaît {#no-ugc-appears}

1. Assurez-vous que MongoDB est installé et exécuté correctement.

1. Vérifiez que MSRP a été configuré comme fournisseur par défaut :

   * Sur toutes les instances d’AEM de création et de publication, consultez à nouveau la [console Configuration de stockage](srp-config.md) ou vérifiez le référentiel AEM :

   * Dans JCR, si [/etc/socialconfig](http://localhost:4502/crx/de/index.jsp#/etc/socialconfig/) ne contient pas de noeud [srpc](http://localhost:4502/crx/de/index.jsp#/etc/socialconfig/srpc), cela signifie que le fournisseur de stockage est JSRP.
   * Si le noeud srpc existe et contient le noeud [defaultconfiguration](http://localhost:4502/crx/de/index.jsp#/etc/socialconfig/srpc/defaultconfiguration), les propriétés de la configuration par défaut doivent définir MSRP comme fournisseur par défaut.

1. Assurez-vous que AEM a été redémarré une fois que MSRP a été sélectionné.
