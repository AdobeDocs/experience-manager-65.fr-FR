---
title: Personnalisation des tableaux de suivi
seo-title: Personnalisation des tableaux de suivi
description: Comment personnaliser l’affichage des détails des processus utilisateur dans le tableau de la tâche affiché dans l’onglet de suivi de l’espace de travail AEM Forms.
seo-description: Comment personnaliser l’affichage des détails des processus utilisateur dans le tableau de la tâche affiché dans l’onglet de suivi de l’espace de travail AEM Forms.
uuid: 13d6ebf2-99d5-434f-85f9-b0cba5f5751a
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: bb7a6e9f-4f28-4d97-8a0c-949259fd6857
translation-type: tm+mt
source-git-commit: 56c6cfd437ef185336e81373bd5f758205b96317

---


# Personnalisation des tableaux de suivi{#customize-tracking-tables}

L’onglet de suivi dans l’espace de travail AEM Forms permet d’afficher les détails des instances de processus dans lesquelles l’utilisateur connecté est impliqué. Afin de visualiser les tableaux de suivi, vous devez d’abord sélectionner le nom d’un processus dans le volet gauche pour afficher la liste de ses instances dans le volet central. Sélectionnez une instance de processus pour afficher un tableau des tâches générées par cette instance dans le volet droit. Par défaut, les colonnes du tableau affichent les attributs de tâche suivants (l’attribut correspondant dans le modèle de tâche est indiqué entre parenthèses) :

* ID ( `taskId`)
* Nom ( `stepName`)
* Instructions ( `instructions`)
* Action sélectionnée ( `selectedRoute`)
* Heure de création ( `createTime`)
* Heure d’achèvement ( `completeTime`)
* Propriétaire ( `currentAssignment.queueOwner`)

Les attributs restants dans le modèle de tâche disponibles à l’affichage dans le tableau de la tâche sont les suivants :

<table>
 <tbody>
  <tr>
   <td><p>actionInstanceId</p> </td>
   <td><p>isOpenFullScreen</p> </td>
   <td><p>reminderCount</p> </td>
  </tr>
  <tr>
   <td><p>classOfTask</p> </td>
   <td><p>isOwner</p> </td>
   <td><p>routeList</p> </td>
  </tr>
  <tr>
   <td><p>consultGroupId</p> </td>
   <td><p>isRouteSelectionRequired</p> </td>
   <td><p>savedFormCount</p> </td>
  </tr>
  <tr>
   <td><p>contentType</p> </td>
   <td><p>isShowAttachments</p> </td>
   <td><p>serializedImageTicket</p> </td>
  </tr>
  <tr>
   <td><p>createTime</p> </td>
   <td><p>isStartTask</p> </td>
   <td><p>serviceName</p> </td>
  </tr>
  <tr>
   <td><p>creationId</p> </td>
   <td><p>isVisible</p> </td>
   <td><p>serviceTitle</p> </td>
  </tr>
  <tr>
   <td><p>currentAssignment</p> </td>
   <td><p>nextReminder</p> </td>
   <td><p>showACLActions</p> </td>
  </tr>
  <tr>
   <td><p>deadline</p> </td>
   <td><p>numForms</p> </td>
   <td><p>showDirectActions</p> </td>
  </tr>
  <tr>
   <td><p>description</p> </td>
   <td><p>numFormsToBeSaved</p> </td>
   <td><p>status</p> </td>
  </tr>
  <tr>
   <td><p>displayName</p> </td>
   <td><p>outOfOfficeUserId</p> </td>
   <td><p>summaryUrl</p> </td>
  </tr>
  <tr>
   <td><p>forwardGroupId</p> </td>
   <td><p>outOfOfficeUserName</p> </td>
   <td><p>supportsSave</p> </td>
  </tr>
  <tr>
   <td><p>isApprovalUI</p> </td>
   <td><p>priority</p> </td>
   <td><p>taskACL</p> </td>
  </tr>
  <tr>
   <td><p>isCustomUI</p> </td>
   <td><p>processInstanceId</p> </td>
   <td><p>taskFormType</p> </td>
  </tr>
  <tr>
   <td><p>isDefaultImage</p> </td>
   <td><p>processInstanceStatus</p> </td>
   <td><p>taskUserInfo</p> </td>
  </tr>
  <tr>
   <td><p>isLocked</p> </td>
   <td><p>processVariables</p> </td>
   <td> </td>
  </tr>
  <tr>
   <td><p>isMustOpenToComplete</p> </td>
   <td><p>readerSubmitOptions</p> </td>
   <td> </td>
  </tr>
 </tbody>
