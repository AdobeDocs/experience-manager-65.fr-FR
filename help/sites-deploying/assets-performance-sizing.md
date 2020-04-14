---
title: Guide de performances des ressources
seo-title: Guide de performances des ressources
description: 'Découvrez comment déterminer les dimensions optimales du matériel pour une configuration de gestion des actifs numériques (DAM) et comment résoudre les problèmes de performances. '
seo-description: 'Découvrez comment déterminer les dimensions optimales du matériel pour une configuration de gestion des actifs numériques (DAM) et comment résoudre les problèmes de performances. '
uuid: 8291c5b9-c543-41cf-8754-445826200930
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: configuring
discoiquuid: a79839e2-be39-418b-a3bd-f5457e555172
translation-type: tm+mt
source-git-commit: f24142064b15606a5706fe78bf56866f7f9a40ae

---


# Guide de performances des ressources{#assets-performance-guide}

La gestion des ressources numériques est souvent utilisée lorsque les performances sont importantes ; toutefois, la configuration DAM type contient un certain nombre de composants matériels et logiciels qui peuvent affecter les performances. Ce document contient les éléments suivants :

* Informations destinées aux administrateurs système lors de la détermination des dimensions optimales du matériel pour une nouvelle configuration de gestion des actifs numériques
* Informations destinées aux développeurs de logiciels cherchant à résoudre les problèmes de performances concernant des instances de gestion des actifs numériques

## Problèmes de performances {#performance-issues}

Dans la gestion des actifs numériques, des performances insatisfaisantes peuvent avoir un impact sur l’expérience utilisateur de trois façons : performances des interactions, traitement des ressources et vitesse de téléchargement. Pour améliorer les performances, il est important de mesurer les performances observées et d’établir des objectifs de mesures de façon appropriée.

**1. Interactive searching and browsing** Users are searching for assets or browsing the DAM Finder and complain about slow response times or that search results do not show up immediately. Il s’agit d’un problème lié aux performances des interactions.

Les performances des interactions sont mesurées en termes de délai de réponse par page. C’est le temps qui s’écoule entre la réception de la requête HTTP et la fermeture de la réponse HTTP, qui peut être déterminé en examinant les fichiers journaux des demandes. L’objectif de performances du temps de réponse d’une page est généralement inférieur à 2 secondes.

**2. Asset processing** An asset processing problem is when users are uploading assets and it takes minutes until assets are readily converted and ingested into AEM DAM.

Les performances de traitement des ressources sont mesurées en termes de temps d’exécution moyen des workflows. C’est le temps qui s’écoule entre l’appel du workflow de mise à jour d’une ressource et son exécution, qui peut être déterminé en examinant l’interface utilisateur des rapports de workflow. L’objectif de performances dépend généralement de la taille et du type des ressources traitées et du nombre de rendus. Voici des exemples d’objectif de performances :

* Temps inférieur à 10 secondes pour les images dont la résolution est inférieure à 1 280 x 1 280 pixels à l’aide de rendus standard
* Temps inférieur à 1 minute pour les images dont le volume est inférieur à 100 Mo à l’aide de rendus standard
* Temps inférieur à 5 minutes pour les clips vidéo HD dont la durée ne dépasse pas 1 minute

**3. Download speed** A throughput issue is when downloading from AEM DAM takes long and thumbnails do not show up immediately when browsing the DAM Admin or the DAM Finder.

Les performances de débit sont mesurées en termes de taux de téléchargement, exprimé en kilobits par seconde. L’objectif de performances est généralement de 300 kilobits par seconde pour 100 téléchargements simultanés.

**4. Facteurs influençant les performances du traitement des ressources**

Pour estimer le matériel nécessaire au traitement des ressources, les aspects ci-dessous doivent être pris en compte :

* Résolution des images, exprimée en pixels
* Segment de mémoire affecté au processus AEM

Le nombre de pixels d’une image détermine le temps de traitement : un nombre plus importants de pixels se traduit par un temps de traitement plus long.
Le type d’image, le taux de compression ou la taille du fichier dans lequel une image est stockée n’influence pas considérablement les performances globales.

Un segment de mémoire a été identifié comme étant le facteur de limitation le plus important. Chaque fois que la ressource dépasse la mémoire libre disponible, les performances de traitement diminuent rapidement.

Les processus de gestion des actifs numériques sont bien adaptés pour être exécutés en parallèle pour des volumes importants. Le transfert des ressources par lot et les processeurs multicœur accélèrent le temps absolu nécessaire par ressource.

**5. Estimation de la configuration matérielle requise pour l’exécution du traitement des ressources**

Le traitement étendu des ressources numériques nécessite des ressources matérielles optimisées. Les facteurs les plus pertinents sont la taille des images et le débit maximal des images traitées.

Allocate at least 16GB of heap and configure the [!UICONTROL DAM Update Asset] workflow to use the [Camera Raw package](/help/assets/camera-raw.md) for the ingestion of raw images.

## Présentation du système {#understanding-the-system}

