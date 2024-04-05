---
title: Facettes de recherche pour filtrer les résultats de recherche
description: Découvrez comment créer, modifier et utiliser les facettes de recherche dans  [!DNL Adobe Experience Manager].
contentOwner: AG
role: Admin, Developer
feature: Search
exl-id: acaf46e6-ff70-4825-8922-ce8f82905a92
hide: true
solution: Experience Manager, Experience Manager Assets
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '2411'
ht-degree: 100%

---

# Facettes de recherche {#search-facets}

| Version | Lien de l’article |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Cliquez ici](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/admin/search-facets.html?lang=fr) |
| AEM 6.5 | Cet article |

Le déploiement de [!DNL Adobe Experience Manager Assets] à l’échelle de l’entreprise offre la capacité de stocker de nombreuses ressources. Dans certains cas, la recherche de la bonne ressource peut être difficile et longue si vous utilisez uniquement les fonctionnalités de recherche génériques d’[!DNL Experience Manager].

Utilisez les facettes de recherche du panneau Filtres pour ajouter plus de granularité à votre expérience de recherche et rendre la fonctionnalité de recherche plus efficace et plus polyvalente. Ces facettes de recherche utilisent plusieurs dimensions (prédicats) qui vous permettent d’effectuer des recherches plus complexes. Le panneau Filtres inclut quelques facettes standard. Vous pouvez également ajouter des facettes de recherche personnalisées.

En résumé, les facettes de recherche permettent de rechercher des ressources de plusieurs façons plutôt que selon un seul ordre taxonomique prédéterminé. Vous pouvez facilement descendre dans la hiérarchie jusqu’au niveau de détail souhaité pour effectuer une recherche plus précise.

Par exemple, si vous recherchez une image, vous pouvez choisir si vous souhaitez une bitmap ou une image vectorielle. Vous pouvez réduire davantage la portée de la recherche en spécifiant le type MIME de l’image. De même, lors de la recherche de documents, vous pouvez spécifier le format, par exemple PDF ou MS Word.

## Ajout d’un prédicat {#adding-a-predicate}

Les facettes de recherche qui apparaissent dans le panneau Filtres sont définies dans le formulaire de recherche sous-jacent à l’aide de prédicats. Pour afficher d’autres facettes, ajoutez des prédicats au formulaire par défaut ou utilisez un formulaire personnalisé qui comprend les facettes de votre choix.

Pour des recherches de texte intégral, ajoutez le prédicat **[!UICONTROL Texte intégral]** au formulaire. Utilisez le prédicat Propriété pour rechercher des ressources qui correspondent à une seule propriété que vous spécifiez. Ajoutez le prédicat Options pour rechercher des ressources correspondant à une ou plusieurs valeurs pour une propriété spécifique. Ajoutez le prédicat Période pour rechercher des ressources créées au cours d’une période donnée.

1. Cliquez sur le logo d’[!DNL Experience Manager], puis accédez à **[!UICONTROL Outils]** > **[!UICONTROL Général]** > **[!UICONTROL Formulaires de recherche]**.
1. Sur la page [!UICONTROL Formulaires de recherche], sélectionnez **[!UICONTROL Rail de recherche d’administration de ressources]**, puis cliquez sur **[!UICONTROL Modifier]** ![icône modifier](assets/do-not-localize/aemassets_edit.png).

   >[!NOTE]
   >
   >Pour utiliser la fonctionnalité de recherche de dossiers du rail de recherche d’administration préconfiguré d’[!DNL Assets] d’une version antérieure, procédez comme suit :
   >
   >1. Accédez à `/conf/global/settings/dam/search/facets/assets/jcr:content/items` dans CRXDE.
   >1. Supprimez le nœud `type`.
   >1. À partir du chemin `/libs/settings/dam/search/facets/assets/jcr:content/items`, copiez les nœuds `asset`, `directory`, `typeor`, `excludepaths` et `searchtype` dans le chemin mentionné à l’étape 1.
   >1. Enregistrez les modifications.