</table>

Pour les personnalisations suivantes dans le tableau de la tâche, vous devez effectuer des modifications sémantiques dans le code source. See [Introduction to Customizing AEM Forms workspace](/help/forms/using/introduction-customizing-html-workspace.md) fo how you can make semantic changes using workspace SDK and build a minified package from the changed source.

## Modification des colonnes du tableau et de leur tri {#changing-table-columns-and-their-order}

1. Pour modifier les attributs de tâche affichés dans le tableau et leur ordre, configurez le fichier /ws/js/runtime/templates/processinstancehistory.html :

   ```as3
   <table>
       <thead>
           <tr>
               <!-- put the column headings in order here, for example-->
               <th><%= $.t('history.fixedTaskTableHeader.taskName')%></th>
               <th><%= $.t('history.fixedTaskTableHeader.taskInstructions')%></th>
               <th><%= $.t('history.fixedTaskTableHeader.taskRoute')%></th>
               <th><%= $.t('history.fixedTaskTableHeader.taskCreateTime')%></th>
               <th><%= $.t('history.fixedTaskTableHeader.taskCompleteTime')%></th>
           </tr>
       </thead>
   </table>
   ```

   ```as3
   <table>
       <tbody>
           <%_.each(obj, function(task){%>
           <tr>
               <!-- Put the task attributes in the order of headings, for example -->
               <td><%= task.stepName %></td>
               <td><%= task.instructions %></td>
               <td><%= !task.selectedRoute?'':(task.selectedRoute=='null'?'Default':task.selectedRoute) %></td>
               <td><%= task.createTime?task.formattedCreateTime:'' %></td>
               <td><%= task.completeTime? task.formattedCompleteTime:'' %></td>
           </tr>
           <%});%>
       </tbody>
   </table>
   ```

## Tri d’un tableau de suivi {#sorting-a-tracking-table}

Pour trier le tableau de la liste de tâches lorsque vous cliquez sur l’en-tête de la colonne :

1. Register a click handler for `.fixedTaskTableHeader th` in the file `js/runtime/views/processinstancehistory.js`.

   ```as3
   events: {
       //other handlers
       "click .fixedTaskTableHeader th": "onTaskTableHeaderClick",
       //other handlers
   }
   ```

   In the handler, invoke the `onTaskTableHeaderClick` function of `js/runtime/util/history.js`.

   ```as3
   onTaskTableHeaderClick: function (event) {
           history.onTaskTableHeaderClick(event);
   }
   ```

1. Exposez la `TaskTableHeaderClick` méthode dans `js/runtime/util/history.js`.

   La méthode recherche l’attribut de tâche dans l’événement de clic, trie la liste des tâches en fonction de cet attribut, et rend le tableau de la tâche avec la liste des tâches triée.

   Le tri s’effectue à l’aide de la fonction de tri Backbone sur la collection de liste de tâches en fournissant une fonction de comparaison.

   ```as3
       return {
           //other methods
           onTaskTableHeaderClick  : onTaskTableHeaderClick,
           //other methods
       };
   ```

   ```as3
   onTaskTableHeaderClick = function (event) {
           var target = $(event.target),
            comparator,
               attribute;
           if(target.hasClass('taskName')){
            attribute = 'stepName';
           } else if(target.hasClass('taskInstructions')){
               attribute = 'instructions';
           } else if(target.hasClass('taskRoute')){
               attribute = 'selectedRoute';
           } else if(target.hasClass('taskCreateTime')){
               attribute = 'createTime';
           } else if(target.hasClass('taskCompleteTime')){
               attribute = 'completeTime';
           }
           taskList.comparator = function (task) {
            return task.get(attribute);
           };
           taskList.sort();
           render();
       };
   ```
