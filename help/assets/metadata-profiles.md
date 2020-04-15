---
title: de métadonnées pour personnaliser les exigences de métadonnées des ressources
description: Découvrez les profils de métadonnées pour les ressources. Apprenez à créer un profil de métadonnées et à l’appliquer aux ressources d’un dossier.
contentOwner: AG
translation-type: tm+mt
source-git-commit: c7d0bcbf39adfc7dfd01742651589efb72959603

---


# Profils de métadonnées {#metadata-profiles}

Un de métadonnées vous permet d’appliquer des métadonnées par défaut aux fichiers d’un dossier. Créez un de métadonnées et appliquez-le à un dossier. Tout fichier que vous téléchargez ensuite vers le dossier hérite des métadonnées par défaut que vous avez configurées dans le  de métadonnées.

## Ajout d’un profil de métadonnées {#adding-a-metadata-profile}

1. Accédez à **[!UICONTROL Outils > Ressources >]** de métadonnées et appuyez sur **[!UICONTROL Créer]**.
1. Enter a title for the Metadata Profile, for example Sample Metadata, and tap **[!UICONTROL Create]**. The [!UICONTROL Edit Form] for the metadata profile is displayed.

   ![chlimage_1-197](assets/chlimage_1-480.png)

1. Cliquez sur un composant, puis configurez ses propriétés dans l’onglet **[!UICONTROL Paramètres]**. Cliquez par exemple sur le composant **[!UICONTROL Description]** et modifiez ses propriétés.

   ![chlimage_1-198](assets/chlimage_1-481.png)

   Modifiez les propriétés suivantes pour le composant **[!UICONTROL Description]** :

   * **[!UICONTROL Libellé]** du champ : Nom d’affichage de la propriété de métadonnées. Il est uniquement disponible à titre de référence.

   * **[!UICONTROL Associer à la propriété]**: La valeur de cette propriété fournit le chemin/nom relatif au noeud de ressource où elle est enregistrée dans le référentiel. La valeur doit toujours  avec `./` car elle indique que le chemin d’accès se trouve sous le noeud de la ressource.
   ![chlimage_1-199](assets/chlimage_1-482.png)

   La valeur que vous indiquez pour **[!UICONTROL Associer à la propriété]** est stockée en tant que propriété sous le nœud de métadonnées de la ressource. Par exemple, si vous spécifiez . `/jcr:content/metadata/dc:desc` comme nom pour **[!UICONTROL Associer à la propriété]**, AEM Assets stocke la valeur `dc:desc` comme nœud de métadonnées de la ressource.

   * **[!UICONTROL Valeur par défaut]** : utilisez cette propriété pour ajouter une valeur par défaut pour le composant des métadonnées. Par exemple, si vous indiquez « Ma description », cette valeur est affectée à la propriété `dc:desc` au niveau du nœud de métadonnées de la ressource.
   ![chlimage_1-200](assets/chlimage_1-483.png)

   >[!NOTE]
   >
   >Si vous ajoutez une valeur par défaut à une nouvelle propriété de métadonnées (qui n’existe pas encore au niveau du nœud `/jcr:content/metadata`), la propriété et sa valeur ne s’affichent pas, par défaut, sur la page Propriétés de la ressource. To view the new property on the assets&#39; [!UICONTROL Properties] page, modify the corresponding schema form.

1. (Facultatif) Ajoutez d’autres composants à la page Modifier le formulaire depuis l’onglet **[!UICONTROL Créer le formulaire]**, puis configurez leurs propriétés dans l’onglet **[!UICONTROL Paramètres]**. Les propriétés suivantes sont disponibles à partir de l’onglet **[!UICONTROL Créer le formulaire]** :

| Composant | Propriétés |
|---|---|
| [!UICONTROL En-tête de section] | Field Label, <br> Description |
| [!UICONTROL Une seule ligne de texte] | Field Label, <br> Map to property, <br> Default Value |
| [!UICONTROL Texte à plusieurs valeurs] | Field Label, <br> Map to property, <br> Default Value |
| [!UICONTROL Nombre] | Field Label, <br> Map to property, <br> Default Value |
| [!UICONTROL Date] | Field Label, <br> Map to property, <br> Default Value |
| [!UICONTROL Balises standard] | Field Label, <br> Map to property, <br> Default Value, <br> Description |

![chlimage_1-201](assets/chlimage_1-484.png)

