---
title: Gestion des applications et des tâches Forms dans la boîte de réception AEM
description: La boîte de réception AEM vous permet de lancer des workflows basés sur l’utilisation de Forms via l’envoi d’applications et de tâches de gestion.
contentOwner: vishgupt
topic-tags: document_services, publish
products: SG_EXPERIENCEMANAGER/6.5/FORMS
docset: aem65
exl-id: 8d17194b-8baf-4878-b3ae-d351a056aebf
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms, Workflow
role: Admin, User, Developer
source-git-commit: e821be5233fd5f6688507096790d219d25903892
workflow-type: tm+mt
source-wordcount: '1069'
ht-degree: 100%

---

# Gestion des applications et des tâches Forms dans la boîte de réception AEM {#manage-forms-applications-and-tasks-in-aem-inbox}

L’une des nombreuses façons de lancer ou de déclencher un processus orienté formulaire consiste à utiliser des applications dans la boîte de réception AEM. Pour rendre un workflow de Forms disponible en tant qu’application dans la boîte de réception, créez une application de workflow. Pour plus d’informations sur l’application de processus et d’autres façons de lancer les processus de Forms, voir [Lancement d’un processus orienté formulaire sur OSGi](../../forms/using/aem-forms-workflow.md#launch).

En outre, la boîte de réception AEM rassemble les notifications et les tâches provenant de divers composants d’AEM, y compris les workflows de Forms. Lorsqu’un processus Forms contenant une étape Affecter une tâche est déclenché, l’application associée est répertoriée comme une tâche dans la boîte de réception de la personne désignée. Si l’entité désignée est un groupe, la tâche apparaît dans la boîte de réception de toutes les personnes membres du groupe jusqu’à ce qu’une personne demande ou délègue la tâche.

L’interface utilisateur de la boîte de réception fournit la liste et les vues de calendrier pour afficher les tâches. Vous pouvez également configurer les paramètres d’affichage. Vous pouvez filtrer les tâches en fonction de divers paramètres. Pour plus d’informations sur la vue et les filtres, voir [Votre boîte de réception](/help/sites-authoring/inbox.md).

En résumé, la boîte de réception vous permet de créer une nouvelle application et de gérer les tâches affectées.

>[!NOTE]
>
>Vous devez être membre du groupe workflow-users pour pouvoir utiliser la boîte de réception AEM.

## Création d’une application {#create-application}

1. Accédez à la boîte de réception AEM à l’adresse https://’[serveur]:[port/]’/aem/inbox.
1. Dans l’interface utilisateur de la boîte de réception, sélectionnez **[!UICONTROL Créer > Application]**. La page Sélectionner l’application s’affiche.
1. Sélectionnez une application, puis appuyez sur **[!UICONTROL Créer]**. Le formulaire adaptatif associé à l’application s’ouvre. Renseignez les informations dans le formulaire adaptatif et sélectionnez **[!UICONTROL Envoyer]**. Cette action lance le processus associé et crée une tâche dans la boîte de réception de la personne désignée.

## Gestion des tâches {#manage-tasks}

Lorsqu’une workflow de Forms se déclenche et que vous êtes une personne désignée ou que vous faites partie du groupe de personnes désignées, une tâche apparaît dans votre boîte de réception. Vous pouvez afficher les détails de la tâche et effectuer les actions demandées à partir de la boîte de réception.

### Demande ou délégation de tâches {#claim-or-delegate-tasks}

Les tâches affectées à un groupe apparaissent dans la boîte de réception de toutes les personnes membres du groupe. Toute personne membre du groupe peut demander la tâche ou la déléguer à une autre personne membre du groupe. Pour ce faire :

1. Sélectionnez la miniature de la tâche. Les options d’ouverture ou de délégation de la tâche s’affichent en haut.

   ![select-task](assets/select-task.png)

1. Utilisez l’une des méthodes suivantes :

   * Pour déléguer la tâche, sélectionnez **[!UICONTROL Déléguer]**. La boîte de dialogue Déléguer l’élément s’affiche. Sélectionnez un utilisateur ou une utilisatrice (vous pouvez également ajouter un commentaire) puis sélectionnez **[!UICONTROL OK]**.

   ![déléguer](assets/delegate.png)

   * Pour revendiquer la tâche, sélectionnez **[!UICONTROL Ouvrir]**. La boîte de dialogue Auto-affecter s’affiche. Sélectionnez **[!UICONTROL Continuer]** pour revendiquer la tâche. La tâche demandée apparaît dans votre boîte de réception, avec vous en tant que personne désignée.

   ![claim](assets/claim.png)

### Affichage des détails et actions sur les tâches {#view-details-and-perform-actions-on-tasks}

Lorsque vous ouvrez une tâche, vous pouvez afficher les détails de celle-ci et exécuter les actions disponibles. Les actions disponibles pour une tâche sont définies à l’étape Attribuer une tâche du workflow de Forms associé.

1. Sélectionnez la miniature de la tâche. Les options pour ouvrir ou déléguer la tâche sélectionnée s’affichent en haut.
1. Sélectionnez **Ouvrir** pour afficher les détails de la tâche. La vue détaillée de la tâche s’ouvre. Dans cette vue, vous pouvez afficher les détails de la tâche et travailler sur cette dernière.

   >[!NOTE]
   >
   >Si une tâche est affectée à un groupe, vous devez d’abord la demander pour pouvoir l’ouvrir dans la vue détaillée.

![détails de la tâche](assets/task-details.png)

La vue détaillée de tâche comprend les sections suivantes :

* Détails de la tâche
* Formulaire
* Détails du processus
* Barre d’outils Actions

#### Détails de la tâche {#task-details}

La section Détails de la tâche affiche des informations sur la tâche. Les informations affichées dépendent des paramètres de configuration de l’[étape Affecter une tâche](/help/sites-developing/workflows-step-ref.md) dans le processus. Dans l’exemple ci-dessus s’affichent la description, le statut, la date de début et le workflow utilisé pour la tâche. Vous pouvez également joindre un fichier à la tâche.

#### Formulaire {#form}

L’onglet Formulaire dans la zone de contenu principale affiche le formulaire envoyé et les pièces jointes du champ, le cas échéant.

#### Détails du processus {#workflow-details}

L’onglet Détails du workflow en haut affiche la progression de la tâche via différentes étapes du worflow. Il affiche les étapes terminées, en cours et en attente pour la tâche. Les étapes d’un processus sont définies à [l’étape Affecter une tâche](/help/sites-developing/workflows-step-ref.md) du processus associé.

En outre, l’onglet affiche l’historique de la tâche pour chaque étape terminée dans le workflow. Vous pouvez sélectionner **[!UICONTROL Afficher les détails]** d’une étape terminée afin d’en connaître les détails. Cette action permet d’afficher les détails de la tâche : les commentaires, les pièces jointes de formulaire et de tâches, le statut, les dates de début et de fin, etc.

![workflow-details](assets/workflow-details.png)

#### Barre d’outils Actions {#actions-toolbar}

La barre d’outils Actions affiche toutes les options disponibles pour la tâche. Les actions Enregistrer, Réinitialiser et Déléguer sont des actions par défaut, mais d’autres actions disponibles sont configurées dans l’[étape Affecter une tâche](/help/sites-developing/workflows-step-ref.md). Dans l’exemple ci-dessus, les options Approuver et Rejeter sont configurées dans le workflow.

Lorsque vous agissez sur la tâche, elle se poursuit dans le workflow.

### Afficher les tâches terminées {#view-completed-tasks}

La boîte de réception AEM affiche uniquement les tâches actives. Les tâches terminées n’apparaissent pas dans la liste. Cependant, vous pouvez utiliser les filtres de la boîte de réception pour filtrer les tâches en fonction de plusieurs paramètres, tels que le type de tâche, le statut, les dates de début et de fin, etc. Pour afficher les tâches terminées :

1. Dans la boîte de réception AEM, sélectionnez ![toggle-side-panel1](assets/toggle-side-panel1.png) pour ouvrir le sélecteur de filtres.
1. Sélectionnez l’accordéon **[!UICONTROL Statut de la tâche]** et sélectionnez **[!UICONTROL Terminé]**. Toutes vos tâches terminées s’affichent.

   ![filter](assets/filter.png)

1. Sélectionnez une tâche et cliquez sur **[!UICONTROL Ouvrir]**.

La tâche s’ouvre pour afficher le document ou le formulaire adaptatif associé à la tâche. Pour les formulaires adaptatifs, la tâche affiche le formulaire adaptatif en lecture seule ou son document d’enregistrement PDF tel que configuré dans l’onglet Formulaire/Document de l’[étape de workflow Affecter une tâche](/help/sites-developing/workflows-step-ref.md).

La section de détails de la tâche affiche des informations telles qu’une mesure prise, l’état de la tâche, la date de début et la date de fin.

![completed-task](assets/completed-task.png)

L’onglet **[!UICONTROL Détails du processus]** affiche chaque étape du processus. Sélectionnez **[!UICONTROL Afficher les détails]** d’une étape pour obtenir des informations détaillées.

![completed-task-workflow](assets/completed-task-workflow.png)

## Résolution des problèmes {#troubleshooting-workflows}

### Impossible de voir des éléments liés au processus AEM dans la boîte de réception AEM {#unable-to-see-aem-worklow-items}

Une personne propriétaire de modèle de workflow ne peut pas afficher des éléments liés au workflow AEM dans la boîte de réception AEM. Pour résoudre ce problème, ajoutez les index suivants à votre référentiel AEM et recréez l’index.

1. Pour ajouter des index, utilisez l’une des méthodes suivantes :

   * Créez les nœuds suivants dans CRX DE à `/oak:index/workflowDataLucene/indexRules/granite:InboxItem/properties` avec les propriétés respectives spécifiées dans le tableau suivant :

     | Nœud | Propriété | Type |
     |---|---|---|
     | sharedWith | sharedWith | CHAÎNE |
     | verrouillé | verrouillé | BOOLÉEN |
     | renvoyé | renvoyé | BOOLÉEN |
     | allowInboxSharing | allowInboxSharing | BOOLÉEN |
     | allowExplicitSharing | allowExplicitSharing | BOOLÉEN |


   * Déployez les index par le biais d’un package AEM. Vous pouvez utiliser un projet [AEM Archetype](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/developing/archetype/using.html?lang=fr) pour créer un package AEM déployable. Utilisez l’exemple de code suivant pour ajouter des index à un projet AEM Archetype :

   ```Java
      .property("sharedWith", "sharedWith").type(TYPENAME_STRING).propertyIndex()
      .property("locked", "locked").type(TYPENAME_BOOLEAN).propertyIndex()
      .property("returned", "returned").type(TYPENAME_BOOLEAN).propertyIndex()
      .property("allowInboxSharing", "allowInboxSharing").type(TYPENAME_BOOLEAN).propertyIndex()
      .property("allowExplicitSharing", "allowExplicitSharing").type(TYPENAME_BOOLEAN).propertyIndex()
   ```

1. [Créez un index de propriétés et définissez-le sur Vrai](https://experienceleague.adobe.com/docs/experience-manager-65/deploying/deploying/queries-and-indexing.html?lang=fr#the-property-index).

1. Après avoir configuré des index dans CRX DE ou procédé au déploiement via un package, [réindexez le référentiel](https://helpx.adobe.com/fr/experience-manager/kb/HowToCheckLuceneIndex.html#Completelyrebuildtheindex).

https://experienceleague.adobe.com/docs/experience-manager-65/deploying/deploying/queries-and-indexing.html?lang=fr
