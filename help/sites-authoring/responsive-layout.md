---
title: Mise en page réactive pour vos pages de contenu
description: Adobe Experience Manager vous propose des fonctionnalités de mise en page réactive à l’aide du composant Conteneur de mise en page.
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: page-authoring
content-type: reference
exl-id: 760b8419-5cf8-49c5-8d4f-6691f5256c53
solution: Experience Manager, Experience Manager Sites
feature: Authoring
role: User,Admin,Developer
source-git-commit: c77849740fab51377ce60aff5f611e0408dca728
workflow-type: tm+mt
source-wordcount: '1853'
ht-degree: 100%

---


# Disposition réactive{#responsive-layout}

Adobe Experience Manager vous permet de créer une disposition réactive à l’aide du composant **Conteneur de disposition**.

>[!TIP]
>
>Ce document présente une vue d’ensemble des fonctionnalités du conteneur de mise en page disponibles pour la création de contenu.
>
>Pour l’administration et le développement de vos sites, les détails de configuration du conteneur de mise en page sont décrits dans le document [Configuration du conteneur de mise en page et du mode Mise en page](/help/sites-authoring/responsive-layout.md).

## Vue d’ensemble {#overview}

Le composant **Conteneur de mise en page** offre un système de paragraphe qui permet de positionner des composants sur une grille réactive. Cette grille peut réorganiser la disposition en fonction de la taille et du format de la fenêtre/l’appareil. Le composant est utilisé avec le [**mode Disposition**](/help/sites-authoring/responsive-layout.md#defining-layouts-layout-mode), ce qui permet de créer et de modifier votre disposition réactive en fonction de l’appareil.

Le conteneur de mise en page :

* Permet un alignement horizontal sur la grille, ainsi que la possibilité de placer côte à côte les composants dans la grille et de définir quand ils doivent être réduits/développés.
* Il utilise des points d’arrêt prédéfinis (par exemple, pour le téléphone, la tablette, etc.) vous permettant de définir le comportement requis du contenu pour l’orientation/les appareils associés.

   * Par exemple, vous pouvez personnaliser la taille du composant ou décider s’il peut être affiché sur des appareils spécifiques.

* Peut être imbriqué pour permettre le contrôle des colonnes.

L’utilisateur ou l’utilisatrice peut ensuite afficher le rendu du contenu pour des appareils spécifiques à l’aide de l’émulateur.

>[!CAUTION]
>
>Bien que le composant conteneur de mise en page soit disponible dans l’IU classique, il n’est entièrement fonctionnel et pris en charge que dans l’interface utilisateur optimisée pour les écrans tactiles.

AEM effectue une mise en page réactive de vos pages en combinant plusieurs mécanismes :

* Composant [**Conteneur de mise en page**](#adding-a-layout-container-and-its-content-edit-mode)

  Ce composant, qui est disponible dans l’[explorateur de composants](/help/sites-authoring/author-environment-tools.md#components-browser), fournit un système de paragraphes/grille qui permet d’ajouter et de positionner des composants dans une grille réactive. Il peut également être défini comme le système de paragraphes par défaut de votre page.

* [**Mode Mise en page**](/help/sites-authoring/responsive-layout.md#defining-layouts-layout-mode)

  Une fois que le conteneur de disposition est positionné sur la page, vous pouvez utiliser le mode **Disposition** pour placer le contenu dans la grille réactive.

* [**Émulateur**](#selecting-a-device-to-emulate)
Vous pouvez ainsi créer et modifier des sites web réactifs qui réorganisent la disposition en fonction de la taille de l’appareil ou de la fenêtre en redimensionnant les composants de manière interactive. L’utilisateur ou l’utilisatrice peut alors voir comment le contenu est rendu à l’aide de l’émulateur.

Grâce à ces mécanismes de grille réactive, vous pouvez :

* utiliser des points d’arrêt pour définir différentes mises en page de contenu en fonction de la largeur de l’appareil (selon le type et l’orientation de l’appareil) ;
* utiliser ces points d’arrêt et les mises en page de contenu pour veiller à ce que le contenu s’ajuste à la taille de la fenêtre du navigateur sur le poste de travail ;
* utiliser l’alignement horizontal sur la grille, ce qui permet de placer les composants dans la grille, de les redimensionner selon les besoins et de définir quand ils doivent être réduits ou développés pour être côte à côte ou l’un au-dessus de l’autre ;
* masquer des composants pour des mises en page spécifiques à certains appareils ;
* contrôler les colonnes.

En fonction de votre projet, le conteneur de mise en page peut être utilisé en tant que système de paragraphes par défaut pour vos pages ou en tant que composant pouvant être ajouté à votre page via l’explorateur de composants (ou les deux).

>[!NOTE]
>
>Adobe propose une [documentation GitHub](https://adobe-marketing-cloud.github.io/aem-responsivegrid/) sur la disposition réactive. Celle-ci peut servir de référence et être distribuée aux équipes de développement d’applications front-end pour leur permettre d’utiliser la grille AEM en dehors d’AEM, par exemple lors de la création de maquettes HTML statiques pour un site AEM en préparation.

>[!NOTE]
>
>L’utilisation des mécanismes ci-dessus est activée par une configuration du modèle. Pour plus d’informations, consultez la section [Configuration d’une mise en page réactive](/help/sites-administering/configuring-responsive-layout.md).

## Définitions de mise en page, émulation d’appareil et points d’arrêt {#layout-definitions-device-emulation-and-breakpoints}

Lorsque vous créez le contenu de votre site web, vous voulez être certain que celui-ci sera affiché correctement sur l’appareil utilisé pour le consulter :

Dans AEM, vous pouvez définir des dispositions qui dépendent de la largeur de l’appareil :

* L’émulateur vous permet d’émuler ces mises en page sur divers appareils. Tout comme le type d’appareil, l’orientation, qui est sélectionnée à l’aide de l’option **Rotation du périphérique**, peut avoir une incidence sur le point d’arrêt sélectionné lors du changement de largeur.
* Les points d’arrêt sont des points qui séparent les définitions de mise en page.

   * Ils définissent la largeur maximale (en pixels) de n’importe quel appareil à l’aide d’une mise en page spécifique.
   * Les points d’arrêt sont généralement valides pour plusieurs appareils en fonction de la largeur de leur écran.
   * La plage d’un point d’arrêt s’étend sur la gauche, jusqu’au point d’arrêt suivant.
   * Vous ne pouvez pas sélectionner le point d’arrêt. La sélection de l’appareil et de l’orientation permet de sélectionner automatiquement le point d’arrêt adéquat.

L’appareil **Bureau**, qui ne possède pas de largeur spécifique, est associé au point d’arrêt par défaut (c’est-à-dire tout ce qui se trouve au-dessus du dernier point d’arrêt configuré).

>[!NOTE]
>
>Il est possible de définir des points d’arrêt pour chaque appareil, mais cela augmenterait la charge de travail requise pour la définition des mises en page et la maintenance.

Lors de l’utilisation de l’émulateur, vous sélectionnez un appareil spécifique pour l’émulation et la définition de mise en page. Le point d’arrêt associé est également mis en surbrillance. Toute modification de disposition que vous apportez est applicable aux autres appareils auxquels s’applique le point d’arrêt, c’est-à-dire aux appareils situés à gauche du marqueur de point d’arrêt actif, mais avant le marqueur de point d’arrêt suivant.

Par exemple, lorsque vous sélectionnez l’appareil **iPhone 6 Plus** (défini avec une largeur de 540 pixels) pour l’émulation et la mise en page, le point d’arrêt **Téléphone** (défini sur 768 pixels) est également activé. Toutes les modifications apportées à la mise en page pour l’**iPhone 6** s’appliquent aux autres appareils sous le point d’arrêt **Téléphone**, tel que l’**iPhone 5** (défini sur 320 pixels).

![screen_shot_2018-03-23at084058](assets/screen_shot_2018-03-23at084058.png)

## Sélection d’un appareil à émuler {#selecting-a-device-to-emulate}

1. Ouvrez la page requise en vue de la modifier. Par exemple :

   `http://localhost:4502/editor.html/content/we-retail/us/en/experience.html`

1. Sélectionnez l’icône **Émulateur** dans la barre d’outils supérieure :

   ![Émulateur](do-not-localize/screen_shot_2018-03-23at084256.png)

1. La barre d’outils de l’émulateur s’ouvre.

   ![screen_shot_2018-03-23at084551](assets/screen_shot_2018-03-23at084551.png)

   La barre d’outils de l’émulateur affiche des options de mise en page supplémentaires :

   * **Rotation de l’appareil** : permet de faire pivoter un appareil de l’orientation verticale (portrait) à l’orientation horizontale (paysage), et inversement.

     ![Rotation de l’appareil](do-not-localize/screen_shot_2018-03-23at084612.png) ![Rotation de l’appareil](do-not-localize/screen_shot_2018-03-23at084637.png)

   * **Sélectionner un appareil** : permet de sélectionner un appareil spécifique à émuler dans une liste (pour plus d’informations, voir l’étape suivante).

     ![Sélectionner un appareil](do-not-localize/screen_shot_2018-03-23at084743.png)

1. Pour sélectionner un appareil spécifique à émuler, vous pouvez effectuer l’une des opérations suivantes :

   * utiliser l’icône Sélectionner un périphérique et sélectionner l’appareil dans la liste déroulante ;
   * cliquer sur l’indicateur de l’appareil dans la barre d’outils de l’émulateur.

   ![screen_shot_2018-03-23at084818](assets/screen_shot_2018-03-23at084818.png)

1. Une fois un appareil spécifique sélectionné, vous pouvez visualiser les éléments suivants :

   * Marqueurs actifs de l’appareil sélectionné (**iPad**, par exemple).
   * Marqueurs actifs du [point d’arrêt](/help/sites-authoring/responsive-layout.md#layout-definitions-device-emulation-and-breakpoints) approprié (**Tablette**, par exemple).

   ![screen_shot_2018-03-23at084932](assets/screen_shot_2018-03-23at084932.png)

   * La ligne pointillée bleue représente le *pli* pour l’appareil sélectionné (ici, **iPhone 6**).

   ![screen_shot_2018-03-23at084947](assets/screen_shot_2018-03-23at084947.png)

   * Le pli peut également être considéré comme un saut de ligne de page (à ne pas confondre avec les [points d’arrêt](/help/sites-authoring/responsive-layout.md#layout-definitions-device-emulation-and-breakpoints)) pour le contenu. Il est affiché à des fins pratiques pour indiquer la partie du contenu que l’utilisateur ou l’utilisatrice verra sur l’appareil avant de faire défiler l’écran.
   * La ligne du pli ne s’affiche pas si la hauteur de l’appareil émulé est supérieure à la taille de l’écran.
   * Le pli est affiché pour faciliter le travail de l’auteur et n’apparaît pas sur la page publiée.

## Ajout d’un conteneur de mise en page et de son contenu (mode d’édition) {#adding-a-layout-container-and-its-content-edit-mode}

Un **conteneur de mise en page** est un système de paragraphes qui présente les caractéristiques suivantes :

* Il contient d’autres composants.
* Il définit la mise en page.
* Il répond aux modifications.

>[!NOTE]
>
>S’il n’est pas déjà disponible, le **conteneur de mise en page** doit être explicitement [activé pour un système de paragraphes ou une page](/help/sites-administering/configuring-responsive-layout.md) (en utilisant le mode de [**conception**, par exemple](/help/sites-authoring/default-components-designmode.md)).

1. Le **conteneur de mise en page** est disponible en tant que composant standard dans l’[explorateur de composants](/help/sites-authoring/author-environment-tools.md#components-browser). De là, vous pouvez le faire glisser vers l’emplacement souhaité sur la page, après lequel vous verrez l’espace réservé **Faire glisser les composants ici**.
1. Vous pouvez ensuite ajouter des composants au conteneur de mise en page, qui contiendront le contenu proprement dit :

   ![screen_shot_2018-03-23at085500](assets/screen_shot_2018-03-23at085500.png)

## Sélection et exécution d’une action sur un conteneur de mise en page (mode d’édition) {#selecting-and-taking-action-on-a-layout-container-edit-mode}

À l’instar des autres composants, vous pouvez sélectionner un conteneur de mise en page, puis effectuer une opération (couper, copier, supprimer) sur ce dernier (en mode d’**édition**) :

>[!CAUTION]
>
>Un conteneur de mise en page étant un système de paragraphes, la suppression du composant entraîne la suppression de la grille de mise en page et de tous les composants (ainsi que de leur contenu) qu’il contient.

1. Si vous pointez ou sélectionnez l’espace réservé de la grille, le menu d’actions s’affiche.

   ![screen_shot_2018-03-23at085357](assets/screen_shot_2018-03-23at085357.png)

   Vous devez sélectionner l’option **Parent**.

   ![Option parent](do-not-localize/screen_shot_2018-03-23at085417.png)

1. Si le composant de mise en page est imbriqué, la sélection de l’option **Parent** présente une sélection déroulante, ce qui vous permet de sélectionner le conteneur de mise en page imbriqué ou ses parents.

   Lorsque vous placez le pointeur de la souris sur les noms de conteneurs dans la liste déroulante, leurs contours s’affichent sur la page.

   * Les contours du conteneur de mise en page imbriqué le plus bas s’affichent en noir.
   * Le prochain conteneur de mise en page imbriqué le plus bas s’affiche en gris foncé.
   * Les contours de chaque conteneur successif s’affichent dans une nuance plus claire de gris.

   ![screen_shot_2018-03-23at085636](assets/screen_shot_2018-03-23at085636.png)

1. Cette opération sélectionne l’ensemble de la grille avec son contenu. La barre d’outils d’actions s’affiche. Vous pouvez alors sélectionner une action comme **Supprimer**.

   ![screen_shot_2018-03-23at085724](assets/screen_shot_2018-03-23at085724.png)

## Définition des mises en page (mode Mise en page) {#defining-layouts-layout-mode}

>[!NOTE]
>
>Vous pouvez définir une mise en page distincte pour chaque [point d’arrêt](#layout-definitions-device-emulation-and-breakpoints) (déterminée par l’orientation et le type d’appareil émulé).

Pour configurer la mise en page d’une grille réactive mise en œuvre avec le conteneur de mise en page, vous devez utiliser le mode **Mise en page**.

Le mode **Mise en page** peut être activé de deux façons.

* À l’aide du [menu de mode de la barre d’outils](/help/sites-authoring/author-environment-tools.md#page-modes), en sélectionnant le mode **Mise en page**.

   * Sélectionnez le mode **Mise en page** de la même façon que vous passeriez en mode **Édition** ou en mode **Ciblage**.
   * Le mode **Mise en page** est un **mode** persistant, ce qui signifie qu’il reste sélectionné jusqu’à ce que vous choisissiez un autre mode à l’aide du sélecteur de mode.

* Lors de la [modification d’un composant individuel.](/help/sites-authoring/editing-content.md#edit-component-layout)

   * En utilisant l’option **Mise en page** dans le menu d’action rapide du composant, vous pouvez passer au mode **Mise en page**.
   * Le mode **Mise en page** persiste pendant la modification du composant et bascule vers le mode **Édition** lorsqu’un autre composant est sélectionné.

Une fois le mode Mise en page sélectionné, vous pouvez effectuer diverses actions sur une grille :

* Redimensionnez les composants de contenu à l’aide des points bleus. Le redimensionnement s’accroche toujours à la grille. Lors du redimensionnement, la grille d’arrière-plan s’affiche pour faciliter l’alignement :

  ![screen_shot_2018-03-23at090140](assets/screen_shot_2018-03-23at090140.png)

  >[!NOTE]
  >
  >Les proportions et les rapports sont conservés lorsque des composants, tels que des **images**, sont redimensionnés.

* Cliquez ou appuyez sur un composant de contenu. La barre d’outils propose les options suivantes :

   * **Parent**

     Permet de sélectionner l’intégralité du composant Conteneur de disposition pour effectuer une opération.

   * **Flotter sur une nouvelle ligne**

     Le composant est déplacé vers une nouvelle ligne selon l’espace disponible dans la grille.

   * **Masquer le composant**

     Le composant devient invisible (il peut être restauré à partir de la barre d’outils du conteneur de mise en page).

  ![screen_shot_2018-03-23at090246](assets/screen_shot_2018-03-23at090246.png)

* En mode **Disposition**, appuyez ou cliquez sur **Faire glisser les composants ici** pour sélectionner l’intégralité du composant. La barre d’outils de ce mode s’affiche.

  La barre d’outils propose différentes options en fonction de l’état du composant de mise en page et des composants qui lui sont associés. Par exemple :

   * **Parent** : permet de sélectionner le composant parent.

     ![Parent](do-not-localize/screen_shot_2018-03-23at090823.png)

   * **Afficher les composants masqués** - Affiche tous les composants, ou individuellement certains composants. Ce nombre indique le nombre actuel de composants masqués. Le compteur indique le nombre de composants masqués.

     ![Afficher les composants masqués](do-not-localize/screen_shot_2018-03-23at091007.png)

   * **Rétablir la disposition du point d’arrêt** : rétablit la disposition par défaut. Cela signifie qu’aucune disposition personnalisée ne sera imposée.

     ![Rétablir la disposition du point d’arrêt](do-not-localize/screen_shot_2018-03-23at091013.png)

   * **Flotter sur une nouvelle ligne** : déplace le composant d’une position vers le haut si l’espace est suffisant.

     ![screen_shot_2018-03-23at090829](assets/screen_shot_2018-03-23at090829.png)

   * **Masquer le composant** : masque le composant actif.

     ![Masquer le composant](do-not-localize/screen_shot_2018-03-23at090834.png)

     >[!NOTE]
     >
     >Dans l’exemple ci-dessus, les actions de flottement et de masquage sont disponibles, car ce conteneur de mise en page est imbriqué dans un conteneur de mise en page parent.

   * **Afficher les composants**
Sélectionnez les composants parents pour afficher la barre d’outils comportant l’option **Afficher les composants masqués**. Dans cet exemple, deux composants sont masqués.

     ![screen_shot_2018-03-23at091200](assets/screen_shot_2018-03-23at091200.png)

  Si vous sélectionnez l’option **Afficher les composants masqués**, les composants actuellement masqués s’affichent en bleu à leur position initiale.

  ![screen_shot_2018-03-23at091224](assets/screen_shot_2018-03-23at091224.png)

  Sélectionnez **Restaurer tout** pour afficher tous les composants masqués.
