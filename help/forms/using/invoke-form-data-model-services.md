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
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '513'
ht-degree: 37%

---


# API pour appeler le service de modèle de données de formulaire à partir de formulaires adaptatifs {#api-to-invoke-form-data-model-service-from-adaptive-forms}

## Présentation {#overview}

AEM Forms permet aux auteurs de formulaires de simplifier et améliorer le remplissage de formulaire en appelant les services configurés dans un modèle de données de formulaire depuis un champ de formulaire adaptatif. To invoke a data model service, you can either create a rule in the visual editor or specify a JavaScript using the `guidelib.dataIntegrationUtils.executeOperation` API in the code editor of the [rule editor](/help/forms/using/rule-editor.md).

Ce document aborde la manière d’écrire un script Javascript en utilisant l’API `guidelib.dataIntegrationUtils.executeOperation` pour appeler un service.

## Utilisation de l’API {#using-the-api}

L’API `guidelib.dataIntegrationUtils.executeOperation` appelle un service depuis un champ de formulaire adaptatif. La syntaxe API se présente comme suit :

```javascript
guidelib.dataIntegrationUtils.executeOperation(operationInfo, inputs, outputs)
```

The structure of the `guidelib.dataIntegrationUtils.executeOperation` API specifies details about the service operation. La syntaxe de la structure se présente comme suit.

```javascript
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
   <td><code>operationInfo</code></td>
   <td>Structure permettant de spécifier l’identifiant du modèle de données de formulaire, le titre de l’opération et le nom de l’opération</td>
  </tr>
  <tr>
   <td><code>formDataModelId</code></td>
   <td>Indique le chemin d’accès du référentiel au modèle de données de formulaire, y compris son nom.</td>
  </tr>
  <tr>
   <td><code>operationName</code></td>
   <td>Spécifie le nom de l'opération de service à exécuter.</td>
  </tr>
  <tr>
   <td><code>inputs</code></td>
   <td>Mappe un ou plusieurs objets de formulaire aux arguments d’entrée pour l’opération de service.</td>
  </tr>
  <tr>
   <td><code>Outputs</code></td>
   <td>Maps one or more form objects to output values from the service operation to populate form fields<br /> </td>
  </tr>
  <tr>
   <td><code>success</code></td>
   <td>Renvoie des valeurs basées sur les arguments d’entrée pour l’opération de service. Il s’agit d’un paramètre facultatif utilisé comme fonction de rappel.<br /> </td>
  </tr>
  <tr>
   <td><code>failure</code></td>
   <td>Affiche un message d’erreur si la fonction de rappel de succès n’affiche pas les valeurs de sortie en fonction des arguments d’entrée. Il s’agit d’un paramètre facultatif utilisé comme fonction de rappel.<br /> </td>
  </tr>
 </tbody>
</table>

## Exemple de script pour appeler un service {#sample-script-to-invoke-a-service}

The following sample script uses the `guidelib.dataIntegrationUtils.executeOperation` API to invoke the `getAccountById` service operation configured in the `employeeAccount` form data model.

The `getAccountById` operation takes the value in the `employeeID` form field as input for the `empId` argument and returns employee name, account number, and account balance for the corresponding employee. Les valeurs de sortie sont renseignées dans les champs de formulaire spécifiés. For example, the value in `name` argument is populated in the `fullName` form element and value for `accountNumber` argument in `account` form element.

```javascript
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

## Utilisation de l’API avec la fonction de rappel {#using-the-api-callback}

Vous pouvez également appeler le service de modèle de données de formulaire à l’aide de l’ `guidelib.dataIntegrationUtils.executeOperation` API avec une fonction de rappel. La syntaxe API se présente comme suit :

```javascript
guidelib.dataIntegrationUtils.executeOperation(operationInfo, inputs, outputs, callbackFunction)
```

La fonction de rappel peut avoir des fonctions `success` et `failure` de rappel.

### Exemple de script avec fonctions de rappel de succès et d’échec {#callback-function-success-failure}

The following sample script uses the `guidelib.dataIntegrationUtils.executeOperation` API to invoke the `GETOrder` service operation configured in the `employeeOrder` form data model.

L&#39; `GETOrder` opération prend la valeur du champ de `Order ID` formulaire comme entrée pour l&#39; `orderId` argument et renvoie la valeur de quantité de commande dans la fonction de `success` rappel.  Si la fonction de `success` rappel ne renvoie pas la quantité de commande, la fonction de `failure` rappel affiche le `Error occured` message.

>[!NOTE]
>
> Si vous utilisez la fonction de `success` rappel, les valeurs de sortie ne sont pas renseignées dans les champs de formulaire spécifiés.

```javascript
var operationInfo = {
    "formDataModelId": "/content/dam/formsanddocuments-fdm/employeeOrder",
    "operationTitle": "GETOrder",
    "operationName": "GETOrder"
};
var inputs = {
    "orderId" : Order ID
};
var outputs = {};
var success = function (wsdlOutput, textStatus, jqXHR) {
order_quantity.value = JSON.parse(wsdlOutput).quantity;
 };
var failure = function(){
alert('Error occured');
};
guidelib.dataIntegrationUtils.executeOperation(operationInfo, inputs, outputs, success, failure);
```
