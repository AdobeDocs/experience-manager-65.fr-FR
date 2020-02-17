---
title: Profils d’image de média dynamique
description: Créez des profils d’image qui contiennent des paramètres pour le masquage flou et le recadrage intelligent ou l’échantillon intelligent, ou les deux, puis appliquez le profil à un dossier de ressources d’images.
uuid: 9049fab9-d2be-4118-8684-ce58f3c8c16a
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: administering
content-type: reference
discoiquuid: 4f9301db-edf8-480b-886c-b5e8fca5bf5c
translation-type: tm+mt
source-git-commit: 0595d89409e0ca21f771be5c55c3ec9548a8449f

---


# Profils d’image de média dynamique {#image-profiles}

Lors du téléchargement d’images, vous pouvez automatiquement recadrer l’image au moment du téléchargement en appliquant un profil d’image au dossier.

>[!NOTE]
>
>Le recadrage intelligent est disponible uniquement dans le mode Scene7 de Dynamic Media.

## Crop options {#crop-options}

Vous avez le choix entre deux options de recadrage d’image, ainsi qu’une option permettant d’automatiser la création des échantillons de couleur et d’image.

<table>
 <tbody>
  <tr>
   <td><strong>Option</strong></td>
   <td><strong>Quand utiliser la personnalisation</strong></td>
   <td><strong>Description</strong></td>
  </tr>
  <tr>
   <td>Recadrage des pixels</td>
   <td>Recadrez des images en masse uniquement en fonction des dimensions.</td>
   <td><p>Pour utiliser cette option, sélectionnez <strong>Recadrage des pixels</strong> dans la liste déroulante Options de recadrage.</p> <p>Pour recadrer les bords d’une image, entrez le nombre de pixels à rogner de n’importe quel côté ou de chaque côté de l’image. La proportion du recadrage de l’image dépend du paramètre ppi (pixels par pouce) du fichier image.</p> <p>Le recadrage des pixels d’un profil d’image est rendu de la façon suivante :<br /> </p>
    <ul>
     <li>Les valeurs sont : haut, bas, gauche et droite.</li>
     <li>Le coin supérieur gauche est considéré comme 0,0, et le recadrage des pixels est calculé à partir de cet endroit.</li>
     <li>Point de départ du recadrage : la gauche est X et le haut est Y</li>
     <li>Calcul horizontal : dimension horizontale en pixels de l’image originale moins la gauche puis moins la droite.</li>
     <li>Calcul vertical : hauteur verticale en pixels moins le haut puis moins le bas.</li>
    </ul> <p>Prenons l’exemple d’une image de 4 000 x 3 000 pixels. On utilise les valeurs : haut=250 ; bas=500 ; gauche=300 ; droite=700.</p> <p>À partir du coin supérieur gauche (300,250), recadrez l’image en utilisant l’espace de remplissage de (4000-300-700, 3000-250-500 ou 3000,2250).</p> </td>
  </tr>
  <tr>
   <td>Recadrage intelligent</td>
   <td>Recadrez des images en masse en fonction de leur point focal visuel.</td>
   <td><p>Le recadrage dynamique utilise la puissance de l’intelligence artificielle d’Adobe Sensei afin d’automatiser rapidement le recadrage des images en masse. Il détecte automatiquement le point focal de n’importe quelle image et recadre de façon à capturer le point ciblé prévu, quelle que soit la taille de l’écran.</p> <p>Pour utiliser le recadrage intelligent, sélectionnez <strong>Recadrage intelligent</strong> dans la liste déroulante Options de recadrage, puis à droite de Recadrage d’image réactive, activez la fonction.</p> <p>Les tailles de points d’arrêt par défaut Grand, Moyen et Petit couvrent généralement la gamme de tailles utilisée par la plupart des images sur les appareils mobiles, les tablettes, les ordinateurs de bureau et les bannières. Si vous le souhaitez, vous pouvez modifier les noms par défaut Grand, Moyen et Petit.</p> <p>Pour ajouter d’autres points d’arrêt, cliquez sur <strong>Ajouter un recadrage</strong> ; pour supprimer un recadrage, cliquez sur l’icône de corbeille.</p> </td>
  </tr>
  <tr>
   <td>Échantillon de couleurs et d’images</td>
   <td>Générez en masse un échantillon pour chaque image.</td>
   <td><p><strong>Remarque</strong> : Smart Swatch n’est pas pris en charge par Dynamic Media Classic.</p> <p>Localisez et générez automatiquement des échantillons de qualité supérieure des images de produits qui affichent la couleur ou la texture.</p> <p>Pour utiliser l’échantillon de couleurs et d’images, sélectionnez <strong>Recadrage intelligent</strong> dans la liste déroulante Options de recadrage, puis à droite d’Échantillon de couleurs et d’images, activez la fonction. Saisissez une valeur de pixels dans les zones de texte Largeur et Hauteur.</p> <p>Même si tous les recadrages d’images sont fournis par le rail Rendus, les échantillons sont utilisés uniquement par l’intermédiaire de la fonction Copier l’URL. Notez que vous devez utiliser votre propre composant d’affichage pour effectuer le rendu de l’échantillon sur votre site. (Les bannières de carrousel sont une exception. Dynamic Media fournit le composant d’affichage pour l’échantillon utilisé dans les bannières de carrousel.)</p> <p><strong>Utilisation d’échantillons d’images</strong></p> <p>L’URL des échantillons d’images est simple. Elle suit ce format :</p> <p><code>/is/image/company/&lt;asset_name&gt;:Swatch</code></p> <p>where <code>:Swatch</code> is appended to the asset request.</p> <p><strong>Utilisation des échantillons de couleurs</strong></p> <p>Pour utiliser les échantillons de couleurs, vous effectuez une demande <code>req=userdata</code> de la façon suivante :</p> <p><code>/is/image/&lt;company_name&gt;/&lt;swatch_asset_name&gt;:Swatch?req=userdata</code></p> <p>Par exemple, voici une ressource d’échantillon dans Dynamic Media Classic (Scene7) :</p> <p><code>https://my.company.com:8080/is/image/DemoCo/Sleek:Swatch</code></p> <p>and here is the swatch asset's corresponding <code>req=userdata</code> URL:</p> <p><code>https://my.company.com:8080/is/image/DemoCo/Sleek:Swatch?req=userdata</code></p> <p>The <code>req=userdata</code> response is as follows:</p> <p><code class="code">SmartCropDef=Swatch
       SmartCropHeight=200.0
       SmartCropRect=0.421671,0.389815,0.0848564,0.0592593,200,200
       SmartCropType=Swatch
       SmartCropWidth=200.0
       SmartSwatchColor=0xA56DB2</code></p> <p>Vous pouvez également demander une réponse <code>req=userdata</code> au format XML ou JSON, comme dans les exemples d’URL respectifs suivants :</p> <p><code>https://my.company.com:8080/is/image/DemoCo/Sleek:Swatch?req=userdata,xml</code></p><p><code>SmartSwatchColor</code></p><p></p></td></tr></tbody></table>

