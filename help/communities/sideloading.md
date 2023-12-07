---
title: Chargement partiel des composants
description: Le téléchargement local des composants de communauté est utile lorsqu’une page web est conçue comme une application simple d’une seule page qui modifie dynamiquement ce qui s’affiche en fonction de ce qui est sélectionné par le visiteur du site.
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
exl-id: 960e132c-b370-43d1-bd8f-e7d0ded7c0b3
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '396'
ht-degree: 0%

---

# Chargement partiel des composants {#component-sideloading}

## Vue d’ensemble {#overview}

Le téléchargement local des composants de communauté est utile lorsqu’une page web est conçue comme une application simple d’une seule page qui modifie dynamiquement ce qui s’affiche en fonction de ce qui est sélectionné par le visiteur du site.

Cela est effectué lorsque les composants Communities n’existent pas dans le modèle de page, mais sont ajoutés dynamiquement suite à la sélection d’un visiteur du site.

Étant donné que la structure de composants sociaux (SCF) est légère, seuls les composants SCF qui existent au moment du chargement initial de la page sont enregistrés. Pour qu’un composant SCF ajouté dynamiquement soit enregistré après le chargement de la page, SCF doit être appelé pour &quot;charger côté&quot; le composant.

Lorsqu’une page est conçue pour charger localement des composants Communities, il est possible de mettre en cache la page entière.

Les étapes d’ajout dynamique de composants SCF sont les suivantes :

1. [Ajouter le composant au DOM](#dynamically-add-component-to-dom)

1. [Chargement partiel du composant](#sideload-by-invoking-scf) en utilisant l’une des deux méthodes suivantes :

* [Inclusion dynamique](#dynamic-inclusion)
   * Boostrap tous les composants dynamiquement ajoutés
* [Chargement dynamique](#dynamic-loading)
   * Ajouter un composant spécifique à la demande

>[!NOTE]
>
>Chargement partiel de [ressources non existantes](scf.md#add-or-include-a-communities-component) n’est pas prise en charge.

## Ajout dynamique de composant à DOM {#dynamically-add-component-to-dom}

Que le composant soit inclus dynamiquement ou chargé dynamiquement, il doit d’abord être ajouté au DOM.

Lors de l’ajout du composant SCF, la balise la plus courante à utiliser est la balise DIV, mais d’autres balises peuvent également être utilisées. Comme SCF examine uniquement le DOM au chargement initial de la page, cet ajout au DOM ne sera pas remarqué tant que SCF n’aura pas été explicitement appelé.

Quelle que soit la balise utilisée, l’élément doit au minimum se conformer au modèle d’élément racine SCF normal en contenant les deux attributs suivants :

* **data-component-id**

  Chemin d’accès effectif au composant ajouté.

* **data-scf-component**

  ResourceType du composant.

Voici un exemple de composant de commentaires ajouté :

```xml
<div
    class="scf-commentsystem scf translation-commentsystem"
    data-component-id="<%= currentPage.getPath()%>/jcr:content/content-left/comments"
    data-scf-component="social/commons/components/hbs/comments"
>
</div>
```

## Chargement partiel en appelant SCF {#sideload-by-invoking-scf}

### Inclusion dynamique {#dynamic-inclusion}

L’inclusion dynamique utilise une requête de démarrage qui entraîne l’examen par SCF du modèle DOM et le bootsrapage de tous les composants SCF présents sur la page.

Pour initialiser des composants SCF à tout moment après le chargement de la page, déclenchez simplement un événement JQuery comme celui-ci :

`$(document).trigger(SCF.events.BOOTSTRAP_REQUEST);`

### Chargement dynamique {#dynamic-loading}

Le chargement dynamique permet de contrôler le chargement des composants SCF.

Au lieu d’amorcer tous les composants SCF du modèle DOM, il est possible de spécifier un composant SCF spécifique à charger à l’aide de cette méthode JavaScript :

`SCF.addComponent(document.getElementById(*someId*));`

Où `someId` est la valeur de la variable `data-component-id` attribut.
