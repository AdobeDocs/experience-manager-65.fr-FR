---
title: Transmission de documents à FormsService
seo-title: Transmission de documents à FormsService
description: 'Transmettez au service Forms un objet com.adobe.idp.Document contenant la conception de formulaire. Le service Forms effectue le rendu de la conception de formulaire située dans l’objet com.adobe.idp.Document . '
seo-description: Transmettez au service Forms un objet com.adobe.idp.Document contenant la conception de formulaire. Le service Forms effectue le rendu de la conception de formulaire située dans l’objet com.adobe.idp.Document .
uuid: 841e97f3-ebb8-4340-81a9-b6db11f0ec82
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: e23de3c3-f8a0-459f-801e-a0942fb1c6aa
role: Developer
exl-id: 29c7ebda-407a-464b-a9db-054163f5b737
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1714'
ht-degree: 2%

---

# Transmission de documents au service Forms {#passing-documents-to-the-formsservice}

**Les exemples et les exemples de ce document sont réservés à l’environnement AEM Forms on JEE.**

Le service AEM Forms effectue le rendu de PDF forms interactifs sur les appareils clients, généralement les navigateurs Web, afin de collecter des informations auprès des utilisateurs. Un formulaire PDF interactif est basé sur une conception de formulaire généralement enregistrée en tant que fichier XDP et créée dans Designer. Depuis AEM Forms, vous pouvez transmettre au service Forms un objet `com.adobe.idp.Document` contenant la conception de formulaire. Le service Forms effectue ensuite le rendu de la conception de formulaire située dans l’objet `com.adobe.idp.Document`.

L’un des avantages de la transmission d’un objet `com.adobe.idp.Document` au service Forms réside dans le fait que d’autres opérations de service renvoient une instance `com.adobe.idp.Document`. En d’autres termes, vous pouvez obtenir une instance `com.adobe.idp.Document` à partir d’une autre opération de service et en effectuer le rendu. Supposons, par exemple, qu’un fichier XDP soit stocké dans un noeud Content Services (obsolète) nommé `/Company Home/Form Designs`, comme illustré ci-dessous.

Vous pouvez récupérer Loan.xdp par programmation à partir de Content Services (obsolète) (obsolète) et transmettre le fichier XDP au service Forms dans un objet `com.adobe.idp.Document` .

