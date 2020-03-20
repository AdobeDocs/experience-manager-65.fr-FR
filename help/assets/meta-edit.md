---
title: Modification ou ajout de métadonnées
description: Découvrez les métadonnées des ressources dans AEM Assets et les différentes façons de les modifier.
contentOwner: AG
translation-type: tm+mt
source-git-commit: d15273e9308926ca4745fc1045e2da9fe8ed91d4

---


# Modification ou ajout de métadonnées {#how-to-edit-or-add-metadata}

Les métadonnées sont des informations supplémentaires sur la ressource qui peuvent faire l’objet d’une recherche. Elles sont automatiquement extraites lorsque vous chargez une image. Vous pouvez modifier les métadonnées existantes ou ajouter de nouvelles propriétés de métadonnées à des champs existants (par exemple lorsqu’un champ de métadonnées est vide).

Etant donné que  a besoin de vocabulaires de métadonnées contrôlés et fiables, AEM Assets ne permet pas l’ajout ad hoc de nouvelles propriétés de métadonnées. Bien que les auteurs ne puissent pas ajouter de nouveaux champs de métadonnées aux ressources, les développeurs le peuvent. See [Create new metadata property for assets](meta-edit.md#editing-metadata-schema).

## Edit metadata for an asset {#editing-metadata-for-an-asset}

Pour modifier des métadonnées, procédez comme suit :

1. Utilisez l’une des méthodes suivantes :

   * From the Assets UI, select the asset and click/tap the **[!UICONTROL View Properties]** icon from the toolbar.
   * From the asset thumbnail, select the **[!UICONTROL View Properties]** quick action.
   * From the asset page, click/tap the **[!UICONTROL View Properties]** icon from the toolbar.
      ![chlimage_1-168](assets/chlimage_1-168.png)
   *Figure : Icône Propriétés*

   La page de la ressource affiche toutes les métadonnées de celle-ci. Ces métadonnées sont automatiquement extraites lorsqu’elles sont chargées (assimilées) dans AEM Assets.

   ![sélectionner les propriétés du fichier pour  les métadonnées](assets/asset-metadata.png)


   *Figure : Modification ou ajout de métadonnées sur la page Propriétés du fichier*

1. Apportez les modifications nécessaires aux métadonnées sous les différents onglets. Une fois l’opération terminée, cliquez/appuyez sur **[!UICONTROL Enregistrer]** dans la barre d’outils pour enregistrer vos modifications. Cliquez/appuyez sur **[!UICONTROL Fermer]** pour revenir à l’interface web Ressources.

   >[!NOTE]
   >
   >Si un champ de texte est vide, cela signifie qu’aucune métadonnée n’a été définie. Vous pouvez saisir une valeur dans le champ et l’enregistrer pour ajouter cette propriété de métadonnées.

Toute modification des métadonnées d’un fichier est réécrite dans le fichier binaire d’origine dans le cadre de ses données XMP. Cela se fait via le processus d’écriture différée des métadonnées AEM. Les modifications apportées aux propriétés existantes (telles que `dc:title`) sont écrasées et les propriétés qui viennent d’être créées (notamment les propriétés personnalisées telles que `cq:tags`) sont ajoutées en même temps que le schéma.

XMP write-back is supported and enabled for the platforms and file formats described in [technical requirements.](/help/sites-deploying/technical-requirements.md)

## Modifier le schéma de métadonnées {#editing-metadata-schema}

For details on how to edit metadata schema, see [Edit metadata schema forms](metadata-schemas.md#edit-metadata-schema-forms).

## Register a custom namespace within AEM {#registering-a-custom-namespace-within-aem}

Vous pouvez ajouter vos propres espaces de noms à AEM. Tout comme il existe des espaces de noms prédéfinis tels que cq, jcr et sling, vous pouvez disposer d’un espace de noms pour le traitement des données XML et des métadonnées de votre référentiel.

1. Accédez à la page d’administration du type de noeud `https:[aem_server]:[port]/crx/explorer/nodetypes/index.jsp`.
1. Click or tap **[!UICONTROL Namespaces]** at the top of the page. La page d’administration des espaces de noms s’affiche dans une fenêtre.

1. To add a namespace, click or tap **[!UICONTROL New]** at the bottom.
1. Specify a custom namespace in the XML namespace convention (Specify the id in the form of a URI and an associated prefix for the id), and click or tap **[!UICONTROL Save]**.
