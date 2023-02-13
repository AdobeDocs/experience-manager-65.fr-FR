---
title: « Guide de dimensionnement d’[!DNL Assets] »
description: Bonnes pratiques pour déterminer les mesures efficaces permettant d’estimer l’infrastructure et les ressources nécessaires au déploiement d’ [!DNL Adobe Experience Manager Assets].
contentOwner: AG
role: Architect, Admin
feature: Asset Management
exl-id: fd58ead9-5e18-4f55-8d20-1cf4402fad97
source-git-commit: e24316cb9495a552960ae0620e4198f10a08b691
workflow-type: ht
source-wordcount: '1615'
ht-degree: 100%

---

# Guide de dimensionnement d’[!DNL Assets] {#assets-sizing-guide}

Lors du dimensionnement de l’environnement pour une mise en œuvre d’[!DNL Adobe Experience Manager Assets], il est important de s’assurer que les ressources disponibles sont suffisantes en termes de disque, de processeur, de mémoire, d’entrée/de sortie et de débit réseau. Pour dimensionner la plupart de ces ressources, vous devez comprendre leur mode de chargement dans le système. Si aucune meilleure mesure n’est disponible, vous pouvez diviser la taille de la bibliothèque existante par l’âge de la bibliothèque pour trouver la fréquence de création des ressources.

## Disque {#disk}

### Banque de données {#datastore}

Une erreur courante lors du dimensionnement de l’espace disque requis pour une mise en œuvre d’[!DNL Assets] consiste à baser les calculs sur la taille des images brutes à intégrer dans le système. Par défaut, [!DNL Experience Manager] crée trois rendus en plus de l’image d’origine afin d’effectuer le rendu des éléments de l’interface utilisateur d’[!DNL Experience Manager]. Dans les mises en œuvre précédentes, il a été observé que la taille de ces rendus était deux fois supérieure à la taille des ressources qui sont intégrées.

La plupart des utilisateurs définissent des rendus personnalisés en plus des rendus prêts à l’emploi. En plus des rendus, [!DNL Assets] permet d’extraire des sous-ressources à partir de types de fichiers courants, tels qu’[!DNL Adobe InDesign] et [!DNL Adobe Illustrator].

Enfin, les fonctionnalités de création de versions d’[!DNL Experience Manager] stockent les doublons des ressources dans l’historique des versions. Vous pouvez configurer les versions à purger aussi fréquemment que souhaité. Cependant, de nombreux utilisateurs choisissent de conserver des versions dans le système pendant une longue période, ce qui utilise de l’espace de stockage supplémentaire.

Compte tenu de ces facteurs, vous avez besoin d’une méthodologie permettant de calculer un espace de stockage acceptable afin de stocker les ressources des utilisateurs.

1. Déterminez la taille et le nombre de ressources qui seront chargées dans le système.
1. Obtenez un échantillon représentatif des ressources à charger dans [!DNL Experience Manager]. Par exemple, si vous prévoyez de charger des fichiers PSD, JPG, AI et PDF dans le système, vous avez besoin de plusieurs échantillons d’images de chaque format de fichier. En outre, ces échantillons doivent être représentatifs des différentes tailles de fichiers et de la complexité des images.
1. Définissez les rendus à utiliser.
1. Créez les rendus dans [!DNL Experience Manager] à l’aide des applications [!DNL ImageMagick] ou [!DNL Adobe Creative Cloud]. En plus des rendus que les utilisateurs spécifient, créez des rendus prêts à l’emploi. Pour les utilisateurs qui mettent en œuvre Dynamic Media, vous pouvez utiliser le fichier binaire IC pour générer les rendus PTIFF à stocker dans Experience Manager.
1. Si vous prévoyez d’utiliser des sous-ressources, générez-les pour les types de fichiers appropriés.
1. Comparez la taille des images, rendus et sous-ressources de sortie avec les images d’origine. Cette comparaison permet de générer un facteur de croissance attendu lorsque le système est chargé. Par exemple, si vous générez des rendus et des sous-ressources d’une taille combinée de 3 Go après le traitement de 1 Go de ressources, le facteur de croissance des rendus est de 3.
1. Déterminez la durée maximale pendant laquelle les versions des ressources doivent être conservées dans le système.
1. Déterminez la fréquence à laquelle les ressources existantes sont modifiées dans le système. Si [!DNL Experience Manager] est utilisé comme centre de collaboration dans les workflow de création, le nombre de modifications est élevé. Si seules les ressources terminées sont chargées dans le système, ce nombre est beaucoup plus bas.
1. Déterminez le nombre de ressources chargées dans le système chaque mois. Si vous avez le moindre doute, vérifiez le nombre de ressources actuellement disponibles et divisez ce nombre par l’âge de la ressource la plus ancienne afin de calculer un nombre approximatif.

