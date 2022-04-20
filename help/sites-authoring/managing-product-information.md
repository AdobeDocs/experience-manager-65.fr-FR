---
title: Projet de création et intégration à PIM
seo-title: Creative Project and PIM Integration
description: La fonction Projet de création simplifie l’ensemble du worfklow de séance photo, notamment la génération d’une demande de séance photo, le transfert d’une séance photo, la collaboration sur une séance photo et le regroupement des ressources approuvées
seo-description: Creative Project streamlines the entire photo shoot workflow that including generating a photo shoot request, uploading a photo shoot, collaborating on a photo shoot, and packaging approved assets
uuid: 09f27d36-e725-45cb-88d1-27383aedceed
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: projects
content-type: reference
discoiquuid: 0e5d0a45-c663-4d91-b793-03d39119d103
exl-id: c4eff50e-0d55-4a61-98fd-cc42138656cb
source-git-commit: 200b47070b7ead54ee54eea504bd960d4e0731d9
workflow-type: tm+mt
source-wordcount: '2989'
ht-degree: 40%

---


# Projet de création et intégration à PIM {#creative-project-and-pim-integration}

Si vous êtes un professionnel du marketing ou de la création, vous pouvez utiliser les outils de projet créatif d’Adobe Experience Manager (AEM) pour gérer la photographie de produit liée au commerce électronique et les processus créatifs associés au sein de votre entreprise.

Vous pouvez utiliser le projet créatif pour rationaliser les tâches suivantes dans votre workflow de séance photo :

* Génération d’une demande de séance photo
* Transfert d’une séance photo
* Collaboration sur une séance photo
* Regroupement des ressources approuvées

