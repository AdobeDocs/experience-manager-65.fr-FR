---
title: Configuration solaire pour SRP
seo-title: Configuration solaire pour SRP
description: Une installation Apache Solr peut être partagée entre le magasin de noeuds (Oak) et le magasin commun (SRP) à l’aide de différentes collections.
seo-description: Une installation Apache Solr peut être partagée entre le magasin de noeuds (Oak) et le magasin commun (SRP) à l’aide de différentes collections.
uuid: 7356343d-073c-4266-bdcb-c7e999281476
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: e228f1db-91ea-4ec3-86da-06d89d74bc72
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Configuration solaire pour SRP {#solr-configuration-for-srp}

## Solr pour la plateforme AEM {#solr-for-aem-platform}

Une installation [Apache Solr](https://lucene.apache.org/solr/) peut être partagée entre le magasin [de](../../help/sites-deploying/data-store-config.md) noeuds (Oak) et le magasin [](working-with-srp.md) commun (SRP) en utilisant différentes collections.

Si les collections Oak et SRP sont utilisées de manière intensive, un second Solr peut être installé pour des raisons de performances.

Pour les environnements de production, le mode [](#solrcloud-mode) SolrCloud offre de meilleures performances par rapport au mode autonome (une configuration Solr locale unique).

### Conditions requises {#requirements}

Téléchargez et installez Apache Solr :

* [Version 4.10](https://archive.apache.org/dist/lucene/solr/4.10.4/) ou [version 5](https://archive.apache.org/dist/lucene/solr/5.5.3/)

* Le solaire requiert Java 1.7 ou version ultérieure
* Aucun service requis
* Choix des modes d’exécution :

   * Mode autonome
   * [Mode](#solrcloud-mode) SolrCloud (recommandé pour les environnements de production)

* Choix de la recherche multilingue (MLS)

   * [Installation de Standard MLS](#installing-standard-mls)
   * [Installation de MLS avancé](#installing-advanced-mls)

## Mode SolrCloud {#solrcloud-mode}

[Le mode SolrCloud](https://cwiki.apache.org/confluence/display/solr/SolrCloud) est recommandé pour les environnements de production. Lors de l’exécution en mode SolrCloud, SolrCloud doit être installé et configuré avant d’installer MLS (Multilingual Search).

Il est recommandé de suivre les instructions d’installation de SolrCloud :

* 3 noeuds SolrCloud sur le même serveur
* Un ZooKeeper Apache externe

Il est également recommandé de configurer la JVM pour régler l’utilisation de la mémoire et la collecte des déchets.

### Exemple de configuration JVM {#jvm-configuration-example}

```shell
JVM_OPTS="-server -Xmx2048m -XX:MaxPermSize=768M -XX:+UseConcMarkSweepGC -XX:+CMSClassUnloadingEnabled -Xloggc:../logs/gc.log -XX:+PrintGCDetails -XX:+PrintGCDateStamps -Djava.awt.headless=true"
```

### Commandes de configuration de SolrCloud {#solrcloud-setup-commands}

Lors de l’exécution en mode SolrCloud, avant l’installation de MLS, il est nécessaire d’utiliser les commandes de configuration suivantes de SolrCloud et de les connaître.

#### 1. Téléchargement d’une configuration vers ZooKeeper {#upload-a-configuration-to-zookeeper}

Référence :
[https://cwiki.apache.org/confluence/display/solr/Command+Line+Utilities](https://cwiki.apache.org/confluence/display/solr/Command+Line+Utilities)

Utilisation :
sh ./scripts/cloud-scripts/zkcli.sh \
-cmd upconfig \
-zkhost *server:port* \
-confname *myconfig-name *\
-solrhome- *solr-home-path* \
-confdir *config-dir*

#### 2.Création d’une collection {#create-a-collection}

Référence :
[https://cwiki.apache.org/confluence/display/solr/Solr+Start+Script+Reference#SolrStartScriptReference-Create](https://cwiki.apache.org/confluence/display/solr/Solr+Start+Script+Reference#SolrStartScriptReference-Create)

Utilisation:
./bin/solr create \
-c *mycollection-name*\
-d *config-dir* \
-n nom *myconfig* \
-p *port*\
-s *nombre de tirets* \
-rf *nombre-de-répliques*

#### 3. Liaison d’une collection à un jeu de configuration {#link-a-collection-to-a-configuration-set}

Liez une collection à une configuration déjà chargée dans ZooKeeper.

Référence :
[https://cwiki.apache.org/confluence/display/solr/Command+Line+Utilities](https://cwiki.apache.org/confluence/display/solr/Command+Line+Utilities)

Utilisation :
sh ./scripts/cloud-scripts/zkcli.sh \
-cmd linkconfig \
-zkhost *server:port* \
-collection *mycollection-name* \
-confname *myconfig-name*

### Comparaison des MLS standard et avancés {#comparison-of-standard-and-advanced-mls}

La recherche multilingue (MLS) pour les communautés AEM est conçue pour la plate-forme Solr afin de fournir une recherche améliorée dans toutes les langues prises en charge, y compris l’anglais.

MLS pour les communautés AEM est disponible en tant que MLS standard ou MLS avancé. Standard MLS inclut uniquement les paramètres de configuration Solr et exclut les modules externes ou les fichiers de ressources. Le MLS avancé est une solution plus complète et inclut des paramètres de configuration Solr, ainsi que des modules externes et des ressources connexes.

Standard MLS inclut des améliorations pour la recherche de contenu dans les langues suivantes :

* Anglais : filtre amélioré pour tenter d’établir une correspondance avec les dérivations de mot
* Japonais : amélioration de la définition de jetons japonais pour les caractères demi-largeur

MLS avancé comprend des améliorations pour la recherche de contenu dans les langues suivantes :

* Anglais : briquet remplacé par un lemmatiseur
* Allemand : décompresseur ajouté
* Français : gestion de l’élision ajoutée
* Chinois (simplifié) : ajout d’un jeton plus intelligent
* Diverses langues : ajout d’un radical, d’une liste de mots-clés et d’un normalisateur.

En tout, les 33 langues suivantes sont prises en charge dans Advanced MLS.

| Arabe | Allemand | Norvégien |
|---|---|---|
| Bulgare | Grec | Polonais |
| Chinois (simplifié) | Créole haïtien | Portugais |
| Chinois (traditionnel) | Hébreu | Roumain |
| Tchèque | Hongrois | Russe |
| Danois | Indonésien | Slovaque |
| Néerlandais | Italien | Slovène |
| Anglais | Japonais | Espagnol |
| Estonien | Coréen | Suédois |
| Finnois | Letton | Thaï |
| Français | Lituanien | Turc |

#### Comparaison de la recherche Solr AEM 6.1, de Standard MLS et de Advanced MLS {#comparison-of-aem-solr-search-standard-mls-and-advanced-mls}

**Remarque**: AEM 6.1 fait référence à AEM 6.1 Communities FP3 et versions antérieures.

![chlimage_1-283](assets/chlimage_1-283.png)

### Installation de Standard MLS {#installing-standard-mls}

Pour la collection SRP (MSRP ou DSRP), pour prendre en charge la recherche multilingue standard (MLS), il est nécessaire de modifier deux fichiers de configuration de Solr :

* **schema.xml**
* **solrconfig.xml**

Fichiers MLS standard (schema.xml, solrconfig.xml) pour Solaris 4.10

Fichiers MLS standard (schema.xml, solrconfig.xml) pour Solr 5

Les fichiers MLS standard sont stockés dans le référentiel AEM.

**Remarque**: Bien que les fichiers Solr soient stockés dans le dossier msrp/, ils sont également pour DSRP (aucune modification nécessaire).

**Instructions** de téléchargement : remplacer `solrX` par `solr4` ou `solr5` selon le cas

1. À l’aide de CRXDE|Lite, recherchez

   * /libs/social/config/datastore/msrp/*solrX*/**schema.xml**
   * /libs/social/config/datastore/msrp/*solrX*/**solrconfig.xml**

1. Télécharger sur le serveur local sur lequel Solr est déployé

   * Localisation de la `jcr:content` `jcr:data` propriété du noeud
   * Sélectionnez `view` pour lancer le téléchargement
   * Vérifier que les fichiers sont enregistrés avec les noms et le codage appropriés (UTF8)

1. Suivez les instructions d’installation pour le mode autonome ou SolrCloud.

#### Mode SolrCloud - MLS standard {#solrcloud-mode-standard-mls}

1. Installation et configuration de Solr en mode Solr Cloud
1. Préparez une nouvelle configuration :

   1. Créez *new-config-dir* comme *solr-install-dir*/myconfig/

   1. Copiez le contenu du répertoire de configuration Solr existant dans *new-config-dir*

      * Pour Solr4 : copy *solr-install-dir*/example/solr/collection1/conf/&amp;ast;
      * Pour Solr5 : copy *solr-install-dir*/server/solr/configsets/data_managed_schema_configs/&amp;ast;
   1. Copiez le fichier **schema.xml** téléchargé et le fichier **solrconfig.xml** dans *new-config-dir* pour remplacer les fichiers existants.


1. [Télécharger la nouvelle configuration](#upload-a-configuration-to-zookeeper) vers ZooKeeper
1. [Créez une collection](#create-a-collection) spécifiant les paramètres nécessaires, tels que le nombre de shards, le nombre de réplicas et le nom de configuration.
1. Si le nom de la configuration n’était *pas *fourni lors de la création de la collection, [liez cette nouvelle collection](#link-a-collection-to-a-configuration-set) à la configuration téléchargée sur ZooKeeper.

1. Pour MSRP, exécutez l’outil [de réindexation](msrp.md#msrp-reindex-tool)MSRP, sauf s’il s’agit d’une nouvelle installation.

#### Mode autonome - MLS standard {#standalone-mode-standard-mls}

1. Installer Solr en mode autonome
1. Si vous exécutez Solr5, créez une collection1 (similaire à Solr4) :

   * ./bin/solr start
   * ./bin/solr create_core -c collection1 -d sample_techproducts_configs

1. Sauvegardez **schema.xml** et **solrconfig.xml** dans le répertoire de configuration Solr, par exemple :

   * Pour Solr4 : *solr-install-dir*/exemple/solr/collection1/conf/
   * Créé pour Solr5 : *solr-install-dir*/server/solr/collection1/conf/

1. Copiez les fichiers **schema.xml** et **solrconfig.xml** téléchargés dans le même répertoire.

1. Redémarrer Solr
1. Pour MSRP, exécutez l’outil [de réindexation](#msrpreindextool)MSRP, sauf s’il s’agit d’une nouvelle installation.

### Installation de MLS avancé {#installing-advanced-mls}

Pour que la collection SRP (MSRP ou DSRP) prenne en charge les MLS avancés, de nouveaux modules externes Solr sont requis en plus d’un schéma personnalisé et d’une configuration Solr. Tous les éléments requis sont compressés dans un fichier zip téléchargeable. En outre, un script d’installation est inclus pour une utilisation lorsque Solr est déployé en mode autonome.

Pour obtenir le package MLS avancé, voir [AEM Advanced MLS](deploy-communities.md#aem-advanced-mls) dans la section de déploiement de la documentation.

Pour commencer l’installation en mode SolrCloud ou autonome :

* Téléchargez l’archive ZIP AEM-SOLR-MLS sur le serveur hébergeant Solr.
* Décompresser l&#39;archive

#### Mode SolrCloud - MLS avancé {#solrcloud-mode-advanced-mls}

Instructions d&#39;installation - Notez les quelques différences pour Solr4 et Solr5 :

1. Installation et configuration de Solr en mode Solr Cloud
1. Extrayez le contenu du package MLS avancé sur le disque. Le contenu doit inclure :

   * **schema.xml**
   * **solrconfig.xml**
   * **mots-clés/** dossier
   * **profils/** dossier
   * **dossier extra-libs/**

1. Préparez une nouvelle configuration :

   1. Création d’un répertoire *new-config-dir*

      * Par exemple *solr-install-dir*/myconfig/
      * Création de sous-dossiers stopwords/ et lang/
   1. Copiez le contenu du répertoire de configuration Solr existant dans *new-config-dir*

      * Pour Solr4 : Copiez *solr-install-dir*/exemple/solr/collection1/conf/&amp;ast;
      * Pour Solr5 : Copiez *solr-install-dir*/server/solr/configsets/data_managed_schema_configs/&amp;ast;
   1. Copiez le fichier **schema.xml** extrait et le fichier **solrconfig.xml** dans *new-config-dir* pour remplacer les fichiers existants.
   1. Pour Solr5 : Copiez *solr_install_dir*/server/solr/configsets/sample_techproducts_configs/conf/lang/&amp;ast;.txt&quot; dans *new-config-dir*/lang/
   1. Copiez le dossier/ **mots** de fin extraits dans le dossier *new-config-dir* , ce qui donne *new-config-dir*/stopwords/&amp;ast;.txt



1. [Télécharger la nouvelle configuration](#upload-a-configuration-to-zookeeper) vers ZooKeeper
1. Copiez les nouveaux **profils/** dossier ...

   * Pour Solr4 : Copier dans le dossier/ressources de chaque noeud
   * Pour Solr5 : Copiez dans le dossier server/resources/ de chaque installation Solr. Si tous les noeuds se trouvent dans le même répertoire d’installation Solr, cette étape n’est effectuée qu’une seule fois.

1. Créez un dossier **lib/** dans le répertoire solr-home (contient solr.xml) de chaque noeud dans SolrCloud. Copiez les fichiers JAR des emplacements suivants dans le nouveau dossier lib/ de chaque noeud :

   * **extra-libs/** extrait du package MLS avancé
   * *solr-install-dir/contrib/extraction/lib/*.jar
   * *solr-install-dir/dist/solr-cell*.jar
   * *solr-install-dir/contrib/clustering/lib/*.jar
   * *solr-install-dir/dist/solr-clustering*.jar
   * *solr-install-dir/contrib/langid/lib/*.jar
   * *solr-install-dir/dist/solr-langid*.jar
   * *solr-install-dir/contrib/velocity/lib/*.jar
   * *solr-install-dir/dist/solr-velocity*.jar
   * *solr-install-dir/contrib/analysis-extras/lib/*.jar
   * *solr-install-dir/contrib/analysis-extras/lucene-libs/*.jar

1. [Créez une collection](#create-a-collection) spécifiant les paramètres nécessaires, tels que le nombre de shards, le nombre de réplicas et le nom de configuration.
1. Si le nom de configuration *n’a pas été* fourni lors de la création de la collection, [liez cette nouvelle collection](#link-a-collection-to-a-configuration-set) à la configuration téléchargée sur ZooKeeper.

1. Pour MSRP, exécutez l’outil [de réindexation](#msrpreindextool)MSRP, sauf s’il s’agit d’une nouvelle installation.

#### Mode autonome - MLS avancé {#standalone-mode-advanced-mls}

Un script d’installation est inclus dans le package MLS avancé.

Après avoir extrait le contenu du paquet sur le serveur hébergeant le serveur Solr autonome, exécutez simplement le script d&#39;installation afin d&#39;installer les ressources et les fichiers de configuration nécessaires.

* Installer Solr en mode autonome
* Si vous exécutez Solr5, créez une collection1 (similaire à Solr4) :

   * ./bin/solr start
   * ./bin/solr create_core -c collection1 -d sample_techproducts_configs

* Exécutez le script d’installation : Installer [-v 4|5] - [-d solrhome] - [-c collectionpath]où :

   * -d solrhome

      Répertoire d’installation Solr

   * -c collectionpath

      Chemin d’accès de la collection dans le solaire

   * --help

      Imprimer les options de ligne de commande

   * -v [4|5]

      Définir la version pour solr

* Exemple pour Solr 4.10.4 :

   * Install.bat -v 4 -d c:/solr-4.10.4 -c c:/solr-4.10.4/example/solr/collection1

* Exemple pour Solr 5.4.0 :

   * Install.sh -v 5 -d /tmp/solr-5.4.0 -c /tmp/solr-5.4.0/server/solr/collection1

**Remarque** :

* Le script d’installation sauvegardera les fichiers schema.xml et solrconfig.xml avant d’installer les nouvelles versions en ajoutant &quot;.orig&quot;

### A propos de solrconfig.xml {#about-solrconfig-xml}

Le fichier **solrconfig.xml** contrôle l’intervalle de validation automatique et la visibilité de la recherche et nécessite des tests et des réglages.

&lt;autoCommit> : Par défaut, l’intervalle AutoCommit, qui est une validation sur un stockage stable, est défini sur 15 secondes. La visibilité de la recherche utilise par défaut l’index de pré-validation.

Pour modifier la recherche afin d’utiliser un index mis à jour pour refléter les modifications dues à la validation, définissez &lt;openSearcher> contenu sur true.

&lt;autoSoftCommit> : Une validation &quot;soft&quot; garantit que les modifications sont visibles (l&#39;index est mis à jour), mais ne garantit pas que les modifications sont synchronisées avec un stockage stable (hard commit). Il en résulte une amélioration des performances. Par défaut, &lt;autoSoftCommit> est désactivé avec le paramètre contenu &lt;maxTime> défini sur -1.
