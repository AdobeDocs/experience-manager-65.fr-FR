---
title: Configuration de MongoDB pour la démonstration
seo-title: Configuration de MongoDB pour la démonstration
description: Configuration du protocole MSRP pour une instance d’auteur et une instance de publication
seo-description: Configuration du protocole MSRP pour une instance d’auteur et une instance de publication
uuid: d2035a9e-f05c-4f90-949d-7cdae9646750
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: 0b126218-b142-4d33-a28c-a91ab4fe99ac
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Configuration de MongoDB pour la démonstration {#how-to-setup-mongodb-for-demo}

## Présentation {#introduction}

Ce didacticiel explique comment configurer [MSRP](msrp.md) pour *une instance d’auteur* et *une instance de publication* .

Avec cette configuration, le contenu de la communauté est accessible à partir des environnements d’auteur et de publication sans avoir à transférer ou à inverser la réplication du contenu généré par l’utilisateur (UGC).

Cette configuration est adaptée aux environnements *non productifs* tels que le développement et/ou la démonstration.

**Un environnement *de production*devrait:**

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
   * Configurer pour mongod

      * Pas besoin de configurer les mongos ou le partage
   * Le dossier MongoDB installé sera appelé &lt;mongo-install>
   * Le chemin d’accès au répertoire de données défini sera appelé &lt;mongo-dbpath>.


* MongoDB peut s’exécuter sur le même hôte qu’AEM ou à distance

### Démarrer MongoDB {#start-mongodb}

* &lt;mongo-install>/bin/mongod —dbpath &lt;mongo-dbpath>

Ceci démarrera un serveur MongoDB à l’aide du port par défaut 27017.

* Pour Mac, augmentez ulimit avec l’arg de démarrage &quot;ulimit -n 2048&quot;.

>[!NOTE]
>
>Si MongoDB est démarré *après *AEM, **redémarrez **toutes les **instances AEM **afin qu’elles se connectent correctement à MongoDB.

### Option de production de démonstration : Configuration d’un jeu de réplicas MongoDB {#demo-production-option-setup-mongodb-replica-set}

Les commandes suivantes constituent un exemple de configuration d’un jeu de réplicas avec 3 noeuds sur localhost :

* bin/mongod —port 27017 —dbpath data —replSet rs0&amp;
* bin/mongo

   * cfg = {&quot;_id&quot; : &quot;rs0&quot;,&quot;version&quot; : 1,&quot;membres&quot; : [{&quot;_id&quot; : 0,&quot;host&quot; : &quot;127.0.0.1:27017&quot;}]}
   * rs.initiate(cfg)

* bin/mongod —port 27018 —dbpath data1 —replSet rs0&amp;
* bin/mongod —port 27019 —dbpath data2 —replSet rs0&amp;
* bin/mongo

   * rs.add(&quot;127.0.0.1:27018&quot;)
   * rs.add(&quot;127.0.0.1:27019&quot;)
   * rs.status()

## Solr {#solr}

### Installer Solr {#install-solr}

* Téléchargez Solr depuis [Apache Lucene](https://archive.apache.org/dist/lucene/solr/):

   * Adapté à tous les systèmes d’exploitation
   * Utiliser la version 4.10 ou la version 5
   * Le solaire requiert Java 1.7 ou version ultérieure

* Configuration de base

   * Suivez l&#39;exemple de configuration Solr
   * Aucun service requis
   * Le dossier Solr installé sera appelé &lt;solr-install>

### Configuration de Solr pour les communautés AEM {#configure-solr-for-aem-communities}

Pour configurer une collection Solr pour MSRP pour la démonstration, deux décisions doivent être prises (sélectionnez les liens vers la documentation principale pour plus de détails) :

1. Exécution de Solr en mode autonome ou [SolrCloud](msrp.md#solrcloudmode)
1. Installer la recherche multilingue [standard](msrp.md#installingstandardmls) ou [avancée](msrp.md#installingadvancedmls) (MLS)

### Solr autonome {#standalone-solr}

La méthode d’exécution de Solr peut varier selon la version et le mode d’installation. Le guide [de référence](https://archive.apache.org/dist/lucene/solr/ref-guide/) Solr est la documentation faisant autorité.

Pour simplifier, en utilisant la version 4.10 comme exemple, démarrez Solr en mode autonome :

* cd à &lt;solrinstall>/example
* java -jar start.jar

Ceci démarrera un serveur HTTP Solr en utilisant le port par défaut 8983. Vous pouvez accéder à la console Solr pour obtenir une console Solr à tester.

* console Solr par défaut : [http://localhost:8983/solr/](http://localhost:8983/solr/)

>[!NOTE]
>
>Si Solr Console n&#39;est pas disponible, vérifiez les journaux sous &lt;solrinstall>/example/logs. Vérifiez si SOLR tente de se lier à un nom d’hôte spécifique qui ne peut pas être résolu (ex. &quot;user-macbook-pro&quot;).
Si c&#39;est le cas, mettez à jour le fichier etc/hosts avec une nouvelle entrée pour ce nom d&#39;hôte (par exemple, 127.0.0.1 user-macbook-pro) et Solr démarrera correctement.

### SolrCloud {#solrcloud}

Pour exécuter une configuration solrCloud de base (pas de production), commencez solr par :

* java -Dbootstrap_confdir=./solr/collection1/conf -Dbootstrap_conf=true -DzkRun -jar start.jar

## Identifier MongoDB comme magasin commun {#identify-mongodb-as-common-store}

Lancez l’auteur et publiez les instances AEM, si nécessaire.

Si AEM s’exécutait avant le démarrage de MongoDB, les instances AEM devront être redémarrées.

Suivez les instructions de la page de documentation principale : [MSRP - Magasin commun MongoDB](msrp.md)

## Test {#test}

Pour tester et vérifier le magasin commun MongoDB, publiez un commentaire sur l’instance de publication et affichez-le sur l’instance d’auteur, ainsi que l’UGC dans MongoDB et Solr :

1. Sur l’instance de publication, accédez à la page Guide [des composants](http://localhost:4503/content/community-components/en/comments.html) de la communauté et sélectionnez le composant Commentaires.
1. Connectez-vous pour publier un commentaire :
1. Saisissez du texte dans la zone de texte du commentaire, puis cliquez sur **[!UICONTROL Publier.]**

   ![chlimage_1-191](assets/chlimage_1-191.png)

1. Il vous suffit d’afficher le commentaire sur l’instance [d’](http://localhost:4502/content/community-components/en/comments.html) auteur (probablement encore connecté en tant qu’administrateur/administrateur).

   ![chlimage_1-192](assets/chlimage_1-192.png)

   Remarque : alors qu’il existe des noeuds JCR sous le chemin *asipath* sur l’auteur, ils sont pour la structure SCF. L’UGC réel n’est pas dans le JCR, mais dans la MongoDB.

1. Affichez l’UGC dans mongodb **[!UICONTROL Communities > Collections > Content]**

   ![chlimage_1-193](assets/chlimage_1-193.png)

1. Voir l&#39;UGC en Solr :

   * Accéder au tableau de bord Solr : [http://localhost:8983/solr/](http://localhost:8983/solr/)
   * Utilisateur `core selector` à sélectionner `collection1`
   * Sélectionner `Query`
   * Sélectionner `Execute Query`
   ![chlimage_1-194](assets/chlimage_1-194.png)

## Résolution des incidents {#troubleshooting}

### Aucune UGC n’apparaît {#no-ugc-appears}

1. Assurez-vous que MongoDB est installé et fonctionne correctement.

1. Vérifiez que MSRP a été configuré comme fournisseur par défaut :

   * Sur toutes les instances d’auteur et de publication AEM, revisitez la console de configuration du [stockage](srp-config.md)
   ou consultez le référentiel AEM :

   * Dans JCR, if [/etc/socialconfig](http://localhost:4502/crx/de/index.jsp#/etc/socialconfig/)

      * Ne contient pas de noeud [srpc](http://localhost:4502/crx/de/index.jsp#/etc/socialconfig/srpc) , cela signifie que le fournisseur de stockage est JSRP
      * Si le noeud srpc existe et contient la configuration [par](http://localhost:4502/crx/de/index.jsp#/etc/socialconfig/srpc/defaultconfiguration)défaut du noeud, les propriétés de la configuration par défaut doivent définir MSRP comme fournisseur par défaut


1. Assurez-vous qu’AEM a été redémarré après avoir sélectionné MSRP.
