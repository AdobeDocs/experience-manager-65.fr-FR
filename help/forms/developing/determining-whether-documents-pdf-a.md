---
title: Détermination de la compatibilité des Documents avec la norme PDF/A
seo-title: Détermination de la compatibilité des Documents avec la norme PDF/A
description: 'null'
seo-description: 'null'
uuid: 4e9d8c8f-2153-411b-9c4b-2d14b3c8f4bb
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: c429d6e1-7847-43c8-bf75-cb0078dbb9d5
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '2069'
ht-degree: 5%

---


# Determining Whether Documents Are PDF/A-Compliant {#determining-whether-documents-are-pdf-a-compliant}

Vous pouvez déterminer si un document PDF est compatible PDF/A à l’aide du service Assembler. Un document PDF/A existe comme format d’archivage destiné à la conservation à long terme du contenu du document. Les polices sont incorporées dans le document et le fichier est décompressé. Par conséquent, un document PDF/A est généralement plus volumineux qu’un document PDF standard. De plus, un document PDF/A ne contient aucune donnée audio et vidéo.

La spécification PDF/A-1 comprend deux niveaux de conformité, à savoir A et B. La principale différence entre les deux niveaux est la prise en charge de la structure logique (accessibilité), qui n’est pas requise pour le niveau de conformité B. Quel que soit le niveau de conformité, PDF/A-1 exige que toutes les polices soient incorporées dans le document PDF/A généré. Actuellement, seul le format PDF/A-1b est pris en charge dans la validation (et la conversion).

Aux fins de cette discussion, supposons que le document DDX suivant soit utilisé.

```xml
 <?xml version="1.0" encoding="UTF-8"?>
 <DDX xmlns="https://ns.adobe.com/DDX/1.0/">
         <DocumentInformation source="Loan.pdf" result="Loan_result.xml">
         <PDFAValidation compliance="PDF/A-1b" resultLevel="Detailed"                       ignoreUnusedResources="true" allowCertificationSignatures="true" />
     </DocumentInformation>
 </DDX>
```

Dans ce document DDX, l’ `DocumentInformation` élément demande au service Assembler de renvoyer des informations sur le document PDF d’entrée. Dans l’ `DocumentInformation` élément, l’ `PDFAValidation` élément demande au service Assembler d’indiquer si le document PDF d’entrée est compatible PDF/A.

Le service Assembler renvoie des informations indiquant si le document PDF d’entrée est compatible PDF/A dans un document XML contenant un `PDFAConformance` élément. Si le document PDF d’entrée est compatible PDF/A, la valeur de l’ `PDFAConformance` attribut de l’ `isCompliant` élément est `true`. Si le document PDF n’est pas compatible avec la norme PDF/A, la valeur de l’ `PDFAConformance` attribut de l’ `isCompliant` élément est `false`.

>[!NOTE]
>
>Comme le document DDX spécifié dans cette section contient un `DocumentInformation` élément, le service Assembler renvoie des données XML au lieu d’un document PDF. En d’autres termes, le service Assembler n’assemble ni ne désassemble un document PDF ; elle renvoie des informations sur le document PDF d’entrée dans un document XML.

