---
title: Assemblage de Documents PDF avec des signets
seo-title: Assemblage de Documents PDF avec des signets
description: Utilisez le service Assembler pour modifier un document PDF qui contient des signets afin d’inclure des signets à l’aide de l’API Java et de l’API du service Web.
seo-description: Utilisez le service Assembler pour modifier un document PDF qui contient des signets afin d’inclure des signets à l’aide de l’API Java et de l’API du service Web.
uuid: a306d2a6-0b12-4eb3-bff4-968a33417486
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 9f4711a8-033c-4051-ab41-65a26838899b
role: Développeur
translation-type: tm+mt
source-git-commit: 48726639e93696f32fa368fad2630e6fca50640e
workflow-type: tm+mt
source-wordcount: '2589'
ht-degree: 2%

---


# Assemblage de Documents PDF avec des signets {#assembling-pdf-documents-with-bookmarks}

**Les exemples et exemples de ce document ne concernent que l’environnement AEM Forms on JEE.**

Vous pouvez assembler un document PDF contenant des signets. Par exemple, supposons que vous disposez d’un document PDF qui ne contient pas de signets et que vous souhaitez le modifier en fournissant des signets. Le service Assembler vous permet de lui transmettre un document PDF qui ne contient pas de signets et de récupérer un document PDF contenant des signets.

Les signets contiennent les propriétés suivantes :

* Titre qui s’affiche sous forme de texte à l’écran.
* Action qui spécifie ce qui se produit lorsqu’un utilisateur clique sur le signet. L’action type d’un signet consiste à se déplacer vers un autre emplacement du document actuel ou à ouvrir un autre document PDF, bien que d’autres actions puissent être spécifiées.

Aux fins de cette discussion, supposons que le document DDX suivant soit utilisé.

```xml
 <?xml version="1.0" encoding="UTF-8"?>
 <DDX xmlns="https://ns.adobe.com/DDX/1.0/">
       <PDF result="FinalDoc.pdf">
          <PDF source="Loan.pdf">
             <Bookmarks source="doc2" />
          </PDF>
       </PDF>
 </DDX>
```

Dans ce document DDX, notez que la valeur `Loan.pdf` est affectée à l’attribut source. Ce document DDX spécifie qu’un seul document PDF est transmis au service Assembler. Lors de l’assemblage d’un document PDF avec des signets, vous devez spécifier un document XML de signets qui décrit les signets dans le document de résultats. Pour spécifier un document XML de signet, assurez-vous que l’élément `Bookmarks` est spécifié dans votre document DDX.

