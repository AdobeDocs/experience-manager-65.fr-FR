---
title: Directives de performance
description: Cet article fournit des directives générales sur l’optimisation de la performance de votre déploiement AEM.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: configuring
feature: Configuring
exl-id: 5a305a5b-0c3d-413b-88c1-1f5abf7e1579
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '2935'
ht-degree: 99%

---

# Directives de performance{#performance-guidelines}

Cet page fournit des directives générales sur l’optimisation de la performance de votre déploiement AEM. Si vous débutez avec AEM, consultez les pages suivantes avant de commencer à lire les directives de performance :

* [Concepts de base d’AEM](/help/sites-deploying/deploy.md#basic-concepts)
* [Présentation du stockage dans AEM](/help/sites-deploying/storage-elements-in-aem-6.md#overview-of-storage-in-aem)
* [Déploiements recommandés](/help/sites-deploying/recommended-deploys.md)
* [Exigences techniques](/help/sites-deploying/technical-requirements.md)

Les options de déploiement disponibles dans AEM sont illustrées ci-dessous (faites défiler l’écran pour afficher toutes les options) :

<table>
 <tbody>
  <tr>
   <td><p><strong>AEM</strong></p> <p><strong>Produit</strong></p> </td>
   <td><p><strong>Topologie</strong></p> </td>
   <td><p><strong>Système d’exploitation</strong></p> </td>
   <td><p><strong>Serveur d’applications</strong></p> </td>
   <td><p><strong>JRE</strong></p> </td>
   <td><p><strong>Sécurité</strong></p> </td>
   <td><p><strong>Micronoyau</strong></p> </td>
   <td><p><strong>Magasin de données</strong></p> </td>
   <td><p><strong>Indexation</strong></p> </td>
   <td><p><strong>Serveur web</strong></p> </td>
   <td><p><strong>Navigateur</strong></p> </td>
   <td><p><strong>Experience Cloud</strong></p> </td>
  </tr>
  <tr>
   <td><p>Sites</p> </td>
   <td><p>Non-HA</p> </td>
   <td><p>Windows</p> </td>
   <td><p>CQSE</p> </td>
   <td><p>Oracle</p> </td>
   <td><p>LDAP</p> </td>
   <td><p>TAR</p> </td>
   <td><p>Segment</p> </td>
   <td><p>Propriété</p> </td>
   <td><p>Apache</p> </td>
   <td><p>Edge</p> </td>
   <td><p>Target</p> </td>
  </tr>
  <tr>
   <td><p>Assets</p> </td>
   <td><p>Publish-HA</p> </td>
   <td><p>Solaris™</p> </td>
   <td><p>WebLogic</p> </td>
   <td><p>IBM®</p> </td>
   <td><p>SAML</p> </td>
   <td><p>MongoDB</p> </td>
   <td><p>File</p> </td>
   <td><p>Lucene</p> </td>
   <td><p>IIS</p> </td>
   <td><p>IE</p> </td>
   <td><p>Analyses</p> </td>
  </tr>
  <tr>
   <td><p>Communities</p> </td>
   <td><p>Author-CS</p> </td>
   <td><p>Red Hat®</p> </td>
   <td><p>WebSphere®</p> </td>
   <td><p>HP</p> </td>
   <td><p>Oauth</p> </td>
   <td><p>RDB/Oracle</p> </td>
   <td><p>S3/Azure</p> </td>
   <td><p>Solr</p> </td>
   <td><p>iPlanet</p> </td>
   <td><p>Firefox</p> </td>
   <td><p>Campaign</p> </td>
  </tr>
  <tr>
   <td><p>Forms</p> </td>
   <td><p>Author-Offload</p> </td>
   <td><p>HP-UX</p> </td>
   <td><p>Tomcat</p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p>RDB/DB2</p> </td>
   <td><p>MongoDB</p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p>Chrome</p> </td>
   <td><p>Social</p> </td>
  </tr>
  <tr>
   <td><p>Mobile</p> </td>
   <td><p>Author-Cluster</p> </td>
   <td><p>IBM® AIX®</p> </td>
   <td><p>JBoss®</p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p>RDB/MySQL</p> </td>
   <td><p>RDBMS</p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p>Safari</p> </td>
   <td><p>Audience</p> </td>
  </tr>
  <tr>
   <td><p>Multi-site</p> </td>
   <td><p>ASRP</p> </td>
   <td><p>SUSE®</p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p>RDB/SQLServer</p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p>Assets</p> </td>
  </tr>
  <tr>
   <td><p>Commerce</p> </td>
   <td><p>MSRP</p> </td>
   <td><p>Apple OS</p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p>Activation</p> </td>
  </tr>
  <tr>
   <td><p>Dynamic Media</p> </td>
   <td><p>JSRP</p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p>Mobile</p> </td>
  </tr>
  <tr>
   <td><p>Brand Portal</p> </td>
   <td><p>J2E</p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
  </tr>
  <tr>
   <td><p>AoD</p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
  </tr>
  <tr>
   <td><p>LiveFyre</p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
  </tr>
  <tr>
   <td><p>Screens</p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
  </tr>
  <tr>
   <td><p>Sécurité des documents</p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
  </tr>
  <tr>
   <td><p>Gestion des processus</p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
  </tr>
  <tr>
   <td><p>appli de bureau</p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
   <td><p> </p> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>Les directives de performance s’appliquent principalement à AEM Sites.

## Quand utiliser les directives de performance {#when-to-use-the-performance-guidelines}

Suivez les directives de performance dans les cas suivants :

* **Premier déploiement** : lorsque vous envisagez de déployer AEM Sites ou Assets pour la première fois, il est important de bien comprendre les options disponibles. Surtout pour la configuration du micronoyau, du magasin de nœuds et du magasin de données (par rapport aux paramètres par défaut). Vous pouvez par exemple modifier les paramètres par défaut du magasin de données pour TarMK en magasin de données de fichiers.
* **Mise à niveau vers une nouvelle version** : lors de la mise à niveau vers une nouvelle version, il est important de comprendre les différences de performance par rapport à l’environnement en cours d’exécution. Il s’agit par exemple de la mise à niveau d’AEM 6.1 vers 6.2 ou d’AEM 6.0 CRX2 vers 6.2 OAK.
* **Temps de réponse lent** : lorsque l’architecture Nodestore sélectionnée ne répond pas à vos besoins, il est important de comprendre les différences de performance par rapport aux autres options de topologie. Il s’agit par exemple du déploiement de TarMK au lieu de MongoMK ou de l’utilisation d’un magasin de données de fichiers au lieu d’un magasin de données Amazon S3 ou Microsoft® Azure.
* **Ajout d’autres auteurs et autrices** : lorsque la topologie TarMK recommandée ne répond pas aux exigences de performance et que la mise à niveau du nœud d’instance de création a atteint la capacité maximale disponible, comprenez bien les différences de performance. Comparez l’utilisation de MongoMK avec trois nœuds d’instance de création ou plus. Par exemple, le déploiement de MongoMK au lieu de TarMK.
* **Ajouter plus de contenu**: lorsque l’architecture de l’entrepôt de données recommandée ne répond pas à vos besoins, il est important de comprendre les différences de performances par rapport aux autres options de l’entrepôt de données. Exemple : utilisation du magasin de données Amazon S3 ou Microsoft® Azure au lieu d’un magasin de données de fichiers.

## Présentation {#introduction}

Ce chapitre propose une vue d’ensemble de l’architecture d’AEM et de ses composants les plus importants. Il fournit également des directives de développement et décrit les scénarios de test utilisés dans les tests de référence TarMK et MongoMK.

### La plateforme AEM {#the-aem-platform}

La plateforme AEM comprend les composants suivants :

![chlimage_1](assets/chlimage_1a.png)

Pour plus d’informations sur la plateforme AEM, reportez-vous à la section [Qu’est-ce qu’AEM ?](/help/sites-deploying/deploy.md#what-is-aem).

### L’architecture d’AEM {#the-aem-architecture}

Un déploiement d’AEM comporte trois blocs de création importants. L’**instance de création** qui est utilisée par les personnes qui créent, éditent et approuvent du contenu pour produire et réviser du contenu. Lorsque le contenu est validé, il est publié sur un second type d’instance nommé **instance de publication** à partir de laquelle les personnes utilisatrices finales y accèdent. Le troisième composant clé est le **Dispatcher**, qui est un module chargé de la mise en mémoire cache et du filtrage des URL. Il est installé sur le serveur web. Pour plus d’informations sur l’architecture d’AEM, consultez les [Scénarios de déploiement classiques](/help/sites-deploying/deploy.md#typical-deployment-scenarios).

![chlimage_1-1](assets/chlimage_1-1a.png)

### Micronoyaux {#micro-kernels}

Les micronoyaux agissent comme des gestionnaires de persistance dans AEM. Il existe trois types de micronoyaux utilisés par AEM : TarMK, MongoDB et la base de données relationnelle (prise en charge limitée). Le choix d’une solution adaptée à vos besoins dépend de l’objectif de votre instance et du type de déploiement que vous prévoyez. Pour plus d’informations sur les micronoyaux, consultez la page [Déploiements recommandés](/help/sites-deploying/recommended-deploys.md).

![chlimage_1-2](assets/chlimage_1-2a.png)

### Entrepôt de nœuds {#nodestore}

Dans AEM, les données binaires peuvent être stockées indépendamment des nœuds de contenu. L’emplacement de stockage des données binaires est désigné sous le nom de **magasin de données**, tandis que l’emplacement des nœuds de contenu et des propriétés est nommé **magasin de nœuds**.

>[!NOTE]
>
>Adobe recommande TarMK comme technologie de persistance par défaut à utiliser par la clientèle pour les instances de création et de publication d’AEM.

>[!CAUTION]
>
>Le micronoyau de la base de données relationnelle est pris en charge de manière limitée. Contactez l’[assistance clientèle d’Adobe](https://experienceleague.adobe.com/?support-solution=General&amp;lang=fr&amp;support-tab=home#support) avant d’utiliser ce type de micronoyau.

![chlimage_1-3](assets/chlimage_1-3a.png)

### Magasin de données {#data-store}

Lorsque vous traitez un grand nombre de fichiers binaires, il est recommandé d’utiliser un magasin de données externe au lieu du magasin de nœuds par défaut pour optimiser la performance. Par exemple, si votre projet nécessite un grand nombre de ressources multimédias, leur stockage dans le magasin de données de fichiers ou Azure/S3 rendra leur accès plus rapide que leur stockage direct dans une base de données MongoDB.

Pour plus de détails sur les options de configuration disponibles, consultez la section [Configuration de magasins de nœuds et de magasins de données](/help/sites-deploying/data-store-config.md).

>[!NOTE]
>
>Adobe vous recommande de choisir l’option de déploiement d’AEM sur Azure ou Amazon Web Services (AWS) à l’aide d’Adobe Managed Services. Les clientes et clients bénéficient d’une équipe qui dispose de l’expérience et des compétences nécessaires pour déployer et exploiter AEM dans ces environnements de cloud computing. Consultez les [documents complémentaires sur Adobe Managed Services](https://business.adobe.com/fr/products/experience-manager/managed-services.html?aemClk=t).
>
>Pour obtenir des recommandations sur le déploiement d’AEM sur Azure ou AWS, en dehors d’Adobe Managed Services, Adobe recommande de travailler directement avec le fournisseur de cloud. Vous pouvez également collaborer avec l’un des partenaires d’Adobe qui prend en charge le déploiement d’AEM dans l’environnement cloud de votre choix. Le fournisseur ou partenaire cloud sélectionné est responsable du dimensionnement, de la conception et de l’implémentation de l’architecture qu’ils prennent en charge pour répondre à vos besoins spécifiques en termes de performances, de charge, d’évolutivité et de sécurité.
>
>>Consultez également la page des [exigences techniques](/help/sites-deploying/technical-requirements.md#supported-platforms).

### Rechercher {#search-features}

Les fournisseurs d’index personnalisés utilisés avec AEM sont répertoriés dans cette section. Pour en savoir plus sur l’indexation, consultez la section [Requêtes Oak et indexation](/help/sites-deploying/queries-and-indexing.md).

>[!NOTE]
>
>Adobe recommande d’utiliser l’index Lucene dans la plupart des déploiements. Solr est réservé aux déploiements spécialisés et complexes qui demandent de l’évolutivité.

![chlimage_1-4](assets/chlimage_1-4a.png)

### Conseils de développement {#development-guidelines}

Développez pour AEM et optimisez les **performances et l’évolutivité**. Vous trouverez ci-dessous quelques bonnes pratiques :

**Bonnes pratiques**

* Faites une distinction entre la présentation, la logique et le contenu.
* Utilisez les API d’AEM (Sling etc.) et les outils (la réplication, par exemple) à votre disposition.
* Développez dans le contexte du contenu réel.
* Développez avec une mise en cache optimale en ligne de mire.
* Réduisez le nombre d’enregistrements (par exemple, en utilisant des workflows transitoires).
* Assurez-vous que tous les points d’entrée HTTP sont RESTful.
* Limitez la portée de l’observation JCR.
* Gardez à l’esprit les threads asynchrones.

**Mauvaises pratiques**

* N’utilisez pas directement les API JCR, si possible.
* Ne modifiez pas les répertoires /libs, mais utilisez plutôt des recouvrements.
* N’utilisez pas de requêtes dans la mesure du possible.
* N’utilisez pas de liaisons Sling pour obtenir des services OSGi dans le code Java™, mais utilisez plutôt :

   * @Reference dans un composant DS ;
   * @Inject dans un modèle Sling ;
   * sling.getService() dans une classe d’utilisation Sightly ;
   * sling.getService() dans un JSP ;
   * un ServiceTracker ;
   * un accès direct au registre du service OSGi.

Pour plus d’informations sur le développement sur AEM, consultez la section [Principes de base du développement](/help/sites-developing/the-basics.md). Pour consulter d’autres bonnes pratiques, rendez-vous sur [Bonnes pratiques en matière de développement](/help/sites-developing/best-practices.md).

### Scénarios de référence {#benchmark-scenarios}

>[!NOTE]
>
>Les tests présentés sur cette page ont été réalisés dans un environnement de laboratoire.

Les scénarios de test présentés ci-dessous sont utilisés pour les sections de référence des chapitres TarMK, MongoMk et TarMK contre MongoMk. Pour identifier le scénario qui a été utilisé pour un test comparatif particulier, consultez le champ de scénario du tableau [Caractéristiques techniques](/help/sites-deploying/performance-guidelines.md#tarmk-performance-benchmark).

**Scénario de produit unique**

AEM Assets :

* Interactions utilisateur : parcourir les ressources / rechercher des ressources / télécharger la ressource / lire les métadonnées de la ressource / mettre à jour les métadonnées de la ressource / télécharger la ressource / exécuter le workflow Télécharger la ressource.
* Mode d’exécution : utilisateurs et utilisatrices simultanés, une seule interaction par personne.

**Scénario de produits mixtes**

AEM Sites + AEM Assets :

* Interactions utilisateur de Sites : lire une page d’article / lire une page / créer un paragraphe / modifier le paragraphe / créer une page de contenu / activer la page de contenu / créer une recherche.
* Interactions utilisateur d’Assets : parcourir les ressources / rechercher des ressources / télécharger la ressource / lire les métadonnées de la ressource / mettre à jour les métadonnées de la ressource / télécharger la ressource / exécuter le workflow Télécharger la ressource.
* Mode d’exécution : utilisateurs et utilisatrices simultanés, interactions mixtes par personne.

**Scénario de cas d’utilisation vertical**

Média :

* `Read Article Page (27.4%), Read Page (10.9%), Create Session (2.6%), Activate Content Page (1.7%), Create Content Page (0.4%), Create Paragraph (4.3%), Edit Paragraph (0.9%), Image Component (0.9%), Browse Assets (20%), Read Asset Metadata (8.5%), Download Asset (4.2%), Search Asset (0.2%), Update Asset Metadata (2.4%), Upload Asset (1.2%), Browse Project (4.9%), Read Project (6.6%), Project Add Asset (1.2%), Project Add Site (1.2%), Create Project (0.1%), Author Search (0.4%)`
* Mode d’exécution : utilisateurs et utilisatrices simultanés, interactions mixtes par personne.

## TarMK {#tarmk}

Ce chapitre donne des recommandations pour tirer le meilleur parti des performances de TarMK. Vous y trouverez les exigences minimales en matière d’architecture et la configuration des paramètres. Des tests de référence sont également fournis pour plus de clarté.

Adobe recommande TarMK comme technologie de persistance par défaut à utiliser par les client(e)s dans tous les scénarios de déploiement, pour les instances d’auteur et de publication AEM.

Pour plus d’informations sur TarMK, consultez les [Scénarios de déploiement](/help/sites-deploying/recommended-deploys.md#deployment-scenarios) et la section [Stockage Tar](/help/sites-deploying/storage-elements-in-aem-6.md#tar-storage).

### Recommandations sur l’architecture minimale de TarMK {#tarmk-minimum-architecture-guidelines}

>[!NOTE]
>
>Les recommandations relatives à l’architecture minimale présentées ci-dessous concernent les environnements de production et les sites à trafic élevé. Ces recommandations ne sont **pas** les [spécifications minimales](/help/sites-deploying/technical-requirements.md#prerequisites) requises pour exécuter AEM.

Pour obtenir de bonnes performances lors de l’utilisation de TarMK, commencez par l’architecture suivante :

* une instance de création ;
* deux instances de publication ;
* deux Dispatchers.

Vous trouverez, dans l’exemple ci-dessous, les recommandations sur l’architecture d’AEM Sites et AEM Assets.

>[!NOTE]
>
>La réplication sans binaires doit être **ACTIVÉE** si le magasin de données du fichier est partagé.

**Recommandations sur l’architecture Tar pour AEM Sites**

![chlimage_1-5](assets/chlimage_1-5a.png)

**Conseils d’architecture Tar pour AEM Assets**

![chlimage_1-6](assets/chlimage_1-6a.png)

### Paramètres TarMK recommandés {#tarmk-settings-guideline}

Pour obtenir de bonnes performances, il est recommandé de définir les paramètres comme suit. Pour obtenir des instructions sur la modification des paramètres, [reportez-vous à cette page](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/configuring/configuring-performance.html?lang=fr).

<table>
 <tbody>
  <tr>
   <td><strong>Configuration</strong></td>
   <td><strong>Paramètre</strong></td>
   <td><strong>Valeur </strong></td>
   <td><strong>Description</strong></td>
  </tr>
  <tr>
   <td>Files d’attente des tâches Sling</td>
   <td><code>queue.maxparallel</code></td>
   <td>Définissez la valeur sur la moitié du nombre de cœurs de processeur. </td>
   <td>Par défaut, le nombre de threads simultanés par file d’attente de tâche est égal au nombre de cœurs du processeur.</td>
  </tr>
  <tr>
   <td>File d’attente du workflow transitoire Granite</td>
   <td><code>Max Parallel</code></td>
   <td>Définissez la valeur sur la moitié du nombre de cœurs de processeur.</td>
   <td> </td>
  </tr>
  <tr>
   <td>Paramètres JVM</td>
   <td><p><code>Doak.queryLimitInMemory</code></p> <p><code>Doak.queryLimitReads</code></p> <p><code>Dupdate.limit</code></p> <p><code>Doak.fastQuerySize</code></p> </td>
   <td><p>500000</p> <p>100000</p> <p>250000</p> <p>True</p> </td>
   <td>Pour empêcher les requêtes volumineuses de surcharger les systèmes, ajoutez les paramètres JVM suivants dans le script de démarrage d’AEM.</td>
  </tr>
  <tr>
   <td>Configuration de l’index Lucene</td>
   <td><p><code>CopyOnRead</code></p> <p><code>CopyOnWrite</code></p> <p><code>Prefetch Index Files</code></p> </td>
   <td><p>Activé</p> <p>Activé</p> <p>Activé</p> </td>
   <td>Pour plus d’informations sur les paramètres disponibles, rendez-vous sur <a href="https://jackrabbit.apache.org/oak/docs/query/lucene.html">cette page</a>.</td>
  </tr>
  <tr>
   <td>Magasin de données = Magasin de données S3</td>
   <td><p><code>maxCachedBinarySize</code></p> <p><code>cacheSizeInMB</code></p> </td>
   <td><p>1 048 576 (1 Mo) ou plus petit</p> <p>2 à 10 % de la taille maximale du tas</p> </td>
   <td>Consultez également les <a href="/help/sites-deploying/data-store-config.md#data-store-configurations">configurations du magasin de données</a>.</td>
  </tr>
  <tr>
   <td>Workflow Ressource de mise à jour de la gestion des DAM</td>
   <td><code>Transient Workflow</code></td>
   <td>vérifié</td>
   <td>Ce processus gère la mise à jour des ressources.</td>
  </tr>
  <tr>
   <td>Écriture différée des métadonnées de gestion des DAM</td>
   <td><code>Transient Workflow</code></td>
   <td>vérifié</td>
   <td>Ce workflow gère l’écriture différée XMP au format binaire d’origine et définit la date de la dernière modification dans JCR.</td>
  </tr>
 </tbody>
</table>

### Référence des performances de TarMK {#tarmk-performance-benchmark}

#### Spécifications techniques {#technical-specifications}

Les tests comparatifs ont été réalisés selon les spécifications suivantes :

| | **Nœud Auteur** |
|---|---|
| Serveur | Matériel « métal nu » (HP) |
| Système d’exploitation | Red Hat® Linux® |
| Processeur / Cœurs | Processeur Intel(R) Xeon(R) E5-2407 @2,40 GHz, 8 cœurs |
| Mémoire RAM | 32 Go |
| Disque | Magnétique |
| Java™ | Oracle JRE version 8 |
| JVM Heap | 16 Go |
| Produit | AEM 6.2 |
| Entrepôt de nœuds | TarMK |
| Magasin de données | File DS |
| Scénario | Produit unique : Assets / 30 threads simultanés |

#### Résultats de l’évaluation des performances {#performance-benchmark-results}

>[!NOTE]
>
>Les chiffres présentés ci-dessous ont été normalisés à 1 comme référence et ne sont pas les chiffres de débit réels.

![chlimage_1-7](assets/chlimage_1-7a.png) ![chlimage_1-8](assets/chlimage_1-8a.png)

## MongoMK {#mongomk}

La principale raison pour choisir le serveur principal de persistance MongoMK plutôt que TarMK est de mettre les instances à l’échelle horizontale. Ainsi, au moins deux instances de création actives fonctionnent en permanence et MongoDB est utilisé comme système de stockage de persistance. La nécessité d’exécuter plusieurs instances de création est due au fait que la capacité du processeur et de la mémoire d’un seul serveur, prenant en charge toutes les activités de création simultanées, n’est plus suffisante.

Pour plus d’informations sur TarMK, consultez les [Scénarios de déploiement](/help/sites-deploying/recommended-deploys.md#deployment-scenarios) et la section [Stockage Mongo](/help/sites-deploying/storage-elements-in-aem-6.md#mongo-storage).

### Rrecommandations sur l’architecture minimale de MongoMK {#mongomk-minimum-architecture-guidelines}

Pour tirer le meilleur parti des performances de MongoMK, commencez par l’artchitecture suivante :

* trois instances de création ;
* deux instances de publication ;
* trois instances MongoDB ;
* deux Dispatchers.

>[!NOTE]
>
>Dans les environnements de production, MongoDB est toujours utilisé comme ensemble de répliques avec une instance principale et deux instances secondaires. L’instance principale gère les tâches de lecture et d’écriture, tandis que les instances secondaires peuvent s’occuper des opérations de lecture. Si le stockage n’est pas disponible, l’une des instances secondaires peut être remplacée par un arbitre, mais les ensembles de répliques de MongoDB doivent toujours être composés d’un nombre impair d’instances.

>[!NOTE]
>
>La réplication sans binaires doit être **ACTIVÉE** si le magasin de données du fichier est partagé.

![chlimage_1-9](assets/chlimage_1-9a.png)

### Paramètres MongoMK recommandés {#mongomk-settings-guidelines}

Pour obtenir de bonnes performances, il est recommandé de définir les paramètres comme suit. Pour obtenir des instructions sur la modification des paramètres, [reportez-vous à cette page](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/configuring/configuring-performance.html?lang=fr).

<table>
 <tbody>
  <tr>
   <td><strong>Configuration</strong></td>
   <td><strong>Paramètre</strong></td>
   <td><strong>Valeur (par défaut)</strong></td>
   <td><strong>Description</strong></td>
  </tr>
  <tr>
   <td>Files d’attente des tâches Sling</td>
   <td><code>queue.maxparallel</code></td>
   <td>Définissez la valeur sur la moitié du nombre de cœurs de processeur. </td>
   <td>Par défaut, le nombre de threads simultanés par file d’attente de tâche est égal au nombre de cœurs du processeur.</td>
  </tr>
  <tr>
   <td>File d’attente du workflow transitoire Granite</td>
   <td><code>Max Parallel</code></td>
   <td>Définissez la valeur sur la moitié du nombre de cœurs de processeur.</td>
   <td> </td>
  </tr>
  <tr>
   <td>Paramètres JVM</td>
   <td><p><code>Doak.queryLimitInMemory</code></p> <p><code>Doak.queryLimitReads</code></p> <p><code>Dupdate.limit</code></p> <p><code>Doak.fastQuerySize</code></p> <p><code>Doak.mongo.maxQueryTimeMS</code></p> </td>
   <td><p>500000</p> <p>100000</p> <p>250000</p> <p>True</p> <p>60000</p> </td>
   <td>Pour empêcher les requêtes volumineuses de surcharger les systèmes, ajoutez les paramètres JVM suivants dans le script de démarrage d’AEM.</td>
  </tr>
  <tr>
   <td>Configuration de l’index Lucene</td>
   <td><p><code>CopyOnRead</code></p> <p><code>CopyOnWrite</code></p> <p><code>Prefetch Index Files</code></p> </td>
   <td><p>Activé</p> <p>Activé</p> <p>Activé</p> </td>
   <td>Pour plus d’informations sur les paramètres disponibles, voir <a href="https://jackrabbit.apache.org/oak/docs/query/lucene.html">cette page</a>.</td>
  </tr>
  <tr>
   <td>Magasin de données = Magasin de données S3</td>
   <td><p><code>maxCachedBinarySize</code></p> <p><code>cacheSizeInMB</code></p> </td>
   <td><p>1 048 576 (1 Mo) ou plus petit</p> <p>2 à 10 % de la taille maximale du tas</p> </td>
   <td>Voir aussi <a href="/help/sites-deploying/data-store-config.md#data-store-configurations">Configurations du magasin de données</a>.</td>
  </tr>
  <tr>
   <td>DocumentNodeStoreService</td>
   <td><p><code>cache</code></p> <p><code>nodeCachePercentage</code></p> <p><code>childrenCachePercentage</code></p> <p><code>diffCachePercentage</code></p> <p><code>docChildrenCachePercentage</code></p> <p><code>prevDocCachePercentage</code></p> <p><code>persistentCache</code></p> </td>
   <td><p>2048</p> <p>35 (25)</p> <p>20 (10)</p> <p>30 (5)</p> <p>10 (3)</p> <p>4 (4)</p> <p>./cache,size=2048,binary=0,-compact,-compress</p> </td>
   <td><p>La taille par défaut du cache est définie sur 256 Mo.</p> <p>Cela a un impact sur le temps nécessaire pour effectuer l’invalidation du cache.</p> </td>
  </tr>
  <tr>
   <td>oak-observation</td>
   <td><p><code>thread pool</code></p> <p><code>length</code></p> </td>
   <td><p>min &amp; max = 20</p> <p>50000</p> </td>
   <td> </td>
  </tr>
 </tbody>
</table>

### Référence des performances de MongoMK {#mongomk-performance-benchmark}

### Spécifications techniques {#technical-specifications-1}

Les tests comparatifs ont été réalisés selon les spécifications suivantes :

| | **Nœud Auteur** | **Nœud MongoDB** |
|---|---|---|
| Serveur | Matériel « métal nu » (HP) | Matériel « métal nu » (HP) |
| Système d’exploitation | Red Hat® Linux® | Red Hat® Linux® |
| Processeur / Cœurs | Processeur Intel(R) Xeon(R) E5-2407 @2,40 GHz, 8 cœurs | Processeur Intel(R) Xeon(R) E5-2407 @2,40 GHz, 8 cœurs |
| Mémoire RAM | 32 Go | 32 Go |
| Disque | Magnétique - >1k IOPS | Magnétique - >1k IOPS |
| Java™ | Oracle JRE version 8 | S/O |
| JVM Heap | 16 Go | S/O |
| Produit | AEM 6.2 | MongoDB 3.2 WiredTiger |
| Entrepôt de nœuds | MongoMK | S/O |
| Magasin de données | File DS | S/O |
| Scénario | Produit unique : Assets / 30 threads simultanés | Produit unique : Assets / 30 threads simultanés |

### Résultats de l’évaluation des performances {#performance-benchmark-results-1}

>[!NOTE]
>
>Les chiffres présentés ci-dessous ont été normalisés à 1 comme référence et ne sont pas les chiffres de débit réels.

![chlimage_1-10](assets/chlimage_1-10a.png) ![chlimage_1-11](assets/chlimage_1-11a.png)

## Comparaison de TarMK et MongoMK {#tarmk-vs-mongomk}

La règle de base à prendre en compte pour choisir entre les deux est que TarMK est conçu pour les performances, tandis que MongoMK est utilisé pour l’évolutivité. Adobe recommande TarMK comme technologie de persistance par défaut à utiliser par les utilisateurs dans tous les scénarios de déploiement, pour les instances d’auteur et de publication AEM.

La principale raison pour choisir le serveur principal de persistance MongoMK plutôt que TarMK est de mettre les instances à l’échelle horizontale. Cette fonctionnalité signifie que deux instances de création principales ou plus s’exécutent toujours et utilisent MongoDB comme système de stockage de persistance. La nécessité d’exécuter plusieurs instances de création découle généralement du fait que la capacité du processeur et de la mémoire d’un seul serveur, prenant en charge toutes les activités de création simultanées, n’est plus suffisante.

Pour plus d’informations sur la comparaison de TarMK et MongoMK, voir [Déploiements recommandés](/help/sites-deploying/recommended-deploys.md#microkernels-which-one-to-use).

### Consignes sur la comparaison de TarMK et MongoMk {#tarmk-vs-mongomk-guidelines}

**Avantages de TarMK**

* Conçu spécifiquement pour les applications de gestion de contenu
* Les fichiers sont toujours cohérents et peuvent être sauvegardés à l’aide de n’importe quel outil de sauvegarde basé sur les fichiers
* Fournit un mécanisme de basculement : consultez la section [Cold Standby](/help/sites-deploying/tarmk-cold-standby.md) pour plus d’informations
* Offre des performances élevées et un stockage des données fiable avec un coût d’exploitation minimal
* Coût total de possession plus faible

**Critères de sélection de MongoMK**

* Nombre d’utilisateurs et d’utilisatrices nommés connectés au cours de la journée : des milliers ou plus
* Nombre d’utilisateurs et d’utilisatrices simultanés : des centaines ou plus
* Volume d’ingestions de ressources par jour : des centaines de milliers ou plus
* Volume de modifications de page par jour : des centaines de milliers ou plus
* Volume de recherches par jour : des dizaines de milliers ou plus

### Références concernant la comparaison de TarMK et MongoMK {#tarmk-vs-mongomk-benchmarks}

>[!NOTE]
>
>Les chiffres présentés ci-dessous ont été normalisés à 1 comme référence et ne sont pas des chiffres de débit réels.

### Spécifications techniques du scénario 1 {#scenario-technical-specifications}

<table>
 <tbody>
  <tr>
   <td><strong> </strong></td>
   <td><strong>Nœud OAK de création</strong></td>
   <td><strong>Nœud MongoDB</strong></td>
   <td> </td>
  </tr>
  <tr>
   <td>Serveur</td>
   <td>Matériel « métal nu » (HP)</td>
   <td>Matériel « métal nu » (HP)</td>
   <td> </td>
  </tr>
  <tr>
   <td>Système d’exploitation</td>
   <td>Red Hat® Linux®</td>
   <td>Red Hat® Linux®</td>
   <td> </td>
  </tr>
  <tr>
   <td>Processeur / Cœurs</td>
   <td>Processeur Intel(R) Xeon(R) E5-2407 @2,40 GHz, 8 cœurs</td>
   <td>Processeur Intel(R) Xeon(R) E5-2407 @2,40 GHz, 8 cœurs</td>
   <td> </td>
  </tr>
  <tr>
   <td>Mémoire RAM</td>
   <td>32 Go</td>
   <td>32 Go</td>
   <td> </td>
  </tr>
  <tr>
   <td>Disque</td>
   <td>Magnétique - &gt;1k IOPS</td>
   <td>Magnétique - &gt;1k IOPS</td>
   <td> </td>
  </tr>
  <tr>
   <td>Java™</td>
   <td>Oracle JRE version 8</td>
   <td>S/O</td>
   <td> </td>
  </tr>
  <tr>
   <td>JVM Heap 16 Go</td>
   <td>16 Go</td>
   <td>S/O</td>
   <td> </td>
  </tr>
  <tr>
   <td>Produit </td>
   <td>AEM 6.2</td>
   <td>MongoDB 3.2 WiredTiger</td>
   <td> </td>
  </tr>
  <tr>
   <td>Entrepôt de nœuds</td>
   <td>TarMK ou MongoMK</td>
   <td>S/O</td>
   <td> </td>
  </tr>
  <tr>
   <td>Magasin de données</td>
   <td>File DS </td>
   <td>S/O</td>
   <td> </td>
  </tr>
  <tr>
   <td>Scénario</td>
   <td><p><br /> Produit unique : Ressources / 30 threads simultanés par exécution</p> </td>
   <td> </td>
   <td> </td>
  </tr>
 </tbody>
</table>

### Résultats de la comparaison des performances du scénario 1 {#scenario-performance-benchmark-results}

![chlimage_1-12](assets/chlimage_1-12a.png)

### Spécifications techniques du scénario 2 {#scenario-technical-specifications-1}

>[!NOTE]
>
>Pour permettre le même nombre d’instances de création avec MongoDB qu’avec un système TarMK, vous avez besoin d’un cluster composé de deux nœuds AEM. Un cluster MongoDB à quatre nœuds peut gérer 1,8 fois plus d’instances de création qu’une instance TarMK. Un cluster MongoDB à huit nœuds peut gérer 2,3 fois plus d’instances de création qu’une instance TarMK.

<table>
 <tbody>
  <tr>
   <td><strong> </strong></td>
   <td><strong>Nœud TarMK de création</strong></td>
   <td><strong>Nœud MongoMK de création</strong></td>
   <td><strong>Nœud MongoDB</strong></td>
  </tr>
  <tr>
   <td>Serveur</td>
   <td>AWS c3.8xlarge</td>
   <td>AWS c3.8xlarge</td>
   <td>AWS c3.8xlarge</td>
  </tr>
  <tr>
   <td>Système d’exploitation</td>
   <td>Red Hat® Linux®</td>
   <td>Red Hat® Linux®</td>
   <td>Red Hat® Linux®</td>
  </tr>
  <tr>
   <td>Processeur / Cœurs</td>
   <td>32</td>
   <td>32</td>
   <td>32</td>
  </tr>
  <tr>
   <td>Mémoire RAM</td>
   <td>60 Go</td>
   <td>60 Go</td>
   <td>60 Go</td>
  </tr>
  <tr>
   <td>Disque</td>
   <td>SSD - 10 000 IOPS</td>
   <td>SSD - 10 000 IOPS</td>
   <td>SSD - 10 000 IOPS</td>
  </tr>
  <tr>
   <td>Java™</td>
   <td>Oracle JRE version 8</td>
   <td><br /> Oracle JRE version 8</td>
   <td>S/O</td>
  </tr>
  <tr>
   <td>JVM Heap 16 Go</td>
   <td>30 Go</td>
   <td>30 Go</td>
   <td>S/O</td>
  </tr>
  <tr>
   <td>Produit </td>
   <td>AEM 6.2</td>
   <td>AEM 6.2</td>
   <td><br /> MongoDB 3.2 WiredTiger</td>
  </tr>
  <tr>
   <td>Entrepôt de nœuds</td>
   <td>TarMK </td>
   <td>MongoMK</td>
   <td><br /> S/O</td>
  </tr>
  <tr>
   <td>Magasin de données</td>
   <td>File DS </td>
   <td><br /> File DS</td>
   <td><br /> S/O</td>
  </tr>
  <tr>
   <td>Scénario</td>
   <td><p><br /> <br /> Cas pratique vertical : Media / 2 000 threads simultanés</p> </td>
   <td></td>
   <td></td>
  </tr>
 </tbody>
</table>

### Résultats de la comparaison des performances du scénario 2 {#scenario-performance-benchmark-results-1}

![chlimage_1-13](assets/chlimage_1-13a.png)

### Conseils relatifs à l’évolutivité de l’architecture d’AEM ִSites et d’AEM Assets {#architecture-scalability-guidelines-for-aem-sites-and-assets}

![chlimage_1-14](assets/chlimage_1-14a.png)

## Résumé des recommandations sur les performances  {#summary-of-performance-guidelines}

Consultez ci-dessous un résumé des recommandations fournies sur cette page :

* **TarMK avec magasin de données du fichier** : l’architecture recommandée pour la plupart des clientes et clients :

   * Topologie minimale : une instance de création, deux instances de publication, deux Dispatcher.
   * La réplication sans fichiers binaires doit être activée si le magasin de données du fichier est partagé.

* **MongoMK avec magasin de données du fichier** : l’architecture recommandée pour l’évolutivité horizontale au niveau de création :

   * Topologie minimale : trois instances de création, trois instances MongoDB, deux instances de publication, deux Dispatcher.
   * La réplication sans fichiers binaires doit être activée si le magasin de données du fichier est partagé.

* **Magasin de nœuds** : stocké sur le disque local et non sur un serveur NAS (dispositif de stockage réseau).
* Lorsque vous utilisez **Amazon S3** :

   * Le magasin de données Amazon S3 est partagé entre les niveaux de création et de publication.
   * La réplication sans fichiers binaire doit être activée.
   * La récupération de l’espace mémoire du magasin de données nécessite une première exécution sur tous les nœuds des instances de création et de publication, puis une seconde exécution sur l’instance de création.

* **L’index personnalisé doit être créé en plus de l’index prêt à l’emploi.** : selon les recherches les plus courantes.

   * Les index Lucene doivent être utilisés pour les index personnalisés.

* **La personnalisation du workflow peut améliorer sensiblement les performances** : la suppression de l’étape vidéo dans le workflow « Ressource de mise à jour », la désactivation d’écouteurs qui ne sont pas utilisés, etc.

Pour plus d’informations, consultez également la page [Déploiements recommandés](/help/sites-deploying/recommended-deploys.md).
