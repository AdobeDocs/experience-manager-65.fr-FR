---
title: Facettes de recherche pour filtrer les résultats de la recherche
description: Comment créer, modifier et utiliser les facettes de recherche dans  [!DNL Adobe Experience Manager].
contentOwner: AG
role: Administrateur, développeur
feature: Rechercher
translation-type: tm+mt
source-git-commit: 174e0703ae541641e3dc602e700bcd31624ae62c
workflow-type: tm+mt
source-wordcount: '2427'
ht-degree: 77%

---


# Facettes de recherche {#search-facets}

Un déploiement à l&#39;échelle de l&#39;entreprise de [!DNL Adobe Experience Manager Assets] peut stocker de nombreux actifs. Parfois, trouver le bon fichier peut être ardu et chronophage si vous utilisez uniquement les fonctionnalités de recherche générique de [!DNL Experience Manager].

Utilisez les facettes de recherche dans le panneau Filtres pour ajouter plus de granularité à votre expérience de recherche et rendre ainsi la fonctionnalité de recherche plus efficace et souple. Les facettes de recherche ajoutent des dimensions multiples (prédicats) qui permettent d’effectuer des recherches plus complexes. Le panneau Filtres inclut quelques facettes standard. Vous pouvez également ajouter des facettes de recherche personnalisées.

En résumé, les facettes de recherche permettent de rechercher des ressources de plusieurs façons plutôt que selon un seul ordre taxonomique prédéterminé. Vous pouvez facilement descendre dans la hiérarchie jusqu’au niveau de détail souhaité pour effectuer une recherche plus précise.

Par exemple, si vous recherchez une image, vous pouvez indiquer si vous souhaitez une image bitmap ou vectorielle. Vous pouvez réduire davantage le champ de recherche en spécifiant le type MIME de l’image. De la même façon, si vous recherchez des documents, vous pouvez spécifier le format, par exemple PDF ou MS Word.

## Ajout d’un prédicat {#adding-a-predicate}

Les facettes de recherche qui apparaissent dans le panneau Filtres sont définies dans le formulaire de recherche sous-jacent à l’aide de prédicats. Pour afficher d’autres facettes, ajoutez des prédicats au formulaire par défaut ou utilisez un formulaire personnalisé qui comprend les facettes de votre choix.

Pour les recherches de texte intégral, ajoutez le prédicat [!UICONTROL Texte complet] au formulaire. Utilisez le prédicat Propriété pour rechercher les ressources qui correspondent à une propriété unique que vous spécifiez. Utilisez le prédicat Options pour rechercher les ressources correspondant à une ou plusieurs valeurs pour une propriété spécifique. Ajoutez le prédicat Période pour rechercher les ressources créées au cours d’une période donnée.

1. Cliquez sur le logo [!DNL Experience Manager], puis accédez à **[!UICONTROL Outils]** > **[!UICONTROL Général]** > **[!UICONTROL Rechercher Forms]**.
1. Dans la page Rechercher dans Forms, sélectionnez **[!UICONTROL Actifs Admin Search Rail]**, puis cliquez sur **[!UICONTROL Modifier]** ![icône Modifier](assets/do-not-localize/aemassets_edit.png).

   ![Recherchez et sélectionnez le rail Ressources ou Recherche d’administration.](assets/assets_admin_searchrail.png)

   >[!NOTE]
   >
   >Pour utiliser la fonctionnalité de recherche de dossiers du **rail de recherche d’administration des ressources** préconfiguré à partir d’une version antérieure, effectuez les opérations suivantes :
   >
   >1. Accédez à `/conf/global/settings/dam/search/facets/assets/jcr:content/items` dans CRXDE.
   >1. Supprimez le noeud **type**.
   >1. À partir du chemin d’accès `/libs/settings/dam/search/facets/assets/jcr:content/items`, copiez les noeuds `asset`, `directory`, `typeor`, `excludepaths` et `searchtype` dans le chemin d’accès mentionné à l’étape 1.
   >1. Enregistrez les modifications.


