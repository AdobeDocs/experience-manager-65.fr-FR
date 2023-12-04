---
title: Comment créer un formulaire adaptatif à l’aide d’un schéma JSON ?
description: Découvrez comment créer un formulaire adaptatif à l’aide d’un schéma JSON en tant que modèle de formulaire. Vous pouvez utiliser des schémas JSON existants pour créer des formulaires adaptatifs. Explorez en détail un exemple de schéma JSON, préconfigurez les champs dans la définition de schéma JSON, limitez les valeurs possibles pour un composant de formulaire adaptatif et découvrez les éléments non pris en charge.
feature: Adaptive Forms
role: User, Developer
level: Beginner, Intermediate
exl-id: 1b402aef-a319-4d32-8ada-cadc86f5c872
source-git-commit: bd86d647fdc203015bc70a0f57d5b94b4c634bf9
workflow-type: tm+mt
source-wordcount: '1844'
ht-degree: 48%

---

# Création de formulaires adaptatifs à l’aide d’un schéma JSON {#creating-adaptive-forms-using-json-schema}

<span class="preview"> Adobe recommande d’utiliser la capture de données moderne et extensible. [Composants principaux](https://experienceleague.adobe.com/docs/experience-manager-core-components/using/adaptive-forms/introduction.html?lang=fr) pour [création d’un Forms adaptatif](/help/forms/using/create-an-adaptive-form-core-components.md) ou [Ajout de Forms adaptatif à des pages AEM Sites](/help/forms/using/create-or-add-an-adaptive-form-to-aem-sites-page.md). Ces composants représentent une avancée significative dans la création de Forms adaptatif, ce qui garantit des expériences utilisateur impressionnantes. Cet article décrit l’approche plus ancienne de la création de Forms adaptatif à l’aide de composants de base. </span>

| Version | Lien de l’article |
| -------- | ---------------------------- |
| AEM as a Cloud Service | [Cliquez ici](https://experienceleague.adobe.com/docs/experience-manager-cloud-service/content/forms/adaptive-forms-authoring/authoring-adaptive-forms-foundation-components/create-an-adaptive-form-on-forms-cs/adaptive-form-json-schema-form-model.html?lang=fr) |
| AEM 6.5 | Cet article |


## Prérequis {#prerequisites}

La création d’un formulaire adaptatif à l’aide d’un schéma JSON en tant que modèle de formulaire requiert des connaissances de base en matière de schémas JSON. Il est recommandé de lire le contenu suivant avant cet article.

* [Création d’un formulaire adaptatif](creating-adaptive-form.md)
* [Schéma JSON](https://json-schema.org/)

## Utilisation d’un schéma JSON comme modèle de formulaire  {#using-a-json-schema-as-form-model}

[!DNL Adobe Experience Manager Forms] prend en charge la création d’un formulaire adaptatif en utilisant un schéma JSON existant en tant que modèle de formulaire. Ce schéma JSON représente la structure dans laquelle les données sont générées ou utilisées par le système back-end de votre organisation.  Le schéma JSON que vous utilisez doit être compatible avec les [spécifications v4](https://json-schema.org/draft-04/schema).

Les fonctionnalités clés de l’utilisation d’un schéma JSON sont les suivantes :

* La structure du modèle JSON s’affiche sous forme d’arborescence sous l’onglet Outil de recherche de contenu en mode création pour un formulaire adaptatif. Vous pouvez faire glisser et ajouter un élément de la hiérarchie JSON au formulaire adaptatif.
* Vous pouvez préremplir le formulaire à l’aide de JSON conforme au schéma associé.
* Lors de l’envoi, les données saisies par l’utilisateur sont envoyées au format JSON en phase avec le schéma associé.

Un schéma JSON se compose de types d’éléments simples et complexes. Les éléments possèdent des attributs qui ajoutent des règles à ceux-ci. Lorsque ces éléments et attributs sont déplacés sur un formulaire adaptatif, ils sont automatiquement mappés au composant de formulaire adaptatif correspondant.

Ce mappage des éléments JSON avec les composants de formulaire adaptatif est le suivant :

```json
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
   <td><p>Propriétés de chaînes avec contrainte d’énumération et enumNames.</p> <p>Syntaxe,</p> <p> <code>{</code></p> <p><code>"type" : "string",</code></p> <p><code>"enum" : ["M", "F"]</code></p> <p><code>"enumNames" : ["Male", "Female"]</code></p> <p><code>}</code></p> <p> </p> </td>
   <td><p>Composant Liste déroulante :</p>
    <ul>
     <li>Les valeurs répertoriées dans enumNames s’affichent dans la zone de dépôt.</li>
     <li>Les valeurs répertoriées dans l’énumération sont utilisées pour le calcul.</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p>Propriété de chaîne avec contrainte de format. Par exemple, courrier électronique et date.</p> <p>Syntaxe,</p> <p><code>{</code></p> <p><code>"type" : "string",</code></p> <p><code>"format" : "email"</code></p> <p><code>}</code></p> <p> </p> </td>
   <td>
    <ul>
     <li>Le composant Email est mappé lorsque le type est chaîne et le format est email.</li>
     <li>Le composant de zone de texte avec validation est mappé lorsque le type est chaîne et le format est nom d’hôte.</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p><code>{</code></p> <p><code>"type" : "string",</code></p> <p><code>}</code></p> </td>
   <td><br /> <br /> Champ de texte<br /> <br /> <br /> </td>
  </tr>
  <tr>
   <td>propriété number<br /> </td>
   <td>Champ numérique dont le sous-type est défini pour flotter<br /> </td>
  </tr>
  <tr>
   <td>propriété integer<br /> </td>
   <td>Champ numérique dont le sous-type est défini sur entier<br /> </td>
  </tr>
  <tr>
   <td>propriété boolean<br /> </td>
   <td>Basculer<br /> </td>
  </tr>
  <tr>
   <td>propriété object<br /> </td>
   <td>Panneau<br /> </td>
  </tr>
  <tr>
   <td>Propriété du tableau</td>
   <td>Panneau répétable dont le minimum et le maximum sont respectivement égaux à minItems et maxItems. Seuls les tableaux homogènes sont pris en charge. Par conséquent, la contrainte d’éléments doit être un objet et n’est pas un tableau.<br /> </td>
  </tr>
 </tbody>
</table>

### Propriétés communes de schéma {#common-schema-properties}

Le formulaire adaptatif utilise les informations disponibles dans le schéma JSON pour mapper chaque champ généré. En particulier :

* La propriété `title` sert de libellé aux composants de formulaire adaptatif.
* La propriété `description` est définie comme description longue pour un composant de formulaire adaptatif.
* La propriété `default` sert de valeur initiale d’un champ de formulaire adaptatif.
* La propriété `maxLength` est définie en tant qu’attribut `maxlength` du composant champ de texte.
* Les propriétés `minimum`, `maximum`, `exclusiveMinimum` et `exclusiveMaximum` sont utilisées pour le composant zone numérique.
* Pour prendre en charge la plage de composants `DatePicker component`, les propriétés supplémentaires `minDate` et `maxDate` de schéma JSON sont fournis.
* Les propriétés `minItems` et `maxItems` servent à limiter le nombre d’éléments/champs qui peuvent être ajoutés ou retirés d’un composant de panneau.
* La propriété `readOnly` définit l’attribut `readonly` d’un composant de formulaire adaptatif.
* La propriété `required` marque le champ de formulaire adaptatif comme obligatoire alors qu’en cas de panneau (lorsque le type est objet), les données JSON finales soumises ont des champs avec une valeur vide correspondant à cet objet.
* La propriété `pattern` est définie comme modèle de validation (expression régulière) dans le formulaire adaptatif.
* L’extension du fichier de schéma JSON doit être conservée dans .schema.json. Par exemple, &lt;nom_fichier>.schema.json.

## Exemple de schéma JSON {#sample-json-schema}

Vous trouverez ci-dessous un exemple de schéma JSON.

```json
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

Les clés de définition sont utilisées pour identifier les schémas réutilisables. Les définitions de schéma réutilisables sont utilisées pour créer des fragments. Elle est similaire à l’identification des types complexes dans XSD.  Un exemple de schéma JSON dont la définition est fournie ci-dessous :

```json
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

L’exemple ci-dessus définit un enregistrement de client, où chaque client possède à la fois une adresse de livraison et une adresse de facturation. La structure des deux adresses est la même (les adresses ont une adresse de rue, une ville et un état), il est donc préférable de ne pas dupliquer les adresses. Cela facilite également l’ajout et la suppression de champs pour toute modification ultérieure.

## Préconfiguration des champs dans la définition du schéma JSON {#pre-configuring-fields-in-json-schema-definition}

Vous pouvez utiliser la propriété **aem:afProperties** pour préconfigurer le champ de schéma JSON pour mapper vers un composant de formulaire adaptatif personnalisé. Un exemple est répertorié ci-dessous :

```json
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

## Configuration de scripts ou d’expressions pour les objets de formulaire  {#configure-scripts-or-expressions-for-form-objects}

JavaScript est le langage d’expression des formulaires adaptatifs. Toutes les expressions sont des expressions JavaScript valides et utilisent des API de modèle de script de formulaires adaptatifs. Vous pouvez préconfigurer les objets de formulaire pour [évaluer une expression](adaptive-form-expressions.md) sur un événement de formulaire.

Utilisez la propriété aem:afproperties pour préconfigurer les expressions ou scripts de formulaires adaptatifs pour les composants de ces formulaires. Par exemple, lorsque l’événement initialize est déclenché, le code ci-dessous définit la valeur du champ téléphonique et imprime une valeur dans le journal :

```json
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

Vous devez être membre du [groupe forms-power-user](forms-groups-privileges-tasks.md) pour configurer des scripts ou des expressions pour l’objet de formulaire. Le tableau ci-dessous répertorie tous les événements de script pris en charge pour un composant de formulaire adaptatif.

<table>
 <tbody>
  <tr>
   <th><strong></strong>Composant \ Événement</th>
   <th>initialize <br /> </th>
   <td>Calculer</td>
   <td>Visibilité</td>
   <td>Valider</td>
   <td>Activé</td>
   <td>Validation de la valeur</td>
   <td>Cliquer </td>
   <td>Options</td>
  </tr>
  <tr>
   <td>Champ de texte</td>
   <td><img alt="Icône de coche Oui" src="assets/yes_tick.png" /></td>
   <td><img alt="Icône de coche Oui" src="assets/yes_tick.png" /></td>
   <td><img alt="Icône de coche Oui" src="assets/yes_tick.png" /></td>
   <td><img alt="Icône de coche Oui" src="assets/yes_tick.png" /></td>
   <td><img alt="Icône de coche Oui" src="assets/yes_tick.png" /></td>
   <td><img alt="Icône de coche Oui" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td>Champ numérique</td>
   <td><img alt="Icône de coche Oui" src="assets/yes_tick.png" /></td>
   <td><img alt="Icône de coche Oui" src="assets/yes_tick.png" /></td>
   <td><img alt="Icône de coche Oui" src="assets/yes_tick.png" /></td>
   <td><img alt="Icône de coche Oui" src="assets/yes_tick.png" /></td>
   <td><img alt="Icône de coche Oui" src="assets/yes_tick.png" /></td>
   <td><img alt="Icône de coche Oui" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td>Procédure pas à pas numérique</td>
   <td><img alt="Icône de coche Oui" src="assets/yes_tick.png" /></td>
   <td><img alt="Icône de coche Oui" src="assets/yes_tick.png" /></td>
   <td><img alt="Icône de coche Oui" src="assets/yes_tick.png" /></td>
   <td><img alt="Icône de coche Oui" src="assets/yes_tick.png" /></td>
   <td><img alt="Icône de coche Oui" src="assets/yes_tick.png" /></td>
   <td><img alt="Icône de coche Oui" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td>Bouton radio</td>
   <td><img alt="Icône de coche Oui" src="assets/yes_tick.png" /></td>
   <td><img alt="Icône de coche Oui" src="assets/yes_tick.png" /></td>
   <td><img alt="Icône de coche Oui" src="assets/yes_tick.png" /></td>
   <td><img alt="Icône de coche Oui" src="assets/yes_tick.png" /></td>
   <td><img alt="Icône de coche Oui" src="assets/yes_tick.png" /></td>
   <td><img alt="Icône de coche Oui" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td>Téléphone</td>
   <td><img alt="Icône de coche Oui" src="assets/yes_tick.png" /></td>
   <td><img alt="Icône de coche Oui" src="assets/yes_tick.png" /></td>
   <td><img alt="Icône de coche Oui" src="assets/yes_tick.png" /></td>
   <td><img alt="Icône de coche Oui" src="assets/yes_tick.png" /></td>
   <td><img alt="Icône de coche Oui" src="assets/yes_tick.png" /></td>
   <td><img alt="Icône de coche Oui" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td>Basculer</td>
   <td><img alt="Icône de coche Oui" src="assets/yes_tick.png" /></td>
   <td><img alt="Icône de coche Oui" src="assets/yes_tick.png" /></td>
   <td><img alt="Icône de coche Oui" src="assets/yes_tick.png" /></td>
   <td><img alt="Icône de coche Oui" src="assets/yes_tick.png" /></td>
   <td><img alt="Icône de coche Oui" src="assets/yes_tick.png" /></td>
   <td><img alt="Icône de coche Oui" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td>Bouton</td>
   <td><img alt="Icône de coche Oui" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td><img alt="Icône de coche Oui" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td><img alt="Icône de coche Oui" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td><img alt="Icône de coche Oui" src="assets/yes_tick.png" /></td>
   <td> </td>
  </tr>
  <tr>
   <td>Case à cocher</td>
   <td><img alt="Icône de coche Oui" src="assets/yes_tick.png" /></td>
   <td><img alt="Icône de coche Oui" src="assets/yes_tick.png" /></td>
   <td><img alt="Icône de coche Oui" src="assets/yes_tick.png" /></td>
   <td><img alt="Icône de coche Oui" src="assets/yes_tick.png" /></td>
   <td><img alt="Icône de coche Oui" src="assets/yes_tick.png" /></td>
   <td><img alt="Icône de coche Oui" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td><img alt="Icône de coche Oui" src="assets/yes_tick.png" /></td>
  </tr>
  <tr>
   <td>Liste déroulante</td>
   <td><img alt="Icône de coche Oui" src="assets/yes_tick.png" /></td>
   <td><img alt="Icône de coche Oui" src="assets/yes_tick.png" /></td>
   <td><img alt="Icône de coche Oui" src="assets/yes_tick.png" /></td>
   <td><img alt="Icône de coche Oui" src="assets/yes_tick.png" /></td>
   <td><img alt="Icône de coche Oui" src="assets/yes_tick.png" /></td>
   <td><img alt="Icône de coche Oui" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td><img alt="Icône de coche Oui" src="assets/yes_tick.png" /></td>
  </tr>
  <tr>
   <td>Choix d’image</td>
   <td><img alt="Icône de coche Oui" src="assets/yes_tick.png" /></td>
   <td><img alt="Icône de coche Oui" src="assets/yes_tick.png" /></td>
   <td><img alt="Icône de coche Oui" src="assets/yes_tick.png" /></td>
   <td><img alt="Icône de coche Oui" src="assets/yes_tick.png" /></td>
   <td><img alt="Icône de coche Oui" src="assets/yes_tick.png" /></td>
   <td><img alt="Icône de coche Oui" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td><img alt="Icône de coche Oui" src="assets/yes_tick.png" /></td>
  </tr>
  <tr>
   <td>Champ de saisie de date</td>
   <td><img alt="Icône de coche Oui" src="assets/yes_tick.png" /></td>
   <td><img alt="Icône de coche Oui" src="assets/yes_tick.png" /></td>
   <td><img alt="Icône de coche Oui" src="assets/yes_tick.png" /></td>
   <td><img alt="Icône de coche Oui" src="assets/yes_tick.png" /></td>
   <td><img alt="Icône de coche Oui" src="assets/yes_tick.png" /></td>
   <td><img alt="Icône de coche Oui" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td>Sélecteur de date</td>
   <td><img alt="Icône de coche Oui" src="assets/yes_tick.png" /></td>
   <td><img alt="Icône de coche Oui" src="assets/yes_tick.png" /></td>
   <td><img alt="Icône de coche Oui" src="assets/yes_tick.png" /></td>
   <td><img alt="Icône de coche Oui" src="assets/yes_tick.png" /></td>
   <td><img alt="Icône de coche Oui" src="assets/yes_tick.png" /></td>
   <td><img alt="Icône de coche Oui" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td>E-mail</td>
   <td><img alt="Icône de coche Oui" src="assets/yes_tick.png" /></td>
   <td><img alt="Icône de coche Oui" src="assets/yes_tick.png" /></td>
   <td><img alt="Icône de coche Oui" src="assets/yes_tick.png" /></td>
   <td><img alt="Icône de coche Oui" src="assets/yes_tick.png" /></td>
   <td><img alt="Icône de coche Oui" src="assets/yes_tick.png" /></td>
   <td><img alt="Icône de coche Oui" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td>Pièce jointe</td>
   <td><img alt="Icône de coche Oui" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td><img alt="Icône de coche Oui" src="assets/yes_tick.png" /></td>
   <td><img alt="Icône de coche Oui" src="assets/yes_tick.png" /></td>
   <td><img alt="Icône de coche Oui" src="assets/yes_tick.png" /></td>
   <td><img alt="Icône de coche Oui" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td>Image</td>
   <td><img alt="Icône de coche Oui" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td><img alt="Icône de coche Oui" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td> </td>
   <td> </td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td>Draw</td>
   <td><img alt="Icône de coche Oui" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td><img alt="Icône de coche Oui" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td> </td>
   <td> </td>
   <td> </td>
   <td> </td>
  </tr>
  <tr>
   <td>Panneau</td>
   <td><img alt="Icône de coche Oui" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td><img alt="Icône de coche Oui" src="assets/yes_tick.png" /></td>
   <td> </td>
   <td> </td>
   <td> </td>
   <td> </td>
   <td> </td>
  </tr>
 </tbody>
</table>

Certains exemples d’utilisation d’événements dans un JSON masquent un champ sur l’événement initialize et configurent la valeur d’un autre champ sur l’événement de validation de valeur. Pour plus d’informations sur la création d’expressions pour les événements de script, voir [Expressions de formulaire adaptatif](adaptive-form-expressions.md).

Voici l’exemple de code JSON pour les exemples mentionnés précédemment.

### Masquage d’un champ sur l’événement initialize {#hiding-a-field-on-initialize-event}

```json
"name": {
    "type": "string",
    "aem:afProperties": {
        "events" : {
            "Initialize" : "this.visible = false;"
        }
    }
}
```

#### Configuration de la valeur d’un autre champ sur l’événement de validation de valeur {#configure-value-of-another-field-on-value-commit-event}

```json
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

Vous pouvez ajouter les restrictions suivantes aux éléments de schéma JSON pour limiter les valeurs possibles pour un composant de formulaire adaptatif :

<table>
 <tbody>
  <tr>
   <td><p><strong> Propriété de schéma</strong></p> </td>
   <td><p><strong>Type de données</strong></p> </td>
   <td><p><strong>Description</strong></p> </td>
   <td><p><strong>Composant</strong></p> </td>
  </tr>
  <tr>
   <td><p><code>maximum</code></p> </td>
   <td><p>Chaîne</p> </td>
   <td><p>Spécifie la limite supérieure pour les valeurs numériques et les dates. Par défaut, la valeur maximale est incluse.</p> </td>
   <td>
    <ul>
     <li>Zone numérique</li>
     <li>Procédure pas à pas numérique<br /> </li>
     <li>Sélecteur de date</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p><code>minimum</code></p> </td>
   <td><p>Chaîne</p> </td>
   <td><p>Indique la limite inférieure pour les valeurs numériques et les dates. Par défaut, la valeur minimale est incluse.</p> </td>
   <td>
    <ul>
     <li>Zone numérique</li>
     <li>Procédure pas à pas numérique</li>
     <li>Sélecteur de date</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p><code>exclusiveMaximum</code></p> </td>
   <td><p>Booléen</p> </td>
   <td><p>Si la valeur est true, la valeur numérique ou la date spécifiée dans le composant du formulaire doit être inférieure à la valeur numérique ou la date spécifiée pour la propriété maximum.</p> <p>Si la valeur est false, la valeur numérique ou la date spécifiée dans le composant du formulaire doit être inférieure ou égale à la valeur numérique ou à la date spécifiée pour la propriété maximum.</p> </td>
   <td>
    <ul>
     <li>Zone numérique</li>
     <li>Procédure pas à pas numérique</li>
     <li>Sélecteur de date</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p><code>exclusiveMinimum</code></p> </td>
   <td><p>Booléen</p> </td>
   <td><p>Si la valeur est true, la valeur numérique ou la date spécifiée dans le composant du formulaire doit être supérieure à la valeur numérique ou à la date spécifiée pour la propriété minimum.</p> <p>Si la valeur est false, la valeur numérique ou la date spécifiée dans le composant du formulaire doit être supérieure ou égale à la valeur numérique ou à la date spécifiée pour la propriété minimale.</p> </td>
   <td>
    <ul>
     <li>Zone numérique</li>
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
   <td>Indique le nombre maximal de caractères autorisés dans un composant. La longueur maximale doit être égale ou supérieure à zéro.</td>
   <td>
    <ul>
     <li>Zone de texte</li>
    </ul> </td>
  </tr>
  <tr>
   <td><p><code>pattern</code></p> </td>
   <td><p>Chaîne</p> </td>
   <td><p>Indique la séquence des caractères. Un composant accepte les caractères si les caractères sont conformes au modèle spécifié.</p> <p>La propriété pattern correspond au modèle de validation du composant de formulaire adaptatif correspondant.</p> </td>
   <td>
    <ul>
     <li>Tous les composants de formulaires adaptatifs qui sont mappés vers un schéma XSD </li>
    </ul> </td>
  </tr>
  <tr>
   <td><code>maxItems</code></td>
   <td>Chaîne</td>
   <td>Indique le nombre maximum d’éléments dans un tableau. Le nombre maximal d’éléments doit être égal ou supérieur à zéro.</td>
   <td> </td>
  </tr>
  <tr>
   <td><code>minItems</code></td>
   <td>Chaîne</td>
   <td>Indique le nombre minimum d’éléments dans un tableau. Le nombre d’éléments minimum doit être égal ou supérieur à zéro.</td>
   <td> </td>
  </tr>
 </tbody>
</table>



## Activation des données conformes aux schémas {#enablig-schema-compliant-data}

Pour permettre à tous les Forms adaptatifs basés sur un schéma JSON de générer des données conformes au schéma lors de l’envoi du formulaire, procédez comme suit :

1. Accédez à la console web Experience Manager à l’adresse `https://server:host/system/console/configMgr`.
1. Localiser **[!UICONTROL Configuration de canal web de formulaire adaptatif et de communication interactive]**.
1. Sélectionnez cette option pour ouvrir la configuration en mode d’édition.
1. Sélectionnez la variable **[!UICONTROL Générer des données conformes aux schémas]** .
1. Enregistrez les paramètres.

![configuration du canal web de formulaire adaptatif et de communication interactive](/help/forms/using/assets/af-ic-web-channel-configuration.png)

## Éléments non pris en charge  {#non-supported-constructs}

Les formulaires adaptatifs ne prennent pas en charge les éléments suivants de schéma JSON :

* Type null
* Types d’unions, tels que les types appropriés, et
* OneOf, AnyOf, AllOf et NOT
* Seuls les tableaux homogènes sont pris en charge. Par conséquent, la contrainte d’éléments doit être un objet et non un tableau.

## Questions fréquemment posées {#frequently-asked-questions}

**Pourquoi est-ce que je ne parviens pas à faire glisser des éléments individuels d’un sous-formulaire (structure générée à partir de n’importe quel type complexe) pour les sous-formulaires répétables (les valeurs minOccurs ou maxOccurs sont supérieures à 1) ?**

Dans un sous-formulaire répétable, vous devez utiliser le sous-formulaire complet. Si vous souhaitez uniquement des champs sélectifs, utilisez la structure entière et supprimez les champs indésirables.

**Je dispose d’une longue structure complexe dans l’outil de recherche de contenu. Comment puis-je trouver un élément spécifique ?**

Vous disposez de deux options :

* Parcourez la structure de l’arborescence.
* Utilisez la zone Rechercher pour rechercher un élément.

**Quelle doit être l’extension d’un fichier de schéma JSON ?**

L’extension d’un fichier de schéma JSON doit être .schema.json, Par exemple, &lt;nom_fichier>.schema.json.
