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
exl-id: 6debb1a7-7889-4fdd-87c7-ecb87cc0b1f5
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '306'
ht-degree: 44%

---

# Personnalisation de mouvement {#gesture-customization}

Vous pouvez personnaliser les mouvements de l’application AEM Forms afin de fournir une méthode distincte d’interaction avec l’application. Par exemple, vous pouvez ajouter de nouveaux mouvements pour ouvrir/fermer une tâche ou un point de départ.

## Personnalisation des mouvements dans l’application AEM Forms {#to-customize-gestures-in-aem-forms-app}

Dans l’application AEM Forms, un glissement vers la gauche permet d’ouvrir une nouvelle tâche ou un nouveau point de départ, tandis qu’un glissement vers la droite n’active aucune commande. L’exemple suivant décrit les étapes à suivre pour ouvrir une nouvelle tâche ou un nouveau point de départ en effectuant un glissement vers la droite dans l’application AEM Forms.

1. Ouvrez votre projet.

   * Pour iOS, ouvrez `Capture.xcodeproj` dans Xcode.
   * Pour Android, ouvrez le projet Android dans Eclipse.
   * Pour Windows, ouvrez `MWSWindows.sln` dans Visual Studio.

1. Accédez au dossier views et ouvrez le fichier `task.js` en vue de le modifier.

   * Dans Xcode, accédez au dossier **Capture > www > wsmobile > js > runtime > views** .
   * Dans Eclipse, accédez au dossier **assets > www > wsmobile > js > runtime > views** .
   * Dans Visual Studio, accédez au dossier **MWSWindows > www > wsmobile > js > runtime > views** .

   >[!NOTE]
   >
   >Le fichier task.js contient la vue Backbone associée à chaque tâche ou point de départ, tel que répertorié dans les listes de tâches ou de points de départ.

1. Dans le fichier `task.js`, recherchez la propriété events de la vue.

   La propriété events est une map avec chaque entrée au format :

   `"EventName Selector": "Function"`

   Lorsque vous déclenchez un événement JavaScript nommé `EventName`sur un élément HTML spécifié par `Selector`, `Function`est appelé.

1. Rechercher

   * &quot;appuyez sur .taskContentArea&quot; : &quot;onTaskClick&quot;,

      &quot;appuyez sur .taskOpenArea&quot; : &quot;onTaskClick&quot;,

      &quot;appuyez sur .task-content&quot; : &quot;onTaskClick&quot;,

      &quot;appuyez sur .last_empty_div&quot; : &quot;onTaskClick&quot;,
   et remplacer par

   * &quot;swipe .taskContentArea&quot; : &quot;onTaskClick&quot;,

      &quot;swipe .taskOpenArea&quot; : &quot;onTaskClick&quot;,

      &quot;swipe .task-content&quot; : &quot;onTaskClick&quot;,

      &quot;swipe .last_empty_div&quot; : &quot;onTaskClick&quot;,


1. Enregistrez et fermez le fichier `task.js`.
1. Générez et exécutez l’application AEM Forms. Vous pouvez désormais ouvrir une tâche en faisant glisser votre doigt vers la gauche et la droite.

De même, vous pouvez apporter des modifications dans les autres vues pour différentes combinaisons de mouvements, d’éléments HTML et de fonctions.
