---
title: Création de projets de traduction
description: Apprenez à créer des projets de traduction dans AEM.
contentOwner: AG
translation-type: tm+mt
source-git-commit: a39ee0f435dc43d2c2830b2947e91ffdcf11c7f6

---


# Création de projets de traduction {#creating-translation-projects}

Pour créer une copie de langue, déclenchez l’un des processus de copie de langue suivants disponibles sous le rail de références dans l’interface utilisateur d’AEM.

* **Créer et traduire**: Dans ce flux de travaux, les fichiers à traduire sont copiés dans la langue racine de la langue dans laquelle vous souhaitez les traduire. En outre, en fonction des options que vous sélectionnez, un projet de traduction est créé pour les ressources dans la console Projets. En fonction des paramètres, vous pouvez démarrer le projet de traduction manuellement ou autoriser son exécution automatique dès sa création.

* **Mettre à jour les copies** de langue : Exécutez ce processus pour traduire un groupe supplémentaire de ressources et l’inclure dans une copie de langue pour un paramètre régional spécifique. Dans ce cas, les ressources traduites sont ajoutées au dossier cible qui contient des ressources précédemment traduites.

>[!NOTE]
>
>Les binaires des ressources ne sont traduits que si le fournisseur du service de traduction prend en charge la traduction de binaires.

>[!NOTE]
>
>Si vous lancez un processus de traduction pour des fichiers complexes, tels que des fichiers PDF et InDesign, leurs sous-ressources ou rendus (le cas échéant) ne sont pas envoyés pour traduction.

## Processus Créer et traduire {#create-and-translate-workflow}

Vous utilisez le processus de création et de traduction pour générer des copies de langue pour une langue particulière pour la première fois. Le processus offre les options suivantes :

* Créer uniquement la structure
* Créer un projet de traduction
* Ajouter à un projet de traduction existant

### Créer uniquement la structure {#create-structure-only}

Use the **[!UICONTROL Create structure only]** option to create a target folder hierarchy within the target language root to match the hierarchy of the source folder within the source language root. Dans ce cas, les ressources source sont copiées dans le dossier de destination. Cependant, aucun projet de traduction n’est généré.

1. Dans l’interface utilisateur d’Assets, sélectionnez le dossier source pour lequel vous souhaitez créer une structure au niveau de la racine de la langue cible.
1. Ouvrez le panneau **[!UICONTROL Références]** et cliquez/appuyez sur **[!UICONTROL Copies de langue]** sous **[!UICONTROL Copies]**.

   ![chlimage_1-57](assets/chlimage_1-57.png)

1. Click/tap **[!UICONTROL Create &amp; Translate]** at the bottom.

   ![chlimage_1-58](assets/chlimage_1-58.png)

1. Dans la liste **[!UICONTROL Langues cibles]**, choisissez la langue pour laquelle vous souhaitez créer une structure de dossiers.

   ![chlimage_1-59](assets/chlimage_1-59.png)

1. Dans la liste **[!UICONTROL Projet]**, sélectionnez **[!UICONTROL Créer uniquement la structure]**.

   ![chlimage_1-60](assets/chlimage_1-60.png)

1. Cliquez/appuyez sur **[!UICONTROL Créer]**. The new structure for the target language is listed under **[!UICONTROL Language Copies]**.

   ![chlimage_1-61](assets/chlimage_1-61.png)

1. Cliquez/appuyez sur la structure dans la liste, puis cliquez/appuyez sur **[!UICONTROL Afficher dans Assets]** pour accéder à la structure de dossiers au niveau de la langue cible.

   ![chlimage_1-62](assets/chlimage_1-62.png)

### Créer un projet de traduction {#create-a-new-translation-project}

Si vous utilisez cette option, les ressources à traduire sont copiées dans la racine de la langue vers laquelle vous souhaitez effectuer la traduction. En fonction des options que vous sélectionnez, un projet de traduction est créé pour les ressources dans la console Projets. En fonction des paramètres, le projet de traduction peut être démarré manuellement ou s’exécuter automatiquement dès sa création.

1. Dans l’interface utilisateur d’Assets, sélectionnez le dossier source pour lequel vous souhaitez créer une copie de langue.
1. Ouvrez le panneau **[!UICONTROL Références]** et cliquez/appuyez sur **[!UICONTROL Copies de langue]** sous **[!UICONTROL Copies]**.

   ![chlimage_1-63](assets/chlimage_1-63.png)

1. Click/tap **[!UICONTROL Create &amp; Translate]** at the bottom.

   ![chlimage_1-64](assets/chlimage_1-64.png)

1. Dans la liste **[!UICONTROL Langues cibles]**, choisissez la ou les langues pour lesquelles vous souhaitez créer une structure de dossiers.

   ![chlimage_1-65](assets/chlimage_1-65.png)

