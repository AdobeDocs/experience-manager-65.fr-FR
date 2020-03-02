---
title: Conversion entre formats de fichier et PDF
seo-title: Conversion entre formats de fichier et PDF
description: 'null'
seo-description: 'null'
uuid: f72ad603-c996-4d48-9bfc-bed7bf776af6
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 180cac3f-6378-42bc-9a47-60f9f08a7103
translation-type: tm+mt
source-git-commit: 67ea825215d1ca7cc2e350ed1c128c3146de45ec

---


# Conversion entre formats de fichier et PDF {#converting-between-file-formatsand-pdf}

**A propos du service Generate PDF**

Le service Generate PDF peut convertir de nombreux formats de fichier natifs en PDF. Il convertit également des fichiers PDF en d’autres formats et optimise la taille des documents PDF.

Le service Generate PDF utilise des applications natives pour convertir les formats de fichiers suivants en PDF. Sauf précision contraire, seules les versions allemande, anglaise, française et japonaise de ces applications sont prises en charge. *Windows uniquement* indique la prise en charge de Windows Server® 2003 et Windows Server 2008 uniquement.

* Microsoft Office 2003 et 2007 pour convertir les formats DOC, DOCX, RTF, TXT, XLS, XLSX, PPT, PPTX, VSD, MPP, MPPX, XPS et PUB (Windows uniquement)

   **Remarque**: Acrobat® 9.2 ou version ultérieure est requis pour convertir le format Microsoft XPS au format PDF.*

* Autodesk AutoCAD 2005, 2006, 2007, 2008 et 2009 pour convertir les fichiers DWF, DWG et DXW (en anglais uniquement)
* Corel WordPerfect 12 et X4 pour convertir WPD, QPW, SHW (en anglais uniquement)
* OpenOffice 2.0, 2.4, 3.0.1 et 3.1 pour convertir les formats ODT, ODS, ODP, ODG, ODF, SXW, SXI, SXC, SXD, DOC, DOCX, RTF, TXT, XLS, XLSX, PPT, PPTX, VSD, MPP, MPPX et PUB

   ***Remarque **: Le service Generate PDF ne prend pas en charge les versions 64 bits d’OpenOffice.*

* Adobe Photoshop® CS2 pour convertir le fichier PSD (Windows uniquement)

   ***Remarque**: Photoshop CS3 et CS4 ne sont pas pris en charge car ils ne prennent pas en charge Windows Server 2003 ou Windows Server 2008. *

* Adobe FrameMaker® 7.2 et 8 pour convertir des fichiers FM (Windows uniquement)
* Adobe PageMaker® 7.0 pour convertir les formats PMD, PM6, P65 et PM (Windows uniquement)
* Formats natifs pris en charge par les applications tierces (requiert le développement de fichiers d’installation spécifiques à l’application) (Windows uniquement)

Le service Generate PDF peut convertir les formats standards suivants en PDF.

* Formats vidéo : SWF, FLV (Windows uniquement)
* Formats image : JPEG, JPG, JP2, J2Kí, JPC, J2C, GIF, BMP, TIFF, TIF, PNG, JPF
* HTML (Windows, Sun™ Solaris™ et Linux®)

Le service Generate PDF peut convertir des PDF aux formats de fichiers suivants (Windows uniquement) :

* Encapsulated Postscript (EPS)
* HTML3.2
* HTML 4.01 avec CSS 1.0
* DOC (format Microsoft Word)
* RTF
* Texte (à la fois accessible et brut)
* XML
* PDF/A-1a utilisant uniquement l’espace colorimétrique DeviceRGB
* PDF/A-1b utilisant uniquement l’espace colorimétrique DeviceRGB

Le service Generate PDF requiert que vous réalisiez ces tâches administratives :

* Installez les applications natives requises sur l’ordinateur hébergeant AEM Forms
* Installez Adobe Acrobat Professional ou Acrobat Pro Extended 9.2 sur l’ordinateur hébergeant AEM Forms.
* Réalisez les tâches consécutives à l’installation.

Ces tâches sont décrites dans la section Installation et déploiement d’AEM forms à l’aide de JBoss clé en main.

Vous pouvez effectuer les tâches suivantes à l’aide du service Generate PDF :

* Convertir des formats de fichier natifs en PDF.
* Convertir des documents HTML en documents PDF.
* Convertir des documents PDF en formats de fichier.

