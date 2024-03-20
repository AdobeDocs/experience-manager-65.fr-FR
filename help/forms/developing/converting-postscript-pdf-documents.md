---
title: Convertir des fichiers Postscript en documents PDF
description: Le service Distiller vous permet de convertir des fichiers PostScript®, Encapsulated PostScript (EPS) et PRN en fichiers PDF compacts, fiables et plus sécurisés sur un réseau. Grâce au service Distiller, vous pouvez convertir un grand nombre de documents papier en documents électroniques, tels que des factures et des relevés à l’aide de l’API Java et de l’API de service web.
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
role: Developer
exl-id: 744df8b2-0c61-410f-89e9-20b8adddbf45
solution: Experience Manager, Experience Manager Forms
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '1315'
ht-degree: 99%

---

# Convertir des fichiers Postscript en documents PDF {#converting-postscript-to-pdf-documents}

**Les exemples et les échantillons de ce document sont réservés à l’environnement AEM Forms sur JEE.**

## À propos du service Distiller {#about-the-distiller-service}

Le service Distiller® permet de convertir les fichiers PostScript®, Encapsulated PostScript (EPS) et PRN en fichiers PDF compacts, fiables et plus sécurisés sur un réseau. Ce service est généralement utilisé pour convertir en documents électroniques d’importants volumes de documents papier, tels que des factures et des déclarations. La conversion de documents en PDF permet également aux entreprises d’envoyer à leurs clients un document à la fois dans sa version papier et dans sa version électronique.

