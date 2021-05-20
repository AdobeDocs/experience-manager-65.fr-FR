---
title: Création dynamique de documents DDX
seo-title: Création dynamique de documents DDX
description: Créez un document DDX de manière dynamique à l’aide de l’API Java et de l’API Web Service. La création dynamique d’un document DDX vous permet d’utiliser dans le document DDX des valeurs obtenues lors de l’exécution.
seo-description: Créez un document DDX de manière dynamique à l’aide de l’API Java et de l’API Web Service. La création dynamique d’un document DDX vous permet d’utiliser dans le document DDX des valeurs obtenues lors de l’exécution.
uuid: b73e8069-6c9f-4517-a0ae-f3d503191d2d
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 2ad227de-68a8-446f-8c4f-a33a6f95bec8
role: Developer
exl-id: b3c19c82-e26f-4dc8-b846-6aec705cee08
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '2199'
ht-degree: 4%

---

# Création dynamique de documents DDX {#dynamically-creating-ddx-documents}

**Les exemples et les exemples de ce document sont réservés à l’environnement AEM Forms on JEE.**

Vous pouvez créer dynamiquement un document DDX qui peut être utilisé pour effectuer une opération Assembler. La création dynamique d’un document DDX vous permet d’utiliser dans le document DDX des valeurs obtenues lors de l’exécution. Pour créer dynamiquement un document DX, utilisez des classes appartenant au langage de programmation que vous utilisez. Par exemple, si vous développez votre application cliente à l’aide de Java, utilisez des classes appartenant au package `org.w3c.dom.*`. De même, si vous utilisez Microsoft .NET, utilisez des classes qui appartiennent à l’espace de noms `System.Xml`.

Avant de pouvoir transmettre le document DX au service Assembler, convertissez le fichier XML d’une instance `org.w3c.dom.Document` en instance `com.adobe.idp.Document`. Si vous utilisez des services Web, convertissez le XML du type de données utilisé pour créer le XML (par exemple, `XmlDocument`) en instance `BLOB`.

Pour cette discussion, supposons que le document DDX suivant est créé dynamiquement.

```xml
 <?xml version="1.0" encoding="UTF-8"?>
 <DDX xmlns="https://ns.adobe.com/DDX/1.0/">
      <PDFsFromBookmarks prefix="stmt">
     <PDF source="AssemblerResultPDF.pdf"/>
 </PDFsFromBookmarks>
 </DDX>
```

Ce document DDX désassemble un document PDF. Il est recommandé de vous familiariser avec le désassemblage de documents PDF.

