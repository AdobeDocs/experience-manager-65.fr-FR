---
title: Gérez les métadonnées de vos ressources numériques dans [ ! DNL Adobe Experience Manager].
description: Découvrez les types de métadonnées et comment [ ! DNL Adobe Experience Manager Assets] aide à gérer les métadonnées des ressources afin de faciliter la catégorisation et l’organisation des ressources. [ !DNL Experience Manager] permet d’organiser et de traiter automatiquement les ressources en fonction de leurs métadonnées.
contentOwner: AG
translation-type: tm+mt
source-git-commit: f21e9dbb81f18e07a691b2470c1c5b1569876b17

---


# Gestion des métadonnées des ressources numériques {#managing-metadata-for-digital-assets}

[!DNL Adobe Experience Manager Assets] conserve les métadonnées de chaque fichier. Cela facilite la catégorisation et l&#39;organisation des actifs et aide les personnes qui recherchent un actif spécifique. With the ability to extract metadata from files uploaded to [!DNL Experience Manager Assets], metadata management integrates with the creative workflow. With the ability to keep and manage metadata with your assets, [!DNL Experience Manager Assets] makes it possible to automatically organize and process assets based on their metadata.

* [Métadonnées XMP](xmp.md).
* [Modification ou ajout de métadonnées](meta-edit.md).
* [Référence](meta-ref.md)des schémas de métadonnées.

## Pourquoi les métadonnées sont nécessaires {#why-we-need-metadata}

Les métadonnées désignent les données. À cet égard, les données font référence à votre actif numérique, par exemple une image. Les métadonnées sont essentielles à une gestion efficace des ressources.

Les métadonnées sont la collection de toutes les données disponibles pour un fichier, mais qui ne sont pas nécessairement contenues dans cette image. Voici quelques exemples de métadonnées :

* Nom de la ressource.
* Heure et date de la dernière modification.
* Taille de la ressource telle qu’elle était stockée dans le référentiel.
* Nom du dossier dans lequel il se trouve.
* Ressources connexes ou balises appliquées.

These are the basic metadata properties that [!DNL Experience Manager] can manage for assets, which allows users to see all assets, for example, ordered by their last modification date - useful when trying to discover what assets have recently been added to the repository.

Vous pouvez ajouter d’autres données de niveau supérieur à des ressources numériques, par exemple :

* Type de fichier (s’agit-il d’une image, d’une vidéo, d’un clip audio ou d’un document ?).
* Propriétaire de la ressource.
* Titre de la ressource.
* Description de la ressource.
* Balises affectées à une ressource.

Davantage de métadonnées vous permet de classer davantage les fichiers et s’avère utile à mesure que la quantité d’informations numériques augmente. Il est possible de gérer quelques centaines de fichiers uniquement en fonction des noms de fichier. Toutefois, cette approche n’est pas évolutive et ne s’adapte pas rapidement lorsque le nombre de personnes impliquées et le nombre d’actifs gérés augmentent.

Avec l’ajout de métadonnées, la valeur d’une ressource numérique augmente, car la ressource devient,

* Plus accessible : les systèmes et les utilisateurs peuvent le trouver facilement.
* Plus facile à gérer : vous pouvez trouver plus facilement des ressources présentant le même ensemble de propriétés et leur appliquer des modifications.
* Plus complet : plus vous ajoutez de métadonnées à un fichier, plus il contient d’informations et de contexte.

For these reasons, [!DNL Assets] provides you with the right means of creating, managing, and exchanging metadata for your digital assets.

## Types de métadonnées {#types-of-metadata}

Les deux types de métadonnées de base sont les métadonnées techniques et les métadonnées descriptives.

Les métadonnées techniques sont utiles pour les applications logicielles qui traitent des ressources numériques et ne doivent pas être gérées manuellement. [!DNL Experience Manager Assets] et d’autres logiciels déterminent automatiquement les métadonnées techniques et les métadonnées peuvent changer lorsque la ressource est modifiée. Les métadonnées techniques disponibles d’une ressource dépendent largement du type de fichier de la ressource. Voici quelques exemples de métadonnées techniques :

* Taille d’un fichier.
* Dimensions (hauteur et largeur) d’une image.
* Débit d’un fichier audio ou vidéo.
* Résolution (niveau de détail) d’une image.

Les métadonnées descriptives sont des métadonnées qui concernent le domaine d’application, par exemple l’entreprise d’où provient un fichier. Les métadonnées descriptives ne peuvent pas être déterminées automatiquement. Il est créé manuellement ou semi-automatiquement. Par exemple, une caméra GPS peut automatiquement suivre la latitude et la longitude et ajouter un balisage géographique à l’image.

