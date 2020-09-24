---
title: Package de compatibilité
seo-title: Package de compatibilité
description: L’installation du package de compatibilité sur AEM Forms 6.5 vous permet d’utiliser les actifs Correspondence Management des versions AEM Forms 6.4 et antérieures et les modèles et pages de formulaires adaptatifs obsolètes.
seo-description: L’installation du package de compatibilité sur AEM Forms 6.4 vous permet d’utiliser les actifs de Correspondence Management d’AEM Forms 6.4 et les modèles et pages de formulaires adaptatifs obsolètes
uuid: b49633d6-2cb3-422c-a314-25f3b8a37b7f
contentOwner: gtalwar
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: correspondence-management, installing
geptopics: SG_AEMFORMS/categories/jee
discoiquuid: 73e8ccc6-f857-493e-b6e3-878f93e2a356
docset: aem65
translation-type: tm+mt
source-git-commit: a929252a13f66da8ac3e52aea0655b12bdd1425f
workflow-type: tm+mt
source-wordcount: '343'
ht-degree: 59%

---


# Package de compatibilité{#compatibility-package}

## Présentation {#overview}

Interactive communication is the default and recommended approach to create customer communications in AEM Forms 6.5. To continue using letters in AEM Forms 6.5, you need to install the latest [AEMFD Compatibility package](https://helpx.adobe.com/fr/aem-forms/kb/aem-forms-releases.html).

The AEMFD Compatibility package also allows you to [use the following assets from AEM Forms 6.4, 6.3 and 6.2 on AEM Forms 6.5:](../../forms/using/compatibility-package.md#add-support-for-aem-forms-and-assets-in-aem-forms)

* Fragments de document
* Lettres
* Dictionnaires de données
* Modèles et pages des formulaires adaptatifs obsolètes

For more information, see [Assets made compatible with AEM Forms 6.5 by installing the Compatibility package](../../forms/using/compatibility-package.md#assetsmadecompatible).

## Add support for AEM Forms 6.4, 6.3 and 6.2 assets in AEM Forms 6.5 {#add-support-for-aem-forms-and-assets-in-aem-forms}

Après avoir effectué une mise à niveau, exécutez les opérations suivantes pour installer le package de compatibilité AEMFD et rendre vos actifs compatibles avec la version 6.5 :

Ensure that you have [AEM Compatibility package](https://helpx.adobe.com/fr/aem-forms/kb/aem-forms-releases.html) pre-installed.

1. Install the latest 6.5 [Compatibility package](https://helpx.adobe.com/fr/aem-forms/kb/aem-forms-releases.html).

   Pour plus d’informations sur le téléchargement et l’installation du package, voir [Utilisation de packages](/help/sites-administering/package-manager.md).

1. Une fois les journaux stabilisés, redémarrez le serveur.
1. Utilisez l’utilitaire de migration pour rendre vos actifs compatibles avec la version 6.5.

   For more information, see [migration utility](../../forms/using/migration-utility.md).

## Actifs devenus compatibles avec AEM Forms 6.5 après l’installation du package de compatibilité {#assetsmadecompatible}

En installant le package Compatibilité, vous pouvez rendre les actifs et modèles suivants compatibles avec AEM Forms 6.5 :

* Actifs de Correspondence Management d’AEM 6.4 et versions antérieures:

   * [Lettres](../../forms/using/create-letter.md)
   * [Dictionnaires de données](/help/forms/using/data-dictionary.md)
   * Fragments de document

* Modèles obsolètes de formulaires adaptatifs :

   * /libs/fd/af/templates/blankTemplate2
   * /libs/fd/af/templates/simpleEnrollmentTemplate
   * /libs/fd/af/templates/simpleEnrollmentTemplate2
   * /libs/fd/af/templates/surveyTemplate
   * /libs/fd/af/templates/surveyTemplate2
   * /libs/fd/af/templates/tabbedEnrollmentTemplate
   * /libs/fd/af/templates/tabbedEnrollmentTemplate2
   * /libs/fd/afaddon/templates/advancedEnrollmentTemplate
   * /libs/fd/afaddon/templates/advancedEnrollmentTemplate2

* Pages obsolètes de formulaires adaptatifs :

   * /libs/fd/af/components/page/survey
   * /libs/fd/af/components/page/tabbedenrollment
   * /libs/fd/afaddon/components/page/advancedenrollment

