---
title: Projet de création et intégration à PIM
seo-title: Projet de création et intégration à PIM
description: La fonction Projet de création simplifie l’ensemble du worfklow de séance photo, notamment la génération d’une demande de séance photo, le transfert d’une séance photo, la collaboration sur une séance photo et le regroupement des ressources approuvées
seo-description: La fonction Projet de création simplifie l’ensemble du worfklow de séance photo, notamment la génération d’une demande de séance photo, le transfert d’une séance photo, la collaboration sur une séance photo et le regroupement des ressources approuvées
uuid: 09f27d36-e725-45cb-88d1-27383aedceed
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: projects
content-type: reference
discoiquuid: 0e5d0a45-c663-4d91-b793-03d39119d103
translation-type: tm+mt
source-git-commit: cec6c4f9a1a75eb049dd4b8461c36c8d58d46f79
workflow-type: tm+mt
source-wordcount: '3013'
ht-degree: 70%

---


# Projet de création et intégration à PIM{#creative-project-and-pim-integration}

Si vous êtes spécialiste du marketing ou de la création, vous pouvez utiliser les outils de projet créatif de Adobe Experience Manager (AEM) pour gérer la photographie de produit liée au commerce électronique et les processus créatifs associés au sein de votre entreprise.

En particulier, vous pouvez utiliser la fonction Projet de création pour simplifier les tâches suivantes du worfklow de séance photo :

* Génération d’une demande de séance photo
* Transfert d’une séance photo
* Collaboration sur une séance photo
* Regroupement des ressources approuvées