## Masquage flou {#unsharp-mask}

You use **[!UICONTROL Unsharp mask]** to fine-tune a sharpening filter effect on the final downsampled image. You can control intensity of effect, radius of the effect (measured in pixels), and a threshold of contrast that will be ignored. This effect uses the same options as Adobe Photoshop’s “Unsharp Mask” filter.

>[!NOTE]
>
>Le masque flou est appliqué uniquement aux rendus réduits au sein du PTIFF (pyramid tiff), dont la résolution est réduite de plus de 50 %. Cela signifie que les rendus de taille plus grande à l’intérieur du ptiff ne sont pas affectés par le masque flou tandis que les rendus de plus petite taille, comme les vignettes, sont altérés (et affichent le masque flou).

L’option **[!UICONTROL Masquage flou]** propose les options de filtre suivantes :

<table>
 <tbody>
  <tr>
   <td><strong>Option</strong></td>
   <td><strong>Description</strong></td>
  </tr>
  <tr>
   <td>Quantité</td>
   <td>Contrôle le degré de contraste appliqué aux pixels de contour. La valeur par défaut est 1.75. Pour les images à haute résolution, vous pouvez l’augmenter jusqu’à 5. Considérez la quantité comme une mesure de l’intensité du filtre. La plage est 0 à 5.</td>
  </tr>
  <tr>
   <td>Rayon</td>
   <td>Détermine le nombre de pixels entourant les pixels de contour qui affectent l’accentuation. Pour les images à haute résolution, entrez une valeur comprise entre 1 et 2. Une valeur faible accentue uniquement les pixels de contour ; une valeur élevée accentue une bande plus large de pixels. La valeur appropriée dépend de la taille de l’image. La valeur par défaut est 0,2.  La plage est 0 à 250.</td>
  </tr>
  <tr>
   <td>Seuil</td>
   <td><p>Détermine la plage de contraste à ignorer lorsque le filtre de masquage flou est appliqué. En d’autres termes, cette option définit l’écart recherché entre les pixels et la zone environnante avant qu’ils ne soient considérés comme des pixels de contour et ne soient accentués. Pour éviter d’introduire du bruit, essayez des valeurs comprises entre 0 et 255.</p> </td>
  </tr>
 </tbody>
