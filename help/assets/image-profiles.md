---
title: Profils d’image Dynamic Media
description: Créez des profils d’image qui contiennent des paramètres pour le masquage flou et le recadrage intelligent ou l’échantillon intelligent, ou les deux, puis appliquez le profil à un dossier de ressources d’image.
uuid: 9049fab9-d2be-4118-8684-ce58f3c8c16a
contentOwner: Rick Brough
products: SG_EXPERIENCEMANAGER/6.5/ASSETS
topic-tags: administering
content-type: reference
discoiquuid: 4f9301db-edf8-480b-886c-b5e8fca5bf5c
feature: Profils d’image
role: User, Admin
exl-id: 67240ad0-1a7c-4e58-a518-1e36d771f1a1
source-git-commit: 4b8369de9e6a10b73115d53358ce98729d92ed44
workflow-type: tm+mt
source-wordcount: '2790'
ht-degree: 62%

---

# Profils d’image Dynamic Media {#image-profiles}

Lorsque vous chargez des images, vous pouvez les recadrer automatiquement en appliquant un profil d’image au dossier.

>[!NOTE]
>
>Le recadrage intelligent est disponible uniquement dans le mode Scene7 de Dynamic Media.

>[!IMPORTANT]
>
>Les profils d’image ne s’appliquent pas aux fichiers PDF, GIF animé ou INDD (Adobe InDesign).

## Options de recadrage {#crop-options}

<!-- CQDOC-16069 for paragraph directly below -->

Les coordonnées de recadrage intelligent dépendent du rapport d’aspect (L/H). Pour les différents paramètres de recadrage intelligent d’un profil d’image, si le rapport d’aspect est le même pour les dimensions ajoutées au profil d’image, le même rapport d’aspect est envoyé à Dynamic Media. Adobe vous recommande d’utiliser la même zone de recadrage. Cela permet de s’assurer qu’il n’y a aucune incidence sur les différentes dimensions utilisées dans le profil d’image.

Chaque génération de recadrage intelligent créée nécessite un traitement supplémentaire. Par exemple, l’ajout de plus de cinq proportions de recadrage intelligent peut ralentir le taux d’ingestion des ressources. Cela entraîne également une augmentation de la charge sur les systèmes. Étant donné que le recadrage intelligent s’applique aux dossiers, Adobe vous recommande de l’utiliser *uniquement* pour les dossiers où cela est nécessaire.

Vous avez le choix entre deux options de recadrage d’image. Vous avez également la possibilité d’automatiser la création d’échantillons de couleurs et d’images.

