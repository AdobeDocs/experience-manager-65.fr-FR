---
title: Personnalisation de la page Détails de la tâche
seo-title: Personnalisation de la page Détails de la tâche
description: Comment personnaliser les détails de la tâche dans l’espace de travail AEM Forms pour modifier les informations par défaut affichées relatives à une tâche.
seo-description: Comment personnaliser les détails de la tâche dans l’espace de travail AEM Forms pour modifier les informations par défaut affichées relatives à une tâche.
uuid: d85fae55-8e66-4595-8560-5485622b6841
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 16e57cf6-aaa1-406d-a6ad-71ec60b15386
translation-type: tm+mt
source-git-commit: 726163106ddb80600eaa7cc09b1a2e9b035a223e

---


# Customizing the task details page {#customizing-the-task-details-page}

La page Détails de la tâche contient des informations relatives à une tâche et à ses processus. Toutefois, vous pouvez personnaliser la page Détails de la tâche pour ajouter ou supprimer des informations.

Vous pouvez ajouter les informations ci-dessous à la page Détails de la tâche :

* Informations disponibles dans l’objet JSON d’une tâche (section Tâche dans [Description de l’objet JSON de l’espace de travail AEM Forms](/help/forms/using/html-workspace-json-object-description.md))
* Informations disponibles dans l’objet JSON d’une instance de processus (section Instance de processus dans [Description de l’objet JSON de l’espace de travail AEM Forms](/help/forms/using/html-workspace-json-object-description.md))

Pour personnaliser la page Détails de la tâche :

1. Suivez la [Procédure générique de personnalisation de l’espace de travail AEM Forms.](/help/forms/using/generic-steps-html-workspace-customization.md) 
1. To show any additional information, add corresponding key-value pairs to the `translation.json` file at `todo`block > `details`block > `app`block > [ `required`block].

   The [ `required`block] refers to available blocks, such as the task block for task information, process block for process information, and currentpendingtask block for pending tasks information.

   Par exemple, pour ajouter des informations sur la sélection d’itinéraire requise dans la page Détails de la tâche, vous pouvez ajouter la paire clé-valeur suivante dans le bloc de tâche :

   ```
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

1. Copiez `/libs/ws/js/runtime/templates/taskdetails.html` vers `/apps/ws/js/runtime/templates/taskdetails.html`.

   Ajouter les nouvelles informations à `/apps/ws/js/runtime/templates/taskdetails.html`. Par exemple :

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

   Search and replace `text!/lc/libs/ws/js/runtime/templates/taskdetails.html` with `text!/lc/apps/ws/js/runtime/templates/taskdetails.html`.

>[!NOTE]
>
>To customize the task details page with tasks created in the **Start Process** tab of AEM Forms workspace, add the new information to `/apps/ws/js/runtime/templates/startprocess.html`.
>
>To add new styles for the information added in the details page, modify the CSS file by using the *User interface changes* section in [Workspace Customization](changing-locale-user-interface.md).
