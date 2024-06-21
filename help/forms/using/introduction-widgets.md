---
title: Structure de l’apparence des formulaires adaptatifs et HTML5
description: Mobile Forms génère des modèles de formulaire sous forme de formulaires HTML5. Ces formulaires utilisent les fichiers jQuery, Backbone.js et Underscore.js pour l’apparence et l’activation des scripts.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: customization
exl-id: 3458471a-9815-463e-8044-68631073863c
solution: Experience Manager, Experience Manager Forms
feature: HTML5 Forms
role: User, Developer
source-git-commit: e821be5233fd5f6688507096790d219d25903892
workflow-type: tm+mt
source-wordcount: '1152'
ht-degree: 100%

---

# Structure de l’apparence des formulaires adaptatifs et HTML5 {#appearance-framework-for-adaptive-and-html-forms}

Les formulaires (formulaires adaptatifs et HTML5) utilisent [jQuery](https://jquery.com/), [Backbone.js](https://backbonejs.org/) et [Underscore.js](https://underscorejs.org/) pour l’apparence et les scripts. Les formulaires utilisent également l’architecture des [jQuery UI](https://jqueryui.com/) **widgets** pour tous les éléments interactifs (comme les champs ou les boutons) qu’ils contiennent. Cette architecture permet aux développeurs et aux développeuses de formulaires d’utiliser un riche ensemble de widgets et de modules externes jQuery disponibles dans des formulaires. Vous pouvez également implémenter une logique spécifique au formulaire lors de l’acquisition des données des utilisateurs comme les restrictions leadDigits/trailDigits ou l’implémentation de clauses d’image. Les développeurs et développeuses de formulaires peuvent créer et utiliser des apparences personnalisées pour améliorer l’expérience d’acquisition des données et la rendre plus facile d’utilisation.

Cet article est destiné aux développeurs et aux développeuses possédant des connaissances suffisantes de jQuery et des widgets jQuery. Il fournit des informations sur la structure de l’apparence et permet aux développeurs et aux développeuses de créer une apparence alternative pour un champ de formulaire.

La structure de l’apparence repose sur différentes options, événements (déclencheurs) et fonctions pour capturer les interactions de l’utilisateur ou de l’utilisatrice avec le formulaire, et répond aux changements de modèle pour informer l’utilisateur final. En outre :

* La structure offre un ensemble d’options pour l’apparence d’un champ. Ces options sont des paires clé/valeur et sont divisées en deux catégories : les options communes et les options spécifiques à un type de champ.
* L’apparence, en tant que partie du contrat, déclenche un ensemble d’événements, par exemple, entrer et quitter.
* L’apparence est requise pour implémenter un ensemble de fonctions. Certaines fonctions sont communes, tandis que d’autres sont spécifiques au type de champ.

## Options communes {#common-options}

Les options globales définies sont décrites ci-après. Ces options sont disponibles pour chaque champ.

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
   <td>Les lecteurs d’écran utilisent cette valeur pour énoncer des informations sur le champ. Le formulaire fournit la valeur et vous pouvez la remplacer.<br /> </td>
  </tr>
  <tr>
   <td>tabIndex</td>
   <td>Position du champ dans la séquence de tabulation du formulaire. Remplacez tabIndex uniquement si vous souhaitez modifier l’ordre de tabulation par défaut du formulaire.</td>
  </tr>
  <tr>
   <td>role</td>
   <td>Rôle de l’élément, par exemple, un en-tête ou un tableau.</td>
  </tr>
  <tr>
   <td>height</td>
   <td>Hauteur du widget. Elle est spécifiée en pixels. </td>
  </tr>
  <tr>
   <td>width</td>
   <td>Largeur du widget. Elle est spécifiée en pixels.</td>
  </tr>
  <tr>
   <td>access</td>
   <td>Définit l’accès au contenu d’un objet conteneur, tel qu’un sous-formulaire.</td>
  </tr>
  <tr>
   <td>paraStyles</td>
   <td>La propriété Para d’un élément XFA au widget.</td>
  </tr>
  <tr>
   <td>dir</td>
   <td>La direction du texte. Les valeurs possibles sont ltr (de gauche à droite) et rtl (de droite à gauche).</td>
  </tr>
 </tbody>
</table>

En plus de ces options, la structure offre quelques autres options qui varient selon le type de champ. Les détails des options propres aux champs sont répertoriés ci-dessous.

### Interaction avec la structure des formulaires {#interaction-with-forms-framework}

Pour interagir avec la structure des formulaires, un widget déclenche certains événements pour activer l’exécution du script de formulaire. Si le widget n’exécute pas ces événements, certains des scripts écrits dans le formulaire qui concernent ce champ ne fonctionnent pas.

#### Événements déclenchés par un widget {#events-triggered-by-widget}

<table>
 <tbody>
  <tr>
   <th>Événement </th>
   <th>Description</th>
  </tr>
  <tr>
   <td>XFA_ENTER_EVENT</td>
   <td>Cet événement est déclenché chaque fois que le champ est ciblé. Il autorise l’exécution du script « enter » dans le champ. La syntaxe de déclenchement de l’événement est <br /> (widget)._trigger(xfalib.ut.XfaUtil.prototype.XFA_ENTER_EVENT)<br /> </td>
  </tr>
  <tr>
   <td>XFA_EXIT_EVENT</td>
   <td>Cet événement est déclenché chaque fois que l’utilisateur ou l’utilisatrice quitte le champ. Il permet au moteur de définir la valeur du champ et d’exécuter le script « exit ». La syntaxe de déclenchement de l’événement est <br /> (widget)._trigger(xfalib.ut.XfaUtil.prototype.XFA_EXIT_EVENT)<br /> </td>
  </tr>
  <tr>
   <td>XFA_CHANGE_EVENT</td>
   <td>Cet événement est déclenché pour permettre au moteur d’exécuter le script « change » écrit dans le champ. La syntaxe de déclenchement de l’événement est <br /> (widget)._trigger(xfalib.ut.XfaUtil.prototype.XFA_CHANGE_EVENT)<br /> </td>
  </tr>
  <tr>
   <td>XFA_CLICK_EVENT</td>
   <td>Cet événement est déclenché chaque fois que l’utilisateur ou l’utilisatrice clique sur le champ. Il permet au moteur d’exécuter le script « click » écrit dans le champ. La syntaxe de déclenchement de l’événement est <br /> (widget)._trigger(xfalib.ut.XfaUtil.prototype.XFA_CLICK_EVENT)<br /> </td>
  </tr>
 </tbody>
</table>

#### API implémentées par un widget {#apis-implemented-by-widget}

La structure de l’apparence appelle certaines fonctions du widget qui sont implémentées dans les widgets personnalisés. Le widget doit implémenter les fonctions suivantes :

<table>
 <tbody>
  <tr>
   <th>Fonction</th>
   <th>Description</th>
  </tr>
  <tr>
   <td>focus: function()</td>
   <td>Sélectionne le champ.</td>
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
   <td><p>clearError: function()</p> <p><strong>Remarque</strong> : applicable uniquement aux formulaires HTML5.</p> </td>
   <td>Appelé si les erreurs dans le champ sont corrigées. Le widget masque l’erreur.</td>
  </tr>
 </tbody>
</table>

## Options spécifiques au type de champ {#options-specific-to-type-of-field}

Tous les widgets personnalisés doivent être conformes aux spécifications ci-dessus. Pour utiliser les fonctions de différents champs, le widget doit être conforme aux directives de ce champ particulier.

### TextEdit : champ de texte {#textedit-text-field}

<table>
 <tbody>
  <tr>
   <th>Option</th>
   <th>Description</th>
  </tr>
  <tr>
   <td>multiLine</td>
   <td>Valeur True si le champ prend en charge la saisie d’un caractère de saut de ligne, valeur False dans le cas contraire.</td>
  </tr>
  <tr>
   <td>maxChars</td>
   <td>Nombre maximum de caractères pouvant être entrés dans le champ.</td>
  </tr>
  <tr>
   <td><p>limitLengthToVisibleArea</p> <p><strong>Remarque</strong> : applicable uniquement aux formulaires HTML5</p> </td>
   <td>Spécifie le comportement du champ de texte lorsque la largeur du texte dépasse la largeur du widget.</td>
  </tr>
 </tbody>
</table>

### ChoiceList: DropDownList, ListBox {#choicelist-dropdownlist-listbox}

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
   <td>Tableau des objets à afficher comme des options. Chaque objet contient deux propriétés :<br /> save : valeur à enregistrer, display : valeur à afficher.<br /> <br /> </td>
  </tr>
  <tr>
   <td><p>dans un état modifiable</p> <p><strong>Remarque</strong> : applicable uniquement aux formulaires HTML5.<br /> </p> </td>
   <td>Si la valeur est True, la saisie de texte personnalisé est activée dans le widget.<br /> </td>
  </tr>
  <tr>
   <td>displayValue<br /> </td>
   <td>Tableau des valeurs à afficher.<br /> </td>
  </tr>
  <tr>
   <td>multiselect<br /> </td>
   <td>Valeur True si plusieurs sélections sont autorisées, valeur False dans le cas contraire.<br /> </td>
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
   <td><p>addItem:<em> function(itemValues)<br /> itemValues : objet contenant les valeurs d’affichage et d’enregistrement <br /> {sDisplayVal: &lt;displayValue&gt;, sSaveVal: &lt;save Value&gt;}</em></p> </td>
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

### NumericEdit: NumericField, DecimalField {#numericedit-numericfield-decimalfield}

| Options | Description |
|---|---|
| dataType | Chaîne représentant le type de données du champ (entier/décimal). |
| leadDigits | Nombre maximal de chiffres autorisés dans la partie entière du nombre décimal. |
| fracDigits | Nombre maximal de chiffres autorisés dans la partie décimale du nombre décimal. |
| zero | Chaîne représentant zéro selon la langue du champ. |
| decimal | Chaîne représentant les décimales selon la langue du champ. |

### CheckButton : RadioButton, CheckBox {#checkbutton-radiobutton-checkbox}

<table>
 <tbody>
  <tr>
   <th>Options</th>
   <th>Description</th>
  </tr>
  <tr>
   <td>values</td>
   <td><p>Gamme de valeurs (activé/désactivé/neutre).</p> <p>Il s’agit d’une gamme de valeurs pour les différents états de l’objet checkButton. values[0] représente la valeur lorsque l’état est Activé, values[1] lorsque l’état est Désactivé, <br /> values[2] lorsque l’état est Neutre. La longueur de la gamme de valeurs est égale à la valeur de l’option des états.<br /> </p> </td>
  </tr>
  <tr>
   <td>states</td>
   <td><p>Nombre d’états autorisés. </p> <p>Deux pour les formulaires adaptatifs (activé, désactivé) et trois pour des formulaires HTML5 (activé, désactivé, neutre).</p> </td>
  </tr>
  <tr>
   <td>state</td>
   <td><p>État actuel de l’élément.</p> <p>Deux pour les formulaires adaptatifs (activé, désactivé) et trois pour des formulaires HTML5 (activé, désactivé, neutre).</p> </td>
  </tr>
 </tbody>
</table>

### DateTimeEdit: (DateField) {#datetimeedit-datefield}

| Option | Description |
|---|---|
|  jours | Nom localisé des jours pour ce champ. |
| mois | Nom localisé des mois pour ce champ. |
| zero | Texte localisé pour le chiffre 0. |
| clearText | Texte localisé pour le bouton Effacer. |