1. Sur la page [!UICONTROL Modifier des formulaires de recherche], faites glisser un prédicat de l’onglet **[!UICONTROL Sélectionner le prédicat]** vers le volet principal. Faites glisser, par exemple, **[!UICONTROL Prédicat de la propriété]**.

   ![Sélectionnez et déplacez un prédicat pour personnaliser les filtres de recherche](assets/drag_predicate.png)

   *Figure : Sélectionner et déplacer un prédicat pour personnaliser les filtres de recherche.*

1. Sous l’onglet [!UICONTROL Paramètres], saisissez un libellé de champ, un texte d’espace réservé et une description pour le prédicat. Indiquez un nom valide pour la propriété de métadonnées que vous souhaitez associer au prédicat. Le libellé d’en-tête de l’onglet [!UICONTROL Paramètres] identifie le type de prédicat sélectionné.

1. Dans le champ [!UICONTROL Nom de la propriété], indiquez un nom valide pour la propriété de métadonnées que vous souhaitez associer au prédicat. Il s’agit du nom sur lequel la recherche se base. Par exemple, saisissez `jcr:content/metadata/dc:description` ou `./jcr:content/metadata/dc:description`.

   Vous pouvez également sélectionner un nœud existant dans la boîte de dialogue de sélection.

   ![Associez une propriété de métadonnées à un prédicat dans le champ Nom de propriété](assets/property_settings.png)

   Associez une propriété de métadonnées à un prédicat dans le champ Nom de propriété

1. Cliquez sur **[!UICONTROL Aperçu]** ![aperçu](assets/do-not-localize/preview_icon.png) pour générer un aperçu du panneau Filtres tel qu’il apparaît une fois le prédicat ajouté.
1. Examinez la structure du prédicat en mode Aperçu.

   ![Aperçu du formulaire de recherche avant de soumettre les modifications](assets/preview-1.png)

   Aperçu du formulaire de recherche avant de soumettre les modifications

1. Pour fermer l’aperçu, cliquez sur **[!UICONTROL Fermer]** ![fermer](assets/do-not-localize/close.png) dans le coin supérieur droit de l’aperçu.
1. Pour enregistrer les paramètres, cliquez sur **[!UICONTROL Terminé]**.
1. Accédez au panneau Rechercher dans l’interface utilisateur d’[!DNL Assets]. Le prédicat Propriété est ajouté au panneau.
1. Dans la zone de texte, saisissez une description de la ressource à rechercher. Par exemple, saisissez `Adobe`. Lorsque vous effectuez une recherche, les ressources dont la description correspond à « `Adobe` » sont répertoriés dans les résultats de la recherche.

## Ajout d’un prédicat Options {#adding-an-options-predicate}

Le prédicat Options vous permet d’ajouter plusieurs options de recherche dans le panneau Filtres. Vous pouvez choisir une ou plusieurs options dans le panneau Filtres pour rechercher des ressources. Par exemple, pour rechercher des ressources en fonction du type de fichier, configurez des options telles que Images, Multimédia, Documents et Archives dans le formulaire de recherche. Une fois ces options configurées, la recherche est effectuée sur les ressources de type GIF, JPEG, PNG, etc. lorsque vous sélectionnez l’option Images dans le panneau Filtres.

Pour mapper les options à la propriété correspondante, créez une structure de nœud pour les options et fournissez le chemin du nœud parent dans la propriété Nom de la propriété du prédicat Options. Le nœud parent doit être du type `sling` : `OrderedFolder`. Les options doivent être du type `nt:unstructured`. Les propriétés `jcr:title` et `value` doivent être configurées pour les nœuds d’option.

La propriété `jcr:title` est un nom convivial de l’option qui apparaît dans le panneau Filtres. Le champ `value` est utilisé dans la demande pour correspondre à la propriété spécifiée.

Lorsque vous sélectionnez une option, la recherche est effectuée en fonction de la propriété `value` du nœud d’option et de ses nœuds enfants, le cas échéant. L’arborescence entière sous le nœud d’option est parcourue et la propriété `value` de chaque nœud enfant est combinée à l’aide d’une opération OR pour former la requête.

