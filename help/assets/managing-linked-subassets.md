---
title: Gestion des ressources composites avec des références et plusieurs pages
description: Découvrez comment créer des références à des ressources numériques dans [!DNL Adobe InDesign], [!DNL Adobe Illustrator], et [!DNL Adobe Photoshop]. Utilisez la fonction Visionneuse de page pour afficher les pages de sous-ressources individuelles de fichiers multi-pages, tels que les fichiers PDF, INDD, PPT, PPTX et AI.
contentOwner: AG
role: User, Admin
feature: Asset Management
exl-id: 1ea9d8fe-602c-452b-9a24-4125b705aedf
source-git-commit: 79d8b5896f5f8eb7a22dccea81acf0656d435f2b
workflow-type: tm+mt
source-wordcount: '1424'
ht-degree: 17%

---

# Gestion des ressources composites et multi-pages {#managing-compound-assets}

[!DNL Adobe Experience Manager Assets] peut identifier si un fichier chargé contient des références à des ressources qui existent déjà dans le référentiel. Cette fonctionnalité est disponible uniquement pour les types de formats pris en charge. Si la ressource chargée contient des références à [!DNL Experience Manager] ressources, un lien bidirectionnel est créé entre les ressources chargées et référencées.

Outre la suppression de la redondance, le référencement des ressources dans [!DNL Adobe Creative Cloud] Les applications améliorent la collaboration et augmentent l’efficacité et la productivité des utilisateurs.

[!DNL Experience Manager Assets] prend en charge le référencement bidirectionnel. Vous trouverez des ressources référencées dans la page des détails de la ressource du fichier chargé. En outre, vous pouvez afficher les fichiers de référencement dans la page des détails de la ressource référencée.

Les références sont résolues sur la base du chemin d’accès, du document et de l’ID d’instance des ressources référencées.

## [!DNL Adobe Illustrator]: Ajout de ressources numériques en tant que références {#refai}

Vous pouvez référencer des ressources numériques existantes dans une [!DNL Adobe Illustrator] fichier .

1. Utilisation [[!DNL Experience Manager] application de bureau](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html?lang=fr), récupérez les ressources numériques sur le système de fichiers local. Accédez à l’emplacement du système de fichiers de la ressource que vous souhaitez référencer.
1. Faites glisser la ressource du dossier local vers le [!DNL Illustrator] fichier .

