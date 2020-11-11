---
title: Utiliser le mode Mise en page pour redimensionner les composants pour la communication interactive
description: 'Définir la position des composants à l’aide de la grille réactive disponible en mode Mise en page '
translation-type: tm+mt
source-git-commit: c62ad355469a95db89db44c34bb6df72d8f4bf77
workflow-type: tm+mt
source-wordcount: '867'
ht-degree: 2%

---


# Utiliser le mode Mise en page pour redimensionner les composants {#use-layout-mode-to-resize-components}

L&#39;interface de création de canal Web Interactive Communication vous permet de redimensionner des composants en mode Mise en page. Faites glisser des points bleus dans les colonnes pour définir le début et les points d’extrémité à positionner les composants. Les points bleus s’affichent après avoir appuyé sur le composant dans la grille réactive. La grille réactive est composée de 12 colonnes égales. L’ombrage blanc et bleu des autres colonnes différencie une colonne de l’autre.

Vous pouvez utiliser le mode Mise en page pour redimensionner les composants pour tous les types de périphériques, tels que les ordinateurs de bureau, tablettes, smartphones et autres périphériques plus petits. La tablette dérive automatiquement la configuration de la mise en page de la version de bureau et les périphériques plus petits dérivent la configuration de la mise en page de la version de téléphone. Cependant, vous pouvez remplacer les configurations dérivées automatiquement pour définir une configuration différente pour chaque type de périphérique.

>[!NOTE]
>
>Si vous créez le canal Web à l’aide du canal [Imprimer en tant que gabarit](../../forms/using/create-interactive-communication.md) pour une communication interactive, les composants disponibles pour le redimensionnement incluent également les sous-formulaires et les champs qui sont générés automatiquement dans le canal Web à l’aide du canal Imprimer. Le canal Web conserve la mise en page des éléments du canal Imprimer en mode Mise en page.

## Accès au mode Mise en page {#access-layout-mode}

Sélectionnez **Mise en page** dans la liste déroulante qui s’affiche en haut de l’interface de création Interactive Communication en regard de l’option **Prévisualisation** . Le formulaire s’affiche en mode Mise en page.

1. Connectez-vous à l’instance d’auteur AEM et accédez à **Adobe Experience Manager** > **Formulaires** > **Formulaires et documents**.
1. Créez ou ouvrez une communication [](../../forms/using/create-interactive-communication.md)interactive existante.
1. Sélectionnez **Disposition** dans la liste déroulante qui s’affiche en haut à côté de l’option **Prévisualisation** . Le formulaire s’affiche en mode Mise en page.

   ![Mode de mise en page pour les communications interactives](assets/layout_mode_ic_new.png)

## Redimensionnement des composants {#resize-components}

1. En mode Mise en page, appuyez sur le composant pour le redimensionner. Les points bleus s’affichent en début et à la fin de la grille réactive.
1. Faites glisser les points bleus pour définir la position du composant dans la grille réactive.

   ![Redimensionnement en mode Mise en page](assets/layout_mode_resize_new_updated.png)

   La barre d’outils qui s’affiche après avoir appuyé sur des composants comprend les options suivantes :

   * **Parent :** Sélectionnez le parent d’un composant.
   * **Flotter vers la nouvelle ligne :** Déplacez le composant vers la ligne suivante s’il existe plusieurs composants dans la même ligne.

   Vous pouvez annuler toutes les modifications de redimensionnement et appliquer la mise en page par défaut au panneau contenant des composants redimensionnés à l’aide de l’option **[!UICONTROL Rétablir la mise en page]** du point d’arrêt ( ![Rétablir le point d’arrêt](assets/reverttopreviouslypublishedversion.png)). Appuyez sur le parent du composant redimensionné pour vue à l’option.

   >[!NOTE]
   >
   >Vous ne pouvez pas redimensionner les composants de colonne de tableau, de barre d’outils, de bouton de barre d’outils et de zone de cible à l’aide du mode Disposition. Utilisez le mode Style pour redimensionner ces composants.

### Exemple {#example}