Dans cet exemple de document DDX, l’élément `Bookmarks` spécifie `doc2` comme valeur. Cette valeur indique que la carte d’entrée transmise au service Assembler contient une clé nommée `doc2`. La valeur de la clé `doc2` est une valeur `com.adobe.idp.Document` qui représente le document XML du signet. (Voir &quot;Langue des signets&quot; dans le [Guide de référence du service Assembler et du DDX](https://www.adobe.com/go/learn_aemforms_ddx_63).)

Cette rubrique utilise le langage de signets XML suivant pour assembler un document PDF contenant des signets.

```xml
 <?xml version="1.0" encoding="UTF-8"?>
 <Bookmarks xmlns="https://ns.adobe.com/pdf/bookmarks" version="1.0">
       <Bookmark>
          <Action>
             <Launch NewWindow="true">
                <File Name="C:\Adobe\LoanDetails.pdf" />
             </Launch>
          </Action>
         <Title>Open the Loan document</Title>
       </Bookmark>
 <Bookmark>
          <Action>
             <Launch>
                <Win Name="C:\WINDOWS\notepad.exe" />
             </Launch>
          </Action>
     <Title>Launch NotePad</Title>
       </Bookmark>
 </Bookmarks>
```

Dans ce document XML de signet, notez l’élément Action qui définit l’action exécutée lorsqu’un utilisateur clique sur le signet. Sous l’élément Action se trouve l’élément Launch qui lance des applications, telles que NotePad, et ouvre des fichiers, tels que des fichiers PDF. Pour ouvrir un fichier PDF, vous devez utiliser l’élément Fichier qui spécifie le fichier à ouvrir. Par exemple, dans le fichier XML de signet spécifié dans cette section, le nom du fichier ouvert est LoanDetails.pdf.

>[!NOTE]
>
>Pour plus d&#39;informations sur les actions prises en charge, voir &quot; `Action` element&quot; dans le [Guide de référence du service Assembler et du DDX](https://www.adobe.com/go/learn_aemforms_ddx_63).

Compte tenu du document DDX spécifié dans cette section et du signet du fichier XML en entrée, le service Assembler assemble un document PDF contenant les signets suivants.

![aw_aw_bmark](assets/aw_aw_bmark.png)

Lorsqu&#39;un utilisateur clique sur le signet *Ouvrir les détails du prêt*, le fichier LoanDetails.pdf est ouvert. De même, lorsque l’utilisateur clique sur le signet *Launch NotePad*, NotePad est démarré.

>[!NOTE]
>
>Avant de lire cette section, il est recommandé de se familiariser avec l’assemblage de documents PDF à l’aide du service Assembler. Cette section ne traite pas des concepts, tels que la création d’un objet de collection contenant des documents d’entrée ou l’apprentissage de l’extraction des résultats à partir de l’objet de collection renvoyé. (Voir [Assemblage par programmation de Documents PDF](/help/forms/developing/programmatically-assembling-pdf-documents.md#programmatically-assembling-pdf-documents).)

>[!NOTE]
>
>Pour plus d’informations sur le service Assembler, voir [Guide de référence des services pour AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

>[!NOTE]
>
>Pour plus d’informations sur un document DDX, voir [Service Assembler et Référence DDX](https://www.adobe.com/go/learn_aemforms_ddx_63).

## Résumé des étapes {#summary-of-steps}

Pour assembler un document PDF contenant des signets, effectuez les tâches suivantes :

1. Incluez des fichiers de projet.
1. Créez un client PDF Assembler.
1. Référencez un document DDX existant.
1. Référencez un document PDF auquel les signets sont ajoutés.
1. Référencez le document XML du signet.
1. Ajoutez le document PDF et le document XML du signet à une collection Map.
1. Définissez les options d’exécution.
1. Assemblage du document PDF.
1. Enregistrez le document PDF contenant des signets.

**Inclure les fichiers de projet**

Incluez les fichiers nécessaires dans votre projet de développement. Si vous créez une application cliente à l’aide de Java, incluez les fichiers JAR nécessaires. Si vous utilisez des services Web, veillez à inclure les fichiers proxy.

Les fichiers JAR suivants doivent être ajoutés au chemin de classe de votre projet :

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-assembler-client.jar
* adobe-utilities.jar (requis si AEM Forms est déployé sur JBoss)
* jbossall-client.jar (requis si AEM Forms est déployé sur JBoss)

si AEM Forms est déployé sur un serveur d’applications J2EE pris en charge autre que JBoss, vous devez remplacer les fichiers adobe-utilities.jar et jbossall-client.jar par des fichiers JAR spécifiques au serveur d’applications J2EE sur lequel AEM Forms est déployé. Pour plus d’informations sur l’emplacement de tous les fichiers JAR AEM Forms, voir [Inclusion de fichiers de bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Création d’un client PDF Assembler**

Avant de pouvoir exécuter une opération Assembler par programmation, vous devez créer un client de service Assembler.

**Référencer un document DDX existant**

Un document DDX doit être référencé pour assembler un document PDF. Ce document DDX doit contenir l’élément `Bookmarks`, qui demande au service Assembler d’assembler un PDF contenant des signets. (Voir le document DDX illustré plus haut dans cette section pour un exemple.)

**Référence à un document PDF auquel des signets sont ajoutés**

Référencez un document PDF auquel les signets sont ajoutés. Peu importe que le document PDF référencé contienne déjà des signets. Si l’élément `Bookmarks` est un enfant de l’élément source PDF, les signets remplaceront ceux qui existent déjà dans la source PDF. Cependant, si vous souhaitez conserver les signets existants, assurez-vous que `Bookmarks` est un frère de l’élément source PDF. Prenons l’exemple suivant :

```xml
 <PDF result="foo">
      <PDF source="inDoc"/>
      <Bookmarks source="doc2"/>
 </PDF>
```

**Référence au document XML du signet**

Pour assembler un PDF contenant de nouveaux signets, vous devez référencer un document XML de signet. Le document XML du signet est transmis au service Assembler au sein de l’objet de collecte Map. (Voir le document XML du signet illustré plus haut dans cette section pour un exemple.)

>[!NOTE]
>
>Voir &quot;Langue des signets&quot; dans le [Guide de référence du service Assembler et du DDX](https://www.adobe.com/go/learn_aemforms_ddx_63).

**Ajouter le document PDF et le document XML du signet à une collection Map**

Vous devez ajouter le document PDF auquel les signets sont ajoutés et le document XML du signet à la collection Map. Par conséquent, l’objet de collection Map contient deux éléments : un document PDF et le document XML du signet.

**Définition des options d’exécution**

Vous pouvez définir des options d’exécution qui contrôlent le comportement du service Assembler lorsqu’il effectue une tâche. Par exemple, vous pouvez définir une option qui indique au service Assembler de continuer à traiter une tâche en cas d’erreur. Pour plus d&#39;informations sur les options d&#39;exécution que vous pouvez définir, consultez la référence de classe `AssemblerOptionSpec` dans [AEM Forms API Reference](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

**Assemblage du document PDF**

Pour assembler un document PDF contenant de nouveaux signets, utilisez l’opération `invokeDDX` du service Assembler. La raison pour laquelle vous devez utiliser l&#39;opération `invokeDDX` plutôt que d&#39;autres opérations de service Assembler telles que `invokeOneDocument` est que le service Assembler requiert un document XML de signet transmis dans l&#39;objet de collecte Map. Cet objet est un paramètre de l&#39;opération `invokeDDX`.

**Enregistrer le document PDF contenant des signets**

Vous devez extraire les résultats de l’objet de mappage renvoyé et enregistrer le document PDF correspondant. (Voir &quot;Extraire les résultats&quot; dans [Assemblage par programmation de Documents PDF](/help/forms/developing/programmatically-assembling-pdf-documents.md).)

**Voir également**

[Inclusion des fichiers de bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Assemblage par programmation de Documents PDF](/help/forms/developing/programmatically-assembling-pdf-documents.md)

## Assemblage de documents PDF avec des signets à l’aide de l’API Java {#assemble-pdf-documents-with-bookmarks-using-the-java-api}

Assemblage d’un document PDF avec des signets à l’aide de l’API Service Assembler (Java) :

1. Incluez des fichiers de projet.

   Incluez des fichiers JAR client, tels que adobe-assembler-client.jar, dans le chemin de classe de votre projet Java.

1. Créez un client PDF Assembler.

   * Créez un objet `ServiceClientFactory` qui contient des propriétés de connexion. (Voir [Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties).)
   * Créez un objet `AssemblerServiceClient` en utilisant son constructeur et en transmettant l&#39;objet `ServiceClientFactory`.

1. Référencez un document DDX existant.

   * Créez un objet `java.io.FileInputStream` qui représente le document DDX en utilisant son constructeur et en transmettant une valeur de chaîne qui spécifie l’emplacement du fichier DDX.
   * Créez un objet `com.adobe.idp.Document` en utilisant son constructeur et en transmettant l’objet `java.io.FileInputStream`. 

1. Référencez un document PDF auquel les signets sont ajoutés.

   * Créez un objet `java.io.FileInputStream` en utilisant son constructeur et en transmettant l’emplacement du document PDF.
   * Créez un objet `com.adobe.idp.Document` en utilisant son constructeur et transmettez l’objet `java.io.FileInputStream` contenant le document PDF.

1. Référencez le document XML du signet.

   * Créez un objet `java.io.FileInputStream` en utilisant son constructeur et en transmettant l’emplacement du fichier XML qui représente le document XML du signet.
   * Créez un objet `com.adobe.idp.Document` et transmettez l’objet `java.io.FileInputStream` contenant le document PDF.

1. Ajoutez le document PDF et le document XML du signet à une collection Map.

   * Créez un objet `java.util.Map` utilisé pour stocker à la fois le document PDF d’entrée et le document XML du signet.
   * Ajoutez le document PDF d’entrée en appelant la méthode `java.util.Map` de l’objet `put` et en transmettant les arguments suivants :

      * Valeur de chaîne qui représente le nom de la clé. Cette valeur doit correspondre à la valeur de l’élément source PDF spécifié dans le document DDX.
      * Objet `com.adobe.idp.Document` contenant le document PDF d’entrée.
   * Ajoutez le document XML du signet en appelant la méthode `put` de l’objet `java.util.Map` et en transmettant les arguments suivants :

      * Valeur de chaîne qui représente le nom de la clé. Cette valeur doit correspondre à la valeur de l’élément source Signets spécifié dans le document DDX.
      * Objet `com.adobe.idp.Document` contenant le document XML du signet.


1. Définissez les options d’exécution.

   * Créez un objet `AssemblerOptionSpec` qui stocke les options d’exécution à l’aide de son constructeur.
   * Définissez des options d&#39;exécution pour répondre aux besoins de votre entreprise en appelant une méthode appartenant à l&#39;objet `AssemblerOptionSpec`. Par exemple, pour demander au service Assembler de continuer à traiter une tâche en cas d’erreur, appelez la méthode `AssemblerOptionSpec` de l’objet `setFailOnError` et transmettez `false`.

1. Assemblage du document PDF.

   Appelez la méthode `invokeDDX` de l’objet `AssemblerServiceClient` et transmettez les valeurs requises suivantes :

   * Objet `com.adobe.idp.Document` représentant le document DDX à utiliser
   * Objet `java.util.Map` contenant à la fois le document PDF d’entrée et le document XML du signet.
   * Objet `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` qui spécifie les options d’exécution, y compris la police par défaut et le niveau de journal de tâches

   La méthode `invokeDDX` renvoie un objet `com.adobe.livecycle.assembler.client.AssemblerResult` contenant les résultats de la tâche et les exceptions survenues.

1. Enregistrez le document PDF contenant des signets.

   Pour obtenir le document PDF nouvellement créé, effectuez les opérations suivantes :

   * Appelez la méthode `AssemblerResult` de l’objet `getDocuments`. Cette opération renvoie un objet `java.util.Map`.
   * Effectuez une itération dans l&#39;objet `java.util.Map` jusqu&#39;à ce que vous trouviez l&#39;objet `com.adobe.idp.Document` obtenu. (Vous pouvez utiliser l’élément de résultat PDF spécifié dans le document DDX pour obtenir le document.)
   * Appelez la méthode `com.adobe.idp.Document` de l’objet `copyToFile` pour extraire le document PDF.

**Voir également**

[Début rapide (mode SOAP) : Assemblage de documents PDF avec des signets à l’aide de l’API Java](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-assembling-pdf-documents-with-bookmarks-using-the-java-api)

[Inclusion des fichiers de bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Assemblage de documents PDF avec des signets à l’aide de l’API du service Web {#assemble-pdf-documents-with-bookmarks-using-the-web-service-api}

Assemblage d’un document PDF avec des signets à l’aide de l’API Assembler Service (service Web) :

1. Incluez des fichiers de projet.

   Créez un projet Microsoft .NET qui utilise MTOM. Assurez-vous d’utiliser la définition WSDL suivante : `http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Remplacez `localhost` par l’adresse IP du serveur hébergeant AEM Forms.

1. Créez un client PDF Assembler.

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
   * Renseignez le tableau d’octets avec les données de flux en appelant la méthode `System.IO.FileStream` de l’objet `Read` et en transmettant le tableau d’octets, la position de départ et la longueur du flux à lire.
   * Renseignez l’objet `BLOB` en attribuant son champ `MTOM` au contenu du tableau d’octets.

1. Référencez un document PDF auquel les signets sont ajoutés.

   * Créez un objet `BLOB` en utilisant son constructeur. L’objet `BLOB` est utilisé pour stocker le PDF d’entrée.
   * Créez un objet `System.IO.FileStream` en appelant son constructeur et en transmettant une valeur de chaîne qui représente l’emplacement du fichier du document PDF d’entrée et le mode d’ouverture du fichier.
   * Créez un tableau d’octets qui stocke le contenu de l’objet `System.IO.FileStream`. Vous pouvez déterminer la taille du tableau d’octets en obtenant la propriété `System.IO.FileStream` de l’objet `Length`.
   * Renseignez le tableau d’octets avec les données de flux en appelant la méthode `System.IO.FileStream` de l’objet `Read` et en transmettant le tableau d’octets, la position de départ et la longueur du flux à lire.
   * Renseignez l’objet `BLOB` en attribuant son champ `MTOM` au contenu du tableau d’octets.

1. Référencez le document XML du signet.

   * Créez un objet `BLOB` en utilisant son constructeur. L&#39;objet `BLOB` est utilisé pour stocker le document XML du signet.
   * Créez un objet `System.IO.FileStream` en appelant son constructeur et en transmettant une valeur de chaîne qui représente l’emplacement du fichier du document PDF d’entrée et le mode d’ouverture du fichier.
   * Créez un tableau d’octets qui stocke le contenu de l’objet `System.IO.FileStream`. Vous pouvez déterminer la taille du tableau d’octets en obtenant la propriété `System.IO.FileStream` de l’objet `Length`.
   * Renseignez le tableau d’octets avec les données de flux en appelant la méthode `System.IO.FileStream` de l’objet `Read` et en transmettant le tableau d’octets, la position de départ et la longueur du flux à lire.
   * Renseignez l’objet `BLOB` en attribuant son champ `MTOM` au contenu du tableau d’octets.

1. Ajoutez le document PDF et le document XML du signet à une collection Map.

   * Créez un objet `MyMapOf_xsd_string_To_xsd_anyType`. Cet objet de collection est utilisé pour stocker les documents PDF d’entrée et le document XML du signet.
   * Pour chaque document PDF d’entrée et le document XML du signet, créez un objet `MyMapOf_xsd_string_To_xsd_anyType_Item`.
   * Attribuez une valeur de chaîne qui représente le nom de clé au champ `MyMapOf_xsd_string_To_xsd_anyType_Item` de l&#39;objet `key`. Cette valeur doit correspondre à la valeur de l’élément source PDF spécifié dans le document DDX.
   * Affectez l’objet `BLOB` qui stocke le document PDF au champ `MyMapOf_xsd_string_To_xsd_anyType_Item` de l’objet `value`.
   * Ajoutez l&#39;objet `MyMapOf_xsd_string_To_xsd_anyType_Item` à l&#39;objet `MyMapOf_xsd_string_To_xsd_anyType`. Appelez la méthode `MyMapOf_xsd_string_To_xsd_anyType` de l&#39;objet `Add` et transmettez l&#39;objet `MyMapOf_xsd_string_To_xsd_anyType`. (Effectuez cette tâche pour chaque document PDF d’entrée et le document XML de signet.)

1. Définissez les options d’exécution.

   * Créez un objet `AssemblerOptionSpec` qui stocke les options d’exécution à l’aide de son constructeur.
   * Définissez des options d&#39;exécution pour répondre aux besoins de votre entreprise en attribuant une valeur à un membre de données qui appartient à l&#39;objet `AssemblerOptionSpec`. Par exemple, pour demander au service Assembler de continuer à traiter une tâche en cas d’erreur, affectez `false` au membre de données `failOnError` de l’objet `AssemblerOptionSpec`.

1. Assemblage du document PDF.

   Appelez la méthode `invokeDDX` de l’objet `AssemblerServiceClient` et transmettez les valeurs suivantes :

   * Un objet `BLOB` qui représente le document DDX
   * Tableau `MyMapOf_xsd_string_To_xsd_anyType` contenant les documents d&#39;entrée
   * Objet `AssemblerOptionSpec` qui spécifie les options d’exécution

   La méthode `invokeDDX` renvoie un objet `AssemblerResult` contenant les résultats de la tâche et les exceptions qui peuvent s&#39;être produites.

1. Enregistrez le document PDF contenant des signets.

   Pour obtenir le document PDF nouvellement créé, effectuez les opérations suivantes :

   * Accédez au champ `documents` de l’objet `AssemblerResult`, qui est un objet `Map` contenant les documents PDF résultants.
   * Effectuez une itération dans l&#39;objet `Map` jusqu&#39;à ce que vous trouviez la clé correspondant au nom du document résultant. Ensuite, définissez `value` sur `BLOB`.
   * Extrayez les données binaires qui représentent le document PDF en accédant au champ `BLOB` `MTOM` de l’objet. Cette opération renvoie un tableau d’octets que vous pouvez écrire dans un fichier PDF.

**Voir également**

[Appel de AEM Forms à l’aide de MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
