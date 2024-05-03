---
title: Afficher une liste des formulaires sur une page Web à l’aide d’API
description: Interrogez Forms Manager par programmation pour récupérer une liste de formulaires filtrée et l’afficher sur vos propres pages web.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: publish
exl-id: cfca6656-d2db-476d-a734-7a1d1e44894e
solution: Experience Manager, Experience Manager Forms
role: Admin, User, Developer
source-git-commit: f6771bd1338a4e27a48c3efd39efe18e57cb98f9
workflow-type: tm+mt
source-wordcount: '692'
ht-degree: 100%

---

# Afficher une liste des formulaires sur une page Web à l’aide d’API {#listing-forms-on-a-web-page-using-apis}

AEM Forms fournit une API de recherche basée sur REST que les développeurs Web peuvent utiliser pour interroger et récupérer un jeu de formulaires qui répond à leurs critères de recherche. Vous pouvez utiliser des API pour effectuer des recherches dans des formulaires en fonction de divers filtres. L’objet de réponse contient des attributs et propriétés de formulaire, ainsi que des points d’entrée de rendu.

Pour rechercher des formulaires à l’aide de l’API REST, envoyez une requête GET au serveur à l’adresse `https://'[server]:[port]'/libs/fd/fm/content/manage.json` avec les paramètres de requête décrits ci-dessous.

## Paramètres de requête {#query-parameters}