1. Sur la page [!UICONTROL Modifier des formulaires de recherche], faites glisser un prédicat de l’onglet **[!UICONTROL Sélectionner le prédicat]** vers le volet principal. Faites glisser, par exemple, **[!UICONTROL Prédicat de la propriété]**.

   ![Sélectionnez et déplacez un prédicat pour personnaliser les filtres de recherche](assets/drag_predicate.png)

   *Figure : Sélectionner et déplacer un prédicat pour personnaliser les filtres de recherche.*

1. Sous l’onglet [!UICONTROL Paramètres], saisissez un libellé de champ, un texte d’espace réservé et une description pour le prédicat. Indiquez un nom valide pour la propriété de métadonnées que vous souhaitez associer au prédicat. Le libellé de l&#39;en-tête dans l&#39;onglet [!UICONTROL Paramètres] identifie le type du prédicat sélectionné.

1. Dans le champ **[!UICONTROL Nom de la propriété]**, indiquez un nom valide pour la propriété de métadonnées que vous souhaitez associer au prédicat. Il s’agit du nom sur lequel la recherche se base. Par exemple, saisissez `jcr:content/metadata/dc:description` ou `./jcr:content/metadata/dc:description`.

   Vous pouvez également sélectionner un nœud existant dans la boîte de dialogue de sélection.

   ![Associez une propriété de métadonnées à un prédicat dans le champ Nom de propriété](assets/property_settings.png)

   Associez une propriété de métadonnées à un prédicat dans le champ Nom de propriété

1. Cliquez sur **[!UICONTROL Aperçu]** ![aperçu](assets/do-not-localize/preview_icon.png) pour générer un aperçu du panneau Filtres tel qu’il apparaît une fois le prédicat ajouté.
1. Examinez la structure du prédicat en mode Aperçu.

   ![Aperçu du formulaire de recherche avant de soumettre les modifications](assets/preview-1.png)

   Aperçu du formulaire de recherche avant de soumettre les modifications

1. Pour fermer l’aperçu, cliquez sur **[!UICONTROL Fermer]** ![fermer](assets/do-not-localize/close.png) dans le coin supérieur droit de l’aperçu.
1. Pour enregistrer les paramètres, cliquez sur **[!UICONTROL Terminé]**.
1. Accédez au panneau Rechercher de l&#39;interface utilisateur [!DNL Assets]. Le prédicat Propriété est ajouté au panneau.
1. Entrez une description du fichier à rechercher dans la zone de texte. Par exemple, saisissez `Adobe`. Lorsque vous effectuez une recherche, les ressources dont la description correspond à `Adobe` sont répertoriées dans les résultats de la recherche.

## Ajout d’un prédicat Options {#adding-an-options-predicate}

Le prédicat Options permet d’ajouter des options de recherche multiples dans le panneau Filtres. Vous pouvez choisir une ou plusieurs options dans le panneau Filtres pour rechercher des ressources. Par exemple, pour rechercher des actifs en fonction du type de fichier, configurez des options telles que Images, Multimédia, Documents et Archives dans le formulaire de recherche. Une fois ces options configurées, la recherche est effectuée sur les ressources de type GIF, JPEG, PNG, etc. lorsque vous sélectionnez l’option Images dans le panneau Filtres.

Pour mapper les options à la propriété correspondante, créez une structure de nœud pour les options et fournissez le chemin du nœud parent dans la propriété Nom de la propriété du prédicat Options. Le nœud parent doit être du type `sling` : `OrderedFolder`. Les options doivent être du type `nt:unstructured`. Les propriétés `jcr:title` et `value` doivent être configurées pour les nœuds d’option.

La propriété `jcr:title` est un nom convivial de l’option qui apparaît dans le panneau Filtres. Le champ `value` est utilisé dans la demande pour correspondre à la propriété spécifiée.

Lorsque vous sélectionnez une option, la recherche est effectuée en fonction de la propriété `value` du nœud d’option et de ses nœuds enfants, le cas échéant. L’arborescence entière sous le nœud d’option est parcourue et la propriété `value` de chaque nœud enfant est combinée à l’aide d’une opération OU pour former la requête.

