---
title: Conventions de dénomination des noeuds dans le référentiel de contenu Java
description: Les nœuds dans le référentiel sont soumis aux conventions de dénomination de Java Content Repository
uuid: 0515c5c5-3e93-4710-983f-c08c146467fc
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: 198098c0-432b-4a93-a94e-2552337435dd
exl-id: 01c6bb29-1d2d-4a45-b291-0e8d97c01a08
source-git-commit: a2fd3c0c1892ac648c87ca0dec440e22144c37a2
workflow-type: tm+mt
source-wordcount: '308'
ht-degree: 47%

---

# Conventions de dénomination{#naming-conventions}

Les nœuds dans le référentiel sont soumis aux conventions de dénomination de [Java Content Repository](/help/sites-developing/the-basics.md#java-content-repository). Toutefois, AEM impose d’autres conventions pour le nom des nœuds de page.

## Conventions de dénomination pour les pages {#naming-conventions-for-pages}

Ces conventions de dénomination sont mises en oeuvre à différents niveaux :

* JcrUtil : la mise en oeuvre AEM de la [Utilitaires JCR](#jcr-utilities).
* PageManager : la valeur [Gestionnaire de pages](#page-manager) fournit des méthodes pour les opérations au niveau de la page.
* Selon l’interface utilisateur utilisée :

   * [IU tactile standard](#standard-ui)
   * [Interface utilisateur classique](#classic-ui)

### Utilitaires JCR {#jcr-utilities}

[JcrUtil](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/index.html?com/day/cq/commons/jcr/JcrUtil.html) est l’implémentation AEM des utilitaires JCR. Les mappages de caractères qu’il contrôle et les validations suivantes présentent un intérêt particulier pour la validation des noms :

* `isValidName`

   * Vérifie si le nom n’est pas vide et contient uniquement des caractères valides.
   * Peut être utilisé pour vérifier si un nom proposé est valide.

* `createValidName`

   * Crée un libellé valide à partir d’une chaîne arbitraire.
   * Peut être utilisé pour créer un nom à partir d’un titre.

### Gestionnaire de pages {#page-manager}

[PageManager](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/api/PageManager.html) fournit des méthodes pour les opérations au niveau de la page, sur la base de [JCRUtil](#jcr-utilities).

### Interface utilisateur standard {#standard-ui}

L’IU tactile standard :

* Valide le nom en fonction des restrictions imposées par PageManager lorsque :

   * un titre de page est fourni pour la conversion dans le nom de noeud.
   * un nom de noeud explicite est fourni.

### Interface utilisateur classique {#classic-ui}

L’IU classique impose des restrictions plus strictes :

* Valide le nom lorsqu’un nom de noeud explicite se présente dans l’une des situations suivantes :

   * un titre de page est fourni pour la conversion dans le nom de noeud.
   * un nom de noeud explicite est fourni.

* Caractères valides (seuls ces caractères sont effectivement valides lorsqu’une page est créée dans l’IU classique, même si `PageManagerImpl` autorise des caractères supplémentaires) :

   * &#39;a&#39; à &#39;z&#39;
   * &quot;A&quot; à &quot;Z&quot;
   * &#39;0&#39; à &#39;9&#39;
   * _ (trait de soulignement)
   * `-` (tiret/moins)
