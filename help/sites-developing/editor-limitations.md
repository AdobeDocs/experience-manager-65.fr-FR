---
title: Limites de l’éditeur
seo-title: Editor Limitations
description: L’éditeur de l’interface utilisateur tactile emploie des couches pour interagir avec le contenu confiné dans un iFrame. Cette interaction présente certaines limites pour l’utilisation de l’éditeur, mais également pour les développeurs.
seo-description: The editor in the touch-enabled UI makes use of overlays to interact with content confined in an iframe. This interaction creates some limitations in both usage of the editor and also for developers.
uuid: ff524530-3f3a-4c5b-9f94-4aa9aeb9d461
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: introduction
discoiquuid: d748decb-a614-4c9e-a502-d6176b720f1a
exl-id: fd64f5dc-dfff-466b-8cdd-3c24ea1a15c8
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: ht
source-wordcount: '316'
ht-degree: 100%

---

# Limites de l’éditeur{#editor-limitations}

L’éditeur de l’interface utilisateur tactile emploie des couches pour interagir avec le contenu confiné dans un iFrame. Cette interaction présente certaines limites pour l’utilisation de l’éditeur, mais également pour les développeurs. Cette page résume ces limites et fournit des solutions lorsque cela s’avère possible.

## Limites fonctionnelles {#functional-limitations}

Un auteur peut être confronté aux limites fonctionnelles suivantes lors de l’utilisation de l’éditeur pour créer des pages.

### Liens inactifs {#links-not-active}

Lors de la [modification d’une page](/help/sites-authoring/editing-content.md), les liens ne sont pas actifs.

* [Basculez vers le mode **Aperçu**](/help/sites-authoring/editing-content.md#preview-mode) pour naviguer à l’aide des liens de votre contenu.

### Pages de structure {#structure-pages}

Les pages ne peuvent pas être nommées `structure`. Les pages nommées `structure` ne seront pas modifiables dans l’éditeur de page.

## Limitations de CSS {#css-limitations}

Un développeur peut être confronté aux limites suivantes concernant les interactions de l’éditeur avec CSS.

### Éléments à positionnement absolu {#absolutely-positioned-elements}

Les éléments à positionnement absolu peuvent occasionner des problèmes au niveau de la position de leur incrustation.

* Si cela se produit, assurez-vous que les dimensions de l’élément à positionnement absolu sont correctes, car l’éditeur créera une incrustation ayant exactement les mêmes dimensions.

### Unités vh {#vh-units}

Les unités `vh` ne sont pas prises en charge, car la hauteur de l’iFrame doit être réglée automatiquement par AEM.

### Images d’arrière-plan fixes {#fixed-background-images}

Il est possible que les images d’arrière-plan fixes ne puissent pas être affichées en mode fixe lors du défilement, étant donné qu’elles sont incorporées dans un iFrame.

* Sélectionnez **Afficher la page comme publiée** dans les actions de la barre d’en-tête pour afficher correctement la page.

### Hauteur de 100 % {#height}

La hauteur de 100 % n’est pas prise en charge sur l’élément de corps d’une page.

* Il est possible d’appliquer une solution afin d’implémenter un corps plein écran en « étirant » l’élément de corps comme suit :

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
