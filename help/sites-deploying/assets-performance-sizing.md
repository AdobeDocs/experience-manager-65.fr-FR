---
title: Guide de performances des ressources
description: Découvrez comment déterminer le dimensionnement matériel optimal pour une nouvelle configuration de gestion des ressources numériques (DAM) et comment résoudre les problèmes de performances.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: configuring
exl-id: fbe15e1b-830b-4752-bd02-0d239a90bc68
solution: Experience Manager, Experience Manager Sites
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '1213'
ht-degree: 19%

---

# Guide de performances des ressources{#assets-performance-guide}

La gestion des ressources numériques (DAM) est souvent utilisée lorsque les performances sont importantes. Cependant, la configuration de gestion des actifs numériques type contient plusieurs composants matériels et logiciels qui peuvent affecter les performances. Ce document fournit les informations suivantes :

* Informations destinées aux administrateurs système sur la détermination du dimensionnement matériel optimal pour une nouvelle configuration de gestion des ressources numériques
* Informations destinées aux développeurs de logiciels cherchant à résoudre les problèmes de performances des instances de gestion des actifs numériques

## Problèmes de performances {#performance-issues}

Les performances médiocres de la gestion des ressources numériques peuvent avoir un impact sur l’expérience utilisateur de trois façons : performances interactives, traitement des ressources et vitesse de téléchargement. Pour améliorer les performances, il est important de mesurer correctement les performances observées et d’établir des mesures cibles.

**1. Recherche et navigation interactives** Les utilisateurs cherchent des ressources ou parcourent l’outil de recherche de gestion des ressources numériques et se plaignent de la lenteur des temps de réponse ou du retard d’affichage des résultats de la recherche. Il s’agit d’un problème de performances interactif.

Les performances interactives sont mesurées en termes de temps de réponse de la page. Il s’agit du temps nécessaire entre la réception de la requête HTTP et la fermeture de la réponse HTTP, qui peut être déterminé à partir des fichiers journaux de requête. Les performances cibles standard sont un temps de réponse de la page inférieur à deux secondes.

**2. Traitement des ressources** Un problème de traitement des ressources se produit lorsque les utilisateurs téléchargent des ressources et cela prend des minutes jusqu’à ce que les ressources soient facilement converties et ingérées dans la gestion des ressources numériques Adobe Experience Manager (AEM).

Les performances de traitement des ressources sont mesurées en termes de temps moyen d’achèvement du processus de workflow. Il s’agit du temps qui s’écoule entre l’appel du processus de mise à jour des ressources et la fin, qui peut être déterminé à partir de l’interface utilisateur des rapports de workflow. Les performances de la cible type dépendent de la taille et du type des ressources traitées et du nombre de rendus. Voici des exemples de performances de la cible :

* moins de dix secondes pour les images de moins de 1 280 x 1 280 pixels à l’aide de rendus standard
* moins d’une minute pour les images de moins de 100 Mo utilisant des rendus standard
* moins de cinq minutes pour les clips vidéo HD de moins d’une minute

**3. Vitesse de téléchargement** Un problème de débit se produit : le téléchargement de la gestion des ressources numériques AEM prend du temps et les miniatures ne s’affichent pas immédiatement lors de l’utilisation de l’outil d’administration ou de recherche de la gestion des ressources numériques.

Les performances de débit sont mesurées en termes de taux de téléchargement en kilobits par seconde. Les performances cibles standard sont de 300 Kbit/s pour 100 téléchargements simultanés.

**4. Facteurs influençant les performances de traitement des ressources**

Pour pouvoir estimer le matériel dont vous avez besoin pour traiter les ressources, les aspects suivants doivent être pris en compte :

* Résolution des images en nombre de pixels
* Le tas affecté au processus AEM

Le nombre de pixels contenus dans l’image détermine le temps de traitement ; plus de pixels signifie que le traitement prend plus de temps.
Le type d’image, le taux de compression ou la taille du fichier dans lequel une image est stockée n’influence pas considérablement les performances globales.

Le segment de mémoire a été identifié comme étant le facteur de limitation le plus important. Chaque fois que la ressource dépasse la mémoire disponible, les performances de traitement diminuent rapidement.

Les processus de gestion des ressources numériques sont bien adaptés pour être exécutés en parallèle pour de grandes quantités. Le chargement des ressources par lot et les processeurs multicœur accélèrent le temps absolu nécessaire par ressource.

**5. Estimation de la configuration matérielle requise pour l’exécution du traitement des ressources**

Le traitement étendu des ressources numériques nécessite des ressources matérielles optimisées, les facteurs les plus pertinents sont la taille de l’image et le débit maximal des images traitées.

Allouez au moins 16 Go de segment de mémoire et configurez le workflow [!UICONTROL Ressource de mise à jour de gestion des ressources numériques] pour qu’il utilise le [package Camera Raw](/help/assets/camera-raw.md) pour l’ingestion des images au format RAW.

## Présentation du système {#understanding-the-system}

