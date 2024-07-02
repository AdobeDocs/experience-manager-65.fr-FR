---
title: Préremplir des formulaires avec des dispositions fluides
description: Préremplissez des formulaires avec une disposition fluide pour montrer des données aux utilisateurs dans un formulaire rendu à l’aide de l’API Java et de l’API Web Service.
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
role: Developer
exl-id: ff087084-fb1c-43a4-ae54-cc77eb862493
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,Document Services,APIs & Integrations
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: ht
source-wordcount: '3478'
ht-degree: 100%

---

# Préremplir des formulaires avec des dispositions fluides {#prepopulating-forms-with-flowable-layouts1}

## Préremplir des formulaires avec des dispositions fluides {#prepopulating-forms-with-flowable-layouts2}

Le préremplissage de formulaires montre des données aux utilisateurs dans un formulaire rendu. Supposons, par exemple, qu’un utilisateur se connecte à un site web avec un nom d’utilisateur et un mot de passe. Si l’authentification est réussie, l’application cliente interroge une base de données pour obtenir des informations sur l’utilisateur. Les données sont fusionnées dans le formulaire, puis le formulaire est rendu à l’utilisateur. Par conséquent, l’utilisateur peut visualiser les données personnalisées contenues dans le formulaire.

Le préremplissage d’un formulaire présente les avantages suivants :

* Elle permet à l’utilisateur d’afficher des données personnalisées dans un formulaire.
* Il permet de réduire le volume de saisie de l’utilisateur lors du remplissage du formulaire.
* Elle assure l’intégrité des données grâce au contrôle du placement des données.

Les deux types de source de données suivants peuvent être utilisés pour insérer automatiquement des données dans un formulaire :

* Une source de données XDP, qui obéit au code XML conforme à la syntaxe XFA (ou des données XFDF pour préremplir un formulaire créé à l’aide d’Acrobat).
* Une source de données XML arbitraire qui contient des paires nom/valeur correspondant aux noms des champs du formulaire (les exemples de cette section utilisent une source de données XML arbitraire).

Un élément XML doit exister pour chaque champ de formulaire que vous souhaitez préremplir. Le nom de l’élément XML doit correspondre au nom du champ. Un élément XML est ignoré s’il ne correspond pas à un champ de formulaire ou si le nom de l’élément XML ne correspond pas au nom du champ. Il n’est pas nécessaire de correspondre à l’ordre dans lequel les éléments XML sont affichés, tant que tous les éléments XML sont spécifiés.

Lorsque vous préremplissez un formulaire qui contient déjà des données, vous devez spécifier les données déjà affichées dans la source de données XML. Supposons qu’un formulaire contenant 10 champs comporte des données dans quatre champs. Supposons ensuite que vous souhaitiez préremplir les six champs restants. Dans ce cas, vous devez spécifier 10 éléments XML dans la source de données XML utilisée pour préremplir le formulaire. Si vous ne spécifiez que six éléments, les quatre champs de départ resteront vides.

Vous pouvez, par exemple, préremplir un formulaire tel qu’un exemple de formulaire de confirmation. (voir « Formulaire de confirmation » dans [Générer des formulaires PDF interactifs](/help/forms/developing/rendering-interactive-pdf-forms.md)).

Pour préremplir l’exemple de formulaire de confirmation, vous devez créer une source de données XML qui contient trois éléments XML correspondant aux trois champs du formulaire. Ce formulaire contient les trois champs suivants : `FirstName`, `LastName`, et `Amount`. La première étape consiste à créer une source de données XML contenant des éléments XML correspondant aux champs inclus dans la conception du formulaire. L’étape suivante consiste à attribuer des valeurs de données aux éléments XML, comme illustré dans le code XML suivant.

```xml
     <Untitled>
         <FirstName>Jerry</FirstName>
         <LastName>Johnson</LastName>
         <Amount>250000</Amount>
     </Untitled>
```

Une fois que vous avez prérempli le formulaire de confirmation avec cette source de données XML, puis effectué le rendu du formulaire, les valeurs de données que vous avez attribuées aux éléments XML s’affichent, comme illustré dans le diagramme ci-dessous.

![pf_pf_confirmxml3](assets/pf_pf_confirmxml3.png)

### Préremplir des formulaires avec des dispositions fluides {#prepopulating_forms_with_flowable_layouts-1}

