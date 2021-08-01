---
title: Comment configurer et résoudre les problèmes liés à une grappe de serveurs AEM Forms on JEE ?
description: Découvrez comment configurer et résoudre les problèmes liés à une grappe de serveurs AEM Forms on JEE
source-git-commit: 8502e0227819372db4120d3995fba51c7401d944
workflow-type: tm+mt
source-wordcount: '4033'
ht-degree: 1%

---

# Configuration et dépannage d’une grappe de serveurs AEM Forms on JEE {#configuring-troubleshooting-aem-forms-jee-server-cluster}

## Connaissances préalables {#prerequisites}

Familiarisez-vous avec les serveurs d’applications AEM Forms on JEE, JBoss, WebSphere et Webogic, Red Hat Linux, SUSE Linux, Microsoft Windows, IBM AIX ou Sun Solaris, les Oracles, les serveurs de base de données IBM DB2, SQL Server et les environnements Web.

## Niveau d’utilisateur {#user-level}

Avancé

Une grappe AEM Forms on JEE est une topologie conçue pour permettre à AEM Forms on JEE de résister à l’échec d’un noeud de grappe et d’étendre la capacité du système au-delà des capacités d’un seul noeud. Une grappe combine plusieurs noeuds en un seul système logique qui partage des données et permet aux transactions d’étendre plusieurs noeuds dans leur exécution. Une grappe est le moyen le plus général de mettre à l’échelle AEM Forms on JEE, en ce sens que toute combinaison de services gérant une combinaison de charges de travail peut être prise en charge. Une grappe AEM Forms on JEE n’est pas nécessairement la mieux adaptée à tous les types de déploiement. En particulier, une architecture équilibrée de la charge du serveur non organisée en grappe peut s’avérer appropriée dans de nombreux cas.

Ce document a pour but de discuter des exigences de configuration spécifiques et des problèmes potentiels que vous pouvez rencontrer avec une grappe AEM Forms on JEE.

## Qu’y a-t-il dans un cluster ? {#what-is-in-cluster}

Les noeuds de grappe d’AEM Forms on JEE communiquent entre eux et partagent des informations pour permettre à la grappe dans son ensemble d’avoir une configuration et un état d’application cohérents. Le partage des informations au sein de la grappe est effectué de plusieurs manières différentes simultanément, utilisées dans différents contextes. Les méthodes de base du partage de l&#39;information sont illustrées dans la figure ci-dessous :

![Grappe de serveurs d’applications](assets/application-server-cluster.jpg)

### Grappe de serveurs d’applications {#application-server-cluster}

Une grappe AEM Forms on JEE repose sur les fonctionnalités de mise en grappe du serveur d’applications sous-jacent. Les grappes de serveurs d’applications permettent de gérer la configuration de la grappe dans son ensemble et fournissent des services de grappe de bas niveau tels que JNDI (Java Naming) et Directory Interface (JNDI) qui permettent aux composants logiciels de se trouver les uns les autres dans la grappe. La sophistication des services en grappe et les dépendances techniques sous-jacentes du serveur d’applications dépendent du serveur d’applications. WebSphere et WebLogic disposent de fonctionnalités de gestion sophistiquées pour les grappes, tandis que JBoss a une approche très basique.

### Cache GemFire {#gemfire-cache}

Le cache GemFire est un mécanisme de cache distribué implémenté dans chaque noeud de grappe. Les noeuds se trouvent les uns les autres et créent un cache logique unique qui est conservé cohérent entre les noeuds. Les noeuds qui se trouvent se rejoignent pour gérer un seul cache notionnel affiché comme nuage dans la figure 1. Contrairement au répertoire de stockage global de documents et à la base de données, le cache est une entité purement théorique. Le contenu réellement mis en cache est stocké en mémoire et dans le répertoire `LC_TEMP` de chacun des noeuds de la grappe.

### Base de données {#database}

La base de données d’AEM Forms on JEE, accessible via les sources de données JDBC IDP_DS, EDC_DS et d’autres, est partagée par tous les noeuds de la grappe. La plupart des données persistantes concernant l’état d’AEM Forms on JEE, telles que les transactions en cours, les données utilisateur associées aux transactions en cours, les données concernant la définition des paramètres système, etc., se trouvent dans cette base de données.

### Stockage global de documents {#global-document-storage}

Le stockage global de documents est une zone de stockage basé sur un système de fichiers utilisée par Document Manager (classe IDPDocument) dans AEM Forms on JEE. Le répertoire de stockage global de documents stocke des fichiers de courte et de longue durée qui doivent être accessibles à tous les noeuds de la grappe.

### Autres éléments {#other-items}

