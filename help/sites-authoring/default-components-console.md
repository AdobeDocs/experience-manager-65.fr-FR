---
title: Console des composants
seo-title: Console des composants
description: Console des composants
seo-description: 'null'
uuid: a4e34d81-7875-4e26-8b48-4473e2905c37
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: page-authoring
content-type: reference
discoiquuid: b657f95d-7be3-4409-a31b-d47fb2bfa550
docset: aem65
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '265'
ht-degree: 97%

---


# Console des composants{#components-console}

La console des composants vous permet de parcourir tous les composants définis pour votre instance et d’afficher les informations clés pour chacun d’eux.

Elle est accessible via **Outils** -> **Général** -> **Composants**. Dans la console, les modes Carte et Liste sont disponibles. Comme il n’existe pas de structure d’arborescence pour les composants, le mode Colonnes n’est pas disponible.

![capture d&#39;écran_2019-03-05at113145](assets/screen-shot_2019-03-05at113145.png)

>[!NOTE]
>
>La console des composants affiche tous les composants du système. L’[Explorateur de composants](/help/sites-authoring/author-environment-tools.md#components-browser) affiche les composants qui sont disponibles pour les auteurs et masque tous les groupes de composants qui commencent par un point ( `.`).

## Recherche {#searching}

Avec l’icône **Contenu uniquement** (en haut à gauche), vous pouvez ouvrir le panneau de **recherche** pour rechercher et/ou filtrer les composants :

![screen-shot_2019-03-05at113251](assets/screen-shot_2019-03-05at113251.png)

### Détails des composants {#component-details}

Pour afficher les détails correspondant à un composant spécifique, appuyez/cliquez sur la ressource requise. Trois onglets fournissent :

* **Propriétés**

   ![screen_shot_2018-03-27at165847](assets/screen_shot_2018-03-27at165847.png)

   L’onglet Propriétés vous permet d’effectuer les opérations suivantes :

   * Afficher les propriétés générales du composant.
   * Observez comment l’[icône ou l’abréviation a été définie](/help/sites-developing/components-basics.md#component-icon-in-touch-ui) pour le composant.

      * Cliquez sur la source de l’icône pour accéder à ce composant.
   * Affichez le **Type de ressource** et le **Type de super-ressource** (s’il est défini) du composant.

      * Cliquez sur le type de super-ressource pour accéder à ce composant.
   >[!NOTE]
   >
   >Étant donné que les `/apps` ne sont pas modifiables à l’exécution, la console Composants est en lecture seule.

* **Stratégies**

   ![chlimage_1-169](assets/chlimage_1-169.png)

* **Utilisation en direct**

   ![chlimage_1-170](assets/chlimage_1-170.png)

   >[!CAUTION]
   >
   >En raison de la nature des informations collectées pour cette vue, la collecte/l’affichage de ces informations peut nécessiter un certain temps.

* **Documentation**

   Si le développeur a fourni la [documentation du composant](/help/sites-developing/developing-components.md#documenting-your-component), elle apparaîtra dans l’onglet **Documentation**. Si aucune documentation n’est disponible, l’onglet **Documentation** n’est pas affiché.

   ![chlimage_1-171](assets/chlimage_1-171.png)

