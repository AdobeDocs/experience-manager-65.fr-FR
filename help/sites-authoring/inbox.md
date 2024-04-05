---
title: Votre boîte de réception pour gérer les tâches
description: Gestion de vos tâches avec la boîte de réception dans Adobe Experience Manager 6.5
exl-id: 80b7f179-b011-4f90-b5ab-9ef8a669d271
solution: Experience Manager, Experience Manager Sites
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '1155'
ht-degree: 100%

---

# Votre boîte de réception{#your-inbox}

Vous pouvez recevoir des notifications de diverses sections d’AEM, y compris des workflows et des projets, par exemple sur des :

* Tâches :

   * Elles peuvent également être créées à différents endroits de l’interface utilisateur d’AEM (par exemple, sous **Projets**).
   * Elles peuvent être le produit de l’étape **Créer une tâche** ou **Créer une tâche de projet** d’un workflow.

* Workflows :

   * Éléments de travail correspondant à des actions que vous devez effectuer sur le contenu de la page.

      * Ils sont le produit des étapes **Participant** du workflow.

   * Éléments d’échec, pour permettre aux administrateurs et administratrices d’effectuer à nouveau l’étape qui a échoué.

Vous recevez ces notifications dans votre propre boîte de réception où vous pouvez les afficher et prendre des mesures.

