---
title: Utilisation du sélecteur de catégories et de produits CIF
description: Découvrez comment utiliser le sélecteur de produits et de catégories CIF dans vos composants de commerce client pour aider les auteurs et les spécialistes du marketing à travailler efficacement avec les données de catalogue et de produits commerciaux.
sub-product: Commerce
topics: Development
version: cloud-service
activity: develop
audience: developer
feature: Commerce Integration Framework
translation-type: tm+mt
source-git-commit: d92a635d41cf1b14e109c316bd7264cf7d45a9fe
workflow-type: tm+mt
source-wordcount: '581'
ht-degree: 1%

---

# Sélecteur de création de contenu et de commerce AEM {#cif-pickers}

AEM Content &amp; Commerce Authoring fournit un ensemble d’outils de création pour aider AEM auteurs et spécialistes du marketing à travailler efficacement avec les données et les catalogues des produits commerciaux. Le Sélecteur de produits et le Sélecteur de Catégories font partie du module complémentaire CIF et sont utilisés par les composants principaux CIF. Les projets peuvent utiliser ces sélecteurs dans n’importe quelle boîte de dialogue de composant pour sélectionner des produits ou des catégories.

## Sélecteur de produits {#product-picker}

Pour utiliser le sélecteur de produits dans un composant de projet, un développeur doit ajouter `commerce/gui/components/common/cifproductfield` à une boîte de dialogue de composant. Par exemple, utilisez les éléments suivants pour la boîte de dialogue cq:dialog :

```xml
<product jcr:primaryType="nt:unstructured"
    sling:resourceType="commerce/gui/components/common/cifproductfield"
    fieldDescription="The product or product variant displayed by the teaser"
    fieldLabel="Select Product"
    filter="folderOrProductOrVariant"
    name="./selection"
    selectionId="sku"/>
```

Le champ de produit permet de naviguer jusqu’au produit qu’un utilisateur souhaite sélectionner via les différentes vues. Par défaut, le champ product renvoie l&#39;identifiant du produit, mais il peut être configuré à l&#39;aide de l&#39;attribut `selectionId`.

Le champ du sélecteur de produits prend en charge les propriétés facultatives suivantes :

- selectedId (id, uid, sku, slg, combinéSlug, combinéSku) - permet de choisir l&#39;attribut de produit à renvoyer par le sélecteur (par défaut = id). L’utilisation de sku renvoie l’sku du produit sélectionné, tout en utilisant combinéSku et renvoie une chaîne telle que base#variant avec l’skus du produit de base et la variante sélectionnée, ou une seule sku si un produit de base est sélectionné.
- filter (folderOrProduct, folderOrProductOrVariant) : filtres le contenu à rendre par le sélecteur lors de la navigation dans l’arborescence du produit. folderOrProduct : restitue les dossiers et les produits. folderOrProductOrVariant - effectue le rendu des dossiers, des variantes de produits et de produits. Si un produit ou une variante de produit est rendu, il devient également sélectionnable dans le sélecteur. (par défaut = folderOrProduct)
- multiple (true, false) : permet de sélectionner un ou plusieurs produits (par défaut = false).
- emptyText - pour configurer la valeur de texte vide du champ de sélecteur

En outre, les propriétés de champ de journal standard telles que `name`, `fieldLabel` ou `fieldDescription` sont également prises en charge.

Le composant `cifproductfield` nécessite cif.shell.picker clientlib. Pour ajouter une bibliothèque cliente à une boîte de dialogue, vous pouvez utiliser la propriété extraClientlibs.

Vous trouverez un exemple de fonctionnement complet de `cifproductfield` dans le projet [Composants principaux du FIC](https://github.com/adobe/aem-core-cif-components/blob/master/ui.apps/src/main/content/jcr_root/apps/core/cif/components/commerce/productteaser/v1/productteaser/_cq_dialog/.content.xml). Voir aussi [Personnalisation des boîtes de dialogue](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/customizing.html?lang=en#customizing-dialogs) de la documentation sur les composants principaux AEM.

## Sélecteur de catégories {#category-picker}

Le sélecteur de catégorie peut également être utilisé dans une boîte de dialogue de composant de la même manière que le sélecteur de produits.

Le fragment de code suivant peut être utilisé dans une configuration cq:dialog :

```xml
<category jcr:primaryType="nt:unstructured" 
    sling:resourceType="commerce/gui/components/common/cifcategoryfield" 
    fieldLabel="Category" 
    name="./categoryId" 
    selectionId="uid" />
```

Le champ Sélecteur de catégorie prend en charge les propriétés facultatives suivantes :

- selectedId(id, uid, slg, idAndUrlPath, uidAndUrlPath) - permet de choisir l&#39;attribut de catégorie à renvoyer par le sélecteur (par défaut = id). Les options idAndUrlPath et uidAndUrlPath sont des options spéciales qui stockent les id/uid et url_path de la catégorie, séparés par un | comme par exemple 1|men/tops.
- multiple (true, false) : permet de sélectionner une ou plusieurs catégories (par défaut = false).

En outre, les propriétés de champ de journal standard telles que `name`, `fieldLabel` ou `fieldDescription` sont également prises en charge.

Comme le composant `cifproductfield`, le composant `cifcategoryfield` nécessite également cif.shell.picker clientlib. Pour ajouter une bibliothèque cliente à une boîte de dialogue, vous pouvez utiliser la propriété `extraClientlibs`. Voir [Personnalisation des boîtes de dialogue](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/customizing.html?lang=en#customizing-dialogs) de la documentation sur les composants principaux AEM.

Vous trouverez un exemple de fonctionnement complet de `cifcategoryfield` dans le projet [Composants principaux du FIC](https://github.com/adobe/aem-core-cif-components/blob/master/ui.apps/src/main/content/jcr_root/apps/core/cif/components/commerce/featuredcategorylist/v1/featuredcategorylist/_cq_dialog/.content.xml).
