---
title: Problèmes d’affichage liés aux documents PDF forms XFA et protégés par une politique
description: Problèmes d’affichage liés aux documents PDF forms XFA et protégés par une politique
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: Security
geptopics: SG_AEMFORMS/categories/jee
role: Admin
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms
source-git-commit: ebb61f2c5056a780e829e64031f8eba69a8ae25b
workflow-type: tm+mt
source-wordcount: '390'
ht-degree: 5%

---

# Problèmes d’affichage liés aux documents PDF forms XFA et protégés par une politique

Vérifiez pour les raisons suivantes si vous ne parvenez pas à ouvrir un formulaire PDF XFA ou un document protégé par une politique à l’aide de la gestion des droits d’Adobe LiveCycle :

* Les documents PDF forms basés sur XFA et protégés par une politique nécessitent Adobe® Acrobat® ou Adobe® Reader®, version 8 ou ultérieure. Voir [Téléchargements Adobe](https://www.adobe.com/downloads.html) pour télécharger la dernière version de Reader ou Acrobat.
* Les navigateurs tels que Mozilla Firefox et Google Chrome offrent une visionneuse PDF intégrée qui ne prend pas en charge les PDF forms basés sur XFA. Pour afficher le PDF forms XFA dans ces navigateurs, vous devez configurer pour ouvrir des fichiers PDF à l’aide d’Acrobat ou de Reader. Pour plus d’informations, voir PDF forms basé sur XFA sous Mozilla Firefox et Google Chrome.
* Acrobat et Reader, sous Microsoft® Windows®, vous permettent de configurer pour ouvrir des fichiers PDF en mode d’affichage protégé, ce qui empêche l’ouverture de documents PDF forms et protégés par une politique basés sur XFA. Assurez-vous que le mode protégé d’Acrobat ou de Reader est désactivé. Pour plus d’informations, voir [Mode protégé (Windows uniquement)](https://helpx.adobe.com/fr/acrobat/kb/end-of-support-acrobat-x-reader-x.html).
* Si vous tentez d’accéder à des documents PDF forms XFA ou protégés par une politique sur votre appareil mobile, tenez compte des points suivants :

   * L’ouverture de documents protégés par une politique sur des appareils mobiles nécessite Adobe Reader pour les appareils mobiles. Pour plus d’informations, voir [Application mobile Adobe Reader](https://www.adobe.com/in/acrobat/mobile/acrobat-reader.html).
   * Les appareils mobiles et smartphones iOS, Android et Blackberry ne prennent pas en charge le plug-in Adobe Reader avec les formulaires XFA. LiveCycle ES4 fournit un service qui cible les appareils mobiles utilisant HTML5 ; le créateur du formulaire doit utiliser ce service pour autoriser l’utilisation de formulaires sur ces appareils.
   * Si vous utilisez le style Metro sur un appareil mobile Windows 8, passez à la vue classique ou exploitez HTML5 avec LiveCycle ES4.

>[!NOTE]
>
>LiveCycle ES4 prend en charge le rendu des formulaires XFA dans HTML5 afin que les formulaires puissent être ouverts dans les navigateurs prenant en charge HTML5, y compris ceux qui équipent les appareils mobiles comme iPad. Le rendu HTML5 des formulaires conserve la disposition de la conception de formulaire et prend en charge la plupart des logiques de formulaire (comme JavaScript, form calc et validations de formulaire) intégrées dans le modèle de formulaire XFA. Ainsi, vos investissements technologiques dans les formulaires XFA sont facilement transférés vers les appareils sur lesquels il n’est pas possible d’exécuter le plug-in Adobe Reader.
>Pour plus d’informations, voir Documentation du produit Mise à niveau vers [LiveCycle](https://business.adobe.com/products/experience-manager/forms/aem-forms.html).

[Mentions légales](https://chl-author-preview.corp.adobe.com/content/help/en/legal/legal-notices.html)    |    [Politique de confidentialité en ligne](https://www.adobe.com/fr/privacy.html)