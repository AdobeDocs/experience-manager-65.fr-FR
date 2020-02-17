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

---


# Configuration des points de fin TaskManager {#configuring-task-manager-endpoints}

Les points de fin TaskManager permettent à un utilisateur Workspace d’appeler le service.

**Paramètres des points de fin TaskManager**

Définissez les paramètres suivants pour configurer un point de fin TaskManager.

**** Nom : (obligatoire) identifie le point de fin. Le nom est affiché dans l’affichage carte de Workspace. N’incluez pas de caractère « &lt; », car le nom affiché dans Workspace serait tronqué. Si vous saisissez une URL en tant que nom de point de fin, assurez-vous que celle-ci est conforme aux normes syntaxiques en la matière précisées dans le document RFC1738.

**** Description : Description du point de fin. N’incluez pas de caractère « &lt; », car la description affichée dans Workspace serait tronquée.

**** Instructions de la tâche : Instructions à l’intention de l’utilisateur qui lance ce flux de travail.

**** Propriétaire du processus : Nom de la personne responsable du processus.

**** L’utilisateur peut transférer la tâche : Permet à l’utilisateur de transférer la tâche initiale.

**** Afficher la fenêtre de pièce jointe : Permet à l’utilisateur de voir la fenêtre de pièce jointe.

**** Autoriser l’ajout de pièces jointes : Permet à l’utilisateur d’ajouter des pièces jointes et des notes.

**** Tâche initialement verrouillée : Verrouille la tâche initiale.

**** Ajouter des listes de contrôle d’accès pour les files d’attente partagées : La tâche initiale est créée avec des listes de contrôle d’accès pour les utilisateurs de files d’attente partagées.

**** Catégorisation : (obligatoire) catégorie dans laquelle l’utilisateur verra le formulaire dans Workspace. Sélectionnez une catégorie dans la liste ou sélectionnez Nouvelle catégorie pour ajouter une catégorie.

**** Nom de l’opération : (obligatoire) liste des opérations pouvant être attribuées au point de fin.