| Option | Quand utiliser la personnalisation | Description |
| --- | --- | --- |
| Recadrage des pixels | Recadrez des images en masse uniquement en fonction des dimensions. | Pour utiliser cette option, sélectionnez **[!UICONTROL Recadrage des pixels]** dans la liste déroulante Options de recadrage.<br><br>Pour recadrer les bords d’une image, entrez le nombre de pixels à rogner de n’importe quel côté ou de chaque côté de l’image. La proportion du recadrage de l’image dépend du paramètre ppi (pixels par pouce) du fichier image.<br><br>Un recadrage de pixels de profil d’image s’effectue de la manière suivante :<br> les valeurs ・ sont Haut, Bas, Gauche et Droite.<br>• Le coin supérieur gauche est considéré comme , et le recadrage des pixels est calculé à partir de cet endroit.`0,0`<br>・ Point de départ du recadrage : La gauche est X et la partie supérieure est Y<br> ・ Calcul horizontal : dimension horizontale en pixels de l’image d’origine moins Gauche, puis moins Droite.<br>• Calcul vertical : hauteur verticale en pixels moins le haut puis moins le bas.<br><br>Prenons l’exemple d’une image de 4 000 x 3 000 pixels. Les valeurs utilisées sont les suivantes : haut=250, bas=500, gauche=300, droite=700.<br><br>À partir du coin supérieur gauche (300,250), recadrez l’image en utilisant l’espace de remplissage de (4000-300-700, 3000-250-500 ou 3000,2250). |
| Recadrage intelligent | Recadrez des images en masse en fonction de leur point focal visuel. | Le recadrage dynamique utilise la puissance de l’intelligence artificielle d’Adobe Sensei afin d’automatiser rapidement le recadrage des images en masse. Il détecte automatiquement le point focal de n’importe quelle image et recadre de façon à capturer le point ciblé prévu, quelle que soit la taille de l’écran.</p> <p>Pour utiliser le recadrage intelligent, sélectionnez **[!UICONTROL Recadrage intelligent]** dans la liste déroulante Options de recadrage, puis à droite de Recadrage d’image réactive, activez la fonction.</p> <p>Les tailles de points d’arrêt par défaut Grand, Moyen et Petit couvrent généralement la gamme de tailles utilisée par la plupart des images sur les appareils mobiles, les tablettes, les ordinateurs de bureau et les bannières. Si vous le souhaitez, vous pouvez modifier les noms par défaut Grand, Moyen et Petit.</p> <p>Pour ajouter d’autres points d’arrêt, sélectionnez **[!UICONTROL Ajouter un recadrage]** pour supprimer un recadrage, puis cliquez sur l’icône poubelle. |
| Échantillon de couleurs et d’images | Générez en masse un échantillon pour chaque image. | **Remarque** : Smart Swatch n’est pas pris en charge par Dynamic Media Classic.<br><br>Localisez et générez automatiquement des échantillons de qualité supérieure des images de produits qui affichent la couleur ou la texture.<br><br>Pour utiliser l’échantillon de couleurs et d’images, sélectionnez **[!UICONTROL Recadrage intelligent]** dans la liste déroulante Options de recadrage, puis à droite d’Échantillon de couleurs et d’images, activez la fonction. Saisissez une valeur de pixels dans les zones de texte Largeur et Hauteur.<br><br>Même si tous les recadrages d’images sont fournis par le rail Rendus, les échantillons sont utilisés uniquement par l’intermédiaire de la fonction Copier l’URL. Utilisez votre propre composant d’affichage pour effectuer le rendu de la nuance sur votre site. (Les bannières de carrousel constituent une exception à cette règle. Dynamic Media fournit le composant d’affichage pour l’échantillon utilisé dans les bannières de carrousel.)<br><br>**Utilisation des**<br>&#x200B;échantillons d’images : l’URL des échantillons d’images est simple. <br><br>`/is/image/company/&lt;asset_name&gt;:Swatch`<br>où `:Swatch` est ajouté à la requête de ressource.<br><br>**Utilisation d’**<br>&#x200B;échantillons de couleursPour utiliser des échantillons de couleurs, vous effectuez une  `req=userdata` requête avec les éléments suivants :<br>`/is/image/&lt;company_name&gt;/&lt;swatch_asset_name&gt;:Swatch?req=userdata`<br><br> Par exemple, voici une ressource d’échantillon dans Dynamic Media Classic :<br>`https://my.company.com:8080/is/image/DemoCo/Sleek:Swatch`<br> et voici l’ `req=userdata` URL correspondante de la ressource d’échantillon :<br>`https://my.company.com:8080/is/image/DemoCo/Sleek:Swatch?req=userdata`<br><br> la  `req=userdata` réponse est la suivante :<br>`SmartCropDef=Swatch SmartCropHeight=200.0`<br>`SmartCropRect=0.421671,0.389815,0.0848564,0.0592593,200,200`<br>`SmartCropType=Swatch`<br>`SmartCropWidth=200.0`<br>`SmartSwatchColor=0xA56DB2`<br><br>Vous pouvez également demander une réponse  `req=userdata` au format XML ou JSON, comme dans les exemples d’URL respectifs suivants :<br>`https://my.company.com:8080/is/image/DemoCo/Sleek:Swatch?req=userdata,json`<br>`https://my.company.com:8080/is/image/DemoCo/Sleek:Swatch?req=userdata,xml`<br><br>**Créez votre propre composant WCM pour demander un échantillon de couleur et analysez l’attribut**   `SmartSwatchColor` , représenté par une valeur hexadécimale RVB 24 bits.<br><br>Voir aussi [`userdata` dans le guide de référence des visionneuses](https://experienceleague.adobe.com/docs/dynamic-media-developer-resources/image-serving-api/image-serving-api/http-protocol-reference/command-reference/req/r-userdata.html). |

