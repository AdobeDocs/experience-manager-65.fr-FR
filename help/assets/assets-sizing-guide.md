---
title: Guide de dimensionnement des ressources
description: Meilleures pratiques pour déterminer des mesures efficaces afin d’estimer l’infrastructure et les ressources nécessaires au déploiement des ressources AEM.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 8c907a43b5755de59b2929cf381ea41a7b977e1b

---


# Assets sizing guide {#assets-sizing-guide}

Lors du dimensionnement de l’environnement pour une mise en œuvre d’Adobe Experience Manager (AEM) Assets, il est important de s’assurer que les ressources disponibles sont suffisantes en termes de disque, de processeur, de mémoire, d’entrée/de sortie et de débit réseau. Pour dimensionner la plupart de ces ressources, vous devez comprendre leur mode de chargement dans le système. Si aucune meilleure mesure n’est disponible, vous pouvez diviser la taille de la bibliothèque existante par l’âge de la bibliothèque pour trouver la fréquence de création des ressources.

## Disque {#disk}

### Banque de données {#datastore}

Une erreur courante lors du dimensionnement de l’espace disque requis pour une mise en œuvre d’Assets consiste à baser les calculs sur la taille des images brutes à intégrer dans le système. Par défaut, AEM crée trois rendus en plus de l’image d’origine afin d’effectuer le rendu des éléments de l’interface utilisateur d’AEM. Dans les mises en œuvre précédentes, il a été observé que la taille de ces rendus était deux fois supérieure à la taille des ressources qui sont intégrées.

La plupart des utilisateurs définissent des rendus personnalisés en plus des rendus prêts à l’emploi. En plus des rendus, AEM Assets permet d’extraire des sous-ressources à partir de types de fichiers courants, tels qu’InDesign et Illustrator.

Enfin, les fonctionnalités de contrôle de version d’AEM stockent les  des ressources dans l’historique des versions. Vous pouvez configurer les versions à purger aussi fréquemment que souhaité. Cependant, de nombreux utilisateurs choisissent de conserver des versions dans le système pendant une longue période, ce qui utilise de l’espace de stockage supplémentaire.

Compte tenu de ces facteurs, vous avez besoin d’une méthodologie permettant de calculer un espace de stockage acceptable afin de stocker les ressources des utilisateurs.

1. Déterminez la taille et le nombre de ressources qui seront chargées dans le système.
1. Obtenez un échantillon représentatif des ressources à charger dans AEM. Par exemple, si vous prévoyez de charger des fichiers PSD, JPG, AI et PDF dans le système, vous avez besoin de plusieurs échantillons d’images de chaque format de fichier. En outre, ces échantillons doivent être représentatifs des différentes tailles de fichiers et de la complexité des images.
1. Définissez les rendus à utiliser.
1. Créez les rendus dans AEM en utilisant ImageMagick ou les applications Adobe Creative Cloud. En plus des rendus que les utilisateurs spécifient, créez des rendus prêts à l’emploi. Pour les utilisateurs qui mettent en œuvre Scene7, vous pouvez utiliser le fichier binaire IC pour générer les rendus PTIFF à stocker dans AEM.
1. Si vous prévoyez d’utiliser des sous-ressources, générez-les pour les types de fichiers appropriés. Voir la documentation en ligne sur la génération de pages de sous-ressources à partir de fichiers InDesign ou PNG/PDF provenant de calques d’Illustrator.
1. Comparez la taille des images, rendus et sous-ressources de sortie avec les images d’origine. Cette comparaison permet de générer un facteur de croissance attendu lorsque le système est chargé. Par exemple, si vous générez des rendus et des sous-ressources d’une taille combinée de 3 Go après le traitement de 1 Go de ressources, le facteur de croissance des rendus est de 3.
1. Déterminez la durée maximale pendant laquelle les versions des ressources doivent être conservées dans le système.
1. Déterminez la fréquence à laquelle les ressources existantes sont modifiées dans le système. Si AEM est utilisé comme centre de collaboration dans les workflow de création, le nombre de modifications est élevé. Si seules les ressources terminées sont chargées dans le système, ce nombre est beaucoup plus bas.
1. Déterminez le nombre de ressources chargées dans le système chaque mois. Si vous avez le moindre doute, vérifiez le nombre de ressources actuellement disponibles et divisez ce nombre par l’âge de la ressource la plus ancienne afin de calculer un nombre approximatif.

