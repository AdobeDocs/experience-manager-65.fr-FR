---
title: Personnaliser les détails de la tâche
description: Comment personnaliser la page des détails de la tâche dans l’espace de travail AEM Forms pour modifier les informations par défaut affichées sur une tâche.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
exl-id: 48c24442-22d2-4d1a-9462-0aba78340281
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '263'
ht-degree: 34%

---

# Personnaliser les détails de la tâche {#customizing-the-task-details-page}

La page Détails de la tâche contient des informations relatives à une tâche et à ses processus. Cependant, vous pouvez personnaliser la page Détails de la tâche pour ajouter ou supprimer des informations.

Vous pouvez ajouter les informations suivantes à la page Détails de la tâche :

* Informations disponibles dans l’objet JSON d’une tâche (section Tâche dans [Description de l’objet JSON de l’espace de travail AEM Forms](/help/forms/using/html-workspace-json-object-description.md))
* Informations disponibles dans l’objet JSON d’une instance de processus (section Instance de processus dans [Description de l’objet JSON de l’espace de travail AEM Forms](/help/forms/using/html-workspace-json-object-description.md))

Pour personnaliser la page des détails de la tâche :

1. Suivez [Procédure générique de personnalisation de l’espace de travail AEM Forms.](/help/forms/using/generic-steps-html-workspace-customization.md)
1. Pour afficher d’autres informations, ajoutez les paires clé-valeur correspondantes au `translation.json` fichier à l’emplacement `todo`block > `details`block > `app`block > [`required`block].

   La variable [`required`block] fait référence aux blocs disponibles, tels que le bloc de tâche pour les informations sur la tâche, le bloc de processus pour les informations sur le processus et le bloc de tâche en attente pour les informations sur les tâches en attente.

   Par exemple, pour ajouter des informations sur la sélection d’itinéraire requise dans la page des détails de la tâche, vous pouvez ajouter la paire clé-valeur suivante dans le bloc de tâche :

   ```json
   "todo" : {
       .
       .
       .
       "details" : {
           .
           .
           "task" : {
               .
               .
               "RouteSelectionRequired" : "Route Selection Required"
           }
       }
   }
   ```

   >[!NOTE]
   >
   >Ajoutez les paires clé-valeur correspondantes pour toutes les langues prises en charge.

1. Copiez `/libs/ws/js/runtime/templates/taskdetails.html` dans `/apps/ws/js/runtime/templates/taskdetails.html`.

   Ajoutez les nouvelles informations à `/apps/ws/js/runtime/templates/taskdetails.html`. Par exemple :

   ```css
   <div class="detailsContainer">
       .
       .
       <ul>
           .
           .
           <li>
               <label for="routeSelectionRequired" title="<%= $.t('todo.details.task.RouteSelectionRequired')%>"><%= $.t('todo.details.task.RouteSelectionRequired')%></label>
               <div>
                   <span id="routeSelectionRequired"><%= isRouteSelectionRequired != null ? isRouteSelectionRequired : ''%></span>
               </div>
           </li>
           .
           .
       </ul>
   </div>
   ```

1. Ouvrez /apps/ws/js/registry.js pour le modifier.

   Recherchez et remplacez `text!/lc/libs/ws/js/runtime/templates/taskdetails.html` par `text!/lc/apps/ws/js/runtime/templates/taskdetails.html`.

>[!NOTE]
>
>Pour personnaliser la page Détails de la tâche avec des tâches créées dans l’onglet **Démarrer le processus** de l’espace de travail AEM Forms, ajoutez les nouvelles informations dans `/apps/ws/js/runtime/templates/startprocess.html`.
>
>Pour ajouter de nouveaux styles pour les informations ajoutées dans la page Détails, modifiez le fichier CSS à l’aide de la section *Modifications de l’interface utilisateur* dans [Personnalisation de l’espace de travail](changing-locale-user-interface.md).
