---
title: Utilisation du mode Mise en page pour redimensionner les composants des formulaires adaptatifs
description: 'Définissez la position des composants à l’aide de la grille réactive disponible en mode Mise en page '
feature: Formulaires adaptatifs
exl-id: 5cf76cb1-c92c-4aed-9945-37494fef2d29
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1047'
ht-degree: 75%

---

# Utilisation du mode Mise en page pour redimensionner des composants {#use-layout-mode-to-resize-components}

L’interface de création de formulaires adaptatifs vous permet de redimensionner les composants à l’aide du mode Mise en page . Faites glisser des points bleus dans les colonnes pour définir les points de début et de fin pour positionner les composants. Les points bleus s’affichent après avoir appuyé sur le composant dans la grille réactive. La grille réactive est composée de 12 colonnes égales. L’ombrage blanc et bleu différencie une colonne d’une l’autre.

Vous pouvez utiliser le mode Mise en page afin de redimensionner les composants pour tous les types d’appareils tels que les ordinateurs de bureau, les tablettes, les smartphones et d’autres appareils plus petits. La tablette dérive automatiquement la configuration de la disposition de la version de bureau. Les appareils plus petits dérivent la configuration de la disposition du téléphone. Vous pouvez toutefois remplacer les configurations dérivées automatiquement pour définir une configuration différente pour chaque type d’appareil.

## Accès au mode Mise en page {#access-layout-mode}

Sélectionnez **Mise en page** dans la liste déroulante qui s’affiche en haut de l’interface de création de formulaire adaptatif en regard de l’option **Aperçu** . Le formulaire s’affiche en mode Mise en page.

1. Connectez-vous à l’instance d’auteur AEM et accédez à **Adobe Experience Manager** > **Formulaires** > **Formulaires et documents**.
1. Créez un formulaire adaptatif [existant ou ouvrez-le.](../../forms/using/creating-adaptive-form.md)
1. Sélectionnez **Mise en page** dans la liste déroulante qui s’affiche en haut à côté de l’option **Prévisualiser**. Le formulaire s’affiche en mode Mise en page.

   ![Mode Mise en page](assets/layout_mode_ic_new.png)

## Redimensionner les composants {#resize-components}

1. En mode Mise en page, appuyez sur le composant pour le redimensionner. Les points bleus s’affichent au début et à la fin de la grille réactive.
1. Faites glisser les points bleus pour définir la position du composant dans la grille réactive.

   ![Redimensionnement en mode Mise en page](assets/layout_mode_resize_new_updated1.png)

   La barre d’outils qui s’affiche après avoir appuyé sur des composants comprend les options suivantes :

   * **[!UICONTROL Parent]** : permet de sélectionner le parent d’un composant.
   * **[!UICONTROL Rétablir la disposition des points d’arrêt]** : permet d’annuler toutes les modifications de redimensionnement et d’appliquer la disposition par défaut au composant.
   * **[!UICONTROL Flotter vers la nouvelle ligne]** : permet de placer le composant sur la ligne suivante s’il existe plusieurs composants dans une même ligne.

   Vous pouvez également utiliser l’option **[!UICONTROL Rétablir la disposition du point d’arrêt]** (![Rétablir le point d’arrêt](assets/reverttopreviouslypublishedversion.png)) au niveau du panneau pour annuler toutes les modifications de redimensionnement.

   >[!NOTE]
   >
   >Vous ne pouvez pas redimensionner les composants de colonne de tableau, de barre d’outils, de bouton de barre d’outils et de zone cible à l’aide du mode Mise en page. Utilisez le mode Style pour redimensionner ces composants.

### Exemple {#example}

**Objectif :** vous souhaitez insérer un composant de tableau et un composant Image et les placer l’un parallèlement à l’autre dans un formulaire adaptatif.

1. Insérez les composants de tableau et d’image à l’aide du mode d’édition dans le formulaire adaptatif. Le composant d’image s’affiche après le composant de tableau.
1. Passez en mode Mise en page et appuyez sur le composant Tableau. Les points bleus pour redimensionner le composant s’affichent aux colonnes 1 et 12.
1. Faites glisser le point bleu de la colonne 12 vers la colonne 6 de la grille réactive.

   ![Définition du point de fin du tableau](assets/layout_mode_end_point_table_new.png)

1. De même, sélectionnez le composant Image et faites glisser le point bleu de la colonne 1 vers la colonne 7 de la grille réactive. Les composants de tableau et d’image s’affichent en parallèle.

   ![Tableau et image en parallèle en mode Mise en page](assets/table_image_parallel_new.png)

   Vous pouvez sélectionner le composant d’image et appuyer sur l’option **Flotter jusqu’à la nouvelle ligne** disponible dans la barre d’outils pour déplacer le composant d’image vers la ligne suivante.

## Redimensionnement des panneaux {#resize-panels-layout-mode}

Effectuez les étapes suivantes si vous souhaitez redimensionner l’ensemble du panneau au lieu de composants distincts :

