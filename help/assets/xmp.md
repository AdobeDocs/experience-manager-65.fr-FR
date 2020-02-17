---
title: Prise en charge des métadonnées XMP dans les ressources AEM
description: Découvrez le standard de métadonnées XMP (Extensible Metadata Platform) utilisé par AEM Assets pour la gestion des métadonnées. XMP offre un format standard pour la création, le traitement et l’échange de métadonnées pour une multitude d’applications.
contentOwner: AG
translation-type: tm+mt
source-git-commit: a39ee0f435dc43d2c2830b2947e91ffdcf11c7f6

---


# XMP metadata {#xmp-metadata}

XMP (« Extensible Metadata Platform », plate-forme de métadonnées extensible) est la norme de métadonnées utilisée par AEM Assets pour toute la gestion des métadonnées. XMP fournit un format standard pour la création, le traitement et l’échange de métadonnées pour toute une variété d’applications.

Aside from offering universal metadata encoding that can be embedded into all file formats, XMP provides a rich [content model](xmp.md#xmp-core-concepts) and is [supported by Adobe](xmp.md#advantages-of-xmp) and other companies, so that users of XMP in combination with AEM Assets have a powerful platform to build upon.

La [spécification XMP](https://www.adobe.com/devnet/xmp.html) est disponible auprès d’Adobe.

## What is XMP? {#what-is-xmp}

AEM Assets prend nativement en charge XMP, la plateforme de métadonnées extensible pilotée par Adobe.XMP est une norme de traitement et de stockage des métadonnées propriétaires et normalisées dans les ressources numériques.XMP est conçu pour être la norme commune qui permet à plusieurs applications de fonctionner efficacement avec les métadonnées.

Les professionnels de la production, par exemple, utilisent la prise en charge du format XMP intégré au sein des applications d’Adobe pour communiquer les informations entre divers formats de fichier. Le référentiel AEM Assets extrait les métadonnées XMP et les utilise pour gérer le cycle de vie du contenu. Il offre également la possibilité de créer des processus d’automatisation.

XMP normalise la façon dont les métadonnées sont définies, créées et traitées en fournissant un modèle de données, un modèle de stockage et des schémas. Tous ces concepts sont abordés dans cette section.

Toutes les métadonnées héritées de EXIF, ID3 ou Microsoft Office sont automatiquement converties au format XMP, qui peut être étendu pour prendre en charge le schéma de métadonnées spécifiques au client comme les catalogues de produits.

Dans la norme XMP, les métadonnées sont composées d’un ensemble de propriétés. Ces propriétés sont toujours associées à une entité spécifique appelée ressource ; elles portent sur celle-ci. Dans le cas de XMP, la ressource est toujours la ressource.

### Adobe {#adobe}

Adobe a introduit pour la première fois la norme XMP dans le cadre du logiciel Adobe Acrobat. Depuis, la norme XMP a été largement adoptée.

### XMP ecosystem {#xmp-ecosystem}

XMP définit un modèle de [métadonnées](https://en.wikipedia.org/wiki/Metadata) exploitable avec n’importe quel ensemble défini d’éléments de métadonnées. XMP définit également des [schémas](https://en.wikipedia.org/wiki/XML_schema) spécifiques pour des propriétés de base utiles pour consigner l’historique d’une ressource lorsqu’elle passe par diverses étapes de traitement, de la photographie, en passant par la [numérisation](https://en.wikipedia.org/wiki/Image_scanner) ou la création en tant que texte, à travers des étapes de retouche photo (comme le [cadrage](https://en.wikipedia.org/wiki/Cropping_%28image%29) ou l’ajustement de couleur), pour former une image finale. XMP permet à chaque programme ou appareil d’ajouter ses propres informations à une ressource numérique. Ces informations peuvent être ensuite conservées dans le fichier numérique final.

XMP est le plus souvent sérialisé et stocké à l’aide d’un sous-ensemble du [Resource Description Framework](https://en.wikipedia.org/wiki/Resource_Description_Framework) (RDF) [W3C](https://en.wikipedia.org/wiki/World_Wide_Web_Consortium), qui est à son tour exprimé en langage [XML](https://en.wikipedia.org/wiki/XML).

## Avantages du mode XMP {#advantages-of-xmp}

La norme XMP présente les avantages suivants par rapport aux autres normes de codage et schémas :

* Les métadonnées basées sur la norme XMP sont très puissantes et précises.
* La norme XMP permet de posséder plusieurs valeurs pour une propriété.
* XMP possède un encodage normalisé, ce qui vous permet d’échanger facilement des métadonnées.
* XMP est extensible. Vous pouvez ajouter des informations supplémentaires à vos ressources.

### Extensibles {#extensible}

La norme XMP a été conçue pour être extensible, ce qui vous permet d’ajouter des types de métadonnées personnalisés dans les données XMP. En revanche, ce n’est pas le cas d’EXIF qui présente une liste des propriétés qui ne peut pas être étendue.

>[!NOTE]
>
>En règle générale, XMP ne permet pas l’incorporation des types de données binaires. Pour gérer des données binaires dans XMP, comme des images miniatures, celles-ci doivent être codées dans un format XML tel que `Base64`.

## Notions fondamentales relatives à XMP {#xmp-core-concepts}

Les sections ci-après décrivent les notions fondamentales relatives à XMP, notamment les espaces de noms et les schémas, les propriétés et les valeurs, ainsi que les variantes linguistiques.

### Espaces de noms et schémas {#namespaces-and-schemata}

Un schéma XMP est un ensemble de noms de propriétés défini dans un espace de noms XML commun qui comprend le type des données et des informations descriptives. Un schéma XMP est identifié par l’URI de l’espace de noms XML. L’utilisation des espaces de noms permet d’empêcher tout conflit entre les propriétés dans différents schémas qui portent le même nom, mais ont un sens différent.

For example, the `Creator` property in two independently designed schemas might mean the person who created the asset or it could mean the application that created the asset (for example, Adobe Photoshop).

### Propriétés et valeurs {#properties-and-values}

XMP peut inclure des propriétés de l’un ou de plusieurs des schémas.

Par exemple, un sous-ensemble classique utilisé par de nombreuses applications Adobe peut comprendre les éléments suivants :

* Schéma Dublin Core : dc:title, dc:creator, dc:subject, dc:format, dc:rights
* Schéma de base XMP : xmp:CreateDate, xmp:CreatorTool, xmp:ModifyDate, xmp:metadataDate
* Schéma de gestion des droits XMP : xmpRights:WebStatement, xmpRights:Marked
* Schéma de gestion des médias XMP : xmpMM:DocumentID

### Variantes linguistiques {#language-alternatives}

XMP vous offre la possibilité d’ajouter une propriété `xml:lang` aux propriétés de texte pour spécifier la langue du texte.
