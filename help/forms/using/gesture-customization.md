---
title: Personnalisation de mouvement
description: Découvrez comment personnaliser les gestes dans l’application AEM Forms. Vous pouvez personnaliser les mouvements de l’application AEM Forms pour interagir différemment avec l’application.
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-app
exl-id: 6debb1a7-7889-4fdd-87c7-ecb87cc0b1f5
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
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '328'
ht-degree: 95%
---
# Personnalisation de mouvement {#gesture-customization}

>[!NOTE]
>
>L’application AEM Forms est actuellement obsolète. Pour toute question ou aide, contactez [](mailto:aemformsapp-android@adobe.com).

Vous pouvez personnaliser les mouvements de l’application AEM Forms pour interagir différemment avec l’application. Par exemple, vous pouvez ajouter de nouveaux mouvements pour ouvrir/fermer une tâche ou un point de départ.

## Pour personnaliser les gestes dans l’application AEM Forms {#to-customize-gestures-in-aem-forms-app}

Dans l’application AEM Forms, un glissement vers la gauche permet d’ouvrir une nouvelle tâche ou un nouveau point de départ, tandis qu’un glissement vers la droite n’active aucune commande. L’exemple suivant indique la procédure d’ouverture d’une nouvelle tâche ou d’un nouveau point de départ via un glissement vers la droite dans l’application AEM Forms.

1. Ouvrez votre projet.

   * Pour iOS, ouvrez `Capture.xcodeproj` dans Xcode.
   * Pour Android, ouvrez le projet Android dans Eclipse.
   * Pour Windows, ouvrez `MWSWindows.sln` dans Visual Studio.

1. Accédez au dossier Vues et ouvrez le fichier `task.js` pour le modifier.

   * Dans Xcode, accédez au dossier **Capture > www > wsmobile > js > runtime > views**.
   * Dans Eclipse, accédez au dossier **assets > www > wsmobile > js > runtime > views**.
   * Dans Visual Studio, accédez au dossier **MWSWindows > www > wsmobile > js > runtime > views**.

   >[!NOTE]
   >
   >Le fichier task.js contient la vue Backbone associée à chaque tâche ou point de départ, tel que répertorié dans les listes de tâches ou de points de départ.

1. Dans le fichier `task.js`, recherchez la propriété événements de la vue.

   La propriété événements est un mappage dont chaque entrée est au format :

   `"EventName Selector": "Function"`

   Lorsque vous déclenchez un événement Javascript appelé `EventName` sur un élément HTML spécifié par `Selector`, la fonction `Function` est appelée.

1. Recherche

   * &quot;select .taskContentArea&quot; : &quot;onTaskClick&quot;,

     &quot;select .taskContentArea&quot; : &quot;onTaskClick&quot;,

     &quot;select .task-content&quot; : &quot;onTaskClick&quot;,

     &quot;select .last_empty_div&quot; : &quot;onTaskClick&quot;,

   et remplacer par

   * &quot;swipe .taskContentArea&quot; : &quot;onTaskClick&quot;,

     &quot;swipe .taskOpenArea&quot; : &quot;onTaskClick&quot;,

     &quot;swipe .task-content&quot; : &quot;onTaskClick&quot;,

     &quot;swipe .last_empty_div&quot; : &quot;onTaskClick&quot;,

1. Enregistrez et fermez le fichier `task.js`.
1. Créez et exécutez l’application AEM Forms. Vous pouvez désormais ouvrir une tâche en faisant glisser votre doigt vers la gauche et la droite.

De même, vous pouvez apporter des modifications dans les autres vues pour différentes combinaisons de mouvements, d’éléments HTML et de fonctions.
