---
title: Gestion des ressources composées avec des références et des ressources multi-pages dans Experience Manager
description: Découvrez comment créer des références à des ressources AEM depuis InDesign, Illustrator et Photoshop. Utilisez la fonctionnalité Visionneuse de pages pour afficher les pages de sous-ressources individuelles de fichiers de plusieurs pages, tels que des fichiers PDF, INDD, PPT, PPTX et AI.
contentOwner: AG
translation-type: tm+mt
source-git-commit: b13fe70c4b67b27e0f18bdb557c52e25d21e7f75

---


# Gestion des ressources composées et multi-pages {#managing-compound-assets}

Le composant Adobe Experience Manager (AEM) Assets peut déterminer si un fichier chargé contient des références à des ressources existant déjà dans le référentiel. Cette fonctionnalité est disponible uniquement pour les types de format pris en charge. Si le fichier chargé contient des références à des actifs AEM, un lien bidirectionnel est créé entre les ressources chargées et celles référencées.

En plus de supprimer toute redondance, le référencement des ressources AEM dans les applications Adobe Creative Cloud améliore la collaboration et accroît l’efficacité et la productivité des utilisateurs.

AEM Assets prend en charge le référencement bidirectionnel. Vous trouverez des ressources référencées dans la page des détails de la ressource du fichier chargé. Vous pouvez, en outre, afficher les fichiers de référencement des ressources AEM dans la page des détails de la ressource référencée.

Les références sont résolues sur la base du chemin d’accès, du document et de l’ID d’instance des ressources référencées.

## Ajout de ressources AEM Assets en tant que références dans Adobe Illustrator {#refai}

Vous pouvez référencer des ressources AEM existantes dans un fichier Adobe Illustrator.

