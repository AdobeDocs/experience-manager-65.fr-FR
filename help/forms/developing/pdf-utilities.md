---
title: Utiliser PDF Utilities
description: Le service PDF Utilities vous permet dʼeffectuer les opérations suivantes : convertissez les formats de fichiers PDF et XDP, définissez et récupérez les propriétés de documents PDF et manipulez les métadonnées XMP.
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
role: Developer
exl-id: e4b204ee-7261-42b8-8db8-a92aa9fd0a28
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '2549'
ht-degree: 100%

---

# Utiliser PDF Utilities {#working-with-pdf-utilities}

**Les exemples et les échantillons de ce document sont réservés à l’environnement AEM Forms sur JEE.**

**À propos du service PDF Utilities**

Le service PDF Utilities peut convertir les formats de fichiers PDF et XDP, définir et récupérer les propriétés de documents PDF et manipuler les métadonnées XMP. Par exemple, avant de convertir un document PDF dans un autre format, il est utile d’examiner ses propriétés afin de déterminer l’opération de service à appeler pour la conversion.

Le service PDF Utilities vous permet dʼeffectuer les tâches suivantes :

* Convertir des documents PDF en documents XDP.
* Convertir des documents XDP en documents PDF. (Consultez la section [Convertir des documents XDP en documents PDF](pdf-utilities.md#converting-xdp-documents-into-pdf-documents)).
* Récupérer les propriétés de documents PDF. (Consultez la section [Récupérer les propriétés de documents PDF](pdf-utilities.md#retrieving-pdf-document-properties)).
* Enregistrer un document PDF et lʼoptimiser pour un affichage web rapide. (Consultez la section [Définir les modes d’enregistrement des documents PDF](pdf-utilities.md#setting-pdf-document-save-modes)).

>[!NOTE]
>
>Pour plus d’informations sur le service Forms, Consultez la section [Guide de référence des services AEM Forms](https://help.adobe.com/fr_FR/livecycle/11.0/Services/index.html).

## Convertir des documents PDF en documents XDP {#converting-pdf-documents-into-xdp-documents}

Vous pouvez utiliser les API Java et de service web PDF Utilities pour convertir par programmation des documents PDF en documents XDP.

>[!NOTE]
>
>Pour plus d’informations sur le service PDF Utilities, consultez la section [Guide de référence des services AEM Forms](https://help.adobe.com/fr_FR/livecycle/11.0/Services/index.html).

### Résumé des étapes {#summary-of-steps}

Pour convertir un document PDF en document XDP, procédez comme suit :

1. Incluez les fichiers de projet.
1. Créez un client PDFUtilityService.
1. Appelez l’opération de conversion PDF vers XDP.

**Inclure les fichiers de projet**

Incluez les fichiers nécessaires dans votre projet de développement. Si vous créez une application cliente à l’aide de Java, incluez les fichiers JAR nécessaires. Si vous utilisez des services Web, veillez à inclure les fichiers proxy.

**Créer un client PDFUtilityService**

Avant d’effectuer par programmation une opération PDF Utilities, vous devez créer un client PDFUtilityService. Si vous utilisez l’API Java, créez un objet `PDFUtilityServiceClient`. Si vous utilisez l’API de service web, créez un objet `PDFUtilityServiceService`.

**Appeler l’opération de conversion PDF vers XDP**

Une fois que vous avez créé le client de service, vous pouvez appeler l’opération de conversion PDF vers XDP.

**Voir également**

[Convertir des documents PDF en documents XDP à l’aide de l’API Java](pdf-utilities.md#convert-pdf-documents-into-xdp-documents-using-the-java-api)

[Convertir des documents PDF en documents XDP à l’aide de l’API de service web](pdf-utilities.md#convert-pdf-documents-into-xdp-documents-using-the-web-service-api)

[Inclusion des fichiers de bibliothèque Java d’AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Convertir des documents PDF en documents XDP à l’aide de l’API Java {#convert-pdf-documents-into-xdp-documents-using-the-java-api}

Pour convertir des documents PDF en documents XDP à l’aide de l’API PDF Utilities (Java), procédez comme suit :

1. Inclure les fichiers du projet

   Incluez les fichiers JAR du client, tels que adobe-pdfutility-client.jar, dans le chemin d’accès aux classes de votre projet Java.

1. Créer un client PDFUtilityService

   Créez un objet `PDFUtilityServiceClient` en utilisant son constructeur et en transmettant un objet `ServiceClientFactory` qui contient des propriétés de connexion.

1. Appeler l’opération de conversion PDF vers XDP

   Pour effectuer la conversion, appelez la méthode `convertPDFtoXDP` de l’objet `PDFUtilityServiceClient` et transmettez un objet `com.adobe.idp.Document` qui représente le fichier PDF. La méthode renvoie un objet `com.adobe.idp.Document` qui représente le fichier XDP nouvellement créé.

**Voir également**

[Convertir des documents PDF en documents XDP](pdf-utilities.md#converting-pdf-documents-into-xdp-documents)

[Inclusion des fichiers de bibliothèque Java d’AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Convertir des documents PDF en documents XDP à l’aide de l’API de service web {#convert-pdf-documents-into-xdp-documents-using-the-web-service-api}

Pour convertir des documents PDF en documents XDP à l’aide de l’API PDF Utilities (service web), procédez comme suit :

1. Inclure les fichiers du projet

   * Créez un assemblage client Microsoft .NET qui utilise le fichier WSDL du service PDF Utilities.
   * Référencez l’assemblage client Microsoft .NET.

1. Créer un client PDFUtilityService

   Créez un objet `PDFUtilityServiceService` en utilisant votre constructeur de classe proxy.

1. Appeler l’opération de conversion PDF vers XDP

   Appelez la méthode `convertPDFtoXDP` de l’objet `PDFUtilityServiceService` et transmettez un objet `BLOB` qui représente le fichier PDF. La méthode renvoie un objet `BLOB` qui représente le fichier XDP nouvellement créé.

**Voir également**

[Convertir des documents PDF en documents XDP](pdf-utilities.md#converting-pdf-documents-into-xdp-documents)

[Appeler AEM Forms en utilisant le codage Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

[Créer un assemblage client .NET utilisant le codage Base64](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding)

## Convertir des documents XDP en documents PDF {#converting-xdp-documents-into-pdf-documents}

Vous pouvez utiliser les API Java et de service web PDF Utilities pour convertir par programmation des documents XDP en documents PDF.

>[!NOTE]
>
>Pour plus d’informations sur le service Forms, consultez la section [Guide de référence des services AEM Forms](https://help.adobe.com/fr_FR/livecycle/11.0/Services/index.html).

### Résumé des étapes {#summary_of_steps-1}

Pour convertir un document XDP en document PDF, procédez comme suit :

1. Incluez les fichiers de projet.
1. Créez un client PDFUtilityService.
1. Appelez l’opération de conversion XDP vers PDF.

**Inclure les fichiers de projet**

Incluez les fichiers nécessaires dans votre projet de développement. Si vous créez une application cliente à l’aide de Java, incluez les fichiers JAR nécessaires. Si vous utilisez des services Web, veillez à inclure les fichiers proxy.

**Créer un client PDFUtilityService**

Avant d’effectuer par programmation une opération PDF Utilities, vous devez créer un client PDFUtilityService. Si vous utilisez l’API Java, créez un objet `PDFUtilityServiceClient`. Si vous utilisez l’API de service web, créez un objet `PDFUtilityServiceService`.

**Appeler l’opération de conversion XDP vers PDF**

Une fois que vous avez créé le client de service, vous pouvez appeler l’opération de conversion XDP vers PDF.

**Voir également**

[Convertir des documents XDP en documents PDF à l’aide de l’API Java](pdf-utilities.md#convert-xdp-documents-into-pdf-documents-using-the-java-api)

[Convertir des documents XDP en documents PDF à l’aide de l’API de service web](pdf-utilities.md#converting-xdp-documents-into-pdf-documents-using-the-web-service-api)

[Inclusion des fichiers de bibliothèque Java d’AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Convertir des documents XDP en documents PDF à l’aide de l’API Java {#convert-xdp-documents-into-pdf-documents-using-the-java-api}

Pour convertir des documents XDP en documents PDF à l’aide de l’API PDF Utilities (Java), procédez comme suit :

1. Inclure les fichiers du projet

   Incluez les fichiers JAR clients, tels qu’adobe-livecycle-client.jar, dans le chemin d’accès aux classes du projet Java.

1. Créer un client PDFUtilityService

   Créez un objet `PDFUtilityServiceClient` en utilisant son constructeur et en transmettant un objet `ServiceClientFactory` contenant des propriétés de connexion.

1. Appeler l’opération de conversion XDP vers PDF

   Pour effectuer la conversion, appelez la méthode `convertXDPtoPDF` de l’objet `PDFUtilityServiceClient` et transmettez un objet `com.adobe.idp.Document` qui représente le fichier XDP. La méthode renvoie un objet `com.adobe.idp.Document` qui représente le fichier PDF nouvellement créé.

**Voir également**

[Convertir des documents XDP en documents PDF](pdf-utilities.md#converting-xdp-documents-into-pdf-documents)

[Inclusion des fichiers de bibliothèque Java d’AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Convertir des documents XDP en documents PDF à l’aide de l’API de service web {#converting-xdp-documents-into-pdf-documents-using-the-web-service-api}

Pour convertir des documents XDP en documents PDF à l’aide de l’API PDF Utilities (API de service web), procédez comme suit :

1. Inclure les fichiers du projet

   * Créez un assemblage client Microsoft .NET qui utilise le fichier WSDL du service PDF Utilities.
   * Référencez l’assemblage client Microsoft .NET.

1. Créer un client PDFUtilityService

   Créez un objet `PDFUtilityServiceService` en utilisant votre constructeur de classe proxy.

1. Appeler l’opération de conversion XDP vers PDF

   Pour effectuer la conversion, appelez la méthode `convertXDPtoPDF` de l’objet `PDFUtilityServiceService` et transmettez un objet `BLOB` qui représente le fichier XDP. La méthode renvoie un objet `BLOB` qui représente le fichier PDF nouvellement créé.

**Voir également**

[Convertir des documents XDP en documents PDF](pdf-utilities.md#converting-xdp-documents-into-pdf-documents)

[Appeler AEM Forms en utilisant le codage Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

[Créer un assemblage client .NET utilisant le codage Base64](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding)

## Récupérer les propriétés d’un document PDF {#retrieving-pdf-document-properties}

Vous pouvez utiliser les API Java et de service web PDF Utilities pour récupérer par programmation les propriétés du document PDF, par exemple s’il s’agit d’un formulaire à remplir ou de la version Acrobat minimale requise pour lire le document.

>[!NOTE]
>
>Pour plus d’informations sur le service web PDF Utilities, consultez la section [Guide de référence des services AEM Forms](https://help.adobe.com/fr_FR/livecycle/11.0/Services/index.html).

### Résumé des étapes {#summary_of_steps-2}

Pour récupérer les propriétés du document PDF, procédez comme suit :

1. Incluez les fichiers de projet.
1. Créez un client PDFUtilityService.
1. Appelez l’opération de récupération des propriétés.

**Inclure les fichiers de projet**

Incluez les fichiers nécessaires dans votre projet de développement. Si vous créez une application cliente à l’aide de Java, incluez les fichiers JAR nécessaires. Si vous utilisez des services Web, veillez à inclure les fichiers proxy.

**Créer un client PDFUtilityService**

Avant d’effectuer par programmation une opération PDF Utilities, vous devez créer un client PDFUtilityService. Si vous utilisez l’API Java, créez un objet `PDFUtilityServiceClient`. Si vous utilisez l’API de service web, créez un objet `PDFUtilityServiceService`.

**Appeler l’opération de récupération des propriétés**

Après avoir créé le client de service, vous pouvez appeler l’opération de récupération des propriétés.

**Voir également**

[Récupérer les propriétés d’un document PDF à l’aide de l’API Java](pdf-utilities.md#retrieve-pdf-document-properties-using-the-java-api)

[Récupérer les propriétés d’un document PDF à l’aide de l’API de service web](pdf-utilities.md#retrieve-pdf-document-properties-using-the-web-service-api)

[Inclusion des fichiers de bibliothèque Java d’AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Récupérer les propriétés d’un document PDF à l’aide de l’API Java {#retrieve-pdf-document-properties-using-the-java-api}

Récupérez les propriétés des documents PDF en utilisant l’API PDF Utilities (Java) :

1. Inclure les fichiers du projet

   Incluez les fichiers JAR clients, tels qu’adobe-livecycle-client.jar, dans le chemin d’accès aux classes du projet Java.

1. Créer un client PDFUtilityService

   Créez un objet `PDFUtilityServiceClient` en utilisant son constructeur et en transmettant un objet `ServiceClientFactory` qui contient les propriétés de connexion.

1. Appeler l’opération de récupération des propriétés

   Pour effectuer la conversion, appelez la méthode `getPDFProperties` de l’objet `PDFUtilityServiceClient` et transmettez les éléments suivants :

   * Un objet `com.adobe.idp.Document` qui représente le document PDF.
   * Un objet `PDFPropertiesOptionSpec` qui contient les propriétés à évaluer.

   La méthode renvoie un objet `PDFPropertiesResult` qui contient les résultats de la requête.

**Voir également**

[Récupérer les propriétés d’un document PDF](pdf-utilities.md#retrieving-pdf-document-properties)

[Inclusion des fichiers de bibliothèque Java d’AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Récupérer les propriétés d’un document PDF à l’aide de l’API de service web {#retrieve-pdf-document-properties-using-the-web-service-api}

Récupérez les propriétés des documents PDF à l’aide de l’API du service web PDF Utilities :

1. Inclure les fichiers du projet

   * Créez un assemblage client Microsoft .NET qui utilise le fichier WSDL du service PDF Utilities.
   * Référencez l’assemblage client Microsoft .NET.

1. Créer un client PDFUtilityService

   Créez un objet `PDFUtilityServiceService` en utilisant le constructeur de votre classe proxy.

1. Appeler l’opération de récupération des propriétés

   Pour effectuer la conversion, appelez la méthode `getPDFProperties` de l’objet `PDFUtilityServiceService` et transmettez les éléments suivants :

   * Un objet `BLOB` qui représente le document PDF.
   * Un objet `PDFPropertiesOptionSpec` qui contient les propriétés à évaluer.

   La méthode renvoie un objet `PDFPropertiesResult` qui contient les résultats de la requête.

**Voir également**

[Récupérer les propriétés d’un document PDF](pdf-utilities.md#retrieving-pdf-document-properties)

[Appeler AEM Forms en utilisant le codage Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

[Créer un assemblage client .NET utilisant le codage Base64](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding)

## Définir les modes d’enregistrement des documents PDF {#setting-pdf-document-save-modes}

Vous pouvez utiliser les API Java et du service web du service PDF Utilities pour définir par programmation un mode d’enregistrement pour un document PDF. Lorsque vous utilisez le service PDF Utilities pour définir un mode d’enregistrement, celui-ci ne fait que définir le mode d’enregistrement et n’enregistre pas réellement le document PDF. Le document PDF est enregistré lorsqu’il est transmis à une autre opération de service. Par exemple, vous pouvez utiliser le service PDF Utilities pour définir un mode d’enregistrement spécifique et le transmettre au service chiffrement, où le document PDF est réellement enregistré et chiffré.

>[!NOTE]
>
>Pour plus d’informations sur le service PDF Utilities, consultez [Références des services pour AEM Forms](https://help.adobe.com/fr_FR/livecycle/11.0/Services/index.html).

### Résumé des étapes {#summary_of_steps-3}

Pour définir l’option d’enregistrement des documents PDF, procédez comme suit :

1. Incluez les fichiers de projet.
1. Créez un client PDFUtilityService.
1. Définissez le mode d’enregistrement.
1. Appelez l’opération d’enregistrement.
1. Transmettez le document PDF à une autre opération.

**Inclure les fichiers de projet**

Incluez les fichiers nécessaires dans votre projet de développement. Si vous créez une application cliente à l’aide de Java, incluez les fichiers JAR nécessaires. Si vous utilisez des services Web, veillez à inclure les fichiers proxy.

**Créer un client PDFUtilityService**

Avant d’effectuer par programmation une opération PDF Utilities, vous devez créer un client PDFUtilityService. Si vous utilisez l’API Java, créez un objet `PDFUtilityServiceClient`. Avec l’API de service web, cela se fait à l’aide d’un objet `PDFUtilityServiceService`.

**Définir le mode d’enregistrement**

Vous pouvez choisir l’une des options d’enregistrement suivantes :

* `INCREMENTAL` : pour enregistrer de manière incrémentielle afin de réduire le temps nécessaire à l’enregistrement
* `FAST_WEB_VIEW` : enregistrer pour un affichage rapide sur le Web.
* `FULL` : pour enregistrer en utilisant un enregistrement complet (sans optimisation).

**Appeler l’opération d’enregistrement de style**

Après avoir créé le client de service, vous pouvez appeler l’opération de récupération des propriétés.

**Transmettre le document PDF à une autre opération AEM Forms**

Une fois que le service PDF Utilities a défini le mode d’enregistrement spécifié, transmettez le document PDF à une autre opération AEM Forms. Une fois renvoyé à partir de cette opération, le document PDF est enregistré dans le mode spécifié. Par exemple, si vous utilisez le service PDF Utilities pour définir le mode `FAST_WEB_VIEW`, puis transmettez le document PDF à l’opération `encryptUsingPassword` du service Encryption, le document PDF renvoyé est chiffré avec un mot de passe et est enregistré dans le mode `FAST_WEB_VIEW`.

>[!NOTE]
>
>Le démarrage rapide associé à cette section définit le mode `FAST_WEB_VIEW` puis transmet le document PDF à l’opération `encryptUsingPassword` du service Encryption.

**Voir également**

[Définir des options d’enregistrement de document PDF à l’aide de l’API Java](pdf-utilities.md#set-pdf-document-save-options-using-the-java-api)

[Définir des options d’enregistrement de documents PDF à l’aide de l’API de service web](pdf-utilities.md#set-pdf-document-save-options-using-the-web-service-api)

[Inclusion des fichiers de bibliothèque Java d’AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Chiffrer des documents PDF avec un mot de passe](/help/forms/developing/encrypting-decrypting-pdf-documents.md#encrypting-pdf-documents-with-a-password)

### Définir des options d’enregistrement de document PDF à l’aide de l’API Java {#set-pdf-document-save-options-using-the-java-api}

Pour définir les options d’enregistrement du document PDF à l’aide de l’API PDF Utilities (Java), procédez comme suit :

1. Inclure les fichiers du projet

   Incluez les fichiers JAR clients, tels qu’adobe-livecycle-client.jar, dans le chemin d’accès aux classes du projet Java.

1. Créer un client PDFUtilityService

   Créez un objet `PDFUtilityServiceClient` en utilisant son constructeur et en transmettant un objet `ServiceClientFactory` contenant des propriétés de connexion.

1. Définir le mode d’enregistrement

   * Créez un objet `PDFUtilitySaveMode` en utilisant son constructeur.
   * Définissez le mode d’enregistrement en appelant la méthode `setSaveStyle` de l’objet `PDFUtilitySaveMode` et en transmettant une valeur de chaîne spécifiant le mode d’enregistrement. Par exemple, pour enregistrer en vue dʼun affichage web rapide, transmettez `FAST_WEB_VIEW`.

1. Appeler l’opération d’enregistrement de style

   Appeler la méthode `setSaveMode` de l’objet `PDFUtilityServiceClient` et transmettez les valeurs suivantes :

   * Un objet `com.adobe.idp.Document` qui représente le document PDF.
   * Un objet `PDFUtilitySaveMode` contenant le style d’enregistrement à utiliser.
   * Une valeur booléenne utilisée pour déterminer s’il faut remplacer l’un des paramètres précédents.

   La méthode renvoie un objet `com.adobe.idp.Document` formaté à l’aide du style d’enregistrement spécifié.

1. Transmettre le document PDF à une autre opération AEM Forms

   * Transmettez l’objet `com.adobe.idp.Document` vers une autre opération AEM Forms.

**Voir également**

[Définir les modes d’enregistrement des documents PDF](pdf-utilities.md#setting-pdf-document-save-modes)

[Inclusion des fichiers de bibliothèque Java d’AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Définir des options d’enregistrement de documents PDF à l’aide de l’API de service web {#set-pdf-document-save-options-using-the-web-service-api}

Pour définir les options d’enregistrement du document PDF à l’aide de l’API PDF Utilities (service web), procédez comme suit :

1. Inclure les fichiers du projet

   * Créez un assemblage client Microsoft .NET qui utilise le fichier WSDL du service PDF Utilities.
   * Référencez l’assemblage client Microsoft .NET.

1. Créer un client PDFUtilityService

   Créez un objet `PDFUtilityServiceService` en utilisant votre constructeur de classe proxy.

1. Définir le mode d’enregistrement

   * Créez un objet `PDFUtilitySaveMode` en utilisant son constructeur.
   * Définissez le mode d’enregistrement en attribuant une valeur de chaîne à la méthode `saveStyle` de l’objet `PDFUtilitySaveMode` qui spécifie le mode d’enregistrement. Par exemple, pour enregistrer en vue dʼun affichage web rapide, spécifiez `FAST_WEB_VIEW`.

1. Appeler l’opération d’enregistrement de style

   Appeler la méthode `setSaveMode` de l’objet `PDFUtilityServiceService` et transmettez les valeurs suivantes :

   * Un objet `BLOB` qui représente le document PDF.
   * Un objet `PDFUtilitySaveMode` contenant le style d’enregistrement à utiliser.
   * Une valeur booléenne utilisée pour déterminer s’il faut remplacer l’un des paramètres précédents.

   La méthode renvoie un objet `BLOB` formaté à l’aide du style d’enregistrement spécifié. Vous pouvez ensuite enregistrer cet objet en tant que document PDF.

1. Transmettre le document PDF à une autre opération Forms

   * Transmettez l’objet `BLOB` renvoyé à une autre opération AEM Forms.

**Voir également**

[Définir les modes d’enregistrement des documents PDF](pdf-utilities.md#setting-pdf-document-save-modes)

[Appeler AEM Forms en utilisant le codage Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)

[Créer un assemblage client .NET utilisant le codage Base64](/help/forms/developing/invoking-aem-forms-using-web.md#creating-a-net-client-assembly-that-uses-base64-encoding)

## Nettoyer les documents PDF {#sanitizing-pdf-documents}

Vous pouvez utiliser les API Java PDF Utilities pour convertir par programmation des documents PDF en documents XDP.

>[!NOTE]
>
>Pour plus d’informations sur le service PDF Utilities, consultez la section [Guide de référence des services d’AEM Forms](https://help.adobe.com/fr_FR/livecycle/11.0/Services/index.html).

### Résumé des étapes {#summary_of_steps-4}

Pour nettoyer un document PDF, procédez comme suit :

1. Incluez les fichiers de projet.
1. Créez un client PDFUtilityService.
1. Appelez l’opération de nettoyage.

**Inclure les fichiers de projet**

Incluez les fichiers nécessaires dans votre projet de développement. Pour créer une application cliente à l’aide de Java, vous devez inclure les fichiers JAR nécessaires.

**Créer un client PDFUtilityService**

Avant de pouvoir effectuer une opération d’assainissement par programmation, vous devez créer un client PDFUtilityService. Avec l’API Java, cela se fait en créant un objet `PDFUtilityServiceClient`.

**Appeler l’opération de conversion de PDF vers XDP**

Après avoir créé le client de service, vous pouvez appeler l’opération d’assainissement.

**Voir également**

[Convertir des documents PDF en documents XDP à l’aide de l’API Java](pdf-utilities.md#convert-pdf-documents-into-xdp-documents-using-the-java-api)

[Convertir des documents PDF en documents XDP à l’aide de l’API de service web](pdf-utilities.md#convert-pdf-documents-into-xdp-documents-using-the-web-service-api)

[Inclusion des fichiers de bibliothèque Java d’AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Assainir les documents PDF à l’aide de l’API Java {#sanitize-pdf-documents-using-the-java-api}

Assainissez les documents en utilisant l’API PDF Utilities (Java) :

1. Inclure les fichiers du projet

   Incluez les fichiers JAR du client, tels que adobe-pdfutility-client.jar, dans le chemin d’accès aux classes de votre projet Java.

1. Créer un client PDFUtilityService

   Créez un objet `PDFUtilityServiceClient` en utilisant son constructeur et en transmettant un objet `ServiceClientFactory` qui contient des propriétés de connexion.

1. Appeler l’opération de conversion PDF vers XDP

   Pour effectuer la conversion, appelez la méthode `convertPDFtoXDP` de l’objet `PDFUtilityServiceClient` et transmettez un objet `com.adobe.idp.Document` qui représente le fichier PDF. La méthode renvoie un objet `com.adobe.idp.Document` qui représente le fichier XDP nouvellement créé.

**Voir également**

[Assainissement des documents PDF](/help/forms/developing/pdf-utilities-service-java-api.md#quick-start-soap-mode-sanitizing-pdf-documents)

[Inclusion des fichiers de bibliothèque Java d’AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)
