---
title: Création de styles CSS pour des formulaires HTML5
seo-title: Création de styles CSS pour des formulaires HTML5
description: Découvrez comment modifier l’aspect des formulaires HTML5 en modifiant la classe CSS associée à l’élément de formulaire HTML.
seo-description: Découvrez comment modifier l’aspect des formulaires HTML5 en modifiant la classe CSS associée à l’élément de formulaire HTML.
uuid: 43c689b4-243c-43de-a8be-1eef10d75295
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: a8d986ab-2a4c-488b-957e-4606f7391bd3
translation-type: tm+mt
source-git-commit: 56c6cfd437ef185336e81373bd5f758205b96317

---


# Création de styles CSS pour des formulaires HTML5 {#creating-css-styles-for-html-forms}

Le rendu HTML5 d’un modèle de formulaire XFA comporte plusieurs éléments HTML. Ces éléments sont organisés dans un ordre. Chaque élément comporte des classes CSS bien définies. Vous pouvez utiliser cette classe CSS pour sélectionner et modifier l’apparence d’un élément.

>[!NOTE]
>
>Dans les classes CSS, ne modifiez pas les attributs de position et de taille, tels que la largeur, la hauteur, l’épaisseur de la bordure, le haut, la gauche, la droite, le bas, le remplissage et la marge. Modifier les attributs de position et de taille modifie la disposition du formulaire.

## Classes CSS pour les éléments {#css-classes-nbsp-for-elements-nbsp}

Chaque élément contient des classes CSS bien définies. Vous pouvez modifier ces classes pour modifier l’apparence d’un élément. Chaque élément, à l’exception des éléments de champ et de dessin, comporte deux classes CSS –  Type et Nom.

* Le **type classe** représente le type du champ XFA. Vous pouvez remplacer la classe `type`   pour modifier les styles de tous les éléments d’un type donné.

* Le **nom de classe** correspond au nom du champ XFA. You can override the `name` class to modify and apply custom style to an element.

>[!NOTE]
>
>certains éléments de XFA n’ont pas de nom. Pour modifier les styles de ces composants, modifiez tous les éléments de ce type particulier.

Pour les pages non mentionnées dans AEM Forms Designer, les pages d’un formulaire HTML5 sont nommées dans l’ordre croissant de leur numéro. Par exemple, pour un formulaire HTML5 comportant deux pages, les pages sont nommées Page1 et Page2.

## Elément de champ {#field-element}

L’élément de champ contient deux éléments imbriqués : widget et légende.

**Elément widget**

L’élément widget contient l’élément de l’interface utilisateur d’interaction avec les utilisateurs. Il comporte trois classes CSS :

* **Widget**: Chaque widget a cette classe.
* **name**: Tous les widgets fournis avec AEM contiennent la classe de nom du widget. Pour les widgets personnalisés, le développeur de widgets fournit la classe de nom Widget.
* **type**: Chaque widget comporte un élément d’interface utilisateur. Cette classe définit le type de l’élément d’interface utilisateur.

```xml
<!--field with caption-->
<div class="field numericfield NumericField3 ">
     <div class="caption">
        caption content
     </div>
     <div class="widget numericfieldwidget numericInput">
       widget content
     </div>
</div>

<!--field without caption-->
<div class="widget numericfieldwidget numericInput">
   widget content
</div>
```

Outre les classes type et name, le composant de champ contient également une autre classe CSS nommée **subtype**. Un sous-type identifie le type du champ, par exemple, NumericField, DateField, TextField. Vous pouvez remplacer la classe subtype pour modifier le style de tous les champs de type, sous-type.

## Classes CSS des différents composants {#css-classes-for-different-components}

<table>
 <tbody>
  <tr>
   <td><strong>Composant</strong></td>
   <td><strong>Type</strong></td>
   <td><strong>Name (Nom)</strong></td>
  </tr>
  <tr>
   <td>Page</td>
   <td>page</td>
   <td>Nom défini par l’utilisateur<br /> ou<br /> Page&lt;pageNumber&gt; (valeur par défaut)</td>
  </tr>
  <tr>
   <td>Zone de contenu</td>
   <td>contentarea</td>
   <td>Nom défini par l’utilisateur</td>
  </tr>
  <tr>
   <td>Sous-formulaire</td>
   <td>sous-formulaire</td>
   <td>Nom défini par l’utilisateur</td>
  </tr>
  <tr>
   <td>Groupe d’exclusion</td>
   <td>exclgroup</td>
   <td>Nom défini par l’utilisateur</td>
  </tr>
  <tr>
   <td>Dessin</td>
   <td>draw</td>
   <td>Nom défini par l’utilisateur</td>
  </tr>
  <tr>
   <td>Field (Champ)</td>
   <td>field</td>
   <td>Nom défini par l’utilisateur</td>
  </tr>
  <tr>
   <td>Légende</td>
   <td>caption</td>
   <td>N/A</td>
  </tr>
  <tr>
   <td>Widget</td>
   <td>widget</td>
   <td>Le développeur du widget le définit (pour les widgets définis par l’utilisateur, voir le tableau de la section suivante)</td>
  </tr>
 </tbody>
</table>

## Classes CSS des différents champs {#css-classes-for-different-fields}

AEM Forms Designer prend en charge différents types de champs d’un formulaire, tels que NumericField, DecimalField et le champ Date. Tous ces champs au format HTML contiennent les classes CSS mentionnées ci-dessus. Ils contiennent également certaines classes supplémentaires selon le type de zone.

