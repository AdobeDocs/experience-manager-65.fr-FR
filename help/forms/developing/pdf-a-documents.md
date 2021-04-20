---
title: Utilisation de Documents PDF/A
seo-title: Utilisation de Documents PDF/A
description: Utilisez le service DocConverter pour déterminer si un document PDF est un document PDF/A et convertir des documents PDF en documents PDF/A.
seo-description: Utilisez le service DocConverter pour déterminer si un document PDF est un document PDF/A et convertir des documents PDF en documents PDF/A.
uuid: c258d253-068a-4412-955a-21d8a4792d6f
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 1e6cc554-aef1-463c-906b-634b80a27917
role: Developer
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '2387'
ht-degree: 7%

---


# Utilisation de Documents PDF/A {#working-with-pdf-a-documents}

**A propos du service DocConverter**

Le service DocConverter peut convertir des documents PDF en documents PDA/A. Vous pouvez exécuter ces tâches à l’aide de ce service :

* Conversion de documents PDF en documents PDF/A. (Voir [Conversion de Documents en Documents PDF/A](pdf-a-documents.md#converting-documents-to-pdf-a-documents).)
* Déterminez si les documents PDF sont des documents PDF/A. (Voir [Détermination par programmation de la conformité à la norme PDF/A](pdf-a-documents.md#programmatically-determining-pdf-a-compliancy).)

>[!NOTE]
>
>Pour plus d’informations sur le service DocConverter, voir [Guide de référence des services pour AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

## Conversion de Documents en Documents PDF/A {#converting-documents-to-pdf-a-documents}

Vous pouvez utiliser le service DocConverter pour convertir un document PDF en document PDF/A. Le format PDF/A étant un format d’archivage permettant la conservation à long terme du contenu du document, toutes les polices sont incorporées et le fichier n’est pas compressé. Par conséquent, un document PDF/A est généralement plus volumineux qu’un document PDF standard. De plus, un document PDF/A ne contient aucune donnée audio et vidéo. Avant de convertir un document PDF en document PDF/A, assurez-vous que le document PDF n’est pas un document PDF/A.

La spécification PDF/A-1 comprend deux niveaux de conformité, à savoir A et B. La principale différence entre les deux concerne la prise en charge de la structure logique (accessibilité), qui n’est pas requise pour le niveau de conformité B. Quel que soit le niveau de conformité, PDF/A-1 exige que toutes les polices soient incorporées dans le document PDF/A généré. Actuellement, seul le format PDF/A-1b est pris en charge dans la validation (et la conversion).

Bien que PDF/A soit la norme d’archivage des documents PDF, il n’est pas obligatoire d’utiliser PDF/A pour l’archivage si un document PDF standard répond aux exigences de votre société. La norme PDF/A a pour but d’établir un fichier PDF destiné à l’archivage à long terme et à la conservation des documents.

>[!NOTE]
>
>Pour plus d’informations sur le service DocConverter, voir [Guide de référence des services pour AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Résumé des étapes {#summary-of-steps}

Pour convertir un document PDF en document PDF/A, procédez comme suit :

1. Incluez des fichiers de projet.
1. Création d’un client DocConvert
1. Référencez un document PDF à convertir en document PDF/A.
1. Définissez les informations de suivi.
1. Convertir le document.
1. Enregistrez le document PDF/A.

**Inclure les fichiers de projet**

Incluez les fichiers nécessaires dans votre projet de développement. Si vous créez une application cliente à l’aide de Java, incluez les fichiers JAR nécessaires. Si vous utilisez des services Web, veillez à inclure les fichiers proxy.

Les fichiers JAR suivants doivent être ajoutés au chemin de classe de votre projet :

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-docconverter-client.jar
* adobe-utilities.jar (requis si AEM Forms est déployé sur JBoss Application Server)
* jbossall-client.jar (requis si AEM Forms est déployé sur JBoss Application Server)

Pour plus d’informations sur l’emplacement de ces fichiers JAR, voir [Inclusion de fichiers de bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Création d’un client DocConvert**

Avant de pouvoir exécuter une opération DocConverter par programmation, vous devez créer un client DocConverter. Si vous utilisez l’API Java, créez un objet `DocConverterServiceClient`. Si vous utilisez l’API du service Web DocConverter, créez un objet `DocConverterServiceService`.

**Référence à un document PDF à convertir en document PDF/A**

Récupérez un document PDF à convertir en document PDF/A. Si vous tentez de convertir un document PDF, tel qu’un formulaire Acrobat, en document PDF/A, vous provoquerez une exception.

**Définition des informations de suivi**

Vous pouvez définir une option d’exécution qui détermine la quantité d’informations suivies pendant le processus de conversion. En d’autres termes, vous pouvez définir neuf niveaux différents qui spécifient la quantité d’informations suivies par le service DocConverter lors de la conversion d’un document PDF en document PDF/A.

**Convertir le document**

Après avoir créé le client de service DocConverter, référencez le document PDF à convertir et définissez l’option d’exécution qui spécifie le suivi des informations, vous pouvez convertir le document PDF en document PDF/A.

**Enregistrer le document PDF/A**

Vous pouvez enregistrer le document PDF/A au format PDF.

**Voir également**

[Conversion de documents en documents PDF/A à l’aide de l’API Java](pdf-a-documents.md#convert-documents-to-pdf-a-documents-using-the-java-api)

[Conversion de documents en documents PDF/A à l’aide de l’API du service Web](pdf-a-documents.md#convert-documents-to-pdf-a-documents-using-the-web-service-api)

[Inclusion des fichiers de bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Détermination par programmation de la conformité à la norme PDF/A](pdf-a-documents.md#programmatically-determining-pdf-a-compliancy)

### Convertir des documents en documents PDF/A à l’aide de l’API Java {#convert-documents-to-pdf-a-documents-using-the-java-api}

Conversion d’un document PDF en document PDF/A à l’aide de l’API Java :

1. Inclure les fichiers de projet

   Incluez des fichiers JAR client, tels que adobe-docconverter-client.jar, dans le chemin de classe de votre projet Java.

1. Création d’un client DocConvert

   * Créez un objet `ServiceClientFactory` qui contient des propriétés de connexion.
   * Créez un objet `DocConverterServiceClient` en utilisant son constructeur et en transmettant l’objet `ServiceClientFactory`. 

1. Référence à un document PDF à convertir en document PDF/A

   * Créez un objet `java.io.FileInputStream` représentant le document PDF à convertir à l’aide de son constructeur et transmettez une valeur de chaîne indiquant l’emplacement du fichier PDF.
   * Créez un objet `com.adobe.idp.Document` en utilisant son constructeur et en transmettant l’objet `java.io.FileInputStream`. 

1. Définition des informations de suivi

   * Créez un objet `PDFAConversionOptionSpec` en utilisant son constructeur.
   * Définissez le niveau de suivi des informations en appelant la méthode `PDFAConversionOptionSpec` de l&#39;objet `setLogLevel` et en transmettant une valeur de chaîne qui spécifie le niveau de suivi. Par exemple, transmettez la valeur `FINE`. Pour plus d’informations sur les différentes valeurs, voir la méthode `setLogLevel` dans le [Guide de référence de l’API AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

1. Convertir le document

   Convertissez le document PDF en document PDF/A en appelant la méthode `DocConverterServiceClient` de l’objet `toPDFA` et en transmettant les valeurs suivantes :

   * Objet `com.adobe.idp.Document` contenant le document PDF à convertir
   * L&#39;objet `PDFAConversionOptionSpec` qui spécifie les informations de suivi

   La méthode `toPDFA` renvoie un objet `PDFAConversionResult` contenant le document PDF/A.

1. Enregistrer le document PDF/A

   * Récupérez le document PDF/A en appelant la méthode `PDFAConversionResult` de l’objet `getPDFA`. Cette méthode renvoie un objet `com.adobe.idp.Document` qui représente le document PDF/A.
   * Créez un objet `java.io.File` représentant le fichier PDF/A. Assurez-vous que l’extension de nom de fichier est .pdf.
   * Remplissez le fichier avec des données PDF/A en appelant la méthode `com.adobe.idp.Document` de l’objet `copyToFile` et en transmettant l’objet `java.io.File`.

**Voir également**

[Utilisation de Documents PDF/A](pdf-a-documents.md#working-with-pdf-a-documents)

[Début rapide (mode SOAP) : Conversion d’un document en document PDF/A à l’aide de l’API Java](/help/forms/developing/docconverter-service-java-api-quick.md#quick-start-soap-mode-converting-a-document-to-a-pdf-a-document-using-the-java-api)

[Inclusion des fichiers de bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Convertir des documents en documents PDF/A à l’aide de l’API de service Web {#convert-documents-to-pdf-a-documents-using-the-web-service-api}

Conversion d’un document PDF en document PDF/A à l’aide de l’API DocConverter (service Web) :

1. Inclure les fichiers de projet

   * Créez un assembly client Microsoft .NET qui consomme le fichier WSDL DocConverter.
   * Référencez l&#39;assembly client Microsoft .NET.

1. Création d’un client DocConvert

   * A l&#39;aide de l&#39;assembly client Microsoft .NET, créez un objet `DocConverterServiceService` en appelant son constructeur par défaut.
   * Définissez le membre de données `Credentials` de l’objet avec une valeur `System.Net.NetworkCredential` qui spécifie le nom d’utilisateur et la valeur du mot de passe.`DocConverterServiceService`

1. Référence à un document PDF à convertir en document PDF/A

   * Créez un objet `BLOB` en utilisant son constructeur. L’objet `BLOB` est utilisé pour stocker le document PDF converti en document PDF/A.
   * Créez un objet `System.IO.FileStream` en appelant son constructeur et en transmettant une valeur de chaîne qui représente l’emplacement du fichier du document PDF et le mode d’ouverture du fichier.
   * Créez un tableau d’octets qui stocke le contenu de l’objet `System.IO.FileStream`. Vous pouvez déterminer la taille du tableau d’octets en obtenant la propriété `System.IO.FileStream` de l’objet `Length`.
   * Renseignez le tableau d’octets avec les données de flux en appelant la méthode `System.IO.FileStream` de l’objet `Read` et en transmettant le tableau d’octets, la position de départ et la longueur du flux à lire.
   * Renseignez l’objet `BLOB` en attribuant sa propriété `binaryData` au contenu du tableau d’octets.

1. Définition des informations de suivi

   * Créez un objet `PDFAConversionOptionSpec` en utilisant son constructeur.
   * Définissez le niveau de suivi des informations en attribuant une valeur qui spécifie le niveau de suivi au membre de données `PDFAConversionOptionSpec` de l&#39;objet `logLevel`. Par exemple, affectez la valeur `FINE` à ce membre de données.

1. Convertir le document

   Convertissez le document PDF en document PDF/A en appelant la méthode `DocConverterServiceService` de l’objet `toPDFA` et en transmettant les valeurs suivantes :

   * Objet `BLOB` contenant le document PDF à convertir
   * L&#39;objet `PDFAConversionOptionSpec` qui spécifie les informations de suivi

   La méthode `toPDFA` renvoie un objet `PDFAConversionResult` contenant le document PDF/A.

1. Enregistrer le document PDF/A

   * Créez un objet `BLOB` qui stocke le document PDF/A en obtenant la valeur du membre de données `PDFAConversionResult` de l’objet `PDFADocument`.
   * Créez un tableau d’octets qui stocke le contenu de l’objet `BLOB` renvoyé à l’aide de l’objet `PDFAConversionResult`. Renseignez le tableau d’octets en obtenant la valeur du membre de données `binaryData` de l’objet `BLOB`.
   * Créez un objet `System.IO.FileStream` en appelant son constructeur et en transmettant une valeur de chaîne qui représente l’emplacement du fichier du document PDF/A.
   * Créez un objet `System.IO.BinaryWriter` en appelant son constructeur et en transmettant l&#39;objet `System.IO.FileStream`.
   * Ecrivez le contenu du tableau d’octets dans un fichier PDF en appelant la méthode `System.IO.BinaryWriter` de l’objet `Write` et en transmettant le tableau d’octets.

**Voir également**

[Utilisation de Documents PDF/A](pdf-a-documents.md#working-with-pdf-a-documents)

[Appel de AEM Forms à l’aide du codage Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

[Création d&#39;un assembly client .NET utilisant le codage Base64](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding)

## Détermination par programmation de la conformité à la norme PDF/A {#programmatically-determining-pdf-a-compliancy}

Vous pouvez utiliser le service DocConverter pour déterminer si un document PDF est compatible PDF/A. Pour plus d’informations sur un document PDF/A et comment convertir un document PDF en document PDF/A, voir [Conversion de Documents en Documents PDF/A](pdf-a-documents.md#converting-documents-to-pdf-a-documents).

>[!NOTE]
>
>Pour plus d’informations sur le service DocConverter, voir [Guide de référence des services pour AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Résumé des étapes {#summary_of_steps-1}

Pour déterminer la conformité à la norme PDF/A, procédez comme suit :

1. Incluez des fichiers de projet.
1. Création d’un client DocConvert
1. Référencez un document PDF utilisé pour déterminer la conformité à la norme PDF/A.
1. Définissez les options d’exécution.
1. Récupérez des informations sur le document PDF.

**Inclure les fichiers de projet**

Incluez les fichiers nécessaires dans votre projet de développement. Si vous créez une application cliente à l’aide de Java, incluez les fichiers JAR nécessaires. Si vous utilisez des services Web, veillez à inclure les fichiers proxy.

Les fichiers JAR suivants doivent être ajoutés au chemin de classe de votre projet :

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-docconverter-client.jar
* adobe-utilities.jar (requis si AEM Forms est déployé sur JBoss Application Server)
* jbossall-client.jar (requis si AEM Forms est déployé sur JBoss Application Server)

Pour plus d’informations sur l’emplacement de ces fichiers JAR, voir [Inclusion de fichiers de bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Création d’un client DocConvert**

Avant de pouvoir exécuter une opération DocConverter par programmation, vous devez créer un client DocConverter. Si vous utilisez l’API Java, créez un objet `DocConverterServiceClient`. Si vous utilisez l’API du service Web DocConverter, créez un objet `DocConverterServiceService`.

**Référence à un document PDF utilisé pour déterminer la conformité à la norme PDF/A**

Un document PDF doit être référencé et transmis au service DocConverter pour déterminer si le document PDF est compatible PDF/A.

**Définition des options d’exécution**

Vous pouvez définir une option d’exécution qui détermine la quantité d’informations suivies pendant le processus de conversion. En d’autres termes, vous pouvez définir neuf niveaux différents qui spécifient la quantité d’informations suivies par le service DocConverter lors de la conversion d’un document PDF en document PDF/A.

**Récupération d’informations sur le document PDF**

Après avoir créé le client de service DocConverter, référencé le document PDF et défini les options d’exécution, vous pouvez déterminer si le document PDF est compatible PDF/A.

**Voir également**

[Détermination de la conformité à la norme PDF/A à l’aide de l’API Java](pdf-a-documents.md#determine-pdf-a-compliancy-using-the-java-api)

[Détermination de la conformité à la norme PDF/A à l’aide de l’API du service Web](pdf-a-documents.md#determine-pdf-a-compliancy-using-the-web-service-api)

[Inclusion des fichiers de bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Déterminer la conformité à la norme PDF/A à l’aide de l’API Java {#determine-pdf-a-compliancy-using-the-java-api}

Déterminez la conformité à la norme PDF/A à l’aide de l’API Java :

1. Inclure les fichiers de projet

   Incluez des fichiers JAR client, tels que adobe-docconverter-client.jar, dans le chemin de classe de votre projet Java.

1. Création d’un client DocConvert

   * Créez un objet `ServiceClientFactory` qui contient des propriétés de connexion.
   * Créez un objet `DocConverterServiceClient` en utilisant son constructeur et en transmettant l’objet `ServiceClientFactory`. 

1. Référence à un document PDF utilisé pour déterminer la conformité à la norme PDF/A

   * Créez un objet `java.io.FileInputStream` représentant le document PDF à convertir à l’aide de son constructeur et transmettez une valeur de chaîne indiquant l’emplacement du fichier PDF.
   * Créez un objet `com.adobe.idp.Document` en utilisant son constructeur et en transmettant l’objet `java.io.FileInputStream`. 

1. Définition des options d’exécution

   * Créez un objet `PDFAValidationOptionSpec` en utilisant son constructeur.
   * Définissez le niveau de conformité en appelant la méthode `PDFAValidationOptionSpec` de l&#39;objet `setCompliance` et en transmettant `PDFAValidationOptionSpec.Compliance.PDFA_1B`.
   * Définissez le niveau de suivi des informations en appelant la méthode `PDFAValidationOptionSpec` de l&#39;objet `setLogLevel` et en transmettant une valeur de chaîne qui spécifie le niveau de suivi. Par exemple, transmettez la valeur `FINE`. Pour plus d’informations sur les différentes valeurs, voir la méthode `setLogLevel` dans le [Guide de référence de l’API AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

1. Récupération d’informations sur le document PDF

   Déterminez la conformité à la norme PDF/A en invoquant la méthode `isPDFA` de l’objet `DocConverterServiceClient` et en transmettant les valeurs suivantes :

   * Objet `com.adobe.idp.Document` contenant le document PDF.
   * Objet `PDFAValidationOptionSpec` qui spécifie les options d&#39;exécution.

   La méthode `isPDFA` renvoie un objet `PDFAValidationResult` contenant les résultats de cette opération.

**Voir également**

[Utilisation de Documents PDF/A](pdf-a-documents.md#working-with-pdf-a-documents)

[Début rapide (mode SOAP) : Détermination de la conformité à la norme PDF/A à l’aide de l’API Java](/help/forms/developing/docconverter-service-java-api-quick.md#quick-start-soap-mode-determining-pdf-a-compliancy-using-the-java-api)

[Inclusion des fichiers de bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Déterminer la conformité à la norme PDF/A à l’aide de l’API du service Web {#determine-pdf-a-compliancy-using-the-web-service-api}

Déterminez la conformité à la norme PDF/A en utilisant l’API du service Web :

1. Inclure les fichiers de projet

   * Créez un assembly client Microsoft .NET qui consomme le fichier WSDL DocConverter.
   * Référencez l&#39;assembly client Microsoft .NET.

1. Création d’un client DocConvert

   * A l&#39;aide de l&#39;assembly client Microsoft .NET, créez un objet `DocConverterServiceService` en appelant son constructeur par défaut.
   * Définissez le membre de données `Credentials` de l’objet avec une valeur `System.Net.NetworkCredential` qui spécifie le nom d’utilisateur et la valeur du mot de passe.`DocConverterServiceService`

1. Référence à un document PDF utilisé pour déterminer la conformité à la norme PDF/A

   * Créez un objet `BLOB` en utilisant son constructeur. L’objet `BLOB` est utilisé pour stocker le document PDF converti en document PDF/A.
   * Créez un objet `System.IO.FileStream` en appelant son constructeur et en transmettant une valeur de chaîne qui représente l’emplacement du fichier du document PDF et le mode d’ouverture du fichier.
   * Créez un tableau d’octets qui stocke le contenu de l’objet `System.IO.FileStream`. Vous pouvez déterminer la taille du tableau d’octets en obtenant la propriété `System.IO.FileStream` de l’objet `Length`.
   * Renseignez le tableau d’octets avec les données de flux en appelant la méthode `System.IO.FileStream` de l’objet `Read` et en transmettant le tableau d’octets, la position de départ et la longueur du flux à lire.
   * Renseignez l’objet `BLOB` en attribuant sa propriété `binaryData` au contenu du tableau d’octets.

1. Définition des options d’exécution

   * Créez un objet `PDFAValidationOptionSpec` en utilisant son constructeur.
   * Définissez le niveau de conformité en attribuant au membre de données `compliance` de l&#39;objet `PDFAValidationOptionSpec` la valeur `PDFAConversionOptionSpec_Compliance.PDFA_1B`.
   * Définissez le niveau de suivi des informations en affectant au membre de données `resultLevel` de l&#39;objet `PDFAValidationOptionSpec` la valeur `PDFAValidationOptionSpec_ResultLevel.DETAILED`.

1. Récupération d’informations sur le document PDF

   Déterminez la conformité à la norme PDF/A en invoquant la méthode `isPDFA` de l’objet `DocConverterServiceService` et en transmettant les valeurs suivantes :

   * Objet `BLOB` contenant le document PDF.
   * Objet `PDFAValidationOptionSpec` contenant les options d&#39;exécution.

   La méthode `isPDFA` renvoie un objet `PDFAValidationResult` contenant les résultats de cette opération.

**Voir également**

[Utilisation de Documents PDF/A](pdf-a-documents.md#working-with-pdf-a-documents)

[Appel de AEM Forms à l’aide du codage Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

[Création d&#39;un assembly client .NET utilisant le codage Base64](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding)
