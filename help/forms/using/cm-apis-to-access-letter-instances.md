---
title: Utiliser les API pour accéder aux instances de lettre
description: Découvrez les API et utilisez-les pour accéder par programmation aux instances de lettre dans l’environnement AEM Forms.
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: correspondence-management
feature: Correspondence Management
exl-id: 9d43d9d4-5487-416c-b641-e807227ac056
source-git-commit: 000c22028259eb05a61625d43526a2e8314a1d60
workflow-type: tm+mt
source-wordcount: '597'
ht-degree: 40%

---

# Utiliser les API pour accéder aux instances de lettre {#apis-to-access-letter-instances}

## Présentation {#overview}

À l’aide de l’interface utilisateur de création de correspondance de Correspondence Management, vous pouvez enregistrer les brouillons d’instances de lettre en cours et il existe des instances de lettre envoyées.

Correspondence Management vous fournit des API à l’aide desquelles vous pouvez créer l’interface de liste pour qu’elle fonctionne avec les instances de lettre envoyées ou les brouillons. Les API répertorient et ouvrent les brouillons et les instances de lettre envoyées d’un agent, de sorte que l’agent puisse continuer de travailler sur les brouillons ou les instances de lettre envoyées.

## Récupération des instances de lettre {#fetching-letter-instances}

Correspondence Management expose les API pour récupérer les instances de lettre par le biais du service LetterInstanceService.

| Méthode | Description |
|--- |--- |
| getAllLetterInstances | Récupère des instances de lettre en fonction du paramètre de requête d’entrée. Pour récupérer toutes les instances de lettre, transmettez le paramètre de requête comme nul. |
| getLetterInstance | Récupère l’instance de lettre spécifiée en fonction de l’ID d’instance de lettre. |
| letterInstanceExists | Vérifie si une instance de lettre existe selon le nom donné. |

>[!NOTE]
>
>LetterInstanceService est un service OSGI et son instance peut être récupérée à l’aide de @Reference dans la classe Java™ ou sling.getService(LetterInstanceService). ) dans JSP.

### Utilisation de getAllLetterInstances {#using-nbsp-getallletterinstances}

L’API suivante recherche les instances de lettre en fonction de l’objet de la requête (envoyée et brouillon). Si l’objet de requête est nul, il renvoie toutes les instances de lettre. Cette API renvoie une liste de [LetterInstanceVO](https://experienceleague.adobe.com/docs/experience-manager-release-information/aem-release-updates/previous-updates/aem-previous-versions.html?lang=fr) qui peuvent être utilisés pour extraire des informations supplémentaires sur l’instance de lettre.

**Syntaxe** : `List getAllLetterInstances(Query query) throws ICCException;`

<table>
 <tbody>
  <tr>
   <td><strong>Paramètre</strong></td>
   <td><strong>Description</strong></td>
  </tr>
  <tr>
   <td>query</td>
   <td>Le paramètre de requête est utilisé pour rechercher/filtrer l’instance de lettre. Ici, la requête ne prend en charge que les attributs/propriétés de niveau supérieur de l’objet. La requête se compose d’instructions et l’« attributeName » utilisé dans l’objet d’instruction doit être le nom de la propriété dans l’objet d’instance de lettre.<br /> </td>
  </tr>
 </tbody>
</table>

#### Exemple 1 : récupérer toutes les instances de lettre de type ENVOYÉ {#example-fetch-all-the-letter-instances-of-type-submitted}

Le code suivant renvoie la liste des instances de lettre envoyées. Pour afficher uniquement les brouillons, modifiez `LetterInstanceType.COMPLETE.name()` par `LetterInstanceType.DRAFT.name().`.

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

Le code suivant possède plusieurs instructions dans la même requête pour obtenir les résultats filtrés en fonction de différents critères tels que l’instance de lettre envoyée (attribut submittedby) par un utilisateur, le type de letterInstanceType étant BROUILLON.

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

Récupérez une instance de lettre identifiée par l’ID de l’instance de lettre en question. Il renvoie « null » si l’ID de l’instance ne correspond pas.

**Syntaxe :** `public LetterInstanceVO getLetterInstance(String letterInstanceId) throws ICCException;`

```java
@Reference
LetterInstanceService letterInstanceService;
String letterInstanceId = "/content/apps/cm/letterInstances/1001/sampleLetterInstance";
LetterInstanceVO letterInstance = letterInstanceService.getLetterInstance(letterInstanceId );
```

### Vérification de l’existence de LetterInstance {#verifying-if-letterinstance-exist}

Vérifiez si une instance de lettre existe selon le nom spécifié.

**Syntaxe** : `public Boolean letterInstanceExists(String letterInstanceName) throws ICCException;`

| **Paramètre** | **Description** |
|---|---|
| letterInstanceName | Nom de l’instance de lettre que vous souhaitez vérifier si elle existe. |

```java
@Reference
LetterInstanceService letterInstanceService;
String letterInstanceName = "sampleLetterInstance";
Boolean result = letterInstanceService.letterInstanceExists(letterInstanceName );
```

## Ouverture d’instances de lettre {#opening-letter-instances}

L’instance de lettre peut être du type Envoyé ou Brouillon. L’ouverture des deux types d’instances de lettre présente des comportements différents :

* S’il existe une instance de lettre envoyée, un PDF représentant l’instance de lettre est ouvert. L’instance de lettre envoyée conservée sur le serveur contient également les données XML et XDP traitées, qui peuvent être utilisées pour accomplir et personnaliser davantage un cas tel que la création d’un PDF/A.
* S’il existe une instance Brouillon de lettre, l’interface utilisateur de création de correspondance est rechargée à l’état précédent exact tel qu’il était lors de la création du brouillon.

### Ouverture d’une instance de lettre préliminaire  {#opening-draft-letter-instance-nbsp}

L’interface utilisateur CCR prend en charge le paramètre cmLetterInstanceId, qui peut être utilisé pour la lettre rechargée.

`https://[hostName]:[portNo]/[contextPath]//aem/forms/createcorrespondence.html?random=[randomNo]&cmLetterInstanceId=[letterInstanceId]`

>[!NOTE]
>
Il n’est pas nécessaire de préciser les valeurs cmLetterId ou cmLetterName/State/Version lorsque vous rechargez une correspondance, car les données envoyées contiennent déjà tous les détails sur la correspondance rechargée. RandomNo est utilisé pour éviter les problèmes de cache du navigateur. Vous pouvez utiliser un horodatage comme nombre aléatoire.

### Ouverture d’une instance de lettre envoyée {#opening-submitted-letter-instance}

Le PDF envoyé peut être ouvert directement à l’aide de l’ID d’instance de lettre :

`https://[hostName]:[portNo]/[contextPath]/[letterInstanceId]`
