---
title: Création de projets de traduction
description: Apprenez à créer des projets de traduction dans [!DNL Adobe Experience Manager].
contentOwner: AG
role: Architect, Administrator
feature: Translation
translation-type: tm+mt
source-git-commit: 174e0703ae541641e3dc602e700bcd31624ae62c
workflow-type: tm+mt
source-wordcount: '1881'
ht-degree: 66%

---


# Création de projets de traduction {#creating-translation-projects}

Pour créer une copie de langue, déclenchez l’un des workflows de copie de langue suivants disponibles sous le rail Références dans l’interface utilisateur [!DNL Experience Manager].

* **Créer et traduire** : Dans ce processus, les ressources à traduire sont copiées dans la langue racine de la langue à traduire. En outre, en fonction des options que vous sélectionnez, un projet de traduction est créé pour les ressources dans la console Projets. En fonction des paramètres, vous pouvez démarrer le projet de traduction manuellement ou autoriser son exécution automatique dès sa création.

* **Mettre à jour les copies** de langue : Exécutez ce processus pour traduire un groupe supplémentaire de ressources et l’inclure dans une copie de langue pour un paramètre régional particulier. Dans ce cas, les ressources traduites sont ajoutées au dossier cible qui contient des ressources précédemment traduites.

>[!PREREQUISITES]
>
>* Les utilisateurs qui créent des projets de traduction sont membres du groupe `projects-administrators`.
>* Le prestataire de traduction prend en charge la traduction des binaires.


## Workflow Créer et traduire {#create-and-translate-workflow}

Vous utilisez le workflow Créer et traduire afin de générer des copies de langue dans une langue spécifique pour la première fois. Le workflow offre les options suivantes :

* Créer uniquement la structure.
* Créer un projet de traduction.
* Ajouter à un projet de traduction existant.

### Créer uniquement la structure {#create-structure-only}

Utilisez l’option **[!UICONTROL Créer uniquement la structure]** pour créer une hiérarchie de dossiers cible au niveau de la racine de la langue cible semblable à celle du dossier source au sein de la racine de la langue source. Dans ce cas, les fichiers source sont copiés dans le dossier de destination. Cependant, aucun projet de traduction n’est généré.

1. Dans l&#39;interface [!DNL Assets], sélectionnez le dossier source pour lequel vous souhaitez créer une structure dans la racine du langage de cible.

1. Ouvrez le volet **[!UICONTROL Références]** et cliquez sur **[!UICONTROL Copies de langue]** sous **[!UICONTROL Copies]**.

   ![Copies de langue](assets/translation-language-copies.png)

1. Cliquez sur **[!UICONTROL Créer et traduire]**. Dans la liste **[!UICONTROL Langues cibles]**, choisissez la langue pour laquelle vous souhaitez créer une structure de dossiers.

1. Dans la liste **[!UICONTROL Projet]**, sélectionnez **[!UICONTROL Créer uniquement la structure]**.

1. Cliquez sur **[!UICONTROL Créer]**. La nouvelle structure de la langue cible est répertoriée sous **[!UICONTROL Copies de langue]**.

   ![copies de langue](assets/lang-copy2.png)

1. Cliquez sur la structure de la liste, puis sur **[!UICONTROL Afficher dans les ressources]** pour accéder à la structure de dossiers dans la langue de la cible.

   ![révéler des ressources](assets/reveal-in-assets.png)

### Créer un projet de traduction {#create-a-new-translation-project}

Si vous utilisez cette option, les ressources à traduire sont copiées dans la racine de la langue vers laquelle vous souhaitez effectuer la traduction. En fonction des options que vous sélectionnez, un projet de traduction est créé pour les ressources dans la console Projets. En fonction des paramètres, le projet de traduction peut être démarré manuellement ou s’exécuter automatiquement dès sa création.

1. Dans l&#39;interface utilisateur [!DNL Assets], sélectionnez le dossier source pour lequel vous souhaitez créer une copie de langue.
1. Ouvrez le volet **[!UICONTROL Références]** et cliquez sur **[!UICONTROL Copies de langue]** sous **[!UICONTROL Copies]**.

   ![chlimage_1-63](assets/chlimage_1-63.png)

1. Cliquez sur **[!UICONTROL Créer et traduire]** dans la partie inférieure.

1. Dans la liste **[!UICONTROL Langues cibles]**, choisissez la ou les langues pour lesquelles vous souhaitez créer une structure de dossiers.

   ![chlimage_1-65](assets/chlimage_1-65.png)

1. Dans la liste **[!UICONTROL Projet]**, choisissez **[!UICONTROL Créer un projet de traduction]**.

   ![chlimage_1-66](assets/chlimage_1-66.png)

