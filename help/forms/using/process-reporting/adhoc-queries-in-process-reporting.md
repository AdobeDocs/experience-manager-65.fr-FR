---
title: Requêtes ad hoc dans Process Reporting
description: Créez des requêtes personnalisées pour rechercher les détails des processus et des tâches AEM Forms on JEE dans Process Reporting
content-type: reference
topic-tags: process-reporting
products: SG_EXPERIENCEMANAGER/6.5/FORMS
docset: aem65
exl-id: a096eea0-b2fb-4d86-b729-ca47611135b2
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: 539da06db98395ae6eaee8103a3e4b31204abbb8
workflow-type: ht
source-wordcount: '1635'
ht-degree: 100%

---

# Requêtes ad hoc dans Process Reporting{#ad-hoc-queries-in-process-reporting}

## Requêtes ad hoc dans Process Reporting {#ad-hoc-queries-in-process-reporting-1}

Grâce aux requêtes ad hoc dans Process Reporting, vous pouvez créer des requêtes personnalisées que vous pouvez utiliser pour rechercher les détails des processus et des tâches des instances de processus AEM Forms définies dans votre environnement AEM Forms.

En outre, les requêtes ad hoc peuvent être définies à l’aide de filtres de propriétés de processus et de tâches. Ces filtres peuvent ensuite être enregistrés et utilisés pour exécuter les rapports ultérieurement.

