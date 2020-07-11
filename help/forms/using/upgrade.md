---
title: Mise à niveau vers AEM 6.5 Forms
seo-title: Mise à niveau vers AEM 6.5 Forms
description: Vous pouvez effectuer une mise à niveau directe à partir de AEM 6.3 Forms et AEM 6.4 Forms vers AEM 6.5 Forms.
seo-description: Vous pouvez effectuer une mise à niveau directe à partir de AEM 6.3 Forms et AEM 6.4 Forms vers AEM 6.5 Forms.
uuid: 7a38cd72-2d01-4af7-b6a3-00dc34c4f02b
content-type: reference
topic-tags: installing
geptopics: SG_AEMFORMS/categories/jee
discoiquuid: f89921ef-c638-4a07-88d5-3dd8614c5166
docset: aem65
translation-type: tm+mt
source-git-commit: 1dfc8fa91d3e5ae8ca49cf1f3cb739b59feb18cf
workflow-type: tm+mt
source-wordcount: '232'
ht-degree: 100%

---


# Mise à niveau vers AEM 6.5 Forms{#upgrade-to-aem-forms}

AEM 6.5 Forms comporte plusieurs nouvelles fonctionnalités et améliorations qui optimisent la création, la gestion et la convivialité des formulaires et correspondances. Pour en savoir plus sur toutes les nouvelles fonctionnalités et améliorations d’AEM 6.5 Forms, voir [Résumé des nouvelles fonctionnalités](../../forms/using/whats-new.md).

Vous pouvez mettre à niveau votre installation LiveCycle ou AEM Forms pour obtenir les nouvelles fonctionnalités et améliorations proposées dans AEM 6.5 Forms tout en conservant intactes les données, processus et actifs existants. Lors de la mise à niveau, les métadonnées et l’état des processus sont également conservés. Vous pouvez choisir un chemin de mise à niveau pour commencer la mise à niveau.

Le diagramme suivant affiche les chemins de mise à niveau disponibles pour AEM Forms on OSGi :

![](do-not-localize/osgi-upgrade-path.png)

Vous pouvez effectuer une mise à niveau directe depuis :

* AEM 6.3 Forms on OSGi
* AEM 6.4 Forms on OSGi

Vous pouvez également effectuer une mise à niveau en plusieurs étapes depuis

* AEM 6.0 Forms on OSGi
* AEM 6.1 Forms on OSGi
* AEM 6.2 Forms on OSGi

Le diagramme suivant affiche les chemins de mise à niveau disponibles pour AEM Forms on JEE :

![](do-not-localize/jee-upgrade-6-5.png)

Vous pouvez effectuer une mise à niveau directe depuis :

* AEM 6.3 Forms on JEE
* AEM 6.4 Forms on JEE

Vous pouvez également effectuer une mise à niveau en plusieurs étapes depuis

* LiveCycle ES2
* LiveCycle ES3
* LiveCycle ES4 SP1
* AEM 6.0 Forms on JEE
* AEM 6.1 Forms on JEE
* AEM 6.2 Forms on JEE

<!--
[Work in Progress]

Migration involves moving only assets (PDF, XDP, images, adaptive forms, correspondence management assets) from one server to another - processes (LCA), settings, configurations, and a few other pieces of metadata are not migrated. Perform the following steps to migrate to AEM 6.3 Forms:

1. Set up a fresh environment of [AEM 6.3 Forms](https://adobe.com/go/learn_aemforms_documentation_63).
1. Move XDP or other compatible assets to the freshly set instance. For detailed instructions, see [Importing and exporting assets to AEM Forms](../../forms/using/import-export-forms-templates.md). [
   ](../../forms/using/import-export-forms-templates.md)
1. Build the required services, if any.

   For example, if you are using AEM Forms on JEE Document Services, changes are required in the code to use document services available in AEM Forms on OSGi.

1. Perform post-installation activities:

    * **Run Migration Utility**

      The migration utility makes the adaptive forms and correspondence management assets of earlier versions compatible with AEM 6.3 forms. You can download the utility from AEM Software Distribution. For step-by-step information to configure and use the migration utility, see [migration utility](../../forms/using/migration-utility.md) documentation.

    * **Reconfigure Adobe Sign**

      If you had Adobe Sign configured in the previous version of AEM Forms, then reconfigure Adobe Sign from AEM Cloud services. For more details, see [Integrate Adobe Sign with AEM Forms](../../forms/using/adobe-sign-integration-adaptive-forms.md).

      Moreover, AEM 6.3 Forms release has introduced many new Adobe Sign features. For step-by-step information to use Adobe Sign, see [Using Adobe Sign in an adaptive form](../../forms/using/working-with-adobe-sign.md).

    * **Reconfigure analytics and reports**

      In AEM 6.3 Forms, traffic variable for source and success event for impression are not available. So, when you upgrade to AEM 6.3 Forms, AEM Forms stops sending data to Adobe Analytics server and analytics reports for adaptive forms are not available. Moreover, AEM 6.3 Forms introduces traffic variable for the version of form analytics and success event for the amount of time spent on a field. So, reconfigure analytics and reports for your AEM Forms environment. For detailed steps, see [Configuring analytics and reports](../../forms/using/configure-analytics-forms-documents.md).

      Methods to calculate average fill time for forms and average read time for have changed. So, when you upgrade to AEM 6.3 forms, older data (data from previous AEM Forms release) for these metrics is available only in Adobe Analytics. It is not visible in AEM Forms analytics reports. For these metrics, AEM Forms analytics reports display data which is captured after performing the upgrade.
      
      -->
