---
title: Configurer des points de fin TaskManager
seo-title: Configuring Task Manager endpoints
description: Découvrez comment configurer des points de fin TaskManager.
seo-description: Learn how to configure Task Manager endpoints.
uuid: 07604b10-0bd7-4bce-9624-7ebac4754f56
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/managing_endpoints
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 9c55feb9-23d8-4798-a3c5-70ec736df3ad
exl-id: 8495a3d7-6ac9-41f5-b1f9-31decaba118a
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: ht
source-wordcount: '232'
ht-degree: 100%

---

# Configuration des points de fin TaskManager {#configuring-task-manager-endpoints}

Les points de fin TaskManager permettent à un utilisateur Workspace d’appeler le service.

**Paramètres des points de fin TaskManager**

Définissez les paramètres suivants pour configurer un point de fin TaskManager.

**Nom :** (obligatoire) identifie le point de terminaison. Le nom est affiché dans l’affichage carte de Workspace. N’incluez pas de caractère « &lt; », car le nom affiché dans Workspace serait tronqué. Si vous saisissez une URL en tant que nom de point de fin, assurez-vous que celle-ci est conforme aux normes syntaxiques en la matière précisées dans le document RFC1738.

**Description :** fournit une description du point de terminaison. N’incluez pas de caractère « &lt; », car la description affichée dans Workspace serait tronquée.

**Instructions :** instructions destinées à l’utilisateur qui démarre ce workflow.

**Responsable du processus :** nom de la personne chargée du processus.

**L’utilisateur peut transférer la tâche :** permet à l’utilisateur de transférer la tâche initiale.

**Afficher la fenêtre de pièce jointe :** autorise l’utilisateur à voir la fenêtre de pièce jointe.

**Autoriser l’ajout de pièces jointes :** autorise l’utilisateur à ajouter des pièces jointes et des notes.

**Tâche initialement verrouillée :** verrouille la tâche initiale.

**Ajout de listes ACL pour les files d’attente partagées :** la tâche initiale est créée avec des listes de contrôle d’accès pour les utilisateurs de file d’attente partagée.

**Catégorisation :** (obligatoire) catégorie dans laquelle l’utilisateur verra le formulaire dans Workspace. Sélectionnez une catégorie dans la liste ou sélectionnez Nouvelle catégorie pour ajouter une catégorie.

**Nom de l’opération :** (obligatoire) liste des opérations pouvant être attribuées au point de terminaison.
