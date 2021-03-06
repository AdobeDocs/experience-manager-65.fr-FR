---
title: Test d’une mise en page en responsive design dans We.Retail
seo-title: Test d’une mise en page en responsive design dans We.Retail
description: Test d’une mise en page en responsive design dans We.Retail
seo-description: 'null'
uuid: d9613655-f54e-458f-9175-d07bb868f58b
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: 2d374e88-ea09-43d5-986c-5d77b0705b93
exl-id: 6df5fb10-a7f1-4d5d-ac00-b4be3d5d3d18
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '254'
ht-degree: 75%

---

# Test d’une mise en page en responsive design dans We.Retail{#trying-out-responsive-layout-in-we-retail}

Toutes les pages We.Retail utilisent le composant Conteneur de mises en page pour implémenter la conception réactive. Le conteneur offre un système de paragraphe qui permet de positionner des composants sur une grille réactive. Cette grille peut réorganiser la mise en page en fonction de l’appareil/de la taille de fenêtre et du format. Le composant est utilisé conjointement avec le mode **Mise en page** de l’éditeur de page, ce qui vous permet de créer et de modifier votre mise en page réactive en fonction de l’appareil.

## Test {#trying-it-out}

1. Modifiez la page Arctic Surfing dans la section Experiences de la branche master de langue.

   http://localhost:4502/editor.html/content/we-retail/language-masters/en/experience/arctic-surfing-in-lofoten.html

1. Passez à **Aperçu** pour voir la page telle qu’elle serait affichée pour un internaute. Faites défiler vers le bas pour accéder au contenu de l’article *Aloha spirits in Norther Norway*.

   ![chlimage_1-178](assets/chlimage_1-178.png)

1. Redimensionnez la fenêtre de votre navigateur et observez la mise en page s’adapter dynamiquement au redimensionnement.

   ![chlimage_1-179](assets/chlimage_1-179.png)

1. Passez en mode Mise en page. La barre d’outils de l’émulateur est automatiquement affichée et vous permet de planifier votre mise en page par appareil ciblé.

   La sélection d’un composant affiche des options de flottement et de masquage dans le menu d’édition, ainsi que des poignées de redimensionnement pour le composant.

   ![chlimage_1-180](assets/chlimage_1-180.png)

1. En saisissant et en faisant glisser la poignée de redimensionnement du composant, la grille de mise en page s’affiche automatiquement pour vous assister lors du redimensionnement.

   ![chlimage_1-181](assets/chlimage_1-181.png)

## Informations supplémentaires {#further-information}

Pour plus d’informations, reportez-vous au document de création [Mise en page réactive](/help/sites-authoring/responsive-layout.md) ou au document administrateur [Configuration du conteneur de mises en page et du mode de mise en page](/help/sites-administering/configuring-responsive-layout.md) pour obtenir des détails techniques complets.