</table>

L’accentuation est décrite dans la section [Accentuation des images](/help/assets/assets/s7_sharpening_images.pdf).

## Création de profils d’image de média dynamique {#creating-image-profiles}

Pour définir les paramètres de traitement avancés pour les autres types de ressources, consultez [Configuration du traitement des ressources](config-dms7.md#configuring-asset-processing).

See [Profiles for Processing Metadata, Images, and Videos](processing-profiles.md).

Consultez également la section [Pratiques recommandées pour organiser vos ressources numériques en vue d’utiliser des profils de traitement](/help/assets/organize-assets.md).

**Pour créer des profils d’image de média dynamique**

1. Tap the AEM logo and navigate to **[!UICONTROL Tools > Assets > Image Profiles]**.
1. Tap **[!UICONTROL Create]** to add a new image profile.
1. Saisissez un nom de profil et les valeurs pour un masquage flou, un recadrage et/ou un échantillon.

   Il est parfois utile d’utiliser un nom de profil spécifique à sa finalité prévue. Par exemple, si vous souhaitez créer un profil qui génère des échantillons uniquement (en d’autres termes, le recadrage intelligent est désactivé, et l’échantillon de couleurs et d’images est activé), vous pouvez utiliser le nom de profil « Échantillons intelligents ».

   Voir aussi [Options de recadrage intelligent et d’échantillon intelligent](#crop-options) et [Masquage flou](#unsharp-mask).

   ![recadrer](assets/crop.png)

1. Appuyez sur **[!UICONTROL Enregistrer]**. Le profil nouvellement créé apparaît dans la liste des profils disponibles.

## Modification ou suppression de profils d’image de média dynamique {#editing-or-deleting-image-profiles}

1. Tap the AEM logo and navigate to **[!UICONTROL Tools > Assets > Image Profiles]**.
1. Sélectionnez le profil de l’image que vous souhaitez modifier ou supprimer. Pour le modifier, sélectionnez **[!UICONTROL Modifier le profil de traitement d’image]**. Pour le supprimer, sélectionnez **[!UICONTROL Supprimer le profil de traitement d’image]**.

   ![chlimage_1-254](assets/chlimage_1-254.png)

1. En cas de modification, enregistrez les modifications; En cas de suppression, confirmez la suppression du profil.

## Application d’un profil d’image Contenu multimédia dynamique aux dossiers {#applying-an-image-profile-to-folders}

Lorsque vous affectez un profil d’image à un dossier, tout sous-dossier hérite automatiquement du profil de son dossier parent. Cela signifie que vous ne pouvez affecter qu’un seul profil d’image à un dossier. Nous vous conseillons donc de choisir avec la plus grande attention la structure du dossier dans lequel vous transférez, stockez, utilisez et archivez des ressources.

Si vous avez affecté un profil d’image différent à un dossier, le nouveau profil remplace le précédent. Les ressources du dossier précédent restent inchangées. Le nouveau profil sera appliqué aux ressources ajoutées ultérieurement au dossier.

Les dossiers auxquels un profil est attribué sont indiqués dans l’interface utilisateur grâce au nom du profil qui apparaît sur la carte.

<!-- When you add smart crop to an existing image profile, you need to re-trigger the [DAM Update Asset workflow](assets-workflow.md) if you want to generate crops for existing assets in your asset repository. -->

Vous pouvez appliquer des profils d’image à des dossiers spécifiques, ou de façon globale à toutes les ressources.

Vous pouvez retraiter des fichiers dans un dossier contenant déjà un profil d’image existant que vous avez modifié ultérieurement. Reportez-vous à [Retraitement des fichiers dans un dossier après avoir modifié son profil de traitement](processing-profiles.md#reprocessing-assets).

### Application de profils d’image Contenu multimédia dynamique à des dossiers spécifiques {#applying-image-profiles-to-specific-folders}

You can apply an image profile to a folder from within the **[!UICONTROL Tools]** menu or if you are in the folder, from **[!UICONTROL Properties]**. Cette section décrit comment appliquer des profils d’image aux dossiers en utilisant les deux procédures.

Dans le cas des dossiers auxquels un profil est déjà affecté, le nom du profil est affiché directement sous celui du dossier.

Vous pouvez retraiter des fichiers dans un dossier contenant déjà un profil vidéo existant que vous avez modifié ultérieurement. Reportez-vous à [Retraitement des fichiers dans un dossier après avoir modifié son profil de traitement](processing-profiles.md#reprocessing-assets).

#### Applying Dynamic Media image profiles to folders from Profiles user interface {#applying-image-profiles-to-folders-from-profiles-user-interface}

1. Tap the AEM logo and navigate to **[!UICONTROL Tools > Assets > Image Profiles]**.
1. Sélectionnez le profil d’image à appliquer à un ou à plusieurs dossiers.

   ![chlimage_1-255](assets/chlimage_1-255.png)

1. Tap **[!UICONTROL Apply Processing Profile to Folder(s)]** and select the folder or multiple folders you want use to receive the newly uploaded assets and tap/click **[!UICONTROL Apply]**. Dans le cas des dossiers auxquels un profil est déjà affecté, le nom du profil est affiché directement sous celui du dossier.

#### Applying Dynamic Media image profiles to folders from Properties {#applying-image-profiles-to-folders-from-properties}

1. Tap the AEM logo and navigate to **[!UICONTROL Assets]** and then to the folder that you want to apply an image profile to.
1. On the folder, tap the check mark to select it and then tap **[!UICONTROL Properties]**.
1. Appuyez sur l’onglet **[!UICONTROL Profils d’image]**. From the **[!UICONTROL Profile Name]** drop-down list, select the profile, then tap **[!UICONTROL Save &amp; Close]**. Dans le cas des dossiers auxquels un profil est déjà affecté, le nom du profil est affiché directement sous celui du dossier.

   ![chlimage_1-256](assets/chlimage_1-256.png)

### Application d’un profil d’image Contenu multimédia dynamique à l’échelle mondiale {#applying-an-image-profile-globally}

En plus d’appliquer un profil à un dossier, vous pouvez également en appliquer un de façon globale, de sorte que tout contenu transféré dans AEM Assets soit traité par ce profil, indifféremment du dossier.

Vous pouvez retraiter des fichiers dans un dossier contenant déjà un profil vidéo existant que vous avez modifié ultérieurement. Reportez-vous à [Retraitement des fichiers dans un dossier après avoir modifié son profil de traitement](processing-profiles.md#reprocessing-assets).

**Pour appliquer un profil d’image Contenu multimédia dynamique globalement**:

1. Utilisez l’une des méthodes suivantes :

   * Accédez à `https://&lt;AEM server&gt;/mnt/overlay/dam/gui/content/assets/foldersharewizard.html/content/dam` et appliquez le profil approprié, puis appuyez sur **[!UICONTROL Enregistrer]**.

      ![chlimage_1-257](assets/chlimage_1-257.png)

   * Navigate to CRXDE Lite to the following node: `/content/dam/jcr:content`.

      Ajoutez la propriété `imageProfile:/conf/global/settings/dam/adminui-extension/imageprofile/<name of image profile>` et appuyez sur **[!UICONTROL Enregistrer tout]**.

      ![configure_image_profiles](assets/configure_image_profiles.png)

## Modification du recadrage intelligent ou de l’échantillon intelligent d’une seule image {#editing-the-smart-crop-or-smart-swatch-of-a-single-image}

>[!NOTE]
>
>Le recadrage intelligent est disponible uniquement dans le mode Scene7 de Dynamic Media.

Vous pouvez réaligner ou redimensionner manuellement la fenêtre de recadrage intelligent d’une image pour affiner davantage son point focal.

Une fois que vous avez modifié et enregistré un recadrage intelligent, le changement est propagé partout où vous utilisez le recadrage des images spécifiques.

Vous pouvez exécuter à nouveau le recadrage intelligent pour générer des recadrages supplémentaires, le cas échéant.

Voir aussi [Modification du recadrage intelligent ou de l’échantillon intelligent de plusieurs images](#editing-the-smart-crop-or-smart-swatch-of-multiple-images).

**Pour modifier le recadrage intelligent ou l’échantillon dynamique d’une image** unique :

1. Tap the AEM logo and navigate to **[!UICONTROL Assets]**, then to the folder that has a smart crop or smart swatch image profile applied to it.

1. Appuyez sur le dossier pour ouvrir son contenu.
1. Appuyez sur l’image dont vous souhaitez ajuster le recadrage intelligent ou l’échantillon intelligent.
1. On the toolbar, tap **[!UICONTROL Smart Crop]**.

1. Procédez de l’une des manières suivantes :

   * Près du coin supérieur droit de la page, faites glisser le curseur vers la gauche ou vers la droite pour augmenter ou réduire l’affichage de l’image, respectivement.
   * Dans l’image, faites glisser une poignée d’angle pour régler la taille de la zone visible du recadrage ou de l’échantillon.
   * Dans l’image, faites glisser la zone/l’échantillon vers un nouvel emplacement. Vous pouvez modifier uniquement les échantillons d’images ; les échantillons de couleurs sont statiques.
   * Above the image, tap  **[!UICONTROL Revert]** to undo all your edits and restore the original crop or swatch.

1. Near the upper-right corner of the page, tap **[!UICONTROL Save]**, then tap **[!UICONTROL Close]** to return to the folder of assets.

## Modification du recadrage intelligent ou de l’échantillon intelligent de plusieurs images {#editing-the-smart-crop-or-smart-swatch-of-multiple-images}

Une fois que vous avez appliqué un profil d’image (contenant un recadrage dynamique) à un dossier, un recadrage est appliqué à toutes les images qu’il contient. If desired, you can *manually* realign or resize the smart crop window in multiple images to further refine their focal point.

Une fois que vous avez modifié et enregistré un recadrage intelligent, le changement est propagé partout où vous utilisez le recadrage des images spécifiques.

Vous pouvez exécuter à nouveau le recadrage intelligent pour générer des recadrages supplémentaires, le cas échéant.

**Pour modifier le recadrage intelligent ou l’échantillon dynamique de plusieurs images**:

1. Tap the AEM logo and navigate to **[!UICONTROL Assets]**, then to a folder that has a smart crop or smart swatch image profile applied to it.
1. On the folder, tap the **[!UICONTROL More Actions]** (...) icon, then tap **[!UICONTROL Smart Crop]**.

1. On the **[!UICONTROL Edit Smart Crops]** page, do any of the following:

   * Ajustez la taille d’affichage des images sur la page.

      À droite de la liste déroulante de noms de points d’arrêt, faites glisser le curseur vers la gauche ou la droite pour modifier la taille de l’affichage d’image visible.

      ![edit_smart_cultures-sliderbar](assets/edit_smart_crops-sliderbar.png)

   * Vous pouvez filtrer la liste des images visibles en fonction des noms de points d’arrêt. Dans l’exemple ci-dessous, les images sont filtrées en fonction du nom de point d’arrêt « Moyen ».

       Près du coin supérieur droit de la page, dans la liste déroulante, sélectionnez un nom de point d’arrêt pour filtrer les images que vous souhaitez voir (voir l’image ci-dessus).

      ![edit_smart_cultures-dropdownlist](assets/edit_smart_crops-dropdownlist.png)

   * Redimensionnez la zone de recadrage intelligent. Effectuez l’une des opérations suivantes :

      * Si l’image comporte un recadrage intelligent ou un échantillon intelligent uniquement, faites glisser sur celle-ci la poignée de l’angle de la zone de recadrage pour ajuster la taille de la zone visible du recadrage.
      * Si l’image comporte à la fois un recadrage intelligent et un échantillon intelligent, faites glisser sur celle-ci la poignée de l’angle de la zone de recadrage pour ajuster la taille de la zone visible du recadrage. Ou, appuyez ou cliquez sur l’échantillon intelligent sous l’image (les échantillons de couleurs sont statiques), puis faites glisser la poignée de l’angle de la zone de recadrage pour ajuster la taille de la zone visible de l’échantillon.
      ![Redimensionnement du recadrage intelligent d’une image.](assets/edit_smart_crops-resize.png)

   * Déplacez la zone de recadrage intelligent. Effectuez l’une des opérations suivantes :

      * Si l’image comporte un recadrage intelligent ou un échantillon intelligent uniquement, faites glisser sur celle-ci la zone de recadrage vers un nouvel emplacement.
      * Si l’image comporte à la fois un recadrage intelligent et un échantillon intelligent, faites glisser sur celle-ci la zone de recadrage intelligent vers un nouvel emplacement. Ou, appuyez ou cliquez sur l’échantillon intelligent sous l’image (les échantillons de couleurs sont statiques), puis faites glisser la zone de recadrage intelligent de l’échantillon vers un nouvel emplacement.
      ![edit_smart_cultures-move](assets/edit_smart_crops-move.png)

   * Annulez toutes vos modifications et rétablissez le recadrage intelligent ou l’échantillon intelligent d’origine (s’applique à la session de modification active uniquement).

      Appuyez sur **[!UICONTROL Rétablir]** au-dessus de l’image.

      ![edit_smart_cultures-revert](assets/edit_smart_crops-revert.png)



1. Dans le coin supérieur droit de la page, appuyez sur **[!UICONTROL Enregistrer]**. then tap **[!UICONTROL Close]** to return to the folder of assets.

## Suppression d’un profil d’image d’un dossier {#removing-an-image-profile-from-folders}

Lorsque vous supprimez un profil d’image d’un dossier, tout sous-dossier hérite automatiquement de la suppression du profil de son dossier parent. Cependant, le traitement des fichiers qui s’est produit dans les dossiers reste intact.

You can remove an image profile from a folder from within the **[!UICONTROL Tools]** menu or if you are in the folder, from **[!UICONTROL Properties]**. Cette section décrit comment supprimer des profils d’image appliqués aux dossiers en utilisant les deux procédures.

### Suppression des profils d’image de médias dynamiques des dossiers au moyen de l’interface utilisateur Profils {#removing-image-profiles-from-folders-via-profiles-user-interface}

1. Tap the AEM logo and navigate to **[!UICONTROL Tools > Assets > Image Profiles]**.
1. Sélectionnez le profil d’image à supprimer d’un ou de plusieurs dossiers.
1. Tap **[!UICONTROL Remove Processing Profile from Folder(s)]** and select the folder or multiple folders you want use to remove the profile from and tap **[!UICONTROL Remove]**.

   Le fait que le nom du profil n’apparaît plus sous celui du dossier indique que le profil d’image n’est plus appliqué à un dossier.

### Suppression des profils d’image Contenu multimédia dynamique des dossiers au moyen de propriétés {#removing-image-profiles-from-folders-via-properties}

1. Tap the AEM logo and navigate **[!UICONTROL Assets]** and then to the folder that you want to remove an image profile from.
1. On the folder, tap the check mark to select it, then tap **[!UICONTROL Properties]**.
1. Select the **[!UICONTROL Image Profiles]** tab.
1. Dans le menu déroulant Nom **[!UICONTROL du]** profil, sélectionnez **[!UICONTROL Aucun]**, puis appuyez sur **[!UICONTROL Enregistrer et fermer]**.

   Dans le cas des dossiers auxquels un profil est déjà affecté, le nom du profil est affiché directement sous celui du dossier.
