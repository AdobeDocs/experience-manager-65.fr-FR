---
title: Afficher les statistiques relatives à Work Manager
description: L’onglet Work Manager affiche des statistiques relatives aux éléments de Work Manager. Découvrez comment afficher et filtrer les tâches.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/health_monitor
products: SG_EXPERIENCEMANAGER/6.5/FORMS
exl-id: ce8f7257-bb9a-428d-b816-27b1d1632ee1
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: tm+mt
source-wordcount: '1215'
ht-degree: 100%

---

# Afficher les statistiques relatives à Work Manager {#view-statistics-related-to-work-manager}

L’onglet Work Manager affiche des statistiques relatives aux éléments de Work Manager. Ces tâches se trouvent dans différents états, en fonction de l’endroit où elles se trouvent dans leur processus. (Voir [Statut (pour les catégories Par défaut, Workflow ou Événements uniquement)](view-statistics-related-manager.md#status-for-default-workflow-or-events-categories-only).) Vous pouvez filtrer les informations afin de n’afficher qu’un sous-ensemble des éléments à l’aide des différentes options disponibles (par exemple, Statut ou Catégorie). Vous pouvez trier les tâches ou travaux qui en résultent (par ordre croissant ou décroissant) en cliquant sur l’un des en-têtes de colonne. Vous pouvez également gérer les tâches à l’aide des outils d’opération affichés au-dessus de la liste des tâches.

## Filtrage des tâches {#filter-the-work-items}

1. Cliquez sur l’onglet Work Manager.
1. Choisissez des critères pour un ou plusieurs des filtres suivants, tels que décrits ci-dessous, puis cliquez sur Atteindre.

### Catégorie {#category}

**Par défaut :** toutes les tâches auxquelles le client n’a pas affecté de catégorie lors de leur envoi. Ces tâches étant gérées par Work Manager, les états lui appartiennent.

**Gestionnaire de tâches :** toutes les tâches appartenant au gestionnaire de tâches. Job Manager gère ses propres tâches et dispose de ses propres statuts de tâches. Reportez-vous aux statuts spécifiques des tâches décrits ci-dessous.

**Workflow :** toutes les tâches appartenant à l’exécution de workflow. Workflow ne gère pas ses propres tâches, mais s’appuie sur Work Manager ; les états appartiennent donc à ce dernier.

**Événements :** toutes les tâches appartenant à Gestion des événements. La Gestion des événements ne gère pas ses propres tâches, mais s’appuie sur Work Manager. Les statuts appartiennent donc à ce dernier.

### Statut (pour les catégories Par défaut, Workflow ou Événements uniquement) {#status-for-default-workflow-or-events-categories-only}

**Tout afficher :** affiche toutes les tâches actuelles.

**Programmé :** affiche toutes les tâches prêtes à être exécutées par le serveur d’applications mais pas encore entamées.

**En pause :** affiche toutes les tâches programmées que l’application cliente a mises en pause. Elles peuvent être exécutées ou supprimées (voir Gestion des tâches). 

**En cours :** affiche toutes les tâches que le Work Manager du serveur d’applications a sélectionnées et qui seront menées à bien ou échoueront. Vous ne pouvez pas utiliser d’opérations sur ces tâches.

**Terminé :** affiche toutes les tâches exécutées avec succès. Les tâches persistantes restent dans cet état et les tâches non persistantes sont supprimées une fois les rappels vers les gestionnaires de rappel terminés. Vous pouvez supprimer ces éléments à l’aide de l’opération Supprimer les éléments. (voir Gestion des tâches). 

**Échec :** affiche toutes les tâches n’ayant pas été exécutées avec succès en raison d’une erreur. Ces tâches peuvent être relancées à plusieurs reprises en utilisant l’opération Essayer de relancer les éléments (voir Gestion des tâches). Un lien Échec dans la colonne Statut vous permet d’accéder à des informations détaillées relatives à l’échec.

**Inconnu :** affiche toutes les tâches dont l’état est inconnu.

### Etat (pour la catégorie Job Manager uniquement) {#status-for-job-manager-category-only}

**Terminé :** affiche toutes les tâches exécutées avec succès. Les tâches persistantes restent dans cet état et les tâches non persistantes sont supprimées une fois les rappels vers les gestionnaires de rappel terminés.

**Fin demandée :** affiche les tâches pour lesquelles une demande de fin a été effectuée.

**Échec de la demande :** affiche les tâches pour lesquelles une demande d’échec a été effectuée.

**Échec :** affiche les tâches n’ayant pas été exécutées avec succès en raison d’une erreur. Un lien Échec dans la colonne Statut vous permet d’accéder à des informations détaillées relatives à l’échec.

**Interruption demandée :** affiche les tâches pour lesquelles une demande d’interruption a été effectuée.

**Interrompu :** affiche les tâches ayant pris fin sans avoir été menées à bien.

**Suspension demandée :** affiche les tâches pour lesquelles une demande de suspension a été effectuée.

**Suspendu :** affiche les tâches suspendues.

**Relance demandée :** affiche les tâches pour lesquelles une demande de relance a été effectuée.

**En file d’attente :** affiche les tâches présentes dans la file d’attente.

**En cours :** affiche les tâches en cours d’exécution.

### Nom du serveur {#server-name}

Pour les serveurs organisés en grappes uniquement, sélectionnez le nom du nœud pour afficher les tâches ayant été créées sur ce serveur uniquement. Si Tout afficher est sélectionné, toutes les tâches de tous les nœuds d’un cluster sont affichées.

### Heure de création {#create-time}

Choisissez une option de ce filtre pour afficher uniquement les tâches ayant été créées dans la période sélectionnée. Par exemple, sélectionner 1 jour permet d’afficher toutes les tâches ayant été créées dans les 24 heures précédant l’heure définie dans le champ Avant.

### Avant {#prior-to}

Définit la date et l’heure utilisées par le filtre Heure de création en tant que date de fin. Conservez l’option Utiliser la date et l’heure actuelles sélectionnée pour filtrer à partir de la date et de l’heure actuelles, ou désélectionnez-la et entrez les valeurs appropriées. Cliquez sur les icônes de calendrier ou celles d’horloge pour sélectionner les valeurs en utilisant ces outils.

Par exemple, sélectionner Heure de création = 1 jour et Avant = Utiliser la date et l’heure actuelles renvoie toutes les tâches ayant été créées au cours des dernières 24 heures.

>[!NOTE]
>
>sur les déploiements de bases de données Oracle, les filtres de période (à savoir les paramètres Heures de création et Avant) ne sont pas précis. Utilisez un autre filtre pour récupérer les tâches.

## À propos de l’interface à onglets de Work Manager {#about-the-work-manager-tab-interface}

Lorsque vous exécutez une requête Work Manager ou effectuez une opération sur une tâche, un message s’affiche au-dessus de la liste. Ce message fournit des commentaires sur l’action que vous avez lancée et, parfois, un lien Plus d’infos qui fournit des informations détaillées. Par exemple, si l’opération que vous avez lancée échoue, le message l’indique et fournit un lien vous permettant d’obtenir des informations détaillées sur l’erreur.

Lorsque vous cliquez sur Plus d’infos, la boîte de dialogue Détails de l’opération affiche une liste des tâches ayant été sélectionnées au cours de l’opération. Vous pouvez cliquer sur chaque élément de la liste pour afficher les Détails de l’erreur en bas de la boîte de dialogue.

### Gestion des tâches {#manage-the-work-items-or-jobs}

1. Utilisez les outils d’opération décrits ci-dessous pour gérer les tâches de la liste.

   >[!NOTE]
   >
   >Les opérations disponibles dépendent du statut de l’élément.

   **Supprimer les éléments :** supprime la tâche sélectionnée.

   **Interrompre les éléments :** interrompt la tâche sélectionnée.

   **Relancer les éléments :** relance la tâche sélectionnée depuis son état en pause.

   **Essayer de relancer les éléments :** essaie de relancer la tâche sélectionnée depuis son état actuel.

   Vous pouvez vérifier la bonne réussite d’une opération en cliquant sur Plus d’infos au-dessus de la liste. Une boîte de dialogue contenant les tâches sélectionnées ainsi que leur statut s’affiche.

## Informations supplémentaires sur les statuts des tâches {#additional-information-about-work-item-statuses}

Une transition d’état typique pour une tâche se présente comme suit : Nouveau > Programmé > En cours > Terminé ou Échec.

Le statut En pause interrompt ce flux normal. L’application cliente ou l’administrateur ou l’administratrice système peut initier cette interruption (par exemple, à des fins de maintenance ou de mise à niveau). Vous pouvez annuler cette action en utilisant l’opération Relancer pour que la tâche retourne à un état Programmé.

Une tâche à l’état Programmé est mise en file d’attente pour être exécutée, l’exécution n’ayant pas encore commencé. Ces éléments peuvent être mis en pause ou supprimés, ou passeront à l’état En cours lorsque Work Manager les récupérera de la file d’attente. Les tâches en cours ne peuvent pas être modifiées. Elles se terminent ou échouent.

L’état Échec se produit à la suite d’une condition d’erreur qui survient au cours de l’exécution de la tâche. Si vous pensez que les erreurs sont circonstanciées (qu’elles dépendent du contexte au moment de l’exécution), vous pouvez relancer l’exécution et ainsi remettre la tâche en file d’attente. Seul un nombre limité de relances est autorisé.
