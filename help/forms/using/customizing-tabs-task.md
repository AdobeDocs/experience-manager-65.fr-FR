---
title: Personnalisation des onglets d’une tâche
description: Comment personnaliser les noms des onglets de vos tâches dans l’espace de travail AEM Forms LiveCycle.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
exl-id: 8412cfec-bcab-40b7-9e5b-fcc211d43c0b
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: tm+mt
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
