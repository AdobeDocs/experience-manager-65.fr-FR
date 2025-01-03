---
title: Configurer les files d’attente partagées
description: Les files d’attente partagées vous permettent de configurer et de gérer efficacement les files d’attente d’utilisateur ou d’utilisatrice. Découvrez comment configurer des files d’attente partagées.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms_workflow
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 5f4467c1-0f3f-4dc6-9bd5-98259f327295
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: 6a9806d8f40f711a610c130c63d9ab9b2460d075
workflow-type: tm+mt
source-wordcount: '636'
ht-degree: 100%

---

# Configurer les files d’attente partagées{#configuring-shared-queues}

Les files d’attente partagées vous permettent de configurer et de gérer efficacement les files d’attente d’utilisateur ou d’utilisatrice. Une file d’attente d’utilisateur ou d’utilisatrice correspond à toutes les tâches affectées à un utilisateur ou à une utilisatrice. Voir [Listes de tâches](https://help.adobe.com/fr_FR/livecycle/11.0/WorkspaceHelp/WS92d06802c76abadb-2b6ab502126beb6ba2f-7ffc.2.html) pour plus d’informations. Vous avez la possibilité d’affecter, de retirer l’affectation et de réaffecter les files d’attente d’utilisateur et d’utilisatrice en fonction des besoins de votre société. Vous pouvez gérer les files d’attente partagées de deux manières différentes :

**Gérer l’accès à un utilisateur ou une utilisatrice**

Vous pouvez gérer l’accès à une file d’attente sélectionnée d’utilisateur ou d’utilisatrice à l’aide de cette option.

**Gérer l’accès par un utilisateur ou une utilisatrice**

Vous pouvez gérer les files d’attente partagées affectées à une personne utilisatrice sélectionnée à l’aide de cette option.

## Gestion de l’accès à une file d’attente sélectionnée d’utilisateur ou d’utilisatrice {#managing-access-to-a-selected-user-queue}

La fonctionnalité Gérer l’accès à un utilisateur ou une utilisatrice vous permet de gérer l’accès à une file d’attente sélectionnée d’utilisateur ou d’utilisatrice. Vous pouvez accorder ou révoquer l’accès à une file d’attente sélectionnée d’utilisateur ou d’utilisatrice à d’autres utilisateurs et utilisatrices au sein de votre entreprise. Par exemple, Kara Bowman est absente du bureau. À l’aide de la fonctionnalité Gérer l’accès à un utilisateur ou une utilisatrice , la file d’attente de Kara peut être partagée avec Akira Tanaka et John Jacobs pourqu’elle puisse être terminée. Une fois que Kara revient au bureau, vous pouvez alors révoquer à Akira Tanaka et John Jacobs l’accès à sa file d’attente.

Une fois partagées, ces tâches peuvent être effectuées par l’utilisateur ou l’utilisatrice, avec accès à la file d’attente, à l’aide de Workspace.

>[!NOTE]
>
>Flex Workspace est obsolète pour la version d’AEM Forms.

### Configuration de l’accès à une file d’attente sélectionnée d’utilisateur ou d’utilisatrice {#configuring-access-to-a-selected-user-queue}

>[!NOTE]
> 
> Vérifiez que l’utilisateur ou l’utilisatrice dispose de droits d’administration pour accéder à la console d’administration.

1. Connectez-vous à la console d’administration à l’aide d’un compte d’administration.
1. Sélectionnez **Services** > **Forms Workflow** > **File d’attente partagée**.

1. Dans l’onglet Gérer l’accès à un utilisateur ou une utilisatrice, recherchez et sélectionnez l’utilisateur ou l’utilisatrice dont vous souhaitez partager la file d’attente. À tout moment, le volet inférieur droit affiche la liste des utilisateurs et utilisatrices ayant accès à la file d’attente sélectionnée d’utilisateur ou d’utilisatrice.
1. Dans le volet inférieur gauche, recherchez et sélectionnez l’utilisateur ou l’utilisatrice. Cliquez sur Partager.
1. Cliquez sur Enregistrer pour terminer.

### Révocation de l’accès à une file d’attente sélectionnée d’utilisateur ou d’utilisatrice {#revoking-access-to-a-selected-user-queue}

1. Connectez-vous à la console d’administration à l’aide d’un compte d’administration.
1. Sélectionnez **Services** > **Forms Workflow** > **File d’attente partagée**.

1. Sous l’onglet Gérer l’accès à un utilisateur ou utilisatrice, recherchez et sélectionnez l’utilisateur ou l’utilisatrice dont vous souhaitez gérer la file d’attente.
1. Le volet inférieur droit affiche la liste des utilisateurs et utilisatrices ayant accès à la file d’attente délectionnée d’utilisateur ou d’utilisatrice. Sélectionnez l’utilisateur ou l’utilisatrice et cliquez sur Révoquer.
1. Cliquez sur Enregistrer pour terminer.

## Gestion des files d’attente affectées à un utilisateur ou à une utilisatrice {#managing-queues-assigned-to-a-user}

La fonctionnalité Gérer l’accès par un utilisateur ou une utilisatrice permet de gérer les files d’attente affectées à une personne utilisatrice sélectionnée. Vous pouvez accorder ou révoquer individuellement l’accès aux files d’attente d’un utilisateur ou d’une utilisatrice à une personne utilisatrice sélectionnée. Par exemple, vous souhaitez affecter les files d’attente d’Akira Tanaka et de John Jacobs à Kara Bowman. La fonctionnalité Gérer l’accès par un utilisateur ou une utilisatrice vous permet de rechercher Kara Bowman et de lui accorder l’accès aux tâches affectées à Akira Tanaka et John Jacobs. Vous pouvez ultérieurement révoquer à Kara Bowman l’accès à ces files d’attente.

Une fois affectées, ces tâches peuvent être effectuées par l’utilisateur ou l’utilisatrice à l’aide de Workspace.

>[!NOTE]
>
>Flex Workspace est obsolète pour la version d’AEM Forms.

### Accorder l’accès à une file d’attente sélectionnée d’utilisateur ou d’utilisatrice {#granting-access-to-a-selected-user-queue}

1. Connectez-vous à la console d’administration à l’aide d’un compte d’administration.
1. Sélectionnez **Services** > **Forms Workflow** > **File d’attente partagée**.

1. Dans l’onglet Gérer l’accès à un utilisateur ou une utilisatrice, recherchez et sélectionnez l’utilisateur ou l’utilisatrice dont vous souhaitez partager la file d’attente. À tout moment, le volet inférieur droit affiche la liste des utilisateurs et utilisatrices ayant accès à la file d’attente sélectionnée d’utilisateur ou d’utilisatrice.
1. Dans le volet inférieur gauche, recherchez et sélectionnez les files d’attente d’utilisateur ou d’utilisatrice que vous souhaitez partager avec la personne utilisatrice sélectionnée. Cliquez sur Partager.
1. Cliquez sur Enregistrer pour terminer.

### Révocation de l’accès à une file d’attente sélectionnée d’utilisateur ou d’utilisatrice {#revoking_access_to_a_selected_user_queue-1}

1. Connectez-vous à la console d’administration à l’aide d’un compte d’administration.
1. Sélectionner **Services** > **Forms Workflow** > **File d’attente partagée**.

1. Dans l’onglet Gérer l’accès par un utilisateur ou une utilisatrice, recherchez et sélectionnez l’utilisateur ou l’utilisatrice dont vous souhaitez gérer la file d’attente.
1. Le volet inférieur droit affiche la liste des files d’attente d’utilisateur et d’utilisatrice affectées à la personne utilisatrice sélectionnée. Sélectionnez la file d’attente de l’utilisateur ou de l’utilisatrice et cliquez sur Révoquer.
1. Cliquez sur Enregistrer pour terminer.
