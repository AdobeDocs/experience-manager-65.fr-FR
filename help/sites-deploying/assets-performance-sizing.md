---
title: Guide de performances des ressources
description: Découvrez comment déterminer le dimensionnement matériel optimal pour une nouvelle configuration de la gestion des ressources numériques (DAM) et comment résoudre les problèmes de performances.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: configuring
exl-id: fbe15e1b-830b-4752-bd02-0d239a90bc68
solution: Experience Manager, Experience Manager Sites
feature: Configuring
role: Admin
source-git-commit: f96b178ae84b4b930b59e36d4994970682c53dbd
workflow-type: ht
source-wordcount: '1205'
ht-degree: 100%

---

# Guide de performances des ressources{#assets-performance-guide}

La gestion des ressources numériques (DAM) est souvent utilisée dans les cas où les performances sont importantes. Cependant, la configuration de la gestion des ressources numériques standard contient plusieurs composants matériels et logiciels qui peuvent avoir un impact sur les performances. Ce document fournit ce qui suit :

* Des informations destinées aux administrateurs et administratrices système sur la détermination du dimensionnement matériel optimal pour une nouvelle configuration de la gestion des ressources numériques.
* Des informations destinées aux développeurs et développeuses de logiciels cherchant à résoudre les problèmes de performances des instances de gestion des ressources numériques.

## Problèmes de performances {#performance-issues}

De mauvaises performances de la gestion des ressources numériques peuvent avoir une incidence sur l’expérience utilisateur en termes de performances interactives, de traitement des ressources et de vitesse de téléchargement. Pour améliorer les performances, il est important de mesurer correctement les performances observées et d’établir des mesures cibles.

**1. Recherche et navigation interactives** Les utilisateurs cherchent des ressources ou parcourent l’outil de recherche de gestion des ressources numériques et se plaignent de la lenteur des temps de réponse ou du retard d’affichage des résultats de la recherche. Il s’agit d’un problème de performances interactives.

Les performances interactives sont mesurées en termes de temps de réponse de la page. Il s’agit du temps qui s’écoule entre la réception de la requête HTTP et la fermeture de la réponse HTTP, qui peut être déterminé à partir des fichiers journaux de requête. Les performances cibles standard correspondent à un temps de réponse de la page inférieur à deux secondes.

**2. Traitement des ressources** Un problème de traitement des ressources survient lorsque les utilisateurs et utilisatrices chargent des ressources et que la conversion et l’intégration des ressources dans la gestion des ressources numériques d’Adobe Experience Manager (AEM) prend plusieurs minutes.

Les performances de traitement des ressources sont mesurées en termes de durée moyenne d’achèvement du processus de workflow. Il s’agit du temps qui s’écoule entre l’appel du processus de mise à jour des ressources et la fin du processus, qui peut être déterminé à partir de l’interface utilisateur des rapports de workflow. Les performances cibles type dépendent de la taille et du type des ressources traitées et du nombre de rendus. Voici des exemples d’objectif de performances :

* moins de dix secondes pour les images de moins de 1 280 x 1 280 pixels à l’aide de rendus standard
* moins d’une minute pour les images de moins de 100 Mo à l’aide de rendus standard
* moins de cinq minutes pour les clips vidéo HD de moins d’une minute

**3. Vitesse de téléchargement** Un problème de débit se produit : le téléchargement de la gestion des ressources numériques AEM prend du temps et les miniatures ne s’affichent pas immédiatement lors de l’utilisation de l’outil d’administration ou de recherche de la gestion des ressources numériques.

Les performances de débit sont mesurées en termes de taux de téléchargement en kilobits par seconde. Les performances cibles standard sont de 300 Kbit/s pour 100 téléchargements simultanés.

**4. Facteurs qui influencent les performances de traitement des ressources**

Pour estimer le matériel dont vous avez besoin pour traiter les ressources, tenez compte des aspects suivants :

* La résolution des images en nombre de pixels
* Le tas affecté au processus AEM

Le nombre de pixels d’une image détermine le temps de traitement : un nombre plus important de pixels se traduit par un temps de traitement plus long.
Le type d’image, le taux de compression ou la taille du fichier dans lequel une image est stockée n’influence pas considérablement les performances globales.

Le tas constitue le facteur de limitation le plus important. Chaque fois que la ressource dépasse la mémoire disponible, les performances de traitement chutent.

Les processus de gestion des ressources numériques peuvent facilement être exécutés en parallèle pour des volumes importants. Le chargement des ressources par lot et les processeurs multicœur accélèrent le temps absolu nécessaire par ressource.

**5. Estimation des exigences en termes de matériel pour l’exécution du traitement des ressources**

Le traitement approfondi des ressources numériques nécessite des ressources matérielles optimisées, les facteurs les plus pertinents étant la taille de l’image et le débit maximal des images traitées.

Allouez au moins 16 Go de segment de mémoire et configurez le workflow [!UICONTROL Ressource de mise à jour DAM] pour qu’il utilise le [package Camera Raw](/help/assets/camera-raw.md) pour l’ingestion des images au format RAW.

## Présentation du système {#understanding-the-system}

