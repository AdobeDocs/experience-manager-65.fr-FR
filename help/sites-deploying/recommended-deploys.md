---
title: Déploiements recommandés
description: Cette page se rapporte aux topologies recommandées pour AEM.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: deploying
docset: aem65
exl-id: baec7fc8-d48c-4bc6-b12b-4bf4eff695ea
solution: Experience Manager, Experience Manager Sites
feature: Deploying
role: Admin
source-git-commit: f30decf0e32a520dcda04b89c5c1f5b67ab6e028
workflow-type: tm+mt
source-wordcount: '1756'
ht-degree: 94%

---

# Déploiements recommandés{#recommended-deployments}

>[!NOTE]
>
>Cette page se rapporte aux topologies recommandées pour AEM. Pour plus d’informations sur les fonctionnalités de mise en cluster et sur leur configuration, reportez-vous à la [documentation sur les API Discovery Apache Sling](https://sling.apache.org/documentation/bundles/discovery-api-and-impl.html). 

Les micronoyaux fonctionnent comme des gestionnaires de persistance dans AEM 6.2. Le choix d’un micronoyau adapté à vos besoins dépend de l’objectif de votre instance et du type de déploiement que vous envisagez.

Les exemples ci-dessous visent à indiquer les utilisations recommandées dans les configurations d’AEM les plus courantes.

## Scénarios de déploiement {#deployment-scenarios}

### Instance TarMK unique {#single-tarmk-instance}

Dans ce scénario, une seule instance TarMK s’exécute sur un seul serveur.

**Il s’agit du déploiement par défaut pour les environnements de création.**

![chlimage_1-15](assets/chlimage_1-15.png)

Les avantages :

* Simple
* Maintenance aisée
* Bonne performance

Les inconvénients :

* Non évolutif au-delà des limites de la capacité du serveur
* Aucune capacité de basculement

### TarMK Cold Standby {#tarmk-cold-standby}

Une instance TarMK agit comme l’instance principale. Le référentiel de l’instance principale est répliqué vers un système de basculement de secours.

Le mécanisme Cold Standby peut également être utilisé comme sauvegarde, car le référentiel complet est constamment répliqué sur le serveur de basculement. Le serveur de basculement s’exécute en mode Cold Standby, ce qui signifie que seul le récepteur HttpReceiver de l’instance est en cours d’exécution.

![chlimage_1-16](assets/chlimage_1-16.png)

Les avantages :

* Simplicité
* Maintenabilité
* Performance
* Basculement

Les inconvénients :

* Non évolutif au-delà des limites de la capacité du serveur
* La plupart du temps, un serveur est inactif.
* Le basculement n’est pas automatique. Il doit être détecté en externe avant que le système de basculement puisse commencer à traiter les requêtes.

>[!NOTE]
>
>Pour plus d’informations sur la configuration d’AEM avec TarMK Cold Standby, reportez-vous [cet](/help/sites-deploying/tarmk-cold-standby.md) article.

>[!NOTE]
>
>Le déploiement du mécanisme Cold Standby dans cet exemple de TarMK exige que les instances principales et de secours disposent de licences distinctes, en raison de la réplication constante vers le serveur de basculement. Pour plus d’informations sur les licences, veuillez consulter les [conditions générales de licence d’Adobe](https://www.adobe.com/fr/legal/terms/enterprise-licensing.html).

### Batterie TarMK {#tarmk-farm}

Plusieurs instances Oak s’exécutent chacune avec une instance TarMK. Les référentiels TarMK sont indépendants et doivent être synchronisés.

Le fait que le serveur de création publie le même contenu à chaque personne membre de la batterie assure la synchronisation des référentiels. Pour plus d’informations, voir [Réplication](/help/sites-deploying/replication.md).

Pour AEM Communities, le contenu créé par l’utilisateur ou l’utilisatrice (UGC) n’est jamais répliqué. Pour toutes questions concernant la prise en charge du contenu créé par l’utilisateur dans une ferme TarMK, reportez-vous à la section [Remarques relatives à AEM Communities](#considerations-for-aem-communities).

**Il s’agit du déploiement par défaut pour les environnements de publication.**

![chlimage_1-17](assets/chlimage_1-17.png)

Les avantages :

* Performance
* Évolutivité pour l’accès en lecture
* Basculement

### Cluster Oak avec basculement MongoMK pour une haute disponibilité dans un seul centre de données {#oak-cluster-with-mongomk-failover-for-high-availability-in-a-single-datacenter}

Cette approche implique que plusieurs instances Oak accèdent à un ensemble de réplications MongoDB dans un data center, créant ainsi un cluster actif-actif pour l’environnement de création AEM. Les ensembles de réplications de MongoDB sont utilisés pour fournir un haut niveau de disponibilité et de redondance en cas de panne de matériel ou de réseau.

![chlimage_1-18](assets/chlimage_1-18.png)

Les avantages :

* Possibilité d’effectuer une mise à l’échelle horizontale avec de nouvelles instances de création AEM
* Haute disponibilité, redondance et basculement automatisé de la couche de données

Les inconvénients :

* Les performances peuvent être inférieures à celles de TarMK pour certains scénarios.

### Cluster Oak avec basculement MongoMK sur plusieurs centres de données {#oak-cluster-with-mongomk-failover-across-multiple-datacenters}

Cette approche implique que plusieurs instances Oak accèdent à un ensemble de réplications MongoDB défini sur plusieurs data centers, créant ainsi un cluster actif-actif pour l’environnement de création AEM. Avec plusieurs centres de données, la réplication MongoDB fournit le même niveau élevé de disponibilité et de redondance, mais inclut désormais la capacité de gérer une éventuelle panne de courant du centre de données.

![oakclustermongofailover2datacenters](assets/oakclustermongofailover2datacenters.png)

Les avantages :

* Possibilité d’effectuer une mise à l’échelle horizontale avec de nouvelles instances de création AEM
* Haute disponibilité, redondance et basculement automatisé de la couche de données (y compris les pannes de centre de données)

>[!NOTE]
>
>Dans le diagramme ci-dessus, AEM Server 3 et AEM Server 4 sont présentés avec un état inactif en supposant une latence réseau entre les serveurs d’accès à l’interface d’accès à l’interface d’accès à l’interface d’accès à l’interface d’accès à l’interface d’accès à l’interface utilisateur d’un site d’accès à l’interface utilisateur d’un site d’accès à l’interface utilisateur. [](/help/sites-deploying/aem-with-mongodb.md#checklists) Si la latence maximum est compatible avec les exigences, par exemple en utilisant les zones de disponibilité, les serveurs AEM dans le centre données 2 peuvent être actifs également, créant un cluster AEM actif-actif dans plusieurs centres de données.

>[!NOTE]
>
>Pour plus d’informations sur les concepts architecturaux de MongoDB décrits dans cet article, consultez la section [Réplication MongoDB](https://docs.mongodb.org/manual/replication/).

## Microkernels : lequel utiliser {#microkernels-which-one-to-use}

Le principe de base à ne pas oublier lorsque vous choisissez entre les deux microkernels disponibles est que TarMK est conçu pour les performances, tandis que MongoMK est utilisé pour son évolutivité.

Vous pouvez utiliser ces tableaux de décision pour déterminer le type de déploiement le plus adapté à vos besoins.

Adobe recommande vivement aux clientes et clients d’utiliser TarMK comme technologie de persistance par défaut dans tous les scénarios de déploiement, pour les instances de création et de publication AEM, sauf dans les cas d’utilisation précisés ci-dessous.

### Exceptions au choix d’AEM MongoMK plutôt que de TarMK sur les instances de création {#exceptions-for-choosing-aem-mongomk-over-tarmk-on-author-instances}

La principale raison pour laquelle choisir le serveur principal de persistance MongoMK plutôt que TarMK est de mettre les instances à l’échelle horizontale. Cela implique de disposer d’au moins deux instances de création actives s’exécutant en permanence et d’utiliser MongoDB comme système de stockage de persistance. La nécessité d’exécuter plusieurs instances de création est due au fait que la capacité du processeur et de la mémoire d’un seul serveur, prenant en charge toutes les activités de création simultanées, n’est plus suffisante.

Il est presque impossible de prédire quel sera le modèle exact de simultanéité une fois qu’un nouveau site sera mis en ligne. Par conséquent, Adobe recommande de tenir compte des critères suivants au moment d’évaluer s’il faut utiliser MongoMK et deux nœuds actifs de création ou plus :

1. Nombre d’utilisateurs nommés connectés au cours de la journée : des milliers ou plus.
1. Nombre d’utilisateurs simultanés : des centaines ou plus.
1. Volume d’assimilation de ressources par jour : des centaines de milliers, voire plus.
1. Volume de modifications de pages par jour : des centaines de milliers (y compris les mises à jour automatisées via le Multi-site Manager ou des assimilations de flux d’actualité, par exemple).
1. Volume de recherches par jour : des dizaines de milliers, voire plus.

>[!NOTE]
>
>[Tough Day](/help/sites-developing/tough-day.md) peut être utilisé pour évaluer les performances de l’application du client dans le contexte de la configuration matérielle déployée.

Un déploiement minimal avec MongoDB implique généralement la topologie suivante :

* Un ensemble de réplications MongoDB composé d’un nœud principal, de deux nœuds secondaires avec chacune des instances MongoDB s’exécutant dans une zone de disponibilité avec une latence de moins de 15 millisecondes entre chaque nœud ; 
* Un cluster d’instances de création avec un nœud leader et un nœud non-leader, les deux étant actifs à tout moment, chacune des instances de création étant exécutée dans chacun des centres de données, où les instances principales et secondaires de MongoDB s’exécutent.

En outre, il est vivement recommandé de configurer le magasin de données sur un système de fichiers partagé ou Amazon S3, de sorte que les ressources ou les fichiers binaires ne soient pas stockés dans MongoDB. Cela garantit des performances optimales dans le cadre du déploiement.

L’un des avantages supplémentaires du déploiement d’un ensemble de réplications MongoDB avec un cluster d’au moins deux instances de création est de disposer d’un scénario de récupération automatisée avec un temps d’arrêt minimal en cas d’échec des instances de création, de la réplication MongoDB ou d’un centre de données complet. Néanmoins, le choix de MongoMK plutôt que de TarMK ne doit pas être uniquement motivé par les exigences de récupération, car TarMK peut également fournir une solution de temps d’arrêt minimal avec un mécanisme de basculement contrôlé.

Si les critères ci-dessus ne doivent pas être satisfaits au cours des 18 premiers mois du déploiement, nous vous recommandons de commencer par déployer AEM à l’aide de TarMK, puis de réévaluer votre configuration à une date ultérieure lorsque les critères ci-dessus s’appliquent, et enfin de déterminer s’il faut rester sur TarMK ou migrer vers MongoMK.

### Exceptions au choix d’AEM MongoMK par rapport à TarMK sur les instances de publication {#exceptions-for-choosing-aem-mongomk-over-tarmk-on-publish-instances}

Il n’est pas recommandé de déployer MongoMK pour les instances de publication. Le niveau publication du déploiement est presque toujours déployé en tant que batterie d’instances de publication entièrement indépendantes exécutant TarMK, qui sont synchronisées en répliquant le contenu des instances de création. Cette architecture « shared nothing » (sans partage), propre aux instances de publication, permet au déploiement du niveau publication de se dimensionner horizontalement de manière linéaire. La topologie de batterie offre également l’avantage d’appliquer une mise à jour ou une mise à niveau aux instances de publication de manière progressive, de sorte que toute modification au niveau publication ne nécessite aucun temps d’arrêt.

Cela ne s’applique pas à AEM Communities qui utilise des clusters MongoMK sur le niveau publication lorsqu’il y a plusieurs éditeurs ou éditrices. Si vous choisissez JSRP (consultez la section [Stockage du de contenu de la communauté](/help/communities/working-with-srp.md)), un cluster MongoMK est approprié, comme le serait tout cluster côté publication, quel que soit le MK sélectionné, comme MongoDB ou RDB.

### Conditions préalables et recommandations de déploiement d’AEM avec MongoMK {#prerequisites-and-recommendations-when-deploying-aem-with-mongomk}

Certaines conditions préalables et des recommandations sont disponibles si vous envisagez un déploiement MongoMK pour AEM :

**Conditions préalables obligatoires pour les déploiements de MongoDB :**

1. L’architecture et le dimensionnement du déploiement MongoDB doivent faire partie de la mise en œuvre du projet avec l’aide des architectes MongoDB ou des services de conseil Adobe qui connaissent bien AEM ;
1. L’équipe partenaire ou celle du client ou de la cliente doit disposer de l’expertise MongoDB nécessaire pour être en mesure de maintenir et de gérer un environnement MongoDB existant ou nouveau ;
1. Vous pouvez choisir de déployer la version commerciale ou open source de MongoDB (AEM prend en charge les deux), mais vous devez souscrire un contrat de maintenance et de support MongoDB directement auprès de MongoDB Inc ;
1. Les architectures et infrastructures globales d&#39;AEM et de MongoDB doivent être bien définies et validées par un ou une architecte d&#39;AEM Adobe ;
1. Examinez le modèle de prise en charge des déploiements d’AEM qui incluent MongoDB.

**Recommandations essentielles pour les déploiements de MongoDB :**

* Consultez la [révision de déploiement MongoDB pour Adobe Experience Manager](https://www.mongodb.com/lp/contact/mongodb-adobe-experience-manager);
* Examinez la [liste de contrôle des opérations MongoDB](https://docs.mongodb.org/manual/administration/production-checklist/) ;
* Participez à une [classe de certification sur MongoDB - disponible en ligne](https://university.mongodb.com/).

>[!NOTE]
>
>Pour toute autre question concernant ces instructions, les conditions préalables requises et les recommandations, contactez l’[Assistance clientèle d’Adobe](https://helpx.adobe.com/fr/marketing-cloud/contact-support.html).

### Considérations relatives à AEM Communities {#considerations-for-aem-communities}

Pour les sites qui prévoient de déployer [AEM Communities](/help/communities/overview.md), il est recommandé de [choisir un déploiement](/help/communities/working-with-srp.md#characteristicsofstorageoptions) optimisé pour la gestion du contenu créé par l’utilisatreur ou l’utilisatrice (UGC) publié par les membres de la communauté de l’environnement de publication.

En utilisant un [magasin commun](/help/communities/working-with-srp.md), le contenu généré par l’utilisateur ou l’utilisatrice n’a pas besoin d’être répliqué entre l’instance de création et les autres instances de publication pour obtenir une vue cohérente de celui-ci.

Vous trouverez ci-dessous un ensemble de matrices décisionnelles pour vous aider à choisir le meilleur type de persistance pour votre déploiement :

#### Choix du type de déploiement pour les instances d’auteur {#choosing-the-deployment-type-for-author-instances}

![chlimage_1-19](assets/chlimage_1-19.png)

#### Choix du type de déploiement pour les instances de publication {#choosing-the-deployment-type-for-publish-instances}

![chlimage_1-20](assets/chlimage_1-20.png)

>[!NOTE]
>
>MongoDB est un logiciel tiers non inclus dans le package de licence d’AEM. Pour plus d’informations, consultez la page [Politique de licence de MongoDB](https://www.mongodb.org/about/licensing/).
>
>Pour tirer pleinement parti de votre déploiement AEM, Adobe conseille d’utiliser la version MongoDB Enterprise sous licence afin de bénéficier d’une assistance professionnelle.
>
>La licence comprend un ensemble standard de répliques, composé d’une instance principale et de deux instances secondaires qui peuvent être utilisées pour les déploiements de création ou de publication.
>
>Si vous souhaitez exécuter les instances de création et de publication sur MongoDB, deux licences distinctes doivent être achetées.
>
>Pour plus d’informations, consultez la page [MongoDB pour Adobe Experience Manager](https://www.mongodb.com/lp/contact/mongodb-adobe-experience-manager).
