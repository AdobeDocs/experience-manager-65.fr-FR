---
title: Métadonnées en cascade dans [!DNL Adobe Experience Manager Assets].
description: Cet article décrit comment définir des métadonnées en cascade pour des ressources.
contentOwner: AG
translation-type: tm+mt
source-git-commit: c92215a6cb1f4c3d02e9a5f5b3fd36c65fc002ce
workflow-type: tm+mt
source-wordcount: '948'
ht-degree: 82%

---


# Métadonnées en cascade {#cascading-metadata}

Lors de la capture des informations de métadonnées d’une ressource, les utilisateurs fournissent des informations dans les différents champs disponibles. Vous pouvez afficher des valeurs de champ ou des champs de métadonnées spécifiques en fonction des options sélectionnées dans les autres champs. Ce type d’affichage conditionnel des métadonnées est désigné sous le nom de métadonnées en cascade. En d’autres termes, vous pouvez créer une dépendance entre un champ/une valeur de métadonnées en particulier, ainsi qu’entre un ou plusieurs champs et/ou leurs valeurs.

Utilisez des schémas de métadonnées afin de définir des règles pour afficher les métadonnées en cascade. Par exemple, si votre schéma de métadonnées comprend un champ de type de ressource, vous pouvez définir un ensemble de champs pertinent à afficher en fonction du type de ressource qu’un utilisateur sélectionne.

>[!CAUTION]
>
>Les métadonnées en cascade ne sont pas prises en charge pour les fragments de contenu.

Voici quelques cas d’utilisation pour lesquels vous pouvez définir des métadonnées en cascade :

* Lorsque l’emplacement de l’utilisateur est requis, afficher les noms de ville pertinents en fonction du choix de pays et d’état de l’utilisateur.
* Charger les noms de marques pertinents dans une liste en fonction du choix de catégorie de produits de l’utilisateur.
* Activer/désactiver la visibilité d’un champ spécifique en fonction de la valeur spécifiée dans un autre champ. Par exemple, afficher des champs d’adresse d’expédition distincts si l’utilisateur souhaite la livraison à une autre adresse.
* Désigner un champ comme obligatoire en fonction de la valeur spécifiée dans un autre champ.
* Modifier les options affichées pour un champ particulier en fonction de la valeur spécifiée dans un autre champ.
* Définir la valeur de métadonnées par défaut dans un domaine spécifique en fonction de la valeur spécifiée dans un autre champ.

## Configure cascading metadata in [!DNL Experience Manager] {#configure-cascading-metadata-in-aem}

Supposons que vous souhaitiez afficher les métadonnées en cascade en fonction du type de ressource sélectionné. Quelques exemples

* Pour une vidéo, affichez les champs applicables tels que le format, le codec, la durée, etc.
* Pour un document Word ou PDF, affichez des champs tels que le nombre de pages, l’auteur, etc.

Sans tenir compte du type de ressource choisi, affichez les informations de copyright comme étant un champ requis.

1. Dans [!DNL Experience Manager] l’interface, accédez à **[!UICONTROL Outils]** > **[!UICONTROL Ressources]** > Schémas **** de métadonnées.
1. In the **[!UICONTROL Schema Forms]** page, select a schema form and then click **[!UICONTROL Edit]** from the toolbar to edit the schema.

   ![select_form](assets/select_form.png)

1. (Facultatif) Dans l’éditeur de schéma de métadonnées, créez un champ pour l’application de conditions. Spécifiez un nom et un chemin de propriété sous l’onglet **[!UICONTROL Paramètres.]**

   To create a new tab, click `+` to add a tab and then add a metadata field.

   ![add_tab](assets/add_tab.png)

1. Ajoutez un champ de liste déroulante pour le type de ressource. Spécifiez un nom et un chemin de propriété sous l’onglet **[!UICONTROL Paramètres]**. Ajoutez une description facultative.

   ![asset_type_field](assets/asset_type_field.png)

