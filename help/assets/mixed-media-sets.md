---
title: Visionneuses de médias mixtes
description: Découvrez comment travailler avec des visionneuses de médias mixtes dans Dynamic Media.
uuid: cecad772-ed05-46f6-ba44-107195866b0d
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
discoiquuid: ed84157a-e6b4-4dde-af2e-a1e0b6259628
docset: aem65
feature: Visionneuses de médias mixtes, Gestion des ressources
role: User, Admin
exl-id: 70a72fb9-a289-4eda-abcc-300edf9f1961
source-git-commit: 363e5159d290ecfbf4338f6b9793e11b613389a5
workflow-type: tm+mt
source-wordcount: '1464'
ht-degree: 53%

---

# Visionneuses de médias mixtes{#mixed-media-sets}

Une visionneuse de médias mixtes permet d’offrir un mélange d’images, de visionneuses d’images, de visionneuses à 360° et de vidéos dans une même présentation.

Les visionneuses de médias mixtes sont désignées par une bannière contenant les mots **[!UICONTROL Visionneuse de médias mixtes]**. En outre, si la visionneuse de médias mixtes est publiée, la date de publication, indiquée par l’icône représentant la **[!UICONTROL Terre]**, figure sur la bannière avec la date de dernière modification, indiquée par l’icône représentant un **[!UICONTROL crayon]**.

![chlimage_1-137](assets/chlimage_1-348.png)

>[!NOTE]
>
>Pour plus d’informations sur l’interface utilisateur d’Assets, voir [Gestion des ressources](/help/assets/manage-assets.md).

## Démarrage rapide : Visionneuses de médias mixtes {#quick-start-mixed-media-sets}

Pour démarrer rapidement, procédez comme suit :

