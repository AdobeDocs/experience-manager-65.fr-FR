---
title: Écriture différée XMP sur les rendus
description: Découvrez comment la fonctionnalité d’écriture différée XMP propage les modifications apportées aux métadonnées d’une ressource à l’ensemble des rendus de la ressource ou uniquement à certains d’entre eux.
contentOwner: AG
role: User, Admin
feature: Metadata
exl-id: 82148ae5-37e9-4fc5-ada9-db3d91b29c33
source-git-commit: 9d5440747428830a3aae732bec47d42375777efd
workflow-type: tm+mt
source-wordcount: '819'
ht-degree: 63%

---

# Écriture différée XMP sur les rendus {#xmp-writeback-to-renditions}

| Version | Lien de l’article |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Cliquez ici.](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/admin/xmp-metadata.html?lang=en) |
| AEM 6.5 | Cet article |
| AEM 6.4 | [Cliquez ici.](https://experienceleague.adobe.com/docs/experience-manager-64/assets/administer/xmp-writeback.html?lang=en) |

Cette fonction d’écriture différée XMP dans [!DNL Adobe Experience Manager Assets] reproduit les modifications de métadonnées apportées aux rendus de la ressource d’origine. Lorsque vous modifiez les métadonnées d’une ressource à partir d’Assets ou lors du chargement de la ressource, les modifications sont initialement stockées dans le noeud de métadonnées de la hiérarchie de la ressource.

La fonction Écriture différée XMP permet de propager les modifications de métadonnées à l’ensemble des rendus de la ressource ou uniquement à certains d’entre eux. La fonction réécrit uniquement les propriétés de métadonnées qui utilisent l’espace de noms `jcr`, c’est-à-dire qu’une propriété nommée `dc:title` est réécrite, mais qu’une propriété nommée `mytitle` ne l’est pas.

Supposons que vous remplaciez la propriété [!UICONTROL Titre] d’une ressource intitulée `Classic Leather` par `Nylon`.

![metadata](assets/metadata.png)

Dans ce cas, la variable [!DNL Experience Manager Assets] enregistre les modifications apportées au **[!UICONTROL Titre]** dans la propriété `dc:title` pour les métadonnées de la ressource stockées dans la hiérarchie de la ressource.

![metadata_saved](assets/metadata_stored.png)

Toutefois, [!DNL Experience Manager Assets] ne propage pas automatiquement les modifications apportées aux métadonnées aux rendus d’une ressource. Voir [Comment activer l’écriture différée XMP](#enable-xmp-writeback).

## Activer l’écriture différée XMP {#enable-xmp-writeback}

Pour activer la propagation des modifications apportées aux métadonnées aux rendus de la ressource lors de leur chargement, modifiez la configuration **[!UICONTROL Créateur de rendus de gestion des actifs numériques Adobe CQ]** dans Configuration Manager.

1. Pour ouvrir Configuration Manager, accédez à `https://[aem_server]:[port]/system/console/configMgr`.
1. Ouvrez la configuration **[!UICONTROL Créateur de rendus de gestion des actifs numériques Adobe CQ]**.
1. Sélectionnez l’option **[!UICONTROL Propager XMP]**, puis enregistrez les modifications.

   ![chlimage_1-135](assets/chlimage_1-346.png)

## Activation de l’écriture différée XMP pour des rendus spécifiques {#enabling-xmp-writeback-for-specific-renditions}

Pour laisser la fonction Écriture différée XMP propager les modifications de métadonnées à des rendus spécifiques, spécifiez ces rendus à l’étape XMP processus d’écriture différée de [!UICONTROL Écriture différée des métadonnées de gestion des actifs numériques] workflow. Par défaut, cette étape est configurée avec le rendu d’origine.

Pour que la fonction Écriture différée XMP propage les métadonnées aux miniatures de rendu 140.100.png et 319.319.png, procédez comme suit :

1. Dans l’interface du Experience Manager, accédez à **[!UICONTROL Outils]** > **[!UICONTROL Workflow]** > **[!UICONTROL Modèles]**.
1. Sur la page Modèles, ouvrez le modèle de workflow **[!UICONTROL Écriture différée des métadonnées de gestion des actifs numériques]**.
1. Sur la page de propriétés **[!UICONTROL Écriture différée des métadonnées de gestion des actifs numériques]**, ouvrez l’étape **[!UICONTROL Processus d’écriture différée XMP]**.
1. Dans le [!UICONTROL Propriétés de l’étape] , cliquez sur **[!UICONTROL Processus]** .
1. Dans le **Arguments** box, ajouter `rendition:cq5dam.thumbnail.140.100.png,rendition:cq5dam.thumbnail.319.319.png`, puis cliquez sur **[!UICONTROL OK]**.

   ![step_properties](assets/step_properties.png)

1. Enregistrez les modifications.
1. Pour régénérer les rendus de TIFF pyramidaux pour [!DNL Dynamic Media] images avec les nouveaux attributs, ajoutez le **[!UICONTROL Ressources d’image de processus Dynamic Media]** à l’étape [!UICONTROL Écriture différée des métadonnées de gestion des actifs numériques] workflow.

   Les rendus PTIFF sont uniquement créés et conservés localement dans une implémentation hybride Dynamic Media.

1. Enregistrez le workflow.

Les modifications apportées aux métadonnées sont propagées aux rendus thumbnail.140.100.png et thumbnail.319.319.png de la ressource uniquement.

>[!NOTE]
>
>Pour XMP problèmes d’écriture différée sous Linux 64 bits, voir [Comment activer l’écriture différée XMP sous RedHat Linux 64 bits](https://helpx.adobe.com/experience-manager/kb/enable-xmp-write-back-64-bit-redhat.html).
>
>Pour les plateformes prises en charge, voir [XMP conditions préalables à l’écriture différée des métadonnées](/help/sites-deploying/technical-requirements.md#requirements-for-aem-assets-xmp-metadata-write-back).

## Filtrage des métadonnées XMP {#filtering-xmp-metadata}

[!DNL Experience Manager Assets] prend en charge le filtrage de liste bloquée et de liste autorisée des propriétés/noeuds pour XMP métadonnées lues à partir de binaires de ressources et stockées dans JCR lorsque des ressources sont ingérées.

Le filtrage par liste bloquée permet d’importer toutes les propriétés des métadonnées XMP, à l’exception des propriétés spécifiées pour l’exclusion. Cependant, pour les types de ressources tels que les fichiers INDD comportant un très grand nombre de métadonnées XMP (par exemple 1 000 nœuds avec 10 000 propriétés), les noms des nœuds à filtrer ne sont pas toujours connus à l’avance. Si le filtrage à l’aide d’une liste bloquée permet l’importation d’un grand nombre de ressources avec de nombreuses métadonnées XMP, la variable [!DNL Experience Manager] Le déploiement peut rencontrer des problèmes de stabilité, par exemple des files d’attente d’observation bloquées.

Le filtrage par liste autorisée des métadonnées XMP résout le problème en vous permettant de définir les propriétés XMP à importer. De cette façon, toute propriété XMP autre ou inconnue est ignorée. Pour une compatibilité ascendante, vous pouvez ajouter certaines de ces propriétés au filtre qui utilise une liste bloquée.

>[!NOTE]
>
>Le filtrage fonctionne uniquement pour les propriétés dérivées des sources XMP dans les binaires des ressources. Pour les propriétés dérivées de sources autres que XMP, comme les formats EXIF et IPTC, le filtrage ne fonctionne pas. Par exemple, la date de création de la ressource est stockée dans la propriété appelée `CreateDate` dans EXIF TIFF. Experience Manager stocke cette valeur dans un champ de métadonnées nommé `exif:DateTimeOriginal`. Comme la source est autre que XMP, le filtrage ne fonctionne pas sur cette propriété.

1. Pour ouvrir Configuration Manager, accédez à `https://[aem_server]:[port]/system/console/configMgr`.
1. Ouvrez la configuration **[!UICONTROL Filtre XMP de gestion des actifs numériques Adobe CQ]**.
1. Pour appliquer un filtrage par liste autorisée, sélectionnez **[!UICONTROL Appliquer la liste autorisée aux propriétés XMP]**, puis spécifiez les propriétés à importer dans l’encadré **[!UICONTROL Noms XML autorisés pour le filtrage XMP]**.

   ![chlimage_1-136](assets/chlimage_1-347.png)

1. Pour filtrer les propriétés XMP bloquées après avoir appliqué le filtrage par liste autorisée, spécifiez celles indiquées dans la variable **[!UICONTROL Noms XML bloqués pour le filtrage XMP]** de la boîte.

   >[!NOTE]
   >
   >L’option **[!UICONTROL Appliquer la liste bloquée aux propriétés XMP]** est sélectionnée par défaut. En d’autres termes, le filtrage à l’aide d’une liste bloquée est activé par défaut. Pour désactiver ce type de filtrage, annulez la sélection de la variable **[!UICONTROL Appliquer la Liste bloquée aux propriétés XMP]** .

1. Enregistrez les modifications.
