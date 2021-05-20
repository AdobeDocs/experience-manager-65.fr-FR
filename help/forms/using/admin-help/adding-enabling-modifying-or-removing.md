---
title: Ajout, activation, modification ou suppression de points de fin
seo-title: Ajout, activation, modification ou suppression de points de fin
description: Découvrez comment ajouter, activer, modifier et supprimer des points de fin.
seo-description: Découvrez comment ajouter, activer, modifier et supprimer des points de fin.
uuid: c53f225b-3d55-42f6-8982-0cd7dde0c4f5
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/managing_endpoints
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 7d0d4f96-fc72-4e2b-a2cc-5741b0a30f74
exl-id: b7461d5c-95d1-4da2-9d2a-f54c410a87f9
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '386'
ht-degree: 100%

---

# Ajout, activation, modification ou suppression de points de fin {#adding-enabling-modifying-or-removing-endpoints}

## Ajout d’un point de fin à un service {#add-an-endpoint-to-a-service}

Vous ne pouvez ajouter des points de fin qu’à des services. Un point de fin ne peut pas exister seul ; il doit être associé à un service.

>[!NOTE]
>
>il est conseillé d’utiliser des noms uniques lors de l’ajout de points de fin.

1. Dans Administration Console, cliquez sur Services > Applications et services > Gestion des services.
1. Dans la page Gestion des services, sélectionnez le service à configurer.
1. Dans la liste de l’onglet Points de fin, sélectionnez le type de point de fin à ajouter et cliquez sur Ajouter.
1. En fonction du type de point de fin, configurez d’autres paramètres de point de fin.

[Paramètres des points de fin Watched Folder](/help/forms/using/admin-help/configuring-watched-folder-endpoints.md#watched-folder-endpoint-settings)

[Paramètres des points de fin de courrier électronique](/help/forms/using/admin-help/configuring-email-endpoints.md#email-endpoint-settings)

[Configuration des points de fin TaskManager](/help/forms/using/admin-help/configuring-task-manager-endpoints.md#configuring-task-manager-endpoints)

[Paramètres des points de fin Remoting](/help/forms/using/admin-help/configuring-remoting-endpoints.md#remoting-endpoint-settings)

1. Cliquez sur Ajouter.

## Activation ou désactivation d’un point de fin {#enable-or-disable-an-endpoint}

Par défaut, les nouveaux points de fin sont automatiquement activés. Cependant, si vous en désactivez un, vous devez le réactiver pour qu’il soit opérationnel.

Si vous rencontrez des problèmes avec des services, vous devez désactiver les points de fin associés afin de les résoudre plus facilement. Vous pouvez également désactiver les points de fin lors de la maintenance régulière du système ou lors de la mise à niveau d’un service.

1. Dans Administration Console, cliquez sur Services > Applications et services > Gestion des points de fin.
1. Dans la page Gestion des points de fin, cochez la case associée au point de fin à activer ou désactiver et cliquez sur Activer ou Désactiver.

## Modification d’un point de fin  {#modify-an-endpoint}

>[!NOTE]
>
>Les modifications apportées à la configuration d’un point de fin à l’aide d’Administration Console n’affectent pas les copies effectuées au moment de la conception des applications. Si vous déployez à nouveau une application, toute modification appliquée à son point de fin à l’aide d’Administration Console est perdue.

1. Dans Administration Console, cliquez sur Services > Applications et services > Gestion des points de fin.
1. Dans la page Gestion des points de fin, cliquez sur le point de fin à modifier.
1. Dans la page Mettre à jour le point de fin, modifiez le nom, la description et les paramètres du point de fin.

   >[!NOTE]
   >
   >n’incluez pas de caractère &lt; dans le nom ou la description car ces derniers seraient tronqués lors de leur affichage dans Workspace.

1. Pour enregistrer vos modifications, cliquez sur Mettre à jour.

Pour exécuter cette tâche, vous pouvez également sélectionner un service dans la page Gestion des services, puis cliquer sur l’onglet Points de fin.

## Suppression d’un point de fin  {#remove-an-endpoint}

1. Dans Administration Console, cliquez sur Services > Applications et services > Gestion des points de fin.
1. Dans la page Gestion des points de fin, cochez la case correspondant au point de fin à supprimer, puis cliquez sur Supprimer. Ce point de fin n’est plus affiché.