1. Les paires de clé/valeur sont les options fournies à un utilisateur de formulaire. Vous pouvez fournir des paires clé/valeur manuellement ou à partir d’un fichier JSON.

   * To specify the values manually, select **[!UICONTROL Add Manually]**, and click **[!UICONTROL Add Choice]** and specify the option text and value. Par exemple, spécifiez les types de ressources vidéo, PDF, Word et image.

   * Pour récupérer les valeurs d’un fichier JSON de façon dynamique, sélectionnez **[!UICONTROL Ajouter par chemin JSON]** et indiquez le chemin d’accès au fichier JSON. [!DNL Experience Manager] récupère les paires clé/valeur en temps réel lorsque le formulaire est présenté à l’utilisateur.

   Les deux options s’excluent mutuellement. Vous ne pouvez pas importer les options d’un fichier JSON et les modifier manuellement.

   ![add_choice](assets/add_choice.png)

   >[!NOTE]
   >
   >Lorsque vous ajoutez un fichier JSON, les paires clé/valeur ne sont pas affichées dans l’éditeur de schéma de métadonnées, mais sont disponibles dans le formulaire publié.

   >[!NOTE]
   >
   >Lors de l’ajout de choix, si vous cliquez sur le champ Liste déroulante, l’interface est déformée et l’option de suppression des choix ne fonctionne plus. Ne cliquez pas sur la liste déroulante tant que vous n’avez pas enregistré les modifications. Si vous rencontrez ce problème, enregistrez le schéma et rouvrez-le pour poursuivre l’édition.

1. (Facultatif) Ajoutez les autres champs requis ; par exemple, le format, le codec et la durée de la ressource de type vidéo.

   De la même façon, ajoutez des champs dépendants pour les autres types de ressources. Par exemple, ajoutez des champs Nombre de pages et Auteur pour les ressources de documents, tels que des fichiers PDF et Word.

   ![video_dependent_fields](assets/video_dependent_fields.png)

1. Pour créer une dépendance entre le champ de type de ressource et d’autres champs, sélectionnez le champ dépendant et ouvrez l’onglet **[!UICONTROL Règles]**.

   ![select_dependentfield](assets/select_dependentfield.png)

1. Sous **[!UICONTROL Condition requise]**, sélectionnez l’option **[!UICONTROL Requis, d’après la nouvelle règle]**.
1. Click **[!UICONTROL Add Rule]** and choose the **[!UICONTROL Asset Type]** field to create a dependency. Sélectionnez également la valeur du champ sur lequel vous souhaitez créer la dépendance. Dans ce cas, sélectionnez **[!UICONTROL Vidéo]**. Click **[!UICONTROL Done]** to save the changes.

   ![define_rule](assets/define_rule.png)

   >[!NOTE]
   >
   >Le menu déroulant contenant des valeurs prédéfinies manuellement peut être utilisé avec des règles. Les menus déroulants avec le chemin d’accès JSON configuré ne peuvent pas être utilisés avec des règles qui utilisent des valeurs prédéfinies pour appliquer des conditions. Si les valeurs sont chargées à partir de JSON au moment de l’exécution, il n’est pas possible d’appliquer une règle prédéfinie.

1. Sous **[!UICONTROL Visibilité]**, sélectionnez l’option **[!UICONTROL Visible, d’après la nouvelle règle]**.

1. Click **[!UICONTROL Add Rule]** and choose the **[!UICONTROL Asset Type]** field to create a dependency. Sélectionnez également la valeur du champ sur lequel vous souhaitez créer la dépendance. Dans ce cas, sélectionnez **[!UICONTROL Vidéo]**. Click **[!UICONTROL Done]** to save the changes.

   ![define_visibilityrule](assets/define_visibilityrule.png)

   >[!NOTE]
   >
   >Le fait de cliquer sur un espace (ou tout autre emplacement que les valeurs) réinitialise les valeurs. Si cela se produit, sélectionnez à nouveau les valeurs.

   >[!NOTE]
   >
   >Vous pouvez appliquer les conditions **[!UICONTROL Condition requise]** et **[!UICONTROL Visibilité]** indépendamment l’une de l’autre.

1. De la même façon, créez une dépendance entre la valeur Vidéo dans le champ Type de ressource et d’autres champs, tels que Codec et Durée.
1. Répétez les étapes pour créer une dépendance entre les ressources de documents (PDF, Word) dans le champ [!UICONTROL Type de ressource] et des champs tels que [!UICONTROL Nombre de pages] et [!UICONTROL Auteur].
1. Cliquez sur **[!UICONTROL Enregistrer]**. Appliquez le schéma de métadonnées à un dossier.

1. Accédez au dossier auquel vous avez appliqué le schéma de métadonnées et ouvrez la page des propriétés d’une ressource. En fonction de votre choix dans le champ Type de ressource, les champs de métadonnées en cascade pertinents sont affichés.

   ![Métadonnées en cascade pour une ressource vidéo](assets/video_asset.png)

   *Figure : Métadonnées en cascade pour une vidéo.*

   ![Métadonnées en cascade pour une ressource de document](assets/doc_type_fields.png)

   *Figure : Métadonnées en cascade pour un document.*
