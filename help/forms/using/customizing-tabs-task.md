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
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '121'
ht-degree: 51%

---


# Personnalisation des onglets d’une tâche {#customizing-tabs-for-a-task}

Vous pouvez personnaliser les noms de tabulation pour le composant `Start Process` dans la vue Uber `Start Process` et le composant `Task Details` dans la vue Uber `ToDo`.

1. Suivez la [Procédure générique de personnalisation de l’espace de travail AEM Forms](/help/forms/using/generic-steps-html-workspace-customization.md).
1. Modifiez la valeur de `tabname`dans le fichier `translation.json`.

   Par exemple, remplacez `/apps/ws/locales/en-US/translation.json` par ce qui suit pour l’anglais.

   * Pour les tâches lancées dans le processus de début, utilisez le fragment de code suivant du bloc `"startprocess" : {}`.

   ```json
   "tabname" : {
               "form" : "Application",
               "details" : "Overview",
               "attachments" : "Attachments",
               "notes" : "Helper Notes"
           }
   ```

   * Pour les tâches dans Tâches, utilisez le fragment de code suivant du bloc `"todo" : {}`.

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
   >ajoutez la paire clé-valeur correspondante pour toutes les langues prises en charge.