L’exécution des étapes ci-dessus vous aide à déterminer les éléments suivants :

* Taille brute des ressources à charger
* Nombre de ressources à charger
* Facteur de croissance des rendus
* Nombre de modifications de ressources effectuées par mois
* Nombre de mois pendant lesquels les versions des ressources sont conservées
* Nombre de nouvelles ressources chargées chaque mois
* Années de croissance pour l’allocation de l’espace de stockage

Vous pouvez indiquer ces chiffres dans la feuille de calcul Dimensionnement du réseau afin de déterminer l’espace total requis pour le magasin de données. C’est également un outil utile pour déterminer l’impact de la conservation des versions des ressources ou de la modification des ressources dans [!DNL Experience Manager] sur la croissance du disque.

Les exemples de données renseignés dans l’outil montrent à quel point il est important de réaliser les étapes mentionnées. Si vous dimensionnez le magasin de données uniquement en fonction des images brutes à charger (1 To), vous avez peut-être sous-estimé la taille du référentiel d’un facteur de 15.

[Obtenir le fichier](assets/disk_sizing_tool.xlsx)

### Magasins de données partagées {#shared-datastores}

Les magasins de données volumineux peuvent être partagés en optant pour un magasin de données de fichiers partagée sur un lecteur relié au réseau ou un magasin de données S3. Dans ce cas, les instances individuelles n’ont pas besoin de conserver une copie des fichiers binaires. En outre, un magasin de données partagé facilite la réplication sans fichier binaire et permet de réduire la bande passante utilisée pour répliquer les ressources dans les environnements de publication.

#### Cas d’utilisation {#use-cases}

Le magasin de données peut être partagé entre une instance d’auteur principale et de secours afin de réduire le temps nécessaire à la mise à jour de l’instance de secours avec les modifications apportées à l’instance principale. Vous pouvez également partager la banque de données entre les instances d’auteur et de publication afin de réduire le trafic lors de la réplication.

#### Inconvénients {#drawbacks}

En raison de certains écueils, le partage d’une banque de données n’est pas recommandé dans tous les cas.

#### Point de défaillance unique {#single-point-of-failure}

La mise en œuvre d’une banque de données partagée introduit un point de défaillance unique dans une infrastructure. Supposons que votre système dispose d’une instance d’auteur et de deux instances de publication, chacune dotée de sa propre banque de données. Si l’une d’entre elles tombe en panne, les deux autres peuvent continuer à fonctionner. Toutefois, si la banque de données est partagée, une défaillance de disque unique peut entraîner la défaillance de toute l’infrastructure. Par conséquent, pour pouvoir restaurer rapidement la banque de données partagée, assurez-vous d’en conserver une sauvegarde.

La mise en œuvre du service AWS S3 pour les banques de données partagées est préférable, car il réduit considérablement la probabilité de défaillance par rapport aux architectures de disque normales.

#### Complexité accrue {#increased-complexity}

Les banques de données partagées augmentent également la complexité des opérations, telles que le nettoyage de la mémoire. Normalement, le nettoyage de la mémoire pour une banque de données autonome peut être lancé d’un seul clic. Cependant, les banques de données partagées requièrent des opérations de balayage des repères sur chaque membre utilisant la banque de données, en plus de l’exécution du nettoyage réel sur un seul nœud.

Pour les opérations AWS, la mise en œuvre d’un emplacement central unique (via Amazon S3) plutôt que la création d’une matrice RAID de volumes EBS peut considérablement limiter la complexité et les risques opérationnels du système.

#### Problèmes de performances {#performance-concerns}

Un magasin de données partagé nécessite que les fichiers binaires soient stockés sur un lecteur monté sur le réseau partagé entre toutes les instances. Comme ces fichiers binaires sont accessibles sur un réseau, les performances du système sont affectées. Vous pouvez partiellement atténuer cet impact en utilisant une connexion réseau rapide à une matrice rapide de disques. Toutefois, il s’agit d’une proposition coûteuse. Dans le cas des opérations AWS, tous les disques sont distants et nécessitent une connectivité réseau. Les volumes éphémères perdent des données lorsque l’instance démarre ou s’arrête.

#### Latence {#latency}

La latence dans les mises en œuvre S3 est introduite par les threads d’écriture en arrière-plan. Les procédures de sauvegarde doivent tenir compte de cette latence. De plus, les index Lucene peuvent rester incomplets lors d’une sauvegarde. Cela s’applique à tout fichier sensible au temps écrit dans la banque de données S3 et accessible depuis une autre instance.

