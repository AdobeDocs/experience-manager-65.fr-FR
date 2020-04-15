---
title: Modèles de ressources
description: Découvrez les modèles d’actifs dans AEM Assets et comment utiliser les modèles d’actifs pour créer des documents marketing.
contentOwner: AG
translation-type: tm+mt
source-git-commit: c7d0bcbf39adfc7dfd01742651589efb72959603

---


# Asset templates {#asset-templates}

Les modèles de ressources sont une catégorie spéciale de ressources qui facilite la réutilisation rapide de contenu riche en visuels pour les supports numériques et imprimés. Un modèle de ressource comprend deux parties : une section de message fixe et une section modifiable.

La section fixe peut comprendre du contenu propriétaire, comme le logo d’une marque ou des informations sur les droits d’auteur, pour lequel la modification n’est pas activée. La section modifiable peut contenir du contenu visuel et textuel dans des champs qui peuvent être modifiés pour personnaliser les messages.

La flexibilité d’effectuer des modifications limitées tout en sécurisant la signalisation globale rend les modèles de ressources des blocs de création idéaux pour une adaptation et une distribution rapides du contenu en tant qu’artefacts de contenu pour diverses fonctions. Le reciblage du contenu permet de réduire les coûts de gestion des  imprimés et numériques et de proposer des expériences holistiques et cohérentes dans l’ensemble de ces  de.

En tant que spécialiste du marketing, vous pouvez stocker et gérer des modèles dans AEM Assets et utiliser un modèle de base unique pour créer facilement plusieurs expériences d’impression personnalisée. Vous pouvez créer différents types de documents marketing, par exemple, des brochures, des prospectus, des cartes postales, des cartes de visite, etc. pour transmettre de façon claire votre message marketing à vos clients. Vous pouvez également assembler des documents papier comportant plusieurs pages à partir de documents papier nouveaux ou existants. Vous pouvez surtout diffuser des expériences à la fois numériques et papier simultanément en toute simplicité et offrir ainsi aux utilisateurs une expérience intégrée cohérente.

Bien que les modèles de fichier soient principalement des fichiers Adobe InDesign, la maîtrise d’Adobe InDesign n’empêche pas la création d’artefacts stellaires. Il n’est pas nécessaire de mapper les champs de votre modèle Adobe InDesign avec les champs de vos produits que vous auriez normalement besoin de faire lors de la création de catalogues. Vous pouvez modifier les modèles en mode WYSIWYG directement dans l’interface Web. Toutefois, pour qu’Adobe InDesign puisse traiter vos modifications, vous devez d’abord configurer AEM Assets pour l’intégrer au serveur Adobe InDesign.

La possibilité de modifier des modèles Adobe InDesign à partir de l’interface Web permet d’améliorer la collaboration entre le personnel créatif et le personnel marketing, tout en réduisant le temps de mise sur le marché des initiatives de promotion locales.

Avec les modèles de ressources, vous pouvez :

* Modifier des champs de modèle modifiables depuis l’interface web
* Contrôler les paramètres de base de style du texte, par exemple, la taille, le style et le type de police au niveau des balises
* Modifier les images du modèle à l’aide du sélecteur de contenu
* Prévisualiser les modifications du modèle
* Fusionner plusieurs fichiers de modèle pour créer un document multipage

Lorsque vous choisissez un modèle pour vos documents marketing, AEM Assets crée une copie du modèle qui peut être modifiée. Le modèle original est préservé, ce qui garantit que votre signalétique reste intacte et peut être réutilisée pour renforcer la cohérence de la marque.

Vous pouvez exporter le fichier mis à jour dans le dossier parent aux formats suivants :

* INDD
* PDF
* JPG

Vous pouvez également télécharger ces différents formats sur votre système local.

## Création d’une garantie {#creating-a-collateral}

Imaginons que vous voulez créer des contenus numériques papier, comme des brochures, des prospectus ou des publicités pour une future campagne, et les envoyer à des magasins dans le monde entier. Créer de tels documents à l’aide d’un modèle vous permet de proposer la même expérience client sur tous les canaux de diffusion. Les graphistes peuvent créer des modèles pour la campagne (document d’une seule page ou de plusieurs pages) à l’aide d’une solution de création, comme InDesign et vous les envoyer sur AEM Assets. Avant de créer une garantie, vous devez télécharger à l’avance un ou plusieurs modèles INDD vers Experience Manager et les rendre disponibles.

1. Dans l’interface d’Experience Manager, cliquez sur [!UICONTROL Ressources].

1. Dans les options, choisissez **[!UICONTROL Modèles]**.

   ![chlimage_1-101](assets/chlimage_1-306.png)

