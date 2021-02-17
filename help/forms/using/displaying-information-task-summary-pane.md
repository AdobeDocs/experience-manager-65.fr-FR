---
title: Affichage d’informations dans le volet Résumé de la tâche
seo-title: Affichage d’informations dans le volet Résumé de la tâche
description: Dans l’espace de travail AEM Forms, un panneau de résumé de la tâche peut être configuré afin d’afficher le récapitulatif de la tâche ou d’afficher toute autre page Web.
seo-description: Dans l’espace de travail AEM Forms, un panneau de résumé de la tâche peut être configuré afin d’afficher le récapitulatif de la tâche ou d’afficher toute autre page Web.
uuid: 2fcc3d9f-0ec2-4250-8dc1-9746fd72ea60
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
discoiquuid: 90d0f584-b598-4b21-85d7-31da5f13d404
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '305'
ht-degree: 68%

---


# Affichage d’informations dans le volet Résumé de la tâche {#displaying-information-in-the-task-summary-pane}

Lorsque vous ouvrez une tâche dans l’espace de travail AEM Forms, le volet Résumé de la tâche peut afficher un résumé de la tâche. Ces informations supplémentaires et pertinentes à propos d’une tâche ajoutent de la valeur pour l’utilisateur final de l’espace de travail AEM Forms.

L’espace de travail AEM Forms vous permet d’afficher une page Web de votre choix dans le volet Résumé de la Tâche. Un processus peut être créé pour afficher un volet Résumé de la tâche en utilisant Workbench.

1. Créez un processus Assign Task (Affecter une tâche) dans Workbench. Pour plus d’informations sur l’opération Assign Task, voir la rubrique Référence de service dans [Aide de Workbench](https://help.adobe.com/en_US/AEMForms/6.1/WorkbenchHelp/).

   >[!NOTE]
   >
   >si une URL TaskSummary existe, la vue Résumé de la tâche s’ouvre par défaut au lieu de la vue Formulaire. Dans ce cas, même lorsqu’un utilisateur active l’option Open the form in maximized mode (Ouvrir le formulaire en mode agrandi) dans Assign Task, le formulaire ne s’ouvre pas en mode agrandi.

1. Configurez le champ URL du résumé de la tâche. Vous pouvez spécifier une valeur littérale, un contrôleur, une variable ou une expression XPath.
1. Vous trouverez un exemple d’affichage des informations sur la page du résumé de la tâche ci-dessous.

   * Connectez-vous à l’environnement CRXDE Lite à `https://'[server]:[port]'/lc/crx/de`.
   * `Create a node`**SampleSummary** ` under `/` with type `content:`. In the properties of this node, add `unstructuredsling:` of type String and value ``. In the Access Control List of this node, add an entry for `resourceTypeSampleSummaryPERM_WORKSPACE_` allowing `USERjcr:read` privileges.`
   * `Create a folder`**** SampleSummaryunder  `/apps`. Dans l&#39;Contrôle d&#39;accès Liste de `/apps/SampleSummary`, ajoutez une entrée pour `PERM_WORKSPACE_USER` autorisant `jcr:readprivileges`.
   * `Create a file `html.esp` at `/apps/`. For example, add the following lines in `SampleSummaryhtml.esp`.`

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

   * Définissez la valeur de l’URL de résumé de la tâche sur `/lc/content/SampleSummary.html` dans l’étape Attribuer une Tâche.
   * Lorsque la tâche associée à cette étape Assign Tâche est ouverte dans l’espace de travail AEM Forms, le `html.esp` à `/apps/SampleSummary` est rendu dans le volet de résumé de la tâche.
