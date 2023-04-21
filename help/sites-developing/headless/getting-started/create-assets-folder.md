---
title: Guide de démarrage rapide sur la création d’un dossier de ressources découplées
description: Utilisez des modèles de fragment de contenu AEM pour définir la structure des fragments de contenu, à la base de votre contenu découplé.
exl-id: 8d913056-fcfa-4cdd-b40a-771f13dfd0f4
source-git-commit: 7355c149500f9e5044c9ff78af208d36ee681f56
workflow-type: ht
source-wordcount: '379'
ht-degree: 100%

---

# Guide de démarrage rapide sur la création d’un dossier de ressources découplées {#creating-an-assets-folder}

Utilisez des modèles de fragment de contenu AEM pour définir la structure des fragments de contenu, à la base de votre contenu découplé. Ces fragments sont ensuite stockés dans des dossiers de ressources.

## Qu’est-ce qu’un dossier de ressources ?  {#what-is-an-assets-folder}

[Maintenant que vous avez créé des modèles de fragments de contenu](create-content-model.md) qui définissent la structure souhaitée pour vos futurs fragments de contenu, vous êtes probablement enthousiaste à l’idée d’en créer.

Cependant, vous devez d’abord créer un dossier de ressources pour les stocker.

Les dossiers de ressources servent à [organiser les ressources de contenu traditionnelles](/help/assets/manage-assets.md), comme les images et les vidéos, mais aussi les fragments de contenu.

## Comment créer un dossier de ressources {#how-to-create-an-assets-folder}

Un administrateur n’a besoin de créer des dossiers qu’occasionnellement pour organiser le contenu au fur et à mesure de sa création. Pour les besoins de ce guide de prise en main, il suffit de créer un dossier.

1. Connectez-vous à AEM. Sélectionnez ensuite, dans le menu principal, **Navigation -> Ressources -> Fichiers**.
1. Appuyez ou cliquez sur **Créer -> Dossier**.
1. Indiquez un **titre** et un **nom** pour votre dossier.
   * Le **titre** doit être descriptif.
   * Le **Nom** devient le nom du nœud dans le référentiel.
      * Il sera généré automatiquement en fonction du titre et adapté selon les [conventions d’appellation AEM.](/help/sites-developing/naming-conventions.md)
      * Il peut être adapté si nécessaire.

   ![Créer un dossier](assets/assets-folder-create.png)
1. Sélectionnez le dossier que vous venez de créer, puis sélectionnez **Propriétés** dans la barre d’outils (ou utilisez le [raccourci clavier](/help/sites-authoring/keyboard-shortcuts.md) `p` ).
1. Dans la fenêtre **Propriétés**, sélectionnez l’onglet **Cloud Services**.
1. Pour la **configuration du cloud**, sélectionnez la[ configuration que vous avez créée précédemment.](create-configuration.md)

   ![Configurer le dossier de ressources](assets/assets-folder-configure.png)
1. Appuyez/cliquez sur **Enregistrer et fermer**.
1. Appuyez/cliquez sur **OK** dans la fenêtre de confirmation.

   ![Fenêtre de confirmation](assets/assets-folder-confirmation.png)

Vous pouvez créer des sous-dossiers supplémentaires dans le dossier que vous venez de créer. Les sous-dossiers hériteront de la **configuration du cloud** du dossier parent. Il est toutefois possible de modifier ce paramétrage si vous souhaitez utiliser les modèles d’une autre configuration.

Si vous utilisez une structure de site localisée, vous pouvez [créer une racine de langue](/help/assets/multilingual-assets.md) sous votre nouveau dossier.

## Étapes suivantes {#next-steps}

Maintenant que vous avez créé un dossier pour vos fragments de contenu, vous pouvez passer à la quatrième partie du guide de prise en main et [créer des fragments de contenu.](create-content-fragment.md)

>[!TIP]
>
>Pour plus d’informations sur la gestion des fragments de contenu, consultez la [documentation sur les fragments de contenu](/help/assets/content-fragments/content-fragments.md).
