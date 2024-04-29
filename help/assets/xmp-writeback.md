---
title: Écriture différée XMP sur les rendus
description: Découvrez comment la fonction d’écriture différée XMP propage les modifications de métadonnées d’une ressource à toutes les versions de la ressource ou seulement à certaines d’entre elles.
contentOwner: AG
role: User, Admin
feature: Metadata
exl-id: 82148ae5-37e9-4fc5-ada9-db3d91b29c33
hide: true
solution: Experience Manager, Experience Manager Assets
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: ht
source-wordcount: '798'
ht-degree: 100%

---

# Écriture différée XMP sur les rendus {#xmp-writeback-to-renditions}

| Version | Lien de l’article |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Cliquez ici](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/admin/xmp-metadata.html?lang=fr) |
| AEM 6.5 | Cet article |

Cette fonction d’écriture différée XMP dans [!DNL Adobe Experience Manager Assets] reproduit les modifications de métadonnées apportées aux rendus de la ressource d’origine. Lorsque vous modifiez les métadonnées d’une ressource à partir d’Assets ou lors du chargement de la ressource, les modifications sont initialement stockées dans le nœud des métadonnées de la hiérarchie des ressources.

La fonction Écriture différée XMP permet de propager les modifications de métadonnées à l’ensemble des rendus de la ressource ou uniquement à certains d’entre eux. La fonctionnalité réécrit uniquement les propriétés de métadonnées qui utilisent des espace de noms enregistrés, c’est-à-dire qu’une propriété nommée `dc:title` est réécrite, mais qu’une propriété nommée `mytitle` ne l’est pas.

Supposons que vous remplaciez la propriété [!UICONTROL Titre] d’une ressource intitulée `Classic Leather` par `Nylon`.

![metadata](assets/metadata.png)

Dans ce cas, [!DNL Experience Manager Assets] enregistre les modifications apportées à la propriété **[!UICONTROL Titre]** dans le paramètre `dc:title` des métadonnées stockées dans la hiérarchie de la ressource.

![metadata_saved](assets/metadata_stored.png)

