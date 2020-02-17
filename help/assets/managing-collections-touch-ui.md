---
title: Gestion des collections de fichiers
description: Apprenez à gérer des collections de ressources, telles que créer, afficher, supprimer, modifier et télécharger des collections.
contentOwner: AG
mini-toc-levels: 1
translation-type: tm+mt
source-git-commit: 0ff23556444fcb161b0adf744bb72fdc50322d92

---


# Manage collections {#managing-collections}

Une collection est un ensemble de ressources dans Adobe Experience Manager (AEM) Assets. Vous pouvez utiliser des collections pour partager des ressources entre utilisateurs.

* Une collection peut comporter des ressources provenant de différents emplacements.
* Vous pouvez partager des ressources avec plusieurs utilisateurs dont les niveaux de privilèges sont différents (modification, affichage, etc.).

Vous pouvez partager plusieurs collections avec un utilisateur. Chaque collection contient des références aux ressources. L’intégrité du référentiel des ressources est préservées dans les collections.

Selon la façon dont elles rassemblent les ressources, les collections sont des types suivants :

* Collection contenant une liste de référence statique des ressources, des dossiers et d’autres collections

* Une collection dynamique qui inclut dynamiquement des ressources en fonction d’un critère de recherche

## Navigate the collections console {#navigating-the-collections-console}

Pour ouvrir la console **[!UICONTROL Collections]**, procédez comme suit :

1. Appuyez ou cliquez sur le logo AEM.
1. From the Navigation page, go to **[!UICONTROL Assets]** > **[!UICONTROL Collections]**. La console **[!UICONTROL Collections]** s’affiche.

## Création d’une collection {#creating-a-collection}