1. Enregistrez le [!DNL Illustrator] sur le lecteur monté, ou [charger](/help/assets/manage-assets.md#uploading-assets) au [!DNL Experience Manager] référentiel.

1. Une fois le workflow terminé, accédez à la page des détails de la ressource. Les références aux ressources numériques existantes sont répertoriées sous **[!UICONTROL Dépendances]** dans le **[!UICONTROL Références]** colonne .

   ![chlimage_1-84](assets/chlimage_1-258.png)

1. Les ressources référencées qui apparaissent sous **[!UICONTROL Dépendances]** peuvent également être référencées par des fichiers autres que celui qui est actif. Pour afficher une liste des fichiers de référencement d’une ressource, cliquez sur son nom sous **[!UICONTROL Dépendances]**.

   ![chlimage_1-85](assets/chlimage_1-259.png)

1. Cliquez sur **[!UICONTROL Afficher les propriétés]** dans la barre d’outils. Dans le [!UICONTROL Propriétés] , la liste des fichiers qui font référence à la ressource active apparaît sous la propriété **[!UICONTROL Références]** dans la colonne **[!UICONTROL De base]** .

   ![afficher les références de Experience Manager Assets dans la colonne Références dans les détails de la ressource ;](assets/asset-references.png)

   *Figure : Références de ressource dans les détails de la ressource.*

## [!DNL Adobe InDesign]: Ajout de ressources numériques en tant que références {#add-aem-assets-as-references-in-adobe-indesign}

Pour référencer des ressources numériques depuis un [!DNL InDesign] Faites glisser les ressources vers le fichier [!DNL InDesign] d’exporter le fichier [!DNL InDesign] en tant qu’archive ZIP.

Les ressources référencées existent déjà dans [!DNL Experience Manager Assets]. Vous pouvez extraire des sous-ressources en procédant comme suit : [configuration de l’InDesign Server](indesign.md). Ressources incorporées dans une [!DNL InDesign] sont extraites en tant que sous-ressources.

>[!NOTE]
>
>Si la variable [!DNL InDesign Server] est par proxy, [!DNL InDesign] leur aperçu est incorporé dans leurs métadonnées XMP. Dans ce cas, l’extraction de miniature n’est pas explicitement requise. Cependant, si la variable [!DNL InDesign Server] n’a pas de proxy, les miniatures doivent être explicitement extraites pour [!DNL InDesign] fichiers .

Lorsqu’un fichier INDD est chargé, les références sont récupérées en interrogeant des ressources dont la variable `xmpMM:InstanceID` et `xmpMM:DocumentID` dans le référentiel.

### Création de références en faisant glisser des ressources {#create-references-by-dragging-aem-assets}

Cette procédure est similaire à [ajout de ressources numériques en tant que références dans Adobe Illustrator](#refai).

### Création de références aux ressources en exportant un fichier ZIP {#create-references-to-aem-assets-by-exporting-a-zip-file}

1. Suivez la procédure décrite à la section [Création de modèles de workflow](/help/sites-developing/workflows-models.md) pour créer un nouveau workflow.
1. Utilisez la variable [Fonctionnalité de module](https://helpx.adobe.com/indesign/how-to/indesign-package-files-for-handoff.html) de [!DNL Adobe InDesign] pour exporter le document. [!DNL Adobe InDesign] peut exporter un document et les ressources liées sous la forme d’un assemblage. Dans ce cas, le dossier exporté contient une `Links` dossier contenant des sous-ressources dans [!DNL InDesign] fichier . Le `Links` est présent dans le même dossier que le fichier INDD.
1. Créez un fichier ZIP et téléchargez-le dans le [!DNL Experience Manager] référentiel.
1. Démarrez le `Unarchiver` workflow.
1. Une fois le workflow terminé, les références contenues dans le dossier Liens sont automatiquement référencées en tant que sous-ressources. Pour afficher la liste des ressources référencées, accédez à la page des détails de la ressource du [!DNL InDesign] et fermez la [Rail](/help/sites-authoring/basic-handling.md#rail-selector).

## [!DNL Adobe Photoshop]: Ajout de ressources numériques en tant que références {#refps}

1. Utilisation [!DNL Experience Manager] application de bureau pour accéder à [!DNL Experience Manager Assets]. Téléchargez et affichez les ressources sur le système de fichiers local. Utilisez la variable [!UICONTROL Placer les liens] fonctionnalité dans [!DNL Adobe Photoshop]. Voir [placement de ressources dans l’appli de bureau](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html#place-assets-in-native-documents).

1. Enregistrer dans [!DNL Photoshop] sur le lecteur monté ou [charger](/help/assets/manage-assets.md#uploading-assets) au [!DNL Experience Manager] référentiel.
1. Une fois le workflow terminé, les références aux [!DNL Experience Manager] Les ressources sont répertoriées dans la page des détails de la ressource.

   Pour afficher les ressources référencées, fermez le [rail](/help/sites-authoring/basic-handling.md#rail-selector) dans la page des détails de la ressource.

1. Les ressources référencées contiennent également la liste des ressources à partir desquelles elles sont référencées. Pour afficher la liste des ressources référencées, accédez à la page des détails de la ressource et fermez le [rail](/help/sites-authoring/basic-handling.md#rail-selector).

>[!NOTE]
>
>Les ressources contenues dans des ressources composites peuvent également être référencées par ID de document et ID d’instance. Cette fonctionnalité est disponible avec [!DNL Adobe Illustrator] et [!DNL Adobe Photoshop] versions uniquement. Pour d’autres, le référencement est effectué sur la base du chemin relatif des ressources liées dans la ressource composite principale, comme dans les versions antérieures de [!DNL Experience Manager].

## Création de sous-ressources {#generate-subassets}

Pour les ressources prises en charge avec des formats multi-pages : fichiers de PDF, fichiers AI, [!DNL Microsoft PowerPoint] et [!DNL Apple Keynote] fichiers et [!DNL Adobe InDesign] files — [!DNL Experience Manager] peut générer des sous-ressources qui correspondent à chaque page de la ressource d’origine. Ces sous-ressources sont liées à la fonction *parent* et facilitent l’affichage de plusieurs pages. Pour tous les autres usages, les sous-ressources sont traitées comme des ressources normales dans [!DNL Experience Manager].

La génération de sous-ressources est désactivée par défaut. Pour activer la génération de sous-ressources, procédez comme suit :

1. Se connecter [!DNL Experience Manager] en tant qu’administrateur. Accès **[!UICONTROL Outils]** > **[!UICONTROL Workflow]** > **[!UICONTROL Modèles]**.
1. Sélectionner **[!UICONTROL Ressources de mise à jour de gestion des actifs numériques]** workflow et clic **[!UICONTROL Modifier]**.
1. Cliquez sur **[!UICONTROL Activer/désactiver le panneau latéral]** et recherchez la variable **[!UICONTROL Créer une sous-ressource]** étape . Ajoutez l’étape au workflow. Cliquez sur **[!UICONTROL Synchroniser]**.

Pour générer les sous-ressources, effectuez l’une des opérations suivantes :

* Nouvelles ressources : Le [!UICONTROL Ressources de mise à jour de gestion des actifs numériques] le workflow s’exécute sur toute nouvelle ressource chargée dans [!DNL Experience Manager]. Les sous-ressources sont générées automatiquement pour les nouvelles ressources multi-pages.
* Ressources multi-pages existantes : Exécutez manuellement la variable [!UICONTROL Ressources de mise à jour de gestion des actifs numériques] workflow suivant l’une des étapes :

   * Sélectionnez une ressource et cliquez sur [!UICONTROL Chronologie] pour ouvrir le panneau de gauche. Vous pouvez également utiliser le raccourci clavier `alt + 3`. Cliquez sur [!UICONTROL Démarrer le processus], sélectionnez [!UICONTROL Ressources de mise à jour de gestion des actifs numériques], cliquez sur [!UICONTROL Début], puis cliquez sur [!UICONTROL Continuer].
   * Sélectionnez une ressource et cliquez sur [!UICONTROL Créer] > [!UICONTROL Workflow] dans la barre d’outils. Dans la boîte de dialogue contextuelle, sélectionnez [!UICONTROL Ressources de mise à jour de gestion des actifs numériques] workflow, cliquez sur [!UICONTROL Début], puis cliquez sur [!UICONTROL Continuer].

Pour les documents Microsoft Word, exécutez la variable **[!UICONTROL Documents Word d’analyse de gestion des actifs numériques]** workflow. Elle génère une `cq:Page` à partir du contenu du document Microsoft Word. Les images extraites du document sont référencées à partir du composant `cq:Page`. Ces images sont extraites même si la génération de sous-ressources est désactivée.

>[!NOTE]
>
>Dans le [!UICONTROL Processus Créer un sous-contenu - Propriétés des étapes] in [!UICONTROL Arguments de processus], vous pouvez spécifier le nombre de sous-ressources qui [!DNL Experience Manager] génère. La valeur par défaut est 5. Pour générer toutes les sous-ressources, laissez le champ vide. Si le champ est négatif, aucune sous-ressource n’est générée.

## Affichage des sous-ressources {#viewing-subassets}

Les sous-ressources ne s’affichent que si elles sont générées et disponibles pour la ressource multi-page sélectionnée. Pour afficher les sous-ressources générées, ouvrez la ressource multi-page. Dans la zone supérieure gauche de la page, cliquez sur ![Option d’ouverture du rail de gauche](assets/do-not-localize/aem_leftrail_contentonly.png) et cliquez sur **[!UICONTROL Sous-ressources]** dans la liste. Lorsque vous sélectionnez **[!UICONTROL Sous-ressources]** dans la liste. Vous pouvez également utiliser le raccourci clavier `alt + 5`.

![Affichage des sous-ressources pour une ressource multi-page](assets/view_subassets_simulation.gif)

## Affichage des pages d’un fichier multipage   {#view-pages-of-a-multi-page-file}

Vous pouvez afficher un fichier de plusieurs pages, tel que PDF, INDD, PPT, PPTX et AI, à l’aide de la fonction Visionneuse de page de [!DNL Experience Manager Assets]. Ouvrez une ressource multi-page et cliquez sur **[!UICONTROL Afficher les pages]** dans le coin supérieur gauche de la page. La Visionneuse de page qui s’ouvre affiche les pages de la ressource et les commandes permettant de parcourir et de zoomer sur chaque page.

![Affichage et affichage des pages d’une ressource multipage](assets/view_multipage_asset_fmr.gif)

Pour [!DNL InDesign], vous pouvez extraire des pages à l’aide de [!DNL InDesign Server]. Si les aperçus de pages sont enregistrés pendant la [!DNL InDesign] création de fichier, puis [!DNL InDesign Server] n’est pas nécessaire pour l’extraction de page.

Les options suivantes sont disponibles dans la barre d’outils, dans le rail de gauche, ainsi que dans les commandes de la visionneuse de page :

* **[!UICONTROL Actions du bureau]** pour ouvrir ou afficher une sous-ressource spécifique à l’aide de [!DNL Experience Manager] application de bureau . Découvrez comment [Configuration des actions de bureau](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html?lang=fr#desktopactions-v2) si vous utilisez [!DNL Experience Manager] application de bureau .

* **[!UICONTROL Propriétés]** ouvre l’option [!UICONTROL Propriétés] de la sous-ressource spécifique.

* **[!UICONTROL Annoter]** vous permet d’annoter la sous-ressource spécifique. Les annotations que vous utilisez sur des sous-ressources distinctes sont collectées et affichées ensemble lorsque la ressource parent est ouverte pour affichage.

* **[!UICONTROL Aperçu de la page]** affiche toutes les sous-ressources simultanément.

* **[!UICONTROL Chronologie]** dans le rail de gauche après avoir cliqué sur ![Option d’ouverture du rail de gauche](assets/do-not-localize/aem_leftrail_contentonly.png) affiche le flux d’activité du fichier.

## Bonnes pratiques et limitation {#best-practice-limitation-tips}

* La génération de sous-ressources peut être très gourmande en ressources, quelle que soit [!DNL Experience Manager] déploiement. Si vous générez des sous-ressources lors du chargement de ressources complexes, ajoutez l’étape dans le workflow Ressources de mise à jour de gestion des actifs numériques . Si vous générez des sous-ressources à la demande, créez un workflow distinct pour générer des sous-ressources. Un workflow dédié vous permet d’ignorer les autres étapes du workflow Ressources de mise à jour de gestion des actifs numériques et d’enregistrer les ressources de calcul.

>[!MORELIKETHIS]
>
>* [Utilisation de l’appli de bureau Adobe Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html)
>* [Configuration des actions de bureau dans Adobe Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html#desktopactions-v2)
>* [Création d’objets dynamiques liés dans Adobe Photoshop](https://helpx.adobe.com/photoshop/using/create-smart-objects.html#create-linked-smart-objects)
>* [Placement de graphiques dans Adobe InDesign](https://helpx.adobe.com/fr/indesign/using/placing-graphics.html)

