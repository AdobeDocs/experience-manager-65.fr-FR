---
title: Préparation du contenu à traduire
description: Découvrez comment préparer le contenu à traduire dans Adobe Experience Manager.
contentOwner: Guillaume Carlino
feature: Language Copy
exl-id: 81978733-89a6-4436-bcf1-4bde962ed54f
source-git-commit: 10b370fd8f855f71c6d7d791c272137bb5e04d97
workflow-type: tm+mt
source-wordcount: '669'
ht-degree: 59%

---

# Préparation du contenu à traduire{#preparing-content-for-translation}

Les sites web multilingues fournissent généralement une certaine quantité de contenu dans plusieurs langues. Le site est créé dans une langue, puis traduit dans d’autres langues. En règle générale, les sites multilingues se composent de branches de pages, où chaque branche contient les pages du site dans une langue différente.

L’exemple de site de démonstration de Geometrixx comprend plusieurs branches de langue et utilise la structure suivante :

```xml
/content
    |- geometrixx
             |- en
             |- fr
             |- de
             |- es
             |- it
             |- ja
             |- zh
```

Chaque branche de langue d’un site est appelée « copie de langue ». La page racine d’une copie de langue, appelée « racine de langue », identifie la langue du contenu de la copie de langue. Par exemple, `/content/geometrixx/fr` est la racine de langue de la copie en français. Les copies de langue doivent utiliser une [racine de langue correctement configurée](/help/sites-administering/tc-prep.md#creating-a-language-root) afin que la langue correcte soit ciblée lors de la traduction d’un site source.

La copie de langue pour laquelle vous créez initialement le contenu du site est le gabarit de langue. Le gabarit de langue est la source qui est traduite dans d’autres langues.

Procédez comme suit pour préparer la traduction de vos ressources :

1. Créez la racine de langue de votre gabarit de langue. Par exemple, la racine de langue du site de démonstration Geometrixx en anglais est /content/geometrixx/en. Vérifiez que la racine de langue est configurée conformément aux informations de la section [Création d’une racine de langue](/help/sites-administering/tc-prep.md#creating-a-language-root).
1. Créez le contenu de votre gabarit de langue.
1. Créez la racine de langue de chaque copie de langue pour votre site. Par exemple, la copie en français de l’exemple de site de Geometrixx est /content/geometrixx/fr.

Après avoir préparé le contenu à traduire, vous pouvez créer automatiquement les pages manquantes dans les copies de langue et les projets de traduction associés. (Voir [Création d’un projet de traduction](/help/sites-administering/tc-manage.md).) Pour obtenir une présentation du processus de traduction de contenu dans AEM, consultez [Traduction de contenu pour des sites multilingues](/help/sites-administering/translation.md).

## Création d’une racine de langue {#creating-a-language-root}

Créez une racine de langue comme page racine d’une copie de langue qui identifie la langue du contenu. Après avoir créé la racine de langue, vous pouvez créer des projets de traduction qui incluent la copie de langue.

Pour créer la racine de langue, créez une page, puis utilisez le code de langue ISO comme valeur de la propriété Nom. Le code de la langue doit être dans l’un des formats suivants :

* `<language-code>`Le code de langue pris en charge est un code à deux lettres défini par la norme ISO-639-1, par exemple : `en`.

* `<language-code>_<country-code>` ou `<language-code>-<country-code>`Le code de pays pris en charge est un code à deux lettres en minuscules ou en majuscules, comme défini par la norme ISO 3166, par exemple : `en_US`, `en_us`, `en_GB`, `en-gb`.

Vous pouvez utiliser l’un de ces formats en fonction de la structure choisie pour votre site international. Par exemple, la propriété Nom de la page racine de la copie de langue française de l’exemple de site Geometrixx est définie sur `fr`. La propriété Name est utilisée comme nom du noeud de page dans le référentiel et détermine donc le chemin d’accès de la page. (http://localhost:4502/content/geometrixx/fr.html)

La procédure ci-dessous utilise l’interface utilisateur optimisée pour les écrans tactiles pour créer une copie de langue d’un site web. Pour obtenir des instructions sur l’utilisation de l’interface utilisateur classique, voir [Création d’une racine de langue à l’aide de l’interface utilisateur classique](/help/sites-administering/tc-lroot-classic.md).

1. Accédez à Sites.
1. Cliquez sur le site pour lequel vous souhaitez créer une copie de langue.

   Par exemple, pour créer une copie de langue du site Geometrixx Outdoors, cliquez sur Site Geometrixx Outdoors.

1. Cliquez sur Créer, puis sur Créer une page.

   ![chlimage_1-21](assets/chlimage_1-21a.png)

1. Sélectionnez le modèle de page, puis cliquez sur Suivant.
1. Dans le champ Nom , saisissez le code de pays au format de `<language-code>` ou `<language-code>_<country-code>`, par exemple : `en`, `en_US`, `en_us`, `en_GB`, `en_gb`. Saisissez un titre pour la page.

   ![chlimage_1-22](assets/chlimage_1-22a.png)

1. Cliquez sur Créer. Dans la boîte de dialogue de confirmation, cliquez sur l’une des options suivantes : **Terminé** pour revenir à la console Sites, ou **Ouvrir** pour ouvrir la copie de langue.

## Affichage de le statut des racines de langue {#seeing-the-status-of-language-roots}

L’IU optimisée pour les écrans tactiles fournit un panneau Références qui affiche la liste des racines de langue qui ont été créées.

![chlimage_1-23](assets/chlimage_1-23a.png)

La procédure ci-dessous utilise l’interface utilisateur optimisée pour les écrans tactiles afin d’afficher le panneau Références d’une page.

1. Dans la console Sites, sélectionnez une page du site, puis cliquez sur **Références**.

   ![chlimage_1-24](assets/chlimage_1-24a.png)

1. Dans le panneau Références, cliquez sur **Copies de langue**. Le panneau Copies de langue affiche les copies de langue du site web.
