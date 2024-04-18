---
title: Limites de l’éditeur
description: L’éditeur de l’interface utilisateur tactile utilise des superpositions pour interagir avec le contenu confiné dans un iframe. Cette interaction présente certaines limites pour l’utilisation de l’éditeur, mais également pour les développeurs.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: introduction
exl-id: fd64f5dc-dfff-466b-8cdd-3c24ea1a15c8
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
source-git-commit: 66db4b0b5106617c534b6e1bf428a3057f2c2708
workflow-type: tm+mt
source-wordcount: '308'
ht-degree: 59%

---

# Limites de l’éditeur{#editor-limitations}

L’éditeur de l’interface utilisateur tactile utilise des superpositions pour interagir avec le contenu confiné dans un iframe. Cette interaction présente certaines limites pour l’utilisation de l’éditeur, mais également pour les développeurs. Cette page résume ces limites et fournit des solutions ou des contournements lorsque cela s’avère possible.

## Limites fonctionnelles {#functional-limitations}

Un auteur peut être confronté aux limites fonctionnelles suivantes lors de l’utilisation de l’éditeur pour créer des pages.

### Liens inactifs {#links-not-active}

Lors de la [modification d’une page](/help/sites-authoring/editing-content.md), les liens ne sont pas actifs.

* [Basculez vers le mode **Aperçu**](/help/sites-authoring/editing-content.md#preview-mode) pour naviguer à l’aide des liens de votre contenu.

### Pages de structure {#structure-pages}

Impossible de nommer les pages `structure`. Pages nommées `structure` ne sont pas modifiables dans l’éditeur de page.

## Limitations de CSS {#css-limitations}

Un développeur peut être confronté aux limites suivantes concernant les interactions de l’éditeur avec CSS.

### Éléments à positionnement absolu {#absolutely-positioned-elements}

Les éléments positionnés de manière absolue peuvent entraîner des problèmes de position de leur recouvrement.

* Si cela se produit, assurez-vous que les dimensions de l’élément à positionnement absolu sont correctes, car l’éditeur crée une superposition avec les mêmes dimensions.

### Unités vh {#vh-units}

`vh` ne sont pas prises en charge, car la hauteur de l’iframe doit être ajustée automatiquement par Adobe Experience Manager (AEM).

### Images d’arrière-plan fixes {#fixed-background-images}

Les images d’arrière-plan fixes peuvent ne pas être affichées comme fixes lors du défilement, car elles sont incorporées dans un iframe.

* Sélectionnez **Afficher la page comme publiée** dans les actions de la barre d’en-tête pour afficher correctement la page.

### Hauteur de 100 % {#height}

La hauteur de 100 % n’est pas prise en charge sur l’élément de corps d’une page.

* Une solution de contournement est possible en implémentant un corps plein écran en &quot;étirant&quot; l’élément de corps comme suit :

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
