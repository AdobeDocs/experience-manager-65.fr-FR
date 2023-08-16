---
title: Désassembler des documents PDF par programme
seo-title: Programmatically Disassembling PDF Documents
description: Utilisez le service Assembler pour désassembler un unique document PDF en plusieurs à l’aide de l’API Java et de l’API Web Service.
seo-description: Use the Assembler service to disassemble a single PDF document into multiple PDF documents using the Java API and the Web Service API.
uuid: d71cc044-e948-4b7a-b598-b041723b69e9
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 8e38a597-5d22-4d83-95fe-4494fb04e4a3
role: Developer
exl-id: c5e712e0-5c3f-48cd-91cf-fd347222a6b2
source-git-commit: 10227bcfcfd5a9b0f126fee74dce6ec7842f5e95
workflow-type: tm+mt
source-wordcount: '1761'
ht-degree: 86%

---

# Désassembler des documents PDF par programme {#programmatically-disassembling-pdf-documents}

**Les exemples et les échantillons de ce document sont réservés à l’environnement AEM Forms sur JEE.**

Vous pouvez désassembler un document PDF en le transmettant au service Assembler. Cette tâche est particulièrement utile lorsque le document PDF d’origine a été créé à partir de plusieurs documents séparés, par exemple un ensemble de rapports. Dans l’illustration suivante, DocA est divisé en plusieurs documents générés, où le premier signet de niveau 1 d’une page identifie le début d’un nouveau document généré.

![pd_pd_pdfsfrombookmarks](assets/pd_pd_pdfsfrombookmarks.png)

Pour désassembler un document PDF, assurez-vous que l’élément `PDFsFromBookmarks` se trouve dans le document DDX. L’élément `PDFsFromBookmarks` est un élément généré et ne peut être qu’un élément enfant de l’élément `DDX`. Il ne comporte pas d’attribut `result` car cela peut entraîner la génération de plusieurs documents.

L’élément `PDFsFromBookmarks` entraîne la génération d’un seul document pour chaque signet de niveau 1 dans le document source.

Dans le cadre de cette discussion, supposons que le document DDX suivant soit utilisé.

```xml
 <?xml version="1.0" encoding="UTF-8"?>
 <DDX xmlns="https://ns.adobe.com/DDX/1.0/">
      <PDFsFromBookmarks prefix="stmt">
     <PDF source="AssemblerResultPDF.pdf"/>
 </PDFsFromBookmarks>
 </DDX>
```

>[!NOTE]
>
>Avant de lire cette section, il est recommandé de vous familiariser avec l’assemblage de documents PDF à l’aide du service Assembler. (Voir [Assemblage par programme de documents PDF](/help/forms/developing/programmatically-assembling-pdf-documents.md).)

>[!NOTE]
>
>Lors de la transmission d’un seul document PDF au service Assembler et de la récupération d’un unique document, vous pouvez appeler l’opération `invokeOneDocument`. Toutefois, pour désassembler un document PDF, utilisez l’opération `invokeDDX` car, bien qu’un document PDF d’entrée soit transmis au service Assembler, ce dernier renvoie un objet de collection contenant un ou plusieurs documents.