Les formulaires avec dispositions fluides servent à montrer une quantité indéterminée de données aux utilisateurs. Étant donné que la disposition du formulaire s’ajuste automatiquement à la quantité de données fusionnées, il n’est pas nécessaire de prédéfinir une disposition ou un nombre fixe de pages pour le formulaire, comme c’est le cas pour un formulaire avec une disposition fixe.

Un formulaire est généralement rempli avec des données obtenues lors de l’exécution. Par conséquent, vous pouvez préremplir un formulaire en créant une source de données XML en mémoire et en plaçant les données directement dans la source de données XML en mémoire.

Prenons l’exemple d’une application web, telle qu’une boutique en ligne. Une fois qu’un acheteur en ligne a terminé son achat, tous les articles achetés sont placés dans une source de données XML en mémoire qui est utilisée pour préremplir un formulaire. Le diagramme suivant illustre ce processus, qui est expliqué dans le tableau suivant le diagramme.

![pf_pf_finsrv_webapp_v1](assets/pf_pf_finsrv_webapp_v1.png)

Le tableau suivant décrit les étapes de ce diagramme.

<table>
 <thead>
  <tr>
   <th><p>Étape</p></th>
   <th><p>Description</p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>1</p></td>
   <td><p>Un utilisateur achète des articles dans une boutique en ligne. </p></td>
  </tr>
  <tr>
   <td><p>2</p></td>
   <td><p>Une fois que l’utilisateur a terminé ses achats et cliqué sur le bouton Envoyer, une source de données XML en mémoire est créée. Les articles achetés et les informations utilisateur sont placés dans la source de données XML en mémoire. </p></td>
  </tr>
  <tr>
   <td><p>3</p></td>
   <td><p>La source de données XML est utilisée pour préremplir un formulaire de bon de commande (un exemple de ce formulaire est illustré en dessous de ce tableau). </p></td>
  </tr>
  <tr>
   <td><p>4</p></td>
   <td><p>Le formulaire de bon de commande est rendu au navigateur web client. </p></td>
  </tr>
 </tbody>
</table>

Le diagramme suivant illustre un exemple de formulaire de bon de commande. Les informations du tableau peuvent s’adapter au nombre d’enregistrements dans les données XML.

![pf_pf_poform](assets/pf_pf_poform.png)

>[!NOTE]
>
>Un formulaire peut être prérempli avec des données provenant d’autres sources, telles qu’une base de données d’entreprise ou des applications externes.

### Considérations relatives à la conception d’un formulaire {#form-design-considerations}

