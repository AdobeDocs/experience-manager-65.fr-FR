---
title: Assembler des documents PDF chiffrés
description: Assemblez des documents PDF chiffrés à l’aide de l’API Java et de l’API Web Service.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
role: Developer
exl-id: 2caaca74-640a-4257-a81b-3e8b295cd182
solution: Experience Manager, Experience Manager Forms
source-git-commit: 76fffb11c56dbf7ebee9f6805ae0799cd32985fe
workflow-type: tm+mt
source-wordcount: '1641'
ht-degree: 98%

---

# Assembler des documents PDF chiffrés {#assembling-encrypted-pdf-documents}

**Les exemples et les échantillons de ce document sont réservés à l’environnement AEM Forms sur JEE.**

Vous pouvez chiffrer un document PDF avec un mot de passe en utilisant le service Assembler. Après le chiffrement d’un document PDF avec un mot de passe, l’utilisateur doit spécifier un mot de passe pour l’afficher dans Adobe Reader ou Acrobat. Pour chiffrer un document de PDF avec un mot de passe, le document DDX doit contenir les valeurs d’élément de chiffrement requises pour chiffrer un document de PDF.

Dans le cadre de cette discussion, supposons que le document DDX suivant soit utilisé.

```xml
 <?xml version="1.0" encoding="UTF-8"?>
 <DDX xmlns="https://ns.adobe.com/DDX/1.0/">
        <PDF result="EncryptLoan.pdf" encryption="userProtect">
         <PDF source="inDoc" />
     </PDF>
     <PasswordEncryptionProfile name="userProtect" compatibilityLevel="Acrobat7">
         <OpenPassword>AdobeOpen</OpenPassword>
        </PasswordEncryptionProfile>
 </DDX>
```

Dans ce document DDX, remarquez que la valeur `inDoc` est attribuée à lʼattribut source. Dans les cas où un seul document PDF d’entrée est transmis au service Assembler et un seul document PDF est renvoyé, et que vous appelez lʼopération `invokeOneDocument`, attribuez la valeur `inDoc` à l’attribut source du PDF. Lors de l’appel de lʼopération `invokeOneDocument`, la valeur `inDoc` est une clé prédéfinie qui doit être spécifiée dans le document DDX.

En revanche, lors de la transmission de plusieurs documents PDF d’entrée au service Assembler, vous pouvez appeler lʼopération `invokeDDX`. Dans ce cas, attribuez le nom de fichier du document PDF d’entrée à l’attribut `source`.

Il n’est pas nécessaire que le service de chiffrement fasse partie de votre installation AEM Forms pour chiffrer un document PDF avec un mot de passe. Voir [Chiffrer et déchiffrer des documents PDF](/help/forms/developing/encrypting-decrypting-pdf-documents.md).