1. Appuyez sur l’un des composants du panneau à redimensionner, sélectionnez ![Sélectionner le parent](assets/select_parent_icon.svg), puis la première option dans la liste déroulante, si le panneau est le parent immédiat du composant.

   Les points bleus s’affichent au début et à la fin de la grille réactive.

1. Faites glisser les points bleus pour définir la position du panneau dans la grille réactive.
Vous pouvez répéter les étapes 1 et 2 et sélectionner ![Sélectionner le parent](assets/float_to_new_line_icon.svg) pour déplacer le panneau redimensionné vers la ligne suivante.

## Définition d’une mise en page à plusieurs colonnes pour un panneau

Pour définir le nombre de colonnes d’un panneau, procédez comme suit :

1. En mode **[!UICONTROL Édition]**, appuyez sur le panneau, sélectionnez ![Configurer](assets/configure_icon.png), puis **[!UICONTROL Réactif - tout sur la page sans navigation]** dans la liste déroulante **[!UICONTROL Disposition du panneau]**.

1. Appuyez sur ![Enregistrer](assets/save_icon.svg) pour enregistrer les propriétés.

1. En mode **[!UICONTROL Mise en page]**, appuyez sur l’un des composants du panneau, sélectionnez ![Sélectionner le parent](assets/select_parent_icon.svg), puis le panneau.

1. Appuyez sur ![plusieurs colonnes](assets/multi-column.svg) et sélectionnez le nombre de colonnes dans la liste déroulante. Le nombre de colonnes peut être compris entre 1 et 12. Le panneau est divisé en une mise en page à plusieurs colonnes.

![plusieurs colonnes en mode de mise en page](assets/multi-column-layout.png)

## Activation de la nouvelle grille réactive pour les anciennes dispositions réactives {#enableresponsivegrid}

Activez la nouvelle grille réactive pour les formulaires que vous créez à l’aide d’AEM Forms 6.4 ou d’une version inférieure pour redimensionner les composants.

>[!NOTE]
>
>Le passage à la nouvelle grille réactive ignore les propriétés de disposition déjà définies pour les composants utilisés dans le formulaire.

Pour activer la nouvelle grille réactive, procédez comme suit :

1. Sélectionnez **Mise en page** dans la liste déroulante qui s’affiche en haut à côté de l’option **Prévisualiser**. Une confirmation s’affiche pour activer le mode Mise en page.
1. Appuyez sur **Oui** pour activer le mode **Mise en page** pour le formulaire.

### Incorporation d’un ancien fragment dans un formulaire adaptatif avec une nouvelle disposition réactive {#embed-an-old-fragment-in-an-adaptive-form-with-new-responsive-layout}

La nouvelle disposition réactive du formulaire adaptatif vous permet d’ajouter au formulaire un fragment de formulaire adaptatif avec l’ancienne disposition réactive. La nouvelle disposition ignore toutefois les propriétés de disposition déjà définies pour les composants utilisés dans le fragment. Vous pouvez passer en mode Mise en page pour définir les propriétés de disposition des composants utilisés dans le fragment.

### Incorporer un fragment avec une nouvelle mise en page réactive dans un ancien formulaire adaptatif {#embed-a-fragment-with-new-responsive-layout-in-an-old-adaptive-form}

Si vous incorporez un fragment avec la nouvelle mise en page réactive dans un formulaire adaptatif avec une ancienne mise en page réactive, le système vous invite à activer le mode Mise en page pour le formulaire et à réincorporer le fragment.

Pour activer le mode Mise en page, sélectionnez **Mise en page** dans la liste déroulante qui s’affiche en haut à côté de l’option **Prévisualiser** et appuyez sur **Oui** pour confirmer. Sélectionnez le mode **Édition** pour réincorporer le fragment.

## Désactivation du mode Mise en page pour les formulaires avec une ancienne disposition réactive {#disable-layout-mode-for-forms-with-old-responsive-layout}

Vous pouvez désactiver le mode Mise en page pour les formulaires avec une ancienne disposition réactive en modifiant les propriétés du modèle utilisé dans le formulaire.

Pour désactiver le mode Mise en page, procédez comme suit :

1. Sélectionnez **[!UICONTROL Outils]** > **[!UICONTROL Général]** > **[!UICONTROL Modèles]** et ouvrez le modèle utilisé dans le formulaire en mode **[!UICONTROL Édition]**.
1. Sélectionnez le conteneur de documents dans le volet de gauche et appuyez sur **[!UICONTROL Stratégie.]**

   ![Désactivation du mode Mise en page](assets/policy_disable_layout_mode.png)

1. Appuyez sur l’onglet **[!UICONTROL Paramètres de mise en page]** et sélectionnez **[!UICONTROL Désactiver le mode Mise en page]**.
1. Appuyez sur ![Enregistrer](assets/save_icon.png) pour enregistrer les propriétés.