<table>
 <tbody>
  <tr>
   <td><strong>Nom d’attribut<br /> </strong></td>
   <td><strong>Description<br /> </strong></td>
  </tr>
  <tr>
   <td>func<br /> </td>
   <td><p>Spécifie la fonction à appeler. Pour effectuer une recherche dans les formulaires, définissez la valeur de l’attribut <code>func </code> sur <code>searchForms</code>.</p> <p>Par exemple, <code class="code">
       URLParameterBuilder entityBuilder=new URLParameterBuilder ();
       entityBuilder.add("func", "searchForms");</code></p> <p><strong>Remarque :</strong> <em>ce paramètre est obligatoire.</em><br /> </p> </td>
  </tr>
  <tr>
   <td>appPath<br /> </td>
   <td><p>Spécifie le chemin d’accès à l’application pour rechercher des formulaires. Par défaut, l’attribut appPath recherche toutes les applications disponibles au niveau du nœud racine.<br /> </p> <p>Vous pouvez spécifier plusieurs chemins d’application dans une seule requête. Plusieurs chemins distincts avec une barre verticale (|).  </p> </td>
  </tr>
  <tr>
   <td>cutPoints<br /> </td>
   <td><p>Indique les propriétés à récupérer avec les ressources. Vous pouvez utiliser l’astérisque (*) pour récupérer toutes les propriétés simultanément. Utilisez la barre verticale (|) pour indiquer plusieurs propriétés. </p> <p>Par exemple, <code>cutPoints=propertyName1|propertyName2|propertyName3</code></p> <p><strong>Remarque</strong> : </p>
    <ul>
     <li><em>Les propriétés telles que l’ID, le chemin et le nom sont toujours récupérées. </em></li>
     <li><em>Chaque ressource possède un ensemble de propriétés différent. Les propriétés telles que formUrl, pdfUrl et guideUrl ne dépendent pas de l’attribut cutPoints. Elles dépendent du type de ressource et sont récupérées en conséquence. </em></li>
    </ul> </td>
  </tr>
  <tr>
   <td>relation<br /> </td>
   <td>Indique les ressources connexes à récupérer avec les résultats de la recherche. Vous pouvez sélectionner l’une des options suivantes pour récupérer les ressources connexes :
    <ul>
     <li><strong>NO_RELATION</strong> : ne pas récupérer les ressources connexes.</li>
     <li><strong>IMMEDIATE</strong> : récupérer les ressources liées directement aux résultats de la recherche.</li>
     <li><strong>ALL</strong> : récupérer toutes les ressources liées (directement et indirectement).</li>
    </ul> </td>
  </tr>
  <tr>
   <td>maxSize</td>
   <td>Indique le nombre maximal de formulaires à récupérer.</td>
  </tr>
  <tr>
   <td>offset</td>
   <td>Indique le nombre de formulaires à ignorer depuis le début.</td>
  </tr>
  <tr>
   <td>returnCount</td>
   <td>Indique s’il faut renvoyer ou non les résultats de recherche correspondant aux critères spécifiés. </td>
  </tr>
  <tr>
   <td>statements</td>
   <td><p>Indique la liste d’instructions. Les requêtes sont des exécutions sur la liste des instructions spécifiées au format JSON. </p> <p>Par exemple,</p> <p><code class="code">JSONArray statementArray=new JSONArray();
       JSONObject statement=new JSONObject();
       statement.put("name", "title");
       statement.put("value", "SimpleSurveyAF");
       statement.put("operator", "EQ"); statementArray.put(statement);</code></p> <p>Dans l’exemple ci-dessus, </p>
    <ul>
     <li><strong>name</strong> : spécifie le nom de la propriété à rechercher.</li>
     <li><strong>value</strong> : spécifie la valeur de la propriété à rechercher.</li>
     <li><strong>operator</strong> : spécifie l’opérateur à appliquer lors de la recherche. Les opérateurs ci-dessous sont pris en charge :
      <ul>
       <li>EQ - Est égal à </li>
       <li>NEQ – Est différent de</li>
       <li>GT – Supérieur à</li>
       <li>LT – Inférieur à</li>
       <li>GTEQ – Supérieur ou égal à</li>
       <li>LTEQ – Inférieur ou égal à</li>
       <li>CONTAINS – A contient B si B fait partie de A</li>
       <li>FULLTEXT – Recherche de texte intégral</li>
       <li>STARTSWITH – A commence par B si B est la partie initiale de A</li>
       <li>ENDSWITH – A se termine par B si B est la fin de A</li>
       <li>LIKE – Implémente l’opérateur LIKE</li>
       <li>AND – Combine plusieurs instructions</li>
      </ul> <p><strong>Remarque :</strong> <em>les opérateurs GT, LT, GTEQ et LTEQ s’appliquent aux propriétés de type linéaire telles que LONG, DOUBLE et DATE.</em></p> </li>
    </ul> </td>
  </tr>
  <tr>
   <td>orderings<br /> </td>
   <td><p>Indique les critères d’ordre relatifs aux résultats de la recherche. Les critères sont définis au format JSON. Vous pouvez trier les résultats de la recherche sur plusieurs champs. Les résultats sont triés dans l’ordre selon l’apparition des champs dans la requête.</p> <p>Par exemple,</p> <p>Pour récupérer les résultats de la requête selon la propriété de titre dans l’ordre croissant, ajoutez le paramètre suivant : </p> <p><code class="code">JSONArray orderingsArray=new JSONArray();
       JSONObject orderings=new JSONObject();
       orderings.put("name", "title");
       orderings.put("criteria", "ASC");
       orderingsArray.put(orderings);
       entityBuilder.add("orderings", orderingsArray.toString());</code></p>
    <ul>
     <li><strong>Nom</strong> : spécifie le nom de la propriété à utiliser pour classer les résultats de la recherche.</li>
     <li><strong>Critères</strong> : spécifie l’ordre des résultats. L’attribut d’ordre accepte les valeurs suivantes :
      <ul>
       <li>ASC – Utilisez l’attribut ASC pour classer les résultats dans l’ordre croissant.<br /> </li>
       <li>DES - Utilisez l’attribut DES pour classer les résultats dans l’ordre décroissant.</li>
      </ul> </li>
    </ul> </td>
  </tr>
  <tr>
   <td>includeXdp</td>
   <td>Indique si le contenu binaire doit être récupéré ou non. L’attribut <code>includeXdp</code> s’applique aux ressources de type <code>FORM</code>, <code>PDFFORM</code> et <code>PRINTFORM</code>.</td>
  </tr>
  <tr>
   <td>assetType</td>
   <td>Indique les types de ressources à récupérer de toutes les ressources publiées. Utilisez la barre verticale (|) pour indiquer plusieurs types de ressources. Les types de ressources valides sont FORM, PDFFORM, PRINTFORM, RESOURCE et GUIDE.</td>
  </tr>
 </tbody>