1. Click **[!UICONTROL Create]**, and then choose the collateral you want to create from the menu. For example, choose **[!UICONTROL Brochure]**.

   ![chlimage_1-102](assets/chlimage_1-307.png)

1. Demandez à un ou plusieurs modèles INDD d’être chargés et disponibles dans Experience Manager à l’avance. Choose a template for your brochure, and click **[!UICONTROL Next]**.

   ![chlimage_1-103](assets/chlimage_1-308.png)

1. Entrez un nom et éventuellement une description pour la brochure.

   ![chlimage_1-104](assets/chlimage_1-309.png)

1. (Facultatif) Cliquez sur **[!UICONTROL Balises]** et sélectionnez une ou plusieurs balises pour la brochure. Click **[!UICONTROL Confirm]** to confirm your selection.

   ![chlimage_1-105](assets/chlimage_1-310.png)

1. Cliquez sur **[!UICONTROL Créer]**. Une boîte de dialogue s’ouvre pour confirmer que la nouvelle brochure a été créée. Click **[!UICONTROL Open]** to open the brochure in edit mode.

   <!--![chlimage_1-106](assets/.png) -->

   Vous pouvez aussi fermer la boîte de dialogue et accéder au dossier dans la page Modèles de départ pour afficher la brochure créée. Le type de document apparaît sur sa miniature en mode Carte. Par exemple, Brochure est ici affiché sur la miniature.

   ![chlimage_1-107](assets/chlimage_1-312.png)

## Modification d’une garantie {#editing-a-collateral}

Vous pouvez modifier un document immédiatement après sa création. Vous pouvez aussi choisir de l’ouvrir depuis la page Modèles ou la page des détails du fichier.

