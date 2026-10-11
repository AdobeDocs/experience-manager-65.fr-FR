---
title: Limites de l’éditeur
description: L’éditeur de l’interface utilisateur optimisée pour les écrans tactiles emploie des recouvrements pour interagir avec le contenu confiné dans un iframe. Cette interaction présente certaines limites pour l’utilisation de l’éditeur, mais également pour les développeurs et développeuses.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: introduction
exl-id: fd64f5dc-dfff-466b-8cdd-3c24ea1a15c8
solution: Experience Manager, Experience Manager Sites
feature: Developing
role: Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: c45915cf-e157-4af7-a80d-97b905bcb3a5
    internal-label: Experience Manager Sites
feature_v2:
  - id: c5d917df-d8bd-5e97-a117-6dde1e9f7103
    internal-label: Developing
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '312'
ht-degree: 100%
---
# Limites de l’éditeur{#editor-limitations}

L’éditeur de l’interface utilisateur optimisée pour les écrans tactiles emploie des recouvrements pour interagir avec le contenu confiné dans un iframe. Cette interaction présente certaines limites pour l’utilisation de l’éditeur, mais également pour les développeurs. Cette page résume ces limites et fournit des solutions ou des contournements lorsque cela s’avère possible.

## Limites fonctionnelles {#functional-limitations}

Un auteur peut être confronté aux limites fonctionnelles suivantes lors de l’utilisation de l’éditeur pour créer des pages.

### Liens inactifs {#links-not-active}

Lors de la [modification d’une page](/help/sites-authoring/editing-content.md), les liens ne sont pas actifs.

* [Basculez vers le mode **Aperçu**](/help/sites-authoring/editing-content.md#preview-mode) pour naviguer à l’aide des liens de votre contenu.

### Pages de structure {#structure-pages}

Impossible de nommer les pages `structure`. Les pages nommées `structure` ne seront pas modifiables dans l’éditeur de page.

## Limitations de CSS {#css-limitations}

Un développeur peut être confronté aux limites suivantes concernant les interactions de l’éditeur avec CSS.

### Éléments à positionnement absolu {#absolutely-positioned-elements}

Les éléments positionnés de manière absolue peuvent entraîner des problèmes de position de leur recouvrement.

* Si cela se produit, assurez-vous que les dimensions de l’élément à positionnement absolu sont correctes, car l’éditeur crée un recouvrement avec les mêmes dimensions.

### Unités vh {#vh-units}

Les unités `vh` ne sont pas prises en charge, car la hauteur de l’iframe doit être réglée automatiquement par Adobe Experience Manager (AEM).

### Images d’arrière-plan fixes {#fixed-background-images}

Il est possible que les images d’arrière-plan fixes ne puissent pas être affichées en mode fixe lors du défilement, étant donné qu’elles sont incorporées dans un iframe.

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
