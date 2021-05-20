---
title: Utilisation de PDF Utilities
seo-title: Utilisation de PDF Utilities
description: Utilisez le service PDF Utilities pour convertir les formats de fichiers PDF et XDP, définir et récupérer les propriétés du document PDF et manipuler XMP métadonnées.
seo-description: Utilisez le service PDF Utilities pour convertir les formats de fichiers PDF et XDP, définir et récupérer les propriétés du document PDF et manipuler XMP métadonnées.
uuid: a2ea2359-c547-4f1b-b6ca-f276f816e36a
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: d816bf2e-5236-4084-b7c4-c32b72cdff97
role: Developer
exl-id: e4b204ee-7261-42b8-8db8-a92aa9fd0a28
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '2606'
ht-degree: 5%

---

# Utilisation de PDF Utilities {#working-with-pdf-utilities}

**Les exemples et les exemples de ce document sont réservés à l’environnement AEM Forms on JEE.**

**À propos du service PDF Utilities**

Le service PDF Utilities peut convertir les formats de fichiers PDF et XDP, définir et récupérer des propriétés de document PDF et manipuler XMP métadonnées. Par exemple, avant de convertir un document PDF dans un autre format, il est utile d’examiner ses propriétés pour déterminer l’opération de service à appeler pour la conversion.

Vous pouvez accomplir ces tâches à l’aide du service PDF Utilities :

