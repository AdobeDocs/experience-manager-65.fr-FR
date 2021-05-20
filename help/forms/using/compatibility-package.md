---
title: Package de compatibilité
seo-title: Package de compatibilité
description: L’installation du package de compatibilité sur AEM Forms 6.5 vous permet d’utiliser les actifs Correspondence Management des versions 6.4 et antérieures d’AEM Forms et les modèles et pages de formulaires adaptatifs obsolètes.
seo-description: L’installation du package de compatibilité sur AEM Forms 6.4 vous permet d’utiliser les actifs de Correspondence Management d’AEM Forms 6.4 et les modèles et pages de formulaires adaptatifs obsolètes
uuid: b49633d6-2cb3-422c-a314-25f3b8a37b7f
contentOwner: gtalwar
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: correspondence-management, installing
geptopics: SG_AEMFORMS/categories/jee
discoiquuid: 73e8ccc6-f857-493e-b6e3-878f93e2a356
docset: aem65
role: Administrator
exl-id: bb16017c-a1bf-40d8-a78d-827c05b7ee2e
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '343'
ht-degree: 59%

---

# Package de compatibilité{#compatibility-package}

## Présentation {#overview}

La communication interactive est l’approche par défaut et recommandée pour créer des communications client dans AEM Forms 6.5. Pour continuer à utiliser les lettres dans AEM Forms 6.5, vous devez installer le dernier [package de compatibilité AEMFD](https://helpx.adobe.com/fr/aem-forms/kb/aem-forms-releases.html).

Le package de compatibilité AEMFD vous permet également d’[utiliser les ressources suivantes d’AEM Forms 6.4, 6.3 et 6.2 sur AEM Forms 6.5 :](../../forms/using/compatibility-package.md#add-support-for-aem-forms-and-assets-in-aem-forms)

* Fragments de document
* Lettres
* Dictionnaires de données
* Modèles et pages des formulaires adaptatifs obsolètes

Pour plus d’informations, voir [Ressources rendues compatibles avec AEM Forms 6.5 en installant le package de compatibilité](../../forms/using/compatibility-package.md#assetsmadecompatible).

## Ajout de la prise en charge des ressources AEM Forms 6.4, 6.3 et 6.2 dans AEM Forms 6.5 {#add-support-for-aem-forms-and-assets-in-aem-forms}

Après avoir effectué une mise à niveau, exécutez les opérations suivantes pour installer le package de compatibilité AEMFD et rendre vos actifs compatibles avec la version 6.5 :

Vérifiez que le [package de compatibilité AEM](https://helpx.adobe.com/aem-forms/kb/aem-forms-releases.html) est préinstallé.

1. Installez la dernière version 6.5 [Package de compatibilité](https://helpx.adobe.com/aem-forms/kb/aem-forms-releases.html).

   Pour plus d’informations sur le téléchargement et l’installation du package, voir [Utilisation de packages](/help/sites-administering/package-manager.md).

1. Une fois les journaux stabilisés, redémarrez le serveur.
1. Utilisez l’utilitaire de migration pour rendre vos actifs compatibles avec la version 6.5.

   Pour plus d’informations, voir [Utilitaire de migration](../../forms/using/migration-utility.md).

## Actifs devenus compatibles avec AEM Forms 6.5 après l’installation du package de compatibilité {#assetsmadecompatible}

En installant le package de compatibilité, vous pouvez rendre les actifs et modèles suivants compatibles avec AEM Forms 6.5 :

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
