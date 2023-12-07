---
title: Prise en charge de XFA dans les formulaires adaptatifs basés sur XDP
description: Répertorie les événements XFA, les propriétés, les scripts et la validation pris en charge dans les formulaires adaptatifs.
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
docset: aem65
feature: Adaptive Forms
exl-id: 255be73f-3169-457c-aaa7-a2fb59f1f2cd
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '732'
ht-degree: 73%

---

# Prise en charge de XFA dans les formulaires adaptatifs basés sur XDP{#xfa-support-in-xdp-based-adaptive-forms}

## Présentation {#introduction}

<span class="preview"> Adobe recommande d’utiliser la capture de données moderne et extensible. [Composants principaux](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=fr) pour [création d’un Forms adaptatif](/help/forms/using/create-an-adaptive-form-core-components.md) ou [Ajout de Forms adaptatif à des pages AEM Sites](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md). Ces composants représentent une avancée significative dans la création de Forms adaptatif, ce qui garantit des expériences utilisateur impressionnantes. Cet article décrit l’approche plus ancienne de la création de Forms adaptatif à l’aide de composants de base. </span>

Les formulaires adaptatifs prennent en charge divers événements XFA, propriétés, scripts et validations définis dans un fichier XDP, notamment :

* Exécution de scripts définis sur les événements dans le fichier XDP.
* Capture des valeurs par défaut et des propriétés comportementales pour les champs du fichier XDP.
* Exécution de scripts de validation définis dans le fichier XDP.

Lorsqu’un formulaire adaptatif est créé à partir d’un fichier XDP, les propriétés, les événements et les validations sont automatiquement renseignés dans l’interface utilisateur de création de formulaire. Toutefois, les concepteurs de formulaires peuvent remplacer certains de ces éléments pour créer une autre expérience.

Cet article répertorie les événements, propriétés et validations XFA pris en charge honorés dans les formulaires adaptatifs et explique comment les remplacer dans les formulaires adaptatifs.

## Éléments XFA pris en charge et leur mappage dans les formulaires adaptatifs  {#supported-xfa-elements-and-their-mapping-in-adaptive-forms-br}

### Champs {#fields}

Lorsqu’un formulaire adaptatif est créé à l’aide d’un fichier XDP, vous pouvez faire glisser un champ XFA sur le formulaire adaptatif. Le tableau suivant répertorie la façon dont les champs XFA sont mappés aux champs de formulaire adaptatif.

<table>
 <tbody>
  <tr>
   <td><p><strong>Champ ou conteneur XFA</strong></p> </td>
   <td><p><strong>Composant de formulaire adaptatif correspondant </strong></p> </td>
  </tr>
  <tr>
   <td><p>Bouton </p> </td>
   <td><p>Bouton</p> </td>
  </tr>
  <tr>
   <td><p>Case à cocher </p> </td>
   <td><p>Case à cocher</p> </td>
  </tr>
  <tr>
   <td><p>Zone de liste </p> </td>
   <td><p>Liste déroulante</p> </td>
  </tr>
  <tr>
   <td><p>Champ Date/Heure </p> </td>
   <td><p>Sélecteur de date</p> </td>
  </tr>
  <tr>
   <td><p>Signature tactile</p> </td>
   <td><p>Signature tactile</p> </td>
  </tr>
  <tr>
   <td><p>Champ numérique </p> </td>
   <td><p>Zone numérique</p> </td>
  </tr>
  <tr>
   <td><p>Champ décimal</p> </td>
   <td><p>Zone numérique</p> </td>
  </tr>
  <tr>
   <td><p>Champ de texte </p> </td>
   <td><p>Zone de texte</p> </td>
  </tr>
  <tr>
   <td><p>Champ Mot de passe </p> </td>
   <td><p>Champ de mot de passe</p> </td>
  </tr>
  <tr>
   <td><p>Image</p> </td>
   <td><p>Image</p> </td>
  </tr>
  <tr>
   <td><p>Texte</p> </td>
   <td><p>Texte</p> </td>
  </tr>
  <tr>
   <td><p>Sous-formulaire </p> </td>
   <td><p>Panneau</p> </td>
  </tr>
  <tr>
   <td><p>Zone (groupe)</p> </td>
   <td><p>Panneau</p> </td>
  </tr>
  <tr>
   <td><p>Jeu de sous-formulaires </p> </td>
   <td><p>Panneau</p> </td>
  </tr>
 </tbody>
