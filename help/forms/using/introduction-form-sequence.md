---
title: Présentation de la séquence de formulaires à plusieurs étapes
description: Avec AEM Forms, vous pouvez définir une séquence de panneaux de formulaires dans lesquels vous souhaitez que les utilisateurs et les utilisatrices naviguent et remplissent un formulaire adaptatif.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
docset: aem65
feature: Adaptive Forms
exl-id: 1333c6cb-15cc-429b-a13e-5d23afdee69a
source-git-commit: 474a726058b141985f52a0faec6161a34be1e9dc
workflow-type: ht
source-wordcount: '589'
ht-degree: 100%

---

# Présentation de la séquence de formulaires à plusieurs étapes{#introduction-to-multi-step-form-sequence}

<span class="preview"> Adobe recommande d’utiliser les [composants principaux](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=fr) de capture de données modernes et extensibles pour [créer de nouveaux formulaires adaptatifs](/help/forms/using/create-an-adaptive-form-core-components.md) ou [ajouter des formulaires adaptatifs à des pages AEM Sites](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md). Ces composants représentent une avancée significative dans la création de formulaires adaptatifs, ce qui garantit des expériences utilisateur impressionnantes. Cet article décrit une approche plus ancienne de la création de formulaires adaptatifs à l’aide de composants de base. </span>

| Version | Lien de l’article |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Cliquez ici](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/configure-layout-of-an-adaptive-form/introduction-form-sequence.html?lang=fr) |
| AEM 6.5 | Cet article |


Les formulaires adaptatifs permettent aux auteurs et autrices de formulaires de créer une expérience de capture de données à plusieurs étapes en toute simplicité. Cela s’accompagne d’une prise en charge intégrée pour la création de plusieurs panneaux et l’association de chaque panneau à différents modèles de navigation. Les auteurs et autrices de formulaires peuvent regrouper les champs de formulaire dans des sections logiques et représenter un groupe sous la forme d’un panneau. La navigation globale entre les panneaux est contrôlée à l’aide de la disposition des panneaux. Les auteurs peuvent réorganiser les panneaux selon différentes dispositions en les plaçant, par exemple, de manière séquentielle à l’aide de la disposition Assistant ou de manière ad hoc avec la disposition Onglets. Pour plus d’informations sur les dispositions de panneaux, voir [Fonctionnalités de disposition des formulaires adaptatifs](../../forms/using/layout-capabilities-adaptive-forms.md).

Dans une expérience de remplissage de formulaire classique, les étapes à suivre ne se limitent pas à la capture des données. Un envoi complet de formulaire peut inclure d’autres étapes, comme la signature numérique du formulaire, la vérification des informations renseignées et le traitement des paiements. Cela diffère d’un cas à l&#39;autre.

Si votre cas d’utilisation requiert un ensemble d’étapes pour l’acquisition de données ou si des règles prévoient l’exécution de certaines étapes, AEM Forms vous offre la possibilité d’appliquer cette structure commune au sein des formulaires. La mise en œuvre prédéfinie de la structure d’un formulaire détermine la séquence d’étapes d’un formulaire. ![Exemple de séquence de formulaires à plusieurs étapes](assets/formpipeline.png)

Exemple de séquence de formulaires à plusieurs étapes

Supposons que vous deviez créer une séquence pour les étapes de remplissage, de vérification, de signature et de confirmation d’un formulaire. Pour créer une telle séquence, les étapes sont les suivantes :

1. Définissez un modèle de formulaire et ajoutez-lui le panneau requis. Notez qu’il doit y avoir un seul panneau par étape dans la séquence. Vous pouvez toutefois inclure des sous-panneaux dans un panneau.

   Dans cet exemple, les panneaux suivants peuvent être ajoutés :

   * **Remplir** : contient des champs de formulaire pour l’acquisition de données. Ici, vous pouvez inclure des sous-panneaux imbriqués afin de créer des sections pour différents types d’informations, comme des informations personnelles, familiales ou financières, par exemple.

   * **Vérifier** : contient le composant **Vérifier** qui peut être utilisé dans un formulaire adaptatif à base XFA. Ce panneau affiche les informations saisies dans le panneau Remplir en mode lecture seule à des fins de vérification.

   * **Signer électroniquement** : contient le composant **Sign** qui peut être utilisé dans un formulaire adaptatif XFA. Ce panneau fournit les services de signature suivants :

      * Services Adobe Document Cloud eSign
      * Signature tactile

   * **Confirmation** : contient le composant **Résumé** qui affiche un message de conformation d’envoi du formulaire lorsqu’un utilisateur l’a signé et a atteint l’étape de confirmation (Résumé) dans la séquence. Les auteurs peuvent configurer le texte du composant de Résumé, afficher un message de remerciement et un lien vers le PDF généré, etc.

1. Sélectionnez la disposition du panneau racine en tant qu’**[!UICONTROL Assistant]**.
1. Effectuez les étapes restantes afin de pouvoir créer le modèle de formulaire. Voir [Créer un modèle de formulaire adaptatif personnalisé](../../forms/using/custom-adaptive-forms-templates.md).

Après avoir défini la séquence de formulaires dans le modèle de formulaire, vous pouvez l’utiliser pour créer des formulaires dont la structure de base est définie en tant que séquence en place. Vous pouvez toujours personnaliser le formulaire en fonction de vos besoins.