Outre ces ressources partagées principales, d’autres éléments ont un comportement de cluster spécifique, comme Quartz. Quartz est un sous-système de planificateur utilisé par AEM Forms on JEE, qui utilise des tables de base de données pour conserver ses connaissances sur ce qui a été planifié et sur les activités planifiées en cours d’exécution. Quartz doit être configuré différemment pour les installations à un seul noeud et les grappes, et il reprend son signal d’autres paramètres d’AEM Forms on JEE.

## Problèmes de configuration courants {#common-configuration}

L’une des choses les plus frustrantes concernant la maintenance ou la résolution des problèmes d’une grappe AEM Forms on JEE est qu’il n’existe aucun emplacement unique pour vérifier que la grappe est saine. Pour confirmer que tout est bien dans la grappe, une analyse et une analyse sont nécessaires. Il existe plusieurs modes d’échec du fonctionnement de la grappe, selon ce qui ne fonctionne pas avec la configuration de la grappe. La figure ci-dessous illustre un cluster mal configuré dans lequel plusieurs des ressources partagées sont incorrectement partagées.

![Grappe mal configurée](assets/bad-configuration-cluster.png)

Ce qui est intéressant et important à garder à l’esprit, c’est que vous devez connaître le fonctionnement de la mise en grappe et le type de choses à rechercher et à vérifier dans une grappe, même si vous n’avez pas l’intention d’exécuter AEM Forms on JEE dans une grappe. Cela est dû au fait que certaines parties d’AEM Forms on JEE peuvent avoir des indices sur le fonctionnement incorrect d’une grappe et adopter un comportement inattendu.

Qu&#39;est-ce qui ne va pas avec la configuration de partage de la figure ci-dessus ? Les sections suivantes décrivent les problèmes :

### (1) Configuration de la grappe GemFire {#gemfire-cluster-configuration}

Plusieurs problèmes peuvent se produire avec le cache Gemfire. Deux scénarios types sont les suivants :

* Les noeuds qui devraient pouvoir se trouver les uns les autres ne peuvent pas le faire.

* Les noeuds qui ne sont pas censés être mis en grappe se trouvent les uns les autres et partagent un cache alors qu’ils ne le devraient pas.

Si vous avez des noeuds à mettre en grappe, il est essentiel qu’ils se trouvent les uns les autres sur le réseau. Par défaut, ils le font au moyen de messages UDP à diffusion multiple. Chaque noeud envoie des messages de diffusion publicitaire qu’il est présent, et tout noeud qui reçoit un tel message commence à parler aux autres noeuds qu’il trouve. Ce genre de méthode de découverte automatique est très courant, et de nombreux types de logiciels et d&#39;appareils le font.

Un problème courant avec la découverte automatique est que les messages à diffusion multiple peuvent être filtrés par le réseau dans le cadre de la stratégie réseau ou en raison de règles de pare-feu logiciel, ou peuvent tout simplement ne pas être en mesure de naviguer sur le réseau existant entre les noeuds. En raison de la difficulté générale à obtenir la découverte automatique du portail UDP pour fonctionner dans des réseaux complexes, il est courant que les déploiements de production utilisent une autre méthode de découverte : localisateurs TCP. Vous trouverez une discussion générale sur les localisateurs TCP dans les références .

**Comment savoir si j’utilise des localisateurs ou du protocole UDP ?**

Les propriétés JVM suivantes contrôlent la méthode utilisée par le cache GemFire pour trouver d’autres noeuds.

Paramètres de multidiffusion :

* `adobe.cache.multicast-port`: Port multidiffusion utilisé pour communiquer avec d’autres membres du système distribué. Si cette valeur est définie sur zéro, la multidiffusion est désactivée pour la découverte et la distribution de membres.

* `gemfire.mcast-address` (facultatif) : Permet de remplacer l’adresse IP par défaut utilisée par Gemfire.

Paramètres du localisateur TCP :

* `adobe.cache.cluster-locators`: Adresse IP/nom d’hôte du localisateur TCP et port du localisateur TCP pour tous les localisateurs utilisés par les membres du système pour communiquer avec les localisateurs en cours d’exécution.

La liste doit inclure tous les localisateurs actuellement utilisés et doit être configurée de manière cohérente pour chaque membre du système de grappe.

Si la liste des localisateurs TCP est vide, les localisateurs ne sont pas utilisés et la méthode de multidiffusion est utilisée à la place.

**Comment puis-je vérifier si mon localisateur TCP est en cours d’exécution ?**

Tout d’abord, si les localisateurs TCP sont en cours d’utilisation, vos localisateurs TCP doivent être répertoriés dans la propriété JVM suivante sur tous les noeuds de grappe :

`-Dadobe.cache.cluster-locators=aix01.adobe.com[22345],aix02.adobe.com[22345]`