</table>

### Propriétés {#properties}

Le tableau suivant capture la manière dont divers scripts XFA définis dans les fichiers XDP se comportent dans les formulaires adaptatifs.

<table>
 <tbody>
  <tr>
   <td><p><strong>Propriétés du composant XFA</strong></p> </td>
   <td><p><strong>Comportement correspondant dans les formulaires adaptatifs </strong></p> </td>
  </tr>
  <tr>
   <td><p>somExpression </p> </td>
   <td><p>Chemin d’accès à la propriété référence Bind (bindRef) dans les formulaires adaptatifs. </p> </td>
  </tr>
  <tr>
   <td><p>presence </p> </td>
   <td><p>Associé à la propriété visible dans le formulaire adaptatif. Vous pouvez le remplacer en utilisant l’expression Visibility</p> </td>
  </tr>
  <tr>
   <td><p>accès </p> </td>
   <td><p>Associé à la propriété activée dans le formulaire adaptatif. Vous pouvez le remplacer à l’aide de l’expression Access.</p> </td>
  </tr>
  <tr>
   <td><p>Accessibilité : role </p> </td>
   <td><p>Associé à la propriété « rôle » dans le formulaire adaptatif.</p> </td>
  </tr>
  <tr>
   <td><p>Accessibilité : speakPriority </p> </td>
   <td><p>Associé à la propriété speakPriority dans le formulaire adaptatif. </p> </td>
  </tr>
  <tr>
   <td><p>Accessibilité : speakText</p> </td>
   <td><p>Associé au texte Accessibility personnalisé dans le formulaire adaptatif. </p> </td>
  </tr>
  <tr>
   <td><p>Accessibilité : toolTip </p> </td>
   <td><p>Associé à la propriété « Brève description » dans le formulaire adaptatif.</p> </td>
  </tr>
  <tr>
   <td><p>caption<em> (tous les types de champ)</em></p> </td>
   <td><p>Associé à la propriété Titre dans le formulaire adaptatif.</p> </td>
  </tr>
  <tr>
   <td><p>displayFormat<em> (tous les types de champ)</em></p> </td>
   <td><p>Associé à la propriété Display Pattern dans le formulaire adaptatif. </p> </td>
  </tr>
  <tr>
   <td><p>rawValue<em> (tous les types de champ)</em></p> </td>
   <td><p>Associé à la propriété Value dans le formulaire adaptatif. </p> </td>
  </tr>
  <tr>
   <td><p>items<em> (zone de liste, case à cocher)</em></p> </td>
   <td><p>Associé à la propriété options dans le formulaire adaptatif. Vous pouvez le remplacer à l’aide de l’expression Options.</p> </td>
  </tr>
  <tr>
   <td><p>maxChar<em> (champ de texte)</em></p> </td>
   <td><p>Associé à la propriété Maximum characters allowed dans le formulaire adaptatif. </p> </td>
  </tr>
  <tr>
   <td><p>multiline<em> (champ de texte)</em></p> </td>
   <td><p>Associé à la propriété Allow multiple lines dans le formulaire adaptatif. </p> </td>
  </tr>
  <tr>
   <td><p>fracDigit<em> (champ numérique, champ décimal)</em></p> </td>
   <td><p>Associé à la propriété Frac digits dans le formulaire adaptatif. </p> </td>
  </tr>
  <tr>
   <td><p>leadDigit<em> (champ numérique, champ décimal)</em></p> </td>
   <td><p>Associé à la propriété Lead digits dans le formulaire adaptatif. </p> </td>
  </tr>
  <tr>
   <td><p>multiSelect<em> (zone de liste)</em></p> </td>
   <td><p>Associé à la propriété Allows multiple selection dans le formulaire adaptatif. </p> </td>
  </tr>
 </tbody>
