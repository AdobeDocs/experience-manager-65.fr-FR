---
title: Problèmes d’affichage des formulaires PDF XFA et des documents protégés par une politique
description: Problèmes d’affichage des formulaires PDF XFA et des documents protégés par une politique
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: Security
geptopics: SG_AEMFORMS/categories/jee
role: Admin
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
exl-id: c9beefac-14e9-466c-b5bd-44ffab1fb820
source-git-commit: 913e249ba52f1ee262ed78167ce3b2a857e86213
workflow-type: ht
source-wordcount: '390'
ht-degree: 100%

---

# Problèmes d’affichage des formulaires PDF XFA et des documents protégés par une politique

Vérifiez les raisons suivantes si vous ne parvenez pas à ouvrir un formulaire PDF XFA ou un document protégé par une politique à l’aide d’Adobe LiveCycle Rights Management :

* Les formulaires PDF XFA et les documents protégés par une politique nécessitent Adobe® Acrobat® ou Adobe® Reader®, version 8 ou ultérieure. Accédez aux [Téléchargements Adobe](https://www.adobe.com/downloads.html) pour télécharger la dernière version de Reader ou d’Acrobat.
* Les navigateurs tels que Mozilla Firefox et Google Chrome possèdent une visionneuse PDF intégrée qui ne prend pas en charge les formulaires PDF XFA. Pour afficher les formulaires PDF XFA dans ces navigateurs, vous devez les configurer pour qu’ils ouvrent les fichiers PDF à l’aide d’Acrobat ou de Reader. Pour plus d’informations, consultez Formulaires PDF XFA dans Mozilla Firefox et Google Chrome.
* Acrobat et Reader, sous Microsoft® Windows®, vous permettent de définir l’ouverture des fichiers PDF en mode d’affichage protégé, ce qui empêche l’ouverture de formulaires PDF XFA et de documents protégés par une politique. Assurez-vous que le mode protégé d’Acrobat ou de Reader est désactivé. Pour plus d’informations, voir [Mode protégé (Windows uniquement)](https://helpx.adobe.com/fr/acrobat/kb/end-of-support-acrobat-x-reader-x.html).
* Si vous tentez d’accéder à des formulaires PDF XFA ou à des documents protégés par une politique sur votre appareil mobile, tenez compte des points suivants :

   * L’ouverture de documents protégés par une politique sur des appareils mobiles nécessite Adobe Reader pour les appareils mobiles. Pour plus d’informations, consultez [Application mobile Adobe Reader](https://www.adobe.com/in/acrobat/mobile/acrobat-reader.html).
   * Les appareils mobiles et les smartphones iOS, Android et Blackberry ne prennent pas en charge le plug-in Adobe Reader avec les formulaires XFA. LiveCycle ES4 fournit un service qui cible les appareils mobiles en utilisant du HTML5 ; le créateur ou la créatrice du formulaire doit utiliser ce service pour permettre l’utilisation du formulaire sur ces appareils.
   * Si vous utilisez le style Metro sur un appareil mobile Windows 8, basculez vers la vue classique ou utilisez le HTML5 avec LiveCycle ES4.

>[!NOTE]
>
>LiveCycle ES4 prend en charge le rendu de formulaires XFA en formulaires HTML5 afin que les formulaires puissent être ouverts dans les navigateurs prenant en charge le format HTML5, y compris ceux qui sont installés sur des appareils mobiles, tels que les iPad. Le rendu HTML5 des formulaires conserve la disposition du formulaire et prend en charge la plupart des logiques de formulaire (JavaScript, Form Calc et les validations de formulaire, par exemple) intégrées dans le modèle de formulaire XFA. Ainsi, vos investissements technologiques dans les formulaires XFA sont facilement transférés vers les appareils sur lesquels l’exécution du plug-in Adobe Reader n’est pas possible.
>>Pour plus d’informations, consultez la [documentation de produit LiveCycle](https://business.adobe.com/fr/products/experience-manager/forms/aem-forms.html).

[Mentions légales](https://chl-author-preview.corp.adobe.com/content/help/fr/legal/legal-notices.html) | [Politique de confidentialité en ligne](https://www.adobe.com/privacy.html)
