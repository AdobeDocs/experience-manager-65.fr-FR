---
title: Gestion des métadonnées pour les ressources numériques
description: Découvrez les types de métadonnées et comment AEM Assets aide à gérer les métadonnées afin que les ressources permettent une catégorisation et une organisation plus simples des ressources.
contentOwner: AG
translation-type: tm+mt
source-git-commit: a39ee0f435dc43d2c2830b2947e91ffdcf11c7f6

---


# Manage metadata for digital assets {#managing-metadata-for-digital-assets}

Adobe Experience Manager (AEM) Assets permet de conserver les métadonnées pour chaque ressource. Cela permettra d’obtenir une catégorisation et une organisation plus simples des ressources et d’aider les personnes qui recherchent une ressource spécifique. Avec la possibilité d’extraire les métadonnées à partir des fichiers chargés sur AEM Assets, la gestion des métadonnées s’intègre aux processus créatifs. Avec la possibilité de conserver et de gérer les métadonnées arbitraires avec vos ressources, AEM Assets permet d’organiser et de traiter automatiquement les ressources en fonction de leurs métadonnées.

* [Métadonnées XMP](xmp.md)
* [Comment modifier ou ajouter des métadonnées](meta-edit.md)
* [Référence des schémas de métadonnées](meta-ref.md)

## Pourquoi les métadonnées sont nécessaires {#why-we-need-metadata}

Les métadonnées sont des données sur les données. Les données font référence à la ressource que vous gérez, par exemple une image. Les métadonnées sont importantes, car elles permettent aux utilisateurs de gérer plus efficacement les ressources.

Les métadonnées sont l&#39;ensemble de toutes les données disponibles pour cette image, mais qui ne sont pas nécessairement contenues dans cette image, par exemple :

* nom de la ressource ;
* date et heure de sa dernière modification ;
* taille de l’image au moment du stockage dans le référentiel ;
* nom du dossier qui la contient.

Il s’agit des propriétés de métadonnées de base que AEM peut gérer pour les ressources. Les utilisateurs peuvent ainsi afficher toutes leurs ressources triées, par exemple, selon la date de leur dernière modification. Ceci peut s’avérer utile pour tenter d’identifier les ressources qui ont été récemment ajoutées au référentiel.

Vous pouvez ajouter d’autres données de niveau supérieur à des ressources numériques, par exemple :

* type de ressource (s’agit-il d’une image, d’une vidéo, d’un clip audio ou d’un document ?) ;
* propriétaire de la ressource ;
* titre de la ressource ;
* description de la ressource ;
* balises affectées à une ressource.

Des métadonnées supplémentaires permettent de classer davantage les ressources et sont utiles à mesure que la quantité d’informations numériques augmente. Bien qu’il soit possible pour une personne seule de gérer une liste de plusieurs centaines de fichiers en fonction de leur nom, cela devient impossible lorsque le nombre de personnes impliquées et le nombre de ressources gérées augmentent.

À mesure que des métadonnées sont ajoutées aux ressources, la valeur de celles-ci augmente, car elles deviennent :

* plus accessibles : elles sont plus faciles à trouver ;
* plus faciles à gérer : vous pouvez rechercher plus facilement des ressources avec un même ensemble de propriétés et leur apporter des modifications ;
* plus complexes : plus vous ajoutez de métadonnées à une ressource, plus la gestion des métadonnées devient importante.

Pour ces raisons, Ressources AEM vous fournit les moyens adéquats pour créer, gérer et échanger des métadonnées pour vos ressources numériques.

## Notions fondamentales relatives aux métadonnées {#metadata-basics}

Les métadonnées sont extraites des ressources lorsqu’elles sont importées (assimilées). En outre, l’ajout de métadonnées permet de classer davantage les ressources.

Cette section traite des types de métadonnées et des normes de codage.

### Types de métadonnées {#types-of-metadata}

Il existe deux types fondamentaux de métadonnées :

* les métadonnées techniques ;
* les métadonnées descriptives.

#### Métadonnées techniques {#technical-metadata}

Les métadonnées techniques sont utiles pour les applications logicielles qui traitent de ressources numériques qui ne doivent pas être gérées manuellement. Les métadonnées techniques peuvent être déterminées automatiquement par Ressources AEM ainsi que par d’autres logiciels, et peuvent être changées lorsque la ressource est modifiée. Les métadonnées techniques disponibles pour une ressource dépendent largement du type de fichier de celle-ci. Voici des exemples de métadonnées techniques :

