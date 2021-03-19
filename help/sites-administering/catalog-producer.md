---
title: Catalog Producer
seo-title: Producteur de catalogue
seo-description: Découvrez comment utiliser le Catalog Producer dans AEM Assets pour générer des catalogues de produits à l’aide de vos ressources numériques.
uuid: da822d83-8b99-4089-ae1b-11d897d4044e
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: 90e36522-3af1-4a8a-b044-1c828c52974e
description: Producteur de catalogue
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '901'
ht-degree: 40%

---


# Catalog Producer{#catalog-producer}

Découvrez comment utiliser le Catalog Producer dans AEM Assets pour générer des catalogues de produits à l’aide de vos ressources numériques.

Grâce à Adobe Experience Manager (AEM) Assets Catalog Producer, vous pouvez créer des catalogues pour vos produits de marque à l’aide de modèles InDesign importés à partir d’une application InDesign. Pour importer des modèles d’InDesign, vous devez d’abord intégrer AEM Assets à un serveur d’InDesign.

## Intégration à un serveur InDesign {#integrating-with-indesign-server}

Dans le cadre du processus d’intégration, configurez le flux de travaux **DAM Update Asset**, qui convient à l’intégration à l’InDesign. Configurez également un programme de traitement du proxy pour le serveur InDesign. Pour plus d&#39;informations, voir [Intégration d&#39;AEM Assets à l&#39;InDesign Server](/help/assets/indesign.md).

