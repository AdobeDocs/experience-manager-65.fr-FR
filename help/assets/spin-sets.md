---
title: Visionneuses à 360°
description: Découvrez comment utiliser des visionneuses à 360° dans Dynamic Media.
uuid: 379a20a3-6a17-499a-b0f1-3a835b97aa7b
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
discoiquuid: 8e9b3815-2893-4e6b-ac41-77720b42d56b
docset: aem65
translation-type: tm+mt
source-git-commit: e916f70549197ac9f95443e972401a78735b0560
workflow-type: tm+mt
source-wordcount: '1830'
ht-degree: 96%

---


# Visionneuses à 360°{#spin-sets}

Une visionneuse à 360° simule l’action consistant à faire pivoter un objet pour l’examiner. Les visionneuses à 360° permettent de voir des éléments depuis tous les angles, révélant les détails visuels clés depuis chaque angle.

Une visionneuse à 360° simule une expérience de visionnage à 360°. Dynamic Media fournit des visionneuses à 360° à axe unique avec lesquelles les observateurs peuvent faire pivoter un élément. En outre, les utilisateurs peuvent effectuer un zoom et un panoramique de « forme libre » sur n’importe quelle vue en quelques clics de souris. Ainsi, les utilisateurs peuvent examiner un élément de plus près, depuis un point de vue spécifique.

Spin Sets are designated by a banner with the word **[!UICONTROL SPINSET.]** In addition, if the Spin Set is published, then the publish date, indicated by the **[!UICONTROL World]** icon is on the banner along with the last modification date, indicated by the **[!UICONTROL Pencil]** icon displays.

![chlimage_1-](assets/chlimage_1-380.png)

>[!NOTE]
>
>Pour plus d’informations sur l’interface utilisateur d’Assets, voir [Gestion des ressources avec l’interface utilisateur tactile](/help/assets/managing-assets-touch-ui.md).

## Démarrage rapide : Visionneuse à 360°   {#quick-start-spin-sets}

Pour démarrer rapidement, procédez comme suit :

