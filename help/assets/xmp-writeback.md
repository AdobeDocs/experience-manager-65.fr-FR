---
title: Écriture différée XMP sur les rendus
description: Découvrez comment la fonctionnalité d’écriture différée XMP propage les modifications apportées aux métadonnées d’une ressource à l’ensemble des rendus de la ressource ou uniquement à certains d’entre eux.
contentOwner: AG
translation-type: tm+mt
source-git-commit: a39ee0f435dc43d2c2830b2947e91ffdcf11c7f6

---


# Écriture différée XMP sur les rendus {#xmp-writeback-to-renditions}

La fonction Écriture différée XMP d’Adobe Experience Manager (AEM) Assets réplique les modifications des métadonnées de la ressource sur les rendus de la ressource.

Lorsque vous modifiez les métadonnées d’un fichier dans AEM Assets ou lors du transfert du fichier, les modifications sont initialement stockées dans le noeud de fichier dans Crx-De.

La fonction d’écriture différée XMP propage les modifications de métadonnées à tous les rendus ou à des rendus spécifiques du fichier.

Consider a scenario where you modify the Title property of the asset titled `Classic Leather` to `Nylon`.

![metadata](assets/metadata.png)

Dans ce cas, AEM Assets enregistre les modifications apportées à la propriété **Titre** dans le paramètre `dc:title` des métadonnées stockées dans la hiérarchie de la ressource.

![metadata_saved](assets/metadata_stored.png)

Toutefois, AEM Assets ne propage pas automatiquement les modifications apportées aux métadonnées aux rendus d’une ressource.

La fonction d’enregistrement XMP vous permet de propager les modifications de métadonnées à tous les rendus ou à des rendus spécifiques du fichier. Toutefois, les modifications ne sont pas stockées sous le nœud de métadonnées dans la hiérarchie de la ressource. Au lieu de cela, cette fonction incorpore les modifications dans les fichiers binaires pour les rendus.

## Activation de l’écriture différée XMP {#enabling-xmp-writeback}

Pour activer la propagation des modifications apportées aux métadonnées aux rendus de la ressource lors de leur chargement, modifiez la configuration **Créateur de rendus de gestion des actifs numériques Adobe CQ** dans le gestionnaire de configuration.

1. Pour ouvrir Configuration Manager, accédez à `https://[aem_server]:[port]/system/console/configMgr`.
1. Open the **Adobe CQ DAM Rendition Maker** configuration.
1. Sélectionnez l’option **Propager XMP**, puis enregistrez les modifications.

   ![chlimage_1-135](assets/chlimage_1-346.png)

## Activation de l’écriture différée XMP pour des rendus spécifiques {#enabling-xmp-writeback-for-specific-renditions}

Pour laisser la fonction Écriture différée XMP propager les modifications de métadonnées à des rendus spécifiques, spécifiez ces rendus à l’étape de workflow Écriture différée XMP du workflow Écriture différée des métadonnées de gestion des actifs numériques. Par défaut, cette étape est configurée avec le rendu d’origine.

Pour que la fonction Écriture différée XMP propage les métadonnées aux miniatures de rendu 140.100.png et 319.319.png, procédez comme suit :

1. Tap/click the AEM logo, and then navigate to **Tools** > **Workflow** > **Models**.
1. From the Models page, open the **DAM Metadata Writeback** workflow model.
1. In the **DAM Metadata Writeback** properties page, open the **XMP Writeback Process** step.
1. In the Step Properties dialog box, tap/click the **Process** tab.
1. In the **Arguments** box, add `rendition:cq5dam.thumbnail.140.100.png,rendition:cq5dam.thumbnail.319.319.png`, andd then tap/click **OK**.

   ![step_properties](assets/step_properties.png)

1. Enregistrez les modifications.
1. To regenerate the pyramid TIF renditions for Dynamic Media images with the new attributes, add the **Dynamic Media Process Image Assets** step to the DAM Metadata Writeback workflow.

   Les rendus PTIFF sont uniquement créés et stockés localement, dans une implémentation Dynamic Media hybride.

1. Enregistrez le workflow.

Les modifications de métadonnées sont propagées aux rendus thumbnail.140.100.png et thumbnail.319.319.png de la ressource, et non aux autres.

>[!NOTE]
>
>For XMP writeback issues in 64 bit Linux, see [How to enable XMP write-back on 64-bit RedHat Linux](https://helpx.adobe.com/experience-manager/kb/enable-xmp-write-back-64-bit-redhat.html).
>
>For more information about supported platforms, see [XMP metadata write-back prerequisites](/help/sites-deploying/technical-requirements.md#requirements-for-aem-assets-xmp-metadata-write-back).

## Filtrage des métadonnées XMP {#filtering-xmp-metadata}

AEM Assets prend en charge le filtrage des propriétés/noeuds des listes noires et blanches pour les métadonnées XMP lues à partir des fichiers binaires et stockées dans le JCR lorsque des fichiers sont assimilés.

Le filtrage par liste noire vous permet d’importer toutes les propriétés des métadonnées XMP, à l’exception des propriétés spécifiées pour l’exclusion. Cependant, pour les types de ressources tels que les fichiers INDD comportant un très grand nombre de métadonnées XMP (par exemple 1 000 nœuds avec 10 000 propriétés), les noms des nœuds à filtrer ne sont pas toujours connus à l’avance. Si le filtrage par liste noire permet l’importation d’un grand nombre de ressources avec de nombreuses métadonnées XMP, l’instance/cluster AEM peut rencontrer des problèmes de stabilité, par exemple des files d’attente d’observation bloquées.

Le filtrage par liste blanche des métadonnées XMP résout le problème en vous permettant de définir les propriétés XMP à importer. De cette façon, les autres propriétés XMP ou les propriétés XMP inconnues sont ignorées. Vous pouvez ajouter certaines de ces propriétés au filtre par liste noire à des fins de compatibilité descendante.

>[!NOTE]
>
>Le filtrage fonctionne uniquement pour les propriétés dérivées des sources XMP dans les binaires des ressources. Pour les propriétés dérivées de sources autres que XMP, comme les formats EXIF et IPTC, le filtrage ne fonctionne pas. Par exemple, la date de création de la ressource est stockée dans la propriété appelée `CreateDate` dans EXIF TIFF. AEM stocke cette valeur dans le champ de métadonnées appelé `exif:DateTimeOriginal`. Comme la source est autre que XMP, le filtrage ne fonctionne pas sur cette propriété.

1. Pour ouvrir Configuration Manager, accédez à `https://[aem_server]:[port]/system/console/configMgr`.
1. Open the **Adobe CQ DAM XmpFilter** configuration.
1. To apply whitelist filtering, select **Apply Whitelist to XMP Properties**, and specify the properties to be imported in the **Whitelisted XML Names for XMP filtering** box.

   ![chlimage_1-136](assets/chlimage_1-347.png)

1. To filter out blacklisted XMP properties after applying whitelist filtering, specify them in the **Blacklisted XML Names for XMP filtering** box.

   >[!NOTE]
   >
   >L’option **Appliquer la liste noire aux propriétés XMP** est sélectionnée par défaut. Autrement dit, le filtrage par liste noire est activé par défaut. To disable blacklist filtering, unselect the **Apply Blacklist to XMP Properties** option.

1. Enregistrez les modifications.
