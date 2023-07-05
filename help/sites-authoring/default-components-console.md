---
title: Console des composants
seo-title: Components Console
description: Console des composants
seo-description: null
uuid: a4e34d81-7875-4e26-8b48-4473e2905c37
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: page-authoring
content-type: reference
discoiquuid: b657f95d-7be3-4409-a31b-d47fb2bfa550
docset: aem65
exl-id: d79107b9-dfa4-4e80-870e-0b7ea72f0bc7
source-git-commit: e85aacd45a2bbc38f10d03915e68286f0a55364e
workflow-type: tm+mt
source-wordcount: '263'
ht-degree: 61%

---

# Console des composants{#components-console}

La console Composants vous permet de parcourir tous les composants définis pour votre instance et d’afficher les informations clés de chaque composant.

Elle est accessible via **Outils** -> **Général** -> **Composants**. Dans la console, les vues Carte et Liste sont disponibles. Comme il n’existe pas de structure d’arborescence pour les composants, le mode Colonnes n’est pas disponible.

![screen-shot_2019-03-05at113145](assets/screen-shot_2019-03-05at113145.png)

>[!NOTE]
>
>La console des composants affiche tous les composants du système. L’[Explorateur de composants](/help/sites-authoring/author-environment-tools.md#components-browser) affiche les composants qui sont disponibles pour les auteurs et masque tous les groupes de composants qui commencent par un point (`.`).

## Rechercher {#searching}

Avec l’icône **Contenu uniquement** (en haut à gauche), vous pouvez ouvrir le panneau de **recherche** pour rechercher et/ou filtrer les composants :

![screen-shot_2019-03-05at113251](assets/screen-shot_2019-03-05at113251.png)

### Détails des composants {#component-details}

Pour afficher des détails sur un composant spécifique, appuyez/cliquez sur la ressource requise. Trois onglets sont proposés :

* **Propriétés**

  ![screen_shot_2018-03-27at165847](assets/screen_shot_2018-03-27at165847.png)

  L’onglet Propriétés vous permet d’effectuer les opérations suivantes :

   * Afficher les propriétés générales du composant.
   * Afficher le mode de [une icône ou une abréviation a été définie.](/help/sites-developing/components-basics.md#component-icon-in-touch-ui) pour le composant.

      * Cliquez sur la source de l’icône pour accéder à ce composant.

   * Afficher la variable **Type de ressource** et **Resource Super Type** (s’il est défini) pour le composant.

      * Cliquez sur le type de super-ressource pour accéder à ce composant.

  >[!NOTE]
  >
  >Étant donné que les `/apps` ne sont pas modifiables à l’exécution, la console Composants est en lecture seule.

* **Politiques**

  ![Politiques](assets/chlimage_1-169.png)

* **Utilisation en direct**

  ![Utilisation en direct](assets/chlimage_1-170.png)

  >[!CAUTION]
  >
  >En raison de la nature des informations collectées pour cette vue, la collecte/l’affichage de ces informations peut nécessiter un certain temps.

* **Documentation**

  Si le développeur a fourni [documentation du composant](/help/sites-developing/developing-components.md#documenting-your-component), il apparaîtra sur le **Documentation** . Si aucune documentation n’est disponible, l’onglet **Documentation** n’est pas affiché.

  ![Documentation](assets/chlimage_1-171.png)