Il n’est pas nécessaire d’exécuter les localisateurs sur les noeuds de la grappe d’AEM Forms on JEE ; ils peuvent être exécutés sur d’autres systèmes distincts de la grappe, le cas échéant. Plusieurs systèmes peuvent exécuter des localisateurs et il est généralement recommandé de faire en sorte que ces derniers s’exécutent à deux endroits, ce qui peut entraîner un problème lors du redémarrage de la grappe. Sur chacun des systèmes exécutant des localisateurs, vous devriez être en mesure de vérifier qu’ils s’exécutent à l’aide des commandes suivantes sur ces machines :

`netstat -an | grep 22345`

La réponse attendue doit être la suivante :

`tcp 0 0 *.22345 *.* LISTEN`

Voici une autre commande de vérification :

`ps -ef | grep gemfire`

La réponse attendue doit ressembler à ceci :

`livecycl 331984 1 0 10:14:51 pts/0 0:03 java -cp ./gemfire.jar: -Dgemfire.license-type=production -Dlocators=localhost[22345] com.gemstone.gemfire.distributed.Locator 22345`

**Comment puis-je voir les noeuds que GemFire pense se trouver dans la grappe ?**

GemFire génère des informations de journalisation qui peuvent être utilisées pour diagnostiquer les membres de la grappe qui ont été trouvés et adoptés par le cache de GemFire. Vous pouvez l’utiliser pour vérifier que tous les membres corrects de la grappe sont trouvés et qu’aucune découverte de noeud de grappe supplémentaire ou incorrecte n’est en cours. Le fichier journal de GemFire se trouve dans le répertoire temporaire configuré d’AEM Forms on JEE :

`.../LC_TEMP/adobeZZ__123456/Caching/Gemfire.log`

La chaîne numérique située après `adobeZZ_` est propre au noeud du serveur. Vous devez donc rechercher le contenu réel de votre répertoire temporaire. Les deux caractères suivant `adobe` dépendent du type de serveur de l’application : `wl`, `jb` ou `ws`.

Les exemples de journaux suivants montrent ce qui se passe lorsqu’une grappe de deux noeuds se trouve.

Sur le premier noeud, AP-HP8 :

```xml
[config 2011/08/05 09:28:09.143 EDT GemfireCacheAdapter <server.startup : 0> tid=0x65] This member, ap-hp8(4268):18763, is becoming group coordinator.
[info 2011/08/05 09:28:09.151 EDT GemfireCacheAdapter <server.startup : 0> tid=0x65] Entered into membership in group GF6.5.1.17 with ID ap-hp8(4268)<v0>:18763/56449.
[info 2011/08/05 09:28:09.152 EDT GemfireCacheAdapter <server.startup : 0> tid=0x65] Starting DistributionManager ap-hp8(4268)<v0>:18763/56449.
[info 2011/08/05 09:28:09.153 EDT GemfireCacheAdapter <server.startup : 0> tid=0x65] Initial (membershipManager) view =  [ap-hp8(4268)<v0>:18763/56449]
[info 2011/08/05 09:28:09.153 EDT GemfireCacheAdapter <server.startup : 0> tid=0x65] Admitting member <ap-hp8(4268)<v0>:18763/56449>. Now there are 1 non-admin member(s).
[info 2011/08/05 09:28:09.154 EDT GemfireCacheAdapter <server.startup : 0> tid=0x65] ap-hp8(4268)<v0>:18763/56449 is the elder and the only member.
[info 2011/08/05 09:28:09.163 EDT GemfireCacheAdapter <server.startup : 0> tid=0x65] Did not hear back from any other system. I am the first one.
[info 2011/08/05 09:28:09.164 EDT GemfireCacheAdapter <server.startup : 0> tid=0x65] DistributionManager ap-hp8(4268)<v0>:18763/56449 started on 239.192.81.1[33456]. There were 0 other DMs. others: []
[info 2011/08/05 09:28:20.841 EDT GemfireCacheAdapter <Pooled Message Processor 1> tid=0xc4] New administration member detected at ap-hp7(2821)<v1>:19498/59136.
```

Sur l&#39;autre noeud, AP-HP7 :

```xml
[info 2011/08/05 09:28:09.830 EDT GemfireCacheAdapter <server.startup : 0> tid=0x64] Attempting to join distributed system whose membership coordinator is ap-hp8(4268)<v0>:18763 using membership ID ap-hp7(2821):19498
[info 2011/08/05 09:28:10.058 EDT GemfireCacheAdapter <server.startup : 0> tid=0x64] Entered into membership in group GF6.5.1.17 with ID ap-hp7(2821)<v1>:19498/59136.
[info 2011/08/05 09:28:10.059 EDT GemfireCacheAdapter <server.startup : 0> tid=0x64] Starting DistributionManager ap-hp7(2821)<v1>:19498/59136.
[info 2011/08/05 09:28:10.060 EDT GemfireCacheAdapter <server.startup : 0> tid=0x64] Initial (membershipManager) view =  [ap-hp8(4268)<v0>:18763/56449, ap-hp7(2821)<v1>:19498/59136]
[info 2011/08/05 09:28:10.060 EDT GemfireCacheAdapter <server.startup : 0> tid=0x64] Admitting member <ap-hp8(4268)<v0>:18763/56449>. Now there are 1 non-admin member(s).
[info 2011/08/05 09:28:10.060 EDT GemfireCacheAdapter <server.startup : 0> tid=0x64] Admitting member <ap-hp7(2821)<v1>:19498/59136>. Now there are 2 non-admin member(s).
[info 2011/08/05 09:28:10.128 EDT GemfireCacheAdapter <server.startup : 0> tid=0x64] DistributionManager ap-hp7(2821)<v1>:19498/59136 started on 239.192.81.1[33456]. There were 1 other DMs. others: [ap-hp8(4268)<v0>:18763/56449]
```

