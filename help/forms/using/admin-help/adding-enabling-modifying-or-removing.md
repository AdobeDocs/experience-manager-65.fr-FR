---
title: Ajouter, activer, modifier ou supprimer des points d’entrée
description: Découvrez comment ajouter, activer, modifier et supprimer des points d’entrée.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/managing_endpoints
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: b7461d5c-95d1-4da2-9d2a-f54c410a87f9
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: 6a9806d8f40f711a610c130c63d9ab9b2460d075
workflow-type: ht
source-wordcount: '381'
ht-degree: 100%

---

# Ajouter, activer, modifier ou supprimer des points d’entrée {#adding-enabling-modifying-or-removing-endpoints}

>[!NOTE]
> 
> Vérifiez que l’utilisateur ou l’utilisatrice dispose de droits d’administration pour accéder à la console d’administration.

## Ajouter un point d’entrée à un service {#add-an-endpoint-to-a-service}

Les points d’entrée peuvent uniquement être ajoutés aux services. Un point d’entrée ne peut pas exister seul. Il doit être associé à un service.

>[!NOTE]
>
>Il est recommandé d’utiliser des noms uniques lors de l’ajout de points d’entrée.

1. Dans Administration Console, cliquez sur Services > Applications et services > Gestion des services.
1. Dans la page Gestion des services, sélectionnez le service à configurer.
1. Dans la liste de l’onglet Points d’entrée, sélectionnez le type de point d’entrée à ajouter, puis cliquez sur Ajouter.
1. Selon le type de point d’entrée, configurez des paramètres de point d’entrée supplémentaires.

[Paramètres des points d’entrée Watched Folder](/help/forms/using/admin-help/configuring-watched-folder-endpoints.md#watched-folder-endpoint-settings)

[Paramètres des points d’entrée de courrier électronique](/help/forms/using/admin-help/configuring-email-endpoints.md#email-endpoint-settings)

[Configuration des points d’entrée TaskManager](/help/forms/using/admin-help/configuring-task-manager-endpoints.md#configuring-task-manager-endpoints)

[Paramètres des points d’entrée Remoting](/help/forms/using/admin-help/configuring-remoting-endpoints.md#remoting-endpoint-settings)

1. Cliquez sur Ajouter.

## Activer ou désactiver un point d’entrée {#enable-or-disable-an-endpoint}

Par défaut, les nouveaux points d’entrée sont automatiquement activés. Mais si vous avez désactivé un point d’entrée, vous devez l’activer pour qu’il soit opérationnel.

Si vous rencontrez des difficultés avec les services, désactivez les points d’entrée associés afin de mieux résoudre le problème. Vous pouvez également désactiver les points d’entrée lors de la maintenance régulière du système ou de la mise à niveau d’un service.

1. Dans la console d’administration, cliquez sur Services > Applications et services > Gestion des points d’entrée.
1. Sur la page Gestion des points d’entrée, cochez la case correspondant au point d’entrée à activer ou désactiver, puis cliquez sur Activer ou Désactiver.

## Modifier un point d’entrée {#modify-an-endpoint}

>[!NOTE]
>
>Les modifications apportées à une configuration de point d’entrée à l’aide de la console d’administration ne sont pas répercutées dans les copies de vos applications au moment de la conception. Si vous redéployez une application, toute modification apportée à ses points d’entrée à l’aide de la console d’administration sera perdue.

1. Dans la console d’administration, cliquez sur Services > Applications et services > Gestion des points d’entrée.
1. Sur la page Gestion des points d’entrée, cliquez sur le point d’entrée à modifier.
1. Sur la page Mettre à jour le point d’entrée, modifiez le nom, la description et les paramètres du point d’entrée.

   >[!NOTE]
   >
   >N’incluez pas de caractère &lt; dans le nom ou la description, car cela tronquerait le nom ou la description apparaissant dans Workspace.

1. Pour enregistrer vos modifications, cliquez sur Mettre à jour.

Vous pouvez également effectuer cette tâche à partir de la page Gestion des services en sélectionnant un service, puis en cliquant sur l’onglet Points d’entrée.

## Supprimer un point d’entrée {#remove-an-endpoint}

1. Dans la console d’administration, cliquez sur Services > Applications et services > Gestion des points d’entrée.
1. Dans la page Gestion des points d’entrée, cochez la case correspondant au point d’entrée à supprimer, puis cliquez sur Supprimer. Le point d’entrée n’est plus affiché.
