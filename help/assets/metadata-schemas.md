---
title: Les schémas de métadonnées définissent la disposition de la page des propriétés de métadonnées.
description: Le schéma de métadonnées définit la mise en page de la page des propriétés et les propriétés de métadonnées affichées pour les ressources. Découvrez comment créer un schéma de métadonnées personnalisé, modifier un schéma de métadonnées et appliquer un schéma de métadonnées à des ressources.
contentOwner: AG
mini-toc-levels: 1
role: User,Admin
feature: Metadata
exl-id: 0dd322cd-ce97-4335-825d-71f72a5e438c
hide: true
source-git-commit: 3d5e9ad8ee19756b05e5a77a3f748bc647fcf734
workflow-type: tm+mt
source-wordcount: '3618'
ht-degree: 81%

---

# Schémas de métadonnées {#metadata-schemas}

| Version | Lien de l’article |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Cliquez ici](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/assets/manage/metadata-schemas.html?lang=fr) |
| AEM 6.5 | Cet article |

Les entreprises disposent d’un modèle de métadonnées qui améliore la découverte, l’utilisation, l’interopérabilité des ressources, etc. L’application correcte des métadonnées est sacro-sainte pour gérer les workflows et les processus pilotés par les métadonnées. Pour respecter la stratégie et les normes de métadonnées à l’échelle de l’entreprise, vous pouvez utiliser des schémas de métadonnées qui aident les utilisateurs de la gestion des actifs numériques à s’aligner sur celles-ci. [!DNL Adobe Experience Manager] Met à disposition des méthodes simples et flexibles pour créer, gérer et appliquer des schémas de métadonnées.

Dans [!DNL Adobe Experience Manager Assets], les schémas contiennent des champs spécifiques pour renseigner des informations spécifiques. Il contient également des informations de mise en page pour afficher les champs de métadonnées de manière conviviale. Les propriétés de métadonnées incluent le titre, la description, les types MIME, les balises, etc. Vous pouvez utiliser l’éditeur de [!UICONTROL formulaires de schéma de métadonnées] pour modifier des schémas existants ou ajouter des schémas de métadonnées personnalisés.

Pour afficher et modifier la page des propriétés d’une ressource, procédez comme suit :

1. Cliquez sur l’option **[!UICONTROL Afficher les propriétés]** dans les actions rapides sur la mosaïque de la ressource en mode Carte. Vous pouvez également sélectionner une ressource, puis cliquer sur **[!UICONTROL Propriétés]** ![afficher les propriétés](assets/do-not-localize/info-circle-icon.png) dans la barre d’outils.