En raison du coût élevé de la création manuelle des informations de métadonnées descriptives, des normes ont été définies pour faciliter l’échange des métadonnées entre les systèmes logiciels et les structures.

[!DNL Experience Manager Assets] prend en charge toutes les normes pertinentes pour la gestion des métadonnées.

En raison de l’importance des métadonnées et de l’implication pour créer des métadonnées, des normes ont été définies pour en faciliter l’échange.

## Normes de codage {#encoding-standards}

Il existe différentes manières d’incorporer des métadonnées dans des fichiers. Une sélection de normes de codage est prise en charge :

* XMP: used by [!DNL Assets] to store the extracted metadata within the repository.
* ID3 : pour les fichiers audio et vidéo
* Exif : pour les fichiers image.
* Other/Legacy: from [!DNL Microsoft Word], [!DNL PowerPoint], [!DNL Excel], and so on.

### XMP {#xmp}

[!DNL Extensible Metadata Platform] (XMP) est une norme ouverte utilisée par [!DNL Experience Manager Assets] la gestion des métadonnées. La norme offre le codage universel des métadonnées qui peut être incorporé dans tous les formats de fichier. Adobe et d’autres sociétés prennent en charge la norme XMP car elle fournit un modèle de contenu enrichi. Les utilisateurs de XMP standard et de [!DNL Experience Manager Assets] disposent d&#39;une plate-forme puissante sur laquelle s&#39;appuyer. Pour plus d’informations, voir [XMP](https://www.adobe.com/products/xmp.html).

### ID3 {#id}

Les données stockées dans ces balises ID3 s’affichent lors de la lecture d’un fichier audio numérique sur un ordinateur ou un lecteur MP3 portable.

Les balises ID3 sont destinées au format de fichier MP3. Informations supplémentaires sur les formats :

* Les balises ID3 fonctionnent dans les fichiers MP3 et mp3PRO.
* Le format WAV ne comprend pas de balises.
* WMA possède des balises propriétaires qui n’autorisent pas l’implémentation open-source.
* Le format Ogg Vorbis utilise des commentaires Xiph incorporés dans le conteneur Ogg.
* Le format AAC utilise un format de balisage propriétaire.

### Exif {#exif}

Le format de fichier d’image échangeable (Exif) est le format de métadonnées le plus utilisé dans la photographie numérique. Il permet d’incorporer un vocabulaire fixe de propriétés de métadonnées dans de nombreux formats de fichier, tels que JPEG, TIFF, RIFF et WAV. Exif stores metadata as pairs of a metadata name and a metadata value. These metadata name-value-pairs are also called tags, not to be confused with the tagging in [!DNL Experience Manager]. Exif étant automatiquement créé par des appareils photo numériques modernes et pris en charge par des logiciels graphiques modernes, il peut être considéré comme le plus petit dénominateur commun pour la gestion des métadonnées.

Exif présente une limitation majeure du fait que quelques formats de fichier image populaires tels que BMP, GIF ou PNG ne le prennent pas en charge.

Les champs de métadonnées habituellement définis par Exif sont de nature technique et d’une utilité limitée pour la gestion descriptive des métadonnées. C’est pourquoi [!DNL Experience Manager Assets] les offres mappent les propriétés Exif dans des schémas [de métadonnées](metadata-schemas.md) courants et dans [XMP](xmp-writeback.md).

### Other metadata {#other-metadata}

Les autres métadonnées qui peuvent être incorporées à partir de fichiers comprennent Microsoft Word, PowerPoint, Excel, etc.

## Metadata schemata {#metadata-schemata}

Les schémas de métadonnées sont des ensembles prédéfinis de définitions de propriétés de métadonnées qui peuvent être utilisés dans diverses applications. Les propriétés sont toujours associées à une ressource, ce qui signifie que les propriétés sont &quot;autour&quot; de la ressource.

Vous pouvez également concevoir vos propres schémas de métadonnées s’il n’en existe aucun qui réponde à vos besoins. Ne duplicata pas les informations existantes. Au sein d’une organisation, la séparation des schémas facilite le partage des métadonnées. [!DNL Experience Manager] fournit une liste par défaut des schémas de métadonnées les plus populaires. La liste vous permet de lancer rapidement votre stratégie de métadonnées et de sélectionner rapidement les propriétés de métadonnées dont vous avez besoin.