>[!NOTE]
>
>Voir [Rôles d’utilisateur dans un projet](/help/sites-authoring/projects.md#user-roles-in-a-project) pour plus d’informations sur l’affectation des rôles d’utilisateur et des workflows à certains types d’utilisateurs.

## Exploration des workflows de séance photo de produit  {#exploring-product-photo-shoot-workflows}

La fonction Projet de création fournit divers modèles de projet pour satisfaire aux différentes exigences des projets. Le modèle **Projet de séance photo du produit** est prêt à l’emploi. Ce modèle inclut des workflows de séance photo qui permettent de lancer et de gérer des demandes de séance photo de produit. Il comprend également une série de tâches qui vous permettent d’obtenir des images numériques des produits par l’intermédiaire de processus de révision et d’approbation appropriés.

Le modèle comporte les workflows suivants :

* **Séance photo du produit (intégration de commerce)** : ce worfklow tire parti de l’intégration de commerce avec le système de gestion des informations produit (PIM) afin de générer automatiquement une liste de plans pour les produits sélectionnés (hiérarchie). Vous pouvez afficher les données de produit parmi les métadonnées des ressources une fois que le worfklow est terminé.
* **Séance photo du produit** : ce worfklow vous permet de fournir une liste de plans au lieu de dépendre de l’intégration de commerce. Il mappe les images transférées à un fichier CSV dans le dossier des ressources du projet.

>[!NOTE]
>
>Le fichier CSV transféré dans la tâche Transférer la liste de plans du worfklow Séance photo du produit doit avoir pour nom shotlist.csv.

## Création d’un projet de séance photo du produit {#create-a-product-photo-shoot-project}

1. In the **Projects** console, tap/click **Create** and then choose **Create Project** from the list.

   ![chlimage_1-132](assets/chlimage_1-132a.png)

1. Sur la page **Créer un projet**, sélectionnez un modèle de projet de séance photo et appuyez/cliquez sur **Suivant**.

   ![chlimage_1-133](assets/chlimage_1-133a.png)

1. Saisissez les détails du projet, y compris le titre, la description et l’échéance. Ajoutez des utilisateurs et affectez-leur les différents rôles. Vous pouvez également ajouter une vignette au projet.

   ![chlimage_1-134](assets/chlimage_1-134a.png)

1. Cliquez/appuyez sur **Créer**. Un message de confirmation indique que le projet est créé.
1. Tap/click **Done** to return to the **Projects** console. Alternatively, tap/click **Open** to view the assets within the photoshoot project.

## Commencer à travailler dans un projet de séance photo du produit {#starting-work-in-a-product-photo-shoot-project}

Pour lancer une demande de séance photo, appuyez ou cliquez sur un projet, puis sur **Ajouter un travail** dans la page des détails du projet afin de démarrer un worfklow.

![chlimage_1-135](assets/chlimage_1-135a.png)

Un projet de séance photo du produit comprend les workflows prêts à l’emploi suivants :

* Worfklow Séance photo du produit (Intégration de commerce)
* Worfklow Séance photo du produit

Utilisez le worfklow Séance photo du produit (Intégration de commerce) pour associer les ressources d’images aux produits d’AEM. Ce worfklow tire parti de l’intégration de commerce pour lier les images approuvées aux données de produit existantes à l’emplacement */etc/commerce*.

Le flux de travaux de prise de vue photo de produit (intégration commerciale) comprend les tâches suivantes :

* Créer une liste de plans
* Transférer la séance photo
* Retoucher la séance photo
* Réviser et approuver
* Déplacer vers la tâche de production

Si les informations produit ne sont pas disponibles dans AEM, utilisez le worfklow Séance photo du produit pour associer les ressources d’images aux produits en fonction des détails que vous transférez dans un fichier CSV. Le fichier CSV doit contenir des informations de base sur le produit, telles que l’ID de produit, la catégorie et la description. Le worfklow récupère les ressources approuvées pour les produits.

Ce worfklow implique les tâches suivantes :

* Transférer la liste de plans
* Transférer la séance photo
* Retoucher la séance photo
* Réviser et approuver
* Déplacer vers la tâche de production

Vous pouvez personnaliser ce worfklow à l’aide de l’option de configuration de workflows.

Les deux workflows incluent des étapes pour lier les produits à leurs ressources approuvées. Chaque worfklow comprend les étapes suivantes :

* Configuration de workflows : décrit les options pour personnaliser le worfklow.
* Lancement d’un worfklow de projet : explique comment lancer une séance photo du produit.
* Détails des tâches de worfklow : fournit le détail des tâches disponibles dans le worfklow.

## Suivi de la progression du projet   {#tracking-project-progress}

Vous pouvez effectuer le suivi de l’avancement d’un projet en consultant les tâches actives/terminées au sein d’un projet.

Utilisez les éléments suivants pour surveiller la progression d’un projet :

* **Carte des tâches**

* **Liste de tâches**

La carte de Tâche illustre l&#39;avancement général du projet. Elle s’affiche sur la page Détails du projet si celui-ci contient des tâches associées. La carte des tâches affiche l’état d’achèvement actuel du projet en fonction du nombre de tâches terminées. Elle n’inclut pas les tâches ultérieures.

La carte des tâches contient les informations suivantes :

* Pourcentage de tâches actives
* Pourcentage de tâches terminées

![chlimage_1-136](assets/chlimage_1-136a.png)

La liste de tâches fournit des informations détaillées sur la tâche active du worfklow pour le projet. Pour afficher la liste, appuyez/cliquez sur la carte des tâches. La liste de tâches affiche également des métadonnées telles que la date de début, l’échéance, le cessionnaire, la priorité et l’état de la tâche.

![chlimage_1-137](assets/chlimage_1-137a.png)

## Configuration du worfklow {#workflow-configuration}

Cette tâche consiste à affecter des étapes de worfklow aux utilisateurs en fonction de leurs rôles.

Pour configurer le worfklow **Séance photo du produit** :

1. Navigate to **Tools** > **Workflows**, and then tap the **Models** tile to open the **Workflow Models** page.
1. Select the **Product Photo Shoot** workflow, and the tap the **Edit** icon from the toolbar to open it in edit mode.

   ![chlimage_1-138](assets/chlimage_1-138a.png)

1. In the **Product Photo Shoot Workflow** page, open a project task. Par exemple, ouvrez la tâche **Transférer la liste de plans**.

   ![chlimage_1-139](assets/chlimage_1-139a.png)

1. Cliquez sur l’onglet **Tâche** pour configurer ce qui suit :

   * Le nom de la tâche
   * L’utilisateur par défaut (rôle) qui reçoit la tâche
   * La priorité par défaut de la tâche, qui est affichée dans la liste de tâches de l’utilisateur
   * La description de la tâche à afficher lorsque le cessionnaire ouvre la tâche
   * L’échéance d’une tâche qui est calculée en fonction de l’heure de démarrage de la tâche

1. Cliquez sur **OK** pour enregistrer les paramètres de configuration.

   De même, vous pouvez configurer les tâches suivantes pour le worfklow **Séance photo du produit** :

   * Transférer la séance photo
   * Retoucher la séance photo
   * Critique de la séance photo
   * Déplacer vers la production

   Perform a similar procedure to configure the tasks in the **Product Photo Shoot (Commerce Integration) workflow**.

Cette section décrit comment intégrer la gestion des informations produit (PIM) à votre projet de création.

## Démarrage d’un worfklow de projet {#starting-a-project-workflow}

1. Navigate to a Product Photo Shoot project, and tap/click the **Add Work** icon on the **Workflows** card.
1. Sélectionnez le worfklow **Séance photo du produit (Intégration de commerce)** pour le démarrer. If the product information isn&#39;t available under /etc/commerce, select the **Product Photo Shoot** workflow and start the Product Photo Shoot workflow.

   ![chlimage_1-140](assets/chlimage_1-140a.png)

1. Appuyez/cliquez sur **Suivant** pour lancer le worfklow au sein du projet.
1. Saisissez les détails du worfklow sur la page suivante.

   ![chlimage_1-141](assets/chlimage_1-141a.png)

   Cliquez sur **Envoyer** pour démarrer le worfklow de séance photo. La page de détails du projet de séance photo s’affiche.

   ![chlimage_1-142](assets/chlimage_1-142a.png)

### Détails des tâches de worfklow {#workflow-tasks-details}

Le worfklow de séance photo comprend plusieurs tâches. Chaque tâche est affectée à un groupe d’utilisateurs en fonction de la configuration définie pour la tâche.

#### Tâche Créer une liste de plans {#create-shot-list-task}

La tâche **Créer une liste de plans** permet au propriétaire du projet de sélectionner les produits pour lesquels des images sont requises. Selon l’option sélectionnée par l’utilisateur, un fichier CSV est généré avec les informations de base sur les produits.

1. In the project folder, tap/click the ellipses in the [Tasks Card](#tracking-project-progress) to view the task item in the workflow.

   ![chlimage_1-143](assets/chlimage_1-143a.png)

1. Select the **Create Shot List** task, and then tap/click the **Open** icon from the toolbar.

   ![chlimage_1-144](assets/chlimage_1-144a.png)

1. Passez en revue les détails de la tâche, puis appuyez/cliquez sur le bouton **Créer une liste de plans**.

   ![chlimage_1-145](assets/chlimage_1-145a.png)

1. Sélectionnez les produits pour lesquels des données de produit existent sans images associées.

   ![chlimage_1-146](assets/chlimage_1-146a.png)

1. Tap/click the **Add To Shotlist** icon to create a CSV file that contains a list of all such products. Un message confirme que la liste de plans est créée pour les produits sélectionnés. Cliquez sur **Fermer** pour terminer le worfklow.
1. Une fois la liste de plans créée, le lien **Afficher la liste de plans** apparaît. To add more products to the shot list, tap/click **Add to Shot List**. Dans ce cas, les données sont ajoutées à la liste de plans créée.

   ![chlimage_1-147](assets/chlimage_1-147a.png)

1. Appuyez/cliquez sur **Afficher la liste de plans** afin d’afficher la liste de plans qui vient d’être créée.

   ![chlimage_1-148](assets/chlimage_1-148a.png)

   Pour modifier les données existantes ou ajouter de nouvelles données, appuyez/cliquez sur **Modifier** dans la barre d’outils. Only the **Product **and **Description** fields are editable.

   ![chlimage_1-149](assets/chlimage_1-149a.png)

   After you update the file, tap/click **Save** on toolbar to save the file.

1. After adding the products, tap/click the **Complete** icon on the **Create Shot List **task details page to mark the task as completed. Vous pouvez ajouter un commentaire (facultatif).

   La fin de la tâche apporte les modifications suivantes au sein du projet :

   * Les ressources correspondant à la hiérarchie de produit sont créées dans un dossier portant le même nom que le titre du worfklow.
   * Les métadonnées des ressources peuvent être modifiées depuis la console Ressources, avant même que le photographe ne fournisse les images.
   * Un dossier Séance photo est créé pour stocker les images fournies par le photographe. Ce dossier contient des sous-dossiers pour chaque entrée de produit figurant dans la liste de plans.

   Transférer la liste de plans est la première tâche du worfklow Séance photo du produit (sans intégration de commerce). Appuyez/cliquez sur **Transférer la liste de plans** pour transférer un fichier **shotlist.csv**. Le fichier CSV doit contenir l’ID du produit. Les autres champs sont facultatifs. Vous pouvez les utiliser pour mapper les ressources aux produits.

### Transférer une tâche de liste de plans {#upload-shot-list-task}

Cette tâche fait partie du worfklow Séance photo du produit. Vous effectuez cette tâche si les informations produit ne sont pas disponibles dans AEM. Dans ce cas, vous transférez dans un fichier CSV la liste des produits pour lesquels des ressources d’images sont requises. En fonction des détails contenus dans le fichier CSV, vous mappez les fichiers d’image aux produits.

Utilisez le lien **Afficher la liste de plans** sous la carte du projet de la procédure précédente pour télécharger un exemple de fichier CSV. Consultez le fichier d’exemple pour connaître le contenu habituel d’un fichier CSV.

La liste de produits ou le fichier CSV peut contenir des champs, tels que **Catégorie, Produit, ID, Description** et **Chemin d’accès**. Le champ **ID** est obligatoire et contient l’ID du produit. Les autres champs sont facultatifs.

Un produit peut appartenir à une catégorie particulière. La catégorie du produit peut être indiquée dans le fichier CSV sous la colonne **Catégorie**. Le champ **Produit** contient le nom du produit. Dans le champ **Description**, saisissez la description du produit ou les instructions pour le photographe.

>[!NOTE]
>
>The name of images to be uploaded should start with &quot;**&lt;ProductId>_&quot;** where Product ID is referenced from the **Id** field in the *shotlist.csv* file. For example, for a product in the shot list with **Id 397122**, you can upload files with names **397122_highcontrast.jpg**, **397122_lowlight.png**, and so on.

1. In the project folder, tap/click the ellipses in the [Tasks Card](#tracking-project-progress) to view the list of tasks in the workflow.
1. Select the **Upload Shot List** task, and then tap/click the **Open** icon from the toolbar.

   ![chlimage_1-150](assets/chlimage_1-150a.png)

1. Review the task details and then tap/click the **Upload Shot List** button.

   ![chlimage_1-151](assets/chlimage_1-151a.png)

1. Tap/click the **Upload Shot List** button to upload the CSV file with filename shotlist.csv. Le worfklow identifie ce fichier comme la source à utiliser pour extraire les données de produit de la tâche suivante.
1. Transférez un fichier CSV contenant des informations sur les produits au format approprié. The **View Uploaded Assets** link appears under the card after the CSV file is uploaded.

   ![chlimage_1-152](assets/chlimage_1-152a.png)

   Cliquez sur l’icône **Terminé** pour terminer la tâche.

1. Tap/click the **Complete** icon to complete the task.

### Tâche Transférer la séance photo {#upload-photo-shoot-task}

If you are an Editor, you can upload shots for the products listed in the **shotlist.csv** file that is created or uploaded in the previous task.

The name of images to be uploaded should begin with **&quot;&lt;productId>_&quot;** where Product ID is referenced from the **Id** field in the **shotlist.csv** file. Par exemple, pour un produit dans la liste de plans portant l’**ID 397122**, vous pouvez transférer des fichiers avec les noms **397122_fortcontraste.jpg**, **397122_faibleluminosité.png**, etc.

Vous pouvez transférer les images directement ou transférer un fichier ZIP contenant les images. En fonction de leurs noms, les images sont placées à l’intérieur des dossiers de leurs produits respectifs au sein du dossier **Séance photo**.

1. Under the project folder, tap/click the ellipses in the [Task Card](#tracking-project-progress) to view the task item in the workflow.
1. Select the **Upload Photo Shoot** task, and then tap/click the **Open** icon from the toolbar.

   ![chlimage_1-153](assets/chlimage_1-153a.png)

1. Tap/click **Upload Photo Shoot** and upload the photo shoot images.
1. Appuyez/cliquez sur l’icône **Terminé** de la barre d’outils pour terminer la tâche.

### Tâche Retoucher la séance photo {#retouch-photo-shoot-task}

Si vous disposez de droits de modification, effectuez la tâche Retoucher la séance photo afin de modifier les images transférées dans le dossier Séance photo.

1. Under the project folder, tap/click the ellipses in the [Task Card](#tracking-project-progress) to view the task item in the workflow.
1. Select the **Retouch Photo Shoot** task, and then tap/click the **Open** icon from the toolbar.

   ![chlimage_1-154](assets/chlimage_1-154a.png)

1. Tap/click the **View Uploaded Assets** link in the **Retouch Photo Shoot** page to browse the uploaded images.

   ![chlimage_1-155](assets/chlimage_1-155a.png)

   Si nécessaire, modifiez les images à l’aide d’une application Adobe Creative Cloud.

   ![chlimage_1-156](assets/chlimage_1-156a.png)

1. Appuyez/cliquez sur l’icône **Terminé** de la barre d’outils pour terminer la tâche.

### Tâche Réviser et approuver {#review-and-approve-task}

Cette tâche consiste à réviser les images de la séance photo transférées par un photographe et à les marquer comme approuvées pour utilisation.

1. Under the project folder, tap/click the ellipses in the [Task Card](#tracking-project-progress) to view the task item in the workflow.
1. Select the **Review &amp; Approve** task, and then tap/click the **Open** icon from the toolbar.

   ![chlimage_1-157](assets/chlimage_1-157a.png)

1. In the **Review &amp; Approve** page, assign the review task to role, for example Reviewers, and then tap/click **Review **to start reviewing the uploaded product images.

   ![chlimage_1-158](assets/chlimage_1-158a.png)

1. Sélectionnez une image de produit, puis appuyez/cliquez sur l’icône Approuver de la barre d’outils pour la marquer comme approuvée.

   ![chlimage_1-159](assets/chlimage_1-159a.png)

   Une fois que vous avez approuvé une image, une bannière « Approuvée » s’affiche par-dessus.

   >[!NOTE]
   Vous pouvez laisser certains produits sans image. Vous pouvez revenir ultérieurement sur la tâche et la marquer comme complète lorsque vous avez terminé.

1. Appuyez/cliquez sur **Terminé**. Les images approuvées sont liées aux ressources vides qui ont été créées.

Vous pouvez accéder aux ressources du projet à l’aide de l’interface utilisateur Ressources et vérifier les images approuvées.

Appuyez/cliquez sur Suivant pour visualiser les produits selon votre hiérarchie de données de produit.

La fonction Projet de création associe les ressources approuvées au produit référencé. Les métadonnées de la ressource sont mises à jour avec les informations de base et la référence du produit sous l’onglet **Données de produit** sous Propriétés de l’élément et elles apparaissent dans la section Métadonnées des ressources AEM.

>[!NOTE]
Dans le worfklow Séance photo du produit (sans intégration de commerce), les images approuvées n’ont aucune association avec des produits.

### Déplacer vers la tâche de production {#move-to-production-task}

Cette tâche déplace les ressources approuvées dans le dossier Prêt pour la production de manière à pouvoir les utiliser.

1. Under the project folder, tap/click the ellipses in the [Task Card](#tracking-project-progress) to view the task item in the workflow.
1. Select the **Move to Production** task, and then tap/click the **Open** icon from the toolbar.

   ![chlimage_1-160](assets/chlimage_1-160a.png)

1. Pour afficher les ressources approuvées pour la séance photo avant de les déplacer dans le dossier Prêt pour production, cliquez sur le lien **Afficher les ressources approuvées** situé au-dessous de la miniature du projet sur la page de la tâche **Déplacer vers la production**.

   ![chlimage_1-161](assets/chlimage_1-161a.png)

1. Enter the path of the production-ready folder in the **Move To** field.

   ![chlimage_1-162](assets/chlimage_1-162a.png)

   Tap/click **Move to Production**. Fermez le message de confirmation. Les ressources sont déplacées dans le chemin spécifié et une visionneuse à 360° est créée automatiquement pour les ressources approuvées pour chaque produit en fonction de la hiérarchie des dossiers.

1. Appuyez/cliquez sur l’icône **Terminé** dans la barre d’outils. Le worfklow se termine et la dernière étape est marquée comme étant terminée.

## Affichage des métadonnées des ressources de gestion des actifs numériques {#viewing-dam-asset-metadata}

Après votre approbation, les ressources sont liées aux produits correspondants. La [page des propriétés](/help/assets/manage-assets.md#editing-properties) des ressources approuvées comprend maintenant un nouvel onglet **Données du produit** (les informations sur les produits liés) Cet onglet affiche les détails du produit, le numéro SKU ainsi que d’autres détails relatifs au produit lié à la ressource. Appuyez/cliquez sur l’icône **Modifier** pour mettre à jour une propriété de ressource. Les informations relatives aux produits restent en lecture seule.

Appuyez/cliquez sur le lien qui s’affiche pour accéder à la page des détails du produit correspondante dans la console du produit à laquelle la ressource est associée.

## Personnalisation des worfklow de séance photo du projet {#customizing-the-project-photo-shoot-workflows}

Vous pouvez personnaliser les workflows de travaux de séance photo du projet en fonction de vos besoins. Il s’agit d’une tâche facultative, et basée sur les rôles, que vous effectuez pour définir la valeur d’une variable au sein du projet. Vous pouvez ensuite utiliser ultérieurement la valeur configurée pour prendre une décision.

1. Click/tap the AEM logo, and then navigate to **Tools** > **Workflow** > **Models** to open the Workflow Models page.
1. Sélectionnez le worfklow **Séance photo du produit (Intégration de commerce)** ou **Séance photo du produit**, et cliquez/appuyez sur **Modifier** dans la barre d’outils pour ouvrir le worfklow en mode d’édition.
1. Ouvrez les tâches **Projets** dans le sidekick, puis faites glisser l’étape **Créer une tâche de projet en fonction du rôle** dans le worfklow.

   ![chlimage_1-163](assets/chlimage_1-163a.png)

1. Open the **Role Based Task** step.
1. Sous l’onglet **Tâche**, saisissez le nom de la tâche qui s’affichera dans la liste **Tâche**. Vous pouvez également attribuer la tâche à un rôle, définir la priorité par défaut, fournir une description et spécifier l’heure d’échéance de la tâche.

   ![chlimage_1-164](assets/chlimage_1-164a.png)

1. Sous l’onglet **Acheminement**, spécifiez les actions pour la tâche. Pour ajouter plusieurs actions, appuyez/cliquez sur le lien **Ajouter l’élément **lien.

   ![chlimage_1-165](assets/chlimage_1-165a.png)

1. After adding the options click **OK** to add the changes to the step.

   >[!NOTE]
   Tapping/clicking **OK** does not save the changes in the workflow. Pour enregistrer les modifications dans le worfklow, appuyez/cliquez sur **Enregistrer**.

1. Open the **Workflow** tasks from side kick, and add a **Goto** task.
1. Ouvrez la tâche **Atteindre** et appuyez/cliquez sur l’onglet **Processus**.
1. Saisissez le code suivant dans la zone **Script** :

```
   function check() {

   if (workflowData.getMetaDataMap().get("lastTaskAction","") == "Reject All") {

   return true

   }

   // set copywriter user in metadata

   var previousId = workflowData.getMetaDataMap().get("lastTaskCompletedBy", "");

   workflowData.getMetaDataMap().put("copywriter", previousId);

   return false;

   }
```

>[!NOTE]
For details around scripting in workflow steps, see [Defining a Rule for an OR Split](/help/sites-developing/workflows-models.md).

![chlimage_1-166](assets/chlimage_1-166a.png)

1. Appuyez/cliquez sur **OK**.

1. Tap/click **Save** to save the workflow.

   ![chlimage_1-167](assets/chlimage_1-167a.png)

1. A new Project owner acceptance task now comes up after the [Move to Production task](#move-to-production-task) is completed and is assigned to the owner.

   L’utilisateur avec le rôle de propriétaire peut terminer la tâche et sélectionner une action (parmi la liste des actions ajoutées dans les configurations d’étape de worfklow) à partir de la liste dans la fenêtre contextuelle de commentaires.

   ![chlimage_1-168](assets/chlimage_1-168a.png)

   Sélectionnez l’option appropriée et cliquez sur **Terminer** pour exécuter **Atteindre l’étape** dans le worfklow.

>[!NOTE]
When you start a server, the Project task list servlet caches the mappings between task types and URLs defined under `/libs/cq/core/content/projects/tasktypes`. You can then perform the usual overlay and add custom task types by placing them under `/apps/cq/core/content/projects/tasktypes`.