1. Vous pouvez modifier les différentes propriétés de métadonnées modifiables dans les onglets disponibles. Toutefois, vous ne pouvez pas modifier le [!UICONTROL type] de ressource dans l’onglet [!UICONTROL De base] de la page des propriétés.

   ![Onglet De base des propriétés de la ressource, dans lequel le type de ressource ne peut pas être modifié](assets/asset-properties-basic-tab.png)

   *Image : onglet De base des [!UICONTROL propriétés de la ressource].*

   Assurez-vous qu’une seule propriété est mappée à un champ lorsque vous créez ou modifiez le schéma de métadonnées.

   Pour modifier le type MIME d’une ressource, utilisez un formulaire de schéma de métadonnées personnalisé ou modifiez un formulaire existant. Consultez [Modifier un formulaire de schéma de métadonnées](#edit-metadata-schema-forms) pour plus d’informations. Si vous modifiez le schéma de métadonnées d’un type MIME, la mise en page des propriétés des ressources et de tous les sous-types est modifiée. Par exemple, la modification d’un schéma jpeg sous `default/image` concerne uniquement la disposition des métadonnées (propriétés de ressource) des ressources du type MIME `image/jpeg`. Si vous modifiez le schéma par défaut, les modifications changent toutefois la disposition des métadonnées pour tous les types de ressources.

## Formulaires de schéma de métadonnées {#default-metadata-schema-forms}

Pour afficher la liste des formulaires ou des modèles, dans l’interface [!DNL Experience Manager], accédez à **[!UICONTROL Outils]** > **[!UICONTROL Ressources]** > **[!UICONTROL Schémas de métadonnées]**.

[!DNL Experience Manager] fournit les modèles de formulaire de schéma de métadonnées suivants.

| Modèles |  | Description |
|---|---|---|
| [!UICONTROL default] |  | Le formulaire de schéma de métadonnées de base pour les ressources |
|  | Les formulaires enfants suivants héritent des propriétés du formulaire par [!UICONTROL défaut] : |  |
|  | <ul><li>[!UICONTROL dm_video]</li></ul> | Formulaire de schéma pour les vidéos Dynamic Media. |
|  | <ul><li>[!UICONTROL image]</li></ul> | Formulaire de schéma pour les images dotées d’un type MIME telles que `image/jpeg` et `image/png` <br>Le formulaire [!UICONTROL image] possède les modèles de formulaire enfant suivants : <ul><li> [!UICONTROL jpeg] : formulaire de schéma pour les ressources avec le sous-type [!UICONTROL jpeg].</li> <li>[!UICONTROL tiff] : formulaire de schéma pour les ressources avec le sous-type TIFF.</li></ul> |
|  | <ul><li>[!UICONTROL l’application ;]</li></ul> | Formulaire de schéma pour les ressources dotées du type MIME, par exemple `application/pdf` et `application/zip` <br>[!UICONTROL pdf] : formulaire de schéma pour les ressources avec le sous-type PDF. |
|  | <ul><li>[!UICONTROL vidéo]</li></ul> | Formulaire de schéma pour les ressources vidéo dotées d’un type MIME telles que `video/avi` et `video/mp4` |
| [!UICONTROL collection] |  | Formulaire de schéma pour les collections |
| [!UICONTROL contentfragment] |  | [Formulaire de schéma pour les fragments de contenu](/help/sites-developing/customizing-content-fragments.md) |
| [!UICONTROL formulaires] |  | Ce formulaire de schéma est associé aux [Adobe Experience Manager Forms](/help/forms/home.md). |
| [!UICONTROL ugc_contentfragment] |  | Formulaire de schéma pour les éléments de contenu et les ressources générés par l’utilisateur intégrés dans Experience Manager à partir des médias sociaux. |

>[!NOTE]
>
>Pour afficher les formulaires enfants d’un formulaire de schéma, cliquez sur le nom de ce dernier.

## Ajout d’un formulaire de schéma de métadonnées {#add-a-metadata-schema-form}

Pour ajouter un formulaire de schéma de métadonnées, procédez comme suit :

1. Pour ajouter un modèle personnalisé à la liste, cliquez sur **[!UICONTROL Créer]** dans la barre d’outils.

   >[!NOTE]
   >
   >Un cadenas s’affiche avec les modèles non modifiés. Si vous personnalisez un modèle, il n’est pas verrouillé ![lock closed](assets/do-not-localize/lock_closed_icon.svg).

1. Dans la boîte de dialogue, saisissez le titre du formulaire de schéma, puis cliquez sur **[!UICONTROL Créer]** pour terminer la création du formulaire.

## Modification des formulaires de schéma de métadonnées {#edit-metadata-schema-forms}

Vous pouvez modifier un formulaire de schéma de métadonnées existant ou nouvellement ajouté. Le formulaire de schéma de métadonnées comprend des onglets et des éléments de formulaire dans des onglets. Vous pouvez associer ou configurer ces éléments de formulaire dans un champ au sein d’un nœud de métadonnées dans le référentiel CRX. Vous pouvez ajouter des onglets ou des éléments de formulaire au formulaire de schéma de métadonnées. Les onglets et les éléments de formulaire dérivés du parent sont à l’état verrouillé. Vous ne pouvez pas les modifier au niveau des enfants.

1. Sur la page [!UICONTROL Formulaires de schéma de métadonnées], sélectionnez un formulaire et cliquez sur **[!UICONTROL Modifier]** dans la barre d’outils.

1. Sur la page **[!UICONTROL Éditeur de formulaire de schéma de métadonnées]**, personnalisez le formulaire de métadonnées. Faites glisser les composants nécessaires de l’onglet **[!UICONTROL Créer le formulaire]** vers l’un des onglets.

1. Pour configurer un composant, sélectionnez-le et modifiez ses propriétés dans l’onglet **[!UICONTROL Paramètres]**.

### Composants de l’onglet [!UICONTROL Créer le formulaire] {#components-within-the-build-form-tab}

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

Pour modifier les propriétés d’un composant de métadonnées dans le formulaire, cliquez sur le composant et modifiez l’ensemble ou un sous-ensemble des propriétés suivantes dans l’onglet **[!UICONTROL Paramètres.]** Il est recommandé de ne mapper qu’un champ à une propriété donnée dans le schéma de métadonnées. Sinon, le dernier champ ajouté mappé à la propriété est sélectionné par le système.

**Libellé du champ** : nom de la propriété de métadonnées qui s’affiche sur la page des propriétés de la ressource.

**Associer à la propriété** : cette propriété spécifie le chemin ou le nom relatif du nœud de la ressource où elle est enregistrée dans le référentiel CRX. Elle commence par `./` pour indiquer que le chemin d’accès se situe sous le nœud de la ressource.

Voici des exemples de valeurs valides pour une propriété :

* `./jcr:content/metadata/dc:title` : stocke la valeur dans le nœud de métadonnées de la ressource en tant que propriété `dc:title`.

* `./jcr:created` : stocke la date et l’heure de création d’une ressource. Il s’agit d’une propriété protégée. Si vous configurez ces propriétés, Adobe recommande de les marquer avec l’état Désactiver la modification. Dans le cas contraire, l’erreur « Échec de modification des ressources » est générée lorsque vous enregistrez les propriétés de la ressource.

Pour garantir que le composant s’affiche correctement dans le formulaire de schéma de métadonnées, le chemin de la propriété ne doit pas comporter d’espace.

* **Espace réservé**: Utilisez cette propriété pour spécifier le texte d’espace réservé approprié concernant la propriété de métadonnées.
* **Obligatoire**: Utilisez cette propriété pour marquer une propriété de métadonnées comme étant obligatoire sur la page des propriétés.
* **Désactiver la modification** : utilisez cette propriété pour interdire toute modification apportée à une propriété sur la page des propriétés.
* **Afficher le champ vide en lecture seule** : utilisez cette propriété pour afficher une propriété de métadonnées sur la page Propriétés même si elle ne possède pas de valeur. Par défaut, lorsqu’une propriété de métadonnées ne possède pas de valeur, elle n’est pas répertoriée sur la page Propriétés.
* **Afficher la liste classée** : utilisez cette propriété pour afficher une liste classée de choix..
* **Choix** : utilisez cette propriété pour spécifier des choix dans une liste.
* **Description** : utilisez cette propriété pour ajouter une brève description pour le composant de métadonnées.
* **Classe**: Classe d’objet à laquelle la propriété est associée.
* **Supprimer** : cliquez sur [!UICONTROL Supprimer] pour supprimer un composant du formulaire de schéma.

>[!NOTE]
>
>Le composant [!UICONTROL Champ masqué] n’inclut pas ces attributs. Il inclut plutôt des propriétés, telles que le nom des attributs, la valeur, le libellé du champ et la description. Les valeurs du composant Champ masqué sont envoyées en tant que paramètre de POST chaque fois que la ressource est enregistrée. Il n’est pas enregistré en tant que métadonnées pour la ressource.

Si vous sélectionnez l’option **[!UICONTROL Obligatoire]**, vous pouvez rechercher des fichiers dont les métadonnées obligatoires sont manquantes. Dans le panneau **[!UICONTROL Filtres]**, développez le prédicat **[!UICONTROL Validation des métadonnées]** et sélectionnez l’option **[!UICONTROL Non valide]**. Les résultats de la recherche affichent des fichiers dont les métadonnées obligatoires que vous avez configurées via le formulaire de schéma sont manquantes.

![Option sélectionnée dans le prédicat Validation des métadonnées du panneau Filtres](assets/invalid-metadata-predicate.png)

Si vous ajoutez le composant Métadonnées contextuelles à un onglet d’un formulaire de schéma, le composant apparaît sous forme de liste sur la page Propriétés des ressources auxquelles ce      schéma particulier est appliqué. La liste inclut tous les autres onglets, à l’exception de celui auquel vous avez appliqué le composant Métadonnées contextuelles. Actuellement, cette fonctionnalité fournit des fonctions de base pour contrôler l’affichage des métadonnées en fonction du contexte.

![Composant de métadonnées contextuelles répertoriant les onglets des propriétés des ressources](assets/metadata-contextual-component-list.png)

Pour afficher un onglet sur la page Propriétés en plus de l’onglet auquel le composant Métadonnées contextuelles est appliqué, sélectionnez-le dans la liste. L’onglet est ajouté à la page Propriétés.

![L’onglet sélectionné dans la liste des métadonnées contextuelles s’affiche sur la page des propriétés de la ressource.](assets/contextual-metadata-asset-properties.png)

*Image : métadonnées contextuelles dans la page des propriétés de la ressource.*

### Spécification des propriétés dans le fichier JSON {#specify-properties-in-json-file}

Au lieu de définir les propriétés des options sous l’onglet **[!UICONTROL Paramètres]**, vous pouvez définir les options d’un fichier JSON en spécifiant les paires clé-valeur correspondantes. Spécifiez le chemin d’accès au fichier JSON dans le champ **[!UICONTROL Chemin d’accès JSON]**.

#### Ajout ou suppression d’un onglet dans le formulaire de schéma {#adding-deleting-a-tab-in-the-schema-form}

L’éditeur de schéma vous permet d’ajouter ou de supprimer un onglet. Le formulaire de schéma par défaut inclut les onglets **[!UICONTROL De base]**, **[!UICONTROL Avancé]**, **[!UICONTROL IPTC]** et **[!UICONTROL Extension IPTC]**.

Cliquez sur `+` pour ajouter un onglet à un formulaire de schéma. Par défaut, le nouvel onglet porte le nom `Unnamed-1`. Vous pouvez modifier le nom à partir de l’onglet **[!UICONTROL Paramètres]**. Pour supprimer un onglet, cliquez sur `X`.

![Ajout ou suppression d’un onglet à l’aide de l’éditeur de schéma de métadonnées](assets/metadata-schema-form-new-tab.png)

## Métadonnées en cascade {#cascading-metadata}

Lors de la capture des informations de métadonnées d’une ressource, les utilisateurs fournissent des informations dans les différents champs disponibles. Vous pouvez afficher des champs de métadonnées ou des valeurs de champ spécifiques en fonction des options sélectionnées dans les autres champs. Ce type d’affichage conditionnel des métadonnées est appelé métadonnées en cascade. En d’autres termes, vous pouvez créer une dépendance entre un champ/une valeur de métadonnées spécifique et un ou plusieurs champs et/ou leurs valeurs.

Utilisez des schémas de métadonnées pour définir des règles d’affichage des métadonnées en cascade. Par exemple, si votre schéma de métadonnées comprend un champ de type de ressource, vous pouvez définir un ensemble de champs pertinent à afficher en fonction du type de ressource sélectionné par l’utilisateur.

>[!CAUTION]
>
>Les métadonnées en cascade ne sont pas prises en charge pour les fragments de contenu.

Voici quelques cas d’utilisation pour lesquels vous pouvez définir des métadonnées en cascade :

* Lorsque l’emplacement de l’utilisateur est requis, affichez les noms de ville pertinents en fonction du choix de pays et d’état de l’utilisateur.
* Chargez les noms de marque pertinents dans une liste en fonction du choix de catégorie de produits par l’utilisateur.
* Active/désactive la visibilité d’un champ spécifique en fonction de la valeur spécifiée dans un autre champ. Par exemple, affichez des champs d’adresse de livraison distincts si l’utilisateur souhaite que l’envoi soit envoyé à une autre adresse.
* Désigner un champ comme obligatoire en fonction de la valeur spécifiée dans un autre champ.
* Modifiez les options affichées pour un champ particulier en fonction de la valeur spécifiée dans un autre champ.
* Définissez la valeur de métadonnées par défaut dans un champ particulier en fonction de la valeur spécifiée dans un autre champ.

### Configuration des métadonnées en cascade dans [!DNL Experience Manager] {#configure-cascading-metadata-in-aem}

Supposons que vous souhaitiez afficher des métadonnées en cascade en fonction du type de ressource sélectionné. Quelques exemples

* Pour une vidéo, affichez les champs applicables tels que le format, le codec, la durée, etc.
* Pour un document Word ou PDF, affichez des champs tels que le nombre de pages, l’auteur, etc.

Sans tenir compte du type de ressource choisi, affichez les informations de copyright comme étant un champ requis.

1. Dans l’interface [!DNL Experience Manager], accédez à **[!UICONTROL Outils]** > **[!UICONTROL Ressources]** > **[!UICONTROL Schémas de métadonnées]**.
1. Dans la page **[!UICONTROL Formulaires de schéma]**, sélectionnez un formulaire de schéma, puis cliquez sur **[!UICONTROL Modifier]** dans la barre d’outils pour modifier le schéma.

   ![select_form](assets/select_form.png)

1. (Facultatif) Dans l’éditeur de schéma de métadonnées, créez un champ à conditionner. Spécifiez un nom et un chemin de propriété dans la variable **[!UICONTROL Paramètres]** .

   Pour créer un onglet, cliquez sur `+` afin d’ajouter un onglet, puis ajoutez un champ de métadonnées.

   ![add_tab](assets/add_tab.png)

1. Ajoutez un champ déroulant pour le type de ressource. Spécifiez un nom et un chemin de propriété dans la variable **[!UICONTROL Paramètres]** . Ajoutez une description facultative.

   ![asset_type_field](assets/asset_type_field.png)

1. Les paires clé-valeur sont les options fournies à un utilisateur de formulaire. Vous pouvez fournir les paires clé-valeur manuellement ou à partir d’un fichier JSON.

   * Pour spécifier les valeurs manuellement, sélectionnez **[!UICONTROL Ajouter manuellement]**, cliquez sur **[!UICONTROL Ajouter un choix]**, puis spécifiez le texte et la valeur de l’option. Par exemple, spécifiez les types de ressources Vidéo, PDF, Word et Image.

   * Pour récupérer dynamiquement les valeurs d’un fichier JSON, sélectionnez **[!UICONTROL Ajout via le chemin JSON]** et indiquez le chemin d’accès au fichier JSON. [!DNL Experience Manager] récupère les paires clé/valeur en temps réel lorsque le formulaire est présenté à l’utilisateur.

   Les deux options s’excluent mutuellement. Vous ne pouvez pas importer les options d’un fichier JSON et les modifier manuellement.

   ![add_choice](assets/add_choice.png)

   >[!NOTE]
   >
   >Lorsque vous ajoutez un fichier JSON, les paires clé/valeur ne sont pas affichées dans l’éditeur de schéma de métadonnées, mais sont disponibles dans le formulaire publié.

   >[!NOTE]
   >
   >Lorsque vous ajoutez des choix, si vous cliquez sur le champ de liste déroulante, l’interface se déforme et l’option de suppression des choix cesse de fonctionner. Ne cliquez pas sur la liste déroulante tant que vous n’avez pas enregistré les modifications. Si vous rencontrez ce problème, enregistrez le schéma, puis rouvrez-le pour poursuivre la modification.

1. (Facultatif) Ajoutez les autres champs obligatoires. Par exemple, format, codec et durée pour le type de ressource vidéo.

   De même, ajoutez des champs dépendants pour d’autres types de ressources. Par exemple, ajoutez des champs Nombre de pages et Auteur pour les ressources de documents, tels que des fichiers PDF et Word.

   ![video_dependent_fields](assets/video_dependent_fields.png)

1. Pour créer une dépendance entre le champ de type de ressource et d’autres champs, sélectionnez le champ dépendant et ouvrez l’onglet **[!UICONTROL Règles]**.

   ![select_dependentfield](assets/select_dependentfield.png)

1. Sous **[!UICONTROL Condition requise]**, sélectionnez l’option **[!UICONTROL Requis, d’après la nouvelle règle]**.
1. Cliquez sur **[!UICONTROL Ajouter une règle]**, puis sélectionnez le champ **[!UICONTROL Type de ressource]** pour créer une dépendance. Sélectionnez également la valeur du champ sur lequel vous souhaitez créer la dépendance. Dans ce cas, sélectionnez **[!UICONTROL Vidéo]**. Cliquez sur **[!UICONTROL Terminé]** pour enregistrer les modifications.

   ![define_rule](assets/define_rule.png)

   >[!NOTE]
   >
   >Une liste déroulante avec des valeurs prédéfinies manuellement peut être utilisée avec des règles. Les menus déroulants avec chemin JSON configuré ne peuvent pas être utilisés avec des règles qui utilisent des valeurs prédéfinies pour appliquer des conditions. Si les valeurs sont chargées à partir de JSON au moment de l’exécution, il n’est pas possible d’appliquer une règle prédéfinie.

1. Sous **[!UICONTROL Visibilité]**, sélectionnez l’option **[!UICONTROL Visible, d’après la nouvelle règle]**.

1. Cliquez sur **[!UICONTROL Ajouter une règle]**, puis sélectionnez le champ **[!UICONTROL Type de ressource]** pour créer une dépendance. Sélectionnez également la valeur du champ sur lequel vous souhaitez créer la dépendance. Dans ce cas, sélectionnez **[!UICONTROL Vidéo]**. Cliquez sur **[!UICONTROL Terminé]** pour enregistrer les modifications.

   ![define_visibilityrule](assets/define_visibilityrule.png)

   >[!NOTE]
   >
   >Cliquer sur un espace (ou à tout autre endroit que sur les valeurs) réinitialise les valeurs. Si cela se produit, sélectionnez à nouveau les valeurs.

   >[!NOTE]
   >
   >Vous pouvez appliquer les conditions **[!UICONTROL Condition requise]** et **[!UICONTROL Visibilité]** indépendamment l’une de l’autre.

1. De la même façon, créez une dépendance entre la valeur Vidéo dans le champ Type de ressource et d’autres champs, tels que Codec et Durée.
1. Répétez les étapes pour créer une dépendance entre les ressources de documents (PDF, Word) dans le champ [!UICONTROL Type de ressource] et des champs tels que [!UICONTROL Nombre de pages] et [!UICONTROL Auteur].
1. Cliquez sur **[!UICONTROL Enregistrer]**. Appliquez le schéma de métadonnées à un dossier.

1. Accédez au dossier auquel vous avez appliqué le schéma de métadonnées et ouvrez la page des propriétés d’une ressource. Selon votre choix dans le champ Type de ressource, les champs de métadonnées en cascade pertinents s’affichent.

   ![Métadonnées en cascade pour une ressource vidéo](assets/video_asset.png)

   *Image : métadonnées en cascade pour une vidéo.*

   ![Métadonnées en cascade pour une ressource de document](assets/doc_type_fields.png)

   *Image : métadonnées en cascade pour un document.*

## Suppression de formulaires de schéma de métadonnées {#delete-metadata-schema-forms}

[!DNL Experience Manager] vous permet uniquement de supprimer des formulaires de schéma personnalisés. Il ne permet pas de supprimer les modèles/formulaires de schéma par défaut. Cependant, vous pouvez supprimer toutes les modifications personnalisées dans ces formulaires.

Pour supprimer un formulaire, sélectionnez-le puis cliquez sur Supprimer.

>[!NOTE]
>
>* Après avoir supprimé les modifications personnalisées apportées à un formulaire par défaut, le verrouillage ![lock closed](assets/do-not-localize/lock_closed_icon.svg) réapparaît devant le formulaire. Il indique que l’état par défaut du formulaire a été rétabli.
>* Vous ne pouvez pas supprimer les formulaires de schéma de métadonnées par défaut dans [!DNL Assets].


## Formulaires de schéma pour les types MIME {#schema-forms-for-mime-types}

[!DNL Experience Manager] fournit des formulaires par défaut pour plusieurs types MIME prêts à l’emploi. Vous pouvez toutefois ajouter des formulaires personnalisés pour les ressources de plusieurs types MIME.

### Ajouter des formulaires pour les types MIME {#add-new-forms-for-mime-types}

Créez un formulaire doté du type de formulaire approprié. Par exemple, pour ajouter un modèle pour le sous-type `image/png`, créez le formulaire dans les formulaires « image ». Le titre du formulaire de schéma est le nom du sous-type. Dans ce cas, le titre est `png`.

#### Utiliser un modèle de schéma existant pour divers types MIME {#use-an-existing-schema-template-for-various-mime-types}

Vous pouvez utiliser un modèle existant pour un autre type MIME. Par exemple, utilisez le formulaire `image/jpeg` pour les ressources de type MIME `image/png`.

Dans ce cas, créez un nœud sous `/etc/dam/metadataeditor/mimetypemappings` dans le référentiel CRX. Indiquez un nom pour le nœud et définissez les propriétés suivantes :

| Nom | Description | Type | Valeur |
|------|-------------|------|-------|
| `exposedmimetype` | Nom du formulaire existant à associer | `String` | `image/jpeg` |
| `mimetypes` | Liste des types MIME qui utilisent le formulaire défini dans l’attribut `exposedmimetype`. | `String` | `image/png` |

[!DNL Assets] mappe les types MIME et les formulaires de schéma suivants :

| Formulaire de schéma | Types MIME |
|---|---|
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

La fonction Schéma de métadonnées est réservée aux administrateurs. Toutefois, les administrateurs peuvent fournir l’accès aux non-administrateurs en modifiant certaines autorisations. Fournissez les autorisations de création, de modification et de suppression des utilisateurs non-administrateurs sur le dossier `/conf`.

## Application de métadonnées spécifiques au dossier {#apply-folder-specific-metadata}

[!DNL Assets] vous permet de définir une variation d’un schéma de métadonnées et de l’appliquer à un dossier spécifique.

Par exemple, vous pouvez définir une variante du schéma de métadonnées par défaut et l’appliquer à un dossier. Lorsque vous appliquez le schéma modifié, il remplace le schéma de métadonnées par défaut d’origine appliqué aux ressources du dossier.

Les métadonnées modifiées définies dans le schéma de métadonnées de la variation seront uniquement appliquées aux ressources chargées dans le dossier auquel est appliqué le schéma. Dans les autres dossiers pour lesquels le schéma d’origine est appliqué, [!DNL Assets] continue à utiliser les métadonnées définies dans le schéma d’origine.

L’héritage des métadonnées par les ressources est basé sur le schéma appliqué au dossier de premier niveau dans la hiérarchie. Le même schéma est appliqué ou hérité par les sous-dossiers. Si un autre schéma est appliqué au niveau du sous-dossier, l’héritage s’arrête.

1. Dans l’interface [!DNL Experience Manager], accédez à **[!UICONTROL Outils]** > **[!UICONTROL Ressources]** > **[!UICONTROL Schémas de métadonnées]**. La page **[!UICONTROL Formulaires de schéma de métadonnées]** s’affiche.
1. Cochez la case en regard d’un formulaire, par exemple le formulaire de métadonnées par défaut, puis cliquez sur **[!UICONTROL Copier]** et enregistrez-le en tant que formulaire personnalisé. Spécifiez un nom personnalisé pour le formulaire, par exemple `my_default`. Vous pouvez également créer un formulaire personnalisé.

1. Sur la page **[!UICONTROL Formulaires de schéma de métadonnées]**, sélectionnez le formulaire `my_default`, puis cliquez sur **[!UICONTROL Modifier]**.

1. Sur la page **[!UICONTROL Éditeur de schéma de métadonnées]**, ajoutez un champ de texte au formulaire de schéma. Par exemple, ajoutez un champ avec le libellé **[!UICONTROL Catégorie]**.

   ![Champ de texte ajouté à l’éditeur de formulaire de schéma de métadonnées](assets/text-field-metadata-schema-editor.png)

   *Image : champ de texte ajouté à l’éditeur de formulaire de schéma de métadonnées.*

1. Cliquez sur **[!UICONTROL Enregistrer]**. Le formulaire modifié figure sur la page **[!UICONTROL Formulaires de schéma de métadonnées]**.
1. Cliquez sur **[!UICONTROL Appliquer au(x) dossier(s)]** dans la barre d’outils pour appliquer les métadonnées personnalisées à un dossier.

1. Sélectionnez le dossier auquel appliquer le schéma modifié, puis cliquez sur **[!UICONTROL Appliquer]**.

   ![Sélectionner le dossier auquel appliquer le schéma de métadonnées](assets/metadata-schema-select-folder.png)

1. Si d’autres métadonnées sont appliquées au dossier, un message s’affiche pour vous avertir que vous êtes sur le point de remplacer le schéma de métadonnées existant. Cliquez sur **Remplacer**.
1. Cliquez sur **OK** pour fermer le message de confirmation.
1. Accédez au dossier auquel vous avez appliqué le schéma de métadonnées modifié.

## Définition de métadonnées obligatoires {#define-mandatory-metadata}

Vous pouvez définir des champs obligatoires au niveau d’un dossier, qui s’appliquent aux ressources chargées dans ce dossier. Si vous chargez des ressources présentant des métadonnées manquantes dans des champs obligatoires précédemment définis, une indication visuelle de métadonnées manquantes apparaît sur les ressources en mode Carte.

>[!NOTE]
>
>Un champ de métadonnées peut être défini comme obligatoire en fonction de la valeur d’un autre champ. Dans le mode Carte, [!DNL Experience Manager] n’affiche pas le message d’avertissement concernant les métadonnées manquantes pour ces champs de métadonnées obligatoires.

1. Dans l’interface [!DNL Experience Manager], accédez à **[!UICONTROL Outils]** > **[!UICONTROL Ressources]** > **[!UICONTROL Schémas de métadonnées]**. La page **[!UICONTROL Formulaires de schéma de métadonnées]** s’affiche.
1. Enregistrez le formulaire de métadonnées par défaut en tant que formulaire personnalisé. Par exemple, enregistrez-le sous le nom `my_default`.

1. Modifiez le formulaire personnalisé. Ajoutez un champ obligatoire. Par exemple, ajoutez un champ **[!UICONTROL Catégorie]** et rendez-le obligatoire.

   ![Ajoutez un champ obligatoire au formulaire de métadonnées en sélectionnant Obligatoire dans l’onglet Règles de l’éditeur de formulaire de schéma de métadonnées.](assets/mandatory-field-metadata-schema-editor.png)

   *Image : champ obligatoire dans l’éditeur de formulaire de schéma de métadonnées.*

1. Cliquez sur **[!UICONTROL Enregistrer]**. Le formulaire modifié figure sur la page **[!UICONTROL Formulaires de schéma de métadonnées]**. Sélectionnez le formulaire et cliquez sur **[!UICONTROL Appliquer au(x) dossier(s)]** dans la barre d’outils pour appliquer les métadonnées personnalisées à un dossier.

1. Accédez au dossier et chargez des ressources présentant des données manquantes pour le champ obligatoire que vous avez ajouté au formulaire personnalisé. Un message concernant les métadonnées manquantes pour le champ obligatoire apparaît dans l’affichage Carte de la ressource.

   ![Message indiquant l’absence de métadonnées obligatoires en mode Carte des ressources lors du chargement de ressources dans un dossier](assets/metadata-missing-info-card-view.png)

1. (Facultatif) Accédez à `https://[aem_server]:[port]/system/console/components/`. Configurez et activez le composant `com.day.cq.dam.core.impl.MissingMetadataNotificationJob` ; celui-ci est désactivé par défaut. Définissez la fréquence à laquelle [!DNL Experience Manager] vérifie la validité des métadonnées sur les ressources. Cette configuration ajoute une propriété `hasValidMetadata` au nœud `jcr:content` des ressources. [!DNL Experience Manager] utilise cette propriété pour filtrer les ressources non valides dans un résultat de recherche. Si vous ajoutez une ressource après une vérification, elle n’est pas marquée avec `hasValidMetadata` jusqu’à la prochaine vérification planifiée. Par conséquent, les ressources n’apparaissent pas dans les filtres de recherche pour les métadonnées non valides avant la prochaine vérification planifiée.

   >[!CAUTION]
   >
   >Les contrôles de validation des métadonnées sont des tâches qui nécessitent de nombreuses ressources et qui peuvent donc altérer les performances de votre système. Planifiez les contrôles en conséquence. Si le serveur ne peut pas gérer la charge, essayez de désactiver cette tâche.

<!-- TBD: Add this method to find invalid metadata in the metadata.md article later when it is published as a top-level metadata article.
-->
