---
title: Création de formulaires adaptatifs à l’aide d’un schéma JSON
seo-title: Création de formulaires adaptatifs à l’aide d’un schéma JSON
description: Les formulaires adaptatifs peuvent utiliser un schéma JSON en tant que modèle de formulaire, ce qui vous permet d’exploiter les modèles JSON existants pour créer des formulaires adaptatifs.
seo-description: Les formulaires adaptatifs peuvent utiliser un schéma JSON en tant que modèle de formulaire, ce qui vous permet d’exploiter les modèles JSON existants pour créer des formulaires adaptatifs.
uuid: bdeaeae8-65a3-4c46-b27d-fe68481e31f1
topic-tags: develop
products: SG_EXPERIENCEMANAGER/6.5/FORMS
discoiquuid: 375ba8fc-3152-4564-aec5-fcff2a95cf4c
docset: aem65
translation-type: tm+mt
source-git-commit: 4ecf5efc568cd21f11801a71d491c3d75ca367fe

---


# Création de formulaires adaptatifs à l’aide d’un schéma JSON{#creating-adaptive-forms-using-json-schema}

## Conditions préalables {#prerequisites}

La création d’un formulaire adaptatif à l’aide d’un schéma JSON en tant que modèle de formulaire requiert des connaissances de base en matière de schémas JSON. Il est recommandé de lire le contenu suivant avant cet article.

