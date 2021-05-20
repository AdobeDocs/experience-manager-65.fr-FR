---
title: Connexion aux workflows AEM Forms
seo-title: Connexion aux workflows AEM Forms
description: Utilisez les journaux pour déboguer les problèmes de workflow AEM Forms.
seo-description: Utilisez les journaux pour déboguer les problèmes de workflow AEM Forms.
uuid: 869d0271-c7e3-4b6d-8e63-893dc6af8b8a
contentOwner: anujkapo
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: publish
discoiquuid: 14bb521a-42ea-4fe2-90fb-202e7ddf917a
docset: aem65
exl-id: 601c8d95-0d1a-4945-a522-e85d3e9fc4ae
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '292'
ht-degree: 8%

---

# Connexion aux workflows AEM Forms{#logging-in-aem-forms-workflows}

Les étapes du processus Forms fournissent des journaux détaillés pour déboguer facilement les problèmes liés au processus. Activez la journalisation de débogage pour les workflows AEM Forms afin d’afficher les journaux.

Par défaut, toutes les informations de journalisation sont disponibles dans le fichier **error.log** du répertoire */crx-repository/logs/*.

Les journaux de débogage des processus de formulaires incluent :

* Entrée de chaque étape du workflow. Par exemple :\
   `[DEBUG] "Executing Invoke DDX Process step"`

* Quitter chaque étape du workflow. Par exemple :\
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

L’exemple suivant illustre les journaux de l’étape Signer le document :

```verilog
[DEBUG] Executing sign document step.
[DEBUG] Using adobe sign configuration: <path of adobe sign configuration>
[DEBUG] Invoking Adobe Sign Service for creating agreement
[DEBUG] Agreement created successfully with agreement id <agreement id>
[DEBUG] Exception in Adobe Sign Service <complete stack trace>
[ERROR] Exception in Adobe Sign Service
[DEBUG] Successfully finished sign document step
```

Utilisez les journaux pour évaluer cela :

* Vous utilisez une configuration adobe sign correcte.
* Le service Adobe Sign quitte après la création d’un accord.
* L’étape Signer le document quitte avec un message de réussite.

S’il existe une exception, vous pouvez afficher la trace de la pile complète pour évaluer la cause de l’erreur.

## Activation de la journalisation de débogage pour les workflows AEM Forms {#enable-debug-logging-for-aem-forms-workflows}

Effectuez les étapes suivantes pour activer la journalisation de débogage pour les workflows AEM Forms :

1. Accédez à la page de configuration de la console web AEM à l’adresse:

   https://&#39;[server]:[port]&#39;/system/console/configMgr

1. Sélectionnez **[!UICONTROL Sling]** > **[!UICONTROL Prise en charge du journal]**.
1. Appuyez sur **[!UICONTROL Ajouter un nouvel enregistreur.]**
1. Sélectionnez **[!UICONTROL Debug]** comme **[!UICONTROL Niveau de journal]**.
1. Indiquez l’emplacement du fichier journal. L’emplacement par défaut du fichier journal est le suivant : *logs\error.log*
1. Indiquez le nom du module **com.adobe.granite.workflow.core** dans la colonne **[!UICONTROL Enregistreur]**.

   L’exécution de ces étapes permet de stocker les journaux de débogage pour le module **com.adobe.granite.workflow.core**. Appuyez sur **[!UICONTROL +]** et ajoutez les noms de modules suivants à la liste :

   * com.adobe.fd.workflow
   * com.adobe.fd.workspace
