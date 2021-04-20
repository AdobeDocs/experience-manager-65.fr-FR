---
title: Gérer des ressources composées avec des références et plusieurs pages
description: Découvrez comment créer des références à des ressources numériques à partir de  [!DNL Adobe InDesign], [!DNL Adobe Illustrator], and [!DNL Adobe Photoshop]. Utilisez la fonction Visionneuse de pages pour vue des pages de sous-ressources individuelles de fichiers de plusieurs pages, tels que des fichiers PDF, INDD, PPT, PPTX et AI.
contentOwner: AG
role: Business Practitioner, Administrator
feature: Asset Management
translation-type: tm+mt
source-git-commit: ad0672c345262712e51e821fa4e050b505063ac4
workflow-type: tm+mt
source-wordcount: '1383'
ht-degree: 18%

---


# Gérer les ressources composées et multi-pages {#managing-compound-assets}

[!DNL Adobe Experience Manager Assets] peut déterminer si un fichier téléchargé contient des références à des ressources qui existent déjà dans le référentiel. Cette fonctionnalité est disponible uniquement pour les types de formats pris en charge. Si la ressource téléchargée contient des références à des ressources [!DNL Experience Manager], un lien bidirectionnel est créé entre les ressources téléchargées et référencées.

Outre l&#39;élimination de la redondance, le référencement des ressources dans les applications [!DNL Adobe Creative Cloud] améliore la collaboration et l&#39;efficacité et la productivité des utilisateurs.

[!DNL Experience Manager Assets] prend en charge le référencement bidirectionnel. Vous trouverez des ressources référencées dans la page des détails de la ressource du fichier chargé. En outre, vous pouvez vue les fichiers de référencement dans la page des détails de la ressource de la ressource référencée.

Les références sont résolues sur la base du chemin d’accès, du document et de l’ID d’instance des ressources référencées.

## [!DNL Adobe Illustrator]: Ajouter des ressources numériques en tant que références  {#refai}

Vous pouvez référencer des ressources numériques existantes dans un fichier [!DNL Adobe Illustrator].

1. A l’aide de [[!DNL Experience Manager] l’application de bureau](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html?lang=fr), récupérez les ressources numériques sur le système de fichiers local. Accédez à l&#39;emplacement du système de fichiers de la ressource à référencer.
1. Faites glisser le fichier du dossier local vers le fichier [!DNL Illustrator].

