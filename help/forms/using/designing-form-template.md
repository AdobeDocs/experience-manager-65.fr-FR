---
title: Concevoir des modèles de formulaires HTML5
description: AEM Forms peut effectuer le rendu d’un modèle de formulaire XFA au format HTML5. Les concepteurs de formulaires peuvent créer des modèles de formulaire à l’aide de Designer et utiliser la fonction de génération de rendu au format HTML5.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
docset: aem65
feature: HTML5 Forms,Mobile Forms
exl-id: 7c8d501f-c953-495e-8bac-1f66fd99c783
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: ht
source-wordcount: '480'
ht-degree: 100%

---

# Concevoir des modèles de formulaires HTML5{#designing-form-templates-for-html-forms}

Le composant Formulaires HTML5 d’AEM peut générer le rendu du modèle de formulaire XFA au format HTML5. Les concepteurs de formulaires peuvent créer des modèles de formulaire à l’aide de [Forms Designer](https://www.adobe.com/go/learn_aemforms_designer_63_fr) et utiliser la fonction de génération de rendu au format HTML5. Ces modèles de formulaire, ainsi que leurs ressources, peuvent résider dans le référentiel AEM, un système de fichiers, ou sont accessibles via http. Cependant, si vous envisagez de gérer vos formulaires à l’aide de Forms Manager, les modèles et ressources doivent résider dans le référentiel AEM.

Bien que les formulaires HTML5 adopteent dans une large mesure un comportement similaire à celui des formulaires PDF, il existe certaines fonctionnalités dans les deux formats qui ne s’appliquent pas dans l’autre format. Par exemple, la façon dont les codes à barres sont appliqués sur un formulaire PDF dans Adobe Reader varie par rapport à un formulaire pour appareils mobiles ; de même, la façon dont un formulaire est signé numériquement varie d’un format à l’autre. Pour plus d’informations sur ces variations, consultez la section [Différenciation des fonctions entre formulaires HTML5 et formulaires PDF](../../forms/using/feature-differentiation-html5-forms-pdf-forms.md).

Pour les fonctionnalités XFA courantes, consultez les bonnes pratiques et les instructions suivantes pour concevoir un formulaire compatible avec les deux formats.

## Bonnes pratiques {#best-practices}

La plupart des étapes de conception d’un modèle de formulaire, telles que les liaisons de schéma ou l’écriture d’une logique de formulaire, sont identiques. Cependant, en raison des différences inhérentes entre le moteur de rendu et le moteur de script d’un client lourd comme Adobe Reader et les formulaires basés sur un navigateur, quelques recommandations sont fournies dans l’article [Meilleures pratiques](/help/forms/using/design-accessible-html5-forms.md). Ces bonnes pratiques vous aident à concevoir des modèles de formulaire capables de fonctionner conformément aux attentes dans les deux formats.

### Capacités dans AEM Forms Designer pour les formulaires HTML5 {#capabilities-in-aem-forms-designer-for-html-forms}

#### Aperçu HTML {#preview-html}

L’onglet Aperçu HTML est ajouté au mode de création pour permettre aux concepteurs et conceptrices de formulaires de prévisualiser les formulaires au format HTML5 au cours du processus de création. Pour plus d’informations sur la procédure à suivre pour activer et configurer cette fonctionnalité dans AEM Forms Designer, voir [Aperçu HTML](../../forms/using/preview-xdp-forms-html.md).

#### Signature tactile {#scribble-signature}

La cible principale des formulaires HTML5 est les appareils tactiles. Par conséquent, une nouvelle commande de signature tactile est ajoutée à AEM Forms Designer. Vous pouvez cliquer ou faire glisser-déposer la commande de signature tactile sur votre modèle de formulaire et la configurer. Elle est générée sous la forme d’un champ de saisie tactile dans le rendu HTML5 et peut être utilisée pour apposer une signature tactile sur les appareils tactiles. Sur les ordinateurs de bureau, elle peut être utilisée comme un champ de saisie tactile à l’aide de la commande de souris. Pour plus d’informations sur l’utilisation de cette fonctionnalité, consultez la section [Champ de saisie tactile XFA](../../forms/using/scribble-signature.md).

![4](assets/4.png)

#### Format RTF (Texte enrichi) {#rich-text-format}

Vous pouvez convertir un champ de texte en champ de texte enrichi. Le champ de texte enrichi permet dʼajouter des options de formatage au champ de texte. Pour effectuer une conversion, ouvrez Forms Designer et cliquez sur le champ de texte dans **[!UICONTROL Mode de conception]**. Dans lʼonglet **[!UICONTROL Champ]**, sélectionnez **[!UICONTROL Texte enrichi]** dans la liste déroulante **[!UICONTROL Format du champ]**. Désormais, lorsque le formulaire XFA est rendu sous la forme d’un formulaire HTML5, le champ est rendu sous la forme d’un champ de texte enrichi. Sélectionnez ![Maximiser](assets/maximize_icon.svg) pour afficher des options de formatage supplémentaires.