Par exemple, si vous sélectionnez Images comme type de fichier, la requête de ressources est créée en combinant la propriété `value` à l’aide d’une opération OU. Par exemple, la requête relative à des images est créée en combinant les résultats correspondants pour *image/jpeg*, *image/gif*, *image/png*, *image/pjpeg* et *image/tiff* pour la propriété `jcr:content/metadata/dc:format` à l’aide d’une opération OU.

![La propriété de valeur d’un type de fichier, telle que vue dans CRXDE, est utilisée pour que les requêtes fonctionnent.](assets/filetype-value-property.png)

La propriété de valeur d’un type de fichier, telle que vue dans CRXDE, est utilisée pour que les requêtes fonctionnent.

Au lieu de créer manuellement une structure de noeud pour les options du référentiel CRXDE, vous pouvez définir les options dans un fichier JSON en spécifiant les paires clé-valeur correspondantes. Spécifiez le chemin du fichier JSON dans le champ **[!UICONTROL Nom de la propriété]**. Par exemple, vous pouvez définir les paires clé-valeur `image/bmp`, `image/gif`, `image/jpeg` et `image/png`, puis spécifier leurs valeurs comme illustré dans l’échantillon de fichier JSON ci-dessous. Dans le champ **[!UICONTROL Nom de propriété]**, vous pouvez spécifier le chemin CRXDE pour ce fichier.

```json
{
    "options" :
 [
          {"value" : "image/bmp","text" : "BMP"},
          {"value" : "image/gif","text" : "GIF"},
          {"value" : "image/jpeg","text" : "JPEG"},
          {"value" : "image/png","text" : "PNG"}
 ]
}
```

Si vous souhaitez utiliser un nœud existant, indiquez-le à l’aide de la boîte de dialogue de sélection.

>[!NOTE]
>
>Le prédicat Options est un wrapper personnalisé qui comprend des prédicats de propriété pour démontrer le comportement décrit. Pour l’heure, aucun point de terminaison REST n’est disponible pour la prise en charge native de cette fonctionnalité.

1. Cliquez sur le logo [!DNL Experience Manager], puis accédez à **[!UICONTROL Outils]** > **[!UICONTROL Général]** > **[!UICONTROL Rechercher Forms]**.
1. Dans la page **[!UICONTROL Rechercher Forms]**, sélectionnez **[!UICONTROL Actifs Admin Search Rail]**, puis cliquez sur **[!UICONTROL Modifier]**.
1. Sur la page **[!UICONTROL Modifier le formulaire de recherche]**, faites glisser **[!UICONTROL Options du prédicat]** de l’onglet **[!UICONTROL Sélectionner le prédicat]** jusqu’au volet principal.
1. Dans l’onglet **[!UICONTROL Paramètres]**, saisissez un libellé et un nom pour la propriété. Par exemple, pour rechercher des ressources en fonction de leur format, indiquez un nom convivial pour le libellé ; **[!UICONTROL Type de fichier]**, par exemple. Indiquez la propriété sur laquelle sera axée la recherche dans le champ de propriété ; `jcr:content/metadata/dc:format.`, par exemple.
1. Utilisez l’une des méthodes suivantes :

   * Dans le champ **[!UICONTROL Nom de la propriété]**, indiquez le chemin du fichier JSON où sont définis les nœuds des options et spécifiez les paires clé-valeur correspondantes.
   * Cliquez sur le symbole `+` en regard du champ Options pour spécifier le texte d’affichage et la valeur des options à fournir dans le panneau Filtres. Pour ajouter une autre option, cliquez sur le symbole `+` et répétez l’étape.

1. Assurez-vous que l’option **[!UICONTROL Sélection simple]** est désactivée pour permettre à l’utilisateur de sélectionner plusieurs options à la fois pour les types de fichiers (Images, Documents, Multimédia et Archives, par exemple). Si vous choisissez **[!UICONTROL Sélection simple]**, l’utilisateur ne peut sélectionner qu’une seule option à la fois pour les types de fichiers.

   ![Champs disponibles dans le prédicat Options](assets/options_predicate.png)

   Champs disponibles dans le prédicat Options

1. Dans le champ **[!UICONTROL Description]**, saisissez une description facultative, puis cliquez sur **[!UICONTROL Terminé]**.
1. Accédez au panneau Rechercher. Le prédicat Options est ajouté au panneau **Rechercher**. Les options proposées pour **[!UICONTROL Type de fichier]** sont présentées sous la forme de cases à cocher.