Par exemple, si vous sélectionnez Images comme type de fichier, la requête de ressources est créée en combinant la propriété `value` à l’aide d’une opération OR. Par exemple, la requête relative à des images est créée en combinant les résultats correspondants pour *image/jpeg*, *image/gif*, *image/png*, *image/pjpeg* et *image/tiff* pour la propriété `jcr:content/metadata/dc:format` à l’aide d’une opération OR.

![La propriété de valeur d’un type de fichier, telle qu’affichée dans CRXDE, est utilisée pour que les requêtes fonctionnent.](assets/filetype-value-property.png)

La propriété de valeur d’un type de fichier, telle qu’affichée dans CRXDE, est utilisée pour que les requêtes fonctionnent.

Au lieu de créer manuellement une structure de nœud pour les options du référentiel CRX, vous pouvez définir les options d’un fichier JSON en spécifiant les paires clé-valeur correspondantes. Spécifiez le chemin du fichier JSON dans le champ **[!UICONTROL Nom de la propriété]**. Par exemple, vous pouvez définir les paires clé-valeur `image/bmp`, `image/gif`, `image/jpeg` et `image/png`, puis spécifier leurs valeurs comme illustré dans l’échantillon de fichier JSON ci-dessous. Dans le champ **[!UICONTROL Nom de la propriété]**, vous pouvez spécifier le chemin d’accès CRXDE de ce fichier.

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
>Le prédicat Options est un wrapper personnalisé qui comprend des prédicats de propriété pour démontrer le comportement décrit. Pour l’heure, aucun point d’entrée REST n’est disponible pour la prise en charge native de cette fonctionnalité.

1. Cliquez sur le logo d’[!DNL Experience Manager], puis accédez à **[!UICONTROL Outils]** > **[!UICONTROL Général]** > **[!UICONTROL Formulaires de recherche]**.
1. Sur la page **[!UICONTROL Formulaires de recherche]**, sélectionnez **[!UICONTROL Rail de recherche d’administration de ressources]**, puis cliquez sur **[!UICONTROL Modifier]**.
1. Sur la page **[!UICONTROL Modifier le formulaire de recherche]**, faites glisser **[!UICONTROL Options du prédicat]** de l’onglet **[!UICONTROL Sélectionner le prédicat]** jusqu’au volet principal.
1. Dans l’onglet **[!UICONTROL Paramètres]**, saisissez un libellé et un nom pour la propriété. Par exemple, pour rechercher des ressources en fonction de leur format, indiquez un nom convivial pour le libellé ; **[!UICONTROL Type de fichier]**, par exemple. Spécifiez la propriété en fonction de laquelle la recherche doit être effectuée dans le champ de propriété, par exemple, `jcr:content/metadata/dc:format.`.
1. Utilisez l’une des méthodes suivantes :

   * Dans le champ **[!UICONTROL Nom de la propriété]**, indiquez le chemin du fichier JSON où sont définis les nœuds des options et spécifiez les paires clé-valeur correspondantes.
   * Appuyez sur l’icône `+` à côté du champ Options afin de spécifier le texte affiché et la valeur pour les options que vous souhaitez fournir dans le panneau Filtres. Pour ajouter une autre option, cliquez sur le symbole `+` et répétez l’étape.

1. Assurez-vous que l’option **[!UICONTROL Sélection simple]** est désactivée pour permettre à l’utilisateur de sélectionner plusieurs options à la fois pour les types de fichiers (Images, Documents, Multimédia et Archives, par exemple). Si vous choisissez **[!UICONTROL Sélection simple]**, l’utilisateur ne peut sélectionner qu’une seule option à la fois pour les types de fichiers.

   ![Champs disponibles dans le prédicat Options](assets/options_predicate.png)

   Champs disponibles dans le prédicat Options

1. Dans le champ **[!UICONTROL Description]**, saisissez une description facultative, puis cliquez sur **[!UICONTROL Terminé]**.
1. Accédez au panneau Rechercher. Le prédicat Options est ajouté au panneau **Rechercher**. Les options proposées pour **[!UICONTROL Type de fichier]** sont présentées sous la forme de cases à cocher.