1. Using [AEM desktop app](https://docs.adobe.com/content/help/en/experience-manager-desktop-app/using/using.html), mount AEM Assets repository as a drive on your local machine. Dans le lecteur monté, accédez à l’emplacement de la ressource à référencer.
1. Faites glisser la ressource du volume monté jusqu’au fichier Illustrator.
1. Save the Illustrator file to the mounted drive, or [upload](/help/assets/managing-assets-touch-ui.md#uploading-assets) to the AEM repository.
1. Une fois le processus terminé, accédez à la page des détails de la ressource. Les références à des ressources AEM existantes sont répertoriées sous **[!UICONTROL Dépendances]** dans la colonne **[!UICONTROL Références]**.

   ![chlimage_1-84](assets/chlimage_1-258.png)

1. The referenced assets that appear under **[!UICONTROL Dependencies]** can also be referenced by files other than the current one. Pour afficher une liste des fichiers de référencement d’une ressource, cliquez sur son nom sous **[!UICONTROL Dépendances]**.

   ![chlimage_1-85](assets/chlimage_1-259.png)

1. Click **[!UICONTROL View Properties]** from the toolbar. In the [!UICONTROL Properties] page, the list of files that reference the current asset appear under the **[!UICONTROL References]** column in the **[!UICONTROL Basic]** tab.

   ![chlimage_1-86](assets/chlimage_1-260.png)

## Ajout de ressources AEM Assets en tant que références dans Adobe InDesign {#add-aem-assets-as-references-in-adobe-indesign}

Pour référencer des fichiers AEM depuis un fichier InDesign, faites glisser les fichiers AEM vers le fichier InDesign ou exportez le fichier InDesign sous forme de fichier ZIP.

Les ressources référencées existent déjà dans AEM Assets. Vous pouvez extraire des sous-ressources lors de la [configuration du serveur InDesign](/help/assets/indesign.md). Les ressources intégrées à un fichier InDesign sont extraites sous la forme de sous-ressources.

>[!NOTE]
>
>Si le serveur InDesign est soumis à un proxy, l’aperçu des fichiers InDesign est intégré à leurs métadonnées XMP. Dans ce cas, l’extraction de miniature n’est pas explicitement requise. Toutefois, si le serveur InDesign n’est pas soumis à un proxy, les miniatures doivent être explicitement extraites pour les fichiers InDesign.

### Create references by dragging assets {#create-references-by-dragging-aem-assets}

This procedure is similar to [Add AEM assets as references in Adobe Illustrator](#refai).

### Création de références aux ressources en exportant un fichier ZIP {#create-references-to-aem-assets-by-exporting-a-zip-file}

1. Perform the steps in [Create workflow models](/help/sites-developing/workflows-models.md) to create a new workflow.
1. Utilisez l’option Assemblage d’Adobe InDesign pour exporter le document.
Adobe InDesign peut exporter un document et les ressources liées sous la forme d’un assemblage. Dans ce cas, le dossier exporté contient un dossier Liens dans lequel se trouvent des sous-ressources dans le fichier InDesign.
1. Créez un fichier ZIP et transférez-le dans le référentiel AEM.
1. Start the `Unarchiver` workflow.
1. When the workflow completes, the references in the Links folder are automatically referenced as subassets. To view a list of referred assets, navigate to the asset details page of the InDesign asset and close the [Rail](/help/sites-authoring/basic-handling.md#rail-selector).

## Ajout de ressources AEM Assets en tant que références dans Adobe Photoshop {#refps}

1. À l’aide d’un client WebDAV, montez AEM Assets comme lecteur.
1. Pour créer des références à des ressources AEM dans un fichier Photoshop, accédez aux ressources correspondantes sur le volume monté à l’aide de l’option Importer et lier dans Photoshop.

   ![chlimage_1-87](assets/chlimage_1-261.png)

1. Save in Photoshop file to the mounted drive or or [upload](/help/assets/managing-assets-touch-ui.md#uploading-assets) to the AEM repository.
1. Une fois le processus terminé, les références aux ressources AEM existantes sont répertoriées dans la page des détails de la ressource.

   To view the referenced assets, close the [Rail](/help/sites-authoring/basic-handling.md#rail-selector) in the asset details page.

1. The referenced assets also contain the list of assets they are referenced from. To view a list of referenced assets, navigate to the asset details page and close the [Rail](/help/sites-authoring/basic-handling.md#rail-selector).

>[!NOTE]
>
>Les ressources des ressources composées peuvent également être référencées en fonction de leur ID de document et de leur ID d’instance. Cette fonctionnalité est disponible avec les versions d’Adobe Illustrator et d’Adobe Photoshop uniquement. Pour les autres, le référencement s’effectue sur la base du chemin d’accès relatif des ressources liées dans la ressource composite principale, comme dans les versions précédentes d’AEM.

## Création de sous-ressources {#generate-subassets}

Pour les ressources prises en charge avec des formats de plusieurs pages — fichiers PDF, AI, Microsoft PowerPoint et Apple Keynote et Adobe InDesign — AEM peut générer des sous-ressources qui correspondent à chaque page individuelle de la ressource d’origine. Ces sous-ressources sont liées à la ressource *parente* et facilitent l’affichage de plusieurs pages. Pour toutes les autres raisons, les sous-ressources sont traitées comme des ressources normales dans AEM.

La génération de sous-ressources est désactivée par défaut. Pour activer la génération de sous-ressources, procédez comme suit :

1. Connectez-vous à Experience Manager en tant qu’administrateur. Access **[!UICONTROL Tools > Workflow > Models]**.
1. Sélectionnez **[!UICONTROL DAM Update Asset]** workflow et cliquez sur **[!UICONTROL Modifier]**.
1. Cliquez sur **[!UICONTROL Activer/désactiver le panneau]** latéral et recherchez l’étape **[!UICONTROL Créer un sous-fichier]** . Ajoutez l’étape au processus. Cliquez sur **[!UICONTROL Synchroniser]**.

Pour générer les sous-ressources, procédez de l’une des manières suivantes :

* Nouveaux actifs : Le flux de travaux [!UICONTROL DAM Update Assets] s’exécute sur toute nouvelle ressource téléchargée vers AEM. Les sous-ensembles sont générés automatiquement pour les nouveaux actifs de plusieurs pages.
* Ressources multi-page existantes : Exécutez manuellement le flux de travaux [!UICONTROL DAM Update Assets] en procédant comme suit :

   * Sélectionnez un fichier et cliquez sur [!UICONTROL Chronologie] pour ouvrir le panneau de gauche. Vous pouvez également utiliser le raccourci clavier `alt + 3`. Cliquez sur [!UICONTROL Démarrer le processus], sélectionnez [!UICONTROL DAM Update Asset], cliquez sur [!UICONTROL Démarrer], puis sur [!UICONTROL Continuer.]
   * Sélectionnez un fichier et cliquez sur [!UICONTROL Créer > Processus] dans la barre d’outils. Dans la boîte de dialogue contextuelle, sélectionnez [!UICONTROL Processus de mise à jour des ressources] DAM, cliquez sur [!UICONTROL Démarrer], puis sur [!UICONTROL Continuer].

Plus précisément pour les documents Microsoft Word, exécutez le flux de travail **[!UICONTROL DAM Parse Word Documents]** . Il génère un `cq:Page` composant à partir du contenu du document Microsoft Word. The images extracted from the document are referenced from the `cq:Page` component. Elles sont extraites même si la génération des sous-ressources est désactivée.

## View subassets {#viewing-subassets}

Les sous-ressources s’affichent uniquement si elles sont générées et disponibles pour la ressource multi-page sélectionnée. Pour afficher les sous-ressources générées, ouvrez le fichier de plusieurs pages. Dans la zone supérieure gauche de la page, cliquez sur l’icône ![du rail](assets/do-not-localize/aem_leftrail_contentonly.png) gauche et cliquez sur **[!UICONTROL Sous-ensembles]** dans la liste. Lorsque vous sélectionnez **[!UICONTROL Sous-ensembles]** dans la liste. Vous pouvez également utiliser le raccourci clavier `alt + 5`.

![Affichage des sous-ressources d’un fichier de plusieurs pages](assets/view_subassets_simulation.gif)

## Affichage des pages d’un fichier multipage {#view-pages-of-a-multi-page-file}

Vous pouvez afficher un fichier de plusieurs pages, tel que PDF, INDD, PPT, PPTX et AI, à l’aide de la fonctionnalité de visionneuse de pages des ressources AEM. Ouvrez un fichier de plusieurs pages et cliquez sur **[!UICONTROL Afficher les pages]** dans le coin supérieur gauche de la page. La visionneuse de pages qui s’ouvre affiche les pages du fichier et les commandes permettant de parcourir et de zoomer sur chaque page.

![Affichage et affichage des pages d’un fichier de plusieurs pages](assets/view_multipage_asset_fmr.gif)

S’agissant d’InDesign, vous pouvez extraire des pages à l’aide du serveur InDesign. Si les aperçus des pages sont enregistrés lors de la création du fichier InDesign, le serveur InDesign n’est pas nécessaire pour l’extraction des pages.

Les options suivantes sont disponibles dans la barre d’outils, dans le rail de gauche et dans les commandes de la visionneuse de pages :

* **[!UICONTROL Actions]** de bureau pour ouvrir ou afficher une sous-ressource spécifique à l’aide de l’application de bureau AEM. Découvrez comment [configurer les actions](https://docs.adobe.com/content/help/en/experience-manager-desktop-app/using/using.html#desktopactions-v2) de bureau si vous utilisez l’application de bureau AEM.

* **[!UICONTROL L’option Propriétés]** ouvre la page [!UICONTROL Propriétés] de la sous-ressource spécifique.

* **[!UICONTROL L’option Annoter]** vous permet d’annoter la sous-ressource spécifique. Les annotations que vous utilisez sur des sous-ressources distinctes sont collectées et affichées ensemble lorsque le fichier parent est ouvert pour affichage.

* **[!UICONTROL L’option Aperçu]** de la page affiche toutes les sous-ressources simultanément.

* **[!UICONTROL L’option Chronologie]** du rail de gauche après avoir cliqué sur l’icône ![du rail de](assets/do-not-localize/aem_leftrail_contentonly.png) gauche affiche le flux d’activité du fichier.
