---
title: Détermination de la compatibilité des Documents avec la norme PDF/A
seo-title: Détermination de la compatibilité des Documents avec la norme PDF/A
description: Utilisez le service Assembler pour déterminer si un document PDF est compatible PDF/A à l’aide de l’API Java et de l’API de service Web.
seo-description: Utilisez le service Assembler pour déterminer si un document PDF est compatible PDF/A à l’aide de l’API Java et de l’API de service Web.
uuid: 4e9d8c8f-2153-411b-9c4b-2d14b3c8f4bb
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: c429d6e1-7847-43c8-bf75-cb0078dbb9d5
role: Développeur
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '2110'
ht-degree: 4%

---


# Détermination de la compatibilité des Documents avec la norme PDF/A {#determining-whether-documents-are-pdf-a-compliant}

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

Dans ce document DDX, l’élément `DocumentInformation` demande au service Assembler de renvoyer des informations sur le document PDF d’entrée. Dans l’élément `DocumentInformation`, l’élément `PDFAValidation` demande au service Assembler d’indiquer si le document PDF d’entrée est compatible PDF/A.

Le service Assembler renvoie des informations indiquant si le document PDF d’entrée est compatible PDF/A dans un document XML contenant un élément `PDFAConformance`. Si le document PDF d’entrée est compatible PDF/A, la valeur de l’attribut `isCompliant` de l’élément `PDFAConformance` est `true`. Si le document PDF n’est pas compatible avec PDF/A, la valeur de l’attribut `isCompliant` de l’élément `PDFAConformance` est `false`.

>[!NOTE]
>
>Comme le document DDX spécifié dans cette section contient un élément `DocumentInformation`, le service Assembler renvoie des données XML au lieu d’un document PDF. En d’autres termes, le service Assembler n’assemble ni ne désassemble un document PDF ; elle renvoie des informations sur le document PDF d’entrée dans un document XML.