### Magasin de nœuds ou banque de documents {#node-store-document-store}

Il est difficile d’obtenir des chiffres de dimensionnement précis pour un magasin de nœuds ou une banque de documents en raison des ressources utilisées par les éléments suivants :

* Métadonnées des ressources
* Versions des ressources
* Journaux d’audit
* Processus archivés et actifs

Comme les fichiers binaires sont stockés dans la banque de données, chaque fichier binaire occupe de l’espace. La plupart des référentiels ont une taille inférieure à 100 Go. Cependant, vous pouvez rencontrer des référentiels de plus grande taille pouvant atteindre 1 To. En outre, pour effectuer le compactage hors ligne, vous avez besoin de suffisamment d’espace libre sur le volume pour réécrire le référentiel compacté en plus de la version précompactée. En règle générale, il convient d’avoir un disque faisant 1,5 fois la taille attendue pour le référentiel.

Pour le référentiel, utilisez des disques SSD ou des disques dont le niveau IOPS est supérieur à 3000. Pour éviter que les IOPS n’introduisent des goulets d’étranglement en termes de performances, surveillez les niveaux d’attente des E/S du processeur pour détecter les premiers signes de problèmes.

[Obtenir le fichier](assets/aem_environment_sizingtool.xlsx)

## Réseau {#network}

[!DNL Assets] comporte plusieurs cas d’utilisation qui rendent la performance du réseau plus importante que sur la plupart de nos projets [!DNL Experience Manager]. Un client peut disposer d’un serveur rapide, mais si la connexion réseau n’est pas assez puissante pour soutenir la charge des utilisateurs qui chargent et téléchargent des ressources à partir du système, il semblera toujours lent. Il existe une bonne méthodologie pour déterminer le point d’étranglement de la connexion réseau d’un utilisateur vers [!DNL Experience Manager] dans le document [Observations relatives à Assets en ce qui concerne l’expérience utilisateur, le dimensionnement des instances, l’évaluation des workflows et la topologie réseau](/help/assets/assets-network-considerations.md).

## Limites {#limitations}

Lorsque vous dimensionnez une mise en œuvre, il est important de garder à l’esprit les restrictions du système. Si la mise en œuvre proposée dépasse ces restrictions, utilisez des stratégies créatives, telles que le partitionnement des ressources entre plusieurs mises en œuvre d’[!DNL Assets].

La taille des fichiers n’est pas le seul facteur qui contribue aux problèmes de mémoire insuffisante. Cela dépend également des dimensions de l’image. Vous pouvez éviter les problèmes d’insuffisance de mémoire en fournissant une taille de tas supérieure lorsque vous démarrez [!DNL Experience Manager].

En outre, vous pouvez modifier la propriété de taille de seuil du composant `com.day.cq.dam.commons.handler.StandardImageHandler` dans Configuration Manager pour utiliser un fichier temporaire intermédiaire supérieur à zéro.

## Nombre maximal de ressources {#maximum-number-of-assets}

La limite du nombre de fichiers pouvant exister dans une banque de données peut être de 2,1 milliards en raison des restrictions du système de fichiers. Il est probable que le référentiel rencontre des problèmes en raison du grand nombre de nœuds, bien avant d’atteindre la limite de la banque de données.

Si les rendus ne sont pas générés correctement, utilisez la bibliothèque Camera Raw. Toutefois, dans ce cas, le côté le plus long de l’image ne doit pas dépasser 65 000 pixels. En outre, l’image ne doit pas contenir plus de 512 Mpx (512*1024 x 1024 pixels). La taille de la ressource n’a pas d’importance.

Il est difficile d’estimer avec précision la taille du fichier TIFF pris en charge prêt à l’emploi avec un tas spécifique pour [!DNL Experience Manager] en raison de facteurs supplémentaires, tels que la taille des pixels, qui influence le traitement. Il est possible qu’[!DNL Experience Manager] puisse traiter un fichier prêt à l’emploi d’une taille de 255 Mo, mais ne puisse pas traiter un fichier de 18 Mo, parce que ce dernier comprend un nombre inhabituellement plus élevé de pixels par rapport au premier.

## Taille des ressources {#size-of-assets}

Par défaut, [!DNL Experience Manager] vous permet de charger des ressources d’une taille de fichier allant jusqu’à 2 Go. Pour charger des ressources très volumineuses dans [!DNL Experience Manager], consultez [Configuration pour charger des ressources très volumineuses](managing-video-assets.md#configuration-to-upload-assets-that-are-larger-than-gb).