>[!NOTE]
>
>Pour plus d’informations à propos du service Forms, consultez la section [Guide de référence des services pour AEM Forms](https://help.adobe.com/fr_FR/livecycle/11.0/Services/index.html).

## Convertir des fichiers PostScript en documents PDF {#converting-postscript-to-pdf-documents-inner}

Cette rubrique décrit l’utilisation de l’API du service Distiller (Java et service web) pour convertir par programmation des fichiers PostScript (PS), Encapsulated PostScript (EPS) et PRN en documents PDF.

>[!NOTE]
>
>Pour plus d’informations à propos du service Distiller, consultez la section [Guide de référence des services pour AEM Forms](https://help.adobe.com/fr_FR/livecycle/11.0/Services/index.html).

>[!NOTE]
>
>Pour convertir des fichiers PostScript en documents PDF, Acrobat 9 ou le package redistribuable Microsoft Visual C++ 2005 doit être installé sur le serveur hébergeant AEM Forms.

### Résumé des étapes {#summary-of-steps}

Pour convertir l’un des types pris en charge en document PDF, procédez comme suit :

1. Incluez les fichiers de projet.
1. Créez un client de service Distiller.
1. Récupérez le fichier à convertir.
1. Appelez l’opération de création de PDF.
1. Enregistrez le formulaire PDF.

**Inclure les fichiers de projet**

Incluez les fichiers nécessaires dans votre projet de développement. Si vous créez une application cliente à l’aide de Java, incluez les fichiers JAR nécessaires. Si vous utilisez des services web, veillez à inclure les fichiers proxy.

**Créer un client de service Distiller**

Avant de pouvoir effectuer par programmation une opération de service Distiller, vous devez créer un client de service Distiller. Si vous utilisez l’API Java, créez un objet `DistillerServiceClient`. Si vous utilisez l’API de service web, créez un objet `DistillerServiceService`.

**Récupérer le fichier à convertir**

Récupérez le fichier que vous souhaitez convertir. Par exemple, pour convertir un fichier PS en document PDF, vous devez récupérer le fichier PS.

**Appeler l’opération de création de PDF**

Une fois que vous avez créé le client de service, vous pouvez appeler l’opération de création de PDF. Cette opération nécessite des informations sur le document à convertir, y compris le chemin d’accès au document cible.

**Enregistrer le document PDF**

Vous pouvez enregistrer le document PDF en tant que fichier PDF.

**Voir également**

[Convertir un fichier PostScript en fichier PDF à l’aide de l’API Java](converting-postscript-pdf-documents.md#convert-a-postscript-file-to-pdf-using-the-java-api)

[Convertir un fichier PostScript en fichier PDF à l’aide de l’API de service web](converting-postscript-pdf-documents.md#converting-a-postscript-file-to-pdf-using-the-web-service-api)

[Inclusion des fichiers de bibliothèque Java d’AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Didacticiels de mise en route de l’API Output Service](/help/forms/developing/output-service-java-api-quick.md#output-service-java-api-quick-start-soap)

### Convertir un fichier PostScript en fichier PDF à l’aide de l’API Java {#convert-a-postscript-file-to-pdf-using-the-java-api}

Pour convertir un fichier PostScript en document PDF à l’aide de l’API du service Distiller (Java), procédez comme suit :

1. Incluez les fichiers de projet.

   Incluez les fichiers JAR du client, tels que adobe-distiller-client.jar, dans le chemin d’accès aux classes de votre projet Java.

1. Créez un client de service Distiller.

   * Créez un objet `ServiceClientFactory` qui contient des propriétés de connexion.
   * Créez un objet `DistillerServiceClient` en utilisant son constructeur et en transmettant l’objet `ServiceClientFactory`.

1. Récupérez le fichier à convertir.

   * Créez un objet `java.io.FileInputStream` qui représente le fichier à convertir en utilisant son constructeur et en transmettant une valeur de chaîne qui spécifie l’emplacement du fichier.
   * Créez un objet `com.adobe.idp.Document` en utilisant son constructeur et en transmettant l’objet `java.io.FileInputStream`. 

1. Appelez l’opération de création de PDF.

   Appelez la méthode `createPDF` de l’objet `DistillerServiceClient` et transmettez les valeurs suivantes :

   * Un objet `com.adobe.idp.Document` représentant le fichier PS, EPS ou PRN à convertir.
   * Un objet `java.lang.String` contenant le nom du fichier à convertir.
   * Un objet `java.lang.String` contenant le nom des paramètres Adobe PDF à utiliser.
   * Un objet `java.lang.String` contenant le nom des paramètres de sécurité à utiliser.
   * Un objet `com.adobe.idp.Document` facultatif contenant les paramètres à appliquer lors de la génération du document PDF.
   * Un objet `com.adobe.idp.Document` facultatif contenant des informations de métadonnées à appliquer au document PDF.

   La méthode `createPDF` renvoie un objet `CreatePDFResult` contenant le nouveau document PDF et un fichier journal pouvant être généré. Le fichier journal contient généralement des messages d’erreur ou d’avertissement générés par la requête de conversion.

1. Enregistrez le formulaire PDF.

   Pour obtenir le document PDF nouvellement créé, procédez comme suit :

   * Appelez la méthode `getCreatedDocument` de l’objet `CreatePDFResult`. Cette fonction renvoie un objet `com.adobe.idp.Document`.
   * Appelez la méthode `copyToFile` de l’objet `com.adobe.idp.Document` pour extraire le document PDF.

   De même, pour obtenir le document journal, procédez comme suit.

   * Appelez la méthode `getLogDocument` de l’objet `CreatePDFResult`. Celle-ci renvoie un objet `com.adobe.idp.Document`.
   * Appelez la méthode `copyToFile` de l’objet `com.adobe.idp.Document` pour extraire le document de journal.

**Voir également**

[Résumé des étapes](converting-postscript-pdf-documents.md#summary-of-steps)

[Démarrage rapide (mode SOAP) : convertir un fichier PostScript en document PDF à l’aide de l’API Java](/help/forms/developing/distiller-service-java-api-quick.md#quick-start-soap-mode-converting-a-postscript-file-to-a-pdf-document-using-the-java-api)

[Inclusion des fichiers de bibliothèque Java d’AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Convertir un fichier PostScript en fichier PDF à l’aide de l’API de service web {#converting-a-postscript-file-to-pdf-using-the-web-service-api}

Pour convertir un fichier PostScript en document PDF à l’aide de l’API Distiller Service (service web), procédez comme suit :

1. Incluez les fichiers de projet.

   Créez un projet Microsoft .NET qui utilise MTOM. Veillez à utiliser la définition WSDL suivante : `http://localhost:8080/soap/services/DistillerService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Remplacez `localhost` par l’adresse IP du serveur hébergeant AEM Forms.

1. Créez un client de service Distiller.

   * Créez un objet `DistillerServiceClient` en utilisant son constructeur par défaut.
   * Créez un objet `DistillerServiceClient.Endpoint.Address` en utilisant le constructeur `System.ServiceModel.EndpointAddress`. Transmettez une valeur string qui spécifie le WSDL au service AEM Forms (par exemple `http://localhost:8080/soap/services/DistillerService?blob=mtom`). Il n’est pas nécessaire d’utiliser l’attribut `lc_version`. Cet attribut est utilisé lorsque vous créez une référence de service. Toutefois, spécifiez `?blob=mtom` pour utiliser MTOM.
   * Créez un objet `System.ServiceModel.BasicHttpBinding` en obtenant la valeur du champ `DistillerServiceClient.Endpoint.Binding`. Convertissez la valeur de retour en `BasicHttpBinding`.
   * Définissez le champ `MessageEncoding` de l’objet `System.ServiceModel.BasicHttpBinding` sur `WSMessageEncoding.Mtom`. Cette valeur garantit l’utilisation de MTOM.
   * Activez l’authentification HTTP de base en effectuant les tâches suivantes :

      * Attribuez le nom d’utilisateur AEM forms au champ `DistillerServiceClient.ClientCredentials.UserName.UserName`.
      * Attribuez la valeur de mot de passe correspondante au champ `DistillerServiceClient.ClientCredentials.UserName.Password`.
      * Attribuez la valeur constante `HttpClientCredentialType.Basic` au champ `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Attribuez la valeur constante `BasicHttpSecurityMode.TransportCredentialOnly` au champ `BasicHttpBindingSecurity.Security.Mode`.

1. Récupérez le fichier à convertir.

   * Créez un objet `BLOB` en utilisant son constructeur. Cet objet `BLOB` sert à stocker le fichier à convertir en document PDF.
   * Créez un objet `System.IO.FileStream` en appelant son constructeur et en transmettant une valeur de chaîne qui représente l’emplacement du fichier et son mode d’ouverture.
   * Créez un tableau d’octets qui stocke le contenu de l’objet `System.IO.FileStream`. Vous pouvez déterminer la taille du tableau d’octets en obtenant la propriété `Length` de l’objet `System.IO.FileStream`.
   * Renseignez le tableau d’octets avec les données de diffusion en appelant la méthode `Read` de l’objet `System.IO.FileStream` et en transmettant le tableau d’octets, la position de départ et la longueur du flux à lire.
   * Renseignez l’objet `BLOB` en attribuant sa propriété `MTOM` le contenu du tableau d’octets.

1. Appelez l’opération de création de PDF.

   Appelez la méthode `CreatePDF2` de l’objet `DistillerServiceService` et transmettez les valeurs requises suivantes :

   * Un objet `BLOB` représentant le fichier PS à convertir.
   * Une chaîne contenant le chemin d’accès au fichier à convertir.
   * Un objet de chaîne contenant les paramètres Adobe PDF à utiliser (par exemple, `Standard`).
   * Un objet de chaîne contenant les paramètres de sécurité à utiliser (par exemple, `No Securit`y).
   * Un objet `BLOB` facultatif contenant les paramètres à appliquer lors de la génération du document PDF.
   * Un objet `BLOB` facultatif contenant des informations de métadonnées à appliquer au document PDF.
   * Un paramètre de sortie `BLOB` utilisé pour stocker le document PDF.
   * Un paramètre de sortie `BLOB` utilisé pour stocker le journal.

1. Enregistrez le formulaire PDF.

   * Créez un objet `System.IO.FileStream` en appelant son constructeur. Transmettez une valeur de chaîne représentant l’emplacement du fichier du document PDF signé et son mode d’ouverture.
   * Créez un tableau d’octets qui stocke le contenu de l’objet `BLOB` qui a été renvoyé par la méthode `CreatePDF2` (paramètre de sortie). Renseignez le tableau d’octets en obtenant la valeur du membre de données `MTOM` de l’objet `BLOB`.
   * Créez un objet `System.IO.BinaryWriter` en utilisant son constructeur et en transmettant l’objet `System.IO.FileStream`.
   * Écrivez le contenu du tableau d’octets dans un fichier PDF en appelant la méthode `Write` de l’objet `System.IO.BinaryWriter` et en transmettant le tableau d’octets.

**Voir également**

[Résumé des étapes](converting-postscript-pdf-documents.md#summary-of-steps)

<!-- UNRESOLVED LINKS
[Quick Start (MTOM): Converting a PostScript file to a PDF document using the web service API](unresolvedlink-lc-qs-distiller-di.xml#ws624e3cba99b79e12e69a9941333732bac8-7f01.2)

[Quick Start (SwaRef): Converting a PostScript file to a PDF document using the web service API](unresolvedlink-lc-qs-distiller-di.xml#ws624e3cba99b79e12e69a9941333732bac8-7eff.2)
-->

[Appeler AEM Forms en utilisant MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)

[Appel d’AEM Forms à l’aide de SwaRef](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-swaref)
