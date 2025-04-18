---
title: Éditeur de boîtes de dialogue
description: L’éditeur de boîtes de dialogue fournit une interface graphique pour créer et modifier facilement des boîtes de dialogue et des modèles automatiques.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: development-tools
content-type: reference
exl-id: 57303608-c3e1-4201-8054-1a1798613e2c
solution: Experience Manager, Experience Manager Sites
feature: Developing,Developer Tools
role: Developer
source-git-commit: 305227eff3c0d6414a5ae74bcf3a74309dccdd13
workflow-type: tm+mt
source-wordcount: '474'
ht-degree: 100%

---

# Éditeur de boîtes de dialogue{#dialog-editor}

L’éditeur de boîtes de dialogue fournit une interface graphique pour créer et modifier facilement des boîtes de dialogue et des modèles automatiques.

Pour découvrir comment cet éditeur fonctionne, accédez à CRXDE Lite, développez l’arborescence de l’explorateur pour atteindre `/libs/foundation/components/chart`, puis double-cliquez sur le nœud `dialog` :

![chlimage_1-247](assets/chlimage_1-247.png)

Le nœud de boîtes de dialogue ouvre l’**éditeur de boîtes de dialogue** :

![screen_shot_2012-02-01at25033pm](assets/screen_shot_2012-02-01at25033pm.png)

## Vue d’ensemble de l’interface utilisateur {#user-interface-overview}

L’interface de l’éditeur de boîtes de dialogue se compose de quatre volets :

* La **palette**, dans le coin supérieur gauche. Ce volet contient les widgets disponibles pour créer une boîte de dialogue, tels que les panneaux à onglets, les champs de texte, les listes de sélection et les boutons. Vous pouvez développer les différentes catégories de la palette en cliquant sur la barre de séparation souhaitée.
* Le volet de **structure**, dans le coin inférieur gauche. Ce volet affiche la structure hiérarchique des nœuds qui constituent la définition de la boîte de dialogue. Vous pouvez voir la même structure en développant le nœud de la boîte de dialogue dans CRXDE Lite ou l’explorateur de contenu CRX.
* Le volet **Rendu**, au milieu de la fenêtre. Ce volet affiche comment la définition de la boîte de dialogue définie dans le volet de structure est rendue comme boîte de dialogue réelle.
* Le volet **Propriétés** : Ce volet affiche les propriétés du nœud mis en surbrillance dans le volet de structure.

### Utilisation de l’éditeur de boîtes de dialogue {#using-the-dialog-editor}

Pour créer une boîte de dialogue, la personne fait glisser des éléments de la palette vers le volet de structure, au sein de la hiérarchie de définition de la boîte de dialogue.

Une fois la structure souhaitée terminée, la personne clique sur **Enregistrer**, en haut du volet de rendu.

>[!CAUTION]
>
>L’éditeur de boîte de dialogue sert à créer des boîtes de dialogue simples. Il peut ne pas être en mesure de modifier des définitions de boîte de dialogue plus complexes. Dans les cas où l’éditeur de boîte de dialogue n’autorise pas la modification d’une structure de boîte de dialogue, la définition de la boîte de dialogue doit être créée, modifiée, ou les deux, manuellement. Pour ce faire, modifiez directement la structure de nœud à l’aide de CRXDE Lite ou de l’explorateur de contenu CRX, par exemple.

### Créer une boîte de dialogue {#creating-a-new-dialog}

Pour créer une boîte de dialogue, sélectionnez le composant requis, cliquez sur **Créer...**, puis sur **Créer une boîte de dialogue...**.

Saisissez les informations requises, puis cliquez sur **Enregistrer tout**. Vous pouvez à présent double-cliquer sur la boîte de dialogue pour l’ouvrir dans l’éditeur.

### Utilisation de l’éditeur de boîtes de dialogue pour les modèles automatiques {#using-the-dialog-editor-for-scaffolds}

Un modèle automatique est une page spéciale contenant un formulaire qui peut être rempli et envoyé en une seule étape. Vous pouvez ainsi créer rapidement une page à partir du contenu saisi.

Le formulaire qui constitue un modèle automatique est défini par une définition de boîte de dialogue, tout comme une boîte de dialogue normale, bien qu’il apparaisse sur la page de génération de modèles automatiques sous une autre forme. Les définitions de boîte de dialogue étant utilisées pour définir des modèles automatiques, ces derniers peuvent être conçus à l’aide de l’éditeur de boîtes de dialogue. Lorsque vous utilisez l’éditeur de boîtes de dialogue de cette manière, le volet de rendu affiche toujours la définition de boîte de dialogue sous la forme d’une boîte de dialogue et non d’un modèle automatique.

Pour plus d’informations sur l’utilisation de l’éditeur de boîtes de dialogue pour créer des modèles automatiques, consultez [Génération de modèles automatiques](/help/sites-authoring/scaffolding.md).