>[!NOTE]
>
>Pour plus d’informations sur le service Forms, voir [Référence des services pour AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

## Résumé des étapes {#summary-of-steps}

Pour transmettre un document obtenu à partir de Content Services (obsolète) au service Forms, effectuez les tâches suivantes :

1. Inclure les fichiers de projet.
1. Créez un objet Forms et un objet API Client de Document Management.
1. Récupérez la conception de formulaire auprès de Content Services (obsolète).
1. Générer le formulaire PDF interactif.
1. Exécutez une action avec le flux de données de formulaire.

**Inclure les fichiers de projet**

Incluez les fichiers nécessaires dans votre projet de développement. Si vous créez une application cliente à l’aide de Java, incluez les fichiers JAR nécessaires. Si vous utilisez des services Web, incluez les fichiers proxy.

**Création d’un objet API Forms et client Document Management**

Avant d’effectuer par programmation une opération d’API de service Forms, créez un objet API client Forms. En outre, comme ce workflow récupère un fichier XDP de Content Services (obsolète), créez un objet API Document Management.

**Récupération de la conception de formulaire auprès de Content Services (obsolète)**

Récupérez le fichier XDP à partir de Content Services (obsolète) à l’aide de l’API Java ou de service Web. Le fichier XDP est renvoyé dans une instance `com.adobe.idp.Document` (ou une instance `BLOB` si vous utilisez des services Web). Vous pouvez ensuite transmettre l’instance `com.adobe.idp.Document` au service Forms.

**Rendu d’un formulaire PDF interactif**

Pour effectuer le rendu d’un formulaire interactif, transmettez l’instance `com.adobe.idp.Document` qui a été renvoyée de Content Services (obsolète) au service Forms.

>[!NOTE]
>
>Vous pouvez transmettre au service Forms une balise `com.adobe.idp.Document` contenant la conception de formulaire. Deux nouvelles méthodes nommées `renderPDFForm2` et `renderHTMLForm2` acceptent un objet `com.adobe.idp.Document` contenant une conception de formulaire.

**Exécution d’une action avec le flux de données de formulaire**

Selon le type d’application cliente, vous pouvez écrire le formulaire dans un navigateur Web client ou l’enregistrer en tant que fichier PDF. En règle générale, une application web écrit le formulaire dans un navigateur web. Cependant, une application de bureau enregistre généralement le formulaire au format PDF.

**Voir également**

[Inclusion des fichiers de bibliothèque Java d’AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Démarrages rapides de l’API Forms Service](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

## Transmettre des documents au service Forms à l’aide de l’API Java {#pass-documents-to-the-forms-service-using-the-java-api}

Transmettez un document obtenu à partir de Content Services (obsolète) à l’aide du service Forms et de l’API Content Services (obsolète) (Java) :

1. Inclure les fichiers de projet

   Incluez les fichiers JAR client, tels que adobe-forms-client.jar et adobe-contentservices-client.jar, dans le chemin de classe de votre projet Java.

1. Création d’un objet API Forms et client Document Management

   * Créez un objet `ServiceClientFactory` qui contient des propriétés de connexion. (Voir [Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties).)
   * Créez un objet `FormsServiceClient` en utilisant son constructeur et en transmettant l’objet `ServiceClientFactory`.
   * Créez un objet `DocumentManagementServiceClientImpl` en utilisant son constructeur et en transmettant l’objet `ServiceClientFactory`. 

1. Récupération de la conception de formulaire auprès de Content Services (obsolète)

   Appelez la méthode `retrieveContent` de l’objet `DocumentManagementServiceClientImpl` et transmettez les valeurs suivantes :

   * Une valeur string qui spécifie le magasin où le contenu est ajouté. Le magasin par défaut est `SpacesStore`. Cette valeur est un paramètre obligatoire.
   * Une valeur string qui spécifie le chemin d’accès complet du contenu à récupérer (par exemple, `/Company Home/Form Designs/Loan.xdp`). Cette valeur est un paramètre obligatoire.
   * Une valeur string qui spécifie la version. Cette valeur est un paramètre facultatif et vous pouvez transmettre une chaîne vide. Dans ce cas, la dernière version est récupérée.

   La méthode `retrieveContent` renvoie un objet `CRCResult` contenant le fichier XDP. Obtenez une instance `com.adobe.idp.Document` en appelant la méthode `getDocument` de l’objet `CRCResult`.

1. Rendu d’un formulaire PDF interactif

   Appelez la méthode `renderPDFForm2` de l’objet `FormsServiceClient` et transmettez les valeurs suivantes :

   * Objet `com.adobe.idp.Document` contenant la conception de formulaire récupérée dans Content Services (obsolète).
   * Objet `com.adobe.idp.Document` contenant les données à fusionner avec le formulaire. Si vous ne souhaitez pas fusionner de données, transmettez un objet `com.adobe.idp.Document` vide.
   * Objet `PDFFormRenderSpec` qui stocke les options d’exécution. Cette valeur est un paramètre facultatif. Vous pouvez spécifier `null` si vous ne souhaitez pas spécifier d’options d’exécution.
   * Objet `URLSpec` contenant des valeurs URI. Cette valeur est un paramètre facultatif et vous pouvez spécifier `null`.
   * Objet `java.util.HashMap` qui stocke les pièces jointes. Cette valeur est un paramètre facultatif. Vous pouvez spécifier `null` si vous ne souhaitez pas joindre de fichiers au formulaire.

   La méthode `renderPDFForm` renvoie un objet `FormsResult` contenant un flux de données de formulaire qui doit être écrit dans le navigateur Web client.

1. Exécution d’une action avec le flux de données de formulaire

   * Créez un objet `com.adobe.idp.Document` en appelant la méthode `FormsResult` de l’objet `getOutputContent`.
   * Obtenez le type de contenu de l’objet `com.adobe.idp.Document` en appelant sa méthode `getContentType`.
   * Définissez le type de contenu de l’objet `javax.servlet.http.HttpServletResponse` en appelant sa méthode `setContentType` et en transmettant le type de contenu de l’objet `com.adobe.idp.Document`.
   * Créez un objet `javax.servlet.ServletOutputStream` utilisé pour écrire le flux de données de formulaire dans le navigateur Web client en appelant la méthode `getOutputStream` de l’objet `javax.servlet.http.HttpServletResponse`.
   * Créez un objet `java.io.InputStream` en appelant la méthode `getInputStream` de l’objet `com.adobe.idp.Document`.
   * Créez un tableau d’octets et renseignez-le avec le flux de données de formulaire en appelant la méthode `read` de l’objet `InputStream`. Transmettez le tableau d’octets en tant qu’argument.
   * Appelez la méthode `write` de l’objet `javax.servlet.ServletOutputStream` pour envoyer le flux de données de formulaire au navigateur Web client. Transmettez le tableau d’octets à la méthode `write` .

**Voir également**

[Démarrage rapide (mode SOAP) : Transmission de documents au service Forms à l’aide de l’API Java](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-passing-documents-to-the-forms-service-using-the-java-api)

[Inclusion des fichiers de bibliothèque Java d’AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Transmettre des documents au service Forms à l’aide de l’API de service Web {#pass-documents-to-the-forms-service-using-the-web-service-api}

Transmettez un document obtenu à partir de Content Services (obsolète) à l’aide du service Forms et de l’API Content Services (obsolète) (service Web) :

1. Inclure les fichiers de projet

   Créez un projet Microsoft .NET qui utilise MTOM. Comme cette application cliente appelle deux services AEM Forms, créez deux références de service. Utilisez la définition WSDL suivante pour la référence de service associée au service Forms : `http://localhost:8080/soap/services/FormsService?WSDL&lc_version=9.0.1`.

   Utilisez la définition WSDL suivante pour la référence de service associée au service Document Management : `http://localhost:8080/soap/services/DocumentManagementService?WSDL&lc_version=9.0.1`.

   Comme le type de données `BLOB` est commun aux deux références de service, qualifiez complètement le type de données `BLOB` lors de son utilisation. Dans le démarrage rapide du service Web correspondant, toutes les instances `BLOB` sont entièrement qualifiées.

   >[!NOTE]
   >
   >Remplacez `localhost`par l’adresse IP du serveur hébergeant AEM Forms.

1. Création d’un objet API Forms et client Document Management

   * Créez un objet `FormsServiceClient` à l’aide de son constructeur par défaut.
   * Créez un objet `FormsServiceClient.Endpoint.Address` à l’aide du constructeur `System.ServiceModel.EndpointAddress`. Transmettez une valeur string qui spécifie le WSDL au service AEM Forms (par exemple, `http://localhost:8080/soap/services/FormsService?WSDL`). Vous n’avez pas besoin d’utiliser l’attribut `lc_version`. Cet attribut est utilisé lorsque vous créez une référence de service.)
   * Créez un objet `System.ServiceModel.BasicHttpBinding` en obtenant la valeur du champ `FormsServiceClient.Endpoint.Binding`. Convertissez la valeur de retour en `BasicHttpBinding`.
   * Définissez le champ `MessageEncoding` de l’objet `System.ServiceModel.BasicHttpBinding` sur `WSMessageEncoding.Mtom`. Cette valeur garantit l’utilisation de MTOM.
   * Activez l’authentification HTTP de base en effectuant les tâches suivantes :

      * Attribuez le nom d’utilisateur AEM forms au champ `FormsServiceClient.ClientCredentials.UserName.UserName`.
      * Attribuez la valeur de mot de passe correspondante au champ `FormsServiceClient.ClientCredentials.UserName.Password`.
      * Attribuez la valeur constante `HttpClientCredentialType.Basic` au champ `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
   * Attribuez la valeur constante `BasicHttpSecurityMode.TransportCredentialOnly` au champ `BasicHttpBindingSecurity.Security.Mode`.

   >[!NOTE]
   >
   >Répétez ces étapes pour le client de service `DocumentManagementServiceClient`.

1. Récupération de la conception de formulaire auprès de Content Services (obsolète)

   Récupérez le contenu en appelant la méthode `retrieveContent` de l’objet `DocumentManagementServiceClient` et en transmettant les valeurs suivantes :

   * Une valeur string qui spécifie le magasin où le contenu est ajouté. Le magasin par défaut est `SpacesStore`. Cette valeur est un paramètre obligatoire.
   * Une valeur string qui spécifie le chemin d’accès complet du contenu à récupérer (par exemple, `/Company Home/Form Designs/Loan.xdp`). Cette valeur est un paramètre obligatoire.
   * Une valeur string qui spécifie la version. Cette valeur est un paramètre facultatif et vous pouvez transmettre une chaîne vide. Dans ce cas, la dernière version est récupérée.
   * Un paramètre de sortie string qui stocke la valeur du lien de navigation.
   * Un paramètre de sortie `BLOB` qui stocke le contenu. Vous pouvez utiliser ce paramètre de sortie pour récupérer le contenu.
   * Un paramètre de sortie `ServiceReference1.MyMapOf_xsd_string_To_xsd_anyType` qui stocke les attributs de contenu.
   * Un paramètre de sortie `CRCResult`. Au lieu d’utiliser cet objet, vous pouvez utiliser le paramètre de sortie `BLOB` pour obtenir le contenu.

1. Rendu d’un formulaire PDF interactif

   Appelez la méthode `renderPDFForm2` de l’objet `FormsServiceClient` et transmettez les valeurs suivantes :

   * Objet `BLOB` contenant la conception de formulaire récupérée dans Content Services (obsolète).
   * Objet `BLOB` contenant les données à fusionner avec le formulaire. Si vous ne souhaitez pas fusionner de données, transmettez un objet `BLOB` vide.
   * Objet `PDFFormRenderSpec` qui stocke les options d’exécution. Cette valeur est un paramètre facultatif. Vous pouvez spécifier `null` si vous ne souhaitez pas spécifier d’options d’exécution.
   * Objet `URLSpec` contenant des valeurs URI. Cette valeur est un paramètre facultatif et vous pouvez spécifier `null`.
   * Objet `Map` qui stocke les pièces jointes. Cette valeur est un paramètre facultatif. Vous pouvez spécifier `null` si vous ne souhaitez pas joindre de fichiers au formulaire.
   * Un paramètre de sortie long utilisé pour stocker le nombre de pages.
   * Paramètre de sortie string utilisé pour stocker la valeur du paramètre régional.
   * Un paramètre de sortie `FormsResult` utilisé pour stocker le formulaire PDF interactif `.`

   La méthode `renderPDFForm2` renvoie un objet `FormsResult` contenant le formulaire PDF interactif.

1. Exécution d’une action avec le flux de données de formulaire

   * Créez un objet `BLOB` contenant des données de formulaire en obtenant la valeur du champ `FormsResult` de l’objet `outputContent`.
   * Créez un objet `System.IO.FileStream` en appelant son constructeur. Transmettez une valeur string qui représente l’emplacement du fichier du document PDF interactif et le mode d’ouverture du fichier.
   * Créez un tableau d’octets qui stocke le contenu de l’objet `BLOB` récupéré de l’objet `FormsResult`. Renseignez le tableau d’octets en obtenant la valeur du membre de données `MTOM` de l’objet `BLOB`.
   * Créez un objet `System.IO.BinaryWriter` en appelant son constructeur et en transmettant l’objet `System.IO.FileStream`.
   * Ecrivez le contenu du tableau d’octets dans un fichier PDF en appelant la méthode `System.IO.BinaryWriter` de l’objet `Write` et en transmettant le tableau d’octets.

**Voir également**

[Appel d’AEM Forms à l’aide de MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
