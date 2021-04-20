---
title: Assemblage de Documents PDF non interactifs
seo-title: Assemblage de Documents PDF non interactifs
description: Utilisez un formulaire PDF non interactif comme entrée pour assembler un document PDF non interactif à l’aide de l’API Java et de l’API de service Web.
seo-description: Utilisez un formulaire PDF non interactif comme entrée pour assembler un document PDF non interactif à l’aide de l’API Java et de l’API de service Web.
uuid: 0c7adeb4-9a3a-4ec5-ba33-c3642928d4ea
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 8a75c201-bd88-4809-be08-69de94656489
role: Developer
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '1801'
ht-degree: 2%

---


# Assemblage de Documents PDF non interactifs {#assembling-non-interactive-pdf-documents}

Vous pouvez assembler un document PDF non interactif lorsque vous utilisez un formulaire PDF interactif comme entrée. En d’autres termes, supposons que vous disposez d’un formulaire que les utilisateurs peuvent utiliser pour entrer des données dans ses champs. Vous pouvez transmettre ce formulaire au service Assembler, ce qui entraîne le renvoi par le service Assembler d’un document PDF qui empêche les utilisateurs de saisir des données dans ses champs. Ce document est un formulaire PDF non interactif. Par exemple, l’illustration suivante montre une demande de prêt immobilier qui représente un formulaire interactif.

Aux fins de cette discussion, supposons que le document DDX suivant soit utilisé.

```xml
 <?xml version="1.0" encoding="UTF-8"?>
 <DDX xmlns="https://ns.adobe.com/DDX/1.0/">
      <PDF result="out.pdf">
        <PDF source="inDoc"/>
        <NoXFA/>
      </PDF>
 </DDX>
```

Dans ce document DDX, notez que la valeur `inDoc` est affectée à l’attribut source. Dans les cas où un seul document PDF d’entrée est transmis au service Assembler et où un document PDF est renvoyé et où vous appelez l’opération `invokeOneDocument`, affectez la valeur `inDoc` à l’attribut source PDF. Lors de l’appel de l’opération `invokeOneDocument`, la valeur `inDoc` est une clé prédéfinie qui doit être spécifiée dans le document DDX.

En revanche, lorsque vous transmettez deux ou plusieurs documents PDF d’entrée au service Assembler, vous pouvez appeler l’opération `invokeDDX`. Dans ce cas, attribuez le nom de fichier du document PDF d’entrée à l’attribut `source`.

Ce document DDX contient l’élément `NoXFA` qui demande au service Assembler de renvoyer un document PDF non interactif.

Le service Assembler peut assembler des documents PDF non interactifs sans que le service Output ne fasse partie de votre installation AEM forms si le document PDF d’entrée est basé sur un formulaire Acrobat ou un formulaire XFA statique. Cependant, si le document PDF d’entrée est un formulaire XFA dynamique, le service Output doit faire partie de votre installation AEM forms. Si le service Output ne fait pas partie de votre installation AEM forms lors de l’assemblage d’un formulaire XFA dynamique, une exception est générée. Voir [Création de flux de sortie de Document](/help/forms/developing/creating-document-output-streams.md).

>[!NOTE]
>
>Avant de lire cette section, il est recommandé de se familiariser avec l’assemblage de documents PDF à l’aide du service Assembler. Cette section ne traite pas des concepts, tels que la création d’un objet de collection contenant des documents d’entrée ou l’apprentissage de l’extraction des résultats à partir de l’objet de collection renvoyé. (Voir [Assemblage par programmation de Documents PDF](/help/forms/developing/programmatically-assembling-pdf-documents.md).)

