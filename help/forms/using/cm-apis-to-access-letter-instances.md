---
title: Utiliser les API pour accéder aux instances de lettre
seo-title: Utiliser les API pour accéder aux instances de lettre
description: Découvrez comment utiliser des API pour accéder aux instances de lettre.
seo-description: Découvrez comment utiliser des API pour accéder aux instances de lettre.
uuid: e7fb7798-f49d-458f-87f5-22df5f3e7d10
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: correspondence-management
discoiquuid: 9c27f976-972a-4250-b56d-b84a7d72f8c8
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb
workflow-type: tm+mt
source-wordcount: '592'
ht-degree: 62%

---


# Utiliser les API pour accéder aux instances de lettre {#apis-to-access-letter-instances}

## Présentation {#overview}

A l’aide de l’interface utilisateur de création de correspondance de Correspondence Management, vous pouvez enregistrer des brouillons d’instances de lettre en cours. Vous y trouverez également les instances de lettre envoyées.

Correspondence Management vous fournit des API grâce auxquelles vous pouvez créer l’interface d’énumération pour travailler sur des instances de lettre envoyées ou des brouillons. Les API liste et ouvrent les instances de lettre envoyée et de lettre brouillon d’un agent, de sorte que l’agent puisse continuer à travailler sur les instances de lettre brouillon ou envoyée.

## Récupérer des instances de lettre {#fetching-letter-instances}

Correspondence Management expose les API pour récupérer des instances de lettre par le biais du service LetterInstanceService.

| Méthode | Description |
|--- |--- |
| getAllLetterInstances | Récupère les instances de lettre en fonction du paramètre de requête d’entrée. Pour récupérer toutes les instances de lettre, transmettez le paramètre de requête comme nul. |
| getLetterInstance | Récupère l’instance de lettre spécifiée en fonction de l’ID de l’instance de lettre. |
| letterInstanceExists | Vérifie l’existence d’une instance de lettre selon le nom spécifié. |

>[!NOTE]
>
>LetterInstanceService est un service OSGI et son instance peut être récupérée à l’aide de @Reference dans Java
>Classe ou sling.getService(LetterInstanceService). Classe ) dans JSP.

### Utilisation de getAllLetterInstances {#using-nbsp-getallletterinstances}