1. [Chargez vos ressources](#uploading-assets).

   Commencez par charger les images et les vidéos pour les visionneuses de médias mixtes. Le cas échéant, créez les [Visionneuses d’images](/help/assets/image-sets.md) et [Visionneuses à 360°](/help/assets/spin-sets.md). Comme les utilisateurs peuvent zoomer sur les images dans la visionneuse de médias mixtes, choisissez les images avec soin. Assurez-vous que les images font au moins 2 000 pixels dans leur dimension la plus grande.

1. [Créez une visionneuse de médias mixtes](#creating-mixed-media-sets).

   Pour créer une visionneuse de médias mixtes, dans la page Ressources, sélectionnez **[!UICONTROL Créer]** > **[!UICONTROL Visionneuse de médias mixtes]**, puis attribuez un nom à la visionneuse, sélectionnez les ressources et choisissez l’ordre dans lequel doivent apparaître les images.

   Voir [Utilisation de sélecteurs](/help/assets/working-with-selectors.md).

1. Configurez des [paramètres prédéfinis de visionneuse de médias mixtes](/help/assets/managing-viewer-presets.md), suivant les besoins.

   Les administrateurs peuvent créer ou modifier les paramètres prédéfinis de visionneuse de médias mixtes. Pour afficher votre visionneuse de médias mixtes avec un paramètre prédéfini, sélectionnez la visionneuse puis, dans le menu contextuel du rail gauche, sélectionnez **[!UICONTROL Visionneuses]**.

   Pour créer ou modifier des paramètres prédéfinis de visionneuse, voir **[!UICONTROL Outils]** > **[!UICONTROL Ressources]** > **[!UICONTROL Paramètre prédéfini de visionneuse]**.

   Voir [Ajout et modification de paramètres de visionneuse prédéfinis](/help/assets/managing-viewer-presets.md).

1. [Prévisualisez une visionneuse de médias mixtes](#previewing-mixed-media-sets).

   Sélectionnez la visionneuse de médias mixtes pour pouvoir la prévisualiser. Sélectionnez les icônes des miniatures afin d’examiner votre visionneuse de médias mixtes dans la visionneuse sélectionnée. Vous pouvez choisir différentes visionneuses dans le menu **[!UICONTROL Visionneuses]** disponible dans le menu déroulant du rail gauche.

1. [Publiez une visionneuse de médias mixtes](#publishing-mixed-media-sets).

   La publication d’une visionneuse de médias mixtes active la chaîne URL et d’incorporation. Vous devez, en outre, [publier le paramètre prédéfini de la visionneuse](/help/assets/managing-viewer-presets.md#publishing-viewer-presets).

1. [Liez des URL à l’application web](/help/assets/linking-urls-to-yourwebapplication.md) ou [incorporez la vidéo ou la visionneuse d’images](/help/assets/embed-code.md).

   Adobe Experience Manager Assets crée des appels URL pour les visionneuses de médias mixtes et les active une fois que vous avez publié les visionneuses. Vous pouvez copier ces URL lorsque vous prévisualisez les ressources. Vous pouvez également les incorporer à votre site web.

   Sélectionnez la visionneuse de médias mixtes puis, dans le menu déroulant du rail gauche, sélectionnez **[!UICONTROL Visionneuses]**.

   Voir [Liaison d’une visionneuse de médias mixtes à une page web](/help/assets/linking-urls-to-yourwebapplication.md) et [Incorporation de la visionneuse de vidéos ou d’images](/help/assets/embed-code.md).

Si nécessaire, vous pouvez modifier les [Visionneuses de médias mixtes](#editing-mixed-media-sets). Vous pouvez, en outre, afficher et modifier les [propriétés de la visionneuse de médias mixtes](/help/assets/manage-assets.md#editing-properties).

>[!NOTE]
>
>Si vous rencontrez des problèmes lors de la création des visionneuses, voir [Dépannage de Dynamic Media - mode Scene7](/help/assets/troubleshoot-dms7.md).

## Télécharger les éléments {#uploading-assets}

Commencez par charger les images et les vidéos pour les visionneuses de médias mixtes. Comme les utilisateurs peuvent zoomer sur les images dans la visionneuse de médias mixtes, choisissez les images avec soin. Assurez-vous que les images font au moins 2 000 pixels dans leur dimension la plus grande.

En outre, si vous souhaitez ajouter des visionneuses à 360° ou d’images à la visionneuse de supports variés, créez également ces visionneuses.

## Création d’une visionneuse de médias mixtes {#creating-mixed-media-sets}

Vous pouvez ajouter des images, des visionneuses d’images, des visionneuses à 360° et des vidéos à votre visionneuse de médias mixtes. Assurez-vous que les fichiers, visionneuses d’images et visionneuses à 360° sont prêts pour la publication avant de les ajouter à la visionneuse de médias mixtes.

Lorsque vous ajoutez des ressources à votre visionneuse, elles sont automatiquement ajoutées dans l’ordre alphanumérique. Vous pouvez réorganiser ou trier manuellement les ressources après les avoir ajoutées.

**Création d’une visionneuse de médias mixtes:**

1. Dans Assets, accédez à l’emplacement où vous souhaitez créer une visionneuse de médias mixtes, sélectionnez **[!UICONTROL Créer]**, puis **[!UICONTROL Visionneuse de médias mixtes]**. Vous pouvez également la créer depuis un dossier qui contient les ressources. L’éditeur de visionneuse de médias mixtes s’affiche.

   ![chlimage_1-138](assets/chlimage_1-349.png)

1. Dans le **[!UICONTROL Titre]** de la visionneuse de médias mixtes, saisissez un nom pour la visionneuse. Le nom apparaît dans la bannière située sur la visionneuse de médias mixtes. Vous pouvez aussi saisir une description.

   ![chlimage_1-139](assets/chlimage_1-350.png)

   >[!NOTE]
   >
   >Lors de la création de la visionneuse de médias mixtes, vous pouvez modifier la miniature de la visionneuse ou permettre à Experience Manager de sélectionner la miniature automatiquement en fonction des ressources de la visionneuse de médias mixtes. Pour sélectionner une miniature, sélectionnez **[!UICONTROL Modifier la miniature]** et sélectionnez une image (vous pouvez également accéder à d’autres dossiers pour rechercher des images). Si vous avez sélectionné une miniature, puis décidez que vous souhaitez que Experience Manager en génère une à partir de la visionneuse de médias mixtes, sélectionnez **[!UICONTROL Basculer vers la miniature automatique]**.

1. Sélectionnez le sélecteur de ressources pour sélectionner les ressources à inclure dans votre visionneuse de médias mixtes. Sélectionnez-les, puis sélectionnez **[!UICONTROL Sélectionner]**.

   Le sélecteur de ressources vous permet de rechercher des ressources en saisissant un mot-clé, puis en appuyant sur **[!UICONTROL Retour]**. Vous pouvez également appliquer des filtres pour affiner vos résultats de recherche. Vous pouvez filtrer par chemin, collection, type de fichier et balise. Sélectionnez le filtre, puis sélectionnez l’icône **[!UICONTROL Filtre]** dans la barre d’outils. Modifiez l’affichage en sélectionnant l’icône **[!UICONTROL Afficher]** et en choisissant ensuite le mode **[!UICONTROL Liste]**, **[!UICONTROL Colonnes]** ou **[!UICONTROL Carte]**.

   Voir [Utilisation de sélecteurs](/help/assets/working-with-selectors.md).

   ![chlimage_1-140](assets/chlimage_1-383.png)

1. Réorganisez les ressources en les faisant glisser vers le haut ou le bas de la liste (sélectionnez l’icône de **[!UICONTROL réorganisation]**), le cas échéant.

   ![chlimage_1-141](assets/chlimage_1-352.png)

   Si vous souhaitez ajouter des miniatures, cliquez sur l’icône **+** **[!UICONTROL miniature]** en regard de l’image et accédez à la miniature de votre choix. Lorsque vous avez terminé de sélectionner toutes les images miniatures, sélectionnez **[!UICONTROL Enregistrer]**.

   >[!NOTE]
   >
   >Si vous souhaitez ajouter des ressources, sélectionnez **[!UICONTROL Ajouter une ressource]**.

1. Pour supprimer une ressource, cochez la case correspondante et sélectionnez **[!UICONTROL Supprimer l’actif]**.
1. Pour appliquer un paramètre prédéfini, sélectionnez **[!UICONTROL Paramètre prédéfini]** dans le coin supérieur droit et sélectionnez un paramètre prédéfini à appliquer aux ressources.
1. Sélectionnez **[!UICONTROL Enregistrer]**. La visionneuse de médias mixtes nouvellement créée apparaît dans le dossier dans lequel vous l’avez créée.

## Modification d’une visionneuse de médias mixtes {#editing-mixed-media-sets}

Vous pouvez effectuer différentes tâches de modification sur les ressources dans les visionneuses de médias mixtes, directement dans l’interface utilisateur, [comme vous le feriez dans AEM Assets](/help/assets/manage-assets.md). Vous pouvez également effectuer les actions suivantes dans les visionneuses de médias mixtes :

* Ajouter des ressources à la visionneuse de médias mixtes.
* Réorganiser des ressources de la visionneuse de médias mixtes.
* Supprimer des ressources de la visionneuse de médias mixtes.
* Appliquer des paramètres prédéfinis de visionneuse.
* Modifier la vignette par défaut.

**Modification d’une visionneuse de médias mixtes :**

1. Effectuez l’une des opérations suivantes :

   * Pointez sur une ressource de visionneuse de médias mixtes, puis sélectionnez **[!UICONTROL Modifier]** (icône crayon).
   * Pointez sur une ressource de visionneuse de médias mixtes, sélectionnez **[!UICONTROL Sélectionner]** (icône en forme de coche), puis sélectionnez **[!UICONTROL Modifier]** dans la barre d’outils.

   * Sélectionnez une ressource de visionneuse de médias mixtes, puis sélectionnez **[!UICONTROL Modifier]** (icône crayon) dans la barre d’outils.

1. Dans l’éditeur de visionneuse de médias mixtes, effectuez l’une des actions suivantes :

   * Pour réorganiser les ressources : dans le panneau de gauche, sélectionnez **[!UICONTROL Ressources]** (icône image), puis faites glisser une ressource vers un nouvel emplacement.
   * Pour ajouter des ressources : dans la barre d’outils, sélectionnez **[!UICONTROL Ajouter une ressource]**. Accédez aux ressources. Pour chaque ressource à ajouter, passez la souris sur l’image de la ressource (et non son nom), puis sélectionnez l’icône en forme de coche. Dans le coin supérieur droit, sélectionnez **[!UICONTROL Sélectionner]**.

   * Pour supprimer une ressource : dans le panneau de gauche, sélectionnez **[!UICONTROL Ressources]** (icône image), puis sélectionnez la ressource. Dans la barre d’outils, sélectionnez **[!UICONTROL Supprimer la ressource]**.

   * Pour trier les ressources selon leur nom par ordre croissant ou décroissant, dans le panneau de gauche, sélectionnez **[!UICONTROL Ressources]** (icône image). À droite de l’en-tête **[!UICONTROL Ressources]** , sélectionnez les icônes du signe d’insertion vers le haut ou vers le bas.

      >[!NOTE]
      >
      >* Pour supprimer une visionneuse de médias mixtes dans son ensemble, depuis n’importe quel mode d’affichage (**[!UICONTROL Carte]** ou **[!UICONTROL Colonnes]**, par exemple), accédez à la visionneuse de médias mixtes. Pointez sur la ressource et sélectionnez l’icône en forme de coche pour la sélectionner. Appuyez sur **[!UICONTROL Retour arrière]** au clavier ou sélectionnez **[!UICONTROL Plus]** (trois points) dans la barre d’outils, puis sélectionnez **[!UICONTROL Supprimer]**.
         >
         >
      * Vous pouvez modifier des ressources dans une visionneuse de médias mixtes en y accédant, puis en cliquant sur **[!UICONTROL Définir les membres]** dans le rail de gauche. Sélectionnez l’icône **[!UICONTROL Crayon]** sur une ressource spécifique pour l’ouvrir dans la fenêtre de modification.


1. Sélectionnez **[!UICONTROL Enregistrer]** lorsque vous avez terminé la modification.

   >[!NOTE]
   >
   >* Pour modifier les ressources dans une visionneuse de médias mixtes – Accédez à la visionneuse de médias mixtes. Appuyez sur la visionneuse (sans la sélectionner) pour l’ouvrir dans la page Aperçu du jeu de Experience Manager. Dans le rail de gauche, sélectionnez le signe d’insertion pour ouvrir la liste déroulante, puis sélectionnez **[!UICONTROL Définir les membres]**. Dans la page Définir les membres , passez la souris sur une ressource, puis sélectionnez **[!UICONTROL Modifier]** (icône crayon) pour ouvrir la page de modification.
      >
      >
   * Pour supprimer une visionneuse de médias mixtes dans son ensemble – À partir de n’importe quel mode d’affichage (Mode Carte ou Colonne, par exemple), accédez à la visionneuse de médias mixtes. Pointez sur la visionneuse, puis sélectionnez **Sélectionner** (icône de coche). Appuyez sur **[!UICONTROL Retour arrière]** sur votre clavier ou sélectionnez **[!UICONTROL Plus]** (ligne de trois points), puis sélectionnez **[!UICONTROL Supprimer]**.


## Aperçu d’une visionneuse de médias mixtes {#previewing-mixed-media-sets}

Voir [Aperçu des ressources](/help/assets/previewing-assets.md) pour plus d’informations sur la manière de prévisualiser une visionneuse de médias mixtes.

## Publication d’une visionneuse de médias mixtes {#publishing-mixed-media-sets}

Voir [Publier les ressources](/help/assets/publishing-dynamicmedia-assets.md) pour plus d’informations sur la publication d’une visionneuse de médias mixtes.

>[!NOTE]
>
>Si la visionneuse de médias mixtes n’apparaît pas complètement dans le service de diffusion la première fois que vous la publiez, publiez-la une seconde fois.