## Ajout d’un prédicat de propriété à plusieurs valeurs {#adding-a-multi-value-property-predicate}

Le prédicat de propriété à plusieurs valeurs vous permet de rechercher plusieurs valeurs dans des ressources. Supposons que vous disposiez des images de plusieurs produits dans [!DNL Assets] et que les métadonnées de chaque image comprennent un numéro de SKU qui est associé au produit. Vous pouvez utiliser ce prédicat pour rechercher des images de produit sur la base de plusieurs numéros de SKU.

1. Cliquez sur le logo d’[!DNL Experience Manager], puis accédez à **[!UICONTROL Outils]** > **[!UICONTROL Général]** > **[!UICONTROL Formulaires de recherche]**.
1. Dans la page Formulaires de recherche, sélectionnez **[!UICONTROL Rail de recherche d’administration de ressources]**, puis cliquez sur **[!UICONTROL Modifier]** ![icône modifier](assets/do-not-localize/aemassets_edit.png).
1. Sur la page Modifier le formulaire de recherche, faites glisser **[!UICONTROL Prédicat de propriété à plusieurs valeurs]** de l’onglet **[!UICONTROL Sélectionner le prédicat]** jusqu’au volet principal.
1. Dans l’onglet **[!UICONTROL Paramètres]**, saisissez un libellé et un texte d’espace réservé pour le prédicat. Indiquez le nom de la propriété sur laquelle sera axée la recherche dans le champ de propriété ; `jcr:content/metadata/dc:value`, par exemple. Vous pouvez également utiliser la boîte de dialogue de sélection pour sélectionner un nœud.
1. Assurez-vous que l’option **[!UICONTROL Prise en charge des délimiteurs]** est sélectionnée. Dans le champ **[!UICONTROL Délimiteurs d’entrée]**, spécifiez des délimiteurs pour séparer les valeurs individuelles. Par défaut, la virgule est spécifiée comme séparateur. Vous pouvez spécifier un autre délimiteur.
1. Dans le champ **Description**, saisissez une description facultative, puis cliquez sur **[!UICONTROL Terminé]**.
1. Accédez au panneau Filtres dans l’interface utilisateur d’[!DNL Assets]. Le prédicat **[!UICONTROL Propriété à plusieurs valeurs]** est ajouté au panneau.
1. Spécifiez plusieurs valeurs dans le champ à plusieurs valeurs séparées par des délimiteurs et effectuez la recherche. Le prédicat récupère une correspondance de texte exacte pour les valeurs que vous spécifiez.

## Ajout d’un prédicat de balises {#adding-a-tags-predicate}

Le prédicat de balise vous permet de rechercher des ressources sur la base des balises. Par défaut, [!DNL Assets] recherche une ou plusieurs correspondances de balise dans les ressources en fonction des balises que vous avez spécifiées. En d’autres termes, la requête de recherche effectue une opération OU à l’aide des balises spécifiées. Cependant, vous pouvez utiliser l’option Correspondre à toutes les balises pour rechercher des ressources qui incluent toutes les balises que vous spécifiez.

1. Cliquez sur le logo d’[!DNL Experience Manager], puis accédez à **[!UICONTROL Outils]** > **[!UICONTROL Général]** > **[!UICONTROL Formulaires de recherche]**.
1. Sur la page Formulaires de recherche, sélectionnez **[!UICONTROL Rail de recherche d’administrateurs de ressources]**, puis appuyez sur **[!UICONTROL Modifier]** ![icône modifier](assets/do-not-localize/aemassets_edit.png).
1. Sur la page Modifier le formulaire de recherche, faites glisser **[!UICONTROL Prédicat de balises]** de l’onglet Sélectionner le prédicat jusqu’au volet principal.
1. Dans l’onglet Paramètres, saisissez un texte d’espace réservé pour le prédicat. Indiquez le nom de la propriété sur laquelle sera axée la recherche dans le champ de propriété ; *jcr:content/metadata/cq:tags*, par exemple. Vous pouvez également sélectionner un nœud dans CRXDE à partir de la boîte de dialogue de sélection.
1. Configurez la propriété Chemin d’accès racine aux balises de ce prédicat pour renseigner différentes balises dans la liste Balises.
1. Sélectionnez **[!UICONTROL Option d’affichage de correspondance de toutes les balises]** pour rechercher les ressources qui contiennent toutes les balises que vous spécifiez.

