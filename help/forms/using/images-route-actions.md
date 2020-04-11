---
title: Personnalisation des images utilisées dans les actions d’itinéraire
seo-title: Personnalisation des images utilisées dans les actions d’itinéraire
description: Comment personnaliser les images utilisées dans les actions d’itinéraire dans l’espace de travail LiveCycle AEM Forms.
seo-description: Comment personnaliser les images utilisées dans les actions d’itinéraire dans l’espace de travail LiveCycle AEM Forms.
uuid: 42608376-587e-4b57-a9d5-8f9ebd981426
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 10158c13-47b4-43e3-ac47-690f3cbab158
translation-type: tm+mt
source-git-commit: 56c6cfd437ef185336e81373bd5f758205b96317

---


# Personnalisation des images utilisées dans les actions d’itinéraire {#customize-images-used-in-route-actions}

Pour personnaliser les images utilisées dans les actions d’itinéraire, suivez les étapes décrites dans [Procédure générique de personnalisation](/help/forms/using/generic-steps-html-workspace-customization.md), puis la procédure décrite dans cet article.

## Images pour les actions d’itinéraire {#images-for-route-actions}

1. Ajoutez les styles définissant les images dans le CSS à l’emplacement suivant pour les nouvelles actions d’itinéraire :

   `/apps/ws/css/newStyle.css`

   For example: Add a new style called `myStyle1`as shown below and upload the image file `myStyleIcon1.png` to the `/apps/ws/image`s folder using a WebDAV client.

   >[!NOTE]
   >
   >For more information about WebDAV access, see [https://dev.day.com/docs/en/crx/current/how_to/webdav_access.html](https://docs.adobe.com/docs/en/crx/current/how_to/webdav_access.html).

   >[!NOTE]
   >
   >Utilisez le même nom de style que celui de l’action d’itinéraire.

   ```css
   .myStyle1{
   
           background-image: url('../images/myStyleIcon1.png');
   
       }
   ```

## Menu déroulant de l’action de tâche Liste de tâches {#task-list-task-action-popup}

1. Créez un menu déroulant d’actions de liste de tâches, voir [Création du code de l’espace de travail AEM Forms](/help/forms/using/introduction-customizing-html-workspace.md#main-pars-heading-3). Vous devez utiliser le paquet de développement.

1. Copiez `/libs/ws/js/runtime/templates/task.html` vers `/apps/ws/js/runtime/templates/task.html`.

1. If the name of the CSS style is same as the route action name coming from the server, modify the following code in `/apps/ws/js/runtime/templates/task.html`:

   ```
   <%if(routeList == null){%>
               <li>
                   <a href="javascript:void(0);" title="<%= $.t('taskaction.directcommand.'+availableCommands.directCommands[0])%>" value="<%= availableCommands.directCommands[0]%>" data-action="route"><%= $.t('taskaction.directcommand.'+availableCommands.directCommands[0])%></a>
               </li>
               <%}else{%>
               <%for(var i = 0; i<availableCommands.directCommands.length; i++){%>
               <li>
                   <a href="javascript:void(0);" title="<%= availableCommands.directCommands[i]%>" value="<%= availableCommands.directCommands[i]%>" data-action="route"><%= availableCommands.directCommands[i]%></a>
               </li>
               <%}%>
               <%}%>
   
   To
   
   <%if(routeList == null){%>
               <li class="<%= availableCommands.directCommands[0]%>" alt="<%= $.t('taskaction.directcommand.'+availableCommands.directCommands[0]+'.value')%>">
                   <a href="javascript:void(0);" title="<%= $.t('taskaction.directcommand.'+availableCommands.directCommands[0])%>" value="<%= availableCommands.directCommands[0]%>" data-action="route"><%= $.t('taskaction.directcommand.'+availableCommands.directCommands[0])%></a>
               </li>
               <%}else{%>
               <%for(var i = 0; i<availableCommands.directCommands.length; i++){%>
               <li class="<%= availableCommands.directCommands[i]%>" alt="<%= $.t('taskaction.directcommand.'+availableCommands.directCommands[i]+'.value')%>">
                   <a href="javascript:void(0);" title="<%= availableCommands.directCommands[i]%>" value="<%= availableCommands.directCommands[i]%>" data-action="route"><%= availableCommands.directCommands[i]%></a>
               </li>
               <%}%>
               <%}%>
   ```

1. If the name of the CSS style is different from the route action name coming from the server, modify the following code in `/apps/ws/js/runtime/templates/task.html`. Il ajoute une pile des conditions de servlet `if-else` pour mapper le style avec le nom de l’action d’itinéraire.

```
<%if(routeList == null){%>
            <li>
                <a href="javascript:void(0);" title="<%= $.t('taskaction.directcommand.'+availableCommands.directCommands[0])%>" value="<%= availableCommands.directCommands[0]%>" data-action="route"><%= $.t('taskaction.directcommand.'+availableCommands.directCommands[0])%></a>
            </li>
            <%}else{%>
            <%for(var i = 0; i<availableCommands.directCommands.length; i++){%>
            <li>
                <a href="javascript:void(0);" title="<%= availableCommands.directCommands[i]%>" value="<%= availableCommands.directCommands[i]%>" data-action="route"><%= availableCommands.directCommands[i]%></a>
            </li>
            <%}%>
            <%}%>

To

<%if(routeList == null){%>
            <li class="<%= availableCommands.directCommands[0]%>" alt="<%= $.t('taskaction.directcommand.'+availableCommands.directCommands[0]+'.value')%>">
                <a href="javascript:void(0);" title="<%= $.t('taskaction.directcommand.'+availableCommands.directCommands[0])%>" value="<%= availableCommands.directCommands[0]%>" data-action="route"><%= $.t('taskaction.directcommand.'+availableCommands.directCommands[0])%></a>
            </li>
            <%}else{%>
            <%for(var i = 0; i<availableCommands.directCommands.length; i++){%>
                <%if(availableCommands.directCommands[i].equals("myAction1")){%>
                     <li class="myStyle1" alt="<%= $.t('taskaction.directcommand.'+availableCommands.directCommands[i]+'.value')%>">
                         <a href="javascript:void(0);" title="<%= availableCommands.directCommands[i]%>" value="<%= availableCommands.directCommands[i]%>" data-action="route"><%= availableCommands.directCommands[i]%></a>
                     </li>
                <%}else if(availableCommands.directCommands[i].equals("myAction2")){%>
                     <li class="myStyle2" alt="<%= $.t('taskaction.directcommand.'+availableCommands.directCommands[i]+'.value')%>">
                         <a href="javascript:void(0);" title="<%= availableCommands.directCommands[i]%>" value="<%= availableCommands.directCommands[i]%>" data-action="route"><%= availableCommands.directCommands[i]%></a>
                     </li>
                <%}%>
            <%}%>
            <%}%>
```

## Menu déroulant de l’action de tâche Détails de la tâche {#task-details-task-action-popup}

1. Copiez `/libs/ws/js/runtime/templates/taskdetails.html` vers `/apps/ws/js/runtime/templates/taskdetails.html`.

1. If the name of the CSS style is same as the route action name coming from the server, modify the following code in `/apps/ws/js/runtime/templates/taskdetails.html`:

   ```
   <%for (var i = 0; i < availableCommands.directCommands.length; i++) {%>
                           <li class="routeAction">
                               <a href="javascript:void(0);" title="<%= availableCommands.directCommands[i]%>" value="<%= availableCommands.directCommands[i]%>" data-action="route"><%= availableCommands.directCommands[i]%></a>
                           </li>
                       <%}%>
   
   To
   
   <%for (var i = 0; i < availableCommands.directCommands.length; i++) {%>
                           <li class="routeAction">
                               <a href="javascript:void(0);" title="<%= availableCommands.directCommands[i]%>" value="<%= availableCommands.directCommands[i]%>" data-action="route">
                               <i class="<%= availableCommands.directCommands[i]%>" value="<%= availableCommands.directCommands[i]%>" data-action="route"/>
                               </a>
                           </li>
                       <%}%>
   ```

1. If the name of the CSS style is different from the route action name coming from the server, modify the following code in `/apps/ws/js/runtime/templates/taskdetails.html`. Il ajoute une pile des conditions de servlet `if-else` pour mapper le style avec le nom de l’action d’itinéraire.

   ```
   <%for (var i = 0; i < availableCommands.directCommands.length; i++) {%>
                           <li class="routeAction">
                               <a href="javascript:void(0);" title="<%= availableCommands.directCommands[i]%>" value="<%= availableCommands.directCommands[i]%>" data-action="route"><%= availableCommands.directCommands[i]%></a>
                           </li>
                       <%}%>
   
   To
   
   <%for (var i = 0; i < availableCommands.directCommands.length; i++) {%>
                   <%if(availableCommands.directCommands[i].equals("myAction1")){%>
                       <li class="routeAction">
                               <a href="javascript:void(0);" title="<%= availableCommands.directCommands[i]%>" value="<%= availableCommands.directCommands[i]%>" data-action="route">
                               <i class="myStyle1" value="<%= availableCommands.directCommands[i]%>" data-action="route"/>
                               </a>
                           </li>
                   <%}else if(availableCommands.directCommands[i].equals("myAction2")){%>
                       <li class="routeAction">
                               <a href="javascript:void(0);" title="<%= availableCommands.directCommands[i]%>" value="<%= availableCommands.directCommands[i]%>" data-action="route">
                               <i class="myStyle2" value="<%= availableCommands.directCommands[i]%>" data-action="route"/>
                               </a>
                           </li>
                   <%}%>
               <%}%>
   ```

1. Open `/apps/ws/js/registry.js` for editing and look for the following text :
   `"text!/lc/libs/ws/js/runtime/templates/taskdetails.html"`

1. Remplacez le texte par le texte suivant :
   `"text!/lc/apps/ws/js/runtime/templates/taskdetails.html"`
