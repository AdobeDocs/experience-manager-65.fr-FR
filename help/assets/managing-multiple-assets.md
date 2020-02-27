---
title: Gestion de plusieurs ressources et collections
description: Découvrez comment modifier les métadonnées de plusieurs ressources et collections simultanément pour propager rapidement les modifications courantes des métadonnées.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 9af0ee0ff9d1089b6cf09c52f7f606cce6775d72

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
1. Pour ajouter les nouvelles métadonnées aux métadonnées existantes dans les champs qui contiennent plusieurs valeurs, sélectionnez le mode **[!UICONTROL Ajouter]**. Si vous ne sélectionnez pas cette option, les nouvelles métadonnées remplacent les métadonnées existantes dans les champs. Appuyez/cliquez sur **[!UICONTROL Envoyer]**.

   >[!CAUTION]
   >
   >Pour les champs à une valeur, les nouvelles métadonnées ne sont pas ajoutées à la valeur existante dans le champ, même si vous sélectionnez le **[!UICONTROL mode Ajouter]**.

## Configuration du nombre maximal de paramètres pour la mise à jour des métadonnées en masse {#configlimit}

Pour éviter une situation similaire à DOS, AEM limite le nombre de paramètres pris en charge dans une requête Sling. Lors de la mise à jour simultanée de plusieurs fichiers, vous pouvez atteindre le nombre maximal de paramètres et les métadonnées ne sont pas mises à jour pour d’autres fichiers. AEM génère l’avertissement suivant dans les journaux :

`org.apache.sling.engine.impl.parameters.Util Too many name/value pairs, stopped processing after 10000 entries`

Pour modifier cette limite, accédez à la console web ( **[!UICONTROL Outils]** > **[!UICONTROL Opérations]** > **[!UICONTROL Console web]**) et modifiez la **[!UICONTROL valeur maximale des paramètres POST]** dans la configuration OSGi **[!UICONTROL Gestion des paramètres de requête Sling Apache]**.

>[!MORELIKETHIS]
>
>* [Modification des propriétés de métadonnées de plusieurs collections](managing-collections-touch-ui.md#editing-collection-metadata-in-bulk)

