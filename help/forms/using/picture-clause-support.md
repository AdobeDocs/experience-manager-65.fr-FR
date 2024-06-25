---
title: Prise en charge des clauses d’image pour HTML5 forms
description: HTML5 forms prend en charge les clauses d’image XFA pour afficher la valeur et la valeur formatée de la date, du texte et des synboles numériques.
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: 5e344be7-46cd-4e1f-ae3a-1f89c645cffe
feature: HTML5 Forms,Mobile Forms
exl-id: 7f9c77c6-447a-407f-ae58-6735176dc99c
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '659'
ht-degree: 100%

---

# Prise en charge des clauses d’image pour HTML5 forms {#picture-clause-support-for-html-forms}

HTML5 forms prend en charge les clauses d’image XFA pour afficher la valeur et la valeur formatée de la date, du texte et des synboles numériques. Les expressions de clause d’image suivantes sont prises en charge :

* category(locale){picture-clause} | category(locale){picture-clause} | category(locale){picture-clause}
* category.subcategory{}

>[!NOTE]
>
>À l’heure actuelle, Mobiles Forms ne prend pas en charge la clause d’édition d’image. De plus, les symboles des clauses DateTime et Time Picture ne sont pas pris en charge.

## Symboles de champ de date pris en charge {#supported-date-field-symbols}

Expression prise en charge pour la clause de date d’image :

* date.long{}
* date.short{}
* date.medium{}
* date.full{}
* date.short{}
* date{date Picture Clause symbols}

>[!NOTE]
>
>{MMM D, YYYY} représente le motif par défaut de la clause d’image. Si aucun modèle n’est appliqué, le modèle par défaut est utilisé.

<table>
 <tbody>
  <tr>
   <th><strong>Symbole</strong></th>
   <th>Interprétation</th>
  </tr>
  <tr>
   <td>D</td>
   <td>Jour du mois à 1 ou 2 chiffres (1 à 31)</td>
  </tr>
  <tr>
   <td>DD</td>
   <td>Jour du mois à deux chiffres (01 à 31) complétés par des zéros.<br /> </td>
  </tr>
  <tr>
   <td>M</td>
   <td>Mois de l'année à 1 ou 2 chiffres (1 à 12).<br /> </td>
  </tr>
  <tr>
   <td>MM</td>
   <td>Mois de l’année à deux chiffres (01 à 12) complétés par des zéros.<br /> </td>
  </tr>
  <tr>
   <td>MMM</td>
   <td>Nom du mois abrégé des paramètres régionaux actuels<br /> </td>
  </tr>
  <tr>
   <td>MMMM</td>
   <td>Nom du mois complet des paramètres régionaux actuels<br /> </td>
  </tr>
  <tr>
   <td>EEE</td>
   <td>Nom abrégé du jour de la semaine des paramètres régionaux actuels<br /> </td>
  </tr>
  <tr>
   <td>EEEE</td>
   <td>Nom complet du jour de la semaine des paramètres régionaux actuels<br /> </td>
  </tr>
  <tr>
   <td>YY</td>
   <td>Année à 2 chiffres, où 00 = 2000, 29 = 2029, 30 = 1930 et 99 = 1999<br /> </td>
  </tr>
  <tr>
   <td>YYYY</td>
   <td>Année à 4 chiffres<br /> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
> Selon la conception, le champ Date dans HTML5 Forms ne prend pas en charge le schéma `MM-YYYY` au format d’édition. Toutefois, ce schéma est pris en charge dans le format d’affichage.

## Clause d’image numérique {#numeric-picture-clause}

Les formulaires HTML5 prennent en charge les symboles d’image numérique. Cependant, il existe une différence de prise en charge entre les formulaires PDF et les formulaires HTML.

Dans les **formulaires PDF**, un nombre est mis en forme, quel que soit le nombre de symboles dans la clause d’image.

Dans les **formulaires HTML**, un nombre n’est mis en forme que s’il comporte des chiffres inférieurs au nombre de symboles dans la clause d’image.

**Exemple** : considérons une clause d’image : num{zzz,zzz,zz9}.

Le nombre **10000** est mis en forme en **10 000** dans les formulaires HTML et PDF.

Le nombre 1000000 est mis en forme en 1 000 000 dans les formulaires PDF. Cependant, dans les formulaires HTML, le nombre reste 1000000, sans mise en forme.

Expressions prises en charge pour la clause d’image numérique dans les **formulaires HTML** :

