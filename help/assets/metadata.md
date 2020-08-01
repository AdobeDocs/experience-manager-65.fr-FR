---
title: Gestion des métadonnées des ressources numériques dans  [!DNL Adobe Experience Manager].
description: Découvrez les types de métadonnées ainsi que l’organisation et le traitement des fichiers par  [!DNL Adobe Experience Manager Assets] helps manage metadata for assets to allow easier categorization and organization of assets. [!DNL Experience Manager] en fonction de leurs métadonnées.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 9fc1201db83ae0d3bb902d4dc3ab6d78cc1dc251
workflow-type: tm+mt
source-wordcount: '1412'
ht-degree: 99%

---


# Gestion des métadonnées des ressources numériques {#managing-metadata-for-digital-assets}

[!DNL Adobe Experience Manager Assets] conserve les métadonnées de chaque fichier. Cela permet d’obtenir une catégorisation et une organisation plus simples des ressources, ainsi que d’aider les personnes qui recherchent une ressource spécifique. Grâce à la possibilité d’extraire les métadonnées à partir des fichiers chargés sur [!DNL Experience Manager Assets], la gestion des métadonnées s’intègre aux workflows créatifs. La possibilité de conserver et de gérer les métadonnées de vos fichiers permet aussi d’organiser et de traiter automatiquement les fichiers en fonction de leurs métadonnées.

* [Métadonnées XMP](xmp.md).
* [Modification ou ajout de métadonnées](meta-edit.md).
* [Référence](meta-ref.md)des schémas de métadonnées.

<!--  TBD: Complete this section. Take help from Metadata IRD for DDAM. Also, look at metadata features in Forrester analysis.

## Understand metadata handling in Experience Manager {#metadata-possibilities-with-aem}

Describe the journey of an assets' metadata. What all happens to metadata when an asset is added to Experience Manager.

## Add metadata to your digital assets {#add-metadata}

Typically, the applications that create digital assets add some metadata to the assets created. Before uploading an asset to Experience Manager, you can edit and modify metadata using either the native application used to create an asset or using some metadata editors. When you upload an asset to Experience Manager, the metadata is processed.

## Metadata of assets, folders, and collections {#metadata-of-assets-folders-collections}

## Modify metadata of an asset, folder, or collection {#modify-metadata}

## Modify metadata in bulk {#modify-metadata-in-bulk}

[!DNL Adobe Enterprise Manager Assets] lets you edit the metadata of multiple assets simultaneously so you can quickly propagate common metadata changes to assets in bulk. You can also edit the metadata for multiple collections in bulk.

Use the properties page to perform metadata changes on multiple assets or collections:

* Change metadata properties to a common value
* Add or modify tags

To customize the metadata properties page, including adding, modifying, deleting metadata properties, use the schema editor.

