---
title: Modèles de ressources
description: En savoir plus sur les modèles de ressources dans [!DNL Adobe Experience Manager Assets] et comment utiliser des modèles de ressources pour créer des documents marketing.
contentOwner: AG
role: User
feature: Asset Management,Developer Tools
exl-id: 12c92aad-3a1d-486e-a830-31de2fc6d07b
source-git-commit: bb46b0301c61c07a8967d285ad7977514efbe7ab
workflow-type: tm+mt
source-wordcount: '1544'
ht-degree: 33%

---

# Modèles de ressources {#asset-templates}

Les modèles de ressources sont une classe spéciale de ressources qui facilite la réorientation rapide de contenu visuellement riche pour les médias numériques et imprimés. Un modèle de ressource comprend deux parties : une section de message fixe et une section modifiable. La section fixe peut comprendre du contenu propriétaire, comme le logo d’une marque ou des informations sur les droits d’auteur, pour lequel la modification n’est pas activée. La section modifiable peut contenir du contenu visuel et textuel dans des champs qui peuvent être modifiés pour personnaliser les messages.

La possibilité d’apporter des modifications limitées tout en sécurisant la signalétique globale rend les modèles de ressources des blocs de création idéaux pour une adaptation et une distribution rapides du contenu en tant qu’artefacts de contenu pour diverses fonctions. La redéfinition de l’objectif du contenu permet de réduire le coût de gestion des canaux papier et numériques et de proposer des expériences globales et cohérentes sur l’ensemble de ces canaux.

En tant que marketeur, vous pouvez stocker et gérer des modèles dans [!DNL Experience Manager Assets] et utiliser un seul modèle de base pour créer facilement plusieurs expériences d’impression personnalisées. Vous pouvez créer différents types de documents marketing, par exemple, des brochures, des prospectus, des cartes postales, des cartes de visite, etc. pour transmettre de façon claire votre message marketing à vos clients. Vous pouvez également assembler des documents papier comportant plusieurs pages à partir de documents papier nouveaux ou existants. Vous pouvez surtout diffuser des expériences à la fois numériques et papier simultanément en toute simplicité et offrir ainsi aux utilisateurs une expérience intégrée cohérente.

Tandis que les modèles de ressources [!DNL Adobe InDesign] fichiers, maîtrise en [!DNL Adobe InDesign] n’est pas un obstacle à la création d’artefacts stellaires. Vous n’avez pas besoin de mapper les champs de votre [!DNL Adobe InDesign] modèle avec vos champs de produit que vous devez normalement utiliser lors de la création de catalogues. Vous pouvez éditer les modèles en mode WYSIWYG directement depuis l&#39;interface web. Toutefois, pour [!DNL Adobe InDesign] pour traiter vos modifications, vous devez d’abord configurer [!DNL Experience Manager Assets] pour intégrer à [!DNL Adobe InDesign Server].

La possibilité de modifier [!DNL Adobe InDesign] les modèles de l’interface web favorisent une meilleure collaboration entre les créatifs et le personnel marketing. La vitesse accrue du contenu réduit le délai de mise sur le marché des collatéraux marketing.

Vous pouvez effectuer les opérations suivantes avec les modèles de ressources :

* Modifier des champs de modèle modifiables depuis l’interface web.
* Contrôler les paramètres de base de style du texte, par exemple, la taille, le style et le type de police au niveau des balises.
* Modifier les images du modèle à l’aide du sélecteur de contenu.
* Prévisualiser les modifications du modèle.
* Fusionner plusieurs fichiers de modèle pour créer un document multipage.

Lorsque vous choisissez un modèle pour votre document, [!DNL Experience Manager Assets] crée une copie du modèle que vous pouvez modifier. Le modèle original est préservé, ce qui garantit que votre signalétique reste intacte et peut être réutilisée pour renforcer la cohérence de la marque.

Vous pouvez exporter le fichier mis à jour dans le dossier parent au format INDD, PDF ou JPG. Vous pouvez également télécharger la sortie dans ces formats sur votre système de fichiers local.

## Création d’un document {#creating-a-collateral}

Imaginons que vous voulez créer des contenus numériques papier, comme des brochures, des prospectus ou des publicités pour une future campagne, et les envoyer à des magasins dans le monde entier. Créer de tels documents à l’aide d’un modèle vous permet de proposer la même expérience client sur tous les canaux de diffusion. Les concepteurs peuvent créer des modèles de campagne (une ou plusieurs pages) à l’aide d’une solution créative, telle que [!DNL InDesign] et télécharger les modèles vers [!DNL Experience Manager Assets] pour vous. Avant de créer un document, vous devez charger un ou plusieurs modèles INDD et les rendre disponibles dans [!DNL Experience Manager] à l&#39;avance.

1. Dans [!DNL Experience Manager] clic sur l’interface [!UICONTROL Ressources].

1. Dans les options, choisissez **[!UICONTROL Modèles]**.

   ![chlimage_1-101](assets/chlimage_1-306.png)

1. Cliquez sur **[!UICONTROL Créer]**, puis sélectionnez le document à créer dans le menu . Par exemple, choisissez **[!UICONTROL Brochure]**.

   ![chlimage_1-102](assets/chlimage_1-307.png)

