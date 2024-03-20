---
title: Test d’une mise en page en responsive design dans We.Retail
description: Découvrez comment tester la mise en page réactive dans Adobe Experience Manager à l’aide de We.Retail.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
exl-id: 6df5fb10-a7f1-4d5d-ac00-b4be3d5d3d18
solution: Experience Manager, Experience Manager Sites
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '247'
ht-degree: 85%

---

# Test d’une mise en page en responsive design dans We.Retail{#trying-out-responsive-layout-in-we-retail}

Toutes les pages We.Retail utilisent le composant conteneur de mise en page pour implémenter le responsive design. Le conteneur offre un système de paragraphe qui permet de positionner des composants sur une grille réactive. Cette grille peut réorganiser la disposition en fonction de la taille et du format de la fenêtre/l’appareil. Le composant est utilisé en mode **Disposition** de l’éditeur de page, ce qui permet de créer et de modifier une mise en page en mode responsive design, selon les caractéristiques de l’appareil.

## Essayer de le faire {#trying-it-out}

1. Modifiez la page Surf en Arctique dans la section Expériences de la branche principale de langue.

   http://localhost:4502/editor.html/content/we-retail/language-masters/en/experience/arctic-surfing-in-lofoten.html

1. Passez à **Aperçu** pour voir la page telle qu’elle serait affichée pour un internaute. Faites défiler jusqu’au contenu de l’article *Esprit Aloha dans le nord de la Norvège*.

   ![chlimage_1-178](assets/chlimage_1-178.png)

1. Redimensionnez la fenêtre de votre navigateur et observez la mise en page s’adapter dynamiquement au redimensionnement.

   ![chlimage_1-179](assets/chlimage_1-179.png)

1. Passez en mode Mise en page. La barre d’outils de l’émulateur s’affiche automatiquement, ce qui vous permet de planifier votre disposition par appareil ciblé.

   La sélection d’un composant affiche des options de flottement et de masquage dans le menu d’édition, ainsi que des poignées de redimensionnement pour le composant.

   ![chlimage_1-180](assets/chlimage_1-180.png)

1. En saisissant et en faisant glisser la poignée de redimensionnement du composant, la grille de mise en page s’affiche automatiquement pour vous assister lors du redimensionnement.

   ![chlimage_1-181](assets/chlimage_1-181.png)

## Informations supplémentaires {#further-information}

Pour plus d’informations, voir le document de création [Mise en page réactive](/help/sites-authoring/responsive-layout.md) ou le document administrateur [Configuration du conteneur de mises en page et du mode Mise en page](/help/sites-administering/configuring-responsive-layout.md) pour obtenir des informations techniques complètes.
