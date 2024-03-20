---
title: Convertir entre les formats de fichier et le PDF
description: Utilisez le service Generate PDF pour convertir des formats de fichiers natifs en PDF. Le service Generate PDF convertit également des fichiers PDF en d’autres formats et optimise la taille des documents PDF.
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
role: Developer
exl-id: 10535740-e3c2-4347-a88f-86706ad699b4
solution: Experience Manager, Experience Manager Forms
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '7848'
ht-degree: 98%

---

# Convertir entre les formats de fichier et le PDF {#converting-between-file-formatsand-pdf}

**Les exemples et les échantillons de ce document sont réservés à l’environnement AEM Forms sur JEE.**

**À propos du service Generate PDF**

Le service Generate PDF peut convertir de nombreux formats de fichier natifs en PDF. Il convertit également des fichiers PDF en d’autres formats et optimise la taille des documents PDF.

Le service Generate PDF utilise des applications natives pour convertir les formats de fichiers suivants en PDF. Sauf précision contraire, seules les versions allemande, anglaise, française et japonaise de ces applications sont prises en charge. *Windows uniquement* indique la prise en charge de Windows Server® 2003 et Windows Server 2008 uniquement.

* Microsoft Office 2003 et 2007 pour convertir les formats DOC, DOCX, RTF, TXT, XLS, XLSX, PPT, PPTX, VSD, MPP, MPPX, XPS, et PUB (Windows uniquement).

>[!NOTE]
>
>Acrobat® 9.2 ou une version ultérieure est requis pour convertir le format Microsoft XPS en PDF.

* Autodesk AutoCAD 2005, 2006, 2007, 2008 et 2009 pour convertir les fichiers DWF, DWG et DXW (en anglais uniquement).
* Corel WordPerfect 12 et X4 pour convertir WPD, QPW, SHW (en anglais uniquement).
* OpenOffice 2.0, 2.4, 3.0.1 et 3.1 pour convertir les formats ODT, ODS, ODP, ODG, ODF, SXW, SXI, SXC, SXD, DOC, DOCX, RTF, TXT, XLS, XLSX, PPT, PPTX, VSD, MPP, MPPX et PUB.

>[!NOTE]
>
>le service Generate PDF ne prend pas en charge les versions 64 bits d’OpenOffice.

* Adobe Photoshop® CS2 pour convertir le format PSD (Windows uniquement).

>[!NOTE]
>
>Photoshop CS3 et CS4 ne sont pas pris en charge, car ils ne prennent pas en charge Windows Server 2003 ou Windows Server 2008.

* Adobe FrameMaker® 7.2 et 8 pour convertir le format FM (Windows uniquement).
* Adobe PageMaker 7.0 pour convertir les formats PMD, PM6, P65 et PM (Windows uniquement).
* Formats natifs pris en charge par les applications tierces (requiert le développement de fichiers d’installation spécifiques à l’application) (Windows uniquement)

Le service Generate PDF peut convertir les formats standards suivants en PDF.

* Formats vidéo : SWF, FLV (Windows uniquement)
* Formats image : JPEG, JPG, JP2, J2Kí, JPC, J2C, GIF, BMP, TIFF, TIF, PNG, JPF
* HTML (Windows, Sun™, Solaris™ et Linux®).

Le service Generate PDF peut convertir des PDF aux formats de fichiers suivants (Windows uniquement) :

* Encapsulated Postscript (EPS)
* HTML 3.2
* HTML 4.01 avec CSS 1.0
* DOC (format Microsoft Word)
* RTF
* Texte (à la fois accessible et brut)
* XML
* PDF/A-1a utilisant uniquement l’espace colorimétrique DeviceRGB.
* PDF/A-1b utilisant uniquement l’espace colorimétrique DeviceRGB.

Le service Generate PDF requiert que vous réalisiez ces tâches administratives :

* Installez les applications natives requises sur l’ordinateur hébergeant AEM Forms.
* Installez Adobe Acrobat Professional ou Acrobat Pro Extended 9.2 sur l’ordinateur hébergeant AEM Forms.
* Réalisez les tâches consécutives à l’installation.

Ces tâches sont décrites dans la section Installation et déploiement d’AEM Forms à l’aide de la procédure clé en main de JBoss.

Vous pouvez accomplir ces tâches à l’aide du service Generate PDF :

* Convertissez des formats de fichiers natifs en PDF.
* Convertissez des documents de HTML en documents PDF.
* Convertissez des documents PDF en formats de fichiers.