La réalisation des étapes 1 à 9 vous aide à déterminer ce qui suit :

* Taille brute des ressources à charger
* Nombre de ressources à charger
* Facteur de croissance des rendus
* Nombre de modifications de ressources effectuées par mois
* Nombre de mois pendant lesquels les versions des ressources sont conservées
* Nombre de nouvelles ressources chargées chaque mois
* Nombre d’années de croissance pour lesquelles allouer de l’espace

Vous pouvez indiquer ces chiffres dans la feuille de calcul Dimensionnement du réseau afin de déterminer l’espace total requis pour la banque de données. C’est également un outil utile pour déterminer l’impact de la conservation des versions des ressources ou de la modification des ressources dans AEM sur la croissance du disque.

Les exemples de données renseignés dans l’outil montrent à quel point il est important de réaliser les étapes mentionnées. Si vous dimensionnez la banque de données uniquement en fonction des images brutes à charger (1 To), vous avez peut-être sous-estimé la taille du référentiel d’un facteur de 15.

[Obtenir le fichier](assets/disk_sizing_tool.xlsx)

### Shared datastores {#shared-datastores}

Pour les banques de données volumineuses, vous pouvez mettre en oeuvre une banque de données partagée par le biais d’une banque de données de fichiers partagée sur un lecteur connecté au réseau ou d’une banque de données S3. Dans ce cas, les instances individuelles n’ont pas besoin de conserver une copie des fichiers binaires. En outre, une banque de données partagée facilite la réplication binaire et réduit la bande passante utilisée pour répliquer les ressources afin de publier   de données.

#### Scénarios d’utilisation    {#use-cases}

La banque de données peut être partagée entre une instance d’auteur principale et de secours afin de réduire le temps nécessaire à la mise à jour de l’instance de secours avec les modifications apportées à l’instance principale. Vous pouvez également partager la banque de données entre les instances d’auteur et de publication afin de réduire le trafic lors de la réplication.

#### Inconvénients {#drawbacks}

En raison de certains écueils, le partage d’une banque de données n’est pas recommandé dans tous les cas.

#### Single point of failure {#single-point-of-failure}

La mise en œuvre d’une banque de données partagée introduit un point de défaillance unique dans une infrastructure. Supposons que votre système dispose d’une instance d’auteur et de deux instances de publication, chacune dotée de sa propre banque de données. Si l’une d’entre elles tombe en panne, les deux autres peuvent continuer à fonctionner. Toutefois, si la banque de données est partagée, une défaillance de disque unique peut entraîner la défaillance de toute l’infrastructure. Par conséquent, pour pouvoir restaurer rapidement la banque de données partagée, assurez-vous d’en conserver une sauvegarde.

La mise en œuvre du service AWS S3 pour les banques de données partagées est préférable, car il réduit considérablement la probabilité de défaillance par rapport aux architectures de disque normales.

#### Increased complexity {#increased-complexity}

Les banques de données partagées augmentent également la complexité des opérations, telles que le nettoyage de la mémoire. Normalement, le nettoyage de la mémoire pour une banque de données autonome peut être lancé d’un seul clic. Cependant, les banques de données partagées requièrent des opérations de balayage des repères sur chaque membre utilisant la banque de données, en plus de l’exécution du nettoyage réel sur un seul nœud.

Pour les opérations AWS, la mise en œuvre d’un emplacement central unique (via S3) plutôt que la création d’une matrice RAID de volumes EBS peut considérablement limiter la complexité et les risques opérationnels du système.

#### Performance concerns {#performance-concerns}

Une banque de données partagée nécessite que les fichiers binaires soient stockés sur un lecteur monté sur le réseau partagé entre toutes les instances. Comme ces fichiers binaires sont accessibles sur un réseau, les performances du système sont affectées. Vous pouvez partiellement atténuer cet impact en utilisant une connexion réseau rapide à une matrice rapide de disques. Toutefois, il s’agit d’une proposition coûteuse. Dans le cas des opérations AWS, tous les disques sont distants et nécessitent une connectivité réseau. Les volumes éphémères perdent des données lorsque l’instance démarre ou s’arrête.

#### Latence {#latency}

