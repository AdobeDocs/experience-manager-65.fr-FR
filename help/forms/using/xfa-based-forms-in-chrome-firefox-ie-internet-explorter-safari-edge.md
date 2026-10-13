---
title: Impossible d’ouvrir le PDF forms XFA dans Google Chrome, Firefox, Microsoft&reg ; Edge, Microsoft&reg ; Internet Explorer ou Apple Safari
description: Impossible d’ouvrir le PDF forms XFA dans Google Chrome, Firefox, Microsoft&reg ; Edge, Microsoft&reg ; Internet Explorer ou Apple Safari
feature: Adaptive Forms,Document Services
exl-id: fdd15315-e0d6-4d80-acb4-2e0ecec716c4
solution: Experience Manager, Experience Manager Forms
role: User, Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: e72c079d-d036-46d5-b43d-29b276a174c2
    internal-label: Authoring and publishing content
subfeature_v2:
  - id: a26f372d-6d7c-452b-81df-594dd4365ae1
    internal-label: Adaptive Forms
  - id: f19cff18-c8cc-4a4b-adad-85dd2fa3dbe2
    internal-label: Document Services
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 751e1826ed53df7522418e50a206f0fe622256a4
workflow-type: tm+mt
source-wordcount: '424'
ht-degree: 83%
---
# Impossible d’ouvrir les formulaires PDF XFA dans Google Chrome, Firefox, Microsoft® Edge, Microsoft® Internet Explorer ou Apple Safari.{#unable-to-open-XFA-based-PDF-forms-in-Google-Chrome-Firefox-Microsoft-Edge-Microsoft-Internet-Explorer-or-Apple-Safari}

De nombreuses versions récentes de navigateur offrent leur propre prise en charge limitée des formulaires PDF basés sur XFA. Bien que ces navigateurs puissent ouvrir des formulaires PDF XFA, les fonctionnalités proposées sont limitées. Si vous ne pouvez pas ouvrir ou envoyer un formulaire PDF XFA dans un navigateur moderne, utilisez l’une des méthodes suivantes :

* Utilisez [Adobe® Acrobat®](https://www.adobe.com/fr/acrobat.html) ou [Adobe® Reader®](https://get.adobe.com/fr/reader/) version 8 ou ultérieure pour ouvrir et envoyer des formulaires PDF basés sur XFA.
* Acrobat et Reader, sous Microsoft® Windows®, vous permettent de définir l’ouverture des PDF en mode d’affichage protégé, ce qui empêche l’ouverture de formulaires PDF XFA. Assurez-vous que le mode protégé d’Acrobat ou de Reader est désactivé. Pour plus d’informations, voir [Mode protégé (Windows uniquement)](https://helpx.adobe.com/fr/reader/using/protected-mode-windows.html).
* (Pour les développeurs et développeuses Forms) Adobe Experience Manager Forms prend également en charge :

  * [Le rendu des formulaires basés sur XFA vers des formulaires HTML5](https://experienceleague.adobe.com/docs/experience-manager-65/forms/html5-forms/introduction.html?lang=fr#key-capabilities-of-html-forms-br) de sorte que les formulaires puissent être ouverts dans les navigateurs prenant en charge le format HTML5, y compris ceux qui équipent les appareils mobiles comme l’iPad. Le rendu HTML5 des formulaires conserve la disposition de la conception de formulaire et prend en charge la plupart des logiques de formulaire (JavaScript, form calc et validations de formulaire, par exemple) intégrées dans le modèle de formulaire XFA.
  * [la conversion de formulaires basés sur XFA en formulaires adaptatifs réactifs sur appareils mobiles](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-basic-authoring/creating-adaptive-form.html?lang=fr#create-an-adaptive-form-based-on-an-xfa-form-template). Ces formulaires fournissent une mise en page réactive, des fonctionnalités de personnalisation, et s’adaptent dynamiquement aux réponses des utilisateurs et utilisatrices en ajoutant ou en supprimant des champs ou des sections selon les besoins. Ils fournissent également des connecteurs prêts à l’emploi pour diverses sources de données, des fonctionnalités de document de référence et une connexion facile à Adobe Analytics pour l’évaluation des performances. Pour plus d’informations, voir [Fonctionnalités clés](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/forms-overview/home.html?lang=fr)
    Ainsi, vos investissements technologiques dans les formulaires XFA sont protégés et continuent de fournir une expérience optimale à vos utilisateurs et utilisatrices finaux. Pour plus d’informations, voir [Documentation du produit Adobe Experience Manager Forms](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/forms-overview/home.html?lang=fr).