1. Appuyez/cliquez sur **[!UICONTROL Terminé]**. Le profil de métadonnées est ajouté à la liste des profils de la page **[!UICONTROL Profils de métadonnées]**.<br>


   ![de métadonnées ajouté dans la page  du de métadonnées](assets/MetadataProfiles-page.png)

## Copie d’un profil de métadonnées {#copying-a-metadata-profile}

1. From the **[!UICONTROL Metadata Profiles]** page, select a metadata profile to make a copy of it.

   ![chlimage_1-203](assets/chlimage_1-486.png)

1. Appuyez sur **[!UICONTROL Copier]** dans la barre d’outils.
1. Dans la boîte de dialogue **[!UICONTROL Copier le profil de métadonnées]**, saisissez le nom de la nouvelle copie du profil de métadonnées.
1. Appuyez sur **[!UICONTROL Copier]**. La copie du profil de métadonnées apparaît dans la liste des profils de la page **[!UICONTROL Profils de métadonnées]**.

   ![Une copie du de métadonnées  ajoutée à la page du de métadonnées](assets/copy-metadata-profile.png)

## Suppression d’un profil de métadonnées {#deleting-a-metadata-profile}

1. Dans la page **[!UICONTROL Profils de métadonnées]**, sélectionnez un profil à supprimer.

   ![chlimage_1-205](assets/chlimage_1-488.png)

1. Ta[] **[!UICONTROL Delete Metadata Profiles]** in the toolbar.
1. Dans la boîte de dialogue, cliquez sur **[!UICONTROL Supprimer]** pour confirmer l’opération de suppression. Le profil de métadonnées est supprimé de la liste.

## Application d’un profil de métadonnées à des dossiers {#applying-a-metadata-profile-to-folders}

Lorsque vous affectez un profil de métadonnées à un dossier, tout sous-dossier hérite automatiquement du profil de son dossier parent. Cela signifie que vous ne pouvez affecter qu’un seul profil de métadonnées à un dossier. Nous vous conseillons donc de choisir avec la plus grande attention la structure du dossier dans lequel vous transférez, stockez, utilisez et archivez des ressources.

Si vous avez affecté un profil de métadonnées différent à un dossier, le nouveau profil remplace le précédent. Les ressources du dossier précédent restent inchangées. Le nouveau profil est appliqué aux ressources ajoutées ultérieurement au dossier.

Les dossiers auxquels un profil est affecté sont indiqués dans l’interface utilisateur par le nom du profil apparaissant dans le nom de la carte.

![chlimage_1-206](assets/chlimage_1-489.png)

Vous pouvez appliquer des profils de métadonnées à des dossiers spécifiques ou à l’ensemble des ressources.

