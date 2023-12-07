---
title: Assembler des documents PDF non interactifs
description: Utilisez un formulaire PDF non interactif comme entrée pour assembler un document PDF non interactif à l’aide de l’API Java et de l’API de service web.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
role: Developer
exl-id: 4677b9e5-3811-4de3-b4f4-9574b5898486
source-git-commit: 8b4cb4065ec14e813b49fb0d577c372790c9b21a
workflow-type: tm+mt
source-wordcount: '1763'
ht-degree: 88%

---

# Assembler des documents PDF non interactifs {#assembling-non-interactive-pdf-documents}

Vous pouvez assembler un document PDF non interactif lorsque vous utilisez un formulaire PDF interactif en tant quʼentrée. Prenons lʼexemple suivant : vous disposez dʼun formulaire que les utilisateurs peuvent utiliser pour saisir des données dans ses champs. Vous pouvez transmettre ce formulaire au service Assembler. Ce dernier renvoie alors un document PDF qui empêche les utilisateurs de saisir des données dans ses champs. Ce document est un formulaire PDF non interactif. L’illustration suivante est un exemple de prêt immobilier, sous la forme dʼun formulaire interactif.

Dans le cadre de cette discussion, supposons que le document DDX suivant soit utilisé.

```xml
 <?xml version="1.0" encoding="UTF-8"?>
 <DDX xmlns="https://ns.adobe.com/DDX/1.0/">
      <PDF result="out.pdf">
        <PDF source="inDoc"/>
        <NoXFA/>
      </PDF>
 </DDX>
```

Dans ce document DDX, remarquez que la valeur `inDoc` est attribuée à lʼattribut source. Dans les cas où un seul document PDF d’entrée est transmis au service Assembler et un seul document PDF est renvoyé, et que vous appelez lʼopération `invokeOneDocument`, attribuez la valeur `inDoc` à l’attribut source du PDF. Lors de l’appel de lʼopération `invokeOneDocument`, la valeur `inDoc` est une clé prédéfinie qui doit être spécifiée dans le document DDX.

En revanche, lors de la transmission de plusieurs documents PDF d’entrée au service Assembler, vous pouvez appeler lʼopération `invokeDDX`. Dans cette situation, attribuez le nom du fichier du document PDF d’entrée à lʼattribut `source`.

Ce document DDX contient lʼélément `NoXFA`, qui indique au service Assembler de renvoyer un document PDF non interactif.

Le service Assembler peut assembler des documents PDF non interactifs sans que le service Output fasse partie de votre installation AEM Forms si le documentu PDF d’entrée est basé sur un formulaire Acrobat ou un formulaire XFA statique. Cependant, si le document PDF d’entrée est un formulaire XFA dynamique, le service Output doit faire partie de votre installation AEM Forms. Si le service Output ne fait pas partie de votre installation AEM Forms lorsquʼun formulaire XFA dynamique est assemblé, une exception est générée. Consultez la section [Créer des flux de sortie pour les documents](/help/forms/developing/creating-document-output-streams.md).

>[!NOTE]
>
>Avant de lire cette section, il est recommandé de vous familiariser avec l’assemblage de documents PDF à l’aide du service Assembler. Cette section nʼaborde pas les concepts tels que la création dʼun objet de collection contenant des documents dʼentrée, ou lʼapprentissage de lʼextraction des résultats de lʼobjet de collection retourné. (Consultez la section [Assembler par programmation des documents PDF](/help/forms/developing/programmatically-assembling-pdf-documents.md)).

