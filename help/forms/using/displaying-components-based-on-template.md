---
title: Affichage des composants en fonction du modèle utilisé
seo-title: Affichage des composants en fonction du modèle utilisé
description: Lorsque vous créez un formulaire, découvrez comment vous pouvez activer les composants dans la barre latérale en fonction du modèle sélectionné.
seo-description: Lorsque vous créez un formulaire, découvrez comment vous pouvez activer les composants dans la barre latérale en fonction du modèle sélectionné.
uuid: 790d201b-318d-4d02-9bc5-9d6bc41d057a
contentOwner: sashanka
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: customization
content-type: reference
discoiquuid: f658da57-0134-4458-9ef9-a99787b66742
docset: aem65
translation-type: tm+mt
source-git-commit: 76908a565bf9e6916db39d7db23c04d2d40b3247
workflow-type: tm+mt
source-wordcount: '378'
ht-degree: 75%

---


# Affichage des composants en fonction du modèle utilisé{#displaying-components-based-on-the-template-used}

Lorsqu’un auteur de formulaire crée un formulaire adaptatif à l’aide d’un [modèle](../../forms/using/template-editor.md), il peut consulter et utiliser des composants spécifiques en fonction de la stratégie de modèle. Vous pouvez spécifier une stratégie de contenu de modèle qui vous permet de sélectionner un groupe de composants visible par l’auteur de formulaire lors de la création de formulaires.

## Modification de la stratégie de contenu d’un modèle {#changing-the-content-policy-of-a-template}

Lorsque vous créez un modèle, il est créé sous `/conf` dans le référentiel de contenu. En fonction des dossiers que vous avez créés dans le répertoire `/conf`, le chemin d’accès à votre modèle est le suivant : `/conf/<your-folder>/settings/wcm/templates/<your-template>`.

Effectuez les étapes suivantes pour afficher les composants dans la barre latérale en fonction de la stratégie de contenu d’un modèle :

1. Ouvrez CRXDE Lite.\
   URL: `https://<server>:<port>/crx/de/index.jsp`
1. Dans CRXDE, accédez au dossier dans lequel le modèle est créé.

   Par exemple : `/conf/<your-folder>/`

1. Dans CRXDE, accédez à : `/conf/<your-folder>/settings/wcm/policies/fd/af/layouts/gridFluidLayout/`

   Pour sélectionner un groupe de composants, une nouvelle stratégie de contenu est requise. Pour créer une nouvelle stratégie, copiez-collez la stratégie par défaut et renommez-la.

   Le chemin d’accès à la stratégie de contenu par défaut est : `/conf/<your-folder>/settings/wcm/policies/fd/af/layouts/gridFluidLayout/default`

   Dans le dossier `gridFluidLayout`, copiez-collez la stratégie par défaut et renommez-la. Par exemple, `myPolicy`.

   ![Copie des stratégies par défaut](assets/crx-default1.png)

1. Sélectionnez la nouvelle stratégie que vous créez, puis la propriété **components** dans le panneau de droite avec le type `string[]`.

   Lorsque vous sélectionnez et ouvrez la propriété de composants, la boîte de dialogue Modifier les composants s’affiche. Elle vous permet d’ajouter ou de supprimer les groupes de composants en utilisant les boutons **+** et **-**. Vous pouvez ajouter le groupe de composants qui comprend des composants du formulaire que vous souhaitez que les auteurs utilisent.

   ![Ajouter ou supprimer des composants dans la stratégie](assets/add-components-list1.png)

   Après avoir ajouté un groupe de composants, cliquez sur **OK** pour mettre à jour la liste, puis cliquez sur **Enregistrer tout** au-dessus de la barre d’adresse de CRXDE et actualisez.

1. Dans le modèle, remplacez la stratégie de contenu par défaut par la nouvelle stratégie que vous avez créée. ( `myPolicy` dans cet exemple.)

   Pour modifier la stratégie, dans CRXDE, accédez à `/conf/<your-folder>/settings/wcm/templates/<your-template>/policies/jcr:content/guideContainer/rootPanel/items`.

   Dans la propriété `cq:policy`, remplacez `default` par le nouveau nom de la stratégie ( `myPolicy`).

   ![Stratégie de contenu de modèle mise à jour](assets/updated-policy.png)

   Lorsque vous créez un formulaire à l’aide du modèle, vous pouvez voir les composants supplémentaires dans la barre latérale.

