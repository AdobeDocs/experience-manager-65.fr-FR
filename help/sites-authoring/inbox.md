---
title: 'Votre boîte de réception  '
seo-title: Votre boîte de réception
description: Gestion de vos tâches à l’aide de la boîte de réception
seo-description: Gestion de vos tâches à l’aide de la boîte de réception
uuid: ddd48019-ce69-4a47-be2b-5b66ae2fe3c8
contentOwner: Chris Bohnert
products: SG_EXPERIENCEMANAGER/6.5/SITES
topic-tags: introduction
content-type: reference
discoiquuid: 8b607b55-2412-469f-856b-0a3dea4b0efb
exl-id: 80b7f179-b011-4f90-b5ab-9ef8a669d271
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1148'
ht-degree: 79%

---

# Votre boîte de réception  {#your-inbox}

Vous pouvez recevoir des notifications de diverses sections d’AEM, y compris des workflows et des projets. Ces notifications peuvent par exemple concerner les éléments suivants :

* Tâches :

   * ces notifications peuvent également être créées à différents endroits de l’interface utilisateur AEM, par exemple, sous **Projets** ;
   * elles peuvent être générées par l’étape **Créer une tâche** ou **Créer une tâche de projet** d’un workflow.

* Workflows :

   * tâches correspondant à des opérations que vous devez exécuter sur le contenu de la page ;

      * ces notifications sont générées par l’étape **Participant** des workflows
   * éléments d’échec, pour permettre aux administrateurs de relancer l’étape qui a échoué.


Vous recevez ces notifications dans votre propre boîte de réception où vous pouvez les visualiser et effectuer des actions.

