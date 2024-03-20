---
title: Personnaliser le thème
description: Découvrez comment personnaliser le thème de l’application AEM Forms. Vous pouvez personnaliser le code de HTML et le fichier CSS pour donner à l’organisation un aspect spécifique.
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
exl-id: 9b8c5933-b783-48f9-b463-15a01e06ee98
solution: Experience Manager, Experience Manager Forms
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '238'
ht-degree: 78%

---

# Personnaliser le thème {#theme-customization}

Vous pouvez personnaliser le code HTML et le fichier CSS pour personnaliser l’organisation et l’aspect de l’application AEM Forms. Vous pouvez, par exemple, modifier la couleur du fond d’écran ainsi que la hauteur des tâches ou des points de départ. L’exemple suivant fournit des instructions de modification :

* Afficher les instructions au lieu de la description
* nombre d’itinéraires d’affichage
* dégradé de fond

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

   L’application AEM Forms affiche désormais des instructions au lieu d’une description.
