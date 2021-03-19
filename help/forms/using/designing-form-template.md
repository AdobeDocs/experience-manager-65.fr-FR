---
title: Conception de modèles de formulaires HTML5
seo-title: Conception de modèles de formulaires HTML5
description: AEM Forms permet d’effectuer le rendu d’un modèle de formulaire XFA au format HTML5. Les concepteurs de formulaires peuvent concevoir des modèles de formulaire à l’aide de Designer et utiliser la fonction de génération de rendu au format HTML5.
seo-description: AEM Forms permet d’effectuer le rendu d’un modèle de formulaire XFA au format HTML5. Les concepteurs de formulaires peuvent concevoir des modèles de formulaire à l’aide de Designer et utiliser la fonction de génération de rendu au format HTML5.
uuid: 4f6b7231-4479-400a-adcd-c68064f06b4e
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: f2e9dbe4-e210-41f3-8878-2fc4d166e63c
docset: aem65
feature: Mobile Forms
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '517'
ht-degree: 58%

---


# Conception de modèles de formulaires HTML5{#designing-form-templates-for-html-forms}

Le composant Formulaires HTML5 dans AEM permet de générer le rendu du modèle de formulaire XFA au format HTML5. Les concepteurs de formulaires peuvent créer des modèles de formulaire à l’aide de [Forms Designer](https://www.adobe.com/go/learn_aemforms_designer_63) et utiliser la fonction de génération de rendu au format HTML5. Ces modèles de formulaire, ainsi que leurs ressources, peuvent résider dans le référentiel AEM, un système de fichiers, ou sont accessibles via http. Cependant, si vous prévoyez de gérer vos formulaires à l’aide de Forms Manager, les modèles et les ressources doivent résider dans le référentiel AEM.

Bien que les formulaires HTML5 adopteent dans une large mesure un comportement similaire à celui des formulaires PDF, il existe certaines fonctionnalités dans les deux formats qui ne s’appliquent pas dans l’autre format. Par exemple, la manière dont les codes à barres sont appliqués à un formulaire PDF dans Adobe Reader varie d’un formulaire Mobile ou la manière dont un formulaire est signé numériquement varie également d’un format à l’autre. Pour plus d’informations sur ces variations, voir [Différences de caractéristiques entre les formulaires HTML5 et les PDF forms](../../forms/using/feature-differentiation-html5-forms-pdf-forms.md).

Pour les fonctionnalités XFA courantes, consultez les meilleures pratiques et les directives suivantes pour concevoir un formulaire compatible avec les deux formats.

## Bonnes pratiques {#best-practices}

La plupart des étapes autour de la conception d’un modèle de formulaire, comme lier des schémas ou écrire une logique de formulaire, sont identiques. Cependant, en raison des différences inhérentes entre le moteur de rendu et le moteur de script d’un client lourd comme Adobe Reader et les formulaires basés sur un navigateur, quelques recommandations sont fournies dans l’article [Meilleures pratiques](/help/forms/using/design-accessible-html5-forms.md). Ces bonnes pratiques vous aident à concevoir des modèles de formulaire qui fonctionnent comme prévu dans les deux formats.

### Capacités dans AEM Forms Designer pour les formulaires HTML5 {#capabilities-in-aem-forms-designer-for-html-forms}

#### Aperçu HTML {#preview-html}

L’onglet Aperçu HTML est ajouté au mode de création pour permettre aux concepteurs de formulaires de prévisualiser les formulaires au format HTML5 au cours du processus de création. Pour plus d’informations sur la procédure à suivre pour activer et configurer cette fonctionnalité dans AEM Forms Designer, voir [Aperçu HTML](../../forms/using/preview-xdp-forms-html.md).

#### Signature à main levée {#scribble-signature}

L’objectif clé des formulaires HTML5 est les périphériques tactiles. Par conséquent, une nouvelle commande de signature tactile est ajoutée à AEM Form Designer. Vous pouvez cliquer ou faire glisser et déposer le contrôle de signature tactile sur votre modèle de formulaire et le configurer. Il est rendu sous la forme d’un champ de saisie tactile dans le rendu HTML5 et peut être utilisé pour apposer une signature tactile sur les périphériques tactiles. Sur les ordinateurs de bureau, elle peut être utilisée comme un champ de saisie tactile à l’aide de la commande de souris. Pour plus d’informations sur l’utilisation de cette fonctionnalité, voir [Champ de saisie tactile XFA](../../forms/using/scribble-signature.md).

![4](assets/4.png)

#### Format de texte enrichi {#rich-text-format}

Vous pouvez convertir un champ de texte en champ de texte enrichi. Il ajoute une liste d’options de formatage au champ de texte. Pour convertir, ouvrez Forms Designer, appuyez sur le champ de texte dans **[!UICONTROL Vue de conception]**. Dans l&#39;onglet **[!UICONTROL Champ]**, sélectionnez **[!UICONTROL Texte enrichi]** dans la liste déroulante **[!UICONTROL Format du champ]**. Désormais, lorsque le formulaire XFA est rendu en tant que formulaire HTML5, le champ est rendu en tant que champ de texte enrichi. Appuyez sur ![Maximiser](assets/maximize_icon.svg) pour vue d’autres options de formatage.