>[!NOTE]
>
>Pour plus d’informations sur le service Assembler, consultez la section [Guide de référence des services pour AEM Forms](https://help.adobe.com/fr_FR/livecycle/11.0/Services/index.html).

>[!NOTE]
>
>Pour plus d’informations sur les documents DDX, consultez la section [Guide de référence du service Assembler et de DDX](https://www.adobe.com/go/learn_aemforms_ddx_63).

## Résumé des étapes {#summary-of-steps}

Pour désassembler un document PDF, effectuez les tâches suivantes :

1. Incluez les fichiers de projet.
1. Créez un client Assembler PDF.
1. Référencez un document DX existant.
1. Référencez un document de PDF à désassembler.
1. Définissez les options d’exécution.
1. Désassemblez le document PDF.
1. Enregistrez les documents PDF désassemblés.

**Inclure les fichiers de projet**

Incluez les fichiers nécessaires dans votre projet de développement. Si vous créez une application cliente à l’aide de Java, incluez les fichiers JAR nécessaires. Si vous utilisez des services Web, veillez à inclure les fichiers proxy.

Les fichiers JAR suivants doivent être ajoutés au chemin de classe de votre projet :

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-assembler-client.jar
* adobe-utility.jar (obligatoire si AEM Forms est déployé sur JBoss)
* jbossall-client.jar (obligatoire si AEM Forms est déployé sur JBoss)

Si AEM Forms est déployé sur un serveur applicatif J2EE pris en charge autre que JBoss, vous devez remplacer adobe-utilities.jar et jbossall-client.jar par des fichiers JAR spécifiques à ce serveur.

**Créer un client Assembler PDF**

Avant de pouvoir effectuer une opération Assembler de manière programmée, vous devez créer un client de service Assembler.

**Référencer un document DDX existant**

Un document DDX doit être référencé pour désassembler un document PDF. Ce document DDX doit contenir l’élément `PDFsFromBookmarks`.

**Référencer un document PDF à désassembler**

Pour désassembler un document PDF, référencez un fichier PDF représentant le document PDF à désassembler. Lorsqu’il est transmis au service Assembler, un document PDF distinct est renvoyé pour chaque signet de niveau 1 dans le document.

**Définir les options d’exécution**

Vous pouvez définir des options d’exécution qui contrôlent le comportement du service Assembler lorsqu’il effectue une tâche. Par exemple, vous pouvez définir une option qui indique au service Assembler de continuer à traiter une tâche en cas d’erreur.

**Désassembler le document PDF**

Après avoir créé le client du service Assembler, référencé le document DDX, référencé un document PDF à désassembler et défini les options d’exécution, vous pouvez désassembler un document PDF en appelant la méthode `invokeDDX`. Si le document DDX contient des instructions pour désassembler le document PDF, le service Assembler renvoie les documents PDF désassemblés dans un objet de collection.

**Enregistrer les documents PDF désassemblés**

Tous les documents PDF désassemblés sont renvoyés dans un objet de collection. Effectuez une itération sur l’objet de collection et enregistrez chaque document PDF en tant que fichier PDF.

**Voir également**

[Inclusion des fichiers de bibliothèque Java d’AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Assembler les documents PDF par programmation](/help/forms/developing/programmatically-assembling-pdf-documents.md)

## Désassembler un document PDF à l’aide de l’API Java {#disassemble-a-pdf-document-using-the-java-api}

Désassemblez un document PDF à l’aide de l’API Assembler Service (Java) :

1. Incluez les fichiers de projet.

   Incluez les fichiers JAR client, tels que adobe-assembler-client.jar, dans le chemin de classe de votre projet Java.

1. Créez un client Assembler PDF.

   * Créez un objet `ServiceClientFactory` qui contient des propriétés de connexion.
   * Créez un objet `AssemblerServiceClient` en utilisant son constructeur et en transmettant l’objet `ServiceClientFactory`.

1. Référencez un document DX existant.

   * Créez un objet `java.io.FileInputStream` qui représente le document DDX en utilisant son constructeur et en transmettant une valeur de chaîne qui spécifie l’emplacement du fichier DDX.
   * Créez un objet `com.adobe.idp.Document` en utilisant son constructeur et en transmettant l’objet `java.io.FileInputStream`. 

1. Référencez un document de PDF à désassembler.

   * Créez un objet `java.util.Map` servant à stocker des documents PDF d’entrée à l’aide d’un constructeur `HashMap`.
   * Créez un objet `java.io.FileInputStream` en utilisant son constructeur et en transmettant l’emplacement du document PDF à désassembler.
   * Créez un objet `com.adobe.idp.Document` et transmettez l’objet `java.io.FileInputStream` contenant le document PDF à désassembler.
   * Ajoutez une entrée à l’objet `java.util.Map` en appelant sa méthode `put` et en transmettant les arguments suivants :

      * Une valeur de chaîne qui représente le nom de la clé. Cette valeur doit correspondre à celle de l’élément source PDF spécifié dans le document DDX.
      * Un objet `com.adobe.idp.Document` qui contient le document PDF à désassembler.

1. Définissez les options d’exécution.

   * Créez un objet `AssemblerOptionSpec` qui stocke les options d’exécution en utilisant son constructeur.
   * Définissez les options d’exécution pour répondre à vos exigences professionnelles en appelant une méthode appartenant à l’objet `AssemblerOptionSpec`. Par exemple, pour demander au service Assembler de continuer à traiter une tâche en cas d’erreur, appelez la fonction `AssemblerOptionSpec` de `setFailOnError` méthode et transmission `false`.

1. Désassemblez le document PDF.

   Appeler la variable `AssemblerServiceClient` de `invokeDDX` et transmettez les valeurs requises suivantes :

   * Un objet `com.adobe.idp.Document` qui représente le document DDX à utiliser.
   * Un objet `java.util.Map` qui contient le document PDF à désassembler.
   * Un objet `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` spécifiant les options d’exécution, notamment la police par défaut et le niveau de journalisation de la tâche

   La méthode `invokeDDX` renvoie un objet `com.adobe.livecycle.assembler.client.AssemblerResult` contenant les documents PDF désassemblés et les exceptions survenues.

1. Enregistrez les documents PDF désassemblés.

   Pour obtenir des documents PDF désassemblés, procédez comme suit :

   * Appeler la variable `AssemblerResult` de `getDocuments` . Cette méthode renvoie un objet `java.util.Map`.
   * Effectuez une itération dans l’objet `java.util.Map` jusqu’à ce que vous trouviez l’objet `com.adobe.idp.Document` cible.
   * Appeler la variable `com.adobe.idp.Document` de `copyToFile` pour extraire le document du PDF.

**Voir également**

[Désassembler des documents PDF par programme](#programmatically-disassembling-pdf-documents)

[Démarrage rapide (mode SOAP) : désassembler un document PDF à l’aide de l’API Java](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-disassembling-a-pdf-document-using-the-java-api)

[Inclusion des fichiers de bibliothèque Java d’AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Désassembler un document PDF à l’aide de l’API de service web {#disassemble-a-pdf-document-using-the-web-service-api}

Pour désassembler un document PDF à l’aide de l’API du service Assembler (service web), procédez comme suit :

1. Incluez les fichiers de projet.

   Créez un projet Microsoft .NET qui utilise MTOM. Veillez à utiliser la définition WSDL suivante lors de la définition d’une référence de service : `http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Remplacez `localhost` par l’adresse IP du serveur hébergeant AEM Forms.

1. Créez un client Assembler PDF.

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

   * Créez un objet `BLOB` en utilisant son constructeur. L’objet `BLOB` est utilisé pour stocker le document DDX.
   * Créez un objet `System.IO.FileStream` en appelant son constructeur. Transmettez une valeur de chaîne qui représente l’emplacement du fichier du document DDX et son mode d’ouverture.
   * Créez un tableau d’octets qui stocke le contenu de l’objet `System.IO.FileStream`. Vous pouvez déterminer la taille du tableau d’octets en obtenant la variable `System.IO.FileStream` de `Length` .
   * Renseignez le tableau d’octets avec les données de diffusion en appelant la variable `System.IO.FileStream` de `Read` et transmettre le tableau byte, la position de départ et la longueur du flux à lire.
   * Renseignez l’objet `BLOB` en attribuant sa propriété `MTOM` au contenu du tableau d’octets.

1. Référencez un document de PDF à désassembler.

   * Créez un objet `BLOB` en utilisant son constructeur. L’objet `BLOB` sert à stocker le document PDF d’entrée. Cet objet `BLOB` est transmis à l’opération `invokeOneDocument` comme argument.
   * Créez un objet `System.IO.FileStream` en appelant son constructeur et en transmettant une valeur de chaîne qui représente l’emplacement du document PDF d’entrée et son mode d’ouverture.
   * Créez un tableau d’octets qui stocke le contenu de l’objet `System.IO.FileStream`. Vous pouvez déterminer la taille du tableau d’octets en obtenant la variable `System.IO.FileStream` de `Length` .
   * Renseignez le tableau d’octets avec les données de diffusion en appelant la variable `System.IO.FileStream` de `Read` et transmettre le tableau byte, la position de départ et la longueur du flux à lire.
   * Renseignez l’objet `BLOB` en attribuant à son champ `MTOM` le contenu du tableau d’octets.
   * Créez un objet `MyMapOf_xsd_string_To_xsd_anyType`. Cet objet de collection est utilisé pour stocker le PDF à désassembler.
   * Créez un objet `MyMapOf_xsd_string_To_xsd_anyType_Item`.
   * Affectez une valeur de chaîne qui représente le nom de la clé au champ `key` de l’objet `MyMapOf_xsd_string_To_xsd_anyType_Item`. Cette valeur doit correspondre à celle de l’élément source PDF spécifié dans le document DDX.
   * Affectez l’objet `BLOB` qui stocke le document PDF au champ `value` de l’objet `MyMapOf_xsd_string_To_xsd_anyType_Item`.
   * Ajoutez l’objet `MyMapOf_xsd_string_To_xsd_anyType_Item` à l’objet `MyMapOf_xsd_string_To_xsd_anyType`. Appelez la méthode `Add` de l’objet `MyMapOf_xsd_string_To_xsd_anyType` et transmettez l’objet `MyMapOf_xsd_string_To_xsd_anyType`.

1. Définissez les options d’exécution.

   * Créez un objet `AssemblerOptionSpec` qui stocke les options d’exécution en utilisant son constructeur.
   * Définissez les options d’exécution pour répondre à vos exigences professionnelles en attribuant une valeur à un membre de données qui appartient à l’objet `AssemblerOptionSpec`. Par exemple, pour demander au service Assembler de continuer à traiter une tâche en cas d’erreur, affectez `false` à la fonction `AssemblerOptionSpec` de `failOnError` champ .

1. Désassemblez le document PDF.

   Appeler la variable `AssemblerServiceClient` de `invokeDDX` et transmettez les valeurs suivantes :

   * Un objet `BLOB` qui représente le document DDX qui désassemble le document PDF.
   * L’objet `MyMapOf_xsd_string_To_xsd_anyType` qui contient le document PDF à désassembler.
   * Un objet `AssemblerOptionSpec` qui spécifie les options d’exécution.

   La méthode `invokeDDX` renvoie un objet `AssemblerResult` qui contient les résultats de la tâche et les exceptions survenues.

1. Enregistrez les documents PDF désassemblés.

   Pour obtenir les documents PDF nouvellement créés, procédez comme suit :

   * Accédez au `AssemblerResult` de `documents` , qui est un `Map` contenant les documents de PDF désassemblés.
   * Effectuez une itération par le biais de l’objet `Map` pour obtenir chaque document généré. Ensuite, jetez le de ce membre du tableau `value` à `BLOB`.
   * Extrayez les données binaires qui représentent le document du PDF en accédant à ses `BLOB` de `MTOM` . Cette opération renvoie un tableau d’octets que vous pouvez enregistrer dans un fichier PDF.

**Voir également**

[Désassembler des documents PDF par programme](#programmatically-disassembling-pdf-documents)

[Appeler AEM Forms en utilisant MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