>[!NOTE]
>
>For more information about the Generate PDF service, see [Services Reference for AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

## Conversion de documents Word en documents PDF {#converting-word-documents-to-pdf-documents}

Cette section décrit l’utilisation de l’API Generate PDF pour convertir par programmation un document Microsoft Word en document PDF.

>[!NOTE]
>
>Pour plus d’informations sur les formats de fichier supplémentaires, voir [Ajout de formats](converting-file-formats-pdf.md#adding-support-for-additional-native-file-formats)de fichier natifs pris en charge.

>[!NOTE]
>
>For more information about the Generate PDF service, see [Services Reference for AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Résumé des étapes {#summary-of-steps}

Pour convertir un document Microsoft Word en document PDF, procédez comme suit :

1. Incluez des fichiers de projet.
1. Créez un client Generate PDF.
1. Récupérez le fichier à convertir en document PDF.
1. Convertissez le fichier en document PDF.
1. Récupérez les résultats.

**Inclure les fichiers de projet**

Incluez les fichiers nécessaires dans votre projet de développement. Si vous créez une application cliente à l’aide de Java, incluez les fichiers JAR nécessaires. Si vous utilisez des services Web, veillez à inclure les fichiers proxy.

**Création d’un client Generate PDF**

Avant de pouvoir exécuter par programmation une opération de génération de PDF, créez un client de service Generate PDF. Si vous utilisez l’API Java, créez un `GeneratePdfServiceClient` objet. Si vous utilisez l’API du service Web, créez un `GeneratePDFServiceService` objet.

**Récupérer le fichier à convertir en document PDF**

Récupérez le document Microsoft Word à convertir en document PDF.

**Convertir le fichier en document PDF**

Après avoir créé le client de service Generate PDF, vous pouvez appeler la `createPDF2` méthode. Cette méthode nécessite des informations sur le document à convertir, y compris l’extension de fichier.

**Récupérer les résultats**

Une fois le fichier converti en document PDF, vous pouvez récupérer les résultats. Par exemple, après avoir converti un fichier Word en document PDF, vous pouvez récupérer et enregistrer le document PDF.

**Voir également**

[Conversion de documents Word en documents PDF à l’aide de l’API Java](converting-file-formats-pdf.md#convert-word-documents-to-pdf-documents-using-the-java-api)

[Conversion de documents Word en documents PDF à l’aide de l’API du service Web](converting-file-formats-pdf.md#convert-word-documents-to-pdf-documents-using-the-web-service-api)

[Inclusion des fichiers de bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Démarrage rapide de l’API du service Generate PDF](/help/forms/developing/generate-pdf-service-java-api.md#generate-pdf-service-java-api-quick-start-soap)

### Conversion de documents Word en documents PDF à l’aide de l’API Java {#convert-word-documents-to-pdf-documents-using-the-java-api}

Convertir un document Microsoft Word en document PDF à l’aide de l’API Generate PDF (Java) :

1. Incluez des fichiers de projet.

   Incluez des fichiers JAR client, tels que adobe-generatepdf-client.jar, dans le chemin de classe de votre projet Java.

1. Créez un client Generate PDF.

   * Créez un objet `ServiceClientFactory` qui contient des propriétés de connexion.
   * Créez un objet `GeneratePdfServiceClient` en utilisant son constructeur et en transmettant l’objet `ServiceClientFactory`. 

1. Récupérez le fichier à convertir en document PDF.

   * Créez un `java.io.FileInputStream` objet qui représente le fichier Word à convertir à l’aide de son constructeur. Transmettez une valeur de chaîne qui spécifie l’emplacement du fichier.
   * Créez un objet `com.adobe.idp.Document` en utilisant son constructeur et en transmettant l’objet `java.io.FileInputStream`. 

1. Convertissez le fichier en document PDF.

   Convertissez le fichier en document PDF en appelant la `GeneratePdfServiceClient` `createPDF2` méthode de l’objet et en transmettant les valeurs suivantes :

   * A `com.adobe.idp.Document` object that represents the file to convert.
   * Objet `java.lang.String` contenant l’extension de fichier.
   * Objet `java.lang.String` contenant les paramètres de type de fichier à utiliser dans la conversion. Les paramètres de type de fichier fournissent des paramètres de conversion pour différents types de fichier, tels que .doc ou .xls.
   * Objet `java.lang.String` contenant le nom des paramètres PDF à utiliser. Par exemple, vous pouvez spécifier `Standard`.
   * Objet `java.lang.String` contenant le nom des paramètres de sécurité à utiliser.
   * Objet facultatif `com.adobe.idp.Document` contenant les paramètres à appliquer lors de la génération du document PDF.
   * Objet facultatif `com.adobe.idp.Document` contenant des informations de métadonnées à appliquer au document PDF.
   La `createPDF2` méthode renvoie un `CreatePDFResult` objet contenant le nouveau document PDF et des informations de journal. Le fichier journal contient généralement des messages d’erreur ou d’avertissement générés par la demande de conversion.

1. Récupérez les résultats.

   Pour obtenir le document PDF, procédez comme suit :

   * Appelez la `CreatePDFResult` méthode de l’ `getCreatedDocument` objet, qui renvoie un `com.adobe.idp.Document` objet.
   * Appelez la méthode `com.adobe.idp.Document` `copyToFile` de l’objet pour extraire le document PDF de l’objet créé à l’étape précédente.
   Si vous avez utilisé la `createPDF2` méthode pour obtenir le document journal (non applicable aux conversions HTML), effectuez les actions suivantes :

   * Appelez la méthode `CreatePDFResult` `getLogDocument` de l’objet. Renvoie un `com.adobe.idp.Document` objet.
   * Appelez la méthode `com.adobe.idp.Document` `copyToFile` de l’objet pour extraire le document journal.


**Voir également**

[Résumé des étapes](converting-file-formats-pdf.md#summary-of-steps)

[Démarrage rapide (mode SOAP) : Conversion d’un document Microsoft Word en document PDF à l’aide de l’API Java](/help/forms/developing/generate-pdf-service-java-api.md#quick-start-soap-mode-converting-a-microsoft-word-document-to-a-pdf-document-using-the-java-api)

[Inclusion des fichiers de bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Conversion de documents Word en documents PDF à l’aide de l’API du service Web {#convert-word-documents-to-pdf-documents-using-the-web-service-api}

Convertir un document Microsoft Word en document PDF à l’aide de l’API Generate PDF (service Web) :

1. Incluez des fichiers de projet.

   Créez un projet Microsoft .NET qui utilise MTOM. Veillez à utiliser la définition WSDL suivante : `http://localhost:8080/soap/services/GeneratePDFService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Remplacez `localhost` par l’adresse IP du serveur hébergeant AEM Forms.

1. Créez un client Generate PDF.

   * Create a `GeneratePDFServiceClient` object by using its default constructor.
   * Create a `GeneratePDFServiceClient.Endpoint.Address` object by using the `System.ServiceModel.EndpointAddress` constructor. Transmettez une valeur de chaîne qui spécifie le WSDL au service AEM Forms (par exemple, `http://localhost:8080/soap/services/GeneratePDFService?blob=mtom`). Vous n’avez pas besoin d’utiliser l’ `lc_version` attribut. Spécifiez toutefois `?blob=mtom`.
   * Créez un `System.ServiceModel.BasicHttpBinding` objet en obtenant la valeur du `GeneratePDFServiceClient.Endpoint.Binding` champ. Convertissez la valeur de retour en `BasicHttpBinding`.
   * Définissez le `System.ServiceModel.BasicHttpBinding` champ de l’ `MessageEncoding` objet sur `WSMessageEncoding.Mtom`. Cette valeur garantit l’utilisation de MTOM.
   * Activez l’authentification HTTP de base en effectuant les tâches suivantes :

      * Attribuez le nom d’utilisateur d’AEM forms au champ `GeneratePDFServiceClient.ClientCredentials.UserName.UserName`.
      * Attribuez la valeur de mot de passe correspondante au champ `GeneratePDFServiceClient.ClientCredentials.UserName.Password`.
      * Attribuez la valeur constante `HttpClientCredentialType.Basic` au champ `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Attribuez la valeur constante `BasicHttpSecurityMode.TransportCredentialOnly` au champ `BasicHttpBindingSecurity.Security.Mode`.

1. Récupérez le fichier à convertir en document PDF.

   * Créez un objet `BLOB` en utilisant son constructeur. L’ `BLOB` objet est utilisé pour stocker le fichier à convertir en document PDF.
   * Create a `System.IO.FileStream` object by invoking its constructor. Transmettez une valeur de chaîne qui représente l’emplacement du fichier à convertir et le mode d’ouverture du fichier.
   * Créez un tableau d’octets qui stocke le contenu de l’ `System.IO.FileStream` objet. Vous pouvez déterminer la taille du tableau d’octets en obtenant la `System.IO.FileStream` `Length` propriété de l’objet.
   * Renseignez le tableau d’octets avec les données de flux en appelant la `System.IO.FileStream` `Read` méthode de l’objet et en transmettant le tableau d’octets, la position de départ et la longueur du flux à lire.
   * Renseignez l’ `BLOB` objet en affectant à sa `MTOM` propriété le contenu du tableau d’octets.

1. Convertissez le fichier en document PDF.

   Convertissez le fichier en document PDF en appelant la `GeneratePDFServiceService` `CreatePDF2` méthode de l’objet et en transmettant les valeurs suivantes :

   * Objet `BLOB` représentant le fichier à convertir.
   * Chaîne contenant l’extension de fichier.
   * Objet `java.lang.String` contenant les paramètres de type de fichier à utiliser dans la conversion. Les paramètres de type de fichier fournissent des paramètres de conversion pour différents types de fichier, tels que .doc ou .xls.
   * Objet chaîne contenant les paramètres PDF à utiliser. You can specify `Standard`.
   * Objet chaîne contenant les paramètres de sécurité à utiliser. You can specify `No Security`.
   * Objet facultatif `BLOB` contenant les paramètres à appliquer lors de la génération du document PDF.
   * Objet facultatif `BLOB` contenant des informations de métadonnées à appliquer au document PDF.
   * Paramètre de sortie de type `BLOB` renseigné par la `CreatePDF2` méthode. La `CreatePDF2` méthode remplit cet objet avec le document converti. (Cette valeur de paramètre est requise uniquement pour l’appel de service Web).
   * Paramètre de sortie de type `BLOB` renseigné par la `CreatePDF2` méthode. La `CreatePDF2` méthode remplit cet objet avec le document journal. (Cette valeur de paramètre est requise uniquement pour l’appel de service Web).

1. Récupérez les résultats.

   * Récupérez le document PDF converti en attribuant le `BLOB` `MTOM` champ de l’objet à un tableau d’octets. Le tableau d’octets représente le document PDF converti. Veillez à utiliser l’ `BLOB` objet utilisé comme paramètre de sortie pour la `createPDF2` méthode.
   * Créez un `System.IO.FileStream` objet en appelant son constructeur et en transmettant une valeur de chaîne représentant l’emplacement du fichier du document PDF converti.
   * Create a `System.IO.BinaryWriter` object by invoking its constructor and passing the `System.IO.FileStream` object.
   * Ecrivez le contenu du tableau d’octets dans un fichier PDF en appelant la `System.IO.BinaryWriter` `Write` méthode de l’objet et en transmettant le tableau d’octets.

**Voir également**

[Résumé des étapes](converting-file-formats-pdf.md#summary-of-steps)

[Appel d’AEM Forms à l’aide de MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Appel d’AEM Forms à l’aide de SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Conversion de documents HTML en documents PDF {#converting-html-documents-to-pdf-documents}

Cette section décrit l’utilisation de l’API Generate PDF pour convertir par programmation des documents HTML en documents PDF.

>[!NOTE]
>
>For more information about the Generate PDF service, see [Services Reference for AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Résumé des étapes {#summary_of_steps-1}

Pour convertir un document HTML en document PDF, procédez comme suit :

1. Incluez des fichiers de projet.
1. Créez un client Generate PDF.
1. Récupérez le contenu HTML à convertir en document PDF.
1. Convertissez le contenu HTML en document PDF.
1. Récupérez les résultats.

**Inclure les fichiers de projet**

Incluez les fichiers nécessaires dans votre projet de développement. Si vous créez une application cliente à l’aide de Java, incluez les fichiers JAR nécessaires. Si vous utilisez des services Web, veillez à inclure les fichiers proxy.

**Création d’un client Generate PDF**

Avant de pouvoir exécuter une opération de génération de PDF par programmation, vous devez créer un client de service Generate PDF. Si vous utilisez l’API Java, créez un `GeneratePdfServiceClient` objet. Si vous utilisez l’API du service Web, créez une `GeneratePDFServiceService`.

**Récupérer le contenu HTML à convertir en document PDF**

Référence du contenu HTML à convertir en document PDF. Vous pouvez référencer du contenu HTML, tel qu’un fichier HTML ou un contenu HTML accessible à l’aide d’une URL.

**Conversion du contenu HTML en document PDF**

Après avoir créé le client de service, vous pouvez appeler l’opération de création de PDF appropriée. Cette opération nécessite des informations sur le document à convertir, y compris le chemin d’accès au document cible.

**Récupérer les résultats**

Une fois le contenu HTML converti en document PDF, vous pouvez récupérer les résultats et enregistrer le document PDF.

**Voir également**

[Conversion de contenu HTML en document PDF à l’aide de l’API Java](converting-file-formats-pdf.md#convert-html-content-to-a-pdf-document-using-the-java-api)

[Conversion de contenu HTML en document PDF à l’aide de l’API du service Web](converting-file-formats-pdf.md#convert-html-content-to-a-pdf-document-using-the-web-service-api)

[Inclusion des fichiers de bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Démarrage rapide de l’API du service Generate PDF](/help/forms/developing/generate-pdf-service-java-api.md#generate-pdf-service-java-api-quick-start-soap)

### Conversion de contenu HTML en document PDF à l’aide de l’API Java {#convert-html-content-to-a-pdf-document-using-the-java-api}

Convertir un document HTML en document PDF à l’aide de l’API Generate PDF (Java) :

1. Incluez des fichiers de projet.

   Incluez des fichiers JAR client, tels que adobe-generatepdf-client.jar, dans le chemin de classe de votre projet Java.

1. Créez un client Generate PDF.

   Créez un `GeneratePdfServiceClient` objet en utilisant son constructeur et en transmettant un `ServiceClientFactory` objet contenant des propriétés de connexion.

1. Récupérez le contenu HTML à convertir en document PDF.

   Récupérez du contenu HTML en créant une variable de chaîne et en attribuant une URL pointant vers du contenu HTML.

1. Convertissez le contenu HTML en document PDF.

   Appelez la méthode `GeneratePdfServiceClient` `htmlToPDF2` de l’objet et transmettez les valeurs suivantes :

   * Objet `java.lang.String` contenant l’URL du fichier HTML à convertir.
   * Objet `java.lang.String` contenant les paramètres de type de fichier à utiliser dans la conversion. Les paramètres de type de fichier peuvent inclure des niveaux d’indexation.
   * Objet `java.lang.String` contenant le nom des paramètres de sécurité à utiliser.
   * Objet facultatif `com.adobe.idp.Document` contenant les paramètres à appliquer lors de la génération du document PDF. Si ces informations ne sont pas fournies, les paramètres sont automatiquement choisis en fonction des trois paramètres précédents.
   * Objet facultatif `com.adobe.idp.Document` contenant des informations de métadonnées à appliquer au document PDF.

1. Récupérez les résultats.

   La `htmlToPDF2` méthode renvoie un `HtmlToPdfResult` objet contenant le nouveau document PDF généré. Pour obtenir le document PDF nouvellement créé, procédez comme suit :

   * Appelez la méthode `HtmlToPdfResult` `getCreatedDocument` de l’objet. Renvoie un `com.adobe.idp.Document` objet.
   * Appelez la méthode `com.adobe.idp.Document` `copyToFile` de l’objet pour extraire le document PDF de l’objet créé à l’étape précédente.

**Voir également**

[Conversion de documents HTML en documents PDF](converting-file-formats-pdf.md#converting-html-documents-to-pdf-documents)

[Démarrage rapide (mode SOAP) : Conversion de contenu HTML en document PDF à l’aide de l’API Java](/help/forms/developing/generate-pdf-service-java-api.md#quick-start-soap-mode-converting-html-content-to-a-pdf-document-using-the-java-api)

[Démarrage rapide (mode SOAP) : Conversion de contenu HTML en document PDF à l’aide de l’API Java](/help/forms/developing/generate-pdf-service-java-api.md#quick-start-soap-mode-converting-html-content-to-a-pdf-document-using-the-java-api)

[Inclusion des fichiers de bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Conversion de contenu HTML en document PDF à l’aide de l’API du service Web {#convert-html-content-to-a-pdf-document-using-the-web-service-api}

Convertissez du contenu HTML en document PDF à l’aide de l’API Generate PDF (service Web) :

1. Incluez des fichiers de projet.

   Créez un projet Microsoft .NET qui utilise MTOM. Veillez à utiliser la définition WSDL suivante : `http://localhost:8080/soap/services/GeneratePDFService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Remplacez `localhost` par l’adresse IP du serveur hébergeant AEM Forms.

1. Créez un client Generate PDF.

   * Create a `GeneratePDFServiceClient` object by using its default constructor.
   * Create a `GeneratePDFServiceClient.Endpoint.Address` object by using the `System.ServiceModel.EndpointAddress` constructor. Transmettez une valeur de chaîne qui spécifie le WSDL au service AEM Forms (par exemple, `http://localhost:8080/soap/services/GeneratePDFService?blob=mtom`). Vous n’avez pas besoin d’utiliser l’ `lc_version` attribut. Spécifiez toutefois `?blob=mtom`.
   * Créez un `System.ServiceModel.BasicHttpBinding` objet en obtenant la valeur du `GeneratePDFServiceClient.Endpoint.Binding` champ. Convertissez la valeur de retour en `BasicHttpBinding`.
   * Définissez le `System.ServiceModel.BasicHttpBinding` champ de l’ `MessageEncoding` objet sur `WSMessageEncoding.Mtom`. Cette valeur garantit l’utilisation de MTOM.
   * Activez l’authentification HTTP de base en effectuant les tâches suivantes :

      * Attribuez le nom d’utilisateur d’AEM forms au champ `GeneratePDFServiceClient.ClientCredentials.UserName.UserName`.
      * Attribuez la valeur de mot de passe correspondante au champ `GeneratePDFServiceClient.ClientCredentials.UserName.Password`.
      * Attribuez la valeur constante `HttpClientCredentialType.Basic` au champ `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Attribuez la valeur constante `BasicHttpSecurityMode.TransportCredentialOnly` au champ `BasicHttpBindingSecurity.Security.Mode`.

1. Récupérez le contenu HTML à convertir en document PDF.

   Récupérez du contenu HTML en créant une variable de chaîne et en attribuant une URL pointant vers du contenu HTML.

1. Convertissez le contenu HTML en document PDF.

   Convertissez le contenu HTML en document PDF en appelant la `GeneratePDFServiceService` `HtmlToPDF2` méthode de l’objet et en transmettant les valeurs suivantes :

   * Chaîne contenant le contenu HTML à convertir.
   * Objet `java.lang.String` contenant les paramètres de type de fichier à utiliser dans la conversion.
   * Objet chaîne contenant les paramètres de sécurité à utiliser.
   * Objet facultatif `BLOB` contenant les paramètres à appliquer lors de la génération du document PDF.
   * Objet facultatif `BLOB` contenant des informations de métadonnées à appliquer au document PDF.
   * Paramètre de sortie de type `BLOB` renseigné par la `CreatePDF2` méthode. La `CreatePDF2` méthode remplit cet objet avec le document converti. (Cette valeur de paramètre est requise uniquement pour l’appel de service Web).

1. Récupérez les résultats.

   * Récupérez le document PDF converti en attribuant le `BLOB` `MTOM` champ de l’objet à un tableau d’octets. Le tableau d’octets représente le document PDF converti. Veillez à utiliser l’ `BLOB` objet utilisé comme paramètre de sortie pour la `HtmlToPDF2` méthode.
   * Créez un `System.IO.FileStream` objet en appelant son constructeur et en transmettant une valeur de chaîne représentant l’emplacement du fichier du document PDF converti.
   * Create a `System.IO.BinaryWriter` object by invoking its constructor and passing the `System.IO.FileStream` object.
   * Ecrivez le contenu du tableau d’octets dans un fichier PDF en appelant la `System.IO.BinaryWriter` `Write` méthode de l’objet et en transmettant le tableau d’octets.

**Voir également**

[Conversion de documents HTML en documents PDF](converting-file-formats-pdf.md#converting-html-documents-to-pdf-documents)

[Appel d’AEM Forms à l’aide de MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Appel d’AEM Forms à l’aide de SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Conversion de documents PDF dans des formats autres que des images {#converting-pdf-documents-to-non-image-formats}

Cette section décrit comment vous pouvez utiliser l’API Java Generate PDF et l’API de service Web pour convertir par programmation un document PDF en fichier RTF, qui est un exemple de format autre qu’une image. Les autres formats autres que les images sont HTML, text, DOC et EPS. Lors de la conversion d’un document PDF au format RTF, assurez-vous que le document PDF ne contient aucun élément de formulaire, tel qu’un bouton d’envoi. Les éléments de formulaire ne sont pas convertis.

>[!NOTE]
>
>For more information about the Generate PDF service, see [Services Reference for AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Résumé des étapes {#summary_of_steps-2}

Pour convertir un document PDF en l’un des types pris en charge, procédez comme suit :

1. Incluez des fichiers de projet.
1. Créez un client Generate PDF.
1. Récupérez le document PDF à convertir.
1. Convertir le document PDF.
1. Enregistrez le fichier converti.

**Inclure les fichiers de projet**

Incluez les fichiers nécessaires dans votre projet de développement. Si vous créez une application cliente à l’aide de Java, incluez les fichiers JAR nécessaires. Si vous utilisez des services Web, veillez à inclure les fichiers proxy.

**Création d’un client Generate PDF**

Avant de pouvoir exécuter une opération de génération de PDF par programmation, vous devez créer un client de service Generate PDF. Si vous utilisez l’API Java, créez un `GeneratePdfServiceClient` objet. Si vous utilisez l’API du service Web, créez un `GeneratePDFServiceService` objet.

**Récupérer le document PDF à convertir**

Récupérez le document PDF à convertir dans un format autre qu’une image.

**Conversion du document PDF**

Après avoir créé le client de service, vous pouvez appeler l’opération d’exportation PDF. Cette opération nécessite des informations sur le document à convertir, y compris le chemin d’accès au document cible.

**Enregistrer le fichier converti**

Enregistrez le fichier converti. Par exemple, si vous convertissez un document PDF en fichier RTF, enregistrez le document converti dans un fichier RTF.

**Voir également**

[Conversion d’un document PDF en fichier RTF à l’aide de l’API Java](converting-file-formats-pdf.md#convert-a-pdf-document-to-a-rtf-file-using-the-java-api)

[Conversion d’un document PDF en fichier RTF à l’aide de l’API du service Web](converting-file-formats-pdf.md#convert-a-pdf-document-to-a-rtf-file-using-the-web-service-api)

[Inclusion des fichiers de bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Démarrage rapide de l’API du service Generate PDF](/help/forms/developing/generate-pdf-service-java-api.md#generate-pdf-service-java-api-quick-start-soap)

### Conversion d’un document PDF en fichier RTF à l’aide de l’API Java {#convert-a-pdf-document-to-a-rtf-file-using-the-java-api}

Convertir un document PDF en fichier RTF à l’aide de l’API Generate PDF (Java) :

1. Incluez des fichiers de projet.

   Incluez des fichiers JAR client, tels que adobe-generatepdf-client.jar, dans le chemin de classe de votre projet Java.

1. Créez un client Generate PDF.

   Créez un `GeneratePdfServiceClient` objet en utilisant son constructeur et en transmettant un `ServiceClientFactory` objet contenant des propriétés de connexion.

1. Récupérez le document PDF à convertir.

   * Créez un `java.io.FileInputStream` objet représentant le document PDF à convertir à l’aide de son constructeur. Transmettez une valeur de chaîne qui spécifie l’emplacement du document PDF.
   * Créez un objet `com.adobe.idp.Document` en utilisant son constructeur et en transmettant l’objet `java.io.FileInputStream`. 

1. Convertir le document PDF.

   Appelez la méthode `GeneratePdfServiceClient` `exportPDF2` de l’objet et transmettez les valeurs suivantes :

   * Objet `com.adobe.idp.Document` représentant le fichier PDF à convertir.
   * Objet `java.lang.String` contenant le nom du fichier à convertir.
   * Objet `java.lang.String` contenant le nom des paramètres Adobe PDF.
   * Objet `ConvertPDFFormatType` spécifiant le type de fichier cible de la conversion.
   * Objet facultatif `com.adobe.idp.Document` contenant les paramètres à appliquer lors de la génération du document PDF.
   La `exportPDF2` méthode renvoie un `ExportPDFResult` objet contenant le fichier converti.

1. Convertir le document PDF.

   Pour obtenir le fichier nouvellement créé, procédez comme suit :

   * Appelez la méthode `ExportPDFResult` `getConvertedDocument` de l’objet. Renvoie un `com.adobe.idp.Document` objet.
   * Appelez la méthode `com.adobe.idp.Document` `copyToFile` de l’objet pour extraire le nouveau document.

**Voir également**

[Résumé des étapes](converting-file-formats-pdf.md#summary-of-steps)

[Démarrage rapide (mode SOAP) : Conversion de contenu HTML en document PDF à l’aide de l’API Java](/help/forms/developing/generate-pdf-service-java-api.md#quick-start-soap-mode-converting-html-content-to-a-pdf-document-using-the-java-api)

[Inclusion des fichiers de bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Conversion d’un document PDF en fichier RTF à l’aide de l’API du service Web {#convert-a-pdf-document-to-a-rtf-file-using-the-web-service-api}

Convertissez un document PDF en fichier RTF à l’aide de l’API Generate PDF (service Web) :

1. Incluez des fichiers de projet.

   Créez un projet Microsoft .NET qui utilise MTOM. Veillez à utiliser la définition WSDL suivante : `http://localhost:8080/soap/services/GeneratePDFService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Remplacez `localhost` par l’adresse IP du serveur hébergeant AEM Forms.

1. Créez un client Generate PDf.

   * Create a `GeneratePDFServiceClient` object by using its default constructor.
   * Create a `GeneratePDFServiceClient.Endpoint.Address` object by using the `System.ServiceModel.EndpointAddress` constructor. Transmettez une valeur de chaîne qui spécifie le WSDL au service AEM Forms (par exemple, `http://localhost:8080/soap/services/GeneratePDFService?blob=mtom`). Vous n’avez pas besoin d’utiliser l’ `lc_version` attribut. Spécifiez toutefois `?blob=mtom`.
   * Créez un `System.ServiceModel.BasicHttpBinding` objet en obtenant la valeur du `GeneratePDFServiceClient.Endpoint.Binding` champ. Convertissez la valeur de retour en `BasicHttpBinding`.
   * Définissez le `System.ServiceModel.BasicHttpBinding` champ de l’ `MessageEncoding` objet sur `WSMessageEncoding.Mtom`. Cette valeur garantit l’utilisation de MTOM.
   * Activez l’authentification HTTP de base en effectuant les tâches suivantes :

      * Attribuez le nom d’utilisateur d’AEM forms au champ `GeneratePDFServiceClient.ClientCredentials.UserName.UserName`.
      * Attribuez la valeur de mot de passe correspondante au champ `GeneratePDFServiceClient.ClientCredentials.UserName.Password`.
      * Attribuez la valeur constante `HttpClientCredentialType.Basic` au champ `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Attribuez la valeur constante `BasicHttpSecurityMode.TransportCredentialOnly` au champ `BasicHttpBindingSecurity.Security.Mode`.

1. Récupérez le document PDF à convertir.

   * Créez un objet `BLOB` en utilisant son constructeur. L’ `BLOB` objet est utilisé pour stocker un document PDF converti.
   * Créez un `System.IO.FileStream` objet en appelant son constructeur et en transmettant une valeur de chaîne représentant l’emplacement du fichier PDF et le mode d’ouverture du fichier.
   * Créez un tableau d’octets qui stocke le contenu de l’ `System.IO.FileStream` objet. Vous pouvez déterminer la taille du tableau d’octets en obtenant la `System.IO.FileStream` `Length` propriété de l’objet.
   * Renseignez le tableau d’octets avec les données de flux en appelant la `System.IO.FileStream` `Read` méthode de l’objet et en transmettant le tableau d’octets, la position de départ et la longueur du flux à lire.
   * Renseignez l’ `BLOB` objet en affectant à sa `MTOM` propriété le contenu du tableau d’octets.

1. Convertir le document PDF.

   Appelez la méthode `GeneratePDFServiceServiceWse` `ExportPDF2` de l’objet et transmettez les valeurs suivantes :

   * Objet `BLOB` représentant le fichier PDF à convertir.
   * Chaîne contenant le nom du chemin d’accès du fichier à convertir.
   * Objet `java.lang.String` spécifiant l’emplacement du fichier.
   * Objet chaîne qui spécifie le type de fichier cible de la conversion. Specify `RTF`.
   * Objet facultatif `BLOB` contenant les paramètres à appliquer lors de la génération du document PDF.
   * Paramètre de sortie de type `BLOB` renseigné par la `ExportPDF2` méthode. La `ExportPDF2` méthode remplit cet objet avec le document converti. (Cette valeur de paramètre est requise uniquement pour l’appel de service Web).

1. Enregistrez le fichier converti.

   * Récupérez le document RTF converti en affectant le champ `BLOB` `MTOM` de l’objet à un tableau d’octets. Le tableau d’octets représente le document RTF converti. Veillez à utiliser l’ `BLOB` objet utilisé comme paramètre de sortie pour la `ExportPDF2` méthode.
   * Create a `System.IO.FileStream` object by invoking its constructor. Transmettez une valeur de chaîne qui représente l’emplacement du fichier RTF.
   * Create a `System.IO.BinaryWriter` object by invoking its constructor and passing the `System.IO.FileStream` object.
   * Ecrivez le contenu du tableau d’octets dans un fichier RTF en appelant la méthode `System.IO.BinaryWriter` `Write` de l’objet et en transmettant le tableau d’octets.

**Voir également**

[Résumé des étapes](converting-file-formats-pdf.md#summary-of-steps)

[Appel d’AEM Forms à l’aide de MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Appel d’AEM Forms à l’aide de SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Ajout de la prise en charge de formats de fichier natifs supplémentaires {#adding-support-for-additional-native-file-formats}

Cette section explique comment ajouter la prise en charge de formats de fichier natifs supplémentaires. Il fournit un aperçu des interactions entre le service Generate PDF et les applications natives utilisées par ce service pour convertir des formats de fichier natifs en PDF.

Cette section explique également ce qui suit :

* Comment modifier la réponse fournie par le service Generate PDF aux applications natives que ce produit utilise déjà pour convertir des formats de fichier natifs en PDF
* Interactions entre le service Generate PDF, le composant AppMon (Generate PDF Application Monitor) du service Generate PDF et les applications natives, telles que Microsoft Word
* Les rôles que les grammaires XML jouent dans ces interactions

### Interactions de composant {#component-interactions}

Le service Generate PDF convertit les formats de fichier natifs en appelant l’application associée au format de fichier, puis en interagissant avec l’application pour imprimer le document à l’aide de l’imprimante par défaut. L’imprimante par défaut doit être configurée en tant qu’imprimante Adobe PDF.

Cette illustration présente les composants et les pilotes impliqués dans la prise en charge des applications natives. Il mentionne également les grammaires XML qui influencent les interactions.

Interactions de composants pour la conversion de fichiers natifs

Ce document utilise le terme application ** native pour indiquer l’application utilisée pour produire un format de fichier natif, tel que Microsoft Word.

*AppMon* est un composant d’entreprise qui interagit avec une application native de la même manière qu’un utilisateur navigue dans les boîtes de dialogue présentées par cette application. Les grammaires XML utilisés par AppMon pour indiquer à une application, telle que Microsoft Word, d’ouvrir et d’imprimer un fichier impliquent les tâches suivantes :

1. Pour ouvrir le fichier, choisissez Fichier > Ouvrir
1. Vérification de l&#39;affichage de la boîte de dialogue Ouvrir ; dans le cas contraire, gestion de l’erreur
1. Fourniture du nom de fichier dans le champ Nom de fichier, puis clic sur le bouton Ouvrir
1. Vérification de l’ouverture effective du fichier
1. Ouverture de la boîte de dialogue Imprimer en sélectionnant Fichier > Imprimer
1. Vérification de l’affichage de la boîte de dialogue Imprimer

AppMon utilise des API Win32 standard pour interagir avec des applications tierces afin de transférer des événements d’interface utilisateur tels que des touches de raccourci et des clics de la souris, ce qui s’avère utile pour contrôler ces applications afin de produire des fichiers PDF à partir de ces dernières.

En raison d’une limitation de ces API Win32, AppMon ne peut pas distribuer ces événements d’interface utilisateur à certains types de fenêtres, tels que les barres de menus flottantes (présentes dans certaines applications, comme TextPad), ni certains types de boîtes de dialogue dont le contenu ne peut pas être récupéré à l’aide des API Win32.

Il est facile d&#39;identifier visuellement une barre de menus flottante ; toutefois, il pourrait ne pas être possible d&#39;identifier les types spéciaux de boîtes de dialogue simplement par inspection visuelle. Vous devez disposer d’une application tierce, telle que Microsoft Spy++ (qui fait partie de l’environnement de développement Microsoft Visual C++) ou de son WinID équivalent (qui peut être téléchargée gratuitement à partir de [https://www.dennisbabkin.com/php/download.php?what=WinID](https://www.dennisbabkin.com/php/download.php?what=WinID)), pour examiner une boîte de dialogue afin de déterminer si AppMon serait en mesure d’interagir avec elle à l’aide des API Win32 standard.

Si WinID est en mesure d&#39;extraire le contenu de la boîte de dialogue, tel que le texte, les sous-fenêtres, l&#39;identifiant de classe de fenêtre, etc., AppMon peut également faire de même.

Ce tableau répertorie le type d’informations utilisées pour imprimer des formats de fichier natifs.

<table>
 <thead>
  <tr>
   <th><p>Type d'information</p></th>
   <th><p>Description</p></th>
   <th><p>Modification/création d’entrées liées à des fichiers natifs </p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>Paramètres administratifs </p></td>
   <td><p>Inclut des paramètres PDF, des paramètres de sécurité et des paramètres de type de fichier. </p><p>Les paramètres de type de fichier associent des extensions de nom de fichier aux applications natives correspondantes. Les paramètres de type de fichier spécifient également les paramètres d’application natifs utilisés pour imprimer les fichiers natifs. </p></td>
   <td><p>Pour modifier les paramètres d’une application native déjà prise en charge, l’administrateur système définit les paramètres de type de fichier dans Administration Console. </p><p>Pour ajouter la prise en charge d’un nouveau format de fichier natif, vous devez modifier manuellement le fichier. (voir <a href="converting-file-formats-pdf.md#adding-or-modifying-support-for-a-native-file-format">Ajout ou modification de la prise en charge d’un format</a>de fichier natif). </p></td>
  </tr>
  <tr>
   <td><p>Script </p></td>
   <td><p>Spécifie les interactions entre le service Generate PDF et une application native. Ces interactions orientent généralement l’application à imprimer un fichier vers le pilote Adobe PDF. </p><p>Le script contient des instructions qui demandent à l’application native d’ouvrir des boîtes de dialogue spécifiques et qui fournissent des réponses spécifiques aux champs et aux boutons de ces boîtes de dialogue. </p></td>
   <td><p>Le service Generate PDF inclut des fichiers de script pour toutes les applications natives prises en charge. Vous pouvez modifier ces fichiers à l’aide d’une application de modification XML.</p><p>Pour ajouter la prise en charge d’une nouvelle application native, vous devez créer un fichier de script. (voir <a href="converting-file-formats-pdf.md#creating-or-modifying-an-additional-dialog-xml-file-for-a-native-application">Création ou modification d’un fichier XML de boîte de dialogue supplémentaire pour une application</a>native). </p></td>
  </tr>
  <tr>
   <td><p>Instructions de la boîte de dialogue Générique </p></td>
   <td><p>Indique comment répondre aux boîtes de dialogue communes à plusieurs applications. Ces boîtes de dialogue sont générées par les systèmes d’exploitation, les applications d’assistance (telles que PDFMaker) et les pilotes. </p><p>Le fichier contenant ces informations est appmon.global.en_US.xml.</p></td>
   <td><p>Ne modifiez pas ce fichier. </p></td>
  </tr>
  <tr>
   <td><p>Instructions de la boîte de dialogue spécifique à l’application</p></td>
   <td><p>Indique comment répondre aux boîtes de dialogue spécifiques à l’application. </p><p>Le fichier qui contient ces informations s’affiche.<i>[appname]</i>.dialog.<i>[locale]</i>.xml (par exemple, appmon.word.en_US.xml).</p></td>
   <td><p>Ne modifiez pas ce fichier. </p><p>Pour ajouter des instructions de boîte de dialogue pour une nouvelle application native, voir <a href="converting-file-formats-pdf.md#creating_or_modifying_an_additional_dialog_xml_file_for_a_native_application">Création ou modification d’un fichier XML de boîte de dialogue supplémentaire pour une application</a>native.</p></td>
  </tr>
  <tr>
   <td><p>Autres instructions de la boîte de dialogue spécifique à l’application </p></td>
   <td><p>Spécifie les valeurs de remplacement et les ajouts aux instructions de la boîte de dialogue spécifique à l’application. La section présente un exemple de ces informations. </p><p>Le fichier qui contient ces informations s’affiche.<i>[appname]</i>.addition.<i>[locale]</i>.xml. Par exemple, appmon.addition.en_US.xml.</p></td>
   <td><p>Les fichiers de ce type peuvent être créés et modifiés à l’aide d’une application de modification XML. (voir <a href="converting-file-formats-pdf.md#creating-or-modifying-an-additional-dialog-xml-file-for-a-native-application">Création ou modification d’un fichier XML de boîte de dialogue supplémentaire pour une application</a>native). </p><p><strong>Important</strong>: Vous devez créer des instructions de boîte de dialogue spécifiques à l’application supplémentaires pour chaque application native prise en charge par votre serveur. </p></td>
  </tr>
 </tbody>
</table>

### A propos du script et des fichiers XML de boîte de dialogue {#about-the-script-and-dialog-xml-files}

Les fichiers XML de script demandent au service Generate PDF de naviguer dans les boîtes de dialogue de l’application de la même manière qu’un utilisateur navigue dans les boîtes de dialogue de l’application. Les fichiers XML de script demandent également au service Generate PDF de répondre aux boîtes de dialogue en effectuant des actions telles que l’appui sur les boutons, la sélection ou la désélection des cases à cocher ou la sélection des options de menu.

En revanche, les fichiers XML de boîte de dialogue répondent simplement aux boîtes de dialogue avec les mêmes types d’actions que ceux utilisés dans les fichiers XML de script.

#### Terminologie des éléments de la boîte de dialogue et de la fenêtre {#dialog-box-and-window-element-terminology}

Cette section et la section suivante utilisent une terminologie différente pour les boîtes de dialogue et les composants qu’elles contiennent, selon la perspective décrite. Les composants de la boîte de dialogue sont des éléments tels que des boutons, des champs et des zones de liste modifiable.

Lorsque cette section et la section suivante décrivent les boîtes de dialogue et leurs composants du point de vue d’un utilisateur, des termes tels que *boîte* de dialogue, *bouton*, *champ* et *zone de liste modifiable sont utilisés.*

Lorsque cette section et la section suivante décrivent les boîtes de dialogue et leurs composants du point de vue de leur représentation interne, le terme élément *de* fenêtre est utilisé. La représentation interne des éléments de fenêtre est une hiérarchie, où chaque instance d’élément de fenêtre est identifiée par des libellés. L’instance d’élément de fenêtre décrit également ses caractéristiques physiques et son comportement.

Du point de vue de l’utilisateur, les boîtes de dialogue et leurs composants présentent des comportements différents, certains éléments de la boîte de dialogue étant masqués jusqu’à ce qu’ils soient activés. Du point de vue de la représentation interne, il n&#39;existe aucun problème de comportement de ce genre. Par exemple, la représentation interne d’une boîte de dialogue ressemble à celle des composants qu’elle contient, à l’exception que les composants sont imbriqués dans la boîte de dialogue.

Cette section décrit les éléments XML qui fournissent des instructions à AppMon. Ces éléments ont des noms tels que l’ `dialog` élément et l’ `window` élément. Ce document utilise une police à espacement fixe pour distinguer les éléments XML. L’ `dialog` élément identifie une boîte de dialogue qu’un fichier de script XML peut entraîner pour l’affichage, intentionnel ou non. L’ `window` élément identifie un élément de fenêtre (boîte de dialogue ou composants d’une boîte de dialogue).

#### Hiérarchie {#hierarchy}

Ce diagramme montre la hiérarchie des scripts et des boîtes de dialogue XML. Un fichier XML de script est conforme au schéma script.xsd, qui inclut (au sens XML) le schéma window.xsd. De même, un fichier XML de boîte de dialogue est conforme au schéma dialogs.xsd, qui inclut également le schéma window.xsd.

![as_as_xml_hierarchy](assets/as_as_xml_hierarchy.png)

Hiérarchie du script et du XML de la boîte de dialogue

#### Fichiers XML de script {#script-xml-files}

Un fichier *XML de* script spécifie une série d’étapes qui orientent l’application native vers certains éléments de fenêtre, puis fournissent des réponses à ces éléments. La plupart des réponses sont du texte ou des touches qui correspondent à l’entrée que l’utilisateur doit fournir à un champ, une zone de liste déroulante ou un bouton dans la boîte de dialogue correspondante.

La prise en charge des fichiers XML de script par le service Generate PDF a pour objectif de demander à une application native d’imprimer un fichier natif. Toutefois, les fichiers XML de script peuvent être utilisés pour accomplir toute tâche qu’un utilisateur peut effectuer lors de l’interaction avec les boîtes de dialogue natives de l’application.

Les étapes d’un fichier XML de script sont exécutées dans l’ordre, sans possibilité d’embranchement. Le seul test conditionnel pris en charge est pour le délai d’expiration/la nouvelle tentative, ce qui entraîne l’arrêt d’un script si une étape ne se termine pas correctement dans un délai spécifique et après un nombre spécifique de tentatives.

Outre les étapes séquentielles, les instructions d’une étape sont également exécutées dans l’ordre. Vous devez vous assurer que les étapes et les instructions reflètent l’ordre dans lequel l’utilisateur effectue les mêmes étapes.

Chaque étape d’un fichier XML de script identifie l’élément de fenêtre qui doit apparaître si les instructions de l’étape sont correctement exécutées. Si une boîte de dialogue inattendue s’affiche lors de l’exécution d’une étape de script, le service Generate PDF recherche les fichiers XML de la boîte de dialogue, comme décrit dans la section suivante.

#### Fichiers XML de boîte de dialogue {#dialog-xml-files}

L’exécution d’applications natives affiche différentes boîtes de dialogue, qui s’affichent, que les applications natives soient en mode visible ou invisible. Les boîtes de dialogue peuvent être générées par le système d’exploitation ou par l’application elle-même. Lorsque les applications natives s’exécutent sous le contrôle du service Generate PDF, les boîtes de dialogue du système et des applications natives s’affichent dans une fenêtre invisible.

Un fichier *XML de* boîte de dialogue indique comment le service Generate PDF répond aux boîtes de dialogue du système ou de l’application native. Les fichiers XML de boîte de dialogue permettent au service Generate PDF de répondre aux boîtes de dialogue non sollicitées de manière à faciliter le processus de conversion.

Lorsque le système ou l’application native affiche une boîte de dialogue qui n’est pas gérée par le fichier XML de script en cours d’exécution, le service Generate PDF recherche les fichiers XML de la boîte de dialogue dans cet ordre, en s’arrêtant lorsqu’il trouve une correspondance :

* appmon.*[appname]*.additional.*[locale]*.xml
* appmon.*[appname].[locale]*.xml (ne modifiez pas ce fichier.)
* appmon.global.*[locale]*.xml (ne modifiez pas ce fichier.)

Si le service Generate PDF trouve une correspondance pour la boîte de dialogue, il la ferme en lui envoyant le raccourci clavier ou toute autre action spécifiée pour la boîte de dialogue. Si les instructions de la boîte de dialogue indiquent un message d’abandon, le service Generate PDF met fin à la tâche en cours d’exécution et génère un message d’erreur. Un tel message d’abandon serait spécifié dans l’ `abortMessage` élément de la grammaire XML du script.

Si le service Generate PDF rencontre une boîte de dialogue qui n’est décrite dans aucun des fichiers précédemment répertoriés, le service Generate PDF incorpore la légende de la boîte de dialogue dans l’entrée du fichier journal. La tâche en cours d&#39;exécution arrive à expiration. Vous pouvez ensuite utiliser les informations contenues dans le fichier journal pour rédiger de nouvelles instructions dans le fichier XML de boîte de dialogue supplémentaire pour l’application native.

### Ajout ou modification de la prise en charge d’un format de fichier natif {#adding-or-modifying-support-for-a-native-file-format}

Cette section décrit les tâches que vous devez effectuer pour prendre en charge d’autres formats de fichier natifs ou modifier la prise en charge d’un format de fichier natif déjà pris en charge.

Avant de pouvoir ajouter ou modifier la prise en charge, vous devez exécuter les tâches suivantes.

#### Choix d’un outil d’identification des éléments de fenêtre {#choosing-a-tool-for-identifying-window-elements}

Les fichiers XML de boîte de dialogue et de script nécessitent que vous identifiiez l’élément de fenêtre (boîte de dialogue, champ ou autre composant de boîte de dialogue) auquel répond votre élément de boîte de dialogue ou de script. Par exemple, après qu’un script appelle un menu pour une application native, le script doit identifier l’élément de fenêtre de ce menu auquel des touches ou une action doivent être appliquées.

Vous pouvez facilement identifier une boîte de dialogue par la légende qu’elle affiche dans sa barre de titre. Cependant, vous devez utiliser un outil tel que Microsoft Spy++ pour identifier les éléments de fenêtre de niveau inférieur. Les éléments de la fenêtre de niveau inférieur peuvent être identifiés à l&#39;aide de divers attributs, qui ne sont pas évidents. De plus, chaque application native peut identifier son élément de fenêtre différemment. Il existe donc plusieurs façons d’identifier un élément de fenêtre. Voici l’ordre suggéré pour prendre en compte l’identification des éléments de la fenêtre :

1. Légende elle-même si elle est unique
1. ID de contrôle, qui peut être unique ou non pour une boîte de dialogue donnée
1. Nom de classe, qui peut ou non être unique

N&#39;importe lequel ou une combinaison de ces trois attributs peut être utilisé pour identifier une fenêtre.

Si les attributs n’identifient pas une légende, vous pouvez plutôt identifier un élément de fenêtre en utilisant son index par rapport à son parent. Un *index* spécifie la position de l’élément de fenêtre par rapport à ses éléments de fenêtre frères. Souvent, les index sont le seul moyen d’identifier les zones de liste modifiable.

Tenez compte de ces questions :

* Microsoft Spy++ affiche les légendes à l’aide d’une esperluette (&amp;) afin d’identifier la clé chaude de la légende. Par exemple, Spy++ affiche la légende d’une boîte de dialogue Imprimer sous la forme `Pri&nt`, ce qui indique que la touche *rapide est n*. Les titres de légende dans les fichiers XML de script et de boîte de dialogue doivent omettre les esperluettes.
* Certaines légendes comprennent des sauts de ligne. le service Generate PDF ne peut pas identifier les sauts de ligne. Si une légende comprend un saut de ligne, incluez-en suffisamment pour la différencier des autres options du menu, puis utilisez des expressions régulières pour la partie omise. An example is ( `^Long caption title$`).]. (voir [Utilisation d’expressions régulières dans les attributs](converting-file-formats-pdf.md#using-regular-expressions-in-caption-attributes)de légende).
* Utilisez des entités de caractères (également appelées séquences d’échappement) pour les caractères XML réservés. Par exemple, utilisez `&` pour les esperluettes `<` et `>` pour les symboles inférieur et supérieur à, `&apos;` pour les apostrophes et `&quot;` pour les guillemets.

Si vous prévoyez de travailler sur des fichiers de dialogue ou de script XML, vous devez installer l’application Microsoft Spy++.

#### Déconditionnement des fichiers de boîte de dialogue et de script {#unpackaging-the-dialog-and-script-files}

Les fichiers de boîte de dialogue et de script résident dans le fichier appmondata.jar. Avant de pouvoir modifier ces fichiers ou ajouter de nouveaux fichiers de script ou de boîte de dialogue, vous devez décompresser ce fichier JAR. Supposons, par exemple, que vous souhaitiez ajouter la prise en charge de l’application EditPlus. Vous créez deux fichiers XML, nommés appmon.editplus.script.en_US.xml et appmon.editplus.script.addition.en_US.xml. Ces scripts XML doivent être ajoutés au fichier adobe-appmondata.jar à deux emplacements, comme indiqué ci-dessous :

* adobe-livecycle-native-jboss-x86_win32.ear > adobe-Native2PDFSvc.war\WEB-INF\lib > adobe-native.jar > Native2PDFSvc-native.jar\bin > adobe-appmondata.jar\com\adobe\appmon. Le fichier adobe-livecycle-native-jboss-x86_win32.ear se trouve dans le dossier d’exportation `[AEM forms install directory]\configurationManager`. (si AEM Forms est déployé sur un autre serveur d’applications J2EE, remplacez le fichier adobe-livecycle-native-jboss-x86_win32.ear par le fichier EAR correspondant à votre serveur d’applications J2EE.)
* adobe-generatepdf-dsc.jar > adobe-appmondata.jar\com\adobe\appmon (le fichier adobe-appmondata.jar se trouve dans le fichier adobe-generatepdf-dsc.jar). Le fichier adobe-generatepdf-dsc.jar se trouve dans le `[AEM forms install directory]\deploy` dossier.

Après avoir ajouté ces fichiers XML au fichier adobe-appmondata.jar, vous devez redéployer le composant GeneratePDF. Pour ajouter des fichiers XML de boîte de dialogue et de script au fichier adobe-appmondata.jar, procédez comme suit :

1. A l’aide d’un outil tel que WinZip ou WinRAR, ouvrez le fichier adobe-livecycle-native-jboss-x86_win32.earfile > adobe-Native2PDFSvc.war\WEB-INF\lib > adobe-native.jar > Native2PDFSvc-native.jar\bin > fichier adobe-appmondata.jar.
1. Ajoutez les fichiers XML de boîte de dialogue et de script au fichier appmondata.jar ou modifiez les fichiers XML existants dans ce fichier. (Voir [Création ou modification d’un fichier XML de script pour une](converting-file-formats-pdf.md#creating-or-modifying-a-script-xml-file-for-a-native-application)application native et [Création ou modification d’un fichier XML de boîte de dialogue supplémentaire pour une application](converting-file-formats-pdf.md#creating-or-modifying-an-additional-dialog-xml-file-for-a-native-application)native.)
1. A l’aide d’un outil tel que WinZip ou WinRAR, ouvrez adobe-generatepdf-dsc.jar > adobe-appmondata.jar.
1. Ajoutez les fichiers XML de boîte de dialogue et de script au fichier appmondata.jar ou modifiez les fichiers XML existants dans ce fichier. (Voir [Création ou modification d’un fichier XML de script pour une](converting-file-formats-pdf.md#creating-or-modifying-a-script-xml-file-for-a-native-application)application native et [Création ou modification d’un fichier XML de boîte de dialogue supplémentaire pour une application](converting-file-formats-pdf.md#creating-or-modifying-an-additional-dialog-xml-file-for-a-native-application)native.) Après avoir ajouté les fichiers XML au fichier adobe-appmondata.jar, importez le nouveau fichier adobe-appmondata.jar dans le fichier adobe-generatepdf-dsc.jar.
1. Si vous avez ajouté la prise en charge d’un format de fichier natif supplémentaire, créez une variable d’environnement système qui fournit le chemin d’accès de l’application (voir [Création d’une variable d’environnement pour localiser l’application](converting-file-formats-pdf.md#creating-an-environment-variable-to-locate-the-native-application)native).

**Pour redéployer le composant GeneratePDF**

1. Connectez-vous à Workbench.
1. Select **Window** > **Show Views** > **Components**. Cette action ajoute la vue Composants à Workbench.
1. Cliquez avec le bouton droit sur le composant GeneratePDF, puis sélectionnez **Arrêter le composant**.
1. Une fois le composant arrêté, cliquez avec le bouton droit de la souris et sélectionnez Désinstaller le composant pour le supprimer.
1. Right-click the **Components** icon and select **Install Component**.
1. Recherchez et sélectionnez le fichier adobe-generatepdf-dsc.jar modifié, puis cliquez sur Ouvrir. Un carré rouge apparaît en regard du composant GeneratePDF.
1. Développez le composant GeneratePDF, sélectionnez Descripteurs de service, puis cliquez avec le bouton droit sur GeneratePDFService et sélectionnez Activer le service.
1. Dans la boîte de dialogue de configuration qui s’affiche, saisissez les valeurs de configuration applicables. Si vous laissez ces valeurs vides, les valeurs de configuration par défaut sont utilisées.
1. Cliquez avec le bouton droit de la souris sur GeneratePDF et sélectionnez Démarrer le composant.
1. Développez les services actifs. Une flèche verte apparaît en regard du nom du service s’il est en cours d’exécution. Sinon, le service est à l’état arrêté.
1. Si le service est à l’état arrêté, cliquez avec le bouton droit sur le nom du service et sélectionnez Démarrer le service.

### Création ou modification d’un fichier XML de script pour une application native {#creating-or-modifying-a-script-xml-file-for-a-native-application}

Si vous souhaitez diriger des fichiers vers une nouvelle application native, vous devez créer un fichier XML de script pour cette application. Si vous souhaitez modifier la manière dont le service Generate PDF interagit avec une application native déjà prise en charge, vous devez modifier le script de cette application.

Le script contient des instructions qui parcourent les éléments de fenêtre de l’application native et qui fournissent des réponses spécifiques à ces éléments. Le fichier contenant ces informations est `appmon.[appname]``.script.[locale].xml`. Par exemple, appmon.notes.script.en_US.xml.

#### Identification des étapes que le script doit exécuter {#identifying-steps-the-script-must-execute}

A l’aide de l’application native, déterminez les éléments de fenêtre à parcourir et chaque réponse à apporter pour imprimer le document. Notez les boîtes de dialogue qui résultent d’une réponse. Les étapes sont similaires aux étapes suivantes :

1. Choisissez Fichier > Ouvrir.
1. Spécifiez le chemin, puis cliquez sur Ouvrir.
1. Choisissez Fichier > Imprimer dans la barre de menus.
1. Spécifiez les propriétés requises pour l’imprimante.
1. Sélectionnez Imprimer et attendez l’affichage de la boîte de dialogue Enregistrer sous. La boîte de dialogue Enregistrer sous est requise pour que le service Generate PDF indique la destination du fichier PDF.

#### Identification des boîtes de dialogue spécifiées dans les attributs de légende {#identifying-the-dialogs-specified-in-caption-attributes}

Utilisez Microsoft Spy++ pour obtenir les identités des propriétés des éléments de fenêtre dans l’application native. Vous devez avoir ces identités pour écrire des scripts.

#### Utilisation d’expressions régulières dans les attributs de légende {#using-regular-expressions-in-caption-attributes}

Vous pouvez utiliser des expressions régulières dans les spécifications de légende. Le service Generate PDF utilise la `java.util.regex.Matcher` classe pour prendre en charge les expressions régulières. Cet utilitaire prend en charge les expressions régulières décrites dans `java.util.regex.Pattern`. (Rendez-vous sur le site Web Java à l’adresse [https://java.sun.com/j2se/1.4.2/docs/api/java/util/regex/Pattern.html](https://java.sun.com/j2se/1.4.2/docs/api/java/util/regex/Pattern.html).)

**Expression régulière prenant en compte le nom de fichier placé en préfixe sur le Bloc-notes dans la bannière du Bloc-notes**

```as3
 <!-- The regular expression ".*Notepad" means any number of non-terminating characters followed by Notepad. -->
 <step>
     <expectedWindow>
         <window caption=".*Notepad"/>
     </expectedWindow>
 </step>
```

**Expression régulière différenciant l’impression de la configuration de l’impression**

```as3
 <!-- This regular expression differentiates the Print dialog box from the Print Setup dialog box. The "^" specifies the beginning of the line, and the "$" specifies the end of the line. -->
 <windowList>
     <window controlID="0x01" caption="^Print$" action="press"/>
 </windowList>
```

#### Ordre des éléments window et windowList {#ordering-the-window-and-windowlist-elements}

Vous devez trier `window` et `windowList` les éléments comme suit :

* Lorsque plusieurs `window` éléments apparaissent en tant qu’enfants dans un `windowList` ou `dialog` élément, ordonnez ces `window` éléments dans l’ordre décroissant, avec les longueurs des `caption` noms indiquant la position dans l’ordre.
* Lorsque plusieurs `windowList` éléments apparaissent dans un `window` élément, ordonnez ces `windowList` éléments dans l’ordre décroissant, avec les longueurs des attributs du premier `caption` `indexes/`élément indiquant la position dans l’ordre.

**Ordre des éléments de fenêtre dans un fichier de boîte de dialogue**

```as3
 <!-- The caption attribute in the following window element is 40 characters long. It is the longest caption in this example, so its parent window element appears before the others. -->
 <window caption="Unexpected Failure in DebugActiveProcess">
     <…>
 </window>

 <!-- Caption length is 33 characters. -->
 <window caption="Adobe Acrobat - License Agreement">
     <…>
 </window>

 <!-- Caption length is 33 characters. -->
 <window caption="Microsoft Visual.*Runtime Library">
     <…>
 </window>

 <!-- The caption attribute in the following window element is 28 characters long. It is the shortest caption in this example, so its parent window element appears after the others. -->
 <window caption="Adobe Acrobat - Registration">
     <…>
 </window>
```

**Ordre des éléments de la fenêtre dans un élément windowList**

```as3
 <!-- The caption attribute in the following indexes element is 56 characters long. It is the longest caption in this example, so its parent window element appears before the others. -->
 <windowList>
     <window caption="Can&apos;t exit design mode because.* cannot be created"/>
     <window className="Button" caption="OK" action="press"/>
 </windowList>
 <windowList>
     <window caption="Do you want to continue loading the project?"/>
     <window className="Button" caption="No" action="press"/>
 </windowList>
 <windowList>
     <window caption="The macros in this project are disabled"/>
     <window className="Button" caption="OK" action="press"/>
 </windowList>
```

### Création ou modification d’un fichier XML de boîte de dialogue supplémentaire pour une application native {#creating-or-modifying-an-additional-dialog-xml-file-for-a-native-application}

Si vous créez un script pour une application native qui n’était pas prise en charge précédemment, vous devez également créer un fichier XML de boîte de dialogue supplémentaire pour cette application. Chaque application native utilisée par AppMon ne doit comporter qu’un seul fichier XML de boîte de dialogue supplémentaire. Le fichier XML de boîte de dialogue supplémentaire est requis même si aucune boîte de dialogue non sollicitée n’est prévue. La boîte de dialogue supplémentaire doit comporter au moins un `window` élément, même si `window` cet élément est simplement un espace réservé.

>[!NOTE]
>
>Dans ce contexte, le terme &quot;supplémentaire&quot; désigne le contenu du `appmon.[applicationname].addition.[locale].xml` fichier. Un tel fichier spécifie les remplacements et les ajouts au fichier XML de la boîte de dialogue.

Vous pouvez également modifier le fichier XML de boîte de dialogue supplémentaire pour une application native à ces fins :

* Pour remplacer le fichier XML de boîte de dialogue d’une application avec une réponse différente
* Pour ajouter une réponse à une boîte de dialogue qui n’est pas traitée dans le fichier XML de la boîte de dialogue pour cette application

Le nom de fichier qui identifie un fichier dialogXML supplémentaire est `appmon.[appname].addition.[locale].xml`. Par exemple, appmon.excel.addition.en_US.xml.

Le nom du fichier XML de la boîte de dialogue supplémentaire doit utiliser le format `appmon.[applicationname].addition.[locale].xml`, où ** le nom de l’application doit correspondre exactement au nom de l’application utilisé dans le fichier de configuration XML et dans le script.

>[!NOTE]
>
>Aucune des applications génériques spécifiées dans le fichier de configuration native2pdfconfig.xml ne possède de fichier XML de boîte de dialogue principal. La section [Ajout ou modification de la prise en charge d’un format](converting-file-formats-pdf.md#adding-or-modifying-support-for-a-native-file-format) de fichier natif décrit ces spécifications.

Vous devez classer `windowList` les éléments qui apparaissent comme des enfants dans un `window` élément. (Voir [Ordre des éléments window et windowList](converting-file-formats-pdf.md#ordering-the-window-and-windowlist-elements).)

### Modification du fichier XML de la boîte de dialogue générale {#modifying-the-general-dialog-xml-file}

Vous pouvez modifier le fichier XML de la boîte de dialogue générale pour répondre aux boîtes de dialogue générées par le système ou pour répondre aux boîtes de dialogue communes à plusieurs applications.

#### Ajout d’une entrée de type de fichier dans le fichier de configuration XML {#adding-a-filetype-entry-in-the-xml-configuration-file}

Cette procédure explique comment mettre à jour le fichier de configuration du service Generate PDF afin d’associer des types de fichiers aux applications natives. Pour mettre à jour ce fichier de configuration, vous devez utiliser Administration Console pour exporter les données de configuration dans un fichier. Le nom de fichier par défaut des données de configuration est native2pdfconfig.xml.

**Mise à jour du fichier de configuration du service Generate PDF**

1. Sélectionnez **Accueil** > **Services** > **Adobe PDF Generator** > Fichiers de **configuration, puis sélectionnez Exporter la configuration.******
1. Modifiez l’ `filetype-settings` élément dans le fichier native2pdfconfig.xml, le cas échéant.
1. Sélectionnez **Accueil** > **Services** > **Adobe PDF Generator** > Fichiers de **configuration, puis sélectionnez Importer la configuration.****** Les données de configuration sont importées dans le service Generate PDF, en remplacement des paramètres précédents.

>[!NOTE]
>
>Le nom de l’application est spécifié comme valeur de l’ `GenericApp` attribut de l’ `name` élément. Cette valeur doit correspondre exactement au nom correspondant spécifié dans le script que vous développez pour cette application. De même, l’ `GenericApp` attribut de l’ `displayName` élément doit correspondre exactement à la légende de `expectedWindow` fenêtre du script correspondant. Cette équivalence est évaluée après avoir résolu toutes les expressions régulières qui apparaissent dans les `displayName` attributs ou `caption` .

Dans cet exemple, les données de configuration par défaut fournies avec le service Generate PDF ont été modifiées afin de spécifier que le Bloc-notes (et non Microsoft Word) doit être utilisé pour traiter les fichiers avec l’extension de nom de fichier .txt. Avant cette modification, Microsoft Word était spécifié comme application native devant traiter ces fichiers.

**Modifications relatives à la redirection des fichiers texte vers le Bloc-notes (native2pdfconfig.xml)**

```as3
 <filetype-settings>

 <!-- Some native app file types were omitted for brevity. -->
 <!-- The following GenericApp element specifies Notepad as the native application that should be used to process files that have a txt file name extension. -->
             <GenericApp
                 extensions="txt"
                 name="Notepad" displayName=".*Notepad"/>
             <GenericApp
                 extensions="wpd"
                 name="WordPerfect" displayName="Corel WordPerfect"/>
             <GenericApp extensions="pmd,pm6,p65,pm"
                 name="PageMaker" displayName="Adobe PageMaker"/>
             <GenericApp extensions="fm"
                 name="FrameMaker" displayName="Adobe FrameMaker"/>
             <GenericApp extensions="psd"
                 name="Photoshop" displayName="Adobe Photoshop"/>
         </settings>
     </filetype-settings>
```

#### Création d’une variable d’environnement pour localiser l’application native {#creating-an-environment-variable-to-locate-the-native-application}

Créez une variable d’environnement qui spécifie l’emplacement du fichier exécutable natif de l’application. La variable doit utiliser le format `[applicationname]_PATH`, où le *nom d’application* doit correspondre exactement au nom d’application utilisé dans le fichier de configuration XML et dans le script, et où le chemin d’accès contient le chemin d’accès au fichier exécutable sous la forme de guillemets doubles. Un exemple de cette variable d’environnement est `Photoshop_PATH`.

Après avoir créé la nouvelle variable d’environnement, vous devez redémarrer le serveur sur lequel le service Generate PDF est déployé.

**Création d’une variable système dans l’environnement Windows XP**

1. Sélectionnez **Panneau de configuration > Système**.
1. Dans la boîte de dialogue Propriétés système, cliquez sur l’onglet **Avancé** , puis sur Variables **d’** environnement.
1. Sous Variables système dans la boîte de dialogue Variables d’environnement, cliquez sur **Nouveau**.
1. Dans la boîte de dialogue Nouvelle variable système, dans la zone Nom **de la** variable, saisissez un nom qui utilise le format `[applicationname]_PATH`.
1. Dans la zone **Variable value** , saisissez le chemin d’accès complet et le nom de fichier du fichier exécutable de l’application, puis cliquez sur **OK**. Par exemple, saisissez: `c:\windows\Notepad.exe`
1. Dans la boîte de dialogue Variables d’environnement, cliquez sur **OK**.

**Création d’une variable système à partir de la ligne de commande**

1. Dans une fenêtre de ligne de commande, saisissez la définition de variable, au format suivant :

   ```as3
            [applicationname]_PATH=[Full path name]
   ```

   Par exemple, saisissez: `NotePad_PATH=C:\WINDOWS\NOTEPAD.EXE`

1. Démarrez une nouvelle invite de ligne de commande pour que la variable système prenne effet.

#### Fichiers XML {#xml-files}

AEM Forms inclut des exemples de fichiers XML qui font que le service Generate PDF utilise le Bloc-notes pour traiter tous les fichiers portant l’extension .txt du nom de fichier. Ce code est inclus dans cette section. En outre, vous devez apporter les autres modifications décrites dans cette section.

#### Fichier XML de boîte de dialogue supplémentaire {#additional-dialog-xml-file}

Cet exemple contient les boîtes de dialogue supplémentaires pour l&#39;application Bloc-notes. Ces boîtes de dialogue peuvent s’ajouter à celles spécifiées par le service Generate PDF.

**Boîte de dialogue du Bloc-notes (appmon.Bloc-notes.addition.en_US.xml)**

```as3
 <dialogs app="Notepad" locale="en_US" version="7.0" xmlns:xsi="https://www.w3.org/2001/XMLSchema-instance" xsi:noNamespaceSchemaLocation="dialogs.xsd">
     <window caption="Caption Title">
         <windowList>
             <window className="Button" caption="OK" action="press"/>
         </windowList>
     </window>
 </dialogs>
```

#### Fichier XML de script {#script-xml-file}

Cet exemple montre comment le service Generate PDF doit interagir avec le Bloc-notes pour imprimer des fichiers à l’aide de l’imprimante Adobe PDF.

**Fichier XML de script du Bloc-notes (appmon.Bloc-notes.script.en_US.xml)**

```as3
<?xml version="1.0" encoding="UTF-8" standalone="yes"?>
<!--
*
* ADOBE CONFIDENTIAL
* ___________________
* Copyright 2004 - 2005 Adobe Systems Incorporated
* All Rights Reserved.
*
* NOTICE:  All information contained herein is, and remains
* the property of Adobe Systems Incorporated and its suppliers,
* if any.  The intellectual and technical concepts contained
* herein are proprietary to Adobe Systems Incorporated and its
* suppliers and may be covered by U.S. and Foreign Patents,
* patents in process, and are protected by trade secret or copyright law.
* Dissemination of this information or reproduction of this material
* is strictly forbidden unless prior written permission is obtained
* from Adobe Systems Incorporated.
*-->

<!-- This file automates printing of text files via notepad to Adobe PDF printer. In order to see the complete hierarchy we recommend using the Microsoft Spy++ which details the properties of windows necessary to write scripts. In this sample there are total of eight steps-->

<application name="Notepad" version="9.0" locale="en_US" xmlns:xsi="https://www.w3.org/2001/XMLSchema-instance" xsi:noNamespaceSchemaLocation="scripts.xsd">

    <!-- In this step we wait for the application window to appear -->
    <step>
        <expectedWindow>
            <window caption=".*Notepad"/>
        </expectedWindow>
    </step>

    <!-- In this step, we acquire the application window and send File->Open menu bar, menu item commands and the expectation is the windows Open dialog-->
    <step>
        <acquiredWindow>
            <window caption=".*Notepad">
                <virtualInput>
                    <menuBar>
                        <selection>
                            <name>File</name>
                        </selection>
                        <selection>
                            <name>Open...</name>
                        </selection>
                    </menuBar>
                </virtualInput>
            </window>
        </acquiredWindow>
        <expectedWindow>
            <window caption="Open"/>
        </expectedWindow>
    </step>

    <!-- In this step, we acquire the Open window and then select the 'Edit' widget and input the source path followed by clicking on the 'Open' button . The expectation of this 'action' is that the Open dialog will disappear -->
    <step>
        <acquiredWindow>
            <window caption="Open">
                <windowList>
                    <window className="ComboBoxEx32">
                        <windowList>
                            <window className="ComboBox">
                                <windowList>
                                <window className="Edit" action="inputSourcePath"/>
                                </windowList>
                            </window>
                        </windowList>
                    </window>
                </windowList>
                <windowList>
                    <window className="Button" caption="Open" action="press"/>
                </windowList>
            </window>
        </acquiredWindow>
        <expectedWindow>
            <window caption="Open" action="disappear"/>
        </expectedWindow>
        <pause value="30"/>
    </step>

    <!-- In this step, we acquire the application window and send File->Print menu bar, menu item commands and the expectation is the windows Print dialog-->
    <step>
        <acquiredWindow>
            <window caption=".*Notepad">
                <virtualInput>
                    <menuBar>
                        <selection>
                            <name>File</name>
                        </selection>
                        <selection>
                            <name>Print...</name>
                        </selection>
                    </menuBar>
                </virtualInput>
            </window>
        </acquiredWindow>
        <expectedWindow>
            <window caption="Print">
        </window>
        </expectedWindow>
    </step>

    <!-- In this step, we acquire the Print dialog and click on the 'Preferences' button and the expected window in this case is the dialog with the caption '"Printing Preferences' -->
    <step>
        <acquiredWindow>
            <window caption="Print">
                <windowList>
                    <window caption="General">
                        <windowList>
                            <window className="Button" caption="Preferences" action="press"/>
                        </windowList>
                    </window>
                </windowList>
            </window>
        </acquiredWindow>
        <expectedWindow>
            <window caption="Printing Preferences"/>
        </expectedWindow>
    </step>

    <!-- In this step, we acquire the dialog "Printing Preferences' and select the combo box which is the 10th child of window with caption '"Adobe PDF Settings' and select the first index. (Note: All indeces start with 0.) Besides this we uncheck the box which  has the caption '"View Adobe PDF results' and we click on the button OK. The expectation is that 'Printing Preferences' dialog disappears. -->
    <step>
        <acquiredWindow>
            <window caption="Printing Preferences">
                <windowList>
                    <window caption="Adobe PDF Settings">
                        <windowList>
                            <window className="Button" caption="View Adobe PDF results" action="uncheck"/>
                        </windowList>
                        <windowList>
                            <window className="Button" caption="Ask to Replace existing PDF file" action="uncheck"/>
                        </windowList>
                    </window>
                </windowList>
                <windowList>
                    <window className="Button" caption="OK" action="press"/>
                </windowList>
            </window>
        </acquiredWindow>
        <expectedWindow>
            <window caption="Printing Preferences" action="disappear"/>
        </expectedWindow>
    </step>

    <!-- In this step, we acquire the 'Print' dialog and click on the Print button. The expectation is that the dialog with caption 'Print' disappears. In this case we use the regular expression '^Print$' for specifying the caption given there could be multiple dialogs with caption that includes the word Print. -->
    <step>
        <acquiredWindow>
            <window caption="Print">
                <windowList>
                    <window caption="General"/>
                    <window className="Button" caption="^Print$" action="press"/>
                </windowList>
            </window>
        </acquiredWindow>
        <expectedWindow>
            <window caption="Print" action="disappear"/>
        </expectedWindow>
    </step>
    <step>
        <expectedWindow>
            <window caption="Save PDF File As"/>
        </expectedWindow>
    </step>
    <!-- Finally in this step, we acquire the dialog with caption "Save PDF File As" and in the Edit widget type the destination path for the output PDF file and click on the Save button. The expectation is that the dialog disappears-->
    <step>
        <acquiredWindow>
            <window caption="Save PDF File As">
                <windowList>
                    <window className="Edit" action="inputDestinationPath"/>
                </windowList>
                <windowList>
                    <window className="Button" caption="Save" action="press"/>
                </windowList>
            </window>
        </acquiredWindow>
        <expectedWindow>
            <window caption="Save PDF File As" action="disappear"/>
        </expectedWindow>
    </step>

    <!-- We can always set a retry count or a maximum time for a step. In case we surpass these limitations, PDF Generator generates this abort message and terminates processing. -->
    <abortMessage msg="15078"/>
</application>
```

