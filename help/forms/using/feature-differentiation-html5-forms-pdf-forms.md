---
title: Différences de caractéristiques entre formulaires HTML5 et formulaires PDF
seo-title: Différences de caractéristiques entre formulaires HTML5 et formulaires PDF
description: Caractéristiques prises en charge dans les formulaires HTML5 et les formulaires PDF
seo-description: Caractéristiques prises en charge dans les formulaires HTML5 et les formulaires PDF
uuid: 6ddee197-d108-4897-9976-77d115a06504
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
discoiquuid: bdd97c20-d1f2-4898-9862-1a6a8071be88
docset: aem65
feature: Mobile Forms
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '462'
ht-degree: 87%

---


# Différences de caractéristiques entre formulaires HTML5 et formulaires PDF {#feature-differentiation-between-html-forms-and-pdf-forms}

Le tableau suivant indique les fonctionnalités prises en charge par les formulaires HTML5 et les formulaires PDF :

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
   <td>Les <strong>signatures numériques</strong> ne sont pas prises en charge, mais un nouveau champ <strong>Scribble Signature</strong> (Signature à main levée) est ajouté pour les signatures manuscrites. Il est ainsi possible de signer le formulaire à la main dans le champ <strong>Scribble Signature</strong>. La signature est enregistrée sur le formulaire sous la forme d’une image. Vous pouvez enregistrer des informations de géolocalisation dans le champ <strong>Scribble Signature</strong>.</td>
   <td>Champ de signature disponible pour les <strong>signatures numériques</strong>.</td>
  </tr>
  <tr>
   <td>Fusion des données</td>
   <td>Pris en charge</td>
   <td>Pris en charge</td>
  </tr>
  <tr>
   <td>Images</td>
   <td>Le modèle de données URI est utilisé pour afficher les images. Toutes les versions modernes de navigateurs prennent en charge ce modèle, mais il existe des différences dans la plage des formats d’image que chaque navigateur prend en charge.<br /> </td>
   <td>Les formats .gif, .png, .jpeg, .bmp et .tiff sont pris en charge.</td>
  </tr>
  <tr>
   <td>Pagination<br /> </td>
   <td><p>Un formulaire HTML5 est divisé en panneaux et en zones pour lui donner un aspect similaire aux formulaires PDF. La taille d’une page est calculée de façon dynamique. Si tout le contenu d’une page de formulaire HTML5 est supprimé ou marqué comme masqué, la page vierge est masquée et un espace vide (espace blanc) ne s’affiche pas entre les pages, au-dessus et au-dessous de la page vierge.</p> <p>Si la fusion des données ou des scripts ajoutent du contenu à une page, la longueur de la page s’ajuste au contenu qui vient d’être ajouté. Aucune nouvelle page n’est ajoutée au formulaire pour s’ajuster au contenu qui vient d’être ajouté. </p> <p><strong>Remarque :</strong> lorsque tout le contenu d’une page de formulaire HTML5 est supprimé ou marqué comme masqué, la page vierge (espace blanc) reste visible entre la 1ère et 2e page mais pas entre les autres pages.</p> </td>
   <td>La pagination dans le fichier PDF dépend du contenu des données fusionné ou du contenu de l’utilisateur et le nombre de pages est augmenté/réduit en fonction de ce contenu.</td>
  </tr>
  <tr>
   <td>En-têtes/pieds de page </td>
   <td>Pris en charge. <br /> <br /> Les formulaires mobiles HTML5 ne prenant pas en charge les sauts de page, les en-têtes et les pieds de page n’apparaissent qu’une seule fois. Vous pouvez toutefois les configurer dans la mise en page pour s’afficher en plusieurs endroits dans l’aperçu de formulaires mobiles.<br /> </td>
   <td>Pris en charge.</td>
  </tr>
  <tr>
   <td>Widgets personnalisés</td>
   <td>Il est possible de personnaliser les widgets pour améliorer l’expérience de l’utilisateur sur les périphériques mobiles.<br /> </td>
   <td>Tous les widgets sont verrouillés et aucun widget personnalisé ne peut être connecté.<br /> </td>
  </tr>
  <tr>
   <td>API de script XFA</td>
   <td>Prend en charge les éléments de script XFA les plus couramment utilisés. Pour plus d’informations sur la liste des éléments pris en charge, voir <a href="/help/forms/using/scripting-support.md">Prise en charge des scripts</a>.</td>
   <td>Prend en charge tous les éléments de script XFA.</td>
  </tr>
  <tr>
   <td>API des scripts Acrobat </td>
   <td>Les formulaires HTML5 prennent en charge la plupart des API couramment utilisées. Pour plus d’informations, voir <a href="/help/forms/using/scripting-support.md">Prise en charge des scripts</a>.</td>
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
