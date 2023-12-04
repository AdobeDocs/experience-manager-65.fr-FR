---
title: Utiliser des formulaires à code-barres
seo-title: Working with barcoded forms
description: Décodez les données d’un formulaire PDF ou d’une image contenant un code à barres à l’aide de l’API Java et de l’API de service web.
seo-description: Decode data from a PDF form or an image that contains a barcode using the Java API and Web Service API.
uuid: e56c3c94-384d-401f-b418-dd34cdc57eda
contentOwner: admin
content-type: reference
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: eb28ac30-265c-4611-8247-1f4bc826f254
role: Developer
exl-id: dd32808e-b773-48a2-90e1-7a277d349493
source-git-commit: 10b370fd8f855f71c6d7d791c272137bb5e04d97
workflow-type: tm+mt
source-wordcount: '1911'
ht-degree: 84%

---

# Utiliser des formulaires à code-barres {#working-with-barcoded-forms}

**Les exemples et les échantillons de ce document sont réservés à l’environnement AEM Forms sur JEE.**

## À propos du service Barcoded Forms {#about-the-barcoded-forms-service}

Le service Barcoded Forms automatise la capture de données à partir de formulaires d’impression et de saisie et intègre les informations capturées dans les systèmes informatiques de base d’une organisation.

Grâce au service Barcoded Forms, vous pouvez ajouter des codes-barres unidimensionnels et bidimensionnels aux formulaires PDF interactifs. Vous pouvez ensuite publier les formulaires à code-barres sur un site web ou les distribuer par e-mail ou CD. Lorsqu’un utilisateur remplit un formulaire à code-barres en utilisant Adobe Reader, Acrobat Professional ou Acrobat Standard, le code-barres est automatiquement mis à jour afin de coder les données de formulaire fournies par lʼutilisateur. L’utilisateur peut envoyer le formulaire par voie électronique ou l’imprimer sur papier et le soumettre par courrier, par fax ou en mains propres. Vous pouvez ensuite extraire les données fournies par l’utilisateur dans le cadre d’un workflow automatisé, en acheminant les données entre les processus d’approbation et les systèmes d’entreprise.

