---
title: API pour appeler le service de modèle de données de formulaire à partir de formulaires adaptatifs
seo-title: API pour appeler le service de modèle de données de formulaire à partir de formulaires adaptatifs
description: Décrit l’API invokeWebServices que vous pouvez utiliser pour appeler les services Web écrits dans WSDL depuis un champ de formulaire adaptatif.
seo-description: Décrit l’API invokeWebServices que vous pouvez utiliser pour appeler les services Web écrits dans WSDL depuis un champ de formulaire adaptatif.
uuid: 40561086-e69d-4e6a-9543-1eb2f54cd836
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: develop
discoiquuid: aa3e50f1-8f5a-489d-a42e-a928e437ab79
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# API pour appeler le service de modèle de données de formulaire à partir de formulaires adaptatifs {#api-to-invoke-form-data-model-service-from-adaptive-forms}

## Présentation {#overview}

AEM Forms permet aux auteurs de formulaires de simplifier et améliorer le remplissage de formulaire en appelant les services configurés dans un modèle de données de formulaire depuis un champ de formulaire adaptatif. To invoke a data model service, you can either create a rule in the visual editor or specify a JavaScript using the `guidelib.dataIntegrationUtils.executeOperation` API in the code editor of the [rule editor](/help/forms/using/rule-editor.md).

Ce document aborde la manière d’écrire un script Javascript en utilisant l’API `guidelib.dataIntegrationUtils.executeOperation` pour appeler un service.

## Utilisation de l’API {#using-the-api}

L’API `guidelib.dataIntegrationUtils.executeOperation` appelle un service depuis un champ de formulaire adaptatif. La syntaxe API se présente comme suit :

```
guidelib.dataIntegrationUtils.executeOperation(operationInfo, inputs, outputs)
```

L’API requiert les paramètres suivants.

| Paramètre | Description |
|---|---|
| `operationInfo` | Structure permettant de spécifier l’identifiant du modèle de données de formulaire, le titre de l’opération et le nom de l’opération |
| `inputs` | Structure permettant de spécifier les objets de formulaire dont les valeurs sont saisies dans l’opération de service |
| `outputs` | Structure permettant de spécifier les objets de formulaire qui seront renseignés avec les valeurs renvoyées par l’opération de service |

The structure of the `guidelib.dataIntegrationUtils.executeOperation` API specifies details about the service operation. La syntaxe de la structure se présente comme suit.

```
var operationInfo = {
formDataModelId,
operationTitle,
operationName
};
var inputs = {
inputField1,
inputFieldN
};
var outputs = {
outputField1,
outputFieldN
}
```

La structure de l’API spécifie les détails suivants concernant l’opération de service.

<table>
 <tbody>
  <tr>
   <th>Paramètre</th>
   <th>Description</th>
  </tr>
  <tr>
   <td><code>forDataModelId</code></td>
   <td>Spécifiez le chemin d’accès au référentiel vers le modèle de données de formulaire, y compris son nom</td>
  </tr>
  <tr>
   <td><code>operationName</code></td>
   <td>Indiquez le nom de l’opération de service à exécuter</td>
  </tr>
  <tr>
   <td><code>input</code></td>
   <td>Mappez un ou plusieurs objets de formulaire aux arguments d’entrée pour l’opération de service</td>
  </tr>
  <tr>
   <td>Sortie</td>
   <td>Mappez un ou plusieurs objets de formulaire aux valeurs de sortie de l’opération de service afin de renseigner les champs de formulaire<br /> </td>
  </tr>
 </tbody>
</table>

## Exemple de script pour appeler un service {#sample-script-to-invoke-a-service}

The following sample script uses the `guidelib.dataIntegrationUtils.executeOperation` API to invoke the `getAccountById` service operation configured in the `employeeAccount` form data model.

The `getAccountById` operation takes the value in the `employeeID` form field as input for the `empId` argument and returns employee name, account number, and account balance for the corresponding employee. Les valeurs de sortie sont renseignées dans les champs de formulaire spécifiés. For example, the value in `name` argument is populated in the `fullName` form element and value for `accountNumber` argument in `account` form element.

```
var operationInfo = {
"formDataModelId": "/content/dam/formsanddocuments-fdm/employeeAccount",
"operationName": "getAccountDetails"
};
var inputs = {
"empid" : employeeID
};
var outputs = {
"name" : fullName,
"accountNumber" : account,
"balance" : balance
};
guidelib.dataIntegrationUtils.executeOperation(operationInfo, inputs, outputs);
```

