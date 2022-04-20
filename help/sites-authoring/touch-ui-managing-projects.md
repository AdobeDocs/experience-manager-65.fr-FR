---
title: Gestion de projets
seo-title: Managing Projects
description: La console Projets vous permet d’organiser votre projet en regroupant les ressources dans une seule entité accessible et gérée dans la console Projets.
seo-description: Projects lets you organize your project by grouping resources into one entity which can be acessed and managed intheProjects console
uuid: ac937582-181f-429b-9404-3c71d1241495
contentOwner: Guillaume Carlino
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: projects
content-type: reference
discoiquuid: fb354c72-debb-4fb6-9ccf-56ff5785c3ae
exl-id: 62586c8e-dab4-4be9-a44a-2c072effe3c0
source-git-commit: 200b47070b7ead54ee54eea504bd960d4e0731d9
workflow-type: tm+mt
source-wordcount: '987'
ht-degree: 23%

---


# Gestion de projets {#managing-projects}

Dans le **Projets** , vous accédez à vos projets et vous les gérez.

![Console Projets](assets/projects-console.png)

À l’aide de la console, vous pouvez créer un projet, associer des ressources à votre projet et supprimer un projet ou des liens vers des ressources.

## Conditions d’accès {#access-requirements}

Envoie une fonction d’AEM standard sans nécessiter de configuration supplémentaire.

Toutefois, pour que les utilisateurs participant à des projets voient d’autres utilisateurs/groupes lorsqu’ils utilisent des projets, comme lors de la création de projets, de la création de tâches/workflows ou de l’affichage et de la gestion de l’équipe, ces utilisateurs doivent disposer d’un accès en lecture à `/home/users` et `/home/groups`.

Le moyen le plus simple de le faire est de donner au **projects-users** accès en lecture au groupe `/home/users` et `/home/groups`.

## Création d’un projet {#creating-a-project}

Pour créer un projet, procédez comme suit.