## Accentuation {#unsharp-mask}

Utilisez le masque **[!UICONTROL Accentuation]** pour affiner l’effet d’un filtre d’accentuation sur l’image finale sous-échantillonnée. Vous pouvez contrôler l’intensité de l’effet, le rayon de l’effet (mesuré en pixels) et un seuil de contraste qui est ignoré. Cet effet utilise les mêmes options que le filtre *Accentuation* d’Adobe Photoshop.

>[!NOTE]
>
>Le masque flou est appliqué uniquement aux rendus réduits au sein du PTIFF (pyramid tiff), dont la résolution est réduite de plus de 50 %. Cela signifie que les rendus de plus grande taille dans le ptiff ne sont pas affectés par le masquage flou, tandis que les rendus de plus petite taille, tels que les miniatures, sont modifiés (et affichent le masque flou).

L’option **[!UICONTROL Accentuation]** propose les options de filtre suivantes :

| Option | Description |
| --- | --- |
| Quantité | Contrôle le degré de contraste appliqué aux pixels de contour. La valeur par défaut est 1.75. Pour les images à haute résolution, vous pouvez l’augmenter jusqu’à 5. Considérez la quantité comme une mesure de l’intensité du filtre. La plage est 0 à 5. |
| Rayon | Détermine le nombre de pixels entourant les pixels de contour qui affectent l’accentuation. Pour les images à haute résolution, entrez une valeur comprise entre 1 et 2. Une valeur faible accentue uniquement les pixels de contour ; une valeur élevée accentue une bande plus large de pixels. La valeur appropriée dépend de la taille de l’image. La valeur par défaut est 0,2.  La plage est 0 à 250. |
| Seuil | Détermine la plage de contraste à ignorer lorsque le filtre de masquage flou est appliqué. En d’autres termes, cette option définit l’écart recherché entre les pixels et la zone environnante avant qu’ils ne soient considérés comme des pixels de contour et ne soient accentués. Pour éviter d’introduire du bruit, essayez des valeurs comprises entre 0 et 255. |

