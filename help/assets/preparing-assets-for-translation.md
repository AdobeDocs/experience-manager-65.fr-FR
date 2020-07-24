---
title: Préparation des ressources pour la traduction
description: Créez des dossiers racine de langue pour préparer les fichiers à la traduction afin de prendre en charge les fichiers multilingues.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 29cf202b2522b4e624960e8b911f77ec7f291e24
workflow-type: tm+mt
source-wordcount: '450'
ht-degree: 66%

---


# Préparation des ressources pour la traduction {#preparing-assets-for-translation}

Les ressources multilingues sont des ressources comportant des fichiers binaires, des métadonnées et des balises dans plusieurs langues. En règle générale, les fichiers binaires, les métadonnées et les balises d’une ressource existent dans une langue, et sont ensuite traduits dans d’autres langues pour être utilisés dans des projets multilingues.

Dans les ressources d’Adobe Experience Manager, les ressources multilingues sont incluses dans des dossiers, où chaque dossier contient les ressources dans une langue différente.

Chaque dossier de langue est appelé une copie de langue. Le dossier racine d’une copie de langue, nommé racine de langue, identifie la langue du contenu de la copie de langue. For example, */content/dam/it* is the Italian language root for the Italian language copy. Les copies de langue doivent utiliser une [racine de langue correctement configurée](preparing-assets-for-translation.md#creating-a-language-root) pour que la langue correcte soit ciblée lors de la traduction des ressources source.

La copie de langue pour laquelle vous ajoutez initialement des ressources est le gabarit de langue. Le gabarit de langue est la source qui est traduite dans d’autres langues. L’exemple de hiérarchie de dossiers comporte plusieurs racines de langue :

```
 /content
  /- dam
   |- en
   |- fr
   |- de
   |- es
   |- it
   |- ja
   |- zh
```

Procédez comme suit pour préparer la traduction de vos ressources :

1. Créez la racine de langue de votre gabarit de langue. Par exemple, la racine de langue de la copie en anglais dans l’exemple de hiérarchie de dossiers est `/content/dam/en`. Ensure that the language root is correctly configured according to the information in [Create a Language Root](preparing-assets-for-translation.md#creating-a-language-root).

1. Ajoutez des ressources à votre gabarit de langue.
1. Créez la racine de langue de chaque langue cible pour laquelle vous avez besoin d’une copie de langue.

## Create a language root {#creating-a-language-root}

Pour créer la racine de langue, créez un dossier, puis utilisez le code de langue ISO comme valeur de la propriété Nom. Après avoir créé la racine de langue, vous pouvez créer une copie de langue à n’importe quel niveau dans la racine de langue.

Par exemple, la page racine de la copie en italien de l’exemple de hiérarchie présente la propriété Nom `it`. La propriété Nom est utilisée comme nom du nœud de ressource dans le référentiel et détermine donc le chemin d’accès des ressources. (`https://[aem_server]:[port]/assets.html/content/dam/it/`).

1. From the Assets console, click **[!UICONTROL Create]** and choose **[!UICONTROL Folder]** from the menu.

   ![Créer un dossier](assets/Create-folder.png)

1. In the **[!UICONTROL Name]** field type the country code in the format of `<language-code>`.

   ![Ajouter le code de langue dans le dossier](assets/Add-language-code-in-folder.png)

1. Cliquez sur **[!UICONTROL Créer]**. La racine de langue est créée dans la console Ressources.

## Affichage des racines de langue {#viewing-language-roots}

Experience Manager interface provides a **[!UICONTROL References]** panel that displays a list of language roots that have been created within Assets.

1. Dans la console Ressources, choisissez le gabarit de langue pour lequel vous souhaitez créer des copies de langue.
1. Dans le rail de gauche, sélectionnez l’option **[!UICONTROL Références]** pour ouvrir le volet [!UICONTROL Référence] .

   ![chlimage_1-122](assets/chlimage_1-122.png)

1. In the References pane, click **[!UICONTROL Language Copies]**. The [!UICONTROL Language Copies] panel shows the language copies of the assets.

   ![copies de langue](assets/lang-copy2.png)
