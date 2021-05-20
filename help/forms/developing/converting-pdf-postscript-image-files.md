---
title: Conversion de fichiers PDF en fichiers Postscript et Image
seo-title: Conversion de fichiers PDF en fichiers Postscript et Image
description: Utilisez le service Convert PDF pour convertir des documents PDF au format PostScript et dans plusieurs formats d’image (JPEG, JPEG 2000, PNG et TIFF) à l’aide de l’API Java et de l’API Web Service.
seo-description: Utilisez le service Convert PDF pour convertir des documents PDF au format PostScript et dans plusieurs formats d’image (JPEG, JPEG 2000, PNG et TIFF) à l’aide de l’API Java et de l’API Web Service.
uuid: 07da0391-7180-4197-aaa6-ae753d753b84
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: f8707752-2c83-461a-b83d-708754b0f3f6
role: Developer
exl-id: 31730c24-46c3-4111-9391-ccd4342740e9
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '2846'
ht-degree: 5%

---

# Conversion de PDF en fichiers Postscript et image {#converting-pdf-to-postscript-andimage-files}

**Les exemples et les exemples de ce document sont réservés à l’environnement AEM Forms on JEE.**

**À propos du service Convert PDF**

Le service Convert PDF convertit les documents PDF en PostScript et en plusieurs formats d’image (JPEG, JPEG 2000, PNG et TIFF). La conversion d’un document PDF en PostScript est utile pour les impressions sans assistance reposant sur un serveur exécutées sur n’importe quelle imprimante PostScript. La conversion d’un document PDF en fichier TIFF comportant plusieurs pages est pratique lors de l’archivage de documents dans des systèmes de gestion de contenu qui ne prennent pas en charge les documents PDF.

Vous pouvez accomplir ces tâches à l’aide du service Convert PDF :

* Convertir des documents PDF en PostScript.
* Convertir des documents PDF en formats d’image.

