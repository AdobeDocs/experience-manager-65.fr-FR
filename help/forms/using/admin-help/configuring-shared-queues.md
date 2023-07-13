---
title: Configurer les files d’attente partagées
description: Les files d’attente partagées vous permettent de configurer et de gérer efficacement les files d’attente d’utilisateur. Découvrez comment configurer des files d’attente partagées.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms_workflow
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 5f4467c1-0f3f-4dc6-9bd5-98259f327295
source-git-commit: e068cee192c0837f1473802143e0793674d400e8
workflow-type: tm+mt
source-wordcount: '642'
ht-degree: 7%

---

# Configurer les files d’attente partagées{#configuring-shared-queues}

Les files d’attente partagées vous permettent de configurer et de gérer efficacement les files d’attente d’utilisateur. Une file d’attente d’utilisateur correspond à toutes les tâches affectées à un utilisateur. Voir [Listes de tâches](https://help.adobe.com/fr_FR/livecycle/11.0/WorkspaceHelp/WS92d06802c76abadb-2b6ab502126beb6ba2f-7ffc.2.html) pour plus d’informations. Vous pouvez affecter, annuler l’affectation et réaffecter des files d’attente d’utilisateur en fonction des besoins de votre entreprise. Vous pouvez gérer les files d’attente partagées de deux façons :

**Gérer l’accès à un utilisateur**

Vous pouvez gérer l’accès à une file d’attente d’utilisateur sélectionnée à l’aide de cette option.

**Gérer l’accès par un utilisateur**

Vous pouvez gérer les files d’attente partagées affectées à un utilisateur sélectionné à l’aide de cette option.

## Gestion de l’accès à une file d’attente d’utilisateur sélectionnée {#managing-access-to-a-selected-user-queue}

La fonctionnalité Gérer l’accès à un utilisateur vous permet de gérer l’accès à une file d’attente d’utilisateur sélectionnée. Vous pouvez accorder ou révoquer l’accès à une file d’attente d’utilisateurs sélectionnée à d’autres utilisateurs de votre entreprise. Par exemple, Kara Bowman est absente du bureau. À l’aide de la fonctionnalité Gérer l’accès à un utilisateur , la file d’attente de Kara peut être partagée avec Akira Tanaka et John Jacobs pour la fin. Par la suite, lorsque Kara revient au bureau, vous pouvez révoquer l’accès à sa file d’attente d’Akira Tanaka et de John Jacobs.

Une fois partagées, ces tâches peuvent être effectuées par l’utilisateur, avec accès à la file d’attente, à l’aide de Workspace.

>[!NOTE]
>
>Flex Workspace est obsolète pour la version d’AEM Forms.

### Configuration de l’accès à une file d’attente d’utilisateur sélectionnée {#configuring-access-to-a-selected-user-queue}

1. Connectez-vous à Administration Console à l’aide d’un compte administrateur.
1. Sélectionner **Services** > **Forms Workflow** > **File d’attente partagée**.

1. Dans l’onglet Gérer l’accès à un utilisateur , recherchez et sélectionnez l’utilisateur dont vous souhaitez partager la file d’attente. À tout moment, le volet inférieur droit affiche la liste des utilisateurs ayant accès à la file d’attente d’utilisateurs sélectionnée.
1. Dans le volet inférieur gauche, recherchez et sélectionnez l’utilisateur. Cliquez sur Partager.
1. Cliquez sur Enregistrer pour terminer.

### Révocation de l’accès à une file d’attente d’utilisateur sélectionnée {#revoking-access-to-a-selected-user-queue}

1. Connectez-vous à Administration Console à l’aide d’un compte administrateur.
1. Sélectionner **Services** > **Forms Workflow** > **File d’attente partagée**.

1. Dans l’onglet Gérer l’accès à un utilisateur , recherchez et sélectionnez l’utilisateur dont vous souhaitez gérer la file d’attente.
1. Le volet inférieur droit affiche la liste des utilisateurs ayant accès à la file d’attente d’utilisateurs sélectionnée. Sélectionnez l’utilisateur et cliquez sur Révoquer.
1. Cliquez sur Enregistrer pour terminer.

## Gestion des files d’attente affectées à un utilisateur {#managing-queues-assigned-to-a-user}

La fonctionnalité Gérer l’accès par un utilisateur vous permet de gérer les files d’attente affectées à un utilisateur sélectionné. Vous pouvez accorder ou révoquer individuellement l’accès aux files d’attente d’utilisateur à un utilisateur sélectionné. Par exemple, vous souhaitez affecter les files d’attente d’utilisateur Akira Tanaka et John Jacobs à Kara Bowman. La fonctionnalité Gérer l’accès par un utilisateur vous permet de rechercher Kara Bowman et d’accorder l’accès aux tâches affectées à Akira Tanaka et John Jacobs. Vous pouvez ultérieurement révoquer à Kara Bowman l’accès à ces files d’attente d’utilisateur.

Une fois affectées, ces tâches peuvent être effectuées par l’utilisateur à l’aide de Workspace.

>[!NOTE]
>
>Flex Workspace est obsolète pour la version d’AEM Forms.

### Octroi de l’accès à une file d’attente d’utilisateur sélectionnée {#granting-access-to-a-selected-user-queue}

1. Connectez-vous à Administration Console à l’aide d’un compte administrateur.
1. Sélectionner **Services** > **Forms Workflow** > **File d’attente partagée**.

1. Dans l’onglet Gérer l’accès à un utilisateur , recherchez et sélectionnez l’utilisateur dont vous souhaitez partager la file d’attente. À tout moment, le volet inférieur droit affiche la liste des utilisateurs ayant accès à la file d’attente d’utilisateurs sélectionnée.
1. Dans le volet inférieur gauche, recherchez et sélectionnez les files d’attente d’utilisateur que vous souhaitez partager avec l’utilisateur sélectionné. Cliquez sur Partager.
1. Cliquez sur Enregistrer pour terminer.

### Révocation de l’accès à une file d’attente d’utilisateur sélectionnée {#revoking_access_to_a_selected_user_queue-1}

1. Connectez-vous à Administration Console à l’aide d’un compte administrateur.
1. Sélectionner **Services** > **Forms Workflow** > **File d’attente partagée**.

1. Dans l’onglet Gérer l’accès par un utilisateur , recherchez et sélectionnez l’utilisateur dont vous souhaitez gérer la file d’attente.
1. Le volet inférieur droit affiche la liste des files d’attente d’utilisateur affectées à l’utilisateur sélectionné. Sélectionnez la file d’attente de l’utilisateur et cliquez sur Révoquer.
1. Cliquez sur Enregistrer pour terminer.
