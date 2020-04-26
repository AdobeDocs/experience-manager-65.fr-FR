---
title: Gérez les métadonnées de vos ressources numériques dans [!DNL Adobe Experience Manager].
description: Découvrez les types de métadonnées et comment [!DNL Adobe Experience Manager Assets] aide à gérer les métadonnées des ressources afin de faciliter la catégorisation et l’organisation des ressources. [!DNL Experience Manager] permet d’organiser et de traiter automatiquement les fichiers en fonction de leurs métadonnées.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 9bf48a6057e08e9feafc0e18d6fa9d0145768cf2

---


# Gestion des métadonnées des ressources numériques {#managing-metadata-for-digital-assets}

[!DNL Adobe Experience Manager Assets] conserve les métadonnées de chaque fichier. Cela facilite la catégorisation et l&#39;organisation des ressources et aide les personnes qui recherchent un actif spécifique. With the ability to extract metadata from files uploaded to [!DNL Experience Manager Assets], metadata management integrates with the creative workflow. With the ability to keep and manage metadata with your assets, [!DNL Experience Manager Assets] makes it possible to automatically organize and process assets based on their metadata.

* [Métadonnées XMP](xmp.md).
* [Modification ou ajout de métadonnées](meta-edit.md).
* [Référence](meta-ref.md)des schémas de métadonnées.

## Pourquoi les métadonnées sont nécessaires {#why-we-need-metadata}

Les métadonnées désignent les données relatives aux données. À cet égard, les données font référence à votre actif numérique, par exemple une image. Les métadonnées sont essentielles pour une gestion efficace des ressources.

Les métadonnées sont la collection de toutes les données disponibles pour un fichier, mais elles ne sont pas nécessairement contenues dans cette image. Voici quelques exemples de métadonnées :

* Nom du fichier.
* Heure et date de la dernière modification.
* Taille de la ressource telle qu’elle était stockée dans le référentiel.
* Nom du dossier dans lequel il se trouve.
* Ressources connexes ou balises appliquées.

These are the basic metadata properties that [!DNL Experience Manager] can manage for assets, which allows users to see all assets, for example, ordered by their last modification date - useful when trying to discover what assets have recently been added to the repository.

Vous pouvez ajouter d’autres données de niveau supérieur à des ressources numériques, par exemple :

* Type de fichier (s’agit-il d’une image, d’une vidéo, d’un clip audio ou d’un  ?).
* Propriétaire de la ressource.
* Titre de la ressource.
* Description de la ressource.
* Balises affectées à un fichier.

Un plus grand nombre de métadonnées vous permet de classer davantage les fichiers et s’avère utile à mesure que la quantité d’informations numériques augmente. Il est possible de gérer quelques centaines de fichiers uniquement en fonction des noms de fichier. Toutefois, cette approche n’est pas évolutive et ne fonctionne pas rapidement lorsque le nombre de personnes impliquées et le nombre d’actifs gérés augmentent.

Avec l’ajout de métadonnées, la valeur d’une ressource numérique augmente, car la ressource devient :

* Plus accessible : les systèmes et les utilisateurs peuvent le trouver facilement.
* Plus facile à gérer : vous pouvez trouver plus facilement des ressources ayant le même jeu de propriétés et leur appliquer des modifications.
* Plus complet : plus vous avez ajouté de métadonnées à un fichier, plus il contient d’informations et de contexte.

For these reasons, [!DNL Assets] provides you with the right means of creating, managing, and exchanging metadata for your digital assets.

## Types de métadonnées {#types-of-metadata}

Les deux types de métadonnées de base sont les métadonnées techniques et les métadonnées descriptives.

Les métadonnées techniques sont utiles pour les applications logicielles qui traitent de ressources numériques et ne doivent pas être gérées manuellement. [!DNL Experience Manager Assets] et d’autres logiciels déterminent automatiquement les métadonnées techniques et les métadonnées peuvent changer lorsque le fichier est modifié. Les métadonnées techniques disponibles d’un fichier dépendent largement du type de fichier du fichier. Voici quelques exemples de métadonnées techniques :

* Taille d’un fichier.
* Dimensions (hauteur et largeur) d’une image.
* Débit d’un fichier audio ou vidéo.
* Résolution (niveau de détail) d’une image.

