---
title: ' ad hoc dans le de processus '
seo-title: ' ad hoc dans le de processus '
description: Création d’un personnalisé pour rechercher des détails sur le processus AEM Forms sur JEE et les  de dans le  de processus
seo-description: Création d’un personnalisé pour rechercher des détails sur le processus AEM Forms sur JEE et les  de dans le  de processus
uuid: db0c5c28-b213-4582-a6ed-df127e570a4e
content-type: reference
topic-tags: process-reporting
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: b0a544e2-2ce4-48e2-a721-82f481d36004
docset: aem65
translation-type: tm+mt
source-git-commit: 56c6cfd437ef185336e81373bd5f758205b96317

---


#  ad hoc dans le de processus{#ad-hoc-queries-in-process-reporting}

##  ad hoc dans le de processus {#ad-hoc-queries-in-process-reporting-1}

Les  ad hoc dans le de processus vous permettent de créer des  personnalisées que vous pouvez utiliser pour rechercher des détails de processus et de des instances de processus AEM Forms définies dans votre deformulaires AEM.

En outre, les  de ad hoc peuvent être définies à l’aide de l’ de propriétés de processus et de. Ces  peuvent ensuite être enregistrées et utilisées pour exécuter les rapports ultérieurement.

[**Recherche **](/help/forms/using/process-reporting/adhoc-queries-in-process-reporting.md#p-process-task-search-p)de processus : Recherchez des instances de processus avec un filtre de recherche défini par l’utilisateur en fonction des attributs de processus.

[**Détails **](/help/forms/using/process-reporting/adhoc-queries-in-process-reporting.md#p-process-task-details-p)du processus :  les détails d’une instance de processus en spécifiant l’ID de processus.

**Recherche** : Recherchez des instances de  avec un filtre de recherche défini par l’utilisateur en fonction d’attributs .

**Détails** des  du :  les détails d’une instance de  en spécifiant l’ID de l’ de l’.

### Processus et {#processes-and-tasks}

Les étapes que vous suivez pour créer des  et exécuter des  de pour les détails du processus sont identiques à celles que vous suivez pour les  deprocessus.

Cela signifie que les interfaces utilisateur pour la recherche de processus et la recherche de ne diffèrent que dans les champs par lesquels vous pouvez effectuer une recherche et dans les champs renvoyés dans les résultats de la recherche. Cela s’explique simplement par le fait que, bien que de nombreux champs soient identiques, certains champs sont spécifiques aux processus et certains champs sont spécifiques aux  de.

Cet article détaille les descriptions des sections Processus/ Recherche et processus/Détails . Aux emplacements appropriés, toute différence spécifique sera spécifiquement appelée.

## Recherche de processus/ {#process-task-search}

Utilisez Process/Search pour définir des  de pour interroger les instances de processus/de.

### Pour créer un de recherche de processus/ {#to-create-a-process-task-search-query}

1. Pour  l&#39; de recherche de processus/enregistrée ou pour créer un **, cliquez sur** Adhoc de **** puis sur Recherchede processus/deprocessus/dedemande.

   ![search_nodes](assets/search_nodes.png)

   Le panneau **Mon** s’affiche à droite de la  de l’arborescence.

   Dans le panneau **Mes** , vous pouvez créer un nouveau  ad hoc et cliquer pour exécuter les  précédemment enregistrées.

   ![my___panel](assets/my_filters_panel.png)

1. Pour exécuter un  existant, il vous suffit de cliquer sur le  du dans le panneau **Mon** .
1. Pour créer un , cliquez sur **Ajouter** (+).

   Le panneau **Créer un filtre** s’affiche.

   ![create_filter_panel](assets/create_filter_panel.png)

   Un  est constitué d’un ou de plusieurs  de. Pour créer un filtre, ajoutez une rangée de filtre au  du. Par défaut, une ligne de filtre est ajoutée au  du.

   **Pour définir un filtre**

   1. Sélectionnez un champ.

      ![filter_field](assets/filter_field.png)

      >[!NOTE]
      >
      >Le de champs contient les champs spécifiques au processus/AEM Forms.

   1. Sélectionnez une condition.

      ![filter_condition](assets/filter_condition.png)

      >[!NOTE]
      >
      >Les conditions répertoriées dépendent de l’attribut sélectionné pour le filtrage.

   1. Entrez une valeur.

      ![filter_value](assets/filter_value.png)

   1. Pour ajouter un autre filtre au , cliquez sur **Ajouter (+)** à droite de la ligne de filtre.

      Pour supprimer un filtre du , cliquez sur **Supprimer (-)** à droite de la ligne de filtre.

      ![filter_add_del](assets/filter_add_del.png)

Après avoir créé un  de, utilisez les options dans le coin supérieur droit du panneau **Créer un filtre** pour :

* **Annuler**: Annulez les modifications et revenez au panneau **Mon** .
* **Exécuter**: Exécutez le  actuel pour voir et / ou vérifier les résultats. Dans ce cas, vous n’avez pas besoin d’enregistrer le  avant d’exécuter le  du. Vous pouvez vérifier les résultats, effectuer des modifications si nécessaire, puis enregistrer le  du lorsque vous êtes satisfait de la sortie.
* **Enregistrer**: Enregistrez le filtre. Le filtre peut ensuite être affiché et exécuté à partir du panneau **Mon** .

### Options du panneau Mon {#options-in-my-filters-panel}

Utilisez les options du panneau **Mon** pour **Ajouter** lc_pr_add_filter ![,](assets/lc_pr_add_filter.png)**Modifierlc_pr_delete_filterouSupprimerlc_pr_edit_filtrer un ad hoc.**![](assets/lc_pr_delete_filter.png)****![](assets/lc_pr_edit_filter.png)

![my___options](assets/my_filters_options.png)

### Pour exécuter un  de recherche {#to-execute-a-search-query}

1. Pour exécuter un , cliquez sur le filtre dans le panneau **Mon** ou cliquez sur le bouton **Exécuter** si vous créez ou modifiez un filtre.
1. Les résultats de la  s’affichent dans le panneau **Rapport** de la fenêtre de **de** processus.

   ![process_search_result](assets/process_search_result.png)

   Vous pouvez paginer les résultats de la recherche à l’aide du panneau de pagination affiché au bas du rapport.

   ![process_result_pgn](assets/process_result_pgn.png)

   Dans le  déroulant **Afficher** , choisissez le nombre de résultats à afficher par page.

   Dans la zone de texte **Page** , saisissez un numéro de page pour accéder directement à cette page.

1. Les champs suivants sont affichés dans un résultat de recherche de processus :

   * **ID** du processus : ID du processus. Le champ est lié par un hyperlien. Si vous cliquez sur un ID de processus dans ce champ, vous êtes redirigé vers le panneau Détails **[!UICONTROL du]** processus pour le processus.
   * **Initiateur**: Utilisateur AEM Forms qui a démarré l’instance de processus
   * **Heure** de création : Date et heure de démarrage de l’instance de processus
   * **Heure** terminée : Date et heure auxquelles l’instance de processus s’est terminée
   * **Durée**: Durée du  à la fin de l’instance de processus
   * **État**: Statut actuel de l’instance de processus.
   Par défaut, le résultat est trié par ID de processus. Toutefois, pour trier le résultat selon l’un des champs, cliquez sur le titre du champ.

   Puisque le tri est une opération de basculement, cliquez sur un en-tête de colonne pour trier le résultat par ordre croissant et cliquez de nouveau dessus pour trier par ordre décroissant.

   De même, les champs suivants s’affichent dans un résultat de recherche  :

   * **ID** : ID du . Le champ est lié par un hyperlien. Si vous cliquez sur un ID de  dans ce champ, vous êtes redirigé vers le panneau Détails **[!UICONTROL de l’]** pour l’.
   * **Initiateur**: Utilisateur AEM Forms qui a démarré l’instance de processus
   * **Heure** de création : Date et heure de démarrage de l’instance de processus
   * **Heure** terminée : Date et heure auxquelles l’instance de processus s’est terminée
   * **Durée**: Durée du  à la fin de l’instance de processus
   * **État**: Statut actuel de l’instance de processus.
   Par défaut, le résultat est trié par ID de  du. Toutefois, pour trier le résultat selon l’un des champs, cliquez sur le titre du champ. Le résultat est trié selon la colonne indiquée par une flèche foncée en regard de l’en-tête de colonne.

   Puisque le tri est une opération de basculement, cliquez sur un en-tête de champ pour trier le résultat par ordre croissant et cliquez de nouveau dessus pour trier par ordre décroissant. L’ordre de tri actuel (croissant/décroissant) est indiqué par la direction d’une flèche foncée en regard de l’en-tête de colonne.

   ![_search_result](assets/task_search_result.png)

1. Cliquez sur le bouton de rail ![lc_pr_rail_button](assets/lc_pr_rail_button.png) dans l’angle supérieur gauche pour réduire le volet **Mon****et étendre l’espace disponible pour le panneau** Rapport.
1. Utilisez les options dans le coin supérieur droit du panneau **Rapport **pour effectuer des opérations sur le résultat  du.

   * **Actualiser**: Actualise le rapport avec les données les plus récentes dans le  

   * **Exporter au format CSV**: Exportez les données du rapport dans un fichier séparé par des virgules.
   >[!NOTE]
   >
   >Lorsque vous exportez un rapport, le résultat entier de la recherche est exporté dans un fichier CSV et pas seulement dans la page active.

## Détails du processus/ de {#process-task-details}

Le panneau Détails **du** processus vous permet de  les détails d’un processus spécifique.

De la même manière, vous utilisez le panneau Détails **du** pour  les détails d’un  spécifique.

### Pour  les détails du processus/du {#to-view-process-task-details}

Vous pouvez  les détails d’un processus/d’un AEM Forms spécifique  :

* **A partir d’un résultat de recherche Processus/**
* **En saisissant l’ID de processus/de dans le panneau Détails du processus/du**

#### A partir d’un résultat de recherche Processus/ {#from-a-process-task-search-result}

1. Exécutez une recherche de processus/de. Pour plus d’informations, voir [Exécution d’un](#to-execute-a-search-query)de recherche de processus.

   Les identifiants de processus affichés dans le résultat sont liés.

   ![process_id_](assets/process_id_list.png)

1. Cliquez sur un ID de processus dans le  pour  les détails de ce processus dans le panneau Détails **du** processus.

   Le résultat du  Détails **du** processus/du affiche les détails des /formulaires contenus dans le processus/le.

   Par défaut, le résultat est trié par/ID de formulaire. Toutefois, pour trier le résultat selon l’un des champs, cliquez sur le titre du champ. La colonne dans laquelle le résultat est trié est indiquée par une flèche foncée en regard de l’en-tête de colonne.

   Puisque le tri est une opération de basculement, cliquez sur un en-tête de champ pour trier le résultat par ordre croissant et cliquez de nouveau dessus pour trier par ordre décroissant. L’ordre de tri actuel (croissant/décroissant) est indiqué par la direction d’une flèche foncée en regard de l’en-tête de colonne.

   **Résultat des détails du processus**

   ![process_details](assets/process_details.png)

   **Panneau de gauche :** Affiche les détails suivants du processus sélectionné :

   * Nom du processus
   * Date de création du processus
   * Date d&#39;achèvement du processus
   * Durée du processus
   * Statut du processus
   * Initiateur du processus
   **Panneau supérieur droit :** Affiche les détails suivants du  de qui constitue le processus sélectionné :

   * ID 
   * Nom 
   * Propriétaire 
   * Date de création du 
   *  date de mise à jour
   * Heure de fin de  du
   * Durée 
   * Statut 
   **Panneau inférieur droit :** Affiche les détails suivants de l’historique des processus sélectionnés :

   * Nom du processus
   * Initiateur du processus
   * Heure de mise à jour du processus
   * Date d&#39;achèvement du processus
   * Statut du processus
   **Résultat  Détails du**

   ![task_details](assets/task_details.png)

   **Panneau de gauche :** Affiche les détails suivants du  sélectionné :

   * Nom de la tâche
   * ID du processus auquel appartient ce 
   * Description du 
   * Date de création du 
   * Heure de fin de  du
   * Durée 
   * Statut 
   * Chemin d&#39;accès sélectionné 
   **Panneau supérieur droit :** Affiche les détails suivants des formulaires qui composent le  sélectionné :

   * ID de formulaire
   * Date de création du formulaire
   * Date de mise à jour du formulaire
   * URL du modèle de formulaire
   **Panneau inférieur droit :** Affiche les détails suivants de l’historique des processus du  sélectionné :

   * Type d’affectation 
   * Propriétaire 
   * Date de création de l’affectation 
   *  date de mise à jour






1. Cliquez sur **Retour au processus/ Recherche** pour revenir au résultat de la recherche à partir duquel les détails du processus/du ont été analysés.

   ![back_to_search](assets/back_to_search.png)

   Toutefois, si les détails du processus/du  ont été trouvés en saisissant un ID de processus/de spécifique, le fait de cliquer sur Retour au processus/ **Recherche de** processus/devous ramène à la recherchede processus/de, sans afficher de résultat de recherche.

#### En saisissant l’ID de processus/de dans le panneau Détails du processus/du {#by-entering-the-process-task-id-in-the-process-task-details-panel-br}

1. Accédez au panneau Détails **du** processus/du .

   ![details_nodes](assets/details_nodes.png)

1. Dans la zone de texte ID de processus/d’, saisissez l’ ID de processus/d’.

   ![process_details-1](assets/process_details-1.png)

   Les champs du résultat du  Détails **du** processus/du sont des champs spécifiques à un processus/un  AEM Forms.

   Dans le cas d’un processus, le résultat  affiche les détails du  contenu dans le processus.

   Dans le cas d’un , le résultat  du affiche les détails des formulaires contenus dans le .