* Convertissez des documents PDF en documents XDP.
* Convertissez des documents XDP en documents PDF. (Voir [Conversion de documents XDP en documents PDF](pdf-utilities.md#converting-xdp-documents-into-pdf-documents).)
* Récupérez les propriétés du document PDF. (Voir [Récupération des propriétés du document PDF](pdf-utilities.md#retrieving-pdf-document-properties).)
* Enregistrez un document PDF et optimisez-le pour un affichage Web rapide. (Voir [Définition des modes d’enregistrement du document PDF](pdf-utilities.md#setting-pdf-document-save-modes).)

>[!NOTE]
>
>Pour plus d’informations sur le service PDF Utilities, voir [Référence des services pour AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

## Conversion de documents PDF en documents XDP {#converting-pdf-documents-into-xdp-documents}

Vous pouvez utiliser les API Java et Web PDF Utilities pour convertir par programmation des documents PDF en documents XDP.

>[!NOTE]
>
>Pour plus d’informations sur le service PDF Utilities, voir [Référence des services pour AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Résumé des étapes {#summary-of-steps}

Pour convertir un document PDF en document XDP, procédez comme suit :

1. Inclure les fichiers de projet.
1. Créez un client PDFUtilityService.
1. Appelez l’opération de conversion PDF vers XDP.

**Inclure les fichiers de projet**

Incluez les fichiers nécessaires dans votre projet de développement. Si vous créez une application cliente à l’aide de Java, incluez les fichiers JAR nécessaires. Si vous utilisez des services Web, veillez à inclure les fichiers proxy.

**Création d’un client PDFUtilityService**

Avant d’effectuer par programmation une opération PDF Utilities, vous devez créer un client PDFUtilityService . Avec l’API Java, cela est possible en créant un objet `PDFUtilityServiceClient`. Avec l’API de service Web, cela est réalisé à l’aide d’un objet `PDFUtilityServiceService`.

**Appeler l’opération de conversion PDF vers XDP**

Après avoir créé le client de service, vous pouvez appeler l’opération de conversion PDF vers XDP.

**Voir également**

[Convertir des documents PDF en documents XDP à l’aide de l’API Java](pdf-utilities.md#convert-pdf-documents-into-xdp-documents-using-the-java-api)

[Convertir des documents PDF en documents XDP à l’aide de l’API de service Web](pdf-utilities.md#convert-pdf-documents-into-xdp-documents-using-the-web-service-api)

[Inclusion des fichiers de bibliothèque Java d’AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Convertir des documents PDF en documents XDP à l’aide de l’API Java {#convert-pdf-documents-into-xdp-documents-using-the-java-api}

Convertissez des documents PDF en documents XDP à l’aide de l’API PDF Utilities (Java) :

1. Inclure les fichiers de projet

   Incluez les fichiers JAR client, tels que adobe-pdfutility-client.jar, dans le chemin d’accès à la classe de votre projet Java.

1. Création d’un client PDFUtilityService

   Créez un objet `PDFUtilityServiceClient` en utilisant son constructeur et en transmettant un objet `ServiceClientFactory` contenant des propriétés de connexion.

1. Appeler l’opération de conversion PDF vers XDP

   Pour effectuer la conversion, appelez la méthode `PDFUtilityServiceClient` de l’objet `convertPDFtoXDP` et transmettez un objet `com.adobe.idp.Document` représentant le fichier PDF. La méthode renvoie un objet `com.adobe.idp.Document` qui représente le fichier XDP nouvellement créé.

**Voir également**

[Conversion de documents PDF en documents XDP](pdf-utilities.md#converting-pdf-documents-into-xdp-documents)

[Inclusion des fichiers de bibliothèque Java d’AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Convertir des documents PDF en documents XDP à l’aide de l’API de service Web {#convert-pdf-documents-into-xdp-documents-using-the-web-service-api}

Convertissez des documents PDF en documents XDP à l’aide de l’API PDF Utilities (service Web) :

1. Inclure les fichiers de projet

   * Créez un assemblage client Microsoft .NET qui utilise le fichier WSDL du service PDF Utilities.
   * Référencez l’assemblage client Microsoft .NET.

1. Création d’un client PDFUtilityService

   Créez un objet `PDFUtilityServiceService` à l’aide de votre constructeur de classe proxy.

1. Appeler l’opération de conversion PDF vers XDP

   Appelez la méthode `convertPDFtoXDP` de l’objet `PDFUtilityServiceService` et transmettez un objet `BLOB` représentant le fichier PDF. La méthode renvoie un objet `BLOB` qui représente le fichier XDP nouvellement créé.

**Voir également**

[Conversion de documents PDF en documents XDP](pdf-utilities.md#converting-pdf-documents-into-xdp-documents)

[Appel d’AEM Forms à l’aide du codage Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

[Création d’un assemblage client .NET utilisant le codage Base64](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding)

## Conversion de documents XDP en documents PDF {#converting-xdp-documents-into-pdf-documents}

Vous pouvez utiliser les API Java et Web PDF Utilities pour convertir par programmation des documents XDP en documents PDF.

>[!NOTE]
>
>Pour plus d’informations sur le service PDF Utilities, voir [Référence des services pour AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Résumé des étapes {#summary_of_steps-1}

Pour convertir un document XDP en document PDF, procédez comme suit :

1. Inclure les fichiers de projet.
1. Créez un client PDFUtilityService.
1. Appeler l’opération de conversion XDP vers PDF.

**Inclure les fichiers de projet**

Incluez les fichiers nécessaires dans votre projet de développement. Si vous créez une application cliente à l’aide de Java, incluez les fichiers JAR nécessaires. Si vous utilisez des services Web, veillez à inclure les fichiers proxy.

**Création d’un client PDFUtilityService**

Avant d’effectuer par programmation une opération PDF Utilities, vous devez créer un client PDFUtilityService . Avec l’API Java, cela est possible en créant un objet `PDFUtilityServiceClient`. Avec l’API de service Web, cela est réalisé à l’aide d’un objet `PDFUtilityServiceService`.

**Appeler l’opération de conversion XDP vers PDF**

Après avoir créé le client de service, vous pouvez appeler l’opération de conversion XDP vers PDF.

**Voir également**

[Convertir des documents XDP en documents PDF à l’aide de l’API Java](pdf-utilities.md#convert-xdp-documents-into-pdf-documents-using-the-java-api)

[Conversion de documents XDP en documents PDF à l’aide de l’API du service Web](pdf-utilities.md#converting-xdp-documents-into-pdf-documents-using-the-web-service-api)

[Inclusion des fichiers de bibliothèque Java d’AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Convertir des documents XDP en documents PDF à l’aide de l’API Java {#convert-xdp-documents-into-pdf-documents-using-the-java-api}

Convertissez des documents XDP en documents PDF à l’aide de l’API PDF Utilities (Java) :

1. Inclure les fichiers de projet

   Incluez les fichiers JAR client, tels que adobe-pdfutility-client.jar, dans le chemin de classe de votre projet Java.

1. Création d’un client PDFUtilityService

   Créez un objet `PDFUtilityServiceClient` en utilisant son constructeur et en transmettant un objet `ServiceClientFactory` contenant des propriétés de connexion.

1. Appeler l’opération de conversion XDP vers PDF

   Pour effectuer la conversion, appelez la méthode `PDFUtilityServiceClient` de l’objet `convertXDPtoPDF` et transmettez un objet `com.adobe.idp.Document` représentant le fichier XDP. La méthode renvoie un objet `com.adobe.idp.Document` qui représente le fichier PDF nouvellement créé.

**Voir également**

[Conversion de documents XDP en documents PDF](pdf-utilities.md#converting-xdp-documents-into-pdf-documents)

[Inclusion des fichiers de bibliothèque Java d’AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Conversion de documents XDP en documents PDF à l’aide de l’API de service Web {#converting-xdp-documents-into-pdf-documents-using-the-web-service-api}

Convertissez des documents XDP en documents PDF à l’aide de l’API PDF Utilities (API de service Web) :

1. Inclure les fichiers de projet

   * Créez un assemblage client Microsoft .NET qui utilise le fichier WSDL du service PDF Utilities.
   * Référencez l’assemblage client Microsoft .NET.

1. Création d’un client PDFUtilityService

   Créez un objet `PDFUtilityServiceService` à l’aide de votre constructeur de classe proxy.

1. Appeler l’opération de conversion XDP vers PDF

   Pour effectuer la conversion, appelez la méthode `PDFUtilityServiceService` de l’objet `convertXDPtoPDF` et transmettez un objet `BLOB` représentant le fichier XDP. La méthode renvoie un objet `BLOB` qui représente le fichier PDF nouvellement créé.

**Voir également**

[Conversion de documents XDP en documents PDF](pdf-utilities.md#converting-xdp-documents-into-pdf-documents)

[Appel d’AEM Forms à l’aide du codage Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

[Création d’un assemblage client .NET utilisant le codage Base64](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding)

## Récupération des propriétés du document PDF {#retrieving-pdf-document-properties}

Vous pouvez utiliser les API Java et Web PDF Utilities pour récupérer par programmation les propriétés du document PDF, par exemple s’il s’agit d’un formulaire à remplir ou de la version Acrobat minimale requise pour lire le document.

>[!NOTE]
>
>Pour plus d’informations sur le service PDF Utilities, voir [Référence des services pour AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63)

### Résumé des étapes {#summary_of_steps-2}

Pour récupérer les propriétés du document PDF, procédez comme suit :

1. Inclure les fichiers de projet.
1. Créez un client PDFUtilityService.
1. Appelez l’opération de récupération des propriétés.

**Inclure les fichiers de projet**

Incluez les fichiers nécessaires dans votre projet de développement. Si vous créez une application cliente à l’aide de Java, incluez les fichiers JAR nécessaires. Si vous utilisez des services Web, veillez à inclure les fichiers proxy.

**Création d’un client PDFUtilityService**

Avant d’effectuer par programmation une opération PDF Utilities, vous devez créer un client PDFUtilityService . Avec l’API Java, cela est possible en créant un objet `PDFUtilityServiceClient`. Avec l’API de service Web, cela est effectué à l’aide d’un objet `PDFUtilityServiceService`.

**Appeler l’opération de récupération des propriétés**

Après avoir créé le client de service, vous pouvez appeler l’opération de récupération des propriétés.

**Voir également**

[Récupération des propriétés du document PDF à l’aide de l’API Java](pdf-utilities.md#retrieve-pdf-document-properties-using-the-java-api)

[Récupération des propriétés de document PDF à l’aide de l’API de service Web](pdf-utilities.md#retrieve-pdf-document-properties-using-the-web-service-api)

[Inclusion des fichiers de bibliothèque Java d’AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Récupérer les propriétés du document PDF à l’aide de l’API Java {#retrieve-pdf-document-properties-using-the-java-api}

Récupérez les propriétés du document PDF à l’aide de l’API PDF Utilities (Java) :

1. Inclure les fichiers de projet

   Incluez les fichiers JAR client, tels que adobe-pdfutility-client.jar, dans le chemin de classe de votre projet Java.

1. Création d’un client PDFUtilityService

   Créez un objet `PDFUtilityServiceClient` en utilisant son constructeur et en transmettant un objet `ServiceClientFactory` contenant des propriétés de connexion.

1. Appeler l’opération de récupération des propriétés

   Pour effectuer la conversion, appelez la méthode `getPDFProperties` de l’objet `PDFUtilityServiceClient` et transmettez les éléments suivants :

   * Objet `com.adobe.idp.Document` représentant le document PDF.
   * Objet `PDFPropertiesOptionSpec` contenant les propriétés à évaluer.

   La méthode renvoie un objet `PDFPropertiesResult` contenant les résultats de la requête.

**Voir également**

[Récupération des propriétés du document PDF](pdf-utilities.md#retrieving-pdf-document-properties)

[Inclusion des fichiers de bibliothèque Java d’AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Récupérer les propriétés du document PDF à l’aide de l’API de service Web {#retrieve-pdf-document-properties-using-the-web-service-api}

Récupérez les propriétés du document PDF à l’aide de l’API du service Web PDF Utilities :

1. Inclure les fichiers de projet

   * Créez un assemblage client Microsoft .NET qui utilise le fichier WSDL du service PDF Utilities.
   * Référencez l’assemblage client Microsoft .NET.

1. Création d’un client PDFUtilityService

   Créez un objet `PDFUtilityServiceService` à l’aide de votre constructeur de classe proxy.

1. Appeler l’opération de récupération des propriétés

   Pour effectuer la conversion, appelez la méthode `getPDFProperties` de l’objet `PDFUtilityServiceService` et transmettez les éléments suivants :

   * Objet `BLOB` représentant le document PDF.
   * Objet `PDFPropertiesOptionSpec` contenant les propriétés à évaluer.

   La méthode renvoie un objet `PDFPropertiesResult` contenant les résultats de la requête.

**Voir également**

[Récupération des propriétés du document PDF](pdf-utilities.md#retrieving-pdf-document-properties)

[Appel d’AEM Forms à l’aide du codage Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

[Création d’un assemblage client .NET utilisant le codage Base64](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding)

## Définition des modes d’enregistrement du document PDF {#setting-pdf-document-save-modes}

Vous pouvez utiliser les API Java et Web du service PDF Utilities pour configurer par programmation un mode d’enregistrement pour un document PDF. Lors de l’utilisation du service PDF Utilities pour définir un mode d’enregistrement, le service PDF Utilities définit uniquement le mode d’enregistrement et n’enregistre pas le document PDF. Le document PDF est enregistré lorsqu’il est transmis à une autre opération de service. Par exemple, vous pouvez utiliser le service PDF Utilities pour définir un mode d’enregistrement spécifique et le transmettre au service Encryption, où le document PDF est réellement enregistré et chiffré.

>[!NOTE]
>
>Pour plus d’informations sur le service PDF Utilities, voir [Référence des services pour AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Résumé des étapes {#summary_of_steps-3}

Pour définir l’option d’enregistrement pour les documents PDF, procédez comme suit :

1. Inclure les fichiers de projet.
1. Créez un client PDFUtilityService.
1. Définissez le mode d’enregistrement.
1. Appelez l’opération d’enregistrement.
1. Transmettez le document PDF à une autre opération.

**Inclure les fichiers de projet**

Incluez les fichiers nécessaires dans votre projet de développement. Si vous créez une application cliente à l’aide de Java, incluez les fichiers JAR nécessaires. Si vous utilisez des services Web, veillez à inclure les fichiers proxy.

**Création d’un client PDFUtilityService**

Avant d’effectuer par programmation une opération PDF Utilities, vous devez créer un client PDFUtilityService . Avec l’API Java, cela est possible en créant un objet `PDFUtilityServiceClient`. Avec l’API de service Web, cela est effectué à l’aide d’un objet `PDFUtilityServiceService`.

**Définition du mode d’enregistrement**

Vous pouvez choisir l’une des options d’enregistrement suivantes :

* `INCREMENTAL`: Pour économiser de manière incrémentielle afin de réduire le temps nécessaire à l’enregistrement
* `FAST_WEB_VIEW`: enregistrer pour un affichage web rapide ;
* `FULL`: Enregistrement complet (sans optimisation)

**Appeler l’opération d’enregistrement de style**

Après avoir créé le client de service, vous pouvez appeler l’opération de récupération des propriétés.

**Transmettre le document PDF à une autre opération AEM Forms**

Une fois que le service PDF Utilities a défini le mode d’enregistrement spécifié, transmettez le document PDF à une autre opération AEM Forms. Une fois renvoyé à partir de cette opération, le document PDF est enregistré dans le mode spécifié. Par exemple, si vous utilisez le service PDF Utilities pour définir le mode `FAST_WEB_VIEW`, puis transmettez le document PDF à l’opération `encryptUsingPassword` du service Encryption, le document PDF renvoyé est chiffré avec un mot de passe et enregistré en mode `FAST_WEB_VIEW`.

>[!NOTE]
>
>Le didacticiel de mise en route associé à cette section définit le mode `FAST_WEB_VIEW`, puis transmet le document PDF à l’opération `encryptUsingPassword` du service Encryption.

**Voir également**

[Définition des options d’enregistrement de documents PDF à l’aide de l’API Java](pdf-utilities.md#set-pdf-document-save-options-using-the-java-api)

[Définition des options d’enregistrement de documents PDF à l’aide de l’API de service Web](pdf-utilities.md#set-pdf-document-save-options-using-the-web-service-api)

[Inclusion des fichiers de bibliothèque Java d’AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Chiffrement de documents PDF avec un mot de passe](/help/forms/developing/encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-a-password)

### Définition des options d’enregistrement de document PDF à l’aide de l’API Java {#set-pdf-document-save-options-using-the-java-api}

Définissez les options d’enregistrement du document PDF à l’aide de l’API PDF Utilities (Java) :

1. Inclure les fichiers de projet

   Incluez les fichiers JAR client, tels que adobe-pdfutility-client.jar, dans le chemin de classe de votre projet Java.

1. Création d’un client PDFUtilityService

   Créez un objet `PDFUtilityServiceClient` en utilisant son constructeur et en transmettant un objet `ServiceClientFactory` contenant des propriétés de connexion.

1. Définition du mode d’enregistrement

   * Créez un objet `PDFUtilitySaveMode` en utilisant son constructeur.
   * Définissez le mode d’enregistrement en appelant la méthode `setSaveStyle` de l’objet `PDFUtilitySaveMode` et en transmettant une valeur string qui spécifie le mode d’enregistrement. Par exemple, pour enregistrer pour un affichage web rapide, transmettez `FAST_WEB_VIEW`.

1. Appeler l’opération d’enregistrement de style

   Appelez la méthode `setSaveMode` de l’objet `PDFUtilityServiceClient` et transmettez les valeurs suivantes :

   * Objet `com.adobe.idp.Document` représentant le document PDF.
   * Objet `PDFUtilitySaveMode` contenant le style d’enregistrement à utiliser.
   * Valeur booléenne utilisée pour déterminer s’il faut remplacer des paramètres précédents.

   La méthode renvoie un objet `com.adobe.idp.Document` formaté à l’aide du style d’enregistrement spécifié.

1. Transmettre le document PDF à une autre opération AEM Forms

   * Transmettez l’objet `com.adobe.idp.Document` renvoyé à une autre opération AEM Forms.

**Voir également**

[Définition des modes d’enregistrement du document PDF](pdf-utilities.md#setting-pdf-document-save-modes)

[Inclusion des fichiers de bibliothèque Java d’AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Définir les options d’enregistrement de documents PDF à l’aide de l’API de service Web {#set-pdf-document-save-options-using-the-web-service-api}

Définissez les options d’enregistrement du document PDF à l’aide de l’API PDF Utilities (service Web) :

1. Inclure les fichiers de projet

   * Créez un assemblage client Microsoft .NET qui utilise le fichier WSDL du service PDF Utilities.
   * Référencez l’assemblage client Microsoft .NET.

1. Création d’un client PDFUtilityService

   Créez un objet `PDFUtilityServiceService` à l’aide de votre constructeur de classe proxy.

1. Définition du mode d’enregistrement

   * Créez un objet `PDFUtilitySaveMode` en utilisant son constructeur.
   * Définissez le mode d’enregistrement en attribuant une valeur string à la méthode `saveStyle` de l’objet `PDFUtilitySaveMode` qui spécifie le mode d’enregistrement. Par exemple, pour enregistrer pour un affichage web rapide, spécifiez `FAST_WEB_VIEW`.

1. Appeler l’opération d’enregistrement de style

   Appelez la méthode `setSaveMode` de l’objet `PDFUtilityServiceService` et transmettez les valeurs suivantes :

   * Objet `BLOB` représentant le document PDF.
   * Objet `PDFUtilitySaveMode` contenant le style d’enregistrement à utiliser.
   * Valeur booléenne utilisée pour déterminer s’il faut remplacer des paramètres précédents.

   La méthode renvoie un objet `BLOB` formaté à l’aide du style d’enregistrement spécifié. Vous pouvez ensuite enregistrer cet objet au format PDF.

1. Transmettre le document PDF à une autre opération Forms

   * Transmettez l’objet `BLOB` renvoyé à une autre opération AEM Forms.

**Voir également**

[Définition des modes d’enregistrement du document PDF](pdf-utilities.md#setting-pdf-document-save-modes)

[Appel d’AEM Forms à l’aide du codage Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

[Création d’un assemblage client .NET utilisant le codage Base64](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding)

## assainir les documents PDF {#sanitizing-pdf-documents}

Vous pouvez utiliser les API Java PDF Utilities pour convertir par programmation des documents PDF en documents XDP.

>[!NOTE]
>
>Pour plus d’informations sur le service PDF Utilities, voir [Référence des services pour AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

### Résumé des étapes {#summary_of_steps-4}

Pour assainir un document PDF, procédez comme suit :

1. Inclure les fichiers de projet.
1. Créez un client PDFUtilityService.
1. Appeler l’opération d’assainissement.

**Inclure les fichiers de projet**

Incluez les fichiers nécessaires dans votre projet de développement. Pour créer une application cliente à l’aide de Java, vous devez inclure les fichiers JAR nécessaires.

**Création d’un client PDFUtilityService**

Avant de pouvoir effectuer une opération d’assainissement par programmation, vous devez créer un client PDFUtilityService . Avec l’API Java, cela est possible en créant un objet `PDFUtilityServiceClient`.

**Appeler l’opération de conversion PDF vers XDP**

Après avoir créé le client de service, vous pouvez appeler l’opération d’assainissement.

**Voir également**

[Convertir des documents PDF en documents XDP à l’aide de l’API Java](pdf-utilities.md#convert-pdf-documents-into-xdp-documents-using-the-java-api)

[Convertir des documents PDF en documents XDP à l’aide de l’API de service Web](pdf-utilities.md#convert-pdf-documents-into-xdp-documents-using-the-web-service-api)

[Inclusion des fichiers de bibliothèque Java d’AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### assainir des documents PDF à l’aide de l’API Java {#sanitize-pdf-documents-using-the-java-api}

assainir des documents à l’aide de l’API PDF Utilities (Java) :

1. Inclure les fichiers de projet

   Incluez les fichiers JAR client, tels que adobe-pdfutility-client.jar, dans le chemin d’accès à la classe de votre projet Java.

1. Création d’un client PDFUtilityService

   Créez un objet `PDFUtilityServiceClient` en utilisant son constructeur et en transmettant un objet `ServiceClientFactory` contenant des propriétés de connexion.

1. Appeler l’opération de conversion PDF vers XDP

   Pour effectuer la conversion, appelez la méthode `PDFUtilityServiceClient` de l’objet `convertPDFtoXDP` et transmettez un objet `com.adobe.idp.Document` représentant le fichier PDF. La méthode renvoie un objet `com.adobe.idp.Document` qui représente le fichier XDP nouvellement créé.

**Voir également**

[Assainissement des documents PDF](/help/forms/developing/pdf-utilities-service-java-api.md#quick-start-soap-mode-sanitizing-pdf-documents)

[Inclusion des fichiers de bibliothèque Java d’AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)
