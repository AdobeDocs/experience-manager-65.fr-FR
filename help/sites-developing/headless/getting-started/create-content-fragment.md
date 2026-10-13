---
title: Guide de démarrage rapide sur la création de fragments de contenu découplés
description: Découvrez comment utiliser les fragments de contenu AEM pour concevoir, de créer, d’organiser et d’utiliser du contenu indépendant des pages pour une diffusion découplée.
exl-id: 5787204d-bcce-447e-b98c-2bc1c0d744c3
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
source-wordcount: '378'
ht-degree: 100%
---
# Guide de démarrage rapide sur la création de fragments de contenu découplés {#creating-content-fragments}

Découvrez comment utiliser les fragments de contenu AEM pour concevoir, de créer, d’organiser et d’utiliser du contenu indépendant des pages pour une diffusion découplée.

## Que sont les fragments de contenu ? {#what-are-content-fragments}

[Maintenant que vous avez créé un dossier de ressources](create-assets-folder.md) dans lequel vous pouvez stocker vos fragments de contenu, vous pouvez créer les fragments.

Les fragments de contenu vous permettent de concevoir, de créer, d’organiser et de publier du contenu indépendant des pages. Ils permettent de préparer le contenu prêt à être utilisé dans des emplacements multiples et sur plusieurs canaux.

Les fragments de contenu contiennent du contenu structuré et peuvent être diffusés au format JSON.

## Création d’un fragment de contenu {#how-to-create-a-content-fragment}

Les créateurs ou créatrices de contenu créeront tout nombre de fragments de contenu pour représenter le contenu qu’ils créent. Ce sera leur principale tâche dans AEM. Pour les besoins de ce guide de prise en main, nous n’aurons besoin d’en créer qu’un.

1. Connectez-vous à AEM et dans le menu principal, sélectionnez **Navigation > Ressources**.
1. Accédez au [dossier que vous avez créé précédemment.](create-assets-folder.md)
1. Cliquez sur **Créer > Fragment de contenu**.
1. La création d’un fragment de contenu est présentée sous la forme d’un assistant en deux étapes. Commencez par sélectionner le modèle à utiliser pour créer votre fragment de contenu, puis cliquez sur **Suivant**.
   * Les modèles disponibles dépendent de la [**configuration du cloud** que vous avez définie pour le dossier de ressources](create-assets-folder.md) dans lequel vous créez le fragment de contenu.
   * Si vous recevez le message `We could not find any models`, vérifiez la configuration de votre dossier de ressources.

   ![Sélectionner un modèle de fragment de contenu](assets/content-fragment-model-select.png)
1. Définissez un **titre**, une **description** et des **balises** si nécessaire, puis cliquez sur **Créer**.

   ![Créer un fragment de contenu](assets/content-fragment-create.png)
1. Cliquez sur **Ouvrir** dans la fenêtre de confirmation.

   ![Confirmation de création du fragment de contenu](assets/content-fragment-confirmation.png)
1. Fournissez les détails du fragment de contenu dans l’éditeur de fragment de contenu.

   ![Éditeur de fragment de contenu](assets/content-fragment-edit.png)
1. Cliquez sur **Enregistrer** ou **Enregistrer et fermer**.

Les fragments de contenu peuvent faire référence à d’autres fragments de contenu, ce qui permet d’obtenir une structure de contenu imbriquée si nécessaire.

Les fragments de contenu peuvent également faire référence à d’autres ressources dans AEM. [Ces ressources doivent être stockées dans AEM](/help/assets/manage-assets.md) avant de créer un fragment de contenu de référence.

## Étapes suivantes {#next-steps}

Maintenant que vous avez créé un fragment de contenu, vous pouvez passer à la dernière partie du guide de prise en main et [créer des requêtes d’API pour accéder aux fragments de contenu et les diffuser.](create-api-request.md)

>[!TIP]
>
>Pour plus d’informations sur la gestion des fragments de contenu, voir la [documentation sur les fragments de contenu](/help/assets/content-fragments/content-fragments.md).