1. [Chargez les images pour plusieurs vues.](#uploading-assets-for-spin-sets)

   Vous avez besoin au minimum de 8 à 12 prises de vue d’un élément pour pouvoir utiliser une visionneuse à 360° unidimensionnelle et de 16 à 24 prises de vue pour pouvoir utiliser une visionneuse à 360° bidimensionnelle. Les prises de vue doivent être réalisées à intervalles réguliers pour donner l’impression que l’objet est en rotation et retourné. Par exemple, si une visionneuse unidimensionnelle comprend 12 prises de vue, faites pivoter l’objet de 30 degrés (360/12) pour chaque prise de vue.

1. [Créez une visionneuse à 360°.](#creating-spin-sets)

   Pour créer une visionneuse à 360°, sélectionnez **[!UICONTROL Créer > Visionneuse à 360°]**. Attribuez ensuite un nom à la visionneuse, sélectionnez des ressources et choisissez l’ordre dans lequel doivent apparaître les images.

   Voir [Utilisation de sélecteurs](/help/assets/working-with-selectors.md).

   >[!NOTE]
   >
   >Vous pouvez également créer des visionneuses à 360° automatiquement par l’intermédiaire des [paramètres prédéfinis d’ensemble par lot](/help/assets/config-dms7.md#creating%20batch%20set%20presets%20to%20auto-generate%20image%20sets%20and%20spin%20sets). **Important :** Les ensembles par lot sont créés par le système IPS (Image Production System) dans le cadre de l’ingestion des ressources et sont disponibles uniquement dans le mode Scene7 de Dynamic Media.

1. Configurez des [paramètres prédéfinis de visionneuse à 360°](/help/assets/managing-viewer-presets.md), selon les besoins.

   Les administrateurs peuvent créer ou modifier les paramètres prédéfinis de visionneuse à 360°. Pour afficher votre visionneuse à 360° avec un paramètre prédéfini, sélectionnez la visionneuse puis, dans le menu contextuel du rail gauche, sélectionnez **Visionneuses**.

   Accédez à **[!UICONTROL Outils > Ressources > Paramètres visionneuse]** pour créer ou modifier les paramètres prédéfinis de la visionneuse.

   Voir [Ajout et modification de paramètres prédéfinis de la visionneuse](/help/assets/managing-viewer-presets.md).

1. [Affichez une visionneuse à 360°](#viewing-spin-sets). 

   Vous pouvez afficher les visionneuses créées par le biais des paramètres prédéfinis d’ensemble par lot et y accéder de trois manières différentes. Les visionneuses créées à l’aide de paramètres prédéfinis d’ensemble par lot ne s’affichent *pas* dans l’interface utilisateur.

1. [Prévisualisez une visionneuse à 360°.](/help/assets/previewing-assets.md)

   Sélectionnez la visionneuse à 360° pour pouvoir la prévisualiser. Faites pivoter la visionneuse à 360°. Vous pouvez choisir différentes visionneuses dans le menu **[!UICONTROL Visionneuses]** disponible dans le menu déroulant du rail gauche.

1. [Publiez une visionneuse à 360°.](/help/assets/publishing-dynamicmedia-assets.md)

   La publication d’une visionneuse à 360° active la chaîne d’URL et d’incorporation. Vous devez, en outre, [publier le paramètre prédéfini de la visionneuse](/help/assets/managing-viewer-presets.md).

1. [Liez des URL à l’application web](/help/assets/linking-urls-to-yourwebapplication.md) ou [incorporez la vidéo ou la visionneuse d’images](/help/assets/embed-code.md).

   AEM Assets crée des appels URL pour les visionneuses à 360° et les active une fois que vous avez publié la visionneuse à 360°. Vous pouvez copier ces URL lorsque vous prévisualisez les ressources. Vous pouvez également les incorporer à votre site web.

   Sélectionnez la visionneuse à 360° puis, dans le menu déroulant du rail gauche, sélectionnez **[!UICONTROL Visionneuses.]**

   Voir [Liaison d’une visionneuse à 360° à une page web](/help/assets/linking-urls-to-yourwebapplication.md) et [Incorporation d’une vidéo ou d’une visionneuse d’images](/help/assets/embed-code.md).

Le cas échéant, vous pouvez [modifier les visionneuses à 360°](#editing-spin-sets). Vous pouvez, en outre, afficher et modifier les [propriétés de la visionneuse à 360°](/help/assets/managing-assets-touch-ui.md#editing-properties).

## Chargement de ressources pour les visionneuses à 360° {#uploading-assets-for-spin-sets}

Vous avez besoin au minimum de 8 à 12 prises de vue d’un élément pour pouvoir utiliser une visionneuse à 360° unidimensionnelle et de 16 à 24 prises de vue pour pouvoir utiliser une visionneuse à 360° bidimensionnelle. Les prises de vue doivent être réalisées à intervalles réguliers pour donner l’impression que l’objet est en rotation et retourné. Par exemple, si une visionneuse unidimensionnelle comprend 12 prises de vue, faites pivoter l’objet de 30 degrés (360/12) pour chaque prise de vue.

Vous pouvez charger des images pour les visionneuses à 360° comme vous le [feriez pour n’importe quelle autre ressource dans AEM Assets](/help/assets/managing-assets-touch-ui.md).

### Instructions relatives à la capture d’images pour la visionneuse à 360° {#guidelines-for-shooting-spin-set-images}

Vous trouverez ci-dessous des pratiques recommandées relatives aux images de la visionneuse à 360°. En général, plus vous avez d’images dans la visionneuse à 360°, plus l’effet de rotation est réussi. Néanmoins, l’inclusion de nombreuses images dans la visionneuse augmente également la durée de chargement de ces dernières. AEM recommande de suivre les instructions suivantes pour les prises de vue à utiliser dans les visionneuses à 360° :

* Au minimum, utilisez 8 à 12 images dans une visionneuse à 360° unidimensionnelle et 16 à 24 images dans une visionneuse à 360° bidimensionnelle. 8 images au minimum sont nécessaires pour effectuer une rotation de 360 degrés. Les visionneuses à 360° unidimensionnelles sont plus courantes que les visionneuses à 360° bidimensionnelles, car la création de ces dernières demande beaucoup de travail.
* Utilisez un format d’image sans perte (formats TIFF et PNG recommandés).
* Masquez toutes les images pour faire apparaître l’objet sur un fond blanc ou fortement contrasté. Ajoutez éventuellement des ombres.
* Assurez-vous que les détails du produit sont bien éclairés et que leur mise au point est nette.
* Utilisez un mannequin ou un modèle pour la prise de vue d’articles de mode. Souvent, le mannequin est complètement masqué (en utilisant un mannequin transparent) ou bien un mannequin stylisé est présenté dans l’image. Vous pouvez créer une visionneuse à 360° « sur modèle » en définissant le nombre d’angles. Marquez chaque angle avec du ruban adhésif sur le sol afin de guider le modèle à regarder dans la direction de chaque prise de vue.

## Création d’une visionneuse à 360°   {#creating-spin-sets}

Cette section décrit comment créer des visionneuses à 360° dans AEM.

>[!NOTE]
>
>Vous pouvez également créer des visionneuses à 360° automatiquement par l’intermédiaire des [paramètres prédéfinis d’ensemble par lot](/help/assets/config-dms7.md#creating%20batch%20set%20presets%20to%20auto-generate%20image%20sets%20and%20spin%20sets). **Important :** Les ensembles par lot sont créés par le système IPS (Image Production System) dans le cadre de l’ingestion des ressources et sont disponibles uniquement dans le mode Scene7 de Dynamic Media.
>
>Voir « Création de paramètres prédéfinis d’ensemble par lot pour générer automatiquement des visionneuses d’images et des visionneuses à 360° » dans [Configuration de Dynamic Media – mode Scene7](/help/assets/config-dms7.md#creating%20batch%20set%20presets%20to%20auto-generate%20image%20sets%20and%20spin%20sets).


>[!NOTE]
>
>L’ordre dans lequel les images apparaissent dans une visionneuse à 360° a une importance. Veillez à les mettre dans le bon ordre afin que la rotation soit une vue à 360° parfaite.

**Pour créer des visionneuses à 360°**

1. Dans Assets, accédez à l’emplacement où vous souhaitez créer une visionneuse à 360°, cliquez sur **[!UICONTROL Créer]**, puis sélectionnez **[!UICONTROL Visionneuse à 360°.]** Vous pouvez également la créer depuis un dossier qui contient les ressources. L’éditeur de visionneuse à 360° s’affiche.

   ![6_5_spinset-createpulldownmenu](assets/6_5_spinset-createpulldownmenu.png)

1. Dans le champ **[!UICONTROL Titre]** de l’éditeur de visionneuse à 360°, entrez un nom pour la visionneuse à 360°. Le nom apparaît dans la bannière située sur la visionneuse à 360°. Vous pouvez aussi saisir une description.

   ![6_5_spinset-spinseteditortitle](assets/6_5_spinset-spinseteditortitle.png)

   >[!NOTE]
   >
   >Lors de la création de la visionneuse à 360°, vous pouvez modifier la miniature de la visionneuse ou autoriser AEM à sélectionner la miniature automatiquement en fonction des ressources de la visionneuse à 360°. Pour sélectionner une miniature, cliquez sur **[!UICONTROL Modifier la miniature]** et sélectionnez une image (vous pouvez également accéder à d’autres dossiers pour trouver des images). Si vous avez sélectionné une miniature, puis décidez que vous souhaitez qu’AEM en génère une depuis la visionneuse à 360°, sélectionnez **[!UICONTROL Basculer vers les miniatures automatiques.]**

1. Effectuez l’une des opérations suivantes :

   * Dans le coin supérieur gauche de la page de l’éditeur de visionneuse à 360°, appuyez sur **[!UICONTROL Ajouter une ressource.]**

   * Au milieu de la page de l’éditeur de visionneuse à 360°, appuyez sur **[!UICONTROL Appuyer pour ouvrir le sélecteur de ressources.]**
   Appuyez pour sélectionner les ressources que vous souhaitez inclure dans la visionneuse à 360°. Les ressources sélectionnées sont cochées. Lorsque vous avez terminé, en haut à droite de la page, appuyez sur **[!UICONTROL Sélectionner.]**

   Le sélecteur de ressources vous permet de rechercher des ressources en saisissant un mot-clé, puis en appuyant sur **[!UICONTROL Retour**. Vous pouvez également appliquer des filtres pour affiner vos résultats de recherche. Vous pouvez filtrer par chemin, collection, type de fichier et balise. Sélectionnez le filtre, puis appuyez sur l’icône **[!UICONTROL Filtre]** de la barre d’outils. Modifiez l’affichage en appuyant sur l’icône Affichage et en sélectionnant **[!UICONTROL Mode Colonnes]**, **[!UICONTROL Mode Carte]** ou **[!UICONTROL Mode Liste.]**

   Voir [Utilisation de sélecteurs](/help/assets/working-with-selectors.md).

   ![chlimage_1-383](assets/chlimage_1-383.png)

1. Lorsque vous ajoutez des ressources à votre visionneuse, elles sont automatiquement ajoutées dans l’ordre alphanumérique. Vous pouvez réorganiser ou trier manuellement les ressources une fois qu’elles ont été ajoutées.

   Si nécessaire, faites glisser l’icône Réorganiser d’une ressource vers la droite du nom de fichier de la ressource pour réorganiser les images vers le haut ou le bas de la liste définie.

   ![Réorganisation de l’image 11 dans la visionneuse à 360° en la faisant glisser vers un nouvel emplacement.](assets/6_5_spinset-reorderassets.png)

   Réorganisation de l’image 11 dans la visionneuse à 360° en la faisant glisser vers un nouvel emplacement.

1. (En option) Effectuez l’une des actions suivantes :

   * Pour supprimer une image, sélectionnez-la et appuyez sur **[!UICONTROL Supprimer la ressource.]**

   * Pour appliquer un paramètre prédéfini, en haut à droite de la page, appuyez sur **[!UICONTROL Paramètre prédéfini]**, puis sélectionnez un paramètre prédéfini à appliquer en une seule fois à toutes les ressources.

1. Click **[!UICONTROL Save.]** Your newly created Spin Set appears in the folder you created it in.

## Affichage de visionneuses à 360°   {#viewing-spin-sets}

Vous pouvez créer des visionneuses à 360° dans l’interface utilisateur ou automatiquement à l’aide des [paramètres prédéfinis d’ensemble par lot](/help/assets/config-dms7.md#creating%20batch%20set%20presets%20to%20auto-generate%20image%20sets%20and%20spin%20sets). (Notez toutefois que les visionneuses créées à l’aide de paramètres prédéfinis d’ensemble par lot *ne s’affichent pas* dans l’interface utilisateur.) Vous pouvez accéder aux visionneuses créées au moyen de paramètres prédéfinis d’ensemble par lot de trois manières différentes. (Ces méthodes sont disponibles même si vous avez créé les visionneuses à 360° dans l’interface utilisateur.)

>[!NOTE]
>
>Vous pouvez également afficher les visionneuses par le biais de l’interface utilisateur, comme indiqué dans [Modification d’une visionneuse à 360°](#editing-spin-sets).

**Pour afficher des visionneuses à 360°**.

1. Lors de l’ouverture des propriétés d’une ressource individuelle. Les propriétés indiquent les jeux dont la ressource sélectionnée fait partie (sous **[!UICONTROL Membre des visionneuses]**). Cliquez sur le nom de la visionneuse pour l’afficher intégralement.

   ![chlimage_1-156](assets/chlimage_1-384.png)

1. À partir de l’image membre d’une visionneuse, sélectionnez le menu **[!UICONTROL Visionneuses]** pour afficher les visionneuses dont la ressource fait partie.

   ![chlimage_1-157](assets/chlimage_1-385.png)

1. À partir de la recherche, vous pouvez **[!UICONTROL sélectionner des filtres]**, développer **[!UICONTROL Dynamic Media]** et **[!UICONTROL sélectionner des jeux.]**

   La recherche renvoie les visionneuses correspondantes qui ont soit été créées manuellement dans l’interface utilisateur, soit automatiquement au moyen de paramètres prédéfinis d’ensemble par lot. Dans le cas des visionneuses automatisées, la requête de recherche est effectuée à l’aide du critère `Starts with`, à la différence de la recherche AEM qui repose sur l’utilisation du critère `Contains`. La définition du filtre sur **[!UICONTROL Visionneuses]** constitue la seule méthode de recherche dans des visionneuses automatisées.

   ![chlimage_1-158](assets/chlimage_1-386.png)

## Modification d’une visionneuse à 360°{#editing-spin-sets}

Vous pouvez effectuer diverses tâches de modification sur les visionneuses à 360°, notamment :

* Ajouter des images à la visionneuse à 360°.
* Réorganiser des images dans la visionneuse à 360°.
* Supprimer les ressources de la visionneuse à 360°.
* Appliquer des paramètres prédéfinis de visionneuse.
* Supprimer la visionneuse à 360°.

**Pour modifier une visionneuse à 360°**

1. Effectuez l’une des opérations suivantes :

   * Pointez sur une ressource de visionneuse à 360°, puis appuyez sur **[!UICONTROL Modifier]** (icône de crayon).
   * Pointez sur une ressource de visionneuse à 360°, appuyez sur **[!UICONTROL Sélectionner]** (icône de coche), puis sur **[!UICONTROL Modifier]** sur la barre d’outils.

   * Appuyez sur une ressource de visionneuse à 360°, puis sur **[!UICONTROL Modifier]** (icône de crayon) sur la barre d’outils.

1. Pour modifier la visionneuse à 360°, effectuez l’une des opérations suivantes :

   * Pour réorganiser les images, faites glisser une image vers son nouvel emplacement (sélectionnez l’icône de réorganisation pour déplacer les éléments).
   * Pour trier les éléments dans l’ordre ascendant ou descendant, cliquez sur l’en-tête de colonne.
   * Pour ajouter une ressource ou mettre à jour une ressource existante, cliquez sur **[!UICONTROL Ajouter une ressource.]** Accédez à une ressource, sélectionnez-la, puis appuyez sur **[!UICONTROL Sélectionner]** en haut à droite.
Si vous supprimez l’image qu’AEM utilise pour la miniature en la remplaçant par une autre image, la ressource d’origine s’affiche toujours.
   * Pour supprimer une ressource, sélectionnez-la et cliquez ou appuyez sur **[!UICONTROL Supprimer la ressource.]**
   * Pour appliquer un paramètre prédéfini, appuyez ou cliquez sur l’icône Paramètre prédéfini et sélectionnez-en un.
   * Pour supprimer une visionneuse à 360°, accédez à cette dernière, sélectionnez-la, puis choisissez **[!UICONTROL Supprimer]**

   >[!NOTE]
   >
   >Vous pouvez modifier les images d’une visionneuse à 360° en y accédant, en appuyant sur **[!UICONTROL Définir les membres]** dans le rail gauche, puis en appuyant sur l’icône en forme de crayon d’une ressource pour ouvrir la fenêtre de modification.

1. Lorsque vous avez terminé les modifications, cliquez sur **[!UICONTROL Enregistrer]**.

## Aperçu d’une visionneuse à 360°   {#previewing-spin-sets}

Voir aussi [Aperçu des ressources](/help/assets/previewing-assets.md).

## Publication d’une visionneuse à 360°   {#publishing-spin-sets}

Voir [Publication de ressources](/help/assets/publishing-dynamicmedia-assets.md).
