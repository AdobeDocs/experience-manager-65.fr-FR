---
title: Chargement latéral des composants
description: Le chargement latéral des composants de Communities est utile lorsqu’une page web est conçue comme une application simple sur une seule page qui modifie dynamiquement les éléments affichés en fonction de ce qui est sélectionné par le visiteur du site
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: 960e132c-b370-43d1-bd8f-e7d0ded7c0b3
solution: Experience Manager
feature: Communities
role: Admin
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
feature_v2:
  - id: b013f126-a97e-52d1-9f79-cb5bbb12114e
    internal-label: Communities
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '402'
ht-degree: 0%
---
# Chargement latéral des composants {#component-sideloading}

## Vue d’ensemble {#overview}

Le chargement latéral des composants de Communities est utile lorsqu’une page web est conçue comme une application simple sur une seule page qui modifie dynamiquement les éléments affichés en fonction de ce qui est sélectionné par le visiteur du site.

Cela s’effectue lorsque les composants de communautés n’existent pas dans le modèle de page, mais sont ajoutés dynamiquement à la suite d’une sélection d’un visiteur ou d’une visiteuse du site.

Étant donné que la structure des composants sociaux (SCF) est légère, seuls les composants SCF qui existent au moment du chargement initial de la page sont enregistrés. Pour qu’un composant SCF ajouté dynamiquement soit enregistré après le chargement de la page, SCF doit être appelé pour « charger le composant sur le serveur latéral ».

Lorsqu’une page est conçue pour charger des composants de communautés sur le serveur, il est possible de mettre en cache la page entière.

Pour ajouter dynamiquement des composants SCF, procédez comme suit :

1. [Ajouter le composant au DOM](#dynamically-add-component-to-dom)

1. [Chargez le composant sur le côté](#sideload-by-invoking-scf) en utilisant l’une des deux méthodes suivantes :

* [Inclusion dynamique](#dynamic-inclusion)
  * Amorcer tous les composants ajoutés dynamiquement
* [Chargement dynamique](#dynamic-loading)
  * Ajouter un composant spécifique à la demande

>[!NOTE]
>
>Le chargement latéral de [&#x200B; ressources non existantes &#x200B;](scf.md#add-or-include-a-communities-component) n’est pas pris en charge.

## Ajout dynamique d’un composant au DOM {#dynamically-add-component-to-dom}

Que le composant soit inclus ou chargé dynamiquement, il doit d’abord être ajouté au DOM.

Lors de l’ajout du composant SCF, la balise la plus courante à utiliser est la balise DIV, mais d’autres balises peuvent également être utilisées. SCF n’examine le DOM que lors du chargement initial de la page. Aussi, cet ajout au DOM passera inaperçu jusqu’à ce que SCF soit explicitement appelé.

Quelle que soit la balise utilisée, l’élément doit au minimum être conforme au modèle d’élément racine SCF normal en contenant les deux attributs suivants :

* **data-component-id**

  Chemin d’accès effectif au composant ajouté.

* **data-scf-component**

  ResourceType du composant.

Voici un exemple de composant Commentaires ajouté :

```xml
<div
    class="scf-commentsystem scf translation-commentsystem"
    data-component-id="<%= currentPage.getPath()%>/jcr:content/content-left/comments"
    data-scf-component="social/commons/components/hbs/comments"
>
</div>
```

## Chargement latéral en appelant SCF {#sideload-by-invoking-scf}

### Inclusion Dynamique {#dynamic-inclusion}

L’inclusion dynamique utilise une requête d’amorçage qui entraîne l’examen par le SCF du DOM et l’amorçage de tous les composants SCF trouvés sur la page.

Pour initialiser les composants SCF à tout moment après le chargement de la page, il vous suffit de déclencher un événement JQuery comme suit :

`$(document).trigger(SCF.events.BOOTSTRAP_REQUEST);`

### Chargement dynamique {#dynamic-loading}

Le chargement dynamique permet de contrôler le chargement des composants SCF.

Au lieu d’amorcer tous les composants SCF trouvés dans le DOM, il est possible de spécifier un composant SCF spécifique à charger à l’aide de cette méthode JavaScript :

`SCF.addComponent(document.getElementById(*someId*));`

Où `someId` est la valeur de l’attribut `data-component-id`.