1. Demandez au moins un modèle INDD téléchargé vers et disponible dans [!DNL Experience Manager] à l&#39;avance. Choisissez un modèle pour votre brochure, puis cliquez sur **[!UICONTROL Suivant]**.
1. Entrez un nom et éventuellement une description pour la brochure.

   ![chlimage_1-104](assets/chlimage_1-309.png)

1. (Facultatif) Cliquez sur **[!UICONTROL Balises]** et sélectionnez une ou plusieurs balises pour la brochure. Cliquez sur **[!UICONTROL Confirmer]** pour confirmer votre sélection.
1. Cliquez sur **[!UICONTROL Créer]**. Une boîte de dialogue s’ouvre pour confirmer que la nouvelle brochure a été créée. Cliquez sur **[!UICONTROL Ouvrir]** pour ouvrir la brochure en mode d’édition.

   <!--![chlimage_1-106](assets/.png) -->

   Vous pouvez aussi fermer la boîte de dialogue et accéder au dossier dans la page Modèles de départ pour afficher la brochure créée. Le type de document apparaît sur sa miniature en mode Carte. Par exemple, dans ce cas, le mot [!UICONTROL Brochure] s’affiche sur la miniature.

   ![chlimage_1-107](assets/chlimage_1-312.png)

## Modification d’un document {#editing-a-collateral}

Vous pouvez modifier un document immédiatement après sa création. Vous pouvez également l’ouvrir à partir du [!UICONTROL Modèles] ou de la page de la ressource.