>[!NOTE]
>
>Vous pouvez générer des modèles InDesign à partir de fichiers InDesign avant de les importer dans AEM Assets. Pour plus d’informations, voir [Utilisation de fichiers et de modèles](https://helpx.adobe.com/fr/indesign/using/files-templates.html).
>
>Vous pouvez associer les éléments dans vos modèles InDesign à des balises XML. Les balises mappées s’affichent sous forme de propriétés lorsque vous mappez les propriétés d’un produit aux propriétés d’un modèle dans Catalog Producer. Pour en savoir plus sur le balisage XML dans les fichiers d’InDesign, voir [Balisage de contenu pour XML](https://helpx.adobe.com/fr/indesign/using/tagging-content-xml.html).

>[!NOTE]
>
>Seuls des fichiers InDesign (.indd) sont utilisés comme modèles. Les fichiers possédant l’extension « .indt » ne sont pas pris en charge.

## Création d’un catalogue {#creating-a-catalog}

Catalog Producer utilise des données de gestion d’informations sur les produits pour mapper les propriétés d’un produit aux propriétés XML affichées dans le modèle. Pour créer un catalogue, procédez comme suit :

1. Dans l’interface utilisateur Ressources, appuyez/cliquez sur le **logo de l’AEM**, puis accédez à **Ressources > Catalogues**.
1. Dans la page **Catalogues**, appuyez/cliquez sur **Créer** dans la barre d’outils, puis sélectionnez **Catalogue** dans la liste.
1. Dans la page **Créer un catalogue**, saisissez un nom et une description (facultatif) pour le catalogue et spécifiez des balises, le cas échéant. Vous pouvez également ajouter une miniature.

   ![create_catalog](assets/create_catalog.png)

1. Appuyez/cliquez sur **Enregistrer**. Une boîte de dialogue de confirmation vous informe que le catalogue a été créé. Appuyez/cliquez sur **Terminé** pour fermer la boîte de dialogue.
1. Pour ouvrir le catalogue que vous avez créé, appuyez/cliquez dessus à partir de la page **Catalogues**.

   >[!NOTE]
   >
   >Pour ouvrir le catalogue, vous pouvez également appuyer/cliquer sur **Ouvrir** dans la boîte de dialogue de confirmation mentionnée à l’étape précédente.

1. Pour ajouter des pages au catalogue, appuyez/cliquez sur **Créer** dans la barre d’outils, puis sélectionnez l’option **Nouvelle page**.
1. Dans l’assistant, sélectionnez un modèle InDesign pour votre page. Ensuite, appuyez/cliquez sur **Suivant**.
1. Spécifiez un nom pour la page et une description (facultative). Spécifiez des balises, le cas échéant.
1. Appuyez/cliquez sur **Créer** dans la barre d’outils. Ensuite, appuyez/cliquez sur **Ouvrir** dans la boîte de dialogue. Les propriétés du produit sont affichées dans le volet gauche. Les propriétés prédéfinies du modèle InDesign s’affichent dans le volet droit.
1. Dans le volet gauche, faites glisser les propriétés du produit vers les propriétés du modèle InDesign, puis créez un mappage entre elles.

   Pour vue de l’affichage de la page en temps réel, appuyez/cliquez sur l’onglet **Prévisualisation** dans le volet de droite.

1. Pour créer d’autres pages, répétez les étapes 6 à 9. Pour créer des pages similaires pour d’autres produits, sélectionnez la page et appuyez/cliquez sur l’icône **Créer des pages similaires** de la barre d’outils.

   ![create_similaire_pages](assets/create_similar_pages.png)

   >[!NOTE]
   >
   >Vous ne pouvez créer des pages similaires que pour les produits ayant une structure similaire.

   Appuyez/cliquez sur l’icône Ajouter, sélectionnez les produits à l’aide du sélecteur de produits, puis appuyez/cliquez sur **Sélectionner** dans la barre d’outils.

   ![select_product](assets/select_product.png)

1. Dans la barre d’outils, cliquez/appuyez sur **Créer**. Appuyez/cliquez sur **Terminé** pour fermer la boîte de dialogue. Les pages similaires sont incluses dans votre catalogue.
1. Pour ajouter un fichier d’InDesign existant à votre catalogue, appuyez/cliquez sur **Créer** dans la barre d’outils, puis sélectionnez l’option **Ajouter à la page existante**.
1. Sélectionnez le fichier d’InDesign, puis appuyez/cliquez sur **Ajouter** dans la barre d’outils. Ensuite, appuyez/cliquez sur **OK** pour fermer la boîte de dialogue.

   Si les métadonnées des produits que vous référencez dans les pages du catalogue sont modifiées, les modifications ne sont pas automatiquement répercutées dans les pages du catalogue. Une bannière intitulée **Echelle** apparaît sur les images de produit dans les pages du catalogue de référencement, indiquant que les métadonnées des produits référencés ne sont pas à jour.

   ![chlimage_1-117](assets/chlimage_1-117a.png)

   Pour vous assurer que les images du produit reflètent les dernières modifications des métadonnées, sélectionnez la page dans la console Catalogue et cliquez/appuyez sur l’icône **Mettre à jour la page** de la barre d’outils.

   ![chlimage_1-118](assets/chlimage_1-118a.png)

   >[!NOTE]
   >
   >Pour modifier les métadonnées d’un produit référencé, accédez à la console Produits (**AEM Logo** > **Commerce** > **Produits**), puis sélectionnez le produit. Ensuite, cliquez/appuyez sur l&#39;icône **Propriétés de la Vue** de la barre d&#39;outils et modifiez les métadonnées dans la page Propriétés de la ressource.

1. Pour réorganiser les pages du catalogue, appuyez/cliquez sur l&#39;icône **Créer** de la barre d&#39;outils, puis choisissez **Fusionner** dans le menu. Dans l’assistant, le carrousel dans la partie supérieure permet de réorganiser les pages en les faisant glisser. Vous pouvez également supprimer des pages.

1. Appuyez/cliquez sur **Suivant**. Pour ajouter un fichier d&#39;InDesign existant en tant que page de garde, appuyez/cliquez sur **Parcourir** en regard de la zone **Sélectionner la page de garde** et spécifiez le chemin d&#39;accès du modèle de page de garde.
1. Appuyez/cliquez sur **Enregistrer**, puis appuyez/cliquez sur **Terminé** pour fermer la boîte de dialogue de confirmation.
Lorsque vous sélectionnez l’option **Terminé**, une boîte de dialogue s’ouvre pour indiquer si vous souhaitez obtenir un rendu .pdf.
   ![export to ](assets/CatalogPDF.png)
pdfSi l’option Acrobat(PDF) est sélectionnée, un rendu pdf est créé dans   **/jcr:content/** renditionen plus du rendu indesign. Vous pouvez télécharger tous les rendus en cochant la case &quot;Rendus&quot; dans la boîte de dialogue de téléchargement.

1. Pour générer une prévisualisation pour le catalogue que vous avez créé, sélectionnez-la dans la console **Catalogues**, puis cliquez sur l&#39;icône **Prévisualisation** de la barre d&#39;outils.

   ![chlimage_1-119](assets/chlimage_1-119a.png)

   Consultez les pages de votre catalogue dans l’aperçu. Appuyez/cliquez sur **Fermer** pour fermer l’aperçu.