[**Recherche de processus**](/help/forms/using/process-reporting/adhoc-queries-in-process-reporting.md#p-process-task-search-p) : recherchez des instances de processus avec un filtre de recherche défini par l’utilisateur en fonction des attributs de processus.

[**Détails du processus**](/help/forms/using/process-reporting/adhoc-queries-in-process-reporting.md#p-process-task-details-p) : affichez les détails d’une instance de processus en spécifiant l’identifiant de processus.

**Recherche de tâches** : recherchez des instances de tâche avec un filtre de recherche défini par l’utilisateur en fonction des attributs de tâche.

**Détails de la tâche** : affichez les détails d’une instance de tâche en spécifiant son identifiant.

### Processus et tâches {#processes-and-tasks}

Les étapes que vous suivez pour créer des filtres et exécuter des requêtes pour les détails de processus sont les mêmes que pour les tâches.

Par conséquent, les interfaces utilisateur de la recherche de processus et de la recherche de tâches ne diffèrent qu’au niveau des champs que vous pouvez rechercher et des champs renvoyés dans les résultats de recherche. Cela est simplement dû au fait que, alors que de nombreux champs sont identiques, certains sont spécifiques aux processus et d’autres sont spécifiques aux tâches.

Cet article détaille les descriptions des sections de recherche de processus/tâches et de détails de processus/tâches. Toutes les différences spécifiques sont indiquées de manière spécifique aux emplacements appropriés.

## Recherche de processus/tâches {#process-task-search}

Vous utilisez la recherche de processus/tâches pour définir des filtres pour interroger des instances de processus/tâche.

### Pour créer une demande de recherche de processus/tâches {#to-create-a-process-task-search-query}

1. Pour afficher les demandes de recherche de processus/tâches enregistrées ou créer une demande, cliquez sur **Requêtes ad hoc**, puis cliquez sur **Recherche de processus/tâches**.

   ![nœuds_recherche](assets/search_nodes.png)

   Le panneau **Mes filtres** s’affiche à droite de l’arborescence.

   Dans le panneau **Mes filtres**, vous pouvez créer des requêtes ad hoc et cliquer pour exécuter des requêtes précédemment enregistrées.

   ![panneau_mes_filtres](assets/my_filters_panel.png)

1. Pour exécuter une requête existante, il vous suffit de cliquer dessus dans le panneau **Mes filtres**.
1. Pour créer une requête, cliquez sur **Ajouter** (+).

   Le panneau **Créer un filtre** s’affiche.

   ![panneau_créer_filtre](assets/create_filter_panel.png)

   Une requête se compose d’un ou de plusieurs filtres de requête. Pour créer un filtre, ajoutez une ligne de filtre à la requête. Par défaut, une ligne de filtre est ajoutée à la requête.

   **Pour définir un filtre**

   1. Sélectionnez un champ.

      ![champ_filtre](assets/filter_field.png)

      >[!NOTE]
      >
      >La liste des champs contient les champs spécifiques au processus ou à la tâche AEM Forms.

   1. Sélectionnez une condition.

      ![condition_filtre](assets/filter_condition.png)

      >[!NOTE]
      >
      >Les conditions répertoriées dépendent de l’attribut sélectionné pour le filtrage.

   1. Saisissez une valeur.

      ![valeur_filtre](assets/filter_value.png)

   1. Pour ajouter un autre filtre à la requête, cliquez sur **Ajouter (+)** à droite de la ligne de filtre.

      Pour supprimer un filtre de la requête, cliquez sur **Supprimer (-)** à droite de la ligne de filtre.

      ![ajout_suppression_filtre](assets/filter_add_del.png)

Après avoir créé une requête, utilisez les options situées dans le coin supérieur droit du panneau **Créer un filtre** :

* **Annuler** : annulez les modifications et revenez au panneau **Mes filtres**.
* **Exécuter** : exécutez la requête actuelle pour afficher et/ou vérifier les résultats. Dans ce cas, il n’est pas nécessaire d’enregistrer la requête avant de l’exécuter. Vous pouvez vérifier les résultats, apporter des modifications si nécessaire, puis enregistrer la requête lorsque les résultats vous conviennent.
* **Enregistrer** : enregistrez le filtre. Vous pouvez ensuite afficher et exécuter le filtre à partir du panneau **Mes filtres**.

### Options dans le panneau Mes filtres {#options-in-my-filters-panel}

Utilisez les options du panneau **Mes filtres** pour **Ajouter** ![lc_pr_add_filter](assets/lc_pr_add_filter.png), **Modifier** ![lc_pr_delete_filter](assets/lc_pr_delete_filter.png) ou **Supprimer** ![lc_pr_edit_filter](assets/lc_pr_edit_filter.png) une demande ad hoc.

![my_filters_options](assets/my_filters_options.png)

### Exécuter une requête {#to-execute-a-search-query}

1. Pour exécuter une requête, cliquez sur le filtre dans le panneau **Mes filtres** ou cliquez sur le bouton **Exécuter** si vous créez ou modifiez un filtre.
1. Les résultats de la demande s’affichent dans le panneau **Rapport** de la fenêtre **Process Reporting**.

   ![process_search_result](assets/process_search_result.png)

   Vous pouvez paginer les résultats de la recherche à l’aide du panneau de pagination affiché au bas du rapport.

   ![process_result_pgn](assets/process_result_pgn.png)

   Dans la liste déroulante **Affichage**, choisissez le nombre de résultats à afficher par page.

   Dans la zone de texte **Page**, saisissez un numéro de page pour y accéder directement.

1. Les champs suivants s’affichent dans un résultat de recherche de processus :

   * **Identifiant de processus** : l’identifiant du processus. Le champ contient un lien hypertexte. Si vous cliquez sur un identifiant de processus dans ce champ, vous êtes redirigé vers le panneau **[!UICONTROL Détails du processus]**.
   * **Initiateur** : l’utilisateur AEM Forms qui a démarré l’instance de processus
   * **Heure de création** : date et heure de démarrage de l’instance de processus
   * **Heure de terminaison** : date et heure auxquelles l’instance de processus s’est terminée
   * **Durée** : durée du début jusqu’à la réalisation de l’instance de processus.
   * **Statut** : statut actuel de l’instance de processus.

   Par défaut, le résultat est trié par identifiant de processus. Toutefois, pour trier le résultat en fonction de l’un des champs, cliquez sur le titre du champ.

   Comme le tri est une opération de basculement, cliquez sur un en-tête de colonne pour trier le résultat par ordre croissant et cliquez de nouveau dessus pour le trier par ordre décroissant.

   De même, les champs suivants s’affichent dans un résultat de recherche de tâche :

   * **Identifiant de tâche** : l’identifiant de la tâche. Le champ contient un lien hypertexte. Si vous cliquez sur un identifiant de tâche dans ce champ, vous êtes redirigé vers le panneau **[!UICONTROL Détails de la tâche]**.
   * **Initiateur** : l’utilisateur AEM Forms qui a démarré l’instance de processus
   * **Heure de création** : date et heure de démarrage de l’instance de processus
   * **Heure de terminaison** : date et heure auxquelles l’instance de processus s’est terminée
   * **Durée** : durée du début jusqu’à la réalisation de l’instance de processus.
   * **Statut** : statut actuel de l’instance de processus.

   Par défaut, le résultat est trié par identifiant de tâche. Toutefois, pour trier le résultat en fonction de l’un des champs, cliquez sur son titre. Le résultat est trié selon la colonne indiquée par une flèche sombre à côté de l’en-tête de colonne.

   Comme le tri est une opération de basculement, cliquez sur un en-tête de champ pour trier le résultat par ordre croissant et cliquez de nouveau dessus pour le trier par ordre décroissant. L’ordre de tri actuel (croissant/décroissant) est indiqué par la direction d’une flèche sombre à côté de l’en-tête de colonne.

   ![task_search_result](assets/task_search_result.png)

1. Cliquez sur le bouton de rail ![lc_pr_rail_button](assets/lc_pr_rail_button.png) dans le coin supérieur gauche pour réduire le panneau **Mes filtres** et agrandir l’espace disponible pour le panneau **Rapport**.
1. Utilisez les options situées dans le coin supérieur droit du panneau « Rapport » pour effectuer des opérations sur le résultat de la demande.

   * **Actualiser** : actualise le rapport avec les dernières données stockées

   * **Exportation au format CSV** : exportez les données du rapport dans un fichier séparé par des virgules.

   >[!NOTE]
   >
   >Lorsque vous exportez un rapport, l’ensemble du résultat de la recherche est exporté dans un fichier CSV et pas seulement dans la page active.

## Détails du processus/de la tâche {#process-task-details}

Vous utilisez le panneau **Détails du processus** pour afficher les détails d’un processus spécifique.

De même, vous utilisez le panneau **Détails de la tâche** pour afficher les détails d’une tâche spécifique.

### Pour afficher les détails d’un processus/d’une tâche {#to-view-process-task-details}

Vous pouvez afficher les détails d’un processus/d’une tâche AEM Forms spécifique :

* **À partir du résultat de recherche de processus/tâche**
* **En saisissant l’ID du processus/de la tâche dans le panneau Détails du processus / de la tâche**

#### À partir des résultats de la recherche d’un processus / d’une tâche {#from-a-process-task-search-result}

1. Exécutez une recherche de processus/tâche. Pour plus d’informations, consultez la section [Pour exécuter une requête de processus](#to-execute-a-search-query).

   Notez que les ID de processus affichés dans les résultats de la recherche sont liés.

   ![process_id_list](assets/process_id_list.png)

1. Cliquez sur un ID de processus dans la liste pour afficher les détails de ce processus dans le panneau **Détails du processus**.

   Les résultats de la recherche des **Détails du processus / de la tâche** affiche les détails des tâches/formulaires contenus dans le processus / la tâche.

   Par défaut, le résultat est trié par ID de tâche/formulaire. Toutefois, pour trier le résultat en fonction de l’un des champs, cliquez sur son titre. La colonne selon laquelle les résultats sont triés est indiquée par une flèche foncée en regard de l’en-tête de colonne.

   Comme le tri est une opération de basculement, cliquez sur un en-tête de champ pour trier le résultat par ordre croissant et cliquez de nouveau dessus pour le trier par ordre décroissant. L’ordre de tri actuel (croissant/décroissant) est indiqué par la direction d’une flèche sombre à côté de l’en-tête de colonne.

   **Résultats des Détails du processus**

   ![process_details](assets/process_details.png)

   **Volet de gauche :** affiche les détails suivants du processus sélectionné :

   * Nom du processus
   * Date et heure de création du processus
   * Date et heure de fin du processus
   * Durée du processus
   * État du processus
   * Initiateur du processus

   **Volet supérieur droit :** affiche les détails suivants des tâches qui composent le processus sélectionné :

   * ID de la tâche
   * Nom de la tâche
   * Propriétaire de la tâche
   * Date et heure de création de la tâche
   * Date et heure de mise à jour de la tâche
   * Date et heure de fin de la tâche
   * Durée de la tâche
   * État de la tâche

   **Volet inférieur droit :** affiche les détails suivants de l’historique du processus sélectionné :

   * Nom du processus
   * Initiateur du processus
   * Date et heure de mise à jour du processus
   * Date et heure de fin du processus
   * État du processus

   **Résultats des détails de la tâche**

   ![task_details](assets/task_details.png)

   **Volet de gauche :** affiche les détails suivants de la tâche sélectionnée :

   * Nom de la tâche
   * ID du processus auquel cette tâche appartient
   * Description de la tâche
   * Date et heure de création de la tâche
   * Date et heure de fin de la tâche
   * Durée de la tâche
   * État de la tâche
   * Itinéraire sélectionné de la tâche

   **Volet supérieur droit :** affiche les détails suivants des formulaires qui composent la tâche sélectionnée :

   * ID de formulaire
   * Date de création du formulaire
   * Date de mise à jour du formulaire
   * URL du modèle de formulaire

   **Panneau inférieur droit :** il affiche les détails suivants de l’historique des processus de la tâche sélectionnée :

   * Type d’affectation de tâche
   * Propriétaire de la tâche
   * Date de création de l’affectation de tâche
   * Date et heure de mise à jour de la tâche

1. Cliquez sur **Retour à la recherche du processus / de la tâche** pour revenir au résultat de recherche à partir duquel les détails du processus/de la tâche ont été tirés.

   ![back_to_search](assets/back_to_search.png)

   Cependant, si les détails du processus/de la tâche ont été trouvés en saisissant un ID de processus/de tâche spécifique, le fait de cliquer sur Retour à la recherche du processus/de la tâche vous ramène à **Recherche du processus/de la tâche**, sans afficher de résultat de recherche.

#### En saisissant l’ID de processus/tâche dans le panneau Détails du processus/de la tâche {#by-entering-the-process-task-id-in-the-process-task-details-panel-br}

1. Accédez au panneau **Détails du processus/de la tâche**.

   ![details_nodes](assets/details_nodes.png)

1. Dans la zone de texte ID du processus/de la tâche, saisissez l’ID du processus/de la tâche.

   ![process_details-1](assets/process_details-1.png)

   Les champs de résultats de la requête **Détails du processus/de la tâche** sont des champs spécifiques à un processus/une tâche AEM Forms.

   Pour un processus, le résultat de la requête affiche les détails des tâches contenues dans le processus.

   Pour une tâche, le résultat de la requête affiche les détails des formulaires contenus dans la tâche.
