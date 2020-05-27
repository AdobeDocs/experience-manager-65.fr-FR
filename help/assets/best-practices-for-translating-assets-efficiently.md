---
title: Meilleures pratiques de traduction des ressources
description: Meilleures pratiques pour une gestion efficace des ressources afin de synchroniser les diverses versions traduites et de rationaliser les workflows de traduction.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 566add37d6dd7efe22a99fc234ca42878f050aee
workflow-type: tm+mt
source-wordcount: '497'
ht-degree: 82%

---


# Meilleures pratiques de traduction des ressources {#best-practices-for-translating-assets-efficiently}

Adobe Experience Manager Assets prend en charge des workflows multilingues pour traduire des fichiers binaires, des métadonnées et des balises pour les ressources numériques en plusieurs langues et pour gérer les ressources traduites. Pour plus d’informations, voir [Ressources multilingues](multilingual-assets.md).

Pour une gestion efficace des ressources et pour garantir la synchronisation des différentes versions traduites, créez des [copies de langue](preparing-assets-for-translation.md) des ressources avant d’exécuter les workflows de traduction.

Une copie de langue d’une ressource ou d’un groupe de ressources est un frère de langue (ou une version de la ou des ressources dans une langue apparentée) avec une hiérarchie de contenu similaire.

Chaque copie de langue est une ressource indépendante. Par conséquent, la traduction des ressources dans plusieurs paramètres régionaux peut considérablement augmenter la taille du référentiel CRX. Par exemple, la traduction de ressources d’une taille combinée de 10 Go en deux langues peut augmenter la taille du référentiel d’environ 20 Go (10 Go pour chaque langue).

Les fichiers binaires des ressources occupent un espace de stockage beaucoup plus important que les métadonnées et les balises. Par conséquent, si la traduction des métadonnées et des balises est suffisante pour atteindre votre objectif, omettez de traduire les fichiers binaires. Vous pouvez conserver la copie d’origine des fichiers binaires dans le référentiel pour une association avec des métadonnées et des balises traduites dans différents paramètres régionaux. La conservation d’une copie unique des fichiers binaires, au lieu de plusieurs versions traduites, minimise l’impact sur la taille du référentiel.

L’entrepôt de données basé sur les fichiers et l’entrepôt de données Amazon S3 fournissent une infrastructure de stockage mieux adaptée à ces scénarios. Ces référentiels de stockage enregistrent une copie unique des fichiers binaires des ressources (y compris les rendus) pouvant être partagée en fonction des métadonnées et des balises dans plusieurs paramètres régionaux. Par conséquent, la création de copies de langue des ressources et la traduction des métadonnées et des balises n’affectent pas la taille du référentiel.

Vous pouvez également apporter des modifications de configuration à quelques workflow et à la structure d’intégration de traduction afin de rationaliser davantage le workflow.

1. Utilisez l’une des méthodes suivantes :

   * [Configurer l’entrepôt de données basé sur les fichiers](/help/sites-deploying/data-store-config.md)
   * [Configurer l’entrepôt de données Amazon S3](/help/sites-deploying/data-store-config.md)

1. Disable the [DAM MetaData Write-back](/help/sites-administering/workflow-offloader.md#disable-offloading) workflow.

   Comme son nom l’indique, le workflow [!UICONTROL Écriture différée des métadonnées de gestion des actifs numériques] réécrit les métadonnées sur le fichier binaire. Comme les métadonnées changent après la traduction, l’écriture différée sur le fichier binaire génère un fichier binaire différent pour chaque copie de langue.

   >[!NOTE]
   >
   >La désactivation du workflow [!UICONTROL Écriture différée des métadonnées de gestion des actifs numériques] désactive l’écriture différée des métadonnées XMP sur les fichiers binaires des ressources. Par conséquent, les modifications futures des métadonnées ne sont plus enregistrées dans les ressources. Évaluez les conséquences avant de désactiver ce workflow.

1. Activez le workflow [!UICONTROL Définir la date de dernière modification].

   Le workflow [!UICONTROL Définir la date de dernière modification] configure la date de dernière modification pour une ressource. Comme vous désactivez ce processus à l’étape 2, Assets ne peut plus tenir à jour la date de dernière modification des ressources. Par conséquent, activez le workflow *Définir la date de dernière modification* pour vous assurer que les dates de dernière modification des ressources sont à jour. Les ressources dont les dates de dernière modification sont obsolètes peuvent entraîner des erreurs.

1. [Configurez la structure d’intégration de traduction](/help/sites-administering/tc-tic.md) pour arrêter la traduction des fichiers binaires des ressources. Unselect the **[!UICONTROL Translate Assets]** option under the Assets tab to stop the translation of Asset binaries.
1. Translate asset metadata/tags using [Multilingual asset workflows](multilingual-assets.md).