You can create a collection either with [static references](#creating-a-collection-with-static-references) or based on a [search criteria-based filter](#creating-a-smart-collection). Vous pouvez également créer une collection à partir d’une Lightbox.

### Create a collection with static references {#creating-a-collection-with-static-references}

Vous pouvez créer une collection avec des références statiques, par exemple, une collection avec des références aux ressources, aux dossiers, aux collections, aux visionneuses à 360° et aux visionneuses d’images.

1. Accédez à la console **[!UICONTROL Collections]**.
1. From the toolbar, tap/click **[!UICONTROL Create]**.
1. Sur la page **[!UICONTROL Créer une collection]**, saisissez un titre et une description facultative pour la collection.
1. Ajoutez des membres à la collection et attribuez les autorisations appropriées. Vous pouvez également sélectionner **[!UICONTROL Collection publique]** pour permettre à tous les utilisateurs d’accéder à la collection.

   >[!NOTE]
   >
   >Pour permettre aux membres de partager des collections avec d’autres utilisateurs, vous devez accorder les autorisations de lecture au groupe `dam-users` dans le chemin `home/users`. Give permission to the users at `/content/dam/collections` location to allow the users to view the Collections in pop up lists. Vous pouvez également intégrer l’utilisateur au groupe `dam-users`.

1. (Facultatif) Ajoutez une image de miniature pour la collection.
1. Tap/click **[!UICONTROL Create]**, and then tap/click **[!UICONTROL OK]** to close the dialog. Une collection avec le titre et les propriétés spécifiés s’ouvre dans la console Collections.

   >[!NOTE]
   >
   >AEM Assets vous permet de créer des tâches de révision pour une collection de la même façon que vous créez des tâches de révision pour un dossier de ressources.

   Pour ajouter des ressources à la collection, accédez à l’interface utilisateur Assets. Pour plus d’informations, voir [Ajout de ressources à une collection](/help/assets/managing-collections-touch-ui.md#adding-assets-to-a-collection).

### Create collections using dropzone {#create-collections-using-dropzone}

Vous pouvez faire glisser des ressources de l’interface utilisateur Assets jusqu’à une collection. Vous pouvez également créer une copie d’une collection et faire glisser les ressources jusqu’à celle-ci.

1. Dans l’IU Assets, sélectionnez les ressources à ajouter à une collection.
1. Drag the assets to the **[!UICONTROL Drop in Collection]** zone.

   ![drop_in_collection](assets/drop_in_collection.png)

   Release the mouse button when the Dropzone becomes active, and its label changes to **[!UICONTROL Drop to Add]**.

   ![drop_to_add](assets/drop_to_add.png)

   Vous pouvez également appuyer/cliquer sur l’icône **[!UICONTROL À la collection]** de la barre d’outils.

   ![chlimage_1-6](assets/chlimage_1-109.png)

1. In the **[!UICONTROL Add To Collection]** page, tap/click the **[!UICONTROL Create Collection]** icon from the toolbar.

   Si vous souhaitez ajouter les ressources à une collection existante, sélectionnez cette dernière dans la page Sélectionner, puis appuyez/cliquez sur **[!UICONTROL Ajouter]**. Par défaut, la collection mise le plus récemment à jour est sélectionnée.

1. Dans la boîte de dialogue **[!UICONTROL Créer une collection]**, indiquez un nom pour la collection. Si vous souhaitez que la collection soit accessible à tous les utilisateurs, sélectionnez **[!UICONTROL Collection publique]**.
1. Tap/click **[!UICONTROL Continue]** to create the collection.

### Création d’une collection dynamique {#creating-a-smart-collection}

Une collection dynamique utilise des critères de recherche pour rassembler les ressources de manière dynamique. Vous pouvez créer une collection dynamique en utilisant uniquement des fichiers ou en utilisant des fichiers et des dossiers.

1. Navigate to the Assets UI, and tap/click the **[!UICONTROL Search]** icon.
1. Entrez le mot-clé de recherche dans la zone Omnisearch et appuyez sur Entrée. Appuyez/cliquez sur l’icône GlobalNav pour afficher le panneau Filtres et pour appliquer un filtre de recherche à partir du panneau Recherche.
1. Dans la liste **[!UICONTROL Fichiers et dossiers]**, sélectionnez **[!UICONTROL Fichiers]**.

   ![files_option](assets/files_option.png)

1. Appuyez/cliquez sur **[!UICONTROL Enregistrer la collection dynamique]**.
1. Spécifiez le nom de la collection. Sélectionnez **[!UICONTROL Public]** pour ajouter le groupe Utilisateurs DAM avec le rôle Observateur à la collection dynamique.

   ![save_collection](assets/save_collection.png)

   >[!NOTE]
   >
   >If you select **[!UICONTROL Public]**, the smart collection becomes available to everyone with the Owner role after you create it.
   >
   >
   >Si vous désactivez la case à cocher **[!UICONTROL Public]**, le groupe Utilisateurs DAM n’est plus associé à la collection dynamique.

1. Tap/click **[!UICONTROL Save]** to create the smart collection, and then close the message box to complete the process.

   The new smart collection is also added to the **[!UICONTROL Saved Searches]** list.

   ![collection_listing](assets/collection_listing.png)

   The label of the **[!UICONTROL Create Smart Selection]** button changes to **[!UICONTROL Edit Smart Selection]**. To edit the settings of the smart collection, select **[!UICONTROL Files]** from the **[!UICONTROL Files &amp; Folders]** list. Then, tap/click the **[!UICONTROL Edit Smart Selection]** button.

   ![chlimage_1-7](assets/chlimage_1-112.png)

## Add assets to a collection {#adding-assets-to-a-collection}

Vous pouvez ajouter des ressources à une collection qui comporte une liste de ressources ou de dossiers référencés.

>[!NOTE]
>
>Les collections dynamiques utilisent une requête de recherche pour rassembler les ressources. Pour cette raison, les références statiques aux ressources et dossiers ne s’appliquent pas à celles-ci.

1. Dans l’IU AEM, accédez à l’emplacement de la ressource que vous souhaitez ajouter à une collection.
1. Sélectionnez la ressource et appuyez/cliquez sur l’icône **[!UICONTROL À la collection]** dans la barre d’outils.

   ![chlimage_1-8](assets/chlimage_1-113.png)

   Alternatively, you can drag the asset to the **[!UICONTROL Drop in Collection]** zone. Release the mouse button when the drop zone becomes active and its label changes to **[!UICONTROL Drop to Add]**.

1. In the **[!UICONTROL Add To Collection]** page, select the collection to which you want to add the asset.
1. Appuyez/cliquez sur **[!UICONTROL Ajouter]**, puis fermez le message de confirmation. La ressource est ajoutée à la collection.

## Modification d’une collection dynamique {#editing-a-smart-collection}

Smart collections are built by saving a search so you can alter their content by modifying the search parameters of the [saved search](#editing-saved-searches).

1. In the Assets UI, tap/click the **[!UICONTROL Search]** icon from the toolbar.

   ![chlimage_1-9](assets/chlimage_1-110.png)

1. Avec le curseur dans la zone Omnisearch, appuyez sur la touche Retour.
1. Appuyez/cliquez sur l’icône de navigation globale pour afficher le panneau Filtres.
1. Dans la liste **[!UICONTROL Recherches enregistrées]**, sélectionnez la collection dynamique que vous souhaitez modifier. Le panneau de recherche affiche les filtres configurés pour la recherche enregistrée.

   ![select_smart_collection](assets/select_smart_collection.png)

1. Dans la liste **[!UICONTROL Fichiers et dossiers]**, sélectionnez **[!UICONTROL Fichiers]**.
1. Modifiez un ou plusieurs filtres selon vos besoins. Tap/click **[!UICONTROL Edit Smart Collection]**.

   Vous pouvez également modifier le nom de la collection dynamique.

   ![edit_smart_collection_dialog](assets/edit_smart_collectiondialog.png)

1. Appuyez/cliquez sur **[!UICONTROL Enregistrer]**. La boîte de dialogue **[!UICONTROL Modif. collection dynam.]** s’affiche.
1. Appuyez/cliquez sur **[!UICONTROL Remplacer]** pour remplacer la collection dynamique d’origine par la collection modifiée. Sinon, sélectionnez **[!UICONTROL Enregistrer sous]** pour enregistrer la collection modifiée séparément.
1. Dans la boîte de dialogue de confirmation, appuyez/cliquez sur **[!UICONTROL Enregistrer]** pour terminer le processus.

## View and edit collection metadata {#viewing-and-editing-collection-metadata}

Les métadonnées de collection incluent les données sur la collection, notamment toute balise qui est ajoutée.

1. From the Collections console, select a collection and tap/click the **[!UICONTROL Properties]** icon from the toolbar.
1. In the **[!UICONTROL Collection Metadata]** page, view the collection metadata from the **[!UICONTROL Basic]** and **Advanced** tabs.
1. Modify the metadata, as necessary, and then tap/click **[!UICONTROL Save &amp; Close]** from the toolbar to save the changes.

### Edit collection metadata in bulk {#editing-collection-metadata-in-bulk}

Vous pouvez modifier simultanément les métadonnées de plusieurs collections. Cette fonctionnalité vous aide à répliquer rapidement des métadonnées communes dans plusieurs collections.

1. Dans la console Collections, sélectionnez au moins deux collections dont vous souhaitez modifier les métadonnées.
1. From the toolbar, tap/click the **[!UICONTROL Properties]** icon.
1. In the **[!UICONTROL Collection Metadata]** page, edit the metadata under the **[!UICONTROL Basic]** and **[!UICONTROL Advanced]** tabs, as necessary.
1. Tap/click **[!UICONTROL Save &amp; Close]** from the toolbar, and then close the confirmation dialog to complete the process.
1. Pour ajouter les nouvelles métadonnées aux métadonnées existantes, sélectionnez **[!UICONTROL Mode d’ajout]**. Si vous ne sélectionnez pas cette option, les nouvelles métadonnées remplacent les métadonnées existantes dans les champs. Tap/click **[!UICONTROL Submit]**.

   >[!NOTE]
   >
   >Le mode d’ajout fonctionne uniquement avec les champs pouvant contenir plusieurs valeurs. Pour les champs ne pouvant contenir qu’une seule valeur, les nouvelles métadonnées ne sont pas ajoutées à la valeur existante dans le champ, même si vous sélectionnez **[!UICONTROL Mode d’ajout]**.

## Rechercher des collections {#searching-collections}

Vous pouvez effectuer des recherches dans des collections à partir de la console Collections. Lorsque vous effectuez des recherches avec des mots-clés dans la zone Omnisearch, AEM Assets recherche les noms des collections, les métadonnées et les balises ajoutées aux collections.

Si vous recherchez des collections à partir du niveau supérieur, seules les collections individuelles sont renvoyées dans les résultats de recherche. Les ressources ou dossiers à l’intérieur des collections sont exclus. Dans tous les autres cas (par exemple, dans une collection individuelle ou dans une hiérarchie de dossiers), tous les fichiers, dossiers et collections appropriés sont renvoyés.

## Recherche dans les collections {#searching-within-collections}

Dans la console Collections, appuyez/cliquez sur une collection pour l’ouvrir.

Dans une collection, la recherche se limite aux ressources (ainsi qu’aux balises et métadonnées) de la collection en cours d’affichage. Lorsque vous effectuez une recherche dans un dossier, tous les fichiers correspondants et les dossiers enfants du dossier actif sont renvoyés. Lorsque vous effectuez une recherche dans une collection, seuls les fichiers, dossiers et autres collections correspondant aux membres directs de la collection sont renvoyés.

## Modifier les paramètres de la collection {#editing-collection-settings}

Vous pouvez modifier les paramètres d’une collection, tels que le titre et la description, ou ajouter des membres à une collection.

1. Select a collection, and tap/click the **[!UICONTROL Settings]** icon in the toolbar. Vous pouvez également utiliser l’action rapide **[!UICONTROL Paramètres]** à partir de la miniature de la collection.
1. Modify the collection settings in the **[!UICONTROL Collection Settings]** page. For example, modify the collection title, descriptions, members, and permissions as discussed in [Adding Collections](#creating-a-collection).

1. Tap/click **[!UICONTROL Save]** to save the changes.

## Suppression d’une collection {#deleting-a-collection}

1. Dans la console Collections, sélectionnez une ou plusieurs collections et appuyez/cliquez sur l’icône Supprimer dans la barre d’outils.

   ![chlimage_1-11](assets/chlimage_1-177.png)

1. In the dialog, tap/click **[!UICONTROL Delete]** to confirm the delete action.

   >[!NOTE]
   >
   >Vous pouvez également supprimer les collections dynamiques en [supprimant les recherches enregistrées](#deleting-saved-searches).

## Téléchargement d’une collection {#downloading-a-collection}

Lorsque vous téléchargez une collection, l’intégralité de la hiérarchie des ressources de la collection est téléchargée, y compris les dossiers et les collections enfants.

1. Dans la console Collections, sélectionnez une ou plusieurs collections à télécharger.
1. Dans la barre d’outils, appuyez/cliquez sur l’icône de téléchargement.
1. Dans la boîte de dialogue **[!UICONTROL Télécharger]**, appuyez/cliquez sur **[!UICONTROL Télécharger]**. Si vous souhaitez télécharger les rendus des ressources dans la collection, sélectionnez **[!UICONTROL Rendus]**. Sélectionnez l’option **[!UICONTROL Courrier électronique]** pour envoyer une notification électronique au propriétaire de la collection.

   Lorsque vous sélectionnez une collection à télécharger, l’ensemble de la hiérarchie de dossiers sous cette collection est téléchargé. To include each collection you download (including assets in child collections nested under the parent collection) in an individual folder, select **[!UICONTROL Create separate folder for each asset]**.

## Création de collections imbriquées {#creating-nested-collections}

Vous pouvez ajouter une collection à une autre collection, créant ainsi une collection imbriquée.

1. From the Collections console, select the desired collection or group of collections, and tap or click the **[!UICONTROL To Collection]** icon in the toolbar.

   ![chlimage_1-12](assets/chlimage_1-109.png)

1. Sur la page **[!UICONTROL Ajouter à la collection]**, sélectionnez la collection à laquelle vous souhaitez ajouter la collection.

   >[!NOTE]
   >
   >The most recently updated collection is selected by default in the **[!UICONTROL Add To Collection]** page.

1. Appuyez/cliquez sur **[!UICONTROL Ajouter]**. Un message confirme l’ajout de la collection à la collection cible sur la page **[!UICONTROL Sélectionner la destination]**. Fermez le message pour terminer le processus.

>[!NOTE]
>
>Les collections dynamiques ne peuvent pas être imbriquées. En d’autres termes, elles ne peuvent pas comporter d’autres collections.

## Recherches enregistrées {#saved-searches}

Dans l’interface utilisateur Ressources, vous pouvez rechercher ou filtrer des ressources selon des règles, critères de recherche ou facettes de recherche personnalisées. If you save these as **[!UICONTROL Saved Searches]**, you can access them later from the **[!UICONTROL Saved Searches]** list in the Filter panel. La création d’une recherche enregistrée entraîne celle d’une collection dynamique.

![saved_searches_list](assets/saved_searches_list.png)

### Création de recherches enregistrées {#creating-saved-searches}

Les recherches enregistrées sont créées lorsque vous créez une collection dynamique. Les collections dynamiques sont automatiquement ajoutées à la liste Recherches **** enregistrées. The Saved Searches query for the collection is saved in the `dam:query` property in crxde at the relative location `/content/dam/collections/`.

>[!NOTE]
>
>Vous pouvez partager les collections dynamiques comme s’il s’agissait de collections statiques.

### Modifier les recherches enregistrées {#editing-saved-searches}

La modification des recherches enregistrées est identique à celle des collections dynamiques. Pour plus d’informations, voir [Modification d’une collection dynamique](/help/assets/managing-collections-touch-ui.md#editing-a-smart-collection).

### Supprimer les recherches enregistrées {#deleting-saved-searches}

1. Accédez à l’interface utilisateur Ressources, puis appuyez/cliquez sur l’icône Rechercher dans la barre d’outils.

   ![chlimage_1-13](assets/chlimage_1-114.png)

1. Placez le curseur dans la zone de recherche et appuyez sur la touche Entrée.
1. Appuyez ou cliquez sur l’icône de navigation globale afin d’afficher le panneau Filtres.

1. From the **[!UICONTROL Saved Searches]** list, tap **[!UICONTROL Delete]** next to the smart collection that you want to delete.

   ![select_smart_collection-1](assets/select_smart_collection-1.png)

1. In the dialog, tap **[!UICONTROL Delete]** to delete the saved search.

## Execute a workflow on a collection {#running-a-workflow-on-a-collection}

Vous pouvez exécuter un processus pour les ressources d’une collection. Si la collection contient des collections imbriquées, le processus s’exécute également sur les ressources de ces dernières. Toutefois, si la collection et les collections imbriquées contiennent des ressources en double, le processus ne s’exécute qu’une seule fois pour ces ressources.

1. Dans la console Collections, sélectionnez une collection sur laquelle exécuter un processus.
1. Tap/click the GlobalNav icon, and choose **[!UICONTROL Timeline]** from the list.
1. From the timeline, click or tap the Caret icon at the bottom, and then tap **[!UICONTROL Start Workflow]**.

   ![chlimage_1-14](assets/chlimage_1-137.png)

1. Dans la section **[!UICONTROL Démarrer le processus]**, sélectionnez un modèle de processus dans la liste. Sélectionnez par exemple le modèle **[!UICONTROL Ressources de mise à jour de gestion des actifs numériques]**.
1. Saisissez un titre pour le workflow, puis appuyez/cliquez sur **[!UICONTROL Démarrer]**.
1. Dans la boîte de dialogue, appuyez/cliquez sur **[!UICONTROL Poursuivre]**. Le processus s’exécute sur toutes les ressources de la collection.

>[!MORELIKETHIS]
>
>* [Configuration des notifications électroniques d’AEM Assets](/help/sites-administering/notification.md#assetsconfig)
>* [Modification des propriétés de métadonnées de plusieurs collections](/help/assets/managing-multiple-assets.md)
>* [Création d’une tâche de révision pour les collections](/help/assets/bulk-approval.md)

