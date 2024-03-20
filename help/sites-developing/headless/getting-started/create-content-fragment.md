---
title: Guide de démarrage rapide sur la création de fragments de contenu découplés
description: Découvrez comment utiliser les fragments de contenu AEM pour concevoir, créer, organiser et utiliser du contenu indépendant des pages pour une diffusion découplée.
exl-id: 5787204d-bcce-447e-b98c-2bc1c0d744c3
solution: Experience Manager, Experience Manager Sites
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '375'
ht-degree: 85%

---

# Guide de démarrage rapide sur la création de fragments de contenu découplés {#creating-content-fragments}

Découvrez comment utiliser les fragments de contenu AEM pour concevoir, créer, organiser et utiliser du contenu indépendant des pages pour une diffusion découplée.

## Que sont les fragments de contenu ?  {#what-are-content-fragments}

[Maintenant que vous avez créé un dossier de ressources](create-assets-folder.md) dans lequel vous pouvez stocker vos fragments de contenu, vous pouvez créer les fragments.

Les fragments de contenu vous permettent de concevoir, de créer, d’organiser et de publier du contenu indépendant des pages. Ils permettent de préparer le contenu prêt à être utilisé dans des emplacements multiples et sur plusieurs canaux.

Les fragments de contenu contiennent du contenu structuré et peuvent être diffusés au format JSON.

## Création d’un fragment de contenu {#how-to-create-a-content-fragment}

Les auteurs et autrices de contenu créeront n’importe quel nombre de fragments de contenu pour représenter le contenu créé. Ce sera leur principale tâche dans AEM. Pour les besoins de ce guide de prise en main, nous n’aurons besoin d’en créer qu’un.

1. Connectez-vous à AEM et sélectionnez dans le menu principal **Navigation > Ressources**.
1. Accédez au [dossier que vous avez créé précédemment.](create-assets-folder.md)
1. Cliquez sur **Créer > Fragment de contenu**.
1. La création d’un fragment de contenu est présentée sous la forme d’un assistant en deux étapes. Sélectionnez d’abord le modèle que vous souhaitez utiliser pour créer votre fragment de contenu, puis cliquez sur **Suivant**.
   * Les modèles disponibles dépendent de la [**configuration du cloud** que vous avez définie pour le dossier de ressources](create-assets-folder.md) dans lequel vous créez le fragment de contenu.
   * Si vous recevez le message `We could not find any models`, vérifiez la configuration de votre dossier de ressources.

   ![Sélectionner un modèle de fragment de contenu](assets/content-fragment-model-select.png)
1. Fournissez une **Titre**, **Description**, et **Balises** Si nécessaire, cliquez sur **Créer**.

   ![Créer un fragment de contenu](assets/content-fragment-create.png)
1. Cliquez sur **Ouvrir** dans la fenêtre de confirmation.

   ![Confirmation de création du fragment de contenu](assets/content-fragment-confirmation.png)
1. Fournissez les détails du fragment de contenu dans l’éditeur de fragment de contenu.

   ![Éditeur de fragment de contenu](assets/content-fragment-edit.png)
1. Cliquez sur **Enregistrer** ou  **Enregistrer et fermer**.

Les fragments de contenu peuvent faire référence à d’autres fragments de contenu, ce qui permet d’obtenir une structure de contenu imbriquée si nécessaire.

Les fragments de contenu peuvent également faire référence à d’autres ressources dans AEM. [Ces ressources doivent être stockées dans AEM](/help/assets/manage-assets.md) avant de créer un fragment de contenu de référence.

## Étapes suivantes {#next-steps}

Maintenant que vous avez créé un fragment de contenu, vous pouvez passer à la dernière partie du guide de prise en main et [créer des requêtes d’API pour accéder aux fragments de contenu et les diffuser.](create-api-request.md)

>[!TIP]
>
>Pour plus d’informations sur la gestion des fragments de contenu, voir la [documentation sur les fragments de contenu](/help/assets/content-fragments/content-fragments.md).
