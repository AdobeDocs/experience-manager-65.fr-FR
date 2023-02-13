---
title: Afficher des informations dans le volet Résumé de la tâche
seo-title: Displaying information in the Task Summary pane
description: Dans l’espace de travail AEM Forms, un panneau de résumé de la tâche peut être configuré afin d’afficher le récapitulatif de la tâche ou d’afficher toute autre page Web.
seo-description: In AEM Forms workspace, a Task Summary pane can be configured to summarize the task or display any other web page.
uuid: 2fcc3d9f-0ec2-4250-8dc1-9746fd72ea60
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 90d0f584-b598-4b21-85d7-31da5f13d404
exl-id: 0b3087fe-a3fb-4eac-ad4b-c123526e8195
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: ht
source-wordcount: '277'
ht-degree: 100%

---

# Afficher des informations dans le volet Résumé de la tâche {#displaying-information-in-the-task-summary-pane}

Lorsque vous ouvrez une tâche dans l’espace de travail AEM Forms, le volet Résumé de la tâche peut afficher un résumé de la tâche. Ces informations supplémentaires et pertinentes à propos d’une tâche ajoutent de la valeur pour l’utilisateur final de l’espace de travail AEM Forms.

L’espace de travail AEM Forms vous permet d’afficher une page web de votre choix dans le volet Résumé de la tâche. Un processus peut être créé pour afficher un volet Résumé de la tâche en utilisant Workbench.

1. Créez un processus Assign Task (Affecter une tâche) dans Workbench. Pour plus d’informations sur l’opération Assign Task, voir la rubrique Référence de service dans [Aide de Workbench](https://help.adobe.com/en_US/AEMForms/6.1/WorkbenchHelp/).

   >[!NOTE]
   >
   >si une URL TaskSummary existe, la vue Résumé de la tâche s’ouvre par défaut au lieu de la vue Formulaire. Dans ce cas, même lorsqu’un utilisateur active l’option Open the form in maximized mode (Ouvrir le formulaire en mode agrandi) dans Assign Task, le formulaire ne s’ouvre pas en mode agrandi.

1. Configurez le champ URL du résumé de la tâche. Vous pouvez spécifier une valeur littérale, un contrôleur, une variable ou une expression XPath.
1. Vous trouverez un exemple d’affichage des informations sur la page du résumé de la tâche ci-dessous.

   * Connectez-vous à l’environnement CRXDE Lite à l’adresse `https://'[server]:[port]'/lc/crx/de`.
   * `Create a node`**SampleSummary** ` under `/content` with type `nt:unstructured`. In the properties of this node, add `sling:resourceType` of type String and value `SampleSummary`. In the Access Control List of this node, add an entry for `PERM_WORKSPACE_USER` allowing `jcr:read` privileges.`
   * `Create a folder`**SampleSummary** sous `/apps`. Dans la liste de contrôle d’accès de `/apps/SampleSummary`, ajoutez une entrée pour `PERM_WORKSPACE_USER` autorisant `jcr:readprivileges`.
   * `Create a file `html.esp` at `/apps/SampleSummary`. For example, add the following lines in `html.esp`.`

   ```html
   <html>
       <body>
           <h1>Sample Summary</h1>
           <br/>
           <p>Hello Sir!
               <br/>
               This is sample summary page for this task.
           </p>
       </body>
   </html>
   ```

   * Définissez la valeur de l’URL du résumé de la tâche comme `/lc/content/SampleSummary.html` à l’étape d’affectation des tâches.
   * Lorsque la tâche associée à cette étape est ouverte dans l’espace de travail AEM Forms, le `html.esp` dans `/apps/SampleSummary` est rendu dans le volet de résumé de la tâche.