Une configuration de gestion des actifs numériques comprend généralement des utilisateurs finaux, qui accèdent à la gestion des actifs numériques au moyen d’un équilibreur de charge. L’instance de gestion des actifs numériques peut faire partie d’une configuration en cluster, où chaque instance de gestion des actifs numériques peut être exécutée dans un processus de machine virtuelle Java sur un ordinateur physique ou sur une machine virtuelle. Le stockage de gestion des actifs numériques est fourni par un disque RAID dans le cas des configurations à un ordinateur ou par un stockage en réseau géré dans le cas de configurations en cluster.

La légende ci-dessous décrit les écueils potentiels en matière de performances avec quelques solutions, au besoin.

**Connexion réseau à l’utilisateur** final Une connexion réseau lente peut entraîner des problèmes de débit, parfois aussi des problèmes de latence. La connexion que le fournisseur d’accès Internet fournit à l’utilisateur est parfois lente, en particulier pour ce qui est des intranets. C’est un signe de topologie de réseau inappropriée.

**Système** de fichiers temporaires Un système de fichiers local lent peut entraîner des problèmes de performances interactives, surtout en ce qui concerne la recherche, car les index de recherche sont stockés sur le disque local. Cela peut, par ailleurs, entraîner des problèmes de traitement des ressources si le processus de ligne de commande est utilisé.

**AEM DAM Finder** Les problèmes de performances interactifs, souvent rencontrés dans les recherches, sont dus à une utilisation élevée du processeur en raison de nombreux utilisateurs simultanés ou d’autres processus gourmands en ressources sur la même instance. Pour améliorer les performances, passez des machines virtuelles à des ordinateurs dédiés et assurez-vous qu’il n’y a pas d’autres services exécutés sur l’ordinateur. En cas de charge élevée sur le processeur, causée par le traitement des ressources et un nombre important d’utilisateurs simultanés, Day recommande d’ajouter des nœuds de cluster supplémentaires.

**Processus** de gestion des actifs numériques AEM Les processus de gestion des actifs qui s’exécutent de longue date lors de l’assimilation des actifs provoquent des problèmes de performances de traitement des actifs. En fonction du type de ressources traitées, cela peut indiquer une surutilisation du processeur. Day recommande de réduire le nombre des autres processus exécutés sur le système et d’augmenter le nombre de processeurs disponibles en ajoutant des nœuds de cluster.

**Connectivité** NAS Une connectivité réseau faible au NAS entraîne des problèmes de performances interactives, car l&#39;accès aux nouveaux noeuds pendant le traitement des ressources est ralenti en raison de la latence du réseau. De plus, un débit réseau lent affecte négativement le débit, mais également les performances de traitement des ressources, car le chargement et l’enregistrement des rendus sont ralentis.

Les raisons de la latence et du débit insatisfaisants dans un stockage NAS résident généralement dans la topologie de réseau ou la surutilisation du stockage NAS par d’autres services.

**en réseau rattaché** Les systèmes de en réseau rattaché à un réseau trop utilisé peuvent causer toute une gamme de problèmes :

* Un espace disque faible est un problème rencontré fréquemment, qui peut être résolu en dimensionnant correctement un projet de gestion des actifs numériques. 
* Une latence de disque élevée se traduit par des temps d’accès lents pour CRX et peut entraîner des problèmes de performances des interactions.
* Un débit de disque lent peut entraîner des performances faibles pour la gestion des actifs numériques CQ5.

## Test des performances {#testing-for-performance}

Pour tous les projets de gestion des actifs numériques, veillez à établir un programme de test des performances pouvant identifier et résoudre rapidement les goulets d’étranglement. À cet effet, envisagez les points de contrôle suivants :

1. Tests des performances de bout en bout à l’aide de JMeter : simulez un exemple de session de recherche afin de détecter des problèmes de performances des interactions.
1. Tests du débit et de la latence à l’aide de JMeter : l’exécution sur un ordinateur client permet de s’assurer qu’il n’y a pas de problèmes liés à la topologie.
1. Tests de traitement des ressources normalisés : intégrez un petit nombre d’exemples de ressources et mesurer le temps. Cette opération doit inclure l’intégration des workflows externes.
1. Surveillez l’utilisation du processeur, du disque et de la mémoire de chaque nœud de cluster.
1. Diagnostic des performances de lecture/écriture CRX permettant d’identifier les problèmes non liés au traitement.
1. Surveillez la latence réseau et le débit du cluster de gestion des actifs numériques sur votre stockage réseau (NAS).
1. Testez les performances en lecture et en écriture, ainsi que la latence du disque directement sur le stockage réseau (NAS), si cela est possible.

## Ajustement des goulets d’étranglement {#tweaking-bottlenecks}

Les ajustements de performances ci-dessous ont été utilisés dans les projets jusque-ici :

* Génération sélective du rendu : ne générez que les rendus dont vous avez besoin en ajoutant des conditions au workflow de traitement des ressources afin que les rendus plus coûteux ne soient produits que pour les ressources sélectionnées.
* Stockage des données partagées sur des instances : lorsque l’espace disque est saturé, cela peut réduire considérablement la quantité d’espace disque nécessaire, au prix d’efforts de configuration plus importants et de la perte du nettoyage automatique de la banque de données.

## Informations complémentaires {#further-reading}

* [Analyse des processus lents et bloqués](https://helpx.adobe.com/experience-manager/kb/AnalyzeSlowAndBlockedProcesses.html)