Les schémas de métadonnées pris en charge sont répertoriés ci-dessous.

### Standard metadata {#standard-metadata}

* DC - [!DNL Dublin Core] est un ensemble important et largement utilisé de métadonnées.
* DICOM - Digital Imaging and Communications in Medicine.
* Iptc4xmpCore et iptc4xmpExt - International Press Communications Standard contient de nombreuses métadonnées spécifiques à un sujet.
* rdf - Resource Description Framework : pour les métadonnées web de sémantique générique.
* d’écriture différée xmp - [!DNL Extensible Metadata Platform].
* xmpBJ - Basic Job Ticketing.

### Application-specific metadata {#application-specific-metadata}

Les métadonnées propres à l’application comprennent des métadonnées techniques et descriptives. Si vous utilisez ces métadonnées, d’autres applications risquent de ne pas pouvoir les utiliser. Par exemple, si vous disposez d’un fichier contenant des métadonnées et qu’une autre application de rendu d’image tente d’accéder aux métadonnées, il se peut qu’elle ne puisse pas accéder aux métadonnées. [!DNL Adobe Photoshop] Si vos fichiers contiennent de nombreuses métadonnées spécifiques à l’application, vous pouvez créer une étape de flux de travail qui transforme une propriété spécifique à l’application en propriété standard.

* ACDSee - Metadata managed by the [!DNL ACDSee] program. Voir [www.acdsee.com/](https://www.acdsee.com/).
* Album - [!DNL Adobe Photoshop Album].
* CQ - Used by [!DNL Experience Manager Assets].
* DAM - Used by [!DNL Experience Manager Assets].
* DEX - [Optima SC Description explorer](http://www.optimasc.com/products/dex/index.html) est une collection d&#39;outils pour la gestion des métadonnées et des fichiers pour les systèmes d&#39;exploitation Windows.
* CRS - [Adobe Photoshop Camera Raw](https://helpx.adobe.com/camera-raw/using/introduction-camera-raw.html).
* LR - [!DNL Adobe Lightroom].
* MediaPro - [iView MediaPro](https://en.wikipedia.org/wiki/Phase_One_Media_Pro).
* MicrosoftPhoto et MP - Microsoft Photo.
* PDF &amp; PDF/X.
* Photoshop et psAux - [!DNL Adobe Photoshop].

### Digital Rights Management metadata {#digital-rights-management-metadata}

* CC - [!DNL Creative Commons].
* [!DNL XMPRights].
* PLUS - [Picture Licensing Universal System](https://www.useplus.com).
* PRISM - [Publishing Requirements for Industry Standard Metadata](https://www.idealliance.org/prism-metadata).
* PRL - PRISM Rights Language.
* PUR - Droits d’utilisation de PRISM.
* `xmpPlus` - Intégration de PLUS avec XMP.

### Photography-specific metadata {#photography-specific-metadata}

* Exif - Informations techniques de la caméra, y compris la position GPS.
* CRS - [!DNL Camera Raw] schéma.
* `iptc4xmpCore` et `iptc4xmpExt`.
* TIFF - métadonnées d’image (pas seulement pour les images TIFF).

### Print-specific metadata {#print-specific-metadata}

* PDF et PDF/X - Adobe PDF et applications tierces.
* PRISM - [www.prismstandard.org](https://www.prismstandard.org) Publishing Requirements for Industry Standard Metadata.
* XMP.
* `xmpPG` - Métadonnées XMP pour le texte paginé.

### Métadonnées multimédias {#multimedia-specific-metadata}

* `xmpDM` - [!DNL Dynamic Media].
* `xmpMM` - Gestion des médias.

## Processus pilotés par les métadonnées {#metadata-driven-workflows}

La création de workflows pilotés par les métadonnées permet d’automatiser certains processus, ce qui améliore l’efficacité. Dans un processus piloté par les métadonnées, le système de gestion du flux de travail lit le flux de travail et, par conséquent, exécute une action prédéfinie. Voici quelques exemples d’utilisation des workflows pilotés par les métadonnées :

* Le processus peut vérifier si une image a un titre ou non. Dans le cas contraire, le système vous avertit d’ajouter un titre.
* Le processus peut vérifier si une mention de copyright sur un fichier permet la distribution ou non. En conséquence, le système envoie la ressource à un serveur ou à un autre.
* Un processus peut rechercher des fichiers sans métadonnées prédéfinies obligatoires ou des fichiers avec des métadonnées *non valides* .
