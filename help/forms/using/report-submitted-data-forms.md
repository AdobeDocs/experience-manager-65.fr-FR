---
title: API pour travailler avec des formulaires envoyés sur le portail de formulaires
seo-title: API pour travailler avec des formulaires envoyés sur le portail de formulaires
description: AEM Forms fournit des API que vous pouvez utiliser pour interroger et agir sur des données de formulaire envoyées sur le portail de formulaires.
seo-description: AEM Forms fournit des API que vous pouvez utiliser pour interroger et agir sur des données de formulaire envoyées sur le portail de formulaires.
uuid: c47c8392-e5a9-4c40-b65e-4a7f379a6b45
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: publish, developer-reference
discoiquuid: 9457effd-3595-452f-a976-ad9eda6dc909
translation-type: tm+mt
source-git-commit: 46f2ae565fe4a8cfea49572eb87a489cb5d9ebd7
workflow-type: tm+mt
source-wordcount: '570'
ht-degree: 99%

---


# API pour travailler avec des formulaires envoyés sur le portail de formulaires {#apis-to-work-with-submitted-forms-on-forms-portal}

AEM Forms fournit des API que vous pouvez utiliser pour interroger les données de formulaire envoyées via un portail de formulaires. En outre, vous pouvez envoyer des commentaires ou mettre à jour les propriétés des formulaires envoyés à l’aide des API décrites dans ce document.

>[!NOTE]
>
>Les utilisateurs qui appelleront les API doivent être ajoutés au groupe de réviseurs comme décrit dans la section [Associer des réviseurs d’envoi à un formulaire](/help/forms/using/adding-reviewers-form.md).

## GET /content/forms/portal/submission.review.json?func=getFormsForSubmissionReview {#get-content-forms-portal-submission-review-json-func-getformsforsubmissionreview-br}

Renvoie une liste de tous les formulaires éligibles.

### paramètres d’URL {#url-parameters}

Cette API ne nécessite pas de paramètres supplémentaires.

### Réponse {#response}

L’objet de réponse contient un tableau JSON qui inclut les noms de formulaires et leur chemin d’accès au référentiel. La structure de la réponse est comme suit :

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

Renvoie les détails de tous les formulaires envoyés. Cependant, vous pouvez utiliser les paramètres d’URL pour limiter les résultats.

### paramètres d’URL {#url-parameters-1}

Spécifiez les paramètres suivants dans l’URL de requête :

<table>
 <tbody>
  <tr>
   <th>Paramètre</th>
   <th>Description</th>
  </tr>
  <tr>
   <td><code>formPath</code></td>
   <td>Spécifie le chemin d’accès au référentiel CRX dans lequel se trouve le formulaire. Si vous ne spécifiez pas le chemin d’accès au formulaire, une réponse vide est envoyée.<br /> </td>
  </tr>
  <tr>
   <td><code>offset</code> (facultatif)</td>
   <td>Spécifie le point de départ dans l’index de l’ensemble de résultats. La valeur par défaut est <strong>0</strong>.</td>
  </tr>
  <tr>
   <td><code>limit</code> (facultatif)</td>
   <td>Limite le nombre de résultats. La valeur par défaut est <strong>30</strong>.</td>
  </tr>
  <tr>
   <td><code>orderby</code> <br /> (facultatif)</td>
   <td>Spécifie la propriété pour trier les résultats. La valeur par défaut est <strong>jcr:lastModified</strong>, elle trie les résultats selon l’heure de la dernière modification.</td>
  </tr>
  <tr>
   <td><code>sort</code> <br /> (facultatif)</td>
   <td>Spécifie l’ordre pour trier les résultats. La valeur par défaut est <strong>desc</strong>, elle trie les résultats dans l’ordre décroissant. Vous pouvez spécifier <code>asc</code> pour trier les résultats dans l’ordre croissant.</td>
  </tr>
  <tr>
   <td><code>cutPoints</code> <br /> (facultatif)</td>
   <td>Spécifie une liste de propriétés de formulaire séparées par des virgules du formulaire à inclure dans les résultats. Les propriétés par défaut sont : <br /> <code>formName</code>, <code>formPath</code>, <code>submitID</code>, <code>formType</code>, <code>jcr:lastModified</code>, <code>owner</code></td>
  </tr>
  <tr>
   <td><code>search</code> <br /> (facultatif)</td>
   <td>Recherche la valeur spécifiée dans les propriétés de formulaire, puis renvoie les formulaires avec les valeurs correspondantes. La valeur par défaut est <strong>""</strong>.</td>
  </tr>
 </tbody>
</table>

### Réponse {#response-1}

L’objet de réponse contient un tableau JSON qui comprend les informations des formulaires spécifiés. La structure de la réponse est comme suit :

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

### paramètres d’URL {#url-parameters-2}

Spécifiez les paramètres suivants dans l’URL de requête :

| Paramètre | Description |
|---|---|
| `submitID` | Définit l’ID des métadonnées associé à une instance d’envoi. |
| `Comment` | Spécifie le texte pour que le commentaire s’ajoute à l’instance d’envoi spécifiée. |

### Réponse {#response-2}

Renvoie un ID de commentaire sur la publication réussie d’un commentaire.

### Exemple {#example-2}

**URL de la demande**

```http
https://[host:'port'/content/forms/portal/submission.review.json?func=addComment&submitID=1403037413508500&comment=API+test+comment
```

**Réponse**

```java
1403873422601300
```

## GET /content/forms/portal/submission.review.json?func=getComments    {#get-content-forms-portal-submission-review-json-func-getcomments-nbsp}

Renvoie tous les commentaires publiés sur l’instance d’envoi spécifiée.

### paramètres d’URL {#url-parameters-3}

Spécifiez le paramètre suivant dans l’URL de requête :

| Paramètre | Description |
|---|---|
| `submitID` | Définit l’ID des métadonnées d’une instance d’envoi. |

### Réponse {#response-3}

L’objet de réponse contient un tableau JSON qui comprend tous les commentaires associés à l’ID d’envoi spécifié. La structure de la réponse est comme suit :

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

Met à jour la valeur de la propriété spécifiée de l’instance spécifiée de formulaire envoyé.

### paramètres d’URL {#url-parameters-4}

Spécifiez les paramètres suivants dans l’URL de requête :

| Paramètre | Description |
|---|---|
| `submitID` | Définit l’ID des métadonnées associé à une instance d’envoi. |
| `property` | Spécifie la propriété de formulaire à mettre à jour. |
| `value` | Indique la valeur de la propriété de formulaire à mettre à jour. |

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

