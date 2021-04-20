---
title: Conversion de PostScript en Documents PDF
seo-title: Conversion de PostScript en Documents PDF
description: Utilisez le service Distiller pour convertir des fichiers PostScript®, Encapsulated PostScript (EPS) et PRN en fichiers PDF compacts, fiables et plus sécurisés sur un réseau. Le service Distiller convertit de gros volumes de documents imprimés en documents électroniques, tels que des factures et des relevés à l’aide de l’API Java et de l’API de service Web.
seo-description: Utilisez le service Distiller pour convertir des fichiers PostScript®, Encapsulated PostScript (EPS) et PRN en fichiers PDF compacts, fiables et plus sécurisés sur un réseau. Le service Distiller convertit de gros volumes de documents imprimés en documents électroniques, tels que des factures et des relevés à l’aide de l’API Java et de l’API de service Web.
uuid: 2143f406-1fdd-4551-a738-1a8388f8d478
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 06ad343a-f74d-41f5-b3c8-b85bb723ceeb
role: Developer
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '1380'
ht-degree: 7%

---


# Conversion de PostScript en Documents PDF {#converting-postscript-to-pdf-documents}

**Les exemples et exemples de ce document ne concernent que l’environnement AEM Forms on JEE.**

## À propos du service Distiller {#about-the-distiller-service}

Le service Distiller® convertit les fichiers PostScript®, Encapsulated PostScript (EPS) et PRN en fichiers PDF compacts, fiables et plus sécurisés sur un réseau. Ce service est généralement utilisé pour convertir en documents électroniques d’importants volumes de documents papier, tels que des factures et des déclarations. La conversion de documents en PDF permet également aux entreprises d’envoyer à leurs clients un document à la fois dans sa version papier et dans sa version électronique.