* taille d’un fichier ;
* dimensions (hauteur et largeur) d’une image ;
* débit d’un fichier audio ou vidéo ;
* résolution (niveau de détail) d’une image.

#### Métadonnées descriptives {#descriptive-metadata}

Les métadonnées descriptives sont des métadonnées qui concernent le domaine d’application, par exemple l’activité dont provient une ressource. Les métadonnées descriptives ne peuvent pas être automatiquement déterminées. Elles doivent être créées manuellement ou de manière semi-automatique. Par exemple, un appareil photo avec GPS peut suivre automatiquement la latitude et la longitude auxquelles a été prise une photo et ajouter ces informations aux métadonnées de l’image.

En raison du coût élevé de la création manuelle des informations de métadonnées descriptives, des normes ont été définies pour faciliter l’échange des métadonnées entre les systèmes logiciels et les structures.

Ressources AEM prend en charge l’ensemble des normes pertinentes pour la gestion des métadonnées.

En raison de l’importance des métadonnées et de l’implication pour créer des métadonnées, des normes ont été définies pour en faciliter l’échange.

### Normes de codage {#encoding-standards}

Les métadonnées peuvent être incorporées de plusieurs manières différentes dans des fichiers. Plusieurs normes de codage sont prises en charge :

* XMP : utilisé par Ressources AEM pour stocker les métadonnées extraites au sein du référentiel.
* ID3 : pour les fichiers audio et vidéo
* EXIF : pour les fichiers image
* Autre/Hérité : à partir de Microsoft Word, PowerPoint, Excel, etc.

#### XMP {#xmp}

XMP signifie plateforme de métadonnées extensible et est la norme de métadonnées utilisée par AEM Assets pour la gestion de toutes les métadonnées. Outre le codage universel de métadonnées pouvant être incorporé dans tous les formats de fichier, XMP fournit un modèle de contenu enrichi et est pris en charge par Adobe et d’autres entreprises, de sorte que les utilisateurs de XMP en association avec les ressources AEM disposent d’une plateforme puissante sur laquelle construire.

#### ID3 {#id}

Les données stockées dans ces balises ID3 s’affichent lors de la lecture d’un fichier audio numérique sur un ordinateur ou un lecteur MP3 portable.

Les balises ID3 sont destinées au format de fichier MP3. Informations supplémentaires sur les formats :

* Les balises ID3 fonctionnent dans les fichiers MP3 et MP3pro.
* Le format WAV ne comprend pas de balises.
* Le format WMA comprend des balises propriétaires qui ne permettent pas une mise en œuvre Open Source.
* Le format Ogg Vorbis utilise des commentaires Xiph incorporés dans le conteneur Ogg.
* Le format AAC utilise un format de balisage propriétaire.

#### EXIF {#exif}

EXIF signifie format de fichier d’image échangeable et est le format de métadonnées le plus utilisé dans la photographie numérique. Il permet d’incorporer un vocabulaire fixe de propriétés de métadonnées dans plusieurs formats de fichier, tels que JPEG, TIFF, RIFF et WAV.

Le fait que le format EXIF ne soit pas pris en charge par d’autres formats de fichier image populaires comme BMP, GIF ou PNG constitue une limite majeure.

EXIF stocke chaque métadonnée sous la forme d’une paire constituée du nom et de la valeur de la métadonnée. Ces paires de nom et de valeur de métadonnées sont également appelées des balises, que l’on ne doit pas confondre avec le balisage dans AEM.

Comme le format EXIF est automatiquement créé par les appareils photo numériques modernes et pris en charge par les logiciels graphiques modernes, il peut être considéré comme le plus petit dénominateur commun pour la gestion des métadonnées.

Most of the metadata fields defined by EXIF are of a highly technical nature and of limited use for descriptive metadata management. For this reason, AEM Assets offers mapping of EXIF properties into [common metadata schemata](metadata-schemas.md) and into [XMP](xmp-writeback.md), the powerful metadata format AEM Assets uses for metadata management.

#### Autres métadonnées {#other-metadata}

Les autres métadonnées pouvant être incorporées à partir de fichiers sont Microsoft Word, PowerPoint, Excel, etc.

## Schémas de métadonnées {#metadata-schemata}

Les schémas de métadonnées sont des ensembles prédéfinis de définitions de propriétés de métadonnées qui peuvent être utilisés dans un large éventail d’applications. Les propriétés sont toujours associées à une ressource, ce qui signifie que les propriétés concernent la ressource.

