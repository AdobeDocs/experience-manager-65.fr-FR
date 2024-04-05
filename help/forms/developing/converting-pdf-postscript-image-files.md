---
title: Convertir des PDF en fichiers Postscript et dʼimage
description: Utilisez le service Convert PDF pour convertir des documents PDF en PostScript et en plusieurs formats d’image (JPEG, JPEG 2000, PNG et TIFF) à l’aide de l’API Java et de l’API de service web.
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
role: Developer
exl-id: 31730c24-46c3-4111-9391-ccd4342740e9
solution: Experience Manager, Experience Manager Forms
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '2774'
ht-degree: 100%

---

# Convertir des PDF en fichiers Postscript et dʼimage {#converting-pdf-to-postscript-andimage-files}

**Les exemples et les échantillons de ce document sont réservés à l’environnement AEM Forms sur JEE.**

**À propos du service Convert PDF**

Le service Convert PDF convertit des documents PDF en fichiers PostScript ou en plusieurs formats d’image (JPEG, JPEG 2000, PNG et TIFF). La conversion d’un document PDF en PostScript est utile pour les impressions sans assistance reposant sur un serveur exécutées sur n’importe quelle imprimante PostScript. La conversion d’un document PDF en fichier TIFF comportant plusieurs pages est pratique lors de l’archivage de documents dans des systèmes de gestion de contenu qui ne prennent pas en charge les documents PDF.

Le service Convert PDF vous permet dʼeffectuer les tâches suivantes :

* Convertir des documents PDF en PostScript.
* Convertir des documents PDF en formats d’image.

