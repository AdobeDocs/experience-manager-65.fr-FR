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

**Description : description** du point de terminaison. N’incluez pas de caractère « &lt; », car la description affichée dans Workspace serait tronquée.

**Instructions de tâche :** instructions destinées à l’utilisateur qui début ce flux de travail.

**Propriétaire du processus :** nom de la personne responsable du processus.

**L’utilisateur peut transférer la Tâche :** permet à l’utilisateur de transférer la tâche initiale.

**Afficher la fenêtre de pièce jointe :** permet à l’utilisateur de voir la fenêtre de pièce jointe.

**Autoriser l’Ajoute des pièces jointes :** permet à l’utilisateur d’ajouter des pièces jointes et des notes.

**Tâche initialement verrouillée :** verrouille la tâche initiale.

**Ajouter des listes de contrôle d’accès pour les files d’attente partagées :** la tâche initiale est créée avec des listes de contrôle d’accès pour les utilisateurs des files d’attente partagées.

**Catégorisation :**  (obligatoire) catégorie dans laquelle l’utilisateur voit le formulaire dans Workspace. Sélectionnez une catégorie dans la liste ou sélectionnez Nouvelle catégorie pour ajouter une catégorie.

**Nom de l’opération :** (obligatoire) liste d’opérations pouvant être attribuées au point de terminaison.
