---
title: Visionneuses à 360°
description: Découvrez comment utiliser des visionneuses à 360° dans Contenu multimédia dynamique
uuid: 379a20a3-6a17-499a-b0f1-3a835b97aa7b
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: dynamic-media
content-type: reference
discoiquuid: 8e9b3815-2893-4e6b-ac41-77720b42d56b
docset: aem65
translation-type: tm+mt
source-git-commit: 0595d89409e0ca21f771be5c55c3ec9548a8449f

---


# Visionneuses à 360°{#spin-sets}

Une visionneuse à 360° simule l’action consistant à faire pivoter un objet pour l’examiner. Les visionneuses à 360° permettent de voir des éléments depuis tous les angles, révélant les détails visuels clés depuis chaque angle.

Une visionneuse à 360° simule une expérience de visionnage à 360°. Dynamic Media fournit des visionneuses à 360° à axe unique avec lesquelles les observateurs peuvent faire pivoter un élément. En outre, les utilisateurs peuvent effectuer un zoom et un panoramique de « forme libre » sur n’importe quelle vue en quelques clics de souris. Ainsi, les utilisateurs peuvent examiner un élément de plus près, depuis un point de vue spécifique.

Spin Sets are designated by a banner with the word **[!UICONTROL SPINSET]**. In addition, if the Spin Set is published, then the publish date, indicated by the **[!UICONTROL World]** icon is on the banner along with the last modification date, indicated by the **[!UICONTROL Pencil]** icon displays.

![chlimage_1-](assets/chlimage_1-380.png)

>[!NOTE]
>
>Pour plus d’informations sur l’interface utilisateur des ressources, voir [Gestion des ressources avec l’interface utilisateur tactile](/help/assets/managing-assets-touch-ui.md).

## Démarrage rapide : Visionneuse à 360° {#quick-start-spin-sets}

Pour démarrer rapidement, procédez comme suit :