1. Dans le **Projets** console, appuyez ou cliquez sur **Créer** pour ouvrir le **Créer un projet** assistant.
1. Sélectionnez le modèle, puis cliquez sur **Suivant**. Vous pouvez en savoir plus sur les modèles de projet standard. [ici.](/help/sites-authoring/projects.md#project-templates)

   ![Assistant Créer un projet](assets/create-project-wizard.png)

1. Définissez le **titre** et la **description**, puis ajoutez une **miniature** s’il y a lieu. Vous pouvez également ajouter ou supprimer des utilisateurs et définir le groupe auquel ils appartiennent.

   ![Étape Propriétés de l’assistant](assets/create-project-wizard-properties.png)

1. Cliquez/appuyez sur **Créer**. Le message de confirmation vous demande si vous voulez ouvrir votre projet ou revenir à la console.

La procédure de création d’un projet est la même pour tous les modèles de projet. La différence entre les types de projets se rapporte aux projets disponibles. [rôles utilisateur](/help/sites-authoring/projects.md) et [workflows.](/help/sites-authoring/projects-with-workflows.md)

### Association de ressources à votre projet {#associating-resources-with-your-project}

Les projets vous permettent de regrouper des ressources dans une seule entité afin de les gérer dans leur ensemble. Par conséquent, vous devez associer des ressources à votre projet. Ces ressources sont regroupées dans le projet sous la forme **Mosaïques**. Les types de ressources que vous pouvez ajouter sont décrits dans la section [Mosaïques de projet](/help/sites-authoring/projects.md#project-tiles).

Pour associer des ressources à votre projet :

1. Ouvrez votre projet à partir de la console **Projets**.
1. Cliquez/appuyez sur **Ajouter une mosaïque** et sélectionnez celle que vous souhaitez lier à votre projet. Vous pouvez sélectionner plusieurs types de mosaïque.

   ![Ajouter une mosaïque](assets/project-add-tile.png)

1. Cliquez/appuyez sur **Créer**. La ressource est désormais associée à votre projet et vous pouvez y accéder à partir du projet.

### Ajout d’éléments à une mosaïque {#adding-items-to-a-tile}

Dans certaines mosaïques, vous pouvez ajouter plusieurs éléments. Par exemple, plusieurs workflows ou expériences peuvent être exécutés simultanément.

Pour ajouter des éléments à une mosaïque :

1. Dans **Projets**, accédez au projet, puis cliquez sur l’icône en forme de chevron descendant en haut à droite de la mosaïque à laquelle vous souhaitez ajouter un élément et sélectionnez l’option appropriée.

   * L’option dépend du type de mosaïque. Par exemple, il peut être **Créer une tâche** pour le **Tâches** ou **Démarrer le processus** pour le **Workflows** mosaïque.

   ![chevron en mosaïque](assets/project-tile-create-task.png)

1. Ajoutez l’élément à la mosaïque comme vous le feriez lors de la création d’une mosaïque. Les mosaïques de projets sont décrites [ici.](/help/sites-authoring/projects.md#project-tiles)

## Affichage des informations du projet {#viewing-project-info}

L’objectif principal des projets est de regrouper les informations associées dans un seul endroit afin de les rendre plus accessibles et exploitables. Vous pouvez accéder à ces informations de différentes manières.

### Ouverture d’une mosaïque {#opening-a-tile}

Vous pouvez voir les éléments qui ont été ajoutés à une mosaïque ou modifier/supprimer des éléments de la mosaïque.

Pour ouvrir une mosaïque afin d’afficher ou de modifier des éléments :

1. Appuyez ou cliquez sur l’icône représentant des points de suspension en bas à droite de la mosaïque.

   ![Mosaïque Tâches](assets/project-tile-tasks.png)

1. AEM ouvre la console pour les types d’éléments associés à la mosaïque et aux filtres en fonction du projet sélectionné.

   ![Tâches du projet](assets/project-tasks.png)

### Affichage d’une chronologie de projet {#viewing-a-project-timeline}

La chronologie du projet fournit des informations sur le moment auquel les ressources du projet ont été utilisées pour la dernière fois. Pour afficher la chronologie du projet, procédez comme suit.

1. Dans le **Projets** console, cliquez ou appuyez sur **Chronologie** dans le sélecteur de rail en haut à gauche de la console.
   ![Sélection du mode Chronologie](assets/projects-timeline-rail.png)
2. Dans la console, sélectionnez le projet pour lequel vous souhaitez afficher sa chronologie.
   ![Mode Chronologie du projet](assets/project-timeline-view.png)

Les ressources s’affichent dans le rail. Utilisez le sélecteur de rail pour revenir à la vue normale lorsque vous avez terminé.

### Affichage de projets inactifs {#viewing-active-inactive-projects}

Pour basculer entre votre principal et [les projets inactifs,](#making-projects-inactive-or-active) dans le **Projets** , cliquez sur la console **Activation/désactivation de projets Principaux** dans la barre d’outils.

![Icône Activer/désactiver les projets principaux](assets/projects-toggle-active.png)

Par défaut, la console affiche les projets principaux. Cliquez sur le bouton **Activation/désactivation de projets Principaux** une fois pour passer à l’affichage des projets inactifs. Cliquez à nouveau dessus pour revenir aux projets principaux.

## Organisation des projets {#organizing-projects}

Plusieurs options permettent d’organiser vos projets de manière à ce que la variable **Projets** console gérable.

### Dossiers de projet {#project-folders}

Vous pouvez créer des dossiers dans le **Projets** pour regrouper et organiser des projets similaires.

1. Dans le **Projets** appuyez ou cliquez sur la console **Créer** puis **Créer un dossier**.

   ![Créer un dossier](assets/project-create-folder.png)

1. Attribuez un titre à votre dossier et cliquez sur **Créer**.

1. Le dossier est ajouté à la console.

Vous pouvez désormais créer des projets dans le dossier . Vous pouvez créer plusieurs dossiers et les imbriquer.

### Désactivation des projets {#making-projects-inactive-or-active}

Vous pouvez marquer un projet comme inactif s’il est terminé, mais vous souhaitez toujours conserver les informations le concernant. [Les projets inactifs s’affichent désormais](#viewing-active-inactive-projects) par défaut dans le **Projets** console.

Pour rendre un projet inactif, procédez comme suit.

1. Ouvrez le **Propriétés du projet** de la fenêtre du projet.
   * Vous pouvez le faire à partir de la console en sélectionnant le projet ou à partir du projet via le **Informations sur le projet** mosaïque.
1. Dans le **Propriétés du projet** , modifiez la fenêtre **État du projet** curseur à partir de **Principal** to **Inactif**.

   ![Sélecteur d’état du projet dans la fenêtre des propriétés](assets/project-status.png)

1. Appuyez ou cliquez sur **Enregistrer et fermer** pour enregistrer vos modifications.

### Suppression de projets {#deleting-a-project}

Pour supprimer un projet, procédez comme suit.

1. Accédez au niveau supérieur de la **Projets** console.
1. Sélection de votre projet dans la console.
1. Appuyez ou cliquez sur **Supprimer** dans la barre d’outils.
1. AEM peut supprimer/modifier les données de projet associées lors de la suppression du projet. Sélectionnez les options dont vous avez besoin dans la **Supprimer le projet** boîte de dialogue.
   * Supprimer les groupes de projets et les rôles
   * Supprimer le dossier Ressources du projet
   * Arrêter les processus de projet

   ![Options de suppression de projet](assets/project-delete-options.png)
1. Appuyez ou cliquez sur **Supprimer** pour supprimer le projet avec les options sélectionnées.

Pour en savoir plus sur les groupes créés automatiquement par les projets, voir [Création automatique de groupe](/help/sites-authoring/projects.md#auto-group-creation) pour plus d’informations.
