---
title: 'schémas de métadonnées pour définir la disposition de la page des propriétés de métadonnées dans [!DNL Adobe Experience Manager Assets]. '
description: Le schéma de métadonnées définit la mise en page de la page de propriétés, ainsi que les propriétés de métadonnées affichées pour les ressources. Apprenez à créer un schéma de métadonnées personnalisé, à le modifier et à l’appliquer aux ressources.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 29cf202b2522b4e624960e8b911f77ec7f291e24
workflow-type: tm+mt
source-wordcount: '2667'
ht-degree: 52%

---


# Schémas de métadonnées {#metadata-schemas}

Les entreprises proposent un modèle de métadonnées qui améliore la découverte, l’utilisation, l’interopérabilité des ressources, etc. L’application correcte des métadonnées est indispensable à la gestion de workflows et de processus reposant sur les métadonnées. Pour respecter la stratégie et les normes de métadonnées à l’échelle de l’entreprise, vous pouvez utiliser des schémas de métadonnées qui aident les utilisateurs de la gestion des actifs numériques à s’aligner. [!DNL Adobe Experience Manager] permet des méthodes simples et flexibles pour créer, gérer et appliquer des schémas de métadonnées.

Dans [!DNL Adobe Experience Manager Assets], les schémas contiennent des champs spécifiques pour des informations spécifiques à remplir. Il contient également des informations de mise en page pour afficher les champs de métadonnées d’une manière conviviale. Les propriétés de métadonnées comprennent le titre, la description, les types MIME, les balises, etc. You can use the [!UICONTROL Metadata Schema Forms] editor to modify the existing schemas or add custom metadata schemas.

Pour vue et modifier la page de propriétés d’un fichier, procédez comme suit :

1. Cliquez sur l’option Propriétés **[!UICONTROL de la]** Vue dans les actions rapides de la mosaïque de ressources de la vue de carte. Vous pouvez également sélectionner un élément, puis cliquer sur **[!UICONTROL Propriétés]** Propriétés de la ![vue](assets/do-not-localize/info-circle-icon.png) dans la barre d’outils.

1. Vous pouvez modifier les différentes propriétés de métadonnées modifiables sous les onglets disponibles. However, you cannot modify the asset [!UICONTROL Type] in the [!UICONTROL Basic] tab of properties page.

   ![Onglet de base Propriétés du fichier, où le type de fichier ne peut pas être modifié](assets/asset-properties-basic-tab.png)

*Figure : Onglet Simple sur[!UICONTROL Propriétés]du fichier.*

