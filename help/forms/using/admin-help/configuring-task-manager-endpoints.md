---
title: Configuration des points de fin TaskManager
seo-title: Configuration des points de fin TaskManager
description: Découvrez comment configurer des points de fin TaskManager.
seo-description: Découvrez comment configurer des points de fin TaskManager.
uuid: 07604b10-0bd7-4bce-9624-7ebac4754f56
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/managing_endpoints
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 9c55feb9-23d8-4798-a3c5-70ec736df3ad
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '243'
ht-degree: 51%

---


# Configuration des points de fin TaskManager {#configuring-task-manager-endpoints}

Les points de fin TaskManager permettent à un utilisateur Workspace d’appeler le service.

**Paramètres des points de fin TaskManager**

Définissez les paramètres suivants pour configurer un point de fin TaskManager.

**Nom :** (obligatoire) identifie le point de terminaison. Le nom est affiché dans l’affichage carte de Workspace. N’incluez pas de caractère « &lt; », car le nom affiché dans Workspace serait tronqué. Si vous saisissez une URL en tant que nom de point de fin, assurez-vous que celle-ci est conforme aux normes syntaxiques en la matière précisées dans le document RFC1738.

**Description :** Description du point de terminaison. N’incluez pas de caractère « &lt; », car la description affichée dans Workspace serait tronquée.

**Instructions de tâche :** Instructions destinées à l’utilisateur qui début ce processus.

**Propriétaire du processus :** Nom de la personne responsable du processus.

**L’utilisateur peut transférer la Tâche :** Permet à l’utilisateur de transférer la tâche initiale.

**Afficher la fenêtre des pièces jointes :** Permet à l’utilisateur d’afficher la fenêtre des pièces jointes.

**Autoriser l’Ajoute des pièces jointes :** Permet à l’utilisateur d’ajouter des pièces jointes et des notes.

**Tâche initialement verrouillée :** Verrouille la tâche initiale.

**Ajouter des listes ACL pour les files d&#39;attente partagées :** La tâche initiale est créée avec des listes ACL pour les utilisateurs de files d’attente partagées.

**Catégorisation :** (obligatoire) catégorie d’affichage du formulaire par l’utilisateur dans Workspace. Sélectionnez une catégorie dans la liste ou sélectionnez Nouvelle catégorie pour ajouter une catégorie.

**Nom de l&#39;opération :** (obligatoire) liste d’opérations qui peut être affectée au point de terminaison.
