---
title: Rapports des Requêtes ad hoc dans le processus
seo-title: Rapports des Requêtes ad hoc dans le processus
description: Créez des requêtes personnalisées pour rechercher les détails de processus et de tâche AEM Forms on JEE dans le Rapports de processus.
seo-description: Créez des requêtes personnalisées pour rechercher les détails de processus et de tâche AEM Forms on JEE dans le Rapports de processus.
uuid: db0c5c28-b213-4582-a6ed-df127e570a4e
content-type: reference
topic-tags: process-reporting
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: b0a544e2-2ce4-48e2-a721-82f481d36004
docset: aem65
translation-type: tm+mt
source-git-commit: 56c6cfd437ef185336e81373bd5f758205b96317
workflow-type: tm+mt
source-wordcount: '1695'
ht-degree: 0%

---


# Rapports des Requêtes ad hoc dans le processus{#ad-hoc-queries-in-process-reporting}

## Rapports des requêtes ad hoc dans le processus {#ad-hoc-queries-in-process-reporting-1}

Les requêtes ad hoc dans le Rapports de processus vous permettent de créer des requêtes personnalisées que vous pouvez utiliser pour rechercher les détails de processus et de tâche des instances de processus AEM Forms définies dans votre environnement AEM Forms.

En outre, les requêtes ad hoc peuvent être définies à l’aide de filtres de propriétés de processus et de tâche. Ces filtres peuvent ensuite être enregistrés et utilisés pour exécuter les rapports ultérieurement.