L’accentuation est décrite dans [Accentuation des images](/help/assets/assets/sharpening_images.pdf.

## Création de profils d’image Dynamic Media {#creating-image-profiles}

Pour définir des paramètres de traitement avancés pour d’autres types de ressources, voir [Configuration du traitement des ressources](config-dms7.md#configuring-asset-processing).

Voir [Profils de traitement des métadonnées, des images et des vidéos](processing-profiles.md).

Consultez également la section [Bonnes pratiques pour organiser vos ressources numériques en vue d’utiliser des profils de traitement](/help/assets/organize-assets.md).

**Pour créer des profils d’image Dynamic Media :**

1. Sélectionnez le logo Adobe Experience Manager et accédez à **[!UICONTROL Outils]** > **[!UICONTROL Ressources]** > **[!UICONTROL Profils d’image]**.
1. Sélectionnez **[!UICONTROL Créer]** afin d’ajouter un profil d’image.
1. Saisissez un nom de profil et les valeurs pour une accentuation, un recadrage et un échantillon.

   Utilisez un nom de profil spécifique à son objectif prévu. Par exemple, si vous souhaitez créer un profil qui génère des échantillons uniquement (c’est-à-dire que le recadrage intelligent est désactivé (désactivé) et que l’échantillon de couleur et d’image est activé), utilisez le nom de profil &quot;Nuancier intelligent&quot;.

   Voir aussi [Options de recadrage intelligent et d’échantillonnage intelligent](#crop-options) et [Accentuation](#unsharp-mask).

   ![recadrer](assets/crop.png)

1. Sélectionnez **[!UICONTROL Enregistrer]**. Le profil nouvellement créé apparaît dans la liste des profils disponibles.

## Modification ou suppression de profils d’image Dynamic Media {#editing-or-deleting-image-profiles}

1. Sélectionnez le logo du Experience Manager et accédez à **[!UICONTROL Outils]** > **[!UICONTROL Ressources]** > **[!UICONTROL Profils d’image]**.
1. Sélectionnez le profil d’image à modifier ou à supprimer. Pour le modifier, sélectionnez **[!UICONTROL Modifier le profil d’image]**. Pour le supprimer, sélectionnez **[!UICONTROL Supprimer le profil d’image]**.

   ![chlimage_1-254](assets/chlimage_1-254.png)

1. En cas de modification, enregistrez les modifications ; en cas de suppression, confirmez la suppression du profil.

## Application d’un profil d’image Dynamic Media à des dossiers {#applying-an-image-profile-to-folders}

Lorsque vous affectez un profil d’image à un dossier, tout sous-dossier hérite automatiquement du profil de son dossier parent. Ce workflow signifie que vous ne pouvez affecter qu’un seul profil d’image à un dossier. Ainsi, réfléchissez soigneusement à la structure de dossiers de l’emplacement où vous téléchargez, stockez, utilisez et archivez les ressources.

Si vous avez affecté un profil d’image différent à un dossier, le nouveau profil remplace le précédent. Les ressources du dossier précédent restent inchangées. Le nouveau profil sera appliqué aux ressources ajoutées ultérieurement au dossier.

Les dossiers auxquels un profil est affecté sont indiqués dans l’interface utilisateur à l’aide du nom de profil qui apparaît dans la carte.

<!-- When you add smart crop to an existing image profile, you need to re-trigger the [DAM Update Asset workflow](assets-workflow.md) if you want to generate crops for existing assets in your asset repository. -->

Vous pouvez appliquer des profils d’image à des dossiers spécifiques, ou de façon globale à toutes les ressources.

Vous pouvez retraiter des ressources dans un dossier qui comporte déjà un profil d’image que vous avez modifié. Voir [Retraiter les ressources dans un dossier après avoir modifié son profil de traitement](processing-profiles.md#reprocessing-assets).

### Application de profils d’image Dynamic Media à des dossiers spécifiques {#applying-image-profiles-to-specific-folders}

Vous pouvez appliquer un profil d’image à un dossier à partir du menu **[!UICONTROL Outils]**, ou si vous êtes dans le dossier, via **[!UICONTROL Propriétés]**. Cette section décrit comment appliquer des profils d’image aux dossiers de deux manières.

Dans le cas des dossiers auxquels un profil est déjà affecté, le nom du profil est affiché directement sous celui du dossier.

Vous pouvez traiter une nouvelle fois des ressources dans un dossier qui comporte déjà un profil vidéo que vous avez modifié. Voir [Retraiter les ressources dans un dossier après avoir modifié son profil de traitement](processing-profiles.md#reprocessing-assets).

#### Application de profils d’image Dynamic Media à des dossiers à partir de l’interface utilisateur des profils {#applying-image-profiles-to-folders-from-profiles-user-interface}

1. Sélectionnez le logo du Experience Manager et accédez à **[!UICONTROL Outils]** > **[!UICONTROL Ressources]** > **[!UICONTROL Profils d’image]**.
1. Sélectionnez le profil d’image à appliquer à un ou plusieurs dossiers.

   ![chlimage_1-255](assets/chlimage_1-255.png)

1. Sélectionnez **[!UICONTROL Appliquer le profil de traitement aux dossiers]** et sélectionnez le ou les dossiers que vous souhaitez utiliser pour recevoir les ressources nouvellement chargées, puis sélectionnez **[!UICONTROL Appliquer]**. Dans le cas des dossiers auxquels un profil est déjà affecté, le nom du profil est affiché directement sous celui du dossier.

#### Application de profils d’image Dynamic Media aux dossiers à partir des propriétés {#applying-image-profiles-to-folders-from-properties}

1. Sélectionnez le logo de l’Experience League et accédez à **[!UICONTROL Ressources]**. Accédez ensuite au dossier parent du dossier auquel vous souhaitez appliquer un profil d’image.
1. Dans le dossier, cochez la case pour la sélectionner, puis sélectionnez **[!UICONTROL Propriétés]**.
1. Sélectionnez l’onglet **[!UICONTROL Profils d’image.]** Dans la liste déroulante **[!UICONTROL Nom du profil]**, sélectionnez le profil, puis **[!UICONTROL Enregistrer et fermer]**. Dans le cas des dossiers auxquels un profil est déjà affecté, le nom du profil est affiché directement sous celui du dossier.

   ![chlimage_1-256](assets/chlimage_1-256.png)

### Application globale d’un profil d’image Dynamic Media {#applying-an-image-profile-globally}

En plus d’appliquer un profil à un dossier, vous pouvez en appliquer un de façon globale, de sorte que tout contenu chargé dans Experience Manager Assets soit traité par ce profil, indifféremment du dossier.

Vous pouvez traiter une nouvelle fois des ressources dans un dossier qui comporte déjà un profil vidéo que vous avez modifié. Voir [Retraitement des ressources dans un dossier après avoir modifié son profil de traitement](processing-profiles.md#reprocessing-assets).

**Pour appliquer globalement un profil d’image Dynamic Media :**

1. Utilisez l’une des méthodes suivantes :

   * Accédez à `https://&lt;AEM server&gt;/mnt/overlay/dam/gui/content/assets/foldersharewizard.html/content/dam` et appliquez le profil approprié, puis sélectionnez **[!UICONTROL Enregistrer]**.

      ![chlimage_1-257](assets/chlimage_1-257.png)

   * Accédez au nœud suivant de CRXDE Lite : `/content/dam/jcr:content`.

      Ajoutez la propriété `imageProfile:/conf/global/settings/dam/adminui-extension/imageprofile/<name of image profile>` et sélectionnez **[!UICONTROL Enregistrer tout]**.

      ![configure_image_profiles](assets/configure_image_profiles.png)

## Modification du recadrage intelligent ou de l’échantillon intelligent d’une seule image {#editing-the-smart-crop-or-smart-swatch-of-a-single-image}

>[!NOTE]
>
>Le recadrage intelligent est disponible uniquement dans le mode Scene7 de Dynamic Media.

Vous pouvez réaligner ou redimensionner manuellement la fenêtre de recadrage intelligent d’une image pour affiner davantage son point focal.

Une fois que vous avez modifié et enregistré un recadrage intelligent, le changement est propagé partout où vous utilisez le recadrage des images spécifiques.

Vous pouvez exécuter à nouveau le recadrage intelligent pour générer des recadrages supplémentaires, si nécessaire.

Voir aussi [Modification du recadrage intelligent ou de l’échantillon intelligent de plusieurs images](#editing-the-smart-crop-or-smart-swatch-of-multiple-images).

**Pour modifier le recadrage intelligent ou l’échantillon intelligent d’une seule image :**

1. Sélectionnez le logo du Experience Manager et accédez à **[!UICONTROL Ressources]**, puis au dossier auquel est appliqué un profil d’image de recadrage intelligent ou d’échantillon intelligent.

1. Sélectionnez le dossier pour pouvoir ouvrir son contenu.
1. Sélectionnez l’image dont vous souhaitez ajuster le recadrage intelligent ou l’échantillon intelligent.
1. Dans la barre d’outils, sélectionnez **[!UICONTROL Recadrage intelligent]**.

1. Procédez de l’une des manières suivantes :

   * Près du coin supérieur droit de la page, faites glisser le curseur vers la gauche ou vers la droite pour augmenter ou réduire l’affichage de l’image, respectivement.
   * Dans l’image, faites glisser une poignée d’angle pour régler la taille de la zone visible du recadrage ou de l’échantillon.
   * Dans l’image, faites glisser la zone/l’échantillon vers un nouvel emplacement. Vous pouvez modifier uniquement les échantillons d’images ; les échantillons de couleurs sont statiques.
   * Au-dessus de l’image, sélectionnez **[!UICONTROL Rétablir]** pour annuler toutes vos modifications et restaurer le recadrage ou l’échantillon d’origine.

1. Près du coin supérieur droit de la page, sélectionnez **[!UICONTROL Enregistrer]**, puis sélectionnez **[!UICONTROL Fermer]** pour revenir au dossier des ressources.

## Modification du recadrage intelligent ou de l’échantillon intelligent de plusieurs images {#editing-the-smart-crop-or-smart-swatch-of-multiple-images}

Après avoir appliqué un profil d’image (contenant un recadrage intelligent) à un dossier, un recadrage est appliqué à toutes les images de ce dossier. Si vous le souhaitez, vous pouvez réaligner ou redimensionner *manuellement* la fenêtre de recadrage intelligent dans plusieurs images pour affiner davantage leur point focal.

Une fois que vous avez modifié et enregistré un recadrage intelligent, le changement est propagé partout où vous utilisez le recadrage des images spécifiques.

Vous pouvez exécuter à nouveau le recadrage intelligent pour générer des recadrages supplémentaires, si nécessaire.

**Pour modifier le recadrage intelligent ou l’échantillon intelligent de plusieurs images :**

1. Sélectionnez le logo du Experience Manager et accédez à **[!UICONTROL Ressources]**, puis à un dossier auquel est appliqué un profil d’image de recadrage intelligent ou d’échantillon intelligent.
1. Dans le dossier, sélectionnez l’icône **[!UICONTROL Autres actions]** (...), puis sélectionnez **[!UICONTROL Recadrage intelligent]**.

1. Sur la page **[!UICONTROL Modifier les recadrages intelligents]**, utilisez l’une des méthodes suivantes :

   * Ajustez la taille d’affichage des images sur la page.

      À droite de la liste déroulante de noms de points d’arrêt, faites glisser le curseur vers la gauche ou la droite pour modifier la taille de l’affichage d’image visible.

      ![edit_smart_crops-sliderbar](assets/edit_smart_crops-sliderbar.png)

   * Vous pouvez filtrer la liste des images visibles en fonction des noms de points d’arrêt. Dans l’exemple ci-dessous, les images sont filtrées en fonction du nom de point d’arrêt « Moyenne ».

      Près du coin supérieur droit de la page, dans la liste déroulante, sélectionnez un nom de point d’arrêt pour filtrer les images que vous souhaitez voir (voir l’image ci-dessus).

      ![edit_smart_crops-dropdownlist](assets/edit_smart_crops-dropdownlist.png)

   * Redimensionnez la zone de recadrage intelligent. Effectuez l’une des opérations suivantes :

      * Si l’image comporte un recadrage intelligent ou un échantillon intelligent uniquement, faites glisser sur celle-ci la poignée de l’angle de la zone de recadrage pour ajuster la taille de la zone visible du recadrage.
      * Si l’image comporte à la fois un recadrage intelligent et un échantillon intelligent, faites glisser sur celle-ci la poignée de l’angle de la zone de recadrage pour ajuster la taille de la zone visible du recadrage. Vous pouvez également sélectionner l’échantillon intelligent sous l’image (les échantillons de couleurs sont statiques), puis faire glisser la poignée de l’angle de la zone de recadrage pour ajuster la taille de la zone visible de l’échantillon.

      ![Redimensionnement du recadrage intelligent d’une image](assets/edit_smart_crops-resize.png)

   * Déplacez la zone de recadrage intelligent. Effectuez l’une des opérations suivantes :

      * Si l’image comporte un recadrage intelligent ou un échantillon intelligent uniquement, faites glisser sur celle-ci la zone de recadrage vers un nouvel emplacement.
      * Si l’image comporte à la fois un recadrage intelligent et un échantillon intelligent, faites glisser sur celle-ci la zone de recadrage intelligent vers un nouvel emplacement. Vous pouvez également sélectionner l’échantillon intelligent sous l’image (les échantillons de couleurs sont statiques), puis faire glisser la zone de recadrage d’échantillon intelligent vers un nouvel emplacement.

      ![edit_smart_crops-move](assets/edit_smart_crops-move.png)

   * Annulez toutes vos modifications et rétablissez le recadrage intelligent ou l’échantillon intelligent d’origine (s’applique à la session de modification active uniquement).

      Sélectionnez **[!UICONTROL Rétablir]** au-dessus de l’image.

      ![edit_smart_crops-revert](assets/edit_smart_crops-revert.png)



1. Près du coin supérieur droit de la page, sélectionnez **[!UICONTROL Enregistrer]**, puis sélectionnez **[!UICONTROL Fermer]** pour revenir au dossier des ressources.

## Suppression d’un profil d’image Dynamic Media d’un dossier {#removing-an-image-profile-from-folders}

Lorsque vous supprimez un profil d’image d’un dossier, tout sous-dossier hérite automatiquement de la suppression du profil de son dossier parent. Cependant, le traitement des fichiers qui s’est produit dans les dossiers reste intact.

Vous pouvez supprimer un profil d’image appliqué à un dossier dans le menu **[!UICONTROL Outils]**, ou si vous êtes dans le dossier, via **[!UICONTROL Propriétés]**. Cette section décrit comment supprimer des profils d’image appliqués aux dossiers en utilisant les deux procédures.

### Suppression de profils d’image Dynamic Media des dossiers à l’aide de l’interface utilisateur Profils {#removing-image-profiles-from-folders-via-profiles-user-interface}

1. Sélectionnez le logo du Experience Manager et accédez à **[!UICONTROL Outils]** > **[!UICONTROL Ressources]** > **[!UICONTROL Profils d’image]**.
1. Sélectionnez le profil d’image à supprimer d’un ou de plusieurs dossiers.
1. Sélectionnez **[!UICONTROL Supprimer le profil de traitement des dossiers]** , sélectionnez le ou les dossiers desquels vous souhaitez supprimer le profil, puis sélectionnez **[!UICONTROL Supprimer]**.

   Le fait que le nom du profil n’apparaît plus sous celui du dossier indique que le profil d’image n’est plus appliqué à un dossier.

### Suppression de profils d’image Dynamic Media des dossiers au moyen des propriétés {#removing-image-profiles-from-folders-via-properties}

1. Sélectionnez le logo du Experience Manager et accédez à **[!UICONTROL Ressources]** , puis au dossier duquel vous souhaitez supprimer un profil d’image.
1. Dans le dossier, cochez la case pour la sélectionner, puis sélectionnez **[!UICONTROL Propriétés]**.
1. Sélectionnez l’onglet **[!UICONTROL Profils d’image]**.
1. Dans la liste déroulante **[!UICONTROL Nom du profil]**, sélectionnez **[!UICONTROL Aucun]**, puis sélectionnez **[!UICONTROL Enregistrer et fermer]**.

   Dans le cas des dossiers auxquels un profil est déjà affecté, le nom du profil est affiché directement sous celui du dossier.
