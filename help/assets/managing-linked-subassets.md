---
title: Gestion des ressources composites avec des références et plusieurs pages
description: Découvrez comment créer des références aux ressources numériques dans  [!DNL Adobe InDesign], [!DNL Adobe Illustrator], and [!DNL Adobe Photoshop]. Utilisez la fonction Visionneuse de page pour afficher les pages de sous-ressources individuelles de fichiers multi-pages, tels que des fichiers PDF, INDD, PPT, PPTX et AI.
contentOwner: AG
role: Business Practitioner, Administrator
feature: Gestion des ressources
exl-id: 1ea9d8fe-602c-452b-9a24-4125b705aedf
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1380'
ht-degree: 18%

---

# Gestion des ressources composites et multi-pages {#managing-compound-assets}

[!DNL Adobe Experience Manager Assets] peut identifier si un fichier chargé contient des références à des ressources qui existent déjà dans le référentiel. Cette fonctionnalité est disponible uniquement pour les types de formats pris en charge. Si la ressource chargée contient des références aux ressources [!DNL Experience Manager], un lien bidirectionnel est créé entre les ressources chargées et référencées.

Outre l’élimination de la redondance, le référencement des ressources dans les applications [!DNL Adobe Creative Cloud] améliore la collaboration et accroît l’efficacité et la productivité des utilisateurs.

[!DNL Experience Manager Assets] prend en charge le référencement bidirectionnel. Vous trouverez des ressources référencées dans la page des détails de la ressource du fichier chargé. En outre, vous pouvez afficher les fichiers de référencement dans la page des détails de la ressource référencée.

Les références sont résolues sur la base du chemin d’accès, du document et de l’ID d’instance des ressources référencées.

## [!DNL Adobe Illustrator]: Ajout de ressources numériques en tant que références {#refai}

Vous pouvez référencer des ressources numériques existantes dans un fichier [!DNL Adobe Illustrator].

1. À l’aide de [[!DNL Experience Manager] l’appli de bureau ](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html?lang=fr), récupérez les ressources numériques sur le système de fichiers local. Accédez à l’emplacement du système de fichiers de la ressource que vous souhaitez référencer.
1. Faites glisser la ressource du dossier local vers le fichier [!DNL Illustrator].

