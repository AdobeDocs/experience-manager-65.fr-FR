---
title: Personnalisation du thème
description: Découvrez comment personnaliser le thème de l’application AEM Forms. Vous pouvez personnaliser le code HTML et le fichier CSS pour personnaliser l’organisation et l’aspect de l’application AEM Forms.
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
exl-id: 9b8c5933-b783-48f9-b463-15a01e06ee98
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: e72c079d-d036-46d5-b43d-29b276a174c2
    internal-label: Authoring and publishing content
subfeature_v2:
  - id: a26f372d-6d7c-452b-81df-594dd4365ae1
    internal-label: Adaptive Forms
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 751e1826ed53df7522418e50a206f0fe622256a4
workflow-type: tm+mt
source-wordcount: '254'
ht-degree: 94%
---
# Personnalisation du thème {#theme-customization}

>[!NOTE]
>
>L’application AEM Forms est actuellement obsolète. Pour toute question ou aide, contactez [&#128279;](mailto:aemformsapp-android@adobe.com).

Vous pouvez personnaliser le code HTML et le fichier CSS pour personnaliser l’organisation et l’aspect de l’application AEM Forms. Vous pouvez, par exemple, modifier la couleur d’arrière-plan ainsi que la hauteur des tâches ou des Startpoints. L’exemple suivant fournit des instructions pour modifier :

* Afficher les instructions au lieu de la description
* nombre d’itinéraires affichés
* Couleur de dégradé d’arrière-plan

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
1. Ouvrez l’application AEM Forms.

   L’application AEM Forms affiche désormais des instructions au lieu d’une description.