Vous pouvez également concevoir vos propres schémas de métadonnées s’il n’en existe aucun qui répond à vos besoins (veillez toutefois à ne pas dupliquer quelque chose qui existe déjà). Dans une structure, la séparation des schémas facilite le partage des métadonnées entre différentes structures.

AEM fournit une liste prête à l’emploi des schémas de métadonnées les plus populaires, ce qui vous permet de démarrer rapidement votre stratégie de métadonnées et de sélectionner les propriétés de métadonnées dont vous avez besoin dans un schéma déjà défini.

Les schémas de métadonnées pris en charge sont répertoriés dans la section qui suit.

### Métadonnées standard {#standard-metadata}

* dc - Dublin Core : ensemble de métadonnées le plus important et le plus largement utilisé.
* DICOM - Digital Imaging and Communications in Medicine
* Iptc4xmpCore et iptc4xmpExt - International Press Communications Standard - quantité de métadonnées spécifiques à un sujet
* rdf - Resource Description Framework : pour les métadonnées web de sémantique générique
* xmp - Extensible Metadata Platform
* xmpBJ - Basic Job Ticketing

### Métadonnées spécifiques à l’application {#application-specific-metadata}

>[!NOTE]
>
>Les métadonnées spécifiques à l’application comprennent des métadonnées techniques et des métadonnées descriptives. Si vous y avez recours, d’autres applications peuvent ne pas être en mesure de les utiliser. Par exemple, si vous disposez d’une ressource avec des métadonnées Adobe Photoshop et si une autre application de rendu d’image tente d’accéder aux métadonnées, il est possible qu’elle n’y parvienne pas.
>
>Si vous estimez que vos ressources comprennent trop de métadonnées spécifiques à l’application, vous pouvez créer une étape de processus qui remplace la propriété propre à l’application par une propriété standard.

* acdsee - metadata managed by the ACDSee program [www.acdsee.com/](https://www.acdsee.com/)
* album - Adobe Photoshop Album
* cq - utilisé par AEM Assets
* dam - utilisé par Ressources AEM
* dex - Optima SC Description Explorer
* crs - Adobe Photoshop Camera Raw
* lr - Adobe Lightroom
* mediapro - IView MediaPro
* MicrosoftPhoto et MP - Microsoft Photo
* pdf amd pdfx
* photoshop et psAux - Adobe Photoshop

### Métadonnées de gestion des droits numériques {#digital-rights-management-metadata}

* cc - creative commons
* xmpRights
* plus - Système universel de licences d&#39;image - https://www.useplus.com/
* prism - https://www.idealliance.org/prism-metadata de publication DPS pour les métadonnées standard du secteur
* prl - Prism Rights Language
* pur - Prism Usage Rights
* xmpPlus - intégration de PLUS avec XMP

### Métadonnées spécifiques à la photographie {#photography-specific-metadata}

* exif - de nombreuses informations techniques de l’appareil photo, notamment la position GPS
* crs - photoshop camera raw
* Iptc4xmpCore et iptc4xmpExt
* TIFF - métadonnées d’image (pas seulement pour les images TIFF)

### Métadonnées spécifiques à l’impression {#print-specific-metadata}

* pdf et pdfx - Adobe PDF et applications tierces
* prism - [www.prismstandard.org](https://www.prismstandard.org) Publishing Requirements for Industry Standard Metadata
* xmp
* xmpPG - xmp pour le texte paginé

### Métadonnées multimédia {#multimedia-specific-metadata}

* xmpDM - Dynamic Media
* xmpMM - Gestion des médias

## Processus pilotés par les métadonnées {#metadata-driven-workflows}

La création de processus pilotés par les métadonnées vous permet d’automatiser certains processus, ce qui améliore l’efficacité. Dans un processus piloté par les métadonnées, le système de gestion de processus lit le processus et exécute ensuite une action prédéfinie.

Voici quelques exemples d’utilisation des processus pilotés par les métadonnées :

* Le processus peut vérifier si une image possède un titre. Si elle n’en possède pas, le système demande à un utilisateur spécifique d’ajouter un titre.
* Le processus peut vérifier si un avis de droit d’auteur sur une ressource autorise la distribution. S’il l’autorise, le système envoie la ressource à un serveur. S’il ne l’autorise pas, le système envoie la ressource à un autre serveur.
