---
title: Prise en charge de XFA dans les formulaires adaptatifs basés sur XDP
seo-title: Prise en charge de XFA dans les formulaires adaptatifs basés sur XDP
description: Répertorie les événements XFA pris en charge, les propriétés, les scripts et la validation dans les formulaires adaptatifs.
seo-description: Répertorie les événements XFA pris en charge, les propriétés, les scripts et la validation dans les formulaires adaptatifs.
uuid: 75d3c292-cfed-438f-afdb-4071d95a08b7
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
discoiquuid: 05303b29-9058-4723-b134-4ba605fe40c7
docset: aem65
feature: Formulaires adaptatifs
exl-id: 255be73f-3169-457c-aaa7-a2fb59f1f2cd
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '702'
ht-degree: 94%

---

# Prise en charge de XFA dans les formulaires adaptatifs basés sur XDP{#xfa-support-in-xdp-based-adaptive-forms}

## Présentation {#introduction}

Les formulaires adaptatifs prennent en charge différents événements XFA, propriétés, scripts et validations définis dans un fichier XDP, notamment : 

* Exécution de scripts définis sur les événements dans le fichier XDP.
* Capture des valeurs par défaut et des propriétés comportementales pour les champs du fichier XDP.
* Exécution de scripts de validation définis dans le fichier XDP.

Lorsqu’un formulaire adaptatif est créé à partir d’un fichier XDP, les propriétés, les événements et les validations sont automatiquement renseignés sur l’interface utilisateur de création de formulaire. Toutefois, les concepteurs de formulaires peuvent remplacer certains de ces éléments pour créer une autre expérience.

Cet article répertorie les événements XFA, les propriétés et les validations pris en charge dans les formulaires adaptatifs et explique comment les remplacer dans ces formulaires. 

## Éléments XFA pris en charge et leur mappage dans les formulaires adaptatifs{#supported-xfa-elements-and-their-mapping-in-adaptive-forms-br}   

### Champs {#fields}

Lorsqu’un formulaire adaptatif est créé à l’aide d’un fichier XDP, vous pouvez faire glisser et déposer un champ XFA dans le formulaire adaptatif. Le tableau suivant répertorie la façon dont les champs XFA sont associés à des champs de formulaire adaptatif. 

<table>
 <tbody>
  <tr>
   <td><p><strong>Champ ou conteneur XFA</strong></p> </td>
   <td><p><strong>Composant de formulaire adaptatif correspondant    </strong></p> </td>
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
   <td><p>Zone de mot de passe</p> </td>
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
   <td><p><strong>Comportement correspondant dans les formulaires adaptatifs    </strong></p> </td>
  </tr>
  <tr>
   <td><p>somExpression </p> </td>
   <td><p>Chemin d’accès à la propriété référence Bind (bindRef) dans les formulaires adaptatifs.   </p> </td>
  </tr>
  <tr>
   <td><p>presence </p> </td>
   <td><p>Associé à la propriété visible dans le formulaire adaptatif. Vous pouvez le remplacer en utilisant l’expression Visibility</p> </td>
  </tr>
  <tr>
   <td><p>access </p> </td>
   <td><p>Associé à la propriété activée dans le formulaire adaptatif. Vous pouvez le remplacer à l’aide de l’expression Access.</p> </td>
  </tr>
  <tr>
   <td><p>Accessibilité : role </p> </td>
   <td><p>Associé à la propriété role dans le formulaire adaptatif.</p> </td>
  </tr>
  <tr>
   <td><p>Accessibilité : speakPriority </p> </td>
   <td><p>Associé à la propriété speakPriority dans le formulaire adaptatif.   </p> </td>
  </tr>
  <tr>
   <td><p>Accessibilité : speakText</p> </td>
   <td><p>Associé au texte Accessibility personnalisé dans le formulaire adaptatif.   </p> </td>
  </tr>
  <tr>
   <td><p>Accessibilité : toolTip </p> </td>
   <td><p>Associé à la propriété short description dans le formulaire adaptatif.</p> </td>
  </tr>
  <tr>
   <td><p>caption<em> (tous les types de champ)</em></p> </td>
   <td><p>Associé à la propriété Title dans le formulaire adaptatif.</p> </td>
  </tr>
  <tr>
   <td><p>displayFormat<em> (tous les types de champ)</em></p> </td>
   <td><p>Associé à la propriété Display Pattern dans le formulaire adaptatif.   </p> </td>
  </tr>
  <tr>
   <td><p>rawValue<em> (tous les types de champ)</em></p> </td>
   <td><p>Associé à la propriété Value dans le formulaire adaptatif.   </p> </td>
  </tr>
  <tr>
   <td><p>items<em> (zone de liste, case à cocher)</em></p> </td>
   <td><p>Associé à la propriété options dans le formulaire adaptatif. Vous pouvez le remplacer à l’aide de l’expression Options.</p> </td>
  </tr>
  <tr>
   <td><p>maxChar<em> (champ de texte)</em></p> </td>
   <td><p>Associé à la propriété Maximum characters allowed dans le formulaire adaptatif.   </p> </td>
  </tr>
  <tr>
   <td><p>multiline<em> (champ de texte)</em></p> </td>
   <td><p>Associé à la propriété Allow multiple lines dans le formulaire adaptatif.   </p> </td>
  </tr>
  <tr>
   <td><p>fracDigit<em> (champ numérique, champ décimal)</em></p> </td>
   <td><p>Associé à la propriété Frac digits dans le formulaire adaptatif.   </p> </td>
  </tr>
  <tr>
   <td><p>leadDigit<em> (champ numérique, champ décimal)</em></p> </td>
   <td><p>Associé à la propriété Lead digits dans le formulaire adaptatif.   </p> </td>
  </tr>
  <tr>
   <td><p>multiSelect<em> (zone de liste)</em></p> </td>
   <td><p>Associé à la propriété Allows multiple selection dans le formulaire adaptatif.   </p> </td>
  </tr>
 </tbody>
