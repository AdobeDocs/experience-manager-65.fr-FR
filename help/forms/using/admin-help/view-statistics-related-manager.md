---
title: Afficher les statistiques relatives à Work Manager
seo-title: View statistics related to Work Manager
description: L’onglet Work Manager affiche des statistiques relatives aux éléments de Work Manager. Découvrez comment afficher et filtrer les tâches.
seo-description: The Work Manager tab displays statistics that relate to Work Manager items. Learn how you can view and filter the work items.
uuid: c3a575c7-773d-477a-bc75-6cbcf8b836b8
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/health_monitor
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 8e1b2f7c-2609-474b-a1b2-fa820df74ae3
exl-id: ce8f7257-bb9a-428d-b816-27b1d1632ee1
source-git-commit: 50d29c967a675db92e077916fb4adef6d2d98a1a
workflow-type: tm+mt
source-wordcount: '1211'
ht-degree: 34%

---

# Afficher les statistiques relatives à Work Manager {#view-statistics-related-to-work-manager}

L’onglet Work Manager affiche des statistiques relatives aux éléments de Work Manager. Ces tâches se trouvent dans différents états en fonction de l’endroit où elles se trouvent dans leur processus. (Voir [État (pour les catégories Par défaut, Workflow ou Événements uniquement)](view-statistics-related-manager.md#status-for-default-workflow-or-events-categories-only).) Vous pouvez filtrer les informations afin de n’afficher qu’un sous-ensemble des éléments à l’aide des différentes options disponibles (par exemple, État ou Catégorie). Vous pouvez trier les tâches ou les tâches qui en résultent (par ordre croissant ou décroissant) en cliquant sur l’un des en-têtes de colonne. Vous pouvez également gérer les tâches à l’aide des outils d’opération affichés au-dessus de la liste des tâches.

## Filtrage des éléments de travail {#filter-the-work-items}

1. Cliquez sur l’onglet Work Manager.
1. Sélectionnez les critères d’un ou de plusieurs des filtres décrits ci-dessous, puis cliquez sur Aller.

### Catégorie {#category}

**Par défaut :** toutes les tâches auxquelles le client n’a pas affecté de catégorie lors de leur envoi. Ces tâches étant gérées par Work Manager, les états lui appartiennent.

**Gestionnaire de tâches :** toutes les tâches appartenant au gestionnaire de tâches. Job Manager gère ses propres tâches et dispose de ses propres états de tâches. Reportez-vous aux états spécifiques des tâches décrits ci-dessous.

**Workflow :** toutes les tâches appartenant à l’exécution de workflow. Workflow ne gère pas ses propres tâches, mais s’appuie sur Work Manager ; les états appartiennent donc à ce dernier.

**Événements :** toutes les tâches appartenant à Gestion des événements. La gestion des événements ne gère pas ses propres tâches, mais s’appuie sur Work Manager. Par conséquent, les états appartiennent à Work Manager.

### État (pour les catégories Par défaut, Workflow ou Événements uniquement) {#status-for-default-workflow-or-events-categories-only}

**Tout afficher :** affiche toutes les tâches actuelles.

**Programmé :** affiche toutes les tâches prêtes à être exécutées par le serveur d’applications mais pas encore entamées.

**En pause :** affiche toutes les tâches programmées que l’application cliente a mises en pause. Elles peuvent être exécutées ou supprimées (voir Gestion des tâches). 

**En cours :** affiche toutes les tâches que le Work Manager du serveur d’applications a sélectionnées et qui seront menées à bien ou échoueront. Vous ne pouvez pas utiliser d’opérations sur ces tâches.

**Terminé :** affiche toutes les tâches exécutées avec succès. Les tâches persistantes restent dans cet état et les tâches non persistantes sont supprimées une fois les rappels vers les gestionnaires de rappel terminés. Vous pouvez supprimer ces éléments à l’aide de l’opération Supprimer les éléments . (voir Gestion des tâches). 

**Échec :** affiche toutes les tâches n’ayant pas été exécutées avec succès en raison d’une erreur. Ces tâches peuvent être relancées à plusieurs reprises en utilisant l’opération Essayer de relancer les éléments (voir Gestion des tâches). Un lien Echec dans la colonne Etat permet d&#39;accéder aux détails de l&#39;échec.

**Inconnu :** affiche toutes les tâches dont l’état est inconnu.

### Etat (pour la catégorie Job Manager uniquement) {#status-for-job-manager-category-only}

**Terminé :** affiche toutes les tâches exécutées avec succès. Les tâches persistantes restent dans cet état et les tâches non persistantes sont supprimées une fois les rappels vers les gestionnaires de rappel terminés.

**Fin demandée :** affiche les tâches pour lesquelles une demande de fin a été effectuée.

**Échec de la demande :** affiche les tâches pour lesquelles une demande d’échec a été effectuée.

**Échec :** affiche les tâches n’ayant pas été exécutées avec succès en raison d’une erreur. Un lien Echec dans la colonne Etat permet d&#39;accéder aux détails de l&#39;échec.

**Interruption demandée :** affiche les tâches pour lesquelles une demande d’interruption a été effectuée.

**Interrompu :** affiche les tâches ayant pris fin sans avoir été menées à bien.

**Suspension demandée :** affiche les tâches pour lesquelles une demande de suspension a été effectuée.

**Suspendu :** affiche les tâches suspendues.

**Relance demandée :** affiche les tâches pour lesquelles une demande de relance a été effectuée.

**En file d’attente :** affiche les tâches présentes dans la file d’attente.

**En cours :** affiche les tâches en cours d’exécution.

### Nom du serveur {#server-name}

Pour les serveurs en grappe uniquement, sélectionnez le nom du noeud pour afficher les tâches ou les tâches qui ont été créées sur ce serveur uniquement. Si l’option Tout afficher est sélectionnée, toutes les tâches de tous les noeuds d’une grappe sont affichées.

### Heure de création {#create-time}

Sélectionnez une option dans ce filtre pour n’afficher que les tâches qui ont été créées pendant la période sélectionnée. Par exemple, si vous sélectionnez 1 jour , toutes les tâches qui ont été créées dans les 24 heures précédant l’heure définie dans le filtre Avant.

### Avant {#prior-to}

Définit la date et l’heure utilisées par le filtre Heure de création comme date de fin. Conservez l’option Utiliser la date et l’heure actuelles sélectionnée pour filtrer à partir de la date et de l’heure actuelles, ou désélectionnez l’option et saisissez les valeurs appropriées. Cliquez sur les icônes de calendrier ou d’horloge pour sélectionner des valeurs à l’aide de ces outils.

Par exemple, la sélection de l’option Heure de création = 1 jour et Avant = Utiliser la date et l’heure actuelles renvoie toutes les tâches créées au cours des dernières 24 heures.

>[!NOTE]
>
>Sur les déploiements de base de données Oracle, les filtres de période (c’est-à-dire les paramètres Heure de création et Avant) ne fonctionnent pas correctement. Utilisez un autre filtre pour récupérer les tâches.

## A propos de l’interface de l’onglet Work Manager {#about-the-work-manager-tab-interface}

Lorsque vous exécutez une requête Work Manager ou effectuez une opération sur une tâche, un message s’affiche au-dessus de la liste. Ce message fournit des commentaires sur l’action que vous avez lancée et, dans certains cas, un lien Plus d’informations pour fournir des détails. Par exemple, si l’opération que vous avez lancée a échoué, le message indique autant et fournit un lien pour obtenir des détails sur l’erreur.

Lorsque vous cliquez sur Plus d’informations, la boîte de dialogue Détails de l’opération affiche la liste des tâches qui ont été sélectionnées au cours de l’opération. Vous pouvez cliquer sur chaque élément de la liste pour afficher les détails de l’erreur au bas de la boîte de dialogue.

### Gestion des tâches {#manage-the-work-items-or-jobs}

1. Utilisez les outils d’opération décrits ci-dessous pour gérer les tâches de la liste.

   >[!NOTE]
   >
   >Les opérations sont disponibles en fonction de l’état de l’élément.

   **Supprimer des éléments :** Supprime la tâche sélectionnée.

   **Interrompre les éléments :** interrompt la tâche sélectionnée.

   **Relancer les éléments :** relance la tâche sélectionnée depuis son état en pause.

   **Essayer de relancer les éléments :** essaie de relancer la tâche sélectionnée depuis son état actuel.

   Vous pouvez vérifier si une opération a réussi en cliquant sur Plus d’informations au-dessus de la liste. Une boîte de dialogue contenant les tâches sélectionnées et leur état s’affiche.

## Informations supplémentaires sur les états des éléments de travail {#additional-information-about-work-item-statuses}

Une transition d’état standard pour une tâche est Nouveau > Planifié > En cours > Terminé ou Échec.

L’état En pause interrompt ce flux normal. L’application cliente ou l’administrateur système peuvent lancer cette interruption (par exemple, pour la maintenance ou la mise à niveau). Vous pouvez inverser cette action en utilisant l’opération Reprendre pour remettre l’élément de travail à l’état Planifié.

Un élément de travail à l’état Planifié est mis en file d’attente pour exécution qui n’a pas encore commencé. Ces éléments peuvent être suspendus ou supprimés, ou passeront à l’état En cours lorsque Work Manager les sortira de la file d’attente. Les éléments de travail en cours ne peuvent pas être modifiés. Ils seront terminés ou échoueront.

L’état Échec se produit à la suite d’une condition d’erreur qui se produit lors de l’exécution de l’élément de travail. Si vous pensez que les erreurs sont circonstancielles (en raison du contexte au moment de l’exécution), vous pouvez relancer l’exécution, remettant l’élément de travail dans la file d’attente. Seul un nombre limité de reprises est autorisé.
