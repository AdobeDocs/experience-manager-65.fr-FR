---
title: Présentation de la séquence de formulaires à plusieurs étapes
seo-title: Introduction to multi-step form sequence
description: Avec AEM Forms, vous pouvez définir une séquence de panneaux de formulaires dans lesquels vous souhaitez que les utilisateurs naviguent et remplissent un formulaire adaptatif.
seo-description: With AEM Forms, you can define a sequence of form panel in which you want users to navigate and fill an adaptive form.
uuid: db1aac25-fe69-4e43-88d1-4a15389b507f
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
discoiquuid: 0f335ea0-504f-4cc0-b97b-c3fc715bcc2e
docset: aem65
feature: Adaptive Forms
exl-id: 1333c6cb-15cc-429b-a13e-5d23afdee69a
source-git-commit: 1683338f02d01d5d9843368955fa42f309718f26
workflow-type: tm+mt
source-wordcount: '538'
ht-degree: 48%

---

# Présentation de la séquence de formulaires à plusieurs étapes{#introduction-to-multi-step-form-sequence}

| Version | Lien de l’article |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Cliquez ici](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/configure-layout-of-an-adaptive-form/introduction-form-sequence.html) |
| AEM 6.5 | Cet article |


Les formulaires adaptatifs permettent aux auteurs de formulaires de créer facilement une expérience de capture de données à plusieurs étapes. Il s’accompagne d’une prise en charge intégrée pour la création de plusieurs panneaux et l’association de chaque panneau à différents modèles de navigation. Les auteurs de formulaire peuvent regrouper les champs de formulaire dans des sections logiques et représenter un groupe sous la forme d’un panneau. La navigation globale entre les panneaux est contrôlée à l’aide de la disposition des panneaux. Les auteurs peuvent réorganiser les panneaux selon différentes dispositions en les plaçant, par exemple, de manière séquentielle à l’aide de la disposition Assistant ou de manière ad hoc avec la disposition Onglets. Pour plus d’informations sur les dispositions de panneaux, voir [Fonctionnalités de disposition des formulaires adaptatifs](../../forms/using/layout-capabilities-adaptive-forms.md).

Dans le cadre d’une expérience de remplissage de formulaire classique, il existe davantage d’étapes à suivre que la simple capture de données. Un envoi complet de formulaire peut inclure d’autres étapes, comme la signature numérique du formulaire, la vérification des informations renseignées dans le formulaire, le traitement des paiements, etc. Cela diffère d&#39;un cas à l&#39;autre.

Si votre cas d’utilisation requiert un ensemble d’étapes pour l’acquisition de données ou si des réglementations doivent être suivies, AEM Forms vous offre un moyen d’appliquer cette structure commune à tous les formulaires. L’implémentation prédéfinie de la structure de formulaires détermine la séquence d’étapes d’un formulaire. ![Exemple de séquence de formulaires à plusieurs étapes](assets/formpipeline.png)

Exemple de séquence de formulaires à plusieurs étapes

Prenons un cas d’utilisation où vous devez créer une séquence pour les étapes de remplissage, de vérification, de signature et de confirmation d’un formulaire. Les étapes de création d’une telle séquence sont les suivantes :

1. Définissez un modèle de formulaire et ajoutez-y le panneau requis. Notez qu’il doit y avoir un panneau pour chaque étape de la séquence. Vous pouvez toutefois inclure des sous-panneaux dans un panneau.

   Dans cet exemple, nous pouvons ajouter les panneaux suivants :

   * **Remplir**: Il contient des champs de formulaires pour la capture de données. Vous pouvez inclure des sous-panneaux imbriqués afin de créer des sections pour différents types d’information ; personnel, famille ou financier, par exemple.

   * **Vérifier** : contient le composant **Vérifier** qui peut être utilisé dans un formulaire adaptatif à base XFA. Ce panneau affiche les informations saisies dans le panneau Remplir en mode lecture seule à des fins de vérification.

   * **Signer électroniquement** : contient le composant **Sign** qui peut être utilisé dans un formulaire adaptatif XFA. il fournit les services de signature suivants :

      * Services Adobe Document Cloud eSign
      * Signature tactile

   * **Confirmation** : contient le composant **Résumé** qui affiche un message de conformation d’envoi du formulaire lorsqu’un utilisateur l’a signé et a atteint l’étape de confirmation (Résumé) dans la séquence. Les auteurs peuvent configurer le texte du composant de Résumé, afficher un message de remerciement et un lien vers le PDF généré, etc.

1. Sélectionnez la disposition du panneau racine comme **[!UICONTROL Assistant]**.
1. Effectuez les étapes restantes pour créer le modèle de formulaire. Pour plus d’informations, voir [Création d’un modèle de formulaire adaptatif personnalisé](../../forms/using/custom-adaptive-forms-templates.md).

Après avoir défini la séquence des formulaires dans le modèle de formulaire, vous pourrez vous en servir pour créer des formulaires dont la séquence active sera utilisée comme structure de base. Cependant, vous pourrez toujours personnaliser le formulaire en fonction de vos besoins.