## Ajouter un prédicat de propriété à plusieurs valeurs {#adding-a-multi-value-property-predicate}

Le prédicat de propriété à plusieurs valeurs vous permet de rechercher plusieurs valeurs dans des ressources. Supposons que vous ayez des images de plusieurs produits dans [!DNL Assets] et que les métadonnées de chaque image incluent un numéro SKU associé au produit. Vous pouvez utiliser ce prédicat pour rechercher des images de produit sur la base de plusieurs numéros de SKU.

1. Cliquez sur le logo [!DNL Experience Manager], puis accédez à **[!UICONTROL Outils]** > **[!UICONTROL Général]** > **[!UICONTROL Rechercher Forms]**.
1. Sur la page Rechercher dans Forms, sélectionnez **[!UICONTROL Actifs Admin Search Rail]**, puis cliquez sur **[!UICONTROL Modifier]** ![icône Modifier](assets/do-not-localize/aemassets_edit.png).
1. Sur la page Modifier le formulaire de recherche, faites glisser **[!UICONTROL Prédicat de propriété à plusieurs valeurs]** de l’onglet **[!UICONTROL Sélectionner le prédicat]** jusqu’au volet principal.
1. Dans l’onglet **[!UICONTROL Paramètres]**, saisissez un libellé et un texte d’espace réservé pour le prédicat. Indiquez le nom de la propriété sur laquelle sera axée la recherche dans le champ de propriété ; `jcr:content/metadata/dc:value`, par exemple. Vous pouvez également utiliser la boîte de dialogue de sélection pour sélectionner un nœud.
1. Assurez-vous que l’option **[!UICONTROL Prise en charge des délimiteurs]** est sélectionnée. Dans le champ **[!UICONTROL Délimiteurs d’entrée]**, spécifiez des délimiteurs pour séparer les valeurs individuelles. Par défaut, la virgule est spécifiée comme séparateur. Vous pouvez spécifier un autre délimiteur.
1. Dans le champ **Description**, saisissez une description facultative, puis cliquez sur **[!UICONTROL Terminé]**.
1. Accédez au panneau Filtres de l&#39;interface utilisateur [!DNL Assets]. Le prédicat **[!UICONTROL Propriété à plusieurs valeurs]** est ajouté au panneau.
1. Indiquez plusieurs valeurs dans le champ Valeur multiple, en les séparant par des délimiteurs, puis effectuez la recherche. Le prédicat récupère une correspondance de texte exacte pour les valeurs que vous avez spécifiées.

## Ajout d’un prédicat de balises {#adding-a-tags-predicate}

Le prédicat Balise vous permet d’effectuer des recherches de ressources basées sur des balises. Par défaut, [!DNL Assets] recherche des ressources pour qu’une ou plusieurs balises correspondent en fonction des balises que vous spécifiez. En d’autres termes, la requête de recherche effectue une opération OR à l’aide des balises indiquées. Cependant, vous pouvez utiliser l’option de correspondance de toutes les balises pour rechercher les ressources qui contiennent toutes les balises que vous spécifiez.

1. Cliquez sur le logo [!DNL Experience Manager], puis accédez à **[!UICONTROL Outils]** > **[!UICONTROL Général]** > **[!UICONTROL Rechercher Forms]**.
1. Dans la page Rechercher dans Forms, sélectionnez **[!UICONTROL Actifs Admin Search Rail]**, puis cliquez sur **[!UICONTROL Modifier]** ![icône Modifier](assets/do-not-localize/aemassets_edit.png).
1. Sur la page Modifier le formulaire de recherche, faites glisser **[!UICONTROL Prédicat de balises]** de l’onglet Sélectionner le prédicat jusqu’au volet principal.
1. Dans l’onglet Paramètres, saisissez un texte d’espace réservé pour le prédicat. Indiquez le nom de la propriété sur laquelle sera axée la recherche dans le champ de propriété ; *jcr:content/metadata/cq:tags*, par exemple. Vous pouvez également sélectionner un nœud dans CRXDE à partir de la boîte de dialogue de sélection.
1. Configurez la propriété Chemin d’accès aux balises racines de ce prédicat pour renseigner les différentes balises dans la liste Balises.
1. Sélectionnez **[!UICONTROL Option d’affichage de correspondance de toutes les balises]** pour rechercher les ressources qui contiennent toutes les balises que vous spécifiez.

