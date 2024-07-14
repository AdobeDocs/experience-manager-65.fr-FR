---
title: API pour travailler avec des formulaires envoyés sur le portail de formulaires
description: AEM Forms fournit des API que vous pouvez utiliser pour interroger et prendre des mesures sur les données de formulaires soumises dans le portail Formulaires.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: publish, developer-reference
feature: Forms Portal
exl-id: a685889e-5d24-471c-926d-dbb096792bc8
solution: Experience Manager, Experience Manager Forms
role: User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: tm+mt
source-wordcount: '539'
ht-degree: 100%

---

# API pour travailler avec des formulaires envoyés sur le portail de formulaires {#apis-to-work-with-submitted-forms-on-forms-portal}

AEM Forms fournit des API que vous pouvez utiliser pour interroger les données de formulaire envoyées via un portail de formulaires. En outre, vous pouvez envoyer des commentaires ou mettre à jour les propriétés des formulaires envoyés à l’aide des API décrites dans ce document.

>[!NOTE]
>
>Les utilisateurs qui appelleront les API doivent être ajoutés au groupe de réviseurs comme décrit dans la section [Associer des réviseurs d’envoi à un formulaire](/help/forms/using/adding-reviewers-form.md).

## GET /content/forms/portal/submission.review.json?func=getFormsForSubmissionReview {#get-content-forms-portal-submission-review-json-func-getformsforsubmissionreview-br}

Renvoie une liste de tous les formulaires éligibles.

### Paramètres d’URL {#url-parameters}

Cette API ne nécessite pas de paramètres supplémentaires.

### Réponse {#response}

L’objet de réponse contient un tableau JSON qui inclut les noms de formulaires et leur chemin d’accès de référentiel. La structure de la réponse est la suivante :

```json
[
 {formName: "<form name>",
 formPath: "<path to the form>" },
 {.....},
 ......]
```

### Exemple {#example}

**URL de la demande**

```http
https://[host]:[port]/content/forms/portal/submission.review.json?func=getFormsForSubmissionReview
```

**Réponse**

```json
[{"formPath":"/content/dam/formsanddocuments/forms-review/form2","formName":"form2"},{"formPath":"/content/dam/formsanddocuments/forms-review/form1","formName":"form1"}]
```

## GET /content/forms/portal/submission.review.json?func=getAllSubmissions {#get-content-forms-portal-submission-review-json-func-getallsubmissions}

Renvoie les détails de tous les formulaires envoyés. Cependant, vous pouvez utiliser des paramètres d&#39;URL pour limiter les résultats.

### Paramètres d’URL {#url-parameters-1}

Spécifiez les paramètres suivants dans l’URL de requête :

<table>
 <tbody>
  <tr>
   <th>Paramètre</th>
   <th>Description</th>
  </tr>
  <tr>
   <td><code>formPath</code></td>
   <td>Spécifie le chemin d’accès du référentiel CRX où réside le formulaire. Si vous ne spécifiez pas le chemin d’accès du formulaire, il renvoie une réponse vide.<br /> </td>
  </tr>
  <tr>
   <td><code>offset</code><br /> (facultatif)</td>
   <td>Spécifie le point de départ dans l’index du jeu de résultats. La valeur par défaut est <strong>0</strong>.</td>
  </tr>
  <tr>
   <td><code>limit</code><br /> (facultatif)</td>
   <td>Limite le nombre de résultats. La valeur par défaut est <strong>30</strong>.</td>
  </tr>
  <tr>
   <td><code>orderby</code> <br /> (facultatif)</td>
   <td>Spécifie la propriété de tri des résultats. La valeur par défaut est <strong>jcr:lastModified</strong>, qui trie les résultats en fonction de l’heure de la dernière modification.</td>
  </tr>
  <tr>
   <td><code>sort</code> <br /> (facultatif)</td>
   <td>Spécifie l’ordre de tri des résultats. La valeur par défaut est <strong>desc</strong>, qui trie les résultats par ordre décroissant. Vous pouvez spécifier <code>asc</code> pour trier les résultats dans l’ordre croissant.</td>
  </tr>
  <tr>
   <td><code>cutPoints</code> <br /> (facultatif)</td>
   <td>Spécifie une liste de propriétés de formulaire séparées par des virgules du formulaire à inclure dans les résultats. Les propriétés par défaut sont les suivantes : <br /> <code>formName</code>, <code>formPath</code>, <code>submitID</code>, <code>formType</code>, <code>jcr:lastModified</code>, <code>owner</code></td>
  </tr>
  <tr>
   <td><code>search</code> <br /> (facultatif)</td>
   <td>Recherche la valeur spécifiée dans les propriétés du formulaire et renvoie les formulaires avec les valeurs correspondantes. La valeur par défaut est <strong>""</strong>.</td>
  </tr>
 </tbody>
