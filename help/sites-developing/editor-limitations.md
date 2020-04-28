---
title: Limites de l’éditeur
seo-title: Limites de l’éditeur
description: 'L’éditeur de l’interface utilisateur tactile emploie des couches pour interagir avec le contenu confiné dans un iFrame. Cette interaction présente certaines limites pour l’utilisation de l’éditeur, mais également pour les développeurs. '
seo-description: 'L’éditeur de l’interface utilisateur tactile emploie des couches pour interagir avec le contenu confiné dans un iFrame. Cette interaction présente certaines limites pour l’utilisation de l’éditeur, mais également pour les développeurs. '
uuid: ff524530-3f3a-4c5b-9f94-4aa9aeb9d461
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: introduction
discoiquuid: d748decb-a614-4c9e-a502-d6176b720f1a
translation-type: tm+mt
source-git-commit: 844d42ed50da153077423190684aa85265bce12f

---


# Limites de l’éditeur{#editor-limitations}

L’éditeur de l’interface utilisateur tactile emploie des couches pour interagir avec le contenu confiné dans un iFrame. Cette interaction présente certaines limites pour l’utilisation de l’éditeur, mais également pour les développeurs. Cette page résume ces limites et fournit des solutions lorsque cela s’avère possible.

## Limites fonctionnelles {#functional-limitations}

Un auteur peut être confronté aux limites fonctionnelles suivantes lors de l’utilisation de l’éditeur pour créer des pages.

### Liens inactifs {#links-not-active}

When [editing a page](/help/sites-authoring/editing-content.md), links are not active.

* [Passez en mode ****](/help/sites-authoring/editing-content.md#preview-mode) pour naviguer à l’aide des liens de votre contenu.

### Pages de structure {#structure-pages}

Impossible de nommer les pages `structure`. Les pages nommées `structure` ne peuvent pas être modifiées dans l’éditeur de page.

## Limitations CSS {#css-limitations}

Un développeur peut être confronté aux limites suivantes concernant les interactions de l’éditeur avec CSS.

### Éléments à positionnement absolu {#absolutely-positioned-elements}

Les éléments à positionnement absolu peuvent occasionner des problèmes au niveau de la position de leur incrustation.

* Si cela se produit, assurez-vous que les dimensions de l’élément à positionnement absolu sont correctes, car l’éditeur créera une incrustation ayant exactement les mêmes dimensions.

### Unités vh {#vh-units}

`vh` ne sont pas prises en charge, car la hauteur de l’iframe doit être automatiquement ajustée par AEM.

### Images d’arrière-plan fixes {#fixed-background-images}

Il est possible que les images d’arrière-plan fixes ne puissent pas être affichées en mode fixe lors du défilement, étant donné qu’elles sont incorporées dans un iFrame.

* Selecting **View Page as Published** in the header bar actions displays the page properly.

### Hauteur de 100 %{#height}

La hauteur de 100 % n’est pas prise en charge sur l’élément de corps d’une page.

* Une solution de contournement est possible pour implémenter un corps plein écran en &quot;étirant&quot; l’élément de corps comme suit :

```xml
body {
    position: absolute;
    top: 0;
    bottom: 0;
    right: 0;
    left: 0;
}
```

### Réduction de marge {#margin-collapsing}

Des problèmes de réduction de marge peuvent apparaître si le premier élément enfant de l’élément de corps comporte une marge.

* La solution consiste à ajouter un clearfix au niveau de l’élément de corps comme suit :

```xml
body:before, body:after{
    content: ' ';
    display: table;
}
```

