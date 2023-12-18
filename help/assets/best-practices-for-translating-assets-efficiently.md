---
title: Bonnes pratiques relatives à la traduction des ressources
description: Bonnes pratiques pour une gestion efficace des ressources afin de synchroniser les diverses versions traduites et de rationaliser les workflows de traduction.
contentOwner: AG
role: Admin
feature: Asset Management
exl-id: e632dcdb-b2b9-45bc-89e7-337b44b6fc61
source-git-commit: 259f257964829b65bb71b5a46583997581a91a4e
workflow-type: ht
source-wordcount: '415'
ht-degree: 100%

---

# Bonnes pratiques relatives à la traduction des ressources {#best-practices-for-translating-assets-efficiently}

[!DNL Adobe Experience Manager Assets] prend en charge des workflow multilingues permettant de traduire les fichiers binaires, les métadonnées et les balises des ressources numériques dans plusieurs paramètres régionaux et de gérer les ressources traduites. Pour plus d’informations, consultez [Ressources multilingues](multilingual-assets.md).

Pour une gestion efficace des ressources afin de garantir que les différentes versions traduites restent synchronisées, créez des [copies de langue](preparing-assets-for-translation.md) pour les ressources avant d’exécuter des workflows de traduction.

La copie de langue d’une ressource ou d’un groupe de ressources est un parent de langue (ou une version des ressources dans une langue commune) avec une hiérarchie de contenu similaire.

Chaque copie de langue est une ressource indépendante. Par conséquent, la traduction de ressources en plusieurs paramètres régionaux peut augmenter considérablement la taille du référentiel CRX. Par exemple, la traduction de ressources d’une taille combinée de 10 Go en deux langues peut augmenter la taille du référentiel d’environ 20 Go (10 Go pour chaque langue).

Les fichiers binaires des ressources occupent un espace de stockage beaucoup plus important que les métadonnées et les balises. Par conséquent, si la traduction des métadonnées et des balises est adaptée à votre objectif, omettez de traduire les binaires. Vous pouvez conserver la copie d’origine des binaires dans le référentiel pour l’associer aux métadonnées et aux balises traduites dans différents paramètres régionaux. La conservation d’une seule copie de binaires, au lieu de plusieurs versions traduites, réduit l’impact sur la taille du référentiel.

File Data Store et Amazon S3 Data Store fournissent une infrastructure de stockage qui convient le mieux à ces scénarios. Ces référentiels de stockage stockent une seule copie des binaires de ressources (y compris les rendus) qui peut être partagée par les métadonnées et les balises dans plusieurs paramètres régionaux. Par conséquent, la création de copies de langue de ressource et la traduction des métadonnées et des balises n’ont aucune incidence sur la taille du référentiel.

Vous pouvez également apporter quelques modifications de configuration à quelques workflows et à la structure d’intégration de traduction afin de rationaliser davantage le processus.

1. Utilisez l’une des méthodes suivantes :

   * [Configurer le magasin de données basé sur les fichiers](/help/sites-deploying/data-store-config.md)
   * [Configurer le magasin de données Amazon S3](/help/sites-deploying/data-store-config.md)

<!--
1. Disable the [DAM MetaData Write-back](/help/sites-administering/workflow-offloader.md#disable-offloading) workflow.

   As the name suggests, the [!UICONTROL DAM Metadata Writeback] workflow rewrites the metadata to the binary file. Because the metadata changes after translation, writing it back to the binary file generates a different binary for a language copy.

   >[!NOTE]
   >
   >Disabling the [!UICONTROL DAM MetaData Writeback] workflow turns off XMP metadata write-back on asset binaries. Consequently, future metadata changes are no longer be saved within the assets. Evaluate the consequences before disabling this workflow.
-->

1. Activez le workflow [!UICONTROL Définir la date de dernière modification].

   Le workflow [!UICONTROL Écriture différée des métadonnées de gestion des ressources numériques] configure la date de dernière modification d’une ressource. Comme vous désactivez ce workflow à l’étape 2, [!DNL Assets] n’est plus en mesure de maintenir à jour la date de dernière modification des ressources. Par conséquent, activez le workflow *Définir la date de dernière modification* pour vous assurer que les dates de dernière modification des ressources sont à jour. Les ressources dont les dates de dernière modification sont obsolètes peuvent entraîner des erreurs.

1. [Configurez le framework d’intégration de traduction](/help/sites-administering/tc-tic.md) pour arrêter la traduction des fichiers binaires de ressources. Désactivez l’option **[!UICONTROL Traduire les ressources]** dans l’onglet [!UICONTROL Ressources] pour arrêter la traduction des fichiers binaires des ressources.
1. Traduisez les métadonnées/balises des ressources à l’aide des [workflow des ressources multilingues](multilingual-assets.md).
