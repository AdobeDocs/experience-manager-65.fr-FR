---
title: Conversion de fichiers PDF en fichiers Postscript et Image
seo-title: Conversion de fichiers PDF en fichiers Postscript et Image
description: 'null'
seo-description: 'null'
uuid: 07da0391-7180-4197-aaa6-ae753d753b84
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: f8707752-2c83-461a-b83d-708754b0f3f6
translation-type: tm+mt
source-git-commit: f9389a06f9c2cd720919486765cee76257f272c3

---


# Conversion de fichiers PDF en fichiers Postscript et Image {#converting-pdf-to-postscript-andimage-files}

**A propos du service Convert PDF**

Le service Convert PDF convertit les  PDF au format PostScript et dans divers formats d’image (JPEG, JPEG 2000, PNG et TIFF). La conversion d’un document PDF en PostScript est utile pour les impressions sans assistance reposant sur un serveur exécutées sur n’importe quelle imprimante PostScript. La conversion d’un document PDF en fichier TIFF comportant plusieurs pages est pratique lors de l’archivage de documents dans des systèmes de gestion de contenu qui ne prennent pas en charge les documents PDF.

Vous pouvez accomplir ces  de à l’aide du service Convert PDF :

* Convertir des documents PDF en PostScript.
* Convertissez les  PDF en formats d’image.

