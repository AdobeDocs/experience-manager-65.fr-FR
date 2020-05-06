---
title: Modèles de ressources dans [!DNL Adobe Experience Manager Assets].
description: Learn about Asset templates in [!DNL Adobe Experience Manager Assets] and how to use asset templates to create marketing collateral.
contentOwner: AG
translation-type: tm+mt
source-git-commit: 99ce6e0572797b7bccf755aede93623be6bd5698
workflow-type: tm+mt
source-wordcount: '1553'
ht-degree: 34%

---


# Asset templates {#asset-templates}

Les modèles de ressources sont une catégorie spéciale de ressources qui facilite la réaffectation rapide de contenu visuellement riche pour les supports numériques et imprimés. Un modèle de ressource comprend deux parties : une section de message fixe et une section modifiable. La section fixe peut comprendre du contenu propriétaire, comme le logo d’une marque ou des informations sur les droits d’auteur, pour lequel la modification n’est pas activée. La section modifiable peut contenir du contenu visuel et textuel dans des champs qui peuvent être modifiés pour personnaliser la messagerie.

La souplesse d’effectuer des modifications limitées tout en sécurisant la signalisation globale rend les modèles de ressources des blocs de construction idéaux pour une adaptation et une distribution rapides du contenu en tant qu’artefacts de contenu pour diverses fonctions. La redéfinition du contenu permet de réduire les coûts de gestion des canaux imprimés et numériques et de proposer des expériences holistiques et cohérentes sur l’ensemble de ces canaux.

As a marketer, you can store and manage templates within [!DNL Experience Manager Assets] and use a single base template to create multiple personalized print experiences with ease. Vous pouvez créer différents types de documents marketing, par exemple, des brochures, des prospectus, des cartes postales, des cartes de visite, etc. pour transmettre de façon claire votre message marketing à vos clients. Vous pouvez également assembler des documents papier comportant plusieurs pages à partir de documents papier nouveaux ou existants. Vous pouvez surtout diffuser des expériences à la fois numériques et papier simultanément en toute simplicité et offrir ainsi aux utilisateurs une expérience intégrée cohérente.

While asset templates are mostly [!DNL Adobe InDesign] files, proficiency in [!DNL Adobe InDesign] is not a barrier to creating stellar artifacts. You need not map the fields of your [!DNL Adobe InDesign] template with your product fields that you otherwise require to when creating catalogs. Vous pouvez modifier les modèles en mode WYSIWYG directement sur l’interface Web. However, for [!DNL Adobe InDesign] to process your editing changes, you must first configure [!DNL Experience Manager Assets] to integrate with [!DNL Adobe InDesign Server].

La possibilité de modifier [!DNL Adobe InDesign] des modèles à partir de l’interface Web favorise une plus grande collaboration entre le personnel créatif et le personnel marketing. La vitesse accrue du contenu réduit le délai de mise sur le marché des garanties marketing.

Les modèles de ressources permettent d’effectuer les opérations suivantes :

* Modifier des champs de modèle modifiables depuis l’interface web.
* Contrôler les paramètres de base de style du texte, par exemple, la taille, le style et le type de police au niveau des balises.
* Modifier les images du modèle à l’aide du sélecteur de contenu.
* Prévisualiser les modifications du modèle.
* Fusionner plusieurs fichiers de modèle pour créer un document multipage.

When you choose a template for your collateral, [!DNL Experience Manager Assets] creates a copy of the template that you can edit. Le modèle original est préservé, ce qui garantit que votre signalétique reste intacte et peut être réutilisée pour renforcer la cohérence de la marque.

Vous pouvez exporter le fichier mis à jour dans le dossier parent aux formats INDD, PDF ou JPG. Vous pouvez également télécharger la sortie dans ces formats vers votre système de fichiers local.

## Créer une garantie {#creating-a-collateral}

Imaginons que vous voulez créer des contenus numériques papier, comme des brochures, des prospectus ou des publicités pour une future campagne, et les envoyer à des magasins dans le monde entier. Créer de tels documents à l’aide d’un modèle vous permet de proposer la même expérience client sur tous les canaux de diffusion. Designers can create the campaign templates (single-page or multi-page) using a creative solution, such as [!DNL InDesign] and upload the templates to [!DNL Experience Manager Assets] for you. Avant de créer une garantie, demandez qu’un ou plusieurs modèles INDD soient chargés et disponibles [!DNL Experience Manager] à l’avance.

1. Dans [!DNL Experience Manager] l’interface, cliquez sur [!UICONTROL Ressources].

1. Dans les options, choisissez **[!UICONTROL Modèles]**.

   ![chlimage_1-101](assets/chlimage_1-306.png)

1. Click **[!UICONTROL Create]**, and then choose the collateral you want to create from the menu. For example, choose **[!UICONTROL Brochure]**.

   ![chlimage_1-102](assets/chlimage_1-307.png)

