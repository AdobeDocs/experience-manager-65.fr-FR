---
title: Composant Separator dans les formulaires adaptatifs
description: Vous pouvez utiliser le composant séparateur pour isoler visuellement les sections d’un formulaire.
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
docset: aem65
feature: Adaptive Forms,Foundation Components
exl-id: 11cbf865-c8e2-4833-b0b8-a3cb5e42f5cd
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: ht
source-wordcount: '361'
ht-degree: 100%

---

# Composant Separator dans les formulaires adaptatifs{#separator-component-in-adaptive-forms}

<span class="preview"> Adobe recommande d’utiliser les [composants principaux](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=fr) de capture de données modernes et extensibles pour [créer de nouveaux formulaires adaptatifs](/help/forms/using/create-an-adaptive-form-core-components.md) ou [ajouter des formulaires adaptatifs à des pages AEM Sites](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md). Ces composants représentent une avancée significative dans la création de formulaires adaptatifs, ce qui garantit des expériences utilisateur impressionnantes. Cet article décrit une approche plus ancienne de la création de formulaires adaptatifs à l’aide de composants de base. </span>

Vous pouvez utiliser le composant Séparateur pour isoler visuellement les panneaux d’un formulaire. Vous pouvez définir l’aspect général et le style d’un composant Séparateur en spécifiant les propriétés suivantes du composant :

* **Nom de l’élément :** indique le nom du composant. L’expression SOM intègre au composant la valeur spécifiée dans le champ de nom d’élément.
* **Épaisseur :** indique l’épaisseur en pixels du composant séparateur.

* **Classe CSS :** spécifie la classe CSS personnalisée pour le composant séparateur

* **Styles en ligne :** avec AEM Forms, vous pouvez désormais appliquer des styles CSS en ligne à chaque composant de formulaire adaptatif et prévisualiser les modifications en temps réel.

Vous pouvez utiliser le mode Mise en page pour définir le nombre de colonnes sur lequel s’étend le composant séparateur. Pour plus d’informations, voir [Utilisation du mode Mise en page pour redimensionner les composants](../../forms/using/resize-using-layout-mode.md).

Pour définir les propriétés d’un composant Séparateur :

1. Sélectionnez un composant Séparateur et sélectionnez ![cmppr](assets/cmppr.png). Les propriétés s’ouvrent dans la barre latérale.
1. Cliquez sur un onglet dans la section Propriétés CSS intégrées afin de spécifier les propriétés CSS. Par exemple : a. Dans l’onglet Champ, cliquez sur **Ajouter un élément**. Une ligne avec deux champs est ajoutée.
1. Dans le premier champ de gauche, spécifiez une propriété CSS3 à appliquer. Par exemple : **border**. Vous pouvez également sélectionner une propriété en cliquant sur la flèche vers le bas. La liste déroulante n’est pas exhaustive et vous pouvez spécifier n’importe quel nom de propriété CSS3 prise en charge dans ce champ.
1. Dans le champ adjacent, spécifiez une valeur valide pour la propriété CSS3 spécifiée. Par exemple : **3-px solid black**.
1. Cliquez sur **Ajouter un élément** pour définir une autre propriété et sa valeur.
1. Cliquez sur **Aperçu** pour prévisualiser les modifications dans le formulaire.
1. Cliquez sur **OK** pour confirmer les modifications ou sur **Annuler** pour quitter la boîte de dialogue sans modification.
