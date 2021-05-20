---
title: Assemblage de documents PDF chiffrés
seo-title: Assemblage de documents PDF chiffrés
description: Assemblez des documents PDF chiffrés à l’aide de l’API Java et de l’API Web Service.
seo-description: Assemblez des documents PDF chiffrés à l’aide de l’API Java et de l’API Web Service.
uuid: d0948ec9-ab67-4fe4-9062-1c4938460b43
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 6d75c7b1-9c0e-47f3-bdb1-61acf16b97f9
role: Developer
exl-id: 2caaca74-640a-4257-a81b-3e8b295cd182
source-git-commit: b220adf6fa3e9faf94389b9a9416b7fca2f89d9d
workflow-type: tm+mt
source-wordcount: '1675'
ht-degree: 6%

---

# Assemblage de documents PDF chiffrés {#assembling-encrypted-pdf-documents}

**Les exemples et les exemples de ce document sont réservés à l’environnement AEM Forms on JEE.**

Vous pouvez chiffrer un document PDF avec un mot de passe à l’aide du service Assembler. Après le chiffrement d’un document PDF avec un mot de passe, l’utilisateur doit spécifier un mot de passe pour l’afficher dans Adobe Reader ou Acrobat. Pour chiffrer un document PDF avec un mot de passe, le document DDX doit contenir les valeurs d’élément de chiffrement requises.

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

Dans ce document DDX, notez que la valeur `inDoc` est affectée à l’attribut source. Dans les cas où un seul document PDF d’entrée est transmis au service Assembler et qu’un seul document PDF est renvoyé, et où vous appelez l’opération `invokeOneDocument` , attribuez la valeur `inDoc` à l’attribut de source PDF. Lors de l’appel de l’opération `invokeOneDocument`, la valeur `inDoc` est une clé prédéfinie qui doit être spécifiée dans le document DDX.

En revanche, lorsque vous transmettez plusieurs documents PDF d’entrée au service Assembler, vous pouvez appeler l’opération `invokeDDX`. Dans ce cas, affectez le nom de fichier du document PDF d’entrée à l’attribut `source` .

Le service Encryption ne doit pas nécessairement faire partie de votre installation AEM forms pour chiffrer un document PDF avec un mot de passe. Voir [Chiffrement et déchiffrement de documents PDF](/help/forms/developing/encrypting-decrypting-pdf-documents.md).