</table>

## Exemple de requête {#sample-request}

```json
func : searchForms
appPath : /content/dam/formsanddocuments/MyApplication23
cutPoints : title|description|author|status|creationDate|lastModifiedDate|activationDate|expiryDate|tags|allowedRenderFormat|formmodel
relation : NO_RELATION
includeXdp : false
maxSize : 10
offset : 0
returnCount : true
statements: [{"name":"name","value":"*Claim.xdp","operator":"CONTAINS"},
                {"name":"","value":"Expense","operator":"FULLTEXT"},
                {"name":"description","value":"ABCD*","operator":"CONTAINS"},
                {"name":"status","value":"false","operator":"EQ"},
                {"name":"lastModifiedDate","value":"01/09/2013","operator":"GTEQ"},
                {"name":"lastModifiedDate","value":"01/18/2013","operator":"LTEQ"}]
orderings:[{"name" :"lastModifiedDate":"order":"ASC"}]
```

## Exemple de réponse {#sample-response}

```json
[
{"resultCount":2},
    {"assetType":"FORM","name":"ExpenseClaim.xdp","id":"509fa2d5-e3c9-407b-b8dc-fa0ba08eb0ce",
       "path":"/content/dam/formsanddocuments/MyApplication23/1.0/ExpenseClaim.xdp",
       "title":"Expense Report","description":"ABCDEFGIJK","author":"Frank Bowman",
       "tags":[],"formUrl":"/content/dam/formsanddocuments/MyApplication23/1.0/ExpenseClaim.xdp/jcr:content",
       "pdfUrl":"/content/dam/formsanddocuments/MyApplication23/1.0/ExpenseClaim.xdp/jcr:content?type=pdf",
       "references":[],"images":[{"assetType":"resource","name":"Image.gif","id":"5477a127-8bbf-4cec-8f81-2689e5cb4a15",
       "path":"/content/dam/formsanddocuments/MyApplication23/1.0/Image.gif","resourceSize":0}],
       "status":false,"creationDate":1358429845623,"lastModifiedDate":1358429846771},
{"assetType":"FORM","name":"ExpenseClaim.xdp","id":"4312239b-b666-4d36-95bc-641b3a39ddd4",
       "path":"/content/dam/formsanddocuments/MyApplication23/ExpenseClaim.xdp",
       "title":"Expense Report","description":"ABCDefghijklm","author":"Frank Bowman",
       "tags":[],"formUrl":"/content/dam/formsanddocuments/MyApplication23/ExpenseClaim.xdp/jcr:content",
       "pdfUrl":"/content/dam/formsanddocuments/MyApplication23/ExpenseClaim.xdp/jcr:content?type=pdf",
       "references":[],"images":[{"assetType":"resource","name":"Image.gif","id":"118a2e3f-7097-4d8c-85d1-651306de284a",
       "path":"/content/dam/formsanddocuments/MyApplication23/Image.gif","resourceSize":0}],"status":false,
       "creationDate":1358429856690,"lastModifiedDate":1358430109023}
]
```

## Articles connexes

* [Activer des composants du portail Formulaires](/help/forms/using/enabling-forms-portal-components.md)
* [Créer une page du portail Formulaires](/help/forms/using/creating-form-portal-page.md)
* [Affichage de la liste des formulaires sur une page Web à l’aide d’API](/help/forms/using/listing-forms-webpage-using-apis.md)
* [Utiliser le composant Brouillons et Envois](/help/forms/using/draft-submission-component.md)
* [Personnaliser le stockage des brouillons de formulaires et des formulaires envoyés](/help/forms/using/draft-submission-component.md)
* [Exemple d’intégration d’un composant brouillons &amp; envois à la base de données](/help/forms/using/integrate-draft-submission-database.md)
* [Personnalisation de modèles pour les composants Forms Portal](/help/forms/using/customizing-templates-forms-portal-components.md)
* [Présentation de la publication de formulaires sur un portail](/help/forms/using/introduction-publishing-forms.md)
