---
title: Modification de la police de l’interface
seo-title: Modification de la police de l’interface
description: Procédure de modification des polices sur l’interface utilisateur de manière sélective.
seo-description: Procédure de modification des polices sur l’interface utilisateur de manière sélective.
uuid: 421fdd24-441a-4092-8c52-f3ed3d5d5671
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 9fcb80b4-cbc2-48a5-afd1-4f3bc50bc503
docset: aem65
translation-type: tm+mt
source-git-commit: 56c6cfd437ef185336e81373bd5f758205b96317

---


# Modification de la police de l’interface{#changing-the-font-on-the-interface}

Vous pouvez modifier la police affichée dans l’espace de travail AEM Forms. Les polices utilisées dans une section spécifique de l’interface utilisateur sont définies dans la section correspondante de la feuille de style. Vous pouvez modifier les polices sur l’interface utilisateur de manière sélective.

Follow the [Generic steps for AEM Forms workspace customization](../../forms/using/generic-steps-html-workspace-customization.md) and depending on your requirements, follow the steps for customizing CSS, HTML, or both.

1. Modifiez ou ajoutez la famille de police dans un style existant.
1. Modifiez ou ajoutez la famille de police en ligne pour l’élément HTML.
1. Ajoutez un style et utilisez-le pour l’élément HTML.

Par exemple, pour remplacer la police du texte de la barre de navigation supérieure par Courier New, procédez comme suit :

1. Connectez-vous à CRXDE Lite en accédant à `https://'[server]:[port]'/lc/crx/de/index.jsp`.
1. Utilisez l’une des méthodes suivantes :

   1. Pour modifier la famille de police dans un style existant, ajoutez la ligne suivante dans le fichier newStyle.css sous /apps/ws/css.

      ```css
      #topnav a {
         font-family: "Courier New";
      }
      ```

   1. To add the font-family inline for the HTML element, copy the `/libs/ws/js/runtime/templates/appnavigation.html` file to `/apps/ws/js/runtime/templates/appnavigation.html`.

      Mettez à jour le fichier apps/ws/js/runtime/templates/appnavigation.html comme suit :

      ```
      <li class="process"><a href="#" title="<%= $.t('index.header.topnav.startprocess.detail')%>" style="font-family:Courier New;" ><%= $.t('index.header.topnav.startprocess.name')%></a></li>
      <li class="todo"><a href="#/todo" title="<%= $.t('index.header.topnav.todo.detail')%>" style="font-family:Courier New;" ><%= $.t('index.header.topnav.todo.name')%></a></li>
      <li class="track"><a href="#/tracking" title="<%= $.t('index.header.topnav.tracking.detail')%>" style="font-family:Courier New;" ><%= $.t('index.header.topnav.tracking.name')%></a></li>
      <li class="preference"><a href="#/preferences" title="<%= $.t('index.header.topnav.preferences.detail')%>" style="font-family:Courier New;" ><%= $.t('index.header.topnav.preferences.name')%></a></li>
      ```

      Open the /apps/ws/js/registry.js file for editing and replace `text!/lc/libs/ws/js/runtime/templates/appnavigation.html` with `text!/lc/apps/ws/js/runtime/templates/appnavigation.html`.

   1. Pour ajouter un style qui définit la famille de police, ajoutez la ligne suivante dans le fichier newStyle.css sous /apps/ws/css.

      ```css
      .myNewFontStyle a {
         font-family: "Courier New";
      }
      ```

      Pour ajouter la famille de police en ligne pour l’élément HTML, ajoutez le code suivant dans le fichier appnavigation.html sous /apps/ws/js/runtime/templates.

      ```css
      <div id="topnav" class="myNewFontStyle">
          <ul>
              <li class="process"><a href="#" title="<%= $.t('index.header.topnav.startprocess.detail')%>" ><%= $.t('index.header.topnav.startprocess.name')%></a></li>
              <li class="todo"><a href="#/todo" title="<%= $.t('index.header.topnav.todo.detail')%>"><%= $.t('index.header.topnav.todo.name')%></a></li>
              <li class="track"><a href="#/tracking" title="<%= $.t('index.header.topnav.tracking.detail')%>" ><%= $.t('index.header.topnav.tracking.name')%></a></li>
              <li class="preference"><a href="#/preferences" title="<%= $.t('index.header.topnav.preferences.detail')%>" ><%= $.t('index.header.topnav.preferences.name')%></a></li>
          </ul>
      </div>
      ```

1. Relancez l’espace de travail et effacez le cache du navigateur pour que les modifications soient visibles.

![change_font_before](assets/change_font_before.png)

Barre de navigation supérieure avant la personnalisation de la police

![change_font_after](assets/change_font_after.png)

Barre de navigation supérieure après la personnalisation de la police du premier onglet