1. Dans le champ **[!UICONTROL Description]**, saisissez une description facultative, puis cliquez sur **[!UICONTROL Terminé]**.
1. Accédez au panneau Rechercher. Le prédicat **[!UICONTROL Balises]** est ajouté au panneau Rechercher.
1. Spécifiez des balises en fonction desquelles vous souhaitez rechercher des ressources ou faites votre choix dans la liste de suggestions.

1. Sélectionnez **[!UICONTROL Correspondre à toutes]** pour rechercher les correspondances qui incluent toutes les balises que vous spécifiez.

## Ajout d’autres prédicats {#adding-other-predicates}

Tout comme vous ajoutez un prédicat Propriété ou un prédicat Options, vous pouvez ajouter les autres prédicats suivants au panneau Rechercher :

| Nom du prédicat | Description | Propriétés |
|---|---|---|
| [!UICONTROL Texte intégral] | Prédicat de recherche permettant d’effectuer une recherche de texte intégral dans un nœud de ressource entier. Il est mappé à l’opérateur jcr:contains. Vous pouvez spécifier un chemin d’accès relatif si vous souhaitez effectuer une recherche de texte intégral sur une partie spécifique du nœud de ressource. | <ul><li>Libellé</li><li>Espace réservé</li><li>Nom de la propriété</li><li>Description</li></ul> |
| [!UICONTROL Explorateur de chemins d’accès] | Prédicat de recherche permettant de rechercher des ressources dans des dossiers et des sous-dossiers à un chemin d’accès racine préconfiguré. | <ul><li>Espace réservé</li><li>Chemin d’accès racine</li><li>Description</li></ul> |
| [!UICONTROL Chemin] | Utilisez-le pour filtrer les résultats selon l’emplacement. Vous pouvez spécifier plusieurs chemins d’accès en tant qu’options. | <ul><li>Libellé</li><li>Chemin</li><li>Description</li></ul> |
| [!UICONTROL Statut de publication] | Prédicat de recherche permettant de rechercher des ressources en fonction de leur statut de publication. | <ul><li>Libellé</li><li>Nom de la propriété</li><li>Description</li></ul> |
| [!UICONTROL Date relative] | Prédicat de recherche permettant de rechercher des ressources en fonction de leur date de création. Vous pouvez, par exemple, configurer des options telles qu’il y a 2 mois, il y a 3 semaines, etc. | <ul><li>Libellé</li><li>Nom de la propriété</li><li>Date relative</li></ul> |
| [!UICONTROL Étendue] | Prédicat de recherche permettant de rechercher des ressources comprises dans une étendue spécifiée. Dans le panneau Rechercher, vous pouvez spécifier des valeurs maximale et minimale pour l’étendue. | <ul><li>Libellé</li><li>Nom de la propriété</li><li>Description</li></ul> |
| [!UICONTROL Période] | Prédicat de recherche permettant de rechercher des ressources créées pendant une période spécifiée pour une propriété de date. Dans le panneau de recherche, vous pouvez spécifier des dates de début et de fin à l’aide du sélecteur de dates. | <ul><li>Libellé</li><li>Espace réservé</li><li>Nom de la propriété</li><li>Texte de la plage (De)</li><li>Texte de la plage (À)</li><li>Description</li></ul> |
| [!UICONTROL Date] | Prédicat de recherche permettant de rechercher à l’aide d’un curseur des ressources selon une propriété de date. | <ul><li>Libellé</li><li>Nom de la propriété</li><li>Description</li></ul> |
| [!UICONTROL Taille de fichier] | Prédicat de recherche permettant de rechercher des ressources en fonction de leur taille. Il s’agit d’un prédicat basé sur un curseur, dans lequel vous sélectionnez les options de curseur à partir d’un nœud configurable. Les options par défaut sont définies sous /libs/dam/options/predicates/filesize dans le référentiel CRXDE. La taille du fichier est exprimée en octets. | <ul><li>Libellé</li><li>Nom de la propriété</li><li>Chemin</li><li>Description</li></ul> |
| [!UICONTROL Dernière modification de la ressource] | Prédicat de recherche permettant de rechercher des ressources récemment modifiées. | <ul><li>Nom de la propriété</li><li>Valeur de propriété</li><li>Description</li></ul> |
| [!UICONTROL Statut de publication] | Prédicat de recherche permettant de rechercher des ressources en fonction de leur statut de publication. | <ul><li>Libellé</li><li>Nom de la propriété</li><li>Description</li></ul> |
| [!UICONTROL Évaluation] | Prédicat de recherche permettant de rechercher des ressources en fonction de leur évaluation moyenne. | <ul><li>Libellé</li><li>Nom de la propriété</li><li>Chemin d’accès aux options</li><li>Description</li></ul> |
| [!UICONTROL État d’expiration] | Prédicat de recherche permettant de rechercher des ressources en fonction de leur état d’expiration. | <ul><li>Libellé</li><li>Nom de la propriété</li><li>Description</li></ul> |
| [!UICONTROL Masqué] | Prédicat de recherche qui définit une propriété de champ masqué pour rechercher des ressources. | <ul><li>Nom de la propriété</li><li>Valeur de propriété</li><li>Description</li></ul> |

