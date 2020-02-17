---
title: Assemblage de documents PDF non interactifs
seo-title: Assemblage de documents PDF non interactifs
description: 'null'
seo-description: 'null'
uuid: 0c7adeb4-9a3a-4ec5-ba33-c3642928d4ea
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 8a75c201-bd88-4809-be08-69de94656489
translation-type: tm+mt
source-git-commit: a3c303d4e3a85e1b2e794bec2006c335056309fb

---


# Assemblage de documents PDF non interactifs {#assembling-non-interactive-pdf-documents}

Vous pouvez assembler un document PDF non interactif lorsque vous utilisez un formulaire PDF interactif comme entrée. En d’autres termes, supposons que vous disposez d’un formulaire que les utilisateurs peuvent utiliser pour entrer des données dans ses champs. Vous pouvez transmettre ce formulaire au service Assembler, de sorte que le service Assembler renvoie un document PDF qui empêche les utilisateurs de saisir des données dans ses champs. Ce document est un formulaire PDF non interactif. Par exemple, l’illustration suivante montre une demande de prêt immobilier qui représente un formulaire interactif.

Aux fins de cette discussion, supposons que le document DDX suivant soit utilisé.

```as3
 <?xml version="1.0" encoding="UTF-8"?>
 <DDX xmlns="https://ns.adobe.com/DDX/1.0/">
      <PDF result="out.pdf">
        <PDF source="inDoc"/>
        <NoXFA/>
      </PDF>
 </DDX>
```

Dans ce document DDX, notez que la valeur est affectée à l’attribut source `inDoc`. Dans les cas où un seul document PDF d’entrée est transmis au service Assembler et où un seul document PDF est renvoyé, et où vous appelez l’ `invokeOneDocument` opération, affectez la valeur `inDoc` à l’attribut source PDF. Lors de l’appel de l’ `invokeOneDocument` opération, la `inDoc` valeur est une clé prédéfinie qui doit être spécifiée dans le document DDX.

En revanche, lorsque vous transmettez deux documents PDF d’entrée ou plus au service Assembler, vous pouvez appeler l’ `invokeDDX` opération. Dans ce cas, attribuez le nom de fichier du document PDF d’entrée à l’ `source` attribut.

Ce document DDX contient l’ `NoXFA` élément, qui demande au service Assembler de renvoyer un document PDF non interactif.

Le service Assembler peut assembler des documents PDF non interactifs sans que le service Output fasse partie de votre installation AEM forms si le document PDF d’entrée est basé sur un formulaire Acrobat ou un formulaire XFA statique. Cependant, si le document PDF d’entrée est un formulaire XFA dynamique, le service Output doit faire partie de votre installation AEM forms. Si le service Output ne fait pas partie de votre installation AEM forms lors de l’assemblage d’un formulaire XFA dynamique, une exception est générée. Voir [Création de flux](/help/forms/developing/creating-document-output-streams.md)de sortie de document.

>[!NOTE]
>
>Avant de lire cette section, il est recommandé de vous familiariser avec l’assemblage de documents PDF à l’aide du service Assembler. Cette section ne traite pas des concepts, tels que la création d’un objet de collection contenant des documents d’entrée ou l’apprentissage de l’extraction des résultats de l’objet de collection renvoyé. (Voir Assemblage [programmatique de documents](/help/forms/developing/programmatically-assembling-pdf-documents.md)PDF.)