1. Dans le champ **[!UICONTROL Description]**, saisissez une description facultative, puis cliquez sur **[!UICONTROL Terminé]**.
1. Accédez au panneau Rechercher. Le prédicat **[!UICONTROL Balises]** est ajouté au panneau Rechercher.
1. Indiquez les balises sur la base desquelles vous souhaitez rechercher des ressources ou faites votre sélection dans la liste des suggestions.

1. Sélectionnez **[!UICONTROL Correspondre à tous les critères]** pour rechercher les ressources qui contiennent toutes les balises que vous spécifiez.

## Ajouter d&#39;autres prédicats {#adding-other-predicates}

Tout comme vous ajoutez un prédicat Propriété ou un prédicat Options, vous pouvez ajouter les autres prédicats suivants au panneau Rechercher :

| Nom du prédicat | Description | Propriétés |
|---|---|---|
| [!UICONTROL Texte intégral] | Prédicat de recherche permettant d’effectuer une recherche de texte intégral dans un nœud de ressource entier. Il est mappé à l’opérateur jcr:contains. Vous pouvez indiquer un chemin d’accès relatif si vous souhaitez effectuer une recherche de texte intégral sur une partie spécifique du nœud de ressource. | <ul><li>Libellé</li><li>Espace réservé</li><li>Nom de la propriété</li><li>Description</li></ul> |
| [!UICONTROL Explorateur de chemins d’accès] | Prédicat de recherche pour rechercher des fichiers dans des dossiers et des sous-dossiers à un chemin racine préconfiguré | <ul><li>Espace réservé</li><li>Chemin racine</li><li>Description</li></ul> |
| [!UICONTROL Chemin] | Utilisez-le pour filtrer les résultats selon l’emplacement. Vous pouvez spécifier différents chemins d’accès sous la forme d’options. | <ul><li>Libellé</li><li>Chemin</li><li>Description</li></ul> |
| [!UICONTROL État de publication] | Prédicat de recherche permettant de rechercher des ressources en fonction de leur état de publication. | <ul><li>Libellé</li><li>Nom de la propriété</li><li>Description</li></ul> |
| [!UICONTROL Date relative] | Prédicat de recherche permettant de rechercher des ressources en fonction de leur date de création. Vous pouvez, par exemple, configurer des options telles que « il y a 2 mois », « il y a 3 semaines », etc. | <ul><li>Libellé</li><li>Nom de la propriété</li><li>Date relative</li></ul> |
| [!UICONTROL Étendue] | Prédicat de recherche permettant de rechercher des ressources comprises dans une étendue spécifiée. Dans le panneau Rechercher, vous pouvez spécifier des valeurs maximale et minimale pour l’étendue. | <ul><li>Libellé</li><li>Nom de la propriété</li><li>Description</li></ul> |
| [!UICONTROL Période] | Prédicat de recherche permettant de rechercher des ressources créées pendant une période spécifiée pour une propriété de date. Vous pouvez spécifier des dates de début et de fin dans le panneau Rechercher à l’aide des sélecteurs de date. | <ul><li>Libellé</li><li>Espace réservé</li><li>Nom de la propriété</li><li>Texte de la plage (De)</li><li>Texte de la plage (À)</li><li>Description</li></ul> |
| [!UICONTROL Date] | Prédicat de recherche permettant de rechercher à l’aide d’un curseur des ressources selon une propriété de date. | <ul><li>Libellé</li><li>Nom de la propriété</li><li>Description</li></ul> |
| [!UICONTROL Taille de fichier] | Prédicat de recherche permettant de rechercher des ressources en fonction de leur taille. Il s’agit d’un prédicat basé sur un curseur, dans lequel vous sélectionnez les options de curseur à partir d’un nœud configurable. Les options par défaut sont définies dans /libs/dam/options/prédicates/filesize dans le référentiel CRXDE. La taille du fichier est exprimée en octets. | <ul><li>Libellé</li><li>Nom de la propriété</li><li>Chemin</li><li>Description</li></ul> |
| [!UICONTROL Dernière modification de la ressource] | Prédicat de recherche permettant de rechercher des ressources récemment modifiées. | <ul><li>Nom de la propriété</li><li>Valeur de la propriété</li><li>Description</li></ul> |
| [!UICONTROL État de publication] | Prédicat de recherche permettant de rechercher des ressources en fonction de leur état de publication. | <ul><li>Libellé</li><li>Nom de la propriété</li><li>Description</li></ul> |
| [!UICONTROL Évaluation] | Prédicat de recherche permettant de rechercher des ressources en fonction de leur évaluation moyenne. | <ul><li>Libellé</li><li>Nom de la propriété</li><li>Chemin d’accès aux options</li><li>Description</li></ul> |
| [!UICONTROL État d’expiration] | Prédicat de recherche permettant de rechercher des ressources en fonction de leur état d’expiration. | <ul><li>Libellé</li><li>Nom de la propriété</li><li>Description</li></ul> |
| [!UICONTROL Masqué] | Prédicat de recherche permettant de définir une propriété de champ masqué pour rechercher des ressources. | <ul><li>Nom de la propriété</li><li>Valeur de la propriété</li><li>Description</li></ul> |

