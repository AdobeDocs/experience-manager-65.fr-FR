---
title: Transmission de documents au service Forms
description: Transmettez au service Forms un objet com.adobe.idp.Document contenant la conception du formulaire. Le service Forms effectue le rendu de la conception de formulaire située dans l’objet com.adobe.idp.Document.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/rendering_forms
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
role: Developer
exl-id: 29c7ebda-407a-464b-a9db-054163f5b737
solution: Experience Manager, Experience Manager Forms
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: ht
source-wordcount: '1677'
ht-degree: 100%

---

# Transmettre des documents au service Forms {#passing-documents-to-the-formsservice}

**Les exemples et les échantillons de ce document sont réservés à l’environnement AEM Forms sur JEE.**

Le service AEM Forms effectue le rendu de PDF forms interactifs sur les appareils clients, généralement des navigateurs Web, afin de collecter des informations auprès des utilisateurs. Un formulaire PDF interactif est basé sur une conception de formulaire généralement enregistrée sous forme de fichier XDP et créée dans Designer. À partir d’AEM Forms, vous pouvez transmettre au service Forms un objet `com.adobe.idp.Document` qui contient la conception du formulaire. Le service Forms effectue ensuite le rendu de la conception du formulaire située dans l’objet `com.adobe.idp.Document`.

L’avantage de transmettre un objet `com.adobe.idp.Document` au service Forms est que les autres opérations du service renvoient une instance `com.adobe.idp.Document`. En d’autres termes, vous pouvez obtenir une instance `com.adobe.idp.Document` à partir d’une autre opération de service et en effectuer le rendu. Par exemple, supposons qu’un fichier XDP soit stocké dans un nœud de Content Services (obsolète) appelé `/Company Home/Form Designs`, comme illustré ci-dessous.

Vous pouvez récupérer Loan.xdp par programmation à partir de Content Services (obsolète) (obsolète) et transmettre le fichier XDP au service Forms dans un objet `com.adobe.idp.Document`.

