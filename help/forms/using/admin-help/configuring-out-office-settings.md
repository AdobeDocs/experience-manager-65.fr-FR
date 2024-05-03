---
title: Configurer les paramètres d’absence du bureau
description: La fonctionnalité Absent du bureau vous permet de spécifier quand un utilisateur ou une utilisatrice sera absent du bureau et incapable d'accomplir les tâches assignées par AEM Forms.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms_workflow
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 1c8ad09b-d44a-4d90-86d5-d4c66cf5c57c
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: tm+mt
source-wordcount: '659'
ht-degree: 100%

---

# Configurer les paramètres d’absence du bureau {#configuring-out-of-office-settings}

La fonctionnalité Absent du bureau permet aux utilisateurs et utilisatrices ou aux administrateurs et administratrices de spécifier quand une personne sera absente du bureau et ne pourra pas effectuer les tâches assignées par AEM Forms. Lorsqu&#39;une personne est définie sur Absent du bureau, ses tâches sont attribuées à un ou plusieurs personnes désignées. Les utilisateurs et les utilisatrices peuvent modifier leurs paramètres d’absence du bureau dans l’espace de travail ou les administrateurs et les administratrices peuvent également modifier les paramètres à la place d’un utilisateur ou une utilisatrice dans Forms Workflow.

Lors de la création d’un processus, l’utilisateur ou l’utilisatrice de Workbench peut spécifier si une tâche peut être redirigée en raison des paramètres d’absence du bureau.

## Afficher les informations d’absence du bureau d’un utilisateur ou d’une utilisatrice {#view-a-user-s-out-of-office-information}

1. Dans la console d’administration, cliquez sur Services > Forms Workflow > Absence du bureau.
1. Dans la zone située en haut de la page Absence du bureau, vous pouvez effectuer l’une des opérations suivantes :

   **Rechercher par nom**

   Sélectionnez l’option Rechercher par nom. Saisissez tout ou partie du nom de l’utilisateur ou de l’utilisatrice, puis cliquez sur Rechercher. Si vous laissez le champ vide, Forms Workflow renvoie une liste de l’ensemble des utilisateurs et utilisatrices.

   **Rechercher par période**

   Sélectionnez l’option Rechercher par période. Spécifiez les dates de début et de fin ainsi que les horodatages souhaités pour affiner les résultats de la recherche. Cliquez sur Rechercher.

1. Cliquez sur un nom d’utilisateur ou d’utilisatrice pour afficher ses informations d’absence du bureau sous la liste des utilisateurs et utilisatrices.

## Modifier le statut d’absence d’un utilisateur ou d’une utilisatrice {#change-a-user-s-out-of-office-status}

1. Recherchez l’utilisateur ou l’utilisatrice, comme décrit dans [Afficher les informations d’absence du bureau d’un utilisateur ou d’une utilisatrice](configuring-out-office-settings.md#view-a-user-s-out-of-office-information).
1. Cliquez sur le nom de l’utilisatrice ou l’utilisateur voulu.
1. À partir du *Nom d’utilisateur* dans la liste, sélectionnez Au bureau ou Absent du bureau.
1. Cliquez sur Enregistrer.

## Ajouter une période d’absence du bureau pour un utilisateur ou une utilisatrice {#add-an-out-of-office-date-range-for-a-user}

1. Recherchez l’utilisateur ou l’utilisatrice, comme décrit dans[Afficher les informations d’absence du bureau d’un utilisateur ou une utilisatrice](configuring-out-office-settings.md#view-a-user-s-out-of-office-information).
1. Cliquez sur le nom de l’utilisatrice ou l’utilisateur voulu.
1. Cliquez sur Ajouter une période.
1. Entrez une heure de début et une heure de fin. Vous pouvez cliquer sur l’icône Calendrier pour sélectionner une date. Si vous ne spécifiez pas d’heure de fin, l’utilisatrice ou l’utilisateur sera défini comme absent du bureau indéfiniment.
1. Cliquez sur Enregistrer.

## Attribuer un utilisateur ou une utilisatrice pour les tâches d’absence du bureau {#assign-a-user-for-out-of-office-tasks}

Lorsqu’une utilisatrice ou un utilisateur est absent du bureau, vous pouvez affecter un ou plusieurs utilisateurs ou utilisatrices à l’exécution de nouvelles tâches pour l’utilisateur ou l’utilisatrice. Vous pouvez définir les configurations suivantes :

* Attribuez toutes les nouvelles tâches à une personne désignée par défaut.
* Ne réaffectez aucune tâche. Les nouvelles tâches restent assignées à l’utilisatrice ou l’utilisateur absent du bureau.
* Attribuez un utilisateur ou une utilisatrice par défaut qui recevra la plupart des tâches de l’utilisateur ou l’utilisatrice, mais précisez que les tâches de certains processus sont réaffectées à d’autres utilisateurs et utilisatrices ou restent attribuées à l’utilisatrice ou l’utilisateur qui est absent du bureau.
* N’attribuez pas d’utilisateur ou d’utilisatrice par défaut, mais attribuez certaines tâches de certains processus à des utilisateurs et utilisatrices spécifiques.

   1. Recherchez l’utilisateur ou l’utilisatrice, comme décrit dans [Afficher les informations d’absence du bureau d’un utilisateur ou une utilisatrice](configuring-out-office-settings.md#view-a-user-s-out-of-office-information).
   1. Cliquez sur le nom de l’utilisatrice ou l’utilisateur voulu.
   1. Dans la liste Utilisateur par défaut pour les tâches d’absence du bureau, sélectionnez un utilisateur ou une utilisatrice dans la liste. Si vous ne souhaitez pas désigner un utilisateur ou une utilisatrice par défaut pour recevoir les éléments réaffectés, sélectionnez Ne pas attribuer.

      Si le nom d’utilisatrice ou utilisateur approprié n’apparaît pas dans la liste, cliquez sur Rechercher un utilisateur et utilisez la boîte de dialogue de Rechercher un utilisateur pour rechercher l’utilisateur ou l’utilisatrice. Sélectionnez l’utilisarice ou l’utilisateur approprié dans la liste et cliquez sur Sélectionner un utilisateur. Vous pouvez également cliquer sur Afficher le planning de l’utilisateur dans la boîte de dialogue Rechercher un utilisateur pour voir le planning d’absence de l’utilisatrice ou l’utilisateur sélectionné.

   1. S’il y a des processus qui ne doivent pas être envoyés à l’utilisateur ou à l’utilisatrice par défaut, cliquez sur Ajouter une exception, sélectionnez le processus, puis choisissez un autre utilisateur ou une autre utilisatrice dans la liste. Vous pouvez également sélectionner Ne pas attribuer pour que la tâche reste attribuée à l’utilisatrice ou l’utilisateur absent du bureau.
   1. Cliquez sur Enregistrer.