>[!NOTE]
>
>Pour plus d’informations sur le service Assembler, voir [Référence des services pour AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

>[!NOTE]
>
>Pour plus d’informations sur un document DDX, voir [Guide de référence du service Assembler et de DDX](https://www.adobe.com/go/learn_aemforms_ddx_63).

## Résumé des étapes {#summary-of-steps}

Pour assembler un document PDF chiffré, procédez comme suit :

1. Inclure les fichiers de projet.
1. Créez un client PDF Assembler.
1. Référencez un document DX existant.
1. Référencez un document PDF non sécurisé.
1. Définissez les options d’exécution.
1. Chiffrez le document.
1. Enregistrez le document PDF chiffré.

**Inclure les fichiers de projet**

Incluez les fichiers nécessaires dans votre projet de développement. Si vous créez une application cliente à l’aide de Java, incluez les fichiers JAR nécessaires. Si vous utilisez des services Web, veillez à inclure les fichiers proxy.

Les fichiers JAR suivants doivent être ajoutés au chemin de classe de votre projet :

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-assembler-client.jar
* adobe-utility.jar (obligatoire si AEM Forms est déployé sur JBoss)
* jbossall-client.jar (obligatoire si AEM Forms est déployé sur JBoss)

si AEM Forms est déployé sur un serveur d’applications J2EE pris en charge autre que JBoss, vous devez remplacer les fichiers adobe-utility.jar et jbossall-client.jar par des fichiers JAR spécifiques au serveur d’applications J2EE sur lequel AEM Forms est déployé. Pour plus d’informations sur l’emplacement de tous les fichiers JAR AEM Forms, voir [Inclusion des fichiers de bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Création d’un client Assembler**

Avant d’effectuer une opération Assembler par programmation, vous devez créer un client de service Assembler.

**Référence à un document DDX existant**

Un document DDX doit être référencé pour assembler un document PDF. Prenons l’exemple du document DDX introduit dans cette section. Pour chiffrer un document PDF, le document DDX doit contenir l’élément `PasswordEncryptionProfile` .

**Référence à un document PDF non protégé**

Un document PDF non sécurisé doit être référencé et transmis au service Assembler pour le chiffrer. Si vous référencez un document PDF déjà chiffré, une exception est générée.

**Définition des options d’exécution**

Vous pouvez définir des options d’exécution qui contrôlent le comportement du service Assembler lorsqu’il effectue une tâche. Par exemple, vous pouvez définir une option qui indique au service Assembler de continuer à traiter une tâche en cas d’erreur. Pour plus d’informations sur les options d’exécution que vous pouvez définir, voir la référence de classe `AssemblerOptionSpec` dans [Référence de l’API AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

**Chiffrer le document**

Après avoir créé le client de service Assembler, référencez le document DDX contenant des informations de chiffrement, référencez un document PDF non sécurisé et définissez les options d’exécution, vous pouvez appeler l’opération `invokeOneDocument`. Comme un seul document PDF d’entrée est transmis au service Assembler (et qu’un seul document est renvoyé), vous pouvez utiliser l’opération `invokeOneDocument` au lieu de l’opération `invokeDDX`.

**Enregistrement du document PDF chiffré**

Si un seul document PDF est transmis au service Assembler, le service Assembler renvoie un seul document au lieu d’un objet de collection. En d’autres termes, lors de l’appel de l’opération `invokeOneDocument`, un seul document est renvoyé. Comme le document DDX référencé dans cette section contient des informations de chiffrement, le service Assembler renvoie un document PDF chiffré avec un mot de passe.

**Voir également**

[Inclusion des fichiers de bibliothèque Java d’AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Assemblage de documents PDF par programmation](/help/forms/developing/programmatically-assembling-pdf-documents.md)

## Assemblez un document PDF chiffré à l’aide de l’API Java {#assemble-an-encrypted-pdf-document-using-the-java-api}

1. Inclure les fichiers de projet.

   Incluez des fichiers JAR client, tels que adobe-assembler-client.jar, dans le chemin d’accès à la classe de votre projet Java.

1. Créez un client Assembler.

   * Créez un objet `ServiceClientFactory` qui contient des propriétés de connexion.
   * Créez un objet `AssemblerServiceClient` en utilisant son constructeur et en transmettant l’objet `ServiceClientFactory`.

1. Référencez un document DX existant.

   * Créez un objet `java.io.FileInputStream` qui représente le document DDX en utilisant son constructeur et en transmettant une valeur string qui spécifie l’emplacement du fichier DDX.
   * Créez un objet `com.adobe.idp.Document` en utilisant son constructeur et en transmettant l’objet `java.io.FileInputStream`. 

1. Référencez un document PDF non sécurisé.

   * Créez un objet `java.io.FileInputStream` en utilisant son constructeur et en transmettant l’emplacement d’un document PDF non sécurisé.
   * Créez un objet `com.adobe.idp.Document` et transmettez l’objet `java.io.FileInputStream` contenant le document PDF. Cet objet `com.adobe.idp.Document` est transmis à la méthode `invokeOneDocument` .

1. Définissez les options d’exécution.

   * Créez un objet `AssemblerOptionSpec` qui stocke les options d’exécution à l’aide de son constructeur.
   * Définissez les options d’exécution pour répondre aux besoins de votre entreprise en appelant une méthode appartenant à l’objet `AssemblerOptionSpec` . Par exemple, pour demander au service Assembler de continuer à traiter une tâche en cas d’erreur, appelez la méthode `setFailOnError` de l’objet `false` et transmettez `AssemblerOptionSpec`.

1. Chiffrez le document.

   Appelez la méthode `invokeOneDocument` de l’objet `AssemblerServiceClient` et transmettez les valeurs suivantes :

   * Objet `com.adobe.idp.Document` représentant le document DDX. Assurez-vous que ce document DX contient la valeur `inDoc` de l’élément de source PDF.
   * Objet `com.adobe.idp.Document` contenant le document PDF non sécurisé.
   * Objet `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` qui spécifie les options d’exécution, y compris la police par défaut et le niveau de journalisation de la tâche.

   La méthode `invokeOneDocument` renvoie un objet `com.adobe.idp.Document` contenant un document PDF chiffré par mot de passe.

1. Enregistrez le document PDF chiffré.

   * Créez un objet `java.io.File` et assurez-vous que l’extension de nom de fichier est .pdf.
   * Appelez la méthode `copyToFile` de l’objet `Document` pour copier le contenu de l’objet `Document` dans le fichier. Assurez-vous d’utiliser l’objet `Document` renvoyé par la méthode `invokeOneDocument`.

**Voir également**

[Démarrage rapide (mode SOAP) : Assemblage d’un document PDF chiffré à l’aide de l’API Java](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-assembling-an-encrypted-pdf-document-using-the-java-api)

## Assemblez un document PDF chiffré à l’aide de l’API de service Web {#assemble-an-encrypted-pdf-document-using-the-web-service-api}

1. Inclure les fichiers de projet.

   Créez un projet Microsoft .NET qui utilise MTOM. Assurez-vous d’utiliser la définition WSDL suivante lors de la définition d’une référence de service : `http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Remplacez `localhost` par l’adresse IP du serveur hébergeant AEM Forms.

1. Créez un client Assembler.

   * Créez un objet `AssemblerServiceClient` à l’aide de son constructeur par défaut.
   * Créez un objet `AssemblerServiceClient.Endpoint.Address` à l’aide du constructeur `System.ServiceModel.EndpointAddress`. Transmettez une valeur string qui spécifie le WSDL au service AEM Forms (par exemple, `http://localhost:8080/soap/services/AssemblerService?blob=mtom`). Vous n’avez pas besoin d’utiliser l’attribut `lc_version`. Cet attribut est utilisé lorsque vous créez une référence de service.
   * Créez un objet `System.ServiceModel.BasicHttpBinding` en obtenant la valeur du champ `AssemblerServiceClient.Endpoint.Binding`. Convertissez la valeur de retour en `BasicHttpBinding`.
   * Définissez le champ `MessageEncoding` de l’objet `System.ServiceModel.BasicHttpBinding` sur `WSMessageEncoding.Mtom`. Cette valeur garantit l’utilisation de MTOM.
   * Activez l’authentification HTTP de base en effectuant les tâches suivantes :

      * Attribuez le nom d’utilisateur AEM forms au champ `AssemblerServiceClient.ClientCredentials.UserName.UserName`.
      * Attribuez la valeur de mot de passe correspondante au champ `AssemblerServiceClient.ClientCredentials.UserName.Password`.
      * Attribuez la valeur constante `HttpClientCredentialType.Basic` au champ `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Attribuez la valeur constante `BasicHttpSecurityMode.TransportCredentialOnly` au champ `BasicHttpBindingSecurity.Security.Mode`.

1. Référencez un document DX existant.

   * Créez un objet `BLOB` en utilisant son constructeur. L’objet `BLOB` est utilisé pour stocker le document DDX.
   * Créez un objet `System.IO.FileStream` en appelant son constructeur et en transmettant une valeur string qui représente l’emplacement du fichier du document DDX et le mode d’ouverture du fichier.
   * Créez un tableau d’octets qui stocke le contenu de l’objet `System.IO.FileStream`. Vous pouvez déterminer la taille du tableau d’octets en obtenant la propriété `System.IO.FileStream` de l’objet `Length`.
   * Renseignez le tableau d’octets avec les données de flux en appelant la méthode `System.IO.FileStream` de l’objet `Read` et en transmettant le tableau d’octets, la position de départ et la longueur du flux à lire.
   * Renseignez l’objet `BLOB` en attribuant son champ `MTOM` avec le contenu du tableau d’octets.

1. Référencez un document PDF non sécurisé.

   * Créez un objet `BLOB` en utilisant son constructeur. L’objet `BLOB` est utilisé pour stocker le document PDF d’entrée. Cet objet `BLOB` est transmis à `invokeOneDocument` en tant qu’argument.
   * Créez un objet `System.IO.FileStream` en appelant son constructeur et en transmettant une valeur string qui représente l’emplacement du fichier du document PDF d’entrée et le mode d’ouverture du fichier.
   * Créez un tableau d’octets qui stocke le contenu de l’objet `System.IO.FileStream`. Vous pouvez déterminer la taille du tableau d’octets en obtenant la propriété `System.IO.FileStream` de l’objet `Length`.
   * Renseignez le tableau d’octets avec les données de flux en appelant la méthode `System.IO.FileStream` de l’objet `Read` et en transmettant le tableau d’octets, la position de départ et la longueur du flux à lire.
   * Renseignez l’objet `BLOB` en attribuant son champ `MTOM` avec le contenu du tableau d’octets.

1. Définissez les options d’exécution.

   * Créez un objet `AssemblerOptionSpec` qui stocke les options d’exécution à l’aide de son constructeur.
   * Définissez des options d’exécution pour répondre aux besoins de votre entreprise en attribuant une valeur à un membre de données qui appartient à l’objet `AssemblerOptionSpec`. Par exemple, pour demander au service Assembler de continuer à traiter une tâche en cas d’erreur, affectez `false` au membre de données `failOnError` de l’objet `AssemblerOptionSpec`.

1. Chiffrez le document.

   Appelez la méthode `invokeOneDocument` de l’objet `AssemblerServiceClient` et transmettez les valeurs suivantes :

   * Objet `BLOB` représentant le document DDX
   * Objet `BLOB` représentant le document PDF non sécurisé
   * Objet `AssemblerOptionSpec` spécifiant les options d’exécution

   La méthode `invokeOneDocument` renvoie un objet `BLOB` contenant un document PDF chiffré.

1. Enregistrez le document PDF chiffré.

   * Créez un objet `System.IO.FileStream` en appelant son constructeur et en transmettant une valeur string qui représente l’emplacement du fichier du document PDF chiffré et le mode d’ouverture du fichier.
   * Créez un tableau d’octets qui stocke le contenu de l’objet `BLOB` renvoyé par la méthode `invokeOneDocument`. Renseignez le tableau d’octets en obtenant la valeur du membre de données `MTOM` de l’objet `BLOB`.
   * Créez un objet `System.IO.BinaryWriter` en appelant son constructeur et en transmettant l’objet `System.IO.FileStream`.
   * Ecrivez le contenu du tableau d’octets dans un fichier PDF en appelant la méthode `System.IO.BinaryWriter` de l’objet `Write` et en transmettant le tableau d’octets.

**Voir également**

[Appel d’AEM Forms à l’aide de MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
