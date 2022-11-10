---
title: Impossible d’ouvrir les PDF forms basés sur XFA dans Google Chrome, Firefox, Microsoft Edge, Microsoft Internet Explorer ou Apple Safari.
seo-title: Unable to open XFA-based PDF forms in Google Chrome, Firefox, Microsoft Edge, Microsoft Internet Explorer, or Apple Safari
feature: Adaptive Forms
source-git-commit: faaec082169e3d03c75b8d762dbe4d76475766af
workflow-type: tm+mt
source-wordcount: '391'
ht-degree: 0%

---


# Impossible d’ouvrir les PDF forms basés sur XFA dans Google Chrome, Firefox, Microsoft Edge, Microsoft Internet Explorer ou Apple Safari.{#unable-to-open-XFA-based-PDF-forms-in-Google-Chrome-Firefox-Microsoft-Edge-Microsoft-Internet-Explorer-or-Apple-Safari}

De nombreuses versions récentes de navigateur incluent leur propre prise en charge limitée des PDF forms basés sur XFA. Bien que ces navigateurs puissent ouvrir des PDF forms XFA, l’étendue de la prise en charge est inconnue. Si vous ne pouvez pas ouvrir ou envoyer un formulaire de PDF basé sur XFA dans un navigateur moderne, utilisez l’une des méthodes suivantes :

* Utilisation [Adobe® Acrobat®](https://www.adobe.com/acrobat.html) ou [Adobe® Adobe® Reader®](https://get.adobe.com/fr/reader/), version 8 ou ultérieure pour ouvrir et envoyer des PDF forms basés sur XFA.
* Acrobat et Reader, sous Microsoft® Windows®, vous permettent de configurer pour ouvrir des PDF en mode Affichage protégé, ce qui empêche l’ouverture de PDF forms basés sur XFA. Assurez-vous que le mode Vue protégée de votre Acrobat ou Reader est désactivé. Pour plus d’informations, voir [Vue protégée (Windows uniquement)](https://helpx.adobe.com/in/reader/using/protected-mode-windows.html).
* Si vous essayez d’accéder aux PDF forms basés sur XFA sur votre appareil mobile, utilisez Adobe Reader pour mobile. Pour plus d’informations, voir [Application mobile Adobe Reader](https://www.adobe.com/in/acrobat/mobile/acrobat-reader.html).
* (Pour les développeurs Forms) Adobe Experience Manager Forms fournit également une assistance pour la
   * [rendu des formulaires basés sur XFA dans HTML5 Forms ;](https://experienceleague.adobe.com/docs/experience-manager-65/forms/html5-forms/introduction.html?#key-capabilities-of-html-forms-br) de sorte que les formulaires puissent être ouverts dans les navigateurs prenant en charge HTML5, y compris ceux qui s’exécutent sur des périphériques mobiles comme iPad. Le rendu HTML5 des formulaires conserve la disposition de la conception de formulaire et prend en charge la plupart des logiques de formulaire (JavaScript, Calc de formulaire et validations de formulaire, par exemple) intégrées dans le modèle de formulaire XFA.
   * [Conversion de formulaires basés sur XFA en Forms adaptatif mobile réactif](https://experienceleague.adobe.com/docs/experience-manager-65/forms/adaptive-forms-basic-authoring/creating-adaptive-form.html?#create-an-adaptive-form-based-on-an-xfa-form-template). Ces formulaires offrent une mise en page réactive, des fonctionnalités de personnalisation et s’adaptent dynamiquement aux réponses des utilisateurs en ajoutant ou en supprimant des champs ou des sections selon les besoins. Ils fournissent également des connecteurs prêts à l’emploi pour diverses sources de données, des fonctionnalités de document d’enregistrement et une connexion facile à Adobe Analytics pour l’évaluation des performances. Pour plus d’informations, voir [Fonctionnalités clés et fonctionnalités](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/key-features.html).

Ainsi, vos investissements technologiques dans les formulaires XFA sont facilement transférés vers les périphériques où l’exécution du module externe Adobe Reader n’est pas possible. Pour plus d’informations, voir [Documentation du produit Adobe Experience Manager Forms](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/home.html).