1. Dans la liste **[!UICONTROL Projet]**, choisissez **[!UICONTROL Créer un projet de traduction]**.

   ![chlimage_1-66](assets/chlimage_1-66.png)

1. Dans le champ **[!UICONTROL Titre du projet]**, saisissez un titre pour le projet.

   ![chlimage_1-67](assets/chlimage_1-67.png)

1. Cliquez/appuyez sur **[!UICONTROL Créer]**. Les ressources du dossier source sont copiées vers les dossiers cibles pour les paramètres régionaux que vous avez sélectionnés à l’étape 4.

   ![chlimage_1-68](assets/chlimage_1-68.png)

1. Pour accéder au dossier, sélectionnez la copie de langue, puis cliquez sur **[!UICONTROL Afficher dans Assets]**.

   ![chlimage_1-69](assets/chlimage_1-69.png)

1. Accédez à la console Projets. Le dossier de traduction est copié dans la console Projets.

   ![chlimage_1-70](assets/chlimage_1-70.png)

1. Ouvrez le dossier pour afficher le projet de traduction.

   ![chlimage_1-71](assets/chlimage_1-71.png)

1. Cliquez/appuyez sur le projet pour ouvrir la page de détails.

   ![chlimage_1-72](assets/chlimage_1-72.png)

1. Pour afficher l’état de la tâche de traduction, cliquez sur les points de suspension en bas de la mosaïque **[!UICONTROL Tâche de traduction]**.

   ![chlimage_1-73](assets/chlimage_1-73.png)

   Pour plus d’informations sur les états des tâches, voir [Surveillance de l’état d’une tâche de traduction](/help/sites-administering/tc-manage.md#monitoring-the-status-of-a-translation-job).

1. Accédez à l’interface utilisateur d’Assets et ouvrez la page Propriétés de chacune des ressources traduites afin d’afficher les métadonnées traduites.

   ![chlimage_1-74](assets/chlimage_1-74.png)

   >[!NOTE]
   >
   >Cette fonctionnalité est disponible à la fois pour les ressources et les dossiers. Lorsqu’une ressource est sélectionnée au lieu d’un dossier, la hiérarchie de dossiers complète jusqu’à la langue racine est copiée afin de créer une copie de langue pour la ressource.

### Ajouter à un projet de traduction existant {#add-to-existing-translation-project}

Si vous utilisez cette option, le processus de traduction s’exécute pour les ressources que vous ajoutez au dossier source après l’exécution d’un précédent processus de traduction. Seules les nouvelles ressources ajoutées sont copiées dans le dossier cible contenant les ressources précédemment traduites. Aucun projet de traduction n’est créé dans ce cas.

1. Dans l’interface utilisateur d’Assets, accédez au dossier source qui contient des ressources non traduites.
1. Select an asset you want to translate, and open the **[!UICONTROL Reference pane]**. The **[!UICONTROL Language Copies]** section displays the number of translation copies that are currently available.
1. Click/tap **[!UICONTROL Language Copies]** under **[!UICONTROL Copies]**. Une liste des copies de traduction disponibles s’affiche.
1. Click/tap **[!UICONTROL Create &amp; Translate]** at the bottom.

   ![chlimage_1-75](assets/chlimage_1-75.png)

1. Dans la liste **[!UICONTROL Langues cibles]**, choisissez la ou les langues pour lesquelles vous souhaitez créer une structure de dossiers.

   ![chlimage_1-76](assets/chlimage_1-76.png)

1. Dans la liste **[!UICONTROL Projet]**, sélectionnez **[!UICONTROL Ajouter à un projet de traduction existant]** afin d’exécuter le processus de traduction sur le dossier.

   ![chlimage_1-77](assets/chlimage_1-77.png)

   >[!NOTE]
   >
   >Si vous sélectionnez l’option **[!UICONTROL Ajouter à un projet de traduction existant]**, votre projet de traduction est ajouté à un projet préexistant uniquement si les paramètres du projet correspondent exactement à ceux du projet préexistant. Dans le cas contraire, un nouveau projet est créé.

1. Dans la liste **[!UICONTROL Projet de traduction existant]**, choisissez un projet auquel ajouter la ressource à traduire.

   ![chlimage_1-78](assets/chlimage_1-78.png)

1. Cliquez/appuyez sur **[!UICONTROL Créer]**. Les ressources à traduire sont ajoutées au dossier cible. Le dossier mis à jour est répertorié sous la section **[!UICONTROL Copies de langue]**.

   ![chlimage_1-79](assets/chlimage_1-79.png)

1. Accédez à la console Projets, puis ouvrez le projet de traduction existant auquel vous avez ajouté des ressources.
1. Cliquez/appuyez sur le projet de traduction pour afficher la page de détails du projet.

   ![chlimage_1-80](assets/chlimage_1-80.png)

1. Click/tap the ellipsis at the bottom of the **Translation Job** tile to view the assets in the translation workflow. La liste des tâches de traduction contient également des entrées pour les balises et les métadonnées des ressources. Ces entrées indiquent que les métadonnées et les balises des ressources sont également traduites.

   >[!NOTE]
   >
   >Si vous supprimez l’entrée des étiquettes ou des métadonnées, aucune balise ou métadonnée n’est traduite pour l’ensemble des ressources.

   >[!NOTE]
   >
   >Si vous utilisez la traduction automatique, les binaires des ressources ne sont pas traduits.

   >[!NOTE]
   >
   >Si la ressource que vous ajoutez à la tâche de traduction contient des sous-ressources, sélectionnez-les et supprimez-les pour que la traduction se déroule sans problème.

1. To start the translation for the assets, click/tap the arrow on the **[!UICONTROL Translation Job]** tile and select **[!UICONTROL Start]** from the list.

   ![chlimage_1-81](assets/chlimage_1-81.png)

   Un message indique le début de la tâche de traduction.

   ![chlimage_1-82](assets/chlimage_1-82.png)

1. Pour afficher l’état de la tâche de traduction, cliquez/appuyez sur les points de suspension en bas de la mosaïque **[!UICONTROL Tâche de traduction]**.

   ![chlimage_1-83](assets/chlimage_1-83.png)

   For more details, see [Monitoring the Status of a Translation Job](/help/sites-administering/tc-manage.md#monitoring-the-status-of-a-translation-job).

1. Une fois la traduction terminée, l’état devient Prêt pour la révision. Accédez à l’interface utilisateur d’Assets et ouvrez la page Propriétés de chacune des ressources traduites afin d’afficher les métadonnées traduites.

## Màj des copies de langue {#update-language-copies}

Exécutez ce processus pour traduire un ensemble de ressources supplémentaire et l’intégrer à une copie de langue pour des paramètres régionaux spécifiques. Dans ce cas, les ressources traduites sont ajoutées au dossier cible qui contient des ressources précédemment traduites. Selon les options choisies, un projet de traduction est créé ou un projet de traduction existant est mis à jour avec les nouvelles ressources. Le processus Màj des copies de langue comprend les options suivantes :

* Créer un projet de traduction
* Ajouter à un projet de traduction existant

### Créer un projet de traduction {#create-a-new-translation-project-1}

Si vous utilisez cette option, un projet de traduction est créé pour le jeu de ressources pour lequel vous souhaitez mettre à jour une copie de langue.

1. Dans l’interface utilisateur d’Assets, sélectionnez le dossier source auquel vous avez ajouté une ressource.
1. Open the **[!UICONTROL References]** pane, and click/tap **[!UICONTROL Language Copies]** under **[!UICONTROL Copies]** to display the list of language copies.
1. Cochez la case en regard de **[!UICONTROL Copies de langue]**, puis sélectionnez le dossier cible correspondant aux paramètres régionaux appropriés.

   ![chlimage_1-84](assets/chlimage_1-84.png)

1. Cliquez/appuyez sur **[!UICONTROL Màj des copies de langue]** en bas de la page.

   ![chlimage_1-85](assets/chlimage_1-85.png)

1. Dans la liste **[!UICONTROL Projet]**, choisissez **[!UICONTROL Créer un projet de traduction]**.

   ![chlimage_1-86](assets/chlimage_1-86.png)

1. Dans le champ **[!UICONTROL Titre du projet]**, saisissez un titre pour le projet.

   ![chlimage_1-87](assets/chlimage_1-87.png)

1. Cliquez/appuyez sur **[!UICONTROL Démarrer]**.
1. Accédez à la console Projets. Le dossier de traduction est copié dans la console Projets.

   ![chlimage_1-88](assets/chlimage_1-88.png)

1. Ouvrez le dossier pour afficher le projet de traduction.

   ![chlimage_1-89](assets/chlimage_1-89.png)

1. Cliquez/appuyez sur le projet pour ouvrir la page de détails.

   ![chlimage_1-90](assets/chlimage_1-90.png)

1. Pour commencer la traduction des ressources, cliquez sur la flèche au niveau de la mosaïque **[!UICONTROL Tâche de traduction]** et sélectionnez **[!UICONTROL Démarrer]** dans la liste.

   ![chlimage_1-91](assets/chlimage_1-91.png)

   Un message indique le début de la tâche de traduction.

   ![chlimage_1-92](assets/chlimage_1-92.png)

1. Pour afficher l’état de la tâche de traduction, cliquez/appuyez sur les points de suspension en bas de la mosaïque **[!UICONTROL Tâche de traduction]**.

   ![chlimage_1-93](assets/chlimage_1-93.png)

   Pour plus d’informations sur les états des tâches, voir [Surveillance de l’état d’une tâche de traduction](../sites-administering/tc-manage.md#monitoring-the-status-of-a-translation-job).

1. Accédez à l’interface utilisateur d’Assets et ouvrez la page Propriétés de chacune des ressources traduites afin d’afficher les métadonnées traduites.

### Ajouter à un projet de traduction existant {#add-to-existing-translation-project-1}

Si vous utilisez cette option, l’ensemble de ressources est ajouté à un projet de traduction existant afin de mettre à jour la copie de langue pour les paramètres régionaux que vous sélectionnez.

1. Dans l’interface utilisateur d’Assets, sélectionnez le dossier source auquel vous avez ajouté un dossier de ressources.
1. Open the **[!UICONTROL References pane]**, and click/tap **[!UICONTROL Language Copies]** under **[!UICONTROL Copies]** to display the list of language copies.

   ![chlimage_1-94](assets/chlimage_1-94.png)

1. Select the check box before **[!UICONTROL Language Copies]**, which selects all language copies. Désélectionnez les autres copies à l’exception des copies de langue correspondant aux paramètres régionaux dans lesquels vous souhaitez traduire.

   ![chlimage_1-95](assets/chlimage_1-95.png)

1. Cliquez/appuyez sur **[!UICONTROL Màj des copies de langue]** en bas de la page.

   ![chlimage_1-96](assets/chlimage_1-96.png)

1. From the **[!UICONTROL Project]** list, choose **[!UICONTROL Add to existing translation project]**.

   ![chlimage_1-97](assets/chlimage_1-97.png)

1. Dans la liste **[!UICONTROL Projet de traduction existant]**, choisissez un projet auquel ajouter la ressource à traduire.

   ![chlimage_1-98](assets/chlimage_1-98.png)

1. Cliquez/appuyez sur **[!UICONTROL Démarrer]**.
1. See steps 9-14 of [Add to existing translation project](translation-projects.md#add-to-existing-translation-project) to complete the rest of the procedure.

## Création de copies de langue temporaires {#creating-temporary-language-copies}

Lorsque vous exécutez un processus de traduction pour mettre à jour une copie de langue avec les versions modifiées des ressources d’origine, la copie de langue existante est conservée jusqu’à ce que vous approuviez la ou les ressources traduites. AEM Assets stocke les nouvelles ressources traduites dans un emplacement temporaire et met à jour la copie de langue existante après votre approbation explicite des ressources. Si vous rejetez les ressources, la copie de langue reste inchangée.

1. Click/tap the source root folder under **[!UICONTROL Language Copies]** for which you already created a language copy, and then click/tap **[!UICONTROL Reveal in Assets]** to open the folder in AEM Assets.

   ![chlimage_1-99](assets/chlimage_1-99.png)

1. Dans l’interface utilisateur d’Assets, sélectionnez une ressource que vous avez déjà traduite et cliquez/appuyez sur l’icône **[!UICONTROL Modifier]** dans la barre d’outils pour ouvrir la ressource en mode d’édition.
1. Modifiez la ressource et enregistrez les modifications.
1. Perform steps 2-14 of the [Add to existing translation project](#add-to-existing-translation-project) procedure to update the language copy.
1. Click/tap the ellipsis at the bottom of the **[!UICONTROL Translation Job]** tile. Dans la liste des ressources sur la page **[!UICONTROL Tâche de traduction]**, vous pouvez voir l’emplacement temporaire dans lequel la version traduite de la ressource est stockée.

   ![chlimage_1-101](assets/chlimage_1-101.png)

1. Cochez la case en regard de **[!UICONTROL Titre]**.
1. From the toolbar, click/tap **[!UICONTROL Accept Translation]** and then click/tap **[!UICONTROL Accept]** in the dialog to overwrite the translated asset in the target folder with the translated version of the edited asset.

   ![chlimage_1-102](assets/chlimage_1-102.png)

   >[!NOTE]
   >
   >Pour permettre au processus de traduction de mettre à jour la ou les ressources de destination, acceptez à la fois la ressource et les métadonnées.

   Click/tap **[!UICONTROL Reject Translation]** to retain the originally translated version of the asset in the target locale root and reject the edited version.

   ![chlimage_1-103](assets/chlimage_1-103.png)

1. Accédez à la console Ressources et ouvrez la page Propriétés de chacune des ressources traduites afin d’afficher les métadonnées traduites.

For tips on translating metadata for assets efficiently, see [5 Steps for Efficiently Translating Metadata](https://blogs.adobe.com/experiencedelivers/experience-management/translate_aemassets_metadata/).