1. Demander qu’un ou plusieurs modèles INDD soient chargés et disponibles [!DNL Experience Manager] à l’avance. Choose a template for your brochure, and click **[!UICONTROL Next]**.

   ![chlimage_1-103](assets/chlimage_1-308.png)

1. Entrez un nom et éventuellement une description pour la brochure.

   ![chlimage_1-104](assets/chlimage_1-309.png)

1. (Facultatif) Cliquez sur **[!UICONTROL Balises]** et sélectionnez une ou plusieurs balises pour la brochure. Click **[!UICONTROL Confirm]** to confirm your selection.

   ![chlimage_1-105](assets/chlimage_1-310.png)

1. Cliquez sur **[!UICONTROL Créer]**. Une boîte de dialogue s’ouvre pour confirmer que la nouvelle brochure a été créée. Click **[!UICONTROL Open]** to open the brochure in edit mode.

   <!--![chlimage_1-106](assets/.png) -->

   Vous pouvez aussi fermer la boîte de dialogue et accéder au dossier dans la page Modèles de départ pour afficher la brochure créée. Le type de document apparaît sur sa miniature en mode Carte. For example, in this case, the word [!UICONTROL Brochure] is displayed on the thumbnail.

   ![chlimage_1-107](assets/chlimage_1-312.png)

## Modification d’une garantie {#editing-a-collateral}

Vous pouvez modifier un document immédiatement après sa création. Alternatively, you open it from the [!UICONTROL Templates] page or the asset page.