* num.integer{}
* num.decimal{}
* num.currency{}
* num.percent{}
* num{Numeric Picture Clause Symbols}

<table>
 <tbody>
  <tr>
   <th><strong>Symbole</strong></th>
   <th><strong>Interprétation</strong></th>
   <th>Analyse des valeurs d’entrée</th>
  </tr>
  <tr>
   <td>9</td>
   <td><strong>Mise en forme de sortie</strong> : un seul chiffre. Ou le chiffre zéro si les données d'entrée sont vides ou un espace à la position correspondante.<br /> </td>
   <td>Un seul chiffre</td>
  </tr>
  <tr>
   <td>Z</td>
   <td><strong>Mise en forme de sortie</strong> : un seul chiffre. Ou un espace si les données d'entrée sont vides, un espace, ou le chiffre zéro à la position correspondante.<br /> </td>
   <td>Un seul chiffre ou un espace</td>
  </tr>
  <tr>
   <td>z</td>
   <td><strong>Mise en forme de sortie</strong> : un seul chiffre. Ou rien si les données d'entrée sont vides, un espace ou le chiffre zéro à la position correspondante.<br /> </td>
   <td>Un chiffre ou rien</td>
  </tr>
  <tr>
   <td>E</td>
   <td><strong>Mise en forme de sortie</strong> : la partie exposant d’un nombre à virgule flottante constituée du symbole exponentiel (E). Suivi du signe plus ou moins facultatif. Suivi de la valeur de l’exposant.<br /> </td>
   <td>Identique à la mise en forme de sortie</td>
  </tr>
  <tr>
   <td>CR ou cr<br /> </td>
   <td>Symbole du crédit (CR) si le nombre est négatif. Sinon rien.</td>
   <td><br type="_moz" /> </td>
  </tr>
  <tr>
   <td>S ou s<br /> </td>
   <td>Mise en forme de sortie : un signe moins si le nombre est négatif. Sinon, un espace.<br /> </td>
   <td>Signe moins si le nombre est négatif. Signe plus si le nombre est positif.</td>
  </tr>
  <tr>
   <td>V</td>
   <td>Base décimale des paramètres régionaux actuels. Permet à la base décimale d’être implicite lors de l’analyse des entrées.</td>
   <td><br type="_moz" /> </td>
  </tr>
  <tr>
   <td>v</td>
   <td>Base décimale des paramètres régionaux actuels. Permet à la base décimale d’être implicite lors de l’analyse des entrées et de la mise en forme de la sortie.</td>
   <td><br type="_moz" /> </td>
  </tr>
  <tr>
   <td>.</td>
   <td>Base décimale des paramètres régionaux actuels.</td>
   <td><br type="_moz" /> </td>
  </tr>
  <tr>
   <td>, (U+FF0C)</td>
   <td>Séparateur d’un groupe de valeurs du jeu de paramètres régionaux dominant.</td>
   <td><br type="_moz" /> </td>
  </tr>
  <tr>
   <td>$ (U+FF04)</td>
   <td>Symbole de devise du jeu de paramètres régionaux dominant.</td>
   <td><br type="_moz" /> </td>
  </tr>
  <tr>
   <td>% (U+FF05)</td>
   <td>Symbole de pourcentage du jeu de paramètres régionaux dominant.</td>
   <td><br type="_moz" /> </td>
  </tr>
  <tr>
   <td>( (U+FF08)</td>
   <td>Parenthèse gauche si le nombre est négatif. Sinon, un espace.</td>
   <td><br type="_moz" /> </td>
  </tr>
  <tr>
   <td>) (U+FF09)</td>
   <td>Parenthèse droite si le nombre est négatif. Sinon, un espace.</td>
   <td><br type="_moz" /> </td>
  </tr>
  <tr>
   <td>t</td>
   <td>Caractère de tabulation</td>
   <td><br type="_moz" /> </td>
  </tr>
 </tbody>
</table>

## Clause de texte d’image {#text-picture-clause}

Les formulaires HTML5 prennent en charge les expressions de clause de texte d’image suivantes :

* text{text Picture clause symbols}

| **Symbole** | **Interprétation** |
|---|---|
| A | Caractère alphabétique unique. |
| X | Caractère unique. |
| O | Caractère alphanumérique unique. |
| 0 (zéro) | Caractère alphanumérique unique. |
| 9 | Un seul chiffre. |