>[!NOTE]
>
>The bulk editing methods work for assets available in a folder or a collection. For the assets that are available across folders or match a common criteria, it is possible to [bulk update the metadata after searching](search-assets.md#metadataupdates).

1. In the [!DNL Assets] user interface, navigate to the location of the assets you want to edit.
1. Select the assets for which you want to edit common properties.
1. From the toolbar, click **[!UICONTROL Properties]** to open the properties page for the selected assets.

   >[!NOTE]
   >
   >When you select multiple assets, the lowest common parent form is selected for the assets. In other words, the properties page only displays metadata fields that are common across the properties pages of all the individual assets.

1. Modify the metadata properties for selected assets under the various tabs.
1. To view the metadata editor for a specific asset, deselect the remaining assets in the list. The metadata editor fields are populated with the metadata for the particular asset.

   >[!NOTE]
   >
   >* In the properties page, you can remove assets from the asset list by deselecting them. The asset list has all the assets selected by default. The metadata for assets that you remove from the list is not updated.
   >* At the top of assets list, select the check box near **[!UICONTROL Title]** to toggle between selecting the assets and clearing the list.

1. To select a different metadata schema for the assets, click **[!UICONTROL Settings]** from the toolbar, and select the desired schema.
1. Save the changes.
1. To append the new metadata with the existing metadata in fields that contain multiple values, select **[!UICONTROL Append mode]**. If you do not select this option, the new metadata replaces the existing metadata in the fields. click **[!UICONTROL Submit]**.

   >[!CAUTION]
   >
   >For single-value fields, the new metadata is not appended to the existing value in the field even if you select **[!UICONTROL Append mode]**.

## Configure limit for bulk metadata update {#limit-bulk-metadata-updates}

To prevent DOS like situation, Enterprise Manager limits the number of parameters supported in a Sling request. When updating metadata of many assets in one go, you may reach the limit and the metadata does not get updated for more assets. Enterprise Manager generates the following warning in the logs:

`org.apache.sling.engine.impl.parameters.Util Too many name/value pairs, stopped processing after 10000 entries`

To change the limit, access **[!UICONTROL Tools]** > **[!UICONTROL Operations]** > **[!UICONTROL Web Console]** and change the value of **[!UICONTROL Maximum POST Parameters]** in **[!UICONTROL Apache Sling Request Parameter Handling]** OSGi configuration.

-->

## Pourquoi les métadonnées sont nécessaires {#why-we-need-metadata}

Les métadonnées sont des données de description des données. À cet égard, elles font référence à vos ressources numériques (ou actifs), par exemple une image. Les métadonnées sont essentielles pour gérer efficacement des ressources.

Elles constituent un ensemble de toutes les données disponibles pour cette image, mais sans qu’elles y soient contenues. Voici quelques exemples de métadonnées :

* Nom de la ressource.
* Heure et date de la dernière modification.
* Taille de la ressource au moment du stockage dans le référentiel.
* Nom du dossier où elle se trouve.
* Ressources connexes ou balises appliquées.

Les propriétés de métadonnées de base décrites ci-dessus sont utilisées par [!DNL Experience Manager] pour gérer les ressources et permettre aux utilisateurs de les visualiser. Par exemple, ordonner les ressources selon la date de leur dernière modification est utile pour identifier des ressources ajoutées récemment.

Vous pouvez ajouter d’autres données de niveau supérieur à des ressources numériques, par exemple :

* Type de ressource (s’agit-il d’une image, d’une vidéo, d’un clip audio ou d’un document ?).
* Propriétaire.
* Intitulé.
* Description.
* Balises affectées à cette ressource.

D’autres métadonnées permettent de classer les fichiers de manière plus détaillée à mesure que le volume d’informations numériques augmente. Il est ainsi possible de gérer quelques centaines de fichiers en ne prenant en compte que leurs noms. Pour autant, cette approche n’est pas évolutive. Elle est insuffisante si le nombre de personnes concernées et la quantité de ressources gérées augmentent.

Avec l’ajout de métadonnées, la valeur d’une ressource numérique augmente, car elle devient :

* plus accessible : les systèmes et les utilisateurs peuvent la trouver facilement ;
* plus facile à gérer : vous pouvez rechercher plus facilement des ressources avec un même ensemble de propriétés et leur apporter des modifications ;
* complète : la ressource contient davantage d’informations et de contexte grâce à un plus grand nombre de métadonnées.

Ainsi, [!DNL Assets] vous fournit les moyens adéquats pour créer, gérer et échanger des métadonnées pour vos ressources numériques.

## Types de métadonnées {#types-of-metadata}

Les deux types de métadonnées de base sont les métadonnées techniques et les métadonnées descriptives.

Les métadonnées techniques sont utiles pour les applications logicielles qui traitent des ressources numériques. Elles ne doivent pas être gérées manuellement. [!DNL Experience Manager Assets] et d’autres logiciels déterminent automatiquement les métadonnées techniques qui peuvent changer lorsque la ressource est modifiée. Les métadonnées techniques disponibles d’une ressource dépendent largement de son type de fichier. Voici quelques exemples de métadonnées techniques :

* taille d’un fichier ;
* dimensions (hauteur et largeur) d’une image ;
* débit d’un fichier audio ou vidéo ;
* résolution (niveau de détail) d’une image.

Les métadonnées descriptives concernent le domaine d’application, par exemple l’entreprise d’où provient un fichier et ne peuvent pas être déterminées automatiquement. Elles sont créées manuellement ou semi-automatiquement. Par exemple, une caméra GPS peut automatiquement suivre la latitude et la longitude et ajouter un balisage géographique à l’image.

La création manuelle d’informations descriptives de métadonnées coûte cher. Des normes ont donc été mises en place pour faciliter l’échange de métadonnées entre les systèmes logiciels et les organisations. [!DNL Experience Manager Assets] prend en charge l’ensemble des normes pertinentes pour la gestion des métadonnées.

## Normes de codage {#encoding-standards}

Il existe différentes manières d’incorporer des métadonnées dans des fichiers. Un certain nombre de normes de codage sont prises en charge :

* XMP : utilisé par [!DNL Assets] pour stocker les métadonnées extraites dans le référentiel.
* ID3 : pour les fichiers audio et vidéo.
* Exif : pour les fichiers image.
* Autres normes/normes héritées : [!DNL Microsoft Word], [!DNL PowerPoint], [!DNL Excel], etc.

### XMP {#xmp}

[!DNL Extensible Metadata Platform] (XMP) est une norme ouverte utilisée par [!DNL Experience Manager Assets] pour la gestion des métadonnées. La norme permet le codage universel des métadonnées en l’incorporant dans tous les formats de fichier. Adobe et d’autres entreprises prennent en charge la norme XMP, car elle offre un modèle de contenu enrichi. Les utilisateurs de XMP standard et de [!DNL Experience Manager Assets] disposent d’une plate-forme puissante sur laquelle s’appuyer. Pour plus d’informations, voir la section [XMP](https://www.adobe.com/products/xmp.html).

### ID3 {#id}

Les données stockées dans ces balises ID3 s’affichent lors de la lecture d’un fichier audio numérique sur un ordinateur ou un lecteur MP3 portable.

Les balises ID3 sont destinées au format de fichier MP3. Informations supplémentaires sur les formats :

* Les balises ID3 fonctionnent dans les fichiers MP3 et mp3PRO.
* Le format WAV ne contient pas de balises.
* Le format WMA possède des balises propriétaires qui n’autorisent pas l’implémentation Open Source.
* Le format Ogg Vorbis utilise des commentaires Xiph incorporés dans le conteneur Ogg.
* Le format AAC utilise un format de balisage propriétaire.

### Exif {#exif}

Le format de fichier d’image échangeable (Exif) est le plus utilisé dans la photographie numérique pour les métadonnées. Il permet d’incorporer un vocabulaire fixe de propriétés de métadonnées dans de nombreux formats de fichiers, tels que JPEG, TIFF, RIFF et WAV. Le format Exif stocke chaque métadonnée sous la forme d’une paire constituée du nom et de la valeur de la métadonnée. Ces paires de nom et de valeur de métadonnées sont également appelées des balises, que l’on ne doit pas confondre avec le balisage dans [!DNL Experience Manager]. Les caméras numériques modernes créent des métadonnées Exif que les logiciels graphiques modernes savent prendre en charge. Le format Exif est le plus petit dénominateur commun pour la gestion des métadonnées, en particulier concernant les images.

Le fait que ce format ne soit pas pris en charge par quelques formats de fichiers image très appréciés comme BMP, GIF ou PNG constitue une limite majeure.

Les champs de métadonnées définis par Exif sont généralement de nature technique et d’une utilité limitée pour la gestion descriptive des métadonnées. D’où l’intérêt de [!DNL Experience Manager Assets] pour mapper les propriétés Exif dans des [schémas de métadonnées courants](metadata-schemas.md)[ et dans XMP](xmp-writeback.md).

### Autres métadonnées {#other-metadata}

Les autres métadonnées qui peuvent être incorporées à partir de fichiers comprennent celles de [!DNL Microsoft Word], [!DNL PowerPoint], [!DNL Excel], etc.

## Schémas de métadonnées {#metadata-schemata}

Les schémas de métadonnées sont des ensembles prédéfinis de définitions de propriétés de métadonnées qui peuvent être utilisés dans différentes applications. Les propriétés sont toujours associées à une ressource, ce qui signifie que les propriétés « concernent » cette ressource.

Vous pouvez également concevoir vos propres schémas de métadonnées s’il n’en existe aucun qui réponde à vos besoins. Ne dupliquez pas les informations existantes. Au sein d’une organisation, la séparation des schémas facilite le partage des métadonnées. [!DNL Experience Manager] fournit une liste par défaut des schémas de métadonnées les plus utilisés. La liste vous permet de lancer rapidement votre stratégie de métadonnées et de choisir rapidement les propriétés de métadonnées dont vous avez besoin.

Les schémas de métadonnées pris en charge sont répertoriés ci-dessous.

### Métadonnées standard {#standard-metadata}

* DC – [!DNL Dublin Core] est un ensemble de métadonnées important et largement utilisé.
* DICOM – Digital Imaging and Communications in Medicine.
* `Iptc4xmpCore` et `iptc4xmpExt` – International Press Communications Standard contient de nombreuses métadonnées spécifiques à un sujet.
* RDF – Resource Description Framework : pour les métadonnées web de sémantique générique.
* XMP – [!DNL Extensible Metadata Platform].
* `xmpBJ` – Basic Job Ticketing.

### Métadonnées spécifiques à l’application {#application-specific-metadata}

Les métadonnées spécifiques à l’application englobent des métadonnées techniques et descriptives. Si vous utilisez ces types de métadonnées, il se peut que d’autres applications ne soient pas en mesure de les exploiter. Par exemple, il est possible qu’une autre application de rendu d’image ne puisse pas accéder aux métadonnées [!DNL Adobe Photoshop]. Vous pouvez créer une étape de workflow qui transforme une propriété spécifique à l’application en propriété standard.

* ACDSee – métadonnées gérées par le programme. [!DNL ACDSee] Voir [www.acdsee.com/](https://www.acdsee.com/).
* Album – [!DNL Adobe Photoshop Album].
* CQ – utilisées par [!DNL Experience Manager Assets].
* DAM – utilisées par [!DNL Experience Manager Assets].
* DEX – [Optima SC Description explorer](http://www.optimasc.com/products/dex/index.html) est une collection d’outils pour la gestion des métadonnées et des fichiers pour les systèmes d’exploitation Windows.
* CRS – [Adobe Photoshop Camera Raw](https://helpx.adobe.com/fr/camera-raw/using/introduction-camera-raw.html).
* LR – [!DNL Adobe Lightroom].
* MediaPro – [iView MediaPro](https://fr.wikipedia.org/wiki/Phase_One_Media_Pro).
* MicrosoftPhoto et MP – Microsoft Photo.
* PDF et PDF/X.
* Photoshop et psAux – [!DNL Adobe Photoshop].

### Métadonnées de gestion des droits numériques {#digital-rights-management-metadata}

* CC – [!DNL Creative Commons].
* [!DNL XMPRights].
* PLUS – [Picture Licensing Universal System](https://www.useplus.com).
* PRISM – [ Exigences de publication pour les métadonnées standard du secteur (Publishing Requirements for Industry Standard Metadata). ](https://www.idealliance.org/prism-metadata)
* PRL – PRISM Rights Language.
* PUR – PRISM Usage Rights.
* `xmpPlus` – intégration de PLUS avec XMP.

### Métadonnées spécifiques à la photographie {#photography-specific-metadata}

* Exif – de nombreuses informations techniques issues de l’appareil photo, notamment la position GPS.
* CRS – [!DNL Camera Raw] schéma.
* `iptc4xmpCore` et `iptc4xmpExt`.
* TIFF – métadonnées d’image (pas seulement pour les images TIFF).

### Métadonnées spécifiques à l’impression {#print-specific-metadata}

* PDF et PDF/X – Adobe PDF et applications tierces.
* PRISM – [ Exigences de publication pour les métadonnées standard du secteur (Publishing Requirements for Industry Standard Metadata). ](https://www.prismstandard.org)
* XMP – [!DNL Extensible Metadata Platform].
* `xmpPG` – Métadonnées XMP pour le texte paginé.

### Métadonnées multimédias {#multimedia-specific-metadata}

* `xmpDM` – [!DNL Dynamic Media].
* `xmpMM` – Gestion des médias.

## Workflows pilotés par les métadonnées {#metadata-driven-workflows}

La création de workflows pilotés par les métadonnées permet d’automatiser certains processus, ce qui en améliore l’efficacité. Dans un workflow piloté par les métadonnées, le système de gestion des workflows exécute ainsi une action prédéfinie après avoir lu un workflow. Voici quelques exemples d’utilisation des workflows pilotés par les métadonnées :

* Le workflow peut vérifier si une image contient un titre. Dans le cas contraire, le système vous avertit d’ajouter un titre.
* Le workflow peut vérifier si une mention de droit d’auteur relative à un fichier permet la distribution ou non. Ainsi, le système envoie la ressource à un serveur ou à un autre.
* Un workflow peut rechercher des ressources sans métadonnées obligatoires prédéfinies ou des ressources contenant des métadonnées *non valides*.

>[!MORELIKETHIS]
>
>* [Modification des propriétés de métadonnées de plusieurs collections](managing-collections-touch-ui.md#editing-collection-metadata-in-bulk)
>* [Métadonnées XMP](xmp.md).
>* [Modification ou ajout de métadonnées](meta-edit.md).
>* [Référence](meta-ref.md)des schémas de métadonnées.

