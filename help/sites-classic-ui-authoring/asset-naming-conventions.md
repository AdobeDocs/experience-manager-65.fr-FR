---
title: Conventions de dénomination pour le test des ressources
seo-title: Conventions de dénomination des ressources
description: Les nœuds dans le référentiel sont soumis aux conventions de dénomination de Java Content Repository. Toutefois, Adobe Experience Manager impose d’autres conventions pour le nom des nœuds de ressource.
seo-description: Les nœuds dans le référentiel sont soumis aux conventions de dénomination de Java Content Repository. Toutefois, Adobe Experience Manager impose d’autres conventions pour le nom des nœuds de ressource.
uuid: 6b622a60-90e8-461e-9b67-42c11c7038f9
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: authoring
content-type: reference
discoiquuid: 55e66c66-0120-4ed4-94c5-d65a434bb59b
exl-id: bb6a5913-0871-47c7-8641-936e98920ec0
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '159'
ht-degree: 99%

---

# Conventions de dénomination des ressources testing{#naming-conventions-for-assets-testing}

Les nœuds dans le référentiel sont soumis aux conventions de dénomination de [Java Content Repository](/help/sites-developing/the-basics.md#java-content-repository). Toutefois, Adobe Experience Manager impose d’autres conventions pour le nom des nœuds de ressource.

## IU classique {#classic-ui}

L’IU classique applique des restrictions plus strictes :

* Valide le nom de ressource dans le cas d’un nom de nœud explicite lorsque :

   * un titre de ressource est fourni pour la conversion dans le nom de nœud
   * un nom de nœud explicite est fourni

* Caractères valides (seuls ces caractères sont effectivement valides lorsqu’une ressource est créée dans l’IU classique) :

   * « a » à « z »
   * « A » à « Z »
   * « 0 » à « 9 »
   * _ (trait de soulignement)
   * `-` (tiret/moins)