* [Création d’un formulaire adaptatif](../../forms/using/creating-adaptive-form.md)
* [Schéma JSON](https://json-schema.org/)

## Utilisation d’un schéma JSON comme modèle de formulaire  {#using-a-json-schema-as-form-model}

AEM Forms prend en charge la création d’un formulaire adaptatif en utilisant un schéma JSON existant en tant que modèle de formulaire. Ce schéma JSON représente la structure dans laquelle les données sont générées ou utilisées par le système principal de votre organisation. Le schéma JSON que vous utilisez doit être compatible avec les [spécifications v4](https://json-schema.org/draft-04/schema).

Les principales fonctionnalités de l’utilisation d’un schéma JSON sont les suivantes :

* La structure du modèle JSON s’affiche sous forme d’arborescence sous l’onglet Outil de recherche de contenu en mode création pour un formulaire adaptatif. Vous pouvez faire glisser et ajouter un élément de la hiérarchie JSON dans le formulaire adaptatif.
* Vous pouvez préremplir le formulaire avec le code JSON conforme au schéma associé.
* Au moment de l’envoi, les données saisies par l’utilisateur sont envoyées au format JSON approprié pour le schéma associé.

Un schéma JSON se compose de types d’éléments simples et complexes. Les éléments possèdent des attributs qui ajoutent des règles à ceux-ci. Lorsque ces éléments et attributs sont déplacés vers un formulaire adaptatif, ils sont automatiquement mis en correspondance avec les composants de formulaires adaptatifs correspondants.

Cette mise en correspondance des éléments JSON avec les composants de formulaires adaptatifs est la suivante :

```
"birthDate": {
              "type": "string",
              "format": "date",
              "pattern": "date{DD MMMM, YYYY}",
              "aem:affKeyword": [
                "DOB",
                "Date of Birth"
              ],
              "description": "Date of birth in DD MMMM, YYYY",
              "aem:afProperties": {
                "displayPictureClause": "date{DD MMMM, YYYY}",
                "displayPatternType": "date{DD MMMM, YYYY}",
                "validationPatternType": "date{DD MMMM, YYYY}",
                "validatePictureClause": "date{DD MMMM, YYYY}",
                "validatePictureClauseMessage": "Date must be in DD MMMM, YYYY format."
              }
```

<table>
 <tbody>
  <tr>
   <th><strong>Élément, propriétés ou attributs JSON</strong></th>
   <th><strong>Composant de formulaire adaptatif</strong></th>
  </tr>
  <tr>
   <td><p>Propriétés de chaîne avec les contraintes enum et enumNames.</p> <p>Syntaxe,</p> <p> <code>{</code></p> <p><code>"type" : "string",</code></p> <p><code>"enum" : ["M", "F"]</code></p> <p><code>"enumNames" : ["Male", "Female"]</code></p> <p><code>}</code></p> <p> </p> </td>
   <td><p>Composant de liste déroulante :</p>
    <ul>
     <li>Les valeurs énumérées dans enumNames s’affichent dans la boîte de dialogue.</li>
     <li>Les valeurs répertoriées dans l’énumération sont utilisées pour le calcul.</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p>Propriété de chaîne avec contrainte de format. Par exemple, e-mail et date.</p> <p>Syntaxe,</p> <p><code>{</code></p> <p><code>"type" : "string",</code></p> <p><code>"format" : "email"</code></p> <p><code>}</code></p> <p> </p> </td>
   <td>
    <ul>
     <li>Le composant de message électronique est mappé lorsque le type est une chaîne et le format un message électronique.</li>
     <li>Le composant de textbox avec validation est mappé lorsque le type est une chaîne et le format un nom d’hôte.</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p>{</p> <p>"type" : "string",</p> <p>}</p> </td>
   <td><br /> <br /> Champ de texte<br /> <br /> <br /> </td>
  </tr>
  <tr>
   <td>propriété de nombre<br /> </td>
   <td>Champ numérique dont le sous-type est défini comme flottant<br /> </td>
  </tr>
  <tr>
   <td>Propriété Entier<br /> </td>
   <td>Champ numérique dont le sous-type est défini sur entier<br /> </td>
  </tr>
  <tr>
   <td>Propriété Booléen<br /> </td>
   <td>Basculer<br /> </td>
  </tr>
  <tr>
   <td>Propriété de l’objet<br /> </td>
   <td>Panneau<br /> </td>
  </tr>
  <tr>
   <td>Propriété de tableau</td>
   <td>Panneau répétable avec le minimum et le maximum égaux aux minItems et maxItems respectivement. Seuls les tableaux homogènes sont pris en charge. Par conséquent, la contrainte d’éléments doit être un objet et n’est pas un tableau.<br /> </td>
  </tr>
 </tbody>
</table>

### Propriétés communes de schéma {#common-schema-properties}

Le formulaire adaptatif utilise les informations disponibles dans le schéma JSON pour mapper chaque champ généré. En particulier :

* La propriété title sert de libellé aux composants du formulaire adaptatif.
* La propriété description est définie comme une description longue pour un composant de formulaire adaptatif.
* La propriété par défaut sert de valeur initiale à un champ de formulaire adaptatif.
* La propriété maxLength est définie comme attribut maxlength du composant de champ de texte.
* Les propriétés minimales, maximales, exclusivesMinimum et exclusivesMaximum sont utilisées pour le composant de zone numérique.
* Pour prendre en charge la plage du composant DatePicker, d’autres propriétés de schéma JSON minDate et maxDate sont fournies.
* Les propriétés minItems et maxItems permettent de limiter le nombre d’éléments/de champs qui peuvent être ajoutés ou supprimés d’un composant de panneau.
* La propriété readOnly définit l’attribut readonly d’un composant de formulaire adaptatif.
* La propriété requise marque le champ du formulaire adaptatif comme étant obligatoire, alors que dans le cas d’un panneau (où type est objet), les données JSON finales envoyées comportent des champs avec une valeur vide correspondant à cet objet.
* La propriété pattern est définie en tant que modèle de validation (expression régulière) dans le formulaire adaptatif.
* L’extension du fichier de schéma JSON doit être conservée dans .schema.json. Par exemple, &lt;nom_fichier>.schema.json.

## Exemple de schéma JSON {#sample-json-schema}

Vous trouverez ci-dessous un exemple de schéma JSON.

```
{
 "$schema": "https://json-schema.org/draft-04/schema#",
 "definitions": {
  "employee": {
   "type": "object",
   "properties": {
    "userName": {
     "type": "string"
    },
    "dateOfBirth": {
     "type": "string",
     "format": "date"
    },
    "email": {
     "type": "string",
     "format": "email"
    },
    "language": {
     "type": "string"
    },
    "personalDetails": {
     "$ref": "#/definitions/personalDetails"
    },
    "projectDetails": {
     "$ref": "#/definitions/projectDetails"
    }
   },
   "required": [
    "userName",
    "dateOfBirth",
    "language"
   ]
  },
  "personalDetails": {
   "type": "object",
   "properties": {
    "GeneralDetails": {
     "$ref": "#/definitions/GeneralDetails"
    },
    "Family": {
     "$ref": "#/definitions/Family"
    },
    "Income": {
     "$ref": "#/definitions/Income"
    }
   }
  },
  "projectDetails": {
   "type": "array",
   "items": {
    "properties": {
     "name": {
      "type": "string"
     },
     "age": {
      "type": "number"
     },
     "projects": {
      "$ref": "#/definitions/projects"
     }
    }
   },
   "minItems": 1,
   "maxItems": 4
  },
  "projects": {
   "type": "array",
   "items": {
    "properties": {
     "name": {
      "type": "string"
     },
     "age": {
      "type": "number"
     },
     "projectsAdditional": {
      "$ref": "#/definitions/projectsAdditional"
     }
    }
   },
   "minItems": 1,
   "maxItems": 4
  },
  "projectsAdditional": {
   "type": "array",
   "items": {
    "properties": {
     "Additional_name": {
      "type": "string"
     },
     "Additional_areacode": {
      "type": "number"
     }
    }
   },
   "minItems": 1,
   "maxItems": 4
  },
  "GeneralDetails": {
   "type": "object",
   "properties": {
    "age": {
     "type": "number"
    },
    "married": {
     "type": "boolean"
    },
    "phone": {
     "type": "number",
     "aem:afProperties": {
      "sling:resourceType": "/libs/fd/af/components/guidetelephone",
      "guideNodeClass": "guideTelephone"
     }
    },
    "address": {
     "type": "string"
    }
   }
  },
  "Family": {
   "type": "object",
   "properties": {
    "spouse": {
     "$ref": "#/definitions/spouse"
    },
    "kids": {
     "$ref": "#/definitions/kids"
    }
   }
  },
  "Income": {
   "type": "object",
   "properties": {
    "monthly": {
     "type": "number"
    },
    "yearly": {
     "type": "number"
    }
   }
  },
  "spouse": {
   "type": "object",
   "properties": {
    "name": {
     "type": "string"
    },
    "Income": {
     "$ref": "#/definitions/Income"
    }
   }
  },
  "kids": {
   "type": "array",
   "items": {
    "properties": {
     "name": {
      "type": "string"
     },
     "age": {
      "type": "number"
     }
    }
   },
   "minItems": 1,
   "maxItems": 4
  }
 },
 "type": "object",
 "properties": {
  "employee": {
   "$ref": "#/definitions/employee"
  }
 }
}
```

### Définitions de schéma réutilisables {#reusable-schema-definitions}

Les touches de définition sont utilisées pour identifier les schémas réutilisables. Les définitions de schéma réutilisables sont utilisées pour créer des fragments. Il est semblable à l’identification des types complexes dans XSD. Un exemple de schéma JSON dont la définition est fournie ci-dessous :

```
{
  "$schema": "https://json-schema.org/draft-04/schema#",

  "definitions": {
    "address": {
      "type": "object",
      "properties": {
        "street_address": { "type": "string" },
        "city":           { "type": "string" },
        "state":          { "type": "string" }
      },
      "required": ["street_address", "city", "state"]
    }
  },

  "type": "object",

  "properties": {
    "billing_address": { "$ref": "#/definitions/address" },
    "shipping_address": { "$ref": "#/definitions/address" }
  }
}
```

L’exemple ci-dessus définit un enregistrement de client dans lequel chaque client dispose d’une expédition et d’une adresse de facturation. La structure des deux adresses est la même : les adresses indiquent une rue, la ville et un état. Il est donc préférable de ne pas dupliquer les adresses. Cela simplifie également l’ajout et la suppression de champs simples pour toutes les nouvelles modifications.

## Préconfiguration des champs dans la définition du schéma JSON {#pre-configuring-fields-in-json-schema-definition}

You can use the **aem:afProperties** property to preconfigure JSON Schema field to map to a custom adaptive form component. Un exemple est répertorié ci-dessous :

```
{
    "properties": {
        "sizeInMB": {
            "type": "integer",
            "minimum": 16,
            "maximum": 512,
            "aem:afProperties" : {
                 "sling:resourceType" : "/apps/fd/af/components/guideTextBox",
                 "guideNodeClass" : "guideTextBox"
             }
        }
    },
    "required": [ "sizeInMB" ],
    "additionalProperties": false
}
```

## Configuration de scripts ou d’expressions pour les objets de formulaire {#configure-scripts-or-expressions-for-form-objects}

JavaScript est le langage d’expression utilisé pour les formulaires adaptatifs. Toutes les expressions sont des expressions JavaScript valides qui utilisent des API de modèle de script pour les formulaires adaptatifs. Vous pouvez préconfigurer des objets de formulaire pour [évaluer une expression](../../forms/using/adaptive-form-expressions.md) sur un événement de formulaire.

Utilisez la propriété aem:afproperties pour préconfigurer les expressions ou scripts de formulaire adaptatif pour les composants de formulaire adaptatif. Par exemple, lorsque l’événement initialize est déclenché, le code ci-dessous définit la valeur du champ de téléphone et imprime une valeur dans le journal :

```
"telephone": {
  "type": "string",
  "pattern": "/\\d{10}/",
  "aem:affKeyword": ["phone", "telephone","mobile phone", "work phone", "home phone", "telephone number", "telephone no", "phone number"],
  "description": "Telephone Number",
  "aem:afProperties" : {
    "sling:resourceType" : "fd/af/components/guidetelephone",
    "guideNodeClass" : "guideTelephone",
    "events": {
      "Initialize" : "this.value = \"1234567890\"; console.log(\"ef:gh\") "
    }
  }
}
```

Vous devez être membre du groupe [](/help/forms/using/forms-groups-privileges-tasks.md) forms-power-user pour configurer des scripts ou des expressions pour l’objet de formulaire. Le tableau ci-dessous répertorie tous les événements de script pris en charge pour un composant de formulaire adaptatif.

<table>
 <tbody>
  <tr>
   <th><strong></strong>Composant \ Evénement</th>
   <th>initialize <br /> </th>
   <td>Calculer</td>
   <td>Visibilité</td>
   <td>Valider</td>
   <td>Activé</td>
   <td>Validation de la valeur</td>
   <td>Cliquez sur </td>
   <td>Options</td>
  </tr>
  <tr>
   <td>Champ de texte</td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td>Champ numérique</td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td>Procédure pas à pas numérique</td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td>Bouton radio</td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td>Téléphone</td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td>Basculer</td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td>Bouton</td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
  </tr>
  <tr>
   <td>Case à cocher</td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
  </tr>
  <tr>
   <td>Liste déroulante</td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
  </tr>
  <tr>
   <td>Choix d’image</td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
  </tr>
  <tr>
   <td>Champ de saisie de date</td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td>Sélecteur de date</td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td>Courriel</td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td>Pièce jointe</td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td>Image</td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td> </td>
   <td> </td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td>Dessin</td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td> </td>
   <td> </td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td>Panneau</td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td><img alt="" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td> </td>
   <td> </td>
   <td> </td>
   <td> </td>
  </tr>
 </tbody>
</table>

Certains exemples d’utilisation d’événements dans un JSON masquent un champ sur un événement initialize et configurent la valeur d’un autre champ sur un événement de validation de valeur. Pour plus d’informations sur la création d’expressions pour les événements de script, voir Expressions [de formulaire](../../forms/using/adaptive-form-expressions.md)adaptatif.

Voici l’exemple de code JSON pour les exemples susmentionnés.

### Masquage d’un champ sur un événement initialize {#hiding-a-field-on-initialize-event}

```
"name": {
    "type": "string",
    "aem:afProperties": {
        "events" : {
            "Initialize" : "this.visible = false;"
        }
    }
}
```

#### Configurer la valeur d’un autre champ sur l’événement de validation de valeur {#configure-value-of-another-field-on-value-commit-event}

```
"Income": {
    "type": "object",
    "properties": {
        "monthly": {
            "type": "number",
            "aem:afProperties": {
                "events" : {
                    "Value Commit" : "IncomeYearly.value = this.value * 12;"
                }
            }
        },
        "yearly": {
            "type": "number",
            "aem:afProperties": {
                "name": "IncomeYearly"
            }
        }
    }
}
```

## Valeurs possibles de limite pour un composant de formulaire adaptatif {#limit-acceptable-values-for-an-adaptive-form-component}

Vous pouvez ajouter les restrictions suivantes aux éléments de schéma JSON pour limiter les valeurs acceptables pour un composant de formulaire adaptatif :

<table>
 <tbody>
  <tr>
   <td><p><strong> Propriété de schéma</strong></p> </td>
   <td><p><strong>Type de données</strong></p> </td>
   <td><p><strong>Description</strong></p> </td>
   <td><p><strong>Component</strong></p> </td>
  </tr>
  <tr>
   <td><p><code>maximum</code></p> </td>
   <td><p>Chaîne</p> </td>
   <td><p>Spécifie la limite supérieure pour les valeurs numériques et les dates. Par défaut, la valeur maximale est incluse.</p> </td>
   <td>
    <ul>
     <li>Champ numérique</li>
     <li>Procédure pas à pas numérique<br /> </li>
     <li>Sélecteur de date</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p><code>minimum</code></p> </td>
   <td><p>Chaîne</p> </td>
   <td><p>Définit la limite inférieure pour les valeurs numériques et les dates. Par défaut, la valeur minimale est incluse.</p> </td>
   <td>
    <ul>
     <li>Champ numérique</li>
     <li>Procédure pas à pas numérique</li>
     <li>Sélecteur de date</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p><code>exclusiveMaximum</code></p> </td>
   <td><p>Booléen  </p> </td>
   <td><p>Si elle est définie sur true, la valeur numérique ou la date spécifiée dans le composant de formulaire doit être inférieure à la valeur numérique ou la date spécifiée pour la propriété maximum.</p> <p>Si elle est définie sur false, la valeur numérique ou la date spécifiée dans le composant de formulaire doit inférieure ou égale à la valeur numérique ou la date spécifiée pour la propriété maximum.</p> </td>
   <td>
    <ul>
     <li>Champ numérique</li>
     <li>Procédure pas à pas numérique</li>
     <li>Sélecteur de date</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p><code>exclusiveMinimum</code></p> </td>
   <td><p>Booléen  </p> </td>
   <td><p>Si elle est définie sur true, la valeur numérique ou la date spécifiée dans le composant de formulaire doit être supérieure à la valeur numérique ou la date spécifiée pour la propriété minimum.</p> <p>Si elle est définie sur false, la valeur numérique ou la date spécifiée dans le composant de formulaire doit être supérieure ou égale à la valeur numérique ou la date spécifiée pour la propriété minimum.</p> </td>
   <td>
    <ul>
     <li>Champ numérique</li>
     <li>Procédure pas à pas numérique</li>
     <li>Sélecteur de date</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p><code>minLength</code></p> </td>
   <td><p>Chaîne</p> </td>
   <td><p>Indique le nombre minimum de caractères autorisés dans un composant. La longueur minimale doit être égale ou supérieure à zéro.</p> </td>
   <td>
    <ul>
     <li>Zone de texte</li>
    </ul> </td>
  </tr>
  <tr>
   <td><code>maxLength</code></td>
   <td>Chaîne</td>
   <td>Spécifie le nombre maximal de caractères autorisés dans un composant. La longueur maximale doit être égale ou supérieure à zéro.</td>
   <td>
    <ul>
     <li>Zone de texte</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p><code>pattern</code></p> </td>
   <td><p>Chaîne</p> </td>
   <td><p>Spécifie la séquence de caractères. Un composant accepte les caractères si les caractères sont conformes au modèle spécifié.</p> <p>Les propriétés de motif mappent vers le motif de validation du composant de formulaire adaptatif correspondant.</p> </td>
   <td>
    <ul>
     <li>Tous les composants de formulaires adaptatifs qui sont mappés vers un schéma XSD </li>
    </ul> </td>
  </tr>
  <tr>
   <td>maxItems</td>
   <td>Chaîne</td>
   <td>Indique le nombre maximum d’éléments dans un tableau. Le nombre maximal d’éléments doit être égal ou supérieur à zéro.</td>
   <td> </td>
  </tr>
  <tr>
   <td>minItems</td>
   <td>Chaîne</td>
   <td>Indique le nombre minimum d’éléments dans un tableau. Le nombre d’éléments minimum doit être égal ou supérieur à zéro.</td>
   <td> </td>
  </tr>
 </tbody>
</table>

## Éléments non pris en charge  {#non-supported-constructs}

Les formulaires adaptatifs ne prennent pas en charge les éléments suivants de schéma JSON :

* Type nul
* Types d’union tels quels et
* OneOf, AnyOf, AllOf, et NOT
* Seuls les tableaux homogènes sont pris en charge. Par conséquent, la contrainte d’éléments doit être un objet et ne doit pas être un tableau.

## Forum aux questions {#frequently-asked-questions}

**Pourquoi est-ce que je ne parviens pas à faire glisser des éléments individuels d’un sous-formulaire (structure générée à partir de n’importe quel type complexe) pour les sous-formulaires répétables (les valeurs minOccurs ou maxOccurs sont supérieures à 1) ?**

Dans un sous-formulaire répétable, vous devez utiliser le sous-formulaire complet. Si vous souhaitez uniquement des champs sélectifs, utilisez la structure entière et supprimez les champs indésirables.

**Je dispose d’une longue structure complexe dans l’Outil de recherche de contenu. Comment puis-je trouver un élément spécifique ?**

Vous disposez de deux options :

* Parcourez la structure de l’arborescence. 
* Utilisez la zone Rechercher pour rechercher un élément.

**Quelle doit être l’extension du fichier de schéma JSON ?**

L’extension du fichier de schéma JSON doit être .schema.json. Par exemple, &lt;nom_fichier>.schema.json.
