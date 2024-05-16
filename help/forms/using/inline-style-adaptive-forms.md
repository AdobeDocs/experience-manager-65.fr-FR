---
title: Styles intégrés des composants de formulaire adaptatif
description: Si vous pouvez appliquer des styles personnalisés à un formulaire adaptatif, vous pouvez également appliquer des propriétés CSS intégrées aux différents composants d’un formulaire adaptatif.
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: author
docset: aem65
feature: Adaptive Forms, Foundation Components
exl-id: 67cfecb8-c31d-4192-904d-7bfaa1a31ea5
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: ht
source-wordcount: '592'
ht-degree: 100%

---

# Styles intégrés des composants de formulaire adaptatif {#inline-styling-of-adaptive-form-components}

<span class="preview"> Adobe recommande d’utiliser les [composants principaux](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=fr) de capture de données modernes et extensibles pour [créer de nouveaux formulaires adaptatifs](/help/forms/using/create-an-adaptive-form-core-components.md) ou [ajouter des formulaires adaptatifs à des pages AEM Sites](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md). Ces composants représentent une avancée significative dans la création de formulaires adaptatifs, ce qui garantit des expériences utilisateur impressionnantes. Cet article décrit l’ancienne approche de la création de formulaires adaptatifs à l’aide de composants de base. </span>

| Version | Lien de l’article |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Cliquez ici](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/configure-layout-of-an-adaptive-form/inline-style-adaptive-forms.html?lang=fr) |
| AEM 6.5 | Cet article |

Vous pouvez définir l’aspect général et le style d’un formulaire adaptatif en spécifiant les styles à l’aide d’un [éditeur de thèmes](../../forms/using/themes.md). En outre, vous pouvez appliquer des styles CSS intégrés à différents composants de formulaire adaptatif et prévisualiser les modifications apportées au fur et à mesure. Les styles intégrés remplacent les styles fournis dans le thème.

## Application des propriétés de style CSS intégré {#apply-inline-css-properties}

Pour ajouter des styles intégrés à un composant :

1. Ouvrez votre formulaire dans l’éditeur de formulaires, puis choisissez le mode Style. Pour passer au mode Style, dans la barre d’outils de la page, sélectionnez ![canvas-drop-down](assets/canvas-drop-down.png) > **Style**.
1. Sélectionnez un composant dans la page, puis sélectionnez le bouton Modifier ![edit-button](assets/edit-button.png). Les propriétés de style s’ouvrent dans la barre latérale.

   Vous pouvez également sélectionner des composants dans l’arborescence de hiérarchie de formulaire dans la barre latérale. L’arborescence de hiérarchie de formulaires est disponible sous forme d’objets de formulaire dans la barre latérale.

   Vous pouvez également sélectionner un composant dans la barre latérale. Dans le mode Style, vous pouvez afficher les composants répertoriés sous Objets de formulaire. Toutefois, la liste Objets de formulaire dans la barre latérale répertorie les composants tels que les champs et les panneaux. Les champs et les panneaux sont des composants génériques qui peuvent contenir des composants tels que des zones de texte et des boutons radio.

   Lorsque vous sélectionnez un composant dans la barre latérale, vous voyez tous les sous-composants répertoriés et les propriétés du composant sélectionné. Vous pouvez sélectionner un sous-composant spécifié et lui appliquer une mise en forme.

1. Cliquez sur un onglet de la barre latérale pour spécifier les propriétés CSS. Vous pouvez définir des propriétés telles que les suivantes :

   * Dimensions et position (paramètre d’affichage, remplissage, hauteur, largeur, marge, position, index z, flottant, clair, débordement)
   * Texte (famille de polices, épaisseur, couleur, taille, hauteur de ligne et alignement)
   * Arrière-plan (image et gradient, couleur d’arrière-plan)
   * Bordure (largeur, style, couleur, rayon)
   * Effets (ombre, opacité)
   * Avancé (permet de saisir un CSS personnalisé pour le composant)

1. De même, vous pouvez appliquer des styles pour d’autres parties d’un composant tels que Widget, Légende et Aide.
1. Sélectionnez **Terminé** pour confirmer les modifications ou sur **Annuler** pour annuler les modifications.

## Exemple : styles intégrés pour un composant de champ {#example-inline-styles-for-a-field-component}

Les images suivantes illustrent une zone de texte avant et après l’application des styles intégrés.

![Composant de zone de texte avant l’application du style intégré](assets/no-style.png)

Composant de zone de texte avant d’appliquer les propriétés de style intégrées

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
   <td><p>Largeur de la bordure = 2 px</p> <p>Style de bordure = plein</p> <p>Couleur de la bordure = #1111</p> </td>
   <td><p>Crée une bordure large noire 2 px autour du champ.</p> </td>
  </tr>
  <tr>
   <td><p>Zone de texte</p> </td>
   <td><p>background-color</p> </td>
   <td><p>#6495ED</p> </td>
   <td><p>Modifie la couleur d’arrière-plan en CornflowerBlue (#6495ED).</p> <p>Remarque : vous pouvez spécifier un nom de couleur ou son code hexadécimal dans le champ Valeur.</p> </td>
  </tr>
  <tr>
   <td><p>Libellé</p> </td>
   <td><p>Dimensions et position &gt; largeur</p> </td>
   <td><p>100 px</p> </td>
   <td><p>Définit la largeur sur 100 px pour le libellé.</p> </td>
  </tr>
  <tr>
   <td>Icône d’aide du champ</td>
   <td>Texte &gt; Couleur de police</td>
   <td>#2ECC40</td>
   <td>Modifie la couleur de la face de l’icône d’aide.</td>
  </tr>
  <tr>
   <td><p>Description longue</p> </td>
   <td><p>text-align</p> </td>
   <td><p>center</p> </td>
   <td><p>Aligne la description longue pour faciliter le centrage.</p> </td>
  </tr>
 </tbody>
</table>

![Style de zone de texte après l’application du style intégré](assets/applied-style.png)

Composant de zone de texte après application des propriétés de style intégré

En suivant les étapes ci-dessus, vous pouvez sélectionner et mettre en forme d’autres composants, tels que les panneaux, les boutons d’envoi et les boutons radio.

>[!NOTE]
>
>Les propriétés de style varient en fonction du composant sélectionné.
