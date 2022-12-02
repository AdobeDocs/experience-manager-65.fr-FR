---
title: Personnalisation des onglets d’une tâche
seo-title: Customizing tabs for a task
description: Comment personnaliser les noms des onglets des tâches dans l’espace de travail LiveCycle AEM Forms.
seo-description: How-to customize the names of the tabs for your tasks, in LiveCycle AEM Forms workspace.
uuid: 77eabb63-f8ea-4ec0-8a41-b51c65cdecc0
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: ac0a281f-f589-4a70-9bc7-1a23e054b02f
exl-id: 8412cfec-bcab-40b7-9e5b-fcc211d43c0b
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: ht
source-wordcount: '101'
ht-degree: 100%

---

# Personnalisation des onglets d’une tâche {#customizing-tabs-for-a-task}

Vous pouvez personnaliser les noms des onglets pour le `Start Process`composant dans l’affichage `Start Process` Uber et le `Task Details` composant `ToDo` de l’affichage Uber.

1. Suivez la [Procédure générique de personnalisation de l’espace de travail AEM Forms](/help/forms/using/generic-steps-html-workspace-customization.md).
1. Modifiez la valeur de `tabname` dans le fichier `translation.json`.

   Par exemple, modifiez `/apps/ws/locales/en-US/translation.json`/ pour l’anglais de la façon suivante.

   * Pour des tâches lancées dans le processus de démarrage, utilisez le fragment de code ci-dessous dans le bloc `"startprocess" : {}`.

   ```json
   "tabname" : {
               "form" : "Application",
               "details" : "Overview",
               "attachments" : "Attachments",
               "notes" : "Helper Notes"
           }
   ```

   * Pour des tâches dans Tâches, utilisez le fragment de code suivant dans le bloc `"todo" : {}`.

   ```json
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
   >Ajoutez la paire clé-valeur correspondante pour toutes les langues prises en charge.
