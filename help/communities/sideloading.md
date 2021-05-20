---
title: Chargement partiel des composants
seo-title: Chargement partiel des composants
description: Le téléchargement local des composants de communauté est utile lorsqu’une page web est conçue comme une application simple d’une seule page qui modifie dynamiquement ce qui s’affiche en fonction de ce qui est sélectionné par le visiteur du site.
seo-description: Le téléchargement local des composants de communauté est utile lorsqu’une page web est conçue comme une application simple d’une seule page qui modifie dynamiquement ce qui s’affiche en fonction de ce qui est sélectionné par le visiteur du site.
uuid: 8c9a5fde-26a3-4610-bc14-f8b665059015
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: a9cb5294-e5ab-445b-b7c2-ffeecda91c50
exl-id: 960e132c-b370-43d1-bd8f-e7d0ded7c0b3
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '430'
ht-degree: 0%

---

# Chargement des composants {#component-sideloading}

## Présentation {#overview}

Le téléchargement local des composants de communauté est utile lorsqu’une page web est conçue comme une application simple d’une seule page qui modifie dynamiquement ce qui s’affiche en fonction de ce qui est sélectionné par le visiteur du site.

Cela est effectué lorsque les composants Communities n’existent pas dans le modèle de page, mais sont ajoutés dynamiquement suite à la sélection d’un visiteur du site.

Étant donné que la structure de composants sociaux (SCF) est légère, seuls les composants SCF qui existent au moment du chargement initial de la page sont enregistrés. Pour qu’un composant SCF ajouté dynamiquement soit enregistré après le chargement de la page, SCF doit être appelé pour &quot;charger côté&quot; le composant.

Lorsqu’une page est conçue pour charger localement des composants Communities, il est possible de mettre en cache la page entière.

Les étapes d’ajout dynamique de composants SCF sont les suivantes :

1. [Ajouter le composant au DOM](#dynamically-add-component-to-dom)

1. [Téléchargez le ](#sideload-by-invoking-scf) composant de l’une des deux façons suivantes :

* [Inclusion dynamique](#dynamic-inclusion)
   * Boostrap tous les composants dynamiquement ajoutés
* [Chargement dynamique](#dynamic-loading)
   * Ajouter un composant spécifique à la demande

>[!NOTE]
>
>Le téléchargement de [ressources non existantes](scf.md#add-or-include-a-communities-component) n’est pas pris en charge.

## Ajouter dynamiquement le composant au DOM {#dynamically-add-component-to-dom}

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

Où `someId` est la valeur de l’attribut `data-component-id`.