[**Recherche**](/help/forms/using/process-reporting/adhoc-queries-in-process-reporting.md#p-process-task-search-p) de processus : Recherchez des instances de processus avec un filtre de recherche défini par l’utilisateur en fonction d’attributs de processus.

[**Détails**](/help/forms/using/process-reporting/adhoc-queries-in-process-reporting.md#p-process-task-details-p) du processus : Détails de la vue d’une instance de processus en spécifiant l’ID de processus.

**Tâche Search**: Recherchez des instances de tâche avec un filtre de recherche défini par l’utilisateur en fonction d’attributs de tâche.

**Détails** de la tâche : Détails de la vue d’une instance de tâche en spécifiant l’identifiant de tâche.

### Processus et Tâches {#processes-and-tasks}

Les étapes que vous suivez pour créer des filtres et exécuter des requêtes pour les détails du processus sont les mêmes que pour les tâches.

Cela signifie que les interfaces utilisateur pour la recherche de processus et la recherche de Tâche diffèrent uniquement dans les champs par lesquels vous pouvez effectuer une recherche et dans les champs renvoyés dans les résultats de la recherche. Cela s’explique simplement par le fait que, bien que de nombreux champs soient identiques, certains champs sont spécifiques aux processus et certains champs sont spécifiques aux tâches.

Cet article détaille les descriptions des sections Process/Tâche Search and Process/Tâche Details. Dans les endroits appropriés, toute différence spécifique sera spécifiquement appelée.

## Recherche de processus/Tâche {#process-task-search}

Vous utilisez la recherche de processus/Tâche pour définir des filtres pour interroger les instances de processus/tâche.

### Pour créer une requête de recherche de processus/Tâche {#to-create-a-process-task-search-query}

1. Pour vue des requêtes de recherche de processus/Tâche enregistrées ou pour créer une requête, cliquez sur Requêtes **** ad hoc, puis sur Recherche **** de processus/Tâche.

   ![search_nodes](assets/search_nodes.png)

   Le panneau **Mes Filtres** s’affiche à droite de la vue de l’arborescence.

   Dans le panneau **Mes Filtres** , vous pouvez créer des requêtes ad hoc et cliquer pour exécuter des requêtes précédemment enregistrées.

   ![my_filtres_panel](assets/my_filters_panel.png)

1. Pour exécuter une requête existante, il vous suffit de cliquer sur la requête dans le panneau **Mes Filtres** .
1. Pour créer une requête, cliquez sur **Ajouter** (+).

   Le panneau **Créer un filtre** s’affiche.

   ![create_filter_panel](assets/create_filter_panel.png)

   Une requête se compose d’un ou de plusieurs filtres de requête. Pour créer un filtre, ajoutez une rangée de filtre à la requête. Par défaut, une ligne de filtre est ajoutée à la requête.

   **Pour définir un filtre**

   1. Sélectionnez un champ.

      ![filter_field](assets/filter_field.png)

      >[!NOTE]
      >
      >La liste de champs contient les champs spécifiques au processus/tâche AEM Forms.

   1. Sélectionnez une condition.

      ![filter_condition](assets/filter_condition.png)

      >[!NOTE]
      >
      >Les conditions répertoriées dépendent de l’attribut sélectionné pour le filtrage.

   1. Saisissez une valeur.

      ![filter_value](assets/filter_value.png)

   1. Pour ajouter un autre filtre à la requête, cliquez sur **Ajouter (+)** à droite de la ligne de filtre.

      Pour supprimer un filtre de la requête, cliquez sur **Supprimer (-)** à droite de la ligne de filtre.

      ![filter_add_del](assets/filter_add_del.png)

Après avoir créé une requête, utilisez les options situées dans le coin supérieur droit du panneau **Créer un filtre** pour :

* **Annuler**: Annulez les modifications et revenez au panneau **Mes Filtres** .
* **Exécuter**: Exécutez la requête actuelle pour afficher et/ou vérifier les résultats. Dans ce cas, il n’est pas nécessaire d’enregistrer la requête avant d’exécuter la requête. Vous pouvez vérifier les résultats, apporter des modifications si nécessaire, puis enregistrer la requête lorsque la sortie vous convient.
* **Enregistrer**: Enregistrez le filtre. Le filtre peut ensuite être affiché et exécuté à partir du panneau **Mes Filtres** .

### Options dans le panneau Mes Filtres {#options-in-my-filters-panel}

Utilisez les options du panneau **Mes Filtres** pour **Ajouter** ![lc_pr_add_filter](assets/lc_pr_add_filter.png), **Edit lc_pr_delete_filter ou Deletelc_pr_edit_filteran ad hoc requête.**![](assets/lc_pr_delete_filter.png)****![](assets/lc_pr_edit_filter.png)

![my_filtres_options](assets/my_filters_options.png)

### Pour exécuter une requête de recherche {#to-execute-a-search-query}

1. Pour exécuter une requête, cliquez sur le filtre dans le panneau **Mes Filtres** ou cliquez sur le bouton **Exécuter** si vous créez ou modifiez un filtre.
1. Les résultats de la requête s’affichent dans le panneau **Rapport** de la fenêtre Rapports **de** processus.

   ![process_search_result](assets/process_search_result.png)

   Vous pouvez paginer les résultats de la recherche à l&#39;aide du panneau de pagination affiché au bas du rapport.

   ![process_result_pgn](assets/process_result_pgn.png)

   Dans la liste **déroulante Afficher** , choisissez le nombre de résultats à afficher par page.

   Dans la zone de texte **Page** , entrez un numéro de page pour accéder directement à cette page.

1. Les champs suivants s’affichent dans un résultat de recherche de processus :

   * **ID** du processus : ID du processus. Le champ est lié par un hyperlien. Si vous cliquez sur un ID de processus dans ce champ, vous êtes redirigé vers le panneau Détails **[!UICONTROL du]** processus pour le processus.
   * **Initiateur**: Utilisateur AEM Forms qui a démarré l’instance de processus
   * **Heure** de création : Date et heure de démarrage de l’instance de processus
   * **Heure** terminée : Date et heure auxquelles l’instance de processus s’est terminée
   * **Durée**: Durée du début à la fin de l’instance de processus
   * **État**: Statut actuel de l’instance de processus.

   Par défaut, le résultat est trié par ID de processus. Cependant, pour trier le résultat selon l’un des champs, cliquez sur le titre du champ.

   Puisque le tri est une opération de basculement, cliquez sur un en-tête de colonne pour trier le résultat par ordre croissant et cliquez de nouveau dessus pour trier par ordre décroissant.

   De même, les champs suivants s’affichent dans un résultat de recherche de Tâche :

   * **ID** de tâche : ID de la tâche. Le champ est lié par un hyperlien. Si vous cliquez sur un ID de tâche dans ce champ, vous êtes redirigé vers le panneau Détails **[!UICONTROL de la]** Tâche pour la tâche.
   * **Initiateur**: Utilisateur AEM Forms qui a démarré l’instance de processus
   * **Heure** de création : Date et heure de démarrage de l’instance de processus
   * **Heure** terminée : Date et heure auxquelles l’instance de processus s’est terminée
   * **Durée**: Durée du début à la fin de l’instance de processus
   * **État**: Statut actuel de l’instance de processus.

   Par défaut, le résultat est trié par ID de Tâche. Cependant, pour trier le résultat selon l’un des champs, cliquez sur le titre du champ. Le résultat est trié selon la colonne indiquée par une flèche sombre en regard de l’en-tête de colonne.

   Puisque le tri est une opération de basculement, cliquez sur un en-tête de champ pour trier le résultat par ordre croissant et cliquez de nouveau dessus pour trier par ordre décroissant. L&#39;ordre de tri actuel (croissant/décroissant) est indiqué par la direction de la flèche sombre en regard de l&#39;en-tête de colonne.

   ![tâche_search_result](assets/task_search_result.png)

1. Cliquez sur le bouton ![](assets/lc_pr_rail_button.png) lc_pr_rail_button **dans l’angle supérieur gauche pour réduire le volet** Mes Filtres **et augmenter l’espace disponible pour le panneau** Rapport.
1. Utilisez les options situées dans le coin supérieur droit du **panneau **Rapport **pour effectuer des opérations sur le résultat de la requête.

   * **Actualiser**: Actualise le rapport avec les dernières données stockées dans l&#39;enregistrement

   * **Exporter au format CSV**: Exportez les données du rapport dans un fichier séparé par des virgules.
   >[!NOTE]
   >
   >Lorsque vous exportez un rapport, le résultat entier de la recherche est exporté dans un fichier CSV et pas seulement la page active.

## Détails du processus/de la Tâche {#process-task-details}

Utilisez le panneau Détails **du** processus pour vue les détails d’un processus spécifique.

De même, vous utilisez le panneau Détails **de la** Tâche pour vue des détails d’une tâche spécifique.

### Pour vue des détails sur le processus/la Tâche {#to-view-process-task-details}

Vous pouvez vue les détails d’un processus/tâche AEM Forms spécifique :

* **A partir d&#39;un résultat de recherche de processus/Tâche**
* **En saisissant l’ID de processus/de Tâche dans le panneau Détails du processus/de la Tâche**

#### A partir d&#39;un résultat de recherche de processus/Tâche {#from-a-process-task-search-result}

1. Exécutez une recherche de processus/tâche. Pour plus d’informations, voir [Exécution d’une requête](#to-execute-a-search-query)de recherche de processus.

   Notez que les ID de processus affichés dans le résultat sont liés par un hyperlien.

   ![process_id_liste](assets/process_id_list.png)

1. Cliquez sur un ID de processus dans la liste pour vue les détails de ce processus dans le panneau Détails **du** processus.

   Le résultat de la requête Détails **du** processus/de la Tâche affiche les détails des tâches/formulaires contenus dans le processus/la tâche.

   Par défaut, le résultat est trié par Tâche/ID de formulaire. Cependant, pour trier le résultat selon l’un des champs, cliquez sur le titre du champ. La colonne de tri du résultat est indiquée par une flèche foncée en regard de l’en-tête de colonne.

   Puisque le tri est une opération de basculement, cliquez sur un en-tête de champ pour trier le résultat par ordre croissant et cliquez de nouveau dessus pour trier par ordre décroissant. L&#39;ordre de tri actuel (croissant/décroissant) est indiqué par la direction de la flèche sombre en regard de l&#39;en-tête de colonne.

   **Résultat des détails du processus**

   ![process_details](assets/process_details.png)

   **Panneau de gauche :** Affiche les détails suivants du processus sélectionné :

   * Nom du processus
   * Date de création du processus
   * Heure de fin du processus
   * Durée du processus
   * Statut du processus
   * Initiateur du processus

   **Panneau supérieur droit :** Affiche les détails suivants des tâches qui composent le processus sélectionné :

   * ID de tâche
   * Nom de la tâche
   * Propriétaire de la tâche
   * Date de création de la tâche
   * Date de mise à jour de la tâche
   * Date de fin de tâche
   * Durée de la tâche
   * Statut de la tâche

   **Panneau inférieur droit :** Affiche les détails suivants de l&#39;historique des processus du processus sélectionné :

   * Nom du processus
   * Initiateur du processus
   * Heure de mise à jour du processus
   * Heure de fin du processus
   * Statut du processus

   **Résultat des détails de la tâche**

   ![task_details](assets/task_details.png)

   **Panneau de gauche :** Affiche les détails suivants de la tâche sélectionnée :

   * Nom de la tâche
   * ID du processus auquel cette tâche appartient
   * Description de la tâche
   * Date de création de la tâche
   * Date de fin de tâche
   * Durée de la tâche
   * Statut de la tâche
   * Chemin de tâche sélectionné

   **Panneau supérieur droit :** Affiche les détails suivants des formulaires qui composent la tâche sélectionnée :

   * ID de formulaire
   * Date de création du formulaire
   * Date de mise à jour du formulaire
   * URL du modèle de formulaire

   **Panneau inférieur droit :** Affiche les détails suivants de l&#39;historique des processus de la tâche sélectionnée :

   * Type d&#39;affectation de tâche
   * Propriétaire de la tâche
   * Date de création de l&#39;affectation de tâche
   * Date de mise à jour de la tâche






1. Cliquez sur **Retour à Recherche** de processus/Tâche pour revenir au résultat de la recherche à partir duquel les détails du processus/de la tâche ont été analysés.

   ![back_to_search](assets/back_to_search.png)

   Cependant, si les détails du processus/de la tâche ont été trouvés en saisissant un ID de processus/de tâche spécifique, cliquez sur Retour au processus/Recherche de Tâche pour revenir à la recherche **de** processus/de Tâche, sans afficher aucun résultat de recherche.

#### En saisissant l’ID de processus/de Tâche dans le panneau Détails du processus/de la Tâche {#by-entering-the-process-task-id-in-the-process-task-details-panel-br}

1. Accédez au panneau Détails **du** processus/de la Tâche.

   ![details_nodes](assets/details_nodes.png)

1. Dans la zone de texte ID de processus/de Tâche, saisissez l’ID de processus/de tâche.

   ![process_details-1](assets/process_details-1.png)

   Les champs du résultat de la requête Détails **du** processus/Tâche sont des champs spécifiques à un processus/tâche AEM Forms.

   Pour un processus, le résultat de la requête affiche les détails des tâches contenues dans le processus.

   Pour une tâche, le résultat de la requête affiche les détails des formulaires contenus dans la tâche.
