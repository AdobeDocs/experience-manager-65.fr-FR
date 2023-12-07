---
title: Structure de l’apparence des formulaires adaptatifs et HTML5
description: Mobile Forms effectue le rendu des modèles de formulaire sous la forme de formulaires HTML5. Ces formulaires utilisent les fichiers jQuery, Backbone.js et Underscore.js pour l’apparence et pour activer les scripts.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: customization
exl-id: 3458471a-9815-463e-8044-68631073863c
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '1152'
ht-degree: 31%

---

# Structure de l’apparence des formulaires adaptatifs et HTML5 {#appearance-framework-for-adaptive-and-html-forms}

Les formulaires (formulaires adaptatifs et HTML5) utilisent [jQuery](https://jquery.com/), [Backbone.js](https://backbonejs.org/) et [Underscore.js](https://underscorejs.org/) pour l’apparence et les scripts. Les formulaires utilisent également l’architecture des [jQuery UI](https://jqueryui.com/) **widgets** pour tous les éléments interactifs (comme les champs ou les boutons) qu’ils contiennent. Cette architecture permet aux développeurs de formulaires d’utiliser un riche ensemble de widgets et modules externes jQuery disponibles dans Forms. Vous pouvez également implémenter une logique spécifique au formulaire lors de l’acquisition des données des utilisateurs comme les restrictions leadDigits/trailDigits ou l’implémentation de clauses d’image. Les développeurs de formulaires peuvent créer et utiliser des apparences personnalisées pour améliorer l’expérience de capture des données et la rendre plus conviviale.

Cet article est destiné aux développeurs possédant des connaissances suffisantes sur jQuery et les widgets jQuery. Il fournit des informations sur la structure de l’apparence et permet aux développeurs de créer une autre apparence pour un champ de formulaire.

La structure de l’apparence repose sur diverses options, événements (déclencheurs) et fonctions pour capturer les interactions utilisateur avec le formulaire et répond aux modifications de modèle pour informer l’utilisateur final. En outre :

* La structure fournit un ensemble d’options pour l’aspect d’un champ. Ces options sont des paires clé-valeur et divisées en deux catégories : les options courantes et les options spécifiques au type de champ.
* L’aspect, dans le cadre du contrat, déclenche un ensemble d’événements tels que enter et quitter.
* L’aspect est requis pour implémenter un ensemble de fonctions. Certaines fonctions sont courantes, tandis que d’autres sont spécifiques aux fonctions de type champ.

## Options communes {#common-options}

Vous trouverez ci-dessous les options globales définies. Ces options sont disponibles pour chaque champ.

<table>
 <tbody>
  <tr>
   <th>Propriété </th>
   <th>Description</th>
  </tr>
  <tr>
   <td>name</td>
   <td>Identificateur qui permet de désigner un objet ou un événement dans les expressions de script. Par exemple, cette propriété indique le nom de l’application hôte.</td>
  </tr>
  <tr>
   <td>value</td>
   <td>Valeur réelle du champ. </td>
  </tr>
  <tr>
   <td>displayValue</td>
   <td>Cette valeur du champ est affichée. </td>
  </tr>
  <tr>
   <td>screenReaderText</td>
   <td>Les Readers d’écran utilisent cette valeur pour narrer les informations sur le champ. Le formulaire fournit la valeur et vous pouvez la remplacer.<br /> </td>
  </tr>
  <tr>
   <td>tabIndex</td>
   <td>Position du champ dans la séquence de tabulation du formulaire. Remplacez tabIndex uniquement si vous souhaitez modifier l’ordre de tabulation par défaut du formulaire.</td>
  </tr>
  <tr>
   <td>rôle</td>
   <td>Rôle de l’élément, par exemple, En-tête ou Tableau.</td>
  </tr>
  <tr>
   <td>hauteur</td>
   <td>Hauteur du widget. Il est spécifié en pixels. </td>
  </tr>
  <tr>
   <td>width</td>
   <td>Largeur du widget. Il est spécifié en pixels.</td>
  </tr>
  <tr>
   <td>access</td>
   <td>Contrôles utilisés pour accéder au contenu d’un objet conteneur, tel qu’un sous-formulaire.</td>
  </tr>
  <tr>
   <td>paraStyles</td>
   <td>La propriété para d’un élément XFA au widget.</td>
  </tr>
  <tr>
   <td>dir</td>
   <td>Orientation du texte. Les valeurs possibles sont ltr (de gauche à droite) et rtl (de droite à gauche).</td>
  </tr>
 </tbody>
</table>

Outre ces options, la structure fournit d’autres options qui varient selon le type de champ. Les détails des options spécifiques aux champs sont répertoriés ci-dessous.

### Interaction avec la structure de formulaires {#interaction-with-forms-framework}

Pour interagir avec la structure de formulaires, un widget déclenche certains événements pour permettre au script de formulaire de fonctionner. Si le widget ne génère pas ces événements, certains des scripts écrits dans le formulaire pour ce champ ne fonctionnent pas.

#### Événements déclenchés par le widget {#events-triggered-by-widget}

<table>
 <tbody>
  <tr>
   <th>Événement </th>
   <th>Description</th>
  </tr>
  <tr>
   <td>XFA_ENTER_EVENT</td>
   <td>Cet événement est déclenché chaque fois que le champ est ciblé. Il autorise l’exécution du script « enter » dans le champ. La syntaxe de déclenchement de l’événement est la suivante :<br /> (widget)._trigger(xfalib.ut.XfaUtil.prototype.XFA_ENTER_EVENT)<br /> </td>
  </tr>
  <tr>
   <td>XFA_EXIT_EVENT</td>
   <td>Cet événement est déclenché chaque fois que l’utilisateur quitte le champ. Il permet au moteur de définir la valeur du champ et d’exécuter le script « exit ». La syntaxe de déclenchement de l’événement est la suivante :<br /> (widget)._trigger(xfalib.ut.XfaUtil.prototype.XFA_EXIT_EVENT)<br /> </td>
  </tr>
  <tr>
   <td>XFA_CHANGE_EVENT</td>
   <td>Cet événement est déclenché pour permettre au moteur d’exécuter le script « change » écrit dans le champ. La syntaxe de déclenchement de l’événement est la suivante :<br /> (widget)._trigger(xfalib.ut.XfaUtil.prototype.XFA_CHANGE_EVENT)<br /> </td>
  </tr>
  <tr>
   <td>XFA_CLICK_EVENT</td>
   <td>Cet événement est déclenché chaque fois que l’utilisateur clique sur le champ. Il permet au moteur d’exécuter le script « click » écrit dans le champ. La syntaxe de déclenchement de l’événement est la suivante :<br /> (widget)._trigger(xfalib.ut.XfaUtil.prototype.XFA_CLICK_EVENT)<br /> </td>
  </tr>
 </tbody>
</table>

#### API implémentées par widget {#apis-implemented-by-widget}

La structure de l’apparence appelle certaines fonctions du widget qui sont implémentées dans les widgets personnalisés. Le widget doit implémenter les fonctions suivantes :

<table>
 <tbody>
  <tr>
   <th>Fonction</th>
   <th>Description</th>
  </tr>
  <tr>
   <td>focus : function()</td>
   <td>Place l’accent sur le champ.</td>
  </tr>
  <tr>
   <td>click: function()</td>
   <td>Se concentre sur le champ et appelle XFA_CLICK_EVENT.</td>
  </tr>
  <tr>
   <td><p>markError:function(errorMessage, errorType)<br /> <br /> <em>errorMessage : chaîne </em>représente l’erreur<br /> <em>errorType : chaîne ("avertissement"/"erreur")</em></p> <p><strong>Remarque</strong>: applicable uniquement aux formulaires HTML5.</p> </td>
   <td>Envoie le message d’erreur et le type d’erreur au widget. Le widget affiche l’erreur.</td>
  </tr>
  <tr>
   <td><p>clearError : function()</p> <p><strong>Remarque</strong>: applicable uniquement aux formulaires HTML5.</p> </td>
   <td>Appelé si les erreurs dans le champ sont corrigées. Le widget masque l’erreur.</td>
  </tr>
 </tbody>
</table>

## Options spécifiques au type de champ {#options-specific-to-type-of-field}

Tous les widgets personnalisés doivent être conformes aux spécifications ci-dessus. Pour utiliser les fonctions de différents champs, le widget doit être conforme aux directives de ce champ particulier.

### TextEdit : champ de texte {#textedit-text-field}

<table>
 <tbody>
  <tr>
   <th>Option</th>
   <th>Description</th>
  </tr>
  <tr>
   <td>multiline</td>
   <td>True si le champ prend en charge la saisie d’un caractère de saut de ligne, sinon false.</td>
  </tr>
  <tr>
   <td>maxChars</td>
   <td>Nombre maximum de caractères pouvant être renseignés dans le champ.</td>
  </tr>
  <tr>
   <td><p>limitLengthToVisibleArea</p> <p><strong>Remarque</strong>: applicable uniquement aux formulaires HTML5</p> </td>
   <td>Indique le comportement du champ de texte lorsque la largeur du texte dépasse la largeur du widget.</td>
  </tr>
 </tbody>
</table>

### ChoiceList : DropDownList, ListBox {#choicelist-dropdownlist-listbox}

<table>
 <tbody>
  <tr>
   <th>Option</th>
   <th>Description</th>
  </tr>
  <tr>
   <td>value<br /> </td>
   <td>Tableau des valeurs sélectionnées.<br /> </td>
  </tr>
  <tr>
   <td>items<br /> </td>
   <td>Tableau d’objets à afficher en tant qu’options. Chaque objet contient deux propriétés :<br /> save : valeur à enregistrer, display : valeur à afficher.<br /> <br /> </td>
  </tr>
  <tr>
   <td><p>dans un état modifiable</p> <p><strong>Remarque</strong>: applicable uniquement aux formulaires HTML5.<br /> </p> </td>
   <td>Si la valeur est true, la saisie de texte personnalisé est activée dans le widget.<br /> </td>
  </tr>
  <tr>
   <td>displayValue<br /> </td>
   <td>Tableau de valeurs à afficher.<br /> </td>
  </tr>
  <tr>
   <td>multiselect<br /> </td>
   <td>True si plusieurs sélections sont autorisées, sinon false.<br /> </td>
  </tr>
 </tbody>
</table>

#### API {#api}

<table>
 <tbody>
  <tr>
   <th>Fonction</th>
   <th>Description</th>
  </tr>
  <tr>
   <td><p>addItem:<em> function(itemValues)<br /> itemValues : objet contenant la valeur display et save <br /> {sDisplayVal : &lt;displayvalue&gt;, sSaveVal : &lt;save value=""&gt;}</em></p> </td>
   <td>Ajoute un élément à la liste.</td>
  </tr>
  <tr>
   <td>deleteItem<em> : function(nIndex)<br /> nIndex : index de l’élément à supprimer de la liste<br /> </em><br /> <br /> </td>
   <td>Supprime une option de la liste. </td>
  </tr>
  <tr>
   <td>clearItems:<code> function()</code></td>
   <td>Efface toutes les options de la liste.</td>
  </tr>
 </tbody>
</table>

### NumericEdit : champ numérique, champ décimal {#numericedit-numericfield-decimalfield}

| Options | Description |
|---|---|
| dataType | Chaîne représentant le type de données du champ (entier/décimal). |
| leadDigits | Nombre maximal de chiffres autorisés dans le nombre décimal. |
| fracDigits | Nombre maximal de chiffres de fraction autorisés dans le nombre décimal. |
| zero | Représentation sous forme de chaîne de zéro dans la langue du champ. |
| decimal | Représentation sous forme de chaîne des décimales dans la langue du champ. |

### CheckButton : RadioButton, CheckBox {#checkbutton-radiobutton-checkbox}

<table>
 <tbody>
  <tr>
   <th>Options</th>
   <th>Description</th>
  </tr>
  <tr>
   <td>values</td>
   <td><p>Tableau de valeurs (activé/désactivé/neutre).</p> <p>Il s’agit d’un tableau de valeurs pour les différents états de checkButton. values[0] est la valeur lorsque l’état est activé, values[1] est la valeur lorsque l’état est désactivé,<br /> values[2] est la valeur lorsque l’état est NEUTRAL. La longueur du tableau de valeurs est égale à la valeur de l’option d’état.<br /> </p> </td>
  </tr>
  <tr>
   <td>states</td>
   <td><p>Nombre d’états autorisés. </p> <p>Deux pour les formulaires adaptatifs (activé, désactivé) et trois pour des formulaires HTML5 (activé, désactivé, neutre).</p> </td>
  </tr>
  <tr>
   <td>state</td>
   <td><p>Etat actuel de l’élément.</p> <p>Deux pour les formulaires adaptatifs (activé, désactivé) et trois pour des formulaires HTML5 (activé, désactivé, neutre).</p> </td>
  </tr>
 </tbody>
</table>

### DateTimeEdit: (DateField) {#datetimeedit-datefield}

| Option | Description |
|---|---|
|  jours | Nom localisé des jours pour ce champ. |
| mois | Noms de mois localisés pour ce champ. |
| zero | Texte localisé pour le nombre 0. |
| clearText | Texte localisé pour le bouton Effacer. |