**Et si GemFire trouve des noeuds qu’il ne devrait pas ?**

Chaque grappe distincte qui partage un réseau d’entreprise doit utiliser un ensemble distinct de localisateurs TCP, si des localisateurs TCP sont utilisés, ou un numéro de port UDP distinct si une configuration UDP à diffusion multiple est utilisée. Comme la découverte automatique UDP est la configuration par défaut d’AEM Forms on JEE et que le même port par défaut, 33456, peut être utilisé par plusieurs grappes, il est possible que les grappes qui ne doivent pas tenter de communiquer le fassent de manière inattendue ; par exemple, les grappes de production et d’assurance qualité doivent rester distinctes, mais peuvent se connecter les unes aux autres par le biais de la multidiffusion UDP.

La situation la plus courante lorsque vous découvrez des ports en double dans un réseau auquel GemFire n’est pas correctement mis en grappe est lors de l’amorçage d’une grappe. Ce que vous pouvez découvrir, c&#39;est que le processus de bootstrap échoue sans cause claire. En règle générale, des erreurs telles que celle-ci s’affichent :

```xml
Caused by: com.ibm.ejs.container.UnknownLocalException: nested exception is: com.adobe.pof.schema.ObjectTypeNotFoundException: Object Type: dsc.sc_service_configuration not found.
                at com.adobe.pof.schema.POFDefaultDomain.getObjectType(POFDefaultDomain.java:93)
                at com.adobe.idp.dsc.initializer.DSCInitializerBean.serviceConfigAuditAttributeExists(DSCInitializerBean.java:225)
                at com.adobe.idp.dsc.initializer.DSCInitializerBean.installSchema(DSCInitializerBean.java:186)
                at com.adobe.idp.dsc.initializer.DSCInitializerBean.bootstrap(DSCInitializerBean.java:94)
                at com.adobe.idp.dsc.initializer.EJSLocalStatelessDSCInitializerBeanLocalEJB_7bb34e85.bootstrap(Unknown Source)
                at com.adobe.livecycle.bootstrap.bootstrappers.DSCBootstrapper.bootstrap(DSCBootstrapper.java:68)
```

Dans ce cas, le programme de démarrage fonctionne avec GemFire pour accéder aux tables requises. Il existe une incohérence entre les tables accessibles via JDBC et les informations de table mises en cache renvoyées par GemFire, qui proviennent d’une autre grappe avec une base de données sous-jacente différente.

Bien qu’un port en double apparaisse souvent lors du démarrage, il est possible que cette situation s’affiche ultérieurement, lorsqu’une grappe est redémarrée après avoir été arrêtée lorsque le démarrage de l’autre grappe s’est produit, ou lorsque la configuration du réseau est modifiée pour rendre visibles les grappes qui étaient auparavant isolées à des fins de multidiffusion.

Pour diagnostiquer ces situations, il est préférable d’examiner les journaux GemFire et de soigneusement déterminer si seuls les noeuds attendus sont détectés. Pour résoudre le problème, il est nécessaire de modifier la variable

`adobe.cache.multicast-port`

d’une valeur différente sur l’une ou les deux grappes.

### 2) Partage du stockage global de documents {#gds-sharing}

Le partage du répertoire de stockage global de documents est configuré en dehors d’AEM Forms on JEE lui-même, au niveau O/S, où vous devez organiser la mise à disposition de la même structure de répertoires partagée pour tous les noeuds de la grappe. Sur les systèmes de type Windows, cela se fait généralement en configurant un partage de fichiers soit d’un noeud à l’autre, soit d’un système de fichiers distant, tel qu’une solution NAS, sur tous les noeuds. Sur les systèmes UNIX, le partage du stockage global de documents est généralement effectué par le biais d’un partage de fichiers NFS, à nouveau, soit d’un noeud à l’autre, soit d’un appareil NAS.

Un mode d’échec possible de la grappe est si ce partage de fichiers distant n’est plus disponible ou présente des problèmes subtils. Un montage distant peut échouer en raison de problèmes réseau, de paramètres de sécurité ou d’une configuration incorrecte. Un redémarrage du système peut entraîner des modifications de configuration effectuées plusieurs jours ou semaines à l’avance, ce qui peut entraîner des surprises.