</table>

### Réponse {#response-1}

L’objet de réponse contient un tableau JSON qui inclut les détails des formulaires spécifiés. La structure de la réponse est la suivante :

```json
{
 total: "<total number of submissions>",
 items: [{ formName: "<name of the form>", formPath: "<path to the form>", owner: "<owner of the form>"},
 ....]}
```

### Exemple {#example-1}

**URL de la demande**

```http
https://[host]:[port]/content/forms/portal/submission.review.json?func=getAllSubmissions&formPath=/content/dam/formsanddocuments/forms-review/form2
```

**Réponse**

```json
{"total":1,"items":[{"formName":"form2","formPath":"/content/dam/formsanddocuments/forms-review/form2","submitID":"1403037413508500","formType":"af","jcr:lastModified":"2015-11-05T17:52:32.243+05:30","owner":"admin"}]}
```

## POST /content/forms/portal/submission.review.json?func=addComment {#post-content-forms-portal-submission-review-json-func-addcomment-br}

Ajoute un commentaire à l’instance d’envoi spécifiée.

### Paramètres d’URL {#url-parameters-2}

Spécifiez les paramètres suivants dans l’URL de requête :

| Paramètre | Description |
|---|---|
| `submitID` | Définit l’ID des métadonnées associé à une instance d’envoi. |
| `Comment` | Spécifie le texte du commentaire à ajouter à l’instance d’envoi spécifiée. |

### Réponse {#response-2}

Renvoie un ID de commentaire en cas de réussite de la publication d’un commentaire.

### Exemple {#example-2}

**URL de la demande**

```http
https://[host:'port'/content/forms/portal/submission.review.json?func=addComment&submitID=1403037413508500&comment=API+test+comment
```

**Réponse**

```java
1403873422601300
```

## GET /content/forms/portal/submission.review.json?func=getComments {#get-content-forms-portal-submission-review-json-func-getcomments-nbsp}

Renvoie tous les commentaires publiés sur l’instance d’envoi spécifiée.

### Paramètres d’URL {#url-parameters-3}

Spécifiez le paramètre suivant dans l’URL de requête :

| Paramètre | Description |
|---|---|
| `submitID` | Spécifie l’ID des métadonnées d’une instance d’envoi. |

### Réponse {#response-3}

L’objet de réponse contient un tableau JSON qui inclut tous les commentaires associés à l’ID d’envoi spécifié. La structure de la réponse est la suivante :

```json
[{
 owner: "<name of the commenter>",
 comment: "<comment text>",
 time: "<time when the comment was posted>"},
 { }......]
```

### Exemple {#example-3}

**URL de la demande**

```http
https://[host]:'port'/content/forms/portal/submission.review.json?func=getComments&submitID=1403037413508500
```

**Réponse**

```java
[{"owner":"fr1","comment":"API test comment","time":1446726988250}]
```

## POST /content/forms/portal/submission.review.json?func=updateSubmission {#post-content-forms-portal-submission-review-json-func-updatesubmission-br}

Met à jour la valeur de la propriété spécifiée de l’instance de formulaire envoyée spécifiée.

### Paramètres d’URL {#url-parameters-4}

Spécifiez les paramètres suivants dans l’URL de requête :

| Paramètre | Description |
|---|---|
| `submitID` | Définit l’ID des métadonnées associé à une instance d’envoi. |
| `property` | Spécifie la propriété de formulaire à mettre à jour. |
| `value` | Spécifie la valeur de la propriété de formulaire à mettre à jour. |

### Réponse {#response-4}

Renvoie un objet JSON avec des informations sur la mise à jour publiée.

### Exemple {#example-4}

**URL de la demande**

```http
https://[host]:'port'/content/forms/portal/submission.review.json?func=updateSubmission&submitID=1403037413508500&value=sample_value&property=some_new_prop
```

**Réponse**

```json
{"formName":"form2","owner":"admin","jcr:lastModified":1446727516593,"path":"/content/forms/fp/admin/submit/metadata/1403037413508500.html","submitID":"1403037413508500","status":"submitted"}
```
