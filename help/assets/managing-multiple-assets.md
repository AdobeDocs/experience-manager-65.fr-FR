---
title: Gestion de plusieurs ressources et collections
description: Découvrez comment modifier les métadonnées de plusieurs ressources et collections simultanément pour propager rapidement les modifications courantes des métadonnées.
contentOwner: AG
translation-type: tm+mt
source-git-commit: a39ee0f435dc43d2c2830b2947e91ffdcf11c7f6

---


# Gestion des ressources et des collections {#managing-multiple-assets-and-collections}

Adobe Enterprise Manager (AEM) Assets vous permet de modifier les métadonnées de plusieurs ressources simultanément afin de propager rapidement en gros les modifications de métadonnées communes vers les ressources. Vous pouvez également modifier en gros les métadonnées de plusieurs collections.

Utilisez la page des propriétés pour effectuer des modifications de métadonnées sur plusieurs ressources ou collections :

* Remplacer les propriétés de métadonnées par une valeur commune
* Ajouter ou modifier des balises

Pour personnaliser la page des propriétés de métadonnées, y compris l’ajout, la modification et la suppression de propriétés de métadonnées, utilisez l’éditeur de schéma.

>[!NOTE]
>
>Les méthodes de modification en masse fonctionnent pour les ressources disponibles dans un dossier ou une collection. Pour les ressources disponibles dans plusieurs dossiers ou correspondant à un critère commun, il est possible de mettre à jour [les métadonnées en masse après une recherche](search-assets.md#metadataupdates).

## Edit metadata properties of multiple assets {#editing-metadata-properties-of-multiple-assets}

1. Dans l’interface utilisateur Ressources, accédez à l’emplacement des ressources à modifier.
1. Sélectionnez les ressources dont vous souhaitez modifier les propriétés communes.
1. Sur la barre d’outils, appuyez/cliquez sur l’icône **[!UICONTROL Propriétés]** pour ouvrir la page des propriétés des ressources sélectionnées.

   >[!NOTE]
   >
   >Lorsque vous sélectionnez plusieurs ressources, la plus petite forme parent commune est sélectionnée. En d’autres termes, la page de propriétés affiche uniquement les champs de métadonnées communs aux pages de propriétés de tous les fichiers individuels.

1. Modifiez les propriétés de métadonnées des ressources sélectionnées dans les différents onglets.
1. Pour afficher l’éditeur de métadonnées pour une ressource spécifique, désélectionnez les autres ressources de la liste. Les champs de l’éditeur de métadonnées sont renseignés avec les métadonnées de la ressource particulière.

   >[!NOTE]
   >
   >* Dans la page des propriétés, vous pouvez supprimer des ressources de la liste des ressources en les désélectionnant. La liste des ressources contient toutes les ressources sélectionnées par défaut. Les métadonnées des ressources que vous supprimez de la liste ne sont pas mises à jour.
   >* At the top of assets list, select the check box near **[!UICONTROL Title]** to toggle between selecting the assets and clearing the list.


1. Pour sélectionner un schéma de métadonnées différent pour les ressources, appuyez/cliquez sur l’icône **[!UICONTROL Paramètres]** dans la barre d’outils, puis sélectionnez le schéma souhaité.
1. Enregistrez les modifications.
1. To append the new metadata with the existing metadata in fields that contain multiple values, select **[!UICONTROL Append mode]**. Si vous ne sélectionnez pas cette option, les nouvelles métadonnées remplacent les métadonnées existantes dans les champs. Tap/click **[!UICONTROL Submit]**.

   >[!CAUTION]
   >
   >Pour les champs à une seule valeur, les nouvelles métadonnées ne sont pas ajoutées à la valeur existante dans le champ même si vous sélectionnez **[!UICONTROL Mode d’ajout]**.

## Edit metadata properties of multiple collections {#editing-metadata-properties-of-multiple-collections}

1. Dans la console Collections, sélectionnez les collections à modifier.
1. From the toolbar, tap/click **[!UICONTROL Properties]** to open the properties page for the selected collections.
1. Modifiez les propriétés de métadonnées des collections sélectionnées dans les différents onglets.

   >[!NOTE]
   >
   >Les métadonnées que vous ajoutez pour les collections sélectionnées remplacent les métadonnées précédentes de ces collections, à l’exception des balises. Any tags you add in the **[!UICONTROL Tags]** field, are appended to the existing list of tags in the metadata.

1. Pour afficher les propriétés de métadonnées associées à une collection spécifique, désélectionnez les autres collections dans la liste des collections. Les champs de l’éditeur de métadonnées sont renseignés avec les métadonnées de la collection particulière.

   >[!NOTE]
   >
   >* Dans la page des propriétés de collection, vous pouvez supprimer des collections de la liste des collections en les désélectionnant. La liste des collections contient toutes les collections sélectionnées par défaut. Les métadonnées des collections que vous supprimez ne sont pas mises à jour.
   >* At the top of the list, select the check box near **[!UICONTROL Title]** to toggle between selecting the collections and clearing the list.


1. Enregistrez les modifications.

## Configuration du nombre maximal de paramètres pour la mise à jour des métadonnées en masse {#configlimit}

Pour éviter une situation similaire à DOS, AEM limite le nombre de paramètres pris en charge dans une requête Sling. Lors de la mise à jour simultanée de plusieurs fichiers, vous pouvez atteindre le nombre maximal de paramètres et les métadonnées ne sont pas mises à jour pour d’autres fichiers. AEM génère l’avertissement suivant dans les journaux :

`org.apache.sling.engine.impl.parameters.Util Too many name/value pairs, stopped processing after 10000 entries`

Pour modifier le nombre maximal de paramètres, accédez à la console Web (**[!UICONTROL Outils]** > **[!UICONTROL Opérations]** > **[!UICONTROL Console Web]**), puis changez le **[!UICONTROL nombre maximal de paramètres POST]** dans la configuration OSGi de **[!UICONTROL gestion des paramètres de requête Sling Apache]**.
