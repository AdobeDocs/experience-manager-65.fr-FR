---
title: Assemblage de Documents PDF chiffrés
seo-title: Assemblage de Documents PDF chiffrés
description: 'null'
seo-description: 'null'
uuid: d0948ec9-ab67-4fe4-9062-1c4938460b43
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 6d75c7b1-9c0e-47f3-bdb1-61acf16b97f9
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '1639'
ht-degree: 6%

---


# Assemblage de Documents PDF chiffrés {#assembling-encrypted-pdf-documents}

Vous pouvez chiffrer un document PDF avec un mot de passe à l’aide du service Assembler. Après le chiffrement d’un document PDF avec un mot de passe, l’utilisateur doit spécifier un mot de passe pour l’afficher dans Adobe Reader ou Acrobat. Pour chiffrer un document PDF avec un mot de passe, le document DDX doit contenir les valeurs d’élément de chiffrement requises.

Aux fins de cette discussion, supposons que le document DDX suivant soit utilisé.

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

Dans ce document DDX, notez que la valeur est affectée à l’attribut source `inDoc`. Dans les cas où un seul document PDF d’entrée est transmis au service Assembler et où un document PDF est renvoyé et où vous appelez l’ `invokeOneDocument` opération, affectez la valeur `inDoc` à l’attribut source PDF. Lors de l’appel de l’ `invokeOneDocument` opération, la `inDoc` valeur est une clé prédéfinie qui doit être spécifiée dans le document DDX.

En revanche, lorsque vous transmettez deux ou plusieurs documents PDF d’entrée au service Assembler, vous pouvez appeler l’ `invokeDDX` opération. Dans ce cas, attribuez le nom de fichier du document PDF d’entrée à l’ `source` attribut.

Le service Encryption n’a pas besoin de faire partie de votre installation AEM forms pour chiffrer un document PDF avec un mot de passe. Voir [Chiffrement et déchiffrement des Documents](/help/forms/developing/encrypting-decrypting-pdf-documents.md)PDF.