>[!NOTE]
>
>Prêt à l’emploi, AEM est préchargé avec des tâches administratives affectées au groupe d’administrateurs et administratrices. Voir [Tâches administratives prêtes à l’emploi](#out-of-the-box-administrative-tasks) pour plus d’informations.

>[!NOTE]
>
>Pour plus d’informations sur les types d’éléments, voir aussi :
>
>* [Projets](/help/sites-authoring/touch-ui-managing-projects.md)
>* [Projets – Utilisation des Tâches](/help/sites-authoring/task-content.md)
>* [Workflows](/help/sites-authoring/workflows.md)
>* [Formulaires](/help/forms/using/introduction-aem-forms.md)
>

## Boîte de réception dans l’en-tête {#inbox-in-the-header}

Dans les deux consoles, le nombre actuel d’éléments présents dans votre boîte de réception est indiqué dans l’en-tête. L’indicateur peut également être ouvert pour permettre un accès rapide aux pages nécessitant des actions ou un accès à la boîte de réception :

![wf-80](assets/wf-80.png)

>[!NOTE]
>
>Certaines opérations sont également répertoriées dans le [mode Carte de la ressource appropriée](/help/sites-authoring/basic-handling.md#card-view).

## Tâches administratives prêtes à l’emploi  {#out-of-the-box-administrative-tasks}

Prêt à l’emploi, AEM est préchargé avec quatre tâches affectées au groupe d’administrateurs et administratrices.

* [Configurer Analytics et Targeting](/help/sites-administering/opt-in.md)
* [Appliquer la liste de contrôle de sécurité AEM](/help/sites-administering/security-checklist.md)
* Autoriser la collecte de statistiques d’utilisation agrégées
* [Configurer le HTTPS](/help/sites-administering/ssl-by-default.md)

## Ouverture de la boîte de réception {#opening-the-inbox}

Pour ouvrir la boîte de réception des notifications AEM :

1. Cliquez sur l’indicateur dans la barre d’outils.

1. Sélectionnez **Afficher tout**. La **boîte de réception AEM** s’ouvre. La boîte de réception affiche les éléments des workflows, des projets et des tâches.
1. La vue par défaut est [Liste](#inbox-list-view), mais vous pouvez également passer à la vue [Calendrier](#inbox-calendar-view). Pour ce faire, utilisez le sélecteur de vue (barre d’outils, en haut à droite).

   Vous pouvez également définir les [paramètres d’affichage](#inbox-view-settings) pour ces deux vues. Les options disponibles dépendent de l’affichage actuel.

   ![wf-79](assets/inbox-list-view.png)

>[!NOTE]
>
>La boîte de réception fonctionne comme une console. Vous pouvez ainsi utiliser la [navigation globale](/help/sites-authoring/basic-handling.md#global-navigation) ou la fonction de [recherche](/help/sites-authoring/search.md) pour accéder à un autre emplacement lorsque vous avez terminé.

### Boîte de réception – Vue Liste {#inbox-list-view}

Cette vue affiche tous les éléments, ainsi que des informations importantes :

![wf-82](assets/wf-82.png)

### Boîte de réception – Mode Calendrier {#inbox-calendar-view}

Cette vue présente les éléments en fonction de leur position dans le calendrier et de la vue précise que vous avez sélectionnée :

![wf-93](assets/wf-93.png)

Vous pouvez :

* sélectionner une vue spécifique (**Chronologie**, **Colonne**, **Liste**) ;

* spécifier les tâches à afficher selon **Planning** : **Tous**, **Prévus**, **En cours**, **Échéance proche** et **Échéance dépassée** ;

* analyser en profondeur pour obtenir plus d’informations sur un élément ;
* sélectionner une période sur laquelle cibler la vue :

![wf-91](assets/wf-91.png)

### Boîte de réception - Paramètres {#inbox-view-settings}

Pour les deux vues (Liste et Calendrier), vous pouvez définir des paramètres :

* **Vue Calendrier**

  Pour la **vue Calendrier**, vous pouvez configurer les éléments suivants :

   * **Regrouper par**
   * **Planification** ou **Aucun**
   * **Taille des cartes**

  ![wf-92](assets/wf-92.png)

* **Vue Liste**

  Pour la **vue Liste**, vous pouvez configurer le mécanisme de tri :

   * **Champ de tri**
   * **Ordre de tri**

  ![wf-83](assets/inbox-settings.png)

### Boîte de réception - Contrôle d’administration {#inbox-admin-control}

L’option Contrôle d’administration permet les actions suivantes aux responsables de l’administration :

* Personnalisation des colonnes de la boîte de réception AEM

* Personnalisation du texte et du logo de l’en-tête

* Contrôle de l’affichage des liens de navigation disponibles dans l’en-tête

L’option Contrôle d’administration n’est visible que pour les membres du groupe `administrators` ou `workflow-administrators`.

* **Personnalisation des colonnes** : personnalisez une boîte de réception AEM pour modifier le titre par défaut d’une colonne, réorganiser la position d’une colonne et afficher des colonnes supplémentaires en fonction des données d’un workflow.
   * **Ajouter une colonne** : sélectionnez une colonne à ajouter dans la boîte de réception AEM.
   * **Modifier une colonne** : passez la souris sur le titre de la colonne et cliquez sur l’icône ![modifier](assets/edit.svg) pour saisir le nom d’affichage d’une colonne.
   * **Supprimer une colonne** : cliquez sur l’icône ![supprimer](assets/delete_updated.svg) pour supprimer la colonne de la boîte de réception AEM.
   * **Déplacer la colonne** : faites glisser l’icône ![déplacer](assets/move_updated.svg) pour déplacer une colonne vers un nouvel emplacement dans la boîte de réception d’AEM.

  ![admin-control](assets/admin-control-column-customize.png)

* **Personnalisation de l’image de marque**

   * **Personnaliser le texte de l’en-tête :** spécifiez le texte à afficher dans l’en-tête pour remplacer le texte **Adobe Experience Manager** par défaut.

   * **Personnaliser le logo :** spécifiez l’image à afficher dans l’en-tête en tant que logo. Chargez une image dans la gestion des ressources numériques (DAM) et faites-y référence dans le champ.

* **Navigation de l’utilisateur**
   * **Masquer les options de navigation :** sélectionnez cette option pour masquer les options de navigation disponibles dans l’en-tête. Les options de navigation incluent des liens vers d’autres solutions, un lien Aide et les options de création disponibles lorsque vous appuyez sur le logo ou le texte Adobe Experience Manager.
* **Enregistrer :** cliquez sur cette option pour enregistrer les paramètres.

## Action sur un élément {#taking-action-on-an-item}

>[!NOTE]
>
>Bien qu’il soit possible de sélectionner plusieurs éléments, des actions ne peuvent être entreprises que sur un seul élément à la fois.


1. Pour agir sur un élément, sélectionnez la miniature de l’élément approprié. Les icônes des actions applicables à cet élément s’affichent dans la barre d’outils :

   ![wf-84](assets/wf-84.png)

   Les actions disponibles varient selon l’élément et incluent les opérations suivantes :

   * L’action **Terminer** ; par exemple une tâche ou un élément de workflow.
   * **Réaffecter**/**Déléguer** un élément.
   * **Ouvrir** un élément ; selon le type d’élément, cette action permet d’effectuer les opérations suivantes :

      * afficher les propriétés de l’élément ;
      * Ouvrir un tableau de bord ou un assistant pour effectuer d’autres actions ;
      * ouvrir la documentation connexe.

   * **Revenir** à une étape précédente.
   * Afficher le payload pour un workflow.
   * Créer un projet à partir de l’élément.

   >[!NOTE]
   >
   >Pour plus d’informations, voir :
   >
   >* Éléments de workflow – [Participation aux workflows](/help/sites-authoring/workflows-participating.md)

1. Une action démarre en fonction de l’élément sélectionné, par exemple :

   * une boîte de dialogue correspondant à l’opération s’ouvre ;
   * un assistant d’action démarre ;
   * une page de documentation s’ouvre.

   Par exemple, la fonction **Réaffecter** ouvre une boîte de dialogue :

   ![wf-85](assets/wf-85.png)

   Selon qu’une boîte de dialogue, une page de documentation ou un assistant a été ouvert, vous pouvez :

   * Confirmez l’action appropriée, par exemple Réaffecter.
   * Annuler l’action.
   * Flèche vers l’arrière ; par exemple, si une page de documentation ou un assistant d’action a été ouvert, vous pouvez revenir à la boîte de réception.

## Création d’une tâche {#creating-a-task}

Vous pouvez créer des tâches à partir de la boîte de réception :

1. Sélectionner **Créer**, puis **Tâche**.
1. Renseignez les champs nécessaires dans les onglets **De base** et **Avancé** (seul le **titre** est obligatoire, tous les autres sont facultatifs) :

   * **De base** :

      * **Titre**
      * **Projet**
      * **Cessionnaire**
      * **Contenu** : similaire à payload, il s’agit d’une référence de la tâche à un emplacement dans le référentiel.
      * **Description**
      * **Priorité de la tâche**
      * **Date de début**
      * **Date d’échéance**

   ![wf-86](assets/wf-86.png)

   * **Avancé**

      * **Nom** : ce champ est utilisé pour former l’URL. S’il est vide, le nom est basé sur le champ **Titre**.

   ![wf-87](assets/wf-87.png)

1. Sélectionnez **Envoyer**.

## Création d’un projet {#creating-a-project}

Pour certaines tâches, vous pouvez créer un [projet](/help/sites-authoring/projects.md) en fonction de cette tâche :

1. Sélectionnez la tâche appropriée en appuyant/cliquant sur la miniature.

   >[!NOTE]
   >
   >Seules les tâches créées à l’aide de l’option **Créer** de la **boîte de réception** peuvent être utilisées pour créer un projet.
   >
   >Les éléments de travail (d’un workflow) ne peuvent pas être utilisés pour créer un projet.

1. Sélectionnez **Créer un projet** depuis la barre d’outils pour ouvrir l’assistant.
1. Sélectionnez le modèle requis, puis **Suivant** :
1. Spécifiez les propriétés requises :

   * **De base**

      * **Titre**
      * **Description**
      * **Date de début**
      * **Date d’échéance**
      * **Utilisateur** et rôle

   * **Avancé**

      * **Nom**

   >[!NOTE]
   >
   >Voir [Création d’un projet](/help/sites-authoring/touch-ui-managing-projects.md#creating-a-project) pour obtenir des informations complètes.

1. Sélectionnez **Créer** pour confirmer l’action.

## Filtrage des éléments dans la boîte de réception AEM {#filtering-items-in-the-aem-inbox}

Vous pouvez filtrer les éléments répertoriés :

1. Ouvrez la **boîte de réception AEM**.

1. Ouvrez le sélecteur de filtre :

   ![wf-88](assets/wf-88.png)

1. Vous pouvez filtrer les éléments répertoriés en fonction d’une série de critères qui peuvent pour la plupart être affinés, par exemple :

   ![wf-89](assets/wf-89.png)

   >[!NOTE]
   >
   >Dans la vue [Liste](#inbox-view-settings), vous pouvez également configurer l’ordre de tri dans les [paramètres d’affichage](#inbox-list-view).
