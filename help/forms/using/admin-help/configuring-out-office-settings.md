---
title: Configuration des paramètres d’absence du bureau
seo-title: Configuration des paramètres d’absence du bureau
description: La fonction d’absence du bureau vous permet de spécifier les périodes pendant lesquelles un utilisateur est absent du bureau et n’est pas en mesure d’exécuter les tâches qui lui ont été affectées par AEM forms.
seo-description: La fonction d’absence du bureau vous permet de spécifier les périodes pendant lesquelles un utilisateur est absent du bureau et n’est pas en mesure d’exécuter les tâches qui lui ont été affectées par AEM forms.
uuid: 0d01df0a-aa6a-40e5-bf24-423ed1c932cc
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms_workflow
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 30312159-58a5-4781-b554-29dcbce696cb
exl-id: 1c8ad09b-d44a-4d90-86d5-d4c66cf5c57c
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '691'
ht-degree: 96%

---

# Configuration des paramètres d’absence du bureau {#configuring-out-of-office-settings}

La fonction d’absence du bureau permet aux utilisateurs ou aux administrateurs de spécifier les périodes pendant lesquelles un utilisateur est absent du bureau et n’est pas en mesure d’exécuter les tâches qui lui ont été affectées par AEM forms. Lorsqu’un utilisateur est absent du bureau, ses tâches sont attribuées à un ou plusieurs autres utilisateurs désignés. Les utilisateurs peuvent modifier leurs paramètres d’absence du bureau dans Workspace ou les administrateurs peuvent modifier les paramètres à la place d’un utilisateur dans le processus des formulaires.

Lors de la création d’un processus, l’utilisateur de Workbench peut spécifier si une tâche peut être redirigée en fonction de paramètres d’absence du bureau.

## Affichage des informations d’absence du bureau d’un utilisateur {#view-a-user-s-out-of-office-information}

1. Dans Administration Console, cliquez sur Services > Processus des formulaires > Absence du bureau.
1. Dans la zone adjacente à la page Absence du bureau, vous pouvez effectuer l’une des actions suivantes :

   **Rechercher par nom :**

   sélectionnez l’option Rechercher par nom. Saisissez une partie ou la totalité du nom d’utilisateur et cliquez sur Rechercher. Si vous ne remplissez pas le champ, le processus des formulaires renvoie la liste de tous les utilisateurs.

   **Rechercher par plage de dates :**

   sélectionnez l’option Rechercher par plage de dates. Spécifiez les dates de début et de fin, ainsi que l’horodatage de la période souhaitée pour limiter les résultats de la recherche. Cliquez sur Rechercher.

1. Cliquez sur le nom d’un utilisateur pour afficher ses informations d’absence du bureau au-dessous de la liste des utilisateurs.

## Modification de l’état d’absence du bureau d’un utilisateur  {#change-a-user-s-out-of-office-status}

1. Recherchez l’utilisateur, comme indiqué dans [Affichage des informations d’absence du bureau d’un utilisateur](configuring-out-office-settings.md#view-a-user-s-out-of-office-information).
1. Cliquez sur le nom de l’utilisateur voulu.
1. Dans la liste *Nom d’utilisateur* est actuellement, sélectionnez Au bureau ou Absence du bureau.
1. Cliquez sur Enregistrer.

## Ajout d’une plage de dates d’absence du bureau d’un utilisateur  {#add-an-out-of-office-date-range-for-a-user}

1. Recherchez l’utilisateur, comme indiqué dans [Affichage des informations d’absence du bureau d’un utilisateur](configuring-out-office-settings.md#view-a-user-s-out-of-office-information).
1. Cliquez sur le nom de l’utilisateur voulu.
1. Cliquez sur Ajouter une plage de dates.
1. Saisissez une heure de début et une heure de fin. Vous pouvez cliquer sur l’icône du calendrier pour sélectionner une date. Si vous ne spécifiez pas d’heure de fin, l’utilisateur est considéré comme étant indéfiniment absent du bureau.
1. Cliquez sur Enregistrer.

## Affectation d’un utilisateur aux tâches d’absence du bureau  {#assign-a-user-for-out-of-office-tasks}

Vous pouvez affecter l’exécution des tâches d’un utilisateur absent du bureau à un ou plusieurs autres utilisateurs. Vous pouvez définir les configurations suivantes :

* affecter toute nouvelle tâche à un utilisateur désigné par défaut ;
* ne pas réaffecter les tâches (les nouvelles tâches restent affectées à l’utilisateur absent du bureau) ;
* désigner un utilisateur par défaut qui recevra la plupart des tâches de l’utilisateur absent du bureau, mais préciser que les tâches de certains processus seront réaffectées à d’autres utilisateurs ou resteront affectées à l’utilisateur absent du bureau ;
* ne pas désigner d’utilisateur par défaut, mais affecter les tâches de certains processus à des utilisateurs spécifiques.

   1. Recherchez l’utilisateur, comme indiqué dans [Affichage des informations d’absence du bureau d’un utilisateur](configuring-out-office-settings.md#view-a-user-s-out-of-office-information).
   1. Cliquez sur le nom de l’utilisateur voulu.
   1. Dans la liste Utilisateur par défaut pour les tâches d’absence du bureau, sélectionnez un utilisateur. Si vous ne souhaitez pas désigner un utilisateur par défaut pour la réception des éléments réaffectés, sélectionnez Ne pas affecter.

      Si le nom de l’utilisateur voulu n’apparaît pas dans la liste, cliquez sur Rechercher un utilisateur et recherchez l’utilisateur voulu à partir de la boîte de dialogue qui s’affiche. Sélectionnez l’utilisateur voulu dans la liste et cliquez sur Sélectionner un utilisateur. Vous pouvez aussi cliquer sur Afficher le programme de l’utilisateur dans la boîte de dialogue Rechercher un utilisateur pour afficher le programme d’absence du bureau de l’utilisateur sélectionné.

   1. Si certains processus ne doivent pas être envoyés à l’utilisateur par défaut, cliquez sur Ajouter une exception, puis sélectionnez le processus et un autre utilisateur dans la liste. Vous pouvez également sélectionner Ne pas affecter pour que la tâche reste attribuée à l’utilisateur absent du bureau.
   1. Cliquez sur Enregistrer.
