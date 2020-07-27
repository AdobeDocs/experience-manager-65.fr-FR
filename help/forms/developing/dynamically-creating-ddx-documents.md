---
title: Création dynamique de Documents DDX
seo-title: Création dynamique de Documents DDX
description: 'null'
seo-description: 'null'
uuid: b73e8069-6c9f-4517-a0ae-f3d503191d2d
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 2ad227de-68a8-446f-8c4f-a33a6f95bec8
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '2123'
ht-degree: 4%

---


# Création dynamique de Documents DDX {#dynamically-creating-ddx-documents}

Vous pouvez créer de manière dynamique un document DDX qui peut être utilisé pour effectuer une opération Assembler. La création dynamique d’un document DDX vous permet d’utiliser dans le document DDX des valeurs obtenues lors de l’exécution. Pour créer de manière dynamique un document DDX, utilisez des classes qui appartiennent au langage de programmation que vous utilisez. Par exemple, si vous développez votre application cliente à l’aide de Java, utilisez des classes qui appartiennent au `org.w3c.dom.*`package. De même, si vous utilisez Microsoft .NET, utilisez des classes qui appartiennent à l&#39; `System.Xml` espace de nommage.

Avant de pouvoir transmettre le document DDX au service Assembler, convertissez le XML d’une `org.w3c.dom.Document` instance en une `com.adobe.idp.Document` instance. Si vous utilisez des services Web, convertissez le XML du type de données utilisé pour créer le XML (par exemple, `XmlDocument`) en une `BLOB` instance.

Pour cette discussion, supposons que le document DDX suivant soit créé dynamiquement.

```xml
 <?xml version="1.0" encoding="UTF-8"?>
 <DDX xmlns="https://ns.adobe.com/DDX/1.0/">
      <PDFsFromBookmarks prefix="stmt">
     <PDF source="AssemblerResultPDF.pdf"/>
 </PDFsFromBookmarks>
 </DDX>
```

Ce document DDX désassemble un document PDF. Il est recommandé de se familiariser avec le démontage des documents PDF.