>[!NOTE]
>
>Pour plus d’informations sur le service Forms, consultez [Références des services pour AEM Forms](https://help.adobe.com/fr_FR/livecycle/11.0/Services/index.html).

## Résumé des étapes {#summary-of-steps}

Pour transmettre un document obtenu à partir de Content Services (obsolète) au service Forms, effectuez les tâches suivantes :

1. Incluez les fichiers de projet.
1. Créez un objet Forms et un objet API Client de Document Management.
1. Récupérez la conception de formulaire auprès de Content Services (obsolète).
1. Effectuez le rendu du formulaire PDF interactif.
1. Exécutez une action avec le flux de données de formulaire.

**Inclure les fichiers de projet**

Incluez les fichiers nécessaires dans votre projet de développement. Si vous créez une application cliente à l’aide de Java, incluez les fichiers JAR nécessaires. Si vous utilisez des services web, incluez les fichiers proxy.

**Créer un objet API Client Forms et un objet API Client Document Management**

Avant d’effectuer par programmation une opération d’API de service Forms, créez un objet API client Forms. En outre, comme ce workflow récupère un fichier XDP de Content Services (obsolète), créez un objet API Document Management.

**Récupérer la conception de formulaire à partir de Content Services (obsolète)**

Récupérez le fichier XDP à partir de Content Services (obsolète) à l’aide de l’API Java ou de service web. Le fichier XDP est renvoyé dans une instance `com.adobe.idp.Document` (ou une instance `BLOB` si vous utilisez des services Web). Vous pouvez ensuite transmettre l’instance `com.adobe.idp.Document` au service Forms.

**Effectuer le rendu d’un formulaire PDF interactif**

Pour effectuer le rendu d’un formulaire interactif, transmettez l’instance `com.adobe.idp.Document` renvoyée par Content Services (obsolète) au service Forms.

>[!NOTE]
>
>Vous pouvez transmettre au service Forms un `com.adobe.idp.Document` qui contient la conception du formulaire. Deux nouvelles méthodes appelées `renderPDFForm2` et `renderHTMLForm2` acceptent un objet `com.adobe.idp.Document` qui contient une conception de formulaire.

**Exécuter une action avec le flux de données du formulaire**

Selon le type d’application client, vous pouvez écrire le formulaire dans le navigateur Web du client ou l’enregistrer comme fichier PDF. En règle générale, une application Web écrit le formulaire dans le navigateur Web. Cependant, une application de bureau enregistre généralement le formulaire sous forme de fichier PDF.

**Voir également**

[Inclusion des fichiers de bibliothèque Java d’AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Démarrages rapides de l’API Forms Service](/help/forms/developing/forms-service-api-quick-starts.md#forms-service-api-quick-starts)

## Transmettre des documents au service Forms à l’aide de l’API Java {#pass-documents-to-the-forms-service-using-the-java-api}

Transmettez un document obtenu à partir de Content Services (obsolète) à l’aide du service Forms et de l’API Content Services (obsolète) (Java) :

1. Inclure les fichiers du projet

   Incluez les fichiers JAR du client, tels que adobe-forms-client.jar et adobe-contentservices-client.jar, dans le chemin d’accès aux classes de votre projet Java.

1. Créer un objet API Client Forms et un objet API Client Document Management

   * Créez un objet `ServiceClientFactory` qui contient des propriétés de connexion. (Voir [Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties).)
   * Créez un objet `FormsServiceClient` en utilisant son constructeur et en transmettant l’objet `ServiceClientFactory`.
   * Créez un objet `DocumentManagementServiceClientImpl` en utilisant son constructeur et en transmettant l’objet `ServiceClientFactory`. 

1. Récupérer la conception du formulaire à partir de Content Services (obsolète)

   Appelez la méthode `retrieveContent` de l’objet `DocumentManagementServiceClientImpl` et transmettez les valeurs suivantes :

   * Valeur string qui spécifie le magasin où le contenu est ajouté. Le magasin par défaut est `SpacesStore`. Cette valeur est un paramètre obligatoire.
   * Valeur string qui spécifie le chemin d’accès complet du contenu à récupérer (par exemple `/Company Home/Form Designs/Loan.xdp`). Cette valeur est un paramètre obligatoire.
   * Valeur string qui spécifie la version. Cette valeur est un paramètre facultatif et vous pouvez transmettre une chaîne vide. Dans ce cas, la dernière version est récupérée.

   La méthode `retrieveContent` renvoie un objet `CRCResult` qui contient le fichier XDP. Obtenez une instance `com.adobe.idp.Document` en appelant la méthode `getDocument` de l’objet `CRCResult`.

1. Effectuer le rendu d’un formulaire PDF interactif

   Appelez la méthode `renderPDFForm2` de l’objet `FormsServiceClient` et transmettez les valeurs suivantes :

   * Un objet `com.adobe.idp.Document` contenant la conception du formulaire récupéré à partir de Content Services (obsolète).
   * Un objet `com.adobe.idp.Document` qui contient les données à fusionner avec le formulaire. Si vous ne souhaitez pas fusionner des données, transmettez un objet `com.adobe.idp.Document`.
   * Un objet `PDFFormRenderSpec` qui stocke les options d’exécution. Cette valeur est un paramètre facultatif. Vous pouvez indiquer `null` si vous ne souhaitez pas spécifier d’options d’exécution.
   * Un objet `URLSpec` qui contient des valeurs URI. Cette valeur est un paramètre facultatif. Vous pouvez spécifier `null`.
   * Un objet `java.util.HashMap` qui stocke les pièces jointes. Cette valeur est un paramètre facultatif. Vous pouvez spécifier `null` si vous ne souhaitez pas joindre de fichiers au formulaire.

   La méthode `renderPDFForm` renvoie un objet `FormsResult` qui contient un flux de données de formulaire qui doit être écrit dans le navigateur Web du client.

1. Effectuer une action avec le flux de données du formulaire

   * Créez un objet `com.adobe.idp.Document` en appelant la méthode `getOutputContent` de l’objet `FormsResult`.
   * Accédez au type de contenu de l’objet `com.adobe.idp.Document` en appelant sa méthode `getContentType`.
   * Définissez le type de contenu de l’objet `javax.servlet.http.HttpServletResponse` en appelant sa méthode `setContentType` et en transmettant le type de contenu de l’objet `com.adobe.idp.Document`.
   * Créez un objet `javax.servlet.ServletOutputStream` utilisé pour écrire le flux de données de formulaire dans le navigateur web client en appelant la méthode `getOutputStream` de l’objet `javax.servlet.http.HttpServletResponse`.
   * Créez un objet `java.io.InputStream` en appelant la méthode `getInputStream` de l’objet `com.adobe.idp.Document`.
   * Créez un tableau d’octets et renseignez-le avec le flux de données du formulaire en appelant la méthode `read` de l’objet `InputStream`. Transmettez le tableau d’octets comme argument.
   * Appelez la méthode `write` de l’objet `javax.servlet.ServletOutputStream` pour envoyer le flux de données du formulaire au navigateur Web du client. Transmettez le tableau d’octets à la méthode `write`.

**Voir également**

[Démarrage rapide (mode SOAP) : transmettre des documents au service Forms à l’aide de l’API Java](/help/forms/developing/forms-service-api-quick-starts.md#quick-start-soap-mode-passing-documents-to-the-forms-service-using-the-java-api)

[Inclusion des fichiers de bibliothèque Java d’AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Transmettre des documents au service Forms à l’aide de l’API du service web {#pass-documents-to-the-forms-service-using-the-web-service-api}

Transmettez un document obtenu à partir de Content Services (obsolète) en utilisant le service Forms et de l’API (service Web) de Content Services (obsolète) :

1. Inclure les fichiers du projet

   Créez un projet Microsoft .NET qui utilise MTOM. Étant donné que cette application cliente appelle deux services AEM Forms, créez deux références de service. Utilisez la définition WSDL suivante pour la référence de service associée au service Forms : `http://localhost:8080/soap/services/FormsService?WSDL&lc_version=9.0.1`.

   Utilisez la définition WSDL suivante pour la référence de service associée au service Document Management : `http://localhost:8080/soap/services/DocumentManagementService?WSDL&lc_version=9.0.1`.

   Étant donné que le type de données `BLOB` est commun aux deux références de service, il qualifie entièrement le type de données `BLOB` lors de son utilisation. Dans le démarrage rapide du service web correspondant, toutes les instances `BLOB` sont entièrement qualifiées.

   >[!NOTE]
   >
   >Remplacez `localhost` par l’adresse IP du serveur hébergeant AEM Forms.

1. Créer un objet API Client Forms et un objet API Client Document Management

   * Créez un objet `FormsServiceClient` en utilisant son constructeur par défaut.
   * Créez un objet `FormsServiceClient.Endpoint.Address` en utilisant le constructeur `System.ServiceModel.EndpointAddress`. Transmettez une valeur de chaîne qui spécifie le WSDL au service AEM Forms (par exemple, `http://localhost:8080/soap/services/FormsService?WSDL`). Vous n’avez pas besoin d’utiliser l’attribut `lc_version`. Cet attribut est utilisé lorsque vous créez une référence de service.)
   * Créez un objet `System.ServiceModel.BasicHttpBinding` en obtenant la valeur du champ `FormsServiceClient.Endpoint.Binding`. Convertissez la valeur de retour en `BasicHttpBinding`.
   * Définissez le champ `MessageEncoding` de l’objet `System.ServiceModel.BasicHttpBinding` sur `WSMessageEncoding.Mtom`. Cette valeur garantit l’utilisation de MTOM.
   * Activez l’authentification HTTP de base en effectuant les tâches suivantes :

      * Attribuez le nom d’utilisateur AEM forms au champ `FormsServiceClient.ClientCredentials.UserName.UserName`.
      * Attribuez la valeur de mot de passe correspondante au champ `FormsServiceClient.ClientCredentials.UserName.Password`.
      * Attribuez la valeur constante `HttpClientCredentialType.Basic` au champ `BasicHttpBindingSecurity.Transport.ClientCredentialType`.

   * Attribuez la valeur constante `BasicHttpSecurityMode.TransportCredentialOnly` au champ `BasicHttpBindingSecurity.Security.Mode`.

   >[!NOTE]
   >
   >Répétez ces étapes pour le client de service `DocumentManagementServiceClient`.

1. Récupérer la conception du formulaire à partir de Content Services (obsolète)

   Récupérez le contenu en appelant la méthode `retrieveContent` de l’objet `DocumentManagementServiceClient` et en transmettant les valeurs suivantes :

   * Valeur string qui spécifie le magasin où le contenu est ajouté. Le magasin par défaut est `SpacesStore`. Cette valeur est un paramètre obligatoire.
   * Valeur string qui spécifie le chemin d’accès complet du contenu à récupérer (par exemple `/Company Home/Form Designs/Loan.xdp`). Cette valeur est un paramètre obligatoire.
   * Valeur string qui spécifie la version. Cette valeur est un paramètre facultatif et vous pouvez transmettre une chaîne vide. Dans ce cas, la dernière version est récupérée.
   * Paramètre de sortie string qui stocke la valeur du lien de navigation.
   * Paramètre de sortie `BLOB` stockant le contenu. Vous pouvez utiliser ce paramètre de sortie pour récupérer le contenu.
   * Paramètre de sortie `ServiceReference1.MyMapOf_xsd_string_To_xsd_anyType` stockant les attributs de contenu.
   * Un paramètre de sortie `CRCResult`. Au lieu d’utiliser cet objet, vous pouvez utiliser le paramètre de sortie `BLOB` pour obtenir le contenu.

1. Effectuer le rendu d’un formulaire PDF interactif

   Appelez la méthode `renderPDFForm2` de l’objet `FormsServiceClient` et transmettez les valeurs suivantes :

   * Un objet `BLOB` contenant la conception du formulaire récupéré à partir de Content Services (obsolète).
   * Un objet `BLOB` qui contient les données à fusionner avec le formulaire. Si vous ne souhaitez pas fusionner des données, transmettez un objet `BLOB`.
   * Un objet `PDFFormRenderSpec` qui stocke les options d’exécution. Cette valeur est un paramètre facultatif. Vous pouvez indiquer `null` si vous ne souhaitez pas spécifier d’options d’exécution.
   * Un objet `URLSpec` qui contient des valeurs URI. Cette valeur est un paramètre facultatif. Vous pouvez spécifier `null`.
   * Un objet `Map` qui stocke les pièces jointes. Cette valeur est un paramètre facultatif. Vous pouvez spécifier `null` si vous ne souhaitez pas joindre de fichiers au formulaire.
   * Un paramètre de sortie long qui est utilisé pour stocker le nombre de pages.
   * Un paramètre de sortie de chaîne qui est utilisé pour stocker la valeur du paramètre régional.
   * Un paramètre de sortie `FormsResult` qui est utilisé pour stocker le formulaire PDF interactif `.`.

   La méthode `renderPDFForm2` renvoie un objet `FormsResult` qui contient le formulaire PDF interactif.

1. Effectuer une action avec le flux de données du formulaire

   * Créez un objet `BLOB` qui contient des données de formulaire en obtenant la valeur du champ `outputContent` de l’objet `FormsResult`.
   * Créez un objet `System.IO.FileStream` en utilisant son constructeur. Transmettez une valeur string qui représente l’emplacement du fichier du document PDF interactif et le mode d’ouverture du fichier.
   * Créez un tableau d’octets qui stocke le contenu de l’objet `BLOB` récupéré dans l’objet `FormsResult`. Renseignez le tableau d’octets en obtenant la valeur du membre de données `MTOM` de l’objet `BLOB`.
   * Créez un objet `System.IO.BinaryWriter` en utilisant son constructeur et en transmettant l’objet `System.IO.FileStream`.
   * Écrivez le contenu du tableau d’octets dans un fichier PDF en appelant la méthode `Write` de l’objet `System.IO.BinaryWriter` et en transmettant le tableau d’octets.

**Voir également**

[Appeler AEM Forms en utilisant MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