1. Enregistrez le fichier [!DNL Illustrator] sur le lecteur monté ou [téléchargez](/help/assets/manage-assets.md#uploading-assets) dans le référentiel [!DNL Experience Manager].

1. Une fois le workflow terminé, accédez à la page des détails de la ressource. Les références aux ressources numériques existantes sont répertoriées sous **[!UICONTROL Dépendances]** dans la colonne **[!UICONTROL Références]**.

   ![chlimage_1-84](assets/chlimage_1-258.png)

1. Les ressources référencées qui apparaissent sous **[!UICONTROL Dépendances]** peuvent également être référencées par des fichiers autres que celui qui est actif. Pour afficher une liste des fichiers de référencement d’une ressource, cliquez sur son nom sous **[!UICONTROL Dépendances]**.

   ![chlimage_1-85](assets/chlimage_1-259.png)

1. Cliquez sur **[!UICONTROL Afficher les propriétés]** dans la barre d’outils. Dans la page [!UICONTROL Propriétés] , la liste des fichiers qui référencent la ressource active apparaît sous la colonne **[!UICONTROL Références]** dans l’onglet **[!UICONTROL De base]**.

   ![afficher les références des ressources Experience Manager dans la colonne Références dans les détails de la ressource ;](assets/asset-references.png)

   *Figure : Références de ressource dans les détails de la ressource.*

## [!DNL Adobe InDesign]: Ajout de ressources numériques en tant que références  {#add-aem-assets-as-references-in-adobe-indesign}

Pour référencer des ressources numériques à partir d’un fichier [!DNL InDesign], faites-les glisser vers le fichier [!DNL InDesign] ou exportez le fichier [!DNL InDesign] sous la forme d’une archive ZIP.

Les ressources référencées existent déjà dans [!DNL Experience Manager Assets]. Vous pouvez extraire des sous-ressources en [configurant InDesign Server](indesign.md). Les ressources incorporées dans un fichier [!DNL InDesign] sont extraites en tant que sous-ressources.

>[!NOTE]
>
>Si le [!DNL InDesign Server] est en proxy, l’aperçu des fichiers [!DNL InDesign] est incorporé dans leurs métadonnées XMP. Dans ce cas, l’extraction de miniature n’est pas explicitement requise. Cependant, si la balise [!DNL InDesign Server] n’est pas en proxy, les miniatures doivent être explicitement extraites pour les fichiers [!DNL InDesign].

Lorsqu’un fichier INDD est chargé, les références sont récupérées en interrogeant des ressources ayant des propriétés `xmpMM:InstanceID` et `xmpMM:DocumentID` dans le référentiel.

### Création de références en faisant glisser des ressources {#create-references-by-dragging-aem-assets}

Cette procédure est similaire à l’[ajout de ressources numériques en tant que références dans Adobe Illustrator](#refai).

### Création de références aux ressources en exportant un fichier ZIP {#create-references-to-aem-assets-by-exporting-a-zip-file}

1. Exécutez les étapes de la section [Création de modèles de workflow](/help/sites-developing/workflows-models.md) pour créer un nouveau workflow.
1. Utilisez la [fonction Package](https://helpx.adobe.com/indesign/how-to/indesign-package-files-for-handoff.html) de [!DNL Adobe InDesign] pour exporter le document. [!DNL Adobe InDesign] peut exporter un document et les ressources liées sous la forme d’un assemblage. Dans ce cas, le dossier exporté contient un dossier `Links` contenant des sous-ressources dans le fichier [!DNL InDesign]. Le dossier `Links` est présent dans le même dossier que le fichier INDD.
1. Créez un fichier ZIP et téléchargez-le dans le référentiel [!DNL Experience Manager].
1. Démarrez le workflow `Unarchiver`.
1. Une fois le workflow terminé, les références contenues dans le dossier Liens sont automatiquement référencées en tant que sous-ressources. Pour afficher la liste des ressources référencées, accédez à la page des détails de la ressource [!DNL InDesign] et fermez le [rail](/help/sites-authoring/basic-handling.md#rail-selector).

## [!DNL Adobe Photoshop]: Ajout de ressources numériques en tant que références {#refps}

1. Utilisez l’ [!DNL Experience Manager] appli de bureau pour accéder à [!DNL Experience Manager Assets]. Téléchargez et affichez les ressources sur le système de fichiers local. Utilisez la fonctionnalité [!UICONTROL Placer Linked] dans [!DNL Adobe Photoshop]. Voir [Placement de ressources dans l’appli de bureau ](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html#place-assets-in-native-documents).

   ![chlimage_1-87](assets/chlimage_1-261.png)

1. Enregistrez le fichier [!DNL Photoshop] sur le lecteur monté ou [chargez](/help/assets/manage-assets.md#uploading-assets) dans le référentiel [!DNL Experience Manager].
1. Une fois le workflow terminé, les références aux ressources [!DNL Experience Manager] existantes sont répertoriées dans la page des détails de la ressource.

   Pour afficher les ressources référencées, fermez le [rail](/help/sites-authoring/basic-handling.md#rail-selector) dans la page des détails de la ressource.

1. Les ressources référencées contiennent également la liste des ressources à partir desquelles elles sont référencées. Pour afficher la liste des ressources référencées, accédez à la page des détails de la ressource et fermez le [rail](/help/sites-authoring/basic-handling.md#rail-selector).

>[!NOTE]
>
>Les ressources contenues dans des ressources composites peuvent également être référencées par ID de document et ID d’instance. Cette fonctionnalité est disponible avec les versions [!DNL Adobe Illustrator] et [!DNL Adobe Photoshop] uniquement. Pour d’autres, le référencement est effectué sur la base du chemin relatif des ressources liées dans la ressource composite principale, comme dans les versions antérieures de [!DNL Experience Manager].

## Créer des sous-ressources {#generate-subassets}

Pour les ressources prises en charge avec des formats multi-pages (fichiers PDF, AI, fichiers [!DNL Microsoft PowerPoint] et [!DNL Apple Keynote] et fichiers [!DNL Adobe InDesign]), [!DNL Experience Manager] peut générer des sous-ressources qui correspondent à chaque page de la ressource d’origine. Ces sous-ressources sont liées à la ressource *parent* et facilitent l’affichage de plusieurs pages. Pour tous les autres usages, les sous-ressources sont traitées comme des ressources normales dans [!DNL Experience Manager].

La génération de sous-ressources est désactivée par défaut. Pour activer la génération de sous-ressources, procédez comme suit :

1. Connectez-vous à [!DNL Experience Manager] en tant qu’administrateur. Accédez à **[!UICONTROL Outils]** **[!UICONTROL Processus]** > **[!UICONTROL Modèles]**.
1. Sélectionnez le workflow **[!UICONTROL Ressources de mise à jour de gestion des actifs numériques]** et cliquez sur **[!UICONTROL Modifier]**.
1. Cliquez sur **[!UICONTROL Activer/désactiver le panneau latéral]** et recherchez l’étape **[!UICONTROL Créer un sous-contenu]** . Ajoutez l’étape au workflow. Cliquez sur **[!UICONTROL Synchroniser]**.

Pour générer les sous-ressources, effectuez l’une des opérations suivantes :

* Nouvelles ressources : Le workflow [!UICONTROL Ressources de mise à jour de gestion des actifs numériques] s’exécute sur toute nouvelle ressource qui est téléchargée vers [!DNL Experience Manager]. Les sous-ressources sont générées automatiquement pour les nouvelles ressources multi-pages.
* Ressources multi-pages existantes : Exécutez manuellement le workflow [!UICONTROL Ressources de mise à jour de gestion des actifs numériques] en procédant comme suit :

   * Sélectionnez une ressource et cliquez sur [!UICONTROL Chronologie] pour ouvrir le panneau de gauche. Vous pouvez également utiliser le raccourci clavier `alt + 3`. Cliquez sur [!UICONTROL Démarrer le processus], sélectionnez [!UICONTROL Ressources de mise à jour de gestion des actifs numériques], cliquez sur [!UICONTROL Démarrer], puis cliquez sur [!UICONTROL Continuer].
   * Sélectionnez une ressource et cliquez sur [!UICONTROL Créer] > [!UICONTROL Workflow] dans la barre d’outils. Dans la boîte de dialogue contextuelle, sélectionnez le workflow [!UICONTROL Ressources de mise à jour de gestion des actifs numériques], cliquez sur [!UICONTROL Démarrer], puis sur [!UICONTROL Continuer].

Pour les documents Microsoft Word, exécutez le workflow **[!UICONTROL Documents Word d’analyse de gestion des actifs numériques]**. Il génère un composant `cq:Page` à partir du contenu du document Microsoft Word. Les images extraites du document sont référencées à partir du composant `cq:Page`. Elles sont extraites même si la génération des sous-ressources est désactivée.

## Affichage des sous-ressources {#viewing-subassets}

Les sous-ressources ne s’affichent que si elles sont générées et disponibles pour la ressource multi-page sélectionnée. Pour afficher les sous-ressources générées, ouvrez la ressource multi-page. Dans la zone supérieure gauche de la page, cliquez sur ![Option pour ouvrir le rail de gauche](assets/do-not-localize/aem_leftrail_contentonly.png) et cliquez sur **[!UICONTROL Sous-ressources]** dans la liste. Lorsque vous sélectionnez **[!UICONTROL Sous-ressources]** dans la liste. Vous pouvez également utiliser le raccourci clavier `alt + 5`.

![Affichage des sous-ressources pour une ressource multi-page](assets/view_subassets_simulation.gif)

## Affichage des pages d’un fichier multipage   {#view-pages-of-a-multi-page-file}

Vous pouvez afficher un fichier de plusieurs pages, tel que PDF, INDD, PPT, PPTX et AI, à l’aide de la fonction Visionneuse de page de [!DNL Experience Manager Assets]. Ouvrez une ressource de plusieurs pages et cliquez sur **[!UICONTROL Afficher les pages]** dans le coin supérieur gauche de la page. La Visionneuse de page qui s’ouvre affiche les pages de la ressource et les commandes permettant de parcourir et de zoomer sur chaque page.

![Affichage et affichage des pages d’une ressource multipage](assets/view_multipage_asset_fmr.gif)

Pour [!DNL InDesign], vous pouvez extraire des pages à l’aide de [!DNL InDesign Server]. Si les aperçus des pages sont enregistrés lors de la création du fichier [!DNL InDesign] , [!DNL InDesign Server] n’est pas nécessaire pour l’extraction de page.

Les options suivantes sont disponibles dans la barre d’outils, dans le rail de gauche, ainsi que dans les commandes de la visionneuse de page :

* **[!UICONTROL Actions]** de bureau pour ouvrir ou afficher une sous-ressource spécifique à l’aide de l’appli de  [!DNL Experience Manager] bureau . Découvrez comment [configurer les actions de bureau](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html?lang=fr#desktopactions-v2) si vous utilisez l’appli de bureau [!DNL Experience Manager].

* **** L’option Propriétés ouvre la   page Propriétés de la sous-ressource spécifique.

* **** L’option Annotation vous permet d’annoter la sous-ressource spécifique. Les annotations que vous utilisez sur des sous-ressources distinctes sont collectées et affichées ensemble lorsque la ressource parent est ouverte pour affichage.

* **[!UICONTROL L’option]** Aperçu de page affiche toutes les sous-ressources simultanément.

* **** L’option Chronologie du rail de gauche après avoir cliqué sur  ![Option pour ouvrir le ](assets/do-not-localize/aem_leftrail_contentonly.png) rail de gauche affiche le flux d’activité du fichier.

## Bonnes pratiques et limitation {#best-practice-limitation-tips}

* La génération de sous-ressources peut être très gourmande en ressources pour tout déploiement [!DNL Experience Manager]. Si vous générez des sous-ressources lors du chargement de ressources complexes, ajoutez l’étape dans le workflow Ressources de mise à jour de gestion des actifs numériques . Si vous générez des sous-ressources à la demande, créez un workflow distinct pour générer des sous-ressources. Un workflow dédié vous permet d’ignorer les autres étapes du workflow Ressources de mise à jour de gestion des actifs numériques et d’enregistrer les ressources de calcul.

>[!MORELIKETHIS]
>
>* [Utilisation de l’appli de bureau Adobe Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html)
>* [Configuration des actions de bureau dans Adobe Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html#desktopactions-v2)
>* [Création d’objets dynamiques liés dans Adobe Photoshop](https://helpx.adobe.com/photoshop/using/create-smart-objects.html#create-linked-smart-objects)
>* [Placement de graphiques dans Adobe InDesign](https://helpx.adobe.com/fr/indesign/using/placing-graphics.html)