Une configuration DAM standard consiste à ce que les utilisateurs finaux accèdent à DAM via un équilibreur de charge. L’instance DAM peut faire partie d’une configuration en grappe, où chaque instance DAM s’exécute dans un processus de machine virtuelle Java™ sur une machine physique ou virtuelle. Le stockage DAM est fourni soit par un disque RAID s’il existe des configurations mono-machine, soit par un stockage connecté au réseau géré en cas de configurations en grappe.

La légende suivante décrit les zones présentant un risque de performance avec certaines solutions, le cas échéant.

**Connexion réseau à l’utilisateur final** Une connexion réseau lente peut entraîner des problèmes de débit et, dans de rares cas, des problèmes de latence. Parfois, l’utilisateur a une connexion lente du FAI, en particulier dans les intranets. C’est un signe de topologie de réseau incorrecte.

**Système de fichiers temporaire** Un système de fichiers local lent peut entraîner des problèmes de performances interactives, en particulier lors de la recherche, car les index de recherche sont stockés sur le disque local. Cela peut également entraîner des problèmes de traitement des ressources si le processus de ligne de commande est utilisé.

**Outil de recherche de la gestion des ressources numériques** Les problèmes de performances interactive, souvent rencontrés lors des recherches, sont dus à une utilisation élevée du processeur en raison de nombreux utilisateurs simultanés ou d’autres processus utilisant le processeur sur la même instance. Passer de machines virtuelles à des machines dédiées et s’assurer qu’aucun autre service n’est exécuté sur l’ordinateur peut contribuer à améliorer les performances. Si une charge élevée du processeur est due au traitement des ressources et à de nombreux utilisateurs simultanés, Day recommande d’ajouter des noeuds de cluster supplémentaires.

**Processus de gestion des ressources numériques AEM** Les workflows dont l’exécution est longue pendant l’intégration des ressources entraînent des problèmes de performances du traitement des ressources. Selon le type de ressources en cours de traitement, cela peut indiquer une surutilisation du processeur. Day recommande de réduire le nombre d’autres processus exécutés sur le système et d’augmenter le nombre de processeurs disponibles en ajoutant des noeuds de grappe.

**Connectivité aux NAS** Une mauvaise connectivité réseau aux périphériques NAS (Network Attached Storage, stockage réseau) entraîne des problèmes de performances des interactions, car l’accès à de nouveaux nœuds pendant le traitement des ressources est ralenti en raison de la latence du réseau. En outre, la lenteur du débit réseau affecte négativement le débit, mais aussi les performances de traitement des ressources, car le chargement et l’enregistrement des rendus sont ralentis.

Les raisons d’une latence et d’un débit faibles dans un NAS sont la topologie du réseau ou la surutilisation du NAS par d’autres services.

**Stockage connecté au réseau** Les systèmes de stockage en réseau surutilisés peuvent entraîner toute une gamme de problèmes :

* Un espace disque faible est un problème rencontré fréquemment, qui peut être résolu en dimensionnant correctement un projet de gestion des ressources numériques. 
* Une latence de disque élevée se propage dans des temps d’accès lents pour CRX et peut entraîner des problèmes de performances interactives.
* Un débit de disque lent peut entraîner des performances faibles pour la gestion des ressources numériques CQ5.

## Test des performances {#testing-for-performance}

Pour chaque projet de gestion des ressources numériques, veillez à établir un régime de test de performance qui peut identifier et résoudre les goulets d’étranglement rapidement. Pour ce faire, tenez compte des points de contrôle suivants :

1. Tests de performance de bout en bout à l’aide de JMeter : simulez un exemple de session de recherche et de navigation pour détecter des problèmes de performances interactives.
1. Tests de débit et de latence à l’aide de JMeter : l’exécution sur un ordinateur client garantit qu’il n’y a aucun problème de topologie.
1. Tests de traitement des ressources normalisés : assimilez quelques exemples de ressources et mesurez le temps. Cela doit inclure l’intégration de workflow externe.
1. Surveillez l’utilisation du processeur, du disque et de la mémoire de chaque noeud de la grappe.
1. Diagnostic des performances de lecture/écriture CRX pour identifier les problèmes liés au non-traitement.
1. Surveillez la latence du réseau et le débit du cluster DAM vers votre NAS.
1. Testez, lisez et écrivez des performances et une latence du disque directement sur le NAS, si possible.

## Réduire les goulets d’étranglement {#tweaking-bottlenecks}

Jusqu’à présent, les ajustements de performances suivants ont été utilisés dans les projets :

* Génération sélective de rendus : générez uniquement les rendus dont vous avez besoin en ajoutant des conditions au workflow de traitement des ressources, de sorte que les rendus plus coûteux ne soient générés que pour des ressources sélectionnées.
* Entrepôt de données partagé entre instances : lorsque l’espace disque est faible, cela peut considérablement réduire la quantité d’espace disque nécessaire au prix d’efforts de configuration plus importants et de la perte du nettoyage automatique de la banque de données.

## Informations complémentaires {#further-reading}

* [Analyse des processus lents et bloqués](https://helpx.adobe.com/fr/experience-manager/kb/AnalyzeSlowAndBlockedProcesses.html)
