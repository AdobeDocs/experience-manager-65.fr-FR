---
title: Conventions de dénomination pour le test des ressources
description: Les nœuds dans le référentiel sont soumis aux conventions de dénomination de Java Content Repository. Toutefois, Adobe Experience Manager impose d’autres conventions pour le nom des nœuds de ressource.
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: authoring
content-type: reference
exl-id: bb6a5913-0871-47c7-8641-936e98920ec0
solution: Experience Manager, Experience Manager Sites
feature: Authoring
role: User
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: c45915cf-e157-4af7-a80d-97b905bcb3a5
    internal-label: Experience Manager Sites
feature_v2:
  - id: e2c1b6d3-bb7e-4fe8-8c72-f7b403298e91
    internal-label: Authoring
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '130'
ht-degree: 100%
---
# Conventions de dénomination pour le test des ressources{#naming-conventions-for-assets-testing}

Les nœuds dans le référentiel sont soumis aux conventions de dénomination de [Java Content Repository](/help/sites-developing/the-basics.md#java-content-repository). Toutefois, Adobe Experience Manager impose d’autres conventions pour le nom des nœuds de ressource.

## Interface utilisateur classique {#classic-ui}

L’IU classique impose des restrictions plus strictes :

* Valide le nom de la ressource avec un nom de nœud explicite lorsque l’une des conditions suivantes se vérifie :

  * un titre de ressource est fourni pour une conversion en nom de nœud ;
  * un nom de nœud explicite est fourni.

* Caractères valides (seuls ces caractères sont réellement valides lors de la création d’une ressource dans l’interface utilisateur classique) :

  * « a » à « z »
  * « A » à « Z »
  * « 0 » à « 9 »
  * _ (trait de soulignement)
  * `-` (tiret/moins)
