---
title: Afficher les composants en fonction du modèle utilisé
description: Lorsque vous créez un formulaire, découvrez comment activer les composants dans la barre latérale en fonction du modèle sélectionné.
contentOwner: sashanka
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: customization
content-type: reference
docset: aem65
exl-id: 1fc56829-db81-4450-b1d8-b4a31110199e
solution: Experience Manager, Experience Manager Forms
role: User, Developer
feature: Adaptive Forms,Foundation Components
source-git-commit: 8a77756e8ba771c8de9950c2323bef8f23cc59b4
workflow-type: ht
source-wordcount: '351'
ht-degree: 100%

---

# Affichage des composants en fonction du modèle utilisé{#displaying-components-based-on-the-template-used}

Lorsqu’un créateur ou une créatrice de formulaire crée un formulaire adaptatif à l’aide d’un [modèle](../../forms/using/template-editor.md), il ou elle peut afficher et utiliser des composants spécifiques en fonction de la politique de modèle. Vous pouvez spécifier une politique de contenu de modèle qui vous permet de choisir un groupe de composants visible par l’auteur ou l’autrice du formulaire au moment de la création du formulaire.

## Modification de la politique de contenu d’un modèle {#changing-the-content-policy-of-a-template}

Lorsque vous créez un modèle, il est créé sous `/conf` dans le référentiel de contenu. En fonction des dossiers que vous avez créés dans le répertoire `/conf`, le chemin d’accès à votre modèle est : `/conf/<your-folder>/settings/wcm/templates/<your-template>`.

Effectuez les étapes suivantes pour afficher les composants dans la barre latérale en fonction de la politique de contenu d’un modèle :

1. Ouvrez CRXDE Lite.\
   URL : `https://<server>:<port>/crx/de/index.jsp`
1. Dans CRXDE, accédez au dossier dans lequel le modèle est créé.

   Par exemple : `/conf/<your-folder>/`

1. Dans CRXDE, accédez à : `/conf/<your-folder>/settings/wcm/policies/fd/af/layouts/gridFluidLayout/`.

   Pour sélectionner un groupe de composants, une nouvelle politique de contenu est nécessaire. Pour créer une politique, copiez-collez la politique par défaut et renommez-la.

   Le chemin d’accès à la politique de contenu par défaut est : `/conf/<your-folder>/settings/wcm/policies/fd/af/layouts/gridFluidLayout/default`.

   Dans le dossier `gridFluidLayout`, copiez-collez la politique par défaut et renommez-la. Par exemple, `myPolicy`.

   ![Copie des politiques par défaut](assets/crx-default1.png)

1. Sélectionnez la nouvelle politique que vous créez puis sélectionnez la propriété **composants** dans le panneau de droite avec le type `string[]`.

   Lorsque vous sélectionnez et ouvrez la propriété de composants, la boîte de dialogue Modifier les composants s’affiche. La boîte de dialogue Modifier les composants vous permet d’ajouter ou de supprimer des groupes de composants à l’aide des boutons **+** et **-**. Vous pouvez ajouter le groupe de composants qui comprend des composants du formulaire que vous souhaitez que les auteurs utilisent.

   ![Ajouter ou supprimer des composants dans la politique](assets/add-components-list1.png)

   Après avoir ajouté un groupe de composants, cliquez sur **OK** pour mettre à jour la liste, puis cliquez sur **Enregistrer tout** au-dessus de la barre d’adresse de CRXDE et actualisez.

1. Dans le modèle, remplacez la politique de contenu par défaut par la nouvelle politique que vous avez créée. (`myPolicy` dans cet exemple.)

   Pour modifier la politique, dans CRXDE, accédez à `/conf/<your-folder>/settings/wcm/templates/<your-template>/policies/jcr:content/guideContainer/rootPanel/items`.

   Dans la propriété `cq:policy`, modifiez `default` pour le nouveau nom de la politique (`myPolicy`).

   ![Politique de contenu de modèle mise à jour](assets/updated-policy.png)

   Lorsque vous créez un formulaire à l’aide du modèle, vous pouvez voir les composants supplémentaires dans la barre latérale.