L’API suivante recherche les instances de lettre en fonction de l’objet de la requête (envoyée et brouillon). Si l’objet requête est nul, il renvoie toutes les instances de lettre. Cette API renvoie la liste des objets [LetterInstanceVO](https://helpx.adobe.com/experience-manager/6-2/forms/javadocs/com/adobe/icc/dbforms/obj/LetterInstanceVO.html) qui peuvent être utilisés pour extraire des informations supplémentaires sur l’instance de lettre.

**Syntaxe** :  `List getAllLetterInstances(Query query) throws ICCException;`

<table>
 <tbody>
  <tr>
   <td><strong>Paramètre</strong></td>
   <td><strong>Description</strong></td>
  </tr>
  <tr>
   <td>query</td>
   <td>Le paramètre de requête est utilisé pour trouver/filtrer l’instance de lettre. Ici, la requête ne prend en charge que les attributs/propriétés de niveau supérieur de l’objet. La requête se compose d’instructions et l’« attributename » utilisé dans l’objet d’instruction doit être le nom de la propriété dans l’objet d’instance de lettre.<br /> </td>
  </tr>
 </tbody>
</table>

#### Exemple 1 : récupérer toutes les instances de lettre de type ENVOYEE {#example-fetch-all-the-letter-instances-of-type-submitted}

Le code suivant renvoie la liste des instances de lettre envoyées. Pour obtenir uniquement des brouillons, remplacez `LetterInstanceType.COMPLETE.name()` par `LetterInstanceType.DRAFT.name().`.

```java
@Reference
LetterInstanceService letterInstanceService;
Query query = new Query();

List<LetterInstanceVO> submittedLetterInstances = new ArrayList<LetterInstanceVO>();

Statement statementForInstanceType = new Statement();
statementForInstanceType.setAttributeName("letterInstanceType");
statementForInstanceType.setOperator(Operator.EQUALS);
statementForInstanceType.setAttributeValue(LetterInstanceType.COMPLETE.name());
query.addStatement(statementForInstanceType);
submittedLetterInstances = letterInstanceService.getAllLetterInstances(query);
```

#### Exemple 2 : récupérer toutes les instances de lettre envoyées par un utilisateur, le type d’instance de lettre étant BROUILLON {#example-nbsp-fetch-all-the-letter-instances-submitted-by-a-user-and-letter-instance-type-is-draft}

Le code suivant comporte plusieurs instructions dans la même requête pour que les résultats soient filtrés en fonction de différents critères tels que l’instance de lettre envoyée (attribut submittedby) par un utilisateur et le type de letterInstanceType est BROUILLON.

```java
@Reference
LetterInstanceService letterInstanceService;

String submittedBy = "tglodman";
Query query = new Query();

List<LetterInstanceVO> submittedLetterInstances = new ArrayList<LetterInstanceVO>();

Statement statementForInstanceType = new Statement();
statementForInstanceType.setAttributeName("letterInstanceType");
statementForInstanceType.setOperator(Operator.EQUALS);
statementForInstanceType.setAttributeValue(LetterInstanceType.COMPLETE.name());
query.addStatement(statementForInstanceType);

Statement statementForSubmittedBy = new Statement();
statementForSubmittedBy .setAttributeName("submittedby");
statementForSubmittedBy .setOperator(Operator.EQUALS);
statementForSubmittedBy .setAttributeValue(submittedBy);
query.addStatement(statementForSubmittedBy );
submittedLetterInstances = letterInstanceService.getAllLetterInstances(query);
```

### Utilisation de getLetterInstance {#using-nbsp-getletterinstance}

Récupérez une instance de lettre identifiée par l’ID de l’instance de lettre en question. Elle renvoie &quot;null si l’ID d’instance ne correspond pas.

**Syntaxe :** `public LetterInstanceVO getLetterInstance(String letterInstanceId) throws ICCException;`

```java
@Reference
LetterInstanceService letterInstanceService;
String letterInstanceId = "/content/apps/cm/letterInstances/1001/sampleLetterInstance";
LetterInstanceVO letterInstance = letterInstanceService.getLetterInstance(letterInstanceId );
```

### Vérification de l’existence de LetterInstance {#verifying-if-letterinstance-exist}

Vérifier si une instance de lettre existe selon le nom donné

**Syntaxe** :  `public Boolean letterInstanceExists(String letterInstanceName) throws ICCException;`

| **Paramètre** | **Description** |
|---|---|
| letterInstanceName | Il s’agit du nom de l’instance de lettre dont vous souhaitez vérifier l’existence. |

```java
@Reference
LetterInstanceService letterInstanceService;
String letterInstanceName = "sampleLetterInstance";
Boolean result = letterInstanceService.letterInstanceExists(letterInstanceName );
```

## Ouverture d’instances de lettre  {#opening-letter-instances}

L’instance de lettre peut être de type Envoyée ou Brouillon. L’ouverture des deux types d’instance de lettre présente deux cas de figure différents :

* Dans le cas d’une instance de lettre envoyée, un PDF représentant l’instance de lettre s’ouvre. L’instance de lettre envoyée conservée sur le serveur contient également les données XML et XDP traitées qui peuvent être utilisées à des fins d’exécution et de personnalisation selon les cas d’utilisation, comme la création d’un PDF/A.
* Dans le cas d’un brouillon d’instance de lettre, l’interface utilisateur de création de correspondance réapparaît exactement comme elle se présentait au moment où le brouillon a été créé

### Ouverture d’un brouillon d’instance de lettre  {#opening-draft-letter-instance-nbsp}

L’interface utilisateur CCR prend en charge le paramètre cmLetterInstanceId, qui peut être utilisé pour une lettre rechargée.

`https://[hostName]:[portNo]/[contextPath]//aem/forms/createcorrespondence.html?random=[randomNo]&cmLetterInstanceId=[letterInstanceId]`

>[!NOTE]
>
>Il n’est pas nécessaire de spécifier cmLetterId ou cmLetterName/State/Version lors du rechargement d’une correspondance, car les données envoyées contiennent déjà tous les détails sur la correspondance rechargée. RandomNo est utilisé pour éviter les problèmes de cache du navigateur. Vous pouvez utiliser l’horodatage comme nombre aléatoire.

### Ouverture d’une instance de lettre envoyée {#opening-submitted-letter-instance}

Le PDF envoyé peut être directement ouvert en utilisant l’ID de l’instance de lettre :

`https://[hostName]:[portNo]/[contextPath]/[letterInstanceId]`