Toutefois, [!DNL Experience Manager Assets] ne propage pas automatiquement les modifications apportées aux métadonnées dans les rendus d’une ressource. Consultez la section [Activer l’écriture différée XMP](#enable-xmp-writeback).

## Activation de l’écriture différée XMP {#enable-xmp-writeback}

Pour activer la propagation des modifications apportées aux métadonnées aux rendus de la ressource lors de leur chargement, modifiez la configuration **[!UICONTROL Créateur de rendus de gestion des actifs numériques Adobe CQ]** dans Configuration Manager.

1. Pour ouvrir Configuration Manager, accédez à `https://[aem_server]:[port]/system/console/configMgr`.
1. Ouvrez la configuration **[!UICONTROL Créateur de rendus de gestion des actifs numériques Adobe CQ]**.
1. Sélectionnez l’option **[!UICONTROL Propager XMP]**, puis enregistrez les modifications.

   ![chlimage_1-135](assets/chlimage_1-346.png)

## Activation de l’écriture différée XMP pour des rendus spécifiques {#enabling-xmp-writeback-for-specific-renditions}

Pour permettre à la fonction Écriture différée XMP de propager les modifications de métadonnées à des rendus spécifiques, spécifiez ces rendus à l’étape de workflow Écriture différée XMP du workflow [!UICONTROL Écriture différée des métadonnées de gestion des ressources numériques]. Par défaut, cette étape est configurée avec le rendu d’origine.

Pour que la fonctionnalité d’écriture différée XMP propage les métadonnées aux miniatures des rendus 140.100.png et 319.319.png, suivez ces étapes.

1. Dans l’interface d’Experience Manager, accédez à **[!UICONTROL Outils]** > **[!UICONTROL Workflow]** > **[!UICONTROL Modèles]**.
1. Sur la page Modèles, ouvrez le modèle de workflow **[!UICONTROL Écriture différée des métadonnées de gestion des actifs numériques]**.
1. Sur la page de propriétés **[!UICONTROL Écriture différée des métadonnées de gestion des actifs numériques]**, ouvrez l’étape **[!UICONTROL Processus d’écriture différée XMP]**.
1. Dans la boîte de dialogue [!UICONTROL Propriétés des étapes], cliquez sur l’onglet **[!UICONTROL Processus]**.
1. Dans la zone **Arguments**, ajoutez `rendition:cq5dam.thumbnail.140.100.png,rendition:cq5dam.thumbnail.319.319.png`, et cliquez sur **[!UICONTROL OK]**.

   ![step_properties](assets/step_properties.png)

1. Enregistrez les modifications.
1. Afin de régénérer les rendus Pyramid TIFF pour les images [!DNL Dynamic Media] avec les nouveaux attributs, ajoutez l’étape **[!UICONTROL Ressources d’image du processus Dynamic Media]** au workflow [!UICONTROL Écriture différée des métadonnées de gestion des ressources numériques].

   Les rendus PTIFF sont uniquement créés et conservés localement dans une implémentation hybride de Dynamic Media.

1. Enregistrez le workflow.

Les modifications apportées aux métadonnées sont propagées aux rendus thumbnail.140.100.png et thumbnail.319.319.png de la ressource uniquement.

>[!NOTE]
>
>Si vous rencontrez des problèmes liés à l’écriture différée XMP sous Linux 64 bits, consultez la section [Activation de l’écriture différée XMP sous Red Hat Linux 64 bits](https://helpx.adobe.com/fr/experience-manager/kb/enable-xmp-write-back-64-bit-redhat.html).
>
>Pour connaître les plateformes prises en charge, consultez les [Conditions préalables à l’écriture différée des métadonnées XMP](/help/sites-deploying/technical-requirements.md#requirements-for-aem-assets-xmp-metadata-write-back).

## Filtrage des métadonnées XMP {#filtering-xmp-metadata}

[!DNL Experience Manager Assets] prend en charge le filtrage par liste bloquée et par liste autorisée de propriétés/nœuds pour les métadonnées XMP qui sont lues à partir de binaires de ressources et stockées dans JCR quand les ressources sont ingérées.

Le filtrage par liste bloquée permet d’importer toutes les propriétés des métadonnées XMP, à l’exception des propriétés spécifiées pour l’exclusion. Cependant, pour les types de ressources tels que les fichiers INDD comportant un très grand nombre de métadonnées XMP (par exemple 1 000 nœuds avec 10 000 propriétés), les noms des nœuds à filtrer ne sont pas toujours connus à l’avance. Si le filtrage par liste bloquée permet l’importation d’un grand nombre de ressources avec de nombreuses métadonnées XMP, le déploiement d’[!DNL Experience Manager] peut rencontrer des problèmes de stabilité, par exemple des files d’attente d’observation bloquées.

Le filtrage par liste autorisée des métadonnées XMP résout le problème en vous permettant de définir les propriétés XMP à importer. De cette façon, les autres propriétés XMP ou les propriétés XMP inconnues sont ignorées. Pour une compatibilité ascendante, vous pouvez ajouter certaines de ces propriétés au filtre qui utilise une liste bloquée.

>[!NOTE]
>
>Le filtrage fonctionne uniquement pour les propriétés dérivées des sources XMP dans les fichiers binaires de ressources. Pour les propriétés dérivées de sources non XMP, telles que les formats EXIF et IPTC, le filtrage ne fonctionne pas. Par exemple, la date de création de la ressource est stockée dans la propriété appelée `CreateDate` dans EXIF TIFF. Experience Manager stocke cette valeur dans un champ de métadonnées nommé `exif:DateTimeOriginal`. Comme la source est autre que XMP, le filtrage ne fonctionne pas sur cette propriété.

1. Pour ouvrir Configuration Manager, accédez à `https://[aem_server]:[port]/system/console/configMgr`.
1. Ouvrez la configuration **[!UICONTROL Filtre XMP de gestion des actifs numériques Adobe CQ]**.
1. Pour appliquer un filtrage par liste autorisée, sélectionnez **[!UICONTROL Appliquer la liste autorisée aux propriétés XMP]**, puis spécifiez les propriétés à importer dans la zone **[!UICONTROL Noms XML autorisés pour le filtrage XMP]**.

   ![chlimage_1-136](assets/chlimage_1-347.png)

1. Pour filtrer les propriétés XMP bloquées après l’application du filtrage par liste autorisée, spécifiez celles qui se trouvent dans la zone **[!UICONTROL Noms XML bloqués pour le filtrage XMP]**.

   >[!NOTE]
   >
   >L’option **[!UICONTROL Appliquer la liste bloquée aux propriétés XMP]** est sélectionnée par défaut. En d’autres termes, le filtrage à l’aide d’une liste bloquée est activé par défaut. Pour désactiver ce type de filtrage, désélectionnez l’option **[!UICONTROL Appliquer la liste bloquée aux propriétés XMP]**.

1. Enregistrez les modifications.