Vous pouvez retraiter des ressources dans un dossier qui comporte déjà un profil de métadonnées que vous avez modifié ultérieurement. Voir [Retraitement des ressources dans un dossier après avoir modifié son profil de traitement](processing-profiles.md#reprocessing-assets).

### Application de profils de métadonnées à des dossiers spécifiques {#applying-metadata-profiles-to-specific-folders}

Vous pouvez appliquer un profil de métadonnées à un dossier à partir du menu **[!UICONTROL Outils]** ou, si vous êtes dans le dossier, à partir de **[!UICONTROL Propriétés]**. Cette section décrit comment appliquer des profils de métadonnées aux dossiers des deux manières.

Dans le cas des dossiers auxquels un profil est déjà affecté, le nom du profil est affiché directement sous celui du dossier.

Vous pouvez retraiter des ressources dans un dossier qui comporte déjà un profil vidéo que vous avez modifié. Voir [Retraitement des ressources dans un dossier après avoir modifié son profil de traitement](processing-profiles.md#reprocessing-assets).

#### Application de profils de métadonnées à des dossiers à partir de l’interface utilisateur des profils {#applying-metadata-profiles-to-folders-from-profiles-user-interface}

Pour appliquer le de métadonnées, procédez comme suit :

1. Appuyez sur le logo AEM et accédez à **[!UICONTROL Outils > Ressources > Profils de métadonnées]**.
1. Sélectionnez le profil de métadonnées à appliquer à un ou à plusieurs dossiers.

   ![chlimage_1-207](assets/chlimage_1-490.png)

1. Appuyez sur **[!UICONTROL Appliquer le profil de métadonnées au ou aux dossiers]** et sélectionnez ensuite le(s) dossier(s) que vous souhaitez utiliser pour recevoir les ressources récemment chargées. Ensuite, appuyez sur **[!UICONTROL Terminé]**. Dans le cas des dossiers auxquels un profil est déjà affecté, le nom du profil est affiché directement sous celui du dossier.

#### Application de profils de métadonnées aux dossiers à partir des propriétés {#applying-metadata-profiles-to-folders-from-properties}

1. Dans le rail de gauche, appuyez sur **[!UICONTROL Ressources]**, puis accédez au dossier auquel vous souhaitez appliquer un profil de métadonnées.
1. Dans le dossier, appuyez ou cliquez sur la coche afin de la sélectionner, puis appuyez ou cliquez sur **[!UICONTROL Propriétés]**.

1. Select the **[!UICONTROL Metadata Profiles]** tab and select the profile from the drop-down menu and tap **[!UICONTROL Save]**.

   ![chlimage_1-208](assets/chlimage_1-491.png)

   Dans le cas des dossiers auxquels un profil est déjà affecté, le nom du profil est affiché directement sous celui du dossier.

### Application d’un profil de métadonnées à l’ensemble des ressources {#applying-a-metadata-profile-globally}

En plus d’appliquer un profil à un dossier, vous pouvez en appliquer un de façon globale, de sorte que tout contenu chargé dans AEM Assets soit traité par ce profil, indifféremment du dossier.

Vous pouvez retraiter des ressources dans un dossier qui comporte déjà un profil de métadonnées que vous avez modifié ultérieurement. Voir [Retraitement des ressources dans un dossier après avoir modifié son profil de traitement](processing-profiles.md#reprocessing-assets).

**Pour appliquer un profil de façon globale, effectuez l’une des opérations suivantes :**

* Accédez à `https://[aem_server]:[port]/mnt/overlay/dam/gui/content/assets/foldersharewizard.html/content/dam` et appliquez le profil approprié, puis appuyez sur **[!UICONTROL Enregistrer]**.

   ![chlimage_1-209](assets/chlimage_1-492.png)

* Accédez au nœud suivant de CRXDE Lite : `/content/dam/jcr:content`. Ajoutez la propriété `metadataProfile:/etc/dam/metadata/dynamicmedia/<name of metadata profile>` et appuyez sur **Tout enregistrer**.

   ![chlimage_1-210](assets/chlimage_1-493.png)

## Remove a metadata profile from folders {#removing-a-metadata-profile-from-folders}

Lorsque vous supprimez un profil de métadonnées d’un dossier, tout sous-dossier hérite automatiquement de la suppression du profil de son dossier parent. Cependant, le traitement des fichiers qui s’est produit dans les dossiers reste intact.

Vous pouvez supprimer un profil de métadonnées d’un dossier à partir du menu **[!UICONTROL Outils]** ou, si vous êtes dans le dossier, à partir de **[!UICONTROL Propriétés]**. Cette section décrit comment supprimer des profils de métadonnées des dossiers des deux manières.

### Remove metadata profiles from folders via Profiles user interface {#removing-metadata-profiles-from-folders-via-profiles-user-interface}

1. Appuyez ou cliquez sur le logo AEM et accédez à **[!UICONTROL Outils > Ressources > Profils de métadonnées]**.
1. Sélectionnez le profil de métadonnées à supprimer d’un ou de plusieurs dossiers.
1. Appuyez sur **[!UICONTROL Supprimer le profil de métadonnées du ou des dossiers]** et sélectionnez ensuite le(s) dossier(s) duquel (desquels) vous souhaitez supprimer le profil. Ensuite, appuyez sur **[!UICONTROL Terminé]**.

   Le fait que le nom du profil n’apparaît plus sous celui du dossier indique que le profil de métadonnées n’est plus appliqué à un dossier.

### Remove metadata profiles from folders via Properties {#removing-metadata-profiles-from-folders-via-properties}

1. Appuyez sur le logo AEM, puis accédez à **[!UICONTROL Ressources]** et au dossier duquel vous souhaitez supprimer un profil de métadonnées.
1. Dans le dossier, appuyez sur la coche pour la sélectionner, puis sur **[!UICONTROL Propriétés]**.
1. Sélectionnez l’onglet **[!UICONTROL Profils de métadonnées]**, puis **[!UICONTROL Aucun]** dans le menu déroulant, et cliquez sur **[!UICONTROL Enregistrer]**. Dans le cas des dossiers auxquels un profil est déjà affecté, le nom du profil est affiché directement sous celui du dossier.

>[!MORELIKETHIS]
>
>* [de traitement des métadonnées, des images et des vidéos](processing-profiles.md)
>* [Bonnes pratiques pour organiser vos ressources numériques afin d’utiliser les de traitement](/help/assets/organize-assets.md)

