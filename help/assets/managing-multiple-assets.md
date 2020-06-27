---
title: Gérez les métadonnées de nombreux fichiers et collections dans Adobe Enterprise Manager.
description: Modifiez simultanément les métadonnées de nombreux fichiers et collections afin de propager rapidement les modifications de métadonnées courantes.
contentOwner: AG
translation-type: tm+mt
source-git-commit: a61e1e9ffb132b59c725b2078f09641a3c2a479a
workflow-type: tm+mt
source-wordcount: '495'
ht-degree: 63%

---


# Gestion des ressources et des collections {#managing-multiple-assets-and-collections}

Adobe Enterprise Manager Assets vous permet de modifier simultanément les métadonnées de plusieurs fichiers afin que vous puissiez rapidement propager les modifications de métadonnées courantes aux fichiers en bloc. Vous pouvez également modifier en gros les métadonnées de plusieurs collections.

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
1. From the toolbar, click **[!UICONTROL Properties]** to open the properties page for the selected assets.

   >[!NOTE]
   >
   >Lorsque vous sélectionnez plusieurs ressources, la plus petite forme parent commune est sélectionnée. En d’autres termes, la page de propriétés affiche uniquement les champs de métadonnées communs aux pages de propriétés de tous les fichiers individuels.

1. Modifiez les propriétés de métadonnées des ressources sélectionnées dans les différents onglets.
1. Pour afficher l’éditeur de métadonnées pour une ressource spécifique, désélectionnez les autres ressources de la liste. Les champs de l’éditeur de métadonnées sont renseignés avec les métadonnées de la ressource particulière.

   >[!NOTE]
   >
   >* Dans la page des propriétés, vous pouvez supprimer des ressources de la liste des ressources en les désélectionnant. La liste des ressources contient toutes les ressources sélectionnées par défaut. Les métadonnées des ressources que vous supprimez de la liste ne sont pas mises à jour.
   >* En haut de la liste des ressources, cochez la case située en regard de l’option **[!UICONTROL Titre]** pour passer de la sélection des ressources à l’effacement de la liste, et inversement.


1. To select a different metadata schema for the assets, click **[!UICONTROL Settings]** from the toolbar, and select the desired schema.
1. Enregistrez les modifications.
1. Pour ajouter les nouvelles métadonnées aux métadonnées existantes dans les champs contenant plusieurs valeurs, sélectionnez **[!UICONTROL Mode d’ajout]**. Si vous ne sélectionnez pas cette option, les nouvelles métadonnées remplacent les métadonnées existantes dans les champs. Cliquez sur **[!UICONTROL Envoyer]**.

   >[!CAUTION]
   >
   >Pour les champs à une seule valeur, les nouvelles métadonnées ne sont pas ajoutées à la valeur existante dans le champ même si vous sélectionnez **[!UICONTROL Mode d’ajout]**.

## Configuration du nombre maximal de paramètres pour la mise à jour des métadonnées en masse {#configlimit}

Pour éviter une situation similaire à celle de DOS, Enterprise Manager limite le nombre de paramètres pris en charge dans une requête Sling. Lors de la mise à jour simultanée de plusieurs fichiers, vous pouvez atteindre le nombre maximal de paramètres et les métadonnées ne sont pas mises à jour pour d’autres fichiers. Enterprise Manager génère l’avertissement suivant dans les journaux :

`org.apache.sling.engine.impl.parameters.Util Too many name/value pairs, stopped processing after 10000 entries`

To change the limit, access **[!UICONTROL Tools]** > **[!UICONTROL Operations]** > **[!UICONTROL Web Console]** and change the value of **[!UICONTROL Maximum POST Parameters]** in **[!UICONTROL Apache Sling Request Parameter Handling]** OSGi configuration.

>[!MORELIKETHIS]
>
>* [Modification des propriétés de métadonnées de plusieurs collections](managing-collections-touch-ui.md#editing-collection-metadata-in-bulk)

