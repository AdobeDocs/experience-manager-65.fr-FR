---
title: Prise en charge des clauses d’image pour HTML5 forms
seo-title: Prise en charge des clauses d’image pour HTML5 forms
description: HTML5 forms prend en charge les clauses d’image XFA pour afficher la valeur et la valeur formatée de la date, du texte et des synboles numériques.
seo-description: HTML5 forms prend en charge les clauses d’image XFA pour afficher la valeur et la valeur formatée de la date, du texte et des synboles numériques.
uuid: ca5074ce-8219-4f27-a37c-b1f0dca4ce03
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: 5e344be7-46cd-4e1f-ae3a-1f89c645cffe
feature: Mobile Forms
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '638'
ht-degree: 96%

---


# Prise en charge des clauses d’image pour les formulaires HTML5 {#picture-clause-support-for-html-forms}

HTML5 forms prend en charge les clauses d’image XFA pour afficher la valeur et la valeur formatée de la date, du texte et des synboles numériques. Les expressions de clause d’image suivantes sont prises en charge :

* category(locale){picture-clause} | category(locale){picture-clause} | category(locale){picture-clause}
* category.subcategory{}

>[!NOTE]
>
>Mobile Forms ne prend actuellement pas en charge la clause de modification de l’image. En outre, les symboles de clause DateTime et Image horaire ne sont pas pris en charge.

## Symboles de champ date pris en charge {#supported-date-field-symbols}

Expressions prises en charge pour la clause d’image de date :

* date.long{}
* date.short{}
* date.medium{}
* date.full{}
* date.short{}
* date{symboles de la clause d’image de date}

>[!NOTE]
>
>{MMM D, YYYY} représente le motif par défaut de la clause d’image. Si aucun motif n’est appliqué, le motif par défaut est utilisé.

<table>
 <tbody>
  <tr>
   <th><strong>Symbole</strong></th>
   <th>Interprétation</th>
  </tr>
  <tr>
   <td>D</td>
   <td>Jour du mois à 1 ou 2 chiffres (1-31).</td>
  </tr>
  <tr>
   <td>JJ</td>
   <td>Jour du mois à deux chiffres avec le zéro (01-31).<br /> </td>
  </tr>
  <tr>
   <td>M</td>
   <td>Mois de l’année à 1 ou 2 chiffres (1-12).<br />  </td>
  </tr>
  <tr>
   <td>MM</td>
   <td>Mois de l’année à deux chiffres avec le zéro (01-12).<br /> </td>
  </tr>
  <tr>
   <td>MMM</td>
   <td>Nom abrégé du mois dans la langue courante<br /> </td>
  </tr>
  <tr>
   <td>MMMM</td>
   <td>Nom du mois complet dans la langue courante<br /> </td>
  </tr>
  <tr>
   <td>EEE</td>
   <td>Nom abrégé du jour de la semaine dans la langue courante<br /> </td>
  </tr>
  <tr>
   <td>EEEE</td>
   <td>Nom complet du jour de la semaine dans la langue courante<br /> </td>
  </tr>
  <tr>
   <td>AA</td>
   <td>Année à 2 chiffres, où 00 = 2000, 29 = 2029, 30 = 1930 et 99 = 1999<br /> </td>
  </tr>
  <tr>
   <td>AAAA</td>
   <td>Année à 4 chiffres<br /> </td>
  </tr>
 </tbody>
</table>

## Clause d’image numérique {#numeric-picture-clause}

HTML5 forms prend en charge les symboles d’image numérique. Toutefois, il existe une différence de prise en charge entre les formulaires PDF et les formulaires HTML.

Dans les **formulaires PDF**, un nombre est formaté indépendamment du nombre de symboles que contient la clause d’image.

Dans les **formulaires HTML**, un nombre est formaté uniquement s’il contient des chiffres inférieurs à ceux du nombre de symboles dans la clause d’image.

**Exemple** : prenez une clause d’image : num{zzz,zzz,zz9}.

Le nombre **10000** est formaté sous la forme **10 000** dans les formulaires HTML et PDF.