**Que se passerait-il si un partage NFS ne se monte pas ?**

Sous UNIX, la manière dont les montages NFS sont mappés à la structure de répertoires peut permettre la disponibilité d’un répertoire de stockage global de documents apparemment utilisable, même si le montage échoue. Prenez en compte les éléments suivants :

* Serveur NAS : Dossier partagé NFS /u01/iapply/livecycle_gds
* Noeud 1 : un point de montage vers le dossier partagé (hébergé sur le serveur DB) situé ici : /u01/iapply/livecycle_gds
* Noeud 2 : un point de montage vers le dossier partagé (hébergé sur le serveur DB) situé ici : /u01/iapply/livecycle_gds

* LCES spécifie le chemin d’accès au répertoire de stockage global de documents : /u01/iapply/livecycle_gds

Si le montage sur le noeud 1 échoue, la structure de répertoire contiendra toujours un chemin /u01/iapply/livecycle_gds vers le point de montage vide, et le noeud apparaîtra correctement. Mais comme le contenu du répertoire de stockage global de documents n’est pas réellement partagé avec l’autre noeud, la grappe ne fonctionnera pas correctement. Cela peut arriver, et cela arrive, et le résultat est que la grappe échoue de manière mystérieuse.

La bonne pratique consiste à organiser les éléments de sorte que le point de montage Linux ne soit pas utilisé comme racine du répertoire de stockage global de documents, mais qu’un répertoire dans celui-ci soit utilisé comme racine de stockage global de documents :

* Si vous disposez d’un serveur NFS, il peut avoir un répertoire : /some/storage/lc_cluster_dev/LC_GDS
* Et sur votre noeud de grappe, vous avez un point de montage : /u01/iapply/shared
* Montez nfs_server : /some/storage/lc_cluster_dev/u01/iapply/shared
* Pointez votre répertoire de stockage global de documents sur /u01/iapply/shared/LC_GDS.

Désormais, si, pour une raison quelconque, le montage ne réussit pas, le point de montage nu ne contient pas de répertoire LC_GDS et votre grappe échouera de manière prévisible, puisqu’elle ne trouve aucun répertoire de stockage global de documents.

**Comment puis-je vérifier que tous les noeuds voient le même répertoire de stockage global de documents et possèdent les mêmes autorisations ?**

La vérification de l’accès et du partage du stockage global de documents est préférable en accédant à chacun des noeuds en tant qu’utilisateur interactif, soit par SSH, soit par telnet sur les noeuds UNIX, soit via un poste de travail distant sur les systèmes Windows. Vous devez pouvoir accéder au répertoire de stockage global de documents ou au système de fichiers configuré sur chaque noeud et créer des fichiers de test à partir de chaque noeud visible sur tous les autres noeuds.

Faites attention à l’ID utilisateur sous lequel AEM Forms on JEE fonctionne. Sur les installations clé en main Windows, il s’agit d’un administrateur local. Sous UNIX, il peut s’agir d’un utilisateur de service spécifique configuré dans le script de démarrage ou dans la configuration du serveur d’applications. Il est important que cet identifiant utilisateur soit en mesure de créer et de manipuler les fichiers du répertoire de stockage global de documents de manière égale sur tous les noeuds.

Sur les systèmes UNIX, les configurations NFS échouent souvent à faire confiance à la propriété racine ou aux droits d’accès racine aux fichiers et aux objets. Si vous exécutez le serveur d’applications en tant qu’utilisateur root, vous constatez principalement que vous devez spécifier des options sur le serveur NFS, le noeud qui monte les fichiers ou les deux pour permettre un accès et un contrôle bilatéraux des fichiers créés par un noeud et accessibles par un autre.

### (3) Partage de bases de données {#database-sharing}

Pour qu’une grappe fonctionne correctement, il est essentiel que la même base de données soit partagée par tous les membres de la grappe. Pour éviter cela, il suffit de procéder comme suit :

* définition accidentelle des IDP_DS, EDC_DS, AdobeDefaultSA_DS ou d’autres sources de données requises différemment sur des noeuds de grappe distincts, de sorte que les noeuds pointent vers différentes bases de données.
* définition accidentelle de plusieurs noeuds distincts pour partager une base de données lorsqu’ils ne le devraient pas.

Selon votre serveur d’applications, il peut être naturel que la connexion JDBC soit définie dans une portée de grappe, de sorte que différentes définitions ne soient pas possibles sur différents noeuds. Toutefois, sur JBoss, il est entièrement possible de configurer des éléments de sorte qu’une source de données, telle que IDP_DS, pointe vers une base de données sur le noeud 1, mais pointe vers autre chose sur le noeud 2.