>[!NOTE]
>
>Voir [Rôles d’utilisateur dans un projet](/help/sites-authoring/projects.md#user-roles-in-a-project) pour plus d’informations sur l’affectation des rôles d’utilisateur et des workflows à certains types d’utilisateurs.

## Workflows de séance photo du produit  {#exploring-product-photo-shoot-workflows}

La fonction Projet de création fournit divers modèles de projet pour satisfaire aux différentes exigences des projets. Le modèle **Projet de séance photo du produit** est prêt à l’emploi. Ce modèle inclut des workflows de séance photo qui permettent de lancer et de gérer des demandes de séance photo de produit. Il comprend également une série de tâches qui vous permettent d’obtenir des images numériques des produits par l’intermédiaire de processus de révision et d’approbation appropriés.

## Création d’un projet de séance photo de produit {#create-a-product-photo-shoot-project}

1. Dans le **Projets** console, appuyez ou cliquez sur **Créer** puis choisissez **Créer un projet** dans la liste.

   ![Bouton Créer un projet](assets/chlimage_1-132a.png)

1. Dans le **Créer un projet** , sélectionnez **Projet de séance photo du produit** modèle et appuyez ou cliquez sur **Suivant**.

   ![Assistant de projet](assets/chlimage_1-133a.png)

1. Saisissez les détails du projet, y compris le titre, la description et l’échéance. Ajoutez des utilisateurs et affectez-leur les différents rôles. Vous pouvez également ajouter une vignette au projet.

   ![Détails du projet](assets/chlimage_1-134a.png)

1. Appuyez ou cliquez sur **Créer**. Un message de confirmation indique que le projet est créé.
1. Appuyez ou cliquez sur **Terminé** pour revenir au **Projets** console. Vous pouvez également appuyer ou cliquer sur **Ouvrir** pour afficher les ressources du projet.

## Commencer à travailler dans un projet de séance photo du produit {#starting-work-in-a-product-photo-shoot-project}

Pour lancer une demande de séance photo, appuyez ou cliquez sur un projet, puis appuyez ou cliquez sur **Ajouter un travail** dans la page des détails du projet pour démarrer un workflow.

![Ajouter un travail](assets/chlimage_1-135a.png)

A **Projet de séance photo du produit** inclut les workflows d’usine suivants :

* **Workflow Séance photo du produit (Intégration de commerce)**: Ce workflow exploite l’intégration commerciale au système de gestion de l’information sur les produits (PIM) pour générer automatiquement une liste de plans pour les produits sélectionnés (hiérarchie). Vous pouvez afficher les données de produit parmi les métadonnées des ressources une fois que le worfklow est terminé.
* **Workflow de séance photo du produit**: Ce workflow permet de fournir une liste de plans plutôt que de dépendre de l&#39;intégration commerciale. Il mappe les images transférées à un fichier CSV dans le dossier des ressources du projet.

Utilisez la variable **Séance photo du produit (intégration Commerce)** workflow pour mapper les ressources image aux produits dans AEM. Ce workflow exploite l’intégration commerciale pour lier les images approuvées aux données de produit existantes à l’emplacement `/etc/commerce`.

Le **Séance photo du produit (intégration Commerce)** Le workflow comprend les tâches suivantes :

* Créer une liste de plans
* Transférer la séance photo
* Retoucher la séance photo
* Réviser et approuver
* Déplacer vers la tâche de production

Si les informations sur les produits ne sont pas disponibles dans AEM, utilisez la variable **Séance photo du produit** pour mapper des ressources image aux produits en fonction des détails que vous chargez dans un fichier CSV. Le fichier CSV doit contenir des informations de base sur le produit, telles que l’ID de produit, la catégorie et la description. Le worfklow récupère les ressources approuvées pour les produits.

Ce worfklow implique les tâches suivantes :

* Transférer la liste de plans
* Transférer la séance photo
* Retoucher la séance photo
* Réviser et approuver
* Déplacer vers la tâche de production

Vous pouvez personnaliser ce worfklow à l’aide de l’option de configuration de workflows.

Les deux workflows incluent des étapes pour lier les produits à leurs ressources approuvées. Chaque worfklow comprend les étapes suivantes :

* Configuration de workflows : décrit les options pour personnaliser le worfklow.
* Démarrage d’un workflow de projet : Explique comment démarrer une séance photo de produit
* Détails des tâches de worfklow : fournit le détail des tâches disponibles dans le worfklow.

## Suivi de la progression du projet {#tracking-project-progress}

Vous pouvez effectuer le suivi de l’avancement d’un projet en consultant les tâches actives/terminées au sein d’un projet.

Utilisez les éléments suivants pour surveiller la progression d’un projet :

* Carte des tâches
* Liste de tâches

La fiche de tâche représente la progression globale du projet. Il apparaît sur la page des détails du projet uniquement si le projet comporte des tâches associées. La carte de tâche affiche l’état d’achèvement actuel du projet en fonction du nombre de tâches terminées. Elle n’inclut pas les tâches ultérieures.

La carte de tâche fournit les détails suivants :

* Pourcentage de tâches actives
* Pourcentage de tâches terminées

![Carte des tâches](assets/chlimage_1-136a.png)

La liste des tâches fournit des informations détaillées sur la tâche de workflow actuellement principale pour le projet. Pour afficher la liste, appuyez ou cliquez sur la carte de la tâche. La liste des tâches affiche également des métadonnées telles que la date de début, l’échéance, la personne désignée, la priorité et l’état de la tâche.

![Liste de tâches](assets/chlimage_1-137a.png)

## Configuration du worfklow {#workflow-configuration}

Cette tâche consiste à affecter des étapes de worfklow aux utilisateurs en fonction de leurs rôles.

Pour configurer le worfklow **Séance photo du produit** :

1. Accédez à **Outils** > **Workflows**, puis appuyez sur le bouton **Modèles** pour ouvrir la mosaïque **Modèles de processus** page.
1. Sélectionnez la **Séance photo du produit** et appuyez sur **Modifier** dans la barre d’outils pour l’ouvrir en mode d’édition.

   ![Modèle Séance photo du produit](assets/chlimage_1-138a.png)

1. Dans le **Workflow de séance photo du produit** , ouvrez une tâche de projet. Par exemple, ouvrez la tâche **Transférer la liste de plans**.

   ![Modifier le modèle](assets/project-photo-shoot-workflow-model.png)

1. Appuyez ou cliquez sur le bouton **Tâche** pour configurer les éléments suivants :

   * Le nom de la tâche
   * L’utilisateur par défaut (rôle) qui reçoit la tâche
   * La priorité par défaut de la tâche, qui est affichée dans la liste de tâches de l’utilisateur
   * La description de la tâche à afficher lorsque le cessionnaire ouvre la tâche
   * L’échéance d’une tâche qui est calculée en fonction de l’heure de démarrage de la tâche

1. Cliquez sur **OK** pour enregistrer les paramètres de configuration.

Vous pouvez configurer les tâches supplémentaires pour la **Séance photo du produit** d’une manière similaire.

Procédez de la même manière pour configurer les tâches dans le **Workflow Séance photo du produit (Intégration de commerce)**.

## Démarrage d’un worfklow de projet {#starting-a-project-workflow}

Cette section décrit comment intégrer la gestion des informations produit (PIM) à votre projet de création.

1. Accédez à un projet de séance photo de produit, puis appuyez ou cliquez sur le bouton **Ajouter un travail** sur l’icône **Workflows** carte.
1. Sélectionnez la **Séance photo du produit (intégration Commerce)** carte de workflow pour démarrer **Séance photo du produit (intégration Commerce)** workflow. Si les informations sur le produit ne sont pas disponibles sous `/etc/commerce`, sélectionnez la variable **Séance photo du produit** et démarrez le **Séance photo du produit** workflow.

   ![Assistant de workflow](assets/chlimage_1-140a.png)

1. Appuyez ou cliquez sur **Suivant** pour lancer le workflow dans le projet.
1. Saisissez les détails du worfklow sur la page suivante.

   ![Détails du processus](assets/chlimage_1-141a.png)

1. Appuyez ou cliquez sur **Envoyer** pour démarrer le processus de séance photo. La page de détails du projet de séance photo s’affiche.

   ![Page Projet avec nouveau workflow](assets/chlimage_1-142a.png)

### Détails des tâches de worfklow {#workflow-tasks-details}

Le worfklow de séance photo comprend plusieurs tâches. Chaque tâche est affectée à un groupe d’utilisateurs en fonction de la configuration définie pour la tâche.

#### Tâche Créer une liste de plans {#create-shot-list-task}

La tâche **Créer une liste de plans** permet au propriétaire du projet de sélectionner les produits pour lesquels des images sont requises. Selon l’option sélectionnée par l’utilisateur, un fichier CSV est généré avec les informations de base sur les produits.

1. Dans le dossier du projet, appuyez ou cliquez sur le bouton représentant des points de suspension en bas à droite de l’événement [Carte des tâches](#tracking-project-progress) pour afficher l’élément de tâche dans le workflow.

   ![Carte des tâches](assets/chlimage_1-143a.png)

1. Sélectionnez la **Créer une liste de plans** , puis appuyez/cliquez sur l’icône **Ouvrir** dans la barre d’outils.

   ![Ouverture d’une tâche de liste de plans](assets/chlimage_1-144a.png)

1. Passez en revue les détails de la tâche, puis appuyez/cliquez sur le bouton **Créer une liste de plans**.

   ![Détails de la tâche de liste de plans](assets/chlimage_1-145a.png)

1. Sélectionnez les produits pour lesquels des données de produit existent sans images associées.

   ![Sélection de produits](assets/chlimage_1-146a.png)

1. Appuyez ou cliquez sur le bouton **Ajouter à la liste de plans** pour créer un fichier CSV contenant la liste de tous ces produits. Un message confirme que la liste de plans est créée pour les produits sélectionnés. Cliquez sur **Fermer** pour terminer le worfklow.

1. Une fois la liste de plans créée, le lien **Afficher la liste de plans** apparaît. Pour ajouter d’autres produits à la liste de plans, appuyez ou cliquez sur **Ajouter à la liste de plans**. Dans ce cas, les données sont ajoutées à la liste de plans créée.

   ![Ajouter à la liste de plans](assets/chlimage_1-147a.png)

1. Appuyez ou cliquez sur **Afficher la liste de plans** pour afficher la nouvelle liste de plans.

   ![Afficher la liste de plans](assets/chlimage_1-148a.png)

   Pour modifier les données existantes ou ajouter de nouvelles données, appuyez/cliquez sur **Modifier** dans la barre d’outils. Seul le **produit **et **Description** sont modifiables.

   ![Modifier la liste de plans](assets/chlimage_1-149a.png)

   Une fois le fichier mis à jour, appuyez ou cliquez sur **Enregistrer** sur la barre d’outils pour enregistrer le fichier.

1. Après avoir ajouté les produits, appuyez ou cliquez sur l’icône **Terminer** sur l’icône **Créer une liste de plans** page détails de la tâche pour marquer la tâche comme terminée. Vous pouvez ajouter un commentaire (facultatif).

La fin de la tâche apporte les modifications suivantes au sein du projet :

* Les ressources correspondant à la hiérarchie de produit sont créées dans un dossier portant le même nom que le titre du worfklow.
* Les métadonnées des ressources peuvent être modifiées depuis la console Ressources, avant même que le photographe ne fournisse les images.
* Un dossier de séance photo est créé pour stocker les images fournies par le photographe. Le dossier de séance photo contient des sous-dossiers pour chaque entrée de produit dans la liste de plans.

### Transférer une tâche de liste de plans {#upload-shot-list-task}

Cette tâche fait partie du worfklow Séance photo du produit. Vous effectuez cette tâche si les informations produit ne sont pas disponibles dans AEM. Dans ce cas, vous transférez dans un fichier CSV la liste des produits pour lesquels des ressources d’images sont requises. En fonction des détails du fichier CSV, vous mappez les ressources image avec les produits. Le fichier doit être un fichier CSV nommé `shotlist.csv`.

Utilisez le lien **Afficher la liste de plans** sous la carte du projet de la procédure précédente pour télécharger un exemple de fichier CSV. Consultez le fichier d’exemple pour connaître le contenu habituel d’un fichier CSV.

La liste de produits ou le fichier CSV peut contenir des champs, tels que **Catégorie, Produit, ID, Description** et **Chemin d’accès**. Le champ **ID** est obligatoire et contient l’ID du produit. Les autres champs sont facultatifs.

Un produit peut appartenir à une catégorie particulière. La catégorie du produit peut être indiquée dans le fichier CSV sous la colonne **Catégorie**. Le champ **Produit** contient le nom du produit. Dans le champ **Description**, saisissez la description du produit ou les instructions pour le photographe.

1. Dans le dossier du projet, appuyez ou cliquez sur le bouton représentant des points de suspension en bas à droite de l’événement [Carte des tâches](#tracking-project-progress) pour afficher la liste des tâches du workflow.
1. Sélectionnez la **Transférer la liste de plans** puis appuyez ou cliquez sur l’icône **Ouvrir** dans la barre d’outils.

   ![Télécharger la liste de plans](assets/chlimage_1-150a.png)

1. Vérifiez les détails de la tâche, puis appuyez ou cliquez sur l’icône **Transférer la liste de plans** bouton .

   ![Chargement de la liste de plans](assets/chlimage_1-151a.png)

1. Appuyez ou cliquez sur le bouton **Transférer la liste de plans** pour télécharger le fichier CSV. Le worfklow identifie ce fichier comme la source à utiliser pour extraire les données de produit de la tâche suivante.
1. Transférez un fichier CSV contenant des informations sur les produits au format approprié. Le **Affichage des ressources téléchargées** s’affiche sous la carte une fois le fichier CSV chargé.

   ![Chargement des informations sur les produits](assets/chlimage_1-152a.png)

   Cliquez sur l’icône **Terminé** pour terminer la tâche.

1. Appuyez/cliquez sur le bouton **Terminer** pour terminer la tâche.

### Tâche Transférer la séance photo {#upload-photo-shoot-task}

Si vous êtes un éditeur, vous pouvez télécharger des plans pour les produits répertoriés dans la section **shotlist.csv** fichier créé ou chargé dans la tâche précédente.

Le nom des images à télécharger doit commencer par `<ProductId_>` where `ProductId` est référencé à partir de la fonction **Id** dans le champ `shotlist.csv` fichier . Par exemple, pour un produit de la liste de plans avec **Id** `397122`, vous téléchargerez des fichiers avec des noms `397122_highcontrast.jpg`, `397122_lowlight.png`, etc.

Vous pouvez transférer les images directement ou transférer un fichier ZIP contenant les images. En fonction de leurs noms, les images sont placées dans les dossiers de produits respectifs dans le dossier de séance photo.

1. Sous le dossier du projet, appuyez ou cliquez sur le bouton représentant des points de suspension en bas à droite de l’objet [Task Card](#tracking-project-progress) pour afficher l’élément de tâche dans le workflow.
1. Sélectionnez la **Télécharger la séance photo** puis appuyez ou cliquez sur l’icône **Ouvrir** dans la barre d’outils.

   ![Télécharger la séance photo](assets/chlimage_1-153a.png)

1. Appuyez ou cliquez sur **Télécharger la séance photo** et téléchargez les photos de la séance photo.
1. Appuyez ou cliquez sur le bouton **Terminer** dans la barre d’outils pour terminer la tâche.

### Tâche Retoucher la séance photo {#retouch-photo-shoot-task}

Si vous disposez de droits de modification, effectuez l’opération **Retoucher la séance photo** tâche de modification des images téléchargées dans le dossier de la séance photo.

1. Sous le dossier du projet, appuyez ou cliquez sur le bouton représentant des points de suspension en bas à droite de l’événement [Task Card](#tracking-project-progress) pour afficher l’élément de tâche dans le workflow.
1. Sélectionnez la **Retoucher la séance photo** , puis appuyez/cliquez sur l’icône **Ouvrir** dans la barre d’outils.

   ![Retoucher la séance photo](assets/chlimage_1-154a.png)

1. Appuyez ou cliquez sur le bouton **Affichage des ressources téléchargées** dans le **Retoucher la séance photo** pour parcourir les images téléchargées.

   ![Affichage des ressources chargées](assets/chlimage_1-155a.png)

   Si nécessaire, modifiez les images à l’aide d’une application Adobe Creative Cloud.

   ![Modifier une ressource](assets/chlimage_1-156a.png)

1. Appuyez ou cliquez sur le bouton **Terminer** dans la barre d’outils pour terminer la tâche.

### Tâche Réviser et approuver {#review-and-approve-task}

Cette tâche consiste à réviser les images de la séance photo transférées par un photographe et à les marquer comme approuvées pour utilisation.

1. Sous le dossier du projet, appuyez ou cliquez sur le bouton représentant des points de suspension en bas à droite de l’objet [Task Card](#tracking-project-progress) pour afficher l’élément de tâche dans le workflow.
1. Sélectionnez la **Réviser et approuver** puis appuyez ou cliquez sur l’icône **Ouvrir** dans la barre d’outils.

   ![Réviser et approuver](assets/chlimage_1-157a.png)

1. Dans le **Réviser et approuver** , affectez une tâche de révision à un rôle, puis appuyez ou cliquez sur **Réviser** pour commencer à consulter les images de produit chargées.

   ![Commencer à vérifier les ressources](assets/chlimage_1-158a.png)

1. Sélectionnez une image de produit, puis appuyez ou cliquez sur l’icône **Approuver** dans la barre d’outils pour la marquer comme approuvée. Une fois que vous avez approuvé une image, une bannière « Approuvée » s’affiche par-dessus.

   ![Valider une image](assets/chlimage_1-159a.png)

1. Appuyez ou cliquez sur **Terminer**. Les images approuvées sont liées aux ressources vides qui ont été créées.

Vous pouvez laisser certains produits sans image. Vous pouvez revenir ultérieurement sur la tâche et la marquer comme complète lorsque vous avez terminé.

Vous pouvez accéder aux ressources du projet à l’aide de l’interface utilisateur Ressources et vérifier les images approuvées.

Appuyez ou cliquez sur le niveau suivant pour afficher les produits selon votre hiérarchie de données de produit.

La fonction Projet de création associe les ressources approuvées au produit référencé. Les métadonnées de la ressource sont mises à jour avec les informations de base et la référence du produit sous l’onglet **Données de produit** sous Propriétés de l’élément et elles apparaissent dans la section Métadonnées des ressources AEM.

>[!NOTE]
>
>Dans le **Workflow Séance photo du produit** (sans intégration de commerce), les images approuvées n’ont aucune association avec les produits.

### Déplacer vers la tâche de production {#move-to-production-task}

Cette tâche déplace les ressources approuvées dans le dossier Prêt pour la production de manière à pouvoir les utiliser.

1. Sous le dossier du projet, appuyez ou cliquez sur le bouton représentant des points de suspension en bas à droite de l’objet [Task Card](#tracking-project-progress) pour afficher l’élément de tâche dans le workflow.
1. Sélectionnez la **Déplacer vers la production** puis appuyez ou cliquez sur l’icône **Ouvrir** dans la barre d’outils.

   ![Déplacer vers la production](assets/chlimage_1-160a.png)

1. Pour afficher les ressources approuvées pour la séance photo avant de les déplacer dans le dossier Prêt pour production, cliquez sur le lien **Afficher les ressources approuvées** situé au-dessous de la miniature du projet sur la page de la tâche **Déplacer vers la production**.

   ![Déplacer vers la page de tâche de production](assets/chlimage_1-161a.png)

1. Saisissez le chemin d’accès au dossier prêt pour la production dans le champ **Déplacer vers** champ .

   ![Déplacer vers le chemin](assets/chlimage_1-162a.png)

1. Appuyez ou cliquez sur **Déplacer vers la production**. Fermez le message de confirmation. Les ressources sont déplacées vers le chemin d’accès mentionné et une visionneuse à 360° est automatiquement créée pour les ressources approuvées pour chaque produit en fonction de la hiérarchie des dossiers.

1. Appuyez/cliquez sur l’icône **Terminé** dans la barre d’outils. Le worfklow se termine et la dernière étape est marquée comme étant terminée.

## Affichage des métadonnées des ressources de gestion des actifs numériques {#viewing-dam-asset-metadata}

Après votre approbation, les ressources sont liées aux produits correspondants. La [page des propriétés](/help/assets/manage-assets.md#editing-properties) des ressources approuvées comprend maintenant un nouvel onglet **Données du produit** (les informations sur les produits liés) Cet onglet affiche les détails du produit, le numéro SKU ainsi que d’autres détails relatifs au produit lié à la ressource. Appuyez ou cliquez sur le bouton **Modifier** pour mettre à jour une propriété de ressource. Les informations relatives aux produits restent en lecture seule.

Appuyez ou cliquez sur le lien qui s’affiche pour accéder à la page des détails du produit correspondante dans la console du produit à laquelle la ressource est associée.

## Personnalisation des worfklow de séance photo du projet {#customizing-the-project-photo-shoot-workflows}

Vous pouvez personnaliser la variable **Séance photo du projet** workflows selon vos besoins. Il s’agit d’une tâche facultative, et basée sur les rôles, que vous effectuez pour définir la valeur d’une variable au sein du projet. Vous pouvez ensuite utiliser ultérieurement la valeur configurée pour prendre une décision.

1. Cliquez ou appuyez sur le logo AEM, puis accédez à **Outils** > **Workflow** > **Modèles** pour ouvrir le **Modèles de processus** page.
1. Sélectionnez la **Séance photo du produit (intégration Commerce)** ou le workflow **Séance photo du produit** workflow et clic ou appui **Modifier** de la barre d’outils pour ouvrir le workflow en mode d’édition.
1. Ouvrez le panneau latéral et localisez le **Créer une tâche de projet basée sur un rôle** et faites-le glisser sur le workflow.

   ![Création d’une tâche de projet basée sur les rôles](assets/project-model-role-based.png)

1. Ouvrez le **Tâche basée sur les rôles** étape .
1. Sur le **Tâche** indiquez un nom pour la tâche qui s’affichera dans la liste des tâches. Vous pouvez également affecter la tâche à un rôle, définir la priorité par défaut, fournir une description et spécifier l’heure d’échéance de la tâche.

   ![Configuration de l’étape du workflow](assets/project-task-step.png)

1. Sur le **Routage** , spécifiez les actions de la tâche. Pour ajouter plusieurs actions, appuyez ou cliquez sur le bouton **Ajouter un élément** lien.

   ![Onglet Routage](assets/project-task-step-routing.png)

1. Après avoir ajouté les options, cliquez sur **OK** pour ajouter les modifications à l’étape.

1. De retour dans le **Modèle de workflow** appuyez ou cliquez sur la fenêtre **Synchronisation** pour enregistrer les modifications de l’ensemble du workflow. Appuyez ou cliquez sur **OK** pour l’étape n’enregistre pas les modifications dans le workflow. Pour enregistrer les modifications dans le workflow, appuyez ou cliquez sur **Synchronisation**.

1. Ouvrez le panneau latéral et localisez le **Atteindre l’étape** et faites-le glisser sur le workflow.

1. Ouvrez le **Atteindre** et appuyez ou cliquez sur **Processus** .

1. Sélectionnez la **Étape cible** pour accéder à et spécifier que la variable **Expression de routage** est un script ECMA. Indiquez ensuite le code suivant dans la variable **Script** field :

   ```javascript
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

   >[!TIP]
   >
   >Pour plus d’informations sur les scripts des étapes de processus, voir [Définition d’une règle pour une division OU](/help/sites-developing/workflows-models.md).

   ![Atteindre le script](assets/project-workflow-goto.png)

1. Appuyez ou cliquez sur **OK**.

1. Appuyez ou cliquez sur **Synchronisation** pour enregistrer le workflow.

Une nouvelle tâche apparaît maintenant après la [Tâche Déplacer vers la production](#move-to-production-task) est terminée et est affectée au propriétaire.

L’utilisateur de la variable **Propriétaire** rôle peut terminer la tâche et sélectionner une action (dans la liste des actions ajoutées dans les configurations des étapes du workflow) dans la liste de la fenêtre contextuelle des commentaires.

>[!NOTE]
>
>Lorsque vous démarrez un serveur, le servlet de liste des tâches de projet met en cache les mappages entre les types de tâches et les URL définis sous `/libs/cq/core/content/projects/tasktypes`. Vous pouvez ensuite effectuer la superposition habituelle et ajouter des types de tâche personnalisés en les plaçant sous `/apps/cq/core/content/projects/tasktypes`.
