---
title: Comment ouvrir un PDF forms XFA sur Firefox et Chrome
description: Comment ouvrir un PDF forms XFA sur Firefox et Chrome
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: Security
geptopics: SG_AEMFORMS/categories/jee
role: Admin
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
source-git-commit: ebb61f2c5056a780e829e64031f8eba69a8ae25b
workflow-type: tm+mt
source-wordcount: '287'
ht-degree: 1%

---

# Comment ouvrir un PDF forms XFA sur Firefox et Chrome

## Problème

La visionneuse PDF intégrée introduite avec Mozilla Firefox et Google Chrome ne prend pas en charge les PDF forms basés sur XFA. Par conséquent, les PDF forms basés sur XFA ne s’ouvrent pas dans les versions ultérieures de Firefox et Chrome.

## Solution

Pour utiliser PDF forms basé sur XFA sur Firefox et Chrome, procédez comme suit pour configurer Firefox et Chrome pour ouvrir des PDF à l’aide d’Adobe Reader ou Adobe Acrobat.

>[!NOTE]
> 
> Assurez-vous qu’Adobe Reader ou Adobe Acrobat est installé sur votre ordinateur.

### Configuration de Firefox

1. Dans Firefox, choisissez **Outils > Options**.

1. Dans la boîte de dialogue Options, cliquez sur **Applications**.

1. Dans l’onglet Applications , saisissez PDF dans le champ de recherche.

1. Pour le type de contenu Portable Document Format (PDF) dans les résultats de la recherche, sélectionnez **Utiliser Adobe Acrobat (dans Firefox)** dans la liste déroulante Action .
   ![use-adobe-acrobat](/help/forms/using/assets/use-adobe-acrobat.png)
1. Cliquez sur OK.

1. Redémarrez Firefox.

### Configuration de Chrome

1. Dans Chrome, rendez-vous sur chrome://plugins/.

1. Cliquez sur Désactiver sous Visionneuse Chrome PDF, puis sur Activer sous Plug-in Adobe PDF.
   ![chrome-pdf-viewer](/help/forms/using/assets/chrome-image.png)
Pour plus d’informations, voir la documentation du plug-in [Adobe PDF](https://support.google.com/chrome/?hl=en&amp;visit_id=638803785294106945-2276548125&amp;rd=4&amp;topic=3421431#topic=7439538) de Google.

>[!NOTE]
> 
> LiveCycle ES4 prend en charge le rendu des formulaires XFA dans HTML5 afin que les formulaires puissent être ouverts dans les navigateurs prenant en charge HTML5, y compris ceux qui équipent les appareils mobiles comme iPad. Le rendu HTML5 des formulaires conserve la disposition de la conception de formulaire et prend en charge la plupart des logiques de formulaire (comme JavaScript, form calc et validations de formulaire) intégrées dans le modèle de formulaire XFA. Ainsi, vos investissements technologiques dans les formulaires XFA sont facilement transférés vers les appareils sur lesquels l’exécution du plug-in Adobe Reader n’est pas possible.
>Pour plus d’informations, voir [Documentation du produit LiveCycle](https://business.adobe.com/products/experience-manager/forms/aem-forms.html).

[Mentions légales](https://chl-author-preview.corp.adobe.com/content/help/en/legal/legal-notices.html)    |    [Politique de confidentialité en ligne](https://www.adobe.com/fr/privacy.html)