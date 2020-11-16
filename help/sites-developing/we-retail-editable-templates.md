---
title: Test des modèles modifiables dans We.Retail
seo-title: Test des modèles modifiables dans We.Retail
description: 'null'
seo-description: 'null'
uuid: 0d4b97cb-efcc-4312-a783-eae3ecd6f889
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
discoiquuid: 3cc8ac23-98ff-449f-bd76-1203c7cbbed7
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '485'
ht-degree: 86%

---


# Test des modèles modifiables dans We.Retail{#trying-out-editable-templates-in-we-retail}

Grâce aux modèles modifiables, les tâches de création et de gestion des modèles ne sont plus réservées aux seuls développeurs. Un type d’utilisateur expérimenté, appelé créateur (ou auteur) de modèles, peut également créer des modèles. Les développeurs doivent encore configurer l’environnement, créer des bibliothèques clientes et créer les composants à utiliser. Cependant, une fois ces bases en place, l’auteur de modèles peut créer et configurer des modèles sans projet de développement.

Toutes les pages We.Retail reposent sur des modèles modifiables, ce qui permet aux non-développeurs d’adapter et de personnaliser les modèles.

## Test {#trying-it-out}

1. Modifiez la page Équipement de la branche principale de langue.

   http://localhost:4502/editor.html/content/we-retail/language-masters/en/equipment.html

1. Notez que le sélecteur de mode ne propose plus de mode Conception. Toutes les pages de We.Retail reposent sur des modèles modifiables. Pour modifier la conception de ces modèles, vous devez recourir à l’éditeur de modèles.
1. From the **Page information** menu select **Edit Template**.
1. Vous modifiez à présent le modèle « Page de modèle ».

   Le mode de structure de la page vous permet de modifier la structure du modèle. Cela comprend, par exemple, les composants qui sont autorisés dans le conteneur de mises en page.

   ![chlimage_1-138](assets/chlimage_1-138.png)

1. Configurez les stratégies du conteneur de mises en page pour définir les composant autorisés dans le conteneur.

   Les stratégies correspondent aux configurations de conception.

   ![chlimage_1-139](assets/chlimage_1-139.png)

1. Dans la boîte de dialogue de conception du conteneur de mises en page, vous pouvez effectuer les opérations suivantes :

   * Sélectionner une stratégie existante ou en créer une nouvelle pour le conteneur.
   * Sélectionner les composants autorisés dans le conteneur.
   * Définir les composants par défaut à placer lorsqu’une ressource est déplacée dans le conteneur.

   ![chlimage_1-140](assets/chlimage_1-140.png)

1. De retour dans l’éditeur de modèles, vous pouvez modifier la stratégie du composant de texte dans le conteneur de mises en page.

   Ce permet d’effectuer les opérations suivantes :

   * Sélectionner une stratégie existante ou en créer une nouvelle pour le conteneur.
   * Définir les fonctionnalités dont dispose le créateur de la page lorsqu’il utilise ce composant :

      * Sources de collage autorisées
      * Options de mise en forme
      * Styles de paragraphe autorisés
      * Caractères spéciaux autorisés

   De nombreux composants basés sur les composants principaux permettent de configurer des options au niveau du composant par le biais de modèles modifiables, rendant ainsi inutile toute personnalisation de la part des développeurs.

   ![chlimage_1-141](assets/chlimage_1-141.png)

1. De retour dans l’éditeur de modèles, vous pouvez utiliser le sélecteur de mode pour passer en mode **Contenu initial** et définir ainsi le contenu requis sur la page.

   Le mode **Disposition** peut être utilisé tel quel sur une page normale pour définir la mise en page du modèle.

## Informations supplémentaires {#more-information}

For further information please refer to the authoring document [Creating Page Templates](/help/sites-authoring/templates.md) or the developer document Page [Templates - Editable](/help/sites-developing/page-templates-editable.md) for complete technical details on editable templates.

Vous pouvez également vous renseigner sur les [composants principaux](/help/sites-developing/we-retail-core-components.md). See the authoring document [Core Components](https://docs.adobe.com/content/help/fr-FR/experience-manager-core-components/using/introduction.html) for an overview of the capabilities of the core components and the developer document [Developing Core Components](https://helpx.adobe.com/experience-manager/core-components/using/developing.html) for a technical overview.

