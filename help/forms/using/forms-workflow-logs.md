---
title: 'Connexion au AEM Forms '
seo-title: 'Connexion au AEM Forms '
description: Utilisez les journaux pour déboguer les problèmes de flux de travaux AEM Forms.
seo-description: Utilisez les journaux pour déboguer les problèmes de flux de travaux AEM Forms.
uuid: 869d0271-c7e3-4b6d-8e63-893dc6af8b8a
contentOwner: anujkapo
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: publish
discoiquuid: 14bb521a-42ea-4fe2-90fb-202e7ddf917a
docset: aem65
translation-type: tm+mt
source-git-commit: 317fadfe48724270e59644d2ed9a90fbee95cf9f

---


# Connexion au AEM Forms{#logging-in-aem-forms-workflows}

Les étapes du processus des formulaires fournissent des journaux détaillés pour déboguer les problèmes liés au processus. Activez la journalisation du débogage pour le AEM Forms pour  les journaux.

By default, all logging information is available in the **error.log** file at the */crx-repository/logs/* directory.

Les journaux de débogage des  de formulaires incluent :

* Entrée de chaque étape du processus. Par exemple :\
   `[DEBUG] "Executing Invoke DDX Process step"`

* Quitter chaque étape du processus. Par exemple :\
   `[DEBUG] "Successfully finished Invoke DDX Process step"`

* Messages d’appel du service. Par exemple :\
   `[DEBUG] Invoking Adobe Sign Service for creating agreement`

* Messages de sortie du service. Par exemple :\
   `[DEBUG] Agreement created successfully with agreement id <agreement id>`

* Variables lues à partir du mappage de métadonnées. Par exemple :\
   `[DEBUG] Successfully retrieved variable <variable name> from workflow meta data map`

* Variables écrites dans le référentiel JCR. Par exemple :

   ```
      [DEBUG] Successfully written variable <variable name> into meta data node at <JCR path where meta data is being written>
   ```

* Messages d’exception avec trace de pile complète. Par exemple :\
   `[DEBUG] Exception in Adobe Sign Service <complete stack trace>`

* Paramètres de métadonnées d’étape dynamique. Par exemple :

   ```
   [DEBUG] Document of Record to be generated for adaptive form <path of adaptive form>
    [DEBUG] Locale to be used for Document of Record is <locale>
   ```

L’exemple suivant illustre les journaux de l’étape de  de signature :

```xml
[DEBUG] Executing sign document step.
[DEBUG] Using adobe sign configuration: <path of adobe sign configuration>
[DEBUG] Invoking Adobe Sign Service for creating agreement
[DEBUG] Agreement created successfully with agreement id <agreement id>
[DEBUG] Exception in Adobe Sign Service <complete stack trace>
[ERROR] Exception in Adobe Sign Service
[DEBUG] Successfully finished sign document step
```

Utilisez les journaux pour évaluer ce qui suit :

* Vous utilisez une configuration adobe sign correcte.
* Le service Adobe Sign se ferme après avoir créé un accord.
* L’étape Signer le  se termine par un message de réussite.

S’il existe une exception, vous pouvez  la trace de pile complète pour évaluer la cause de l’erreur.

## Activation de la journalisation du débogage pour les  AEM Forms {#enable-debug-logging-for-aem-forms-workflows}

Suivez les étapes ci-dessous pour activer la journalisation du débogage pour les  AEM Forms :

1. Accédez au gestionnaire de configuration de la console Web AEM à l’adresse :

   https://&#39;[server]:[port]&#39;/system/console/configMgr

1. Sélectionnez **[!UICONTROL Sling]** > Prise en charge **[!UICONTROL des]** journaux.
1. Appuyez sur **[!UICONTROL Ajouter nouveau journal.]**
1. Sélectionnez **[!UICONTROL Déboguer]** comme niveau **[!UICONTROL du]** journal.
1. Spécifiez l’emplacement du fichier journal. L’emplacement par défaut du fichier journal est : *logs\error.log*
1. Indiquez le nom du package **com.adobe.granite.workflow.core** dans la colonne **[!UICONTROL Logger]** .

   L’exécution de ces étapes permet de stocker les journaux de débogage du package **com.adobe.granite.workflow.core** . Appuyez sur **[!UICONTROL +]** et ajoutez les noms de package suivants au :

   * com.adobe.fd.workflow
   * com.adobe.fd.workspace

