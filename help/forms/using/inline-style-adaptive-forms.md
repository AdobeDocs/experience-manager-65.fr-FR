---
title: Styles intégrés des composants de formulaire adaptatif
seo-title: Propriétés CSS intégrées pour les composants de formulaire adaptatif
description: Si vous pouvez appliquer des styles personnalisés à un formulaire adaptatif, vous pouvez également appliquer des propriétés de style CSS intégré sur les différents composants d’un formulaire adaptatif.
seo-description: Si vous pouvez appliquer des styles personnalisés à un formulaire adaptatif, vous pouvez également appliquer des propriétés de style CSS intégré sur les différents composants d’un formulaire adaptatif.
uuid: e863780e-2250-4bea-9569-22be5638d54e
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
discoiquuid: 21dec713-c76d-408b-baea-fc585377b429
docset: aem65
translation-type: tm+mt
source-git-commit: 33f73225fbb2c48353c1f34db3339c0bb79d4236
workflow-type: tm+mt
source-wordcount: '556'
ht-degree: 91%

---


# Styles intégrés des composants de formulaire adaptatif {#inline-styling-of-adaptive-form-components}

Vous pouvez définir l’aspect général et le style d’un formulaire adaptatif en spécifiant les styles à l’aide d’un [éditeur de thème](../../forms/using/themes.md). En outre, vous pouvez appliquer des styles CSS intégrés à différents composants de formulaire adaptatif et prévisualiser les modifications apportées à la volée. Les styles intégrés remplacent les styles fournis dans le thème.

## Application des propriétés de style CSS intégré {#apply-inline-css-properties}

Pour ajouter des styles intégrés à un composant :

1. Ouvrez votre formulaire dans l’éditeur de formulaire, puis choisissez le mode Style. Pour passer en mode Style, dans la barre d’outils de la page, appuyez sur ![liste déroulante de trame](assets/canvas-drop-down.png) > **Style**.
1. Sélectionnez un composant dans la page, puis appuyez sur le bouton Modifier ![bouton Modifier](assets/edit-button.png). Les propriétés de style s’ouvrent dans la barre latérale.

   Vous pouvez également sélectionner des composants dans l’arborescence de hiérarchie de formulaire dans la barre latérale. L’arborescence de hiérarchie de formulaire est disponible sous forme d’objets de formulaire dans la barre latérale.

   Vous pouvez également sélectionner un composant dans la barre latérale. Dans le mode Style, vous pouvez afficher les composants répertoriés sous Objets de formulaire. Toutefois, la liste des objets de formulaire de la barre latérale répertorie les composants de listes tels que les champs et les panneaux. Les champs et les panneaux sont des composants génériques qui peuvent contenir des composants, tels qu’une zone de texte et des boutons radio.

   Lorsque vous sélectionnez un composant dans la barre latérale, vous voyez tous les sous-composants répertoriés et les propriétés du composant sélectionné. Vous pouvez sélectionner un sous-composant spécifié et le styliser.

1. Cliquez sur un onglet de la barre latérale pour spécifier les propriétés CSS. Vous pouvez définir des propriétés telles que les suivantes :

   * Dimensions et position (paramètre d’affichage, remplissage, hauteur, largeur, marge, position, index z, flottant, clair, débordement)
   * Texte (famille de polices, épaisseur, couleur, taille, hauteur de ligne et alignement)
   * Arrière-plan (image et gradient, couleur d’arrière-plan)
   * Bordure (largeur, style, couleur, rayon)
   * Effets (ombre, opacité)
   * Avancé (permet de saisir un CSS personnalisé pour le composant)

1. De même, vous pouvez appliquer des styles pour d’autres parties d’un composant, tels que Widget, Légende et Aide.
1. Appuyez sur **Terminé** pour confirmer les modifications ou sur **Annuler** pour annuler les modifications.

## Exemple : styles en ligne pour un composant de champ {#example-inline-styles-for-a-field-component}

Les images suivantes illustrent une zone de texte avant et après l’application des styles intégrés.

![Composant de zone de texte avant l’application du style intégré](assets/no-style.png)

Composant de zone de texte avant l’application des propriétés de style intégré

Notez la modification du style de la zone de texte comme illustré ci-dessous après l’application des propriétés CSS suivantes.

<table>
 <tbody>
  <tr>
   <td><p>Sélecteur</p> </td>
   <td><p>Propriété CSS</p> </td>
   <td><p>Valeur</p> </td>
   <td><p>Effet</p> </td>
  </tr>
  <tr>
   <td><p>Champ</p> </td>
   <td><p>bordure</p> </td>
   <td><p>Largeur de la bordure = 2px</p> <p>Style de la bordure = plein</p> <p>Couleur de la bordure = #1111</p> </td>
   <td><p>Crée une bordure large noire 2px autour du champ</p> </td>
  </tr>
  <tr>
   <td><p>Zone de texte</p> </td>
   <td><p>couleur d’arrière-plan</p> </td>
   <td><p>#6495ED</p> </td>
   <td><p>Modifie la couleur d’arrière-plan en CornflowerBlue (#6495ED)</p> <p>Remarque : vous pouvez spécifier un nom de couleur ou son code hexadécimal dans le champ Valeur.</p> </td>
  </tr>
  <tr>
   <td><p>Libellé</p> </td>
   <td><p>Dimensions et position &gt; largeur</p> </td>
   <td><p>100px</p> </td>
   <td><p>Définit la largeur sur 100 px pour le libellé</p> </td>
  </tr>
  <tr>
   <td>Icône d’aide du champ</td>
   <td>Texte &gt; Couleur de la police</td>
   <td>#2ECC40</td>
   <td>Modifie la couleur de l’icône d’aide.</td>
  </tr>
  <tr>
   <td><p>Description longue</p> </td>
   <td><p>alignement de texte</p> </td>
   <td><p>centre</p> </td>
   <td><p>Aligne la description longue pour faciliter le centrage</p> </td>
  </tr>
 </tbody>
</table>

![Style de zone de texte après l’application du style intégré](assets/applied-style.png)

Composant de zone de texte après l’application des propriétés de style intégré

En suivant les étapes ci-dessus, vous pouvez sélectionner et styliser d’autres composants, tels que les panneaux, les boutons d’envoi et les boutons radio.

>[!NOTE]
>
>Les propriétés de style varient en fonction du composant sélectionné.