>[!NOTE]
>
>Pour plus d’informations sur le service Assembler, consultez la section [Guide de référence des services pour AEM Forms](https://help.adobe.com/fr_FR/livecycle/11.0/Services/index.html).

>[!NOTE]
>
>Pour plus d’informations sur les documents DDX, consultez la section [Guide de référence du service Assembler et de DDX](https://www.adobe.com/go/learn_aemforms_ddx_63).

## Résumé des étapes {#summary-of-steps}

Pour assembler un document PDF non interactif, procédez comme suit :

1. Incluez les fichiers de projet.
1. Créez un client Assembler PDF.
1. Référencez un document DX existant.
1. Référencez un document PDF interactif.
1. Définissez les options d’exécution.
1. Assemblez le document PDF.
1. Enregistrez le document PDF non interactif.

**Inclure les fichiers de projet**

Incluez les fichiers nécessaires dans votre projet de développement. Si vous créez une application cliente à l’aide de Java, incluez les fichiers JAR nécessaires. Si vous utilisez des services Web, veillez à inclure les fichiers proxy.

Les fichiers JAR suivants doivent être ajoutés au chemin de classe de votre projet :

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-assembler-client.jar
* adobe-utility.jar (obligatoire si AEM Forms est déployé sur JBoss)
* jbossall-client.jar (obligatoire si AEM Forms est déployé sur JBoss)

si AEM Forms est déployé sur un serveur d’applications J2EE pris en charge autre que JBoss, vous devez remplacer les fichiers adobe-utility.jar et jbossall-client.jar par des fichiers JAR spécifiques au serveur d’applications J2EE sur lequel AEM Forms est déployé.

**Créer un client Assembler**

Avant de pouvoir effectuer une opération Assembler de manière programmée, vous devez créer un client de service Assembler.

**Référencer un document DDX existant**

Un document DDX doit être référencé pour assembler un document PDF. Ce document DDX doit contenir lʼélément `NoXFA`, qui indique au service Assembler de renvoyer un document PDF non interactif.

**Référencer un document PDF interactif**

Un document PDF interactif doit être référencé et transmis au service Assembler pour obtenir en retour un document PDF non interactif.

**Définir les options d’exécution**

Vous pouvez définir des options d’exécution qui contrôlent le comportement du service Assembler lors de l’exécution d’une tâche. Par exemple, vous pouvez définir une option qui indique au service Assembler de continuer à traiter une tâche en cas d’erreur.

**Assembler le document PDF**

Une fois que vous avez créé le client du service Assembler, référencé le document DDX ainsi quʼun document PDF interactif et défini les options d’exécution, vous pouvez appeler lʼopération `invokeOneDocument`. Comme un seul document PDF d’entrée est transmis au service Assembler et qu’un seul document est renvoyé, vous pouvez utiliser lʼopération `invokeOneDocument`, au lieu de lʼopération `invokeDDX`.

**Enregistrer le document PDF non interactif**

Si un seul document PDF est transmis au service Assembler, il renvoie un seul document au lieu d’un objet de collection. Autrement dit, lors de l’appel de lʼopération `invokeOneDocument`, un seul document est renvoyé. Comme le document DDX référencé dans cette section contient des instructions pour créer un document PDF non interactif, le service Assembler renvoie un document PDF non interactif, qui peut être enregistré au format PDF.

**Voir également**

[Inclusion des fichiers de bibliothèque Java d’AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Assembler les documents PDF par programmation](/help/forms/developing/programmatically-assembling-pdf-documents.md)

## Assembler un document PDF non interactif à l’aide de l’API Java {#assemble-a-non-interactive-pdf-document-using-the-java-api}

Assemblez un document PDF non interactif à l’aide de l’API du service Assembler (Java) :

1. Incluez les fichiers de projet.

   Incluez les fichiers JAR client, tels que adobe-assembler-client.jar, dans le chemin de classe de votre projet Java.

1. Créez un client Assembler.

   * Créez un objet `ServiceClientFactory` qui contient des propriétés de connexion.
   * Créez un objet `AssemblerServiceClient` en utilisant son constructeur et en transmettant l’objet `ServiceClientFactory`.

1. Référencez un document DX existant.

   * Créez un objet `java.io.FileInputStream` qui représente le document DDX en utilisant son constructeur et en transmettant une valeur de chaîne qui spécifie l’emplacement du fichier DDX.
   * Créez un objet `com.adobe.idp.Document` en utilisant son constructeur et en transmettant l’objet `java.io.FileInputStream`. 

1. Référencez un document PDF interactif.

   * Créez un objet `java.io.FileInputStream` en utilisant son constructeur et en transmettant l’emplacement d’un document PDF interactif.
   * Créez un objet `com.adobe.idp.Document` et transmettez l’objet `java.io.FileInputStream` qui contient le document PDF. Cet objet `com.adobe.idp.Document` est transmis à la méthode `invokeOneDocument`.

1. Définissez les options d’exécution.

   * Créez un objet `AssemblerOptionSpec` qui stocke les options d’exécution en utilisant son constructeur.
   * Définissez les options d’exécution pour répondre à vos exigences professionnelles en appelant une méthode appartenant à l’objet `AssemblerOptionSpec`. Par exemple, pour demander au service Assembler de continuer à traiter une tâche en cas d’erreur, appelez la fonction `AssemblerOptionSpec` de `setFailOnError` méthode et transmission `false`.

1. Assemblez le document PDF.

   Appeler la variable `AssemblerServiceClient` de `invokeOneDocument` et transmettez les valeurs suivantes :

   * Objet `com.adobe.idp.Document` représentant le document DDX. Assurez-vous que ce document DDX contient la valeur `inDoc` pour l’élément de source PDF.
   * Objet `com.adobe.idp.Document` contenant le document PDF interactif.
   * Objet `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` spécifiant les options d’exécution, y compris la police par défaut et le niveau du log de traitement.

   La méthode `invokeOneDocument` renvoie un objet `com.adobe.idp.Document` contenant un document PDF non interactif.

1. Enregistrez le document PDF non interactif.

   * Créez un objet `java.io.File` et assurez-vous que l’extension du nom du fichier est .pdf.
   * Appeler la variable `Document` de `copyToFile` pour copier le contenu de la méthode `Document` vers le fichier . Veillez à utiliser l’objet `Document` renvoyé par la méthode `invokeOneDocument`.

* « Démarrage rapide (mode SOAP) : assembler un document PDF non interactif à l’aide de l’API Java. »

## Assembler un document PDF non interactif à l’aide de l’API Web Service {#assemble-a-non-interactive-pdf-document-using-the-web-service-api}

Assemblez un document PDF non interactif en utilisant l’API du Service Assembler (Web Service) :

1. Incluez les fichiers de projet.

   Créez un projet Microsoft .NET qui utilise MTOM. Veillez à utiliser la définition WSDL suivante : `http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Remplacez `localhost` par l’adresse IP du serveur hébergeant AEM Forms.

1. Créez un client Assembler.

   * Créez un objet `AssemblerServiceClient` en utilisant son constructeur par défaut.
   * Créez un objet `AssemblerServiceClient.Endpoint.Address` en utilisant le constructeur `System.ServiceModel.EndpointAddress`. Transmettez une valeur de chaîne qui spécifie le WSDL au service AEM Forms (par exemple, `http://localhost:8080/soap/services/AssemblerService?blob=mtom`). Vous n’avez pas besoin d’utiliser l’attribut `lc_version`. Cet attribut est utilisé lorsque vous créez une référence de service.
   * Créez un objet `System.ServiceModel.BasicHttpBinding` en récupérant la valeur du champ `AssemblerServiceClient.Endpoint.Binding`. Convertissez la valeur de retour en `BasicHttpBinding`.
   * Définissez la variable `System.ServiceModel.BasicHttpBinding` de `MessageEncoding` champ à `WSMessageEncoding.Mtom`. Cette valeur garantit l’utilisation de MTOM.
   * Activez l’authentification HTTP de base en effectuant les tâches suivantes :

      * Attribuez le nom d’utilisateur AEM forms au champ `AssemblerServiceClient.ClientCredentials.UserName.UserName`.
      * Attribuez la valeur de mot de passe correspondante au champ `AssemblerServiceClient.ClientCredentials.UserName.Password`.
      * Attribuez la valeur constante `HttpClientCredentialType.Basic` au champ `BasicHttpBindingSecurity.Transport.ClientCredentialType`.
      * Attribuez la valeur constante `BasicHttpSecurityMode.TransportCredentialOnly` au champ `BasicHttpBindingSecurity.Security.Mode`.

1. Référencez un document DX existant.

   * Créez un objet `BLOB` en utilisant son constructeur. L’objet `BLOB` sert à stocker le document DDX.
   * Créez un objet `System.IO.FileStream` en appelant son constructeur et en transmettant une valeur de chaîne qui représente l’emplacement du fichier du document DDX et le mode d’ouverture du fichier.
   * Créez un tableau d’octets qui stocke le contenu de l’objet `System.IO.FileStream`. Vous pouvez déterminer la taille du tableau d’octets en obtenant la variable `System.IO.FileStream` de `Length` .
   * Renseignez le tableau d’octets avec les données de diffusion en appelant la variable `System.IO.FileStream` de `Read` . Transmettez le tableau d’octets, la position de départ et la longueur du flux à lire.
   * Renseignez l’objet `BLOB` en attribuant à son champ `MTOM` le contenu du tableau d’octets.

1. Référencez un document PDF interactif.

   * Créez un objet `BLOB` en utilisant son constructeur. L’objet `BLOB` sert à stocker le document PDF d’entrée. Cet objet `BLOB` est transmis à `invokeOneDocument` comme argument.
   * Créez un objet `System.IO.FileStream` en appelant son constructeur et en transmettant une valeur de chaîne qui représente l’emplacement du fichier PDF d’entrée et le mode d’ouverture du fichier.
   * Créez un tableau d’octets qui stocke le contenu de l’objet `System.IO.FileStream`. Vous pouvez déterminer la taille du tableau d’octets en obtenant la variable `System.IO.FileStream` de `Length` .
   * Renseignez le tableau d’octets avec les données de diffusion en appelant la variable `System.IO.FileStream` de `Read` . Transmettez le tableau d’octets, la position de départ et la longueur du flux à lire.
   * Renseignez l’objet `BLOB` en affectant à son champ `MTOM` le contenu du tableau d’octets.

1. Définissez les options d’exécution.

   * Créez un objet `AssemblerOptionSpec` qui stocke les options d’exécution en utilisant son constructeur.
   * Définissez les options d’exécution pour répondre à vos exigences professionnelles en attribuant une valeur à un membre de données qui appartient à l’objet `AssemblerOptionSpec`. Par exemple, pour demander au service Assembler de continuer à traiter une tâche en cas d’erreur, affectez `false` à la fonction `AssemblerOptionSpec` de `failOnError` membre de données.

1. Assemblez le document PDF.

   Appeler la variable `AssemblerServiceClient` de `invokeOneDocument` et transmettez les valeurs suivantes :

   * Objet `BLOB` représentant le document DDX.
   * Un objet `BLOB` qui représente le document PDF interactif.
   * Un objet `AssemblerOptionSpec` qui spécifie les options d’exécution.

   La méthode `invokeOneDocument` renvoie un objet `BLOB` qui contient un document PDF non interactif.

1. Enregistrez le document PDF non interactif.

   * Créez un objet `System.IO.FileStream` en appelant son constructeur et en transmettant une valeur de chaîne qui représente l’emplacement du fichier PDF non interactif et son mode d’ouverture.
   * Créez un tableau d’octets qui stocke le contenu de l’objet `BLOB` renvoyé par la méthode `invokeOneDocument`. Renseignez le tableau d’octets en obtenant la valeur de la variable `BLOB` de `MTOM` champ .
   * Créez un objet `System.IO.BinaryWriter` en utilisant son constructeur et en transmettant l’objet `System.IO.FileStream`.
   * Ecrivez le contenu du tableau d’octets dans un fichier de PDF en appelant la méthode `System.IO.BinaryWriter` de `Write` et transmission du tableau d’octets.

* « Démarrage rapide (MTOM) : assembler un document PDF non interactif à l’aide de l’API de service web. ».

**Voir également**

[Appeler AEM Forms en utilisant MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
