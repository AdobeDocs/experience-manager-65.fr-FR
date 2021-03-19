---
title: Composant Separator dans les formulaires adaptatifs
seo-title: Composant Separator dans les formulaires adaptatifs
description: Vous pouvez utiliser le composant Separator pour isoler visuellement les sections d’un formulaire.
seo-description: Vous pouvez utiliser le composant Separator pour isoler visuellement les sections d’un formulaire.
uuid: f8d2aed3-52aa-437f-bfe3-0c8779e7986c
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
discoiquuid: a8aa77fe-5880-4c4e-9e1b-3c5a8772c29d
docset: aem65
feature: Formulaires adaptatifs
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '317'
ht-degree: 85%

---


# Composant Separator dans les formulaires adaptatifs{#separator-component-in-adaptive-forms}

Vous pouvez utiliser le composant Separator pour isoler visuellement les volets d’un formulaire. Vous pouvez définir l’aspect général et le style d’un composant Separator en spécifiant les propriétés suivantes du composant :

* **Nom d’élément :** spécifie le nom du composant. L’expression SOM intègre au composant la valeur spécifiée dans le champ de nom d’élément.
* **Epaisseur :** indique l’épaisseur du composant de séparateur en pixels.

* **Classe CSS :** spécifie la classe CSS personnalisée pour le composant de séparateur

* **Styles en ligne :** avec AEM Forms, vous pouvez désormais appliquer des styles CSS en ligne à chaque composant de formulaire adaptatif et prévisualiser les modifications en temps réel.

Vous pouvez utiliser le mode Disposition pour définir le nombre de colonnes auxquelles s’étend le composant Separator. Pour plus d’informations, voir [Utilisation du mode Mise en page pour redimensionner les composants](../../forms/using/resize-using-layout-mode.md).

Pour définir les propriétés d’un composant de séparateur :

1. Sélectionnez un composant Separator et appuyez sur ![cmppr](assets/cmppr.png). Les propriétés s’ouvrent dans la zone latérale.
1. Cliquez sur un onglet dans la section Propriétés CSS intégrées pour spécifier les propriétés CSS. Par exemple, dans l’onglet Champ, cliquez sur **Ajouter un élément**. Une ligne avec deux champs est ajoutée.
1. Dans le premier champ de gauche, spécifiez une propriété CSS3 à appliquer. Par exemple, la **bordure**. Vous pouvez également sélectionner une propriété en cliquant sur le bouton de flèche vers le bas. La liste déroulante n’est pas exhaustive et vous pouvez spécifier n’importe quel nom de propriété CSS3 prise en charge dans ce champ.
1. Dans le champ adjacent, spécifiez une valeur valide pour la propriété CSS3 spécifiée. Par exemple,**noir 3px**.
1. Cliquez sur **Ajouter un élément** pour définir une autre propriété et sa valeur.
1. Cliquez sur **Aperçu** pour prévisualiser les modifications dans le formulaire.
1. Cliquez sur **OK** pour confirmer les modifications ou **sur** Annuler pour quitter la boîte de dialogue sans modification.

