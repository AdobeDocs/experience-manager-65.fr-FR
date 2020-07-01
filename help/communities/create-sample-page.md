---
title: Créer un exemple de page
seo-title: Créer un exemple de page
description: Créer un exemple de site communautaire
seo-description: Créer un exemple de site communautaire
uuid: 04a8f027-b7d8-493a-a9bd-5c4a6715d754
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/COMMUNITIES
content-type: reference
topic-tags: developing
discoiquuid: a03145f7-6697-4797-b73e-6f8d241ce469
translation-type: tm+mt
source-git-commit: 56c2e6b55964ea5f3e180b17bd2a244882aa62ea
workflow-type: tm+mt
source-wordcount: '420'
ht-degree: 4%

---


# Create a Sample Page {#create-a-sample-page}

Depuis les communautés AEM 6.1, le moyen le plus simple de créer un exemple de page consiste à créer un site communautaire simple, constitué simplement d’une fonction Page.

Ceci inclut un composant parsys afin que vous puissiez [activer les composants pour la création](basics.md#accessing-communities-components).

Une autre option d&#39;exploration avec des échantillons de composants consiste à utiliser les fonctionnalités présentées dans le Guide [des composants](components-guide.md)communautaires.

## Créer un site communautaire {#create-a-community-site}

Cela ressemble beaucoup à la création d&#39;un nouveau site décrit dans [Prise en main des AEM Communities](getting-started.md).

La principale différence est que ce tutoriel va créer un nouveau modèle de site communautaire qui ne contient que la fonction [](functions.md#page-function) Page afin de créer un site communautaire simple et gratuit d&#39;autres fonctionnalités (autres que les fonctionnalités préprogrammées de base pour tous les sites communautaires).

### Créer un nouveau modèle de site {#create-new-site-template}

Pour commencer, créez un modèle [de site](sites.md)communautaire simple.

Dans la navigation globale sur une instance d’auteur, sélectionnez **[!UICONTROL Outils]** > **[!UICONTROL Communautés]** > Modèles **[!UICONTROL de]** site.

![chlimage_1-82](assets/chlimage_1-82.png)

* Sélectionner `Create button`
* INFORMATIONS DE BASE

   * `Name`: Modèle de page unique
   * `Description`: Modèle constitué d’une fonction Page unique.
   * Sélectionner `Enabled`

![chlimage_1-83](assets/chlimage_1-83.png)

* STRUCTURE

   * Faire glisser une `Page` fonction vers le créateur de modèles
   * Pour les détails de la fonction de configuration, saisissez

      * `Title`: Page unique
      * `URL`: page

![chlimage_1-84](assets/chlimage_1-84.png)

* Sélectionner **`Save`** pour la configuration
* Sélectionner **`Save`** pour le modèle de site

### Créer un site de communauté {#create-new-community-site}

Créez maintenant un site communautaire basé sur le modèle de site simple.

Après avoir créé le modèle de site, dans la navigation globale, sélectionnez **[!UICONTROL Communautés > Sites]**.

![chlimage_1-85](assets/chlimage_1-85.png)

* Icône Sélectionner **`Create`**

* Étape `1 - Site Template`

   * `Title`: Site communautaire simple
   * `Description`: Site communautaire constitué d&#39;une seule page d&#39;expérimentation.
   * `Community Site Root: (leave blank)`
   * `Community Site Base Language: English`
   * `Name`: sample

      * url = http://localhost:4502/content/sites/sample

      * `Template`: choisir `Single Page Template`

      ![chlimage_1-86](assets/chlimage_1-86.png)


* Sélectionner `Next`
* Étape `2 - Design`

   * Sélectionner n’importe quelle conception

* Sélectionner `Next`
* Sélectionner `Next`

   (Accepter tous les paramètres par défaut)

* Sélectionner `Create`

   ![chlimage_1-87](assets/chlimage_1-87.png)

## Publication du site {#publish-the-site}

![chlimage_1-88](assets/chlimage_1-88.png)

Dans la console [Sites](sites-console.md)de la communauté, sélectionnez l’icône Publier pour publier le site, par défaut sur http://localhost:4503.

## Ouvrez le site en mode d’édition sur l’auteur. {#open-the-site-on-author-in-edit-mode}

![chlimage_1-89](assets/chlimage_1-89.png)

Sélectionnez l&#39;icône d&#39;ouverture du site pour vue du site en mode d&#39;édition.

L’URL sera [http://localhost:4502/editor.html/content/sites/sample/en.html](http://localhost:4502/editor.html/content/sites/sample/en.html)

![chlimage_1-90](assets/chlimage_1-90.png)

Sur la page d&#39;accueil simple, il est possible de voir ce qui est précâblé à travers les fonctions et modèles de la communauté, et de jouer avec l&#39;ajout et la configuration des composants de la communauté.

## Site de Vue sur la publication {#view-site-on-publish}

Après avoir publié la page, ouvrez la page sur l’instance [de](http://localhost:4503/content/sites/sample/en.html) publication afin d’expérimenter les fonctionnalités en tant que visiteur de site anonyme, membre connecté ou administrateur. Le lien Administration visible dans l’environnement d’auteur n’apparaît pas dans l’environnement de publication, sauf si un administrateur se connecte.