Les formulaires avec des dispositions fluides sont basés sur des conceptions de formulaire créées dans Designer. Une conception de formulaire spécifie un ensemble de règles de disposition, de présentation et de capture de données, y compris le calcul de valeurs en fonction des entrées de l’utilisateur. Les règles sont appliquées lorsque des données sont entrées dans un formulaire. Les champs ajoutés à un formulaire sont des sous-formulaires qui se trouvent dans la conception de formulaire. Par exemple, dans le formulaire de bon de commande illustré dans le diagramme précédent, chaque ligne est un sous-formulaire. Pour plus d’informations sur la création d’une conception de formulaire contenant des sous-formulaires, voir [Création d’un formulaire de bon de commande avec une disposition fluide](https://www.adobe.com/go/learn_aemforms_qs_poformflowable_9_fr).

### Comprendre les sous-groupes de données {#understanding-data-subgroups}

Une source de données XML est utilisée pour préremplir des formulaires avec des dispositions fixes et des dispositions fluides. Cependant, la différence est qu’une source de données XML qui préremplit un formulaire avec une disposition fluide contient des éléments XML répétitifs, qui sont utilisés pour préremplir des sous-formulaires répétés dans le formulaire. Ces éléments XML qui se répètent sont appelés sous-groupes de données.

Une source de données XML utilisée pour préremplir le formulaire de bon de commande illustré dans le diagramme précédent contient quatre sous-groupes de données qui se répètent. Chaque sous-groupe de données correspond à un article acheté. Les articles achetés sont : un écran, une lampe de bureau, un téléphone et un carnet d’adresses.

La source de données XML suivante est utilisée pour préremplir le formulaire de bon de commande.

```xml
     <header>
         <!-- XML elements used to prepopulate non-repeating fields such as address
         <!and city
         <txtPONum>8745236985</txtPONum>
         <dtmDate>2004-02-08</dtmDate>
         <txtOrderedByCompanyName>Any Company Name</txtOrderedByCompanyName>
         <txtOrderedByAddress>555, Any Blvd.</txtOrderedByAddress>
         <txtOrderedByCity>Any City</txtOrderedByCity>
         <txtOrderedByStateProv>ST</txtOrderedByStateProv>
         <txtOrderedByZipCode>12345</txtOrderedByZipCode>
         <txtOrderedByCountry>Any Country</txtOrderedByCountry>
         <txtOrderedByPhone>(123) 456-7890</txtOrderedByPhone>
         <txtOrderedByFax>(123) 456-7899</txtOrderedByFax>
         <txtOrderedByContactName>Contact Name</txtOrderedByContactName>
         <txtDeliverToCompanyName>Any Company Name</txtDeliverToCompanyName>
         <txtDeliverToAddress>7895, Any Street</txtDeliverToAddress>
         <txtDeliverToCity>Any City</txtDeliverToCity>
         <txtDeliverToStateProv>ST</txtDeliverToStateProv>
         <txtDeliverToZipCode>12346</txtDeliverToZipCode>
         <txtDeliverToCountry>Any Country</txtDeliverToCountry>
         <txtDeliverToPhone>(123) 456-7891</txtDeliverToPhone>
         <txtDeliverToFax>(123) 456-7899</txtDeliverToFax>
         <txtDeliverToContactName>Contact Name</txtDeliverToContactName>
     </header>
     <detail>
         <!-- A data subgroup that contains information about the monitor>
         <txtPartNum>00010-100</txtPartNum>
         <txtDescription>Monitor</txtDescription>
         <numQty>1</numQty>
         <numUnitPrice>350.00</numUnitPrice>
     </detail>
     <detail>
         <!-- A data subgroup that contains information about the desk lamp>
         <txtPartNum>00010-200</txtPartNum>
         <txtDescription>Desk lamps</txtDescription>
         <numQty>3</numQty>
         <numUnitPrice>55.00</numUnitPrice>
     </detail>
     <detail>
         <!-- A data subgroup that contains information about the Phone>
             <txtPartNum>00025-275</txtPartNum>
             <txtDescription>Phone</txtDescription>
             <numQty>5</numQty>
             <numUnitPrice>85.00</numUnitPrice>
     </detail>
     <detail>
         <!-- A data subgroup that contains information about the address book>
         <txtPartNum>00300-896</txtPartNum>
         <txtDescription>Address book</txtDescription>
         <numQty>2</numQty>
         <numUnitPrice>15.00</numUnitPrice>
     </detail>
```

Notez que chaque sous-groupe de données contient quatre éléments XML qui correspondent aux informations suivantes :

* Numéro de pièce de l’article
* Description de l’article
* Quantité d’articles
* Prix unitaire

Le nom de l’élément XML parent d’un sous-groupe de données doit correspondre au nom du sous-formulaire situé dans la conception de formulaire. Par exemple, dans le diagramme précédent, notez que le nom de l’élément XML parent du sous-groupe de données est `detail`. Cela correspond au nom du sous-formulaire situé dans la conception de formulaire sur laquelle repose le formulaire de bon de commande. Si le nom de l’élément XML parent du sous-groupe de données et le sous-formulaire ne correspondent pas, aucun formulaire côté serveur ne sera prérempli.

Chaque sous-groupe de données doit contenir des éléments XML correspondant aux noms des champs du sous-formulaire. Le sous-formulaire `detail` situé dans la conception de formulaire contient les champs suivants :

* txtPartNum
* txtDescription
* numQty
* numUnitPrice

>[!NOTE]
>
>Si vous tentez de préremplir un formulaire avec une source de données contenant des éléments XML qui se répètent et définissez l’option `RenderAtClient` sur `No`, seul le premier enregistrement de données est fusionné dans le formulaire. Pour vous assurer que tous les enregistrements de données sont fusionnés dans le formulaire, définissez le `RenderAtClient` sur `Yes`. Pour plus d’informations sur l’option `RenderAtClient`, voir [Rendu de formulaire sur le client](/help/forms/developing/rendering-forms-client.md).

>[!NOTE]
>
>Pour plus d’informations sur le service Forms, voir [Références des services pour AEM Forms](https://help.adobe.com/fr_FR/livecycle/11.0/Services/index.html).

### Résumé des étapes {#summary-of-steps}

Pour préremplir un formulaire avec une disposition fluide, procédez comme suit :

1. Incluez les fichiers de projet.
1. Créez une source de données XML en mémoire.
1. Convertissez la source de données XML.
1. Générez un formulaire prérempli.

**Inclure des fichiers de projet**

Incluez les fichiers nécessaires dans votre projet de développement. Si vous créez une application cliente à l’aide de Java, incluez les fichiers JAR nécessaires. Si vous utilisez des services Web, veillez à inclure les fichiers proxy.

**Inclure des fichiers de projet**

Incluez les fichiers nécessaires dans votre projet de développement. Si vous créez une application cliente à l’aide de Java, incluez les fichiers JAR nécessaires. Si vous utilisez des services Web, veillez à inclure les fichiers proxy.

**Créer une source de données XML en mémoire**

Vous pouvez utiliser des classes `org.w3c.dom` pour créer une source de données XML en mémoire afin de préremplir un formulaire avec une disposition fluide. Placez les données dans une source de données XML conforme au formulaire. Pour plus d’informations sur la relation entre un formulaire avec une disposition souple et la source de données XML, consultez la section [Présentation des sous-groupes de données](#understanding-data-subgroups).

**Convertir la source de données XML**

Une source de données XML en mémoire créée à l’aide des classes `org.w3c.dom` peut être convertie en un objet `com.adobe.idp.Document` avant de pouvoir être utilisée pour préremplir un formulaire. Une source de données XML en mémoire peut être convertie à l’aide de classes de transformation XML Java.

>[!NOTE]
>
>Si vous utilisez le fichier WSDL du service Forms pour préremplir un formulaire, vous devez convertir un objet `org.w3c.dom.Document` en un objet `BLOB`.

**Restituer un formulaire prérempli**

Vous pouvez restituer un formulaire prérempli de la même manière que pour tout autre formulaire. La seule différence est que vous utilisez lʼobjet `com.adobe.idp.Document` qui contient la source de données XML pour préremplir le formulaire.

**Voir également**

[Inclusion des fichiers de bibliothèque Java d’AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Démarrages rapides de l’API Forms Service](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

[Effectuer le rendu de formulaires PDF interactifs](/help/forms/developing/rendering-interactive-pdf-forms.md)

[Créer des applications web qui génèrent des formulaires](/help/forms/developing/creating-web-applications-renders-forms.md)

### Préremplir des formulaires à l’aide de l’API Java {#prepopulating-forms-using-the-java-api}

Pour préremplir un formulaire avec une disposition souple à l’aide de l’API Forms (Java), procédez comme suit :

1. Inclure les fichiers du projet

   Incluez les fichiers clients JAR, tels qu’adobe-forms-client.jar, dans votre chemin de classe de projet Java. Pour plus d’informations sur l’emplacement de ces fichiers, voir [Inclusion des fichiers de bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

1. Créer une source de données XML en mémoire

   * Créez un objet `DocumentBuilderFactory` Java en appelant la méthode `newInstance` de la classe `DocumentBuilderFactory`.
   * Créez un objet `DocumentBuilder` Java en appelant la méthode `newDocumentBuilder` de l’objet `DocumentBuilderFactory`.
   * Appelez la méthode `newDocument` de l’objet `DocumentBuilder` pour instancier un objet `org.w3c.dom.Document`.
   * Créez l’élément racine de la source de données XML en appelant la méthode `createElement` de l’objet `org.w3c.dom.Document`. Cela crée un objet `Element` qui représente l’élément racine. Transmettez une valeur de chaîne représentant le nom de l’élément à la méthode `createElement`. Convertissez la valeur de retour en `Element`. Ensuite, ajoutez l’élément racine au document en appelant la méthode `appendChild` de l’objet `Document` et transmettez l’objet de l’élément racine en tant qu’argument. Les lignes de code suivantes illustrent cette logique dʼapplication :

     ` Element root = (Element)document.createElement("transaction");  document.appendChild(root);`

   * Créez l’élément d’en-tête de la source de données XML en appelant la méthode `createElement` de l’objet `Document`. Transmettez une valeur de chaîne représentant le nom de l’élément à la méthode `createElement`. Convertissez la valeur de retour en `Element`. Enfin, ajoutez l’élément d’en-tête à l’élément racine en appelant la méthode `appendChild` de l’objet `root` et transmettez l’objet d’élément d’en-tête en tant qu’argument. Les éléments XML qui sont ajoutés à l’élément dʼen-tête correspondent à la partie statique du formulaire. Les lignes de code suivantes illustrent cette logique dʼapplication :

     ` Element header = (Element)document.createElement("header");  root.appendChild(header);`

   * Créez un élément enfant qui appartient à l’élément d’en-tête en appelant la méthode `createElement` de lʼobjet `Document` et transmettez une valeur de chaîne qui représente le nom de l’élément. Convertissez la valeur de retour en `Element`. Définissez ensuite une valeur pour l’élément enfant en appelant sa méthode `appendChild` et transmettez la méthode `createTextNode` de lʼobjet `Document` comme argument. Définissez une valeur de chaîne qui apparaîtra comme la valeur de lʼélément enfant. Enfin, ajoutez lʼélément enfant à lʼélément dʼen-tête en appelant la méthode `appendChild` de lʼélément dʼen-tête et en transmettant lʼobjet d’élément enfant sous forme dʼargument. Les lignes de code suivantes illustrent cette logique dʼapplication :

     ` Element poNum= (Element)document.createElement("txtPONum");  poNum.appendChild(document.createTextNode("8745236985"));  header.appendChild(LastName);`


   * Ajoutez tous les éléments restants à l’élément d’en-tête en répétant la dernière sous-étape pour chaque champ apparaissant dans la partie statique du formulaire (dans le diagramme de source de données XML, ces champs figurent dans la section A (Consultez la section [Présentation des sous-groupes de données](#understanding-data-subgroups)).
   * Créez l’élément de détail de la source de données XML en appelant la méthode `createElement` de lʼobjet `Document`. Transmettez une valeur de chaîne représentant le nom de l’élément à la méthode `createElement`. Convertissez la valeur de retour en `Element`. Ajoutez ensuite l’élément de détail à l’élément racine en appelant la méthode `appendChild` de lʼobjet `root` et transmettez l’objet d’élément de détail comme argument. Les éléments XML ajoutés à l’élément de détail correspondent à la partie dynamique du formulaire. Les lignes de code suivantes illustrent cette logique dʼapplication :

     ` Element detail = (Element)document.createElement("detail");  root.appendChild(detail);`

   * Créez un élément enfant qui appartient à l’élément de détail en appelant la méthode `createElement` de lʼobjet `Document` et transmettez une valeur de chaîne qui représente le nom de l’élément. Convertissez la valeur de retour en `Element`. Définissez ensuite une valeur pour l’élément enfant en appelant sa méthode `appendChild` et transmettez la méthode `createTextNode` de lʼobjet `Document` comme argument. Définissez une valeur de chaîne qui apparaîtra comme la valeur de lʼélément enfant. Pour terminer, ajoutez lʼélément enfant à lʼélément de détail en appelant la méthode `appendChild` de lʼélément de détail et transmettez lʼobjet de lʼélément enfant sous forme dʼargument. Les lignes de code suivantes illustrent cette logique dʼapplication :

     ` Element txtPartNum = (Element)document.createElement("txtPartNum");  txtPartNum.appendChild(document.createTextNode("00010-100"));  detail.appendChild(txtPartNum);`

   * Répétez la dernière sous-étape pour tous les éléments XML à ajouter à lʼélément de détail. Pour créer correctement la source de données XML utilisée pour remplir le formulaire de bon de commande, vous devez ajouter les éléments XML suivants à l’élément de détail : `txtDescription`, `numQty` et `numUnitPrice`.
   * Répétez les deux dernières sous-étapes pour tous les éléments de données utilisés pour préremplir le formulaire.

1. Convertir la source de données XML

   * Créez un objet `javax.xml.transform.Transformer` en appelant la méthode statique `newInstance` de lʼobjet `javax.xml.transform.Transformer`.
   * Créez un objet `Transformer` en appelant la méthode `newTransformer` de l’objet `TransformerFactory`.
   * Créez un objet `ByteArrayOutputStream` en utilisant son constructeur.
   * Créez un objet `javax.xml.transform.dom.DOMSource` en utilisant son constructeur et en transmettant l’objet `org.w3c.dom.Document` qui a été créé à l’étape 1.
   * Créez un objet `javax.xml.transform.dom.DOMSource` en utilisant son constructeur et en transmettant l’objet `ByteArrayOutputStream`. 
   * Renseignez l’objet `ByteArrayOutputStream` Java en appelant la méthode `transform` de l’objet `javax.xml.transform.Transformer` et en transmettant les objets `javax.xml.transform.dom.DOMSource` et `javax.xml.transform.stream.StreamResult`.
   * Créez un tableau d’octets et affectez la taille de l’objet `ByteArrayOutputStream` au tableau d’octets.
   * Renseignez le tableau dʼoctets en appelant la méthode `toByteArray` de lʼobjet `ByteArrayOutputStream`.
   * Créez un objet `com.adobe.idp.Document` en utilisant son constructeur et en transmettant le tableau d’octets.

1. Effectuer le rendu d’un formulaire prérempli

   Appelez la méthode `renderPDFForm` de l’objet `FormsServiceClient` et transmettez les valeurs suivantes :

   * Une valeur de chaîne qui spécifie le nom de la conception de formulaire, y compris l’extension du nom de fichier.
   * Un objet `com.adobe.idp.Document` contenant les données à fusionner avec le formulaire. Veillez à utiliser l’objet `com.adobe.idp.Document` créé aux étapes 1 et 2.
   * Un objet `PDFFormRenderSpec` qui stocke les options d’exécution.
   * Un objet `URLSpec` contenant des valeurs URI requises par le service Forms.
   * Un objet `java.util.HashMap` qui stocke les pièces jointes. Ce paramètre est facultatif et vous pouvez spécifier `null` si vous ne souhaitez pas joindre de fichiers au formulaire.

   La méthode `renderPDFForm` renvoie un objet `FormsResult` contenant un flux de données de formulaire qui doit être écrit dans le navigateur web client.

   * Créez un objet `javax.servlet.ServletOutputStream` utilisé pour envoyer un flux de données de formulaire au navigateur web client.
   * Créez un objet `com.adobe.idp.Document` en appelant la méthode `getOutputContent` de l’objet `FormsResult`.
   * Créez un objet `java.io.InputStream` en appelant la méthode `getInputStream` de l’objet `com.adobe.idp.Document`.
   * Créez un tableau d’octets et remplissez-le avec le flux de données du formulaire en appelant la méthode `read` de l’objet `InputStream` et en transmettant le tableau d’octets comme argument.
   * Appelez la méthode `write` de l’objet `javax.servlet.ServletOutputStream` pour envoyer le flux de données du formulaire au navigateur web du client. Transmettez le tableau d’octets à la méthode `write`.

**Voir également**

[Démarrage rapide (mode SOAP) : préremplir des formulaires avec des dispositions fluides à l’aide de l’API Java](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-prepopulating-forms-with-flowable-layouts-using-the-java-api)

[Inclusion des fichiers de bibliothèque Java d’AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Préremplir des formulaires à l’aide de l’API de service web {#prepopulating-forms-using-the-web-service-api}

Pour préremplir un formulaire avec une disposition fluide à l’aide de l’API Forms (service web), procédez comme suit :

1. Inclure les fichiers du projet

   * Créez des classes proxy Java qui utilisent le WSDL du service Forms. (Voir [Créer des classes proxy Java à l’aide d’Apache Axis](/help/forms/developing/invoking-aem-forms-using-web.md#creating-java-proxy-classes-using-apache-axis).)
   * Incluez les classes proxy Java dans le chemin d’accès de classe.

1. Créer une source de données XML en mémoire

   * Créez un objet `DocumentBuilderFactory` Java en appelant la méthode `newInstance` de la classe `DocumentBuilderFactory`.
   * Créez un objet `DocumentBuilder` Java en appelant la méthode `newDocumentBuilder` de l’objet `DocumentBuilderFactory`.
   * Appelez la méthode `newDocument` de l’objet `DocumentBuilder` pour instancier un objet `org.w3c.dom.Document`.
   * Créez l’élément racine de la source de données XML en appelant la méthode `createElement` de l’objet `org.w3c.dom.Document`. Cela crée un objet `Element` qui représente l’élément racine. Transmettez une valeur de chaîne représentant le nom de l’élément à la méthode `createElement`. Convertissez la valeur de retour en `Element`. Ensuite, ajoutez l’élément racine au document en appelant la méthode `appendChild` de l’objet `Document` et transmettez l’objet de l’élément racine en tant qu’argument. Les lignes de code suivantes illustrent cette logique dʼapplication :

     ` Element root = (Element)document.createElement("transaction");  document.appendChild(root);`

   * Créez l’élément d’en-tête de la source de données XML en appelant la méthode `createElement` de l’objet `Document`. Transmettez une valeur de chaîne représentant le nom de l’élément à la méthode `createElement`. Convertissez la valeur de retour en `Element`. Enfin, ajoutez l’élément d’en-tête à l’élément racine en appelant la méthode `appendChild` de l’objet `root` et transmettez l’objet d’élément d’en-tête en tant qu’argument. Les éléments XML qui sont ajoutés à l’élément dʼen-tête correspondent à la partie statique du formulaire. Les lignes de code suivantes illustrent cette logique dʼapplication :

     ` Element header = (Element)document.createElement("header");  root.appendChild(header);`

   * Créez un élément enfant qui appartient à l’élément d’en-tête en appelant la méthode `createElement` de lʼobjet `Document` et transmettez une valeur de chaîne qui représente le nom de l’élément. Convertissez la valeur de retour en `Element`. Définissez ensuite une valeur pour l’élément enfant en appelant sa méthode `appendChild` et transmettez la méthode `createTextNode` de lʼobjet `Document` comme argument. Définissez une valeur de chaîne qui apparaîtra comme la valeur de lʼélément enfant. Enfin, ajoutez lʼélément enfant à lʼélément dʼen-tête en appelant la méthode `appendChild` de lʼélément dʼen-tête et en transmettant lʼobjet élément enfant sous forme dʼargument. Les lignes de code suivantes illustrent cette logique dʼapplication :

     ` Element poNum= (Element)document.createElement("txtPONum");  poNum.appendChild(document.createTextNode("8745236985"));  header.appendChild(LastName);`

   * Ajoutez tous les autres éléments à lʼélément dʼen-tête en répétant la dernière sous-étape pour chaque champ apparaissant dans la partie statique du formulaire (dans le diagramme de la source de données XML, ces champs figurent dans la section A. Consultez la section [Comprendre les sous-groupes de données](#understanding-data-subgroups)).
   * Créez l’élément de détail de la source de données XML en appelant la méthode `createElement` de lʼobjet `Document`. Transmettez une valeur de chaîne représentant le nom de l’élément à la méthode `createElement`. Convertissez la valeur de retour en `Element`. Ajoutez ensuite l’élément de détail à l’élément racine en appelant la méthode `appendChild` de lʼobjet `root` et transmettez l’objet d’élément de détail comme argument. Les éléments XML ajoutés à l’élément de détail correspondent à la partie dynamique du formulaire. Les lignes de code suivantes illustrent cette logique dʼapplication :

     ` Element detail = (Element)document.createElement("detail");  root.appendChild(detail);`

   * Créez un élément enfant appartenant à lʼélément de détail en appelant la méthode `createElement` de lʼobjet `Document` et transmettez une valeur de chaîne qui représente le nom de lʼélément. Convertissez la valeur de retour en `Element`. Définissez ensuite une valeur pour l’élément enfant en appelant sa méthode `appendChild` et transmettez la méthode `createTextNode` de lʼobjet `Document` comme argument. Définissez une valeur de chaîne qui apparaîtra comme la valeur de lʼélément enfant. Pour terminer, ajoutez lʼélément enfant à lʼélément de détail en appelant la méthode `appendChild` de lʼélément de détail et transmettez lʼobjet de lʼélément enfant sous forme dʼargument. Les lignes de code suivantes illustrent cette logique dʼapplication :

     ` Element txtPartNum = (Element)document.createElement("txtPartNum");  txtPartNum.appendChild(document.createTextNode("00010-100"));  detail.appendChild(txtPartNum);`

   * Répétez la dernière sous-étape pour tous les éléments XML à ajouter à lʼélément de détail. Pour créer correctement la source de données XML utilisée pour remplir le formulaire de bon de commande, vous devez ajouter les éléments XML suivants à l’élément de détail : `txtDescription`, `numQty` et `numUnitPrice`.
   * Répétez les deux dernières sous-étapes pour tous les éléments de données utilisés pour préremplir le formulaire.

1. Convertir la source de données XML

   * Créez un objet `javax.xml.transform.Transformer` en appelant la méthode statique `newInstance` de lʼobjet `javax.xml.transform.Transformer`.
   * Créez un objet `Transformer` en appelant la méthode `newTransformer` de l’objet `TransformerFactory`.
   * Créez un objet `ByteArrayOutputStream` en utilisant son constructeur.
   * Créez un objet `javax.xml.transform.dom.DOMSource` en utilisant son constructeur et en transmettant l’objet `org.w3c.dom.Document` qui a été créé à l’étape 1.
   * Créez un objet `javax.xml.transform.dom.DOMSource` en utilisant son constructeur et en transmettant l’objet `ByteArrayOutputStream`. 
   * Renseignez l’objet `ByteArrayOutputStream` Java en appelant la méthode `transform` de l’objet `javax.xml.transform.Transformer` et en transmettant les objets `javax.xml.transform.dom.DOMSource` et `javax.xml.transform.stream.StreamResult`.
   * Créez un tableau d’octets et affectez la taille de l’objet `ByteArrayOutputStream` au tableau d’octets.
   * Renseignez le tableau dʼoctets en appelant la méthode `toByteArray` de lʼobjet `ByteArrayOutputStream`.
   * Créez un objet `BLOB` en utilisant son constructeur, appelez sa méthode `setBinaryData`, puis transmettez le tableau dʼoctets.

1. Effectuer le rendu d’un formulaire prérempli

   Appelez la méthode `renderPDFForm` de l’objet `FormsService` et transmettez les valeurs suivantes :

   * Une valeur de chaîne qui spécifie le nom de la conception de formulaire, y compris l’extension du nom de fichier.
   * Un objet `BLOB` qui contient des données à fusionner avec le formulaire. Veillez à utiliser lʼobjet `BLOB` créé aux étapes 1 et 2.
   * Un objet `PDFFormRenderSpecc` qui stocke les options dʼexécution. Pour plus dʼinformations, consultez la section [Référence de lʼAPI AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).
   * Un objet `URLSpec` qui contient des valeurs URI qui sont requises par le service Forms.
   * Un objet `java.util.HashMap` qui stocke les pièces jointes. Il sʼagit dʼun paramètre facultatif. Vous pouvez indiquer `null` si vous ne souhaitez pas joindre de fichier au formulaire.
   * Un objet `com.adobe.idp.services.holders.BLOBHolder` vide qui est renseigné par la méthode. Il permet de stocker le formulaire PDF rendu.
   * Un objet `javax.xml.rpc.holders.LongHolder` vide qui est renseigné par la méthode. (Cet argument permet de stocker le nombre de pages du formulaire).
   * Un objet `javax.xml.rpc.holders.StringHolder` vide qui est renseigné par la méthode. (Cet argument permet de stocker la valeur du paramètre régional).
   * Un objet `com.adobe.idp.services.holders.FormsResultHolder` vide qui contiendra les résultats de cette opération.

   La méthode `renderPDFForm` renseigne l’objet `com.adobe.idp.services.holders.FormsResultHolder` qui est transmis en tant que dernière valeur d’argument avec un flux de données de formulaire qui doit être écrit dans le navigateur web client.

   * Créez un objet `FormResult` en obtenant la valeur du membre de données `value` de l’objet `com.adobe.idp.services.holders.FormsResultHolder`.
   * Créez un objet `BLOB` qui contient les données du formulaire en appelant la méthode `getOutputContent` de l’objet `FormsResult`.
   * Obtenez le type de contenu de l’objet `BLOB` en appelant sa méthode `getContentType`.
   * Définissez le type de contenu de l’objet `javax.servlet.http.HttpServletResponse` en appelant sa méthode `setContentType` et en transmettant le type de contenu de l’objet `BLOB`.
   * Créez un objet `javax.servlet.ServletOutputStream` utilisé pour écrire le flux de données de formulaire dans le navigateur web client en appelant la méthode `getOutputStream` de l’objet `javax.servlet.http.HttpServletResponse`.
   * Créez un tableau d’octets et renseignez-le en appelant la méthode `getBinaryData` de l’objet `BLOB`. Cette tâche affecte le contenu de l’objet `FormsResult` au tableau d’octets.
   * Appelez la méthode `write` de l’objet `javax.servlet.http.HttpServletResponse` pour envoyer le flux de données du formulaire vers le navigateur web du client. Transmettez le tableau d’octets à la méthode `write`.

   >[!NOTE]
   >
   >La méthode `renderPDFForm` renseigne l’objet `com.adobe.idp.services.holders.FormsResultHolder` qui est transmis en tant que dernière valeur d’argument avec un flux de données de formulaire qui doit être écrit dans le navigateur web client.

**Voir également**

[Appeler AEM Forms en utilisant le codage Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
