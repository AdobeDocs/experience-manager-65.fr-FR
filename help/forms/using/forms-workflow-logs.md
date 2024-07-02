---
title: Journalisation des workflows AEM Forms
description: Découvrez comment déboguer les problèmes d’AEM Forms Workflow et activer la journalisation du débogage d’AEM Forms Workflow afin d’afficher les journaux.
contentOwner: anujkapo
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: publish
docset: aem65
exl-id: 601c8d95-0d1a-4945-a522-e85d3e9fc4ae
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
role: User, Developer
source-git-commit: 9f59606bb58b9e90f07bd22e89f3213afb54a697
workflow-type: ht
source-wordcount: '292'
ht-degree: 100%

---

# Journalisation des workflows AEM Forms{#logging-in-aem-forms-workflows}

Les étapes de Forms Workflow fournissent des journaux détaillés pour déboguer facilement les problèmes liés aux workflows. Activez la journalisation de débogage pour les workflows AEM Forms afin d’afficher les journaux.

Par défaut, toutes les informations relatives à la journalisation sont disponibles dans le fichier **error.log** du répertoire */crx-repository/logs/*.

Les journaux de débogage des workflows Forms incluent les éléments suivants :

* Entrée de chaque étape du workflow. Par exemple :\
  `[DEBUG] "Executing Invoke DDX Process step"`

* Sortie de chaque étape du workflow. Par exemple :\
  `[DEBUG] "Successfully finished Invoke DDX Process step"`

* Messages d’appel du service. Par exemple :\
  `[DEBUG] Invoking Adobe Sign Service for creating agreement`

* Messages de sortie du service. Par exemple :\
  `[DEBUG] Agreement created successfully with agreement id <agreement id>`

* Variables lues à partir du mappage de métadonnées. Par exemple :\
  `[DEBUG] Successfully retrieved variable <variable name> from workflow meta data map`

* Variables écrites dans le référentiel JCR. Par exemple :

  ```verilog
     [DEBUG] Successfully written variable <variable name> into meta data node at <JCR path where meta data is being written>
  ```

* Messages d’exception avec trace de pile complète. Par exemple :\
  `[DEBUG] Exception in Adobe Sign Service <complete stack trace>`

* Paramètres de métadonnées d’étape dynamique. Par exemple :

  ```verilog
  [DEBUG] Document of Record to be generated for adaptive form <path of adaptive form>
   [DEBUG] Locale to be used for Document of Record is <locale>
  ```

L’exemple suivant illustre les journaux de l’étape Signer le document :

```verilog
[DEBUG] Executing sign document step.
[DEBUG] Using adobe sign configuration: <path of adobe sign configuration>
[DEBUG] Invoking Adobe Sign Service for creating agreement
[DEBUG] Agreement created successfully with agreement id <agreement id>
[DEBUG] Exception in Adobe Sign Service <complete stack trace>
[ERROR] Exception in Adobe Sign Service
[DEBUG] Successfully finished sign document step
```

Utilisez les journaux pour évaluer les éléments suivants :

* Vous utilisez une configuration Adobe Sign appropriée.
* Le service Adobe Sign se ferme après la création d’un contrat.
* L’étape Signer le document se ferme avec un message de réussite.

S’il existe une exception, vous pouvez afficher la trace de la pile complète pour évaluer la cause de l’erreur.

## Activer la journalisation du débogage pour les workflows AEM Forms {#enable-debug-logging-for-aem-forms-workflows}

Procédez comme suit pour activer la journalisation du débogage pour les workflows AEM Forms :

1. Accédez à la page de configuration de la console web AEM à l’adresse:

   https://&#39;[server]:[port]&#39;/system/console/configMgr

1. Sélectionnez **[!UICONTROL Sling]** > **[!UICONTROL Prise en charge du journal]**.
1. Appuyez sur **[!UICONTROL Ajouter une nouvelle journalisation]**.
1. Sélectionnez **[!UICONTROL Débogage]** pour le **[!UICONTROL Niveau de journalisation]**.
1. Indiquez l’emplacement du fichier journal. L’emplacement par défaut du fichier journal est le suivant : *logs\error.log*.
1. Précisez le nom du package **com.adobe.granite.workflow.core** dans la colonne **[!UICONTROL Journalisation]**.

   L’exécution de ces étapes permet de stocker les journaux de débogage du package **com.adobe.granite.workflow.core**. Sélectionnez **[!UICONTROL +]** et ajoutez les noms de packages suivants à la liste :

   * com.adobe.fd.workflow
   * com.adobe.fd.workspace
