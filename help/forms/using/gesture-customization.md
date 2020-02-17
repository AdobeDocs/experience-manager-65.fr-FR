---
title: Personnalisation de mouvement
seo-title: Personnalisation de mouvement
description: Personnaliser les mouvements sur votre application AEM Forms
seo-description: Personnaliser les mouvements sur votre application AEM Forms
uuid: 117e0e21-66bd-42f1-879c-6c1443991974
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
discoiquuid: 747d13d3-e7cc-4aa1-bcc8-4b57157e71ed
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Personnalisation de mouvement {#gesture-customization}

Vous pouvez personnaliser les mouvements de l’application AEM Forms pour fournir une méthode distincte d’interaction avec l’application. Par exemple, vous pouvez ajouter de nouveaux mouvements pour ouvrir/fermer une tâche ou un point de départ.

## Personnalisation des mouvements dans l’application AEM Forms {#to-customize-gestures-in-aem-forms-app}

Dans l’application AEM Forms, un glissement vers la gauche permet d’ouvrir une nouvelle tâche ou un nouveau point de départ, tandis qu’un glissement vers la droite n’active aucune commande. L’exemple suivant décrit la procédure à suivre pour ouvrir une nouvelle tâche ou un nouveau point de départ lors des mouvements de glissement vers la droite dans l’application AEM Forms.

1. Ouvrez votre projet.

   * For iOS, open `Capture.xcodeproj` in Xcode
   * Pour Android, ouvrez le projet Android dans Eclipse.
   * For Windows, open `MWSWindows.sln` in Visual Studio.

1. Navigate to the views folder and open the `task.js` file for editing.

   * In Xcode, navigate to the **Capture > www > wsmobile > js > runtime > views** folder.
   * In Eclipse, navigate to the **assets > www > wsmobile > js > runtime > views** folder.
   * In Visual Studio, navigate to the **MWSWindows > www > wsmobile > js > runtime > views** folder.
   >[!NOTE]
   >
   >Le fichier task.js contient la vue Backbone associée à chaque tâche ou point de départ, tel que répertorié dans les listes de tâches ou de points de départ.

1. In the `task.js` file, search for the events property of the view.

   La propriété events est un mappage avec chaque entrée au format :

   `"EventName Selector": "Function"`

   When you trigger a Javascript event named `EventName`on an HTML element specified by `Selector`, the `Function`is called.

1. Rechercher

   * &quot;tap .taskContentArea&quot; : &quot;onTaskClick&quot;,

      &quot;tap .taskOpenArea&quot; : &quot;onTaskClick&quot;,

      &quot;tap .task-content&quot; : &quot;onTaskClick&quot;,

      &quot;tap.last_empty_div&quot; : &quot;onTaskClick&quot;,
   et remplacer par

   * &quot;swipe.taskContentArea&quot; : &quot;onTaskClick&quot;,

      &quot;swipe .taskOpenArea&quot; : &quot;onTaskClick&quot;,

      &quot;swipe .task-content&quot; : &quot;onTaskClick&quot;,

      &quot;swipe.last_empty_div&quot; : &quot;onTaskClick&quot;,


1. Save and close the `task.js` file.
1. Générez et exécutez l’application AEM Forms. Vous pouvez désormais ouvrir une tâche en faisant glisser votre doigt vers la gauche et la droite.

De même, vous pouvez apporter des modifications dans les autres vues pour différentes combinaisons de mouvements, d’éléments HTML et de fonctions.

**[Contacter le support technique](https://www.adobe.com/account/sign-in.supportportal.html)**