**Objectif :** Vous souhaitez insérer un composant de tableau et un composant d’image et les positionner en parallèle dans une communication interactive.

1. Insérez le tableau et les composants d’image en mode Edition dans le canal Web d’une communication interactive. Le composant d’image s’affiche après le composant de tableau.
1. Passez en mode Mise en page et appuyez sur le composant Tableau. Les points bleus pour redimensionner le composant s’affichent aux colonnes 1 et 12.
1. Faites glisser le point bleu de la colonne 12 vers la colonne 6 de la grille réactive.

   ![Définir le point de fin du tableau](assets/layout_mode_end_point_table_new.png)

1. De même, sélectionnez le composant Image et faites glisser le point bleu de la colonne 1 vers la colonne 7 de la grille dynamique. Les composants de tableau et d’image s’affichent en parallèle.

   ![Tableau et image en parallèle en mode Disposition](assets/table_image_parallel_new.png)

   Vous pouvez sélectionner le composant Image et appuyer sur l’option **Flotter sur la nouvelle ligne** disponible dans la barre d’outils pour déplacer le composant Image vers la ligne suivante.

## Redimensionnement des panneaux {#resize-panels-layout-mode}

Exécutez les étapes suivantes si vous souhaitez redimensionner l’ensemble du panneau au lieu de composants individuels :

1. Appuyez sur l’un des composants du panneau à redimensionner, sélectionnez ![Sélectionner le parent](assets/select_parent_icon.svg)et sélectionnez la première option dans la liste déroulante, si le panneau est le parent immédiat du composant.

   Les points bleus s’affichent en début et à la fin de la grille réactive.

1. Faites glisser les points bleus pour définir la position du panneau dans la grille réactive.
Vous pouvez répéter les étapes 1 et 2 et sélectionner ![Sélectionner le parent](assets/float_to_new_line_icon.svg) pour déplacer le panneau redimensionné sur la ligne suivante.

## Définition de la disposition à plusieurs colonnes pour un panneau

Exécutez les étapes suivantes pour définir le nombre de colonnes d’un panneau :

1. En mode **[!UICONTROL Edition]** , appuyez sur le panneau, sélectionnez ![Configurer](assets/configure_icon.png), puis sélectionnez **[!UICONTROL Réactif - tout sur la page sans option de navigation]** dans la liste déroulante Disposition du **[!UICONTROL panneau.]**

1. Appuyez sur ![Save](assets/save_icon.svg) (Enregistrer) pour enregistrer les propriétés.

1. En mode **[!UICONTROL Mise en page]** , appuyez sur l’un des composants du panneau, sélectionnez ![Sélectionner un parent](assets/select_parent_icon.svg), puis sélectionnez le panneau.

1. Appuyez sur ![plusieurs colonnes](assets/multi-column.svg) et sélectionnez le nombre de colonnes dans la liste déroulante. Le nombre de colonnes peut être compris entre 1 et 12. Le panneau est divisé en plusieurs colonnes.

![plusieurs colonnes en mode de mise en page](assets/multi-column-layout.png)

## Désactiver le mode de mise en page pour les formulaires avec une ancienne mise en page réactive {#disable-layout-mode-for-forms-with-old-responsive-layout}

Vous pouvez désactiver le mode Disposition pour les formulaires dotés d’une ancienne disposition réactive en modifiant les propriétés du modèle utilisé dans le formulaire.

Pour désactiver le mode Disposition, procédez comme suit :

1. Sélectionnez **[!UICONTROL Outils]** > **[!UICONTROL Général]** > **[!UICONTROL Modèles]** et ouvrez le modèle utilisé dans le formulaire en mode **[!UICONTROL Modifier.]**
1. Sélectionnez le Conteneur de Document dans le volet de gauche et appuyez sur **[!UICONTROL Stratégie.]**

   ![Désactiver le mode de mise en page](assets/policy_disable_layout_mode.png)

1. Appuyez sur l’onglet Paramètres **[!UICONTROL de]** mise en page et sélectionnez **[!UICONTROL Désactiver le mode]** de mise en page.
1. Tap ![Save changes](assets/save_icon.png) to save the template properties.

