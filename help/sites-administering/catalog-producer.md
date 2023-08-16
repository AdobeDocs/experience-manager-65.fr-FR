---
title: Catalog Producer
seo-title: Catalog Producer
seo-description: Learn how to use Catalog Producer in AEM Assets to generate product catalogs using your digital assets.
uuid: da822d83-8b99-4089-ae1b-11d897d4044e
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: integration
content-type: reference
discoiquuid: 90e36522-3af1-4a8a-b044-1c828c52974e
description: Catalog Producer
exl-id: 76a46c62-d47d-4970-8a3a-d56015639548
source-git-commit: 50d29c967a675db92e077916fb4adef6d2d98a1a
workflow-type: tm+mt
source-wordcount: '881'
ht-degree: 88%

---

# Catalog Producer{#catalog-producer}

Découvrez comment utiliser Catalog Producer dans AEM Assets pour générer des catalogues de produits à l’aide de vos ressources numériques.

Grâce au Catalog Producer d’Adobe Experience Manager (AEM) Assets, vous pouvez créer des catalogues pour vos produits de marque à l’aide de modèles InDesign importés à partir d’une application InDesign. Pour importer des modèles InDesign, intégrez d’abord AEM Assets à un serveur InDesign.

## Intégration à un serveur InDesign {#integrating-with-indesign-server}

Dans le cadre du processus d’intégration, configurez le workflow **Ressource de mise à jour de la gestion des ressources numériques** qui est adapté à l’intégration à InDesign. Configurez également un programme de traitement du proxy pour le serveur InDesign. Pour plus de détails, consultez [Intégration d’AEM Assets au serveur InDesign](/help/assets/indesign.md).

