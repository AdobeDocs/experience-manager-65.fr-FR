---
title: Prise en charge des métadonnées XMP dans [!DNL Adobe Experience Manager Assets].
description: Learn about the XMP (Extensible Metadata Platform) metadata standard used by [!DNL Experience Manager Assets] for metadata management. XMP offre un format standard pour la création, le traitement et l’échange de métadonnées pour une multitude d’applications.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 9fc1201db83ae0d3bb902d4dc3ab6d78cc1dc251
workflow-type: tm+mt
source-wordcount: '776'
ht-degree: 78%

---


# Métadonnées XMP {#xmp-metadata}

XMP (Extensible Metadata Platform) est la norme de métadonnées utilisée par [!DNL Adobe Experience Manager Assets] la gestion de toutes les métadonnées. XMP offre un format standard pour la création, le traitement et l’échange de métadonnées pour une multitude d’applications.

En plus d’un codage de métadonnées universel qui peut être incorporé dans tous les formats de fichier, XMP fournit un [modèle de contenu](xmp.md#xmp-core-concepts) riche et est [pris en charge par Adobe](xmp.md#advantages-of-xmp) et d’autres sociétés. Ainsi, les utilisateurs XMP, en association avec , disposent d’une plate-forme puissante sur laquelle s’appuyer.[!DNL Assets]

La [spécification XMP](https://www.adobe.com/devnet/xmp.html) est disponible auprès d’Adobe.

## What is XMP? {#what-is-xmp}

[!DNL Assets] prend nativement en charge le XMP - l&#39;Extensible Metadata Platform piloté par l&#39;Adobe. XMP est une norme destinée au traitement et au stockage de métadonnées normalisées et propriétaires dans les ressources numériques. La norme XMP est conçue pour être la norme commune permettant à plusieurs applications de fonctionner efficacement avec les métadonnées.

Production professionals, for example, use the built-in XMP support within Adobe&#39;s applications to pass information across multiple file formats. [!DNL Assets] repository extracts the XMP metadata and uses it to manage the content lifecycle and offers the ability to create automation workflows.

XMP normalise la façon dont les métadonnées sont définies, créées et traitées en fournissant un modèle de données, un modèle de stockage et des schémas. Tous ces concepts sont abordés dans cette section.

Toutes les métadonnées héritées d’EXIF, d’ID3 ou de Microsoft Office sont automatiquement converties au format XMP, qui peut être étendu pour prendre en charge le schéma de métadonnées spécifiques au client comme les catalogues de produits.

Dans la norme XMP, les métadonnées sont constituées d’un ensemble de propriétés. Ces propriétés sont toujours associées à une entité particulière appelée ressource ; c&#39;est-à-dire que les propriétés sont &quot;environ&quot; la ressource. Dans le cas de XMP, il s’agit toujours de la ressource (ou actif).

### Adobe {#adobe}

Adobe a introduit pour la première fois la norme XMP dans le cadre du logiciel Adobe Acrobat. Depuis, la norme XMP a été largement adoptée.

### XMP ecosystem {#xmp-ecosystem}

XMP définit un modèle de [métadonnées](https://fr.wikipedia.org/wiki/Métadonnée) exploitable avec n’importe quel ensemble défini d’éléments de métadonnées. XMP définit également des [schémas](https://en.wikipedia.org/wiki/XML_schema) spécifiques pour des propriétés de base utiles pour consigner l’historique d’une ressource lorsqu’elle passe par diverses étapes de traitement, de la photographie, en passant par la [numérisation](https://fr.wikipedia.org/wiki/Scanner_(informatique)) ou la création en tant que texte, à travers des étapes de retouche photo (comme le [recadrage](https://fr.wikipedia.org/wiki/Recadrage_(image)) ou l’ajustement de couleur), pour former une image finale. XMP permet à chaque programme ou appareil d’ajouter ses propres informations à une ressource numérique. Ces informations peuvent être ensuite conservées dans le fichier numérique final.

XMP est le plus souvent sérialisé et stocké à l’aide d’un sous-ensemble du [W3C](https://fr.wikipedia.org/wiki/World_Wide_Web_Consortium) [Resource Description Framework](https://fr.wikipedia.org/wiki/Resource_Description_Framework) (RDF), exprimé à son tour en format [XML](https://fr.wikipedia.org/wiki/Extensible_Markup_Language).

## Avantages du mode XMP  {#advantages-of-xmp}

La norme XMP présente les avantages suivants par rapport aux autres normes de codage et schémas :

* Les métadonnées basées sur la norme XMP sont très puissantes et précises.
* La norme XMP permet de définir plusieurs valeurs pour une propriété.
* XMP dispose d’un encodage normalisé, ce qui vous permet d’échanger facilement des métadonnées.
* Le format XMP est extensible. Vous pouvez ajouter d’autres informations à vos ressources.

### Extensibles {#extensible}

La norme XMP a été conçue pour être extensible, ce qui vous permet d’ajouter des types de métadonnées personnalisés dans les données XMP. En revanche, ce n’est pas le cas d’EXIF qui présente une liste des propriétés qui ne peut pas être étendue.

>[!NOTE]
>
>En règle générale, XMP ne permet pas l’incorporation des types de données binaires. Pour gérer des données binaires dans XMP, comme des images miniatures, celles-ci doivent être codées dans un format XML tel que `Base64`.

## Notions fondamentales relatives à XMP {#xmp-core-concepts}

Les sections ci-après décrivent les notions fondamentales relatives à XMP, notamment les espaces de noms et les schémas, les propriétés et les valeurs, ainsi que les variantes linguistiques.

### Espaces de noms et schémas {#namespaces-and-schemata}

Un schéma XMP est un ensemble de noms de propriétés défini dans un espace de noms XML commun qui comprend
le type des données et des informations descriptives. Un schéma XMP est identifié par l’URI de l’espace de noms XML. L’utilisation des espaces de noms permet d’empêcher tout conflit entre les propriétés dans différents schémas qui portent le même nom, mais ont un sens différent.

For example, the `Creator` property in two independently designed schemas might mean the person who created the asset or it could mean the application that created the asset (for example, Adobe Photoshop).

### Propriétés et valeurs {#properties-and-values}

XMP peut inclure des propriétés de l’un ou de plusieurs des schémas. Par exemple, un sous-ensemble classique utilisé par de nombreuses applications Adobe peut comprendre les éléments suivants :

* Schéma Dublin Core : `dc:title`, `dc:creator`, `dc:subject`, `dc:format`, `dc:rights`.
* XMP basic schema: `xmp:CreateDate`, `xmp:CreatorTool`, `xmp:ModifyDate`, `xmp:metadataDate`.
* XMP rights management schema: `xmpRights:WebStatement`, `xmpRights:Marked`.
* XMP media management schema: `xmpMM:DocumentID`.

### Variantes linguistiques {#language-alternatives}

XMP lets you add an `xml:lang` property to text properties to specify the language of the text.