>[!NOTE]
>
>For more information about the Assembler service, see [Services Reference for AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

>[!NOTE]
>
>Pour plus d’informations sur un document DDX, voir [Service Assembler et Référence](https://www.adobe.com/go/learn_aemforms_ddx_63)DDX.

## Résumé des étapes {#summary-of-steps}

Pour déterminer si un document PDF est compatible PDF/A, effectuez les tâches suivantes :

1. Incluez des fichiers de projet.
1. Créez un client PDF Assembler.
1. Référencez un document DDX existant.
1. Référencez un document PDF utilisé pour déterminer la conformité à la norme PDF/A.
1. Définissez les options d’exécution.
1. Récupérez des informations sur le document PDF.
1. Enregistrez le document XML renvoyé.

**Inclure les fichiers de projet**

Incluez les fichiers nécessaires dans votre projet de développement. Si vous créez une application cliente à l’aide de Java, incluez les fichiers JAR nécessaires. Si vous utilisez des services Web, veillez à inclure les fichiers proxy.

Les fichiers JAR suivants doivent être ajoutés au chemin de classe de votre projet :

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-assembler-client.jar
* adobe-utilities.jar (requis si le AEM Forms est déployé sur JBoss)
* jbossall-client.jar (requis si le AEM Forms est déployé sur JBoss)

si le AEM Forms est déployé sur un serveur d’applications J2EE pris en charge autre que JBoss, vous devez remplacer les fichiers adobe-utilities.jar et jbossall-client.jar par des fichiers JAR spécifiques au serveur d’applications J2EE sur lequel le AEM Forms est déployé. For information about the location of all AEM Forms JAR files, see [Including AEM Forms Java library files](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Création d’un client PDF Assembler**

Avant de pouvoir exécuter une opération Assembler par programmation, vous devez créer un client de service Assembler.

**Référencer un document DDX existant**

Un document DDX doit être référencé pour effectuer une opération de service Assembler. Pour déterminer si un document PDF d’entrée est compatible PDF/A, assurez-vous que le document DDX contient l’ `PDFAValidation` élément dans un `DocumentInformation` élément. L’ `PDFAValidation` élément demande au service Assembler de renvoyer un document XML qui indique si le document PDF d’entrée est compatible PDF/A.

**Référence à un document PDF utilisé pour déterminer la conformité à la norme PDF/A**

Un document PDF doit être référencé et transmis au service Assembler pour déterminer si le document PDF est compatible PDF/A.

**Définition des options d’exécution**

Vous pouvez définir des options d’exécution qui contrôlent le comportement du service Assembler lorsqu’il effectue une tâche. Par exemple, vous pouvez définir une option qui indique au service Assembler de continuer à traiter une tâche en cas d’erreur. Pour plus d’informations sur les options d’exécution que vous pouvez définir, voir la référence de `AssemblerOptionSpec` classe dans Référence [API](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)AEM Forms.

**Récupération d’informations sur le document PDF**

Après avoir créé le client de service Assembler, référencé le document DDX, référencé un document PDF interactif et défini les options d’exécution, vous pouvez appeler l’ `invokeDDX` opération. Le document DDX contenant l’ `DocumentInformation` élément, le service Assembler renvoie des données XML au lieu d’un document PDF.

**Enregistrer le document XML renvoyé**

Le document XML renvoyé par le service Assembler indique si le document PDF d’entrée est compatible PDF/A. Par exemple, si le document PDF d’entrée n’est pas compatible PDF/A, le service Assembler renvoie un document XML contenant l’élément suivant :

```xml
 <PDFAConformance isCompliant="false" compliance="PDF/A-1b" resultLevel="Detailed" ignoreUnusedResources="true" allowCertificationSignatures="true">
```

Enregistrez le document XML en tant que fichier XML afin que vous puissiez ouvrir le fichier et vue les résultats.

**Voir également**

[Déterminez si un document est compatible PDF/A à l’aide de l’API Java.](/help/forms/developing/determining-whether-documents-pdf-a.md#determine-whether-a-document-is-pdf-a-compliant-using-the-java-api)

[Déterminer si un document est compatible PDF/A à l’aide de l’API du service Web](/help/forms/developing/determining-whether-documents-pdf-a.md#determine-whether-a-document-is-pdf-a-compliant-using-the-web-service-api)

[Inclusion des fichiers de bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Assemblage par programmation de Documents PDF](/help/forms/developing/programmatically-assembling-pdf-documents.md)

## Déterminez si un document est compatible PDF/A à l’aide de l’API Java. {#determine-whether-a-document-is-pdf-a-compliant-using-the-java-api}

Déterminez si un document PDF est compatible PDF/A à l’aide de l’API Assembler Service (Java) :

1. Incluez des fichiers de projet.

   Incluez des fichiers JAR client, tels que adobe-assembler-client.jar, dans le chemin de classe de votre projet Java.

1. Créez un client PDF Assembler.

   * Créez un objet `ServiceClientFactory` qui contient des propriétés de connexion.
   * Create an `AssemblerServiceClient` object by using its constructor and passing the `ServiceClientFactory` object.

1. Référencez un document DDX existant.

   * Créez un `java.io.FileInputStream` objet qui représente le document DDX en utilisant son constructeur et en transmettant une valeur de chaîne qui spécifie l’emplacement du fichier DDX. Pour déterminer si le document PDF est compatible PDF/A, assurez-vous que le document DDX contient l’ `PDFAValidation` élément contenu dans un `DocumentInformation` élément.
   * Créez un objet `com.adobe.idp.Document` en utilisant son constructeur et en transmettant l’objet `java.io.FileInputStream`. 

1. Référencez un document PDF utilisé pour déterminer la conformité à la norme PDF/A.

   * Créez un `java.io.FileInputStream` objet en utilisant son constructeur et en transmettant l’emplacement d’un document PDF utilisé pour déterminer la conformité à la norme PDF/A.
   * Créez un `com.adobe.idp.Document` objet en utilisant son constructeur et en transmettant l’ `java.io.FileInputStream` objet qui contient le document PDF.
   * Créez un `java.util.Map` objet utilisé pour stocker le document PDF d’entrée à l’aide d’un `HashMap` constructeur.
   * Ajoutez une entrée à l’ `java.util.Map` objet en invoquant sa `put` méthode et en transmettant les arguments suivants :

      * Valeur de chaîne qui représente le nom de la clé. Cette valeur doit correspondre à la valeur de l’élément source spécifié dans le document DDX. Par exemple, la valeur de l’élément source situé dans le document DDX introduit dans cette section est Loan.pdf.
      * Objet `com.adobe.idp.Document` contenant le document PDF d’entrée.

1. Définissez les options d’exécution.

   * Créez un `AssemblerOptionSpec` objet qui stocke les options d’exécution à l’aide de son constructeur.
   * Définissez des options d’exécution pour répondre aux besoins de votre entreprise en appelant une méthode qui appartient à l’ `AssemblerOptionSpec` objet. Par exemple, pour demander au service Assembler de continuer à traiter une tâche en cas d’erreur, appelez la `AssemblerOptionSpec` méthode de l’ `setFailOnError` objet et passez `false`.

1. Récupérez des informations sur le document PDF.

   Appelez la méthode `AssemblerServiceClient` de l’ `invokeDDX` objet et transmettez les valeurs requises suivantes :

   * Objet `com.adobe.idp.Document` représentant le document DDX à utiliser
   * Objet `java.util.Map` contenant le fichier PDF d’entrée utilisé pour déterminer la conformité à la norme PDF/A
   * A `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` object that specifies the run-time options

   La `invokeDDX` méthode renvoie un `com.adobe.livecycle.assembler.client.AssemblerResult` objet contenant des données XML qui indique si le document PDF d’entrée est compatible PDF/A.

1. Enregistrez le document XML renvoyé.

   Pour obtenir des données XML spécifiant si le document PDF d’entrée est un document PDF/A, effectuez les actions suivantes :

   * Appelle la méthode `AssemblerResult` de l’ `getDocuments` objet. Cette méthode renvoie un `java.util.Map` objet.
   * Effectuez une itération sur l’ `java.util.Map` objet jusqu’à ce que vous trouviez l’ `com.adobe.idp.Document` objet obtenu.
   * Appelez la méthode `com.adobe.idp.Document` de l’objet `copyToFile` pour extraire le document XML. Assurez-vous d’enregistrer les données XML dans un fichier XML.

**Voir également**

[Début rapide (mode SOAP) : Détermination de la conformité d’un document à la norme PDF/A à l’aide de l’API](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-determining-whether-a-document-is-pdf-a-compliant-using-the-java-api) Java (mode SOAP)

[Inclusion des fichiers de bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Déterminer si un document est compatible PDF/A à l’aide de l’API du service Web {#determine-whether-a-document-is-pdf-a-compliant-using-the-web-service-api}

Déterminez si un document PDF est compatible PDF/A à l’aide de l’API Assembler Service (service Web) :

1. Incluez des fichiers de projet.

   Créez un projet Microsoft .NET qui utilise MTOM. Assurez-vous d’utiliser la définition WSDL suivante : `http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Remplacez `localhost` par l’adresse IP du serveur hébergeant les AEM Forms.

1. Créez un client PDF Assembler.

   * Créez un `AssemblerServiceClient` objet en utilisant son constructeur par défaut.
   * Créez un `AssemblerServiceClient.Endpoint.Address` objet en utilisant le `System.ServiceModel.EndpointAddress` constructeur. Transmettez une valeur de chaîne qui spécifie le WSDL au service AEM Forms (par exemple, `http://localhost:8080/soap/services/AssemblerService?blob=mtom`). Vous n’avez pas besoin d’utiliser l’ `lc_version` attribut. Cet attribut est utilisé lorsque vous créez une référence de service.)
   * Créez un `System.ServiceModel.BasicHttpBinding` objet en obtenant la valeur du `AssemblerServiceClient.Endpoint.Binding` champ. Convertissez la valeur de retour en `BasicHttpBinding`.
   * Définissez le `System.ServiceModel.BasicHttpBinding` champ de l’ `MessageEncoding` objet sur `WSMessageEncoding.Mtom`. Cette valeur garantit l’utilisation de MTOM.
   * Activez l’authentification HTTP de base en exécutant les tâches suivantes :

      * Attribuez le nom d’utilisateur AEM forms au champ `AssemblerServiceClient.ClientCredentials.UserName.UserName`.
      * Attribuez la valeur de mot de passe correspondante au champ `AssemblerServiceClient.ClientCredentials.UserName.Password`.
      * Attribuez la valeur constante `HttpClientCredentialType.Basic` au champ `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Attribuez la valeur constante `BasicHttpSecurityMode.TransportCredentialOnly` au champ `BasicHttpBindingSecurity.Security.Mode`.

1. Référencez un document DDX existant.

   * Créez un objet `BLOB` en utilisant son constructeur. L’ `BLOB` objet est utilisé pour stocker le document DDX.
   * Créez un `System.IO.FileStream` objet en appelant son constructeur et en transmettant une valeur de chaîne qui représente l’emplacement du fichier du document DDX et le mode d’ouverture du fichier.
   * Créez un tableau d’octets qui stocke le contenu de l’ `System.IO.FileStream` objet. Vous pouvez déterminer la taille du tableau d’octets en obtenant la `System.IO.FileStream` `Length` propriété de l’objet.
   * Renseignez le tableau d’octets avec les données de flux en appelant la `System.IO.FileStream` `Read` méthode de l’objet et en transmettant le tableau d’octets, la position de départ et la longueur du flux à lire.
   * Renseignez l’ `BLOB` objet en affectant son `MTOM` champ au contenu du tableau d’octets.

1. Référencez un document PDF utilisé pour déterminer la conformité à la norme PDF/A.

   * Créez un objet `BLOB` en utilisant son constructeur. L’ `BLOB` objet est utilisé pour stocker le document PDF d’entrée.
   * Créez un `System.IO.FileStream` objet en appelant son constructeur et en transmettant une valeur de chaîne qui représente l’emplacement du fichier du document PDF d’entrée et le mode d’ouverture du fichier.
   * Créez un tableau d’octets qui stocke le contenu de l’ `System.IO.FileStream` objet. Vous pouvez déterminer la taille du tableau d’octets en obtenant la `System.IO.FileStream` `Length` propriété de l’objet.
   * Renseignez le tableau d’octets avec les données de flux en appelant la `System.IO.FileStream` `Read` méthode de l’objet et en transmettant le tableau d’octets, la position de départ et la longueur du flux à lire.
   * Renseignez l’ `BLOB` objet en attribuant sa `MTOM` propriété au contenu du tableau d’octets.
   * Create a `MyMapOf_xsd_string_To_xsd_anyType` object. Cet objet de collection est utilisé pour stocker le document PDF.
   * Create a `MyMapOf_xsd_string_To_xsd_anyType_Item` object.
   * Attribuez une valeur de chaîne qui représente le nom de clé au `MyMapOf_xsd_string_To_xsd_anyType_Item` `key` champ de l’objet. Cette valeur doit correspondre à la valeur de l’élément source PDF spécifié dans le document DDX.
   * Affectez l’ `BLOB` objet qui stocke le document PDF au `MyMapOf_xsd_string_To_xsd_anyType_Item` `value` champ de l’objet.
   * Ajoutez l’ `MyMapOf_xsd_string_To_xsd_anyType_Item` objet sur l’ `MyMapOf_xsd_string_To_xsd_anyType` objet. Appelez la `MyMapOf_xsd_string_To_xsd_anyType` méthode de l’ `Add` objet et transmettez l’ `MyMapOf_xsd_string_To_xsd_anyType` objet.

1. Définissez les options d’exécution.

   * Créez un `AssemblerOptionSpec` objet qui stocke les options d’exécution à l’aide de son constructeur.
   * Définissez des options d’exécution pour répondre aux besoins de votre entreprise en attribuant une valeur à un membre de données qui appartient à l’ `AssemblerOptionSpec` objet. Par exemple, pour demander au service Assembler de poursuivre le traitement d’une tâche en cas d’erreur, affectez-lui `false` le membre `AssemblerOptionSpec` de données de l’ `failOnError` objet.

1. Récupérez des informations sur le document PDF.

   Appelez la méthode `AssemblerServiceService` de l’ `invoke` objet et transmettez les valeurs suivantes :

   * Objet `BLOB` représentant le document DDX.
   * Objet `MyMapOf_xsd_string_To_xsd_anyType` contenant le document PDF d’entrée. Ses clés doivent correspondre aux noms des fichiers source PDF et ses valeurs doivent correspondre à l’objet `BLOB` correspondant au fichier PDF d’entrée.
   * Objet `AssemblerOptionSpec` spécifiant les options d’exécution.

   La `invoke` méthode renvoie un `AssemblerResult` objet qui contient des données XML spécifiant si le document PDF d’entrée est un document PDF/A.

1. Enregistrez le document XML renvoyé.

   Pour obtenir des données XML spécifiant si le document PDF d’entrée est un document PDF/A, effectuez les actions suivantes :

   * Accédez au `AssemblerResult` champ de l’ `documents` objet, qui est un `Map` objet qui contient les données XML spécifiant si le document PDF d’entrée est un document PDF/A.
   * Effectuez une itération sur l’ `Map` objet pour obtenir chaque document résultant. Ensuite, définissez la valeur du membre de la baie sur une `BLOB`valeur.
   * Extrayez les données binaires qui représentent les données XML en accédant au `BLOB` `MTOM` champ de son objet. Ce champ stocke un tableau d’octets que vous pouvez écrire dans un fichier XML.

**Voir également**

[Appel de AEM Forms à l’aide de MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