>[!NOTE]
>
>Pour plus d’informations sur le service Assembler, consultez [Références des services pour AEM Forms](https://help.adobe.com/fr_FR/livecycle/11.0/Services/index.html).

>[!NOTE]
>
>Pour plus d’informations sur les documents DDX, consultez la section [Guide de référence du service Assembler et de DDX](https://www.adobe.com/go/learn_aemforms_ddx_63).

## Résumé des étapes {#summary-of-steps}

Pour assembler un document PDF chiffré, procédez comme suit :

1. Incluez les fichiers de projet.
1. Créez un client Assembler PDF.
1. Référencez un document DX existant.
1. Référencez un document PDF non sécurisé.
1. Définissez les options d’exécution.
1. Chiffrez le document.
1. Enregistrez le document PDF chiffré.

**Incluez les fichiers de projet**.

Incluez les fichiers nécessaires dans votre projet de développement. Si vous créez une application cliente à l’aide de Java, incluez les fichiers JAR nécessaires. Si vous utilisez des services Web, veillez à inclure les fichiers proxy.

Les fichiers JAR suivants doivent être ajoutés au chemin d’accès aux classes de votre projet :

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-assembler-client.jar
* adobe-utility.jar (obligatoire si AEM Forms est déployé sur JBoss)
* jbossall-client.jar (obligatoire si AEM Forms est déployé sur JBoss)

Si AEM Forms est déployé sur un serveur d’applications J2EE pris en charge et différent de JBoss, vous devez remplacer les fichiers adobe-utilities.jar et jbossall-client.jar par des fichiers JAR spécifiques au serveur d’applications J2EE sur lequel AEM Forms est déployé. Pour plus d’informations sur l’emplacement de tous les fichiers JAR d’AEM Forms, consultez [Inclure les fichiers de la bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Créer un client Assembler**

Avant de pouvoir effectuer une opération Assembler de manière programmée, vous devez créer un client de service Assembler.

**Référencer un document DDX existant**

Un document DDX doit être référencé pour assembler un document PDF. Prenons par exemple le document DDX qui a été présenté dans cette section. Pour chiffrer un document PDF, le document DDX doit contenir l’élément `PasswordEncryptionProfile`.

**Référencer un document PDF non sécurisé**

Un document PDF non sécurisé doit être référencé et transmis au service Assembler pour le chiffrer. Si vous référencez un document PDF déjà chiffré, une exception est générée.

**Définir les options d’exécution**

Vous pouvez définir des options d’exécution qui contrôlent le comportement du service Assembler lorsqu’il effectue une tâche. Par exemple, vous pouvez définir une option qui indique au service Assembler de continuer à traiter une tâche même en cas d’erreur. Pour plus d’informations sur les options d’exécution que vous pouvez définir, consultez la référence de la classe `AssemblerOptionSpec` dans [Référence de l’API AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

**Chiffrer le document**

Après avoir créé le client de service Assembler, référencé le document DDX contenant les informations de chiffrement, référencé un document PDF non sécurisé et défini les options d’exécution, vous pouvez appeler l’opération `invokeOneDocument`. Comme un seul document PDF d’entrée est transmis au service Assembler (et qu’un seul document est renvoyé), vous pouvez utiliser l’opération `invokeOneDocument` au lieu de l’opération `invokeDDX`.

**Enregistrer le document PDF chiffré**

Si un seul document PDF est transmis au service Assembler, ce dernier renvoie un seul document au lieu d’un objet de collection. En d’autres termes, lors de l’appel de l’opération `invokeOneDocument`, un seul document est renvoyé. Comme le document DDX référencé dans cette section contient des informations de chiffrement, le service Assembler renvoie un document PDF chiffré par un mot de passe.

**Voir également**

[Inclusion des fichiers de bibliothèque Java d’AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Assembler les documents PDF par programmation](/help/forms/developing/programmatically-assembling-pdf-documents.md)

## Assembler un document PDF chiffré à l’aide de l’API Java {#assemble-an-encrypted-pdf-document-using-the-java-api}

1. Incluez les fichiers de projet.

   Incluez les fichiers JAR clients, tels que adobe-assembler-client.jar, dans le chemin d’accès aux classes de votre projet Java.

1. Créez un client Assembler.

   * Créez un objet `ServiceClientFactory` qui contient des propriétés de connexion.
   * Créez un objet `AssemblerServiceClient` en utilisant son constructeur et en transmettant l’objet `ServiceClientFactory`.

1. Référencez un document DX existant.

   * Créez un objet `java.io.FileInputStream` qui représente le document DDX en utilisant son constructeur et en transmettant une valeur de chaîne qui spécifie l’emplacement du fichier DDX.
   * Créez un objet `com.adobe.idp.Document` en utilisant son constructeur et en transmettant l’objet `java.io.FileInputStream`. 

1. Référencez un document PDF non sécurisé.

   * Créez un objet `java.io.FileInputStream` en utilisant son constructeur et en transmettant l’emplacement d’un document PDF non sécurisé.
   * Créez un objet `com.adobe.idp.Document` et transmettez l’objet `java.io.FileInputStream` qui contient le document PDF. Cet objet `com.adobe.idp.Document` est transmis à la méthode `invokeOneDocument`.

1. Définissez les options d’exécution.

   * Créez un objet `AssemblerOptionSpec` qui stocke les options d’exécution en utilisant son constructeur.
   * Définissez les options d’exécution pour répondre à vos exigences professionnelles en appelant une méthode appartenant à l’objet `AssemblerOptionSpec`. Par exemple, pour demander au service Assembler de continuer à traiter une tâche en cas d’erreur, appelez la méthode `setFailOnError` de l’objet `AssemblerOptionSpec` et transmettez `false`.

1. Chiffrez le document.

   Appelez la méthode `invokeOneDocument` de l’objet `AssemblerServiceClient` et transmettez les valeurs suivantes :

   * Objet `com.adobe.idp.Document` représentant le document DDX. Assurez-vous que ce document DDX contient la valeur `inDoc` pour l’élément PDF source.
   * Objet `com.adobe.idp.Document` contenant le document PDF non sécurisé.
   * Objet `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` spécifiant les options d’exécution, notamment la police par défaut et le niveau de log de traitement.

   La méthode `invokeOneDocument` renvoie un objet `com.adobe.idp.Document` qui contient un document PDF chiffré par mot de passe.

1. Enregistrez le document PDF chiffré.

   * Créez un objet `java.io.File` et assurez-vous que l’extension du nom du fichier est .pdf.
   * Appelez la méthode `copyToFile` de l’objet `Document` pour copier le contenu de l’objet `Document` dans le fichier. Veillez à utiliser l’objet `Document` renvoyé par la méthode `invokeOneDocument`.

**Voir également**

[Démarrage rapide (mode SOAP) : assembler un document PDF chiffré à l’aide de l’API Java.](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-assembling-an-encrypted-pdf-document-using-the-java-api)

## Assembler un document PDF chiffré à l’aide de l’API Web Service {#assemble-an-encrypted-pdf-document-using-the-web-service-api}

1. Incluez les fichiers de projet.

   Créez un projet Microsoft .NET qui utilise MTOM. Veillez à utiliser la définition WSDL suivante lors de la définition d’une référence de service : `http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Remplacez `localhost` par l’adresse IP du serveur hébergeant AEM Forms.

1. Créez un client Assembler.

   * Créez un objet `AssemblerServiceClient` en utilisant son constructeur par défaut.
   * Créez un objet `AssemblerServiceClient.Endpoint.Address` en utilisant le constructeur `System.ServiceModel.EndpointAddress`. Transmettez une valeur de chaîne qui spécifie le WSDL au service AEM Forms (par exemple, `http://localhost:8080/soap/services/AssemblerService?blob=mtom`). Vous n’avez pas besoin d’utiliser l’attribut `lc_version`. Cet attribut est utilisé lorsque vous créez une référence de service.
   * Créez un objet `System.ServiceModel.BasicHttpBinding` en récupérant la valeur du champ `AssemblerServiceClient.Endpoint.Binding`. Convertissez la valeur de retour en `BasicHttpBinding`.
   * Définissez le champ `MessageEncoding` de l’objet `System.ServiceModel.BasicHttpBinding` sur `WSMessageEncoding.Mtom`. Cette valeur garantit l’utilisation de MTOM.
   * Activez l’authentification HTTP de base en effectuant les tâches suivantes :

      * Attribuez le nom d’utilisateur AEM forms au champ `AssemblerServiceClient.ClientCredentials.UserName.UserName`.
      * Attribuez la valeur de mot de passe correspondante au champ `AssemblerServiceClient.ClientCredentials.UserName.Password`.
      * Attribuez la valeur constante `HttpClientCredentialType.Basic` au champ `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Attribuez la valeur constante `BasicHttpSecurityMode.TransportCredentialOnly` au champ `BasicHttpBindingSecurity.Security.Mode`.

1. Référencez un document DX existant.

   * Créez un objet `BLOB` en utilisant son constructeur. L’objet `BLOB` sert à stocker le document DDX.
   * Créez un objet `System.IO.FileStream` en appelant son constructeur et en transmettant une valeur de chaîne qui représente l’emplacement du fichier du document DDX et le mode d’ouverture du fichier.
   * Créez un tableau d’octets qui stocke le contenu de l’objet `System.IO.FileStream`. Vous pouvez déterminer la taille du tableau d’octets en obtenant la propriété `Length` de l’objet `System.IO.FileStream`.
   * Renseignez le tableau d’octets avec les données de flux en appelant la méthode `Read` de l’objet `System.IO.FileStream` et en transmettant le tableau d’octets, la position de départ et la longueur du flux à lire.
   * Renseignez l’objet `BLOB` en attribuant le contenu du tableau d’octets à son champ `MTOM`.

1. Référencez un document PDF non sécurisé.

   * Créez un objet `BLOB` en utilisant son constructeur. L’objet `BLOB` sert à stocker le document PDF d’entrée. Cet objet `BLOB` est transmis à `invokeOneDocument` comme argument.
   * Créez un objet `System.IO.FileStream` en appelant son constructeur et en transmettant une valeur de chaîne qui représente l’emplacement du fichier PDF d’entrée et le mode d’ouverture du fichier.
   * Créez un tableau d’octets qui stocke le contenu de l’objet `System.IO.FileStream`. Vous pouvez déterminer la taille du tableau d’octets en obtenant la propriété `Length` de l’objet `System.IO.FileStream`.
   * Renseignez le tableau d’octets avec les données de flux en appelant la méthode `Read` de l’objet `System.IO.FileStream` et en transmettant le tableau d’octets, la position de départ et la longueur du flux à lire.
   * Renseignez l’objet `BLOB` en affectant à son champ `MTOM` le contenu du tableau d’octets.

1. Définissez les options d’exécution.

   * Créez un objet `AssemblerOptionSpec` qui stocke les options d’exécution en utilisant son constructeur.
   * Définissez les options d’exécution pour répondre à vos exigences professionnelles en attribuant une valeur à un membre de données qui appartient à l’objet `AssemblerOptionSpec`. Par exemple, pour demander au service Assembler de continuer à traiter une tâche en cas d’erreur, affectez `false` au membre de données `failOnError` de l’objet `AssemblerOptionSpec`.

1. Chiffrez le document.

   Appelez la méthode `invokeOneDocument` de l’objet `AssemblerServiceClient` et transmettez les valeurs suivantes :

   * Un objet `BLOB` représentant le document DDX
   * Un objet `BLOB` qui représente le document PDF non protégé
   * Un objet `AssemblerOptionSpec` qui spécifie les options d’exécution

   La méthode `invokeOneDocument` renvoie un objet `BLOB` contenant un document PDF chiffré.

1. Enregistrez le document PDF chiffré.

   * Créez un objet `System.IO.FileStream` en appelant son constructeur et en transmettant une valeur string qui représente l’emplacement du fichier du document PDF chiffré et le mode d’ouverture du fichier.
   * Créez un tableau dʼoctets qui stocke le contenu de lʼobjet `BLOB` que la méthode `invokeOneDocument` a renvoyé. Renseignez le tableau d’octets en obtenant la valeur du membre de données `MTOM` de l’objet `BLOB`.
   * Créez un objet `System.IO.BinaryWriter` en utilisant son constructeur et en transmettant l’objet `System.IO.FileStream`.
   * Écrivez le contenu du tableau d’octets dans un fichier PDF en appelant la méthode `Write` de l’objet `System.IO.BinaryWriter` et en transmettant le tableau d’octets.

**Voir également**

[Appeler AEM Forms en utilisant MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