</table>

### Scripts {#scripts}

Le tableau suivant capture la manière dont divers scripts XFA définis dans les fichiers XDP se comportent dans les formulaires adaptatifs.

<table>
 <tbody>
  <tr>
   <td><p><strong>Événements de script XFA</strong></p> </td>
   <td><p><strong>Comportement correspondant dans les formulaires adaptatifs </strong></p> </td>
  </tr>
  <tr>
   <td><p>initialize </p> </td>
   <td><p>Ce script est exécuté lors de l’exécution et ne peut pas être remplacé dans les formulaires adaptatifs. </p> </td>
  </tr>
  <tr>
   <td><p>calculate</p> </td>
   <td><p>Associé à l’expression Calculate dans le formulaire adaptatif. </p> </td>
  </tr>
  <tr>
   <td><p>validate </p> </td>
   <td><p>Associé à l’expression Validation dans le formulaire adaptatif. </p> </td>
  </tr>
  <tr>
   <td><p>validationState </p> </td>
   <td><p>Ce script est exécuté lors de l’exécution et ne peut pas être remplacé dans les formulaires adaptatifs.<br />  </p> </td>
  </tr>
  <tr>
   <td><p>exit </p> </td>
   <td><p>Ce script est exécuté lors de l’exécution et ne peut pas être remplacé dans les formulaires adaptatifs. </p> </td>
  </tr>
  <tr>
   <td><p>click (champs de bouton)</p> </td>
   <td><p>Associé à l’expression Click du bouton.</p> </td>
  </tr>
  <tr>
   <td><p>Prise en charge de script côté serveur</p> </td>
   <td><p>Ce script est exécuté lors de l’exécution et ne peut pas être remplacé dans les formulaires adaptatifs. </p> </td>
  </tr>
  <tr>
   <td><p>Prise en charge des services Web</p> </td>
   <td><p>Ce script est exécuté lors de l’exécution et ne peut pas être remplacé dans les formulaires adaptatifs. </p> </td>
  </tr>
  <tr>
   <td><p>Modification (champ de saisie tactile, bouton radio, case à cocher)</p> </td>
   <td><p>Ce script est exécuté lors de l’exécution et ne peut pas être remplacé dans les formulaires adaptatifs. </p> </td>
  </tr>
 </tbody>
</table>

### Validations {#validations}

Le tableau suivant capture la manière dont les validations XFA sont associées aux validations dans les formulaires adaptatifs. 

<table>
 <tbody>
  <tr>
   <td><p><strong>Validation XFA</strong></p> </td>
   <td><p><strong>Validation correspondante dans les formulaires adaptatifs </strong></p> </td>
  </tr>
  <tr>
   <td><p>Modèle de validation (formatTest)</p> </td>
   <td><p>validatePictureClause</p> </td>
  </tr>
  <tr>
   <td><p>Message du modèle de validation (formatTestMessage)</p> </td>
   <td><p>validatePictureMessage</p> </td>
  </tr>
  <tr>
   <td><p>Required (nullTest)</p> </td>
   <td><p>mandatory </p> </td>
  </tr>
  <tr>
   <td><p>Empty Message (nullTestMessage) </p> </td>
   <td><p>mandatoryMessage</p> </td>
  </tr>
  <tr>
   <td><p>Validate script (scriptTest)</p> </td>
   <td><p>validateExp</p> </td>
  </tr>
  <tr>
   <td><p>Message du script de validation (scriptTestMessage)</p> </td>
   <td><p>validateMessage</p> </td>
  </tr>
 </tbody>
</table>

>[!NOTE]
>
>Vous ne pouvez pas remplacer la propriété obligatoire pour les boutons radio de formulaire adaptatif et les groupes de cases à cocher liés aux boutons de contrôle XFA.
