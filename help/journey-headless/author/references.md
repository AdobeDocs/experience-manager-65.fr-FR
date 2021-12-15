---
title: En savoir plus sur l’utilisation de références dans les fragments de contenu
description: Découvrez comment utiliser des références dans des fragments de contenu pour du contenu, d’autres fragments et d’autres ressources (médias). Introduisez la nécessité et la mécanique des fragments imbriqués pour la création CMS sans affichage.
index: true
hide: false
hidefromtoc: false
source-git-commit: 9661061a98c31fbb74bd0716dbedc7abef298f44
workflow-type: tm+mt
source-wordcount: '731'
ht-degree: 10%

---

# En savoir plus sur l’utilisation de références dans les fragments de contenu {#author-headless-references}

## L&#39;histoire jusqu&#39;à présent {#story-so-far}

Au début du [AEM Parcours de création de contenu sans affichage](overview.md) la valeur [Introduction](introduction.md) couvrait les concepts de base et la terminologie relatifs à la création pour les sans-tête.

Vous avez appris les principes de base de la création CMS sans affichage avec une introduction à la création avec AEMaaCS, et en particulier à la création de fragments de contenu.

Cet article s’appuie sur ces éléments afin que vous compreniez comment utiliser des références pour créer votre propre contenu pour votre projet AEM sans interface.

## Objectif {#objective}

* **Audience** : Niveau avancé
* **Objectif**: Introduisez l’utilisation de références pour la création CMS sans affichage. Quels types de références sont disponibles et à quelles fins :

   * Références du contenu
   * Références de ressources/médias
   * Références à un fragment
   * Références ad hoc depuis un bloc de texte

## Références {#what-are-references}

Les références sont simplement un mécanisme de connexion de vos ressources, qu’il s’agisse d’autres contenus, ressources (comme dans les images) ou autres fragments. Bien que très similaire, il existe des différences.

Certaines références comportent des types de données dédiés (par exemple, Références de contenu et Références de fragment), tandis que d’autres sont simplement ajoutées comme référence dans un bloc de texte (références de ressources et références ad hoc).

![Fragments de contenu - Références](/help/journey-headless/author/assets/headless-journey-author-references-01.png)

## Références du contenu {#content-references}

C’est exactement ce que font les références de contenu : elles vous permettent de référencer tout autre contenu. Un navigateur s’ouvre, vous permettant de sélectionner l’élément de contenu.

## Références de ressources/médias {#assets-media-references}

Les ressources (images ou médias, par exemple) peuvent être référencées dans un bloc de texte à l’aide de la fonction **Insérer une ressource** . Un navigateur s’ouvre alors pour vous permettre de sélectionner la ressource.

![Fragments de contenu - Insérer une ressource](/help/journey-headless/author/assets/headless-journey-author-references-02.png)

## Références à un fragment {#fragment-references}

Encore une fois, les Références de fragment font exactement cela : elles vous permettent de référencer un autre fragment. La raison pour laquelle cela est important nécessite un peu plus d&#39;explications.

Par exemple, les modèles de fragment de contenu suivants peuvent être définis :

* Ville
* Société
* Personne
* Distinctions

Cela semble assez simple, mais bien sûr, une entreprise a à la fois un PDG et des employés....et ce sont tous des gens, chacun défini comme une Personne.

Et une Personne peut recevoir un Prix (ou peut-être deux).

* Mon entreprise - Société
   * PDG - Personne
   * Employé(s) - Personne
      * Prix(s) personnel(s) - Prix

Et c&#39;est juste pour commencer. En fonction de la complexité, une récompense peut être propre à une entreprise ou son siège social dans une ville donnée.

Vous pouvez représenter ces interrelations à l’aide des Références de fragment, car elles sont comprises à la fois par vous (l’auteur) et par les applications sans tête.

En tant qu’auteur, vous n’êtes pas responsable de la définition de ces relations (c’est l’architecte de contenu qui définit ces relations lors de la création du modèle de fragment de contenu), mais vous devez savoir comment reconnaître et modifier les références.

### Création de fragments imbriqués {#author-nested-fragment}

La création de références de fragments est assez simple (bien que le champ ne soit généralement pas étiqueté comme **Référence de fragment**). Vous pouvez saisir directement la référence ou (plus probablement) sélectionner l’icône de dossier pour ouvrir un navigateur qui vous permet de naviguer et de sélectionner le fragment dont vous avez besoin.

![Fragments de contenu - Références](/help/journey-headless/author/assets/headless-journey-author-references-03.png)

La définition du modèle de fragment de contenu contrôle :

* si vous pouvez choisir d’ajouter plusieurs références ;
* les types de modèles de fragments de contenu que vous pouvez sélectionner ; Le modèle de fragment de contenu définit les modèles de fragment autorisés pour la référence. AEM présente donc uniquement les fragments basés sur ces modèles.

### Navigation dans les fragments imbriqués {#navigate-nested-fragment}

En utilisant la variable **Arborescence de structure** de l’éditeur de fragment de contenu, vous pouvez parcourir les fragments référencés par votre fragment, puis parcourir toutes les références qu’ils peuvent contenir. La sélection d’une référence ouvre ce fragment en vue de le modifier.

>[!NOTE]
>
>À l’aide des chemins de navigation du panneau principal, vous pouvez revenir à votre point de départ.

![Arborescence de la structure du fragment de contenu](/help/assets/content-fragments/assets/cfm-structuretree-02.png)

## Références ad hoc {#adhoc-references}

Les références ad hoc peuvent être ajoutées sous la forme d’un lien simple dans un bloc de texte :

![Fragments de contenu - Références ad hoc](/help/journey-headless/author/assets/headless-journey-author-references-04.png)

## Et après ? {#whats-next}

Maintenant que vous en savez plus sur les références et la structure dans les fragments de contenu, l’étape suivante consiste à [En savoir plus sur les métadonnées et le balisage](metadata-tagging.md). Cette section présente et discute de la manière dont vous pouvez définir des métadonnées et des balises pour vos fragments de contenu.

## Ressources supplémentaires {#additional-resources}

* [Utilisation de fragments de contenu](/help/assets/content-fragments/content-fragments.md)

   * [Gestion des fragments de contenu](/help/assets/content-fragments/content-fragments-managing.md)

      * [Application de la configuration à votre dossier de ressources](/help/assets/content-fragments/content-fragments-configuration-browser.md#apply-the-configuration-to-your-assets-folder)

      * [Création d’un fragment de contenu](/help/assets/content-fragments/content-fragments-managing.md#creating-a-content-fragment)
   * [Variations - création de fragments de contenu](/help/assets/content-fragments/content-fragments-variations.md)

   * [Modèles de fragment de contenu](/help/assets/content-fragments/content-fragments-models.md)

      * [Modèles de fragment de contenu - Types de données](/help/assets/content-fragments/content-fragments-models.md#data-types)

      * [Modèles de fragment de contenu - Propriétés](/help/assets/content-fragments/content-fragments-models.md#properties)


* Guides de prise en main
   * [Guide de démarrage rapide sur la création d’un dossier de ressources découplées](/help/sites-developing/headless/getting-started/create-assets-folder.md)

* [AEM Parcours d’architecture de contenu sans affichage](/help/journey-headless/architect/overview.md)

* [AEM Parcours de traduction sans affichage](/help/journey-headless/translation/overview.md)
