---
title: Utilisation des utilitaires PDF
seo-title: Utilisation des utilitaires PDF
description: 'null'
seo-description: 'null'
uuid: a2ea2359-c547-4f1b-b6ca-f276f816e36a
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: d816bf2e-5236-4084-b7c4-c32b72cdff97
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Utilisation des utilitaires PDF {#working-with-pdf-utilities}

**À propos du service PDF Utilities**

Le service PDF Utilities peut convertir les formats de fichiers PDF et XDP, définir et récupérer les propriétés du document PDF et manipuler les métadonnées XMP. Par exemple, avant de convertir un document PDF dans un autre format, il est utile d’examiner ses propriétés afin de déterminer l’opération de service à appeler pour la conversion.

Vous pouvez effectuer les tâches suivantes à l’aide du service PDF Utilities :

* Convertir des documents PDF en documents XDP.
* Convertir des documents XDP en documents PDF. (voir [Conversion de documents XDP en documents](pdf-utilities.md#converting-xdp-documents-into-pdf-documents)PDF).
* Récupérez les propriétés du document PDF. (Voir [Récupération des propriétés](pdf-utilities.md#retrieving-pdf-document-properties)du document PDF.)
* Enregistrez un document PDF et optimisez-le pour un affichage Web rapide. (voir [Définition des modes](pdf-utilities.md#setting-pdf-document-save-modes)d’enregistrement de document PDF).

>[!NOTE]
>
>For more information about the PDF Utilities service, see [Services Reference for AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

## Conversion de documents PDF en documents XDP {#converting-pdf-documents-into-xdp-documents}

Vous pouvez utiliser les API Java et Web Utilities de PDF pour convertir par programmation des documents PDF en documents XDP.

>[!NOTE]
>
>For more information about the PDF Utilities service, see [Services Reference for AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Résumé des étapes {#summary-of-steps}

Pour convertir un document PDF en document XDP, procédez comme suit :

1. Incluez des fichiers de projet.
1. Créez un client PDFUtilityService.
1. Appelez l’opération de conversion PDF vers XDP.

**Inclure les fichiers de projet**

Incluez les fichiers nécessaires dans votre projet de développement. Si vous créez une application cliente à l’aide de Java, incluez les fichiers JAR nécessaires. Si vous utilisez des services Web, veillez à inclure les fichiers proxy.

**Création d’un client PDFUtilityService**

Avant de pouvoir exécuter une opération PDF Utilities par programmation, vous devez créer un client PDFUtilityService. Avec l’API Java, cela se fait en créant un `PDFUtilityServiceClient` objet. Avec l’API du service Web, cela se fait en utilisant un `PDFUtilityServiceService` objet.

**Appel de l’opération de conversion PDF vers XDP**

Après avoir créé le client de service, vous pouvez appeler l’opération de conversion PDF vers XDP.

**Voir également**

[Conversion de documents PDF en documents XDP à l’aide de l’API Java](pdf-utilities.md#convert-pdf-documents-into-xdp-documents-using-the-java-api)

[Conversion de documents PDF en documents XDP à l’aide de l’API de service Web](pdf-utilities.md#convert-pdf-documents-into-xdp-documents-using-the-web-service-api)

[Inclusion des fichiers de bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Conversion de documents PDF en documents XDP à l’aide de l’API Java {#convert-pdf-documents-into-xdp-documents-using-the-java-api}

Convertissez des documents PDF en documents XDP à l’aide de l’API PDF Utilities (Java) :

1. Inclure les fichiers de projet

   Incluez les fichiers JAR client, tels que adobe-pdfutility-client.jar, dans le chemin de classe de votre projet Java.

1. Création d’un client PDFUtilityService

   Créez un `PDFUtilityServiceClient` objet en utilisant son constructeur et en transmettant un `ServiceClientFactory` objet contenant des propriétés de connexion.

1. Appel de l’opération de conversion PDF vers XDP

   Pour effectuer la conversion, appelez la `PDFUtilityServiceClient` méthode de l’objet et transmettez un `convertPDFtoXDP` `com.adobe.idp.Document` objet qui représente le fichier PDF. La méthode renvoie un `com.adobe.idp.Document` objet qui représente le fichier XDP nouvellement créé.

**Voir également**

[Conversion de documents PDF en documents XDP](pdf-utilities.md#converting-pdf-documents-into-xdp-documents)

[Inclusion des fichiers de bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Conversion de documents PDF en documents XDP à l’aide de l’API de service Web {#convert-pdf-documents-into-xdp-documents-using-the-web-service-api}

Convertissez des documents PDF en documents XDP à l’aide de l’API PDF Utilities (service Web) :

1. Inclure les fichiers de projet

   * Créez un assembly client Microsoft .NET qui consomme le fichier WSDL du service PDF Utilities.
   * Référencez l&#39;assembly client Microsoft .NET.

1. Création d’un client PDFUtilityService

   Créez un `PDFUtilityServiceService` objet à l’aide de votre constructeur de classe proxy.

1. Appel de l’opération de conversion PDF vers XDP

   Appelez la `PDFUtilityServiceService` méthode de l’ `convertPDFtoXDP` objet et transmettez un `BLOB` objet représentant le fichier PDF. La méthode renvoie un `BLOB` objet qui représente le fichier XDP nouvellement créé.

**Voir également**

[Conversion de documents PDF en documents XDP](pdf-utilities.md#converting-pdf-documents-into-xdp-documents)

[Appel d’AEM Forms à l’aide du codage Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

[Création d&#39;un assembly client .NET utilisant le codage Base64](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding)

## Conversion de documents XDP en documents PDF {#converting-xdp-documents-into-pdf-documents}

Vous pouvez utiliser les API Java des utilitaires PDF et des services Web pour convertir par programmation des documents XDP en documents PDF.

>[!NOTE]
>
>For more information about the PDF Utilities service, see [Services Reference for AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Résumé des étapes {#summary_of_steps-1}

Pour convertir un document XDP en document PDF, procédez comme suit :

1. Incluez des fichiers de projet.
1. Créez un client PDFUtilityService.
1. Appelez l’opération de conversion XDP vers PDF.

**Inclure les fichiers de projet**

Incluez les fichiers nécessaires dans votre projet de développement. Si vous créez une application cliente à l’aide de Java, incluez les fichiers JAR nécessaires. Si vous utilisez des services Web, veillez à inclure les fichiers proxy.

**Création d’un client PDFUtilityService**

Avant de pouvoir exécuter une opération PDF Utilities par programmation, vous devez créer un client PDFUtilityService. Avec l’API Java, cela se fait en créant un `PDFUtilityServiceClient` objet. Avec l’API du service Web, cela se fait en utilisant un `PDFUtilityServiceService` objet.

**Appeler l’opération de conversion XDP vers PDF**

Après avoir créé le client de service, vous pouvez appeler l’opération de conversion XDP vers PDF.

**Voir également**

[Conversion de documents XDP en documents PDF à l’aide de l’API Java](pdf-utilities.md#convert-xdp-documents-into-pdf-documents-using-the-java-api)

[Conversion de documents XDP en documents PDF à l’aide de l’API de service Web](pdf-utilities.md#converting-xdp-documents-into-pdf-documents-using-the-web-service-api)

[Inclusion des fichiers de bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Conversion de documents XDP en documents PDF à l’aide de l’API Java {#convert-xdp-documents-into-pdf-documents-using-the-java-api}

Convertissez des documents XDP en documents PDF à l’aide de l’API PDF Utilities (Java) :

1. Inclure les fichiers de projet

   Incluez des fichiers JAR client, tels que adobe-pdfutility-client.jar, dans le chemin de classe de votre projet Java.

1. Création d’un client PDFUtilityService

   Créez un `PDFUtilityServiceClient` objet en utilisant son constructeur et en transmettant un `ServiceClientFactory` objet contenant des propriétés de connexion.

1. Appeler l’opération de conversion XDP vers PDF

   Pour effectuer la conversion, appelez la `PDFUtilityServiceClient` méthode de l’objet et transmettez un `convertXDPtoPDF` `com.adobe.idp.Document` objet qui représente le fichier XDP. La méthode renvoie un `com.adobe.idp.Document` objet représentant le fichier PDF nouvellement créé.

**Voir également**

[Conversion de documents XDP en documents PDF](pdf-utilities.md#converting-xdp-documents-into-pdf-documents)

[Inclusion des fichiers de bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Conversion de documents XDP en documents PDF à l’aide de l’API de service Web {#converting-xdp-documents-into-pdf-documents-using-the-web-service-api}

Convertissez des documents XDP en documents PDF à l’aide de l’API PDF Utilities (API de service Web) :

1. Inclure les fichiers de projet

   * Créez un assembly client Microsoft .NET qui consomme le fichier WSDL du service PDF Utilities.
   * Référencez l&#39;assembly client Microsoft .NET.

1. Création d’un client PDFUtilityService

   Créez un `PDFUtilityServiceService` objet à l’aide de votre constructeur de classe proxy.

1. Appeler l’opération de conversion XDP vers PDF

   Pour effectuer la conversion, appelez la `PDFUtilityServiceService` méthode de l’objet et transmettez un `convertXDPtoPDF` `BLOB` objet qui représente le fichier XDP. La méthode renvoie un `BLOB` objet représentant le fichier PDF nouvellement créé.

**Voir également**

[Conversion de documents XDP en documents PDF](pdf-utilities.md#converting-xdp-documents-into-pdf-documents)

[Appel d’AEM Forms à l’aide du codage Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

[Création d&#39;un assembly client .NET utilisant le codage Base64](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding)

## Récupération des propriétés du document PDF {#retrieving-pdf-document-properties}

Vous pouvez utiliser les API Java et Web Utilities de PDF pour récupérer par programmation les propriétés du document PDF, par exemple s’il s’agit d’un formulaire à remplir ou de la version minimale d’Acrobat requise pour lire le document.

>[!NOTE]
>
>For more information about the PDF Utilities service, see [Services Reference for AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63)

### Résumé des étapes {#summary_of_steps-2}

Pour récupérer les propriétés du document PDF, procédez comme suit :

1. Incluez des fichiers de projet.
1. Créez un client PDFUtilityService.
1. Appelez l’opération de récupération des propriétés.

**Inclure les fichiers de projet**

Incluez les fichiers nécessaires dans votre projet de développement. Si vous créez une application cliente à l’aide de Java, incluez les fichiers JAR nécessaires. Si vous utilisez des services Web, veillez à inclure les fichiers proxy.

**Création d’un client PDFUtilityService**

Avant de pouvoir exécuter une opération PDF Utilities par programmation, vous devez créer un client PDFUtilityService. Avec l’API Java, cela se fait en créant un `PDFUtilityServiceClient` objet. Avec l’API du service Web, cela se fait à l’aide d’un `PDFUtilityServiceService` objet.

**Appeler l’opération de récupération des propriétés**

Après avoir créé le client de service, vous pouvez appeler l’opération de récupération des propriétés.

**Voir également**

[Récupération des propriétés du document PDF à l’aide de l’API Java](pdf-utilities.md#retrieve-pdf-document-properties-using-the-java-api)

[Récupération des propriétés du document PDF à l’aide de l’API du service Web](pdf-utilities.md#retrieve-pdf-document-properties-using-the-web-service-api)

[Inclusion des fichiers de bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Récupération des propriétés du document PDF à l’aide de l’API Java {#retrieve-pdf-document-properties-using-the-java-api}

Récupérez les propriétés du document PDF à l’aide de l’API PDF Utilities (Java) :

1. Inclure les fichiers de projet

   Incluez des fichiers JAR client, tels que adobe-pdfutility-client.jar, dans le chemin de classe de votre projet Java.

1. Création d’un client PDFUtilityService

   Créez un `PDFUtilityServiceClient` objet en utilisant son constructeur et en transmettant un `ServiceClientFactory` objet contenant des propriétés de connexion.

1. Appeler l’opération de récupération des propriétés

   Pour effectuer la conversion, appelez la `PDFUtilityServiceClient` `getPDFProperties` méthode de l’objet et transmettez ce qui suit :

   * A `com.adobe.idp.Document` object that represents the PDF document.
   * Objet `PDFPropertiesOptionSpec` contenant les propriétés à évaluer.
   La méthode renvoie un `PDFPropertiesResult` objet contenant les résultats de la requête.

**Voir également**

[Récupération des propriétés du document PDF](pdf-utilities.md#retrieving-pdf-document-properties)

[Inclusion des fichiers de bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Récupération des propriétés du document PDF à l’aide de l’API du service Web {#retrieve-pdf-document-properties-using-the-web-service-api}

Récupérez les propriétés du document PDF à l’aide de l’API du service Web PDF Utilities :

1. Inclure les fichiers de projet

   * Créez un assembly client Microsoft .NET qui consomme le fichier WSDL du service PDF Utilities.
   * Référencez l&#39;assembly client Microsoft .NET.

1. Création d’un client PDFUtilityService

   Créez un `PDFUtilityServiceService` objet à l’aide de votre constructeur de classe proxy.

1. Appeler l’opération de récupération des propriétés

   Pour effectuer la conversion, appelez la `PDFUtilityServiceService` `getPDFProperties` méthode de l’objet et transmettez ce qui suit :

   * A `BLOB` object that represents the PDF document.
   * Objet `PDFPropertiesOptionSpec` contenant les propriétés à évaluer.
   La méthode renvoie un `PDFPropertiesResult` objet contenant les résultats de la requête.

**Voir également**

[Récupération des propriétés du document PDF](pdf-utilities.md#retrieving-pdf-document-properties)

[Appel d’AEM Forms à l’aide du codage Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

[Création d&#39;un assembly client .NET utilisant le codage Base64](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding)

## Définition des modes d’enregistrement des documents PDF {#setting-pdf-document-save-modes}

Vous pouvez utiliser les API Java et Web du service PDF Utilities pour définir par programmation un mode d’enregistrement pour un document PDF. Lors de l’utilisation du service PDF Utilities pour définir un mode d’enregistrement, le service PDF Utilities définit uniquement le mode d’enregistrement et n’enregistre pas le document PDF. Le document PDF est enregistré lorsqu’il est transmis à une autre opération de service. Par exemple, vous pouvez utiliser le service PDF Utilities pour définir un mode d’enregistrement spécifique et le transmettre au service Encryption, où le document PDF est en fait enregistré et chiffré.

>[!NOTE]
>
>For more information about the PDF Utilities service, see [Services Reference for AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Résumé des étapes {#summary_of_steps-3}

Pour définir l’option d’enregistrement des documents PDF, procédez comme suit :

1. Incluez des fichiers de projet.
1. Créez un client PDFUtilityService.
1. Définissez le mode d’enregistrement.
1. Appelez l’opération d’enregistrement.
1. Transmettez le document PDF à une autre opération.

**Inclure les fichiers de projet**

Incluez les fichiers nécessaires dans votre projet de développement. Si vous créez une application cliente à l’aide de Java, incluez les fichiers JAR nécessaires. Si vous utilisez des services Web, veillez à inclure les fichiers proxy.

**Création d’un client PDFUtilityService**

Avant de pouvoir exécuter une opération PDF Utilities par programmation, vous devez créer un client PDFUtilityService. Avec l’API Java, cela se fait en créant un `PDFUtilityServiceClient` objet. Avec l’API du service Web, cela se fait à l’aide d’un `PDFUtilityServiceService` objet.

**Définition du mode Enregistrer**

Vous pouvez choisir l’une des options d’enregistrement suivantes :

* `INCREMENTAL`: Pour économiser progressivement afin de réduire le temps nécessaire pour économiser
* `FAST_WEB_VIEW`: enregistrer pour un affichage Web rapide
* `FULL`: Pour enregistrer avec un enregistrement complet (sans optimisation)

**Appeler l’opération d’enregistrement du style**

Après avoir créé le client de service, vous pouvez appeler l’opération de récupération des propriétés.

**Transmettre le document PDF à une autre opération AEM Forms**

Une fois que le service PDF Utilities a défini le mode d’enregistrement spécifié, transmettez le document PDF à une autre opération AEM Forms. Une fois renvoyé à partir de cette opération, le document PDF est enregistré dans le mode spécifié. Par exemple, si vous utilisez le service PDF Utilities pour définir le `FAST_WEB_VIEW` mode, puis transmettez le document PDF au `encryptUsingPassword` fonctionnement du service Encryption, le document PDF renvoyé est chiffré avec un mot de passe et enregistré en `FAST_WEB_VIEW` mode.

>[!NOTE]
>
>La section Démarrage rapide associée à cette section définit le `FAST_WEB_VIEW` mode, puis transmet le document PDF au `encryptUsingPassword` fonctionnement du service Encryption.

**Voir également**

[Définition des options d’enregistrement des documents PDF à l’aide de l’API Java](pdf-utilities.md#set-pdf-document-save-options-using-the-java-api)

[Définition des options d’enregistrement de documents PDF à l’aide de l’API de service Web](pdf-utilities.md#set-pdf-document-save-options-using-the-web-service-api)

[Inclusion des fichiers de bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Chiffrement de documents PDF avec un mot de passe](/help/forms/developing/encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-a-password)

### Définition des options d’enregistrement des documents PDF à l’aide de l’API Java {#set-pdf-document-save-options-using-the-java-api}

Définissez les options d’enregistrement du document PDF à l’aide de l’API PDF Utilities (Java) :

1. Inclure les fichiers de projet

   Incluez des fichiers JAR client, tels que adobe-pdfutility-client.jar, dans le chemin de classe de votre projet Java.

1. Création d’un client PDFUtilityService

   Créez un `PDFUtilityServiceClient` objet en utilisant son constructeur et en transmettant un `ServiceClientFactory` objet contenant des propriétés de connexion.

1. Définition du mode Enregistrer

   * Créez un objet `PDFUtilitySaveMode` en utilisant son constructeur.
   * Définissez le mode d’enregistrement en appelant la `PDFUtilitySaveMode` `setSaveStyle` méthode de l’objet et en transmettant une valeur de chaîne qui spécifie le mode d’enregistrement. Par exemple, pour l’enregistrement en vue d’un affichage Web rapide, transmettez `FAST_WEB_VIEW`.

1. Appeler l’opération d’enregistrement du style

   Appelez la méthode `PDFUtilityServiceClient` `setSaveMode` de l’objet et transmettez les valeurs suivantes :

   * A `com.adobe.idp.Document` object that represents the PDF document.
   * Objet `PDFUtilitySaveMode` contenant le style d’enregistrement à utiliser.
   * Valeur booléenne utilisée pour déterminer si des paramètres antérieurs doivent être remplacés.
   La méthode renvoie un `com.adobe.idp.Document` objet formaté à l’aide du style d’enregistrement spécifié.

1. Transmettre le document PDF à une autre opération AEM Forms

   * Transmettez l’ `com.adobe.idp.Document` objet renvoyé à une autre opération AEM Forms.

**Voir également**

[Définition des modes d’enregistrement des documents PDF](pdf-utilities.md#setting-pdf-document-save-modes)

[Inclusion des fichiers de bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Définition des options d’enregistrement de documents PDF à l’aide de l’API de service Web {#set-pdf-document-save-options-using-the-web-service-api}

Définissez les options d’enregistrement du document PDF à l’aide de l’API PDF Utilities (service Web) :

1. Inclure les fichiers de projet

   * Créez un assembly client Microsoft .NET qui consomme le fichier WSDL du service PDF Utilities.
   * Référencez l&#39;assembly client Microsoft .NET.

1. Création d’un client PDFUtilityService

   Créez un `PDFUtilityServiceService` objet à l’aide de votre constructeur de classe proxy.

1. Définition du mode Enregistrer

   * Créez un objet `PDFUtilitySaveMode` en utilisant son constructeur.
   * Définissez le mode d’enregistrement en attribuant une valeur de chaîne à la `PDFUtilitySaveMode` `saveStyle` méthode de l’objet qui spécifie le mode d’enregistrement. Par exemple, pour enregistrer un contenu pour un affichage Web rapide, spécifiez `FAST_WEB_VIEW`.

1. Appeler l’opération d’enregistrement du style

   Appelez la méthode `PDFUtilityServiceService` `setSaveMode` de l’objet et transmettez les valeurs suivantes :

   * A `BLOB` object that represents the PDF document.
   * Objet `PDFUtilitySaveMode` contenant le style d’enregistrement à utiliser.
   * Valeur booléenne utilisée pour déterminer si des paramètres antérieurs doivent être remplacés.
   La méthode renvoie un `BLOB` objet formaté à l’aide du style d’enregistrement spécifié. Vous pouvez ensuite enregistrer cet objet au format PDF.

1. Transmettre le document PDF à une autre opération Forms

   * Transmettez l’ `BLOB` objet renvoyé à une autre opération AEM Forms.

**Voir également**

[Définition des modes d’enregistrement des documents PDF](pdf-utilities.md#setting-pdf-document-save-modes)

[Appel d’AEM Forms à l’aide du codage Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

[Création d&#39;un assembly client .NET utilisant le codage Base64](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding)

## Assainissement des documents PDF {#sanitizing-pdf-documents}

Vous pouvez utiliser les API Java PDF Utilities pour convertir par programmation des documents PDF en documents XDP.

>[!NOTE]
>
>For more information about the PDF Utilities service, see [Services Reference for AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Résumé des étapes {#summary_of_steps-4}

Pour assainir un document PDF, procédez comme suit :

1. Incluez des fichiers de projet.
1. Créez un client PDFUtilityService.
1. Appelez l’opération d’assainissement.

**Inclure les fichiers de projet**

Incluez les fichiers nécessaires dans votre projet de développement. Pour créer une application cliente à l’aide de Java, incluez les fichiers JAR nécessaires.

**Création d’un client PDFUtilityService**

Avant de pouvoir effectuer une opération d’assainissement par programmation, vous devez créer un client PDFUtilityService. Avec l’API Java, cela se fait en créant un `PDFUtilityServiceClient` objet.

**Appel de l’opération de conversion PDF vers XDP**

Après avoir créé le client de service, vous pouvez appeler l’opération d’assainissement.

**Voir également**

[Conversion de documents PDF en documents XDP à l’aide de l’API Java](pdf-utilities.md#convert-pdf-documents-into-xdp-documents-using-the-java-api)

[Conversion de documents PDF en documents XDP à l’aide de l’API de service Web](pdf-utilities.md#convert-pdf-documents-into-xdp-documents-using-the-web-service-api)

[Inclusion des fichiers de bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Assainissement des documents PDF à l’aide de l’API Java {#sanitize-pdf-documents-using-the-java-api}

Pour assainir des documents, utilisez l’API PDF Utilities (Java) :

1. Inclure les fichiers de projet

   Incluez les fichiers JAR client, tels que adobe-pdfutility-client.jar, dans le chemin de classe de votre projet Java.

1. Création d’un client PDFUtilityService

   Créez un `PDFUtilityServiceClient` objet en utilisant son constructeur et en transmettant un `ServiceClientFactory` objet contenant des propriétés de connexion.

1. Appel de l’opération de conversion PDF vers XDP

   Pour effectuer la conversion, appelez la `PDFUtilityServiceClient` méthode de l’objet et transmettez un `convertPDFtoXDP` `com.adobe.idp.Document` objet qui représente le fichier PDF. La méthode renvoie un `com.adobe.idp.Document` objet qui représente le fichier XDP nouvellement créé.

**Voir également**

[Assainissement des documents PDF](/help/forms/developing/pdf-utilities-service-java-api.md#quick-start-soap-mode-sanitizing-pdf-documents)

[Inclusion des fichiers de bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)
