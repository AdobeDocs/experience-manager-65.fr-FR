---
title: Impossible d’ouvrir les formulaires PDF XFA dans Google Chrome, Firefox, Microsoft Edge, Microsoft Internet Explorer ou Apple Safari.
description: Impossible d’ouvrir les formulaires PDF XFA dans Google Chrome, Firefox, Microsoft Edge, Microsoft Internet Explorer ou Apple Safari.
feature: Adaptive Forms
exl-id: fdd15315-e0d6-4d80-acb4-2e0ecec716c4
solution: Experience Manager, Experience Manager Forms
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '341'
ht-degree: 100%

---

# Impossible d’ouvrir les formulaires PDF XFA dans Google Chrome, Firefox, Microsoft® Edge, Microsoft® Internet Explorer ou Apple Safari.{#unable-to-open-XFA-based-PDF-forms-in-Google-Chrome-Firefox-Microsoft-Edge-Microsoft-Internet-Explorer-or-Apple-Safari}

De nombreuses versions récentes de navigateur offrent leur propre prise en charge limitée des formulaires PDF basés sur XFA. Bien que ces navigateurs puissent ouvrir des formulaires PDF XFA, les fonctionnalités proposées sont limitées. Si vous ne pouvez pas ouvrir ou envoyer un formulaire PDF XFA dans un navigateur moderne, utilisez l’une des méthodes suivantes :

* Utilisez [Adobe® Acrobat®](https://www.adobe.com/fr/acrobat.html) ou [Adobe® Reader®](https://get.adobe.com/fr/reader/) version 8 ou ultérieure pour ouvrir et envoyer des formulaires PDF basés sur XFA.
* Acrobat et Reader, sous Microsoft® Windows®, vous permettent de définir l’ouverture des PDF en mode d’affichage protégé, ce qui empêche l’ouverture de formulaires PDF XFA. Assurez-vous que le mode protégé d’Acrobat ou de Reader est désactivé. Pour plus d’informations, voir [Mode protégé (Windows uniquement)](https://helpx.adobe.com/fr/reader/using/protected-mode-windows.html).
* (Pour les développeurs et développeuses Forms) Adobe Experience Manager Forms prend également en charge :

   * [Le rendu des formulaires basés sur XFA vers des formulaires HTML5](https://experienceleague.adobe.com/docs/experience-manager-65/forms/html5-forms/introduction.html?lang=fr#key-capabilities-of-html-forms-br) de sorte que les formulaires puissent être ouverts dans les navigateurs prenant en charge le format HTML5, y compris ceux qui équipent les appareils mobiles comme l’iPad. Le rendu HTML5 des formulaires conserve la disposition de la conception de formulaire et prend en charge la plupart des logiques de formulaire (JavaScript, form calc et validations de formulaire, par exemple) intégrées dans le modèle de formulaire XFA.
   * [la conversion de formulaires basés sur XFA en formulaires adaptatifs réactifs sur appareils mobiles](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-basic-authoring/creating-adaptive-form.html?lang=fr#create-an-adaptive-form-based-on-an-xfa-form-template). Ces formulaires fournissent une mise en page réactive, des fonctionnalités de personnalisation, et s’adaptent dynamiquement aux réponses des utilisateurs et utilisatrices en ajoutant ou en supprimant des champs ou des sections selon les besoins. Ils fournissent également des connecteurs prêts à l’emploi pour diverses sources de données, des fonctionnalités de document d’enregistrement et une connexion facile à Adobe Analytics pour l’évaluation des performances. Pour plus d’informations, consultez la section [Fonctionnalités et capacités essentielles](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/forms-overview/home.html?lang=fr).
Ainsi, vos investissements technologiques dans les formulaires XFA sont garantis et continuent d’offrir une expérience optimale à vos utilisateurs et utilisatrices finaux. Pour plus d’informations, voir [Documentation du produit Adobe Experience Manager Forms](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/forms-overview/home.html?lang=fr).
