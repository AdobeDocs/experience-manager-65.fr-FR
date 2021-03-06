---
title: Conceptions et Designer
seo-title: Conceptions et Designer
description: Vous devez créer une conception pour votre site web et dans AEM. Pour ce faire, vous allez utiliser le Designer.
seo-description: Vous devez créer une conception pour votre site web et dans AEM. Pour ce faire, vous allez utiliser le Designer.
uuid: b880ab49-8bea-4925-9b7b-e911ebda14ee
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
discoiquuid: f9bcb6eb-1df4-4709-bcec-bef0931f797a
exl-id: c81c5910-b6c9-41bd-8840-a6782792701f
source-git-commit: adbdff9ff5b5bd8f5f6b22fb724a0e5273072de2
workflow-type: tm+mt
source-wordcount: '386'
ht-degree: 58%

---

# Conceptions et Designer{#designs-and-the-designer}

>[!CAUTION]
>
>Cet article explique comment créer un site web à partir de l’IU classique. Adobe vous recommande de tirer parti des technologies AEM les plus récentes pour vos sites web. Vous en trouverez une description détaillée dans l’article [Prise en main du développement d’AEM Sites](/help/sites-developing/getting-started.md).

Designer permet de créer une conception pour votre site web à l’aide de l’[interface utilisateur classique](/help/release-notes/touch-ui-features-status.md) dans AEM.

>[!NOTE]
>
>Pour plus d’informations sur l’accessibilité web, voir [AEM et les instructions pour l’accessibilité web](/help/managing/web-accessibility.md).

## Utilisation de Designer {#using-the-designer}

Votre conception peut être définie dans la section **designs** de l’onglet **Outils** :

![screen_shot_2012-02-01at30237pm](assets/screen_shot_2012-02-01at30237pm.png)

Ici, vous pouvez créer la structure requise pour stocker la conception, puis stocker les feuilles de style en cascade (CSS) et les images requises.

Les conceptions sont stockées sous `/apps/<your-project>`. Le chemin d’accès à la conception à utiliser pour un site web est spécifié à l’aide de la propriété `cq:designPath` du nœud `jcr:content`.

![chlimage_1-74](assets/chlimage_1-74a.png)

>[!NOTE]
>
>Toutes les modifications apportées à une page dans le mode Création sont conservées sous le nœud de conception du site et sont automatiquement appliquées à toutes les pages qui présentent la même conception.

## Éléments nécessaires  {#what-you-will-need}

Pour créer votre conception, vous aurez besoin des éléments suivants :

**CSS**  : les feuilles de style en cascade définissent les formats de zones spécifiques sur vos pages.
**Images**  : images utilisées pour des fonctionnalités telles que des arrière-plans et des boutons.

### Points à prendre en compte lors de la conception de votre site web {#considerations-when-designing-your-website}

Lors du développement d’un site web, il est vivement recommandé de stocker les images et les fichiers CSS sous `/apps/<your-project>` afin de pouvoir référencer vos ressources en fonction de la conception actuelle, comme décrit par l’extrait de code suivant.

```xml
<%= currentDesign.getPath() + "/static/img/icon.gif %>
```

L’exemple précédent offre plusieurs avantages :

* Les composants peuvent avoir une apparence différente selon que chaque site utilise un chemin de conception différent.
* La reconception du site web peut simplement être effectuée en pointant le chemin de conception vers un noeud différent à la racine du site, de `design/v1` à `design/v2.`.

* `/etc/designs` et  `/content` sont les seules URL externes que le navigateur voit vous protéger d’un utilisateur externe qui se demande ce qui se trouve sous votre  `/apps` arborescence. Les avantages des URL ci-dessus aident également l’administrateur système à mieux configurer la sécurité, dans la mesure où vous limitez l’exposition des ressources à une poignée d’emplacements distincts.