Les métadonnées descriptives sont des métadonnées qui concernent le domaine d’application, par exemple l’entreprise d’où provient un fichier. Les métadonnées descriptives ne peuvent pas être déterminées automatiquement. Elle est créée manuellement ou semi-automatiquement. Par exemple, une caméra GPS peut automatiquement suivre la latitude et la longitude et ajouter une balise géographique à l’image.

En raison du coût élevé de la création manuelle des informations de métadonnées descriptives, des normes ont été définies pour faciliter l’échange des métadonnées entre les systèmes logiciels et les structures.

[!DNL Experience Manager Assets] prend en charge toutes les normes pertinentes pour la gestion des métadonnées.

En raison de l’importance des métadonnées et de l’implication pour créer des métadonnées, des normes ont été définies pour en faciliter l’échange.

## Normes de codage {#encoding-standards}

Il existe différentes manières d’incorporer des métadonnées dans des fichiers. Certaines normes de codage sont prises en charge :

* XMP: used by [!DNL Assets] to store the extracted metadata within the repository.
* ID3 : pour les fichiers audio et vidéo
* Exif : pour les fichiers image.
* Autre/Hérité : à partir de Microsoft Word, PowerPoint, Excel, etc.

### XMP {#xmp}

XMP (Extensible Metadata Platform) est une norme ouverte utilisée par [!DNL Experience Manager Assets] tous les gestionnaires de métadonnées. Le standard  le codage de métadonnées universel qui peut être incorporé dans tous les formats de fichier. Adobe et d’autres  prennent en charge la norme XMP car elle fournit un modèle de contenu enrichi. Les utilisateurs de XMP standard et de [!DNL Experience Manager Assets] ont une plate-forme puissante sur laquelle construire. Pour plus d’informations, voir [XMP](https://www.adobe.com/products/xmp.html).

### ID3 {#id}

Les données stockées dans ces balises ID3 s’affichent lors de la lecture d’un fichier audio numérique sur un ordinateur ou un lecteur MP3 portable.

Les balises ID3 sont destinées au format de fichier MP3. Informations supplémentaires sur les formats :

* Les balises ID3 fonctionnent dans les fichiers MP3 et mp3PRO.
* Le format WAV ne comprend pas de balises.
* WMA possède des balises propriétaires qui n’autorisent pas l’implémentation open-source.
* Le format Ogg Vorbis utilise des commentaires Xiph incorporés dans le conteneur Ogg.
* Le format AAC utilise un format de balisage propriétaire.

### Exif {#exif}

Le format de fichier d’image échangeable (Exif) est le format de métadonnées le plus utilisé dans la photographie numérique. Il permet d’incorporer un vocabulaire fixe des propriétés de métadonnées dans de nombreux formats de fichier, tels que JPEG, TIFF, RIFF et WAV. Exif stores metadata as pairs of a metadata name and a metadata value. These metadata name-value-pairs are also called tags, not to be confused with the tagging in [!DNL Experience Manager]. Comme Exif est automatiquement créé par les appareils photo numériques modernes et pris en charge par les logiciels graphiques modernes, il peut être considéré comme le plus petit dénominateur commun pour la gestion des métadonnées.

Une des principales limites d’Exif est que quelques formats de fichier d’image courants, tels que BMP, GIF ou PNG, ne le prennent pas en charge.

Les champs de métadonnées habituellement définis par Exif sont de nature technique et sont d’une utilité limitée pour la gestion descriptive des métadonnées. C’est pourquoi [!DNL Experience Manager Assets]  mappage des propriétés Exif dans des données [de schémas de métadonnées](metadata-schemas.md) courants et dans [XMP](xmp-writeback.md).

### Other metadata {#other-metadata}

Les autres métadonnées qui peuvent être incorporées à partir de fichiers comprennent Microsoft Word, PowerPoint, Excel, etc.

## Metadata schemata {#metadata-schemata}

Les  de métadonnées sont des jeux prédéfinis de définitions de propriétés de métadonnées qui peuvent être utilisées dans diverses applications. Les propriétés sont toujours associées à une ressource, ce qui signifie que les propriétés sont &quot;à propos&quot; de la ressource.

Vous pouvez également concevoir vos propres schémas de métadonnées s’il n’en existe aucun qui réponde à vos besoins. Ne  pas les informations existantes. Au sein d’une entreprise, la séparation des schémas facilite le partage des métadonnées. [!DNL Experience Manager] fournit un  par défaut des schémas de métadonnées les plus populaires. Le vous permet de lancer rapidement votre stratégie de métadonnées et de sélectionner rapidement les propriétés de métadonnées dont vous avez besoin.

Les schémas de métadonnées pris en charge sont répertoriés ci-dessous.

### Standard metadata {#standard-metadata}

* dc - Dublin Core - l’ensemble de métadonnées le plus important et le plus utilisé.
* DICOM - Digital Imaging and Communications in Medicine.
* Iptc4xmpCore et iptc4xmpExt - International Press Communications Standard - un grand nombre de métadonnées spécifiques au sujet.
* rdf - Resource Description Framework : pour les métadonnées web de sémantique générique.
* xmp - Extensible Metadata Platform.
* xmpBJ - Basic Job Ticketing.

### Application-specific metadata {#application-specific-metadata}

Les métadonnées propres à l’application comprennent des métadonnées techniques et descriptives. Si vous les utilisez, il se peut que d’autres applications ne puissent pas utiliser les métadonnées. Par exemple, si vous disposez d’un fichier avec [!DNL Adobe Photoshop] des métadonnées et qu’une autre application de rendu d’image tente d’accéder aux métadonnées, il se peut qu’il ne soit pas en mesure d’accéder aux métadonnées. Si vous constatez que vos fichiers contiennent de nombreuses métadonnées spécifiques à l’application, vous pouvez créer une étape de flux de travail qui transforme une propriété spécifique à l’application en propriété standard.

* acdsee - métadonnées gérées par le programme ACDSee [www.acdsee.com/](https://www.acdsee.com/).
* album - Adobe Photoshop Album.
* cq - used by [!DNL Experience Manager Assets].
* dam - used by [!DNL Experience Manager Assets].
* dex - Optima SC Description Explorer.
* crs - Adobe Photoshop Camera Raw.
* lr - Adobe Lightroom.
* mediapro - IView MediaPro.
* MicrosoftPhoto et MP - Microsoft Photo.
* pdf et pdfx.
* photoshop et psAux - Adobe Photoshop.

### Digital Rights Management metadata {#digital-rights-management-metadata}

* cc - creative commons
* xmpRights
* plus - Picture Licensing Universal System - https://www.useplus.com/
* prism - https://www.idealliance.org/prism-metadata Exigences de publication pour les métadonnées standard du secteur (Publishing Requirements for Industry Standard Metadata)
* prl - Prism Rights Language
* pur - Prism Usage Rights
* xmpPlus - intégration de PLUS avec XMP

### Photography-specific metadata {#photography-specific-metadata}

* exif - de nombreuses informations techniques de l’appareil photo, notamment la position GPS
* crs - photoshop camera raw
* Iptc4xmpCore et iptc4xmpExt
* TIFF - métadonnées d’image (pas seulement pour les images TIFF)

### Print-specific metadata {#print-specific-metadata}

* pdf et pdfx - Adobe PDF et applications tierces
* prism - [www.prismstandard.org](https://www.prismstandard.org) Exigences de publication pour les métadonnées standard du secteur (Publishing Requirements for Industry Standard Metadata)
* xmp
* xmpPG - xmp pour le texte paginé

### Métadonnées multimédias {#multimedia-specific-metadata}

* xmpDM - Dynamic Media
* xmpMM - Gestion des médias

## Processus pilotés par les métadonnées {#metadata-driven-workflows}

La création d’un axé sur les métadonnées permet d’automatiser certains processus, ce qui améliore l’efficacité. Dans un flux de travail axé sur les métadonnées, le système de gestion du flux de travail lit le flux de travail et effectue par conséquent une action prédéfinie. Voici quelques exemples d’utilisation des workflows pilotés par les métadonnées :

* Le workflow peut vérifier si une image possède un titre. Si elle n’en possède pas, le système demande à un utilisateur spécifique d’ajouter un titre.
* Le workflow peut vérifier si un avis de droit d’auteur sur une ressource autorise la distribution. S’il l’autorise, le système envoie la ressource à un serveur. S’il ne l’autorise pas, le système envoie la ressource à un autre serveur.
* Un processus peut rechercher des fichiers sans métadonnées prédéfinies et obligatoires ou avec des métadonnées *non valides* .