>[!NOTE]
>
>Pour plus d’informations sur le service Assembler, voir [Guide de référence des services pour AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

>[!NOTE]
>
>Pour plus d’informations sur un document DDX, voir [Service Assembler et Référence DDX](https://www.adobe.com/go/learn_aemforms_ddx_63).

## Résumé des étapes {#summary-of-steps}

Pour assembler un document PDF non interactif, effectuez les tâches suivantes :

1. Incluez des fichiers de projet.
1. Créez un client PDF Assembler.
1. Référencez un document DDX existant.
1. Référencez un document PDF interactif.
1. Définissez les options d’exécution.
1. Assemblage du document PDF.
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

**Référencer un document DDX existant**

Un document DDX doit être référencé pour assembler un document PDF. Ce document DDX doit contenir l’élément `NoXFA`, qui demande au service Assembler de renvoyer un document PDF non interactif.

**Référence à un document PDF interactif**

Un document PDF interactif doit être référencé et transmis au service Assembler pour récupérer un document PDF non interactif.

**Définition des options d’exécution**

Vous pouvez définir des options d’exécution qui contrôlent le comportement du service Assembler lorsqu’il effectue une tâche. Par exemple, vous pouvez définir une option qui indique au service Assembler de continuer à traiter une tâche en cas d’erreur.

**Assemblage du document PDF**

Après avoir créé le client de service Assembler, référencé le document DDX, référencé un document PDF interactif et défini les options d’exécution, vous pouvez appeler l’opération `invokeOneDocument`. Comme un seul document PDF d’entrée est transmis au service Assembler et qu’un seul document est renvoyé, vous pouvez utiliser l’opération `invokeOneDocument` plutôt que l’opération `invokeDDX`.

**Enregistrer le document PDF non interactif**

Si un seul document PDF est transmis au service Assembler, le service Assembler renvoie un seul document au lieu d’un objet de collection. En d’autres termes, lors de l’appel de l’opération `invokeOneDocument`, un seul document est renvoyé. Comme le document DDX référencé dans cette section contient des instructions pour créer un document PDF non interactif, le service Assembler renvoie un document PDF non interactif qui peut être enregistré en tant que fichier PDF.

**Voir également**

[Inclusion des fichiers de bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Assemblage par programmation de Documents PDF](/help/forms/developing/programmatically-assembling-pdf-documents.md)

## Assemblage d’un document PDF non interactif à l’aide de l’API Java {#assemble-a-non-interactive-pdf-document-using-the-java-api}

Assemblage d’un document PDF non interactif à l’aide de l’API du service Assembler (Java) :

1. Incluez des fichiers de projet.

   Incluez des fichiers JAR client, tels que adobe-assembler-client.jar, dans le chemin de classe de votre projet Java.

1. Créez un client Assembler.

   * Créez un objet `ServiceClientFactory` qui contient des propriétés de connexion.
   * Créez un objet `AssemblerServiceClient` en utilisant son constructeur et en transmettant l&#39;objet `ServiceClientFactory`.

1. Référencez un document DDX existant.

   * Créez un objet `java.io.FileInputStream` qui représente le document DDX en utilisant son constructeur et en transmettant une valeur de chaîne qui spécifie l’emplacement du fichier DDX.
   * Créez un objet `com.adobe.idp.Document` en utilisant son constructeur et en transmettant l’objet `java.io.FileInputStream`. 

1. Référencez un document PDF interactif.

   * Créez un objet `java.io.FileInputStream` en utilisant son constructeur et en transmettant l’emplacement d’un document PDF interactif.
   * Créez un objet `com.adobe.idp.Document` et transmettez l’objet `java.io.FileInputStream` contenant le document PDF. Cet objet `com.adobe.idp.Document` est transmis à la méthode `invokeOneDocument`.

1. Définissez les options d’exécution.

   * Créez un objet `AssemblerOptionSpec` qui stocke les options d’exécution à l’aide de son constructeur.
   * Définissez des options d&#39;exécution pour répondre aux besoins de votre entreprise en appelant une méthode appartenant à l&#39;objet `AssemblerOptionSpec`. Par exemple, pour demander au service Assembler de continuer à traiter une tâche en cas d’erreur, appelez la méthode `AssemblerOptionSpec` de l’objet `setFailOnError` et transmettez `false`.

1. Assemblage du document PDF.

   Appelez la méthode `invokeOneDocument` de l’objet `AssemblerServiceClient` et transmettez les valeurs suivantes :

   * Objet `com.adobe.idp.Document` représentant le document DDX. Assurez-vous que ce document DDX contient la valeur `inDoc` de l’élément source PDF.
   * Objet `com.adobe.idp.Document` contenant le document PDF interactif.
   * Objet `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` qui spécifie les options d’exécution, y compris la police par défaut et le niveau de journal de tâches.

   La méthode `invokeOneDocument` renvoie un objet `com.adobe.idp.Document` contenant un document PDF non interactif.

1. Enregistrez le document PDF non interactif.

   * Créez un objet `java.io.File` et assurez-vous que l’extension de nom de fichier est .pdf.
   * Appelez la méthode `Document` de l&#39;objet `copyToFile` pour copier le contenu de l&#39;objet `Document` dans le fichier. Assurez-vous d’utiliser l’objet `Document` renvoyé par la méthode `invokeOneDocument`.

* &quot;Début rapide (mode SOAP) : Assemblage d’un document PDF non interactif à l’aide de l’API Java&quot;

## Assemblage d’un document PDF non interactif à l’aide de l’API du service Web {#assemble-a-non-interactive-pdf-document-using-the-web-service-api}

Assemblage d’un document PDF non interactif à l’aide de l’API Assembler Service (service Web) :

1. Incluez des fichiers de projet.

   Créez un projet Microsoft .NET qui utilise MTOM. Assurez-vous d’utiliser la définition WSDL suivante : `http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Remplacez `localhost` par l’adresse IP du serveur hébergeant AEM Forms.

1. Créez un client Assembler.

   * Créez un objet `AssemblerServiceClient` en utilisant son constructeur par défaut.
   * Créez un objet `AssemblerServiceClient.Endpoint.Address` en utilisant le constructeur `System.ServiceModel.EndpointAddress`. Transmettez une valeur de chaîne qui spécifie le WSDL au service AEM Forms (par exemple, `http://localhost:8080/soap/services/AssemblerService?blob=mtom`). Vous n&#39;avez pas besoin d&#39;utiliser l&#39;attribut `lc_version`. Cet attribut est utilisé lorsque vous créez une référence de service.
   * Créez un objet `System.ServiceModel.BasicHttpBinding` en obtenant la valeur du champ `AssemblerServiceClient.Endpoint.Binding`. Convertissez la valeur de retour en `BasicHttpBinding`.
   * Définissez le champ `MessageEncoding` de l’objet `System.ServiceModel.BasicHttpBinding` sur `WSMessageEncoding.Mtom`. Cette valeur garantit l’utilisation de MTOM.
   * Activez l’authentification HTTP de base en exécutant les tâches suivantes :

      * Attribuez le nom d’utilisateur AEM forms au champ `AssemblerServiceClient.ClientCredentials.UserName.UserName`.
      * Attribuez la valeur de mot de passe correspondante au champ `AssemblerServiceClient.ClientCredentials.UserName.Password`.
      * Affectez la valeur constante `HttpClientCredentialType.Basic` au champ `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Affectez la valeur constante `BasicHttpSecurityMode.TransportCredentialOnly` au champ `BasicHttpBindingSecurity.Security.Mode`.

1. Référencez un document DDX existant.

   * Créez un objet `BLOB` en utilisant son constructeur. L’objet `BLOB` est utilisé pour stocker le document DDX.
   * Créez un objet `System.IO.FileStream` en appelant son constructeur et en transmettant une valeur de chaîne qui représente l’emplacement du fichier du document DDX et le mode d’ouverture du fichier.
   * Créez un tableau d’octets qui stocke le contenu de l’objet `System.IO.FileStream`. Vous pouvez déterminer la taille du tableau d’octets en obtenant la propriété `System.IO.FileStream` de l’objet `Length`.
   * Renseignez le tableau d’octets avec les données de flux en appelant la méthode `System.IO.FileStream` de l’objet `Read`. Passez le tableau d’octets, la position de départ et la longueur du flux à lire.
   * Renseignez l’objet `BLOB` en attribuant son champ `MTOM` au contenu du tableau d’octets.

1. Référencez un document PDF interactif.

   * Créez un objet `BLOB` en utilisant son constructeur. L’objet `BLOB` est utilisé pour stocker le document PDF d’entrée. Cet objet `BLOB` est transmis à `invokeOneDocument` en tant qu&#39;argument.
   * Créez un objet `System.IO.FileStream` en appelant son constructeur et en transmettant une valeur de chaîne qui représente l’emplacement du fichier du document PDF d’entrée et le mode d’ouverture du fichier.
   * Créez un tableau d’octets qui stocke le contenu de l’objet `System.IO.FileStream`. Vous pouvez déterminer la taille du tableau d’octets en obtenant la propriété `System.IO.FileStream` de l’objet `Length`.
   * Renseignez le tableau d’octets avec les données de flux en appelant la méthode `System.IO.FileStream` de l’objet `Read`. Passez le tableau d’octets, la position de départ et la longueur du flux à lire.
   * Renseignez l’objet `BLOB` en attribuant son champ `MTOM` au contenu du tableau d’octets.

1. Définissez les options d’exécution.

   * Créez un objet `AssemblerOptionSpec` qui stocke les options d’exécution à l’aide de son constructeur.
   * Définissez des options d&#39;exécution pour répondre aux besoins de votre entreprise en attribuant une valeur à un membre de données qui appartient à l&#39;objet `AssemblerOptionSpec`. Par exemple, pour demander au service Assembler de continuer à traiter une tâche en cas d’erreur, affectez `false` au membre de données `failOnError` de l’objet `AssemblerOptionSpec`.

1. Assemblage du document PDF.

   Appelez la méthode `invokeOneDocument` de l’objet `AssemblerServiceClient` et transmettez les valeurs suivantes :

   * Un objet `BLOB` qui représente le document DDX
   * Objet `BLOB` représentant le document PDF interactif
   * Objet `AssemblerOptionSpec` qui spécifie les options d’exécution

   La méthode `invokeOneDocument` renvoie un objet `BLOB` contenant un document PDF non interactif.

1. Enregistrez le document PDF non interactif.

   * Créez un objet `System.IO.FileStream` en appelant son constructeur et en transmettant une valeur de chaîne qui représente l’emplacement du fichier du document PDF non interactif et le mode d’ouverture du fichier.
   * Créez un tableau d’octets qui stocke le contenu de l’objet `BLOB` renvoyé par la méthode `invokeOneDocument`. Renseignez le tableau d’octets en obtenant la valeur du champ `BLOB` de l’objet `MTOM`.
   * Créez un objet `System.IO.BinaryWriter` en appelant son constructeur et en transmettant l&#39;objet `System.IO.FileStream`.
   * Ecrivez le contenu du tableau d’octets dans un fichier PDF en appelant la méthode `System.IO.BinaryWriter` de l’objet `Write` et en transmettant le tableau d’octets.

* &quot;Début rapide (MTOM) : Assemblage d’un document PDF non interactif à l’aide de l’API du service Web&quot;.

**Voir également**

[Appel de AEM Forms à l’aide de MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