>[!NOTE]
>
>AEM est fourni avec des tâches administratives prêtes à l’emploi attribuées au groupe d’utilisateurs administrateurs. Voir [Tâches administratives prêtes à l’emploi](#out-of-the-box-administrative-tasks) pour plus d’informations.

>[!NOTE]
>
>Pour plus d’informations sur les types d’éléments, voir aussi :
>
>* [Projets](/help/sites-authoring/touch-ui-managing-projects.md)
* [Projets – Utilisation des tâches](/help/sites-authoring/task-content.md)
* [Workflows](/help/sites-authoring/workflows.md)
* [Formulaires](/help/forms/home.md)



## Boîte de réception dans l’en-tête {#inbox-in-the-header}

Dans les deux consoles, le nombre actuel d’éléments présents dans votre boîte de réception est indiqué dans l’en-tête. Vous pouvez également ouvrir l’indicateur pour accéder rapidement aux pages nécessitant une ou plusieurs opérations ou pour accéder à la boîte de réception :

![wf-80](assets/wf-80.png)

>[!NOTE]
Certaines opérations sont également répertoriées en [mode Carte de la ressource appropriée](/help/sites-authoring/basic-handling.md#card-view).

## Tâches administratives prêtes à l’emploi  {#out-of-the-box-administrative-tasks}

AEM est fourni avec quatre tâches prêtes à l’emploi attribuées au groupe d’utilisateurs administrateurs.

* [Configurer Analytics et Targeting](/help/sites-administering/opt-in.md)
* [Appliquer la liste de contrôle de sécurité AEM](/help/sites-administering/security-checklist.md)
* Autoriser la collecte de statistiques d’utilisation agrégées
* [Configurer HTTPS](/help/sites-administering/ssl-by-default.md)

## Ouverture de la boîte de réception   {#opening-the-inbox}

Pour ouvrir la boîte de réception des notifications AEM :

1. Cliquez/appuyez sur l’indicateur dans la barre d’outils.

1. Sélectionnez **Afficher tout**. La **boîte de réception AEM** s’ouvre. La boîte de réception affiche les éléments des workflows, des projets et des tâches.
1. La vue par défaut est [Liste](#inbox-list-view), mais vous pouvez également passer à la [Vue Calendrier](#inbox-calendar-view). Pour ce faire, utilisez le sélecteur de vue (barre d’outils, en haut à droite).

   Vous pouvez également définir les [paramètres d’affichage](#inbox-view-settings) pour ces deux modes ; les options disponibles dépendent du mode actif.

   ![wf-79](assets/inbox-list-view.png)

>[!NOTE]
La boîte de réception fonctionne comme une console. Vous pouvez ainsi utiliser la [navigation globale](/help/sites-authoring/basic-handling.md#global-navigation) ou la fonction de [recherche](/help/sites-authoring/search.md) pour accéder à un autre emplacement lorsque vous avez terminé.

### Boîte de réception – Mode Liste {#inbox-list-view}

Ce mode affiche tous les éléments, ainsi que les principales informations clés :

![wf-82](assets/wf-82.png)

### Boîte de réception – Mode Calendrier {#inbox-calendar-view}

Ce mode affiche les éléments en fonction de leur position dans le calendrier et du mode d’affichage que vous avez sélectionné :

![wf-93](assets/wf-93.png)

Vous pouvez :

* sélectionner un mode d’affichage spécifique (**Chronologie**, **Colonne**, **Liste**) ;

* spécifier les tâches à afficher (**Planification**, **Tous**, **Planifiés**, **En cours**, **Échéance proche** et **Échéance dépassée**) ;

* descendre dans la hiérarchie pour obtenir plus d’informations sur un élément ;
* sélectionner une période sur laquelle cibler la vue :

![wf-91](assets/wf-91.png)

### Boîte de réception - Paramètres {#inbox-view-settings}

Vous pouvez définir des paramètres d’affichage pour les deux modes (Liste et Calendrier) :

* **Vue Calendrier**

   Pour le **mode Calendrier**, vous pouvez configurer les paramètres suivants :

   * **Regrouper par**
   * **Planification** ou **Aucun**
   * **Taille des cartes**

   ![wf-92](assets/wf-92.png)

* **Mode Liste**

   Pour le **mode Liste**, vous pouvez configurer le mécanisme de tri :

   * **Champ de tri**
   * **Ordre de tri**

   ![wf-83](assets/inbox-settings.png)

### Boîte de réception - Contrôle d’administration {#inbox-admin-control}

L’option Contrôle d’administration permet aux administrateurs de :

* Personnalisation des colonnes de la boîte de réception AEM

* Personnalisation du texte et du logo de l’en-tête

* Contrôle de l’affichage des liens de navigation disponibles dans l’en-tête

L’option Contrôle d’administration est visible uniquement pour les membres du groupe `administrators` ou `workflow-administrators` .

* **Personnalisation des colonnes** : Personnalisez une boîte de réception d’AEM pour modifier le titre par défaut d’une colonne, réorganiser la position d’une colonne et afficher des colonnes supplémentaires en fonction des données d’un workflow.
   * **Ajouter une colonne** : Sélectionnez une colonne à ajouter dans AEM boîte de réception.
   * **Modifier la colonne** : Passez la souris sur le titre de la colonne et appuyez sur  ![](assets/edit.svg) Modifier pour saisir le nom d’affichage d’une colonne.
   * **Supprimer la colonne** : Appuyez sur l’ ![](assets/delete_updated.svg) icône Supprimer pour supprimer la colonne de la boîte de réception AEM.
   * **Déplacer la colonne** : Faites glisser l’ ![](assets/move_updated.svg) icône de déplacement pour déplacer une colonne vers un nouvel emplacement dans AEM boîte de réception.

   ![admin-control](assets/admin-control-column-customize.png)

* **Personnalisation de l’identité graphique**

   * **Personnaliser le texte de l’en-tête :** spécifiez le texte à afficher dans l’en-tête pour remplacer le texte  **Adobe Experience** Manager par défaut.

   * **Personnaliser le logo :** spécifiez l’image à afficher dans l’en-tête sous forme de logo. Chargez une image dans la gestion des ressources numériques (DAM) et faites-y référence dans le champ .

* **Navigation de l’utilisateur**
   * **Masquer les options de navigation :**  sélectionnez cette option pour masquer les options de navigation disponibles dans l’en-tête. Les options de navigation incluent des liens vers d’autres solutions, un lien d’aide et les options de création disponibles lorsque vous appuyez sur le logo ou le texte Adobe Experience Manager.
* **Enregistrer :** appuyez/cliquez sur cette option pour enregistrer les paramètres.

## Action sur un élément {#taking-action-on-an-item}

>[!NOTE]
Bien qu’il soit possible de sélectionner plusieurs éléments, des actions ne peuvent être entreprises que sur un seul élément à la fois.


1. Pour agir sur un élément, sélectionnez la miniature de l’élément souhaité. Les icônes des actions applicables à cet élément apparaissent dans la barre d’outils :

   ![wf-84](assets/wf-84.png)

   Les actions disponibles varient selon l’élément et incluent les opérations suivantes :

   * **Terminer** l’action; par exemple, une tâche ou un élément de workflow.
   * **Réaffecter**/**Déléguer** un élément.
   * **Ouvrir** un élément ; selon le type d’élément, cette action permet d’effectuer les opérations suivantes :

      * Afficher les propriétés de l’élément.
      * Ouvrir un tableau de bord ou un assistant pour effectuer d’autres actions.
      * Ouvrir la documentation associée.
   * **Revenir** à une étape précédente.
   * Afficher la charge utile pour un workflow.
   * Créer un projet à partir de l’élément.

   >[!NOTE]
   Pour plus d’informations, voir :
   * Éléments de workflow – [Participation aux workflows](/help/sites-authoring/workflows-participating.md)


1. Une action démarre en fonction de l’élément sélectionné ; par exemple :

   * Une boîte de dialogue correspondant à l’opération s’ouvre.
   * Un assistant d’action démarre.
   * Une page de documentation s’ouvre.

   Par exemple, **Réaffecter** ouvre une boîte de dialogue :

   ![wf-85](assets/wf-85.png)

   Selon qu’une boîte de dialogue, une page de documentation ou un assistant a été ouvert, vous pouvez :

   * Confirmer l’action appropriée, par exemple Réaffecter.
   * Annuler l’action.
   * Cliquer sur la flèche Précédent ; par exemple, si une page de documentation ou un assistant d’action a été ouvert, vous pouvez revenir à la boîte de réception.


## Création d’une tâche {#creating-a-task}

Vous pouvez créer des tâches directement à partir de la boîte de réception :

1. Sélectionnez **Créer**, puis **Tâche**.
1. Renseignez les champs nécessaires dans les onglets **De base** et **Avancé** ; seul le champ **Titre** est obligatoire, tous les autres sont facultatifs :

   * **De base** :

      * **Titre**
      * **Projet**
      * **Cessionnaire**
      * **Contenu** : similaire à Charge utile ; il s’agit d’une référence de la tâche à un emplacement dans le référentiel
      * **Description**
      * **Priorité de la tâche**
      * **Date de début**
      * **Échéance**

   ![wf-86](assets/wf-86.png)

   * **Avancé**

      * **Nom** : ce champ est utilisé pour former l’URL ; s’il est vide, le nom est basé sur le champ **Titre**.

   ![wf-87](assets/wf-87.png)

1. Sélectionnez **Envoyer**.

## Création d’un projet {#creating-a-project}

Pour certaines tâches, vous pouvez créer un [projet](/help/sites-authoring/projects.md) basé sur cette tâche :

1. Sélectionnez la tâche appropriée en appuyant/cliquant sur la miniature.

   >[!NOTE]
   Seules les tâches créées à l’aide de l’option **Créer** de la **boîte de réception** peuvent être utilisées pour créer un projet.
   Les éléments de travail (d’un workflow) ne peuvent pas être utilisés pour créer un projet.

1. Sélectionnez **Créer un projet** depuis la barre d’outils pour ouvrir l’assistant.
1. Sélectionnez le modèle approprié, puis **Suivant**.
1. Spécifiez les propriétés requises :

   * **De base**

      * **Titre**
      * **Description**
      * **Date de début**
      * **Échéance**
      * **Utilisateur** et rôle
   * **Avancé**

      * **Nom**
   >[!NOTE]
   Pour plus d’informations, voir [Création d’un projet](/help/sites-authoring/touch-ui-managing-projects.md#creating-a-project).

1. Sélectionnez **Créer** pour confirmer l’action.

## Filtrage des éléments dans la boîte de réception AEM {#filtering-items-in-the-aem-inbox}

Vous pouvez filtrer les éléments répertoriés :

1. Ouvrez la **boîte de réception AEM**.

1. Ouvrez le sélecteur de filtre :

   ![wf-88](assets/wf-88.png)

1. Vous pouvez filtrer les éléments répertoriés en fonction d’une série de critères, pouvant pour la plupart être affinés, par exemple :

   ![wf-89](assets/wf-89.png)

   >[!NOTE]
   En [mode Liste](#inbox-view-settings), vous pouvez également configurer l’ordre de tri dans les [paramètres d’affichage](#inbox-list-view).
