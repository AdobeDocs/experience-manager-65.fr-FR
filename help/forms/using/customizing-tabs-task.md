---
title: Personnalisation des onglets d’une tâche
seo-title: Personnalisation des onglets d’une tâche
description: Comment personnaliser les noms des onglets des tâches dans l’espace de travail LiveCycle AEM Forms.
seo-description: Comment personnaliser les noms des onglets des tâches dans l’espace de travail LiveCycle AEM Forms.
uuid: 77eabb63-f8ea-4ec0-8a41-b51c65cdecc0
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: ac0a281f-f589-4a70-9bc7-1a23e054b02f
translation-type: tm+mt
source-git-commit: 56c6cfd437ef185336e81373bd5f758205b96317

---


# Personnalisation des onglets d’une tâche {#customizing-tabs-for-a-task}

Vous pouvez personnaliser les noms d’onglets pour le `Start Process` composant dans le  `Start Process` Uber et le `Task Details` dans le  `ToDo` Uber.

1. Suivez la [Procédure générique de personnalisation de l’espace de travail AEM Forms](/help/forms/using/generic-steps-html-workspace-customization.md).
1. Change the value of `tabname`in the `translation.json` file.

   For example, change `/apps/ws/locales/en-US/translation.json` for English to the following.

   * For tasks initiated in the start process, use the following snippet from the `"startprocess" : {}` block.

   ```
   "tabname" : {
               "form" : "Application",
               "details" : "Overview",
               "attachments" : "Attachments",
               "notes" : "Helper Notes"
           }
   ```

   * For tasks in To-do, use the following snippet from the `"todo" : {}` block.

   ```
   "tabname" : {
               "summary" : "Bird's-eye view",
               "history" : "Past",
               "form" : "Form",
               "details" : "Overview",
               "attachments" : "Attachments",
               "notes" : "Notes"
   }
   ```

   >[!NOTE]
   >
   >ajoutez la paire clé-valeur correspondante pour toutes les langues prises en charge.
