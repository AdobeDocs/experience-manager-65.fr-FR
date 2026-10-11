---
title: Présentation des formulaires HTML5
description: Les formulaires HTML5 sont une nouvelle fonctionnalité du logiciel Adobe Experience Manager 6.0 (AEM 6.0). Ils permettent d’effectuer le rendu des modèles de formulaires XFA au format HTML5.
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
docset: aem65
feature: HTML5 Forms,Mobile Forms
exl-id: 0facca18-ffa1-420c-859a-6f1f2c449d71
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
product_v2:
  - id: fd1f54a9-f50c-467d-8956-cebbaf4f3eb8
    internal-label: Experience Manager
  - id: e8f6de9b-cf88-4405-8d10-15efa08c230e
    internal-label: Experience Manager Forms
feature_v2:
  - id: 97aafc4b-2598-52d6-9012-295a95969e38
    internal-label: HTML5 Forms
  - id: 59f95943-e802-56ac-990d-21ab923984c1
    internal-label: Mobile Forms
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
source-git-commit: 1880cdd6fa659c17e8efb3854b9b9441ff22c2b2
workflow-type: tm+mt
source-wordcount: '422'
ht-degree: 100%
---
# Présentation des formulaires HTML5{#introduction-to-html-forms}

Les formulaires HTML5 sont une nouvelle fonctionnalité du logiciel Adobe Experience Manager 6.0 (AEM 6.0). Ils permettent d’effectuer le rendu des modèles de formulaires XFA au format HTML5. Cette fonctionnalité permet le rendu des formulaires sur les appareils mobiles et les navigateurs de bureau ne prenant pas en charge les documents XFA en PDF. Les formulaires HTML5 prennent en charge les fonctionnalités existantes des modèles de formulaires XFA, mais ajoutent également de nouvelles fonctionnalités, telles que la signature manuscrite, pour les appareils mobiles.

Les formulaires HTML5 génèrent des documents basés sur des éléments HTML5 standards. Vous pouvez afficher les formulaires HTML5 dans tous les navigateurs récents prenant en charge le format HTML5. Il n’est pas nécessaire d’installer de module externe de navigateur supplémentaire pour les navigateurs. Pour plus d’informations sur les navigateurs pris en charge, consultez la section [Plateformes clientes prises en charge](https://adobe.com/go/learn_aemforms_supportedplatforms_63_fr).

![Aperçu du formulaire HTML5](do-not-localize/mobile_form_on_an_ipad_date_14.png)

## Fonctionnalités essentielles des formulaires HTML5 {#key-capabilities-of-html-forms-br}

* Rendu des formulaires XFA existants en HTML5 pris en charge sur tous les navigateurs compatibles.
* Exploitation des fonctionnalités standard de conception des formulaires XFA pour les appliquer aux formulaires sur périphériques mobiles.
* Utilisation des fonctionnalités XFA dynamiques au format HTML5.
* Utilisation de la mise en page haute précision SVG (SVG 1.1) pour une correspondance parfaite avec la mise en page de textes PDF.
* Prise en charge de Javascript et de FormCalc.
* Assemblage dynamique de fragments dans des formulaires interactifs en fonction d’événements basés sur des données ou des entrées saisies par l’utilisateur ou l’utilisatrice.
* Prise en charge des CSS personnalisées pour correspondre à l’aspect standard des formulaires de votre entreprise.
* Prise en charge de widgets personnalisés pour une expérience de capture de données riche.
* Prise en charge de l’intégration avec des applications Web.

### Publication multicanal {#multichannel-publishing}

Les développeurs et développeuses de formulaires peuvent utiliser un modèle XFA pour effectuer le rendu des formulaires aux formats PDF et HTML5. Cette fonctionnalité peut s’avérer utile dans les cas où vous avez un jeu de formulaires XFA important nécessitant des modifications mineures pour s’adapter aux pratiques de conception des formulaires HTML5. Vous pouvez générer les formulaires XFA existants au format HTML5 pour cibler différents périphériques ne prenant pas encore en charge le format PDF basé sur XFA.

## Gestion des formulaires HTML5 {#manage-html-forms}

AEM fournit également un affichage unifié permettant de répertorier et gérer tous les modèles de formulaires à l’aide de l’interface utilisateur d’AEM Forms. Vous pouvez activer, désactiver, publier, et prévisualiser des formulaires. Pour en savoir plus, voir [Présentation de la gestion des formulaires](../../forms/using/introduction-managing-forms.md).

### Personnalisation des formulaires {#forms-customization}

Mobile Forms effectue le rendu des modèles de formulaires à l’aide d’éléments HTML5 standard. Cela facilite la personnalisation et l’extension des formulaires au format HTML5 à l’aide de technologies Web, principalement CSS et JavaScript. Vous pouvez facilement personnaliser l’apparence de widgets existants, créer vos propres widgets personnalisés ou utiliser des styles personnalisés dans les formulaires. Pour plus d’informations sur la création de widgets personnalisés et la personnalisation de widgets existants, consultez la section [Ajout de widgets personnalisés aux formulaires HTML5](../../forms/using/custom-widgets.md).