</table>

### Scripts {#scripts}

Le tableau suivant capture la manière dont divers scripts XFA définis dans les fichiers XDP se comportent dans les formulaires adaptatifs.

<table>
 <tbody>
  <tr>
   <td><p><strong>Événements de script XFA</strong></p> </td>
   <td><p><strong>Comportement correspondant dans les formulaires adaptatifs    </strong></p> </td>
  </tr>
  <tr>
   <td><p>initialize </p> </td>
   <td><p>Ce script est exécuté lors de l’exécution et ne peut pas être remplacé dans les formulaires adaptatifs.   </p> </td>
  </tr>
  <tr>
   <td><p>calculate</p> </td>
   <td><p>Associé à l’expression Calculate dans le formulaire adaptatif.   </p> </td>
  </tr>
  <tr>
   <td><p>validate </p> </td>
   <td><p>Associé à l’expression Validation dans le formulaire adaptatif.   </p> </td>
  </tr>
  <tr>
   <td><p>validationState </p> </td>
   <td><p>Ce script est exécuté lors de l’exécution et ne peut pas être remplacé dans les formulaires adaptatifs.<br />    </p> </td>
  </tr>
  <tr>
   <td><p>exit </p> </td>
   <td><p>Ce script est exécuté lors de l’exécution et ne peut pas être remplacé dans les formulaires adaptatifs.   </p> </td>
  </tr>
  <tr>
   <td><p>click (champs de bouton)</p> </td>
   <td><p>Associé à l’expression Click du bouton.</p> </td>
  </tr>
  <tr>
   <td><p>Prise en charge de script côté serveur</p> </td>
   <td><p>Ce script est exécuté lors de l’exécution et ne peut pas être remplacé dans les formulaires adaptatifs.   </p> </td>
  </tr>
  <tr>
   <td><p>Prise en charge des services Web</p> </td>
   <td><p>Ce script est exécuté lors de l’exécution et ne peut pas être remplacé dans les formulaires adaptatifs.   </p> </td>
  </tr>
  <tr>
   <td><p>Modification (champ de saisie tactile, bouton radio, case à cocher)</p> </td>
   <td><p>Ce script est exécuté lors de l’exécution et ne peut pas être remplacé dans les formulaires adaptatifs.   </p> </td>
  </tr>
 </tbody>
</table>

### Validations {#validations}

Le tableau suivant capture la manière dont les validations XFA sont associées aux validations dans les formulaires adaptatifs.   

<table>
 <tbody>
  <tr>
   <td><p><strong>Validation XFA</strong></p> </td>
   <td><p><strong>Validation correspondante dans les formulaires adaptatifs    </strong></p> </td>
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
>Vous ne pouvez pas remplacer la propriété obligatoire pour le groupe bouton radio et case à cocher du formulaire adaptatif qui est lié aux boutons de vérification XFA.