>[!NOTE]
>
>For more information about the Assembler service, see [Services Reference for AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

>[!NOTE]
>
>Pour plus d’informations sur un document DDX, voir [Service Assembler et Référence](https://www.adobe.com/go/learn_aemforms_ddx_63)DDX.

## Résumé des étapes {#summary-of-steps}

Pour assembler un document PDF chiffré, procédez comme suit :

1. Incluez des fichiers de projet.
1. Créez un client PDF Assembler.
1. Référencez un document DDX existant.
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
* adobe-utilities.jar (requis si le AEM Forms est déployé sur JBoss)
* jbossall-client.jar (requis si le AEM Forms est déployé sur JBoss)

si le AEM Forms est déployé sur un serveur d’applications J2EE pris en charge autre que JBoss, vous devez remplacer les fichiers adobe-utilities.jar et jbossall-client.jar par des fichiers JAR spécifiques au serveur d’applications J2EE sur lequel le AEM Forms est déployé. For information about the location of all AEM Forms JAR files, see [Including AEM Forms Java library files](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Création d’un client Assembler**

Avant de pouvoir exécuter une opération Assembler par programmation, vous devez créer un client de service Assembler.

**Référencer un document DDX existant**

Un document DDX doit être référencé pour assembler un document PDF. Prenons l’exemple du document DDX introduit dans cette section. Pour chiffrer un document PDF, le document DDX doit contenir l’ `PasswordEncryptionProfile` élément.

**Référence à un document PDF non sécurisé**

Un document PDF non sécurisé doit être référencé et transmis au service Assembler pour le chiffrer. Si vous référencez un document PDF déjà chiffré, une exception est générée.

**Définition des options d’exécution**

Vous pouvez définir des options d’exécution qui contrôlent le comportement du service Assembler lorsqu’il effectue une tâche. Par exemple, vous pouvez définir une option qui indique au service Assembler de continuer à traiter une tâche en cas d’erreur. Pour plus d’informations sur les options d’exécution que vous pouvez définir, voir la référence de `AssemblerOptionSpec` classe dans Référence [API](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)AEM Forms.

**Chiffrer le document**

Après avoir créé le client de service Assembler, fait référence au document DDX qui contient des informations de chiffrement, fait référence à un document PDF non sécurisé et défini les options d’exécution, vous pouvez appeler l’ `invokeOneDocument` opération. Comme un seul document PDF d’entrée est transmis au service Assembler (et qu’un document est renvoyé), vous pouvez utiliser l’ `invokeOneDocument` opération au lieu de l’ `invokeDDX` opération.

**Enregistrer le document PDF chiffré**

Si un seul document PDF est transmis au service Assembler, le service Assembler renvoie un seul document au lieu d’un objet de collection. En d’autres termes, lors de l’appel de l’ `invokeOneDocument` opération, un seul document est renvoyé. Comme le document DDX référencé dans cette section contient des informations de chiffrement, le service Assembler renvoie un document PDF chiffré avec un mot de passe.

**Voir également**

[Inclusion des fichiers de bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Assemblage par programmation de Documents PDF](/help/forms/developing/programmatically-assembling-pdf-documents.md)

## Assemblage d’un document PDF chiffré à l’aide de l’API Java {#assemble-an-encrypted-pdf-document-using-the-java-api}

1. Incluez des fichiers de projet.

   Incluez des fichiers JAR client, tels que adobe-assembler-client.jar, dans le chemin de classe de votre projet Java.

1. Créez un client Assembler.

   * Créez un objet `ServiceClientFactory` qui contient des propriétés de connexion.
   * Create an `AssemblerServiceClient` object by using its constructor and passing the `ServiceClientFactory` object.

1. Référencez un document DDX existant.

   * Créez un `java.io.FileInputStream` objet qui représente le document DDX en utilisant son constructeur et en transmettant une valeur de chaîne qui spécifie l’emplacement du fichier DDX.
   * Créez un objet `com.adobe.idp.Document` en utilisant son constructeur et en transmettant l’objet `java.io.FileInputStream`. 

1. Référencez un document PDF non sécurisé.

   * Créez un `java.io.FileInputStream` objet en utilisant son constructeur et en transmettant l’emplacement d’un document PDF non sécurisé.
   * Créez un `com.adobe.idp.Document` objet et transmettez l’ `java.io.FileInputStream` objet contenant le document PDF. Cet `com.adobe.idp.Document` objet est transmis à la `invokeOneDocument` méthode.

1. Définissez les options d’exécution.

   * Créez un `AssemblerOptionSpec` objet qui stocke les options d’exécution à l’aide de son constructeur.
   * Définissez des options d’exécution pour répondre aux besoins de votre entreprise en appelant une méthode qui appartient à l’ `AssemblerOptionSpec` objet. Par exemple, pour demander au service Assembler de continuer à traiter une tâche en cas d’erreur, appelez la `AssemblerOptionSpec` méthode de l’ `setFailOnError` objet et passez `false`.

1. Chiffrez le document.

   Appelez la méthode `AssemblerServiceClient` de l’ `invokeOneDocument` objet et transmettez les valeurs suivantes :

   * Objet `com.adobe.idp.Document` représentant le document DDX. Assurez-vous que ce document DDX contient la valeur `inDoc` de l’élément source PDF.
   * Objet `com.adobe.idp.Document` contenant le document PDF non sécurisé.
   * Objet `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` spécifiant les options d’exécution, y compris la police par défaut et le niveau de journal des tâches.

   La `invokeOneDocument` méthode renvoie un `com.adobe.idp.Document` objet contenant un document PDF chiffré par mot de passe.

1. Enregistrez le document PDF chiffré.

   * Create a `java.io.File` object and ensure that the file name extension is .pdf.
   * Invoke the `Document` object’s `copyToFile` method to copy the contents of the `Document` object to the file. Assurez-vous d’utiliser l’ `Document` objet renvoyé par la `invokeOneDocument` méthode.

**Voir également**

[Début rapide (mode SOAP) : Assemblage d’un document PDF chiffré à l’aide de l’API Java](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-assembling-an-encrypted-pdf-document-using-the-java-api)

## Assemblage d’un document PDF chiffré à l’aide de l’API du service Web {#assemble-an-encrypted-pdf-document-using-the-web-service-api}

1. Incluez des fichiers de projet.

   Créez un projet Microsoft .NET qui utilise MTOM. Assurez-vous d’utiliser la définition WSDL suivante lors de la définition d’une référence de service : `http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Remplacez `localhost` par l’adresse IP du serveur hébergeant les AEM Forms.

1. Créez un client Assembler.

   * Créez un `AssemblerServiceClient` objet en utilisant son constructeur par défaut.
   * Créez un `AssemblerServiceClient.Endpoint.Address` objet en utilisant le `System.ServiceModel.EndpointAddress` constructeur. Transmettez une valeur de chaîne qui spécifie le WSDL au service AEM Forms (par exemple, `http://localhost:8080/soap/services/AssemblerService?blob=mtom`). Vous n’avez pas besoin d’utiliser l’ `lc_version` attribut. Cet attribut est utilisé lorsque vous créez une référence de service.
   * Créez un `System.ServiceModel.BasicHttpBinding` objet en obtenant la valeur du `AssemblerServiceClient.Endpoint.Binding` champ. Convertissez la valeur de retour en `BasicHttpBinding`.
   * Définissez le `System.ServiceModel.BasicHttpBinding` champ de l’ `MessageEncoding` objet sur `WSMessageEncoding.Mtom`. Cette valeur garantit l’utilisation de MTOM.
   * Activez l’authentification HTTP de base en exécutant les tâches suivantes :

      * Attribuez le nom d’utilisateur AEM forms au champ `AssemblerServiceClient.ClientCredentials.UserName.UserName`.
      * Attribuez la valeur de mot de passe correspondante au champ `AssemblerServiceClient.ClientCredentials.UserName.Password`.
      * Attribuez la valeur constante `HttpClientCredentialType.Basic` au champ `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Attribuez la valeur constante `BasicHttpSecurityMode.TransportCredentialOnly` au champ `BasicHttpBindingSecurity.Security.Mode`.

1. Référencez un document DDX existant.

   * Créez un objet `BLOB` en utilisant son constructeur. L’ `BLOB` objet est utilisé pour stocker le document DDX.
   * Créez un `System.IO.FileStream` objet en appelant son constructeur et en transmettant une valeur de chaîne qui représente l’emplacement du fichier du document DDX et le mode d’ouverture du fichier.
   * Créez un tableau d’octets qui stocke le contenu de l’ `System.IO.FileStream` objet. Vous pouvez déterminer la taille du tableau d’octets en obtenant la `System.IO.FileStream` `Length` propriété de l’objet.
   * Renseignez le tableau d’octets avec les données de flux en appelant la `System.IO.FileStream` `Read` méthode de l’objet et en transmettant le tableau d’octets, la position de départ et la longueur du flux à lire.
   * Renseignez l’ `BLOB` objet en affectant son `MTOM` champ au contenu du tableau d’octets.

1. Référencez un document PDF non sécurisé.

   * Créez un objet `BLOB` en utilisant son constructeur. L’ `BLOB` objet est utilisé pour stocker le document PDF d’entrée. Cet `BLOB` objet est transmis à l’ `invokeOneDocument` objet en tant qu’argument.
   * Créez un `System.IO.FileStream` objet en appelant son constructeur et en transmettant une valeur de chaîne qui représente l’emplacement du fichier du document PDF d’entrée et le mode d’ouverture du fichier.
   * Créez un tableau d’octets qui stocke le contenu de l’ `System.IO.FileStream` objet. Vous pouvez déterminer la taille du tableau d’octets en obtenant la `System.IO.FileStream` `Length` propriété de l’objet.
   * Renseignez le tableau d’octets avec les données de flux en appelant la `System.IO.FileStream` `Read` méthode de l’objet et en transmettant le tableau d’octets, la position de départ et la longueur du flux à lire.
   * Renseignez l’ `BLOB` objet en affectant son `MTOM` champ au contenu du tableau d’octets.

1. Définissez les options d’exécution.

   * Créez un `AssemblerOptionSpec` objet qui stocke les options d’exécution à l’aide de son constructeur.
   * Définissez des options d’exécution pour répondre aux besoins de votre entreprise en attribuant une valeur à un membre de données qui appartient à l’ `AssemblerOptionSpec` objet. Par exemple, pour demander au service Assembler de poursuivre le traitement d’une tâche en cas d’erreur, affectez-lui `false` le membre `AssemblerOptionSpec` de données de l’ `failOnError` objet.

1. Chiffrez le document.

   Appelez la méthode `AssemblerServiceClient` de l’ `invokeOneDocument` objet et transmettez les valeurs suivantes :

   * Objet `BLOB` représentant le document DDX
   * A `BLOB` object that represents the unsecured PDF document
   * Objet `AssemblerOptionSpec` spécifiant les options d’exécution

   La `invokeOneDocument` méthode renvoie un `BLOB` objet contenant un document PDF chiffré.

1. Enregistrez le document PDF chiffré.

   * Créez un `System.IO.FileStream` objet en appelant son constructeur et en transmettant une valeur de chaîne qui représente l’emplacement du fichier du document PDF chiffré et le mode d’ouverture du fichier.
   * Créez un tableau d’octets qui stocke le contenu de l’ `BLOB` objet renvoyé par la `invokeOneDocument` méthode. Renseignez le tableau d’octets en obtenant la valeur du membre `BLOB` de données de l’ `MTOM` objet.
   * Create a `System.IO.BinaryWriter` object by invoking its constructor and passing the `System.IO.FileStream` object.
   * Ecrivez le contenu du tableau d’octets dans un fichier PDF en appelant la méthode `System.IO.BinaryWriter` `Write` de l’objet et en transmettant le tableau d’octets.

**Voir également**

[Appel de AEM Forms à l’aide de MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