1. Pour ouvrir un document pour le modifier, procédez de l’une des façons suivantes :

   * Ouvrez le document (brochure dans ce cas) que vous avez créé à l’étape 7 de la [Création d’un document](/help/assets/asset-templates.md#creating-a-collateral).
   * Sur la page Modèles , accédez au dossier dans lequel vous avez créé le document, puis cliquez sur le bouton [!UICONTROL Modifier] action rapide sur la miniature d’un document.
   * Dans la page Ressource du document, cliquez sur **[!UICONTROL Modifier]** dans la barre d’outils.
   * Sélectionnez le document et cliquez sur **[!UICONTROL Modifier]** dans la barre d’outils.

   <!--![chlimage_1-108](assets/chlimage_1-313.png) -->

   L’outil de recherche de ressources et l’éditeur de texte sont affichés à gauche de la page. L’éditeur de texte s’ouvre par défaut.

   Vous pouvez utiliser l’éditeur de texte pour modifier le texte à afficher dans le champ de texte. Vous pouvez modifier la taille, le style, la couleur et le type de police au niveau de la balise.

   À l’aide de l’outil de recherche de ressources, vous pouvez parcourir ou rechercher des images dans [!DNL Experience Manager Assets] et remplacez les images modifiables dans le modèle par les images de votre choix.

   ![chlimage_1-109](assets/chlimage_1-314.png)

   Les champs modifiables sont affichés à droite. Pour qu’un champ soit modifiable dans [!DNL Experience Manager Assets], le champ correspondant du modèle doit être balisé dans [!DNL InDesign]. En d’autres termes, ils doivent être marqués comme modifiables dans [!DNL InDesign].

   >[!NOTE]
   >
   >Assurez-vous que la variable [!DNL Experience Manager] le déploiement est intégré à un [!DNL InDesign Server] pour activer [!DNL Experience Manager Assets] pour extraire des données à partir de la fonction [!DNL InDesign] et la rendre disponible pour modification. Pour plus d’informations, voir [Intégration de Experience Manager Assets à InDesign Server](/help/assets/indesign.md).

1. Pour modifier le texte d’un champ modifiable, cliquez sur le champ de texte dans la liste des champs modifiables et modifiez le texte dans le champ.

   ![chlimage_1-111](assets/chlimage_1-316.png)

   Vous pouvez modifier les propriétés du texte, par exemple le style, la couleur et la taille de la police à l’aide des options fournies.

1. Cliquez sur **[!UICONTROL Aperçu]** pour prévisualiser les modifications de texte.

1. Pour permuter une image, cliquez sur le bouton **[!UICONTROL Outil de recherche de ressources]** ![chlimage_1-113](assets/chlimage_1-318.png).

1. Sélectionnez le champ d’image dans la liste des champs modifiables, puis faites glisser l’image souhaitée du sélecteur de ressource vers le champ modifiable.

   ![chlimage_1-114](assets/chlimage_1-319.png)

   Vous pouvez également rechercher des images à l’aide de mots-clés, de balises ou selon leur état de publication. Vous pouvez parcourir le [!DNL Experience Manager Assets] et accédez à l’emplacement de l’image souhaitée.

   ![chlimage_1-115](assets/chlimage_1-320.png)

1. Cliquez sur **[!UICONTROL Aperçu]** pour prévisualiser l’image.
1. Pour modifier une page spécifique dans un document multipage, utilisez le navigateur de page en bas de la page.

1. Cliquez sur **[!UICONTROL Aperçu]** dans la barre d’outils pour prévisualiser toutes les modifications. Cliquez sur **[!UICONTROL Terminé]** pour enregistrer les modifications apportées au document.

   >[!NOTE]
   >
   >Les options Aperçu et Terminé sont activées uniquement lorsque les champs d’image modifiables dans le document ne comportent aucune icône manquante. S’il manque des icônes dans votre document, c’est parce que [!DNL Experience Manager] ne parvient pas à résoudre les images dans la variable [!DNL InDesign] modèle. En général, [!DNL Experience Manager] ne peut pas résoudre les images dans les cas suivants :
   >
   >* Les images ne sont pas incorporées dans le sous-jacent [!DNL InDesign] modèle.
   >* Les images sont liées à partir du système de fichiers local.

   >
   >Pour activer [!DNL Experience Manager] pour résoudre des images, procédez comme suit :
   >
   >* Incorporer des images lors de la création [!DNL InDesign] modèles (Voir [A propos des liens et des graphiques incorporés](https://helpx.adobe.com/fr/indesign/using/graphics-links.html)).
   >* Mont [!DNL Experience Manager] à votre système de fichiers local, puis mappez les icônes manquantes avec les ressources existantes dans [!DNL Experience Manager].

   >
   >Pour plus d’informations sur l’utilisation de [!DNL InDesign] documents, voir [bonnes pratiques pour utiliser des documents InDesign dans Experience Manager](https://helpx.adobe.com/experience-manager/kb/best-practices-idd-docs-aem.html).

1. Pour générer un rendu PDF pour la brochure, sélectionnez l’option Acrobat dans la boîte de dialogue, puis cliquez sur **[!UICONTROL Continuer]**.
1. Le document est créé dans le dossier où vous avez commencé. Pour afficher les rendus, ouvrez le document et choisissez **[!UICONTROL Rendus]** dans la liste de navigation globale.

   ![chlimage_1-118](assets/chlimage_1-323.png)

1. Cliquez sur le rendu du PDF dans la liste des rendus pour télécharger le fichier du PDF. Ouvrez le fichier PDF pour réviser le document.

   ![chlimage_1-119](assets/chlimage_1-324.png)

## Fusion de collatéral {#merge-collateral}

1. Dans le [!DNL Experience Manager] clic sur l’interface [!UICONTROL Ressources] sur la page Navigation .

1. Dans les options, choisissez **[!UICONTROL Modèles]**.

1. Cliquez sur **[!UICONTROL Créer]** et choisissez **[!UICONTROL Fusion]** dans le menu.

   ![chlimage_1-120](assets/chlimage_1-325.png)

1. Dans la [!UICONTROL Fusion de modèles] page, cliquez sur **[!UICONTROL Fusion]** ![ajout de ressources](assets/do-not-localize/assets_add_icon.png).

1. Accédez à l’emplacement des documents que vous souhaitez fusionner, cliquez sur les miniatures des documents que vous souhaitez fusionner pour les sélectionner.

   ![chlimage_1-122](assets/chlimage_1-327.png)

   Vous pouvez également rechercher des modèles dans la zone Omni-recherche.

   Vous pouvez parcourir le [!DNL Experience Manager Assets] référentiel ou collections, puis accédez à l’emplacement des modèles souhaités et sélectionnez-les pour la fusion.

   Vous pouvez appliquer différents filtres pour rechercher les modèles souhaités. Par exemple, vous pouvez rechercher des modèles en fonction de leur type ou de leurs balises.

1. Cliquez sur **[!UICONTROL Suivant]** dans la barre d’outils.
1. Dans le **[!UICONTROL Aperçu et réorganisation]** réorganisez les modèles si nécessaire et prévisualisez la sélection des modèles à fusionner. Cliquez ensuite sur **[!UICONTROL Suivant]** dans la barre d’outils.

   ![chlimage_1-126](assets/chlimage_1-331.png)

1. Dans le [!UICONTROL Configurer le modèle] , indiquez un nom pour le document. Vous pouvez également spécifier les balises que vous considérez appropriées. Si vous souhaitez exporter la sortie au format PDF, sélectionnez **[!UICONTROL Acrobat (.PDF)]**. Par défaut, le document est exporté en JPG et [!DNL InDesign] format. Pour modifier la miniature d’affichage des documents de plusieurs pages, cliquez sur **[!UICONTROL Modifier la miniature]**.

   ![chlimage_1-127](assets/chlimage_1-332.png)

1. Cliquez sur **[!UICONTROL Enregistrer]** puis cliquez sur **[!UICONTROL OK]** dans la boîte de dialogue pour fermer la boîte de dialogue. Le document multi-page est créé dans le dossier avec lequel vous avez commencé.

   >[!NOTE]
   >
   >Vous ne pouvez pas modifier ultérieurement un document fusionné ni l’utiliser pour créer d’autres documents.

## Bonnes pratiques et restrictions {#best-practices-limitations-tips}

* Le [!DNL InDesign] dans [!DNL Experience Manager] fonctionne au niveau de la balise et tout le texte sous une seule balise est considéré comme une seule entité. Pour préserver le formatage et les styles du texte lors de la modification, marquez séparément chaque paragraphe (ou texte avec un style différent).
