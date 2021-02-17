---
title: Configuration de Solr pour SRP
seo-title: Configuration de Solr pour SRP
description: Une installation Apache Solr peut être partagée entre le Node Store (Oak) et le Common Store (SRP) en utilisant différentes collections.
seo-description: Une installation Apache Solr peut être partagée entre le Node Store (Oak) et le Common Store (SRP) en utilisant différentes collections.
uuid: 7356343d-073c-4266-bdcb-c7e999281476
contentOwner: Janice Kendall
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: administering
content-type: reference
discoiquuid: e228f1db-91ea-4ec3-86da-06d89d74bc72
translation-type: tm+mt
source-git-commit: 94bc3550a7e18b9203e7a0d495d195d7b798e012
workflow-type: tm+mt
source-wordcount: '1483'
ht-degree: 2%

---


# Configuration Solr pour SRP {#solr-configuration-for-srp}

## Solr pour la plateforme AEM {#solr-for-aem-platform}

Une installation [Apache Solr](https://lucene.apache.org/solr/) peut être partagée entre [Node store](../../help/sites-deploying/data-store-config.md) (Oak) et [common store](working-with-srp.md) (SRP) en utilisant différentes collections.

Si les deux collections Oak et SRP sont utilisées de façon intensive, un second Solr peut être installé pour des raisons de performances.

Pour les environnements de production, le [mode SolrCloud](#solrcloud-mode) offre de meilleures performances par rapport au mode autonome (une seule configuration Solr locale).

### Conditions préalables {#requirements}

Téléchargez et installez Apache Solr :

* [Version 7.0](https://archive.apache.org/dist/lucene/solr/7.0.0/)

* Le serveur requiert Java 1.7 ou version ultérieure
* Aucun service requis
* Choix des modes d&#39;exécution :

   * Mode autonome
   * [Mode](#solrcloud-mode)  SolrCloud (recommandé pour les environnements de production)

* Choix de la recherche multilingue (MLS)

   * [Installation de MLS standard](#installing-standard-mls)
   * [Installation de MLS avancé](#installing-advanced-mls)

## Mode SolrCloud {#solrcloud-mode}

[](https://cwiki.apache.org/confluence/display/solr/SolrCloud) SolrCloudmode est recommandé pour les environnements de production. Lors de l’exécution en mode SolrCloud, SolrCloud doit être installé et configuré avant d’installer la recherche multilingue (MLS).

Il est recommandé de suivre les instructions d’installation de SolrCloud :

* 3 noeuds SolrCloud sur le même serveur.
* Un ZooKeeper Apache externe.

Il est également recommandé de configurer la JVM pour régler l’utilisation de la mémoire et la collecte des déchets.

### Exemple de configuration JVM {#jvm-configuration-example}

```shell
JVM_OPTS="-server -Xmx2048m -XX:MaxPermSize=768M -XX:+UseConcMarkSweepGC -XX:+CMSClassUnloadingEnabled -Xloggc:../logs/gc.log -XX:+PrintGCDetails -XX:+PrintGCDateStamps -Djava.awt.headless=true"
```

### Commandes de configuration de SolrCloud {#solrcloud-setup-commands}

Lors de l’exécution en mode SolrCloud, avant l’installation de MLS, il est nécessaire d’utiliser et de connaître les commandes de configuration suivantes de SolrCloud.

#### 1. Téléchargez une configuration sur ZooKeeper {#upload-a-configuration-to-zookeeper}

Référence :
[https://cwiki.apache.org/confluence/display/solr/Command+Line+Utilities](https://cwiki.apache.org/confluence/display/solr/Command+Line+Utilities)

Utilisation :
sh ./scripts/cloud-scripts/zkcli.sh \
-cmd upconfig \
-zkhost *server:port* \
-confname *myconfig-name *\
-solrhome *solr-home-path* \
-confdir *config-dir*

#### 2. Créez une collection {#create-a-collection}

Référence :
[https://cwiki.apache.org/confluence/display/solr/Solr+Start+Script+Reference#SolrStartScriptReference-Create](https://cwiki.apache.org/confluence/display/solr/Solr+Start+Script+Reference#SolrStartScriptReference-Create)

Utilisation:
./bin/solr create \
-c *nom_collection*\
-d *config-dir* \
-n *nom_myconfig* \
-p *port*\
-s *nombre de shards* \
-rf *nombre de réplicas*

#### 3. Liez une collection à un jeu de configuration {#link-a-collection-to-a-configuration-set}

Liez une collection à une configuration déjà téléchargée sur ZooKeeper.

Référence :
[https://cwiki.apache.org/confluence/display/solr/Command+Line+Utilities](https://cwiki.apache.org/confluence/display/solr/Command+Line+Utilities)

Utilisation :
sh ./scripts/cloud-scripts/zkcli.sh \
-cmd linkconfig \
-zkhost *server:port* \
-collection *nom_collection_mycollection* \
-confname *nom_config*

### Comparaison des MLS standard et avancés {#comparison-of-standard-and-advanced-mls}

La recherche multilingue (MLS) pour l’AEM Communities est conçue pour la plate-forme Solr afin de fournir une recherche améliorée dans toutes les langues prises en charge, y compris l’anglais.

MLS pour les communautés AEM est disponible en tant que MLS standard ou MLS avancé. Standard MLS inclut uniquement les paramètres de configuration Solr et exclut tous les modules externes ou fichiers de ressources. Advanced MLS est la solution la plus complète et inclut des paramètres de configuration Solr ainsi que des modules externes et les ressources connexes.

Standard MLS inclut des améliorations pour la recherche de contenu dans les langues suivantes :

* Anglais : Amélioration de l&#39;horodateur pour tenter de faire correspondre les dérivations de mot.
* Japonais : Amélioration de la création de jetons japonais pour les caractères demi-largeur.

MLS avancé comprend des améliorations pour la recherche de contenu dans les langues suivantes :

* Anglais : Remplacement du tige par un lemmatiseur.
* Allemand : Décompresseur Ajouté.
* Français : Manipulation d’une décision Ajoutée.
* Chinois (simplifié) : Ajouté un jetizer plus intelligent.
* Différentes langues : Ajouté un vermifuge, une liste de mots-clés et un banaliseur.

Au total, les 33 langues suivantes sont prises en charge dans Advanced MLS.

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

#### Comparaison de l&#39;AEM 6.1 Solr search, Standard MLS et Advanced MLS {#comparison-of-aem-solr-search-standard-mls-and-advanced-mls}

**Remarque** : AEM 6.1 se rapporte à AEM 6.1 Communautés FP3 et versions antérieures.

![compare-solr-mls](assets/compare-solr-mls.png)

### Installation du MLS standard {#installing-standard-mls}

Pour la collection SRP (MSRP ou DSRP), pour prendre en charge la recherche multilingue standard (MLS), il est nécessaire de modifier deux des fichiers de configuration de Solr :

* **schéma.xml**
* **solrconfig.xml**

Fichiers MLS standard (schéma.xml, solrconfig.xml) pour Solaris 4.10.

Fichiers MLS standard (schéma.xml, solrconfig.xml) pour Solaris 5.x.

Les fichiers MLS standard sont stockés dans le référentiel AEM.

**Remarque** : Bien que les fichiers Solr soient stockés dans le dossier msrp/, ils sont également pour DSRP (aucune modification nécessaire).

**Télécharger les instructions** : Remplacez  `solrX` par  `solr4` ou  `solr5` selon le cas.

1. A l&#39;aide de CRXDE|Lite, recherchez :

   * `/libs/social/config/datastore/msrp/solrX/schema.xml`
   * `/libs/social/config/datastore/msrp/solrX/solrconfig.xml`

1. Téléchargez sur le serveur local sur lequel Solr est déployé.

   * Localisez la propriété `jcr:content` du noeud `jcr:data`.
   * Sélectionnez `view` pour début le téléchargement.
   * Assurez-vous que les fichiers sont enregistrés avec les noms et le codage appropriés (UTF8).

1. Suivez les instructions d’installation pour le mode autonome ou SolrCloud.

#### Mode SolrCloud - MLS standard {#solrcloud-mode-standard-mls}

1. Installez et configurez Solr en mode SolrCloud.
1. Préparer une nouvelle configuration :

   1. Créez new-config-dir* comme `solr-install-dir*/myconfig/`

   1. Copiez le contenu du répertoire de configuration Solr existant dans *new-config-dir*.

      * Pour Solr4 : copy `solr-install-dir/example/solr/collection1/conf/`
      * Pour Solr5 : copy `solr-install-dir/server/solr/configsets/data_driven_schema_configs/`
   1. Copiez les **schéma.xml** et **solrconfig.xml** téléchargés dans *new-config-dir* pour remplacer les fichiers existants.


1. [Téléchargez la nouvelle ](#upload-a-configuration-to-zookeeper) configuration sur ZooKeeper.
1. [Créez une ](#create-a-collection) collection spécifiant les paramètres nécessaires, tels que le nombre de shards, le nombre de réplicas et le nom de configuration.
1. Si le nom de la configuration n’était *pas *fourni lors de la création de la collection, [liez cette nouvelle collection](#link-a-collection-to-a-configuration-set) avec la configuration téléchargée sur ZooKeeper.

1. Pour MSRP, exécutez [MSRP Reindex Tool](msrp.md#msrp-reindex-tool), sauf s&#39;il s&#39;agit d&#39;une nouvelle installation.

#### Mode autonome - MLS standard {#standalone-mode-standard-mls}

1. Installez Solr en mode autonome.
1. Si vous exécutez Solr5, créez une collection1 (semblable à Solr4) :

   * `./bin/solr start`
   * `./bin/solr create_core -c collection1 -d sample_techproducts_configs`

1. Sauvegardez **schéma.xml** et **solrconfig.xml** dans le répertoire de configuration Solr, par exemple :

   * Pour Solr4 : `solr-install-dir/example/solr/collection1/conf/`
   * Créé pour Solr5 : `solr-install-dir/server/solr/collection1/conf/`

1. Copiez les **schéma.xml** et **solrconfig.xml** téléchargés dans ce même répertoire.

1. Redémarrez Solr.
1. Pour MSRP, exécutez [MSRP Reindex Tool](#msrpreindextool), sauf s&#39;il s&#39;agit d&#39;une nouvelle installation.

### Installation de MLS avancé {#installing-advanced-mls}

Pour que la collection SRP (MSRP ou DSRP) prenne en charge les MLS avancés, de nouveaux modules externes Solr sont requis en plus d&#39;un schéma personnalisé et d&#39;une configuration Solr. Tous les éléments requis sont compressés dans un fichier zip téléchargeable. En outre, un script d’installation est inclus pour une utilisation lorsque Solr est déployé en mode autonome.

Pour obtenir le package MLS avancé, voir [AEM Advanced MLS](deploy-communities.md#aem-advanced-mls) dans la section déploiement de la documentation.

Pour commencer l’installation en mode SolrCloud ou autonome :

* Téléchargez AEM-SOLR-MLS archive zip sur le serveur hébergeant Solr.
* Décompressez l&#39;archive.

#### Mode SolrCloud - MLS avancé {#solrcloud-mode-advanced-mls}

Instructions d&#39;installation - Notez les quelques différences pour Solr4 et Solr5 :

1. Installez et configurez Solr en mode SolrCloud.
1. Extrayez le contenu du package Advanced MLS sur le disque. Le contenu doit inclure :

   * **schéma.xml**
   * **solrconfig.xml**
   * **mot de passe/** dossier
   * **profils/** dossier
   * **extra-libs/** dossier

1. Préparer une nouvelle configuration :

   1. Créer *new-config-dir*

      * Par exemple, `solr-install-dir/myconfig/`
      * Créer des sous-dossiers `stopwords/` et `lang/`
   1. Copiez le contenu du répertoire de configuration Solr existant dans *new-config-dir*.

      * Pour Solr4 : Copier `solr-install-dir/example/solr/collection1/conf/`
      * Pour Solr5 : Copier `solr-install-dir/server/solr/configsets/data_driven_schema_configs/`
   1. Copiez les **schéma.xml** et **solrconfig.xml** extraits dans *new-config-dir* pour remplacer les fichiers existants.
   1. Pour Solr5 : Copier `solr_install_dir/server/solr/configsets/sample_techproducts_configs/conf/lang/*.txt` dans `new-config-dir/lang/`
   1. Copiez le dossier **stopwords/** extrait dans *new-config-dir*, ce qui donne `new-config-dir/stopwords/*.txt`



1. [Téléchargement de la nouvelle ](#upload-a-configuration-to-zookeeper) configuration vers ZooKeeper
1. Copiez le nouveau dossier **profils/**...

   * Pour Solr4 : Copier dans les ressources/dossiers de chaque noeud
   * Pour Solr5 : Copiez dans le dossier server/resources/ de chaque installation Solr. Si tous les noeuds se trouvent dans le même répertoire d’installation Solr, cette étape n’est effectuée qu’une seule fois.

1. Créez un dossier **lib/** dans le répertoire solr-home (contient solr.xml) de chaque noeud dans SolrCloud. Copiez les fichiers JAR des emplacements suivants dans le nouveau dossier lib/ de chaque noeud :

   * **Extralibs/** extrait du package MLS avancé
   * *rép_installation_solr/contrib/extraction/lib/*.jar
   * *solr-install-dir/dist/solr-cell*.jar
   * *rép_installation_solr/contrib/clustering/lib/*.jar
   * *solr-install-dir/dist/solr-clustering*.jar
   * *solr-install-dir/contrib/langid/lib/*.jar
   * *solr-install-dir/dist/solr-langid*.jar
   * *rép_installation_solr/contrib/velocity/lib/*.jar
   * *solr-install-dir/dist/solr-velocity*.jar
   * *solr-install-dir/contrib/analyse-extras/lib/*.jar
   * *solr-install-dir/contrib/analyse-extras/lucene-libs/*.jar

1. [Créez une ](#create-a-collection) collection spécifiant les paramètres nécessaires, tels que le nombre de shards, le nombre de réplicas et le nom de configuration.
1. Si le nom de configuration *n&#39;était pas* fourni lors de la création de la collection, [liez cette nouvelle collection](#link-a-collection-to-a-configuration-set) avec la configuration téléchargée sur ZooKeeper.

1. Pour MSRP, exécutez [MSRP Reindex Tool](#msrpreindextool), sauf s&#39;il s&#39;agit d&#39;une nouvelle installation.

#### Mode autonome - MLS avancé {#standalone-mode-advanced-mls}

Un script d’installation est inclus dans le package MLS avancé.

Après avoir extrait le contenu du package sur le serveur hébergeant le serveur Solr autonome, exécutez simplement le script d&#39;installation afin d&#39;installer les ressources et les fichiers de configuration nécessaires.

* Installez Solr en mode autonome.
* Si vous exécutez Solr5, créez une collection1 (semblable à Solr4) :

   * `./bin/solr start`
   * `./bin/solr create_core -c collection1 -d sample_techproducts_configs`

* Exécutez le script d’installation : Installer [-v 4|5] [-d solrhome] [-c collectionpath]
où :

   * -d solrhome

      Répertoire d’installation Solr

   * -c collectionpath

      Chemin de collecte en solitaire

   * --help

      Imprimer les options de ligne de commande

   * -v [4|5]

      Définition de la version pour solr

* Exemple pour Solr 4.10.4 :

   * Install.bat -v 4 -d c:/solr-4.10.4 -c:/solr-4.10.4/example/solr/collection1

* Exemple pour Solr 5.4.0 :

   * Install.sh -v 5 -d /tmp/solr-5.4.0 -c /tmp/solr-5.4.0/server/solr/collection1

**Remarque** :

* Le script d’installation sauvegardera schéma.xml et solrconfig.xml avant d’installer de nouvelles versions en ajoutant &quot;.orig&quot;

### À propos de solrconfig.xml {#about-solrconfig-xml}

Le fichier **solrconfig.xml** contrôle l’intervalle de validation automatique et la visibilité de la recherche et nécessite des tests et des réglages.

`<autoCommit>`: Par défaut, l’intervalle de validation automatique, qui est une validation difficile à un enregistrement stable, est défini sur 15 secondes. La visibilité de la recherche utilise par défaut l’index de pré-validation.

Pour modifier la recherche pour utiliser un index mis à jour afin de refléter les modifications dues à la validation, définissez `openSearcher` contenu sur true.

`autoSoftCommit`: Une validation &quot;soft&quot; garantit que les modifications sont visibles (l&#39;index est mis à jour), mais ne garantit pas que les modifications sont synchronisées avec un enregistrement stable (hard commit). Il en résulte une amélioration des performances. Par défaut, `autoSoftCommit` est désactivé et `maxTime` contenu est défini sur -1.