>[!NOTE]
>
>For more information about the Assembler service, see [Services Reference for AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

>[!NOTE]
>
>Pour plus d’informations sur un document DDX, voir [Assembler Service et Référence](https://www.adobe.com/go/learn_aemforms_ddx_63)DDX.

## Résumé des étapes {#summary-of-steps}

Pour assembler un document PDF non interactif, procédez comme suit :

1. Incluez des fichiers de projet.
1. Créez un client PDF Assembler.
1. Référencez un document DDX existant.
1. Référencez un document PDF interactif.
1. Définissez les options d’exécution.
1. Assemblez le document PDF.
1. Enregistrez le document PDF non interactif.

**Inclure les fichiers de projet**

Incluez les fichiers nécessaires dans votre projet de développement. Si vous créez une application cliente à l’aide de Java, incluez les fichiers JAR nécessaires. Si vous utilisez des services Web, veillez à inclure les fichiers proxy.

Les fichiers JAR suivants doivent être ajoutés au chemin de classe de votre projet :

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-assembler-client.jar
* adobe-utilities.jar (requis si AEM Forms est déployé sur JBoss)
* jbossall-client.jar (requis si AEM Forms est déployé sur JBoss)

si AEM Forms est déployé sur un serveur d’applications J2EE pris en charge autre que JBoss, vous devez remplacer les fichiers adobe-utilities.jar et jbossall-client.jar par des fichiers JAR spécifiques au serveur d’applications J2EE sur lequel AEM Forms est déployé.

**Création d’un client Assembler**

Avant de pouvoir exécuter une opération Assembler par programmation, vous devez créer un client de service Assembler.

**Référence à un document DDX existant**

Un document DDX doit être référencé pour assembler un document PDF. Ce document DDX doit contenir l’ `NoXFA` élément qui demande au service Assembler de renvoyer un document PDF non interactif.

**Référence à un document PDF interactif**

Un document PDF interactif doit être référencé et transmis au service Assembler pour récupérer un document PDF non interactif.

**Définition des options d’exécution**

Vous pouvez définir des options d’exécution qui contrôlent le comportement du service Assembler lorsqu’il effectue une tâche. Par exemple, vous pouvez définir une option qui indique au service Assembler de poursuivre le traitement d’une tâche en cas d’erreur.

**Assemblage du document PDF**

Après avoir créé le client de service Assembler, référencez le document DDX, référencez un document PDF interactif et définissez les options d’exécution, vous pouvez appeler l’ `invokeOneDocument` opération. Comme un seul document PDF d’entrée est transmis au service Assembler et qu’un seul document est renvoyé, vous pouvez utiliser l’ `invokeOneDocument` opération plutôt que l’ `invokeDDX` opération.

**Enregistrer le document PDF non interactif**

Si un seul document PDF est transmis au service Assembler, le service Assembler renvoie un document unique au lieu d’un objet de collection. En d’autres termes, lors de l’appel de l’ `invokeOneDocument` opération, un seul document est renvoyé. Etant donné que le document DDX référencé dans cette section contient des instructions pour créer un document PDF non interactif, le service Assembler renvoie un document PDF non interactif qui peut être enregistré en tant que fichier PDF.

**Voir également**

[Inclusion des fichiers de bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Assemblage par programmation de documents PDF](/help/forms/developing/programmatically-assembling-pdf-documents.md)

## Assemblage d’un document PDF non interactif à l’aide de l’API Java {#assemble-a-non-interactive-pdf-document-using-the-java-api}

Assemblez un document PDF non interactif à l’aide de l’API du service Assembler (Java) :

1. Incluez des fichiers de projet.

   Incluez des fichiers JAR client, tels que adobe-assembler-client.jar, dans le chemin de classe de votre projet Java.

1. Créez un client Assembler.

   * Créez un objet `ServiceClientFactory` qui contient des propriétés de connexion.
   * Create an `AssemblerServiceClient` object by using its constructor and passing the `ServiceClientFactory` object.

1. Référencez un document DDX existant.

   * Créez un `java.io.FileInputStream` objet qui représente le document DDX en utilisant son constructeur et en transmettant une valeur de chaîne qui spécifie l’emplacement du fichier DDX.
   * Créez un objet `com.adobe.idp.Document` en utilisant son constructeur et en transmettant l’objet `java.io.FileInputStream`. 

1. Référencez un document PDF interactif.

   * Créez un `java.io.FileInputStream` objet en utilisant son constructeur et en transmettant l’emplacement d’un document PDF interactif.
   * Créez un `com.adobe.idp.Document` objet et transmettez l’ `java.io.FileInputStream` objet qui contient le document PDF. Cet `com.adobe.idp.Document` objet est transmis à la `invokeOneDocument` méthode.

1. Définissez les options d’exécution.

   * Créez un `AssemblerOptionSpec` objet qui stocke les options d’exécution à l’aide de son constructeur.
   * Définissez des options d’exécution pour répondre aux besoins de votre entreprise en appelant une méthode qui appartient à l’ `AssemblerOptionSpec` objet. Par exemple, pour demander au service Assembler de poursuivre le traitement d’une tâche en cas d’erreur, appelez la `AssemblerOptionSpec` méthode de l’ `setFailOnError` objet et transmettez-la `false`.

1. Assemblez le document PDF.

   Appelez la méthode `AssemblerServiceClient` `invokeOneDocument` de l’objet et transmettez les valeurs suivantes :

   * Objet `com.adobe.idp.Document` représentant le document DDX. Assurez-vous que ce document DDX contient la valeur `inDoc` de l’élément source PDF.
   * Objet `com.adobe.idp.Document` contenant le document PDF interactif.
   * Objet `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` spécifiant les options d’exécution, notamment la police par défaut et le niveau du journal des tâches.
   La `invokeOneDocument` méthode renvoie un `com.adobe.idp.Document` objet contenant un document PDF non interactif.

1. Enregistrez le document PDF non interactif.

   * Create a `java.io.File` object and ensure that the file name extension is .pdf.
   * Invoke the `Document` object’s `copyToFile` method to copy the contents of the `Document` object to the file. Veillez à utiliser l’ `Document` objet renvoyé par la `invokeOneDocument` méthode.

* &quot;Démarrage rapide (mode SOAP) : Assemblage d’un document PDF non interactif à l’aide de l’API Java&quot;

## Assemblage d’un document PDF non interactif à l’aide de l’API du service Web {#assemble-a-non-interactive-pdf-document-using-the-web-service-api}

Assemblez un document PDF non interactif à l’aide de l’API du service Assembler (service Web) :

1. Incluez des fichiers de projet.

   Créez un projet Microsoft .NET qui utilise MTOM. Veillez à utiliser la définition WSDL suivante : `http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Remplacez `localhost` par l’adresse IP du serveur hébergeant AEM Forms.

1. Créez un client Assembler.

   * Créez un `AssemblerServiceClient` objet à l’aide de son constructeur par défaut.
   * Créez un `AssemblerServiceClient.Endpoint.Address` objet à l’aide du `System.ServiceModel.EndpointAddress` constructeur. Transmettez une valeur de chaîne qui spécifie le WSDL au service AEM Forms (par exemple, `http://localhost:8080/soap/services/AssemblerService?blob=mtom`). Vous n’avez pas besoin d’utiliser l’ `lc_version` attribut. Cet attribut est utilisé lorsque vous créez une référence de service.
   * Créez un `System.ServiceModel.BasicHttpBinding` objet en obtenant la valeur du `AssemblerServiceClient.Endpoint.Binding` champ. Convertissez la valeur de retour en `BasicHttpBinding`.
   * Définissez le `System.ServiceModel.BasicHttpBinding` champ de l’ `MessageEncoding` objet sur `WSMessageEncoding.Mtom`. Cette valeur garantit l’utilisation de MTOM.
   * Activez l’authentification HTTP de base en effectuant les tâches suivantes :

      * Attribuez le nom d’utilisateur d’AEM forms au champ `AssemblerServiceClient.ClientCredentials.UserName.UserName`.
      * Attribuez la valeur de mot de passe correspondante au champ `AssemblerServiceClient.ClientCredentials.UserName.Password`.
      * Attribuez la valeur constante `HttpClientCredentialType.Basic` au champ `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Attribuez la valeur constante `BasicHttpSecurityMode.TransportCredentialOnly` au champ `BasicHttpBindingSecurity.Security.Mode`.

1. Référencez un document DDX existant.

   * Créez un objet `BLOB` en utilisant son constructeur. L’ `BLOB` objet est utilisé pour stocker le document DDX.
   * Créez un `System.IO.FileStream` objet en appelant son constructeur et en transmettant une valeur de chaîne qui représente l’emplacement du fichier du document DDX et le mode d’ouverture du fichier.
   * Créez un tableau d’octets qui stocke le contenu de l’ `System.IO.FileStream` objet. Vous pouvez déterminer la taille du tableau d’octets en obtenant la `System.IO.FileStream` `Length` propriété de l’objet.
   * Renseignez le tableau d’octets avec les données de flux en appelant la `System.IO.FileStream` `Read` méthode de l’objet. Passez le tableau d’octets, la position de départ et la longueur du flux à lire.
   * Renseignez l’ `BLOB` objet en affectant son `MTOM` champ au contenu du tableau d’octets.

1. Référencez un document PDF interactif.

   * Créez un objet `BLOB` en utilisant son constructeur. L’ `BLOB` objet est utilisé pour stocker le document PDF d’entrée. Cet `BLOB` objet est transmis au `invokeOneDocument` en tant qu’argument.
   * Créez un `System.IO.FileStream` objet en appelant son constructeur et en transmettant une valeur de chaîne représentant l’emplacement du fichier PDF d’entrée et le mode d’ouverture du fichier.
   * Créez un tableau d’octets qui stocke le contenu de l’ `System.IO.FileStream` objet. Vous pouvez déterminer la taille du tableau d’octets en obtenant la `System.IO.FileStream` `Length` propriété de l’objet.
   * Renseignez le tableau d’octets avec les données de flux en appelant la `System.IO.FileStream` `Read` méthode de l’objet. Passez le tableau d’octets, la position de départ et la longueur du flux à lire.
   * Renseignez l’ `BLOB` objet en affectant son `MTOM` champ au contenu du tableau d’octets.

1. Définissez les options d’exécution.

   * Créez un `AssemblerOptionSpec` objet qui stocke les options d’exécution à l’aide de son constructeur.
   * Définissez des options d’exécution pour répondre aux besoins de votre entreprise en attribuant une valeur à un membre de données qui appartient à l’ `AssemblerOptionSpec` objet. Par exemple, pour demander au service Assembler de poursuivre le traitement d’une tâche en cas d’erreur, affectez `false` au membre `AssemblerOptionSpec` `failOnError` de données de l’objet.

1. Assemblez le document PDF.

   Appelez la méthode `AssemblerServiceClient` `invokeOneDocument` de l’objet et transmettez les valeurs suivantes :

   * Objet `BLOB` représentant le document DDX
   * A `BLOB` object that represents the interactive PDF document
   * Objet `AssemblerOptionSpec` spécifiant les options d’exécution
   La `invokeOneDocument` méthode renvoie un `BLOB` objet contenant un document PDF non interactif.

1. Enregistrez le document PDF non interactif.

   * Créez un `System.IO.FileStream` objet en appelant son constructeur et en transmettant une valeur de chaîne représentant l’emplacement du fichier PDF non interactif et le mode d’ouverture du fichier.
   * Créez un tableau d’octets qui stocke le contenu de l’ `BLOB` objet renvoyé par la `invokeOneDocument` méthode. Renseignez le tableau d’octets en obtenant la valeur du champ de l’ `BLOB` objet `MTOM` .
   * Create a `System.IO.BinaryWriter` object by invoking its constructor and passing the `System.IO.FileStream` object.
   * Ecrivez le contenu du tableau d’octets dans un fichier PDF en appelant la `System.IO.BinaryWriter` `Write` méthode de l’objet et en transmettant le tableau d’octets.

* &quot;Démarrage rapide (MTOM) : Assemblage d’un document PDF non interactif à l’aide de l’API du service Web&quot;.

**Voir également**

[Appel d’AEM Forms à l’aide de MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
