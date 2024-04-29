---
title: Créer de façon dynamique des documents DDX
description: Créez un document DDX de façon dynamique à l’aide de l’API Java et de l’API Web Service. La création dynamique d’un document DDX vous permet d’utiliser dans le document DDX des valeurs obtenues lors de l’exécution.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
role: Developer
exl-id: b3c19c82-e26f-4dc8-b846-6aec705cee08
solution: Experience Manager, Experience Manager Forms
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: ht
source-wordcount: '2153'
ht-degree: 100%

---

# Créer de façon dynamique des documents DDX {#dynamically-creating-ddx-documents}

**Les exemples et les échantillons de ce document sont réservés à l’environnement AEM Forms sur JEE.**

Vous pouvez créer dynamiquement un document DDX qui peut être utilisé pour effectuer une opération Assembler. La création dynamique d’un document DDX vous permet d’utiliser dans le document DDX des valeurs obtenues lors de l’exécution. Pour créer un document DDX de façon dynamique, utilisez des classes appartenant au langage de programmation que vous utilisez. Par exemple, si vous développez votre application cliente à l’aide de Java, utilisez des classes appartenant au package `org.w3c.dom.*`. De même, si vous utilisez Microsoft .NET, utilisez des classes appartenant à l’espace de noms `System.Xml`.

Avant de pouvoir transmettre le document DDX au service Assembler, convertissez le fichier XML d’une instance `org.w3c.dom.Document` vers une instance `com.adobe.idp.Document`. Si vous utilisez des services web, convertissez le XML à partir du type de données utilisé pour créer le XML (par exemple `XmlDocument`) en instance `BLOB`.

Aux fins de cette discussion, supposons que le document DDX suivant est créé de façon dynamique.

```xml
 <?xml version="1.0" encoding="UTF-8"?>
 <DDX xmlns="https://ns.adobe.com/DDX/1.0/">
      <PDFsFromBookmarks prefix="stmt">
     <PDF source="AssemblerResultPDF.pdf"/>
 </PDFsFromBookmarks>
 </DDX>
```

Ce document DDX désassemble un document PDF. Il est recommandé de vous familiariser avec le désassemblage de documents PDF.

