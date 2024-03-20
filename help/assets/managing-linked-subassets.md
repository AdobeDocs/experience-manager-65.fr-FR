---
title: Gestion des ressources composites avec des références et plusieurs pages
description: Découvrez comment créer des références à des ressources numériques dans  [!DNL Adobe InDesign], [!DNL Adobe Illustrator] et  [!DNL Adobe Photoshop]. Utilisez la fonction Visionneuse de page pour afficher les pages de sous-ressources individuelles de fichiers multi-pages, tels que les fichiers PDF, INDD, PPT, PPTX et AI.
contentOwner: AG
role: User, Admin
feature: Asset Management
exl-id: 1ea9d8fe-602c-452b-9a24-4125b705aedf
solution: Experience Manager, Experience Manager Assets
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '1382'
ht-degree: 97%

---

# Gestion des ressources composites et multi-pages {#managing-compound-assets}

[!DNL Adobe Experience Manager Assets]peut déterminer si un fichier chargé contient des références à des ressources existant déjà dans le référentiel. Cette fonctionnalité est disponible uniquement pour les types de formats pris en charge. Si le fichier chargé contient des références à des ressources [!DNL Experience Manager], un lien bidirectionnel est créé entre les ressources chargées et celles référencées.

En plus de supprimer toute redondance, le référencement des ressources dans les applications [!DNL Adobe Creative Cloud] améliore la collaboration et accroît l’efficacité et la productivité des utilisateurs.

[!DNL Experience Manager Assets] prend en charge le référencement bidirectionnel. Vous trouverez des ressources référencées dans la page des détails de la ressource du fichier chargé. Vous pouvez, en outre, afficher les fichiers de référencement dans la page des détails de la ressource référencée.

Les références sont résolues sur la base du chemin d’accès, du document et de l’ID d’instance des ressources référencées.

## [!DNL Adobe Illustrator] : ajout de ressources numériques en tant que références {#refai}

Vous pouvez référencer des ressources numériques existantes dans un fichier [!DNL Adobe Illustrator].

1. À l’aide de l’application de bureau [[!DNL Experience Manager] ](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html?lang=fr), récupérez les ressources numériques sur le système de fichiers local. Accédez à l’emplacement du système de fichier que vous souhaitez référencer.
1. Faites glisser la ressource du dossier local jusqu’au fichier [!DNL Illustrator].

