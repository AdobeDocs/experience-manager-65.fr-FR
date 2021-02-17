---
title: Configuration des files d’attente partagées
seo-title: Configuration des files d’attente partagées
description: Les files d’attente partagées vous permettent de configurer et de gérer efficacement les files d’attente d’utilisateur. Découvrez comment configurer les files d’attente partagées.
seo-description: Les files d’attente partagées vous permettent de configurer et de gérer efficacement les files d’attente d’utilisateur. Découvrez comment configurer les files d’attente partagées.
uuid: 69ab611d-334b-40a5-bd2d-533d4cb25eda
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/configuring_forms_workflow
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: fc403a60-b635-4334-9bf8-2f3d2036b2f3
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '672'
ht-degree: 97%

---


# Configuration des files d’attente partagées{#configuring-shared-queues}

Les files d’attente partagées vous permettent de configurer et de gérer efficacement les files d’attente d’utilisateur. Une file d’attente d’utilisateur correspond à l’ensemble des tâches affectées à un utilisateur. Voir [Listes Tâches](https://help.adobe.com/en_US/livecycle/11.0/WorkspaceHelp/WS92d06802c76abadb-2b6ab502126beb6ba2f-7ffc.2.html) pour plus d’informations. Vous avez la possibilité d’affecter, de désaffecter et de réaffecter les files d’attente d’utilisateur en fonction des besoins de votre société. Les files d’attente partagées peuvent être gérées de deux manières différentes :

**Gérer l’accès à un utilisateur**

Vous pouvez gérer l’accès à la file d’attente d’utilisateur sélectionnée à l’aide de cette option.

**Gérer l’accès par un utilisateur**

Vous pouvez gérer les files d’attente partagées affectées à un utilisateur sélectionné à l’aide de cette option.

## Gestion de l’accès à une file d’attente d’utilisateur sélectionnée {#managing-access-to-a-selected-user-queue}

L’option Gérer l’accès à un utilisateur permet de gérer l’accès à une file d’attente d’utilisateur sélectionnée. Vous pouvez accorder ou révoquer l’accès à une file d’attente d’utilisateur à d’autres utilisateurs au sein de votre société. Par exemple, Kara Bowman est absente du bureau. La fonction Gérer l’accès à un utilisateur permet de partager sa file d’attente avec Akira Tanaka et John Jacobs pour qu’elle puisse être terminée. Une fois que Kara Bowman revient au bureau, vous pouvez alors révoquer à Akira Tanaka et John Jacobs l’accès à sa file d’attente.

Lorsqu’elles sont partagées, ces tâches peuvent être exécutées par l’utilisateur qui a accès à la file d’attente, à l’aide de Workspace.

>[!NOTE]
>
>Flex Workspace est obsolète pour la version d’AEM Forms.

### Configuration de l’accès à une file d’attente d’utilisateur sélectionnée  {#configuring-access-to-a-selected-user-queue}

1. Connectez-vous à Administration Console à l’aide d’un compte administrateur.
1. Sélectionnez **Services** > **Processus des formulaires** > **File d’attente partagée**.

1. Sous l’onglet Gérer l’accès à un utilisateur, recherchez et sélectionnez l’utilisateur dont vous souhaitez partager la file d’attente. Le volet inférieur droit affiche en permanence la liste des utilisateurs ayant accès à la file d’attente d’utilisateur sélectionnée.
1. Recherchez et sélectionnez l’utilisateur dans le volet inférieur gauche. Cliquez sur Partager.
1. Cliquez sur Enregistrer pour terminer l’opération.

### Révocation de l’accès à une file d’attente d’utilisateur sélectionnée  {#revoking-access-to-a-selected-user-queue}

1. Connectez-vous à Administration Console à l’aide d’un compte administrateur.
1. Sélectionnez **Services** > **Processus des formulaires** > **File d’attente partagée**.

1. Sous l’onglet Gérer l’accès à un utilisateur, recherchez et sélectionnez l’utilisateur dont vous souhaitez gérer la file d’attente.
1. Le volet inférieur droit affiche la liste des utilisateurs ayant accès à la file d’attente d’utilisateur sélectionnée. Sélectionnez l’utilisateur et cliquez sur Révoquer.
1. Cliquez sur Enregistrer pour terminer l’opération.

## Gestion des files d’attente affectées à un utilisateur  {#managing-queues-assigned-to-a-user}

La fonction Gérer l’accès par un utilisateur vous permet de gérer les files d’attente affectées à un utilisateur sélectionné. Vous pouvez accorder ou révoquer l’accès aux files d’attente d’utilisateur à un utilisateur sélectionné de manière individuelle. Vous pouvez, par exemple, affecter les files d’attente d’Akira Tanaka et de John Jacobs à Kara Bowman. La fonction Gérer l’accès par un utilisateur vous permet de rechercher Kara Bowman et de lui accorder l’accès aux tâches affectées à Akira Tanaka et John Jacobs. Vous pouvez ensuite révoquer ultérieurement l’accès de Kara Bowman à ces files d’attente d’utilisateur.

Une fois affectées, ces tâches peuvent être exécutées par l’utilisateur à l’aide de Workspace.

>[!NOTE]
>
>Flex Workspace est obsolète pour la version d’AEM forms.

### Accorder l’accès à une file d’attente d’utilisateur sélectionnée  {#granting-access-to-a-selected-user-queue}

1. Connectez-vous à Administration Console à l’aide d’un compte administrateur.
1. Sélectionnez **Services** > **Processus des formulaires** > **File d’attente partagée**.

1. Sous l’onglet Gérer l’accès à un utilisateur, recherchez et sélectionnez l’utilisateur dont vous souhaitez partager la file d’attente. Le volet inférieur droit affiche en permanence la liste des utilisateurs ayant accès à la file d’attente d’utilisateur sélectionnée.
1. Recherchez et sélectionnez dans le volet inférieur gauche les files d’attente d’utilisateur que vous souhaitez partager avec l’utilisateur sélectionné. Cliquez sur Partager.
1. Cliquez sur Enregistrer pour terminer l’opération.

### Révocation de l’accès à une file d’attente d’utilisateur sélectionnée  {#revoking_access_to_a_selected_user_queue-1}

1. Connectez-vous à Administration Console à l’aide d’un compte administrateur.
1. Sélectionnez **Services** > **Processus des formulaires** > **File d’attente partagée**.

1. Sous l’onglet Gérer l’accès par un utilisateur, recherchez et sélectionnez l’utilisateur dont vous souhaitez gérer la file d’attente.
1. Le volet inférieur droit affiche la liste des files d’attente d’utilisateur affectées à l’utilisateur sélectionné. Sélectionnez la file d’attente d’utilisateur et cliquez sur Révoquer.
1. Cliquez sur Enregistrer pour terminer l’opération.