>[!NOTE]
>
>For more information about the Assembler service, see [Services Reference for AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

>[!NOTE]
>
>Pour plus d’informations sur un document DDX, voir [Service Assembler et Référence](https://www.adobe.com/go/learn_aemforms_ddx_63)DDX.

## Résumé des étapes {#summary-of-steps}

Pour désassembler un document PDF à l’aide d’un document DDX créé dynamiquement, effectuez les tâches suivantes :

1. Incluez des fichiers de projet.
1. Créez un client PDF Assembler.
1. Créez le document DDX.
1. Conversion du document DDX.
1. Définissez les options d’exécution.
1. Désassemblez le document PDF.
1. Enregistrez les documents PDF déassemblés.

**Inclure les fichiers de projet**

Incluez les fichiers nécessaires dans votre projet de développement. Si vous créez une application cliente à l’aide de Java, incluez les fichiers JAR nécessaires. Si vous utilisez des services Web, veillez à inclure les fichiers proxy.

Les fichiers JAR suivants doivent être ajoutés au chemin de classe de votre projet :

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-assembler-client.jar
* adobe-utilities.jar (requis si le AEM Forms est déployé sur JBoss)
* jbossall-client.jar (requis si le AEM Forms est déployé sur JBoss)

**Création d’un client PDF Assembler**

Avant de pouvoir exécuter une opération Assembler par programmation, vous devez créer un client de service Assembler.

**Création du document DDX**

Créez un document DDX à l’aide du langage de programmation utilisé. Pour créer un document DDX qui désassemble un document PDF, assurez-vous qu’il contient l’ `PDFsFromBookmarks` élément. Convertissez le type de données utilisé pour créer le document DDX en `com.adobe.idp.Document` instance si vous utilisez l’API Java. Si vous utilisez des services Web, convertissez le type de données en une `BLOB` instance.

**Conversion du document DDX**

Un document DDX créé à l’aide de `org.w3c.dom` classes doit être converti en `com.adobe.idp.Document` objet. Pour effectuer cette tâche lors de l’utilisation de l’API Java, utilisez les classes de transformation XML Java. Si vous utilisez des services Web, convertissez le document DDX en un `BLOB` objet.

**Référence à un document PDF à désassembler**

Pour désassembler un document PDF, référencez un fichier PDF représentant le document PDF à désassembler. Lorsqu’il est transmis au service Assembler, un document PDF distinct est renvoyé pour chaque signet de niveau 1 du document.

**Définition des options d’exécution**

Vous pouvez définir des options d’exécution qui contrôlent le comportement du service Assembler lorsqu’il effectue une tâche. Par exemple, vous pouvez définir une option qui indique au service Assembler de continuer à traiter une tâche en cas d’erreur. Pour définir les options d’exécution, vous utilisez un `AssemblerOptionSpec` objet.

**Désassembler le document PDF**

Désassemblez le document PDF en appelant l’ `invokeDDX` opération. Transmettez le document DDX créé de manière dynamique. Le service Assembler renvoie des documents PDF désassemblés dans un objet de collection.

**Enregistrer les documents PDF déassemblés**

Tous les documents PDF déassemblés sont renvoyés dans un objet de collection. Effectuez une itération dans l’objet de collection et enregistrez chaque document PDF au format PDF.

**Voir également**

[Création dynamique d’un document DDX à l’aide de l’API Java](/help/forms/developing/dynamically-creating-ddx-documents.md#dynamically-create-a-ddx-document-using-the-java-api)

[Création dynamique d’un document DDX à l’aide de l’API du service Web](/help/forms/developing/dynamically-creating-ddx-documents.md#dynamically-create-a-ddx-document-using-the-web-service-api)

[Inclusion des fichiers de bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Démontage programmatique des Documents PDF](/help/forms/developing/programmatically-disassembling-pdf-documents.md#programmatically-disassembling-pdf-documents)

## Création dynamique d’un document DDX à l’aide de l’API Java {#dynamically-create-a-ddx-document-using-the-java-api}

Créez de manière dynamique un document DDX et désassemblez un document PDF à l’aide de l’API Assembler Service (Java) :

1. Incluez des fichiers de projet.

   Incluez des fichiers JAR client, tels que adobe-assembler-client.jar, dans le chemin de classe de votre projet Java.

1. Créez un client PDF Assembler.

   * Créez un objet `ServiceClientFactory` qui contient des propriétés de connexion.
   * Create an `AssemblerServiceClient` object by using its constructor and passing the `ServiceClientFactory` object.

1. Créez le document DDX.

   * Créez un objet Java `DocumentBuilderFactory` en appelant la `DocumentBuilderFactory` méthode `newInstance` class.
   * Créez un objet Java `DocumentBuilder` en appelant la `DocumentBuilderFactory` méthode de l’ `newDocumentBuilder` objet.
   * Appelez la méthode `DocumentBuilder` de l’ `newDocument` objet pour instancier un `org.w3c.dom.Document` objet.
   * Créez l’élément racine du document DDX en appelant la `org.w3c.dom.Document` `createElement` méthode de l’objet. Cette méthode crée un `Element` objet qui représente l’élément racine. Transmettez à la `createElement` méthode une valeur de chaîne représentant le nom de l’élément. Convertissez la valeur de retour en `Element`. Ensuite, définissez une valeur pour l’élément enfant en appelant sa `setAttribute` méthode. Enfin, ajoutez l’élément à l’élément d’en-tête en appelant la `appendChild` méthode de l’élément d’en-tête et transmettez l’objet d’élément enfant en tant qu’argument. Les lignes de code suivantes présentent cette logique d’application :
      ` Element root = (Element)document.createElement("DDX");  root.setAttribute("xmlns","https://ns.adobe.com/DDX/1.0/");  document.appendChild(root);`

   * Créez l’ `PDFsFromBookmarks` élément en appelant la `Document` méthode de l’ `createElement` objet. Transmettez à la `createElement` méthode une valeur de chaîne représentant le nom de l’élément. Convertissez la valeur de retour en `Element`. Définissez une valeur pour l’ `PDFsFromBookmarks` élément en appelant sa `setAttribute` méthode. Ajoutez l’ `PDFsFromBookmarks` élément à l’ `DDX` élément en appelant la `appendChild` méthode de l’élément DDX. Transférez l’objet `PDFsFromBookmarks` d’élément en argument. Les lignes de code suivantes présentent cette logique d’application :

      ` Element PDFsFromBookmarks = (Element)document.createElement("PDFsFromBookmarks");  PDFsFromBookmarks.setAttribute("prefix","stmt");  root.appendChild(PDFsFromBookmarks);`

   * Créez un `PDF` élément en appelant la `Document` méthode de l’ `createElement` objet. Transmettez une valeur de chaîne qui représente le nom de l’élément. Convertissez la valeur de retour en `Element`. Définissez une valeur pour l’ `PDF` élément en appelant sa `setAttribute` méthode. Ajoutez l’ `PDF` élément à l’ `PDFsFromBookmarks` élément en appelant la `PDFsFromBookmarks` méthode de l’ `appendChild` élément. Transférez l’objet `PDF` d’élément en argument. Les lignes de code suivantes présentent cette logique d’application :

      ` Element PDF = (Element)document.createElement("PDF");  PDF.setAttribute("source","AssemblerResultPDF.pdf");  PDFsFromBookmarks.appendChild(PDF);`

1. Conversion du document DDX.

   * Créez un `javax.xml.transform.Transformer` objet en appelant la méthode `javax.xml.transform.Transformer` statique de l’ `newInstance` objet.
   * Créez un `Transformer` objet en appelant la `TransformerFactory` méthode de l’ `newTransformer` objet.
   * Créez un objet `ByteArrayOutputStream` en utilisant son constructeur.
   * Créez un objet `javax.xml.transform.dom.DOMSource` en utilisant son constructeur. Transmettez l’ `org.w3c.dom.Document` objet qui représente le document DDX.
   * Créez un objet `javax.xml.transform.dom.DOMSource` en utilisant son constructeur et en transmettant l’objet `ByteArrayOutputStream`. 
   * Renseignez l’ `ByteArrayOutputStream` objet Java en appelant la `javax.xml.transform.Transformer` méthode de l’ `transform` objet. Transmettez les `javax.xml.transform.dom.DOMSource` objets et les `javax.xml.transform.stream.StreamResult` objets.
   * Créez un tableau d’octets et affectez la taille de l’ `ByteArrayOutputStream` objet au tableau d’octets.
   * Renseignez le tableau d’octets en appelant la `ByteArrayOutputStream` `toByteArray` méthode de l’objet.
   * Create a `com.adobe.idp.Document` object by using its constructor and passing the byte array.

1. Référencez un document PDF à désassembler.

   * Créez un `java.util.Map` objet utilisé pour stocker des documents PDF d’entrée à l’aide d’un `HashMap` constructeur.
   * Créez un `java.io.FileInputStream` objet en utilisant son constructeur et en transmettant l’emplacement du document PDF à désassembler.
   * Create a `com.adobe.idp.Document` object. Transmettez l’ `java.io.FileInputStream` objet contenant le document PDF à désassembler.
   * Ajoutez une entrée à l’ `java.util.Map` objet en invoquant sa `put` méthode et en transmettant les arguments suivants :

      * Valeur de chaîne qui représente le nom de la clé. Cette valeur doit correspondre à la valeur de l’élément source PDF spécifié dans le document DDX. (Dans le document DDX créé dynamiquement, la valeur est `AssemblerResultPDF.pdf`.)
      * Objet `com.adobe.idp.Document` contenant le document PDF à désassembler.

1. Définissez les options d’exécution.

   * Créez un `AssemblerOptionSpec` objet qui stocke les options d’exécution à l’aide de son constructeur.
   * Définissez des options d’exécution pour répondre aux besoins de votre entreprise en appelant une méthode qui appartient à l’ `AssemblerOptionSpec` objet. Par exemple, pour demander au service Assembler de continuer à traiter une tâche en cas d’erreur, appelez la `AssemblerOptionSpec` méthode de l’ `setFailOnError` objet et passez `false`.

1. Désassemblez le document PDF.

   Appelez la méthode `AssemblerServiceClient` de l’ `invokeDDX` objet et transmettez les valeurs suivantes :

   * Objet `com.adobe.idp.Document` représentant le document DDX créé de manière dynamique
   * Objet `java.util.Map` contenant le document PDF à désassembler
   * Objet `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` spécifiant les options d’exécution, y compris la police par défaut et le niveau du journal des tâches

   La `invokeDDX` méthode renvoie un `com.adobe.livecycle.assembler.client.AssemblerResult` objet contenant les documents PDF désassemblés et les exceptions survenues.

1. Enregistrez les documents PDF déassemblés.

   Pour obtenir les documents PDF déassemblés, effectuez les actions suivantes :

   * Appelle la méthode `AssemblerResult` de l’ `getDocuments` objet. Cette méthode renvoie un `java.util.Map` objet.
   * Effectuez une itération sur l’ `java.util.Map` objet jusqu’à ce que vous trouviez l’ `com.adobe.idp.Document` objet obtenu.
   * Appelez la méthode `com.adobe.idp.Document` de l’objet `copyToFile` pour extraire le document PDF.

**Voir également**

[Début rapide (mode SOAP) : Création dynamique d’un document DDX à l’aide de l’API Java](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-dynamically-creating-a-ddx-document-using-the-java-api)

[Inclusion des fichiers de bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Création dynamique d’un document DDX à l’aide de l’API du service Web {#dynamically-create-a-ddx-document-using-the-web-service-api}

Créez de manière dynamique un document DDX et désassemblez un document PDF à l’aide de l’API Assembler Service (service Web) :

1. Incluez des fichiers de projet.

   Créez un projet Microsoft .NET qui utilise MTOM. Assurez-vous d’utiliser la définition WSDL suivante lors de la définition d’une référence de service : `http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Remplacez `localhost` par l’adresse IP du serveur hébergeant les AEM Forms.

1. Créez un client PDF Assembler.

   * Créez un `AssemblerServiceClient` objet en utilisant son constructeur par défaut.
   * Créez un `AssemblerServiceClient.Endpoint.Address` objet en utilisant le `System.ServiceModel.EndpointAddress` constructeur. Transmettez une valeur de chaîne qui spécifie le WSDL au service AEM Forms (par exemple, `http://localhost:8080/soap/services/AssemblerService?blob=mtom`). Vous n’avez pas besoin d’utiliser l’ `lc_version` attribut. Cet attribut est utilisé lorsque vous créez une référence de service.
   * Créez un `System.ServiceModel.BasicHttpBinding` objet en obtenant la valeur du `AssemblerServiceClient.Endpoint.Binding` champ. Convertissez la valeur de retour en `BasicHttpBinding`.
   * Définissez le `System.ServiceModel.BasicHttpBinding` champ de l’ `MessageEncoding` objet sur `WSMessageEncoding.Mtom`. Cette valeur garantit l’utilisation de MTOM.
   * Activez l’authentification HTTP de base en exécutant les tâches suivantes :

      * Attribuez le nom d’utilisateur AEM forms au champ `AssemblerServiceClient.ClientCredentials.UserName.UserName`.
      * Attribuez la valeur de mot de passe correspondante au champ `AssemblerServiceClient.ClientCredentials.UserName.Password`.
      * Attribuez la valeur constante `HttpClientCredentialType.Basic` au champ `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Attribuez la valeur constante `BasicHttpSecurityMode.TransportCredentialOnly` au champ `BasicHttpBindingSecurity.Security.Mode`.

1. Créez le document DDX.

   * Créez un objet `System.Xml.XmlElement` en utilisant son constructeur.
   * Créez l’élément racine du document DDX en appelant la `XmlElement` `CreateElement` méthode de l’objet. Cette méthode crée un `Element` objet qui représente l’élément racine. Transmettez à la `CreateElement` méthode une valeur de chaîne représentant le nom de l’élément. Définissez une valeur pour l’élément DDX en appelant sa `SetAttribute` méthode. Enfin, ajoutez l’élément au document DDX en appelant la méthode `XmlElement` de l’ `AppendChild` objet. Transférez l’objet DDX en argument. Les lignes de code suivantes présentent cette logique d’application :

      ` System.Xml.XmlElement root = ddx.CreateElement("DDX");  root.SetAttribute("xmlns", "https://ns.adobe.com/DDX/1.0/");  ddx.AppendChild(root);`

   * Créez l’ `PDFsFromBookmarks` élément du document DDX en appelant la `XmlElement` méthode de l’ `CreateElement` objet. Transmettez à la `CreateElement` méthode une valeur de chaîne représentant le nom de l’élément. Ensuite, définissez une valeur pour l’élément en appelant sa `SetAttribute` méthode. Ajoutez l’ `PDFsFromBookmarks` élément à l’élément racine en appelant la `DDX` méthode de l’ `AppendChild` élément. Transférez l’objet `PDFsFromBookmarks` d’élément en argument. Les lignes de code suivantes présentent cette logique d’application :

      ` XmlElement PDFsFromBookmarks = ddx.CreateElement("PDFsFromBookmarks");  PDFsFromBookmarks.SetAttribute("prefix", "stmt");  root.AppendChild(PDFsFromBookmarks);`

   * Créez l’ `PDF` élément du document DDX en appelant la `XmlElement` méthode de l’ `CreateElement` objet. Transmettez à la `CreateElement` méthode une valeur de chaîne représentant le nom de l’élément. Ensuite, définissez une valeur pour l’élément enfant en appelant sa `SetAttribute` méthode. Ajoutez l’ `PDF` élément à l’ `PDFsFromBookmarks` élément en appelant la `PDFsFromBookmarks` méthode de l’ `AppendChild` élément. Transférez l’objet `PDF` d’élément en argument. Les lignes de code suivantes présentent cette logique d’application :

      ` XmlElement PDF = ddx.CreateElement("PDF");  PDF.SetAttribute("source", "AssemblerResultPDF.pdf");  PDFsFromBookmarks.AppendChild(PDF);`

1. Conversion du document DDX.

   * Créez un objet `System.IO.MemoryStream` en utilisant son constructeur.
   * Renseignez l’ `MemoryStream` objet avec le document DDX en utilisant l’ `XmlElement` objet qui représente le document DDX. Invoke the `XmlElement` object’s `Save` method and pass the `MemoryStream` object.
   * Créez un tableau d’octets et remplissez-le avec les données situées dans l’ `MemoryStream` objet. Le code suivant affiche cette logique d’application :

      ` int bufLen = Convert.ToInt32(stream.Length);  byte[] byteArray = new byte[bufLen];  stream.Position = 0;  int count = stream.Read(byteArray, 0, bufLen);`

   * Create a `BLOB` object. Affectez le tableau d’octets au `BLOB` `MTOM` champ de l’objet.

1. Référencez un document PDF à désassembler.

   * Créez un objet `BLOB` en utilisant son constructeur. L’ `BLOB` objet est utilisé pour stocker le document PDF d’entrée. Cet `BLOB` objet est transmis à l’ `invokeOneDocument` objet en tant qu’argument.
   * Create a `System.IO.FileStream` object by invoking its constructor. Transmettez une valeur de chaîne qui représente l’emplacement du fichier du document PDF d’entrée et le mode d’ouverture du fichier.
   * Créez un tableau d’octets qui stocke le contenu de l’ `System.IO.FileStream` objet. Vous pouvez déterminer la taille du tableau d’octets en obtenant la `System.IO.FileStream` `Length` propriété de l’objet.
   * Renseignez le tableau d’octets avec les données de flux en appelant la `System.IO.FileStream` `Read` méthode de l’objet et en transmettant le tableau d’octets, la position de départ et la longueur du flux à lire.
   * Renseignez l’ `BLOB` objet en attribuant sa `MTOM` propriété au contenu du tableau d’octets.

1. Définissez les options d’exécution.

   * Créez un `AssemblerOptionSpec` objet qui stocke les options d’exécution à l’aide de son constructeur.
   * Définissez des options d’exécution pour répondre aux besoins de votre entreprise en attribuant une valeur à un membre de données qui appartient à l’ `AssemblerOptionSpec` objet. Par exemple, pour demander au service Assembler de poursuivre le traitement d’une tâche en cas d’erreur, affectez-lui `false` le membre `AssemblerOptionSpec` de données de l’ `failOnError` objet.

1. Désassemblez le document PDF.

   Appelez la méthode `AssemblerServiceClient` de l’ `invokeDDX` objet et transmettez les valeurs suivantes :

   * Objet `BLOB` représentant le document DDX créé de manière dynamique
   * Tableau `mapItem` contenant le document PDF d’entrée
   * Objet `AssemblerOptionSpec` spécifiant les options d’exécution

   La `invokeDDX` méthode renvoie un `AssemblerResult` objet qui contient les résultats de la tâche et les exceptions survenues.

1. Enregistrez les documents PDF déassemblés.

   Pour obtenir les documents PDF nouvellement créés, effectuez les opérations suivantes :

   * Accédez au `AssemblerResult` champ de l’ `documents` objet, qui est un `Map` objet contenant les documents PDF déassemblés.
   * Effectuez une itération sur l’ `Map` objet pour obtenir chaque document résultant. Ensuite, déposez les éléments `value` de ce membre de la baie sur un `BLOB`.
   * Extrayez les données binaires qui représentent le document PDF en accédant à la `BLOB` propriété de l’objet `MTOM` en question. Cette opération renvoie un tableau d’octets que vous pouvez écrire dans un fichier PDF.

**Voir également**

[Appel de AEM Forms à l’aide de MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Appel de AEM Forms à l’aide de SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)
