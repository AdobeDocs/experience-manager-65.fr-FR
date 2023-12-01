---
title: Différences de caractéristiques entre formulaires HTML5 et formulaires PDF
description: Découvrez les différences de fonctionnalités entre les formulaires HTML5 et les PDF forms.
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
docset: aem65
feature: Mobile Forms
exl-id: 3150f95f-7150-4eee-b5a9-121422dec2a1
source-git-commit: 5e56441d2dc9b280547c91def8d971e7b1dfcfe3
workflow-type: tm+mt
source-wordcount: '447'
ht-degree: 32%

---

# Différences de caractéristiques entre formulaires HTML5 et formulaires PDF {#feature-differentiation-between-html-forms-and-pdf-forms}

Le tableau suivant indique les fonctionnalités prises en charge par les formulaires HTML5 et les formulaires PDF :

<table>
 <tbody>
  <tr>
   <th>Fonctionnalité</th>
   <th>Formulaires HTML5</th>
   <th>PDF</th>
  </tr>
  <tr>
   <td>Codes à barres<br /> </td>
   <td>Non disponible au niveau de l’interface utilisateur. </td>
   <td>Pris en charge</td>
  </tr>
  <tr>
   <td>Champ de signature<br /> </td>
   <td><strong>Signatures numériques</strong> ne sont pas pris en charge, mais une nouvelle <strong>Signature tactile</strong> est ajouté pour les signatures de type papier. Vous pouvez signer à main levée sur le formulaire à l’aide de la fonction <strong>Signature tactile</strong> champ . La signature est enregistrée sur le formulaire sous forme d’image. Vous pouvez enregistrer les informations de géolocalisation dans la variable <strong>Signature tactile</strong> champ .</td>
   <td>Champ de signature disponible pour <strong>Signatures numériques</strong>.</td>
  </tr>
  <tr>
   <td>Fusion des données</td>
   <td>Pris en charge</td>
   <td>Pris en charge</td>
  </tr>
  <tr>
   <td>Images</td>
   <td>Le schéma d’URI de données est utilisé pour afficher les images. Toutes les versions modernes des navigateurs prennent en charge ce modèle, mais il existe des différences dans la plage des formats d’image pris en charge par chaque navigateur.<br /> </td>
   <td>Les formats .gif, .png, .jpeg, .bmp et .tiff sont pris en charge.</td>
  </tr>
  <tr>
   <td>Pagination<br /> </td>
   <td><p>Un formulaire HTML5 est divisé en panneaux et cases pour lui donner une apparence similaire aux PDF forms. La taille de la page est calculée dynamiquement. Si tout le contenu d’une page d’un formulaire HTML5 est supprimé ou marqué comme masqué, la page vierge est masquée. Un espace vide (espace vide) n’est pas affiché entre les pages au-dessus et au-dessous de la page vierge.</p> <p>Si la fusion de données ou les scripts ajoutent du contenu à une page, la longueur de la page s’étend pour s’adapter au contenu nouvellement ajouté. Aucune nouvelle page n’est ajoutée au formulaire pour s’adapter au contenu nouvellement ajouté. </p> <p><strong>Remarque :</strong> Lorsque tout le contenu d’une page d’un formulaire HTML5 est supprimé ou marqué comme masqué, la page vierge (espace vide) reste visible entre la première et la deuxième page, mais pas entre les autres pages.</p> </td>
   <td>La pagination des documents PDF dépend du contenu des données fusionnées ou du contenu de l’utilisateur : le nombre de pages est augmenté/réduit en conséquence.</td>
  </tr>
  <tr>
   <td>En-têtes/pieds de page </td>
   <td>Pris en charge. <br /> <br /> Les formulaires mobiles HTML5 ne prenant pas en charge les sauts de page, les en-têtes et les pieds de page n’apparaissent qu’une seule fois. Vous pouvez toutefois les configurer dans la mise en page afin qu’elles s’affichent à plusieurs endroits dans l’aperçu des formulaires mobiles.<br /> </td>
   <td>Pris en charge.</td>
  </tr>
  <tr>
   <td>Widgets personnalisés</td>
   <td>Vous pouvez personnaliser des widgets pour améliorer l’expérience utilisateur sur les appareils mobiles.<br /> </td>
   <td>Tous les widgets sont verrouillés et aucun widget personnalisé ne peut être connecté.<br /> </td>
  </tr>
  <tr>
   <td>API de script XFA</td>
   <td>Prend en charge les éléments de scripts XFA les plus fréquemment utilisés. Pour obtenir la liste détaillée des éléments pris en charge, voir <a href="/help/forms/using/scripting-support.md">prise en charge des scripts</a>.</td>
   <td>Prend en charge tous les éléments de script XFA.</td>
  </tr>
  <tr>
   <td>API des scripts Acrobat </td>
   <td>Les formulaires HTML5 prennent en charge la plupart des API couramment utilisées. Pour plus d’informations, consultez la section <a href="/help/forms/using/scripting-support.md">Prise en charge des scripts</a>.</td>
   <td>Si le fichier PDF est ouvert dans Acrobat ou Reader, il prend également en charge toutes les API de script fournies par Acrobat.</td>
  </tr>
  <tr>
   <td>Prise en charge des langues écrites de droite à gauche </td>
   <td>Pris en charge</td>
   <td>Pris en charge</td>
  </tr>
 </tbody>
</table>

<!--Follow the best practices to enable a form template for HTML5 renditions and ensure that the behavior and appearance of HTML5 forms and XFA-based PDF is consistent. For detailed list of best practices, see [Best practices to design an HTML5 form.](/help/forms/using/best-practices-design-html5-forms.md)-->
