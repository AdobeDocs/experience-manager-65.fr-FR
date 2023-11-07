---
title: Ajouter, activer, modifier ou supprimer des points d’entrée
seo-title: Adding, enabling, modifying, or removing endpoints
description: Découvrez comment ajouter, activer, modifier et supprimer des points de fin.
seo-description: Learn how to add, enable, modify and remove endpoints.
uuid: c53f225b-3d55-42f6-8982-0cd7dde0c4f5
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/managing_endpoints
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 7d0d4f96-fc72-4e2b-a2cc-5741b0a30f74
exl-id: b7461d5c-95d1-4da2-9d2a-f54c410a87f9
source-git-commit: 49688c1e64038ff5fde617e52e1c14878e3191e5
workflow-type: tm+mt
source-wordcount: '369'
ht-degree: 10%

---

# Ajouter, activer, modifier ou supprimer des points d’entrée {#adding-enabling-modifying-or-removing-endpoints}

## Ajout d’un point de fin à un service {#add-an-endpoint-to-a-service}

Les points de fin peuvent uniquement être ajoutés aux services. Un point de terminaison ne peut pas exister seul ; il doit être associé à un service.

>[!NOTE]
>
>Il est recommandé d’utiliser des noms uniques lors de l’ajout de points de fin.

1. Dans Administration Console, cliquez sur Services > Applications et services > Gestion des services.
1. Sur la page Gestion des services, cliquez sur le service à configurer.
1. Dans la liste de l’onglet Points de fin , sélectionnez le type de point de fin à ajouter, puis cliquez sur Ajouter.
1. Selon le type de point de fin, configurez des paramètres de point de fin supplémentaires.

[Paramètres des points d’entrée Watched Folder](/help/forms/using/admin-help/configuring-watched-folder-endpoints.md#watched-folder-endpoint-settings)

[Paramètres des points d’entrée de courrier électronique](/help/forms/using/admin-help/configuring-email-endpoints.md#email-endpoint-settings)

[Configuration des points d’entrée TaskManager](/help/forms/using/admin-help/configuring-task-manager-endpoints.md#configuring-task-manager-endpoints)

[Paramètres des points d’entrée Remoting](/help/forms/using/admin-help/configuring-remoting-endpoints.md#remoting-endpoint-settings)

1. Cliquez sur Ajouter.

## Activation ou désactivation d’un point de fin {#enable-or-disable-an-endpoint}

Par défaut, les nouveaux points de fin sont automatiquement activés. Mais si vous avez désactivé un point de terminaison, vous devez l’activer pour qu’il soit opérationnel.

Si vous rencontrez des problèmes avec les services, désactivez les points de terminaison associés afin de mieux résoudre le problème. Vous pouvez également désactiver les points de fin lors de la maintenance régulière du système ou lors de la mise à niveau d’un service.

1. Dans Administration Console, cliquez sur Services > Applications et services > Gestion des points de fin.
1. Sur la page Gestion des points de fin, cochez la case correspondant au point de fin à activer ou désactiver, puis cliquez sur Activer ou Désactiver.

## Modification d’un point de fin {#modify-an-endpoint}

>[!NOTE]
>
>Les modifications apportées à une configuration de point de terminaison à l’aide d’Administration Console ne sont pas répercutées dans les copies au moment de la conception de vos applications. Si vous redéployez une application, toute modification apportée à ses points de fin à l’aide d’Administration Console sera perdue.

1. Dans Administration Console, cliquez sur Services > Applications et services > Gestion des points de fin.
1. Sur la page Gestion des points de fin, cliquez sur le point de fin à modifier.
1. Sur la page Mettre à jour le point de fin , modifiez le nom, la description et les paramètres du point de fin.

   >[!NOTE]
   >
   >N’incluez pas de caractère &lt; dans le nom ou la description, car cela tronquera le nom ou la description affiché dans Workspace.

1. Pour enregistrer vos modifications, cliquez sur Mettre à jour.

Vous pouvez également effectuer cette tâche à partir de la page Gestion des services en sélectionnant un service, puis en cliquant sur l’onglet Points de fin .

## Suppression d’un point de fin {#remove-an-endpoint}

1. Dans Administration Console, cliquez sur Services > Applications et services > Gestion des points de fin.
1. Sur la page Gestion des points de fin, cochez la case correspondant au point de fin à supprimer, puis cliquez sur Supprimer. Le point de terminaison n’est plus affiché.
