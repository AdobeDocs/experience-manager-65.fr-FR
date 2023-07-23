---
title: Composant Separator dans les formulaires adaptatifs
seo-title: Separator component in adaptive forms
description: Vous pouvez utiliser le composant séparateur pour isoler visuellement les sections d’un formulaire.
seo-description: You can use the separator component to visually segregate sections of a form.
uuid: f8d2aed3-52aa-437f-bfe3-0c8779e7986c
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
discoiquuid: a8aa77fe-5880-4c4e-9e1b-3c5a8772c29d
docset: aem65
feature: Adaptive Forms
exl-id: 11cbf865-c8e2-4833-b0b8-a3cb5e42f5cd
source-git-commit: e7a3558ae04cd6816ed73589c67b0297f05adce2
workflow-type: tm+mt
source-wordcount: '354'
ht-degree: 55%

---

# Composant Separator dans les formulaires adaptatifs{#separator-component-in-adaptive-forms}

<span class="preview"> Adobe recommande d’utiliser la capture de données moderne et extensible. [Composants principaux](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=fr) pour [création d’un Forms adaptatif](/help/forms/using/create-an-adaptive-form-core-components.md) ou [Ajout de Forms adaptatif à des pages AEM Sites](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md). Ces composants représentent une avancée significative dans la création de Forms adaptatif, ce qui garantit des expériences utilisateur impressionnantes. Cet article décrit l’approche plus ancienne de la création de Forms adaptatif à l’aide de composants de base. </span>

Vous pouvez utiliser le composant séparateur pour isoler visuellement les panneaux d’un formulaire. Vous pouvez définir l’aspect général et le style d’un composant séparateur en spécifiant les propriétés suivantes du composant :

* **Nom de l’élément :** Indique le nom du composant. Les expressions SOM s’adressent au composant avec la valeur spécifiée dans le champ Nom de l’élément .
* **Épaisseur :** indique l’épaisseur en pixels du composant séparateur.

* **Classe CSS :** spécifie la classe CSS personnalisée pour le composant séparateur

* **Styles en ligne :** avec AEM Forms, vous pouvez désormais appliquer des styles CSS en ligne à chaque composant de formulaire adaptatif et prévisualiser les modifications en temps réel.

Vous pouvez utiliser le mode Mise en page pour définir le nombre de colonnes sur lequel s’étend le composant séparateur. Pour plus d’informations, voir [Utilisation du mode Mise en page pour redimensionner les composants](../../forms/using/resize-using-layout-mode.md).

Pour définir les propriétés d’un composant séparateur :

1. Sélectionnez un composant séparateur et appuyez sur ![cmppr](assets/cmppr.png). Les propriétés s’ouvrent dans la barre latérale.
1. Cliquez sur un onglet de la section Propriétés CSS intégrées pour spécifier les propriétés CSS. Par exemple : a. Dans l’onglet Champ, cliquez sur **Ajouter un élément**. Une ligne avec deux champs est ajoutée.
1. Dans le premier champ de gauche, spécifiez une propriété CSS3 à appliquer. Par exemple : **border**. Vous pouvez également sélectionner une propriété en cliquant sur la flèche vers le bas. La liste déroulante n’est pas exhaustive et vous pouvez spécifier n’importe quel nom de propriété CSS3 prise en charge dans ce champ.
1. Dans le champ adjacent, spécifiez une valeur valide pour la propriété CSS3 spécifiée. Par exemple : **noir 3px**.
1. Cliquez sur **Ajouter un élément** pour définir une autre propriété et sa valeur.
1. Cliquez sur **Aperçu** pour prévisualiser les modifications dans le formulaire.
1. Cliquez sur **OK** pour confirmer les modifications ou **sur** Annuler pour quitter la boîte de dialogue sans modification.