Le nombre 1000000 est formaté sous la forme 1 000 000 dans les formulaires PDF. Toutefois, dans les formulaires HTML, ce nombre n’est pas formaté et conserve la forme 1000000.

Les expressions prises en charge pour la clause d’image numérique dans **Forms HTML** sont les suivantes :

* num.integer{}
* num.decimal{}
* num.currency{}
* num.percent{}
* num{symboles de la clause d’image numérique}

<table>
 <tbody>
  <tr>
   <th><strong>Symbole</strong></th>
   <th><strong>Interprétation</strong></th>
   <th>Analyse des valeurs d’entrée</th>
  </tr>
  <tr>
   <td>9</td>
   <td><strong>Formatage des valeurs de sortie</strong> : un seul chiffre. Ou pour le chiffre zéro si les données d’entrée sont vides ou un espace à l’emplacement correspondant.<br /> </td>
   <td>Chiffre simple</td>
  </tr>
  <tr>
   <td>Z</td>
   <td><strong>Formatage des valeurs de sortie</strong> : un seul chiffre. Ou pour un espace si les données d’entrée sont vides, un espace ou le chiffre zéro à l’emplacement correspondant.<br /> </td>
   <td>Un seul chiffre ou un espace</td>
  </tr>
  <tr>
   <td>z</td>
   <td><strong>Formatage des valeurs de sortie</strong> : un seul chiffre. Ou pour un blanc si les données d’entrée sont vides, un espace ou le chiffre zéro à l’emplacement correspondant.<br /> </td>
   <td>Un seul chiffre ou rien</td>
  </tr>
  <tr>
   <td>E</td>
   <td><strong>Formatage des valeurs de sortie</strong> : la partie exposant d’un nombre à virgule flottante du symbole exponentiel (E). Suivi du signe plus ou moins facultatif. Suivi de la valeur de l’exposant.<br /> </td>
   <td>Identique au formatage des valeurs de sortie</td>
  </tr>
  <tr>
   <td>CR ou cr<br /> </td>
   <td>Symbole du crédit (CR) lorsque le nombre est négatif. Sinon rien.</td>
   <td><br type="_moz" /> </td>
  </tr>
  <tr>
   <td>S ou s<br /> </td>
   <td>Formatage des valeurs de sortie : un signe moins si le nombre est négatif. Sinon un espace.<br /> </td>
   <td>Signe moins si le nombre est négatif. Signe plus si le nombre est positif.</td>
  </tr>
  <tr>
   <td>V</td>
   <td>Base décimale du jeu de paramètres régionaux dominant. Permet d’indiquer la base décimale lors de l’analyse de l’entrée.</td>
   <td><br type="_moz" /> </td>
  </tr>
  <tr>
   <td>v</td>
   <td>Base décimale du jeu de paramètres régionaux dominant. Permet d’indiquer la base décimale lors de l’analyse des valeurs d’entrée et du formatage des valeurs de sortie.</td>
   <td><br type="_moz" /> </td>
  </tr>
  <tr>
   <td>.</td>
   <td>Base décimale du jeu de paramètres régionaux dominant.</td>
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
   <td>Parenthèse gauche si le nombre est négatif. Sinon un espace.</td>
   <td><br type="_moz" /> </td>
  </tr>
  <tr>
   <td>) (U+FF09)</td>
   <td>Parenthèse droite si le nombre est négatif. Sinon un espace.</td>
   <td><br type="_moz" /> </td>
  </tr>
  <tr>
   <td>t</td>
   <td>Caractère de tabulation</td>
   <td><br type="_moz" /> </td>
  </tr>
 </tbody>
</table>

## Clause d’image de texte  {#text-picture-clause}

HTML5 forms prend en charge les expressions de clause d’image de texte suivantes :

* text{symboles de clause d’image de texte}

| **Symbole** | **Interprétation** |
|---|---|
| A | Caractère alphabétique simple. |
| X | Caractère simple. |
| O | Caractère alphanumérique simple. |
| 0 (zéro) | Caractère alphanumérique simple. |
| 9 | Chiffre simple. |