Chaque champ contient un widget associé qui représente l’élément de l’interface utilisateur. Les classes de chaque champ et les widgets associés à chaque champ sont répertoriés ci-dessous.

<table>
 <tbody>
  <tr>
   <td><strong>Type de champ</strong></td>
   <td><strong>Sous-type</strong></td>
   <td><strong>Nom du widget</strong></td>
   <td><strong>Type de widget</strong></td>
   <td><strong>Balise d’interface utilisateur HTML</strong></td>
  </tr>
  <tr>
   <td>Bouton<br type="_moz" /> </td>
   <td>N/A</td>
   <td>xfaButton<br type="_moz" /> </td>
   <td>buttonfieldwidget<br type="_moz" /> </td>
   <td>input type=button<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>CheckButton<br type="_moz" /> </td>
   <td>checkboxfield<br /> </td>
   <td>XfaCheckBox<br type="_moz" /> </td>
   <td>checkboxfieldwidget<br type="_moz" /> </td>
   <td>input type=checkbox<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>DateField<br type="_moz" /> </td>
   <td>datefield<br type="_moz" /> </td>
   <td>dateField<br type="_moz" /> </td>
   <td>datefieldwidget<br type="_moz" /> </td>
   <td>input type=text<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>DateTimeField<br type="_moz" /> </td>
   <td>textfield<br type="_moz" /> </td>
   <td>textField<br type="_moz" /> </td>
   <td>textfieldwidget</td>
   <td>input type=text<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>DecimalField<br type="_moz" /> </td>
   <td>numericfield<br type="_moz" /> </td>
   <td>numericInput<br type="_moz" /> </td>
   <td>numericfieldwidget<br type="_moz" /> </td>
   <td>input type=text<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>DropDown<br type="_moz" /> </td>
   <td>choicelist<br type="_moz" /> </td>
   <td>dropDownListWidget<br type="_moz" /> </td>
   <td>choicelistwidget<br type="_moz" /> </td>
   <td>select</td>
  </tr>
  <tr>
   <td>ListBox<br type="_moz" /> </td>
   <td>choicelist<br type="_moz" /> </td>
   <td>listBoxWidget<br type="_moz" /> </td>
   <td>choicelistwidget<br type="_moz" /> </td>
   <td>ol</td>
  </tr>
  <tr>
   <td>NumericField<br type="_moz" /> </td>
   <td>numericfield<br type="_moz" /> </td>
   <td>numericInput<br type="_moz" /> </td>
   <td>numericfieldwidget<br type="_moz" /> </td>
   <td>input type=text<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>PasswordField<br type="_moz" /> </td>
   <td>passwordfield<br type="_moz" /> </td>
   <td>defaultWidget<br type="_moz" /> </td>
   <td>passwordfieldwidget<br type="_moz" /> </td>
   <td>input type=password<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>RadioButton<br type="_moz" /> </td>
   <td>radiofield<br type="_moz" /> </td>
   <td>XfaCheckBox<br type="_moz" /> </td>
   <td>radiofieldwidget<br type="_moz" /> </td>
   <td>input type=radio<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>TextField<br type="_moz" /> </td>
   <td>textfield<br type="_moz" /> </td>
   <td>textField<br type="_moz" /> </td>
   <td>textfieldwidget<br type="_moz" /> </td>
   <td>input type=text<br type="_moz" /> </td>
  </tr>
  <tr>
   <td>TimeField<br type="_moz" /> </td>
   <td>textfield<br type="_moz" /> </td>
   <td>textField<br type="_moz" /> </td>
   <td>textfieldwidget<br type="_moz" /> </td>
   <td>input type=text<br type="_moz" /> </td>
  </tr>
 </tbody>
</table>

## Classes CSS des différents éléments de dessin {#css-classes-for-different-draw-elements}

Vous pouvez insérer des éléments statiques de dessin comme un texte et des images à l’aide d’AEM Forms Designer. Pour chaque élément de dessin, une classe CSS distincte est associée à cet élément. La liste des classes CSS des éléments de dessin est répertoriée ci-dessous. Une classe de dessin est associée à chaque élément de dessin.

| **Type de dessin** | **Classe CSS** |
|---|---|
| Text (Texte) | text |
| Image | image |
| Rectangle | rectangle |
| Ligne | line |

## Style des autres parties du formulaire {#styling-other-parts-of-the-form}

Outre l’aspect des composants de l’interface utilisateur dans le formulaire HTML, vous pouvez modifier le style des éléments tels que les erreurs en ligne, les avertissements en ligne et les champs contenant des erreurs de validation.

`Styling Inline Errors`

Lorsque la validation d’un champ aboutit à une erreur, une erreur en ligne est affichée lorsque le champ est actif. Pour modifier le style des erreurs en ligne, remplacez l’ID CSS **error-msg**.

`Styling Inline Warnings`

Lorsque la validation d’un champ résulte en un avertissement, un avertissement en ligne s’affiche lorsque le champ est actif. Pour modifier le style de ces avertissements en ligne, remplacez l’ID CSS **warning-msg**.

`Styling Fields with Validation Errors`

Lorsque la fonction de validation d’un champ échoue, le style du widget change. This style change is done by applying a CSS class **widgetError** on the widget component. To modify the default styling, override the **widgetError** class.