>[!NOTE]
>
>For more information about the Convert PDF service, see [Services Reference for AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

## Converting PDF Documents to PostScript {#converting-pdf-documents-to-postscript}

Cette rubrique explique comment utiliser l’API Convert PDF Service (Java et service Web) pour convertir par programmation des  PDF en fichiers PostScript. Le  PDF converti en fichier PostScript doit être un PDF non interactif. En d’autres termes, si vous tentez de convertir un PDF interactif en fichier PostScript, une exception est générée.

>[!NOTE]
>
>For more information about the Convert PDF service, see [Services Reference for AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Résumé des étapes {#summary-of-steps}

Pour convertir un PDF en fichier PostScript, procédez comme suit :

1. Incluez des fichiers de projet.
1. Créez un client de service Convert PDF.
1. Référencez le PDF à convertir en fichier PostScript.
1. Définissez les options d’exécution de conversion.
1. Convertissez le PDF en fichier PostScript.
1. Enregistrez le fichier PostScript.

**Inclure les fichiers de projet**

Incluez les fichiers nécessaires dans votre projet de développement. Si vous créez une application cliente à l’aide de Java, incluez les fichiers JAR nécessaires. Si vous utilisez des services Web, veillez à inclure les fichiers proxy.

**Création d’un client Convert PDF**

Avant de pouvoir exécuter une opération de service Convert PDF par programmation, vous devez créer un client de service Convert PDF. Si vous utilisez l’API Java, créez un `ConvertPdfServiceClient` objet. Si vous utilisez l’API du service Web, créez un `ConvertPDFServiceService` objet.

Cette section utilise la fonctionnalité de service Web introduite dans AEM Forms. Pour accéder à une nouvelle fonctionnalité, vous devez construire votre objet proxy à l’aide de l’ `lc_version` attribut. (voir &quot;Accès à de nouvelles fonctionnalités à l’aide de services Web&quot; dans [Appel d’AEM Forms à l’aide de services](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-web-services)Web).

**Référencer le PDF à convertir en fichier PostScript**

Référencez le PDF que vous souhaitez convertir en fichier PostScript. Comme indiqué précédemment dans cette rubrique, le  PDF doit être un PDF non interactif. Si vous tentez de convertir un PDF interactif en fichier PostScript, une exception est générée.

**Définition des options d’exécution de conversion**

Lors de la conversion d’un PDF en fichier PostScript, vous pouvez définir des options d’exécution qui spécifient le type PostScript créé. Par exemple, vous pouvez définir un fichier PostScript de niveau 3.

En règle générale, le fichier PostScript généré reflète la taille du PDF d’entrée. Si vous sélectionnez l’ `ShrinkToFit` option (qui réduit la sortie du fichier PostScript pour l’adapter à la page), vous ne verrez pas de différence entre le  PDF d’entrée et le fichier PostScript généré. L’ `ShrinkToFit` option prend effet uniquement si vous choisissez d’imprimer sur une page plus petite que le  PDF d’entrée. Pour sélectionner un format de page plus petit, définissez l’ `PageSize` option. En outre, il est recommandé de définir l’ `RotateAndCenter` option `true` pour obtenir la sortie PostScript appropriée.

De même, si vous sélectionnez l’ `ExpandToFit` option (qui étend la sortie du fichier PostScript pour l’adapter à la page), elle ne prend effet que si vous choisissez d’imprimer sur une taille de page supérieure à la  PDF d’entrée. Pour sélectionner un format de page plus grand, définissez l’ `PageSize` option. En outre, il est recommandé de définir l’ `RotateAndCenter` option `true` pour obtenir la sortie PostScript appropriée.

>[!NOTE]
>
>Pour plus d’informations sur les valeurs d’exécution que vous pouvez définir, voir la référence de `ToPSOptionsSpec` classe dans Référence [API](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)AEM Forms.

**Conversion du PDF en fichier PostScript**

Après avoir créé le client de service et défini les options d’exécution, vous pouvez appeler l’opération de conversion PostScript. Cette opération nécessite des informations sur le à convertir, y compris le niveau PostScript préféré pour l’  de.

**Enregistrement du fichier PostScript**

Après avoir converti le PDF au format PostScript, vous pouvez enregistrer la sortie dans un fichier PostScript.

**Voir également**

[Conversion d’un PDF en PS à l’aide de l’API Java](converting-pdf-postscript-image-files.md#convert-a-pdf-document-to-ps-using-the-java-api)

[Conversion d’un PDF en PS à l’aide de l’API du service Web](converting-pdf-postscript-image-files.md#convert-a-pdf-document-to-ps-using-the-web-service-api)

[Inclusion des fichiers de bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[rapide de l’API du service Conversion PDF](/help/forms/developing/convert-pdf-service-java-api.md#convert-pdf-service-java-api-quick-start-soap)

### Conversion d’un PDF en PS à l’aide de l’API Java {#convert-a-pdf-document-to-ps-using-the-java-api}

Conversion d’un PDF en PostScript à l’aide de l’API de service Convert PDF (Java) :

1. Incluez des fichiers de projet.

   Incluez des fichiers JAR client, tels que adobe-convertpdf-client.jar, dans le chemin de classe de votre projet Java.

1. Créez un client Convert PDF.

   * Créez un objet `ServiceClientFactory` qui contient des propriétés de connexion.
   * Créez un objet `ConvertPdfServiceClient` en utilisant son constructeur et en transmettant l’objet `ServiceClientFactory`. 

1. Référencez le PDF à convertir en fichier PostScript.

   * Créez un `java.io.FileInputStream` objet à l’aide de son constructeur et transmettez une valeur de chaîne indiquant l’emplacement du PDF à convertir.
   * Créez un `com.adobe.idp.Document` objet qui stocke le PDF à l’aide du `com.adobe.idp.Document` constructeur. Transmettez l’ `java.io.FileInputStream` objet contenant le  PDF.

1. Définissez les options d’exécution de conversion.

   * Create a `ToPSOptionsSpec` object by invoking its constructor.
   * Définissez les options d’exécution en appelant une méthode appropriée qui appartient à l’ `ToPSOptionsSpec` objet. Par exemple, pour définir le niveau PostScript créé, appelez la `ToPSOptionsSpec` méthode de l’ `setPsLevel` objet et transmettez une valeur de `PSLevel` qui spécifie le niveau PostScript. Pour plus d’informations sur toutes les valeurs d’exécution que vous pouvez définir, voir la référence de `ToPSOptionsSpec` classe dans le Guide de référence [de l’API](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)AEM Forms.

1. Convertissez le PDF en fichier PostScript.

   Appelez la méthode `ConvertPdfServiceClient`de l’ `toPS2` objet et transmettez les valeurs suivantes :

   * Objet `com.adobe.idp.Document` représentant le PDF à convertir en fichier PostScript.
   * Objet `ToPSOptionsSpec` spécifiant les options d’exécution PostScript.
   La `toPS2` méthode renvoie un `Document` objet qui contient le nouveau  PostScript.

1. Enregistrez le fichier PostScript.

   * Create a `java.io.File` object and ensure that the file name extension is .ps.
   * Appelez la `Document` méthode de l’ `copyToFile` objet pour copier le contenu de l’ `Document` objet dans le fichier (veillez à utiliser l’ `Document` objet renvoyé par la `toPS2` méthode).

**Voir également**

[Résumé des étapes](converting-pdf-postscript-image-files.md#summary-of-steps)

[rapide (mode SOAP) : Conversion d’un PDF en PostScript à l’aide de l’API Java](/help/forms/developing/convert-pdf-service-java-api.md#quick-start-soap-mode-converting-a-pdf-document-to-postscript-using-the-java-api)

[Inclusion des fichiers de bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Conversion d’un PDF en PS à l’aide de l’API du service Web {#convert-a-pdf-document-to-ps-using-the-web-service-api}

Conversion d’un PDF en PostScript à l’aide de l’API Convert PDF Service (service Web) :

1. Incluez des fichiers de projet.

   Créez un projet Microsoft .NET qui utilise MTOM. Veillez à utiliser la définition WSDL suivante : `http://localhost:8080/soap/services/ConvertPDFService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Remplacez `localhost` par l’adresse IP du serveur hébergeant AEM Forms.

1. Créez un client Convert PDF.

   * Create a `ConvertPdfServiceClient` object by using its default constructor.
   * Create a `ConvertPdfServiceClient.Endpoint.Address` object by using the `System.ServiceModel.EndpointAddress` constructor. Transmettez une valeur de chaîne qui spécifie le WSDL au service AEM Forms (par exemple, `http://localhost:8080/soap/services/ConvertPDFService?blob=mtom`). Vous n’avez pas besoin d’utiliser l’ `lc_version` attribut. Spécifiez toutefois `?blob=mtom`.
   * Créez un `System.ServiceModel.BasicHttpBinding` objet en obtenant la valeur du `ConvertPdfServiceClient.Endpoint.Binding` champ. Convertissez la valeur de retour en `BasicHttpBinding`.
   * Définissez le `System.ServiceModel.BasicHttpBinding` champ de l’ `MessageEncoding` objet sur `WSMessageEncoding.Mtom`. Cette valeur garantit l’utilisation de MTOM.
   * Activez l’authentification HTTP de base en effectuant le  suivant :

      * Attribuez le nom d’utilisateur d’AEM forms au champ `ConvertPdfServiceClient.ClientCredentials.UserName.UserName`.
      * Attribuez la valeur de mot de passe correspondante au champ `ConvertPdfServiceClient.ClientCredentials.UserName.Password`.
      * Attribuez la valeur constante `HttpClientCredentialType.Basic` au champ `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Attribuez la valeur constante `BasicHttpSecurityMode.TransportCredentialOnly` au champ `BasicHttpBindingSecurity.Security.Mode`.

1. Référencez le PDF à convertir en fichier PostScript.

   * Créez un objet `BLOB` en utilisant son constructeur. L’ `BLOB` objet est utilisé pour stocker un PDF converti en fichier PostScript.
   * Créez un `System.IO.FileStream` objet en appelant son constructeur et en transmettant une valeur de chaîne représentant l’emplacement du fichier du PDF à convertir et le mode d’ouverture du fichier.
   * Créez un tableau d’octets qui stocke le contenu de l’ `System.IO.FileStream` objet. Vous pouvez déterminer la taille du tableau d’octets en obtenant la `System.IO.FileStream` `Length` propriété de l’objet.
   * Renseignez le tableau d’octets avec les données de flux en appelant la `System.IO.FileStream` `Read` méthode de l’objet et en transmettant le tableau d’octets, la position de départ et la longueur du flux à lire.
   * Renseignez l’ `BLOB` objet en affectant son `MTOM` champ au contenu du tableau d’octets.

1. Définissez les options d’exécution de conversion.

   * Create a `ToPSOptionsSpec` object by invoking its constructor.
   * Définissez les options d’exécution en attribuant une valeur au membre de données de l’ `ToPSOptionsSpec` objet. Par exemple, pour définir le niveau PostScript qui est créé, affectez une `PSLevel` valeur  au membre `ToPSOptionsSpec` `psLevel` de données de l’objet.

1. Convertissez le PDF en fichier PostScript.

   Appelez la méthode `GeneratePDFServiceService` `toPS2` de l’objet et transmettez les valeurs suivantes :

   * Objet `BLOB` représentant le PDF à convertir en fichier PostScript
   * Objet `ToPSOptionsSpec` spécifiant les options d’exécution
   Une fois la conversion terminée, extrayez les données binaires qui représentent le PostScript en accédant à la `BLOB` propriété de son `MTOM` objet. Cette opération renvoie un tableau d’octets que vous pouvez écrire dans un fichier PostScript.

1. Enregistrez le fichier PostScript.

   * Create a `System.IO.FileStream` object by invoking its constructor. Transmettez une valeur de chaîne qui représente l’emplacement du fichier PS.
   * Créez un tableau d’octets qui stocke le contenu des données de l’ `BLOB` objet renvoyé par la `encryptPDFUsingPassword` méthode. Renseignez le tableau d’octets en obtenant la valeur du champ de l’ `BLOB` objet `MTOM` .
   * Create a `System.IO.BinaryWriter` object by invoking its constructor and passing the `System.IO.FileStream` object.
   * Ecrivez le contenu du tableau d’octets dans le fichier PostScript en appelant la `System.IO.BinaryWriter` `Write` méthode de l’objet et en transmettant le tableau d’octets.

**Voir également**

[Résumé des étapes](converting-pdf-postscript-image-files.md#summary-of-steps)

[Appel d’AEM Forms à l’aide de MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Appel d’AEM Forms à l’aide de SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Conversion de  PDF au format d’image {#converting-pdf-documents-to-image-formats}

Vous pouvez utiliser le service Convert PDF pour convertir par programmation des  PDF aux formats d’image, notamment JPEG, JPEG 2000, TIFF et PNG. En convertissant un  PDF en fichier image, vous pouvez utiliser le PDF  comme fichier image. Vous pouvez, par exemple, placer l’image dans un système de  d’entreprise pour .

Lors de la conversion d’un PDF en image, le service Convert PDF crée une image distincte pour chaque page de l’ de. En d’autres termes, si le  compte 20 pages, le service Convert PDF crée 20 fichiers image. Lors de la conversion d’un PDF en format d’image, vous pouvez créer des images individuelles pour chaque page du  PDF ou un fichier d’image unique pour l’ensemble duPDF.

>[!NOTE]
>
>For more information about the Convert PDF service, see [Services Reference for AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Résumé des étapes {#summary_of_steps-1}

Pour convertir un PDF en l’un des types pris en charge, procédez comme suit :

1. Incluez des fichiers de projet.
1. Créez un client de service Convert PDF.
1. Récupérez le PDF à convertir.
1. Définissez les options d’exécution.
1. Convertissez le PDF en image.
1. Récupérez les fichiers image d’une collection.

**Inclure les fichiers de projet**

Incluez les fichiers nécessaires dans votre projet de développement. Si vous créez une application cliente à l’aide de Java, incluez les fichiers JAR nécessaires. Si vous utilisez des services Web, veillez à inclure les fichiers proxy.

**Création d’un client Convert PDF**

Avant de pouvoir exécuter une opération de service Convert PDF par programmation, vous devez créer un client de service Convert PDF. Si vous utilisez l’API Java, créez un `ConvertPdfServiceClient` objet. Si vous utilisez l’API du service Web, créez un `ConvertPDFServiceService` objet.

**Récupérer le PDF à convertir**

Vous devez récupérer le PDF à convertir en image. Vous ne pouvez pas convertir un PDF interactif en image. Si vous tentez de le faire, une exception est levée. Pour convertir un  PDF interactif en fichier image, vous devez aplatir le PDF  avant de le convertir. (voir [Aplatissement des](/help/forms/developing/creating-document-output-streams.md#flattening-pdf-documents)PDF).

**Définition des options d’exécution**

Vous devez définir des options d’exécution telles que le format d’image et les valeurs de résolution. Pour plus d’informations sur les valeurs d’exécution, voir la référence de `ToImageOptionsSpec` classe dans le Guide de référence [de l’API](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)AEM Forms.

**Convertir le PDF en image**

Après avoir créé le client de service et défini les options d’exécution, vous pouvez convertir le PDF en image. Un objet de collection contenant les images est renvoyé.

**Récupération des fichiers image d’une collection**

Vous pouvez récupérer des fichiers image à partir d’un objet de collection renvoyé par le service Convert PDF. Chaque élément de la collection est une `com.adobe.idp.Document` instance (ou une `BLOB` instance si vous utilisez des services Web) que vous pouvez enregistrer en tant que fichier image, tel qu’un fichier JPG.

Le format du fichier image dépend de l’option d’ `ImageConvertFormat` exécution. En d’autres termes, si vous définissez l’option `ImageConvertFormat` d’exécution sur `ImageConvertFormat.JPEG`, vous pouvez enregistrer des fichiers d’image au format JPG.

**Voir également**

[Inclusion des fichiers de bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[rapide de l’API du service Conversion PDF](/help/forms/developing/convert-pdf-service-java-api.md#convert-pdf-service-java-api-quick-start-soap)

### Conversion d’un PDF en fichiers image à l’aide de l’API Java {#convert-a-pdf-document-to-image-files-using-the-java-api}

Conversion d’un PDF en format d’image à l’aide de l’API du service Convert PDF (Java) :

1. Incluez des fichiers de projet.

   Incluez des fichiers JAR client, tels que adobe-convertpdf-client.jar, dans le chemin de classe de votre projet Java.

1. Créez un client Convert PDF.

   * Créez un objet `ServiceClientFactory` qui contient des propriétés de connexion.
   * Créez un objet `ConvertPdfServiceClient` en utilisant son constructeur et en transmettant l’objet `ServiceClientFactory`. 

1. Récupérez le PDF à convertir.

   * Créez un `java.io.FileInputStream` objet représentant le PDF à convertir à l’aide de son constructeur et transmettez une valeur de chaîne indiquant l’emplacement du  du PDF.
   * Créez un objet `com.adobe.idp.Document` en utilisant son constructeur et en transmettant l’objet `java.io.FileInputStream`. 

1. Définissez les options d’exécution.

   * Créez un objet `ToImageOptionsSpec` en utilisant son constructeur.
   * Appelez les méthodes qui appartiennent à cet objet selon les besoins. Par exemple, définissez le type d’image en appelant la `setImageConvertFormat` méthode et en transmettant une valeur `ImageConvertFormat` enum qui spécifie le type de format.
   >[!NOTE]
   >
   >La définition de la `ImageConvertFormat` valeur  est obligatoire.

1. Convertissez le PDF en image.

   Appelez la méthode `ConvertPdfServiceClient` `toImage2` de l’objet et transmettez les valeurs suivantes :

   * Objet `com.adobe.idp.Document` représentant le fichier PDF à convertir.
   * Objet `com.adobe.livecycle.converpdfservice.client.ToImageOptionsSpec` contenant les différentes préférences relatives au format d’image  du.
   La `toImage2` méthode renvoie un `java.util.List` objet contenant des images. Chaque élément de la collection est une `com.adobe.idp.Document` instance.

1. Récupérez les fichiers image d’une collection.

   Effectuez une itération dans l’ `java.util.List` objet pour déterminer si des images sont présentes. Chaque élément est une `com.adobe.idp.Document` instance. Enregistrez l’image en appelant la `com.adobe.idp.Document` méthode de l’objet et en transmettant un `copyToFile` `java.io.File` objet.

**Voir également**

[rapide (mode SOAP) : Conversion d’un PDF en fichiers JPEG à l’aide de l’API Java](/help/forms/developing/convert-pdf-service-java-api.md#quick-start-soap-mode-converting-a-pdf-document-to-jpeg-files-using-the-java-api)

### Conversion d’un PDF en fichiers image à l’aide de l’API du service Web {#convert-a-pdf-document-to-image-files-using-the-web-service-api}

Conversion d’un PDF en format d’image à l’aide de l’API Convert PDF Service (service Web) :

1. Incluez des fichiers de projet.

   Créez un projet Microsoft .NET qui utilise MTOM. Veillez à utiliser la définition WSDL suivante : `http://localhost:8080/soap/services/ConvertPDFService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Remplacez `localhost` par l’adresse IP du serveur hébergeant AEM Forms.

1. Créez un client PDF converti.

   * Create a `ConvertPdfServiceClient` object by using its default constructor.
   * Create a `ConvertPdfServiceClient.Endpoint.Address` object by using the `System.ServiceModel.EndpointAddress` constructor. Transmettez une valeur de chaîne qui spécifie le WSDL au service AEM Forms (par exemple, `http://localhost:8080/soap/services/ConvertPDFService?blob=mtom`). Vous n’avez pas besoin d’utiliser l’ `lc_version` attribut. Spécifiez toutefois `?blob=mtom`.
   * Créez un `System.ServiceModel.BasicHttpBinding` objet en obtenant la valeur du `ConvertPdfServiceClient.Endpoint.Binding` champ. Convertissez la valeur de retour en `BasicHttpBinding`.
   * Définissez le `System.ServiceModel.BasicHttpBinding` champ de l’ `MessageEncoding` objet sur `WSMessageEncoding.Mtom`. Cette valeur garantit l’utilisation de MTOM.
   * Activez l’authentification HTTP de base en effectuant le  suivant :

      * Attribuez le nom d’utilisateur d’AEM forms au champ `ConvertPdfServiceClient.ClientCredentials.UserName.UserName`.
      * Attribuez la valeur de mot de passe correspondante au champ `ConvertPdfServiceClient.ClientCredentials.UserName.Password`.
      * Attribuez la valeur constante `HttpClientCredentialType.Basic` au champ `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Attribuez la valeur constante `BasicHttpSecurityMode.TransportCredentialOnly` au champ `BasicHttpBindingSecurity.Security.Mode`.

1. Récupérez le PDF à convertir.

   * Créez un objet `BLOB` en utilisant son constructeur. Cet `BLOB` objet est utilisé pour stocker le formulaire PDF.
   * Create a `System.IO.FileStream` object by invoking its constructor. Transmettez une valeur de chaîne qui spécifie l’emplacement du formulaire PDF et le mode d’ouverture du fichier.
   * Créez un tableau d’octets qui stocke le contenu de l’ `System.IO.FileStream` objet. Déterminez la taille du tableau d’octets en obtenant la `System.IO.FileStream` `Length` propriété de l’objet.
   * Renseignez le tableau d’octets avec les données de flux en appelant la `System.IO.FileStream` `Read` méthode de l’objet. Passez le tableau d’octets, la position de départ et la longueur du flux à lire.
   * Renseignez l’ `BLOB` objet en affectant son `MTOM` champ au contenu du tableau d’octets.

1. Définissez les options d’exécution.

   * Créez un objet `ToImageOptionsSpec` en utilisant son constructeur.
   * Appelez les méthodes qui appartiennent à cet objet selon les besoins. Par exemple, définissez le type d’image en appelant la `setImageConvertFormat` méthode et en transmettant une valeur de  `ImageConvertFormat` qui spécifie le type de format.
   >[!NOTE]
   >
   >La définition de la `ImageConvertFormat` valeur  est obligatoire.

1. Convertissez le PDF en image.

   Appelez la méthode `ConvertPDFServiceService` `toImage2` de l’objet et transmettez les valeurs suivantes :

   * Objet `BLOB` représentant le fichier à convertir
   * Objet `ToImageOptionsSpec` contenant les différentes préférences concernant le format d’image 
   La `toImage2` méthode renvoie un `MyArrayOfBLOB` objet contenant les fichiers image nouvellement créés.

1. Récupérez les fichiers image d’une collection.

   * Déterminez le nombre d’éléments dans l’ `MyArrayOfBLOB` objet en obtenant la valeur de son `Count` champ. Chaque élément est un `BLOB` objet qui contient l’image.
   * Effectuez une itération dans l’ `MyArrayOfBLOB` objet et enregistrez chaque fichier image.

**Voir également**

[Appel d’AEM Forms à l’aide de MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Appel d’AEM Forms à l’aide de SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)