>[!NOTE]
>
>Pour plus d’informations sur le service Assembler, voir [Guide de référence des services pour AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

>[!NOTE]
>
>Pour plus d’informations sur un document DDX, voir [Service Assembler et Référence DDX](https://www.adobe.com/go/learn_aemforms_ddx_63).

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
* adobe-utilities.jar (requis si AEM Forms est déployé sur JBoss)
* jbossall-client.jar (requis si AEM Forms est déployé sur JBoss)

si AEM Forms est déployé sur un serveur d’applications J2EE pris en charge autre que JBoss, vous devez remplacer les fichiers adobe-utilities.jar et jbossall-client.jar par des fichiers JAR spécifiques au serveur d’applications J2EE sur lequel AEM Forms est déployé. Pour plus d’informations sur l’emplacement de tous les fichiers JAR AEM Forms, voir [Inclusion de fichiers de bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Création d’un client PDF Assembler**

Avant de pouvoir exécuter une opération Assembler par programmation, vous devez créer un client de service Assembler.

**Référencer un document DDX existant**

Un document DDX doit être référencé pour effectuer une opération de service Assembler. Pour déterminer si un document PDF d’entrée est compatible PDF/A, assurez-vous que le document DDX contient l’élément `PDFAValidation` dans un élément `DocumentInformation`. L’élément `PDFAValidation` indique au service Assembler de renvoyer un document XML qui indique si le document PDF d’entrée est compatible PDF/A.

**Référence à un document PDF utilisé pour déterminer la conformité à la norme PDF/A**

Un document PDF doit être référencé et transmis au service Assembler pour déterminer si le document PDF est compatible PDF/A.

**Définition des options d’exécution**

Vous pouvez définir des options d’exécution qui contrôlent le comportement du service Assembler lorsqu’il effectue une tâche. Par exemple, vous pouvez définir une option qui indique au service Assembler de continuer à traiter une tâche en cas d’erreur. Pour plus d&#39;informations sur les options d&#39;exécution que vous pouvez définir, consultez la référence de classe `AssemblerOptionSpec` dans [AEM Forms API Reference](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

**Récupération d’informations sur le document PDF**

Après avoir créé le client de service Assembler, référencé le document DDX, référencé un document PDF interactif et défini les options d’exécution, vous pouvez appeler l’opération `invokeDDX`. Le document DDX contenant l’élément `DocumentInformation`, le service Assembler renvoie des données XML au lieu d’un document PDF.

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

## Déterminez si un document est compatible PDF/A à l’aide de l’API Java {#determine-whether-a-document-is-pdf-a-compliant-using-the-java-api}.

Déterminez si un document PDF est compatible PDF/A à l’aide de l’API Assembler Service (Java) :

1. Incluez des fichiers de projet.

   Incluez des fichiers JAR client, tels que adobe-assembler-client.jar, dans le chemin de classe de votre projet Java.

1. Créez un client PDF Assembler.

   * Créez un objet `ServiceClientFactory` qui contient des propriétés de connexion.
   * Créez un objet `AssemblerServiceClient` en utilisant son constructeur et en transmettant l&#39;objet `ServiceClientFactory`.

1. Référencez un document DDX existant.

   * Créez un objet `java.io.FileInputStream` qui représente le document DDX en utilisant son constructeur et en transmettant une valeur de chaîne qui spécifie l’emplacement du fichier DDX. Pour déterminer si le document PDF est compatible PDF/A, assurez-vous que le document DDX contient l’élément `PDFAValidation` contenu dans un élément `DocumentInformation`.
   * Créez un objet `com.adobe.idp.Document` en utilisant son constructeur et en transmettant l’objet `java.io.FileInputStream`. 

1. Référencez un document PDF utilisé pour déterminer la conformité à la norme PDF/A.

   * Créez un objet `java.io.FileInputStream` en utilisant son constructeur et en transmettant l’emplacement d’un document PDF utilisé pour déterminer la conformité à la norme PDF/A.
   * Créez un objet `com.adobe.idp.Document` en utilisant son constructeur et en transmettant l’objet `java.io.FileInputStream` contenant le document PDF.
   * Créez un objet `java.util.Map` utilisé pour stocker le document PDF d’entrée à l’aide d’un constructeur `HashMap`.
   * Ajoutez une entrée à l&#39;objet `java.util.Map` en invoquant sa méthode `put` et en transmettant les arguments suivants :

      * Valeur de chaîne qui représente le nom de la clé. Cette valeur doit correspondre à la valeur de l’élément source spécifié dans le document DDX. Par exemple, la valeur de l’élément source situé dans le document DDX introduit dans cette section est Loan.pdf.
      * Objet `com.adobe.idp.Document` contenant le document PDF d’entrée.

1. Définissez les options d’exécution.

   * Créez un objet `AssemblerOptionSpec` qui stocke les options d’exécution à l’aide de son constructeur.
   * Définissez des options d&#39;exécution pour répondre aux besoins de votre entreprise en appelant une méthode appartenant à l&#39;objet `AssemblerOptionSpec`. Par exemple, pour demander au service Assembler de continuer à traiter une tâche en cas d’erreur, appelez la méthode `AssemblerOptionSpec` de l’objet `setFailOnError` et transmettez `false`.

1. Récupérez des informations sur le document PDF.

   Appelez la méthode `invokeDDX` de l’objet `AssemblerServiceClient` et transmettez les valeurs requises suivantes :

   * Objet `com.adobe.idp.Document` représentant le document DDX à utiliser
   * Objet `java.util.Map` contenant le fichier PDF d’entrée utilisé pour déterminer la conformité à la norme PDF/A
   * Objet `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` qui spécifie les options d’exécution

   La méthode `invokeDDX` renvoie un objet `com.adobe.livecycle.assembler.client.AssemblerResult` contenant des données XML qui indique si le document PDF d’entrée est compatible PDF/A.

1. Enregistrez le document XML renvoyé.

   Pour obtenir des données XML spécifiant si le document PDF d’entrée est un document PDF/A, effectuez les actions suivantes :

   * Appelez la méthode `AssemblerResult` de l’objet `getDocuments`. Cette opération renvoie un objet `java.util.Map`.
   * Effectuez une itération dans l&#39;objet `java.util.Map` jusqu&#39;à ce que vous trouviez l&#39;objet `com.adobe.idp.Document` obtenu.
   * Appelez la méthode `com.adobe.idp.Document` de l’objet `copyToFile` pour extraire le document XML. Assurez-vous d’enregistrer les données XML dans un fichier XML.

**Voir également**

[Début rapide (mode SOAP) : Détermination de la conformité d’un document à la norme PDF/A à l’aide de l’API](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-determining-whether-a-document-is-pdf-a-compliant-using-the-java-api)  Java (mode SOAP)

[Inclusion des fichiers de bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Déterminez si un document est compatible PDF/A à l’aide de l’API de service Web {#determine-whether-a-document-is-pdf-a-compliant-using-the-web-service-api}.

Déterminez si un document PDF est compatible PDF/A à l’aide de l’API Assembler Service (service Web) :

1. Incluez des fichiers de projet.

   Créez un projet Microsoft .NET qui utilise MTOM. Assurez-vous d’utiliser la définition WSDL suivante : `http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Remplacez `localhost` par l’adresse IP du serveur hébergeant AEM Forms.

1. Créez un client PDF Assembler.

   * Créez un objet `AssemblerServiceClient` en utilisant son constructeur par défaut.
   * Créez un objet `AssemblerServiceClient.Endpoint.Address` en utilisant le constructeur `System.ServiceModel.EndpointAddress`. Transmettez une valeur de chaîne qui spécifie le WSDL au service AEM Forms (par exemple, `http://localhost:8080/soap/services/AssemblerService?blob=mtom`). Vous n&#39;avez pas besoin d&#39;utiliser l&#39;attribut `lc_version`. Cet attribut est utilisé lorsque vous créez une référence de service.)
   * Créez un objet `System.ServiceModel.BasicHttpBinding` en obtenant la valeur du champ `AssemblerServiceClient.Endpoint.Binding`. Convertissez la valeur de retour en `BasicHttpBinding`.
   * Définissez le champ `MessageEncoding` de l’objet `System.ServiceModel.BasicHttpBinding` sur `WSMessageEncoding.Mtom`. Cette valeur garantit l’utilisation de MTOM.
   * Activez l’authentification HTTP de base en exécutant les tâches suivantes :

      * Attribuez le nom d’utilisateur AEM forms au champ `AssemblerServiceClient.ClientCredentials.UserName.UserName`.
      * Attribuez la valeur de mot de passe correspondante au champ `AssemblerServiceClient.ClientCredentials.UserName.Password`.
      * Affectez la valeur constante `HttpClientCredentialType.Basic` au champ `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Affectez la valeur constante `BasicHttpSecurityMode.TransportCredentialOnly` au champ `BasicHttpBindingSecurity.Security.Mode`.

1. Référencez un document DDX existant.

   * Créez un objet `BLOB` en utilisant son constructeur. L’objet `BLOB` est utilisé pour stocker le document DDX.
   * Créez un objet `System.IO.FileStream` en appelant son constructeur et en transmettant une valeur de chaîne qui représente l’emplacement du fichier du document DDX et le mode d’ouverture du fichier.
   * Créez un tableau d’octets qui stocke le contenu de l’objet `System.IO.FileStream`. Vous pouvez déterminer la taille du tableau d’octets en obtenant la propriété `System.IO.FileStream` de l’objet `Length`.
   * Renseignez le tableau d’octets avec les données de flux en appelant la méthode `System.IO.FileStream` de l’objet `Read` et en transmettant le tableau d’octets, la position de départ et la longueur du flux à lire.
   * Renseignez l’objet `BLOB` en attribuant son champ `MTOM` au contenu du tableau d’octets.

1. Référencez un document PDF utilisé pour déterminer la conformité à la norme PDF/A.

   * Créez un objet `BLOB` en utilisant son constructeur. L’objet `BLOB` est utilisé pour stocker le document PDF d’entrée.
   * Créez un objet `System.IO.FileStream` en appelant son constructeur et en transmettant une valeur de chaîne qui représente l’emplacement du fichier du document PDF d’entrée et le mode d’ouverture du fichier.
   * Créez un tableau d’octets qui stocke le contenu de l’objet `System.IO.FileStream`. Vous pouvez déterminer la taille du tableau d’octets en obtenant la propriété `System.IO.FileStream` de l’objet `Length`.
   * Renseignez le tableau d’octets avec les données de flux en appelant la méthode `System.IO.FileStream` de l’objet `Read` et en transmettant le tableau d’octets, la position de départ et la longueur du flux à lire.
   * Renseignez l’objet `BLOB` en attribuant sa propriété `MTOM` au contenu du tableau d’octets.
   * Créez un objet `MyMapOf_xsd_string_To_xsd_anyType`. Cet objet de collection est utilisé pour stocker le document PDF.
   * Créez un objet `MyMapOf_xsd_string_To_xsd_anyType_Item`.
   * Attribuez une valeur de chaîne qui représente le nom de clé au champ `MyMapOf_xsd_string_To_xsd_anyType_Item` de l&#39;objet `key`. Cette valeur doit correspondre à la valeur de l’élément source PDF spécifié dans le document DDX.
   * Affectez l’objet `BLOB` qui stocke le document PDF au champ `MyMapOf_xsd_string_To_xsd_anyType_Item` de l’objet `value`.
   * Ajoutez l&#39;objet `MyMapOf_xsd_string_To_xsd_anyType_Item` à l&#39;objet `MyMapOf_xsd_string_To_xsd_anyType`. Appelez la méthode `MyMapOf_xsd_string_To_xsd_anyType` object&#39; `Add` et transmettez l&#39;objet `MyMapOf_xsd_string_To_xsd_anyType`.

1. Définissez les options d’exécution.

   * Créez un objet `AssemblerOptionSpec` qui stocke les options d’exécution à l’aide de son constructeur.
   * Définissez des options d&#39;exécution pour répondre aux besoins de votre entreprise en attribuant une valeur à un membre de données qui appartient à l&#39;objet `AssemblerOptionSpec`. Par exemple, pour demander au service Assembler de continuer à traiter une tâche en cas d’erreur, affectez `false` au membre de données `failOnError` de l’objet `AssemblerOptionSpec`.

1. Récupérez des informations sur le document PDF.

   Appelez la méthode `invoke` de l’objet `AssemblerServiceService` et transmettez les valeurs suivantes :

   * Objet `BLOB` représentant le document DDX.
   * Objet `MyMapOf_xsd_string_To_xsd_anyType` contenant le document PDF d’entrée. Ses clés doivent correspondre aux noms des fichiers source PDF et ses valeurs doivent être l’objet `BLOB` correspondant au fichier PDF d’entrée.
   * Objet `AssemblerOptionSpec` qui spécifie les options d’exécution.

   La méthode `invoke` renvoie un objet `AssemblerResult` contenant des données XML qui indique si le document PDF d’entrée est un document PDF/A.

1. Enregistrez le document XML renvoyé.

   Pour obtenir des données XML spécifiant si le document PDF d’entrée est un document PDF/A, effectuez les actions suivantes :

   * Accédez au champ `documents` de l’objet `AssemblerResult`, qui est un objet `Map` contenant les données XML qui spécifient si le document PDF d’entrée est un document PDF/A.
   * Effectuez une itération dans l&#39;objet `Map` pour obtenir chaque document cible. Ensuite, définissez la valeur de ce membre de tableau sur `BLOB`.
   * Extrayez les données binaires qui représentent les données XML en accédant au champ `BLOB` de l&#39;objet `MTOM` de l&#39;objet. Ce champ stocke un tableau d’octets que vous pouvez écrire dans un fichier XML.

**Voir également**

[Appel de AEM Forms à l’aide de MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
