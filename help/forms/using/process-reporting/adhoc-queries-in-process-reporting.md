---
title: Requêtes ad hoc dans les rapports de processus
seo-title: Requêtes ad hoc dans les rapports de processus
description: Création de requêtes personnalisées pour rechercher les détails des processus et des tâches d’AEM Forms sur JEE dans Process Reporting
seo-description: Création de requêtes personnalisées pour rechercher les détails des processus et des tâches d’AEM Forms sur JEE dans Process Reporting
uuid: db0c5c28-b213-4582-a6ed-df127e570a4e
content-type: reference
topic-tags: process-reporting
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: b0a544e2-2ce4-48e2-a721-82f481d36004
docset: aem65
translation-type: tm+mt
source-git-commit: 8f90dc4865126d52e04effc9197ef7145b1a167e

---


# Requêtes ad hoc dans les rapports de processus{#ad-hoc-queries-in-process-reporting}

## Requêtes ad hoc dans Process Reporting {#ad-hoc-queries-in-process-reporting-1}

Les requêtes ad hoc dans Process Reporting vous permettent de créer des requêtes personnalisées que vous pouvez utiliser pour rechercher les détails de processus et de tâche des instances de processus AEM Forms définies dans votre environnement AEM Forms.

En outre, les requêtes ad hoc peuvent être définies à l’aide des filtres de propriétés de processus et de tâche. Ces filtres peuvent ensuite être enregistrés et utilisés pour exécuter les rapports ultérieurement.

