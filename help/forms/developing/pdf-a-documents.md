---
title: Utilisation de documents PDF/A
seo-title: Utilisation de documents PDF/A
description: 'null'
seo-description: 'null'
uuid: c258d253-068a-4412-955a-21d8a4792d6f
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 1e6cc554-aef1-463c-906b-634b80a27917
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Utilisation de documents PDF/A {#working-with-pdf-a-documents}

**A propos du service DocConverter**

Le service DocConverter peut convertir des documents PDF en documents PDA/A. Vous pouvez accomplir les tâches suivantes à l’aide de ce service :

* Convertir des documents PDF en documents PDF/A. (voir [Conversion de documents en documents](pdf-a-documents.md#converting-documents-to-pdf-a-documents)PDF/A).
* Déterminez si les documents PDF sont des documents PDF/A. (Voir Détermination [par programmation de la conformité](pdf-a-documents.md#programmatically-determining-pdf-a-compliancy)à la norme PDF/A.)

>[!NOTE]
>
>For more information about the DocConverter service, see [Services Reference for AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

## Conversion de documents en documents PDF/A {#converting-documents-to-pdf-a-documents}

Vous pouvez utiliser le service DocConverter pour convertir un document PDF en document PDF/A. Le format PDF/A étant un format d’archivage destiné à la conservation à long terme du contenu du document, toutes les polices sont incorporées et le fichier n’est pas compressé. Par conséquent, un document PDF/A est généralement plus volumineux qu’un document PDF standard. De plus, un document PDF/A ne contient aucune donnée audio et vidéo. Avant de convertir un document PDF en document PDF/A, assurez-vous que le document PDF n’est pas un document PDF/A.

La spécification PDF/A-1 comprend deux niveaux de conformité, à savoir A et B. La principale différence entre les deux concerne la prise en charge de la structure logique (accessibilité), qui n&#39;est pas requise pour le niveau de conformité B. Quel que soit le niveau de conformité, PDF/A-1 exige que toutes les polices soient incorporées dans le document PDF/A généré. Actuellement, seul le format PDF/A-1b est pris en charge dans la validation (et la conversion).

Bien que PDF/A soit la norme d’archivage des documents PDF, il n’est pas obligatoire d’utiliser PDF/A pour l’archivage si un document PDF standard répond aux exigences de votre entreprise. La norme PDF/A a pour objectif d’établir un fichier PDF destiné à l’archivage à long terme et à la conservation de documents.

>[!NOTE]
>
>For more information about the DocConverter service, see [Services Reference for AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

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

For information about the location of these JAR files, see [Including AEM Forms Java library files](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Création d’un client DocConvert**

Avant de pouvoir exécuter une opération DocConverter par programmation, vous devez créer un client DocConverter. Si vous utilisez l’API Java, créez un `DocConverterServiceClient` objet. Si vous utilisez l’API du service Web DocConverter, créez un `DocConverterServiceService` objet.

**Référence à un document PDF à convertir en document PDF/A**

Récupérez un document PDF à convertir en document PDF/A. Si vous tentez de convertir un document PDF, tel qu’un formulaire Acrobat, en document PDF/A, vous provoquerez une exception.

**Définition des informations de suivi**

Vous pouvez définir une option d’exécution qui détermine la quantité d’informations suivies pendant le processus de conversion. En d’autres termes, vous pouvez définir neuf niveaux différents qui spécifient la quantité d’informations suivies par le service DocConverter lors de la conversion d’un document PDF en document PDF/A.

**Conversion du document**

Après avoir créé le client de service DocConverter, référencez le document PDF à convertir et définissez l’option d’exécution qui spécifie le suivi des informations, vous pouvez convertir le document PDF en document PDF/A.

**Enregistrement du document PDF/A**

Vous pouvez enregistrer le document PDF/A au format PDF.

**Voir également**

[Conversion de documents en documents PDF/A à l’aide de l’API Java](pdf-a-documents.md#convert-documents-to-pdf-a-documents-using-the-java-api)

[Conversion de documents en documents PDF/A à l’aide de l’API du service Web](pdf-a-documents.md#convert-documents-to-pdf-a-documents-using-the-web-service-api)

[Inclusion des fichiers de bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Détermination par programmation de la conformité à la norme PDF/A](pdf-a-documents.md#programmatically-determining-pdf-a-compliancy)

### Conversion de documents en documents PDF/A à l’aide de l’API Java {#convert-documents-to-pdf-a-documents-using-the-java-api}

Convertir un document PDF en document PDF/A à l’aide de l’API Java :

1. Inclure les fichiers de projet

   Incluez des fichiers JAR client, tels que adobe-docconverter-client.jar, dans le chemin de classe de votre projet Java.

1. Création d’un client DocConvert

   * Créez un objet `ServiceClientFactory` qui contient des propriétés de connexion.
   * Créez un objet `DocConverterServiceClient` en utilisant son constructeur et en transmettant l’objet `ServiceClientFactory`. 

1. Référence à un document PDF à convertir en document PDF/A

   * Créez un `java.io.FileInputStream` objet représentant le document PDF à convertir à l’aide de son constructeur et transmettez une valeur de chaîne indiquant l’emplacement du fichier PDF.
   * Créez un objet `com.adobe.idp.Document` en utilisant son constructeur et en transmettant l’objet `java.io.FileInputStream`. 

1. Définition des informations de suivi

   * Créez un objet `PDFAConversionOptionSpec` en utilisant son constructeur.
   * Définissez le niveau de suivi des informations en appelant la `PDFAConversionOptionSpec` `setLogLevel` méthode de l’objet et en transmettant une valeur de chaîne qui spécifie le niveau de suivi. For example, pass the value `FINE`. Pour plus d’informations sur les différentes valeurs, voir la `setLogLevel` méthode dans le Guide de référence [de l’API](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)AEM Forms.

1. Conversion du document

   Convertissez le document PDF en document PDF/A en appelant la `DocConverterServiceClient` `toPDFA` méthode de l’objet et en transmettant les valeurs suivantes :

   * Objet `com.adobe.idp.Document` contenant le document PDF à convertir
   * Objet `PDFAConversionOptionSpec` spécifiant les informations de suivi
   La `toPDFA` méthode renvoie un `PDFAConversionResult` objet contenant le document PDF/A.

1. Enregistrement du document PDF/A

   * Récupérez le document PDF/A en appelant la `PDFAConversionResult` `getPDFA` méthode de l’objet. Cette méthode renvoie un `com.adobe.idp.Document` objet représentant le document PDF/A.
   * Créez un `java.io.File` objet représentant le fichier PDF/A. Vérifiez que l’extension du nom de fichier est .pdf.
   * Remplissez le fichier avec des données PDF/A en appelant la `com.adobe.idp.Document` méthode de l’objet et en transmettant l’ `copyToFile` `java.io.File` objet.

**Voir également**

[Utilisation de documents PDF/A](pdf-a-documents.md#working-with-pdf-a-documents)

[Démarrage rapide (mode SOAP) : Conversion d’un document au format PDF/A à l’aide de l’API Java](/help/forms/developing/docconverter-service-java-api-quick.md#quick-start-soap-mode-converting-a-document-to-a-pdf-a-document-using-the-java-api)

[Inclusion des fichiers de bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Conversion de documents en documents PDF/A à l’aide de l’API du service Web {#convert-documents-to-pdf-a-documents-using-the-web-service-api}

Conversion d’un document PDF en document PDF/A à l’aide de l’API DocConverter (service Web) :

1. Inclure les fichiers de projet

   * Créez un assembly client Microsoft .NET qui consomme le fichier WSDL DocConverter.
   * Référencez l&#39;assembly client Microsoft .NET.

1. Création d’un client DocConvert

   * A l&#39;aide de l&#39;assembly client Microsoft .NET, créez un `DocConverterServiceService` objet en appelant son constructeur par défaut.
   * Définissez le membre `DocConverterServiceService` de données de l’ `Credentials` objet avec une `System.Net.NetworkCredential` valeur qui spécifie le nom d’utilisateur et la valeur du mot de passe.

1. Référence à un document PDF à convertir en document PDF/A

   * Créez un objet `BLOB` en utilisant son constructeur. L’ `BLOB` objet est utilisé pour stocker le document PDF converti en document PDF/A.
   * Créez un `System.IO.FileStream` objet en appelant son constructeur et en transmettant une valeur de chaîne représentant l’emplacement du fichier PDF et le mode d’ouverture du fichier.
   * Créez un tableau d’octets qui stocke le contenu de l’ `System.IO.FileStream` objet. Vous pouvez déterminer la taille du tableau d’octets en obtenant la `System.IO.FileStream` `Length` propriété de l’objet.
   * Renseignez le tableau d’octets avec les données de flux en appelant la `System.IO.FileStream` `Read` méthode de l’objet et en transmettant le tableau d’octets, la position de départ et la longueur du flux à lire.
   * Renseignez l’ `BLOB` objet en affectant sa `binaryData` propriété au contenu du tableau d’octets.

1. Définition des informations de suivi

   * Créez un objet `PDFAConversionOptionSpec` en utilisant son constructeur.
   * Définissez le niveau de suivi des informations en attribuant une valeur qui spécifie le niveau de suivi au membre `PDFAConversionOptionSpec` `logLevel` de données de l’objet. Par exemple, affectez la valeur `FINE` à ce membre de données.

1. Conversion du document

   Convertissez le document PDF en document PDF/A en appelant la `DocConverterServiceService` `toPDFA` méthode de l’objet et en transmettant les valeurs suivantes :

   * Objet `BLOB` contenant le document PDF à convertir
   * Objet `PDFAConversionOptionSpec` spécifiant les informations de suivi
   La `toPDFA` méthode renvoie un `PDFAConversionResult` objet contenant le document PDF/A.

1. Enregistrement du document PDF/A

   * Créez un `BLOB` objet qui stocke le document PDF/A en récupérant la valeur du membre `PDFAConversionResult` `PDFADocument` de données de l’objet.
   * Créez un tableau d’octets qui stocke le contenu de l’ `BLOB` objet renvoyé à l’aide de l’ `PDFAConversionResult` objet. Renseignez le tableau d’octets en obtenant la valeur du membre `BLOB` `binaryData` de données de l’objet.
   * Créez un `System.IO.FileStream` objet en appelant son constructeur et en transmettant une valeur de chaîne représentant l’emplacement du fichier du document PDF/A.
   * Create a `System.IO.BinaryWriter` object by invoking its constructor and passing the `System.IO.FileStream` object.
   * Ecrivez le contenu du tableau d’octets dans un fichier PDF en appelant la `System.IO.BinaryWriter` `Write` méthode de l’objet et en transmettant le tableau d’octets.

**Voir également**

[Utilisation de documents PDF/A](pdf-a-documents.md#working-with-pdf-a-documents)

[Appel d’AEM Forms à l’aide du codage Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

[Création d&#39;un assembly client .NET utilisant le codage Base64](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding)

## Détermination par programmation de la conformité à la norme PDF/A {#programmatically-determining-pdf-a-compliancy}

Vous pouvez utiliser le service DocConverter pour déterminer si un document PDF est compatible PDF/A. Pour plus d’informations sur un document PDF/A et sur la conversion d’un document PDF en document PDF/A, voir [Conversion de documents en documents](pdf-a-documents.md#converting-documents-to-pdf-a-documents)PDF/A.

>[!NOTE]
>
>For more information about the DocConverter service, see [Services Reference for AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

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

For information about the location of these JAR files, see [Including AEM Forms Java library files](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Création d’un client DocConvert**

Avant de pouvoir exécuter une opération DocConverter par programmation, vous devez créer un client DocConverter. Si vous utilisez l’API Java, créez un `DocConverterServiceClient` objet. Si vous utilisez l’API du service Web DocConverter, créez un `DocConverterServiceService` objet.

**Référence à un document PDF utilisé pour déterminer la conformité à la norme PDF/A**

Un document PDF doit être référencé et transmis au service DocConverter pour déterminer si le document PDF est compatible PDF/A.

**Définition des options d’exécution**

Vous pouvez définir une option d’exécution qui détermine la quantité d’informations suivies pendant le processus de conversion. En d’autres termes, vous pouvez définir neuf niveaux différents qui spécifient le niveau d’informations suivi par le service DocConverter lors de la conversion d’un document PDF en document PDF/A.

**Récupérer des informations sur le document PDF**

Après avoir créé le client de service DocConverter, référencé le document PDF et défini les options d’exécution, vous pouvez déterminer si le document PDF est compatible PDF/A.

**Voir également**

[Déterminer la conformité à la norme PDF/A à l’aide de l’API Java](pdf-a-documents.md#determine-pdf-a-compliancy-using-the-java-api)

[Déterminer la conformité à la norme PDF/A à l’aide de l’API du service Web](pdf-a-documents.md#determine-pdf-a-compliancy-using-the-web-service-api)

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

   * Créez un `java.io.FileInputStream` objet représentant le document PDF à convertir à l’aide de son constructeur et transmettez une valeur de chaîne indiquant l’emplacement du fichier PDF.
   * Créez un objet `com.adobe.idp.Document` en utilisant son constructeur et en transmettant l’objet `java.io.FileInputStream`. 

1. Définition des options d’exécution

   * Créez un objet `PDFAValidationOptionSpec` en utilisant son constructeur.
   * Définissez le niveau de conformité en appelant la `PDFAValidationOptionSpec` méthode de l’objet et en transmettant `setCompliance` `PDFAValidationOptionSpec.Compliance.PDFA_1B`.
   * Définissez le niveau de suivi des informations en appelant la `PDFAValidationOptionSpec` `setLogLevel` méthode de l’objet et en transmettant une valeur de chaîne qui spécifie le niveau de suivi. For example, pass the value `FINE`. Pour plus d’informations sur les différentes valeurs, voir la `setLogLevel` méthode dans le Guide de référence [de l’API](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)AEM Forms.

1. Récupérer des informations sur le document PDF

   Déterminez la conformité à la norme PDF/A en appelant la `DocConverterServiceClient` `isPDFA` méthode de l’objet et en transmettant les valeurs suivantes :

   * Objet `com.adobe.idp.Document` contenant le document PDF.
   * Objet `PDFAValidationOptionSpec` spécifiant les options d’exécution.
   La `isPDFA` méthode renvoie un `PDFAValidationResult` objet qui contient les résultats de cette opération.

**Voir également**

[Utilisation de documents PDF/A](pdf-a-documents.md#working-with-pdf-a-documents)

[Démarrage rapide (mode SOAP) : Détermination de la conformité à la norme PDF/A à l’aide de l’API Java](/help/forms/developing/docconverter-service-java-api-quick.md#quick-start-soap-mode-determining-pdf-a-compliancy-using-the-java-api)

[Inclusion des fichiers de bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Déterminer la conformité à la norme PDF/A à l’aide de l’API du service Web {#determine-pdf-a-compliancy-using-the-web-service-api}

Déterminez la conformité à la norme PDF/A en utilisant l’API du service Web :

1. Inclure les fichiers de projet

   * Créez un assembly client Microsoft .NET qui consomme le fichier WSDL DocConverter.
   * Référencez l&#39;assembly client Microsoft .NET.

1. Création d’un client DocConvert

   * A l&#39;aide de l&#39;assembly client Microsoft .NET, créez un `DocConverterServiceService` objet en appelant son constructeur par défaut.
   * Définissez le membre `DocConverterServiceService` de données de l’ `Credentials` objet avec une `System.Net.NetworkCredential` valeur qui spécifie le nom d’utilisateur et la valeur du mot de passe.

1. Référence à un document PDF utilisé pour déterminer la conformité à la norme PDF/A

   * Créez un objet `BLOB` en utilisant son constructeur. L’ `BLOB` objet est utilisé pour stocker le document PDF converti en document PDF/A.
   * Créez un `System.IO.FileStream` objet en appelant son constructeur et en transmettant une valeur de chaîne représentant l’emplacement du fichier PDF et le mode d’ouverture du fichier.
   * Créez un tableau d’octets qui stocke le contenu de l’ `System.IO.FileStream` objet. Vous pouvez déterminer la taille du tableau d’octets en obtenant la `System.IO.FileStream` `Length` propriété de l’objet.
   * Renseignez le tableau d’octets avec les données de flux en appelant la `System.IO.FileStream` `Read` méthode de l’objet et en transmettant le tableau d’octets, la position de départ et la longueur du flux à lire.
   * Renseignez l’ `BLOB` objet en affectant sa `binaryData` propriété au contenu du tableau d’octets.

1. Définition des options d’exécution

   * Créez un objet `PDFAValidationOptionSpec` en utilisant son constructeur.
   * Définissez le niveau de conformité en affectant la valeur `PDFAValidationOptionSpec` au membre `compliance` `PDFAConversionOptionSpec_Compliance.PDFA_1B`de données de l’objet.
   * Définissez le niveau de suivi des informations en affectant la valeur `PDFAValidationOptionSpec` au membre `resultLevel` `PDFAValidationOptionSpec_ResultLevel.DETAILED`de données de l’objet.

1. Récupérer des informations sur le document PDF

   Déterminez la conformité à la norme PDF/A en appelant la `DocConverterServiceService` `isPDFA` méthode de l’objet et en transmettant les valeurs suivantes :

   * Objet `BLOB` contenant le document PDF.
   * Objet `PDFAValidationOptionSpec` contenant des options d’exécution.
   La `isPDFA` méthode renvoie un `PDFAValidationResult` objet qui contient les résultats de cette opération.

**Voir également**

[Utilisation de documents PDF/A](pdf-a-documents.md#working-with-pdf-a-documents)

[Appel d’AEM Forms à l’aide du codage Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

[Création d&#39;un assembly client .NET utilisant le codage Base64](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding)