## Restauration des facettes de recherche par défaut {#restoring-default-search-facets}

Par défaut, une icône de verrouillage ![icône de verrouillage fermée](assets/do-not-localize/lock_closed_icon.svg) apparaît avant **[!UICONTROL le rail de recherche des administrateurs des ressources]** dans la page **[!UICONTROL Rechercher Forms]**. L’icône de cadenas en regard d’une option de la page Formulaires de recherche indique que les paramètres par défaut sont intacts et non personnalisés. L’icône ![verrouiller l’icône ](assets/do-not-localize/lock_closed_icon.svg) disparaît si vous ajoutez des facettes de recherche au formulaire indiquant que le formulaire par défaut a été modifié.

![L’icône de cadenas en regard d’une option de la page Formulaires de recherche indique que les paramètres par défaut sont intacts et non personnalisés.](assets/locked_admin_rail.png)

Pour restaurer la facette de recherche par défaut, procédez comme suit :

1. Sélectionnez **[!UICONTROL Rail de recherche d’administrateurs de ressources]** sur la page **[!UICONTROL Formulaires de recherche]**.
1. Cliquez sur **[!UICONTROL Supprimer]** ![deleteoutline](assets/do-not-localize/deleteoutline.png) dans la barre d&#39;outils.
1. Dans la boîte de dialogue de confirmation, cliquez sur **[!UICONTROL Supprimer]** pour supprimer les modifications personnalisées.

   Après avoir supprimé les modifications personnalisées des facettes de recherche, l&#39;icône de verrouillage ![verrouiller l&#39;icône ](assets/do-not-localize/lock_closed_icon.svg) réapparaît avant **[!UICONTROL le rail de recherche des administrateurs des ressources]** dans la page **[!UICONTROL Rechercher Forms]**.

## Autorisations d’utilisateur {#user-permissions}

Si le rôle d’administrateur ne vous a pas été attribué, voici la liste des autorisations dont vous avez besoin pour réaliser des actions de modification, de suppression et d’affichage d’aperçu impliquant des facettes de recherche.

| Action | Autorisations |
| ------------------- | ---------------------------------------------------------------- |
| [!UICONTROL Modifier] | Autorisations de lecture et d’écriture sur le noeud `/apps` dans CRXDE |
| [!UICONTROL Supprimer] | Autorisations de lecture, d’écriture et de suppression sur le noeud `/apps` dans CRXDE |
| [!UICONTROL Aperçu] | Autorisations de lecture, d’écriture et de suppression sur le noeud `/var/dam/content` dans CRXDE. De même que les autorisations de lecture et d’écriture sur le nœud `/apps` |

>[!MORELIKETHIS]
>
>* [Extension de la fonctionnalité de recherche de ressources](searchx.md)
>* [Recherche de ressources](search-assets.md)