## Restauration des facettes de recherche par défaut {#restoring-default-search-facets}

Par défaut, une icône de cadenas ![icône cadenas fermé](assets/do-not-localize/lock_closed_icon.svg) apparaît devant le **[!UICONTROL Rail de recherche d’administration de ressources]** dans la page **[!UICONTROL Formulaires de recherche]**. L’icône de cadenas en regard d’une option de la page Formulaires de recherche indique que les paramètres par défaut sont intacts et non personnalisés. L’icône ![icône cadenas fermé](assets/do-not-localize/lock_closed_icon.svg) disparaît lorsque vous ajoutez des facettes de recherche au formulaire, ce qui indique que le formulaire par défaut a été modifié.

![Icône cadenas](assets/locked_admin_rail.png)

Pour restaurer la facette de recherche par défaut, procédez comme suit :

1. Sélectionnez **[!UICONTROL Rail de recherche d’administrateurs de ressources]** sur la page **[!UICONTROL Formulaires de recherche]**.
1. Cliquez sur **[!UICONTROL Supprimer]** ![deletecomposition](assets/do-not-localize/deleteoutline.png) dans la barre d’outils.
1. Dans la boîte de dialogue de confirmation, cliquez sur **[!UICONTROL Supprimer]** pour supprimer les modifications personnalisées.

   Après avoir supprimé les modifications personnalisées apportées aux facettes de recherche, l’icône de cadenas fermé ![icône cadenas fermé](assets/do-not-localize/lock_closed_icon.svg) réapparaît devant le **[!UICONTROL Rail de recherche d’administration de ressources]** de la page **[!UICONTROL Formulaires de recherche]**.

## Autorisations d’utilisateur {#user-permissions}

Si le rôle d’administrateur ne vous a pas été attribué, voici la liste des autorisations dont vous avez besoin pour réaliser des actions de modification, de suppression et d’affichage d’aperçu impliquant des facettes de recherche.

| Action | Autorisations |
| ------------------- | ---------------------------------------------------------------- |
| [!UICONTROL Modifier] | Autorisations en lecture et écriture sur le nœud `/apps` dans CRXDE |
| [!UICONTROL Supprimer] | Autorisations en lecture, écriture et suppression sur le nœud `/apps` dans CRXDE |
| [!UICONTROL Aperçu] | Autorisations en lecture, écriture et suppression sur le nœud `/var/dam/content` dans CRXDE. De même que les autorisations en lecture et écriture sur le nœud `/apps`. |

>[!MORELIKETHIS]
>
>* [Extension de la fonctionnalité de recherche de ressources](searchx.md)
>* [Recherche de ressources](search-assets.md)