1. Enregistrez le fichier [!DNL Illustrator] sur le lecteur monté ou [chargez-le](/help/assets/manage-assets.md#uploading-assets) dans le référentiel [!DNL Experience Manager].

1. Une fois le workflow terminé, accédez à la page des détails de la ressource. Les références à des ressources numériques existantes sont répertoriées sous **[!UICONTROL Dépendances]** dans la colonne **[!UICONTROL Références.]**

   ![chlimage_1-84](assets/chlimage_1-258.png)

1. Les ressources référencées qui apparaissent sous **[!UICONTROL Dépendances]** peuvent également être référencées par des fichiers autres que celui qui est actif. Pour afficher une liste des fichiers de référencement d’une ressource, cliquez sur son nom sous **[!UICONTROL Dépendances]**.

   ![chlimage_1-85](assets/chlimage_1-259.png)

1. Cliquez sur **[!UICONTROL Afficher les propriétés]** dans la barre d’outils. Dans la page des [!UICONTROL propriétés], la liste des fichiers qui référencent la ressource en cours est visible sous la colonne **[!UICONTROL Références]** dans l’onglet **[!UICONTROL De base]**.

   ![afficher les références d’Experience Manager Assets dans la colonne Références dans les détails de la ressource](assets/asset-references.png)

   *Image : Références de ressource dans les détails de la ressource.*

## [!DNL Adobe InDesign] : ajout de ressources numériques en tant que références {#add-aem-assets-as-references-in-adobe-indesign}

Pour référencer des ressources numériques dans un fichier [!DNL InDesign], faites-les glisser jusqu’au fichier [!DNL InDesign] ou exportez le fichier [!DNL InDesign] en tant que fichier ZIP.

Les ressources référencées existent déjà dans [!DNL Experience Manager Assets]. Vous pouvez extraire des sous-ressources lors de la [configuration du serveur InDesign](indesign.md). Les ressources intégrées à un fichier [!DNL InDesign] sont extraites sous la forme de sous-ressources.

>[!NOTE]
>
>Si le [!DNL InDesign Server] est soumis à un proxy, l’aperçu des fichiers [!DNL InDesign] est intégré à leurs métadonnées XMP. Dans ce cas, l’extraction de miniature n’est pas explicitement requise. Toutefois, si le [!DNL InDesign Server] n’est pas soumis à un proxy, les miniatures doivent être explicitement extraites pour les fichiers [!DNL InDesign].

Lorsqu’un fichier INDD est chargé, les références sont récupérées en interrogeant des ressources présentant les propriétés `xmpMM:InstanceID` et `xmpMM:DocumentID` dans le référentiel.

### Création de références en faisant glisser des ressources {#create-references-by-dragging-aem-assets}

Cette procédure est similaire à l’[ajout de ressources en tant que références dans Adobe Illustrator](#refai).

### Création de références dans les ressources en exportant un fichier ZIP {#create-references-to-aem-assets-by-exporting-a-zip-file}

1. Suivez la procédure décrite à la section [Création de modèles de workflow](/help/sites-developing/workflows-models.md) pour créer un workflow.
1. Utilisez la fonctionnalité [Package](https://helpx.adobe.com/indesign/how-to/indesign-package-files-for-handoff.html) d’[!DNL Adobe InDesign] pour exporter le document. [!DNL Adobe InDesign] peut exporter un document et les ressources liées sous la forme d’un package. Dans ce cas, le dossier exporté contient un dossier `Links` dans lequel se trouvent des sous-ressources dans le fichier [!DNL InDesign]. Le dossier `Links` est présent dans le même dossier que le fichier INDD.
1. Créez un fichier ZIP et chargez-le dans le référentiel [!DNL Experience Manager].
1. Lancez le workflow `Unarchiver`.
1. Une fois le workflow terminé, les références du dossier Liens sont automatiquement référencées en tant que sous-ressources. Pour afficher la liste des ressources auxquelles il est fait référence, accédez à la page des détails de la référence de la ressource [!DNL InDesign] et fermez le [rail](/help/sites-authoring/basic-handling.md#rail-selector).

## [!DNL Adobe Photoshop] : ajout de ressources numériques en tant que références {#refps}

1. Utilisez l’application de bureau [!DNL Experience Manager] pour accéder à [!DNL Experience Manager Assets]. Téléchargez et affichez les ressources sur le système de fichiers local. Utilisez la fonctionnalité [!UICONTROL Placer les liens] dans [!DNL Adobe Photoshop]. Consultez la section [Placement de ressources dans l’appli de bureau](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html?lang=fr#place-assets-in-native-documents).

1. Enregistrez le fichier [!DNL Photoshop] sur le lecteur monté ou [chargez-le](/help/assets/manage-assets.md#uploading-assets) vers le référentiel [!DNL Experience Manager].
1. Une fois le workflow terminé, les références aux ressources existantes dans [!DNL Experience Manager] sont répertoriées dans la page des détails de la ressource.

   Pour afficher les ressources référencées, fermez le [rail](/help/sites-authoring/basic-handling.md#rail-selector) dans la page des détails de la ressource.

1. Les ressources référencées contiennent également la liste des ressources à partir desquelles elles sont référencées. Pour afficher la liste des ressources référencées, accédez à la page des détails de la ressource et fermez le [Rail](/help/sites-authoring/basic-handling.md#rail-selector).

>[!NOTE]
>
>Les ressources contenues dans des ressources composites peuvent également être référencées par ID de document et ID d’instance. Cette fonctionnalité est disponible avec les versions d’[!DNL Adobe Illustrator] et d’[!DNL Adobe Photoshop] uniquement. Pour les autres, le référencement s’effectue sur la base du chemin d’accès relatif des ressources liées dans la ressource composite principale, comme dans les versions précédentes d’[!DNL Experience Manager].

## Création de sous-ressources {#generate-subassets}

Pour les ressources prises en charge avec des formats multi-pages (fichiers PDF, fichiers AI, fichiers [!DNL Microsoft PowerPoint] et [!DNL Apple Keynote], et fichiers [!DNL Adobe InDesign]), [!DNL Experience Manager] peut générer des sous-ressources qui correspondent à chaque page de la ressource d’origine. Ces sous-ressources sont liées à la ressource *parent* et facilitent l’affichage de plusieurs pages. Pour tous les autres usages, les sous-ressources sont traitées comme des ressources normales dans [!DNL Experience Manager].

La génération de sous-ressources est désactivée par défaut. Pour activer la génération de sous-ressources, procédez comme suit :

1. Connectez-vous à [!DNL Experience Manager] en tant qu’administrateur. Accédez à **[!UICONTROL Outils]** > **[!UICONTROL Workflow]** > **[!UICONTROL Modèles]**.
1. Sélectionnez le workflow **[!UICONTROL Ressource de mise à jour de gestion des ressources numériques]** et cliquez sur **[!UICONTROL Modifier]**.
1. Cliquez sur **[!UICONTROL Activer/désactiver le panneau latéral]** et recherchez l’étape **[!UICONTROL Créer une sous-ressource]**. Ajoutez l’étape au workflow. Cliquez sur **[!UICONTROL Synchroniser]**.

Pour générer les sous-ressources, effectuez l’une des opérations suivantes :

* Nouvelles ressources : le workflow [!UICONTROL Ressources de mise à jour de gestion des ressources numériques] s’exécute sur toute nouvelle ressource chargée dans [!DNL Experience Manager]. Les sous-ressources sont générées automatiquement pour les nouvelles ressources multi-pages.
* Ressources multi-pages existantes : exécutez manuellement le workflow [!UICONTROL Ressources de mise à jour de gestion des ressources numériques] en suivant l’une de ces étapes :

   * Sélectionnez une ressource et cliquez sur [!UICONTROL Chronologie] pour ouvrir le panneau de gauche. Vous pouvez également utiliser le raccourci clavier `alt + 3`. Cliquez sur [!UICONTROL Démarrer le workflow], sélectionnez [!UICONTROL Ressource de mise à jour de gestion des ressources numériques], cliquez sur [!UICONTROL Démarrer], puis cliquez sur [!UICONTROL Continuer].
   * Sélectionnez une ressource et cliquez sur [!UICONTROL Créer] > [!UICONTROL Workflow] dans la barre d’outils. Dans la boîte de dialogue contextuelle, sélectionnez le workflow [!UICONTROL Ressource de mise à jour de gestion des ressources numériques], cliquez sur [!UICONTROL Début], puis cliquez sur [!UICONTROL Continuer].

Pour les documents Microsoft Word, exécutez le workflow **[!UICONTROL Analyse de gestion des ressources numériques de documents Word]**. Cela génère un composant `cq:Page` à partir du contenu du document Microsoft Word. Les images extraites du document sont référencées à partir du composant `cq:Page`. Elles sont extraites même si la génération des sous-ressources est désactivée.

>[!NOTE]
>
>Dans le [!UICONTROL Processus Créer un sous-contenu - Propriétés des étapes] dans [!UICONTROL Arguments de processus], vous pouvez spécifier le nombre de sous-ressources générées par [!DNL Experience Manager]. La valeur par défaut est 5. Pour générer toutes les sous-ressources, laissez le champ vide. Si le champ est négatif, aucune sous-ressource n’est générée.

## Affichage des sous-ressources {#viewing-subassets}

Les sous-ressources ne s’affichent que si elles sont générées et disponibles pour la ressource multi-page sélectionnée. Pour afficher les sous-ressources générées, ouvrez la ressource multi-page. Dans la zone supérieure gauche de la page, cliquez sur ![Option d’ouverture du rail de gauche](assets/do-not-localize/aem_leftrail_contentonly.png) et cliquez sur **[!UICONTROL Sous-ressources]** dans la liste. Lorsque vous sélectionnez **[!UICONTROL Sous-ressources]** dans la liste. Vous pouvez également utiliser le raccourci clavier `alt + 5`.

![Affichage des sous-ressources pour une ressource multi-page](assets/view_subassets_simulation.gif)

## Affichage des pages d’un fichier multipage {#view-pages-of-a-multi-page-file}

Vous pouvez afficher un fichier de plusieurs pages, tel que PDF, INDD, PPT, PPTX et AI, à l’aide de la fonction Visionneuse de page d’[!DNL Experience Manager Assets]. Ouvrez une ressource multi-page et cliquez sur **[!UICONTROL Afficher les pages]** dans le coin supérieur gauche de la page. La Visionneuse de page qui s’ouvre affiche les pages de la ressource et les commandes permettant de parcourir chaque page et de zoomer sur celles-ci.

![Affichage et consultation des pages d’une ressource multipage](assets/view_multipage_asset_fmr.gif)

Pour [!DNL InDesign], vous pouvez extraire des pages à l’aide d’[!DNL InDesign Server]. Si les aperçus des pages sont enregistrés lors de la création du fichier [!DNL InDesign], [!DNL InDesign Server] n’est pas nécessaire pour l’extraction des pages.

Les options suivantes sont disponibles dans la barre d’outils, dans le rail de gauche, ainsi que dans les commandes de la visionneuse de page :

* **[!UICONTROL Actions du bureau]**, pour ouvrir ou afficher une sous-ressource spécifique à l’aide de l’application de bureau [!DNL Experience Manager]. Découvrez comment [configurer des actions de bureau](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html?lang=fr#desktopactions-v2) si vous utilisez l’application de bureau [!DNL Experience Manager].

* **[!UICONTROL Propriétés]** ouvre l’option [!UICONTROL Propriétés] de la sous-ressource spécifique.

* L’option **[!UICONTROL Annoter]** vous permet d’annoter la sous-ressource spécifique. Les annotations que vous utilisez sur des sous-ressources distinctes sont collectées et affichées ensemble lorsque la ressource parent est ouverte en affichage.

* **[!UICONTROL Aperçu de la page]** affiche toutes les sous-ressources simultanément.

* La **[!UICONTROL Chronologie]**, dans le rail de gauche, après avoir cliqué sur ![Option d’ouverture du rail de gauche](assets/do-not-localize/aem_leftrail_contentonly.png), affiche le flux d’activité du fichier.

## Bonnes pratiques et restrictions {#best-practice-limitation-tips}

* La génération de sous-ressources peut être très gourmande en ressources, quel que soit le déploiement d’[!DNL Experience Manager]. Si vous générez des sous-ressources lors du chargement de ressources complexes, ajoutez l’étape dans le workflow Ressource de mise à jour de gestion des ressources numériques. Si vous générez des sous-ressources à la demande, créez un workflow distinct pour générer des sous-ressources. Un workflow dédié vous permet d’ignorer les autres étapes du workflow Ressource de mise à jour de gestion des ressources numériques et d’économiser en capacités de calcul.

>[!MORELIKETHIS]
>
>* [Utilisation de l’appli de bureau Adobe Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html?lang=fr)
>* [Configuration des actions de bureau dans Adobe Experience Manager](https://experienceleague.adobe.com/docs/experience-manager-desktop-app/using/using.html?lang=fr#desktopactions-v2)
>* [Création d’objets dynamiques liés dans Adobe Photoshop](https://helpx.adobe.com/fr/photoshop/using/create-smart-objects.html#create-linked-smart-objects)
>* [Placement de graphiques dans Adobe InDesign](https://helpx.adobe.com/fr/indesign/using/placing-graphics.html)
