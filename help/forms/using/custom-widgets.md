---
title: Créer des apparences personnalisées dans les formulaires HTML5
description: Vous pouvez ajouter des widgets personnalisés à une Forms mobile. Vous pouvez étendre les widgets jQuery existants ou développer vos propres widgets personnalisés.
contentOwner: robhagat
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: hTML5_forms
docset: aem65
feature: Mobile Forms
exl-id: 76bd1e2d-9e65-452c-8cef-123d28886a62
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '635'
ht-degree: 46%

---

# Créer des apparences personnalisées dans les formulaires HTML5{#create-custom-appearances-in-html-forms}

Vous pouvez ajouter des widgets personnalisés à une Forms mobile. Vous pouvez étendre les widgets jQuery existants ou développer vos propres widgets personnalisés à l’aide de la structure des aspects. Le moteur XFA utilise différents widgets. Consultez la section [Framework d’apparence pour les formulaires adaptatifs et HTML5](/help/forms/using/introduction-widgets.md) pour obtenir des informations détaillées.

![Exemple d’un widget par défaut et d’un widget personnalisé](assets/custom-widgets.jpg)

Exemple d’un widget par défaut et d’un widget personnalisé

## Intégration de widgets personnalisés à des formulaires HTML5 {#integrating-custom-widgets-with-html-forms}

### Création d’un profil  {#create-a-profile-nbsp}

Vous pouvez créer un profil ou choisir un profil existant pour ajouter un widget personnalisé. Pour plus d’informations sur la création de profils, voir [Création d’un profil personnalisé](/help/forms/using/custom-profile.md).

### Créer un widget {#create-a-widget}

Les formulaires HTML5 fournissent une implémentation du framework des widgets qui peut être étendu pour créer d’autres widgets. L’implémentation est un widget jQuery *abstractWidget* qui peut être étendu pour écrire un nouveau widget. Le nouveau widget peut être rendu fonctionnel uniquement en étendant/remplaçant les fonctions mentionnées ci-dessous.

<table>
 <tbody>
  <tr>
   <td>Fonction/classe</td>
   <td>Description</td>
  </tr>
  <tr>
   <td>render</td>
   <td>La fonction de rendu renvoie l’objet jQuery pour l’élément de HTML par défaut du widget. L’élément de HTML par défaut doit être de type pouvant faire l’objet d’un focus. Par exemple : &lt;a&gt;, &lt;input&gt;, et &lt;li&gt;. L’élément renvoyé est utilisé comme $userControl. Si $userControl indique la contrainte ci-dessus, les fonctions de la classe AbstractWidget fonctionnent comme prévu. Dans le cas contraire, une partie des API communes (focus, clic) nécessitent des modifications. </td>
  </tr>
  <tr>
   <td>getEventMap</td>
   <td>Renvoie un mappage pour convertir les événements HTML en événements XFA. <br /> {<br /> blur: XFA_EXIT_EVENT,<br /> }<br /> Cet exemple indique que le flou est un événement HTML et que XFA_EXIT_EVENT est l’événement XFA correspondant. </td>
  </tr>
  <tr>
   <td>getOptionsMap</td>
   <td>Renvoie un mappage qui fournit des détails sur l’action à effectuer lors de la modification d’une option. Les clés sont les options fournies au widget et les valeurs sont les fonctions qui sont appelées lorsqu’une modification de cette option est détectée. Le widget fournit des gestionnaires pour toutes les options courantes (à l’exception de value et displayValue)</td>
  </tr>
  <tr>
   <td>getCommitValue</td>
   <td>La structure du widget charge la fonction chaque fois que la valeur du widget est enregistrée dans XFAModel (par exemple, lors de l’événement exit d’un textField). L’implémentation doit renvoyer la valeur qui est enregistrée dans le widget. Le gestionnaire s’accompagne de la nouvelle valeur de l’option.</td>
  </tr>
  <tr>
   <td>showValue</td>
   <td>Par défaut, dans XFA lors de l’événement enter, la rawValue du champ s’affiche. Cette fonction est appelée pour afficher la rawValue à l’utilisateur. </td>
  </tr>
  <tr>
   <td>showDisplayValue</td>
   <td>Par défaut, dans XFA lors de l’événement de sortie, la valeur formattedValue du champ s’affiche. Cette fonction est appelée pour afficher la formattedValue à l’utilisateur. </td>
  </tr>
 </tbody>
</table>

Pour créer votre propre widget, dans le profil créé précédemment, ajoutez les références du fichier Javascript qui contient les fonctions remplacées et les nouvelles fonctions ajoutées. Par exemple, le widget *sliderNumericFieldWidget* est un widget pour les champs numériques. Pour utiliser le widget dans votre profil, dans la section d’en-tête, insérez la ligne suivante :

```javascript
window.formBridge.registerConfig("widgetConfig" , widgetConfigObject);
```

### Enregistrement du widget personnalisé avec le moteur de script XFA  {#register-custom-widget-with-xfa-scripting-engine-nbsp}

Lorsque le code d’un widget personnalisé est prêt, enregistrez le widget avec le moteur de script à l’aide de l’API `registerConfig` pour [Form Bridge](/help/forms/using/form-bridge-apis.md). widgetConfigObject est utilisé comme entrée.

```javascript
window.formBridge.registerConfig("widgetConfig",
        {
        ".<field-identifier>":"<name-of-the-widget>"
        }
    );
```

#### widgetConfigObject {#widgetconfigobject}

La configuration du widget est fournie sous la forme d’un objet JSON (une collection de paires clé-valeur) où la clé identifie les champs et la valeur représente le widget à utiliser avec ces champs. Voici un exemple de configuration :

```
*{*

*"identifier1" : "customwidgetname",
"identifier2" : "customwidgetname2",
..
}*
```

où l’« identifiant » est un sélecteur CSS jQuery qui représente un champ particulier, un ensemble de champs d’un type particulier ou tous les champs. La liste suivante regroupe les valeurs de l’identifiant dans différents cas :

| Type d’identificateur | formulaire | Description |
|---|---|---|
| Champ particulier avec le nom fieldname | Identifiant :&quot;div.fieldname&quot; | Tous les champs portant le nom &quot;fieldname&quot; sont générés à l’aide du widget. |
| Tous les champs de type « type » (où type est NumericField, DateField, etc.). : | Identifiant : &quot;div.type&quot; | Dans Timefield et DateTimeField, le type est textfield, ces champs n’étant plus pris en charge. |
| Tous les champs | Identifiant : « div.field » |  |
