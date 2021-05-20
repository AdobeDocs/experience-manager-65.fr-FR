---
title: Création d’un exemple de page
seo-title: Création d’un exemple de page
description: Créer un exemple de site de communauté
seo-description: Créer un exemple de site de communauté
uuid: 04a8f027-b7d8-493a-a9bd-5c4a6715d754
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
content-type: reference
topic-tags: developing
discoiquuid: a03145f7-6697-4797-b73e-6f8d241ce469
exl-id: d66fc1ff-a669-4a2c-b45a-093060facd97
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '420'
ht-degree: 2%

---

# Créer un exemple de page {#create-a-sample-page}

Depuis AEM 6.1 Communities, le moyen le plus simple de créer un exemple de page est de créer un site de communauté simple, composé simplement d’une fonction Page .

Cela inclut un composant parsys afin que vous puissiez [activer les composants pour la création](basics.md#accessing-communities-components).

Une autre option d’exploration avec des exemples de composants consiste à utiliser les fonctionnalités présentées dans le [Guide des composants de communauté](components-guide.md).

## Créer un site communautaire {#create-a-community-site}

Ceci est très similaire à la création d’un site décrit dans [Prise en main d’AEM Communities](getting-started.md).

La principale différence réside dans le fait que ce tutoriel crée un nouveau modèle de site communautaire qui ne contient que la [fonction de page](functions.md#page-function) afin de créer un site communautaire simple, sans aucune autre fonctionnalité (autre que les fonctionnalités préconfigurées de base de tous les sites communautaires).

### Créer un modèle de site {#create-new-site-template}

Pour commencer, créez un [modèle de site communautaire](sites.md) simple.

Dans la navigation globale sur une instance d’auteur, sélectionnez **[!UICONTROL Outils]** > **[!UICONTROL Communautés]** > **[!UICONTROL Modèles de site]**.

![create-site-template](assets/create-site-template1.png)

* Sélectionner `Create button`
* INFORMATIONS DE BASE

   * `Name`: Modèle de page unique
   * `Description`: Un modèle constitué d’une fonction Page unique.
   * Sélectionner `Enabled`

![site-template-editor](assets/site-template-editor.png)

* STRUCTURE

   * Faites glisser une fonction `Page` vers le Créateur de modèles
   * Pour les détails de la fonction de configuration, saisissez

      * `Title`: Une seule page
      * `URL`: page

![site-template-editor-structure](assets/site-template-editor1.png)

* Sélectionnez **`Save`** pour la configuration.
* Sélectionnez **`Save`** pour le modèle de site.

### Créer un site de communauté {#create-new-community-site}

Créez maintenant un site communautaire basé sur le modèle de site simple.

Après avoir créé le modèle de site, dans la navigation globale, sélectionnez **[!UICONTROL Communautés > Sites]**.

![create-community-site](assets/create-community-site1.png)

* Icône Sélectionner **`Create`**

* Étape `1 - Site Template`

   * `Title`: Site de communauté simple
   * `Description`: Un site communautaire constitué d’une seule page à des fins d’expérimentation.
   * `Community Site Root: (leave blank)`
   * `Community Site Base Language: English`
   * `Name`: sample

      * url = http://localhost:4502/content/sites/sample

      * `Template`: select  `Single Page Template`

      ![create-community-site-template](assets/create-community-site-template.png)


* Sélectionner `Next`
* Étape `2 - Design`

   * Sélectionner n’importe quelle conception

* Sélectionner `Next`
* Sélectionner `Next`

   (Accepter tous les paramètres par défaut)

* Sélectionner `Create`

   ![create-community-site](assets/create-community-site.png)

## Publier le site {#publish-the-site}

![publish-site](assets/publish-site.png)

Dans la [console Sites de la communauté](sites-console.md), sélectionnez l’icône Publier pour publier le site, par défaut sur http://localhost:4503.

## Ouvrez le site sur l’auteur en mode d’édition {#open-the-site-on-author-in-edit-mode}

![open site](assets/open-site.png)

Sélectionnez l’icône d’ouverture de site pour afficher le site en mode d’édition.

L’URL sera [http://localhost:4502/editor.html/content/sites/sample/en.html](http://localhost:4502/editor.html/content/sites/sample/en.html)

![author-site](assets/author-site.png)

Sur la page d’accueil simple, il est possible de voir ce qui est préconnecté par le biais des fonctions et modèles de communauté, et de jouer avec l’ajout et la configuration de composants de communauté.

## Afficher le site lors de la publication {#view-site-on-publish}

Après avoir publié la page, ouvrez la page sur l’ [instance de publication](http://localhost:4503/content/sites/sample/en.html) afin d’expérimenter les fonctionnalités en tant que visiteur anonyme du site, membre connecté ou administrateur. Le lien Administration visible dans l’environnement de création ne s’affiche pas dans l’environnement de publication, sauf si un administrateur se connecte.