>[!NOTE]
>
>Pour plus d’informations sur le service Distiller, voir [Guide de référence des services pour AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

## Conversion de PostScript en documents PDF {#converting-postscript-to-pdf-documents-inner}

Cette rubrique décrit comment utiliser l’API Distiller Service (Java et service Web) pour convertir par programmation des fichiers PostScript (PS), Encapsulated PostScript (EPS) et PRN en documents PDF.

>[!NOTE]
>
>Pour plus d’informations sur le service Distiller, voir [Guide de référence des services pour AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

>[!NOTE]
>
>Pour convertir des fichiers PostScript en documents PDF, l’un des éléments suivants doit être installé sur le serveur hébergeant AEM Forms : Module redistribuable Acrobat 9 ou Microsoft Visual C++ 2005.

### Résumé des étapes {#summary-of-steps}

Pour convertir l’un des types pris en charge en document PDF, procédez comme suit :

1. Incluez des fichiers de projet.
1. Créez un client de service Distiller.
1. Récupérez le fichier à convertir.
1. Appelez l’opération de création de PDF.
1. Enregistrez le document PDF.

**Inclure les fichiers de projet**

Incluez les fichiers nécessaires dans votre projet de développement. Si vous créez une application cliente à l’aide de Java, incluez les fichiers JAR nécessaires. Si vous utilisez des services Web, veillez à inclure les fichiers proxy.

**Création d’un client de service Distiller**

Avant de pouvoir exécuter une opération de service Distiller par programmation, vous devez créer un client de service Distiller. Si vous utilisez l’API Java, créez un objet `DistillerServiceClient`. Si vous utilisez l’API du service Web, créez un objet `DistillerServiceService`.

**Récupérer le fichier à convertir**

Vous devez récupérer le fichier à convertir. Par exemple, pour convertir un fichier PS en document PDF, vous devez récupérer le fichier PS.

**Appeler l’opération de création de PDF**

Après avoir créé le client de service, vous pouvez appeler l’opération de création de PDF. Cette opération nécessite des informations sur le document à convertir, y compris le chemin d&#39;accès au document de cible.

**Enregistrer le document PDF**

Vous pouvez enregistrer le document PDF au format PDF.

**Voir également**

[Conversion d’un fichier PostScript au format PDF à l’aide de l’API Java](converting-postscript-pdf-documents.md#convert-a-postscript-file-to-pdf-using-the-java-api)

[Conversion d’un fichier PostScript en fichier PDF à l’aide de l’API du service Web](converting-postscript-pdf-documents.md#converting-a-postscript-file-to-pdf-using-the-web-service-api)

[Inclusion des fichiers de bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Débuts rapides de l’API Output Service](/help/forms/developing/output-service-java-api-quick.md#output-service-java-api-quick-start-soap)

### Conversion d’un fichier PostScript au format PDF à l’aide de l’API Java {#convert-a-postscript-file-to-pdf-using-the-java-api}

Convertissez un fichier PostScript en document PDF à l’aide de l’API Distiller Service (Java) :

1. Incluez des fichiers de projet.

   Incluez des fichiers JAR client, tels que adobe-distiller-client.jar, dans le chemin de classe de votre projet Java.

1. Créez un client de service Distiller.

   * Créez un objet `ServiceClientFactory` qui contient des propriétés de connexion.
   * Créez un objet `DistillerServiceClient` en utilisant son constructeur et en transmettant l&#39;objet `ServiceClientFactory`.

1. Récupérez le fichier à convertir.

   * Créez un objet `java.io.FileInputStream` qui représente le fichier à convertir en utilisant son constructeur et en transmettant une valeur de chaîne qui spécifie l&#39;emplacement du fichier.
   * Créez un objet `com.adobe.idp.Document` en utilisant son constructeur et en transmettant l’objet `java.io.FileInputStream`. 

1. Appelez l’opération de création de PDF.

   Appelez la méthode `createPDF` de l’objet `DistillerServiceClient` et transmettez les valeurs suivantes :

   * Objet `com.adobe.idp.Document` représentant le fichier PS, EPS ou PRN à convertir
   * Objet `java.lang.String` contenant le nom du fichier à convertir
   * Objet `java.lang.String` contenant le nom des paramètres Adobe PDF à utiliser
   * Objet `java.lang.String` contenant le nom des paramètres de sécurité à utiliser
   * Objet `com.adobe.idp.Document` facultatif contenant les paramètres à appliquer lors de la génération du document PDF
   * Objet `com.adobe.idp.Document` facultatif contenant des informations de métadonnées à appliquer au document PDF

   La méthode `createPDF` renvoie un objet `CreatePDFResult` contenant le nouveau document PDF et un fichier journal pouvant être généré. Le fichier journal contient généralement des messages d’erreur ou d’avertissement générés par la demande de conversion.

1. Enregistrez le document PDF.

   Pour obtenir le document PDF nouvellement créé, effectuez les opérations suivantes :

   * Appelez la méthode `CreatePDFResult` de l’objet `getCreatedDocument`. Cette opération renvoie un objet `com.adobe.idp.Document`.
   * Appelez la méthode `com.adobe.idp.Document` de l’objet `copyToFile` pour extraire le document PDF.

   De même, pour obtenir le document du journal, effectuez les actions suivantes.

   * Appelez la méthode `CreatePDFResult` de l’objet `getLogDocument`. Cette opération renvoie un objet `com.adobe.idp.Document`.
   * Appelez la méthode `com.adobe.idp.Document` de l&#39;objet `copyToFile` pour extraire le document de journal.


**Voir également**

[Résumé des étapes](converting-postscript-pdf-documents.md#summary-of-steps)

[Début rapide (mode SOAP) : Conversion d’un fichier PostScript en document PDF à l’aide de l’API Java](/help/forms/developing/distiller-service-java-api-quick.md#quick-start-soap-mode-converting-a-postscript-file-to-a-pdf-document-using-the-java-api)

[Inclusion des fichiers de bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Conversion d’un fichier PostScript en fichier PDF à l’aide de l’API du service Web {#converting-a-postscript-file-to-pdf-using-the-web-service-api}

Convertissez un fichier PostScript en document PDF à l’aide de l’API Distiller Service (service Web) :

1. Incluez des fichiers de projet.

   Créez un projet Microsoft .NET qui utilise MTOM. Assurez-vous d’utiliser la définition WSDL suivante : `http://localhost:8080/soap/services/DistillerService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Remplacez `localhost` par l’adresse IP du serveur hébergeant AEM Forms.

1. Créez un client de service Distiller.

   * Créez un objet `DistillerServiceClient` en utilisant son constructeur par défaut.
   * Créez un objet `DistillerServiceClient.Endpoint.Address` en utilisant le constructeur `System.ServiceModel.EndpointAddress`. Transmettez une valeur de chaîne qui spécifie le WSDL au service AEM Forms (par exemple, `http://localhost:8080/soap/services/DistillerService?blob=mtom`). Vous n&#39;avez pas besoin d&#39;utiliser l&#39;attribut `lc_version`. Cet attribut est utilisé lorsque vous créez une référence de service. Cependant, spécifiez `?blob=mtom` pour utiliser MTOM.
   * Créez un objet `System.ServiceModel.BasicHttpBinding` en obtenant la valeur du champ `DistillerServiceClient.Endpoint.Binding`. Convertissez la valeur de retour en `BasicHttpBinding`.
   * Définissez le champ `MessageEncoding` de l’objet `System.ServiceModel.BasicHttpBinding` sur `WSMessageEncoding.Mtom`. Cette valeur garantit l’utilisation de MTOM.
   * Activez l’authentification HTTP de base en exécutant les tâches suivantes :

      * Attribuez le nom d’utilisateur AEM forms au champ `DistillerServiceClient.ClientCredentials.UserName.UserName`.
      * Attribuez la valeur de mot de passe correspondante au champ `DistillerServiceClient.ClientCredentials.UserName.Password`.
      * Affectez la valeur constante `HttpClientCredentialType.Basic` au champ `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Affectez la valeur constante `BasicHttpSecurityMode.TransportCredentialOnly` au champ `BasicHttpBindingSecurity.Security.Mode`.

1. Récupérez le fichier à convertir.

   * Créez un objet `BLOB` en utilisant son constructeur. Cet objet `BLOB` est utilisé pour stocker le fichier à convertir en document PDF.
   * Créez un objet `System.IO.FileStream` en appelant son constructeur et en transmettant une valeur de chaîne qui représente l&#39;emplacement du fichier et le mode d&#39;ouverture du fichier.
   * Créez un tableau d’octets qui stocke le contenu de l’objet `System.IO.FileStream`. Vous pouvez déterminer la taille du tableau d’octets en obtenant la propriété `System.IO.FileStream` de l’objet `Length`.
   * Renseignez le tableau d’octets avec les données de flux en appelant la méthode `System.IO.FileStream` de l’objet `Read` et en transmettant le tableau d’octets, la position de départ et la longueur du flux à lire.
   * Renseignez l’objet `BLOB` en attribuant sa propriété `MTOM` au contenu du tableau d’octets.

1. Appelez l’opération de création de PDF.

   Appelez la méthode `CreatePDF2` de l’objet `DistillerServiceService` et transmettez les valeurs requises suivantes :

   * Objet `BLOB` représentant le fichier PS à convertir
   * Chaîne contenant le nom du chemin d’accès du fichier à convertir
   * Objet de chaîne contenant les paramètres Adobe PDF à utiliser (par exemple, `Standard`)
   * Objet chaîne contenant les paramètres de sécurité à utiliser (par exemple, `No Securit`y)
   * Objet `BLOB` facultatif contenant les paramètres à appliquer lors de la génération du document PDF
   * Objet `BLOB` facultatif contenant des informations de métadonnées à appliquer au document PDF
   * Paramètre de sortie `BLOB` utilisé pour stocker le document PDF
   * Paramètre de sortie `BLOB` utilisé pour stocker le journal

1. Enregistrez le document PDF.

   * Créez un objet `System.IO.FileStream` en appelant son constructeur. Transmettez une valeur de chaîne qui représente l’emplacement du fichier du document PDF signé et le mode d’ouverture du fichier.
   * Créez un tableau d’octets qui stocke le contenu de l’objet `BLOB` renvoyé par la méthode `CreatePDF2` (paramètre de sortie). Renseignez le tableau d’octets en obtenant la valeur du membre de données `MTOM` de l’objet `BLOB`.
   * Créez un objet `System.IO.BinaryWriter` en appelant son constructeur et en transmettant l&#39;objet `System.IO.FileStream`.
   * Ecrivez le contenu du tableau d’octets dans un fichier PDF en appelant la méthode `System.IO.BinaryWriter` de l’objet `Write` et en transmettant le tableau d’octets.

**Voir également**

[Résumé des étapes](converting-postscript-pdf-documents.md#summary-of-steps)

<!-- UNRESOLVED LINKS
[Quick Start (MTOM): Converting a PostScript file to a PDF document using the web service API](unresolvedlink-lc-qs-distiller-di.xml#ws624e3cba99b79e12e69a9941333732bac8-7f01.2)

[Quick Start (SwaRef): Converting a PostScript file to a PDF document using the web service API](unresolvedlink-lc-qs-distiller-di.xml#ws624e3cba99b79e12e69a9941333732bac8-7eff.2)
-->

[Appel de AEM Forms à l’aide de MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Appel de AEM Forms à l’aide de SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)