Pour modifier le type MIME d’une ressource, utilisez un formulaire de schéma de métadonnées personnalisé ou modifiez un formulaire existant. See [Edit Metadata Schema Forms](/help/assets/metadata-schemas.md#edit-metadata-schema-forms) for more information. Si vous modifiez le schéma de métadonnées d’un type MIME, la mise en page des propriétés des fichiers et de tous les sous-types est modifiée. Par exemple, la modification d’un schéma jpeg sous `default/image` concerne uniquement la disposition des métadonnées (propriétés de ressource) des ressources du type MIME `image/jpeg`. Si vous modifiez le schéma par défaut, les modifications changent toutefois la disposition des métadonnées pour tous les types de ressources.

## Formulaires de schéma de métadonnées {#default-metadata-schema-forms}

Pour vue d’une liste de formulaires ou de modèles, dans [!DNL Experience Manager] l’interface, accédez à **[!UICONTROL Outils]** > **[!UICONTROL Ressources]** > Schémas **[!UICONTROL de]** métadonnées.

[!DNL Experience Manager] fournit les modèles de Schéma de métadonnées suivants.

| Modèles |  | Description |
|---|---|---|
| [!UICONTROL default] |  | schéma de métadonnées de base pour les ressources. |
|  | The following child forms inherit the properties of the [!UICONTROL default] form: |  |
|  | <ul><li>[!UICONTROL dm_video]</li></ul> | Schéma de formulaire pour les vidéos Dynamic Media. |
|  | <ul><li>[!UICONTROL image]</li></ul> | Schéma de formulaire pour les images de type MIME, par exemple `image/jpeg` et `image/png`. <br> Le formulaire [!UICONTROL image] comporte les modèles de formulaire enfant suivants : <ul><li> [!UICONTROL jpeg]: Schéma de formulaire pour les ressources avec un sous-type [!UICONTROL jpeg].</li> <li>[!UICONTROL tiff]: Formulaire de Schéma pour les actifs avec un sous-type TIFF.</li></ul> |
|  | <ul><li>[!UICONTROL l’application ;]</li></ul> | Schema form for assets with MIME type such as `application/pdf` and `application/zip`. <br>[!UICONTROL pdf]: Schéma de formulaire pour les ressources avec un sous-type PDF. |
|  | <ul><li>[!UICONTROL vidéo]</li></ul> | Schéma de formulaire pour les ressources vidéo de type MIME, par exemple `video/avi` et `video/mp4`. |
| [!UICONTROL collection] |  | Schéma de formulaire pour les collections. |
| [!UICONTROL contentfragment] |  | [Schéma de formulaire pour les fragments](/help/sites-developing/customizing-content-fragments.md)de contenu. |
| [!UICONTROL forms] |  | This schema form relates to [Adobe Experience Manager Forms](/help/forms/home.md). |
| [!UICONTROL ugc_contentfragment] |  | Formulaire de Schéma pour les éléments de contenu et les ressources générés par l’utilisateur intégrés dans le Experience Manager à partir des médias sociaux. |

>[!NOTE]
>
>Pour afficher les formulaires enfants d’un formulaire de schéma, cliquez sur le nom de ce dernier.

## Ajout d’un formulaire de schéma de métadonnées {#add-a-metadata-schema-form}

Pour ajouter un formulaire de schéma de métadonnées, procédez comme suit :

1. Pour ajouter un modèle personnalisé à la liste, cliquez sur **[!UICONTROL Créer]** dans la barre d’outils.

   >[!NOTE]
   >
   >Un symbole de verrouillage s’affiche avec les modèles non modifiés. Si vous personnalisez un modèle, il n’est pas verrouillé et ![verrouillé fermé](assets/do-not-localize/lock_closed_icon.svg).

1. In the dialog, provide the title of the schema form and click **[!UICONTROL Create]** to complete the form creation process.

## Modification des formulaires de schéma de métadonnées {#edit-metadata-schema-forms}

Vous pouvez modifier un formulaire de schéma de métadonnées existant ou nouvellement ajouté. Le formulaire de schéma de métadonnées contient des onglets et des éléments de formulaire dans les onglets. Vous pouvez associer ou configurer ces éléments de formulaire dans un champ au sein d’un nœud de métadonnées dans le référentiel CRX. Vous pouvez ajouter des onglets ou des éléments de formulaire au formulaire de schéma de métadonnées. Les onglets et les éléments de formulaire dérivés du parent sont à l’état verrouillé. Vous ne pouvez pas les modifier au niveau des enfants.

1. Sur la page Formulaires [!UICONTROL de Schéma de] métadonnées, sélectionnez un formulaire et cliquez sur **[!UICONTROL Modifier]** dans la barre d’outils.

1. Sur la page Editeur **** de Schéma de métadonnées, personnalisez le formulaire de métadonnées. Faites glisser les composants nécessaires de l’onglet **[!UICONTROL Créer un formulaire]** vers l’un des onglets.

   ![Editeur de Schéma de métadonnées pour personnaliser la page Propriétés du fichier](assets/metadata-schema-editor.png)

   *Figure : Page de l’éditeur[!UICONTROL de Schéma de]métadonnées contenant des onglets disponibles.*

1. Pour configurer un composant, sélectionnez-le et modifiez ses propriétés dans l’onglet **[!UICONTROL Paramètres]**.

### Components within the [!UICONTROL Build Form] tab {#components-within-the-build-form-tab}

L’onglet **[!UICONTROL Créer le formulaire]** répertorie les éléments de formulaire que vous utilisez dans votre formulaire de schéma. L’onglet **[!UICONTROL Paramètres]** contient les attributs de chaque élément sélectionné dans l’onglet **[!UICONTROL Créer le formulaire]**. Le tableau suivant répertorie les éléments de formulaire disponibles dans l’onglet **[!UICONTROL Créer le formulaire]** :

| Nom du composant | Description |
| -------------------------------- | ----------------------------------------------------------------------------------- |
| [!UICONTROL En-tête de section] | Permet d’ajouter un en-tête de section pour une liste de composants communs. |
| [!UICONTROL Une seule ligne de texte] | Permet d’ajouter une propriété d’une seule ligne de texte. Il est stocké sous la forme d’une chaîne. |
| [!UICONTROL Texte à plusieurs valeurs] | Permet d’ajouter une propriété de texte à plusieurs valeurs. Il est stocké sous forme de tableau de chaînes. |
| [!UICONTROL Nombre] | Permet d’ajouter un composant de nombre. |
| [!UICONTROL Date] | Permet d’ajouter un composant de date. |
| [!UICONTROL Liste déroulante] | Permet d’ajouter une liste déroulante. |
| [!UICONTROL Balises standard] | Permet d’ajouter une balise. |
| [!UICONTROL Balises intelligentes] | Ajoutez ce composant pour augmenter les capacités de recherche en ajoutant automatiquement des balises de métadonnées. |
| [!UICONTROL Champ masqué] | Permet d’ajouter un champ masqué. Il est envoyé en tant que paramètre POST lorsque la ressource est enregistrée. |
| [!UICONTROL Ressource référencée par] | Ajoutez ce composant pour afficher la liste des ressources référencées par la ressource. |
| [!UICONTROL Référencement des ressources] | Ajoutez ce composant pour afficher la liste des ressources qui référencent la ressource. |
| [!UICONTROL Références du produit] | Ajoutez ce composant pour afficher la liste des produits liés à la ressource. |
| [!UICONTROL Évaluation des ressources] | Ajoutez ce composant afin d’afficher des options pour évaluer la ressource. |
| [!UICONTROL Métadonnées contextuelles] | Ajoutez ce composant pour contrôler l’affichage des autres onglets de métadonnées dans la page de propriétés des ressources. |

#### Modification du composant de métadonnées {#edit-the-metadata-component}

To edit the properties of a metadata component on the form, click the component to edit all or a subset of the following properties in the **[!UICONTROL Settings]** tab.

**Libellé du champ** : nom de la propriété de métadonnées qui s’affiche sur la page des propriétés de la ressource.

**Associer à la propriété**: Cette propriété spécifie le chemin d’accès relatif ou le nom du noeud de ressource où il est enregistré dans le référentiel CRX. It starts with `./` to indicate that the path is under the asset&#39;s node.

Les valeurs admises pour cette propriété sont les suivantes :

* `./jcr:content/metadata/dc:title` : stocke la valeur dans le nœud de métadonnées de la ressource en tant que propriété `dc:title`.

* `./jcr:created` : stocke la date et l’heure de création d’une ressource. Il s’agit d’une propriété protégée. Si vous configurez ces propriétés, Adobe recommande de les marquer avec l’état Désactiver la modification.

Pour garantir que le composant s’affiche correctement dans le formulaire de schéma de métadonnées, le chemin de la propriété ne doit pas comporter d’espace.

* **Espace réservé** : utilisez cette propriété pour spécifier du texte dans l’espace réservé concernant la propriété de métadonnées.
* **Obligatoire** : utilisez cette propriété pour marquer une propriété de métadonnées comme étant obligatoire dans la page Propriétés.
* **Désactiver la modification**: Utilisez cette propriété pour interdire toute modification d’une propriété sur la page des propriétés.
* **Afficher le champ vide en lecture seule** : utilisez cette propriété pour afficher une propriété de métadonnées sur la page Propriétés même si elle ne possède pas de valeur. Par défaut, lorsqu’une propriété de métadonnées ne possède pas de valeur, elle n’est pas répertoriée sur la page Propriétés.
* **Afficher la liste classée** : utilisez cette propriété pour afficher une liste classée de choix..
* **Choix** : utilisez cette propriété pour spécifier des choix dans une liste.
* **Description** : utilisez cette propriété pour ajouter une brève description pour le composant de métadonnées.
* **Classe** : classe d’objets à laquelle la propriété est associée.
* **Supprimer**: Cliquez sur [!UICONTROL Supprimer] pour supprimer un composant du schéma.

>[!NOTE]
>
>The [!UICONTROL Hidden Field] component does not include these attributes. À la place, il comprend des propriétés, telles que les attributs Nom, Valeur, Libellé du champ et Description. Les valeurs du composant Champ masqué sont envoyées en tant que paramètre POST lors de l’enregistrement de la ressource. Elles ne sont pas enregistrées sous forme de métadonnées pour la ressource.

Si vous sélectionnez l’option **[!UICONTROL Obligatoire]**, vous pouvez rechercher des fichiers dont les métadonnées obligatoires sont manquantes. Dans le panneau **[!UICONTROL Filtres]**, développez le prédicat **[!UICONTROL Validation des métadonnées]** et sélectionnez l’option **[!UICONTROL Non valide]**. Les résultats de la recherche affichent des fichiers dont les métadonnées obligatoires que vous avez configurées via le formulaire de schéma sont manquantes.

![Option non valide sélectionnée dans le prédicat Validation des métadonnées du panneau Filtres ](assets/chlimage_1-178.png)

Si vous ajoutez le composant Métadonnées contextuelles à un onglet d’un formulaire de schéma, le composant apparaît sous forme de liste sur la page Propriétés des ressources auxquelles ce       schéma particulier est appliqué. La liste inclut tous les autres onglets, à l’exception de celui auquel vous avez appliqué le composant Métadonnées contextuelles. Actuellement, cette fonctionnalité fournit des fonctions de base pour contrôler l’affichage des métadonnées en fonction du contexte.

![Composant de métadonnées contextuelles répertoriant les onglets des propriétés de la ressource](assets/chlimage_1-179.png)

Pour afficher tout onglet de la page de propriétés en plus de l’onglet dans lequel le composant Métadonnées contextuelles est appliqué, sélectionnez l’onglet dans la liste. L’onglet est ajouté à la page Propriétés.

![L’onglet sélectionné dans la liste de métadonnées contextuelles s’affiche sur la page des propriétés des ressources.](assets/contextual-metadata-asset-properties.png)

*Figure : Métadonnées contextuelles dans la page de propriétés des ressources.*

### Spécification des propriétés dans le fichier JSON {#specify-properties-in-json-file}

Au lieu de définir les propriétés des options sous l’onglet **[!UICONTROL Paramètres]**, vous pouvez définir les options d’un fichier JSON en spécifiant les paires clé-valeur correspondantes. Spécifiez le chemin d’accès au fichier JSON dans le champ **[!UICONTROL Chemin d’accès JSON]**.

#### Ajout ou suppression d’un onglet dans le formulaire de schéma {#adding-deleting-a-tab-in-the-schema-form}

L’éditeur de schéma vous permet d’ajouter ou de supprimer un onglet. The default schema form includes the **[!UICONTROL Basic]**, **[!UICONTROL Advanced]** , **[!UICONTROL IPTC]**, and **[!UICONTROL IPTC Extension]** tabs.

![Onglets par défaut dans le formulaire de Schéma de métadonnées](assets/chlimage_1-181.png)

Cliquez sur `+` pour ajouter un onglet à un formulaire de schéma. By default, the new tab has the name `Unnamed-1`. Vous pouvez modifier le nom à partir de l&#39;onglet **[!UICONTROL Paramètres]**.

Pour supprimer un onglet, cliquez sur `X`.

![Ajouter ou supprimer un onglet à l’aide de l’éditeur de Schéma de métadonnées](assets/chlimage_1-182.png)

## Suppression de formulaires de schéma de métadonnées {#delete-metadata-schema-forms}

[!DNL Experience Manager] vous permet uniquement de supprimer des formulaires de schéma personnalisés. Il ne vous permet pas de supprimer les formulaires/modèles de schéma par défaut. Cependant, vous pouvez supprimer toutes les modifications personnalisées dans ces formulaires.

Pour supprimer un formulaire, sélectionnez-le, puis cliquez sur Supprimer.

>[!NOTE]
>
>* Après avoir supprimé les modifications personnalisées apportées à un formulaire par défaut, le ![verrouillage fermé](assets/do-not-localize/lock_closed_icon.svg) réapparaît avant le formulaire. Il indique que l’état par défaut du formulaire est rétabli.
>* Vous ne pouvez pas supprimer les formulaires de schéma de métadonnées par défaut dans [!DNL Assets].


## Formulaires de schéma pour les types MIME    {#schema-forms-for-mime-types}

[!DNL Experience Manager] fournit des formulaires par défaut pour plusieurs types MIME prêts à l’emploi. Vous pouvez toutefois ajouter des formulaires personnalisés pour les ressources de plusieurs types MIME.

### Add new forms for MIME types {#add-new-forms-for-mime-types}

Créez un formulaire sous le type de formulaire approprié. For example, to add a template for the `image/png` subtype, create the form under the &quot;image&quot; forms. Le titre du formulaire de schéma est le nom du sous-type. In this case, the title is `png`.

#### Use an existing schema template for various MIME types {#use-an-existing-schema-template-for-various-mime-types}

Vous pouvez utiliser un modèle existant pour un autre type MIME. Par exemple, utilisez le formulaire `image/jpeg` pour les ressources de type MIME `image/png`.

In this case, create a node at `/etc/dam/metadataeditor/mimetypemappings` in the CRX repository. Indiquez un nom pour le nœud et définissez les propriétés suivantes :

| Nom | Description | Type | Valeur |
|------|-------------|------|-------|
| `exposedmimetype` | Nom du formulaire existant à associer | `String` | `image/jpeg` |
| `mimetypes` | Liste des types MIME qui utilisent le formulaire défini dans l’attribut `exposedmimetype`. | `String` | `image/png` |

[!DNL Assets] mappe les types MIME et les formulaires de schéma suivants :

| Formulaire de schéma | Types MIME |
| --------------------------- | --------------------------------------------------- |
| image/jpeg | image/pjpeg |
| image/tiff | image/x-tiff |
| application/pdf | application/postscript |
| application/x-ImageSet | Multipart/Related; type=application/x-ImageSet |
| application/x-SpinSet | Multipart/Related; type=application/x-SpinSet |
| application/x-MixedMediaSet | Multipart/Related; type=application/x-MixedMediaSet |
| video/quicktime | video/x-quicktime |
| video/mpeg4 | video/mp4 |
| video/avi | video/avi, video/msvideo, video/x-msvideo |
| video/wmv | video/x-ms-wmv |
| video/flv | video/x-flv |

## Octroi de l’accès aux schémas de métadonnées {#grant-access-to-metadata-schemas}

La fonction Schéma de métadonnées n’est disponible que pour les administrateurs. Cependant, les administrateurs peuvent fournir un accès aux non-administrateurs en modifiant certaines autorisations. Indiquez aux utilisateurs non administrateurs les autorisations de création, de modification et de suppression sur le `/conf` dossier.

## Application de métadonnées spécifiques au dossier {#apply-folder-specific-metadata}

[!DNL Assets] vous permet de définir une variation d’un schéma de métadonnées et de l’appliquer à un dossier spécifique.

Par exemple, vous pouvez définir une variation du schéma de métadonnées par défaut et l’appliquer à un dossier. Lorsque vous appliquez le schéma modifié, il remplace le schéma de métadonnées d’origine par défaut qui est appliqué aux ressources du dossier.

Seuls les fichiers téléchargés vers le dossier auquel ce schéma est appliqué sont conformes aux métadonnées modifiées définies dans le schéma de métadonnées de variante. [!DNL Assets] dans d’autres dossiers où le schéma d’origine est appliqué, la conformité aux métadonnées définies dans le schéma d’origine est maintenue.

L’héritage des métadonnées par les ressources est basé sur le schéma appliqué au dossier de premier niveau dans la hiérarchie. Autrement dit, si un dossier ne contient aucun sous-dossier, les ressources du dossier héritent des métadonnées du schéma appliqué au dossier.

Vous pouvez appliquer un autre schéma au sous-dossier. Les ressources d’un sous-dossier héritent du schéma de métadonnées du sous-dossier immédiat. Si aucun schéma ou le même schéma n’est appliqué au niveau du sous-dossier, ses ressources héritent du schéma du dossier parent.

1. Dans [!DNL Experience Manager] l’interface, accédez à **[!UICONTROL Outils]** > **[!UICONTROL Ressources]** > Schémas **** de métadonnées. La page **[!UICONTROL Formulaires de schéma de métadonnées]** s’affiche.
1. Select the check box before a form, for example the default metadata form, and click the **[!UICONTROL Copy]** and save it as a custom form. Spécifiez un nom personnalisé pour le formulaire, par exemple `my_default`. Vous pouvez également créer un formulaire personnalisé.

1. In the **[!UICONTROL Metadata Schema Forms]** page, select the `my_default` form, and then click **[!UICONTROL Edit]**.

1. Sur la page **[!UICONTROL Éditeur de schéma de métadonnées]**, ajoutez un champ de texte au formulaire de schéma. For example, add a field with the label **[!UICONTROL Category]**.

   ![Champ de texte ajouté à l’éditeur de Schéma de métadonnées](assets/text-field-metadata-schema-editor.png)

   *Figure : Champ de texte ajouté à l’éditeur de schéma de métadonnées.*

1. Cliquez sur **[!UICONTROL Enregistrer]**. Le formulaire modifié figure sur la page **[!UICONTROL Formulaires de schéma de métadonnées]**.
1. Click **[!UICONTROL Apply to Folder(s)]** from the toolbar to apply the custom metadata to a folder.

1. Select the folder on which to apply the modified schema and then click **[!UICONTROL Apply]**.

   ![Sélectionner le dossier dans lequel appliquer le Schéma de métadonnées](assets/chlimage_1-188.png)

1. Si d’autres métadonnées sont appliquées au dossier, un message s’affiche pour vous avertir que vous êtes sur le point de remplacer le schéma de métadonnées existant. Cliquez sur **Remplacer**.
1. Cliquez sur **OK** pour fermer le message de confirmation.
1. Accédez au dossier auquel vous avez appliqué le schéma de métadonnées modifié.

## Définition des métadonnées obligatoires {#define-mandatory-metadata}

Vous pouvez définir des champs obligatoires au niveau d’un dossier, qui s’appliquent aux ressources chargées dans ce dossier. Si vous téléchargez des fichiers avec des métadonnées manquantes pour les champs obligatoires définis précédemment, une indication visuelle des métadonnées manquantes s’affiche sur les fichiers dans la vue de cartes.

>[!NOTE]
>
>Un champ de métadonnées peut être défini comme obligatoire en fonction de la valeur d’un autre champ. In the card view, [!DNL Experience Manager] does not display the warning message about missing metadata for such mandatory metadata fields.

1. Dans [!DNL Experience Manager] l’interface, accédez à **[!UICONTROL Outils]** > **[!UICONTROL Ressources]** > Schémas **** de métadonnées. La page **[!UICONTROL Formulaires de schéma de métadonnées]** s’affiche.
1. Enregistrez le formulaire de métadonnées par défaut en tant que formulaire personnalisé. Par exemple, enregistrez-le sous le nom `my_default`.

1. Modifiez le formulaire personnalisé. Ajoutez un champ obligatoire. Par exemple, ajoutez un champ **[!UICONTROL Catégorie]** et rendez-le obligatoire.

   ![Ajoutez un champ obligatoire au formulaire de métadonnées en sélectionnant Obligatoire dans l’onglet Règles de l’éditeur de Schémas de métadonnées.](assets/mandatory-field-metadata-schema-editor.png)

   *Figure : Champ obligatoire dans l’éditeur de schémas de métadonnées.*

1. Cliquez sur **[!UICONTROL Enregistrer]**. Le formulaire modifié figure sur la page **[!UICONTROL Formulaires de schéma de métadonnées.]** Select the form and then click **[!UICONTROL Apply to Folder(s)]** from the toolbar to apply the custom metadata to a folder.

1. Accédez au dossier et chargez des ressources présentant des données manquantes pour le champ obligatoire que vous avez ajouté au formulaire personnalisé. Un message indiquant les métadonnées manquantes pour le champ obligatoire s’affiche sur la vue de carte de la ressource.

   ![Message signalant l’absence de métadonnées obligatoires sur la vue de la carte de ressources lors du téléchargement de fichiers dans un dossier](assets/chlimage_1-192.png)

1. (Facultatif) Accédez à `https://[aem_server]:[port]/system/console/components/`. Configurez et activez le composant `com.day.cq.dam.core.impl.MissingMetadataNotificationJob` ; celui-ci est désactivé par défaut. Set a frequency at which [!DNL Experience Manager] checks for the validity of metadata on the assets. Cette configuration ajoute une propriété `hasValidMetadata` au nœud `jcr:content` des ressources. [!DNL Experience Manager] utilise cette propriété pour filtrer les actifs non valides dans un résultat de recherche. Si vous ajoutez un fichier après une vérification, le fichier n’est marqué avec `hasValidMetadata` aucun indicateur jusqu’à la prochaine vérification planifiée. Par conséquent, les ressources n’apparaissent pas dans les filtres de recherche pour les métadonnées non valides avant la prochaine vérification planifiée.

   >[!CAUTION]
   >
   >Les contrôles de validation des métadonnées nécessitent beaucoup de ressources et peuvent avoir un impact sur les performances de votre système. Planifiez les contrôles en conséquence. Si le serveur n’est pas en mesure de faire face à la charge, essayez de désactiver cette tâche.

<!-- TBD: Add this method to find invalid metadata in the metadata.md article later when it is published as a top-level metadata article.
-->