>[!NOTE]
>
>Pour plus d’informations sur le service Assembler, consultez la section [Guide de référence des services pour AEM Forms](https://help.adobe.com/fr_FR/livecycle/11.0/Services/index.html).

>[!NOTE]
>
>Pour plus d’informations sur les documents DDX, consultez la section [Guide de référence du service Assembler et de DDX](https://www.adobe.com/go/learn_aemforms_ddx_63).

## Résumé des étapes {#summary-of-steps}

Pour désassembler un document PDF à l’aide d’un document DDX créé de façon dynamique, effectuez les tâches suivantes :

1. Incluez les fichiers de projet.
1. Créez un client Assembler PDF.
1. Créez le document DDX.
1. Convertissez le document DDX.
1. Définissez les options d’exécution.
1. Désassemblez le document PDF.
1. Enregistrez les documents PDF désassemblés.

**Inclure les fichiers de projet**

Incluez les fichiers nécessaires dans votre projet de développement. Si vous créez une application cliente à l’aide de Java, incluez les fichiers JAR nécessaires. Si vous utilisez des services Web, veillez à inclure les fichiers proxy.

Les fichiers JAR suivants doivent être ajoutés au chemin d’accès aux classes de votre projet :

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-assembler-client.jar
* adobe-utility.jar (obligatoire si AEM Forms est déployé sur JBoss)
* jbossall-client.jar (obligatoire si AEM Forms est déployé sur JBoss)

**Créer un client PDF Assembler**

Avant de pouvoir effectuer une opération Assembler par programmation, créez un client de service Assembler.

**Créer le document DDX**

Créez un document DDX à l’aide du langage de programmation que vous utilisez. Pour créer un document DDX qui désassemble un document PDF, assurez-vous qu’il contient l’élément `PDFsFromBookmarks`. Convertissez le type de données utilisé pour créer le document DDX en une instance `com.adobe.idp.Document` si vous utilisez l’API Java. Si vous utilisez des services web, convertissez le type de données en une instance `BLOB`.

**Convertir le document DDX**

Un document DDX créé à l’aide de classes `org.w3c.dom` doit être converti en objet `com.adobe.idp.Document`. Pour effectuer cette tâche lors de l’utilisation de l’API Java, utilisez les classes de transformation XML Java. Si vous utilisez des services web, convertissez le document DDX en un objet `BLOB`.

**Référencer un document PDF à désassembler**

Pour désassembler un document PDF, référencez un fichier PDF représentant le document PDF à désassembler. Lorsqu’il est transmis au service Assembler, un document PDF distinct est renvoyé pour chaque signet de niveau 1 dans le document.

**Définir des options de temps d’exécution**

Vous pouvez définir des options d’exécution qui contrôlent le comportement du service Assembler lors de l’exécution d’une tâche. Par exemple, vous pouvez définir une option qui indique au service Assembler de continuer à traiter une tâche même en cas d’erreur. Pour définir les options de temps d’exécution, utilisez un objet `AssemblerOptionSpec`.

**Désassembler le document PDF**

Désassemblez le document PDF en appelant l’opération `invokeDDX`. Transmettez le document DDX qui a été créé de façon dynamique. Le service Assembler renvoie des documents PDF désassemblés dans un objet de collection.

**Enregistrer des documents PDF désassemblés**

Tous les documents PDF désassemblés sont renvoyés dans un objet de collection. Effectuez une itération sur l’objet de collection et enregistrez chaque document PDF en tant que fichier PDF.

**Voir également**

[Créer de façon dynamique un document DDX à l’aide de l’API Java](/help/forms/developing/dynamically-creating-ddx-documents.md#dynamically-create-a-ddx-document-using-the-java-api)

[Création dynamique d’un document DDX à l’aide de l’API de service web](/help/forms/developing/dynamically-creating-ddx-documents.md#dynamically-create-a-ddx-document-using-the-web-service-api)

[Inclusion des fichiers de bibliothèque Java d’AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Désassembler des documents PDF par programme](/help/forms/developing/programmatically-disassembling-pdf-documents.md#programmatically-disassembling-pdf-documents)

## Créer un document DDX de façon dynamique à l’aide de l’API Java {#dynamically-create-a-ddx-document-using-the-java-api}

Créez un document DDX de façon dynamique et désassemblez un document PDF à l’aide de l’API Assembler Service (Java) :

1. Incluez les fichiers de projet.

   Incluez les fichiers JAR clients, tels que adobe-assembler-client.jar, dans le chemin d’accès aux classes de votre projet Java.

1. Créez un client Assembler PDF.

   * Créez un objet `ServiceClientFactory` qui contient des propriétés de connexion.
   * Créez un objet `AssemblerServiceClient` en utilisant son constructeur et en transmettant l’objet `ServiceClientFactory`.

1. Créez le document DDX.

   * Créez un objet `DocumentBuilderFactory` Java en appelant la méthode `newInstance` de la classe `DocumentBuilderFactory`.
   * Créez un objet `DocumentBuilder` Java en appelant la méthode `newDocumentBuilder` de l’objet `DocumentBuilderFactory`.
   * Appelez la méthode `newDocument` de l’objet `DocumentBuilder` pour instancier un objet `org.w3c.dom.Document`.
   * Créez l’élément racine du document DDX en appelant la méthode `createElement` de l’objet `org.w3c.dom.Document`. Cette méthode crée un objet `Element` qui représente l’élément racine. Transmettez une valeur de chaîne représentant le nom de l’élément à la méthode `createElement`. Convertissez la valeur de retour en `Element`. Ensuite, définissez une valeur pour l’élément enfant en appelant sa méthode `setAttribute`. Enfin, ajoutez l’élément à l’élément d’en-tête en appelant sa méthode `appendChild` et transmettez l’objet d’élément enfant en tant qu’argument. Les lignes de code suivantes illustrent cette logique dʼapplication :
     ` Element root = (Element)document.createElement("DDX");  root.setAttribute("xmlns","https://ns.adobe.com/DDX/1.0/");  document.appendChild(root);`

   * Créez l’élément `PDFsFromBookmarks` en appelant la méthode `createElement` de l’objet `Document`. Transmettez une valeur de chaîne représentant le nom de l’élément à la méthode `createElement`. Convertissez la valeur de retour en `Element`. Définissez une valeur pour l’élément `PDFsFromBookmarks` en appelant sa méthode `setAttribute`. Ajoutez l’élément `PDFsFromBookmarks` à l’élément `DDX` en appelant la méthode `appendChild` de l’élément DDX. Transmettez l’objet d’élément `PDFsFromBookmarks` en tant qu’argument. Les lignes de code suivantes illustrent cette logique dʼapplication :

     ` Element PDFsFromBookmarks = (Element)document.createElement("PDFsFromBookmarks");  PDFsFromBookmarks.setAttribute("prefix","stmt");  root.appendChild(PDFsFromBookmarks);`

   * Créez un élément `PDF` en appelant la méthode `createElement` de l’objet `Document`. Transmettez une valeur de chaîne qui représente le nom de l’élément. Convertissez la valeur de retour en `Element`. Définissez une valeur pour l’élément `PDF` en appelant sa méthode `setAttribute`. Ajoutez l’élément `PDF` à l’élément `PDFsFromBookmarks` en appelant la méthode `appendChild` de l’élément `PDFsFromBookmarks`. Transmettez l’objet d’élément `PDF` en tant qu’argument. Les lignes de code suivantes illustrent cette logique dʼapplication :

     ` Element PDF = (Element)document.createElement("PDF");  PDF.setAttribute("source","AssemblerResultPDF.pdf");  PDFsFromBookmarks.appendChild(PDF);`

1. Convertissez le document DDX.

   * Créez un objet `javax.xml.transform.Transformer` en appelant la méthode statique `newInstance` de lʼobjet `javax.xml.transform.Transformer`.
   * Créez un objet `Transformer` en appelant la méthode `newTransformer` de l’objet `TransformerFactory`.
   * Créez un objet `ByteArrayOutputStream` en utilisant son constructeur.
   * Créez un objet `javax.xml.transform.dom.DOMSource` en utilisant son constructeur. Transmettez l’objet `org.w3c.dom.Document` qui représente le document DDX.
   * Créez un objet `javax.xml.transform.dom.DOMSource` en utilisant son constructeur et en transmettant l’objet `ByteArrayOutputStream`. 
   * Renseignez l’objet `ByteArrayOutputStream` Java en appelant la méthode `transform` de l’objet `javax.xml.transform.Transformer`. Transmettez les objets `javax.xml.transform.dom.DOMSource` et `javax.xml.transform.stream.StreamResult`.
   * Créez un tableau d’octets et affectez la taille de l’objet `ByteArrayOutputStream` au tableau d’octets.
   * Renseignez le tableau dʼoctets en appelant la méthode `toByteArray` de lʼobjet `ByteArrayOutputStream`.
   * Créez un objet `com.adobe.idp.Document` en utilisant son constructeur et en transmettant le tableau d’octets.

1. Référencez un document de PDF à désassembler.

   * Créez un objet `java.util.Map` servant à stocker des documents PDF d’entrée à l’aide d’un constructeur `HashMap`.
   * Créez un objet `java.io.FileInputStream` en utilisant son constructeur et en transmettant l’emplacement du document PDF à désassembler.
   * Créez un objet `com.adobe.idp.Document`. Transmettez l’objet `java.io.FileInputStream` contenant le document PDF à désassembler.
   * Ajoutez une entrée à l’objet `java.util.Map` en appelant sa méthode `put` et en transmettant les arguments suivants :

      * Une valeur de chaîne qui représente le nom de la clé. Cette valeur doit correspondre à celle de l’élément source PDF spécifié dans le document DDX. (Dans le document DDX créé dynamiquement, la valeur est `AssemblerResultPDF.pdf`.)
      * Un objet `com.adobe.idp.Document` qui contient le document PDF à désassembler.

1. Définissez les options d’exécution.

   * Créez un objet `AssemblerOptionSpec` qui stocke les options d’exécution en utilisant son constructeur.
   * Définissez les options d’exécution pour répondre à vos exigences professionnelles en appelant une méthode appartenant à l’objet `AssemblerOptionSpec`. Par exemple, pour demander au service Assembler de continuer à traiter une tâche en cas d’erreur, appelez la méthode `setFailOnError` de l’objet `AssemblerOptionSpec` et transmettez `false`.

1. Désassemblez le document PDF.

   Appelez la méthode `invokeDDX` de l’objet `AssemblerServiceClient` et transmettez les valeurs suivantes :

   * Un objet `com.adobe.idp.Document` représentant le document DDX créé dynamiquement
   * Un objet `java.util.Map` contenant le document PDF à désassembler
   * Un objet `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` spécifiant les options d’exécution, notamment la police par défaut et le niveau de journalisation de la tâche

   La méthode `invokeDDX` renvoie un objet `com.adobe.livecycle.assembler.client.AssemblerResult` contenant les documents PDF désassemblés et les exceptions survenues.

1. Enregistrez les documents PDF désassemblés.

   Pour obtenir des documents PDF désassemblés, procédez comme suit :

   * Appelez la méthode `getDocuments` de l’objet `AssemblerResult`. Cette méthode renvoie un objet `java.util.Map`.
   * Effectuez une itération à l’aide de l’objet `java.util.Map` jusqu’à ce que vous trouviez l’objet `com.adobe.idp.Document` résultant.
   * Appelez la méthode `copyToFile` de l’objet `com.adobe.idp.Document` pour extraire le document PDF.

**Voir également**

[Démarrage rapide (mode SOAP) : création dynamique d’un document DDX à l’aide de l’API Java](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-dynamically-creating-a-ddx-document-using-the-java-api)

[Inclusion des fichiers de bibliothèque Java d’AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Création dynamique d’un document DDX à l’aide de l’API de service web {#dynamically-create-a-ddx-document-using-the-web-service-api}

Créez de manière dynamique un document DDX et désassemblez un document PDF à l’aide de l’API du service Assembler (service web) :

1. Incluez les fichiers de projet.

   Créez un projet Microsoft .NET qui utilise MTOM. Veillez à utiliser la définition WSDL suivante lors de la définition d’une référence de service : `http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Remplacez `localhost` par l’adresse IP du serveur hébergeant AEM Forms.

1. Créez un client Assembler PDF.

   * Créez un objet `AssemblerServiceClient` en utilisant son constructeur par défaut.
   * Créez un objet `AssemblerServiceClient.Endpoint.Address` en utilisant le constructeur `System.ServiceModel.EndpointAddress`. Transmettez une valeur de chaîne qui spécifie le WSDL au service AEM Forms (par exemple, `http://localhost:8080/soap/services/AssemblerService?blob=mtom`). Vous n’avez pas besoin d’utiliser l’attribut `lc_version`. Cet attribut est utilisé lorsque vous créez une référence de service.
   * Créez un objet `System.ServiceModel.BasicHttpBinding` en récupérant la valeur du champ `AssemblerServiceClient.Endpoint.Binding`. Convertissez la valeur de retour en `BasicHttpBinding`.
   * Définissez le champ `MessageEncoding` de l’objet `System.ServiceModel.BasicHttpBinding` sur `WSMessageEncoding.Mtom`. Cette valeur garantit l’utilisation de MTOM.
   * Activez l’authentification HTTP de base en effectuant les tâches suivantes :

      * Attribuez le nom d’utilisateur AEM forms au champ `AssemblerServiceClient.ClientCredentials.UserName.UserName`.
      * Attribuez la valeur de mot de passe correspondante au champ `AssemblerServiceClient.ClientCredentials.UserName.Password`.
      * Attribuez la valeur constante `HttpClientCredentialType.Basic` au champ `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Attribuez la valeur constante `BasicHttpSecurityMode.TransportCredentialOnly` au champ `BasicHttpBindingSecurity.Security.Mode`.

1. Créez le document DDX.

   * Créez un objet `System.Xml.XmlElement` en utilisant son constructeur.
   * Créez l’élément racine du document DDX en appelant la méthode `CreateElement` de l’objet `XmlElement`. Cette méthode crée un objet `Element` qui représente l’élément racine. Transmettez une valeur de chaîne représentant le nom de l’élément à la méthode `CreateElement`. Définissez une valeur pour l’élément DDX en appelant sa méthode `SetAttribute`. Enfin, ajoutez l’élément au document DDX en appelant la méthode `AppendChild` de l’objet `XmlElement`. Transmettez l’objet DDX en tant qu’argument. Les lignes de code suivantes illustrent cette logique dʼapplication :

     ` System.Xml.XmlElement root = ddx.CreateElement("DDX");  root.SetAttribute("xmlns", "https://ns.adobe.com/DDX/1.0/");  ddx.AppendChild(root);`

   * Créez l’élément `PDFsFromBookmarks` du document DDX en appelant la méthode `CreateElement` de l’objet `XmlElement`. Transmettez une valeur de chaîne représentant le nom de l’élément à la méthode `CreateElement`. Ensuite, définissez une valeur pour l’élément en appelant sa méthode `SetAttribute`. Ajoutez l’élément `PDFsFromBookmarks` à l’élément racine en appelant la méthode `AppendChild` de l’élément `DDX`. Transmettez l’objet d’élément `PDFsFromBookmarks` en tant qu’argument. Les lignes de code suivantes illustrent cette logique dʼapplication :

     ` XmlElement PDFsFromBookmarks = ddx.CreateElement("PDFsFromBookmarks");  PDFsFromBookmarks.SetAttribute("prefix", "stmt");  root.AppendChild(PDFsFromBookmarks);`

   * Créez l’élément `PDF` du document DDX en appelant la méthode `CreateElement` de l’objet `XmlElement`. Transmettez une valeur de chaîne représentant le nom de l’élément à la méthode `CreateElement`. Ensuite, définissez une valeur pour l’élément enfant en appelant sa méthode `SetAttribute`. Ajoutez l’élément `PDF` à l’élément `PDFsFromBookmarks` en appelant la méthode `AppendChild` de l’élément `PDFsFromBookmarks`. Transmettez l’objet d’élément `PDF` en tant qu’argument. Les lignes de code suivantes illustrent cette logique dʼapplication :

     ` XmlElement PDF = ddx.CreateElement("PDF");  PDF.SetAttribute("source", "AssemblerResultPDF.pdf");  PDFsFromBookmarks.AppendChild(PDF);`

1. Convertissez le document DDX.

   * Créez un objet `System.IO.MemoryStream` en utilisant son constructeur.
   * Renseignez l’objet `MemoryStream` avec le document DDX en utilisant l’objet `XmlElement` qui représente le document DDX. Appelez la méthode `Save` de l’objet `XmlElement` et transmettez l’objet `MemoryStream`.
   * Créez un tableau d’octets et renseignez-le avec les données contenues dans l’objet `MemoryStream`. Le code suivant présente la logique de cette application :

     ` int bufLen = Convert.ToInt32(stream.Length);  byte[] byteArray = new byte[bufLen];  stream.Position = 0;  int count = stream.Read(byteArray, 0, bufLen);`

   * Créez un objet `BLOB`. Affectez le tableau d’octets au champ `MTOM` de l’objet `BLOB`.

1. Référencez un document de PDF à désassembler.

   * Créez un objet `BLOB` en utilisant son constructeur. L’objet `BLOB` sert à stocker le document PDF d’entrée. Cet objet `BLOB` est transmis à `invokeOneDocument` comme argument.
   * Créez un objet `System.IO.FileStream` en appelant son constructeur. Transmettez une valeur de chaîne qui représente l’emplacement du fichier du document PDF d’entrée et le mode d’ouverture du fichier.
   * Créez un tableau d’octets qui stocke le contenu de l’objet `System.IO.FileStream`. Vous pouvez déterminer la taille du tableau d’octets en obtenant la propriété `Length` de l’objet `System.IO.FileStream`.
   * Renseignez le tableau d’octets avec les données de diffusion en appelant la méthode `Read` de l’objet `System.IO.FileStream` et en transmettant le tableau d’octets, la position de départ et la longueur du flux à lire.
   * Renseignez l’objet `BLOB` en affectant le contenu du tableau d’octets à sa propriété `MTOM`.

1. Définissez les options d’exécution.

   * Créez un objet `AssemblerOptionSpec` qui stocke les options d’exécution en utilisant son constructeur.
   * Définissez les options d’exécution pour répondre à vos exigences professionnelles en attribuant une valeur à un membre de données qui appartient à l’objet `AssemblerOptionSpec`. Par exemple, pour demander au service Assembler de continuer à traiter une tâche en cas d’erreur, affectez `false` au membre de données `failOnError` de l’objet `AssemblerOptionSpec`.

1. Désassemblez le document PDF.

   Appelez la méthode `invokeDDX` de l’objet `AssemblerServiceClient` et transmettez les valeurs suivantes :

   * Un objet `BLOB` qui représente le document DDX créé dynamiquement.
   * Tableau `mapItem` qui contient le document PDF d’entrée.
   * Un objet `AssemblerOptionSpec` qui spécifie les options d’exécution.

   La méthode `invokeDDX` renvoie un objet `AssemblerResult` contenant les résultats de la tâche et les exceptions survenues.

1. Enregistrez les documents PDF désassemblés.

   Pour obtenir les documents PDF nouvellement créés, procédez comme suit :

   * Accédez au champ `documents` de l’objet `AssemblerResult`, qui est un objet `Map` contenant les documents PDF désassemblés.
   * Effectuez une itération par le biais de l’objet `Map` pour obtenir chaque document généré. Convertissez ensuite la `value` de ce membre du tableau en un objet `BLOB`.
   * Extrayez les données binaires représentant le document PDF en accédant à la propriété `MTOM` de son objet `BLOB`. Cette opération renvoie un tableau d’octets que vous pouvez enregistrer dans un fichier PDF.

**Voir également**

[Appeler AEM Forms en utilisant MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Appel d’AEM Forms à l’aide de SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)
