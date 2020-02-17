---
title: Conversion de PostScript en documents PDF
seo-title: Conversion de PostScript en documents PDF
description: 'null'
seo-description: 'null'
uuid: 2143f406-1fdd-4551-a738-1a8388f8d478
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 06ad343a-f74d-41f5-b3c8-b85bb723ceeb
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Conversion de PostScript en documents PDF {#converting-postscript-to-pdf-documents}

## À propos du service Distiller {#about-the-distiller-service}

Le service Distiller® convertit les fichiers PostScript®, Encapsulated PostScript (EPS) et PRN en fichiers PDF compacts, fiables et plus sécurisés sur un réseau. Ce service est généralement utilisé pour convertir en documents électroniques d’importants volumes de documents papier, tels que des factures et des déclarations. La conversion de documents en PDF permet également aux entreprises d’envoyer à leurs clients un document à la fois dans sa version papier et dans sa version électronique.

>[!NOTE]
>
>For more information about the Distiller service, see [Services Reference for AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

## Conversion de documents PostScript en documents PDF {#converting-postscript-to-pdf-documents-inner}

Cette rubrique explique comment utiliser l’API du service Distiller (Java et service Web) pour convertir par programmation des fichiers PostScript (PS), Encapsulated PostScript (EPS) et PRN en documents PDF.

>[!NOTE]
>
>For more information about the Distiller service, see [Services Reference for AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

>[!NOTE]
>
>Pour convertir des fichiers PostScript en documents PDF, l’un des éléments suivants doit être installé sur le serveur hébergeant AEM Forms : Package redistribuable Acrobat 9 ou Microsoft Visual C++ 2005.

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

Avant de pouvoir exécuter une opération de service Distiller par programmation, vous devez créer un client de service Distiller. Si vous utilisez l’API Java, créez un `DistillerServiceClient` objet. Si vous utilisez l’API du service Web, créez un `DistillerServiceService` objet.

**Récupérer le fichier à convertir**

Vous devez récupérer le fichier à convertir. Par exemple, pour convertir un fichier PS en document PDF, vous devez récupérer le fichier PS.

**Appel de l’opération de création de PDF**

Après avoir créé le client de service, vous pouvez appeler l’opération de création du PDF. Cette opération nécessite des informations sur le document à convertir, y compris le chemin d’accès au document cible.

**Enregistrer le document PDF**

Vous pouvez enregistrer le document PDF au format PDF.

**Voir également**

[Conversion d’un fichier PostScript au format PDF à l’aide de l’API Java](converting-postscript-pdf-documents.md#convert-a-postscript-file-to-pdf-using-the-java-api)

[Conversion d’un fichier PostScript au format PDF à l’aide de l’API du service Web](converting-postscript-pdf-documents.md#converting-a-postscript-file-to-pdf-using-the-web-service-api)

[Inclusion des fichiers de bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Démarrage rapide de l’API Output Service](/help/forms/developing/output-service-java-api-quick.md#output-service-java-api-quick-start-soap)

### Conversion d’un fichier PostScript au format PDF à l’aide de l’API Java {#convert-a-postscript-file-to-pdf-using-the-java-api}

Convertissez un fichier PostScript en document PDF à l’aide de l’API Distiller Service (Java) :

1. Incluez des fichiers de projet.

   Incluez des fichiers JAR client, tels que adobe-distiller-client.jar, dans le chemin de classe de votre projet Java.

1. Créez un client de service Distiller.

   * Créez un objet `ServiceClientFactory` qui contient des propriétés de connexion.
   * Create an `DistillerServiceClient` object by using its constructor and passing the `ServiceClientFactory` object.

1. Récupérez le fichier à convertir.

   * Créez un `java.io.FileInputStream` objet représentant le fichier à convertir à l’aide de son constructeur et transmettez une valeur de chaîne indiquant l’emplacement du fichier.
   * Créez un objet `com.adobe.idp.Document` en utilisant son constructeur et en transmettant l’objet `java.io.FileInputStream`. 

1. Appelez l’opération de création de PDF.

   Appelez la méthode `DistillerServiceClient` `createPDF` de l’objet et transmettez les valeurs suivantes :

   * Objet `com.adobe.idp.Document` représentant le fichier PS, EPS ou PRN à convertir
   * Objet `java.lang.String` contenant le nom du fichier à convertir
   * Objet `java.lang.String` contenant le nom des paramètres Adobe PDF à utiliser
   * Objet `java.lang.String` contenant le nom des paramètres de protection à utiliser
   * Objet facultatif `com.adobe.idp.Document` contenant les paramètres à appliquer lors de la génération du document PDF
   * Objet facultatif `com.adobe.idp.Document` contenant des informations de métadonnées à appliquer au document PDF
   La `createPDF` méthode renvoie un `CreatePDFResult` objet contenant le nouveau document PDF et un fichier journal pouvant être généré. Le fichier journal contient généralement des messages d’erreur ou d’avertissement générés par la demande de conversion.

1. Enregistrez le document PDF.

   Pour obtenir le document PDF nouvellement créé, procédez comme suit :

   * Appelez la méthode `CreatePDFResult` `getCreatedDocument` de l’objet. Renvoie un `com.adobe.idp.Document` objet.
   * Appelez la méthode `com.adobe.idp.Document` `copyToFile` de l’objet pour extraire le document PDF.
   De même, pour obtenir le document journal, effectuez les actions suivantes.

   * Appelez la méthode `CreatePDFResult` `getLogDocument` de l’objet. Renvoie un `com.adobe.idp.Document` objet.
   * Appelez la méthode `com.adobe.idp.Document` `copyToFile` de l’objet pour extraire le document journal.


**Voir également**

[Résumé des étapes](converting-postscript-pdf-documents.md#summary-of-steps)

[Démarrage rapide (mode SOAP) : Conversion d’un fichier PostScript en document PDF à l’aide de l’API Java](/help/forms/developing/distiller-service-java-api-quick.md#quick-start-soap-mode-converting-a-postscript-file-to-a-pdf-document-using-the-java-api)

[Inclusion des fichiers de bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Conversion d’un fichier PostScript au format PDF à l’aide de l’API du service Web {#converting-a-postscript-file-to-pdf-using-the-web-service-api}

Convertissez un fichier PostScript en document PDF à l’aide de l’API Distiller Service (service Web) :

1. Incluez des fichiers de projet.

   Créez un projet Microsoft .NET qui utilise MTOM. Veillez à utiliser la définition WSDL suivante : `http://localhost:8080/soap/services/DistillerService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Remplacez `localhost` par l’adresse IP du serveur hébergeant AEM Forms.

1. Créez un client de service Distiller.

   * Create a `DistillerServiceClient` object by using its default constructor.
   * Create a `DistillerServiceClient.Endpoint.Address` object by using the `System.ServiceModel.EndpointAddress` constructor. Transmettez une valeur de chaîne qui spécifie le WSDL au service AEM Forms (par exemple, `http://localhost:8080/soap/services/DistillerService?blob=mtom`). Vous n’avez pas besoin d’utiliser l’ `lc_version` attribut. Cet attribut est utilisé lorsque vous créez une référence de service. Spécifiez toutefois `?blob=mtom` l’utilisation de MTOM.
   * Créez un `System.ServiceModel.BasicHttpBinding` objet en obtenant la valeur du `DistillerServiceClient.Endpoint.Binding` champ. Convertissez la valeur de retour en `BasicHttpBinding`.
   * Définissez le `System.ServiceModel.BasicHttpBinding` champ de l’ `MessageEncoding` objet sur `WSMessageEncoding.Mtom`. Cette valeur garantit l’utilisation de MTOM.
   * Activez l’authentification HTTP de base en effectuant les tâches suivantes :

      * Attribuez le nom d’utilisateur d’AEM forms au champ `DistillerServiceClient.ClientCredentials.UserName.UserName`.
      * Attribuez la valeur de mot de passe correspondante au champ `DistillerServiceClient.ClientCredentials.UserName.Password`.
      * Attribuez la valeur constante `HttpClientCredentialType.Basic` au champ `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Attribuez la valeur constante `BasicHttpSecurityMode.TransportCredentialOnly` au champ `BasicHttpBindingSecurity.Security.Mode`.

1. Récupérez le fichier à convertir.

   * Créez un objet `BLOB` en utilisant son constructeur. Cet `BLOB` objet est utilisé pour stocker le fichier à convertir en document PDF.
   * Créez un `System.IO.FileStream` objet en appelant son constructeur et en transmettant une valeur de chaîne représentant l’emplacement du fichier et le mode d’ouverture du fichier.
   * Créez un tableau d’octets qui stocke le contenu de l’ `System.IO.FileStream` objet. Vous pouvez déterminer la taille du tableau d’octets en obtenant la `System.IO.FileStream` `Length` propriété de l’objet.
   * Renseignez le tableau d’octets avec les données de flux en appelant la `System.IO.FileStream` `Read` méthode de l’objet et en transmettant le tableau d’octets, la position de départ et la longueur du flux à lire.
   * Renseignez l’ `BLOB` objet en affectant sa `MTOM` propriété au contenu du tableau d’octets.

1. Appelez l’opération de création de PDF.

   Appelez la méthode `DistillerServiceService` `CreatePDF2` de l’objet et transmettez les valeurs requises suivantes :

   * Objet `BLOB` représentant le fichier PS à convertir
   * Chaîne contenant le nom du chemin d’accès du fichier à convertir
   * Objet chaîne contenant les paramètres Adobe PDF à utiliser (par exemple, `Standard`)
   * Objet chaîne contenant les paramètres de sécurité à utiliser (par exemple, `No Securit`y)
   * Objet facultatif `BLOB` contenant les paramètres à appliquer lors de la génération du document PDF
   * Objet facultatif `BLOB` contenant des informations de métadonnées à appliquer au document PDF
   * Paramètre `BLOB` de sortie utilisé pour stocker le document PDF
   * Paramètre `BLOB` de sortie utilisé pour stocker le journal

1. Enregistrez le document PDF.

   * Create a `System.IO.FileStream` object by invoking its constructor. Transmettez une valeur de chaîne représentant l’emplacement du fichier PDF signé et le mode d’ouverture du fichier.
   * Créez un tableau d’octets qui stocke le contenu de l’ `BLOB` objet renvoyé par la `CreatePDF2` méthode (paramètre de sortie). Renseignez le tableau d’octets en obtenant la valeur du membre `BLOB` `MTOM` de données de l’objet.
   * Create a `System.IO.BinaryWriter` object by invoking its constructor and passing the `System.IO.FileStream` object.
   * Ecrivez le contenu du tableau d’octets dans un fichier PDF en appelant la `System.IO.BinaryWriter` `Write` méthode de l’objet et en transmettant le tableau d’octets.

**Voir également**

[Résumé des étapes](converting-postscript-pdf-documents.md#summary-of-steps)

<!-- UNRESOLVED LINKS
[Quick Start (MTOM): Converting a PostScript file to a PDF document using the web service API](unresolvedlink-lc-qs-distiller-di.xml#ws624e3cba99b79e12e69a9941333732bac8-7f01.2)

[Quick Start (SwaRef): Converting a PostScript file to a PDF document using the web service API](unresolvedlink-lc-qs-distiller-di.xml#ws624e3cba99b79e12e69a9941333732bac8-7eff.2)
-->

[Appel d’AEM Forms à l’aide de MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Appel d’AEM Forms à l’aide de SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)
