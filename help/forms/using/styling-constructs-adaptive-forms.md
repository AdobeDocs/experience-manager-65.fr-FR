---
title: Mise en forme des éléments pour les formulaires adaptatifs
seo-title: Mise en forme des éléments pour les formulaires adaptatifs
description: La structure LESS permet de personnaliser l’aspect des formulaires adaptatifs.
seo-description: La structure LESS permet de personnaliser l’aspect des formulaires adaptatifs.
uuid: d2e45ad9-7322-43ce-a1dd-ad97e2eea742
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
discoiquuid: ed50fa70-a8dd-4cc6-82a9-d59de0fa417d
docset: aem65
feature: Formulaires adaptatifs
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '2324'
ht-degree: 89%

---


# Mise en forme des éléments pour les formulaires adaptatifs{#styling-constructs-for-adaptive-forms}

## Conditions préalables {#prerequisites}

Connaissances en matière de CSS et structure LESS.

## Eléments personnalisables {#what-can-be-customized}

Cet article répertorie les classes CSS de formulaires adaptatifs accessibles au public. Vous pouvez exploiter ces classes pour mettre en forme différents composants d’un formulaire adaptatif. La définition de style des composants de création, tels que les boîtes de dialogue et les barres d’état qui affichent des avertissements, ne rentre pas dans le cadre de cet article. Utilisez ces mises en forme des éléments pour créer des styles (en utilisant CSS ou Less) uniquement lorsque vous ne pouvez pas appliquer un style aux composants à l’aide de l’[éditeur de thèmes](https://helpx.adobe.com/fr/experience-manager/6-3/forms/using/themes.html).

## Personnalisation des styles dans les formulaires adaptatifs {#customizing-styles-in-adaptive-forms}

La structure LESS simplifie l’utilisation pour personnaliser les styles dans les formulaires adaptatifs. La structure vous permet de définir des styles à l’aide d’un ensemble de variables et de fonctions (mixins). La structure LESS aide à réduire la taille du code imbriqué et augmente sa capacité de réutilisation.

Vous pouvez personnaliser les styles des formulaires adaptatifs des manières suivantes :

* Modification du thème
* Modification du style d’un composant

## Modification du thème  {#changing-theme}

Vous pouvez modifier le thème d’un formulaire adaptatif pour vous assurer que son aspect est cohérent avec les pages Web sur lesquelles le formulaire adaptatif est incorporé.

Les modifications de l’aspect général du formulaire adaptatif via les propriétés CSS font généralement partie des modifications du thème. Les modifications majeures apportées au &quot;ok and entiment&quot; du formulaire adaptatif, telles que les modifications de la disposition et du placement des composants, ne sont pas considérées comme des modifications de thème.

Selon l’amorçage, l’ensemble suivant de propriétés CSS définit le thème d’une page Web :

* Couleur de fond
* Bordure (type, couleur, épaisseur)
* Couleur de la police
* Remplissage
* Marge
* Taille de la police
* Hauteur de ligne

Actuellement, les variables LESS sont définies uniquement pour ces propriétés des différents éléments dans un formulaire adaptatif.

## Modification du style de composant  {#changing-component-style}

Vous pouvez modifier l’apparence, la disposition, le positionnement et la visibilité des éléments. Pour obtenir cette tâche, créez ou mettez à jour vos fichiers .css personnalisés afin d’inclure les éléments de style répertoriés dans cet article.

Pour appliquer un style à un formulaire adaptatif, ouvrez le formulaire adaptatif pour l’édition, ouvrez les propriétés du conteneur de formulaires adaptatifs et spécifiez le chemin du fichier CSS personnalisé dans l’onglet de base. Mises en forme par défaut du formulaire adaptatif remplacé par les mises en forme répertoriées dans le fichier .css personnalisé.

## Composants {#components}

Les composants décrits dans cet article ont leurs classes CSS prédéfinies. Vous pouvez modifier les variables pour modifier les styles dans les classes CSS. Sinon, vous pouvez réécrire la classe entière. Cette section décrit les classes dans les composants et les styles que vous pouvez modifier à l’aide de variables.

## Définition de style du conteneur {#container-styling}

Un conteneur est le composant de niveau supérieur. D’autres panneaux et champs se trouvent sous le composant de conteneur.

<table>
 <tbody>
  <tr>
   <td><p><strong>Classe CSS </strong></p> </td>
   <td><p><code>guideContainerNode</code></p> </td>
  </tr>
 </tbody>
</table>

<table>
 <tbody>
  <tr>
   <td><p><strong>Description des variables</strong></p> </td>
   <td><p><strong>Description des variables</strong></p> </td>
  </tr>
  <tr>
   <td><p><code>container-bgColor</code></p> </td>
   <td><p>Couleur d’arrière-plan du conteneur</p> </td>
  </tr>
  <tr>
   <td><p><code>container-padding</code></p> </td>
   <td><p>Marge intérieure du conteneur</p> </td>
  </tr>
  <tr>
   <td><p><code>container-margin</code></p> </td>
   <td><p>Marge du conteneur</p> </td>
  </tr>
  <tr>
   <td><p><code>container-fontColor</code></p> </td>
   <td><p>Couleur de police du conteneur</p> </td>
  </tr>
 </tbody>
</table>

## Définition de style du champ {#field-styling}

Les formulaires adaptatifs incluent divers types de champs. Chaque champ a un nom de classe unique, qui est le nom du champ. Le champ a également un nom de classe commun `guideFieldNode`.

Les champs incluent des libellés, des widgets, des descriptions d’aide (descriptions longues et courtes), ainsi que des icônes d’aide de champ (point d’interrogation).

<table>
 <tbody>
  <tr>
   <td><p><strong>Classe CSS </strong></p> </td>
   <td><p><code>guideFieldNode</code></p> </td>
  </tr>
 </tbody>
</table>

<table>
 <tbody>
  <tr>
   <td><p><strong>Variables </strong></p> </td>
   <td><p><strong>Description</strong></p> </td>
  </tr>
  <tr>
   <td><p><code>field-padding</code><strong></strong></p> </td>
   <td><p>Marge intérieure du champ</p> </td>
  </tr>
  <tr>
   <td><p><code>field-error-font-color</code></p> </td>
   <td><p>Couleur de police du message d’erreur du champ</p> </td>
  </tr>
  <tr>
   <td><p><code>field-error-font-size</code></p> </td>
   <td><p>Taille de police du message d’erreur du champ</p> </td>
  </tr>
 </tbody>
</table>

## Définition de style de libellé {#label-styling}

L’élément HTML **label** utilisé pour le champ comprend les classes **left** ou **top** selon que l’étiquette se trouve en haut ou à gauche.

<table>
 <tbody>
  <tr>
   <td><p><strong>Classe CSS </strong></p> </td>
   <td><p><code>guideFieldLabel</code></p> </td>
  </tr>
 </tbody>
</table>

<table>
 <tbody>
  <tr>
   <td><p><strong>Variables </strong></p> </td>
   <td><p><strong>Description</strong></p> </td>
  </tr>
  <tr>
   <td><p><code>label-font-color</code></p> </td>
   <td><p>Couleur de police du libellé du champ</p> </td>
  </tr>
  <tr>
   <td><p><code>label-font-size</code></p> </td>
   <td><p>Taille de police du libellé du champ</p> </td>
  </tr>
  <tr>
   <td><p><code>label-line-height</code></p> </td>
   <td>Propriété de hauteur de ligne CSS pour le libellé du champ </td>
  </tr>
  <tr>
   <td><p><code>label-font-weight</code></p> </td>
   <td>Propriété d’épaisseur de police CSS du libellé du champ </td>
  </tr>
  <tr>
   <td><p><code>label-margin</code></p> </td>
   <td><p>Marge du libellé du champ</p> </td>
  </tr>
 </tbody>
</table>

Les règles CSS de l’étiquette sont appliquées à l’aide de l’étiquette **guideFieldLabel**. Si vous êtes un auteur, remplacez cette règle pour que vos modifications personnalisées soient visibles.

## Définition de style des widgets {#widgets-styling}

Selon leur type, les widgets contiennent également des classes. En règle générale, les widgets incluent la classe `guideFieldWidget`. Les widgets fournis avec HTML utilisent normalement les éléments HTML standard input et select. La définition de style s’effectue en conséquence. Vous ne pouvez pas modifier le style d’un widget personnalisé en modifiant les variables.

<table>
 <tbody>
  <tr>
   <td><p><strong>Classe CSS </strong></p> </td>
   <td><p><code>guideFieldWidget</code></p> </td>
  </tr>
 </tbody>
</table>

<table>
 <tbody>
  <tr>
   <td><p><strong>Variables <code></code></strong></p> </td>
   <td><p><strong>Description</strong></p> </td>
  </tr>
  <tr>
   <td><p><code>widgets-bg-color</code></p> </td>
   <td>Couleur d’arrière-plan des widgets (ne fonctionne pas pour les cases à cocher et les boutons radio)</td>
  </tr>
  <tr>
   <td><p><code>widgets-border-color</code></p> </td>
   <td><p>Couleur de bordure des widgets</p> </td>
  </tr>
  <tr>
   <td><p><code>widgets-border-thickness</code></p> </td>
   <td><p>Taille de bordure des widgets</p> </td>
  </tr>
  <tr>
   <td><p><code>widgets-border-radius</code></p> </td>
   <td><p>Rayon de bordure des widgets</p> </td>
  </tr>
  <tr>
   <td><p><code>widgets-border-type</code></p> </td>
   <td><p>Type de bordure des widgets</p> </td>
  </tr>
  <tr>
   <td><p><code>widget-border-focus-type</code></p> </td>
   <td><p>Type de focus des bordures de widget</p> </td>
  </tr>
  <tr>
   <td><p><code>widgets-border</code></p> </td>
   <td><p>Style de bordure consolidée des widgets</p> </td>
  </tr>
  <tr>
   <td><p><code>widgets-font-color</code></p> </td>
   <td><p>Couleur du texte dans le widget</p> </td>
  </tr>
  <tr>
   <td><p><code>widgets-font-size</code></p> </td>
   <td><p>Taille du texte dans le widget</p> </td>
  </tr>
  <tr>
   <td><p><code>widgets-line-height</code></p> </td>
   <td>Propriété de hauteur de ligne CSS du widget </td>
  </tr>
  <tr>
   <td><p><code>widgets-padding</code></p> </td>
   <td><p>Propriété de remplissage CSS du widget</p> </td>
  </tr>
  <tr>
   <td><p><code>widgets-focus-border-color</code></p> </td>
   <td><p>Couleur de bordure lorsque le widget est ciblé</p> </td>
  </tr>
  <tr>
   <td><p><code>widgets-mandatory-border-color</code></p> </td>
   <td><p>Couleur de bordure du widget pour les champs obligatoires</p> </td>
  </tr>
  <tr>
   <td><p><code>widgets-mandatory-bg-color</code></p> </td>
   <td><p>Couleur d’arrière-plan du widget pour les champs obligatoires</p> </td>
  </tr>
  <tr>
   <td><p><code>widgets-disabled-bg-color</code></p> </td>
   <td><p>Couleur d’arrière-plan du widget lorsque le champ est désactivé</p> </td>
  </tr>
  <tr>
   <td><p><code>widgets-disabled-font-color</code></p> </td>
   <td><p>Couleur de police du widget lorsque le champ est désactivé</p> </td>
  </tr>
  <tr>
   <td><p><code>widgets-disabled-border-color</code></p> </td>
   <td><p>Couleur de bordure du widget lorsque le champ est désactivé</p> </td>
  </tr>
  <tr>
   <td><p><code>widget-height</code></p> </td>
   <td>Hauteur du widget (ne fonctionne pas pour les cases à cocher et les boutons radio)</td>
  </tr>
  <tr>
   <td><p><code>checkbutton-height</code></p> </td>
   <td><p>Hauteur de la case à cocher et du bouton radio.</p> </td>
  </tr>
  <tr>
   <td><p><code>listboxwidget-height</code></p> </td>
   <td><p>Hauteur maximale d’une liste déroulante à sélection multiple</p> </td>
  </tr>
 </tbody>
</table>

### Restrictions de la définition de style de widget  {#limitations-in-widget-styling}

La définition du style des champs ciblés, obligatoires et désactivés est limitée à l’aide de variables. Toutefois, vous pouvez le modifier en remplaçant les styles. La restriction à l’aide de variables est fournie principalement pour garder un œil sur le nombre de variables. La restriction peut être assouplie si l’aspect d’un champ change radicalement car il se trouve dans l’un des états décrits précédemment.

## Description d’aide {#help-description}

Un auteur peut spécifier le contenu d’aide dans les champs à l’aide de composants de descriptions longue et courte. Les deux composants ont une classe commune `.guideHelpDescription` et une autre classe `.long`/ `.short`, selon le type de description. Le contenu d’aide est intégré dans un élément de paragraphe pour remplacer la définition de style de la description. La description d’aide (longue et courte) est modifiée à l’aide de variables commençant par widgetshelp, comme indiqué dans le tableau suivant :

<table>
 <tbody>
  <tr>
   <td><p><strong>Variables </strong></p> </td>
   <td><p><strong>Description</strong></p> </td>
  </tr>
  <tr>
   <td><p><code>widgets-help-long-bg-color</code></p> </td>
   <td><p>Couleur d’arrière-plan de l’aide longue des widgets</p> </td>
  </tr>
  <tr>
   <td><p><code>widgets-help-long-border-color</code></p> </td>
   <td><p>Couleur de bordure de l’aide longue des widgets</p> </td>
  </tr>
  <tr>
   <td><p><code>widgets-help-long-border-indicator-color</code></p> </td>
   <td><p>Couleur de bordure d’indicateur gauche de l’aide longue des widgets</p> </td>
  </tr>
  <tr>
   <td><p><code>widgets-help-short-bg-color</code></p> </td>
   <td><p>Couleur d’arrière-plan de l’aide courte des widgets</p> </td>
  </tr>
  <tr>
   <td><p><code>widgets-help-short-color</code></p> </td>
   <td><p>Couleur de police de l’aide courte des widgets</p> </td>
  </tr>
  <tr>
   <td><p><code>widgets-help-short-tooltip-bg-color</code></p> </td>
   <td><p>Couleur d’arrière-plan de l’info-bulle d’aide courte des widgets</p> </td>
  </tr>
  <tr>
   <td><p><code>widgets-help-short-tooltip-color</code></p> </td>
   <td><p>Couleur de police de l’info-bulle d’aide courte des widgets</p> </td>
  </tr>
 </tbody>
</table>

## Termes et conditions  {#terms-and-conditions}

Le widget des termes et conditions (TnC`` ``) vous permet de spécifier les termes et conditions. Vous pouvez personnaliser le widget à l’aide des variables décrites dans le tableau suivant.

<table>
 <tbody>
  <tr>
   <td><p><strong>Variables </strong></p> </td>
   <td><p><strong>Description</strong></p> </td>
  </tr>
  <tr>
   <td><code>tnc-unvisited</code></td>
   <td>Couleur de police du lien TnC non visité.</td>
  </tr>
  <tr>
   <td><code>tnc-visited</code></td>
   <td>Couleur de police du lien TnC visité.</td>
  </tr>
 </tbody>
</table>

## Bouton {#button}

Les boutons sont également des widgets. Toutefois, leur définition de style est légèrement différente des widgets. Dans les formulaires adaptatifs, n’importe lequel des éléments suivants constitue un bouton :

* input[type = text]
* button
* élément avec la classe .button

Code HTML du bouton :

`<button type="button" >`

`<span class="iconButtonicon"></`

`span>`

`<span class="iconButtonlabel"></`

`span>`

`</button>`

<table>
 <tbody>
  <tr>
   <td><p><strong>Classe CSS</strong></p> </td>
   <td><p><strong>Description</strong></p> </td>
  </tr>
  <tr>
   <td><p><code>iconButton-icon</code></p> </td>
   <td><p>Fournit des icônes pour le bouton</p> </td>
  </tr>
  <tr>
   <td><p><code>iconButton-label</code></p> </td>
   <td><p>Définit le style du libellé/de la légende du bouton</p> </td>
  </tr>
 </tbody>
</table>

<table>
 <tbody>
  <tr>
   <td><p><strong>Variables <code></code></strong></p> </td>
   <td><p><strong>Description</strong></p> </td>
  </tr>
  <tr>
   <td><p><code>button-border-size</code></p> </td>
   <td><p>Taille de bordure des boutons</p> </td>
  </tr>
  <tr>
   <td><p><code>button-border-type</code></p> </td>
   <td><p>Type de bordure</p> </td>
  </tr>
  <tr>
   <td><p><code>button-padding</code></p> </td>
   <td><p>Propriété de remplissage CSS du bouton</p> </td>
  </tr>
  <tr>
   <td><p><code>button-font-size</code></p> </td>
   <td><p>Taille de police du bouton</p> </td>
  </tr>
  <tr>
   <td><p><code>button-background-color</code></p> </td>
   <td><p>Couleur d’arrière-plan du bouton</p> </td>
  </tr>
  <tr>
   <td><p><code>button-font-color</code></p> </td>
   <td><p>Couleur de police du bouton</p> </td>
  </tr>
  <tr>
   <td><p><code>button-border-color</code></p> </td>
   <td><p>Couleur de bordure du bouton</p> </td>
  </tr>
  <tr>
   <td><p><code>button-large-padding</code></p> </td>
   <td><p>Marge intérieure des grands boutons (boutons avec la classe .buttonlarge)</p> </td>
  </tr>
  <tr>
   <td><p><code>button-large-font-size</code></p> </td>
   <td><p>Taille de police des grands boutons</p> </td>
  </tr>
  <tr>
   <td><p><code>button-small-padding</code></p> </td>
   <td><p>Marge intérieure des petits boutons (boutons avec la classe .buttonsmall)</p> </td>
  </tr>
  <tr>
   <td><p><code>button-small-font-size</code></p> </td>
   <td><p>Taille de police des petits boutons</p> </td>
  </tr>
  <tr>
   <td><p><code>button-info-background-color</code></p> </td>
   <td><p>Couleur d’arrière-plan des boutons informatifs (boutons avec la classe .buttoninformative)</p> </td>
  </tr>
  <tr>
   <td><p><code>button-info-font-color</code></p> </td>
   <td><p>Couleur de police des boutons informatifs</p> </td>
  </tr>
  <tr>
   <td><p><code>button-info-border-color</code></p> </td>
   <td><p>Couleur de bordure des boutons informatifs</p> </td>
  </tr>
  <tr>
   <td><p><code>button-warning-background-color</code></p> </td>
   <td><p>Couleur d’arrière-plan des boutons d’avertissement (boutons avec la classe .buttonwarning)</p> </td>
  </tr>
  <tr>
   <td><p><code>button-warning-font-color</code></p> </td>
   <td><p>Couleur de police des boutons d’avertissement</p> </td>
  </tr>
  <tr>
   <td><p><code>button-warning-border-color</code></p> </td>
   <td><p>Couleur de bordure des boutons d’avertissement</p> </td>
  </tr>
  <tr>
   <td><p><code>button-alert-background-color</code></p> </td>
   <td><p>Couleur d’arrière-plan des boutons d’alerte (boutons avec la classe .buttonalert)</p> </td>
  </tr>
  <tr>
   <td><p><code>button-alert-font-color</code></p> </td>
   <td><p>Couleur de police des boutons d’alerte</p> </td>
  </tr>
  <tr>
   <td><p><code>button-alert-border-color</code></p> </td>
   <td><p>Couleur de bordure des boutons d’alerte</p> </td>
  </tr>
 </tbody>
</table>

## Point d’interrogation {#question-mark}

Pour les widgets, un point d’interrogation est affiché lorsque l’auteur ajoute une description longue dans le contenu d’aide. L’icône par défaut fournie dans l’amorçage est utilisée. Pour utiliser une icône personnalisée, vous pouvez personnaliser les icônes de l’amorçage.

<table>
 <tbody>
  <tr>
   <td><p><strong>Classe CSS </strong></p> </td>
   <td><p><code>guideHelpQuestionMark</code></p> </td>
  </tr>
 </tbody>
</table>

<table>
 <tbody>
  <tr>
   <td><p><strong>Variables </strong></p> </td>
   <td><p><strong>Description</strong></p> </td>
  </tr>
  <tr>
   <td><p><code>questionmark-font-color</code></p> </td>
   <td><p>Couleur de l’icône</p> </td>
  </tr>
  <tr>
   <td><p><code>questionmark-hover-font-color</code></p> </td>
   <td><p>Couleur de l’icône lorsque le curseur survole au-dessus</p> </td>
  </tr>
 </tbody>
</table>

## Tableau {#table}

Vous pouvez modifier le thème de couleur de l’en-tête et des rangées de contenu d’un tableau en utilisant les variables suivantes.

<table>
 <tbody>
  <tr>
   <td><p><strong>Variables </strong></p> </td>
   <td><p><strong>Description</strong></p> </td>
  </tr>
  <tr>
   <td><p><code>table-header-bg-color</code></p> </td>
   <td><p>Couleur d’arrière-plan de la barre d’en-tête. La valeur par défaut est <code>#333</code>.<br /> </p> </td>
  </tr>
  <tr>
   <td><p><code>table-odd-row-bg-color</code></p> </td>
   <td><p>Couleur d’arrière-plan de la ligne de contenu impaire. La valeur par défaut est <code>rgb(255, 255, 255)</code>.</p> </td>
  </tr>
  <tr>
   <td><p><code>table-even-row-bg-color</code></p> </td>
   <td><p>Couleur d’arrière-plan pour la ligne de contenu paire. La valeur par défaut est <code>#eee</code>.</p> </td>
  </tr>
 </tbody>
</table>

## Pièce jointe {#file-attachment}

Le widget de pièce jointe des formulaires adaptatifs vous permet de télécharger des fichiers. Vous pouvez également personnaliser le widget à l’aide des variables.

<table>
 <tbody>
  <tr>
   <td><p><strong>Variables </strong></p> </td>
   <td><p><strong>Description</strong></p> </td>
  </tr>
  <tr>
   <td><p><code>fileItemPadding</code></p> </td>
   <td><p>Marge intérieure pour les fichiers affichés dans le widget</p> </td>
  </tr>
  <tr>
   <td><p><code>fileItemBackground</code></p> </td>
   <td><p>Couleur d’arrière-plan pour l’élément de fichier</p> </td>
  </tr>
  <tr>
   <td><p><code>fileItemBorderColor</code></p> </td>
   <td><p>Couleur de bordure de la bordure supérieure</p> </td>
  </tr>
  <tr>
   <td><p><code>fileItemColor</code></p> </td>
   <td><p>Couleur de police pour l’élément de fichier</p> </td>
  </tr>
  <tr>
   <td><p><code>filePreviewIconColor</code></p> </td>
   <td><p>Couleur de l’icône d’aperçu (icône d’amorçage) dans le widget</p> </td>
  </tr>
  <tr>
   <td><p><code>fileItemCommentHeight</code></p> </td>
   <td><p>Hauteur de commentaire pour l’élément de fichier</p> </td>
  </tr>
 </tbody>
</table>

## Styles de navigateur  {#navigator-styles}

Il existe quatre types d’onglet de navigateur. Il s’agit des onglets sur la gauche, en haut, de l’assistant et en accordéon. Chaque navigateur possède une classe différente.

<table>
 <tbody>
  <tr>
   <td><p><strong>Navigateur</strong></p> </td>
   <td><p><strong>Classe CSS</strong></p> </td>
  </tr>
  <tr>
   <td><p><code>Accordion</code></p> </td>
   <td><p>.accordion-navigators</p> </td>
  </tr>
  <tr>
   <td><p><code>tabs on the left</code></p> </td>
   <td><p>.tab-navigators-vertical</p> </td>
  </tr>
  <tr>
   <td><p><code>tabs on the top</code></p> </td>
   <td><p>.tab-navigators</p> </td>
  </tr>
  <tr>
   <td><p><code>Wizard</code></p> </td>
   <td><p>.wizard-navigators</p> </td>
  </tr>
 </tbody>
</table>

Voici le code HTML pour l’élément de navigateur d’onglet (similaire aux onglets d’amorçage) :

`<li>`

`<a>tab title</a>`

`</li>`

`Accordion navigator is an exception, it has following barebone`

`structure:`

`<div class="accordion.navigators">`

`<div>`

`<div class = "guideHeader">`

`<a>`

`<span class = "guideSummary" ></code>`

`........................... repeatable buttons, if the repeatable configuration is set ................................`

`<div class = "repeatableButtons">`

`<button name="Add" class="Add"/>`

`<button name="Remove" class="Remove"/>`

`</div>`

`</a>`

`</div>`

`................................ panel content ..................................`

`</div>`

`</div>`

Vous pouvez modifier la définition de style du navigateur à l’aide des règles CSS qui sélectionnent les éléments à l’aide de sélecteurs **descendants.** Par exemple, pour ajouter un style textdecoration à la balise d’ancrage :

Navigateur d’onglets en haut :

`.tab-navigators`

`li a {`

`text-decoration:`

`underline;`

`}`

`Tab navigator on left:`

`.tab-navigators-vertical`

`li a {`

`text-decoration:`

`underline;`

`}`

`Accordion navigator:`

`.accordion-navigators .guideHeader a .guideSummary {`

`text-decoration:`

`underline;`

`}`

`Wizard navigator:`

`.wizard-navigators`

`li a {`

`text-decoration:`

`underline;`

`}`

En outre, il existe des classes pour définir le style des navigateurs d’onglets (gauche et haut) en fonction de la présence de navigateurs imbriqués ou enfants ou de sous-navigateurs.

<table>
 <tbody>
  <tr>
   <td><p><strong>Classe CSS</strong></p> </td>
   <td><p><strong>Description</strong></p> </td>
  </tr>
  <tr>
   <td><p><code>nested_true</code></p> </td>
   <td><p>Navigateurs d’onglets (gauche et haut) qui ont des navigateurs imbriqués/enfants/sous-navigateurs</p> </td>
  </tr>
  <tr>
   <td><p><code>nested_false</code></p> </td>
   <td><p>Navigateurs d’onglets (gauche et haut) qui n’ont pas de navigateur imbriqué/enfant/sous-navigateur</p> </td>
  </tr>
 </tbody>
</table>

La classe guideNavIcon fournit une icône par défaut aux navigateurs d’onglets (gauche et haut) et aux navigateurs de l’assistant.

<table>
 <tbody>
  <tr>
   <td><p><strong>Classe CSS </strong></p> </td>
   <td><p><code>guideNavIcon</code></p> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>Vous pouvez modifier l’icône pour un navigateur particulier en fournissant une classe CSS dans le panneau de création, par exemple &lt;CLASS_NAME>. Vous ajoutez **&lt;CLASS_NAME>_nav** pour l’icône du navigateur.

<table>
 <tbody>
  <tr>
   <td><p><strong>Variables </strong></p> </td>
   <td><p><strong>Description</strong></p> </td>
  </tr>
  <tr>
   <td><p><strong>Navigateurs d’onglets</strong></p> </td>
   <td><p> </p> </td>
  </tr>
  <tr>
   <td><p><code>navigator-bg-color</code></p> </td>
   <td><p>Couleur d’arrière-plan du navigateur d’onglets entier</p> </td>
  </tr>
  <tr>
   <td><p><code>tabs-bg-color</code></p> </td>
   <td><p>Couleur d’arrière-plan de l’onglet</p> </td>
  </tr>
  <tr>
   <td><p><code>tabs-font-color</code></p> </td>
   <td><p>Couleur de police de l’onglet</p> </td>
  </tr>
  <tr>
   <td><p><code>tabs-hover-bg-color</code></p> </td>
   <td><p>Couleur d’arrière-plan de l’onglet au survol</p> </td>
  </tr>
  <tr>
   <td><p><code>tabs-hover-font-color</code></p> </td>
   <td><p>Couleur de police de l’onglet au survol</p> </td>
  </tr>
  <tr>
   <td><p><code>tabs-active-bg-color</code></p> </td>
   <td><p>Couleur d’arrière-plan lorsque le panneau est ciblé (actif)</p> </td>
  </tr>
  <tr>
   <td><p><code>tabs-active-font-color</code></p> </td>
   <td><p>Couleur de police lorsque le panneau est actif</p> </td>
  </tr>
  <tr>
   <td><p><code>tabs-completed-bg-color</code></p> </td>
   <td><p>Couleur d’arrière-plan lorsque l’expression d’achèvement du panneau renvoie true (vrai) </p> </td>
  </tr>
  <tr>
   <td><p><code>tabs-completed-font-color</code></p> </td>
   <td><p>Couleur de police lorsque l’expression d’achèvement du panneau renvoie true (vrai) </p> </td>
  </tr>
  <tr>
   <td><p><code>tabs-stepped-bg-color</code></p> </td>
   <td>Couleur d’arrière-plan lorsque le panneau a été activé une fois mais que l’expression d’achèvement renvoie false (faux) </td>
  </tr>
  <tr>
   <td><p><code>tabs-stepped-font-color</code></p> </td>
   <td>Couleur de police lorsque le panneau a été activé une fois mais que l’expression d’achèvement renvoie false (faux) </td>
  </tr>
  <tr>
   <td><p><code>tabs-border-color</code></p> </td>
   <td><p>Couleur de bordure de l’onglet</p> </td>
  </tr>
  <tr>
   <td><p><code>tabs-font-size</code></p> </td>
   <td><p>Taille de police de l’onglet</p> </td>
  </tr>
  <tr>
   <td><p><code>tabs-padding</code></p> </td>
   <td><p>Marge intérieure de l’onglet</p> </td>
  </tr>
  <tr>
   <td><p><code>tabs-margin</code></p> </td>
   <td><p>Marge de l’onglet</p> </td>
  </tr>
  <tr>
   <td><p><code>tabs-vertical-margin</code></p> </td>
   <td><p>Marge des onglets verticaux</p> </td>
  </tr>
  <tr>
   <td><p><code>tabs-border-thickness</code></p> </td>
   <td><p>Taille de bordure des onglets</p> </td>
  </tr>
  <tr>
   <td><p><code>tabs-min-height</code></p> </td>
   <td><p>Hauteur minimale des onglets</p> </td>
  </tr>
  <tr>
   <td><p><code>heirarichal-indent</code></p> </td>
   <td><p>Retrait des onglets imbriqués</p> </td>
  </tr>
  <tr>
   <td><p><strong>Navigateurs de l’assistant</strong></p> </td>
   <td><p> </p> </td>
  </tr>
  <tr>
   <td><p><code>wizard-navigator-bg-color</code></p> </td>
   <td>Couleur d’arrière-plan du navigateur entier de l’assistant</td>
  </tr>
  <tr>
   <td><p><code>wizard-tabs-bg-color</code></p> </td>
   <td><p>Couleur d’arrière-plan de l’assistant</p> </td>
  </tr>
  <tr>
   <td><p><code>wizard-tabs-font-color</code></p> </td>
   <td><p>Couleur de police de l’assistant</p> </td>
  </tr>
  <tr>
   <td><p><code>wizard-tabs-active-bg-color</code></p> </td>
   <td><p>Couleur d’arrière-plan lorsque le panneau est ciblé (actif)</p> </td>
  </tr>
  <tr>
   <td><p><code>wizard-tabs-active-font-color</code></p> </td>
   <td><p>Couleur de la police lorsque le panneau est ciblé (actif)</p> </td>
  </tr>
  <tr>
   <td><p><code>wizard-tabs-completed-bg-color</code></p> </td>
   <td><p>Couleur d’arrière-plan lorsque l’expression d’achèvement du panneau renvoie true (vrai) </p> </td>
  </tr>
  <tr>
   <td><p><code>wizard-tabs-completed-font-color</code></p> </td>
   <td><p>Couleur de police lorsque l’expression d’achèvement du panneau renvoie true (vrai) </p> </td>
  </tr>
  <tr>
   <td><p><code>wizard-tabs-stepped-bg-color</code></p> </td>
   <td>Couleur d’arrière-plan lorsque le panneau a été activé une fois mais que l’expression d’achèvement renvoie false (faux) </td>
  </tr>
  <tr>
   <td><p><code>wizard-tabs-stepped-font-color</code></p> </td>
   <td><p>Couleur de police lorsque le panneau a été activé une fois mais que l’expression d’achèvement renvoie false (faux)</p> </td>
  </tr>
  <tr>
   <td><p><code>wizard-tabs-border-color</code></p> </td>
   <td><p>Couleur de l’assistant</p> </td>
  </tr>
  <tr>
   <td><p><code>wizard-tabs-font-size</code></p> </td>
   <td><p>Taille de police de l’assistant</p> </td>
  </tr>
  <tr>
   <td><p><code>wizard-tabs-padding</code></p> </td>
   <td><p>Marge intérieure de l’assistant</p> </td>
  </tr>
  <tr>
   <td><p><code>wizard-tabs-border-thickness</code></p> </td>
   <td><p>Taille de bordure de l’assistant</p> </td>
  </tr>
  <tr>
   <td><p><code>wizard-nav-bullet-border</code></p> </td>
   <td><p>Couleur de bordure de la puce du navigateur de l’assistant (devant la légende/le libellé)</p> </td>
  </tr>
  <tr>
   <td><p><code>wizard-progress-bg-color</code></p> </td>
   <td><p>Couleur d’arrière-plan de la barre de progression du navigateur de l’assistant</p> </td>
  </tr>
  <tr>
   <td><p><code>wizard-progress-color</code></p> </td>
   <td><p>Couleur de remplissage de la barre de progression</p> </td>
  </tr>
  <tr>
   <td><p><strong>Navigateurs en accordéon</strong></p> </td>
   <td><p> </p> </td>
  </tr>
  <tr>
   <td><p><code>accordion-tabs-padding</code></p> </td>
   <td><p>Marge intérieure de l’accordéon</p> </td>
  </tr>
 </tbody>
</table>

## Définition de style du panneau {#panel-styling}

Un panneau comporte une barre d’outils facultative et son contenu.

<table>
 <tbody>
  <tr>
   <td><p><strong>Classe CSS </strong></p> </td>
   <td><p><code>guidePanelNode</code></p> </td>
  </tr>
 </tbody>
</table>

<table>
 <tbody>
  <tr>
   <td><p><strong>Variables </strong></p> </td>
   <td><p><strong>Description</strong></p> </td>
  </tr>
  <tr>
   <td><p><code>panel-background-color</code></p> </td>
   <td><p>Couleur d’arrière-plan du panneau</p> </td>
  </tr>
  <tr>
   <td><p><code>panel-font-size</code></p> </td>
   <td><p>Taille de police du texte du panneau</p> </td>
  </tr>
  <tr>
   <td><p><code>panel-font-color</code></p> </td>
   <td><p>Couleur de police du texte du panneau<br /> </p> </td>
  </tr>
  <tr>
   <td><p><code>panel-padding</code></p> </td>
   <td><p>Marge intérieure du panneau</p> </td>
  </tr>
  <tr>
   <td><p><code>panel-description-font-size</code></p> </td>
   <td><p>Taille de police de la description du panneau</p> </td>
  </tr>
  <tr>
   <td><p><code>panel-description-padding</code></p> </td>
   <td><p>Marge intérieure de la description du panneau</p> </td>
  </tr>
  <tr>
   <td><p><code>panel-help-bg-color</code></p> </td>
   <td><p>Couleur d’arrière-plan de l’aide du panneau</p> </td>
  </tr>
  <tr>
   <td><p><code>panel-help-border-indicator-color</code></p> </td>
   <td><p>Couleur de bordure de l’indicateur de l’aide du panneau</p> </td>
  </tr>
 </tbody>
</table>

Le nœud du panneau est divisé en navigateurs et contenu. Il `` ``n’y a pas de composant de définition du style séparé pour le contenu. Les variables décrites sont appliquées sur le navigateur ainsi que sur le contenu.

Le panneau supérieur (RootPanel) ne dispose pas de cette classe.

## Styles mobiles {#mobile-styling}

## Barre d’en-tête {#header-bar}

Ces variables influent sur la barre d’en-tête visible sur un périphérique mobile ou équipé qui contient un titre de panneau et les navigateurs Suivant et Précédent.

<table>
 <tbody>
  <tr>
   <td><p><strong>Classe CSS </strong></p> </td>
   <td><p><code>guide-header-bar</code></p> </td>
  </tr>
 </tbody>
</table>

<table>
 <tbody>
  <tr>
   <td><p><strong>Variables </strong></p> </td>
   <td><p><strong>Description</strong></p> </td>
  </tr>
  <tr>
   <td><p><code>headerbar-background-color</code></p> </td>
   <td><p>Couleur d’arrière-plan de la barre d’en-tête</p> </td>
  </tr>
  <tr>
   <td><p><code>headerbar-font-color</code></p> </td>
   <td><p>Couleur de police du texte dans la barre d’en-tête</p> </td>
  </tr>
  <tr>
   <td><p><code>headerbar-padding</code></p> </td>
   <td><p>Marge intérieure de la barre d’en-tête</p> </td>
  </tr>
 </tbody>
</table>

## Indicateur de défilement  {#scroll-indicator}

Ces variables influent sur l’indicateur de défilement, qui est une flèche orange qui s’affiche sur un périphérique mobile ou équipé d’un petit écran. Un indicateur de défilement indique la présence de contenu au-delà de la partie visible à l’écran. Vous pouvez faire défiler l’écran pour l’afficher. Lorsque vous atteignez la fin du contenu, la flèche disparaît.

<table>
 <tbody>
  <tr>
   <td><p><strong>Classe CSS </strong></p> </td>
   <td><p><code>mobileScrollIndicator</code></p> </td>
  </tr>
 </tbody>
</table>

<table>
 <tbody>
  <tr>
   <td><p><strong>Variables </strong></p> </td>
   <td><p><strong>Description</strong></p> </td>
  </tr>
  <tr>
   <td><p><code>scrollIndicatorBottom</code></p> </td>
   <td><p>Position fixe de l’indicateur de défilement depuis le bas</p> </td>
  </tr>
  <tr>
   <td><p><code>scrollIndicatorRight</code></p> </td>
   <td><p>Position fixe de l’indicateur de défilement depuis la droite</p> </td>
  </tr>
  <tr>
   <td><p><code>scrollIndicatorWidth</code></p> </td>
   <td><p>Largeur de l’indicateur de défilement</p> </td>
  </tr>
  <tr>
   <td><p><code>scrollIndicatorHeight</code></p> </td>
   <td><p>Hauteur de l’indicateur de défilement</p> </td>
  </tr>
 </tbody>
</table>

## Variables spécifiques à la disposition de la barre d’outils fixe pour mobile  {#mobile-fixed-toolbar-layout-specific-variables}

Ces variables dans le tableau suivant influent sur la disposition de la barre d’outils fixe pour mobile.

<table>
 <tbody>
  <tr>
   <td><p><strong>Classe CSS </strong></p> </td>
   <td><p><code>mobileToolbar</code></p> </td>
  </tr>
 </tbody>
</table>

<table>
 <tbody>
  <tr>
   <td><p><strong>Variables </strong></p> </td>
   <td><p><strong>Description</strong></p> </td>
  </tr>
  <tr>
   <td><p><code>mobileToolbarBottom</code></p> </td>
   <td><p>Position fixe de la barre d’outils, sur un périphérique mobile, depuis le bas</p> </td>
  </tr>
  <tr>
   <td><p><code>mobileToolbarTop</code></p> </td>
   <td><p>Position fixe de la barre d’outils, sur un périphérique mobile, depuis le haut</p> </td>
  </tr>
  <tr>
   <td><p><code>mobileToolbarLeft</code></p> </td>
   <td><p>Position fixe de la barre d’outils, sur un périphérique mobile, depuis la gauche</p> </td>
  </tr>
  <tr>
   <td><p><code>mobileToolbarRight</code></p> </td>
   <td><p>Position fixe de la barre d’outils, sur un périphérique mobile, depuis la droite</p> </td>
  </tr>
  <tr>
   <td><p><code>mobileButtonIconTopMargin</code></p> </td>
   <td><p>Position fixe de l’icône des boutons de la barre d’outils, depuis le haut</p> </td>
  </tr>
  <tr>
   <td><p><code>mobileButtonIconWidth</code></p> </td>
   <td><p>Largeur de l’icône des boutons de la barre d’outils sur un périphérique mobile</p> </td>
  </tr>
  <tr>
   <td><p><code>mobileButtonIconHeight</code></p> </td>
   <td><p>Hauteur de l’icône des boutons de la barre d’outils sur un périphérique mobile</p> </td>
  </tr>
  <tr>
   <td><p><code>mobilefixedtoolbarbgcolor</code></p> </td>
   <td><p>Couleur d’arrière-plan de la barre d’outils sur un périphérique mobile</p> </td>
  </tr>
 </tbody>
</table>

## Variable spécifique au thème  {#theme-specific-variable}

Le thème **Inscription simple** sur /etc/clientlibs/fd/af/guidetheme/simpleEnrollment et la catégorie `guide.theme.simpleEnrollment` introduisent également quelques variables. Si vous souhaitez créer un thème qui améliore l&#39;inscription simple, vous pouvez utiliser les &quot;variables supplémentaires&quot; suivantes :

<table>
 <tbody>
  <tr>
   <td><p><strong>Variables </strong></p> </td>
   <td><p><strong>Description</strong></p> </td>
  </tr>
  <tr>
   <td><p><code>button-focus-bg-color</code></p> </td>
   <td><p>Couleur d’arrière-plan du bouton actif</p> </td>
  </tr>
  <tr>
   <td><p><code>button-hover-bg-color</code></p> </td>
   <td><p>Couleur d’arrière-plan du bouton au survol</p> </td>
  </tr>
  <tr>
   <td><p><code>button-radius</code></p> </td>
   <td><p>Rayon du bouton</p> </td>
  </tr>
  <tr>
   <td><p><code>navigation-button-bg-color</code></p> </td>
   <td><p>Couleur d’arrière-plan des boutons de navigation (Précédent/Suivant)</p> </td>
  </tr>
  <tr>
   <td><p><code>navigation-button-bg-hover-color</code></p> </td>
   <td><p>Couleur d’arrière-plan des boutons de navigation (Précédent/Suivant) au survol</p> </td>
  </tr>
  <tr>
   <td><p><code>initial-nav-color</code></p> </td>
   <td><p>Couleur d’arrière-plan des navigateurs de l’assistant et de la barre de progression correspondante, lors du premier rendu.</p> </td>
  </tr>
  <tr>
   <td><p><code>active-nav-color</code></p> </td>
   <td>Couleur d’arrière-plan du navigateur de l’assistant actuel/actif et de la barre de progression correspondante </td>
  </tr>
  <tr>
   <td><p><code>visited-nav-color</code></p> </td>
   <td><p>Couleur d’arrière-plan des navigateurs de l’assistant et de la barre de progression correspondante, qui ont été consultés.</p> </td>
  </tr>
  <tr>
   <td><p><code>tabs-bifercating-border-color</code></p> </td>
   <td><p>Couleur de bordure de bifurcation du conteneur dans les navigateurs et le panneau</p> </td>
  </tr>
  <tr>
   <td><p><code>tabs-navigator-separator-color</code></p> </td>
   <td><p>Couleur de bordure inférieure séparant les onglets pour les onglets sur la gauche (tabNavigators).</p> </td>
  </tr>
  <tr>
   <td><p><code>tabs-child-nav-bg-color</code></p> </td>
   <td><p>Couleur d’arrière-plan des navigateurs imbriqués/enfants/sous-navigateurs du navigateur.</p> </td>
  </tr>
 </tbody>
</table>

