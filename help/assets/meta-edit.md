---
title: Modification ou ajout de métadonnées
description: Learn about asset metadata in [!DNL Adobe Experience Manager Assets] an various ways by which you can edit asset metadata.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 4748eed3ce484e8446b641ccbc7b5d76cb66f428
workflow-type: tm+mt
source-wordcount: '436'
ht-degree: 25%

---


# Modification ou ajout de métadonnées {#how-to-edit-or-add-metadata}

Les métadonnées sont des informations supplémentaires sur la ressource qui peuvent faire l’objet d’une recherche. Elles sont automatiquement extraites lorsque vous chargez une image. Vous pouvez modifier les métadonnées existantes ou ajouter de nouvelles propriétés de métadonnées à un champ existant, par exemple lorsqu’un champ de métadonnées est vide.

Les entreprises ont besoin de vocabulaires de métadonnées contrôlés et fiables. Par conséquent, [!DNL Experience Manager Assets] il n’est pas possible d’ajouter à la demande de nouvelles propriétés de métadonnées. Les développeurs et non les auteurs peuvent ajouter de nouveaux champs de métadonnées pour les ressources. Voir [Création d’une propriété de métadonnées pour les fichiers](meta-edit.md#editing-metadata-schema).

## Edit metadata for an asset {#editing-metadata-for-an-asset}

Pour modifier les métadonnées, procédez comme suit :

1. Utilisez l’une des méthodes suivantes :

   * Dans l’ [!DNL Assets] interface, sélectionnez le fichier et cliquez sur Propriétés **[!UICONTROL de la]** Vue dans la barre d’outils.
   * À partir de la miniature de la ressource, sélectionnez l’action rapide **[!UICONTROL Afficher les propriétés]**.
   * Dans la page des ressources, cliquez sur l’icône **[!UICONTROL d’informations sur les]** ressources des propriétés ![de la](assets/do-not-localize/info-circle-icon.png) Vue dans la barre d’outils.

   La page de ressources affiche toutes les métadonnées du fichier. Les métadonnées sont extraites lorsque le fichier est téléchargé (assimilé) dans [!DNL Experience Manager].

   ![Sélectionner les propriétés d’un fichier pour vue ses métadonnées](assets/asset-metadata.png)

   *Figure : Modifiez ou ajoutez des métadonnées sur la page[!UICONTROL Propriétés]du fichier.*

1. Make edits to the metadata under the various tabs, as required, and when completed, click **[!UICONTROL Save]** from the toolbar to save your changes. Click **[!UICONTROL Close]** to return to the [!DNL Assets] web interface.

   >[!NOTE]
   >
   >Si un champ de texte est vide, cela signifie qu’aucune métadonnée n’a été définie. Vous pouvez saisir une valeur dans le champ et l’enregistrer pour ajouter cette propriété de métadonnées.

Toute modification apportée aux métadonnées d’une ressource est écrite dans les données XMP du binaire d’origine. Le processus d’écriture différée des métadonnées ajoute les métadonnées au fichier binaire d’origine. Changes made to the existing properties (such as `dc:title`) are overwritten and new properties (including custom properties like `cq:tags`) are added with the schema.

XMP write-back is supported and enabled for the platforms and file formats described in [technical requirements.](/help/sites-deploying/technical-requirements.md)

## Modifier le schéma de métadonnées {#editing-metadata-schema}

Pour plus d’informations, reportez-vous à la section [Modification de formulaires](metadata-schemas.md#edit-metadata-schema-forms)de schéma de métadonnées.

## Enregistrement d’un espace de nommage personnalisé dans [!DNL Experience Manager] {#registering-a-custom-namespace-within-aem}

Vous pouvez ajouter vos propres espaces de noms à [!DNL Experience Manager]. Just as there are predefined namespaces such as `cq`, `jcr`, and `sling`, you can have a namespace for your repository metadata and XML processing.

1. Accédez à la page d’administration du type de noeud `https://[aem_server]:[port]/crx/explorer/nodetypes/index.jsp`.
1. Pour accéder à la page Administration des espaces de nommage, cliquez sur **[!UICONTROL Espaces de nommage]** en haut de la page.
1. Pour ajouter un espace de nommage, cliquez sur **[!UICONTROL Nouveau]** en bas de la page.
1. Spécifiez un espace de nommage personnalisé dans la convention d’espace de nommage XML. Spécifiez l’identifiant sous la forme d’un URI et d’un préfixe associé pour l’identifiant. Cliquez sur **[!UICONTROL Enregistrer]**.

>[!MORELIKETHIS]
>
>* [À propos des métadonnées et de leurs besoins dans les ressources](metadata.md)
>* [Métadonnées XMP](xmp.md)
>* [Référence du schéma de métadonnées](meta-ref.md)

