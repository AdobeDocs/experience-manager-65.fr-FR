---
title: Conventions de dénomination
seo-title: Conventions de dénomination
description: Les nœuds dans le référentiel sont soumis aux conventions de dénomination du référentiel Java Content
seo-description: Les nœuds dans le référentiel sont soumis aux conventions de dénomination du référentiel Java Content
uuid: 0515c5c5-3e93-4710-983f-c08c146467fc
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: platform
content-type: reference
discoiquuid: 198098c0-432b-4a93-a94e-2552337435dd
translation-type: tm+mt
source-git-commit: 5128a08d4db21cda821de0698b0ac63ceed24379
workflow-type: tm+mt
source-wordcount: '317'
ht-degree: 95%

---


# Conventions de dénomination{#naming-conventions}

Les nœuds dans le référentiel sont soumis aux conventions de dénomination de [Java Content Repository](/help/sites-developing/the-basics.md#java-content-repository). Toutefois, AEM impose d’autres conventions pour le nom des nœuds de page.

## Conventions de dénomination pour les pages {#naming-conventions-for-pages}

Ces conventions sont mises en place à différents niveaux :

* JcrUtil : implémentation AEM des [utilitaires JCR](#jcr-utilities).
* PageManager : le [Gestionnaire de pages](#page-manager) fournit des méthodes pour les opérations au niveau de la page.
* En fonction de l’IU utilisée :

   * [IU tactile standard](#standard-ui)
   * [IU classique](#classic-ui)

### Utilitaires JCR {#jcr-utilities}

[JcrUtil](https://helpx.adobe.com/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/index.html?com/day/cq/commons/jcr/JcrUtil.html) est l’implémentation AEM des utilitaires JCR. Les mappages de caractères contrôlés et les validations suivantes se révèlent particulièrement intéressants dans le cadre de la validation des noms :

* `isValidName`

   * Vérifie si le nom n’est pas vide et contient uniquement des caractères valides.
   * Peut être utilisé pour vérifier la validité d’un nom proposé.

* `createValidName`

   * Crée un libellé valide à partir d’une chaîne arbitraire.
   * Peut être utilisé pour créer un nom à partir d’un titre.

### Gestionnaire de pages {#page-manager}

[PageManager](https://helpx.adobe.com/fr/experience-manager/6-5/sites/developing/using/reference-materials/javadoc/com/day/cq/wcm/api/PageManager.html) fournit des méthodes pour les opérations au niveau de la page, sur la base de [JCRUtil](#jcr-utilities).

### Interface utilisateur standard {#standard-ui}

L’interface utilisateur tactile standard :

* Valide le nom en fonction des restrictions imposées par PageManager dans l’une des situations suivantes :

   * Un titre de page est fourni pour la conversion dans le nom de nœud.
   * Un nom de nœud explicite est fourni.

### IU classique {#classic-ui}

L’IU classique applique des restrictions plus strictes :

* Valide le nom dans le cas d’un nom de nœud explicite dans l’une des situations suivantes :

   * Un titre de page est fourni pour la conversion dans le nom de nœud.
   * Un nom de nœud explicite est fourni.

* Caractères valides (seuls ces caractères sont effectivement valides lorsqu’une page est créée dans l’IU classique), même si `PageManagerImpl` autorise des caractères supplémentaires) :

   * « a » à « z »
   * « A » à « Z »
   * « 0 » à « 9 »
   * _ (trait de soulignement)
   * `-` (tiret/moins)