Une configuration DAM standard consiste à ce que les utilisateurs finaux accèdent à la gestion des ressources numériques via un équilibreur de charge. L’instance DAM peut faire partie d’une configuration en cluster, où chaque instance DAM s’exécute dans un processus de machine virtuelle Java™ sur une machine physique ou virtuelle. Le stockage DAM est fourni soit par un disque RAID s’il existe des configurations mono-machine, soit par un stockage connecté au réseau et géré en cas de configurations en cluster.

La légende suivante décrit les zones présentant un risque pour les performances avec certaines solutions, le cas échéant.

**Connexion réseau à l’utilisateur final ou l’utilisatrice finale** Une connexion réseau lente peut entraîner des problèmes de débit ainsi que, dans de rares cas, des problèmes de latence. Parfois, l’utilisateur ou l’utilisatrice reçoit une connexion lente du FAI, en particulier dans les intranets. C’est un signe de topologie de réseau incorrecte.

**Système de fichiers temporaires** Un système de fichiers local lent peut entraîner des problèmes de performances dans les interactions, en particulier pour les recherches, car les index de recherche sont stockés sur le disque local. Cela peut, par ailleurs, entraîner des problèmes de traitement des ressources en cas d’utilisation du processus de ligne de commande.

**Outil de recherche de la gestion des ressources numériques** Les problèmes de performances interactive, souvent rencontrés lors des recherches, sont dus à une utilisation élevée du processeur en raison de nombreux utilisateurs simultanés ou d’autres processus utilisant le processeur sur la même instance. Passer de machines virtuelles à des machines dédiées et s’assurer qu’aucun autre service ne s’exécute sur l’ordinateur peut contribuer à améliorer les performances. Si une charge élevée de l’UC est due au traitement des ressources et à de nombreux utilisateurs et utilisatrices simultanés, Day recommande d’ajouter des nœuds de cluster supplémentaires.

**Processus de gestion des ressources numériques AEM** Les workflows dont l’exécution est longue pendant l’intégration des ressources entraînent des problèmes de performances du traitement des ressources. Selon le type de ressources qui sont en cours de traitement, cela peut indiquer une surutilisation de l’UC. Day recommande de réduire le nombre d’autres processus s’exécutant sur le système et d’augmenter le nombre d’UC disponibles en ajoutant des nœuds de cluster.

**Connectivité aux NAS** Une mauvaise connectivité réseau aux périphériques NAS (Network Attached Storage, stockage réseau) entraîne des problèmes de performances des interactions, car l’accès à de nouveaux nœuds pendant le traitement des ressources est ralenti en raison de la latence du réseau. En outre, un débit réseau lent altère le débit, mais aussi les performances de traitement des ressources, car le chargement et l’enregistrement des rendus sont ralentis.

Les raisons d’une latence et d’un débit faibles dans un NAS sont la topologie du réseau ou la surutilisation du NAS par d’autres services.

**NAS (Network Attached Storage)** La surutilisation de systèmes de stockage réseau (NAS) peut entraîner différents problèmes :

* Un espace disque faible est un problème rencontré fréquemment, qui peut être résolu en dimensionnant correctement un projet de gestion des ressources numériques. 
* Une latence de disque élevée se traduit par des temps d’accès lents pour CRX et peut entraîner des problèmes de performances des interactions.
* Un débit de disque lent peut entraîner des performances faibles pour la gestion des ressources numériques CQ5.

## Tester les performances {#testing-for-performance}

Pour chaque projet DAM, créez un régime de tests de performances qui permet d’identifier et de résoudre les goulots d’étranglement rapidement. Pour ce faire, tenez compte des points de contrôle suivants :

1. Tests de performances de bout en bout à l’aide de JMeter : simulez un exemple de session de recherche et de navigation pour détecter des problèmes de performances interactives.
1. Tests de débit et de latence à l’aide de JMeter : l’exécution sur un ordinateur client garantit l’absence de tout problème de topologie.
1. Tests de traitement des ressources normalisés : ingérez quelques exemples de ressources et mesurez le temps. Cela doit inclure l’intégration de workflows externes.
1. Surveillez l’utilisation de l’UC, du disque et de la mémoire de chaque nœud du cluster.
1. Diagnostic des performances de lecture/écriture CRX pour identifier les problèmes liés au non-traitement.
1. Surveillez la latence et le débit du réseau, entre le cluster DAM et votre NAS.
1. Testez les performances de lecture et d’écriture et la latence du disque directement sur le NAS, si possible.

## Réduire les goulets d’étranglement {#tweaking-bottlenecks}

Jusqu’à présent, les ajustements de performances suivants ont été utilisés dans les projets :

* Génération sélective de rendus : générez uniquement les rendus dont vous avez besoin en ajoutant des conditions au workflow de traitement des ressources, de sorte que les rendus plus coûteux ne soient générés que pour certaines ressources.
* Magasin de données partagé entre instances : lorsque l’espace disque est faible, cela peut considérablement réduire la quantité d’espace disque nécessaire au prix d’efforts de configuration plus importants et de la perte du nettoyage automatique du magasin de données.