>[!NOTE]
>
>Pour plus d’informations sur le service Generate PDF, voir [Référence des services pour AEM Forms](https://help.adobe.com/fr_FR/livecycle/11.0/Services/index.html).

## Convertir des documents Word en documents PDF {#converting-word-documents-to-pdf-documents}

Cette section décrit comment utiliser l’API Generate PDF pour convertir par programmation un document Microsoft Word en document PDF.

>[!NOTE]
>
>Pour plus d’informations sur les formats de fichier supplémentaires, voir [Ajouter la prise en charge de formats de fichier natifs supplémentaires](converting-file-formats-pdf.md#adding-support-for-additional-native-file-formats).

>[!NOTE]
>
>Pour plus d’informations sur le service Generate PDF, voir [Référence des services pour AEM Forms](https://help.adobe.com/fr_FR/livecycle/11.0/Services/index.html).

### Résumé des étapes {#summary-of-steps}

Pour convertir un document Microsoft Word en document PDF, procédez comme suit :

1. Incluez les fichiers de projet.
1. Créez un client Generate PDF.
1. Récupérez le fichier à convertir en document PDF.
1. Convertissez le fichier en document PDF.
1. Récupérez les résultats.

**Inclure les fichiers de projet**

Incluez les fichiers nécessaires dans votre projet de développement. Si vous créez une application cliente à l’aide de Java, incluez les fichiers JAR nécessaires. Si vous utilisez des services Web, veillez à inclure les fichiers proxy.

**Créer un client Generate PDF**

Avant de pouvoir exécuter une opération Generate PDF par programmation, créez un client de service Generate PDF. Si vous utilisez l’API Java, créez un objet `GeneratePdfServiceClient`. Si vous utilisez l’API Web Service, créez un objet `GeneratePDFServiceService`.

**Récupérer un fichier à convertir en document PDF**

Récupérez le document Microsoft Word à convertir en document PDF.

**Convertir le fichier en document PDF**

Après avoir créé le client de service Generate PDF, vous pouvez appeler la méthode `createPDF2`. Cette méthode nécessite des informations sur le document à convertir, notamment l’extension de fichier.

**Récupérer les résultats**

Une fois le fichier converti en document PDF, vous pouvez récupérer les résultats. Par exemple, après avoir converti un fichier Word en document PDF, vous pouvez récupérer et enregistrer le document PDF.

**Voir également**

[Convertir des documents Word en documents PDF à l’aide de l’API Java](converting-file-formats-pdf.md#convert-word-documents-to-pdf-documents-using-the-java-api)

[Convertir des documents Word en documents PDF à l’aide de l’API Web Service](converting-file-formats-pdf.md#convert-word-documents-to-pdf-documents-using-the-web-service-api)

[Inclusion des fichiers de bibliothèque Java d’AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Démarrages rapides de l’API du service Generate PDF](/help/forms/developing/generate-pdf-service-java-api.md#generate-pdf-service-java-api-quick-start-soap)

### Convertir des documents Word en documents PDF à l’aide de l’API Java {#convert-word-documents-to-pdf-documents-using-the-java-api}

Convertissez un document Microsoft Word en document PDF à l’aide de l’API Generate PDF (Java) :

1. Incluez les fichiers de projet.

   Incluez les fichiers JAR du client, tels que adobe-generatepdf-client.jar, dans le chemin d’accès aux classes de votre projet Java.

1. Créez un client Generate PDF.

   * Créez un objet `ServiceClientFactory` qui contient des propriétés de connexion.
   * Créez un objet `GeneratePdfServiceClient` en utilisant son constructeur et en transmettant l’objet `ServiceClientFactory`. 

1. Récupérez le fichier à convertir en document PDF.

   * Créez un objet `java.io.FileInputStream` représentant le fichier Word à convertir à l’aide de son constructeur. Transmettez une valeur de chaîne indiquant l’emplacement du fichier.
   * Créez un objet `com.adobe.idp.Document` en utilisant son constructeur et en transmettant l’objet `java.io.FileInputStream`. 

1. Convertissez le fichier en document PDF.

   Convertissez le fichier en document PDF en appelant la méthode `createPDF2` de l’objet `GeneratePdfServiceClient` et en transmettant les valeurs suivantes :

   * Un objet `com.adobe.idp.Document` représentant le fichier à convertir.
   * Un objet `java.lang.String` contenant l’extension de fichier.
   * Un objet `java.lang.String` contenant les paramètres de type de fichier à utiliser lors de la conversion. Les paramètres de type de fichier fournissent des paramètres de conversion pour différents types de fichiers, tels que .doc ou .xls.
   * Un objet `java.lang.String` contenant le nom des paramètres PDF à utiliser. Par exemple, vous pouvez spécifier `Standard`.
   * Un objet `java.lang.String` contenant le nom des paramètres de sécurité à utiliser.
   * Un objet `com.adobe.idp.Document` facultatif contenant les paramètres à appliquer lors de la génération du document PDF.
   * Un objet facultatif `com.adobe.idp.Document` contenant des informations de métadonnées à appliquer au document PDF.

   La méthode `createPDF2` renvoie un objet `CreatePDFResult` contenant le nouveau document PDF et des informations sur le journal. Le fichier journal contient généralement des messages d’erreur ou d’avertissement générés par la demande de conversion.

1. Récupérez les résultats.

   Pour obtenir le document PDF, procédez comme suit :

   * Appelez la méthode `getCreatedDocument` de l’objet `CreatePDFResult`, qui renvoie un objet `com.adobe.idp.Document`.
   * Appelez la méthode `copyToFile` de l’objet `com.adobe.idp.Document` pour extraire le document PDF de l’objet créé à l’étape précédente.

   Si vous avez utilisé la méthode `createPDF2` pour obtenir le document de journal (qui ne s’applique pas aux conversions HTML), procédez comme suit :

   * Appelez la méthode `getLogDocument` de l’objet `CreatePDFResult`. Celle-ci renvoie un objet `com.adobe.idp.Document`.
   * Appelez la méthode `copyToFile` de l’objet `com.adobe.idp.Document` pour extraire le document journal.

**Voir également**

[Résumé des étapes](converting-file-formats-pdf.md#summary-of-steps)

[Démarrage rapide (mode SOAP) : convertir un document Microsoft Word au format PDF à l’aide de l’API Java.](/help/forms/developing/generate-pdf-service-java-api.md#quick-start-soap-mode-converting-a-microsoft-word-document-to-a-pdf-document-using-the-java-api)

[Inclusion des fichiers de bibliothèque Java d’AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Convertir des documents Word en documents PDF à l’aide de l’API Web Service {#convert-word-documents-to-pdf-documents-using-the-web-service-api}

Convertissez un document Microsoft Word en document PDF à l’aide de l’API Generate PDF (service web) :

1. Incluez les fichiers de projet.

   Créez un projet Microsoft .NET qui utilise MTOM. Veillez à utiliser la définition WSDL suivante : `http://localhost:8080/soap/services/GeneratePDFService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Remplacez `localhost` par l’adresse IP du serveur hébergeant AEM Forms.

1. Créez un client Generate PDF.

   * Créez un objet `GeneratePDFServiceClient` en utilisant son constructeur par défaut.
   * Créez un objet `GeneratePDFServiceClient.Endpoint.Address` en utilisant le constructeur `System.ServiceModel.EndpointAddress`. Transmettez une valeur string qui spécifie le WSDL au service AEM Forms (par exemple `http://localhost:8080/soap/services/GeneratePDFService?blob=mtom`). Il n’est pas nécessaire d’utiliser l’attribut `lc_version`. Toutefois, spécifiez `?blob=mtom`.
   * Créez un objet `System.ServiceModel.BasicHttpBinding` en obtenant la valeur du champ `GeneratePDFServiceClient.Endpoint.Binding`. Convertissez la valeur de retour en `BasicHttpBinding`.
   * Définissez le champ `MessageEncoding` de l’objet `System.ServiceModel.BasicHttpBinding` sur `WSMessageEncoding.Mtom`. Cette valeur garantit l’utilisation de MTOM.
   * Activez l’authentification HTTP de base en effectuant les tâches suivantes :

      * Attribuez le nom d’utilisateur AEM forms au champ `GeneratePDFServiceClient.ClientCredentials.UserName.UserName`.
      * Attribuez la valeur de mot de passe correspondante au champ `GeneratePDFServiceClient.ClientCredentials.UserName.Password`.
      * Attribuez la valeur constante `HttpClientCredentialType.Basic` au champ `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Attribuez la valeur constante `BasicHttpSecurityMode.TransportCredentialOnly` au champ `BasicHttpBindingSecurity.Security.Mode`.

1. Récupérez le fichier à convertir en document PDF.

   * Créez un objet `BLOB` en utilisant son constructeur. L’objet `BLOB` sert à stocker le fichier que vous souhaitez convertir en document PDF.
   * Créez un objet `System.IO.FileStream` en appelant son constructeur. Transmettez une valeur de chaîne représentant l’emplacement du fichier à convertir et son mode d’ouverture.
   * Créez un tableau d’octets stockant le contenu de l’objet `System.IO.FileStream`. Vous pouvez déterminer la taille du tableau d’octets en obtenant la propriété `Length` de l’objet `System.IO.FileStream`.
   * Renseignez le tableau d’octets avec les données de flux en appelant la méthode `Read` de l’objet `System.IO.FileStream` et en transmettant le tableau d’octets, la position de départ et la longueur du flux à lire.
   * Renseignez l’objet `BLOB` en affectant à sa propriété `MTOM` le contenu du tableau d’octets.

1. Convertissez le fichier en document PDF.

   Convertissez le fichier en document PDF en appelant la méthode `CreatePDF2` de l’objet `GeneratePDFServiceService` et en transmettant les valeurs suivantes :

   * Un objet `BLOB` représentant le fichier à convertir.
   * Une chaîne contenant l’extension de fichier.
   * Un objet `java.lang.String` contenant les paramètres de type de fichier à utiliser lors de la conversion. Les paramètres de type de fichier fournissent des paramètres de conversion pour différents types de fichiers, tels que .doc ou .xls.
   * Un objet de chaîne contenant les paramètres PDF à utiliser. Vous pouvez préciser `Standard`.
   * Un objet de chaîne contenant les paramètres de sécurité à utiliser. Vous pouvez préciser `No Security`.
   * Un objet `BLOB` contenant les paramètres à appliquer lors de la génération du document PDF.
   * Un objet `BLOB` facultatif contenant des informations de métadonnées à appliquer au document PDF.
   * Un paramètre de sortie de type `BLOB` renseigné par la méthode `CreatePDF2`. La méthode `CreatePDF2` renseigne cet objet avec le document converti. (Cette valeur de paramètre est requise uniquement pour l’appel du service web).
   * Un paramètre de sortie de type `BLOB` renseigné par la méthode `CreatePDF2`. La méthode `CreatePDF2` renseigne cet objet avec le document de journal. (Cette valeur de paramètre est requise uniquement pour l’appel du service web).

1. Récupérez les résultats.

   * Récupérez le document PDF converti en attribuant au champ `MTOM` de l’objet `BLOB` un tableau d’octets. Le tableau d’octets représente le document PDF converti. Veillez à utiliser l’objet `BLOB` servant de paramètre de sortie pour la méthode `createPDF2`.
   * Créez un objet `System.IO.FileStream` en appelant son constructeur et en transmettant une valeur de chaîne représentant l’emplacement du document PDF converti.
   * Créez un objet `System.IO.BinaryWriter` en utilisant son constructeur et en transmettant l’objet `System.IO.FileStream`.
   * Écrivez le contenu du tableau d’octets dans un fichier PDF en appelant la méthode `Write` de l’objet `System.IO.BinaryWriter` et en transmettant le tableau d’octets.

**Voir également**

[Résumé des étapes](converting-file-formats-pdf.md#summary-of-steps)

[Appeler AEM Forms en utilisant MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Appel d’AEM Forms à l’aide de SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Convertir des documents HTML en documents PDF {#converting-html-documents-to-pdf-documents}

Cette section décrit comment utiliser l’API Generate PDF pour convertir par programmation des documents HTML en documents PDF.

>[!NOTE]
>
>Pour plus d’informations sur le service Generate PDF, consultez la section [Références des services pour AEM Forms](https://help.adobe.com/fr_FR/livecycle/11.0/Services/index.html).

### Résumé des étapes {#summary_of_steps-1}

Pour convertir un document HTML en document PDF, procédez comme suit :

1. Incluez les fichiers de projet.
1. Créez un client Generate PDF.
1. Récupérez le contenu du fichier HTML à convertir en document PDF.
1. Convertissez le contenu du fichier HTML en document PDF.
1. Récupérez les résultats.

**Inclure les fichiers de projet**

Incluez les fichiers nécessaires dans votre projet de développement. Si vous créez une application cliente à l’aide de Java, incluez les fichiers JAR nécessaires. Si vous utilisez des services Web, veillez à inclure les fichiers proxy.

**Créer un client Generate PDF**

Avant de pouvoir effectuer par programmation une opération Generate PDF, vous devez créer un client de service Generate PDF. Si vous utilisez l’API Java, créez un objet `GeneratePdfServiceClient`. Si vous utilisez l’API de service web, créez un objet `GeneratePDFServiceService`.

**Récupérer le contenu HTML à convertir en document PDF**

Référencez le contenu HTML que vous souhaitez convertir en document PDF. Vous pouvez référencer un contenu HTML, tel qu’un fichier HTML ou un contenu HTML accessible à l’aide d’une URL.

**Convertir le contenu HTML en document PDF**

Une fois que vous avez créé le client de service, vous pouvez appeler l’opération de création de fichiers PDF appropriée. Cette opération nécessite des informations sur le document à convertir, notamment le chemin d’accès au document cible.

**Récupérer les résultats**

Une fois le contenu HTML converti en document PDF, vous pouvez récupérer les résultats et enregistrer le document PDF.

**Voir également**

[Convertir le contenu HTML en document PDF à l’aide de l’API Java](converting-file-formats-pdf.md#convert-html-content-to-a-pdf-document-using-the-java-api)

[Convertir le contenu HTML en document PDF à l’aide de l’API de service web](converting-file-formats-pdf.md#convert-html-content-to-a-pdf-document-using-the-web-service-api)

[Inclusion des fichiers de bibliothèque Java d’AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Démarrages rapides de l’API du service Generate PDF](/help/forms/developing/generate-pdf-service-java-api.md#generate-pdf-service-java-api-quick-start-soap)

### Convertir le contenu HTML en document PDF à l’aide de l’API Java {#convert-html-content-to-a-pdf-document-using-the-java-api}

Pour convertir un document HTML en document PDF à l’aide de l’API Generate PDF (Java), procédez comme suit :

1. Incluez les fichiers de projet.

   Incluez les fichiers JAR du client, tels que adobe-generatepdf-client.jar, dans le chemin d’accès aux classes de votre projet Java.

1. Créez un client Generate PDF.

   Créez un objet `GeneratePdfServiceClient` en utilisant son constructeur et en transmettant un objet `ServiceClientFactory` contenant des propriétés de connexion.

1. Récupérez le contenu du fichier HTML à convertir en document PDF.

   Récupérez le contenu HTML en créant une variable de chaîne et en affectant une URL qui pointe vers le contenu HTML.

1. Convertissez le contenu du fichier HTML en document PDF.

   Appelez la méthode `htmlToPDF2` de l’objet `GeneratePdfServiceClient` et transmettez les valeurs suivantes :

   * Un objet `java.lang.String` contenant l’URL du fichier HTML à convertir.
   * Un objet `java.lang.String` contenant les paramètres de type de fichier à utiliser lors de la conversion. Les paramètres de type de fichier peuvent inclure des niveaux d’indexation.
   * Un objet `java.lang.String` contenant le nom des paramètres de sécurité à utiliser.
   * Un objet `com.adobe.idp.Document` facultatif contenant les paramètres à appliquer lors de la génération du document PDF. Si ces informations ne sont pas fournies, les paramètres sont automatiquement choisis en fonction des trois paramètres précédents.
   * Un objet `com.adobe.idp.Document` facultatif contenant des informations de métadonnées à appliquer au document PDF.

1. Récupérez les résultats.

   La méthode `htmlToPDF2` renvoie un objet `HtmlToPdfResult` contenant le nouveau document PDF généré. Pour obtenir le document PDF nouvellement créé, procédez comme suit :

   * Appelez la méthode `getCreatedDocument` de lʼobjet `HtmlToPdfResult`. Celle-ci renvoie un objet `com.adobe.idp.Document`.
   * Appelez la méthode `copyToFile` de lʼobjet `com.adobe.idp.Document` pour extraire le document PDF de lʼobjet créé à lʼétape précédente.

**Voir également**

[Convertir des documents HTML en documents PDF](converting-file-formats-pdf.md#converting-html-documents-to-pdf-documents)

[Démarrage rapide (mode SOAP) : convertir du contenu HTML en document PDF à l’aide de l’API Java.](/help/forms/developing/generate-pdf-service-java-api.md#quick-start-soap-mode-converting-html-content-to-a-pdf-document-using-the-java-api)

[Démarrage rapide (mode SOAP) : convertir du contenu HTML en document PDF à l’aide de l’API Java.](/help/forms/developing/generate-pdf-service-java-api.md#quick-start-soap-mode-converting-html-content-to-a-pdf-document-using-the-java-api)

[Inclusion des fichiers de bibliothèque Java d’AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Convertir le contenu HTML en document PDF à l’aide de l’API de service web {#convert-html-content-to-a-pdf-document-using-the-web-service-api}

Pour convertir le contenu HTML en document PDF à l’aide de l’API Generate PDF (service web), procédez comme suit :

1. Incluez les fichiers de projet.

   Créez un projet Microsoft .NET qui utilise MTOM. Veillez à utiliser la définition WSDL suivante : `http://localhost:8080/soap/services/GeneratePDFService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Remplacez `localhost` par l’adresse IP du serveur hébergeant AEM Forms.

1. Créez un client Generate PDF.

   * Créez un objet `GeneratePDFServiceClient` en utilisant son constructeur par défaut.
   * Créez un objet `GeneratePDFServiceClient.Endpoint.Address` en utilisant le constructeur `System.ServiceModel.EndpointAddress`. Transmettez une valeur string qui spécifie le WSDL au service AEM Forms (par exemple `http://localhost:8080/soap/services/GeneratePDFService?blob=mtom`). Il n’est pas nécessaire d’utiliser l’attribut `lc_version`. Toutefois, spécifiez `?blob=mtom`.
   * Créez un objet `System.ServiceModel.BasicHttpBinding` en obtenant la valeur du champ `GeneratePDFServiceClient.Endpoint.Binding`. Convertissez la valeur de retour en `BasicHttpBinding`.
   * Définissez le champ `MessageEncoding` de l’objet `System.ServiceModel.BasicHttpBinding` sur `WSMessageEncoding.Mtom`. Cette valeur garantit l’utilisation de MTOM.
   * Activez l’authentification HTTP de base en effectuant les tâches suivantes :

      * Attribuez le nom d’utilisateur AEM forms au champ `GeneratePDFServiceClient.ClientCredentials.UserName.UserName`.
      * Attribuez la valeur de mot de passe correspondante au champ `GeneratePDFServiceClient.ClientCredentials.UserName.Password`.
      * Attribuez la valeur constante `HttpClientCredentialType.Basic` au champ `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Affectez la valeur constante `BasicHttpSecurityMode.TransportCredentialOnly` au champ `BasicHttpBindingSecurity.Security.Mode`.

1. Récupérez le contenu du fichier HTML à convertir en document PDF.

   Récupérez le contenu HTML en créant une variable de chaîne et en affectant une URL qui pointe vers le contenu HTML.

1. Convertissez le contenu du fichier HTML en document PDF.

   Convertissez le contenu HTML en document PDF en appelant la méthode `HtmlToPDF2` de l’objet `GeneratePDFServiceService` et transmettez les valeurs suivantes :

   * Une chaîne contenant le contenu HTML à convertir.
   * Un objet `java.lang.String` contenant les paramètres de type de fichier à utiliser lors de la conversion.
   * Un objet de chaîne contenant les paramètres de sécurité à utiliser.
   * Un objet `BLOB` facultatif contenant les paramètres à appliquer lors de la génération du document PDF.
   * Un objet `BLOB` facultatif contenant des informations de métadonnées à appliquer au document PDF.
   * Un paramètre de sortie de type `BLOB` renseigné par la méthode `CreatePDF2`. La méthode `CreatePDF2` renseigne cet objet avec le document converti. (Cette valeur de paramètre est requise uniquement pour l’appel du service web).

1. Récupérez les résultats.

   * Récupérez le document PDF converti en attribuant au champ `MTOM` de l’objet `BLOB` un tableau d’octets. Le tableau d’octets représente le document PDF converti. Veillez à utiliser l’objet `BLOB` servant de paramètre de sortie pour la méthode `HtmlToPDF2`.
   * Créez un objet `System.IO.FileStream` en appelant son constructeur et en transmettant une valeur de chaîne représentant l’emplacement du document PDF converti.
   * Créez un objet `System.IO.BinaryWriter` en utilisant son constructeur et en transmettant l’objet `System.IO.FileStream`.
   * Écrivez le contenu du tableau d’octets dans un fichier PDF en appelant la méthode `Write` de l’objet `System.IO.BinaryWriter` et en transmettant le tableau d’octets.

**Voir également**

[Convertir des documents HTML en documents PDF](converting-file-formats-pdf.md#converting-html-documents-to-pdf-documents)

[Appeler AEM Forms en utilisant MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Appel d’AEM Forms à l’aide de SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Convertir des documents PDF en formats non-images {#converting-pdf-documents-to-non-image-formats}

Cette section décrit comment utiliser l’API Java Generate PDF et l’API Web Service pour convertir par programmation un document PDF en fichier RTF, qui est un exemple de format non-image. Entre autres formats non-images, on peut citer HTML, le fichier texte, DOC et EPS. Lors de la conversion d’un document PDF en format RTF, assurez-vous que le document PDF ne contient aucun élément de formulaire, tel qu’un bouton d’envoi. Les éléments de formulaire ne sont pas convertis.

>[!NOTE]
>
>Pour plus d’informations sur le service Generate PDF, voir [Référence des services pour AEM Forms](https://help.adobe.com/fr_FR/livecycle/11.0/Services/index.html).

### Résumé des étapes {#summary_of_steps-2}

Pour convertir un document PDF en l’un des types pris en charge, procédez comme suit :

1. Incluez les fichiers de projet.
1. Créez un client Generate PDF.
1. Récupérez le document du PDF à convertir.
1. Convertissez le document PDF.
1. Enregistrez le fichier converti.

**Inclure des fichiers de projet**

Incluez les fichiers nécessaires dans votre projet de développement. Si vous créez une application cliente à l’aide de Java, incluez les fichiers JAR nécessaires. Si vous utilisez des services Web, veillez à inclure les fichiers proxy.

**Créer un client Generate PDF**

Avant de pouvoir effectuer par programmation une opération Generate PDF, vous devez créer un client de service Generate PDF. Si vous utilisez l’API Java, créez un objet `GeneratePdfServiceClient`. Si vous utilisez l’API Web Service, créez un objet `GeneratePDFServiceService`.

**Récupérer un document PDF à convertir**

Récupérez le document PDF à convertir en un format non-image.

**Convertir le document PDF**

Après avoir créé le client de service, vous pouvez appeler l’opération d’exportation du PDF. Cette opération nécessite des informations sur le document à convertir, notamment le chemin d’accès au document cible.

**Enregistrer le fichier converti**

Enregistrez le fichier converti. Par exemple, si vous convertissez un document PDF en fichier RTF, enregistrez le document converti en fichier RTF.

**Voir également**

[Convertir un document PDF en fichier RTF à l’aide de l’API Java](converting-file-formats-pdf.md#convert-a-pdf-document-to-a-rtf-file-using-the-java-api)

[Convertir un document PDF en fichier RTF à l’aide de l’API Web Service](converting-file-formats-pdf.md#convert-a-pdf-document-to-a-rtf-file-using-the-web-service-api)

[Inclusion des fichiers de bibliothèque Java d’AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Démarrages rapides de l’API du service Generate PDF](/help/forms/developing/generate-pdf-service-java-api.md#generate-pdf-service-java-api-quick-start-soap)

### Convertir un document PDF en fichier RTF à l’aide de l’API Java {#convert-a-pdf-document-to-a-rtf-file-using-the-java-api}

Convertissez un document PDF en fichier RTF à l’aide de l’API Generate PDF (Java) :

1. Incluez les fichiers de projet.

   Incluez les fichiers JAR du client, tels que adobe-generatepdf-client.jar, dans le chemin d’accès aux classes de votre projet Java.

1. Créez un client Generate PDF.

   Créez un objet `GeneratePdfServiceClient` en utilisant son constructeur et en transmettant un objet `ServiceClientFactory` contenant des propriétés de connexion.

1. Récupérez le document du PDF à convertir.

   * Créez un objet `java.io.FileInputStream` représentant le document PDF à convertir à l’aide de son constructeur. Transmettez une valeur de chaîne qui spécifie l’emplacement du document PDF.
   * Créez un objet `com.adobe.idp.Document` en utilisant son constructeur et en transmettant l’objet `java.io.FileInputStream`. 

1. Convertissez le document PDF.

   Appelez la méthode `exportPDF2` de l’objet `GeneratePdfServiceClient` et transmettez les valeurs suivantes :

   * Objet `com.adobe.idp.Document` représentant le fichier PDF à convertir.
   * Objet `java.lang.String` contenant le nom du fichier à convertir.
   * Objet `java.lang.String` contenant le nom des paramètres Adobe PDF.
   * Objet `ConvertPDFFormatType` indiquant le type de fichier cible pour la conversion.
   * Objet `com.adobe.idp.Document` facultatif contenant les paramètres à appliquer lors de la génération du document PDF.

   La méthode `exportPDF2` renvoie un objet `ExportPDFResult` contenant le fichier converti.

1. Convertissez le document PDF.

   Pour obtenir le fichier nouvellement créé, procédez comme suit :

   * Appelez la méthode `getConvertedDocument` de l’objet `ExportPDFResult`. Celle-ci renvoie un objet `com.adobe.idp.Document`.
   * Appelez la méthode `copyToFile` de l’objet `com.adobe.idp.Document` pour extraire le nouveau document.

**Voir également**

[Résumé des étapes](converting-file-formats-pdf.md#summary-of-steps)

[Démarrage rapide (mode SOAP) : convertir du contenu HTML en document PDF à l’aide de l’API Java.](/help/forms/developing/generate-pdf-service-java-api.md#quick-start-soap-mode-converting-html-content-to-a-pdf-document-using-the-java-api)

[Inclusion des fichiers de bibliothèque Java d’AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Convertir un document PDF en fichier RTF à l’aide de l’API Web Service {#convert-a-pdf-document-to-a-rtf-file-using-the-web-service-api}

Convertissez un document PDF en fichier RTF à l’aide de l’API Generate PDF (Web Service) :

1. Incluez les fichiers de projet.

   Créez un projet Microsoft .NET qui utilise MTOM. Veillez à utiliser la définition WSDL suivante : `http://localhost:8080/soap/services/GeneratePDFService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Remplacez `localhost` par l’adresse IP du serveur hébergeant AEM Forms.

1. Créez un client Generate PDF.

   * Créez un objet `GeneratePDFServiceClient` en utilisant son constructeur par défaut.
   * Créez un objet `GeneratePDFServiceClient.Endpoint.Address` en utilisant le constructeur `System.ServiceModel.EndpointAddress`. Transmettez une valeur string qui spécifie le WSDL au service AEM Forms (par exemple `http://localhost:8080/soap/services/GeneratePDFService?blob=mtom`). Il n’est pas nécessaire d’utiliser l’attribut `lc_version`. Toutefois, spécifiez `?blob=mtom`.
   * Créez un objet `System.ServiceModel.BasicHttpBinding` en obtenant la valeur du champ `GeneratePDFServiceClient.Endpoint.Binding`. Convertissez la valeur de retour en `BasicHttpBinding`.
   * Définissez le champ `MessageEncoding` de l’objet `System.ServiceModel.BasicHttpBinding` sur `WSMessageEncoding.Mtom`. Cette valeur garantit l’utilisation de MTOM.
   * Activez l’authentification HTTP de base en effectuant les tâches suivantes :

      * Attribuez le nom d’utilisateur AEM forms au champ `GeneratePDFServiceClient.ClientCredentials.UserName.UserName`.
      * Attribuez la valeur de mot de passe correspondante au champ `GeneratePDFServiceClient.ClientCredentials.UserName.Password`.
      * Attribuez la valeur constante `HttpClientCredentialType.Basic` au champ `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Affectez la valeur constante `BasicHttpSecurityMode.TransportCredentialOnly` au champ `BasicHttpBindingSecurity.Security.Mode`.

1. Récupérez le document du PDF à convertir.

   * Créez un objet `BLOB` en utilisant son constructeur. L’objet `BLOB` sert à stocker un document PDF converti.
   * Créez un objet `System.IO.FileStream` en appelant son constructeur et en transmettant une valeur de chaîne représentant l’emplacement du document PDF et le mode d’ouverture du fichier.
   * Créez un tableau d’octets qui stocke le contenu de l’objet `System.IO.FileStream`. Vous pouvez déterminer la taille du tableau d’octets en obtenant la propriété `Length` de l’objet `System.IO.FileStream`.
   * Renseignez le tableau d’octets avec les données de flux en appelant la méthode `Read` de l’objet `System.IO.FileStream` et en transmettant le tableau d’octets, la position de départ et la longueur du flux à lire.
   * Renseignez l’objet `BLOB` en affectant à sa propriété `MTOM` le contenu du tableau d’octets.

1. Convertissez le document PDF.

   Appelez la méthode `ExportPDF2` de l’objet `GeneratePDFServiceServiceWse` et transmettez les valeurs suivantes :

   * Objet `BLOB` représentant le fichier PDF à convertir.
   * Chaîne contenant le nom du chemin d’accès au fichier à convertir.
   * Objet `java.lang.String` indiquant l’emplacement du fichier.
   * Objet de chaîne spécifiant le type de fichier cible pour la conversion. Spécifiez `RTF`.
   * Objet `BLOB` facultatif contenant les paramètres à appliquer lors de la génération du document PDF.
   * Paramètre de sortie de type `BLOB` renseigné par la méthode `ExportPDF2`. La méthode `ExportPDF2` renseigne cet objet avec le document converti. (Cette valeur de paramètre est requise uniquement pour l’appel du service web).

1. Enregistrez le fichier converti.

   * Récupérez le document RTF converti en attribuant au champ `MTOM` de l’objet `BLOB` un tableau d’octets. Le tableau d’octets représente le document RTF converti. Veillez à utiliser l’objet `BLOB` servant de paramètre de sortie pour la méthode `ExportPDF2`.
   * Créez un objet `System.IO.FileStream` en utilisant son constructeur. Transmettez une valeur de chaîne représentant l’emplacement du fichier RTF.
   * Créez un objet `System.IO.BinaryWriter` en appelant son constructeur et en transmettant l’objet `System.IO.FileStream`.
   * Écrivez le contenu du tableau d’octets dans un fichier RTF en appelant la méthode `Write` de l’objet `System.IO.BinaryWriter` et en transmettant le tableau d’octets.

**Voir également**

[Résumé des étapes](converting-file-formats-pdf.md#summary-of-steps)

[Appeler AEM Forms en utilisant MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Appel d’AEM Forms à l’aide de SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Ajouter la prise en charge de formats de fichier natifs supplémentaires {#adding-support-for-additional-native-file-formats}

Cette section explique comment ajouter la prise en charge de formats de fichiers natifs supplémentaires. Elle présente un aperçu des interactions entre le service Generate PDF et les applications natives utilisées par ce service pour convertir les formats de fichiers natifs en PDF.

Cette section explique également les points suivants :

* Comment modifier la réponse que le service Generate PDF fournit aux applications natives que ce produit utilise déjà pour convertir des formats de fichiers natifs en PDF.
* Les interactions entre le service Generate PDF, le composant Application Monitor (AppMon) du service Generate PDF et les applications natives, telles que Microsoft Word.
* Les rôles joués par la grammaire XML dans ces interactions.

### Les interactions entre composants. {#component-interactions}

Le service Generate PDF convertit les formats de fichiers natifs en appelant l’application associée au format de fichier, puis en interagissant avec l’application pour imprimer le document à l’aide de l’imprimante par défaut. L’imprimante par défaut doit être configurée en tant qu’imprimante Adobe PDF.

Cette illustration présente les composants et les pilotes impliqués dans la prise en charge des applications natives. Elle mentionne également les grammaires XML qui influencent les interactions.

Interactions de composants pour la conversion de fichiers natifs

Ce document utilise le terme *application native* pour indiquer l’application utilisée pour produire un format de fichier natif, tel que Microsoft Word.

*AppMon* est un composant d’entreprise qui interagit avec une application native de la même manière qu’un utilisateur navigue dans les boîtes de dialogue présentées par cette application. Les grammaires XML utilisées par AppMon pour demander à une application, comme Microsoft Word, d’ouvrir et d’imprimer un fichier impliquent les tâches séquentielles suivantes :

1. Ouvrir le fichier en sélectionnant Fichier > Ouvrir.
1. Veiller à ce que la boîte de dialogue Ouvrir s’affiche. Dans le cas contraire, gérer l’erreur.
1. Indiquer le nom du fichier dans le champ Nom du fichier, puis cliquer sur le bouton Ouvrir.
1. S’assurer que le fichier s’ouvre réellement.
1. Ouvrir la boîte de dialogue Imprimer en sélectionnant Fichier > Imprimer.
1. Vérifier que la boîte de dialogue Imprimer s’affiche.

AppMon utilise des API Win32 standard pour interagir avec des applications tierces afin de transférer des événements d’interface utilisateur tels que des touches et des clics de souris, ce qui est utile pour contrôler ces applications afin de produire des fichiers PDF à partir de ces applications.

En raison d’une limitation de ces API Win32, AppMon ne peut pas distribuer ces événements d’interface utilisateur à certains types spécifiques de fenêtres, tels que les barres de menus flottantes (présentes dans certaines applications telles que TextPad), ni certains types de boîtes de dialogue dont le contenu ne peut pas être récupéré à l’aide des API Win32.

Il est facile d’identifier visuellement une barre de menus flottante. Toutefois, il n’est pas évident d’identifier les types spéciaux de boîtes de dialogue par simple inspection visuelle. Vous avez besoin d’une application tierce, telle que Microsoft Spy++ (qui fait partie de l’environnement de développement Microsoft Visual C++) ou de son WinID équivalent (qui peut être téléchargé gratuitement à partir de [https://www.dennisbabkin.com/php/download.php?what=WinID](https://www.dennisbabkin.com/php/download.php?what=WinID)) pour examiner une boîte de dialogue afin de déterminer si AppMon peut interagir avec celle-ci à l’aide d’API Win32 standard.

Si WinID est en mesure d’extraire le contenu de la boîte de dialogue, tel que du texte, les sous-fenêtres, l’identifiant de classe de fenêtre, etc., AppMon pourra également le faire.

Ce tableau répertorie le type d’informations utilisées pour imprimer des formats de fichiers natifs.

<table>
 <thead>
  <tr>
   <th><p>Type d’informations</p></th>
   <th><p>Description</p></th>
   <th><p>Modifier/créer des entrées liées à des fichiers natifs </p></th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td><p>Paramètres d’administration </p></td>
   <td><p>Inclut les paramètres PDF, les paramètres de sécurité et les paramètres de type de fichier. </p><p>Les paramètres de type de fichier associent des extensions de nom de fichier aux applications natives correspondantes. Les paramètres de type de fichier indiquent également les paramètres d’application natifs utilisés pour imprimer des fichiers natifs. </p></td>
   <td><p>Pour modifier les paramètres d’une application native déjà prise en charge, l’administrateur système définit les paramètres de type de fichier dans la console d’administration. </p><p>Pour ajouter la prise en charge d’un nouveau format de fichier natif, vous devez modifier manuellement le fichier. (Voir <a href="converting-file-formats-pdf.md#adding-or-modifying-support-for-a-native-file-format">Ajouter ou modifier la prise en charge d’un format de fichier natif</a>.) </p></td>
  </tr>
  <tr>
   <td><p>Script </p></td>
   <td><p>Indique les interactions entre le service Generate PDF et une application native. De telles interactions demandent généralement à l’application d’imprimer un fichier pour le pilote Adobe PDF. </p><p>Le script contient des instructions qui demandent à l’application native d’ouvrir des boîtes de dialogue spécifiques et qui fournissent des réponses spécifiques aux champs et aux boutons dans ces boîtes de dialogue. </p></td>
   <td><p>Le service Generate PDF comprend des fichiers de script pour toutes les applications natives prises en charge. Vous pouvez modifier ces fichiers à l’aide d’une application d’édition XML.</p><p>Pour ajouter la prise en charge d’une nouvelle application native, vous devez créer un fichier de script. (Voir <a href="converting-file-formats-pdf.md#creating-or-modifying-an-additional-dialog-xml-file-for-a-native-application">Créer ou modifier un fichier XML de boîte de dialogue supplémentaire pour une application native</a>.) </p></td>
  </tr>
  <tr>
   <td><p>Instructions relatives à la boîte de dialogue générique </p></td>
   <td><p>Indique comment répondre à des boîtes de dialogue communes à plusieurs applications. Ces boîtes de dialogue sont générées par des systèmes d’exploitation, des applications d’assistance (telles que PDFMaker) et les pilotes. </p><p>Le fichier contenant ces informations est appmon.global.en_US.xml.</p></td>
   <td><p>Ne modifiez pas ce fichier. </p></td>
  </tr>
  <tr>
   <td><p>Instructions relatives aux boîtes de dialogue spécifiques à l’application</p></td>
   <td><p>Indique comment répondre aux boîtes de dialogue spécifiques à l’application. </p><p>Le fichier contenant ces informations est appmon.<i>`[appname]`</i>.dialog.<i>`[locale]`</i>.xml (par exemple appmon.word.en_US.xml).</p></td>
   <td><p>Ne modifiez pas ce fichier. </p><p>Pour ajouter des instructions relatives aux boîtes de dialogue pour une nouvelle application native, consultez la section <a href="converting-file-formats-pdf.md#creating_or_modifying_an_additional_dialog_xml_file_for_a_native_application">Créer ou modifier un fichier XML de boîte de dialogue supplémentaire pour une application native</a>.</p></td>
  </tr>
  <tr>
   <td><p>Instructions relatives aux boîtes de dialogue supplémentaires spécifiques à l’application </p></td>
   <td><p>Spécifie les remplacements et les ajouts aux instructions de boîte de dialogue spécifiques à l’application. Cette section présente un exemple de ces informations. </p><p>Le fichier contenant ces informations est appmon.<i>`[appname]`</i>.addition.<i>`[locale]`</i>.xml. Par exemple, appmon.addition.en_US.xml.</p></td>
   <td><p>Les fichiers de ce type peuvent être créés et modifiés à l’aide dʼune application dʼédition XML. (Consultez la section <a href="converting-file-formats-pdf.md#creating-or-modifying-an-additional-dialog-xml-file-for-a-native-application">Créer ou modifier un fichier XML de boîte de dialogue supplémentaire pour une application native</a>). </p><p><strong>Important</strong>: créez une boîte de dialogue supplémentaire spécifique à l’application pour chaque application native que votre serveur prendra en charge. </p></td>
  </tr>
 </tbody>
</table>

### À propos des fichiers XML de script et de boîte de dialogue {#about-the-script-and-dialog-xml-files}

Les fichiers XML de script demandent au service Generate PDF de parcourir les boîtes de dialogue de l’application de la même manière qu’un utilisateur le ferait. Les fichiers XML de script demandent également au service Generate PDF de répondre aux boîtes de dialogue en exécutant des actions telles qu’appuyer sur des boutons, sélectionner ou désélectionner des cases à cocher ou encore sélectionner des options de menu.

En revanche, les fichiers XML de boîte de dialogue répondent simplement aux boîtes de dialogue avec les mêmes types d’actions utilisées dans les fichiers XML de script.

#### Terminologie des éléments de boîte de dialogue et de fenêtre {#dialog-box-and-window-element-terminology}

Cette section et la section suivante emploient une terminologie différente pour les boîtes de dialogue et les composants qu’elles contiennent, en fonction du point de vue utilisé. Les composants de boîte de dialogue sont des éléments tels que des boutons, des champs et des zones de liste.

Lorsque cette section et la section suivante décrivent des boîtes de dialogue et leurs composants du point de vue d’un utilisateur, des termes tels que *boîte de dialogue*, *bouton*, *champ*, et *zone de liste* sont utilisés.

En revanche, si ces éléments sont décrits du point de vue de leur représentation interne, le terme *élément de fenêtre* est utilisé. La représentation interne des éléments de fenêtre est une hiérarchie, où chaque instance d’élément de fenêtre est identifiée par des libellés. L’instance d’élément de fenêtre décrit également ses caractéristiques physiques et son comportement.

Du point de vue de l’utilisateur ou de l’utilisatrice, les boîtes de dialogue et leurs composants présentent différents comportements, certains éléments de boîte de dialogue étant masqués jusqu’à leur activation. Du point de vue de la représentation interne, ce problème de comportement nʼexiste pas. Par exemple, la représentation interne d’une boîte de dialogue ressemble à celle des composants qu’elle contient, si ce n’est que les composants sont imbriqués dans la boîte de dialogue.

Cette section décrit les éléments XML qui fournissent des instructions à AppMon. Ces éléments portent des noms tels que élément `dialog` et élément `window`. Ce document utilise une police à espacement fixe pour distinguer les éléments XML. L’élément `dialog` identifie une boîte de dialogue qu’un fichier de script XML peut faire afficher, intentionnellement ou non. L’élément `window` identifie un élément de fenêtre (boîte de dialogue ou composants d’une boîte de dialogue).

#### Hiérarchie {#hierarchy}

Ce diagramme montre la hiérarchie des fichiers XML de script et de dialogue. Un fichier XML de script est conforme au schéma script.xsd, qui inclut (au sens XML) le schéma window.xsd. De même, un fichier XML de boîte de dialogue est conforme au schéma dialogs.xsd, qui inclut également le schéma window.xsd.

![as_as_xml_hierarchy](assets/as_as_xml_hierarchy.png)

Hiérarchie des fichiers XML de script et de dialogue

#### Fichiers XML de script {#script-xml-files}

Un *fichier XML de script* spécifie une série d’étapes qui demandent à l’application native de naviguer vers certains éléments de fenêtre, puis de fournir des réponses à ces éléments. La plupart des réponses sont du texte ou des frappes de touches qui correspondent à l’entrée quʼun utilisateur fournirait à un champ, une zone de liste ou un bouton dans la boîte de dialogue correspondante.

Le service Generate PDF prend en charge les fichiers XML de script afin de permettre à une application native d’imprimer un fichier natif. Cependant, les fichiers XML de script peuvent être utilisés pour accomplir toute tâche qu’un utilisateur ou une utilisatrice peut effectuer lors de l’interaction avec les boîtes de dialogue de l’application native.

Les étapes dʼun fichier XML de script sont exécutées dans lʼordre et chacune dʼentre elles doit obligatoirement être réalisée avant de passer à la suivante. Le seul test conditionnel pris en charge est le délai d’expiration/de nouvelle tentative, qui entraîne l’arrêt d’un script si une étape ne se termine pas correctement dans un délai spécifique et après un certain nombre de tentatives.

Outre le fait que les étapes sont séquentielles, les instructions d’une étape sont également exécutées dans l’ordre. Assurez-vous que les étapes et les instructions correspondent à l’ordre dans lequel un utilisateur effectue les mêmes étapes.

Chaque étape d’un fichier XML de script identifie l’élément de fenêtre qui doit apparaître si les instructions de l’étape sont correctement exécutées. Si une boîte de dialogue inattendue apparaît lors de l’exécution d’une action de script, le service Generate PDF recherche les fichiers XML de boîte de dialogue, comme décrit dans la section suivante.

#### Fichiers XML de boîte de dialogue {#dialog-xml-files}

Lors de l’exécution d’applications natives, différentes boîtes de dialogue sʼaffichent, que les applications natives soient en mode visible ou invisible. Les boîtes de dialogue peuvent être générées par le système d’exploitation ou par l’application elle-même. Lorsque les applications natives sont exécutées sous le contrôle du service Generate PDF, les boîtes de dialogue du système et des applications natives sont affichées dans une fenêtre invisible.

Un *fichier XML de boîte de dialogue* indique comment le service Generate PDF répond aux boîtes de dialogue système ou d’application native. Les fichiers XML de boîte de dialogue permettent au service Generate PDF de répondre aux boîtes de dialogue non demandées de manière à faciliter le processus de conversion.

Lorsque le système ou l’application native affiche une boîte de dialogue qui n’est pas gérée par le fichier XML de script en cours d’exécution, le service Generate PDF recherche les fichiers XML de boîte de dialogue dans cet ordre, et s’arrête lorsqu’il trouve une correspondance :

* appmon.`[appname]`.additional.`[locale]`.xml
* appmon.`[appname]`.`[locale]`.xml (ne modifiez pas ce fichier).
* appmon.global.`[locale]`.xml (ne modifiez pas ce fichier).

Si le service Generate PDF trouve une correspondance pour la boîte de dialogue, il la ferme en lui envoyant la frappe ou toute autre action spécifiée pour la boîte de dialogue. Si les instructions de la boîte de dialogue indiquent un message d’abandon, le service Generate PDF met fin à la tâche en cours d’exécution et génère un message d’erreur. Un tel message d’abandon serait spécifié dans l’élément `abortMessage` de la grammaire XML du script.

Si le service Generate PDF rencontre une boîte de dialogue qui n’est décrite dans aucun des fichiers répertoriés précédemment, le service Generate PDF intègre la légende de la boîte de dialogue dans l’entrée du fichier journal. La tâche en cours d’exécution finit par s’arrêter. Vous pouvez alors utiliser les informations du fichier journal pour composer de nouvelles instructions dans le fichier XML de boîte de dialogue supplémentaire pour l’application native.

### Ajouter ou modifier la prise en charge d’un format de fichier natif {#adding-or-modifying-support-for-a-native-file-format}

Cette section décrit les tâches que vous devez effectuer pour prendre en charge d’autres formats de fichiers natifs ou pour modifier la prise en charge d’un format de fichier natif déjà pris en charge.

Avant de pouvoir ajouter ou modifier la prise en charge, vous devez effectuer les tâches suivantes.

#### Choisir un outil d’identification des éléments de fenêtre {#choosing-a-tool-for-identifying-window-elements}

Les fichiers XML de boîte de dialogue et de script vous demandent d’identifier l’élément de fenêtre (boîte de dialogue, champ ou autre composant de boîte de dialogue) auquel votre élément de boîte de dialogue ou de script répond. Par exemple, lorsqu’un script appelle le menu d’une application native, il doit identifier l’élément de fenêtre de ce menu auquel des frappes ou une action doivent être appliquées.

Vous pouvez facilement identifier une boîte de dialogue par la légende qu’elle affiche dans sa barre de titre. Cependant, vous devez utiliser un outil tel que Microsoft Spy++ pour identifier les éléments de fenêtre de niveau inférieur. Les éléments de fenêtre de niveau inférieur peuvent être identifiés par divers attributs, qui ne sont pas évidents. En outre, chaque application native peut identifier son élément de fenêtre différemment. Par conséquent, il existe plusieurs façons d’identifier un élément de fenêtre. Voici l’ordre suggéré pour prendre en compte l’identification des éléments de fenêtre :

1. La légende elle-même si elle est unique.
1. L’identifiant de contrôle, qui peut être unique ou non pour une boîte de dialogue donnée.
1. Le nom de la classe, qui peut être unique ou non.

L’un ou l’autre de ces trois attributs, ou une combinaison de ceux-ci peut être utilisé pour identifier une fenêtre.

Si les attributs ne permettent pas d’identifier une légende, vous pouvez identifier un élément de fenêtre en utilisant son index par rapport à son parent. Un *index* spécifie la position de l’élément de fenêtre par rapport à ses éléments de fenêtre apparentés. Souvent, les index sont le seul moyen d’identifier les zones de liste modifiable.

Tenez compte de ces problèmes :

* Microsoft Spy++ affiche les légendes à l’aide de l’esperluette (&amp;) pour identifier la touche de raccourci de la légende. Par exemple, Spy++ affiche la légende d’une boîte de dialogue d’impression sous la forme `Pri&nt`, ce qui indique que la touche de raccourci est *n*. Les titres des légendes dans les fichiers XML des scripts et des boîtes de dialogue doivent omettre les esperluettes.
* Certaines légendes comportent des sauts de ligne. Le service Generate PDF ne peut pas identifier les sauts de ligne. Si une légende comprend un saut de ligne, incluez une partie suffisante de la légende pour la différencier des autres éléments du menu, puis utilisez des expressions régulières pour la partie omise. Un exemple est (`^Long caption title$`). (Voir [Utiliser des expressions régulières dans les attributs de légende](converting-file-formats-pdf.md#using-regular-expressions-in-caption-attributes).)
* Utilisez des entités de caractères (également appelées séquences d’échappement) pour les caractères XML réservés. Par exemple, utilisez `&` pour les esperluettes, `<` et `>` pour les symboles inférieur à ou supérieur à, `&apos;` pour les apostrophes et `&quot;` pour les guillemets.

Si vous envisagez de travailler sur des fichiers XML de boîte de dialogue ou de script, vous devez installer l’application Microsoft Spy++.

#### Décompresser les fichiers de boîte de dialogue et de script {#unpackaging-the-dialog-and-script-files}

Les fichiers de boîte de dialogue et de script résident dans le fichier appmondata.jar. Avant de pouvoir modifier l’un de ces fichiers ou ajouter de nouveaux fichiers de script ou de boîte de dialogue, vous devez décompresser ce fichier JAR. Supposons, par exemple, que vous souhaitiez ajouter la prise en charge de l’application EditPlus. Créez deux fichiers XML, nommés appmon.editplus.script.en_US.xml et appmon.editplus.script.addition.en_US.xml. Ces scripts XML doivent être ajoutés au fichier adobe-appmondata.jar à deux emplacements, comme illustré ci-dessous :

* adobe-livecycle-native-jboss-x86_win32.ear > adobe-Native2PDFSvc.war\WEB-INF\lib > adobe-native.jar > Native2PDFSvc-native.jar\bin > adobe-appmondata.jar\com\adobe\appmon. Le fichier adobe-livecycle-native-jboss-x86_win32.ear se trouve dans le dossier d’exportation à `[AEM forms install directory]\configurationManager`. (si AEM Forms est déployé sur un autre serveur d’applications J2EE, remplacez le fichier adobe-livecycle-native-jboss-x86_win32.ear par le fichier EAR correspondant à votre serveur d’applications J2EE.)
* adobe-generatepdf-dsc.jar > adobe-appmondata.jar\com\adobe\appmon (le fichier adobe-appmondata.jar se trouve dans le fichier adobe-generatepdf-dsc.jar). Le fichier adobe-generatepdf-dsc.jar se trouve dans le dossier `[AEM forms install directory]\deploy`.

Après avoir ajouté ces fichiers XML au fichier adobe-appmondata.jar, vous devez redéployer le composant GeneratePDF. Pour ajouter des fichiers XML de boîte de dialogue et de script au fichier adobe-appmondata.jar, procédez comme suit :

1. À l’aide d’un outil tel que WinZip ou WinRAR, ouvrez le fichier adobe-livecycle-native-jboss-x86_win32.earfile > adobe-Native2PDFSvc.war\WEB-INF\lib > adobe-native.jar > Native2PDFSvc-native.jar\bin > adobe-appmondata.jar.
1. Ajoutez la boîte de dialogue et les fichiers XML de script au fichier appmondata.jar ou modifiez les fichiers XML existants dans ce fichier. (Voir [Créer ou modifier un fichier XML de script pour une application native](converting-file-formats-pdf.md#creating-or-modifying-a-script-xml-file-for-a-native-application) et [Créer ou modifier un fichier XML de boîte de dialogue supplémentaire pour une application native](converting-file-formats-pdf.md#creating-or-modifying-an-additional-dialog-xml-file-for-a-native-application).)
1. À l’aide d’un outil tel que WinZip ou WinRAR, ouvrez adobe-generatepdf-dsc.jar > adobe-appmondata.jar.
1. Ajoutez la boîte de dialogue et les fichiers XML de script au fichier appmondata.jar ou modifiez les fichiers XML existants dans ce fichier. (Voir [Créer ou modifier un fichier XML de script pour une application native](converting-file-formats-pdf.md#creating-or-modifying-a-script-xml-file-for-a-native-application) et [Créer ou modifier un fichier XML de boîte de dialogue supplémentaire pour une application native](converting-file-formats-pdf.md#creating-or-modifying-an-additional-dialog-xml-file-for-a-native-application).) Après avoir ajouté les fichiers XML au fichier adobe-appmondata.jar, placez le nouveau fichier adobe-appmondata.jar dans le fichier adobe-generatepdf-dsc.jar.
1. Si vous avez ajouté la prise en charge d’un autre format de fichier natif, créez une variable d’environnement système qui fournit le chemin d’accès à l’application (voir [Créer une variable d’environnement pour localiser l’application native](converting-file-formats-pdf.md#creating-an-environment-variable-to-locate-the-native-application).)

**Pour redéployer le composant GeneratePDF**

1. Connectez-vous à Workbench.
1. Sélectionnez **Fenêtre** > **Afficher les vues** > **Composants**. Cette action ajoute la vue Composants à Workbench.
1. Faites un clic droit sur le composant GeneratePDF, puis sélectionnez **Arrêter le composant**.
1. Une fois le composant arrêté, faites un clic droit et sélectionnez Désinstaller le composant pour le supprimer.
1. Faites un clic droit sur l’icône **Composants** et sélectionnez **Installer un composant**.
1. Recherchez et sélectionnez le fichier adobe-generatepdf-dsc.jar modifié, puis cliquez sur Ouvrir. Un carré rouge s’affiche près du composant GeneratePDF.
1. Développez le composant GeneratePDF, sélectionnez Descripteurs de service, puis faites un clic droit sur Service GeneratePDF et sélectionnez Activer le service.
1. Dans la boîte de dialogue de configuration qui s’affiche, saisissez les valeurs de configuration applicables. Si vous laissez ces valeurs vides, les valeurs de configuration par défaut sont utilisées.
1. Faites un clic droit sur GeneratePDF et sélectionnez Démarrer le composant.
1. Développez Services actifs. Une flèche verte apparaît à côté du nom du service s’il est en cours d’exécution. Sinon, le service est à l’arrêt.
1. Si le service est à l’arrêt, cliquez avec le bouton droit sur le nom du service et sélectionnez Démarrer le service.

### Créer ou modifier un fichier XML de script pour une application native {#creating-or-modifying-a-script-xml-file-for-a-native-application}

Si vous souhaitez rediriger des fichiers vers une nouvelle application native, vous devez créer un fichier XML de script pour cette application. Si vous souhaitez modifier la manière dont le service Generate PDF interagit avec une application native déjà prise en charge, vous devez modifier le script de cette application.

Le script contient des instructions qui parcourent les éléments de fenêtre de l’application native et qui fournissent des réponses spécifiques à ces éléments. Le fichier qui contient ces informations est `appmon.`[appname]`` `.script.`[locale]`.xml`. Exemple : appmon.notepad.script.en_US.xml.

#### Identifier les étapes que le script doit exécuter {#identifying-steps-the-script-must-execute}

À l’aide de l’application native, déterminez les éléments de fenêtre à parcourir et chaque réponse à exécuter pour imprimer le document. Remarquez les boîtes de dialogue qui résultent de chaque réponse. Les étapes sont similaires à celles-ci :

1. Choisissez Fichier > Ouvrir.
1. Spécifiez le chemin d’accès, puis cliquez sur Ouvrir.
1. Sur la barre de menus, sélectionnez Fichier > Imprimer.
1. Spécifiez les propriétés requises pour l’imprimante.
1. Sélectionnez Imprimer et attendez que la boîte de dialogue Enregistrer sous s’affiche. La boîte de dialogue Enregistrer sous est nécessaire pour que le service Generate PDF indique la destination du fichier PDF.

#### Identifier les boîtes de dialogue spécifiées dans les attributs de légende {#identifying-the-dialogs-specified-in-caption-attributes}

Utilisez Microsoft Spy++ pour obtenir les identités des propriétés des éléments de fenêtre dans l’application native. Vous devez disposer de ces identités pour écrire des scripts.

#### Utiliser des expressions régulières dans les attributs de légende {#using-regular-expressions-in-caption-attributes}

Vous pouvez utiliser des expressions régulières dans les spécifications des légendes. Le service Generate PDF utilise la classe `java.util.regex.Matcher` pour prendre en charge les expressions régulières. Cet utilitaire prend en charge les expressions régulières décrites dans `java.util.regex.Pattern`.

**Expression régulière prenant en charge le nom du fichier précédé du Bloc-notes dans la bannière Bloc-notes**

```xml
 <!-- The regular expression ".*Notepad" means any number of non-terminating characters followed by Notepad. -->
 <step>
     <expectedWindow>
         <window caption=".*Notepad"/>
     </expectedWindow>
 </step>
```

**Expression régulière différenciant l’impression de la configuration de l’impression**

```xml
 <!-- This regular expression differentiates the Print dialog box from the Print Setup dialog box. The "^" specifies the beginning of the line, and the "$" specifies the end of the line. -->
 <windowList>
     <window controlID="0x01" caption="^Print$" action="press"/>
 </windowList>
```

#### Organiser les éléments windowList et window {#ordering-the-window-and-windowlist-elements}

Commande `window` et `windowList` comme suit :

* Lorsque plusieurs éléments `window` apparaissent en tant qu’enfants dans un élément `windowList` ou `dialog`, ordonnez ces éléments `window` par ordre décroissant, la longueur des noms `caption` indiquant la position dans l’ordre.
* Lorsque plusieurs éléments `windowList` apparaissent dans un élément `window`, ordonnez ces éléments `windowList` par ordre décroissant, les longueurs des attributs `caption` du premier élément `indexes/` indiquant la position dans l’ordre.

**Ordonner les éléments window dans un fichier de boîte de dialogue**

```xml
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

**Ordonner les éléments de fenêtre dans un élément windowList**

```xml
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

### Créer ou modifier un fichier XML de boîte de dialogue supplémentaire pour une application native {#creating-or-modifying-an-additional-dialog-xml-file-for-a-native-application}

Si vous créez un script pour une application native qui n’était pas prise en charge auparavant, vous devez également créer un fichier XML de boîte de dialogue supplémentaire pour cette application. Chaque application native utilisée par AppMon ne doit avoir quʼun seul fichier XML de boîte de dialogue supplémentaire. Le fichier XML de boîte de dialogue supplémentaire est requis même si aucune boîte de dialogue non sollicitée n’est attendue. La boîte de dialogue supplémentaire doit comporter au moins un élément `window` même si cet élément `window` n’est qu’un espace réservé.

>[!NOTE]
>
>Dans ce contexte, le terme supplémentaire désigne le contenu du fichier `appmon.[applicationname].addition.[locale].xml`. Ce fichier spécifie les remplacements et les ajouts au fichier XML de boîte de dialogue.

Vous pouvez également modifier le fichier XML de boîte de dialogue supplémentaire pour une application native à ces fins :

* Pour remplacer le fichier XML de boîte de dialogue pour une application avec une réponse différente.
* Pour ajouter une réponse à une boîte de dialogue qui n’est pas gérée dans le fichier XML de boîte de dialogue pour cette application.

Le nom du fichier qui identifie un fichier XML de boîte de dialogue supplémentaire est `appmon.[appname].addition.[locale].xml`. Exemple : appmon.excel.addition.en_US.xml.

Le nom du fichier XML de boîte de dialogue supplémentaire doit employer le format `appmon.[applicationname].addition.[locale].xml`, où *applicationname* doit correspondre exactement au nom de l’application utilisé dans le fichier de configuration XML et dans le script.

>[!NOTE]
>
>Aucune des applications génériques spécifiées dans le fichier de configuration native2pdfconfig.xml ne possède de fichier XML de boîte de dialogue principal. La section [Ajouter ou modifier la prise en charge d’un format de fichier natif](converting-file-formats-pdf.md#adding-or-modifying-support-for-a-native-file-format) décrit de telles spécifications.

Commande `windowList` éléments qui apparaissent comme enfants dans un `window` élément . (Consultez la section [Ordonner les éléments window et windowList](converting-file-formats-pdf.md#ordering-the-window-and-windowlist-elements)).

### Modifier le fichier XML de la boîte de dialogue générale {#modifying-the-general-dialog-xml-file}

Vous pouvez modifier le fichier XML de la boîte de dialogue générale pour répondre aux boîtes de dialogue générées par le système ou pour répondre aux boîtes de dialogue communes à plusieurs applications.

#### Ajouter une entrée de type fichier dans le fichier de configuration XML {#adding-a-filetype-entry-in-the-xml-configuration-file}

Cette procédure explique comment mettre à jour le fichier de configuration du service Generate PDF afin dʼassocier les types de fichiers aux applications natives. Pour mettre à jour ce fichier de configuration, vous devez utiliser la console d’administration pour exporter les données de configuration vers un fichier. Le nom de fichier par défaut des données de configuration est native2pdfconfig.xml.

**Mettre à jour le fichier de configuration du service Generate PDF**

1. Sélectionnez **Accueil** > **Services** > **Adobe PDF Generator** > **Fichiers de configuration**, puis sélectionnez **Exporter la configuration**.
1. Modifiez l’élément `filetype-settings` au besoin dans le fichier native2pdfconfig.xml.
1. Sélectionnez **Accueil** > **Services** > **Adobe PDF Generator** > **Fichiers de configuration**, puis cliquez sur **Importer la configuration**. Les données de configuration sont importées dans le service Generate PDF et remplacent les paramètres précédents.

>[!NOTE]
>
>Le nom de l’application est spécifié comme la valeur de l’attribut `name` de l’élément `GenericApp`. Cette valeur doit correspondre exactement au nom spécifié dans le script que vous développez pour cette application. De même, l’attribut `displayName` de l’élément `GenericApp` doit correspondre exactement à la légende de fenêtre `expectedWindow` du script correspondant. Une telle équivalence est évaluée après résolution de toutes les expressions régulières qui apparaissent dans les attributs `displayName` ou `caption`.

Dans cet exemple, les données de configuration par défaut fournies avec le service Generate PDF ont été modifiées afin de spécifier que le Bloc-notes (et non Microsoft Word) doit être utilisé pour traiter les fichiers portant l’extension .txt. Avant cette modification, Microsoft Word était spécifié comme application native pour le traitement de ces fichiers.

**Modifications pour ouvrir les fichiers texte avec le Bloc-notes (native2pdfconfig.xml)**

```xml
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

#### Créer une variable d’environnement pour localiser l’application native {#creating-an-environment-variable-to-locate-the-native-application}

Créez une variable d’environnement qui spécifie l’emplacement du fichier exécutable de l’application native. La variable doit utiliser le format `[applicationname]_PATH`, où *applicationname* doit correspondre exactement au nom de l’application utilisé dans le fichier de configuration XML et dans le script, et où le chemin contient le chemin d’accès de l’exécutable entre guillemets. Exemple de variable d’environnement de ce type : `Photoshop_PATH`.

Après avoir créé la nouvelle variable d’environnement, vous devez redémarrer le serveur sur lequel le service Generate PDF est déployé.

>[!NOTE]
>
> Il est recommandé d’utiliser la commande &quot;Ctrl + C&quot; pour redémarrer le serveur SDK. Le redémarrage du serveur AEM SDK à l’aide d’autres méthodes, par exemple l’arrêt des processus Java, peut entraîner des incohérences dans l’environnement de développement AEM.

**Créer une variable système dans l’environnement Windows XP**

1. Sélectionnez **Panneau de Contrôle > Système**.
1. Dans la boîte de dialogue Propriétés du système, cliquez sur le bouton **Avancé**, puis cliquez sur **Variables d’environnement**.
1. Sous Variables système dans la boîte de dialogue Variables d’environnement, cliquez sur **Nouveau**.
1. Dans la boîte de dialogue Nouvelle variable système, dans la case **Nom de variable**, saisissez un nom qui utilise le format `[applicationname]_PATH`.
1. Dans le champ **Valeur de variable**, saisissez le chemin d’accès complet et le nom de fichier du fichier exécutable de l’application, puis cliquez sur **OK**. Par exemple, saisissez: `c:\windows\Notepad.exe`
1. Dans la boîte de dialogue Variables d’environnement, cliquez sur **OK**.

**Créer une variable système à partir de la ligne de commande**

1. Dans une fenêtre de ligne de commande, saisissez la définition de la variable au format suivant :

   ```shell
            [applicationname]_PATH=[Full path name]
   ```

   Par exemple, saisissez: `NotePad_PATH=C:\WINDOWS\NOTEPAD.EXE`

1. Démarrez une nouvelle invite de ligne de commande pour que la variable système prenne effet.

#### Fichiers XML {#xml-files}

AEM Forms comprend des exemples de fichiers XML qui font en sorte que le service Generate PDF utilise le Bloc-notes pour traiter tous les fichiers avec l’extension .txt. Ce code est inclus dans cette section. En outre, vous devez apporter les autres modifications décrites dans cette section.

#### Fichier XML de boîte de dialogue supplémentaire {#additional-dialog-xml-file}

Cet exemple contient les boîtes de dialogue supplémentaires pour l’application Bloc-notes. Ces boîtes de dialogue peuvent s’ajouter à celles spécifiées par le service Generate PDF.

**Boîtes de dialogue du Bloc-notes (appmon.notepad.addition.fr_FR.xml)**

```xml
 <dialogs app="Notepad" locale="en_US" version="7.0" xmlns:xsi="https://www.w3.org/2001/XMLSchema-instance" xsi:noNamespaceSchemaLocation="dialogs.xsd">
     <window caption="Caption Title">
         <windowList>
             <window className="Button" caption="OK" action="press"/>
         </windowList>
     </window>
 </dialogs>
```

#### Fichier XML de script {#script-xml-file}

Cet exemple montre comment le service Generate PDF doit interagir avec le Bloc-notes pour imprimer des fichiers à l’aide de l’imprimante PDF Adobe.

**Fichier XML de script du Bloc-notes (appmon.notepad.script.fr_FR.xml)**

```xml
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

<!-- This file automates printing of text files via notepad to Adobe PDF printer. To see the complete hierarchy Adobe recommends using the Microsoft Spy++ which details the properties of windows necessary to write scripts. In this sample there are total of eight steps-->

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

    <!-- In this step, we acquire the Print dialog and click the 'Preferences' button and the expected window in this case is the dialog with the caption '"Printing Preferences' -->
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

    <!-- In this step, we acquire the dialog "Printing Preferences' and select the combo box which is the 10th child of window with caption '"Adobe PDF Settings' and select the first index. (Note: All indeces start with 0.) Besides this we uncheck the box which has the caption '"View Adobe PDF results' and we click the button OK. The expectation is that 'Printing Preferences' dialog disappears. -->
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

    <!-- In this step, we acquire the 'Print' dialog and click the Print button. The expectation is that the dialog with caption 'Print' disappears. In this case we use the regular expression '^Print$' for specifying the caption given there could be multiple dialogs with caption that includes the word Print. -->
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
    <!-- Finally in this step, we acquire the dialog with caption "Save PDF File As" and in the Edit widget type the destination path for the output PDF file and click the Save button. The expectation is that the dialog disappears-->
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
