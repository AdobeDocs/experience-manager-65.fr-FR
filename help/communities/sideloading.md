---
title: Chargement partiel des composants
seo-title: Chargement partiel des composants
description: Le téléchargement local des composants de communautés est utile lorsqu’une page Web est conçue comme une application simple d’une seule page qui modifie dynamiquement ce qui s’affiche en fonction de ce qui est sélectionné par le du site.
seo-description: Le téléchargement local des composants de communautés est utile lorsqu’une page Web est conçue comme une application simple d’une seule page qui modifie dynamiquement ce qui s’affiche en fonction de ce qui est sélectionné par le du site.
uuid: 8c9a5fde-26a3-4610-bc14-f8b665059015
contentOwner: msm-service
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
topic-tags: developing
content-type: reference
discoiquuid: a9cb5294-e5ab-445b-b7c2-ffeecda91c50
translation-type: tm+mt
source-git-commit: 89156f94f2d0494d44d4f0b99abfba4fafbc66d3

---


# Chargement partiel des composants {#component-sideloading}

## Présentation {#overview}

Le téléchargement local des composants de communautés est utile lorsqu’une page Web est conçue comme une application simple d’une seule page qui modifie dynamiquement ce qui s’affiche en fonction de ce qui est sélectionné par le du site.

Cela se produit lorsque les composants Communautés n’existent pas dans le modèle de page, mais qu’ils sont dynamiquement ajoutés après une sélection de de site.

Etant donné que le cadre des composants sociaux (SCF) présente une présence légère, seuls les composants SCF existants au moment du chargement initial de la page sont enregistrés. Pour qu’un composant SCF ajouté dynamiquement soit enregistré après le chargement de la page, SCF doit être appelé pour &quot;télécharger localement&quot; le composant.

Lorsqu’une page est conçue pour télécharger localement des composants de communautés, il est possible de mettre en cache la page entière.

Pour ajouter dynamiquement des composants SCF, procédez comme suit :

1. [Ajouter le composant au DOM](#dynamically-add-component-to-dom)

1. [Téléchargez le composant](#sideload-by-invoking-scf) en utilisant l’une des deux méthodes suivantes :

* [Inclusion dynamique](#dynamic-inclusion)
   * Boostrap tous les composants ajoutés dynamiquement
* [Chargement dynamique](#dynamic-loading)
   * Ajouter un composant spécifique à la demande

>[!NOTE]
>
>Le téléchargement de [ressources](scf.md#add-or-include-a-communities-component) non existantes n’est pas pris en charge.


## Ajouter dynamiquement le composant au modèle DOM {#dynamically-add-component-to-dom}

Que le composant soit inclus dynamiquement ou chargé dynamiquement, il doit d’abord être ajouté au modèle DOM.

Lors de l’ajout du composant SCF, la balise la plus courante à utiliser est la balise DIV, mais d’autres balises peuvent également être utilisées. Etant donné que SCF examine uniquement le DOM au chargement initial de la page, cet ajout au DOM passe inaperçu jusqu’à ce que SCF soit explicitement appelé.

Quelle que soit la balise utilisée, l’élément doit au minimum se conformer au modèle d’élément racine SCF normal en contenant les deux attributs suivants :

* **data-component-id**

   Chemin d’accès effectif au composant ajouté.

* **data-scf-component**

   Type de ressource du composant.

Voici un exemple de composant de commentaires ajouté :

```xml
<div
    class="scf-commentsystem scf translation-commentsystem"
    data-component-id="<%= currentPage.getPath()%>/jcr:content/content-left/comments"
    data-scf-component="social/commons/components/hbs/comments"
>
</div>
```

## Téléchargement partiel par appel de SCF {#sideload-by-invoking-scf}

### Inclusion dynamique {#dynamic-inclusion}

L’inclusion dynamique utilise une requête d’amorçage qui entraîne l’examen par SCF du modèle DOM et l’amorçage de tous les composants SCF trouvés sur la page.

Pour initialiser les composants SCF à tout moment après le chargement de la page, il vous suffit de déclencher un JQuery  comme suit :

`$(document).trigger(SCF.events.BOOTSTRAP_REQUEST);`

### Chargement dynamique {#dynamic-loading}

Le chargement dynamique permet de contrôler le chargement des composants SCF.

Au lieu d’amorcer tous les composants SCF trouvés dans le modèle DOM, il est possible de spécifier un composant SCF spécifique à charger à l’aide de cette méthode JavaScript :

`SCF.addComponent(document.getElementById(*someId*));`

Où `someId` est la valeur de l’ `data-component-id` attribut.
