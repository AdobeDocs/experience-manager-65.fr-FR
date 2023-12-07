---
title: Conventions de dénomination pour le test des ressources
description: Les nœuds dans le référentiel sont soumis aux conventions de dénomination de Java Content Repository. Toutefois, Adobe Experience Manager impose d’autres conventions pour le nom des nœuds de ressource.
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: authoring
content-type: reference
exl-id: bb6a5913-0871-47c7-8641-936e98920ec0
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '131'
ht-degree: 69%

---

# Conventions de dénomination pour le test des ressources{#naming-conventions-for-assets-testing}

Les nœuds dans le référentiel sont soumis aux conventions de dénomination de [Java Content Repository](/help/sites-developing/the-basics.md#java-content-repository). Toutefois, Adobe Experience Manager impose d’autres conventions pour le nom des nœuds de ressource.

## Interface utilisateur classique {#classic-ui}

L’IU classique impose des restrictions plus strictes :

* Valide le nom de la ressource lorsqu’un nom de noeud explicite est utilisé dans l’une des situations suivantes :

   * un titre de ressource est fourni pour la conversion dans le nom de noeud.
   * un nom de nœud explicite est fourni.

* Caractères valides (seuls ces caractères sont réellement valides lors de la création d’une ressource dans l’interface utilisateur classique) :

   * « a » à « z »
   * « A » à « Z »
   * « 0 » à « 9 »
   * _ (trait de soulignement)
   * `-` (tiret/moins)