La latence dans les mises en œuvre S3 est introduite par les threads d’écriture en arrière-plan. Les procédures de sauvegarde doivent tenir compte de cette latence. De plus, les index Lucene peuvent rester incomplets lors d’une sauvegarde. Cela s’applique à tout fichier sensible au temps écrit dans la banque de données S3 et accessible depuis une autre instance.

### Node store or document store {#node-store-document-store}

Il est difficile d’obtenir des chiffres de dimensionnement précis pour un magasin de nœuds ou une banque de documents en raison des ressources utilisées par les éléments suivants :

* Métadonnées des ressources
* Versions des ressources
* Journaux d’audit
* Processus archivés et actifs

Comme les fichiers binaires sont stockés dans la banque de données, chaque fichier binaire occupe de l’espace. La plupart des référentiels ont une taille inférieure à 100 Go. Cependant, il peut y avoir de plus grands référentiels jusqu&#39;à 1 To de taille. En outre, pour effectuer le compactage hors ligne, vous avez besoin de suffisamment d’espace libre sur le volume pour réécrire le référentiel compacté en plus de la version précompactée. En règle générale, il convient d’avoir un disque faisant 1,5 fois la taille attendue pour le référentiel.

Pour le référentiel, utilisez des disques SSD ou des disques avec un niveau d&#39;E/S par seconde supérieur à 3 000. Pour éviter que les IOPS n’introduisent des goulets d’étranglement en termes de performances, surveillez les niveaux d’attente des E/S du processeur pour détecter les premiers signes de problèmes.

[Obtenir le fichier](assets/aem_environment_sizingtool.xlsx)

## Réseau {#network}

AEM Assets comporte plusieurs cas d’utilisation qui rendent la performance du réseau plus importante que sur la plupart de nos projets AEM. Un client peut disposer d’un serveur rapide, mais si la connexion réseau n’est pas assez puissante pour soutenir la charge des utilisateurs qui chargent et téléchargent des ressources à partir du système, il semblera toujours lent. There is a good methodology for determining the choke point in a user&#39;s network connection to AEM at [AEM Asset considerations for user experience, instance sizing, workflow evaluation, and network topology](/help/assets/assets-network-considerations.md).

## Restrictions {#limitations}

Lorsque vous dimensionnez une mise en œuvre, il est important de garder à l’esprit les restrictions du système. Si la mise en œuvre proposée dépasse ces restrictions, utilisez des stratégies créatives, telles que le partitionnement des ressources entre plusieurs mises en œuvre d’Assets.

La taille des fichiers n’est pas le seul facteur qui contribue aux problèmes de mémoire insuffisante. Cela dépend également des dimensions de l’image. Vous pouvez éviter les problèmes d’insuffisance de mémoire en fournissant une taille de tas supérieure lorsque vous démarrez AEM.

In addition, you can edit the threshold size property of the `com.day.cq.dam.commons.handler.StandardImageHandler` component in Configuration Manager to use intermediate temporary file greater than zero.

## Nombre maximal de ressources {#maximum-number-of-assets}

La limite du nombre de fichiers pouvant exister dans une banque de données peut être de 2,1 milliards en raison des restrictions du système de fichiers. Il est probable que le référentiel rencontre des problèmes en raison du grand nombre de nœuds, bien avant d’atteindre la limite de la banque de données.

Si les rendus ne sont pas générés correctement, utilisez la bibliothèque Camera Raw. Toutefois, dans ce cas, le côté le plus long de l’image ne doit pas dépasser 65 000 pixels. En outre, l’image ne doit pas contenir plus de 512 MP (512 x 1 024 x 1 024 pixels). La taille du fichier n’a pas d’importance.

Il est difficile d’estimer avec précision la taille du fichier TIFF pris en charge prêt à l’emploi avec un tas spécifique pour AEM, car d’autres facteurs, tels que la taille des pixels, influencent le traitement. Il est possible qu’AEM puisse traiter un fichier de 255 Mo prêt à l’emploi, mais pas une taille de fichier de 18 Mo, car ce dernier comprend un nombre de pixels inhabituellement plus élevé que le premier.

## Size of assets {#size-of-assets}

Par défaut, AEM vous permet de télécharger des fichiers d’une taille de fichier allant jusqu’à 2 Go. Pour télécharger des fichiers très volumineux dans AEM, voir [Configuration pour télécharger des fichiers](managing-video-assets.md#configuration-to-upload-assets-that-are-larger-than-gb)très volumineux.
