---
title: Préparation des ressources pour la traduction
description: Créez des dossiers racine de langue pour préparer les ressources à la traduction afin de prendre en charge les ressources multilingues.
contentOwner: AG
role: User, Admin
feature: Projects
exl-id: eee768e3-3eb4-46fa-b9ae-9ef8764a3a94
solution: Experience Manager, Experience Manager Assets
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: d09181b5-a36a-43de-ba01-36641440bc43
    internal-label: Experience Manager Assets
feature_v2:
  - id: 2e0e1a8a-56e7-5bd5-b805-f35a7c0c2ca7
    internal-label: Projects
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '449'
ht-degree: 100%
---
# Préparation des ressources pour la traduction {#preparing-assets-for-translation}

Les ressources multilingues sont des ressources comportant des fichiers binaires, des métadonnées et des balises dans plusieurs langues. En règle générale, les fichiers binaires, les métadonnées et les balises d’une ressource existent dans une langue, et sont ensuite traduits dans d’autres langues pour être utilisés dans des projets multilingues.

Dans [!DNL Adobe Experience Manager Assets], les ressources multilingues se trouvent dans des dossiers, chaque dossier contenant les ressources dans une langue différente.

Chaque dossier de langue est appelé « copie linguistique ». Le dossier racine d’une copie linguistique, appelé « racine de langue », identifie la langue du contenu de la copie linguistique. Par exemple, */content/dam/it* est la racine de langue italienne de la copie linguistique italienne. Les copies de langue doivent utiliser une [racine de langue correctement configurée](preparing-assets-for-translation.md#creating-a-language-root) pour que la bonne langue soit ciblée lors de la traduction des ressources sources.

La copie linguistique pour laquelle vous ajoutez initialement des ressources est la langue principale. La langue principale est la source qui est traduite dans d’autres langues. L’exemple de hiérarchie de dossiers comporte plusieurs racines de langue :

```shell
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

1. Créez la racine de langue de votre langue principale. Par exemple, la racine de langue de la copie linguistique anglaise dans l’exemple de hiérarchie de dossiers est `/content/dam/en`. Vérifiez que la racine de langue est configurée conformément aux informations de la section [Création d’une racine de langue](preparing-assets-for-translation.md#creating-a-language-root).

1. Ajoutez des ressources à votre langue principale.
1. Créez la racine de langue de chaque langue cible pour laquelle vous avez besoin d’une copie linguistique.

## Création d’une racine de langue {#creating-a-language-root}

Pour créer la racine de langue, créez un dossier, puis utilisez le code de langue ISO comme valeur de la propriété Nom. Après avoir créé la racine de langue, vous pouvez créer une copie linguistique à n’importe quel niveau de la racine de langue.

Par exemple, la page racine de la copie linguistique italienne de l’exemple de hiérarchie présente la propriété Nom `it`. La propriété Nom est utilisée comme nom du nœud de ressource dans le référentiel et détermine donc le chemin d’accès des ressources. (`https://[aem_server]:[port]/assets.html/content/dam/it/`).

1. Dans la console [!DNL Assets], cliquez sur **[!UICONTROL Créer]**, puis sélectionnez **[!UICONTROL Dossier]** dans le menu.

   ![Créer un dossier](assets/Create-folder.png)

1. Dans le champ **[!UICONTROL Nom]**, tapez le code de pays au format `<language-code>`.

   ![Ajout du code de langue dans le dossier](assets/Add-language-code-in-folder.png)

1. Cliquez sur **[!UICONTROL Créer]**. La racine de langue est créée dans la console [!DNL Assets].

## Affichage des racines de langue {#viewing-language-roots}

L’interface [!DNL Experience Manager] contient un panneau **[!UICONTROL Références]** qui affiche une liste des racines de langue créées dans [!DNL Assets].

1. Dans la console [!DNL Assets], choisissez la langue principale pour laquelle vous souhaitez créer des copies de langue.
1. Dans le rail de gauche, sélectionnez l’option **[!UICONTROL Références]** pour ouvrir le volet [!UICONTROL Référence].

   ![chlimage_1-122](assets/chlimage_1-122.png)

1. Dans le volet Références, cliquez sur **[!UICONTROL Copies de langue]**. Le panneau [!UICONTROL Copies de langue] affiche les copies de langue des ressources.

   ![copies de langue](assets/lang-copy2.png)
