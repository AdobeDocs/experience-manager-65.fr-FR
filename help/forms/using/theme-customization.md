---
title: Personnalisation du thème
seo-title: Theme Customization
description: Comment personnaliser le thème de votre application AEM Forms.
seo-description: How to customize the theme of your AEM Forms app.
uuid: 36632e67-1cc6-416d-ae80-d84bbabab4bd
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
discoiquuid: c72f608e-052a-4bf9-b7bc-ddf57483af35
exl-id: 9b8c5933-b783-48f9-b463-15a01e06ee98
source-git-commit: 6bc228866aca785ec768daefb73970fc24568ef0
workflow-type: ht
source-wordcount: '223'
ht-degree: 100%

---

# Personnalisation du thème {#theme-customization}

Vous pouvez personnaliser le code HTML et le fichier CSS pour personnaliser l’organisation et l’aspect de l’application AEM Forms. Vous pouvez, par exemple, modifier la couleur du fond d’écran ainsi que la hauteur des tâches ou des points de départ. L’exemple suivant donne des instructions pour modifier les paramètres suivants :

* Afficher les instructions au lieu de la description
* nombre d’itinéraires d’affichage
* dégradé de couleur d’arrière-plan

## Étapes {#steps}

1. Ouvrez votre projet.

   * Pour iOS, ouvrez `Capture.xcodeproj` dans Xcode.
   * Pour Android, ouvrez le projet Android dans Eclipse.
   * Pour Windows, ouvrez `MWSWindows.sln` dans Visual Studio.

1. Naviguez jusqu’au dossier des modèles.

   * Dans Xcode, accédez au dossier **Capture > www > wsmobile > js > runtime > templates**.
   * Dans Eclipse, accédez au dossier **assets > www > wsmobile > js > runtime > templates**.
   * Dans Visual Studio, accédez au dossier **MWSWindows > www > wsmobile > js > runtime > templates**.

1. Ouvrez le fichier `template.html` pour le modifier.
1. Recherchez la chaîne suivante :

   ```jsp
   <%if ( (task.description !== "") && (task.description !== null) && (typeof task.description !== null) && (typeof task.description !== 'undefined') ) {%>
                  <div class="description_details">
                    <%= task.description %>
                  </div>
                 <%} else
   ```

   Remplacez-la par `<%`.

1. Rercherchez le code suivant dans le fichier `template.html` :

   ```jsp
   <ul id="task_menu_list">
                                   <li class="approve" title="<%= task.availableCommands.directCommands[0]%>" data-routename="<%= task.availableCommands.directCommands[0]%>">
                                       <%= task.availableCommands.directCommands[0]%>
                                   </li>
                                   <li class="reject last" title="<%= task.availableCommands.directCommands[1]%>" data-routename="<%= task.availableCommands.directCommands[1]%>">
                                       <%= task.availableCommands.directCommands[1]%>
                                   </li>
   ```

1. Mettez la ligne suivante en commentaire et enregistrez le fichier.

   ```jsp
   task.availableCommands.directCommands[1]%>">
   <%= task.availableCommands.directCommands[1]%>
   </li>
   ```

1. Accédez au dossier css.

   * Dans Xcode, accédez à **Capture > www > wsmobile > css**.
   * Dans Eclipse, accédez à **assets > www > wsmobile > css**.
   * Dans Visual Studio, accédez à **MWSWindows > www > wsmobile > css**.

1. Ouvrez le fichier `_style.css` pour le modifier.
1. Pour l’image d’arrière-plan, remplacez `#323232` par `#fff`.
1. Enregistrez les modifications apportées, puis fermez le fichier `_style.css`.
1. Ouvrez l’application AEM Forms.

   L’application AEM Forms affiche maintenant les instructions à la place de la description.
