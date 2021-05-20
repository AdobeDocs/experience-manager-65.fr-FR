---
title: Utilisation du sélecteur de catégorie et de produit CIF
description: Découvrez comment utiliser le sélecteur de produits et de catégories CIF dans vos composants de commerce client pour prendre en charge les auteurs et les spécialistes du marketing afin de travailler efficacement avec les données de catalogue et de produits commerciaux.
sub-product: Commerce
topics: Development
version: cloud-service
activity: develop
audience: developer
feature: Commerce Integration Framework
source-git-commit: d92a635d41cf1b14e109c316bd7264cf7d45a9fe
workflow-type: tm+mt
source-wordcount: '581'
ht-degree: 1%

---

# AEM Sélecteurs de création de contenu et de commerce {#cif-pickers}

AEM création de contenu et de commerce fournit un ensemble d’outils de création pour aider AEM auteurs et marketeurs à travailler efficacement avec les données et les catalogues de produits commerciaux. Le sélecteur de produits et le sélecteur de catégorie font partie du module complémentaire CIF et sont utilisés par les composants principaux CIF. Les projets peuvent utiliser ces sélecteurs dans n’importe quelle boîte de dialogue de composant pour sélectionner des produits ou des catégories.

## Sélecteur de produits {#product-picker}

Pour utiliser le sélecteur de produit dans un composant de projet, un développeur doit ajouter `commerce/gui/components/common/cifproductfield` à une boîte de dialogue de composant. Par exemple, utilisez ce qui suit pour cq:dialog :

```xml
<product jcr:primaryType="nt:unstructured"
    sling:resourceType="commerce/gui/components/common/cifproductfield"
    fieldDescription="The product or product variant displayed by the teaser"
    fieldLabel="Select Product"
    filter="folderOrProductOrVariant"
    name="./selection"
    selectionId="sku"/>
```

Le champ de produit permet de naviguer jusqu’au produit qu’un utilisateur souhaite sélectionner via les différentes vues. Par défaut, le champ product renvoie l’identifiant du produit, mais il peut être configuré à l’aide de l’attribut `selectionId` .

Le champ de sélecteur de produits prend en charge les propriétés facultatives suivantes :

- selectionId (id, uid, sku, slg, combinéSlug, combinéSku) - permet de choisir l’attribut de produit à renvoyer par le sélecteur (par défaut = id). L’utilisation de sku renvoie le SKU du produit sélectionné, tout en utilisant la combinaison de sku et renvoie une chaîne du type base#variant avec le SKU du produit de base et la variante sélectionnée, ou une seule SKU si un produit de base est sélectionné.
- filter (folderOrProduct, folderOrProductOrVariant) : filtre le contenu à rendre par le sélecteur lors de la navigation dans l’arborescence du produit. folderOrProduct - effectue le rendu des dossiers et des produits. folderOrProductOrVariant - effectue le rendu des dossiers, des variantes de produits et des variantes de produits. Si un produit ou une variante de produit est rendu, il devient également sélectionnable dans le sélecteur. (par défaut = folderOrProduct)
- multiple (true, false) : permet de sélectionner un ou plusieurs produits (par défaut = false).
- emptyText : pour configurer la valeur de texte vide du champ de sélecteur.

En outre, les propriétés de champ de boîte de dialogue standard telles que `name`, `fieldLabel` ou `fieldDescription` sont également prises en charge.

Le composant `cifproductfield` nécessite la bibliothèque cliente cif.shell.picker. Pour ajouter une bibliothèque cliente à une boîte de dialogue, vous pouvez utiliser la propriété extraClientlibs .

Vous trouverez un exemple complet de `cifproductfield` dans le projet [Composants principaux CIF](https://github.com/adobe/aem-core-cif-components/blob/master/ui.apps/src/main/content/jcr_root/apps/core/cif/components/commerce/productteaser/v1/productteaser/_cq_dialog/.content.xml). Voir aussi [Personnalisation des boîtes de dialogue](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/customizing.html?lang=en#customizing-dialogs) de la documentation sur les composants principaux d’AEM.

## Sélecteur de catégorie {#category-picker}

Le sélecteur de catégorie peut également être utilisé dans une boîte de dialogue de composant de la même manière que le sélecteur de produit.

Le fragment de code suivant peut être utilisé dans une configuration cq:dialog :

```xml
<category jcr:primaryType="nt:unstructured" 
    sling:resourceType="commerce/gui/components/common/cifcategoryfield" 
    fieldLabel="Category" 
    name="./categoryId" 
    selectionId="uid" />
```

Le champ de sélecteur de catégorie prend en charge les propriétés facultatives suivantes :

- selectionId(id, uid, log, idAndUrlPath, uidAndUrlPath) - permet de choisir l’attribut de catégorie à renvoyer par le sélecteur (par défaut = id). idAndUrlPath et uidAndUrlPath sont des options spéciales qui stockent les ID/uid de catégorie et url_path séparés par un | par exemple 1|men/top.
- multiple (true, false) : permet de sélectionner une ou plusieurs catégories (par défaut = false).

En outre, les propriétés de champ de boîte de dialogue standard telles que `name`, `fieldLabel` ou `fieldDescription` sont également prises en charge.

Comme le composant `cifproductfield` , le composant `cifcategoryfield` nécessite également la bibliothèque clif cif.shell.picker . Pour ajouter une bibliothèque cliente à une boîte de dialogue, vous pouvez utiliser la propriété `extraClientlibs` . Voir [Personnalisation des boîtes de dialogue](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/customizing.html?lang=en#customizing-dialogs) de la documentation sur les composants principaux d’AEM.

Vous trouverez un exemple complet de `cifcategoryfield` dans le projet [Composants principaux CIF](https://github.com/adobe/aem-core-cif-components/blob/master/ui.apps/src/main/content/jcr_root/apps/core/cif/components/commerce/featuredcategorylist/v1/featuredcategorylist/_cq_dialog/.content.xml).
