---
title: Création d’un exemple de page
description: Découvrez comment créer un modèle de site de communauté qui ne contient que la fonction Page qui peut vous aider à créer un site de communauté simple.
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
content-type: reference
topic-tags: developing
exl-id: d66fc1ff-a669-4a2c-b45a-093060facd97
solution: Experience Manager
feature: Communities
role: Developer
source-git-commit: 1f56c99980846400cfde8fa4e9a55e885bc2258d
workflow-type: tm+mt
source-wordcount: '405'
ht-degree: 1%

---

# Création d’un exemple de page {#create-a-sample-page}

Depuis AEM 6.1 Communities, le moyen le plus simple de créer un exemple de page est de créer un site de communauté simple, composé simplement d’une fonction Page .

Cela inclut un composant parsys afin que vous puissiez [activer les composants pour la création](basics.md#accessing-communities-components).

Une autre option d’exploration avec des exemples de composants consiste à utiliser les fonctionnalités présentées dans le [Guide des composants de la communauté](components-guide.md).

## Création d’un site de communauté {#create-a-community-site}

Ceci est similaire à la création d’un site décrit dans [Prise en main d’AEM Communities](getting-started.md).

La principale différence réside dans le fait que ce tutoriel crée un modèle de site de communauté qui ne contient que la [fonction de page](functions.md#page-function) pour créer un site de communauté simple. Elle le fait sans aucune autre fonction (autre que les fonctions préconfigurées de base pour tous les sites de la communauté).

### Créer un modèle de site {#create-new-site-template}

Pour commencer, créez un [modèle de site communautaire](sites.md) simple.

Dans la navigation globale sur une instance d’auteur, sélectionnez **[!UICONTROL Outils]** > **[!UICONTROL Communautés]** > **[!UICONTROL Modèles de site]**.

![create-site-template](assets/create-site-template1.png)

* Sélectionnez `Create button`.
* INFORMATIONS DE BASE

   * `Name` : modèle de page unique
   * `Description` : modèle consistant en une seule fonction Page.
   * Sélectionnez `Enabled`.

![site-template-editor](assets/site-template-editor.png)

* STRUCTURE

   * Faites glisser une fonction `Page` vers le Créateur de modèles
   * Pour les détails de la fonction de configuration, saisissez

      * `Title` : Une seule page
      * `URL` : page

![site-template-editor-structure](assets/site-template-editor1.png)

* Sélectionnez **`Save`** pour la configuration.
* Sélectionner **`Save`** pour le modèle de site

### Créer un site de communauté {#create-new-community-site}

Créez maintenant un site communautaire basé sur le modèle de site simple.

Après avoir créé le modèle de site, dans la navigation globale, sélectionnez **[!UICONTROL Communautés > Sites]**.

![create-community-site](assets/create-community-site1.png)

* Icône Sélectionner **`Create`**

* Étape `1 - Site Template`

   * `Title` : site communautaire simple
   * `Description` : site communautaire consistant en une seule page pour l’expérimentation.
   * `Community Site Root: (leave blank)`
   * `Community Site Base Language: English`
   * `Name` : exemple

      * url = http://localhost:4502/content/sites/sample

      * `Template` : choisissez `Single Page Template`

     ![create-community-site-template](assets/create-community-site-template.png)

* Sélectionnez `Next`.
* Étape `2 - Design`

   * Sélectionner n’importe quelle conception

* Sélectionnez `Next`.
* Sélectionnez `Next`.

  (Accepter tous les paramètres par défaut)

* Sélectionnez `Create`.

  ![create-community-site](assets/create-community-site.png)

## Publish du site {#publish-the-site}

![publish-site](assets/publish-site.png)

Dans la [ console de sites communautaires](sites-console.md), sélectionnez l’icône de publication pour publier le site, par défaut sur http://localhost:4503.

## Ouvrez le site en mode d’édition sur l’auteur {#open-the-site-on-author-in-edit-mode}

![open-site](assets/open-site.png)

Sélectionnez l’icône d’ouverture de site pour afficher le site en mode d’édition.

L’URL est [http://localhost:4502/editor.html/content/sites/sample/en.html](http://localhost:4502/editor.html/content/sites/sample/en.html)

![author-site](assets/author-site.png)

Sur la page d’accueil simple, il est possible de voir ce qui est préconnecté par le biais des fonctions et modèles de communauté, et de jouer avec l’ajout et la configuration de composants de communauté.

## Afficher le site sur Publish {#view-site-on-publish}

Après avoir publié la page, ouvrez la page sur l’ [instance de publication](http://localhost:4503/content/sites/sample/en.html) pour tester les fonctionnalités en tant que visiteur anonyme du site, membre connecté ou administrateur. Le lien Administration visible dans l’environnement de création n’apparaît pas dans l’environnement de publication, sauf si un administrateur se connecte.