>[!NOTE]
>
>Pour plus d’informations sur le service Convert PDF, consultez la section [Références des services pour AEM Forms](https://help.adobe.com/fr_FR/livecycle/11.0/Services/index.html).

## Convertir des documents PDF en PostScript {#converting-pdf-documents-to-postscript}

Cette rubrique décrit lʼutilisation de l’API Convert PDF Service (Java et service web) afin de convertir par programmation des documents PDF en fichiers PostScript. Le document PDF converti en fichier PostScript doit être un document PDF non interactif. Dans le cas contraire, une exception est générée.

>[!NOTE]
>
>Pour plus d’informations sur le service Convert PDF, consultez la section [Références des services pour AEM Forms](https://help.adobe.com/fr_FR/livecycle/11.0/Services/index.html).

### Résumé des étapes {#summary-of-steps}

Pour convertir un document PDF en fichier PostScript, procédez comme suit :

1. Incluez les fichiers de projet.
1. Créez un client du service Convert PDF.
1. Référencez le document PDF à convertir en fichier PostScript.
1. Définissez les options d’exécution de conversion.
1. Convertissez un document PDF en fichier PostScript.
1. Enregistrez le fichier PostScript.

**Inclure des fichiers de projet**

Incluez les fichiers nécessaires dans votre projet de développement. Si vous créez une application cliente à l’aide de Java, incluez les fichiers JAR nécessaires. Si vous utilisez des services web, veillez à inclure les fichiers proxy.

**Créer un client PDF Convert**

Avant d’effectuer par programmation une opération du service Convert PDF, vous devez créer un client de service Convert PDF. Si vous utilisez l’API Java, créez un objet `ConvertPdfServiceClient`. Si vous utilisez l’API de service web, créez un objet `ConvertPDFServiceService`.

Cette section utilise la nouvelle fonctionnalité de service web introduite dans AEM Forms. Pour accéder à cette nouvelle fonctionnalité, vous devez construire votre objet proxy à l’aide de lʼattribut `lc_version`. (Consultez la rubrique « Accéder aux nouvelles fonctionnalités à l’aide des services web » dans la section [Appeler AEM Forms à l’aide de services web](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-web-services).)

**Référencer le document PDF à convertir en fichier PostScript**

Référencez le document PDF à convertir en fichier PostScript. Comme indiqué précédemment dans cette rubrique, le document PDF doit être non interactif. Si vous tentez de convertir un document PDF interactif en fichier PostScript, une exception est générée.

**Définir des options d’exécution pour la conversion**

Lors de la conversion d’un document PDF en fichier PostScript, vous pouvez définir des options d’exécution spécifiant le type de fichier PostScript créé. Vous pouvez, par exemple, définir un fichier PostScript Level 3.

En règle générale, la taille du fichier PostScript généré correspond à celle du document PDF d’entrée. Si vous sélectionnez lʼoption `ShrinkToFit` (qui réduit la sortie du fichier PostScript pour lʼajuster à la page), vous ne verrez pas de différence entre le document PDF dʼentrée et le fichier PostScript généré. Lʼoption `ShrinkToFit` ne prend effet que si vous choisissez dʼimprimer sur un format de page inférieur à celui du document PDF dʼentrée. Pour sélectionner un format de page inférieur, définissez lʼoption `PageSize`. En outre, il est recommandé de définir lʼoption `RotateAndCenter` sur `true` pour obtenir la sortie PostScript correcte.

De même, si vous sélectionnez lʼoption `ExpandToFit` (qui ajuste la sortie du fichier PostScript pour lʼadapter à la page), elle ne prend effet que si vous choisissez dʼimprimer sur un format de page supérieur à celui du document PDF dʼentrée. Pour sélectionner un format de page supérieur, définissez lʼoption `PageSize`. En outre, il est recommandé de définir lʼoption `RotateAndCenter` sur `true` pour obtenir la sortie PostScript correcte.

>[!NOTE]
>
>Pour plus d’informations sur les valeurs d’exécution qui peuvent être définies, consultez la référence de classe `ToPSOptionsSpec` dans la section [Référence de l’API AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

**Convertir le document PDF en fichier PostScript**

Une fois le client de service créé et les options d’exécution définies, vous pouvez appeler l’opération de conversion PostScript. Cette opération nécessite des informations sur le document à convertir, y compris le niveau PostScript préféré pour le document cible.

**Enregistrer le fichier PostScript**

Après avoir converti le document PDF en PostScript, vous pouvez enregistrer la sortie en tant que fichier PostScript.

**Voir également**

[Convertir un document PDF en PS à l’aide de l’API Java](converting-pdf-postscript-image-files.md#convert-a-pdf-document-to-ps-using-the-java-api)

[Convertir un document PDF en PS à l’aide de l’API Web Service](converting-pdf-postscript-image-files.md#convert-a-pdf-document-to-ps-using-the-web-service-api)

[Inclusion des fichiers de bibliothèque Java d’AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Démarrages rapides de l’API Convert PDF Service](/help/forms/developing/convert-pdf-service-java-api.md#convert-pdf-service-java-api-quick-start-soap)

### Convertir un document PDF en PS à l’aide de l’API Java {#convert-a-pdf-document-to-ps-using-the-java-api}

Convertissez un document PDF en PostScript à l’aide de l’API Convert PDF Service (Java) :

1. Incluez les fichiers de projet.

   Incluez les fichiers JAR du client, tels qu’adobe-livecycle-client.jar, dans le chemin d’accès aux classes de votre projet Java.

1. Créez un client PDF Convert.

   * Créez un objet `ServiceClientFactory` qui contient des propriétés de connexion.
   * Créez un objet `ConvertPdfServiceClient` en utilisant son constructeur et en transmettant l’objet `ServiceClientFactory`. 

1. Référencez le document PDF à convertir en fichier PostScript.

   * Créez un objet `java.io.FileInputStream` en utilisant son constructeur et en transmettant une valeur string qui spécifie l’emplacement du document PDF à convertir.
   * Créez un objet `com.adobe.idp.Document` qui stocke le document PDF à l’aide du constructeur `com.adobe.idp.Document`. Transmettez l’objet `java.io.FileInputStream` contenant le document PDF.

1. Définissez les options d’exécution de conversion.

   * Créez un objet `ToPSOptionsSpec` en utilisant son constructeur.
   * Définissez les options d’exécution en appelant une méthode appropriée appartenant à l’objet `ToPSOptionsSpec`. Par exemple, pour définir le niveau PostScript créé, appelez la méthode `setPsLevel` de l’objet `ToPSOptionsSpec` et transmettez une valeur d’énumération `PSLevel` spécifiant le niveau PostScript. Pour plus d’informations sur toutes les valeurs d’exécution que vous pouvez définir, voir la référence de classe `ToPSOptionsSpec` dans [Référence de l’API AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

1. Convertissez un document PDF en fichier PostScript.

   Appelez la méthode `toPS2` de l’objet `ConvertPdfServiceClient` et transmettez les valeurs suivantes :

   * Objet `com.adobe.idp.Document` représentant le document PDF à convertir en fichier PostScript.
   * Objet `ToPSOptionsSpec` spécifiant les options d’exécution PostScript.

   La méthode `toPS2` renvoie un objet `Document` contenant le nouveau document PostScript.

1. Enregistrez le fichier PostScript.

   * Créez un objet `java.io.File` et assurez-vous que l’extension du fichier est .ps.
   * Appelez la méthode `copyToFile` de l’objet `Document` pour copier le contenu de l’objet `Document` dans le fichier (veillez à utiliser l’objet `Document` qui a été renvoyé par la méthode `toPS2`).

**Voir également**

[Résumé des étapes](converting-pdf-postscript-image-files.md#summary-of-steps)

[Démarrage rapide (mode SOAP) : convertir un document PDF en PostScript à l’aide de l’API Java.](/help/forms/developing/convert-pdf-service-java-api.md#quick-start-soap-mode-converting-a-pdf-document-to-postscript-using-the-java-api)

[Inclusion des fichiers de bibliothèque Java d’AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Convertir un document PDF en PS à l’aide de l’API Web Service {#convert-a-pdf-document-to-ps-using-the-web-service-api}

Convertissez un document PDF en PostScript à l’aide de l’API Convert PDF Service (Web Service) :

1. Incluez les fichiers de projet.

   Créez un projet Microsoft .NET qui utilise MTOM. Veillez à utiliser la définition WSDL suivante : `http://localhost:8080/soap/services/ConvertPDFService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Remplacez `localhost` avec l’adresse IP du serveur hébergeant AEM Forms.

1. Créez un client PDF Convert.

   * Créez un objet `ConvertPdfServiceClient` en utilisant son constructeur par défaut.
   * Créez un objet `ConvertPdfServiceClient.Endpoint.Address` en utilisant le constructeur `System.ServiceModel.EndpointAddress`. Transmettez une valeur string qui spécifie le WSDL au service AEM Forms (par exemple `http://localhost:8080/soap/services/ConvertPDFService?blob=mtom`). Il n’est pas nécessaire d’utiliser l’attribut `lc_version`. Toutefois, spécifiez `?blob=mtom`.
   * Créez un objet `System.ServiceModel.BasicHttpBinding` en obtenant la valeur du champ `ConvertPdfServiceClient.Endpoint.Binding`. Convertissez la valeur de retour en `BasicHttpBinding`.
   * Définissez le champ `MessageEncoding` de l’objet `System.ServiceModel.BasicHttpBinding` sur `WSMessageEncoding.Mtom`. Cette valeur garantit l’utilisation de MTOM.
   * Activez l’authentification HTTP de base en effectuant les tâches suivantes :

      * Attribuez le nom d’utilisateur AEM forms au champ `ConvertPdfServiceClient.ClientCredentials.UserName.UserName`.
      * Attribuez la valeur de mot de passe correspondante au champ `ConvertPdfServiceClient.ClientCredentials.UserName.Password`.
      * Attribuez la valeur constante `HttpClientCredentialType.Basic` au champ `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Attribuez la valeur constante `BasicHttpSecurityMode.TransportCredentialOnly` au champ `BasicHttpBindingSecurity.Security.Mode`.

1. Référencez le document PDF à convertir en fichier PostScript.

   * Créez un objet `BLOB` en utilisant son constructeur. Lʼobjet `BLOB` sert à stocker un document PDF converti en fichier PostScript.
   * Créez un objet `System.IO.FileStream` en appelant son constructeur et en transmettant une valeur de chaîne, qui représente l’emplacement du fichier du document PDF à convertir et son mode d’ouverture.
   * Créez un tableau d’octets qui stocke le contenu de l’objet `System.IO.FileStream`. Vous pouvez déterminer la taille du tableau d’octets en obtenant la propriété `Length` de l’objet `System.IO.FileStream`.
   * Renseignez le tableau d’octets avec les données de flux en appelant la méthode `Read` de l’objet `System.IO.FileStream` et en transmettant le tableau d’octets, la position de départ et la longueur du flux à lire.
   * Renseignez l’objet `BLOB` en attribuant à son champ `MTOM` le contenu du tableau d’octets.

1. Définissez les options d’exécution de conversion.

   * Créez un objet `ToPSOptionsSpec` en utilisant son constructeur.
   * Définissez les options d’exécution en affectant une valeur au membre de données de l’objet `ToPSOptionsSpec`. Par exemple, pour définir le niveau PostScript créé, affectez une valeur d’énumération `PSLevel` au membre de données `psLevel` de l’objet `ToPSOptionsSpec`.

1. Convertissez un document PDF en fichier PostScript.

   Appelez la méthode `toPS2` de l’objet `GeneratePDFServiceService` et transmettez les valeurs suivantes :

   * Objet `BLOB` représentant le document PDF à convertir en fichier PostScript.
   * Objet `ToPSOptionsSpec` spécifiant les options d’exécution.

   Une fois la conversion terminée, extrayez les données binaires représentant le document PostScript en accédant à la propriété `MTOM` de son objet `BLOB`. Cette opération renvoie un tableau d’octets que vous pouvez écrire dans un fichier PostScript.

1. Enregistrez le fichier PostScript.

   * Créez un objet `System.IO.FileStream` en utilisant son constructeur. Transmettez une valeur string qui représente l’emplacement du fichier PS.
   * Créez un tableau d’octets qui stocke le contenu des données de l’objet `BLOB` qui a été renvoyé par la méthode `encryptPDFUsingPassword`. Renseignez le tableau d’octets en obtenant la valeur du champ `MTOM` de l’objet `BLOB`.
   * Créez un objet `System.IO.BinaryWriter` en utilisant son constructeur et en transmettant l’objet `System.IO.FileStream`.
   * Écrivez le contenu du tableau d’octets dans le fichier PostScript en appelant la méthode `Write` de l’objet `System.IO.BinaryWriter` et en transmettant le tableau d’octets.

**Voir également**

[Résumé des étapes](converting-pdf-postscript-image-files.md#summary-of-steps)

[Appeler AEM Forms en utilisant MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Appel d’AEM Forms à l’aide de SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)

## Convertir des documents PDF en formats d’image {#converting-pdf-documents-to-image-formats}

Vous pouvez utiliser le service Convert PDF pour convertir par programmation des documents PDF en formats d’image, notamment JPEG, JPEG 2000, TIFF et PNG. En convertissant un document PDF en fichier image, vous pouvez utiliser le document PDF comme fichier image. Par exemple, vous pouvez placer l’image dans un système de gestion de contenu d’entreprise à des fins de stockage.

Lors de la conversion d’un document PDF en image, le service Convert PDF crée une image distincte pour chaque page du document. En d’autres termes, si le document comporte 20 pages, le service Convert PDF crée 20 fichiers image. Lors de la conversion d’un document PDF en format d’image, vous pouvez créer des images individuelles pour chaque page dans le document PDF ou un seul fichier image pour l’ensemble du document PDF.

>[!NOTE]
>
>Pour plus d’informations sur le service Convert PDF, voir [Références des services pour AEM Forms](https://help.adobe.com/fr_FR/livecycle/11.0/Services/index.html).

### Résumé des étapes {#summary_of_steps-1}

Pour convertir un document PDF en l’un des types pris en charge, procédez comme suit :

1. Incluez les fichiers de projet.
1. Créez un client du service Convert PDF.
1. Récupérez le document du PDF à convertir.
1. Définissez les options d’exécution.
1. Convertissez le PDF en image.
1. Récupérez les fichiers image d’une collection.

**Inclure les fichiers de projet**

Incluez les fichiers nécessaires dans votre projet de développement. Si vous créez une application cliente à l’aide de Java, incluez les fichiers JAR nécessaires. Si vous utilisez des services web, veillez à inclure les fichiers proxy.

**Créer un client PDF Convert**

Avant d’effectuer par programmation une opération du service Convert PDF, vous devez créer un client de service Convert PDF. Si vous utilisez l’API Java, créez un objet `ConvertPdfServiceClient`. Si vous utilisez l’API Web Service, créez un objet `ConvertPDFServiceService`.

**Récupérer un document PDF à convertir**

Récupérez le document PDF à convertir en image. Vous ne pouvez pas convertir un document PDF interactif en image. Si vous tentez de le faire, une exception est générée. Pour convertir un document PDF interactif en fichier image, vous devez aplatir le document PDF avant de le convertir. (Voir [Aplatir les documents PDF](/help/forms/developing/creating-document-output-streams.md#flattening-pdf-documents).)

**Définir des options d’exécution**

Définissez les options d’exécution, telles que le format de l’image et les valeurs de résolution. Pour plus d’informations sur les valeurs d’exécution, voir la référence de classe `ToImageOptionsSpec` dans [Référence de l’API AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

**Convertir le PDF en image**

Après avoir créé le client de service et défini les options d’exécution, vous pouvez convertir le document du PDF en image. Un objet de collection contenant les images est renvoyé.

**Récupérer les fichiers image d’une collection**

Vous pouvez récupérer des fichiers image à partir d’un objet de collection renvoyé par le service Convert PDF. Chaque élément de la collection est une instance `com.adobe.idp.Document` (ou une instance `BLOB` si vous utilisez des services web) que vous pouvez enregistrer en tant que fichier image, comme un fichier JPG.

Le format du fichier image dépend de l’option d’exécution `ImageConvertFormat`. En d’autres termes, si vous définissez l’option d’exécution `ImageConvertFormat` sur `ImageConvertFormat.JPEG`, vous pouvez enregistrer des fichiers image en tant que fichiers JPG.

**Voir également**

[Inclusion des fichiers de bibliothèque Java d’AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Démarrages rapides de l’API Convert PDF Service](/help/forms/developing/convert-pdf-service-java-api.md#convert-pdf-service-java-api-quick-start-soap)

### Convertir un document PDF en fichiers image à l’aide de l’API Java {#convert-a-pdf-document-to-image-files-using-the-java-api}

Convertissez un document PDF en format d’image à l’aide de l’API Convert PDF Service (Java) :

1. Incluez les fichiers de projet.

   Incluez les fichiers JAR du client, tels qu’adobe-livecycle-client.jar, dans le chemin d’accès aux classes de votre projet Java.

1. Créez un client PDF Convert.

   * Créez un objet `ServiceClientFactory` qui contient des propriétés de connexion.
   * Créez un objet `ConvertPdfServiceClient` en utilisant son constructeur et en transmettant l’objet `ServiceClientFactory`. 

1. Récupérez le document du PDF à convertir.

   * Créez un objet `java.io.FileInputStream` qui représente le document PDF à convertir en utilisant son constructeur et en transmettant une valeur string spécifiant l’emplacement du document du PDF.
   * Créez un objet `com.adobe.idp.Document` en utilisant son constructeur et en transmettant l’objet `java.io.FileInputStream`. 

1. Définissez les options d’exécution.

   * Créez un objet `ToImageOptionsSpec` en utilisant son constructeur.
   * Appelez les méthodes qui appartiennent à cet objet selon les besoins. Par exemple, définissez le type d’image en appelant la méthode `setImageConvertFormat` et en transmettant une valeur d’énumération `ImageConvertFormat` qui spécifie le type de format.

   >[!NOTE]
   >
   >Paramétrer la valeur d’énumération `ImageConvertFormat` est obligatoire.

1. Convertissez le PDF en image.

   Appelez la méthode `toImage2` de l’objet `ConvertPdfServiceClient` et transmettez les valeurs suivantes :

   * Objet `com.adobe.idp.Document` représentant le fichier PDF à convertir.
   * Objet `com.adobe.livecycle.converpdfservice.client.ToImageOptionsSpec` contenant les différentes préférences concernant le format d’image cible.

   La méthode `toImage2` renvoie un objet `java.util.List` contenant des images. Chaque élément de la collection est une instance `com.adobe.idp.Document`.

1. Récupérez les fichiers image d’une collection.

   Effectuez une itération à l’aide de l’objet `java.util.List` pour déterminer si des images sont présentes. Chaque élément est une instance `com.adobe.idp.Document`. Enregistrez l’image en appelant la méthode `copyToFile` de l’objet `com.adobe.idp.Document` et en transmettant un objet `java.io.File`.

**Voir également**

[Démarrage rapide (mode SOAP) : convertir un document PDF en fichiers JPEG à l’aide de l’API Java](/help/forms/developing/convert-pdf-service-java-api.md#quick-start-soap-mode-converting-a-pdf-document-to-jpeg-files-using-the-java-api)

### Convertir un document PDF en fichiers image à l’aide de l’API Web Service {#convert-a-pdf-document-to-image-files-using-the-web-service-api}

Convertissez un document PDF en format d’image à l’aide de l’API Convert PDF Service (Web Service) :

1. Incluez les fichiers de projet.

   Créez un projet Microsoft .NET qui utilise MTOM. Veillez à utiliser la définition WSDL suivante : `http://localhost:8080/soap/services/ConvertPDFService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Remplacez `localhost` avec l’adresse IP du serveur hébergeant AEM Forms.

1. Créez un client PDF convert.

   * Créez un objet `ConvertPdfServiceClient` en utilisant son constructeur par défaut.
   * Créez un objet `ConvertPdfServiceClient.Endpoint.Address` en utilisant le constructeur `System.ServiceModel.EndpointAddress`. Transmettez une valeur string qui spécifie le WSDL au service AEM Forms (par exemple `http://localhost:8080/soap/services/ConvertPDFService?blob=mtom`). Il n’est pas nécessaire d’utiliser l’attribut `lc_version`. Toutefois, spécifiez `?blob=mtom`.
   * Créez un objet `System.ServiceModel.BasicHttpBinding` en obtenant la valeur du champ `ConvertPdfServiceClient.Endpoint.Binding`. Convertissez la valeur de retour en `BasicHttpBinding`.
   * Définissez le champ `MessageEncoding` de l’objet `System.ServiceModel.BasicHttpBinding` sur `WSMessageEncoding.Mtom`. Cette valeur garantit l’utilisation de MTOM.
   * Activez l’authentification HTTP de base en effectuant les tâches suivantes :

      * Attribuez le nom d’utilisateur AEM forms au champ `ConvertPdfServiceClient.ClientCredentials.UserName.UserName`.
      * Attribuez la valeur de mot de passe correspondante au champ `ConvertPdfServiceClient.ClientCredentials.UserName.Password`.
      * Attribuez la valeur constante `HttpClientCredentialType.Basic` au champ `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Affectez la valeur constante `BasicHttpSecurityMode.TransportCredentialOnly` au champ `BasicHttpBindingSecurity.Security.Mode`.

1. Récupérez le document du PDF à convertir.

   * Créez un objet `BLOB` en utilisant son constructeur. Cet objet `BLOB` sert à stocker le formulaire PDF.
   * Créez un objet `System.IO.FileStream` en appelant son constructeur. Transmettez une valeur string qui spécifie l’emplacement du formulaire PDF et le mode d’ouverture du fichier.
   * Créez un tableau d’octets qui stocke le contenu de l’objet `System.IO.FileStream`. Déterminez la taille du tableau d’octets en obtenant la propriété `Length` de l’objet `System.IO.FileStream`.
   * Renseignez le tableau d’octets avec les données de diffusion en appelant la méthode `Read` de l’objet `System.IO.FileStream`. Transmettez le tableau d’octets, la position de départ et la longueur du flux à lire.
   * Renseignez l’objet `BLOB` en affectant à son champ `MTOM` le contenu du tableau d’octets.

1. Définissez les options d’exécution.

   * Créez un objet `ToImageOptionsSpec` en utilisant son constructeur.
   * Appelez les méthodes qui appartiennent à cet objet selon les besoins. Par exemple, définissez le type d’image en appelant la méthode `setImageConvertFormat` et en transmettant une valeur d’énumération `ImageConvertFormat` indiquant le type de format.

   >[!NOTE]
   >
   >La définition de la valeur d’énumération `ImageConvertFormat` est obligatoire.

1. Convertissez le PDF en image.

   Appelez la méthode `toImage2` de l’objet `ConvertPDFServiceService` et transmettez les valeurs suivantes :

   * Un objet `BLOB` représentant le fichier à convertir
   * Un objet `ToImageOptionsSpec` contenant les différentes préférences en matière de format d’image cible

   La méthode `toImage2` renvoie un objet `MyArrayOfBLOB` contenant les fichiers image nouvellement créés.

1. Récupérez les fichiers image d’une collection.

   * Déterminez le nombre d’éléments contenus dans l’objet `MyArrayOfBLOB` en obtenant la valeur de son champ `Count`. Chaque élément est un objet `BLOB` contenant l’image.
   * Effectuez une itération sur l’objet `MyArrayOfBLOB` et enregistrez chaque fichier image.

**Voir également**

[Appeler AEM Forms en utilisant MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Appel d’AEM Forms à l’aide de SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)