[**Recherche **](/help/forms/using/process-reporting/adhoc-queries-in-process-reporting.md#p-process-task-search-p)de processus : Recherchez des instances de processus avec un filtre de recherche défini par l’utilisateur en fonction des attributs de processus.

[**Détails **](/help/forms/using/process-reporting/adhoc-queries-in-process-reporting.md#p-process-task-details-p)du processus : Affichez les détails d’une instance de processus en spécifiant l’ID de processus.

**Recherche** de tâche : Recherchez des instances de tâche avec un filtre de recherche défini par l’utilisateur en fonction des attributs de tâche.

**Détails** de la tâche : Affichez les détails d’une instance de tâche en spécifiant l’ID de la tâche.

### Processus et tâches {#processes-and-tasks}

Les étapes que vous suivez pour créer des filtres et exécuter des requêtes pour des détails de processus sont identiques à celles des tâches.

Cela signifie que les interfaces utilisateur pour la recherche de processus et la recherche de tâches diffèrent uniquement dans les champs par lesquels vous pouvez effectuer une recherche et dans les champs renvoyés dans les résultats de la recherche. Cela s’explique simplement par le fait que, bien que de nombreux champs soient identiques, certains champs sont spécifiques aux processus et certains champs sont spécifiques aux tâches.

Cet article décrit en détail les sections Processus/Recherche de tâche et Détails du processus/Tâche. Aux emplacements appropriés, toute différence spécifique sera spécifiquement appelée.

## Recherche de processus/tâche {#process-task-search}

Vous utilisez la recherche de processus/tâche pour définir des filtres pour interroger les instances de processus/tâche.

### Pour créer une requête de recherche de processus/tâche {#to-create-a-process-task-search-query}

1. Pour afficher les requêtes de recherche de processus/tâche enregistrées ou pour créer une requête, cliquez sur Requêtes **** ad hoc, puis sur Recherche **** de processus/tâche.

   ![search_nodes](assets/search_nodes.png)

   Le panneau **Mes filtres** s’affiche à droite de l’arborescence.

   Dans le panneau **Mes filtres** , vous pouvez créer des requêtes ad hoc et cliquer pour exécuter des requêtes précédemment enregistrées.

   ![my_filters_panel](assets/my_filters_panel.png)

1. Pour exécuter une requête existante, il vous suffit de cliquer sur la requête dans le panneau **Mes filtres** .
1. Pour créer une requête, cliquez sur **Ajouter** (+).

   Le panneau **Créer un filtre** s’affiche.

   ![create_filter_panel](assets/create_filter_panel.png)

   Une requête se compose d’un ou de plusieurs filtres de requête. Pour créer un filtre, ajoutez une ligne de filtre à la requête. Par défaut, une ligne de filtre est ajoutée à la requête.

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

   1. Entrez une valeur.

      ![filter_value](assets/filter_value.png)

   1. Pour ajouter un autre filtre à la requête, cliquez sur **Ajouter (+)** à droite de la ligne de filtre.

      Pour supprimer un filtre de la requête, cliquez sur **Supprimer (-)** à droite de la ligne de filtre.

      ![filter_add_del](assets/filter_add_del.png)

Après avoir créé une requête, utilisez les options dans le coin supérieur droit du panneau **Créer un filtre** pour :

* **Annuler**: Annulez les modifications et revenez au panneau **Mes filtres** .
* **Exécuter**: Exécutez la requête actuelle pour afficher et / ou vérifier les résultats. Dans ce cas, vous n’avez pas besoin d’enregistrer la requête avant de l’exécuter. Vous pouvez vérifier les résultats, effectuer des modifications si nécessaire, puis enregistrer la requête lorsque la sortie vous convient.
* **Enregistrer**: Enregistrez le filtre. Le filtre peut ensuite être affiché et exécuté à partir du panneau **Mes filtres** .

### Options du panneau Mes filtres {#options-in-my-filters-panel}

Utilisez les options du panneau **Mes filtres** pour **Ajouter** ![lc_pr_add_filter](assets/lc_pr_add_filter.png), **Modifier lc_pr_delete_filter ouSupprimerlc_pr_edit_filtrer une requête ad hoc.**![](assets/lc_pr_delete_filter.png)****![](assets/lc_pr_edit_filter.png)

![my_filters_options](assets/my_filters_options.png)

### Pour exécuter une requête de recherche {#to-execute-a-search-query}

1. Pour exécuter une requête, cliquez sur le filtre dans le panneau **Mes filtres** ou cliquez sur le bouton **Exécuter** si vous créez ou modifiez un filtre.
1. Les résultats de la requête s’affichent dans le panneau **Rapport** de la fenêtre **Process Reporting** .

   ![process_search_result](assets/process_search_result.png)

   Vous pouvez paginer les résultats de la recherche à l’aide du panneau de pagination affiché au bas du rapport.

   ![process_result_pgn](assets/process_result_pgn.png)

   Dans la liste déroulante **Afficher** , choisissez le nombre de résultats à afficher par page.

   Dans la zone de texte **Page** , saisissez un numéro de page pour accéder directement à cette page.

1. Les champs suivants sont affichés dans un résultat de recherche de processus :

   * **ID** du processus : ID du processus. Le champ est lié par un hyperlien. Si vous cliquez sur un ID de processus dans ce champ, vous êtes redirigé vers le panneau Détails **[!UICONTROL du]** processus pour le processus.
   * **Initiateur**: Utilisateur AEM Forms qui a démarré l’instance de processus
   * **Heure** de création : Date et heure de démarrage de l’instance de processus
   * **Heure** terminée : Date et heure de fin de l’instance de processus
   * **Durée**: Durée du début à la fin de l’instance de processus
   * **État**: Statut actuel de l’instance de processus.
   Par défaut, le résultat est trié par ID de processus. Toutefois, pour trier le résultat selon l’un des champs, cliquez sur le titre du champ.

   Puisque le tri est une opération de basculement, cliquez sur un en-tête de colonne pour trier le résultat par ordre croissant et cliquez de nouveau dessus pour trier par ordre décroissant.

   De même, les champs suivants sont affichés dans un résultat de recherche de tâche :

   * **ID** de la tâche : ID de la tâche. Le champ est lié par un hyperlien. Si vous cliquez sur un ID de tâche dans ce champ, vous êtes redirigé vers le panneau Détails **[!UICONTROL de la]** tâche correspondant à la tâche.
   * **Initiateur**: Utilisateur AEM Forms qui a démarré l’instance de processus
   * **Heure** de création : Date et heure de démarrage de l’instance de processus
   * **Heure** terminée : Date et heure de fin de l’instance de processus
   * **Durée**: Durée du début à la fin de l’instance de processus
   * **État**: Statut actuel de l’instance de processus.
   Par défaut, le résultat est trié par ID de tâche. Toutefois, pour trier le résultat selon l’un des champs, cliquez sur le titre du champ. Le résultat est trié selon la colonne indiquée par une flèche foncée en regard de l’en-tête de colonne.

   Puisque le tri est une opération de basculement, cliquez sur un en-tête de champ pour trier le résultat par ordre croissant et cliquez de nouveau dessus pour trier par ordre décroissant. L’ordre de tri actuel (croissant/décroissant) est indiqué par la direction de la flèche foncée en regard de l’en-tête de colonne.

   ![task_search_result](assets/task_search_result.png)

1. Cliquez sur le bouton de rail ![lc_pr_rail_button](assets/lc_pr_rail_button.png) dans l’angle supérieur gauche pour réduire le volet **Mes filtres** et étendre l’espace disponible pour le panneau **Rapport** .
1. Utilisez les options dans le coin supérieur droit du panneau **Rapport **pour effectuer des opérations sur le résultat de la requête.

   * **Actualiser**: Actualise le rapport avec les dernières données stockées

   * **Exporter au format CSV**: Exportez les données du rapport dans un fichier séparé par des virgules.
   >[!NOTE]
   >
   >Lorsque vous exportez un rapport, le résultat entier de la recherche est exporté dans un fichier CSV et pas seulement dans la page active.

## Détails du processus/tâche {#process-task-details}

Utilisez le panneau Détails **du** processus pour afficher les détails d’un processus spécifique.

De même, vous utilisez le panneau Détails **de la** tâche pour afficher les détails d’une tâche spécifique.

### Pour afficher les détails du processus/de la tâche {#to-view-process-task-details}

Vous pouvez afficher les détails d’un processus/d’une tâche AEM Forms spécifique :

* **A partir d’un résultat de recherche de processus/tâche**
* **En saisissant l’ID de processus/tâche dans le panneau Détails du processus/de la tâche**

#### A partir d’un résultat de recherche de processus/tâche {#from-a-process-task-search-result}

1. Exécutez une recherche de processus/tâche. Pour plus d’informations, voir [Exécution d’une requête](#to-execute-a-search-query)de recherche de processus.

   Les identifiants de processus affichés dans le résultat sont liés.

   ![process_id_list](assets/process_id_list.png)

1. Cliquez sur un ID de processus dans la liste pour afficher les détails de ce processus dans le panneau Détails **du** processus.

   Le résultat de la requête Détails **du** processus/de la tâche affiche les détails des tâches/formulaires contenus dans le processus/la tâche.

   Par défaut, le résultat est trié par Tâche/ID de formulaire. Toutefois, pour trier le résultat selon l’un des champs, cliquez sur le titre du champ. La colonne dans laquelle le résultat est trié est indiquée par une flèche foncée en regard de l’en-tête de colonne.

   Puisque le tri est une opération de basculement, cliquez sur un en-tête de champ pour trier le résultat par ordre croissant et cliquez de nouveau dessus pour trier par ordre décroissant. L’ordre de tri actuel (croissant/décroissant) est indiqué par la direction de la flèche foncée en regard de l’en-tête de colonne.

   **Résultat des détails du processus**

   ![process_details](assets/process_details.png)

   **** Panneau de gauche : Affiche les détails suivants du processus sélectionné :

   * Nom du processus
   * Date de création du processus
   * Date d&#39;achèvement du processus
   * Durée du processus
   * Statut du processus
   * Initiateur du processus
   **** Panneau supérieur droit : Affiche les détails suivants des tâches qui composent le processus sélectionné :

   * ID de tâche
   * Nom de la tâche
   * Propriétaire de la tâche
   * Date de création de la tâche
   * Heure de mise à jour de la tâche
   * Date d&#39;achèvement de la tâche
   * Durée de la tâche
   * Statut de la tâche
   **** Panneau inférieur droit : Affiche les détails suivants de l’historique des processus sélectionnés :

   * Nom du processus
   * Initiateur du processus
   * Heure de mise à jour du processus
   * Date d&#39;achèvement du processus
   * Statut du processus
   **Résultat des détails de la tâche**

   ![task_details](assets/task_details.png)

   **** Panneau de gauche : Affiche les détails suivants de la tâche sélectionnée :

   * Nom de la tâche
   * ID du processus auquel appartient cette tâche
   * Description de la tâche
   * Date de création de la tâche
   * Date d&#39;achèvement de la tâche
   * Durée de la tâche
   * Statut de la tâche
   * Chemin sélectionné de la tâche
   **** Panneau supérieur droit : Affiche les détails suivants des formulaires qui composent la tâche sélectionnée :

   * ID de formulaire
   * Date de création du formulaire
   * Date de mise à jour du formulaire
   * URL du modèle de formulaire
   **** Panneau inférieur droit : Affiche les détails suivants de l’historique des processus de la tâche sélectionnée :

   * Type d&#39;affectation de tâche
   * Propriétaire de la tâche
   * Date de création de l&#39;affectation de tâche
   * Heure de mise à jour de la tâche






1. Cliquez sur **Retour à la recherche** de processus/tâche pour revenir au résultat de recherche à partir duquel les détails du processus/de la tâche ont été analysés.

   ![back_to_search](assets/back_to_search.png)

   Cependant, si les détails du processus/de la tâche ont été trouvés en saisissant un ID de processus/de tâche spécifique, le fait de cliquer sur Retour au processus/Recherche de tâche vous ramène à la recherche **de** processus/de tâche, sans afficher de résultat de recherche.

#### En saisissant l’ID de processus/tâche dans le panneau Détails du processus/de la tâche {#by-entering-the-process-task-id-in-the-process-task-details-panel-br}

1. Accédez au panneau Détails **du** processus/tâche.

   ![details_nodes](assets/details_nodes.png)

1. Dans la zone de texte ID processus/tâche, saisissez l’ID processus/tâche.

   ![process_details-1](assets/process_details-1.png)

   Les champs du résultat de la requête **Processus/Détails** de la tâche sont des champs spécifiques à un processus/tâche AEM Forms.

   Pour un processus, le résultat de la requête affiche les détails des tâches contenues dans le processus.

   Pour une tâche, le résultat de la requête affiche les détails des formulaires contenus dans la tâche.

[Contacter le support technique](https://www.adobe.com/account/sign-in.supportportal.html)
