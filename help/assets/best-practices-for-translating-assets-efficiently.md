---
title: Meilleures pratiques de traduction des ressources
description: Meilleures pratiques pour une gestion efficace des ressources afin de synchroniser les diverses versions traduites et de rationaliser les workflows de traduction.
contentOwner: AG
role: Administrator
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '417'
ht-degree: 87%

---


# Meilleures pratiques pour traduire des ressources {#best-practices-for-translating-assets-efficiently}

[!DNL Adobe Experience Manager Assets] prend en charge des workflow multilingues permettant de traduire les fichiers binaires, les métadonnées et les balises des ressources numériques en plusieurs paramètres régionaux et de gérer les ressources traduites. Pour plus d’informations, voir [Ressources multilingues](multilingual-assets.md).

Pour une gestion efficace des ressources et pour garantir la synchronisation des différentes versions traduites, créez des [copies de langue](preparing-assets-for-translation.md) des ressources avant d’exécuter les workflows de traduction.

Une copie de langue d’une ressource ou d’un groupe de ressources est un frère de langue (ou une version de la ou des ressources dans une langue apparentée) avec une hiérarchie de contenu similaire.

Chaque copie de langue est une ressource indépendante. Par conséquent, la traduction des ressources dans plusieurs paramètres régionaux peut considérablement augmenter la taille du référentiel CRX. Par exemple, la traduction de ressources d’une taille combinée de 10 Go en deux langues peut augmenter la taille du référentiel d’environ 20 Go (10 Go pour chaque langue).

Les fichiers binaires des ressources occupent un espace de stockage beaucoup plus important que les métadonnées et les balises. Par conséquent, si la traduction des métadonnées et des balises est suffisante pour atteindre votre objectif, omettez de traduire les fichiers binaires. Vous pouvez conserver la copie d’origine des fichiers binaires dans le référentiel pour une association avec des métadonnées et des balises traduites dans différents paramètres régionaux. La conservation d’une copie unique des fichiers binaires, au lieu de plusieurs versions traduites, minimise l’impact sur la taille du référentiel.

L’entrepôt de données basé sur les fichiers et l’entrepôt de données Amazon S3 fournissent une infrastructure de stockage mieux adaptée à ces scénarios. Ces référentiels de stockage enregistrent une copie unique des fichiers binaires des ressources (y compris les rendus) pouvant être partagée en fonction des métadonnées et des balises dans plusieurs paramètres régionaux. Par conséquent, la création de copies de langue des ressources et la traduction des métadonnées et des balises n’affectent pas la taille du référentiel.

Vous pouvez également apporter des modifications de configuration à quelques workflow et à la structure d’intégration de traduction afin de rationaliser davantage le workflow.

1. Utilisez l’une des méthodes suivantes :

   * [Configurer l’entrepôt de données basé sur les fichiers](/help/sites-deploying/data-store-config.md)
   * [Configurer l’entrepôt de données Amazon S3](/help/sites-deploying/data-store-config.md)

<!--
1. Disable the [DAM MetaData Write-back](/help/sites-administering/workflow-offloader.md#disable-offloading) workflow.

   As the name suggests, the [!UICONTROL DAM Metadata Writeback] workflow rewrites the metadata to the binary file. Because the metadata changes after translation, writing it back to the binary file generates a different binary for a language copy.

   >[!NOTE]
   >
   >Disabling the [!UICONTROL DAM MetaData Writeback] workflow turns off XMP metadata write-back on asset binaries. Consequently, future metadata changes are no longer be saved within the assets. Evaluate the consequences before disabling this workflow.
-->

1. Activez le workflow [!UICONTROL Définir la date de dernière modification].

   Le workflow [!UICONTROL Définir la date de dernière modification] configure la date de dernière modification pour une ressource. Comme vous désactivez ce processus à l’étape 2, [!DNL Assets] ne peut plus tenir à jour la date de dernière modification des ressources. Par conséquent, activez le workflow *Définir la date de dernière modification* pour vous assurer que les dates de dernière modification des ressources sont à jour. Les ressources dont les dates de dernière modification sont obsolètes peuvent entraîner des erreurs.

1. [Configurez la structure d’intégration de traduction](/help/sites-administering/tc-tic.md) pour arrêter la traduction des fichiers binaires des ressources. Désélectionnez l’option **[!UICONTROL Traduire les ressources]** sous l’onglet [!UICONTROL Ressources] pour arrêter la traduction des fichiers binaires.
1. Traduisez les métadonnées/balises de fichier à l’aide de [workflows de ressources multilingues](multilingual-assets.md).
