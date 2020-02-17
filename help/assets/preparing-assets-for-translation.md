---
title: Préparation des fichiers pour la traduction
description: Créez des dossiers racine de langue pour préparer les fichiers à la traduction afin de prendre en charge les fichiers multilingues.
contentOwner: AG
translation-type: tm+mt
source-git-commit: a39ee0f435dc43d2c2830b2947e91ffdcf11c7f6

---


# Préparation des fichiers pour la traduction {#preparing-assets-for-translation}

Les ressources multilingues sont des ressources comportant des fichiers binaires, des métadonnées et des balises dans plusieurs langues. En règle générale, les fichiers binaires, les métadonnées et les balises d’une ressource existent dans une langue, et sont ensuite traduits dans d’autres langues pour être utilisés dans des projets multilingues.

Dans Adobe Experience Manager (AEM) Assets, les ressources multilingues se trouvent dans des dossiers, chaque dossier contenant les ressources dans une langue différente.

Chaque dossier de langue est appelé une copie de langue. Le dossier racine d’une copie de langue, nommé racine de langue, identifie la langue du contenu de la copie de langue. For example, */content/dam/it* is the Italian language root for the Italian language copy. Language copies must use a [correctly-configured language root](preparing-assets-for-translation.md#creating-a-language-root) so that the correct language is targeted when translations of source assets are performed.

La copie de langue pour laquelle vous ajoutez initialement des ressources est le gabarit de langue. Le gabarit de langue est la source qui est traduite dans d’autres langues. Un exemple de hiérarchie de dossiers comprend plusieurs racines de langage :

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

1. Créez la racine de langue de votre gabarit de langue. Par exemple, la racine de langue de la copie de langue de l’anglais dans l’exemple de hiérarchie de dossiers est `/content/dam/en`. Ensure that the language root is correctly configured according to the information in [Create a Language Root](preparing-assets-for-translation.md#creating-a-language-root).

1. Ajoutez des ressources à votre gabarit de langue.
1. Créez la racine de langue de chaque langue cible pour laquelle vous avez besoin d’une copie de langue.

## Création d’une racine de langue {#creating-a-language-root}

Pour créer la racine de langue, créez un dossier, puis utilisez le code de langue ISO comme valeur de la propriété Nom. Après avoir créé la racine de langue, vous pouvez créer une copie de langue à n’importe quel niveau dans la racine de langue.

For example, the root page of the Italian language copy of the sample hierarchy has `it` as the Name property. La propriété Nom est utilisée comme nom du nœud de ressource dans le référentiel et détermine donc le chemin d’accès des ressources. (`https://[aem_server]:[port]/assets.html/content/dam/it/`).

1. Dans la console Ressources, cliquez/appuyez sur **[!UICONTROL Créer]** et choisissez **[!UICONTROL Dossier]** dans le menu.

   ![Créer un dossier](assets/Create-folder.png)

1. In the **[!UICONTROL Name]** field type the country code in the format of `<language-code>`.

   ![Ajouter un code de langue dans le dossier](assets/Add-language-code-in-folder.png)

1. Cliquez ou appuyez sur **[!UICONTROL Créer]**. La racine de langue est créée dans la console Ressources. 

## Afficher les racines de langue {#viewing-language-roots}

AEM interface provides a **[!UICONTROL References]** panel that displays a list of language roots that have been created within AEM Assets.

1. Dans la console Ressources, choisissez le gabarit de langue pour lequel vous souhaitez créer des copies de langue.
1. Appuyez ou cliquez sur l’icône de navigation globale et sélectionnez **[!UICONTROL Références]** pour ouvrir le panneau Références.

   ![chlimage_1-122](assets/chlimage_1-122.png)

1. Dans le panneau Références, cliquez ou appuyez sur **[!UICONTROL Copies de langue]**. The [!UICONTROL Language Copies] panel shows the language copies of the assets.

   ![chlimage_1-123](assets/chlimage_1-123.png)