1. Dans le champ **[!UICONTROL Titre du projet]**, saisissez un titre pour le projet.

   ![chlimage_1-67](assets/chlimage_1-67.png)

1. Cliquez sur **[!UICONTROL Créer]**. [!DNL Assets] du dossier source sont copiés dans les dossiers de cible des paramètres régionaux sélectionnés à l’étape 4.

   ![copies de langue](assets/lang-copy2.png)

1. Pour accéder au dossier, sélectionnez la copie de langue, puis cliquez sur **[!UICONTROL Afficher dans Assets]**.

   ![révéler des ressources](assets/reveal-in-assets.png)

1. Accédez à la console Projets. Le dossier de traduction est copié dans la console Projets.

   ![chlimage_1-70](assets/chlimage_1-70.png)

1. Ouvrez le dossier pour afficher le projet de traduction.

   ![chlimage_1-71](assets/chlimage_1-71.png)

1. Cliquez sur le projet pour ouvrir la page de détails.

   ![chlimage_1-72](assets/chlimage_1-72.png)

1. Pour afficher l’état de la tâche de traduction, cliquez sur les points de suspension en bas de la mosaïque **[!UICONTROL Tâche de traduction.]**

   ![chlimage_1-73](assets/chlimage_1-73.png)

   Pour plus d’informations sur les états des tâches, voir [Surveillance de l’état d’une tâche de traduction](/help/sites-administering/tc-manage.md#monitoring-the-status-of-a-translation-job).

1. Accédez à l&#39;interface utilisateur [!DNL Assets] et ouvrez la page [!UICONTROL Propriétés] pour chacun des fichiers traduits afin de vue les métadonnées traduites.

   ![vue des métadonnées traduites dans la page Propriétés du fichier](assets/translated-metadata-asset-properties.png)

   *Figure : Métadonnées traduites dans la page de propriétés des ressources.*

   >[!NOTE]
   >
   >Cette fonctionnalité est disponible à la fois pour les ressources et les dossiers. Lorsqu’une ressource est sélectionnée au lieu d’un dossier, la hiérarchie de dossiers complète jusqu’à la langue racine est copiée afin de créer une copie de langue pour la ressource.

### Ajouter à un projet de traduction existant {#add-to-existing-translation-project}

Si vous utilisez cette option, le workflow de traduction s’exécute pour les ressources que vous ajoutez au dossier source après l’exécution d’un précédent workflow de traduction. Seules les nouvelles ressources ajoutées sont copiées dans le dossier cible contenant les ressources précédemment traduites. Aucun projet de traduction n’est créé dans ce cas.

1. Dans l’interface utilisateur [!DNL Assets], accédez au dossier source qui contient des ressources non traduites.
1. Sélectionnez une ressource à traduire, puis ouvrez le **[!UICONTROL volet Référence]**. La section **[!UICONTROL Copies de langue]** indique le nombre de copies de traduction actuellement disponibles.
1. Cliquez sur **[!UICONTROL Copies de langue]** sous **[!UICONTROL Copies]**. La liste des copies de traduction disponibles s’affiche.
1. Cliquez sur **[!UICONTROL Créer et traduire]** dans la partie inférieure.

1. Dans la liste **[!UICONTROL Langues cibles]**, choisissez la ou les langues pour lesquelles vous souhaitez créer une structure de dossiers.

1. Dans la liste **[!UICONTROL Projet]**, sélectionnez **[!UICONTROL Ajouter à un projet de traduction existant]** afin d’exécuter le workflow de traduction sur le dossier.

   >[!NOTE]
   >
   >Si vous sélectionnez l’option **[!UICONTROL Ajouter à un projet de traduction existant]**, votre projet de traduction est ajouté à un projet préexistant uniquement si les paramètres du projet correspondent exactement à ceux du projet préexistant. Dans le cas contraire, un nouveau projet est créé.

1. Dans la liste **[!UICONTROL Projet de traduction existant]**, choisissez un projet auquel ajouter la ressource à traduire.

1. Cliquez sur **[!UICONTROL Créer]**. Les fichiers à traduire sont ajoutés au dossier cible. Le dossier mis à jour est répertorié sous la section **[!UICONTROL Copies de langue]**.

   ![chlimage_1-79](assets/chlimage_1-79.png)

1. Accédez à la console Projets, puis ouvrez le projet de traduction existant auquel vous avez ajouté des ressources.
1. Cliquez sur le projet de traduction pour afficher la page de détails du projet.

   ![chlimage_1-80](assets/chlimage_1-80.png)

1. Cliquez sur les points de suspension au bas de la mosaïque **Tâche de traduction** pour vue les ressources dans le processus de traduction. La liste des tâches de traduction contient également des entrées pour les balises et les métadonnées des ressources. Ces entrées indiquent que les métadonnées et les balises des ressources sont également traduites.

   >[!NOTE]
   >
   >Si vous supprimez l’entrée des étiquettes ou des métadonnées, aucune balise ou métadonnée n’est traduite pour l’ensemble des ressources.

   >[!NOTE]
   >
   >Si la ressource que vous ajoutez à la tâche de traduction contient des sous-ressources, sélectionnez-les et supprimez-les pour que la traduction se déroule sans problème.

1. Pour commencer la traduction des ressources, cliquez sur la flèche au niveau de la mosaïque **[!UICONTROL Tâche de traduction]** et sélectionnez **[!UICONTROL Démarrer]** dans la liste.

   ![chlimage_1-81](assets/chlimage_1-81.png)

   Un message indique le début de la tâche de traduction.

1. Pour afficher l’état de la tâche de traduction, cliquez sur les points de suspension en bas de la mosaïque **[!UICONTROL Tâche de traduction.]**

   ![chlimage_1-83](assets/chlimage_1-83.png)

   Pour plus de détails, voir [Surveillance de l’état d’une tâche de traduction](/help/sites-administering/tc-manage.md#monitoring-the-status-of-a-translation-job).

1. Une fois la traduction terminée, l’état devient Prêt pour la révision. Accédez à l&#39;interface utilisateur [!DNL Assets] et ouvrez la page Propriétés de chacun des fichiers traduits pour vue les métadonnées traduites.

## Mise à jour des copies de langue {#update-language-copies}

Exécutez ce workflow afin de traduire un ensemble de ressources supplémentaire et de l’intégrer à une copie de langue pour une région donnée. Dans ce cas, les ressources traduites sont ajoutées au dossier cible qui contient des ressources précédemment traduites. Selon les options choisies, un projet de traduction est créé ou un projet de traduction existant est mis à jour avec les nouvelles ressources. Le workflow Màj des copies de langue comprend les options suivantes :

* Créer un projet de traduction
* Ajouter à un projet de traduction existant

### Créer un projet de traduction {#create-a-new-translation-project-1}

Si vous utilisez cette option, un projet de traduction est créé pour l’ensemble de fichiers pour lesquels vous souhaitez mettre à jour une copie de langue.

1. Dans l&#39;interface utilisateur [!DNL Assets], sélectionnez le dossier source dans lequel vous avez ajouté une ressource.
1. Ouvrez le volet **[!UICONTROL Références]**, puis cliquez sur **[!UICONTROL Copies de langue]** sous **[!UICONTROL Copies]** pour afficher la liste des copies de langue.
1. Cochez la case située avant **[!UICONTROL Copies de langue]**, puis sélectionnez le dossier cible correspondant au paramètre régional approprié.

   ![sélectionner une copie de langue](assets/lang-copy1.png)

1. Cliquez sur **[!UICONTROL Mettre à jour les copies de langue]** en bas.

1. Dans la liste **[!UICONTROL Projet]**, choisissez **[!UICONTROL Créer un projet de traduction]**.

1. Dans le champ **[!UICONTROL Titre du projet]**, saisissez un titre pour le projet.

1. Cliquez sur **[!UICONTROL Début]**.
1. Accédez à la console Projets. Le dossier de traduction est copié dans la console Projets.

   ![chlimage_1-88](assets/chlimage_1-88.png)

1. Ouvrez le dossier pour afficher le projet de traduction.

   ![chlimage_1-89](assets/chlimage_1-89.png)

1. Cliquez sur le projet pour ouvrir la page de détails.

   ![chlimage_1-90](assets/chlimage_1-90.png)

1. Pour commencer la traduction des ressources, cliquez sur la flèche au niveau de la mosaïque **[!UICONTROL Tâche de traduction]** et sélectionnez **[!UICONTROL Démarrer]** dans la liste.

   ![chlimage_1-91](assets/chlimage_1-91.png)

   Un message indique le début de la tâche de traduction.

1. Pour afficher l’état de la tâche de traduction, cliquez sur les points de suspension en bas de la mosaïque **[!UICONTROL Tâche de traduction.]**

   ![chlimage_1-93](assets/chlimage_1-93.png)

   Pour plus d’informations sur les états des tâches, voir [Surveillance de l’état d’une tâche de traduction](../sites-administering/tc-manage.md#monitoring-the-status-of-a-translation-job).

1. Accédez à l&#39;interface utilisateur [!DNL Assets] et ouvrez la page Propriétés de chacun des fichiers traduits pour vue les métadonnées traduites.

### Ajouter à un projet de traduction existant {#add-to-existing-translation-project-1}

Si vous utilisez cette option, l’ensemble de ressources est ajouté à un projet de traduction existant afin de mettre à jour la copie de langue pour les paramètres régionaux que vous sélectionnez.

1. Dans l&#39;interface utilisateur [!DNL Assets], sélectionnez le dossier source dans lequel vous avez ajouté un dossier de ressources.
1. Ouvrez le volet **[!UICONTROL Références]**, puis cliquez sur **[!UICONTROL Copies de langue]** sous **[!UICONTROL Copies]** pour afficher la liste des copies de langue.

   ![chlimage_1-94](assets/chlimage_1-94.png)

1. Activez la case à cocher devant **[!UICONTROL Copies de langue]** de façon à sélectionner toutes les copies de langue. Désélectionnez les autres copies à l’exception des copies de langue correspondant aux paramètres régionaux dans lesquels vous souhaitez traduire.

   ![sélectionner une copie de langue](assets/lang-copy1.png)

1. Cliquez sur **[!UICONTROL Mettre à jour les copies de langue]** en bas.

1. Dans la liste **[!UICONTROL Projet]**, choisissez **[!UICONTROL Ajouter à un projet de traduction existant]**.

   ![chlimage_1-97](assets/chlimage_1-97.png)

1. Dans la liste **[!UICONTROL Projet de traduction existant]**, choisissez un projet auquel ajouter la ressource à traduire.

1. Cliquez sur **[!UICONTROL Début]**.
1. Voir les étapes 9 à 14 de la section [Ajouter à un projet de traduction existant](translation-projects.md#add-to-existing-translation-project) pour accomplir le reste de la procédure.

## Création de copies de langue temporaires {#creating-temporary-language-copies}

Lorsque vous exécutez un workflow de traduction pour mettre à jour une copie de langue avec les versions modifiées des ressources d’origine, la copie de langue existante est conservée jusqu’à ce que vous approuviez la ou les ressources traduites. [!DNL Adobe Experience Manager Assets] stocke les nouvelles ressources traduites dans un emplacement temporaire et met à jour la copie de langue existante après votre approbation explicite des ressources. Si vous rejetez les ressources, la copie de langue reste inchangée.

1. Cliquez sur le dossier racine source sous **[!UICONTROL Copies de langue]** pour lesquelles vous avez déjà créé une copie de langue, puis cliquez sur **[!UICONTROL Afficher dans les ressources]** pour ouvrir le dossier dans [!DNL Experience Manager Assets].

   ![chlimage_1-99](assets/chlimage_1-99.png)

1. Dans l&#39;interface [!DNL Assets], sélectionnez un fichier que vous avez déjà traduit et cliquez sur **[!UICONTROL Modifier]** dans la barre d&#39;outils pour ouvrir le fichier en mode d&#39;édition.
1. Modifiez la ressource et enregistrez les modifications.
1. Exécutez les étapes 2 à 14 de la procédure [Ajouter à un projet de traduction existant](#add-to-existing-translation-project) pour mettre à jour la copie de langue.
1. Cliquez sur les points de suspension au bas de la mosaïque **[!UICONTROL Tâche de traduction]**. Dans la liste des ressources sur la page **[!UICONTROL Tâche de traduction]**, vous pouvez voir l’emplacement temporaire dans lequel la version traduite de la ressource est stockée.

   ![chlimage_1-101](assets/chlimage_1-101.png)

1. Cochez la case en regard de **[!UICONTROL Titre]**.
1. Dans la barre d’outils, cliquez sur **[!UICONTROL Accepter la traduction]** ![accepter la traduction](assets/do-not-localize/thumb-up.png), puis sur **[!UICONTROL Accepter]** dans la boîte de dialogue pour remplacer la ressource traduite dans le dossier de cible par la version traduite de la ressource modifiée.

   >[!NOTE]
   >
   >Pour permettre au processus de traduction de mettre à jour les fichiers de destination, acceptez à la fois le fichier et les métadonnées.

   Cliquez sur **[!UICONTROL Rejeter la traduction]** ![rejeter la traduction](assets/do-not-localize/thumb-down.png) pour conserver la version traduite d’origine du fichier dans la racine du paramètre régional de cible et rejeter la version modifiée.

1. Pour vue des métadonnées traduites, accédez à la console [!DNL Assets] et ouvrez la page [!UICONTROL Propriétés] pour chacun des fichiers traduits.

## Conseils et restrictions {#tips-limitations}

* Si vous lancez un processus de traduction pour des ressources complexes, telles que des fichiers PDF et [!DNL Adobe InDesign], leurs sous-ressources ou rendus (le cas échéant) ne sont pas envoyés pour traduction.
* Si vous utilisez la traduction automatique, les fichiers binaires ne sont pas traduits.