>[!NOTE]
>
>Pour plus d’informations sur le service Assembler, voir [Référence des services pour AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

>[!NOTE]
>
>Pour plus d’informations sur un document DDX, voir [Guide de référence du service Assembler et de DDX](https://www.adobe.com/go/learn_aemforms_ddx_63).

## Résumé des étapes {#summary-of-steps}

Pour désassembler un document PDF à l’aide d’un document DDX créé dynamiquement, effectuez les tâches suivantes :

1. Inclure les fichiers de projet.
1. Créez un client PDF Assembler.
1. Créez le document DDX.
1. Convertissez le document DX.
1. Définissez les options d’exécution.
1. Désassemblez le document PDF.
1. Enregistrez les documents PDF désassemblés.

**Inclure les fichiers de projet**

Incluez les fichiers nécessaires dans votre projet de développement. Si vous créez une application cliente à l’aide de Java, incluez les fichiers JAR nécessaires. Si vous utilisez des services Web, veillez à inclure les fichiers proxy.

Les fichiers JAR suivants doivent être ajoutés au chemin de classe de votre projet :

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-assembler-client.jar
* adobe-utility.jar (obligatoire si AEM Forms est déployé sur JBoss)
* jbossall-client.jar (obligatoire si AEM Forms est déployé sur JBoss)

**Création d’un client PDF Assembler**

Avant de pouvoir effectuer une opération Assembler par programmation, créez un client de service Assembler.

**Création du document DDX**

Créez un document DDX à l’aide du langage de programmation que vous utilisez. Pour créer un document DDX qui désassemble un document PDF, assurez-vous qu’il contient l’élément `PDFsFromBookmarks` . Convertissez le type de données utilisé pour créer le document DDX en instance `com.adobe.idp.Document` si vous utilisez l’API Java. Si vous utilisez des services web, convertissez le type de données en instance `BLOB`.

**Convertir le document DDX**

Un document DDX créé à l’aide des classes `org.w3c.dom` doit être converti en objet `com.adobe.idp.Document`. Pour effectuer cette tâche lors de l’utilisation de l’API Java, utilisez les classes de transformation XML Java. Si vous utilisez des services Web, convertissez le document DDX en objet `BLOB`.

**Référence à un document PDF à désassembler**

Pour désassembler un document PDF, référencez un fichier PDF qui représente le document PDF à désassembler. Lorsqu’il est transmis au service Assembler, un document PDF distinct est renvoyé pour chaque signet de niveau 1 dans le document.

**Définition des options d’exécution**

Vous pouvez définir des options d’exécution qui contrôlent le comportement du service Assembler lors de l’exécution d’une tâche. Par exemple, vous pouvez définir une option qui indique au service Assembler de continuer à traiter une tâche en cas d’erreur. Pour définir les options d’exécution, vous utilisez un objet `AssemblerOptionSpec`.

**Désassemblage du document PDF**

Désassemblez le document PDF en appelant l’opération `invokeDDX`. Transmettez le document DDX qui a été créé dynamiquement. Le service Assembler renvoie des documents PDF désassemblés dans un objet de collection.

**Enregistrement des documents PDF désassemblés**

Tous les documents PDF désassemblés sont renvoyés dans un objet de collection. Effectuez une itération sur l’objet de collection et enregistrez chaque document PDF en tant que fichier PDF.

**Voir également**

[Création dynamique d’un document DX à l’aide de l’API Java](/help/forms/developing/dynamically-creating-ddx-documents.md#dynamically-create-a-ddx-document-using-the-java-api)

[Création dynamique d’un document DX à l’aide de l’API de service Web](/help/forms/developing/dynamically-creating-ddx-documents.md#dynamically-create-a-ddx-document-using-the-web-service-api)

[Inclusion des fichiers de bibliothèque Java d’AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Démontage programmatique de documents PDF](/help/forms/developing/programmatically-disassembling-pdf-documents.md#programmatically-disassembling-pdf-documents)

## Créez de manière dynamique un document DX à l’aide de l’API Java {#dynamically-create-a-ddx-document-using-the-java-api}

Créez de manière dynamique un document DX et désassemblez un document PDF à l’aide de l’API Assembler Service (Java) :

1. Inclure les fichiers de projet.

   Incluez des fichiers JAR client, tels que adobe-assembler-client.jar, dans le chemin d’accès à la classe de votre projet Java.

1. Créez un client PDF Assembler.

   * Créez un objet `ServiceClientFactory` qui contient des propriétés de connexion.
   * Créez un objet `AssemblerServiceClient` en utilisant son constructeur et en transmettant l’objet `ServiceClientFactory`.

1. Créez le document DDX.

   * Créez un objet Java `DocumentBuilderFactory` en appelant la méthode `DocumentBuilderFactory` class’ `newInstance` .
   * Créez un objet Java `DocumentBuilder` en appelant la méthode `newDocumentBuilder` de l’objet `DocumentBuilderFactory`.
   * Appelez la méthode `newDocument` de l’objet `DocumentBuilder` pour instancier un objet `org.w3c.dom.Document`.
   * Créez l’élément racine du document DDX en appelant la méthode `org.w3c.dom.Document` de l’objet `createElement`. Cette méthode crée un objet `Element` qui représente l’élément racine. Transmettez une valeur string représentant le nom de l’élément à la méthode `createElement` . Convertissez la valeur de retour en `Element`. Définissez ensuite une valeur pour l’élément enfant en appelant sa méthode `setAttribute`. Enfin, ajoutez l’élément à l’élément d’en-tête en appelant la méthode `appendChild` de l’élément d’en-tête et transmettez l’objet d’élément enfant comme argument. Les lignes de code suivantes présentent cette logique d’application :
      ` Element root = (Element)document.createElement("DDX");  root.setAttribute("xmlns","https://ns.adobe.com/DDX/1.0/");  document.appendChild(root);`

   * Créez l’élément `PDFsFromBookmarks` en appelant la méthode `createElement` de l’objet `Document`. Transmettez une valeur string représentant le nom de l’élément à la méthode `createElement` . Convertissez la valeur de retour en `Element`. Définissez une valeur pour l’élément `PDFsFromBookmarks` en appelant sa méthode `setAttribute`. Ajoutez l’élément `PDFsFromBookmarks` à l’élément `DDX` en appelant la méthode `appendChild` de l’élément DDX. Transmettez l’objet d’élément `PDFsFromBookmarks` en tant qu’argument. Les lignes de code suivantes présentent cette logique d’application :

      ` Element PDFsFromBookmarks = (Element)document.createElement("PDFsFromBookmarks");  PDFsFromBookmarks.setAttribute("prefix","stmt");  root.appendChild(PDFsFromBookmarks);`

   * Créez un élément `PDF` en appelant la méthode `createElement` de l’objet `Document`. Transmettez une valeur string qui représente le nom de l’élément. Convertissez la valeur de retour en `Element`. Définissez une valeur pour l’élément `PDF` en appelant sa méthode `setAttribute`. Ajoutez l’élément `PDF` à l’élément `PDFsFromBookmarks` en appelant la méthode `PDFsFromBookmarks` de l’élément `appendChild` . Transmettez l’objet d’élément `PDF` en tant qu’argument. Les lignes de code suivantes présentent cette logique d’application :

      ` Element PDF = (Element)document.createElement("PDF");  PDF.setAttribute("source","AssemblerResultPDF.pdf");  PDFsFromBookmarks.appendChild(PDF);`

1. Convertissez le document DX.

   * Créez un objet `javax.xml.transform.Transformer` en appelant la méthode `javax.xml.transform.Transformer` statique de l’objet `newInstance`.
   * Créez un objet `Transformer` en appelant la méthode `newTransformer` de l’objet `TransformerFactory`.
   * Créez un objet `ByteArrayOutputStream` en utilisant son constructeur.
   * Créez un objet `javax.xml.transform.dom.DOMSource` en utilisant son constructeur. Transmettez l’objet `org.w3c.dom.Document` qui représente le document DDX.
   * Créez un objet `javax.xml.transform.dom.DOMSource` en utilisant son constructeur et en transmettant l’objet `ByteArrayOutputStream`. 
   * Renseignez l’objet Java `ByteArrayOutputStream` en appelant la méthode `javax.xml.transform.Transformer` de l’objet `transform`. Transmettez les objets `javax.xml.transform.dom.DOMSource` et `javax.xml.transform.stream.StreamResult`.
   * Créez un tableau d’octets et affectez la taille de l’objet `ByteArrayOutputStream` au tableau d’octets.
   * Renseignez le tableau d’octets en appelant la méthode `toByteArray` de l’objet `ByteArrayOutputStream`.
   * Créez un objet `com.adobe.idp.Document` en utilisant son constructeur et en transmettant le tableau d’octets.

1. Référencez un document PDF à désassembler.

   * Créez un objet `java.util.Map` utilisé pour stocker des documents PDF d’entrée à l’aide d’un constructeur `HashMap`.
   * Créez un objet `java.io.FileInputStream` en utilisant son constructeur et en transmettant l’emplacement du document PDF à désassembler.
   * Créez un objet `com.adobe.idp.Document` . Transmettez l’objet `java.io.FileInputStream` contenant le document PDF à désassembler.
   * Ajoutez une entrée à l’objet `java.util.Map` en appelant sa méthode `put` et en transmettant les arguments suivants :

      * Une valeur string qui représente le nom de la clé. Cette valeur doit correspondre à la valeur de l’élément de source PDF spécifié dans le document DDX. (Dans le document DDX créé dynamiquement, la valeur est `AssemblerResultPDF.pdf`.)
      * Objet `com.adobe.idp.Document` contenant le document PDF à désassembler.

1. Définissez les options d’exécution.

   * Créez un objet `AssemblerOptionSpec` qui stocke les options d’exécution à l’aide de son constructeur.
   * Définissez les options d’exécution pour répondre aux besoins de votre entreprise en appelant une méthode appartenant à l’objet `AssemblerOptionSpec` . Par exemple, pour demander au service Assembler de continuer à traiter une tâche en cas d’erreur, appelez la méthode `setFailOnError` de l’objet `false` et transmettez `AssemblerOptionSpec`.

1. Désassemblez le document PDF.

   Appelez la méthode `invokeDDX` de l’objet `AssemblerServiceClient` et transmettez les valeurs suivantes :

   * Objet `com.adobe.idp.Document` représentant le document DDX créé dynamiquement
   * Objet `java.util.Map` contenant le document PDF à désassembler
   * Objet `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` qui spécifie les options d’exécution, y compris la police par défaut et le niveau de journalisation de la tâche

   La méthode `invokeDDX` renvoie un objet `com.adobe.livecycle.assembler.client.AssemblerResult` contenant les documents PDF désassemblés et les exceptions survenues.

1. Enregistrez les documents PDF désassemblés.

   Pour obtenir les documents PDF désassemblés, effectuez les actions suivantes :

   * Appelez la méthode `getDocuments` de l’objet `AssemblerResult`. Cette méthode renvoie un objet `java.util.Map` .
   * Effectuez une itération sur l’objet `java.util.Map` jusqu’à ce que vous trouviez l’objet `com.adobe.idp.Document` résultant.
   * Appelez la méthode `copyToFile` de l’objet `com.adobe.idp.Document` pour extraire le document PDF.

**Voir également**

[Démarrage rapide (mode SOAP) : Création dynamique d’un document DX à l’aide de l’API Java](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-dynamically-creating-a-ddx-document-using-the-java-api)

[Inclusion des fichiers de bibliothèque Java d’AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Créez de manière dynamique un document DX à l’aide de l’API de service Web {#dynamically-create-a-ddx-document-using-the-web-service-api}

Créez de manière dynamique un document DX et désassemblez un document PDF à l’aide de l’API Assembler Service (service Web) :

1. Inclure les fichiers de projet.

   Créez un projet Microsoft .NET qui utilise MTOM. Assurez-vous d’utiliser la définition WSDL suivante lors de la définition d’une référence de service : `http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Remplacez `localhost` par l’adresse IP du serveur hébergeant AEM Forms.

1. Créez un client PDF Assembler.

   * Créez un objet `AssemblerServiceClient` à l’aide de son constructeur par défaut.
   * Créez un objet `AssemblerServiceClient.Endpoint.Address` à l’aide du constructeur `System.ServiceModel.EndpointAddress`. Transmettez une valeur string qui spécifie le WSDL au service AEM Forms (par exemple, `http://localhost:8080/soap/services/AssemblerService?blob=mtom`). Vous n’avez pas besoin d’utiliser l’attribut `lc_version`. Cet attribut est utilisé lorsque vous créez une référence de service.
   * Créez un objet `System.ServiceModel.BasicHttpBinding` en obtenant la valeur du champ `AssemblerServiceClient.Endpoint.Binding`. Convertissez la valeur de retour en `BasicHttpBinding`.
   * Définissez le champ `MessageEncoding` de l’objet `System.ServiceModel.BasicHttpBinding` sur `WSMessageEncoding.Mtom`. Cette valeur garantit l’utilisation de MTOM.
   * Activez l’authentification HTTP de base en effectuant les tâches suivantes :

      * Attribuez le nom d’utilisateur AEM forms au champ `AssemblerServiceClient.ClientCredentials.UserName.UserName`.
      * Attribuez la valeur de mot de passe correspondante au champ `AssemblerServiceClient.ClientCredentials.UserName.Password`.
      * Attribuez la valeur constante `HttpClientCredentialType.Basic` au champ `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Attribuez la valeur constante `BasicHttpSecurityMode.TransportCredentialOnly` au champ `BasicHttpBindingSecurity.Security.Mode`.

1. Créez le document DDX.

   * Créez un objet `System.Xml.XmlElement` en utilisant son constructeur.
   * Créez l’élément racine du document DDX en appelant la méthode `XmlElement` de l’objet `CreateElement`. Cette méthode crée un objet `Element` qui représente l’élément racine. Transmettez une valeur string représentant le nom de l’élément à la méthode `CreateElement` . Définissez une valeur pour l’élément DDX en appelant sa méthode `SetAttribute`. Enfin, ajoutez l’élément au document DDX en appelant la méthode `XmlElement` de l’objet `AppendChild`. Transmettez l’objet DDX en tant qu’argument. Les lignes de code suivantes présentent cette logique d’application :

      ` System.Xml.XmlElement root = ddx.CreateElement("DDX");  root.SetAttribute("xmlns", "https://ns.adobe.com/DDX/1.0/");  ddx.AppendChild(root);`

   * Créez l’élément `PDFsFromBookmarks` du document DDX en appelant la méthode `CreateElement` de l’objet `XmlElement`. Transmettez une valeur string représentant le nom de l’élément à la méthode `CreateElement` . Définissez ensuite une valeur pour l’élément en appelant sa méthode `SetAttribute`. Ajoutez l’élément `PDFsFromBookmarks` à l’élément racine en appelant la méthode `AppendChild` de l’élément `DDX`. Transmettez l’objet d’élément `PDFsFromBookmarks` en tant qu’argument. Les lignes de code suivantes présentent cette logique d’application :

      ` XmlElement PDFsFromBookmarks = ddx.CreateElement("PDFsFromBookmarks");  PDFsFromBookmarks.SetAttribute("prefix", "stmt");  root.AppendChild(PDFsFromBookmarks);`

   * Créez l’élément `PDF` du document DDX en appelant la méthode `CreateElement` de l’objet `XmlElement`. Transmettez une valeur string représentant le nom de l’élément à la méthode `CreateElement` . Définissez ensuite une valeur pour l’élément enfant en appelant sa méthode `SetAttribute`. Ajoutez l’élément `PDF` à l’élément `PDFsFromBookmarks` en appelant la méthode `PDFsFromBookmarks` de l’élément `AppendChild` . Transmettez l’objet d’élément `PDF` en tant qu’argument. Les lignes de code suivantes présentent cette logique d’application :

      ` XmlElement PDF = ddx.CreateElement("PDF");  PDF.SetAttribute("source", "AssemblerResultPDF.pdf");  PDFsFromBookmarks.AppendChild(PDF);`

1. Convertissez le document DX.

   * Créez un objet `System.IO.MemoryStream` en utilisant son constructeur.
   * Remplissez l’objet `MemoryStream` avec le document DDX en utilisant l’objet `XmlElement` qui représente le document DDX. Appelez la méthode `Save` de l’objet `XmlElement` et transmettez l’objet `MemoryStream` .
   * Créez un tableau d’octets et renseignez-le avec les données situées dans l’objet `MemoryStream`. Le code suivant présente la logique de l’application :

      ` int bufLen = Convert.ToInt32(stream.Length);  byte[] byteArray = new byte[bufLen];  stream.Position = 0;  int count = stream.Read(byteArray, 0, bufLen);`

   * Créez un objet `BLOB` . Affectez le tableau d’octets au champ `MTOM` de l’objet `BLOB`.

1. Référencez un document PDF à désassembler.

   * Créez un objet `BLOB` en utilisant son constructeur. L’objet `BLOB` est utilisé pour stocker le document PDF d’entrée. Cet objet `BLOB` est transmis à `invokeOneDocument` en tant qu’argument.
   * Créez un objet `System.IO.FileStream` en appelant son constructeur. Transmettez une valeur string qui représente l’emplacement du fichier du document PDF d’entrée et le mode d’ouverture du fichier.
   * Créez un tableau d’octets qui stocke le contenu de l’objet `System.IO.FileStream`. Vous pouvez déterminer la taille du tableau d’octets en obtenant la propriété `System.IO.FileStream` de l’objet `Length`.
   * Renseignez le tableau d’octets avec les données de flux en appelant la méthode `System.IO.FileStream` de l’objet `Read` et en transmettant le tableau d’octets, la position de départ et la longueur du flux à lire.
   * Renseignez l’objet `BLOB` en attribuant sa propriété `MTOM` au contenu du tableau d’octets.

1. Définissez les options d’exécution.

   * Créez un objet `AssemblerOptionSpec` qui stocke les options d’exécution à l’aide de son constructeur.
   * Définissez des options d’exécution pour répondre aux besoins de votre entreprise en attribuant une valeur à un membre de données qui appartient à l’objet `AssemblerOptionSpec`. Par exemple, pour demander au service Assembler de continuer à traiter une tâche en cas d’erreur, affectez `false` au membre de données `failOnError` de l’objet `AssemblerOptionSpec`.

1. Désassemblez le document PDF.

   Appelez la méthode `invokeDDX` de l’objet `AssemblerServiceClient` et transmettez les valeurs suivantes :

   * Objet `BLOB` représentant le document DDX créé dynamiquement
   * Tableau `mapItem` contenant le document PDF d’entrée
   * Objet `AssemblerOptionSpec` spécifiant les options d’exécution

   La méthode `invokeDDX` renvoie un objet `AssemblerResult` contenant les résultats de la tâche et toutes les exceptions qui se sont produites.

1. Enregistrez les documents PDF désassemblés.

   Pour obtenir les documents PDF nouvellement créés, procédez comme suit :

   * Accédez au champ `documents` de l’objet `AssemblerResult`, qui est un objet `Map` contenant les documents PDF désassemblés.
   * Effectuez une itération sur l’objet `Map` pour obtenir chaque document généré. Ensuite, convertissez le `value` de ce membre de tableau en `BLOB`.
   * Extrayez les données binaires qui représentent le document PDF en accédant à la propriété `MTOM` de l’objet `BLOB`. Cette opération renvoie un tableau d’octets que vous pouvez écrire dans un fichier PDF.

**Voir également**

[Appel d’AEM Forms à l’aide de MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Appel d’AEM Forms à l’aide de SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)
