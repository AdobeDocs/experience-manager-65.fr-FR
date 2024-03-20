---
title: Test des modèles modifiables dans We.Retail
description: Découvrez comment tester des modèles modifiables dans Adobe Experience Manager à l’aide de We.Retail.
contentOwner: User
products: SG_EXPERIENCEMANAGER/6.5/SITES
content-type: reference
topic-tags: best-practices
exl-id: efebe66d-3d30-4033-9c4c-ae347e134f2f
solution: Experience Manager, Experience Manager Sites
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '467'
ht-degree: 82%

---

# Test des modèles modifiables dans We.Retail{#trying-out-editable-templates-in-we-retail}

Grâce aux modèles modifiables, la création et la maintenance de modèles ne sont plus des tâches réservées à l’équipe de développement. Un type d’utilisateur ou d’utilisatrice avancé, appelé auteur ou autrice de modèles, peut également créer des modèles. L’équipe de développement doit encore configurer l’environnement, créer des bibliothèques clientes et créer les composants à utiliser. Cependant, une fois ces bases en place, l’auteur de modèles peut créer et configurer des modèles sans projet de développement.

Toutes les pages de We.Retail sont basées sur des modèles modifiables, ce qui permet aux personnes non développeuses d’adapter et de personnaliser les modèles.

## Essayer de le faire {#trying-it-out}

1. Modifiez la page Matériel de la branche principale de langue.

   http://localhost:4502/editor.html/content/we-retail/language-masters/en/equipment.html

1. Le sélecteur de mode ne propose plus de mode Conception. Toutes les pages de We.Retail sont basées sur des modèles modifiables et la conception de modèles modifiables doit être modifiée dans l’éditeur de modèles.
1. Dans le menu **Informations sur la page**, sélectionnez **Éditer le modèle**.
1. Vous êtes en train de modifier le modèle Page principale.

   Le mode Structure de la page permet de modifier la structure du modèle. Cela inclut, par exemple, les composants autorisés dans le conteneur de mises en page.

   ![chlimage_1-138](assets/chlimage_1-138.png)

1. Configurez les politiques du conteneur de dispositions pour définir les composants autorisés dans le conteneur.

   Les politiques sont l’équivalent des configurations de conception.

   ![chlimage_1-139](assets/chlimage_1-139.png)

1. Dans la boîte de dialogue de conception du conteneur de dispositions, vous pouvez :

   * Sélectionner une stratégie existante ou créer une stratégie pour le conteneur
   * Sélectionner les composants autorisés dans le conteneur
   * Définir les composants par défaut à placer lorsque vous faites glisser une ressource dans le conteneur

   ![chlimage_1-140](assets/chlimage_1-140.png)

1. De retour dans l’éditeur de modèles, vous pouvez modifier la politique du composant de texte dans le conteneur de dispositions.

   Vous pouvez ainsi :

   * Sélectionner une stratégie existante ou créer une stratégie pour le conteneur
   * Définir les fonctionnalités disponibles pour l’auteur ou l’autrice de la page lors de l’utilisation de ce composant, telles que :

      * Sources de collage autorisées
      * Options de mise en forme
      * Styles de paragraphe autorisés
      * Caractères spéciaux autorisés

   De nombreux composants basés sur les composants principaux permettent de configurer des options au niveau du composant par le biais de modèles modifiables, ce qui évite aux développeurs et développeuses de devoir les personnaliser.

   ![chlimage_1-141](assets/chlimage_1-141.png)

1. De retour dans l’éditeur de modèles, vous pouvez utiliser le sélecteur de modes pour passer en mode **Contenu initial** et définir le contenu requis sur la page.

   Le mode **Disposition** peut être utilisé tel quel sur une page normale pour définir la disposition du modèle.

## Informations supplémentaires {#more-information}

Pour plus d’informations, voir le document de création [Création de modèles de page](/help/sites-authoring/templates.md) ou la page du document de développement [Modèles - Modifiables](/help/sites-developing/page-templates-editable.md) pour obtenir des détails techniques complets sur les modèles modifiables.

Vous pouvez également vous renseigner sur les [composants principaux](/help/sites-developing/we-retail-core-components.md). Consultez le document de création de [Composants principaux](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/introduction.html?lang=fr) pour obtenir un aperçu des fonctionnalités des composants principaux ou [Développement de composants principaux](https://helpx.adobe.com/fr/experience-manager/core-components/using/developing.html) pour une présentation technique.
