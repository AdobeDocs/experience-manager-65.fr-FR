---
title: Comment ouvrir un formulaire PDF XFA dans Firefox et Chrome
description: Comment ouvrir un formulaire PDF XFA dans Firefox et Chrome
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: Security
geptopics: SG_AEMFORMS/categories/jee
role: Admin
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
exl-id: 31b52a82-5062-403e-bba7-e6a7e32ee961
source-git-commit: 913e249ba52f1ee262ed78167ce3b2a857e86213
workflow-type: ht
source-wordcount: '287'
ht-degree: 100%

---

# Comment ouvrir un formulaire PDF XFA dans Firefox et Chrome

## Problème

La visionneuse PDF intégrée dans Mozilla Firefox et Google Chrome ne prend pas en charge les formulaires PDF XFA. Par conséquent, les formulaires PDF XFA ne s’ouvrent pas dans les versions ultérieures de Firefox et Chrome.

## Solution

Pour utiliser des formulaires PDF XFA dans Firefox et Chrome, procédez comme suit pour configurer Firefox et Chrome pour ouvrir des PDF à l’aide d’Adobe Reader ou d’Adobe Acrobat.

>[!NOTE]
> 
> Vérifiez qu’Adobe Reader ou Adobe Acrobat est installé sur votre ordinateur.

### Configurer Firefox

1. Dans Firefox, choisissez **Outils > Options**.

1. Dans la boîte de dialogue Options, cliquez sur **Applications**.

1. Dans l’onglet Applications, saisissez PDF dans le champ de recherche.

1. Pour le type de contenu Portable Document Format (PDF) dans les résultats de la recherche, sélectionnez **Utiliser Adobe Acrobat (dans Firefox)** dans la liste déroulante Action.
   ![use-adobe-acrobat](/help/forms/using/assets/use-adobe-acrobat.png)
1. Cliquez sur OK.

1. Redémarrez Firefox.

### Configurer Chrome

1. Dans Chrome, accédez à l’adresse chrome://plugins/.

1. Cliquez sur Désactiver sous Visionneuse PDF Chrome, puis sur Activer sous Extension Adobe PDF.
   ![chrome-pdf-viewer](/help/forms/using/assets/chrome-image.png)
Pour plus d’informations, consultez la documentation Google de l’extension [Adobe PDF](https://support.google.com/chrome/?hl=en&visit_id=638803785294106945-2276548125&rd=4&topic=3421431#topic=7439538).

>[!NOTE]
> 
> LiveCycle ES4 prend en charge le rendu de formulaires XFA en formulaires HTML5 afin que les formulaires puissent être ouverts dans les navigateurs prenant en charge le format HTML5, y compris ceux qui sont installés sur des appareils mobiles, tels que les iPad. Le rendu HTML5 des formulaires conserve la disposition du formulaire et prend en charge la plupart des logiques de formulaire (JavaScript, Form Calc et les validations de formulaire, par exemple) intégrées dans le modèle de formulaire XFA. Ainsi, vos investissements technologiques dans les formulaires XFA sont facilement transférés vers les appareils sur lesquels l’exécution du plug-in Adobe Reader n’est pas possible.
> >Pour plus d’informations, consultez la [documentation de produit LiveCycle](https://business.adobe.com/products/experience-manager/forms/aem-forms.html).

[Mentions légales](https://chl-author-preview.corp.adobe.com/content/help/fr/legal/legal-notices.html) | [Politique de confidentialité en ligne](https://www.adobe.com/privacy.html)