Le problème inverse est plus courant, c’est-à-dire que plusieurs noeuds d’AEM Forms on JEE autonomes (ou en grappe) pointent accidentellement vers le même schéma lorsqu’ils ne sont pas prévus. Cela se produit le plus souvent lorsqu’un DBA distribue sans le savoir les informations de connexion d’une base de données AEM Forms on JEE aux équipes de configuration DEV et AQ, aucune d’entre elles ne sachant que les instances DEV et AQ requièrent des bases de données distinctes.

## Grappe de serveurs d’applications {#application-server-cluster-1}

Pour que la grappe AEM Forms on JEE fonctionne correctement, il est essentiel que le serveur d’applications soit configuré et qu’il fonctionne correctement en tant que grappe. Dans WebSphere et Weblogic, il s’agit d’un processus simple et bien documenté. Dans JBoss, la configuration de la grappe est un peu plus pratique, et s’assurer que les noeuds sont configurés pour agir en tant que grappe et pour trouver et communiquer entre eux peut être un défi. JBoss repose en interne sur JGroups, qui utilise la multidiffusion UDP pour trouver et coordonner les noeuds pairs. Certains des problèmes mentionnés avec GemFire peuvent se produire, comme les noeuds qui ne se trouvent pas les uns les autres quand ils le devraient, ou qui se trouvent quand ils ne le devraient pas.

Références:

* [Services d’entreprise haute disponibilité via des grappes JBoss](https://docs.jboss.org/jbossas/jboss4guide/r4/html/cluster.chapt.html)

* [Oracle WebLogic Server - Utilisation de grappes](https://docs.oracle.com/cd/E12840_01/wls/docs103/pdf/cluster.pdf)

### Comment vérifier que JBoss est mis en grappe correctement ? {#check-jboss-clustering}

Lorsque JBoss démarre, au fur et à mesure que les membres de la grappe sont découverts, les messages de niveau INFO sur le noeud qui rejoint la grappe sont consignés dans le fichier journal/la console.

Si un nom de grappe a été spécifié via l’option de ligne de commande -g lors de l’exécution, des messages similaires à ceux-ci s’affichent :

```xml
GMS: address is 10.36.34.44:55200 (cluster=QE_cluster)
GMS: address is 10.36.34.44:55200 (cluster=QE_cluster-HAPartitionCache)
and ones like:

[org.jboss.ha.framework.interfaces.HAPartition.QE_cluster] (JBoss System Threads(1)-3) Number of cluster members: 1
2011-07-14 11:34:03,072 INFO  [org.jboss.ha.framework.interfaces.HAPartition.QE_cluster] (JBoss System Threads(1)-3) Other members: 0
2011-07-14 11:34:03,138 INFO  [org.jboss.cache.RPCManagerImpl] (main) Received new cluster view: [10.36.34.44:55200|0] [10.36.34.44:55200]
2011-07-14 11:34:03,139 INFO  [org.jboss.cache.RPCManagerImpl] (main) Cache local address is 10.36.34.44:55200
```

### Planificateur Quartz {#quartz-scheduler}

Dans la plupart des cas, l’utilisation du planificateur Quartz interne par AEM Forms on JEE dans une grappe est destinée à suivre automatiquement la configuration de grappe globale d’AEM Forms on JEE en général. Il existe toutefois un bogue, #2794033, qui entraîne l’échec de la configuration automatique de la grappe de Quartz si les localisateurs TCP sont utilisés pour Gemfire au lieu de la découverte automatique à diffusion multiple. Dans ce cas, Quartz s’exécute incorrectement en mode non organisé en grappes. Cela créera des blocages et de la corruption des données dans les tables Quartz. Les effets secondaires sont pires dans la version 8.2.x que 9.0, car Quartz n&#39;est pas autant utilisé, mais il est toujours là.

Les correctifs sont disponibles comme suit pour ce problème : 8.2.1.2 QF2.143 et 9.0.0.2 QF2.44.

Il existe également une solution de contournement, qui consiste à définir les deux propriétés suivantes :

* `-Dadobe.cache.cluster.locators=xxx`

* `-Dadobe.cache.cluster-locators=xxx`

Notez que l’un des paramètres utilise un point entre &quot;grappe&quot; et &quot;localisateurs&quot;, tandis que l’autre utilise un trait d’union. Cela est facile à mettre en oeuvre et moins risqué que l’application d’un correctif logiciel, mais cela implique de créer artificiellement un paramètre de configuration supplémentaire déroutant et mal nommé.

### Comment vérifier que Quartz s’exécute en tant que noeud ou grappe unique ? {#check-quartz}

Pour déterminer comment Quartz s’est configuré, vous devez consulter les messages générés par le service de programmation d’AEM Forms on JEE au démarrage. Ces messages sont générés avec la gravité INFO, et il peut être nécessaire d&#39;ajuster le niveau du journal et de redémarrer pour obtenir les messages. Dans la séquence de démarrage d’AEM Forms on JEE, l’initialisation de Quartz commence par la ligne suivante :

INFO `[com.adobe.idp.scheduler.SchedulerServiceImpl]` IDPSchedulerService onLoad
Il est important de localiser cette première ligne dans les journaux, car certains serveurs d’applications utilisent également Quartz et leurs instances Quartz ne doivent pas être confondues avec l’instance utilisée par le service de programmation d’AEM Forms on JEE. C’est l’indication que le service Planificateur est en cours de démarrage et que les lignes qui le suivent vous indiquent s’il démarre correctement en mode organisé en grappes. Plusieurs messages s’affichent dans cette séquence. Il s’agit du dernier message &quot;démarré&quot; qui indique la configuration de Quartz :

Voici le nom de l’instance Quartz : `IDPSchedulerService_$_ap-hp8.ottperflab.corp.adobe.com1312883903975`. Le nom de l’instance Quartz du planificateur commence toujours par la chaîne `IDPSchedulerService_$_`. La chaîne ajoutée à la fin de cette chaîne indique si Quartz est exécuté ou non en mode organisé en grappes. L’identifiant unique long généré à partir du nom d’hôte du noeud et une longue chaîne de chiffres, ici `ap-hp8.ottperflab.corp.adobe.com1312883903975`, indique qu’il fonctionne dans une grappe. S’il fonctionne comme un seul noeud, l’identifiant sera un nombre à deux chiffres, &quot;20&quot; :

INFO `[org.quartz.core.QuartzScheduler]` Démarrage du planificateur `IDPSchedulerService_$_20`.
Cette vérification doit être effectuée séparément sur tous les noeuds de la grappe, car le planificateur de chaque noeud détermine indépendamment s’il convient d’opérer en mode de grappe.

### Quels types de problèmes résultent si Quartz fonctionne dans le mauvais mode ? {#quartz-running-in-wrong-mode}

Si Quartz est configuré pour s’exécuter en tant que noeud unique, mais qu’il s’exécute effectivement dans une grappe et que vous partagez des tables de base de données Quartz avec d’autres noeuds, le service de programmation d’AEM Forms on JEE ne pourra alors pas fonctionner de manière fiable et s’accompagnera généralement d’blocages de base de données. Il s’agit d’une trace de pile assez typique que vous pouvez voir dans cette situation :

```xml
[1/20/11 10:40:57:584 EST] 00000035 ErrorLogger   E org.quartz.core.ErrorLogger schedulerError An error occured while marking executed job complete. job= 'Asynchronous.TaskFormDataSaved:12955380518320.5650479324757354'
 org.quartz.JobPersistenceException: Couldn't remove trigger: ORA-00060: deadlock detected while waiting for resource  [See nested exception: java.sql.SQLException: ORA-00060: deadlock detected while waiting for resource ]
        at org.quartz.impl.jdbcjobstore.JobStoreSupport.removeTrigger(JobStoreSupport.java:1405)
        at org.quartz.impl.jdbcjobstore.JobStoreSupport.triggeredJobComplete(JobStoreSupport.java:2888)
        at org.quartz.impl.jdbcjobstore.JobStoreSupport$38.execute(JobStoreSupport.java:2872)
        at org.quartz.impl.jdbcjobstore.JobStoreSupport$40.execute(JobStoreSupport.java:3628)
        at org.quartz.impl.jdbcjobstore.JobStoreSupport.executeInNonManagedTXLock(JobStoreSupport.java:3662)
        at org.quartz.impl.jdbcjobstore.JobStoreSupport.executeInNonManagedTXLock(JobStoreSupport.java:3624)
        at org.quartz.impl.jdbcjobstore.JobStoreSupport.triggeredJobComplete(JobStoreSupport.java:2868)
        at org.quartz.core.QuartzScheduler.notifyJobStoreJobComplete(QuartzScheduler.java:1698)
        at org.quartz.core.JobRunShell.run(JobRunShell.java:273)
        at org.quartz.simpl.SimpleThreadPool$WorkerThread.run(SimpleThreadPool.java:529)
Caused by: java.sql.SQLException: ORA-00060: deadlock detected while waiting for resource
```

### Comment synchroniser les horloges système dans une grappe ? {#ynchronize-system-clocks-cluster}

Pour qu’une grappe fonctionne correctement, il est essentiel que les horloges de tous les noeuds de la grappe soient étroitement synchronisées. Cela ne peut pas être effectué de manière adéquate à la main et doit être effectué par une forme de service de synchronisation temporelle qui s’exécute très régulièrement. Les horloges sur tous les noeuds doivent se trouver dans une seconde l’une de l’autre. Les bonnes pratiques exigent que non seulement les noeuds de grappe, mais aussi l’équilibreur de charge, le serveur de base de données, le serveur NAS GDS et tout autre composant soient également synchronisés.

La synchronisation du temps Windows a tendance à être avec le contrôleur de domaine. Les systèmes UNIX peuvent se synchroniser à l’aide de NTP vers une autre source temporelle. Il est préférable que tous les systèmes (noeuds AEM Forms on JEE et autres composants système) se synchronisent sur la même source, si possible.

Il ne suffit absolument pas, même dans les environnements de test les plus temporaires, de définir manuellement les horloges sur les noeuds. La définition manuelle des horloges ne permet pas une synchronisation suffisamment précise, et les horloges des deux noeuds dérivent inévitablement les unes par rapport aux autres, même sur une période d&#39;une journée seulement. Un mécanisme de synchronisation à principal temps est essentiel pour une opération fiable en grappe.

### Équilibreur de charge {#load-balancer}

Un équilibreur de charge HTTP qui distribuera des requêtes HTTP à l’échelle de la grappe est une exigence standard pour une grappe qui fournit des services interactifs utilisateur. L’utilisation réussie d’un équilibreur de charge avec une grappe AEM Forms on JEE nécessite la configuration des éléments suivants :

* attractivité de session

* Règles de réécriture d’URL

* contrôle de l’intégrité du noeud

### Que dois-je faire à propos de ma fonction de contrôle de l’intégrité de l’équilibreur de charge ? {#load-balancer-health-check}

Certains équilibreurs de charge peuvent être configurés pour effectuer un contrôle périodique de l’intégrité sur les noeuds en cours d’équilibrage de charge. En règle générale, il s’agit d’une URL vers une fonction d’application à laquelle le répartiteur de charge tentera d’accéder. Si la charge réussit, le noeud est supposé être sain et est conservé dans l’ensemble d’équilibrage de charge. Si le chargement de l’URL échoue, le noeud est supposé être erroné et est éliminé de l’ensemble. En règle générale, l’URL de contrôle de l’intégrité est simplement connectée à la page de connexion de l’interface utilisateur d’administration d’AEM Forms on JEE. Il ne s’agit pas d’un contrôle d’intégrité idéal pour un membre de la grappe. Il serait préférable d’implémenter un processus de courte durée et d’utiliser l’URL de l’API REST comme fonction de contrôle d’intégrité.

## Chemin d’accès au fichier temporaire et paramètres de cluster similaires {#temporary-file-path-cluster-settings}

Certains paramètres de chemin d’accès aux fichiers d’AEM Forms on JEE sont établis à l’échelle de la grappe et ont le même paramètre en vigueur sur chaque noeud, mais sont interprétés indépendamment sur chaque noeud pour faire référence aux fichiers locaux. Les éléments essentiels à prendre en compte sont les paramètres de chemin de police et les paramètres d’annuaire temporaires. Accédez à l’écran Configurations de base de l’interface utilisateur d’administration (Accueil > Paramètres > Core System > Configurations de base).

Les paramètres suivants doivent être vérifiés :

1. Emplacement du répertoire temporaire :
1. Emplacement du répertoire des polices Adobe Server :
1. Emplacement du répertoire des polices personnalisées :
1. Emplacement du répertoire des polices système :
1. Emplacement du fichier de configuration des services de données

La grappe ne comporte qu’un seul paramètre de chemin d’accès pour chacun de ces paramètres de configuration. Par exemple, l’emplacement de votre répertoire temporaire peut être `/home/project/QA2/LC_TEMP`. Dans une grappe, il est nécessaire que chaque noeud ait effectivement ce chemin d’accès particulier accessible. Si un noeud possède le chemin d’accès au fichier temporaire attendu et qu’un autre noeud ne le possède pas, le noeud qui ne fonctionnera pas correctement.

Bien que ces fichiers et chemins d’accès puissent être partagés entre les noeuds ou situés séparément, ou sur des systèmes de fichiers distants, il est généralement recommandé qu’ils soient des copies locales sur l’espace de stockage disque du noeud local.

Le chemin d’accès au répertoire temporaire, en particulier, ne doit pas être partagé entre les noeuds. Une procédure similaire à celle décrite pour la vérification du répertoire de stockage global de documents doit être utilisée pour vérifier que le répertoire temporaire n’est pas partagé : accédez à chaque noeud, créez un fichier temporaire dans le chemin d’accès indiqué par le paramètre de chemin d’accès, puis vérifiez que les autres noeuds ne partagent pas le fichier. Le chemin d’accès au répertoire temporaire doit faire référence à l’enregistrement de disque local sur chaque noeud, le cas échéant, et doit être vérifié.

Pour chacun des paramètres de chemin d’accès, assurez-vous que le chemin d’accès existe réellement et est accessible à partir de chaque noeud de la grappe, en utilisant l’identité d’utilisation effective sous laquelle AEM Forms on JEE s’exécute. Le contenu du répertoire des polices doit être lisible. Le répertoire temporaire doit permettre la lecture, l’écriture et le contrôle.
