Pour plus d’informations sur le service Barcoded Forms, Consultez la section [Guide de référence des services pour AEM Forms](https://help.adobe.com/fr_FR/livecycle/11.0/Services/index.html).

## Décoder les données Barcoded Forms {#decoding-barcoded-form-data}

Vous pouvez utiliser l’API du service Barcoded Forms pour décoder les données d’un formulaire PDF ou d’une image contenant un code à barres. Le décodage des données de formulaire consiste à extraire les données contenues dans le code à barres. Avant que les données puissent être décodées d’un formulaire PDF (ou d’une image), un utilisateur doit remplir le formulaire avec des données.

>[!NOTE]
>
>Pour plus d’informations sur le service Barcoded Forms, consultez la section [Guide de référence des services pour AEM Forms](https://help.adobe.com/fr_FR/livecycle/11.0/Services/index.html).

### Résumé des étapes {#summary-of-steps}

Pour décoder les données d’un formulaire PDF, procédez comme suit :

1. Incluez les fichiers de projet.
1. Créez un objet API client Barcoded Forms.
1. Obtenez un formulaire PDF contenant des données à code à barres.
1. Décodez les données du formulaire PDF.
1. Convertissez les données en une source de données XML.
1. Traitez les données décodées.

**Inclure les fichiers de projet**

Incluez les fichiers nécessaires dans votre projet de développement. Si vous créez une application cliente à l’aide de Java, incluez les fichiers JAR nécessaires. Si vous utilisez des services web, veillez à inclure les fichiers proxy.

Les fichiers JAR suivants doivent être ajoutés au chemin d’accès aux classes de votre projet :

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-barcodedforms-client.jar
* adobe-utilities.jar (Requis si AEM Forms est déployé sur JBoss)
* jbossall-client.jar (Requis si AEM Forms est déployé sur JBoss)
* xercesImpl.jar (dans &lt;install directory=&quot;&quot;>/Adobe/Adobe_Experience_Manager_forms/sdk/client-libs\thirdparty)

Si AEM Forms est déployé sur un serveur d’applications J2EE pris en charge qui n’est pas JBOSS, vous devez remplacer adobe-utility.jar et jbossall-client.jar par des fichiers JAR spécifiques au serveur d’applications J2EE sur lequel AEM Forms est déployé. Pour plus d’informations sur l’emplacement de tous les fichiers JAR AEM Forms, consultez la section [Inclure des fichiers de bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Créer un objet API client Barcoded Forms**

Avant de pouvoir effectuer par programmation une opération de service Barcoded Forms, vous devez créer un client de service Barcoded Forms. Si vous utilisez l’API Java, créez un objet `BarcodedFormsServiceClient`. Si vous utilisez l’API du service web Barcoded Forms, créez un objet `BarcodedFormsServiceService`.

**Obtenir un formulaire PDF contenant des données à code à barres**

Obtenez un formulaire de PDF contenant un code à barres contenant des données utilisateur.

**Décoder les données du formulaire PDF**

Une fois que vous avez obtenu un formulaire PDF (ou une image) contenant un code à barres, vous pouvez décoder les données. Le service Barcoded Forms prend en charge les types de codes à barres suivants :

* Codes à barres PDF417.
* Codes à barres DataMatrix.
* Codes à barres de type code QR.
* Codes à barres Codabar.
* Codes à barres Code 128.
* Codes à barres Code 39.
* Codes à barres EAN-13.
* Codes à barres EAN-8.

La saisie du jeu de caractères au format hexadécimal dans l’API de décodage implique que le contenu du code à barres est codé sous forme de chaîne hexadécimale. Par exemple, si UTF-8 est spécifié comme codage de caractères dans le formulaire et que Hex est spécifié dans l’opération de décodage, le contenu du code à barres est codé sous la forme d’une chaîne hexadécimale dans l’élément &lt; `xb:content`> dans la sortie décodée. Vous pouvez convertir cette valeur Hex pour obtenir le contenu d’origine en créant une logique d’application dans votre application cliente.

**Convertir les données en source de données XML**

Une fois que vous avez décodé les données de formulaire, vous pouvez les convertir en données XDP ou XFDF. Supposons, par exemple, que vous souhaitiez importer les données dans un autre formulaire. Pour importer les données dans un formulaire XFA, vous devez convertir les données en données XDP. Pour plus d’informations, consultez la section [Importer des données de formulaire](/help/forms/developing/importing-exporting-data.md#importing-form-data).

**Traiter des données décodées**

Vous pouvez traiter les données converties pour répondre aux besoins de votre entreprise. Par exemple, une fois que vous avez décodé et converti les données, vous pouvez les enregistrer dans un fichier, les stocker dans une base de données d’entreprise, remplir un autre formulaire, etc. Cette section explique comment enregistrer les données converties sous la forme d’un fichier XML.

>[!NOTE]
>
>Le service Barcoded Forms ne parvient pas à décoder les données de code à barres lorsque les paramètre de délimiteur de ligne et de délimiteur de champ ont la même valeur.

**Voir également**

[Décoder les données de formulaire à code à barres à l’aide de l’API Java](barcoded-forms.md#decode-barcoded-form-data-using-the-java-api)

[Décoder les données de formulaire à code à barres à l’aide de l’API de service web](barcoded-forms.md#decode-barcoded-form-data-using-the-web-service-api)

[Inclusion des fichiers de bibliothèque Java d’AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Décoder les données de formulaire à code à barres à l’aide de l’API Java {#decode-barcoded-form-data-using-the-java-api}

Pour décoder les données de formulaire à l’aide de l’API Barcoded Forms (Java), procédez comme suit :

1. Inclure les fichiers du projet

   Incluez les fichiers JAR client dans le chemin de classe de votre projet Java.

1. Créer un objet API client Barcoded Forms

   Créez un objet `BarcodedFormsServiceClient` en utilisant son constructeur et en transmettant un objet `ServiceClientFactory` contenant des propriétés de connexion.

1. Obtenir un formulaire PDF contenant des données à code à barres

   * Créez un objet `java.io.FileInputStream` qui représente le formulaire PDF contenant des données à code à barres en utilisant son constructeur et en transmettant une valeur de chaîne qui spécifie l’emplacement du document PDF.
   * Créez un objet `com.adobe.idp.Document` en utilisant son constructeur et en transmettant l’objet `java.io.FileInputStream`. 

1. Décoder les données du formulaire PDF

   Décodez les données du formulaire en appelant la fonction `BarcodedFormsServiceClient` de `decode` et transmission des valeurs suivantes :

   * L’objet `com.adobe.idp.Document` contenant le formulaire PDF.
   * Un objet `java.lang.Boolean` spécifiant s’il faut décoder un code à barres PDF417.
   * Un objet `java.lang.Boolean` spécifiant s’il faut décoder un code à barres DataMatrix.
   * Un objet `java.lang.Boolean` spécifiant s’il faut décoder un code à barres de type code QR.
   * Un objet `java.lang.Boolean` spécifiant s’il faut décoder un code à barres Codabar.
   * Un objet `java.lang.Boolean` spécifiant s’il faut décoder un code à barres 128.
   * Un objet `java.lang.Boolean` spécifiant s’il faut décoder un code à barres 39.
   * Un objet `java.lang.Boolean` spécifiant s’il faut décoder un code à barres EAN-13.
   * Un objet `java.lang.Boolean` spécifiant s’il faut décoder un code à barres EAN-8.
   * Une valeur d’énumération `com.adobe.livecycle.barcodedforms.CharSet` spécifiant la valeur de codage du jeu de caractères utilisé dans le code à barres.

   La méthode `decode` renvoie un objet `org.w3c.dom.Document` contenant des données de formulaire décodées.

1. Convertir les données en source de données XML

   Convertissez les données décodées en données XDP ou XFDF en appelant la fonction `BarcodedFormsServiceClient` de `extractToXML` et transmission des valeurs suivantes :

   * La variable `org.w3c.dom.Document` qui contient des données décodées (veillez à utiliser l’objet `decode` valeur renvoyée par la méthode ).
   * Une valeur d’énumération `com.adobe.livecycle.barcodedforms.Delimiter` spécifiant le délimiteur de ligne. Il est recommandé de spécifier `Delimiter.Carriage_Return`.
   * Une valeur d’énumération `com.adobe.livecycle.barcodedforms.Delimiter` spécifiant le délimiteur de champ. Par exemple, spécifiez `Delimiter.Tab`.
   * Une valeur d’énumération `com.adobe.livecycle.barcodedforms.XMLFormat` spécifiant s’il faut convertir les données du code à barres en données XML XDP ou XFDF. Par exemple, spécifiez `XMLFormat.XDP` pour convertir les données en données XDP.

   >[!NOTE]
   >
   >Ne spécifiez pas les mêmes valeurs pour les paramètres de délimiteur de ligne et de délimiteur de champ.

   La méthode `extractToXML` renvoie un objet `java.util.List` où chaque élément est un objet `org.w3c.dom.Document`. Il existe un élément distinct pour chaque code à barres situé sur le formulaire. En d’autres termes, s’il y a quatre codes à barres sur le formulaire, il y a quatre éléments dans l’objet `java.util.List` renvoyé.

1. Traiter les données décodées

   * Effectuez une itération à l’aide du `java.util.List` pour obtenir chaque objet `org.w3c.dom.Document` qui se trouve dans la liste.
   * Pour chaque élément de la liste, convertissez l’objet `org.w3c.dom.Document` en un objet `com.adobe.idp.Document`. (La logique d’application qui convertit un objet `org.w3c.dom.Document` en un objet `com.adobe.idp.Document` est illustrée dans l’exemple Décoder des données de formulaire à code à barres à l’aide de l’API Java).
   * Enregistrez les données XML en tant que fichier XML en appelant la méthode `com.adobe.idp.Document` de `copyToFile`, et transmission d’un objet File représentant le fichier XML.

**Voir également**

[Démarrage rapide (mode SOAP) : décodage des données de formulaire à code-barres à l’aide de l’API Java](/help/forms/developing/barcoded-forms-service-java-api.md#quick-start-soap-mode-decoding-barcoded-form-data-using-the-java-api)

[Inclusion des fichiers de bibliothèque Java d’AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

### Décoder les données de formulaire à code à barres à l’aide de l’API de service web {#decode-barcoded-form-data-using-the-web-service-api}

Pour décoder les données de formulaire à l’aide de l’API Barcoded Forms (service web), procédez comme suit :

1. Inclure les fichiers du projet

   * Créez un assemblage client Microsoft .NET qui utilise le WSDL du service Barcoded Forms. Pour plus d’informations, consultez la section [Appeler AEM Forms en utilisant le codage base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding).
   * Référencez l’assemblage client Microsoft .NET. Pour plus d’informations, consultez la rubrique « Référencer l’assemblage client .NET » dans la section [Appeler AEM Forms en utilisant le codage Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding).

1. Créer un objet API client Barcoded Forms

   À l’aide de l’assemblage client Microsoft .NET qui utilise le WSDL du service Barcoded Forms, créez un objet `BarcodedFormsServiceService` en appelant son constructeur par défaut.

1. Obtenir un formulaire PDF contenant des données à code à barres

   * Créez un objet `BLOB` en utilisant son constructeur. L’objet `BLOB` sert à stocker un document PDF contenant un code à barres.
   * Créez un objet `System.IO.FileStream` en appelant son constructeur et en transmettant une valeur de chaîne qui représente l’emplacement du document PDF et son mode d’ouverture.
   * Créez un tableau d’octets qui stocke le contenu de l’objet `System.IO.FileStream`. Vous pouvez déterminer la taille du tableau d’octets en obtenant la variable `System.IO.FileStream` de `Length` .
   * Renseignez le tableau d’octets avec les données de diffusion en appelant la variable `System.IO.FileStream` de `Read` et transmettre le tableau byte, la position de départ et la longueur du flux à lire.
   * Renseignez l’objet `BLOB` en attribuant à sa propriété `binaryData` le contenu du tableau d’octets.

1. Décoder les données du formulaire PDF

   Décodez les données du formulaire en appelant la fonction `BarcodedFormsServiceService` de `decode` et transmission des valeurs suivantes :

   * L’objet `BLOB` contenant le formulaire PDF.
   * Un objet `Boolean` spécifiant s’il faut décoder un code à barres PDF417.
   * Un objet `Boolean` spécifiant s’il faut décoder un code à barres DataMatrix.
   * Un objet `Boolean` spécifiant s’il faut décoder un code à barres de type code QR.
   * Un objet `Boolean` spécifiant s’il faut décoder un code à barres Codabar.
   * Un objet `Boolean` spécifiant s’il faut décoder un code à barres 128.
   * Un objet `Bolean` spécifiant s’il faut décoder un code à barres 39.
   * Un objet `Boolean` spécifiant s’il faut décoder un code à barres EAN-13.
   * Un objet `Boolean` spécifiant s’il faut décoder un code à barres EAN-8.
   * Valeur d’énumération `CharSet` spécifiant la valeur de codage du jeu de caractères utilisé dans le code à barres.

   La méthode `decode` renvoie une valeur de chaîne qui contient les données de formulaire décodées.

1. Convertir les données en source de données XML

   Convertissez les données décodées en données XDP ou XFDF en appelant la fonction `BarcodedFormsServiceService` de `extractToXML` et transmission des valeurs suivantes :

   * Une valeur string qui contient des données décodées (veillez à utiliser la variable `decode` valeur renvoyée par la méthode ).
   * Une valeur d’énumération `Delimiter` spécifiant le délimiteur de ligne. Il est recommandé de spécifier `Delimiter.Carriage_Return`.
   * Une valeur d’énumération `Delimiter` spécifiant le délimiteur de champ. Par exemple, spécifiez `Delimiter.Tab`.
   * Une valeur d’énumération `XMLFormat` spécifiant s’il faut convertir les données du code à barres en données XML XDP ou XFDF. Par exemple, spécifiez `XMLFormat.XDP` pour convertir les données en données XDP.

   >[!NOTE]
   >
   >Ne spécifiez pas les mêmes valeurs pour les paramètres de délimiteur de ligne et de délimiteur de champ.

   La méthode `extractToXML` renvoie un tableau `Object` où chaque élément est une instance `BLOB`. Il existe un élément distinct pour chaque code à barres situé sur le formulaire. En d’autres termes, s’il y a quatre codes à barres sur le formulaire, il y a quatre éléments dans le tableau `Object` renvoyé.

1. Traiter les données décodées

   * Créez un objet `System.IO.FileStream` en appelant son constructeur et en transmettant une valeur de chaîne qui représente l’emplacement du fichier du document PDF sécurisé.
   * Créez un tableau d’octets qui stocke le contenu des données de l’objet `BLOB` qui a été renvoyé par la méthode `encryptPDFUsingPassword`. Renseignez le tableau d’octets en obtenant la valeur de la variable `BLOB` de `binaryData` membre de données.
   * Créez un objet `System.IO.BinaryWriter` en utilisant son constructeur et en transmettant l’objet `System.IO.FileStream`.
   * Ecrivez le contenu du tableau d’octets dans un fichier de PDF en appelant la méthode `System.IO.BinaryWriter` de `Write` et transmission du tableau d’octets.

**Voir également**

[Appeler AEM Forms en utilisant le codage Base64](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-base64-encoding)
