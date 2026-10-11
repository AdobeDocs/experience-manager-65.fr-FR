---
title: Afficher des informations dans le volet Résumé de la tâche
description: Dans l’espace de travail AEM Forms, un volet Résumé de la tâche peut être configuré pour résumer la tâche ou afficher toute autre page web.
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: forms-workspace
exl-id: 0b3087fe-a3fb-4eac-ad4b-c123526e8195
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
source-wordcount: '266'
ht-degree: 99%
---
# Afficher des informations dans le volet Résumé de la tâche {#displaying-information-in-the-task-summary-pane}

Lorsque vous ouvrez une tâche dans l’espace de travail AEM Forms, un volet Résumé de la tâche peut afficher un résumé de la tâche. Ces informations supplémentaires et pertinentes pour une tâche ajoutent de la valeur pour l’utilisateur final ou l’utilisatrice finale de l’espace de travail AEM Forms.

L’espace de travail AEM Forms permet d’afficher une page web de votre choix dans le volet Résumé de la tâche. Un processus peut être créé pour afficher un volet Résumé de la tâche en utilisant Workbench.

1. Créez un processus Affecter une tâche dans Workbench. Pour plus d’informations sur l’opération Affecter une tâche, voir la rubrique Référence de service dans l’[Aide de Workbench](https://help.adobe.com/fr_FR/AEMForms/6.1/WorkbenchHelp/).

   >[!NOTE]
   >
   >si une URL TaskSummary existe, la vue Résumé de la tâche s’ouvre par défaut au lieu de la vue Formulaire. Dans ce cas, même lorsqu’un utilisateur ou une utilisatrice active l’option « Ouvrir le formulaire en mode agrandi » dans Affecter une tâche, le formulaire ne s’ouvre pas en mode agrandi.

1. Configurez le champ URL du résumé de la tâche. Vous pouvez spécifier une valeur littérale, un modèle, une variable ou une expression XPath.
1. Vous trouverez ci-dessous un exemple d’affichage des informations sur la page Résumé de la tâche.

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