1. [Téléchargez les images pour plusieurs vues.](#uploading-assets-for-spin-sets)

   Au minimum, vous avez besoin de 8 à 12 prises de vue d’un élément pour une visionneuse à 360° unidimensionnelle et de 16 à 24 prises de vue pour une visionneuse à 360° bidimensionnelle. Les photos doivent être prises à intervalles réguliers pour donner l&#39;impression que l&#39;objet tourne et est retourné. Par exemple, si une visionneuse à 360° unidimensionnelle comprend 12 prises de vue, faites pivoter l’élément de 30 degrés (360/12) pour chaque prise de vue.

1. [Créez une visionneuse à 360°.](#creating-spin-sets)

   To create a Spin Set, select **[!UICONTROL Create > Spin Set]** and then name the set, choose the assets, and choose the order the images appear.

   Voir [Utilisation de sélecteurs](/help/assets/working-with-selectors.md).

   >[!NOTE]
   >
   >Vous pouvez également créer des visionneuses à 360° automatiquement par l’intermédiaire des [paramètres prédéfinis d’ensemble par lot](/help/assets/config-dms7.md#creating%20batch%20set%20presets%20to%20auto-generate%20image%20sets%20and%20spin%20sets). **Important :** Les ensembles par lot sont créés par le système IPS (Image Production System) dans le cadre de l’ingestion des ressources et sont disponibles uniquement dans le mode Scene7 de Dynamic Media.

1. Configurez des [paramètres prédéfinis de visionneuse à 360°](/help/assets/managing-viewer-presets.md), selon les besoins.

   Les administrateurs peuvent créer ou modifier les paramètres prédéfinis de visionneuse à 360°. To see your spin set with a viewer preset, select the spin set, and in the left-rail drop-down menu, select **Viewers**.

   See **[!UICONTROL Tools > Assets > Viewer Presets]** to create or edit viewer presets.

   See [Adding and editing viewer presets.](/help/assets/managing-viewer-presets.md)

1. [Affichez une visionneuse à 360°](#viewing-spin-sets). 

   Vous pouvez afficher les visionneuses créées par le biais des paramètres prédéfinis d’ensemble par lot et y accéder de trois manières différentes. (Sets created using batch set presets, do *not* appear in the user interface.)

1. [Prévisualisez une visionneuse à 360°.](/help/assets/previewing-assets.md)

   Sélectionnez la visionneuse à 360° pour pouvoir la prévisualiser. Faites pivoter la visionneuse à 360°. You can choose different viewers from the **[!UICONTROL Viewers]** menu, available from the left rail drop-down menu.

1. [Publiez une visionneuse à 360°.](/help/assets/publishing-dynamicmedia-assets.md)

   La publication d’une visionneuse à 360° active la chaîne d’URL et d’incorporation. In addition, you must [publish the viewer preset](/help/assets/managing-viewer-presets.md).

1. [Liez des URL à l’application Web](/help/assets/linking-urls-to-yourwebapplication.md) ou [incorporez la vidéo ou la visionneuse d’images](/help/assets/embed-code.md).

   AEM Assets crée des appels URL pour les visionneuses à 360° et les active une fois que vous avez publié la visionneuse à 360°. Vous pouvez copier ces URL lorsque vous prévisualisez les ressources. Vous pouvez également les incorporer à votre site Web.

   Select the Spin Set, then in the left rail drop-down menu, select **[!UICONTROL Viewers]**.

   See [Linking a Spin Set to a web page](/help/assets/linking-urls-to-yourwebapplication.md) and [Embedding the Video or Image Viewer](/help/assets/embed-code.md).

If you need to, you can [edit Spin Sets](#editing-spin-sets). In addition, you can view and modify [Spin Set properties](/help/assets/managing-assets-touch-ui.md#editing-properties).

## Uploading Assets for Spin Sets {#uploading-assets-for-spin-sets}

Au minimum, vous avez besoin de 8 à 12 prises de vue d’un élément pour une visionneuse à 360° unidimensionnelle et de 16 à 24 prises de vue pour une visionneuse à 360° bidimensionnelle. Les photos doivent être prises à intervalles réguliers pour donner l&#39;impression que l&#39;objet tourne et est retourné. Par exemple, si une visionneuse à 360° unidimensionnelle comprend 12 prises de vue, faites pivoter l’élément de 30 degrés (360/12) pour chaque prise de vue.

Vous pouvez télécharger des images pour les visionneuses à 360° comme vous le [feriez pour n’importe quelle autre ressource dans les ressources AEM](/help/assets/managing-assets-touch-ui.md).

### Instructions relatives à la capture d’images pour la visionneuse à 360° {#guidelines-for-shooting-spin-set-images}

Vous trouverez ci-dessous des pratiques recommandées relatives aux images de la visionneuse à 360°. En général, plus vous avez d’images dans la visionneuse à 360°, plus l’effet de rotation est réussi. Néanmoins, l’inclusion de nombreuses images dans la visionneuse augmente également la durée de chargement de ces dernières. AEM recommande de suivre les instructions suivantes pour les prises de vue à utiliser dans les visionneuses à 360° :

* Utilisez au minimum 8 à 12 images dans une visionneuse à 360° unidimensionnelle et 16 à 24 images dans une visionneuse à 360° bidimensionnelle. Un minimum de 8 images est nécessaire pour pouvoir tourner 360 degrés. Les visionneuses à 360° unidimensionnelles sont plus courantes, car la création de visionneuses à 360° bidimensionnelles exige beaucoup de main-d’oeuvre.
* Utilisez un format d’image sans perte (formats TIFF et PNG recommandés).
* Masquez toutes les images pour faire apparaître l’objet sur un fond blanc ou fortement contrasté. Ajoutez éventuellement des ombres.
* Assurez-vous que les détails du produit sont bien éclairés et que leur mise au point est nette.
* Utilisez un mannequin ou un modèle pour la prise de vue d’articles de mode. Souvent, le mannequin est complètement masqué (en utilisant un mannequin transparent) ou bien, un mannequin stylisé est présenté dans l’image. Vous pouvez créer une visionneuse à 360° « sur modèle » en définissant le nombre d’angles. Marquez chaque angle avec du ruban adhésif sur le sol afin de guider le modèle à regarder dans la direction de chaque prise de vue.

## Création d’une visionneuse à 360° {#creating-spin-sets}

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

1. In Assets, navigate to where you want to create a spin set, click **[!UICONTROL Create]**, and select **[!UICONTROL Spin Set]**. Vous pouvez également la créer depuis un dossier qui contient les ressources. L’éditeur de visionneuse à 360° s’affiche.

   ![6_5_spinset-createpulldownmenu](assets/6_5_spinset-createpulldownmenu.png)

1. Dans le champ **[!UICONTROL Titre]** de l’éditeur de visionneuse à 360°, entrez un nom pour la visionneuse à 360°. Le nom apparaît dans la bannière située sur la visionneuse à 360°. Vous pouvez aussi saisir une description.

   ![6_5_spinset-spinseteditortitle](assets/6_5_spinset-spinseteditortitle.png)

   >[!NOTE]
   >
   >Lors de la création de la visionneuse à 360°, vous pouvez modifier la miniature de la visionneuse ou permettre à AEM de sélectionner la miniature automatiquement selon les ressources de la visionneuse à 360°. To select a thumbnail, click **[!UICONTROL Change thumbnail]** and select any image (you can navigate to other folders to find images as well). If you have selected a thumbnail and then decide that you want AEM to generate one from the spin set, select **[!UICONTROL Switch to Automatic thumbnail]**.

1. Effectuez l’une des opérations suivantes :

   * Dans le coin supérieur gauche de la page de l’éditeur de visionneuse à 360°, appuyez sur **[!UICONTROL Ajouter une ressource]**.

   * Au milieu de la page de l’éditeur de visionneuse à 360°, appuyez sur **[!UICONTROL Appuyer pour ouvrir le sélecteur de ressources]**.
   Appuyez pour sélectionner les ressources que vous souhaitez inclure dans la visionneuse à 360°. Les ressources sélectionnées sont cochées. Lorsque vous avez terminé, en haut à droite de la page, appuyez sur **[!UICONTROL Sélectionner]**.

   With the Asset Selector, you can search for assets by typing in a keyword and tapping **[!UICONTROL Return**. Vous pouvez également appliquer des filtres pour affiner les résultats de la recherche. Vous pouvez filtrer par chemin d’accès, collection, type de fichier et balise. Select the filter and then tap the **[!UICONTROL Filter]** icon on the toolbar. Pour modifier l’affichage, appuyez sur l’icône Affichage et sélectionnez **[!UICONTROL Mode Colonne]**, **[!UICONTROL Mode Carte]** ou **[!UICONTROL Mode Liste]**.

   Voir [Utilisation de sélecteurs](/help/assets/working-with-selectors.md).

   ![chlimage_1-383](assets/chlimage_1-383.png)

1. Lorsque vous ajoutez des ressources à votre visionneuse, elles sont automatiquement ajoutées dans l’ordre alphanumérique. Vous pouvez réorganiser ou trier manuellement les ressources après les avoir ajoutées.

   Si nécessaire, faites glisser l’icône Réorganiser d’une ressource vers la droite du nom de fichier de la ressource pour réorganiser les images vers le haut ou le bas de la liste définie.

   ![Réorganisation de l’image 11 dans la visionneuse à 360° en la faisant glisser vers un nouvel emplacement.](assets/6_5_spinset-reorderassets.png)

   Réorganisation de l’image 11 dans la visionneuse à 360° en la faisant glisser vers un nouvel emplacement.

1. (En option) Effectuez l’une des actions suivantes :

   * Pour supprimer une image, sélectionnez-la et appuyez sur **[!UICONTROL Supprimer la ressource]**.

   * Pour appliquer un paramètre prédéfini, en haut à droite de la page, appuyez sur **[!UICONTROL Paramètre prédéfini]**, puis sélectionnez un paramètre prédéfini à appliquer en une seule fois à toutes les ressources.

1. Cliquez sur **[!UICONTROL Enregistrer]**. La visionneuse à 360° nouvellement créée apparaît dans le dossier dans lequel vous l’avez créée.

## Affichage de visionneuses à 360° {#viewing-spin-sets}

Vous pouvez créer des visionneuses à 360° dans l’interface utilisateur ou automatiquement à l’aide des [paramètres prédéfinis d’ensemble par lot](/help/assets/config-dms7.md#creating%20batch%20set%20presets%20to%20auto-generate%20image%20sets%20and%20spin%20sets). However, sets created using batch set presets, do *not* appear in the user interface. Vous pouvez accéder aux visionneuses créées au moyen de paramètres prédéfinis d’ensemble par lot de trois manières différentes. (Ces méthodes sont disponibles même si vous avez créé les visionneuses à 360° dans l’interface utilisateur.)

>[!NOTE]
>
>You can also view sets by way of the user interface as described in [Editing Spin Sets](#editing-spin-sets).

**Pour afficher les visionneuses à 360°**

1. Lors de l’ouverture des propriétés d’une ressource individuelle. Les propriétés indiquent les jeux dont la ressource sélectionnée fait partie (sous **[!UICONTROL Membre des visionneuses]**). Cliquez sur le nom de la visionneuse pour l’afficher intégralement.

   ![chlimage_1-156](assets/chlimage_1-384.png)

1. À partir de l’image membre d’une visionneuse, sélectionnez le menu **[!UICONTROL Visionneuses]** pour afficher les visionneuses dont la ressource fait partie.

   ![chlimage_1-157](assets/chlimage_1-385.png)

1. Dans la recherche, vous pouvez sélectionner **[!UICONTROL Filtres]**, puis développer **[!UICONTROL Média dynamique]** et sélectionner ensuite **[!UICONTROL Visionneuses]**.

   La recherche renvoie les visionneuses correspondantes qui ont soit été créées manuellement dans l’interface utilisateur, soit automatiquement au moyen de paramètres prédéfinis d’ensemble par lot. For automated sets, the search query is conducted using `Starts with` search criteria which is different from AEM search which is based on using `Contains` search criteria. Setting the filter to **[!UICONTROL Sets]** is the only way to search automated sets.

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
   * To add an asset or update an existing asset, click **[!UICONTROL Add Asset]**. Accédez à une ressource, sélectionnez-la, puis appuyez sur **[!UICONTROL Sélectionner]** en haut à droite.
si vous supprimez l’image qu’AEM utilise pour la miniature en la remplaçant par une autre image, la ressource originale s’affiche toujours.
   * To delete an asset, select it and click or tap **[!UICONTROL Delete Asset]**.
   * Pour appliquer un paramètre prédéfini, appuyez ou cliquez sur l’icône Paramètre prédéfini et sélectionnez-en un.
   * Pour supprimer une visionneuse à 360°, accédez à cette dernière, sélectionnez-la, puis choisissez **[!UICONTROL Supprimer]**
   >[!NOTE]
   >
   >Vous pouvez modifier les images d’une visionneuse à 360° en y accédant, en appuyant sur **[!UICONTROL Définir les membres]** dans le rail gauche, puis en appuyant sur l’icône en forme de crayon d’une ressource pour ouvrir la fenêtre de modification.

1. Lorsque vous avez terminé les modifications, cliquez sur **[!UICONTROL Enregistrer]**.

## Aperçu d’une visionneuse à 360° {#previewing-spin-sets}

Voir aussi [Aperçu des ressources](/help/assets/previewing-assets.md).

## Publication d’une visionneuse à 360° {#publishing-spin-sets}

Voir [Publication de ressources](/help/assets/publishing-dynamicmedia-assets.md).
