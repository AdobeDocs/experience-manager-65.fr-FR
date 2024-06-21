---
title: Configurer des points d’entrée TaskManager
description: Découvrez comment configurer des points d’entrée Task Manager pour appeler le service. Différents paramètres sont requis pour la configuration des points d’entrée Task Manager.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/managing_endpoints
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: 8495a3d7-6ac9-41f5-b1f9-31decaba118a
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: e821be5233fd5f6688507096790d219d25903892
workflow-type: tm+mt
source-wordcount: '245'
ht-degree: 100%

---

# Configuration des points d’entrée TaskManager {#configuring-task-manager-endpoints}

Les points d’entrée Task Manager permettent aux utilisateurs et utilisatrices de Workspace d’appeler le service.

**Paramètres des points d’entrée de Task Manager**

Utilisez les paramètres suivants pour configurer un point d’entrée Task Manager.

**Nom :** (obligatoire) identifie le point d’entrée. Le nom est affiché dans l’affichage carte de Workspace. N’incluez pas de caractère « &lt; », car le nom affiché dans Workspace serait tronqué. Si vous saisissez une URL en tant que nom de point d’entrée, assurez-vous que celle-ci est conforme aux normes syntaxiques en la matière précisées dans le document RFC1738.

**Description :** fournit une description du point d’entrée. N’incluez pas de caractère « &lt; », car la description affichée dans Workspace serait tronquée.

**Instructions :** instructions destinées à l’utilisateur qui démarre ce workflow.

**Responsable du processus :** nom de la personne chargée du processus.

**L’utilisateur peut transférer la tâche :** permet à l’utilisateur de transférer la tâche initiale.

**Afficher la fenêtre de pièce jointe :** autorise l’utilisateur à voir la fenêtre de pièce jointe.

**Autoriser l’ajout de pièces jointes :** autorise l’utilisateur à ajouter des pièces jointes et des notes.

**Tâche initialement verrouillée :** verrouille la tâche initiale.

**Ajout de listes ACL pour les files d’attente partagées :** la tâche initiale est créée avec des listes de contrôle d’accès pour les utilisateurs de file d’attente partagée.

**Catégorisation :** (obligatoire) catégorie dans laquelle l’utilisateur verra le formulaire dans Workspace. Sélectionnez une catégorie dans la liste ou sélectionnez Nouvelle catégorie pour ajouter une catégorie.

**Nom de l’opération :** (obligatoire) liste des opérations pouvant être attribuées au point d’entrée.