1. Pour ouvrir un document pour le modifier, procédez de l’une des façons suivantes :

   * Open the collateral (brochure in this case) you created in step 7 of [Create a collateral](/help/assets/asset-templates.md#creating-a-collateral).
   * From the Templates page, navigate to a folder where you created the collateral, and click the [!UICONTROL Edit] quick action on the thumbnail of a collateral.
   * In the asset page for the collateral, click **[!UICONTROL Edit]** from the toolbar.
   * Select the collateral and click **[!UICONTROL Edit]** from the toolbar.
   <!--![chlimage_1-108](assets/chlimage_1-313.png) -->

   L’outil de recherche de ressources et l’éditeur de texte sont affichés à gauche de la page. L’éditeur de texte s’ouvre par défaut.

   Vous pouvez utiliser l’éditeur de texte pour modifier le texte à afficher dans le champ de texte. Vous pouvez modifier la taille, le style, la couleur et le type de police au niveau de la balise.

   Using the asset finder, you can browse or search for images within [!DNL Experience Manager Assets] and replace the editable images in the template with images of your choice.

   ![chlimage_1-109](assets/chlimage_1-314.png)

   Les champs modifiables sont affichés à droite. For a field to be editable in [!DNL Experience Manager Assets], corresponding field in the template must be tagged in [!DNL InDesign]. In other words, they should be marked as editable in [!DNL InDesign].

   ![chlimage_1-110](assets/chlimage_1-315.png)

   >[!NOTE]
   >
   >Ensure that your [!DNL Experience Manager] instance is integrated with an [!DNL InDesign Server] to enable [!DNL Experience Manager Assets] to extract data from the [!DNL InDesign] template and make it available for editing. Pour plus d’informations, reportez-vous à la page [Intégration de ressources Experience Manager avec InDesign Server](/help/assets/indesign.md).

1. Pour modifier le texte d’un champ modifiable, cliquez sur le champ de texte à partir de la liste des champs modifiables et modifiez le texte du champ.

   ![chlimage_1-111](assets/chlimage_1-316.png)

   Vous pouvez modifier les propriétés de texte, par exemple le style, la couleur et la taille de la police, à l’aide des options fournies.

1. Cliquez sur **[!UICONTROL Prévisualisation]** pour prévisualisation des modifications de texte.

   ![chlimage_1-112](assets/chlimage_1-317.png)

1. To swap an image, click the **[!UICONTROL Asset Finder]**.

   ![chlimage_1-113](assets/chlimage_1-318.png)

1. Sélectionnez le champ d’image dans la liste des champs modifiables, puis faites glisser l’image souhaitée du sélecteur de ressource vers le champ modifiable.

   ![chlimage_1-114](assets/chlimage_1-319.png)

   Vous pouvez également rechercher des images à l’aide de mots-clés, de balises ou selon leur état de publication. You can browse through the [!DNL Experience Manager Assets] repository and navigate to the location of the desired image.

   ![chlimage_1-115](assets/chlimage_1-320.png)

1. Cliquez sur **[!UICONTROL Prévisualisation]** pour prévisualisation de l’image.

   ![chlimage_1-116](assets/chlimage_1-321.png)

1. Pour modifier une page spécifique dans une documentation multipage, utilisez le navigateur de page situé en bas.

   ![chlimage_1-117](assets/chlimage_1-322.png)

1. Click **[!UICONTROL Preview]**  on the toolbar to preview all the changes. Click **[!UICONTROL Done]** to save the editing changes to the collateral.

   >[!NOTE]
   >
   >Les icônes Aperçu et Terminé sont activées uniquement lorsqu’il ne manque aucune icône aux champs d’image modifiables dans le document. If there are missing icons in your collateral, it is because [!DNL Experience Manager] is unable to resolve the images in the [!DNL InDesign] template. Usually, [!DNL Experience Manager] is unable to resolve images in the following cases:
   >
   >    * Images are not embedded in the underlying [!DNL InDesign] template.
   >    * Les images sont liées à partir du système de fichiers local.
   >
   >To enable [!DNL Experience Manager] to resolve images, do the following:
   >
   >    * Embed images while creating [!DNL InDesign] templates (See [About links and embedded graphics](https://helpx.adobe.com/fr/indesign/using/graphics-links.html)).
   >    * Mount [!DNL Experience Manager] to your local file system, and then map missing icons with existing assets in [!DNL Experience Manager].
   >
   >For more information around working with [!DNL InDesign] documents, see [Best Practices for Working with InDesign Documents in Experience Manager](https://helpx.adobe.com/experience-manager/kb/best-practices-idd-docs-aem.html).

1. Pour générer un rendu PDF pour la brochure, sélectionnez l’option Acrobat dans la boîte de dialogue, puis cliquez sur **[!UICONTROL Continuer]**.
1. Le document est créé dans le dossier où vous avez commencé. Pour afficher les rendus, ouvrez le document et choisissez **[!UICONTROL Rendus]** dans la liste de navigation globale.

   ![chlimage_1-118](assets/chlimage_1-323.png)

1. Cliquez sur le rendu PDF dans la liste des rendus pour télécharger le fichier PDF. Ouvrez le fichier PDF pour réviser le document.

   ![chlimage_1-119](assets/chlimage_1-324.png)

## Merge collateral {#merge-collateral}

1. Dans l’ [!DNL Experience Manager] interface, cliquez sur [!UICONTROL Ressources] sur la page de navigation.

1. Dans les options, choisissez **[!UICONTROL Modèles]**.

1. Click **[!UICONTROL Create]** and the choose **[!UICONTROL Merge]** from the menu.

   ![chlimage_1-120](assets/chlimage_1-325.png)

1. Dans la page Fusion [!UICONTROL de] modèles, cliquez sur **[!UICONTROL Fusion]**.

   ![chlimage_1-121](assets/chlimage_1-326.png)

1. Accédez à l&#39;emplacement de la garantie que vous souhaitez fusionner, cliquez sur les miniatures de la sûreté à fusionner pour les sélectionner.

   ![chlimage_1-122](assets/chlimage_1-327.png)

   Vous pouvez également rechercher des modèles dans la zone Omnisearch.

   ![chlimage_1-123](assets/chlimage_1-328.png)

   You can browse through the [!DNL Experience Manager Assets] repository or collections, and navigate to the location of the desired templates and then select them to merge.

   ![chlimage_1-124](assets/chlimage_1-329.png)

   Vous pouvez appliquer différents filtres pour rechercher les modèles souhaités. Par exemple, vous pouvez rechercher des modèles en fonction de leur type ou de leurs balises.

   ![chlimage_1-125](assets/chlimage_1-330.png)

1. Click **[!UICONTROL Next]** from the toolbar.
1. In the **[!UICONTROL Preview &amp; Reorder]** screen, rearrange the templates if required and preview the selection of templates to merge. Then, click **[!UICONTROL Next]** from the toolbar.

   ![chlimage_1-126](assets/chlimage_1-331.png)

1. In the [!UICONTROL Configure Template] screen, specify a name for the collateral. Vous pouvez également spécifier les balises que vous considérez appropriées. If you want to export the output in PDF format, select **[!UICONTROL Acrobat (.PDF)]**. By default, the collateral is exported in JPG and [!DNL InDesign] format. To change the display thumbnail for the multi-page collateral, click **[!UICONTROL Change Thumbnail]**.

   ![chlimage_1-127](assets/chlimage_1-332.png)

1. Click **[!UICONTROL Save]** and then click **[!UICONTROL OK]** in the dialog to close the dialog. La documentation multipage est créée dans le dossier que vous avez créé.

   >[!NOTE]
   >
   >Vous ne pouvez pas modifier ultérieurement un document fusionné ni l’utiliser pour créer d’autres documents.

## Best practices and limitations {#best-practices-limitations-tips}

* L’ [!DNL InDesign] éditeur dans [!DNL Experience Manager] fonctionne au niveau de la balise et tout le texte sous une balise unique est considéré comme une entité unique. Pour conserver la mise en forme et les styles du texte lors de la modification, balisez séparément chaque paragraphe (ou le texte avec des styles différents).