1. Enregistrez le fichier [!DNL Illustrator] sur le lecteur monté ou [téléchargez ](/help/assets/manage-assets.md#uploading-assets) dans le référentiel [!DNL Experience Manager].

1. Une fois le workflow terminé, accédez à la page des détails de la ressource. Les références aux ressources numériques existantes sont répertoriées sous **[!UICONTROL Dépendances]** dans la colonne **[!UICONTROL Références]**.

   ![chlimage_1-84](assets/chlimage_1-258.png)

1. Les ressources référencées qui apparaissent sous **[!UICONTROL Dépendances]** peuvent également être référencées par des fichiers autres que celui qui est actif. Pour afficher une liste des fichiers de référencement d’une ressource, cliquez sur son nom sous **[!UICONTROL Dépendances]**.

   ![chlimage_1-85](assets/chlimage_1-259.png)

1. Cliquez sur **[!UICONTROL Propriétés de la Vue]** dans la barre d’outils. Dans la page [!UICONTROL Propriétés], la liste des fichiers qui font référence à la ressource active apparaît sous la colonne **[!UICONTROL Références]** de l&#39;onglet **[!UICONTROL Simple]**.

   ![vue des références des ressources Experience Manager dans la colonne Références dans les détails des ressources](assets/asset-references.png)

   *Figure : Références de ressources dans les détails de la ressource.*

## [!DNL Adobe InDesign]: Ajouter des ressources numériques en tant que références  {#add-aem-assets-as-references-in-adobe-indesign}

Pour référencer des ressources numériques à partir d&#39;un fichier [!DNL InDesign], faites glisser les ressources vers le fichier [!DNL InDesign] ou exportez le fichier [!DNL InDesign] en tant qu&#39;archive ZIP.

Les actifs référencés existent déjà dans [!DNL Experience Manager Assets]. Vous pouvez extraire des sous-ressources en [configurant l’InDesign Server](indesign.md). Les ressources incorporées dans un fichier [!DNL InDesign] sont extraites en tant que sous-ressources.

>[!NOTE]
>
>Si [!DNL InDesign Server] est propagé, la prévisualisation des fichiers [!DNL InDesign] est incorporée dans leurs métadonnées XMP. Dans ce cas, l’extraction de miniature n’est pas explicitement requise. Cependant, si [!DNL InDesign Server] n’est pas un proxy, les miniatures doivent être extraites explicitement pour les fichiers [!DNL InDesign].

Lorsqu’un fichier INDD est téléchargé, les références sont récupérées en interrogeant des ressources dont les propriétés `xmpMM:InstanceID` et `xmpMM:DocumentID` se trouvent dans le référentiel.

### Création de références en faisant glisser des ressources {#create-references-by-dragging-aem-assets}

Cette procédure est similaire à l’[ajout de ressources numériques en tant que références en Adobe Illustrator](#refai).

### Création de références aux ressources en exportant un fichier ZIP {#create-references-to-aem-assets-by-exporting-a-zip-file}

1. Suivez les étapes décrites dans [Créer des modèles de processus](/help/sites-developing/workflows-models.md) pour créer un nouveau processus.
1. Utilisez la fonction [Package](https://helpx.adobe.com/indesign/how-to/indesign-package-files-for-handoff.html) de [!DNL Adobe InDesign] pour exporter le document. [!DNL Adobe InDesign] peut exporter un document et les ressources liées sous la forme d’un assemblage. Dans ce cas, le dossier exporté contient un dossier `Links` contenant des sous-ressources dans le fichier [!DNL InDesign]. Le dossier `Links` se trouve dans le même dossier que le fichier INDD.
1. Créez un fichier ZIP et téléchargez-le dans le référentiel [!DNL Experience Manager].
1. Début du flux de travaux `Unarchiver`.
1. Une fois le processus terminé, les références du dossier Links sont automatiquement référencées en tant que sous-ressources. Pour vue d&#39;une liste de ressources référencées, accédez à la page des détails de la ressource [!DNL InDesign] et fermez le [rail](/help/sites-authoring/basic-handling.md#rail-selector).

## [!DNL Adobe Photoshop]: Ajouter des ressources numériques en tant que références  {#refps}

1. Utilisez [!DNL Experience Manager] application de bureau pour accéder à [!DNL Experience Manager Assets]. Téléchargez et affichez les ressources sur le système de fichiers local. Utilisez la fonctionnalité [!UICONTROL Placer Linked] dans [!DNL Adobe Photoshop]. Voir [placement de ressources dans l’application de bureau](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html#place-assets-in-native-documents).

   ![chlimage_1-87](assets/chlimage_1-261.png)

1. Enregistrez le fichier [!DNL Photoshop] dans le lecteur monté ou [téléchargez ](/help/assets/manage-assets.md#uploading-assets) dans le référentiel [!DNL Experience Manager].
1. Une fois le processus terminé, les références aux ressources [!DNL Experience Manager] existantes sont répertoriées dans la page des détails de la ressource.

   Pour afficher les ressources référencées, fermez le [rail](/help/sites-authoring/basic-handling.md#rail-selector) dans la page des détails de la ressource.

1. Les ressources référencées contiennent également la liste des ressources à partir desquelles elles sont référencées. Pour afficher la liste des ressources référencées, accédez à la page des détails de la ressource et fermez le [rail](/help/sites-authoring/basic-handling.md#rail-selector).

>[!NOTE]
>
>Les ressources contenues dans des ressources composites peuvent également être référencées par ID de document et ID d’instance. Cette fonctionnalité est uniquement disponible avec les versions [!DNL Adobe Illustrator] et [!DNL Adobe Photoshop]. Pour d’autres, le référencement est effectué sur la base du chemin relatif des actifs liés dans l’actif composé principal, comme dans les versions antérieures de [!DNL Experience Manager].

## Créer des sous-ressources {#generate-subassets}

Pour les ressources prises en charge avec des formats de plusieurs pages — fichiers PDF, fichiers AI, [!DNL Microsoft PowerPoint] et [!DNL Apple Keynote] fichiers et [!DNL Adobe InDesign] fichiers — [!DNL Experience Manager] peut générer des sous-ressources qui correspondent à chaque page individuelle de la ressource d’origine. Ces sous-ressources sont liées à la ressource *parent* et facilitent la vue de plusieurs pages. Pour toutes les autres fins, les sous-ressources sont traitées comme des ressources normales dans [!DNL Experience Manager].

La génération de sous-ressources est désactivée par défaut. Pour activer la génération de sous-ressources, procédez comme suit :

1. Connectez-vous à [!DNL Experience Manager] en tant qu&#39;administrateur. Accédez à **[!UICONTROL Outils]** **[!UICONTROL Workflow]** > **[!UICONTROL Modèles]**.
1. Sélectionnez **[!UICONTROL Processus de mise à jour DAM]** et cliquez sur **[!UICONTROL Modifier]**.
1. Cliquez sur **[!UICONTROL Activer/désactiver le panneau latéral]** et recherchez l’étape **[!UICONTROL Créer un sous-actif]**. Ajoutez l’étape au processus. Cliquez sur **[!UICONTROL Synchroniser]**.

Pour générer les sous-ressources, effectuez l’une des opérations suivantes :

* Nouveaux actifs : Le flux de travaux de mise à jour [!UICONTROL DAM Assets] s&#39;exécute sur tout nouveau fichier téléchargé vers [!DNL Experience Manager]. Les sous-ressources sont générées automatiquement pour les nouvelles ressources de plusieurs pages.
* Ressources multi-page existantes : Exécutez manuellement le workflow [!UICONTROL DAM Update Assets] en procédant comme suit :

   * Sélectionnez une ressource et cliquez sur [!UICONTROL Chronologie] pour ouvrir le panneau de gauche. Vous pouvez également utiliser le raccourci clavier `alt + 3`. Cliquez sur [!UICONTROL Processus du Début], sélectionnez [!UICONTROL Fichier de mise à jour DAM], cliquez sur [!UICONTROL Début], puis sur [!UICONTROL Continuer].
   * Sélectionnez une ressource et cliquez sur [!UICONTROL Créer] > [!UICONTROL Workflow] dans la barre d’outils. Dans la boîte de dialogue contextuelle, sélectionnez [!UICONTROL Processus de mise à jour DAM ], cliquez sur [!UICONTROL Début], puis sur [!UICONTROL Continuer].

Plus précisément pour les documents Microsoft Word, exécutez le **[!UICONTROL Documents Word d’analyse DAM]** flux de travaux. Il génère un composant `cq:Page` à partir du contenu du document Microsoft Word. Les images extraites du document sont référencées à partir du composant `cq:Page`. Elles sont extraites même si la génération des sous-ressources est désactivée.

## Affichage des sous-ressources {#viewing-subassets}

Les sous-ressources s’affichent uniquement si elles sont générées et disponibles pour la ressource multi-page sélectionnée. Pour vue des sous-ressources générées, ouvrez la ressource de plusieurs pages. Dans la partie supérieure gauche de la page, cliquez sur ![Option pour ouvrir le rail de gauche](assets/do-not-localize/aem_leftrail_contentonly.png) et cliquez sur **[!UICONTROL Sous-ensembles]** dans la liste. Lorsque vous sélectionnez **[!UICONTROL Sous-ensembles]** dans la liste. Vous pouvez également utiliser le raccourci clavier `alt + 5`.

![Sous-ressources de vue pour une ressource de plusieurs pages](assets/view_subassets_simulation.gif)

## Affichage des pages d’un fichier multipage   {#view-pages-of-a-multi-page-file}

Vous pouvez vue un fichier de plusieurs pages, tel que PDF, INDD, PPT, PPTX et AI, à l’aide de la fonction Page Viewer de [!DNL Experience Manager Assets]. Ouvrez un fichier de plusieurs pages et cliquez sur **[!UICONTROL Pages de Vue]** dans le coin supérieur gauche de la page. La visionneuse de pages qui s’ouvre affiche les pages du fichier et les commandes permettant de parcourir et de zoomer chaque page.

![Vue et affichage des pages d’un fichier de plusieurs pages](assets/view_multipage_asset_fmr.gif)

Pour [!DNL InDesign], vous pouvez extraire des pages à l&#39;aide de [!DNL InDesign Server]. Si les prévisualisations de pages sont enregistrées pendant la création du fichier [!DNL InDesign], [!DNL InDesign Server] n&#39;est pas nécessaire pour l&#39;extraction de la page.

Les options suivantes sont disponibles dans la barre d’outils, dans le rail de gauche et dans les commandes de la visionneuse de pages :

* **[!UICONTROL Les]** actions de bureau permettent d’ouvrir ou d’afficher une sous-ressource spécifique à l’aide d’une application  [!DNL Experience Manager] de bureau. Découvrez comment [configurer les actions de bureau](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html?lang=fr#desktopactions-v2) si vous utilisez [!DNL Experience Manager] une application de bureau.

* **[!UICONTROL L’option]** Propriétés ouvre la   page Propriétés de la sous-ressource spécifique.

* **[!UICONTROL L’option]** Annotateoption vous permet d’annoter la sous-ressource spécifique. Les annotations que vous utilisez sur des sous-ressources distinctes sont collectées et affichées ensemble lorsque le fichier parent est ouvert pour affichage.

* **[!UICONTROL L’option]** Aperçu de la page affiche tous les sous-ressources simultanément.

* **** Timelineoption du rail de gauche après avoir cliqué sur  ![Option pour ouvrir le ](assets/do-not-localize/aem_leftrail_contentonly.png) rail de gauche affiche le flux d&#39;activité du fichier.

## Meilleures pratiques et limitation {#best-practice-limitation-tips}

* La génération de sous-ressources peut nécessiter beaucoup de ressources lors de tout déploiement [!DNL Experience Manager]. Si vous générez des sous-ressources lorsque des ressources complexes sont téléchargées, ajoutez l’étape suivante dans le processus de mise à jour des ressources de gestion des actifs numériques. Si vous générez des sous-ressources à la demande, créez un processus distinct pour générer des sous-ressources. Un processus dédié vous permet d’ignorer les autres étapes du processus de mise à jour des actifs de gestion des actifs numériques et d’enregistrer des ressources de calcul.

>[!MORELIKETHIS]
>
>* [Utilisation de l’appli de bureau Adobe Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html)
>* [Configuration des actions de bureau dans Adobe Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html#desktopactions-v2)
>* [Création d’objets dynamiques liés en Adobe Photoshop](https://helpx.adobe.com/photoshop/using/create-smart-objects.html#create-linked-smart-objects)
>* [Importation de graphiques en Adobe InDesign](https://helpx.adobe.com/fr/indesign/using/placing-graphics.html)

