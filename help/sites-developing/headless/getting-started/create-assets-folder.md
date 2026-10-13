---
title: Guide de démarrage rapide sur la création d’un dossier de ressources découplées
description: Utilisez des modèles de fragment de contenu AEM pour définir la structure des fragments de contenu, à la base de votre contenu découplé.
exl-id: 8d913056-fcfa-4cdd-b40a-771f13dfd0f4
solution: Experience Manager, Experience Manager Sites
feature: Headless,Content Fragments,GraphQL,Persisted Queries,Developing
role: Admin,Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: c45915cf-e157-4af7-a80d-97b905bcb3a5
    internal-label: Experience Manager Sites
feature_v2:
  - id: bfd4bc52-c397-5127-8f86-8953ba9fc0a3
    internal-label: Headless
  - id: c5d917df-d8bd-5e97-a117-6dde1e9f7103
    internal-label: Developing
  - id: a642c50e-80eb-4fc1-a5d2-f3762d1f841d
    internal-label: Administration
  - id: d429a63e-ade4-4117-b04e-9b996d1c94ef
    internal-label: Integrations
  - id: c124fa01-25c5-42ec-adf6-21d1c114058b
    internal-label: Developer tools
subfeature_v2:
  - id: e9db7c79-8f65-4281-a439-c9049296d903
    internal-label: Content Fragments
  - id: a02b73a7-bdfc-4225-bdfd-69f7891ab55e
    internal-label: GraphQL
  - id: d781bc8f-52af-43f6-84d0-b73e59a130d5
    internal-label: Persisted queries
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '369'
ht-degree: 97%
---
# Guide de démarrage rapide sur la création d’un dossier de ressources découplées {#creating-an-assets-folder}

Utilisez des modèles de fragment de contenu AEM pour définir la structure des fragments de contenu, à la base de votre contenu découplé. Ces fragments sont ensuite stockés dans des dossiers de ressources.

## Qu’est-ce qu’un dossier de ressources ? {#what-is-an-assets-folder}

[Maintenant que vous avez créé des modèles de fragments de contenu](create-content-model.md) qui définissent la structure souhaitée pour vos futurs fragments de contenu, vous êtes probablement enthousiaste à l’idée d’en créer.

Cependant, vous devez d’abord créer un dossier de ressources pour les stocker.

Les dossiers de ressources servent à [organiser les ressources de contenu traditionnelles](/help/assets/manage-assets.md), comme les images et les vidéos, mais aussi les fragments de contenu.

## Comment créer un dossier de ressources {#how-to-create-an-assets-folder}

Un administrateur n’a besoin de créer des dossiers qu’occasionnellement pour organiser le contenu au fur et à mesure de sa création. Pour les besoins de ce guide de prise en main, il suffit de créer un dossier.

1. Connectez-vous à AEM. Dans le menu principal, sélectionnez **Navigation > Ressources > Fichiers**.
1. Cliquez sur **Créer > Dossier**.
1. Indiquez un **titre** et un **nom** pour votre dossier.
   * Le **titre** doit être descriptif.
   * Le **Nom** devient le nom du nœud dans le référentiel.
     * Il sera généré automatiquement en fonction du titre et adapté selon les [conventions d’appellation AEM.](/help/sites-developing/naming-conventions.md)
     * Il peut être adapté si nécessaire.

   ![Créer un dossier](assets/assets-folder-create.png)
1. Sélectionnez le dossier que vous venez de créer, puis sélectionnez **Propriétés** dans la barre d’outils (ou utilisez le [raccourci clavier](/help/sites-authoring/keyboard-shortcuts.md) `p`).
1. Dans la fenêtre **Propriétés**, sélectionnez l’onglet **Services cloud**.
1. Pour la **Configuration du cloud** sélectionnez la [configuration que vous avez créée précédemment.](create-configuration.md)
   ![Configurer le dossier de ressources](assets/assets-folder-configure.png)
1. Cliquez sur **Enregistrer et fermer**.
1. Cliquez sur **OK** dans la fenêtre de confirmation.

   ![Fenêtre de confirmation](assets/assets-folder-confirmation.png)

Vous pouvez créer des sous-dossiers supplémentaires dans le dossier que vous venez de créer. Les sous-dossiers hériteront de la **configuration du cloud** du dossier parent. Il est toutefois possible de modifier ce paramétrage si vous souhaitez utiliser les modèles d’une autre configuration.

Si vous utilisez une structure de site localisée, vous pouvez [créer une racine de langue](/help/assets/multilingual-assets.md) sous votre nouveau dossier.

## Étapes suivantes {#next-steps}

Maintenant que vous avez créé un dossier pour vos fragments de contenu, vous pouvez passer à la quatrième partie du guide de prise en main et [créer des fragments de contenu.](create-content-fragment.md)

>[!TIP]
>
>Pour plus d’informations sur la gestion des fragments de contenu, consultez la [documentation sur les fragments de contenu](/help/assets/content-fragments/content-fragments.md).