1. Pour ouvrir un document pour le modifier, procédez de l’une des façons suivantes :

   * Open the collateral (brochure in this case) you created in step 7 of [Create a collateral](/help/assets/asset-templates.md#creating-a-collateral).
   * From the Templates page, navigate to a folder where you created the collateral, and click the [!UICONTROL Edit] quick action on the thumbnail of a collateral.
   * In the asset page for the collateral, click **[!UICONTROL Edit]** from the toolbar.
   * Select the collateral and click **[!UICONTROL Edit]** from the toolbar.
   <!--![chlimage_1-108](assets/chlimage_1-313.png) -->

   L’outil de recherche de ressources et l’éditeur de texte sont affichés à gauche de la page. L’éditeur de texte s’ouvre par défaut.

   Vous pouvez utiliser l’éditeur de texte pour modifier le texte à afficher dans le champ de texte. Vous pouvez modifier la taille, le style, la couleur et le type de police au niveau de la balise.

   À l’aide de l’outil de recherche de ressources, vous pouvez rechercher des images dans AEM Assets et remplacer les images modifiables du modèle par d’autres que vous aurez choisies.

   ![chlimage_1-109](assets/chlimage_1-314.png)

   Les champs modifiables sont affichés à droite. Pour qu’un champ soit modifiable dans AEM Assets, le champ correspondant dans le modèle doit être « marqué » dans InDesign. En d’autres termes, ils doivent être marqués comme modifiables dans InDesign.

   ![chlimage_1-110](assets/chlimage_1-315.png)

   >[!NOTE]
   >
   >Vérifiez que votre instance AEM est intégrée avec un serveur InDesign pour qu’AEM Assets puisse extraire les données du modèle InDesign et les rendre modifiables. For details, see [Integrating AEM Assets with InDesign Server](/help/assets/indesign.md).

1. Pour modifier le texte d’un champ modifiable, cliquez sur le champ de texte dans le des champs modifiables et modifiez le texte dans le champ.

   ![chlimage_1-111](assets/chlimage_1-316.png)

   Vous pouvez modifier les propriétés de texte, par exemple la taille, la couleur ou le style de police à l’aide des options fournies.

1. Cliquez sur **** pour  les modifications apportées au texte.

   ![chlimage_1-112](assets/chlimage_1-317.png)

1. To swap an image, click the **[!UICONTROL Asset Finder]**.

   ![chlimage_1-113](assets/chlimage_1-318.png)

1. Sélectionnez le champ d’image dans la liste des champs modifiables, puis faites glisser l’image souhaitée du sélecteur de ressource vers le champ modifiable.

   ![chlimage_1-114](assets/chlimage_1-319.png)

   Vous pouvez également rechercher des images à l’aide de mots-clés, de balises ou selon leur état de publication. Vous pouvez parcourir le référentiel d’AEM Assets et accéder à l’emplacement de l’image souhaitée.

   ![chlimage_1-115](assets/chlimage_1-320.png)

1. Cliquez sur **** pour  l’image.

   ![chlimage_1-116](assets/chlimage_1-321.png)

1. Pour modifier une page spécifique d’un document collatéral de plusieurs pages, utilisez le navigateur de page situé dans la partie inférieure.

   ![chlimage_1-117](assets/chlimage_1-322.png)

1. Click **[!UICONTROL Preview]**  on the toolbar to preview all the changes. Click **[!UICONTROL Done]** to save the editing changes to the collateral.

   >[!NOTE]
   >
   >Les icônes Aperçu et Terminé sont activées uniquement lorsqu’il ne manque aucune icône aux champs d’image modifiables dans le document. Si des icônes sont manquantes dans votre document, c’est qu’AEM est incapable de résoudre les images du modèle InDesign. AEM ne peut pas résoudre les images dans les cas suivants :
   >
   >    * Les images ne sont pas incorporées dans le modèle InDesign sous-jacent.
   >    * Les images ne sont pas liées depuis le système de fichiers local.
   >
   >Pour permettre à AEM de résoudre les images, procédez de la façon suivante :
   >
   >    * Incorporez les images lorsque vous créez les modèles InDesign (reportez-vous à la section [À propos des liens et des objets graphiques incorporés](https://helpx.adobe.com/fr/indesign/using/graphics-links.html)).
   >    * Montez AEM sur votre système de fichiers local, puis mappez les icônes manquantes avec les ressources AEM existantes.
   >
   >For more information around working with InDesign documents, see [Best Practices for Working with InDesign Documents in AEM](https://helpx.adobe.com/experience-manager/kb/best-practices-idd-docs-aem.html).

1. Pour générer un rendu PDF pour la brochure, sélectionnez l’option Acrobat dans la boîte de dialogue, puis cliquez sur **[!UICONTROL Continuer]**.
1. Le document est créé dans le dossier où vous avez commencé. Pour afficher les rendus, ouvrez le document et choisissez **[!UICONTROL Rendus]** dans la liste de navigation globale.

   ![chlimage_1-118](assets/chlimage_1-323.png)

1. Cliquez sur le rendu PDF dans le  des rendus pour télécharger le fichier PDF. Ouvrez le fichier PDF pour réviser le document.

   ![chlimage_1-119](assets/chlimage_1-324.png)

## Merge collateral {#merge-collateral}

1. Dans l’interface d’Experience Manager, cliquez sur [!UICONTROL Ressources] dans la page de navigation.

1. Dans les options, choisissez **[!UICONTROL Modèles]**.

1. Click **[!UICONTROL Create]** and the choose **[!UICONTROL Merge]** from the menu.

   ![chlimage_1-120](assets/chlimage_1-325.png)

1. Dans la page Fusion [!UICONTROL de] modèles, cliquez sur **[!UICONTROL Fusion]**.

   ![chlimage_1-121](assets/chlimage_1-326.png)

1. Accédez à l&#39;emplacement du document à fusionner, puis cliquez sur les vignettes du document à fusionner pour les sélectionner.

   ![chlimage_1-122](assets/chlimage_1-327.png)

   Vous pouvez également rechercher des modèles dans la zone Omnisearch.

   ![chlimage_1-123](assets/chlimage_1-328.png)

   Vous pouvez parcourir le référentiel ou les collections d’AEM Assets, puis accéder à l’emplacement des modèles souhaités et les sélectionner pour la fusion.

   ![chlimage_1-124](assets/chlimage_1-329.png)

   Vous pouvez appliquer différents filtres pour rechercher les modèles souhaités. Par exemple, vous pouvez rechercher des modèles en fonction de leur type ou de leurs balises.

   ![chlimage_1-125](assets/chlimage_1-330.png)

1. Click **[!UICONTROL Next]** from the toolbar.
1. In the **[!UICONTROL Preview &amp; Reorder]** screen, rearrange the templates if required and preview the selection of templates to merge. Then, click **[!UICONTROL Next]** from the toolbar.

   ![chlimage_1-126](assets/chlimage_1-331.png)

1. In the [!UICONTROL Configure Template] screen, specify a name for the collateral. Vous pouvez également spécifier les balises que vous considérez appropriées. If you want to export the output in PDF format, select **[!UICONTROL Acrobat (.PDF)]**. Par défaut, le document est exporté aux formats JPG et InDesign. To change the display thumbnail for the multi-page collateral, click **[!UICONTROL Change Thumbnail]**.

   ![chlimage_1-127](assets/chlimage_1-332.png)

1. Click **[!UICONTROL Save]** and then click **[!UICONTROL OK]** in the dialog to close the dialog. La documentation multi-page est créée dans le dossier avec lequel vous avez commencé.

   >[!NOTE]
   >
   >Vous ne pouvez pas modifier ultérieurement un document fusionné ni l’utiliser pour créer d’autres documents.