>[!NOTE]
>
>Vous pouvez générer des modèles InDesign à partir de fichiers InDesign avant de les importer dans AEM Assets. Pour plus d’informations, voir [Utilisation de fichiers et de modèles](https://helpx.adobe.com/fr/indesign/using/files-templates.html).
>
>Vous pouvez associer les éléments dans vos modèles InDesign à des balises XML. Les balises mappées s’affichent sous forme de propriétés lorsque vous mappez les propriétés d’un produit aux propriétés d’un modèle dans Catalog Producer. Pour en savoir plus sur les balises XML dans les fichiers InDesign, consultez [Balisage de contenu au format XML](https://helpx.adobe.com/fr/indesign/using/tagging-content-xml.html).

>[!NOTE]
>
>Seuls des fichiers InDesign (.indd) sont utilisés comme modèles. Les fichiers avec l’extension .indt ne sont pas pris en charge.

## Créer un catalogue {#creating-a-catalog}

Catalog Producer utilise des données de gestion d’informations sur les produits pour mapper les propriétés d’un produit aux propriétés XML affichées dans le modèle. Pour créer un catalogue, procédez comme suit :

1. Dans l’interface utilisateur d’Assets, appuyez/cliquez sur le **logo AEM** et sélectionnez **Assets > Catalogues**.
1. Dans la page **Catalogues**, appuyez/cliquez sur **Créer** dans la barre d’outils, puis sélectionnez **Catalogue** dans la liste.
1. Dans la page **Créer un catalogue**, entrez un nom et une description (facultative) pour le catalogue et spécifiez les balises, le cas échéant. Vous pouvez également ajouter une miniature.

   ![create_catalog](assets/create_catalog.png)

1. Appuyez/cliquez sur **Enregistrer**. Une boîte de dialogue de confirmation vous informe que le catalogue a été créé. Appuyez/cliquez sur **Terminé** pour fermer la boîte de dialogue.
1. Pour ouvrir le catalogue que vous avez créé, appuyez/cliquez dessus dans la page **Catalogues**.

   >[!NOTE]
   >
   >Pour ouvrir le catalogue, vous pouvez également appuyer/cliquer sur **Ouvrir** dans la boîte de dialogue de confirmation mentionnée à l’étape précédente.

1. Pour ajouter des pages au catalogue, appuyez/cliquez sur **Créer** dans la barre d’outils, puis sélectionnez l’option **Nouvelle page**.
1. Dans l’assistant, sélectionnez un modèle InDesign pour votre page. Ensuite, appuyez/cliquez sur **Suivant**.
1. Spécifiez un nom pour la page et une description (facultative). Indiquez des balises, le cas échéant.
1. Appuyez/cliquez sur **Créer** dans la barre d’outils. Ensuite, appuyez/cliquez sur **Ouvrir** dans la boîte de dialogue. Les propriétés du produit sont affichées dans le volet gauche. Les propriétés prédéfinies du modèle d’InDesign s’affichent dans le volet de droite.
1. Dans le volet de gauche, faites glisser les propriétés du produit vers les propriétés du modèle d’InDesign, puis créez un mappage entre elles.

   Pour visualiser l’affichage de la page en temps réel, appuyez/cliquez sur l’onglet **Aperçu** du volet droit.

1. Pour créer d’autres pages, répétez les étapes 6 à 9. Pour créer des pages similaires pour d’autres produits, sélectionnez la page et appuyez/cliquez sur l’icône **Créer des pages similaires** de la barre d’outils.

   ![create_similar_pages](assets/create_similar_pages.png)

   >[!NOTE]
   >
   >Vous pouvez uniquement créer des pages similaires pour les produits ayant une structure similaire.

   Appuyez/cliquez sur l’icône Ajouter, sélectionnez les produits à l’aide du sélecteur de produits, puis appuyez/cliquez sur **Sélectionner** dans la barre d’outils.

   ![select_product](assets/select_product.png)

1. Dans la barre d’outils, cliquez/appuyez sur **Créer**. Appuyez/cliquez sur **Terminé** pour fermer la boîte de dialogue. Des pages similaires sont incluses dans votre catalogue.
1. Pour ajouter un fichier InDesign existant dans votre catalogue, appuyez/cliquez sur **Créer** dans la barre d’outils et sélectionnez l’option **Ajouter une page existante**.
1. Sélectionnez le fichier InDesign et appuyez/cliquez sur **Ajouter** dans la barre d’outils. Ensuite, appuyez/cliquez sur **OK** pour fermer la boîte de dialogue.

   Si les métadonnées des produits que vous référencez dans les pages du catalogue sont modifiées, les modifications ne sont pas répercutées automatiquement dans les pages du catalogue. Une bannière **Obsolète** s’affiche sur les images du produit dans toutes les pages du catalogue qui y font référence, ce qui indique que les métadonnées des produits référencés ne sont pas à jour.

   ![chlimage_1-117](assets/chlimage_1-117a.png)

   Pour vous assurer que les images du produit reflètent les dernières modifications des métadonnées, sélectionnez la page dans la console Catalogue et cliquez/appuyez sur l’icône **Mettre à jour une page** de la barre d’outils.

   ![chlimage_1-118](assets/chlimage_1-118a.png)

   >[!NOTE]
   >
   >Pour modifier les métadonnées d’un produit référencé, accédez à la console Produits (**Logo AEM** > **Commerce** > **Produits**) et sélectionnez le produit. Ensuite, cliquez/appuyez sur l’icône **Afficher les propriétés** de la barre d’outils et modifiez les métadonnées dans la page Propriétés de la ressource.

1. Pour réorganiser les pages du catalogue, appuyez/cliquez sur l’icône **Créer** de la barre d’outils, puis sélectionnez **Fusionner** dans le menu. Dans l’assistant, le carrousel situé en haut vous permet de réorganiser les pages en les faisant glisser. Vous pouvez également supprimer des pages.

1. Appuyez/cliquez sur **Suivant**. Pour ajouter un fichier InDesign existant sous forme de page de couverture, appuyez/cliquez sur **Parcourir** en regard de la zone **Choisir la page de couverture** et spécifiez le chemin d’accès au modèle de page de couverture.
1. Appuyez/cliquez sur **Enregistrer**, puis sur **Terminé** pour fermer la boîte de dialogue de confirmation.
Lorsque vous sélectionnez l’option **Terminé**, une boîte de dialogue s’ouvre pour vous demander si vous souhaitez un rendu .pdf.
   ![exportation au format pdf](assets/CatalogPDF.png)
Si l’option Acrobat(PDF) est sélectionnée, un rendu pdf est créé dans  **/jcr:content/renditions**, en plus du rendu indesign. Vous pouvez télécharger tous les rendus en cochant la case « Rendus » dans la boîte de dialogue de téléchargement.

1. Pour générer un aperçu du catalogue que vous venez de créer, sélectionnez-le dans la console **Catalogues**, puis cliquez sur l’icône **Aperçu** de la barre d’outils.

   ![chlimage_1-119](assets/chlimage_1-119a.png)

   Consultez les pages de votre catalogue dans l’aperçu. Appuyez/cliquez sur **Fermer** pour fermer l’aperçu.
