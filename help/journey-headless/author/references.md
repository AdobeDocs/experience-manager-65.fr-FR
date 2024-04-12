---
title: En savoir plus sur l’utilisation de références dans les fragments de contenu
description: Découvrez comment utiliser des références dans des fragments de contenu pour du contenu, d’autres fragments et d’autres ressources (médias). Découvrez l’importance et le fonctionnement des fragments imbriqués pour la création CMS découplée.
exl-id: d54a0a40-a8af-456a-9bf5-219d84540c97
solution: Experience Manager, Experience Manager Sites
feature: Headless,Content Fragments
role: Admin, Architect,Data Architect,Developer,User,Leader
source-git-commit: 9a3008553b8091b66c72e0b6c317573b235eee24
workflow-type: tm+mt
source-wordcount: '722'
ht-degree: 100%

---

# En savoir plus sur l’utilisation de références dans les fragments de contenu {#author-headless-references}

## Un peu d’histoire… {#story-so-far}

Au début du [Parcours de création de contenu découplé AEM](overview.md), l’[Introduction](introduction.md) présentait les concepts de base et la terminologie relatifs à la création découplée.

Vous avez appris les principes de base de la création CMS découplée grâce à une introduction à la création avec AEMaaCS et en particulier à la création de fragments de contenu.

Cet article s’appuie sur ces éléments afin que vous compreniez comment utiliser des références pour créer votre propre contenu pour votre projet AEM découplé.

## Objectif {#objective}

* **Audience** : Niveau avancé
* **Objectif** : découvrez l’utilisation de références pour la création CMS découplée. Quels types de références sont disponibles et à quelles fins :

   * Références du contenu
   * Références de ressources/médias
   * Références à un fragment
   * Références ad hoc depuis un bloc de texte

## Que sont les références {#what-are-references}

Les références sont simplement un mécanisme de connexion de vos ressources, qu’il s’agisse d’autres contenus, ressources (comme dans les images) ou autres fragments. Bien que très similaires, il existe des différences.

Certaines références comportent des types de données dédiés (par exemple, Références de contenu et Références de fragment), tandis que d’autres sont simplement ajoutées comme référence dans un bloc de texte (références de ressources et références ad hoc).

![Fragments de contenu – Références](/help/journey-headless/author/assets/headless-journey-author-references-01.png)

## Références du contenu {#content-references}

Leur nom est clair : les références de contenu vous permettent de faire référence à tout autre contenu. Un navigateur s’ouvre, vous permettant de sélectionner l’élément de contenu.

## Références de ressources/médias {#assets-media-references}

Les ressources (images ou médias, par exemple) peuvent être référencées dans un bloc de texte à l’aide de l’option **Insérer une ressource**. Un navigateur s’ouvre, vous permettant de sélectionner la ressource.

![Fragments de contenu – Insérer une ressource](/help/journey-headless/author/assets/headless-journey-author-references-02.png)

## Références à un fragment {#fragment-references}

Encore une fois, les références de fragment font exactement ce que leur nom suggère : elles vous permettent de faire référence à un autre fragment. La raison pour laquelle il est important d’insister sur ce fait nécessite un peu plus d’explications.

Par exemple, les modèles de fragment de contenu suivants peuvent être définis :

* Ville
* Entreprise
* Personne
* Distinctions

Cela semble évident, mais une entreprise compte à la fois un ou une PDG et des employées et employés…Et chaque élément d’entre eux est défini en tant que personne.

Et une personne peut recevoir une distinction (ou peut-être deux).

* Mon entreprise – Société
   * PDG – Personne
   * Employé(s) – Personne
      * Récompense(s) personnelle(s) – Distinction

Voilà pour commencer. En fonction du niveau de complexité, une distinction peut être propre à une entreprise, ou le siège social d’une entreprise peut être situé dans une ville donnée.

Vous pouvez représenter ces interconnexions à l’aide de références de fragments, car ils peuvent être compris à la fois par vous (l’auteur) et par les applications découplées.

En tant qu’auteur, vous n’êtes pas responsable de la définition de ces relations (l’architecte de contenu les définit lors de la création du modèle de fragment de contenu), mais vous devez savoir comment reconnaître et modifier les références.

### Création de fragments imbriqués {#author-nested-fragment}

La création de références de fragments est assez simple (bien que le champ ne soit généralement pas étiqueté comme **Référence de fragment**). Vous pouvez saisir directement la référence ou (plus couramment) sélectionner l’icône de dossier pour ouvrir un navigateur qui vous permet d’accéder au fragment dont vous avez besoin et de le sélectionner.

![Fragments de contenu – Références](/help/journey-headless/author/assets/headless-journey-author-references-03.png)

La définition du modèle de fragment de contenu contrôle :

* si vous pouvez choisir d’ajouter plusieurs références ;
* les types de modèles de fragments de contenu que vous pouvez sélectionner. Le modèle de fragment de contenu définit les modèles de fragment autorisés comme référence. AEM présente donc uniquement les fragments basés sur ces modèles.

### Navigation dans les fragments imbriqués {#navigate-nested-fragment}

En utilisant la variable **Arborescence de la structure** de l’éditeur de fragment de contenu, vous pouvez parcourir les fragments référencés par votre fragment, puis parcourir toutes les références qu’ils peuvent contenir. La sélection d’une référence ouvre ce fragment en vue de le modifier.

>[!NOTE]
>
>À l’aide des chemins de navigation du panneau principal, vous pouvez revenir à votre point de départ.

![Arborescence de la structure du fragment de contenu.](/help/assets/content-fragments/assets/cfm-structuretree-02.png)

## Références ad hoc {#adhoc-references}

Les références ad hoc peuvent être ajoutées sous la forme d’un simple lien dans un bloc de texte :

![Fragments de contenu – Références ad hoc](/help/journey-headless/author/assets/headless-journey-author-references-04.png)

## Prochaines étapes {#whats-next}

Maintenant que vous en savez plus sur les références et la structure dans les fragments de contenu, l’étape suivante consiste à [en savoir plus sur les métadonnées et le balisage](metadata-tagging.md). Cette section présente et discute de la manière dont vous pouvez définir des métadonnées et des balises pour vos fragments de contenu.

## Ressources supplémentaires {#additional-resources}

* [Utilisation de fragments de contenu](/help/assets/content-fragments/content-fragments.md)

   * [Gestion des fragments de contenu](/help/assets/content-fragments/content-fragments-managing.md)

      * [Application de la configuration à votre dossier de ressources](/help/assets/content-fragments/content-fragments-configuration-browser.md#apply-the-configuration-to-your-assets-folder)

      * [Création d’un fragment de contenu](/help/assets/content-fragments/content-fragments-managing.md#creating-a-content-fragment)

   * [Variations – Création de fragments de contenu](/help/assets/content-fragments/content-fragments-variations.md)

   * [Modèles de fragment de contenu](/help/assets/content-fragments/content-fragments-models.md)

      * [Modèles de fragment de contenu – Types de données](/help/assets/content-fragments/content-fragments-models.md#data-types)

      * [Modèles de fragment de contenu – Propriétés](/help/assets/content-fragments/content-fragments-models.md#properties)

* Guides de prise en main
   * [Guide de démarrage rapide sur la création d’un dossier de ressources découplées](/help/sites-developing/headless/getting-started/create-assets-folder.md)

* [Parcours d’architecture de contenu découplé AEM](/help/journey-headless/architect/overview.md)

* [Parcours de traduction découplée AEM](/help/journey-headless/translation/overview.md)