>[!NOTE]
>
>Pour plus d’informations sur le service Convert PDF, voir [Référence des services pour AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

## Conversion de documents PDF en PostScript {#converting-pdf-documents-to-postscript}

Cette rubrique décrit l’utilisation de l’API Convert PDF Service (Java et service Web) pour convertir des documents PDF par programmation en fichiers PostScript. Le document PDF converti en fichier PostScript doit être un document PDF non interactif. En d’autres termes, si vous tentez de convertir un document PDF interactif en fichier PostScript, une exception est générée.

>[!NOTE]
>
>Pour plus d’informations sur le service Convert PDF, voir [Référence des services pour AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Résumé des étapes {#summary-of-steps}

Pour convertir un document PDF en fichier PostScript, procédez comme suit :

1. Inclure les fichiers de projet.
1. Créez un client de service Convert PDF.
1. Référencez le document PDF à convertir en fichier PostScript.
1. Définissez les options d’exécution de conversion.
1. Convertissez le document PDF en fichier PostScript.
1. Enregistrez le fichier PostScript.

**Inclure les fichiers de projet**

Incluez les fichiers nécessaires dans votre projet de développement. Si vous créez une application cliente à l’aide de Java, incluez les fichiers JAR nécessaires. Si vous utilisez des services Web, veillez à inclure les fichiers proxy.

**Création d’un client Convert PDF**

Avant d’effectuer par programmation une opération de service Convert PDF, vous devez créer un client de service Convert PDF. Si vous utilisez l’API Java, créez un objet `ConvertPdfServiceClient` . Si vous utilisez l’API de service Web, créez un objet `ConvertPDFServiceService` .

Cette section utilise la fonctionnalité de service Web introduite dans AEM Forms. Pour accéder à la nouvelle fonctionnalité, vous devez construire votre objet proxy à l’aide de l’attribut `lc_version`. (Voir &quot;Accès aux nouvelles fonctionnalités à l’aide des services web&quot; dans [Appel d’AEM Forms à l’aide des services web](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-web-services).)

**Référence au document PDF à convertir en fichier PostScript**

Référencez le document PDF que vous souhaitez convertir en fichier PostScript. Comme indiqué précédemment dans cette rubrique, le document PDF doit être un document PDF non interactif. Si vous tentez de convertir un document PDF interactif en fichier PostScript, une exception est générée.

**Définition des options d’exécution de conversion**

Lors de la conversion d’un document PDF en fichier PostScript, vous pouvez définir des options d’exécution spécifiant le type PostScript créé. Vous pouvez par exemple définir un fichier PostScript de niveau 3.

En règle générale, le fichier PostScript généré reflète la taille du document PDF d’entrée. Si vous sélectionnez l’option `ShrinkToFit` (qui réduit la sortie du fichier PostScript pour l’adapter à la page), vous ne verrez aucune différence entre le document PDF d’entrée et le fichier PostScript généré. L’option `ShrinkToFit` ne prend effet que si vous choisissez d’imprimer sur une page plus petite que le document PDF d’entrée. Pour sélectionner un format de page plus petit, définissez l&#39;option `PageSize`. En outre, il est recommandé de définir l’option `RotateAndCenter` sur `true` pour obtenir la sortie PostScript correcte.

De même, si vous sélectionnez l’option `ExpandToFit` (qui étend la sortie du fichier PostScript pour l’adapter à la page), elle ne prend effet que si vous choisissez d’imprimer sur une page plus grande que le document PDF d’entrée. Pour sélectionner une taille de page plus grande, définissez l&#39;option `PageSize`. En outre, il est recommandé de définir l’option `RotateAndCenter` sur `true` pour obtenir la sortie PostScript correcte.

>[!NOTE]
>
>Pour plus d’informations sur les valeurs d’exécution que vous pouvez définir, voir la référence de classe `ToPSOptionsSpec` dans [Référence de l’API AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

**Convertir le document PDF en fichier PostScript**

Après avoir créé le client de service et défini les options d’exécution, vous pouvez appeler l’opération de conversion PostScript. Cette opération nécessite des informations sur le document à convertir, y compris le niveau PostScript préféré pour le document cible.

**Enregistrement du fichier PostScript**

Après avoir converti le document PDF en PostScript, vous pouvez enregistrer la sortie en tant que fichier PostScript.

**Voir également**

[Convertir un document PDF en PS à l’aide de l’API Java](converting-pdf-postscript-image-files.md#convert-a-pdf-document-to-ps-using-the-java-api)

[Convertir un document PDF en PS à l’aide de l’API de service Web](converting-pdf-postscript-image-files.md#convert-a-pdf-document-to-ps-using-the-web-service-api)

[Inclusion des fichiers de bibliothèque Java d’AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Démarrages rapides de l’API Convert PDF Service](/help/forms/developing/convert-pdf-service-java-api.md#convert-pdf-service-java-api-quick-start-soap)

### Convertir un document PDF en PS à l’aide de l’API Java {#convert-a-pdf-document-to-ps-using-the-java-api}

Convertir un document PDF en PostScript à l’aide de l’API Convert PDF Service (Java) :

1. Inclure les fichiers de projet.

   Incluez les fichiers JAR client, tels que adobe-convertpdf-client.jar, dans le chemin de classe de votre projet Java.

1. Créez un client Convert PDF.

   * Créez un objet `ServiceClientFactory` qui contient des propriétés de connexion.
   * Créez un objet `ConvertPdfServiceClient` en utilisant son constructeur et en transmettant l’objet `ServiceClientFactory`. 

1. Référencez le document PDF à convertir en fichier PostScript.

   * Créez un objet `java.io.FileInputStream` en utilisant son constructeur et transmettez une valeur string qui spécifie l’emplacement du document PDF à convertir.
   * Créez un objet `com.adobe.idp.Document` qui stocke le document PDF à l’aide du constructeur `com.adobe.idp.Document`. Transmettez l’objet `java.io.FileInputStream` contenant le document PDF.

1. Définissez les options d’exécution de conversion.

   * Créez un objet `ToPSOptionsSpec` en appelant son constructeur.
   * Définissez les options d’exécution en appelant une méthode appropriée qui appartient à l’objet `ToPSOptionsSpec`. Par exemple, pour définir le niveau PostScript créé, appelez la méthode `setPsLevel` de l’objet `ToPSOptionsSpec` et transmettez une valeur d’énumération `PSLevel` qui spécifie le niveau PostScript. Pour plus d’informations sur toutes les valeurs d’exécution que vous pouvez définir, voir la référence de classe `ToPSOptionsSpec` dans [Référence de l’API AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

1. Convertissez le document PDF en fichier PostScript.

   Appelez la méthode `toPS2` de l’objet `ConvertPdfServiceClient`et transmettez les valeurs suivantes :

   * Objet `com.adobe.idp.Document` représentant le document PDF à convertir en fichier PostScript.
   * Objet `ToPSOptionsSpec` spécifiant les options d’exécution PostScript.

   La méthode `toPS2` renvoie un objet `Document` contenant le nouveau document PostScript.

1. Enregistrez le fichier PostScript.

   * Créez un objet `java.io.File` et assurez-vous que l’extension de nom de fichier est .ps.
   * Appelez la méthode `copyToFile` de l’objet `Document` pour copier le contenu de l’objet `Document` dans le fichier (veillez à utiliser l’objet `Document` renvoyé par la méthode `toPS2` ).

**Voir également**

[Résumé des étapes](converting-pdf-postscript-image-files.md#summary-of-steps)

[Démarrage rapide (mode SOAP) : Conversion d’un document PDF en PostScript à l’aide de l’API Java](/help/forms/developing/convert-pdf-service-java-api.md#quick-start-soap-mode-converting-a-pdf-document-to-postscript-using-the-java-api)

[Inclusion des fichiers de bibliothèque Java d’AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Convertir un document PDF en PS à l’aide de l’API de service Web {#convert-a-pdf-document-to-ps-using-the-web-service-api}

Convertir un document PDF en PostScript à l’aide de l’API Convert PDF Service (service Web) :

1. Inclure les fichiers de projet.

   Créez un projet Microsoft .NET qui utilise MTOM. Assurez-vous d’utiliser la définition WSDL suivante : `http://localhost:8080/soap/services/ConvertPDFService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Remplacez `localhost` par l’adresse IP du serveur hébergeant AEM Forms.

1. Créez un client Convert PDF.

   * Créez un objet `ConvertPdfServiceClient` à l’aide de son constructeur par défaut.
   * Créez un objet `ConvertPdfServiceClient.Endpoint.Address` à l’aide du constructeur `System.ServiceModel.EndpointAddress`. Transmettez une valeur string qui spécifie le WSDL au service AEM Forms (par exemple, `http://localhost:8080/soap/services/ConvertPDFService?blob=mtom`). Vous n’avez pas besoin d’utiliser l’attribut `lc_version`. Spécifiez toutefois `?blob=mtom`.
   * Créez un objet `System.ServiceModel.BasicHttpBinding` en obtenant la valeur du champ `ConvertPdfServiceClient.Endpoint.Binding`. Convertissez la valeur de retour en `BasicHttpBinding`.
   * Définissez le champ `MessageEncoding` de l’objet `System.ServiceModel.BasicHttpBinding` sur `WSMessageEncoding.Mtom`. Cette valeur garantit l’utilisation de MTOM.
   * Activez l’authentification HTTP de base en effectuant les tâches suivantes :

      * Attribuez le nom d’utilisateur AEM forms au champ `ConvertPdfServiceClient.ClientCredentials.UserName.UserName`.
      * Attribuez la valeur de mot de passe correspondante au champ `ConvertPdfServiceClient.ClientCredentials.UserName.Password`.
      * Attribuez la valeur constante `HttpClientCredentialType.Basic` au champ `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Attribuez la valeur constante `BasicHttpSecurityMode.TransportCredentialOnly` au champ `BasicHttpBindingSecurity.Security.Mode`.

1. Référencez le document PDF à convertir en fichier PostScript.

   * Créez un objet `BLOB` en utilisant son constructeur. L’objet `BLOB` est utilisé pour stocker un document PDF converti en fichier PostScript.
   * Créez un objet `System.IO.FileStream` en appelant son constructeur et en transmettant une valeur string qui représente l’emplacement du fichier du document PDF à convertir et le mode d’ouverture du fichier.
   * Créez un tableau d’octets qui stocke le contenu de l’objet `System.IO.FileStream`. Vous pouvez déterminer la taille du tableau d’octets en obtenant la propriété `System.IO.FileStream` de l’objet `Length`.
   * Renseignez le tableau d’octets avec les données de diffusion en appelant la méthode `Read` de l’objet `System.IO.FileStream` et en transmettant le tableau d’octets, la position de départ et la longueur du flux à lire.
   * Renseignez l’objet `BLOB` en attribuant son champ `MTOM` avec le contenu du tableau d’octets.

1. Définissez les options d’exécution de conversion.

   * Créez un objet `ToPSOptionsSpec` en appelant son constructeur.
   * Définissez les options d’exécution en attribuant une valeur au membre de données de l’objet `ToPSOptionsSpec`. Par exemple, pour définir le niveau PostScript créé, affectez une valeur d’énumération `PSLevel` au membre de données `psLevel` de l’objet `ToPSOptionsSpec`.

1. Convertissez le document PDF en fichier PostScript.

   Appelez la méthode `toPS2` de l’objet `GeneratePDFServiceService` et transmettez les valeurs suivantes :

   * Objet `BLOB` représentant le document PDF à convertir en fichier PostScript.
   * Objet `ToPSOptionsSpec` spécifiant les options d’exécution

   Une fois la conversion terminée, extrayez les données binaires représentant le document PostScript en accédant à la propriété `MTOM` de l’objet `BLOB`. Cette opération renvoie un tableau d’octets que vous pouvez écrire dans un fichier PostScript.

1. Enregistrez le fichier PostScript.

   * Créez un objet `System.IO.FileStream` en appelant son constructeur. Transmettez une valeur string qui représente l’emplacement du fichier PS.
   * Créez un tableau d’octets qui stocke le contenu des données de l’objet `BLOB` renvoyé par la méthode `encryptPDFUsingPassword`. Renseignez le tableau d’octets en obtenant la valeur du champ `MTOM` de l’objet `BLOB`.
   * Créez un objet `System.IO.BinaryWriter` en appelant son constructeur et en transmettant l’objet `System.IO.FileStream`.
   * Ecrivez le contenu du tableau d’octets dans le fichier PostScript en appelant la méthode `System.IO.BinaryWriter` de l’objet `Write` et en transmettant le tableau d’octets.

**Voir également**

[Résumé des étapes](converting-pdf-postscript-image-files.md#summary-of-steps)

[Appel d’AEM Forms à l’aide de MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Appel d’AEM Forms à l’aide de SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Conversion de documents PDF au format d’image {#converting-pdf-documents-to-image-formats}

Vous pouvez utiliser le service Convert PDF pour convertir des documents PDF par programmation en formats d’image, notamment JPEG, JPEG 2000, TIFF et PNG. En convertissant un document PDF en fichier image, vous pouvez utiliser le document PDF comme fichier image. Par exemple, vous pouvez placer l’image dans un système de gestion de contenu d’entreprise à des fins de stockage.

Lors de la conversion d’un document PDF en image, le service Convert PDF crée une image distincte pour chaque page du document. En d’autres termes, si le document comporte 20 pages, le service Convert PDF crée 20 fichiers image. Lors de la conversion d’un document PDF au format d’image, vous pouvez créer des images individuelles pour chaque page du document PDF ou un seul fichier image pour l’ensemble du document PDF.

>[!NOTE]
>
>Pour plus d’informations sur le service Convert PDF, voir [Référence des services pour AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Résumé des étapes {#summary_of_steps-1}

Pour convertir un document PDF en l’un des types pris en charge, procédez comme suit :

1. Inclure les fichiers de projet.
1. Créez un client de service Convert PDF.
1. Récupérez le document PDF à convertir.
1. Définissez les options d’exécution.
1. Convertir le PDF en image.
1. Récupérez les fichiers image d’une collection.

**Inclure les fichiers de projet**

Incluez les fichiers nécessaires dans votre projet de développement. Si vous créez une application cliente à l’aide de Java, incluez les fichiers JAR nécessaires. Si vous utilisez des services Web, veillez à inclure les fichiers proxy.

**Création d’un client Convert PDF**

Avant d’effectuer par programmation une opération de service Convert PDF, vous devez créer un client de service Convert PDF. Si vous utilisez l’API Java, créez un objet `ConvertPdfServiceClient` . Si vous utilisez l’API de service Web, créez un objet `ConvertPDFServiceService` .

**Récupération du document PDF à convertir**

Vous devez récupérer le document PDF à convertir en image. Vous ne pouvez pas convertir un document PDF interactif en image. Si vous tentez de le faire, une exception est générée. Pour convertir un document PDF interactif en fichier image, vous devez aplatir le document PDF avant de le convertir. (Voir [Aplatissement de documents PDF](/help/forms/developing/creating-document-output-streams.md#flattening-pdf-documents).)

**Définition des options d’exécution**

Vous devez définir les options d’exécution, telles que le format de l’image et les valeurs de résolution. Pour plus d’informations sur les valeurs d’exécution, voir la référence de classe `ToImageOptionsSpec` dans [Référence de l’API AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

**Convertir le PDF en image**

Après avoir créé le client de service et défini les options d’exécution, vous pouvez convertir le document PDF en image. Un objet de collection contenant les images est renvoyé.

**Récupération des fichiers image d’une collection**

Vous pouvez récupérer des fichiers image à partir d’un objet de collection que le service Convert PDF renvoie. Chaque élément de la collection est une instance `com.adobe.idp.Document` (ou une instance `BLOB` si vous utilisez des services Web) que vous pouvez enregistrer en tant que fichier image, tel qu’un fichier JPG.

Le format du fichier image dépend de l’option d’exécution `ImageConvertFormat`. En d’autres termes, si vous définissez l’option d’exécution `ImageConvertFormat` sur `ImageConvertFormat.JPEG`, vous pouvez enregistrer des fichiers image en tant que fichiers JPG.

**Voir également**

[Inclusion des fichiers de bibliothèque Java d’AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Démarrages rapides de l’API Convert PDF Service](/help/forms/developing/convert-pdf-service-java-api.md#convert-pdf-service-java-api-quick-start-soap)

### Convertir un document PDF en fichiers image à l’aide de l’API Java {#convert-a-pdf-document-to-image-files-using-the-java-api}

Convertir un document PDF en format d’image à l’aide de l’API du service Convert PDF (Java) :

1. Inclure les fichiers de projet.

   Incluez les fichiers JAR client, tels que adobe-convertpdf-client.jar, dans le chemin de classe de votre projet Java.

1. Créez un client Convert PDF.

   * Créez un objet `ServiceClientFactory` qui contient des propriétés de connexion.
   * Créez un objet `ConvertPdfServiceClient` en utilisant son constructeur et en transmettant l’objet `ServiceClientFactory`. 

1. Récupérez le document PDF à convertir.

   * Créez un objet `java.io.FileInputStream` qui représente le document PDF à convertir en utilisant son constructeur et en transmettant une valeur string qui spécifie l’emplacement du document PDF.
   * Créez un objet `com.adobe.idp.Document` en utilisant son constructeur et en transmettant l’objet `java.io.FileInputStream`. 

1. Définissez les options d’exécution.

   * Créez un objet `ToImageOptionsSpec` en utilisant son constructeur.
   * Appelez les méthodes qui appartiennent à cet objet selon les besoins. Par exemple, définissez le type d’image en appelant la méthode `setImageConvertFormat` et en transmettant une valeur d’énumération `ImageConvertFormat` qui spécifie le type de format.

   >[!NOTE]
   >
   >La définition de la valeur de l&#39;énumération `ImageConvertFormat` est obligatoire.

1. Convertir le PDF en image.

   Appelez la méthode `toImage2` de l’objet `ConvertPdfServiceClient` et transmettez les valeurs suivantes :

   * Objet `com.adobe.idp.Document` représentant le fichier PDF à convertir.
   * Objet `com.adobe.livecycle.converpdfservice.client.ToImageOptionsSpec` contenant les différentes préférences concernant le format d’image cible.

   La méthode `toImage2` renvoie un objet `java.util.List` contenant des images. Chaque élément de la collection est une instance `com.adobe.idp.Document`.

1. Récupérez les fichiers image d’une collection.

   Effectuez une itération sur l’objet `java.util.List` pour déterminer si des images sont présentes. Chaque élément est une instance `com.adobe.idp.Document`. Enregistrez l’image en appelant la méthode `com.adobe.idp.Document` de l’objet `copyToFile` et en transmettant un objet `java.io.File`.

**Voir également**

[Démarrage rapide (mode SOAP) : Conversion d’un document PDF en fichiers JPEG à l’aide de l’API Java](/help/forms/developing/convert-pdf-service-java-api.md#quick-start-soap-mode-converting-a-pdf-document-to-jpeg-files-using-the-java-api)

### Convertir un document PDF en fichiers image à l’aide de l’API de service Web {#convert-a-pdf-document-to-image-files-using-the-web-service-api}

Convertir un document PDF en format d’image à l’aide de l’API Convert PDF Service (service Web) :

1. Inclure les fichiers de projet.

   Créez un projet Microsoft .NET qui utilise MTOM. Assurez-vous d’utiliser la définition WSDL suivante : `http://localhost:8080/soap/services/ConvertPDFService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Remplacez `localhost` par l’adresse IP du serveur hébergeant AEM Forms.

1. Créez un client convert PDF.

   * Créez un objet `ConvertPdfServiceClient` à l’aide de son constructeur par défaut.
   * Créez un objet `ConvertPdfServiceClient.Endpoint.Address` à l’aide du constructeur `System.ServiceModel.EndpointAddress`. Transmettez une valeur string qui spécifie le WSDL au service AEM Forms (par exemple, `http://localhost:8080/soap/services/ConvertPDFService?blob=mtom`). Vous n’avez pas besoin d’utiliser l’attribut `lc_version`. Spécifiez toutefois `?blob=mtom`.
   * Créez un objet `System.ServiceModel.BasicHttpBinding` en obtenant la valeur du champ `ConvertPdfServiceClient.Endpoint.Binding`. Convertissez la valeur de retour en `BasicHttpBinding`.
   * Définissez le champ `MessageEncoding` de l’objet `System.ServiceModel.BasicHttpBinding` sur `WSMessageEncoding.Mtom`. Cette valeur garantit l’utilisation de MTOM.
   * Activez l’authentification HTTP de base en effectuant les tâches suivantes :

      * Attribuez le nom d’utilisateur AEM forms au champ `ConvertPdfServiceClient.ClientCredentials.UserName.UserName`.
      * Attribuez la valeur de mot de passe correspondante au champ `ConvertPdfServiceClient.ClientCredentials.UserName.Password`.
      * Attribuez la valeur constante `HttpClientCredentialType.Basic` au champ `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Attribuez la valeur constante `BasicHttpSecurityMode.TransportCredentialOnly` au champ `BasicHttpBindingSecurity.Security.Mode`.

1. Récupérez le document PDF à convertir.

   * Créez un objet `BLOB` en utilisant son constructeur. Cet objet `BLOB` est utilisé pour stocker le formulaire PDF.
   * Créez un objet `System.IO.FileStream` en appelant son constructeur. Transmettez une valeur string qui spécifie l’emplacement du formulaire PDF et le mode d’ouverture du fichier.
   * Créez un tableau d’octets qui stocke le contenu de l’objet `System.IO.FileStream`. Déterminez la taille du tableau d’octets en obtenant la propriété `System.IO.FileStream` de l’objet `Length`.
   * Renseignez le tableau d’octets avec les données de diffusion en appelant la méthode `Read` de l’objet `System.IO.FileStream`. Transmettez le tableau d’octets, la position de départ et la longueur du flux à lire.
   * Renseignez l’objet `BLOB` en attribuant son champ `MTOM` avec le contenu du tableau d’octets.

1. Définissez les options d’exécution.

   * Créez un objet `ToImageOptionsSpec` en utilisant son constructeur.
   * Appelez les méthodes qui appartiennent à cet objet selon les besoins. Par exemple, définissez le type d’image en appelant la méthode `setImageConvertFormat` et en transmettant une valeur d’énumération `ImageConvertFormat` qui spécifie le type de format.

   >[!NOTE]
   >
   >La définition de la valeur de l&#39;énumération `ImageConvertFormat` est obligatoire.

1. Convertir le PDF en image.

   Appelez la méthode `toImage2` de l’objet `ConvertPDFServiceService` et transmettez les valeurs suivantes :

   * Objet `BLOB` représentant le fichier à convertir
   * Objet `ToImageOptionsSpec` contenant les différentes préférences concernant le format d’image cible

   La méthode `toImage2` renvoie un objet `MyArrayOfBLOB` contenant les fichiers image nouvellement créés.

1. Récupérez les fichiers image d’une collection.

   * Déterminez le nombre d’éléments dans l’objet `MyArrayOfBLOB` en obtenant la valeur de son champ `Count`. Chaque élément est un objet `BLOB` contenant l’image.
   * Effectuez une itération sur l’objet `MyArrayOfBLOB` et enregistrez chaque fichier image.

**Voir également**

[Appel d’AEM Forms à l’aide de MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Appel d’AEM Forms à l’aide de SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)
