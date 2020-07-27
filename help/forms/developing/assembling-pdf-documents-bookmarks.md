---
title: Assemblage de Documents PDF avec des signets
seo-title: Assemblage de Documents PDF avec des signets
description: 'null'
seo-description: 'null'
uuid: a306d2a6-0b12-4eb3-bff4-968a33417486
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
discoiquuid: 9f4711a8-033c-4051-ab41-65a26838899b
translation-type: tm+mt
source-git-commit: 1343cc33a1e1ce26c0770a3b49317e82353497ab
workflow-type: tm+mt
source-wordcount: '2526'
ht-degree: 3%

---


# Assemblage de Documents PDF avec des signets {#assembling-pdf-documents-with-bookmarks}

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

Dans ce document DDX, notez que la valeur est affectée à l’attribut source `Loan.pdf`. Ce document DDX spécifie qu’un seul document PDF est transmis au service Assembler. Lors de l’assemblage d’un document PDF avec des signets, vous devez spécifier un document XML de signets qui décrit les signets dans le document de résultats. Pour spécifier un document XML de signet, assurez-vous que l’ `Bookmarks` élément est spécifié dans votre document DDX.

Dans cet exemple de document DDX, l’ `Bookmarks` élément indique `doc2` la valeur. Cette valeur indique que la carte d’entrée transmise au service Assembler contient une clé nommée `doc2`. La valeur de la `doc2` clé est une `com.adobe.idp.Document` valeur qui représente le document XML du signet. (Voir &quot;Langue des signets&quot; dans le Guide de référence [du service](https://www.adobe.com/go/learn_aemforms_ddx_63)Assembler et du DDX.)

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
>Pour plus d’informations sur les actions prises en charge, voir &quot; `Action` element&quot; dans le Guide de référence [du service](https://www.adobe.com/go/learn_aemforms_ddx_63)Assembler et du DDX.

Compte tenu du document DDX spécifié dans cette section et du signet du fichier XML en entrée, le service Assembler assemble un document PDF contenant les signets suivants.

![aw_aw_bmark](assets/aw_aw_bmark.png)

Lorsqu&#39;un utilisateur clique sur le signet *Ouvrir les détails* du prêt, le fichier LoanDetails.pdf est ouvert. De même, lorsque l’utilisateur clique sur le signet *Launch NotePad* , NotePad est démarré.

>[!NOTE]
>
>Avant de lire cette section, il est recommandé de se familiariser avec l’assemblage de documents PDF à l’aide du service Assembler. Cette section ne traite pas des concepts, tels que la création d’un objet de collection contenant des documents d’entrée ou l’apprentissage de l’extraction des résultats à partir de l’objet de collection renvoyé. (voir Assemblage [par programmation de Documents](/help/forms/developing/programmatically-assembling-pdf-documents.md#programmatically-assembling-pdf-documents)PDF).

>[!NOTE]
>
>For more information about the Assembler service, see [Services Reference for AEM Forms](https://www.adobe.com/go/learn_aemforms_services_63).

>[!NOTE]
>
>Pour plus d’informations sur un document DDX, voir [Service Assembler et Référence](https://www.adobe.com/go/learn_aemforms_ddx_63)DDX.

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
* adobe-utilities.jar (requis si le AEM Forms est déployé sur JBoss)
* jbossall-client.jar (requis si le AEM Forms est déployé sur JBoss)

si le AEM Forms est déployé sur un serveur d’applications J2EE pris en charge autre que JBoss, vous devez remplacer les fichiers adobe-utilities.jar et jbossall-client.jar par des fichiers JAR spécifiques au serveur d’applications J2EE sur lequel le AEM Forms est déployé. For information about the location of all AEM Forms JAR files, see [Including AEM Forms Java library files](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Création d’un client PDF Assembler**

Avant de pouvoir exécuter une opération Assembler par programmation, vous devez créer un client de service Assembler.

**Référencer un document DDX existant**

Un document DDX doit être référencé pour assembler un document PDF. Ce document DDX doit contenir l’ `Bookmarks` élément qui indique au service Assembler d’assembler un PDF contenant des signets. (Voir le document DDX illustré plus haut dans cette section pour un exemple.)

**Référence à un document PDF auquel des signets sont ajoutés**

Référencez un document PDF auquel les signets sont ajoutés. Peu importe que le document PDF référencé contienne déjà des signets. Si l’ `Bookmarks` élément est un enfant de l’élément source PDF, les signets remplaceront ceux qui existent déjà dans la source PDF. Toutefois, si vous souhaitez conserver les signets existants, assurez-vous qu’ `Bookmarks` il s’agit d’un frère de l’élément source PDF. Prenons l’exemple suivant :

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
>Voir &quot;Langue des signets&quot; dans le Guide de référence [du service](https://www.adobe.com/go/learn_aemforms_ddx_63)Assembler et du DDX.

**Ajouter le document PDF et le document XML du signet à une collection Map**

Vous devez ajouter le document PDF auquel les signets sont ajoutés et le document XML du signet à la collection Map. Par conséquent, l’objet de collection Map contient deux éléments : un document PDF et le document XML du signet.

**Définition des options d’exécution**

Vous pouvez définir des options d’exécution qui contrôlent le comportement du service Assembler lorsqu’il effectue une tâche. Par exemple, vous pouvez définir une option qui indique au service Assembler de continuer à traiter une tâche en cas d’erreur. Pour plus d’informations sur les options d’exécution que vous pouvez définir, voir la référence de `AssemblerOptionSpec` classe dans Référence [API](https://www.adobe.com/go/learn_aemforms_javadocs_63_en)AEM Forms.

**Assemblage du document PDF**

Pour assembler un document PDF contenant de nouveaux signets, utilisez l’ `invokeDDX` opération du service Assembler. La raison pour laquelle vous devez utiliser l’ `invokeDDX` opération plutôt que d’autres opérations du service Assembler, par exemple `invokeOneDocument` est que le service Assembler requiert un document XML de signet transmis dans l’objet de collecte Map. Cet objet est un paramètre de l&#39; `invokeDDX` opération.

**Enregistrer le document PDF contenant des signets**

Vous devez extraire les résultats de l’objet de mappage renvoyé et enregistrer le document PDF correspondant. (voir la section &quot;Extraction des résultats&quot; dans Assemblage [par programmation de Documents](/help/forms/developing/programmatically-assembling-pdf-documents.md)PDF).

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
   * Create an `AssemblerServiceClient` object by using its constructor and passing the `ServiceClientFactory` object.

1. Référencez un document DDX existant.

   * Créez un `java.io.FileInputStream` objet qui représente le document DDX en utilisant son constructeur et en transmettant une valeur de chaîne qui spécifie l’emplacement du fichier DDX.
   * Créez un objet `com.adobe.idp.Document` en utilisant son constructeur et en transmettant l’objet `java.io.FileInputStream`. 

1. Référencez un document PDF auquel les signets sont ajoutés.

   * Créez un `java.io.FileInputStream` objet en utilisant son constructeur et en transmettant l’emplacement du document PDF.
   * Créez un `com.adobe.idp.Document` objet à l’aide de son constructeur et transmettez l’ `java.io.FileInputStream` objet qui contient le document PDF.

1. Référencez le document XML du signet.

   * Créez un `java.io.FileInputStream` objet en utilisant son constructeur et en transmettant l’emplacement du fichier XML qui représente le document XML du signet.
   * Créez un `com.adobe.idp.Document` objet et transmettez l’ `java.io.FileInputStream` objet contenant le document PDF.

1. Ajoutez le document PDF et le document XML du signet à une collection Map.

   * Créez un `java.util.Map` objet utilisé pour stocker le document PDF d’entrée et le document XML du signet.
   * Ajoutez le document PDF d’entrée en appelant la `java.util.Map` `put` méthode de l’objet et en transmettant les arguments suivants :

      * Valeur de chaîne qui représente le nom de la clé. Cette valeur doit correspondre à la valeur de l’élément source PDF spécifié dans le document DDX.
      * Objet `com.adobe.idp.Document` contenant le document PDF d’entrée.
   * Ajoutez le document XML du signet en appelant la `java.util.Map` `put` méthode de l’objet et en transmettant les arguments suivants :

      * Valeur de chaîne qui représente le nom de la clé. Cette valeur doit correspondre à la valeur de l’élément source Signets spécifié dans le document DDX.
      * Objet `com.adobe.idp.Document` contenant le document XML du signet.


1. Définissez les options d’exécution.

   * Créez un `AssemblerOptionSpec` objet qui stocke les options d’exécution à l’aide de son constructeur.
   * Définissez des options d’exécution pour répondre aux besoins de votre entreprise en appelant une méthode qui appartient à l’ `AssemblerOptionSpec` objet. Par exemple, pour demander au service Assembler de continuer à traiter une tâche en cas d’erreur, appelez la `AssemblerOptionSpec` méthode de l’ `setFailOnError` objet et passez `false`.

1. Assemblage du document PDF.

   Appelez la méthode `AssemblerServiceClient` de l’ `invokeDDX` objet et transmettez les valeurs requises suivantes :

   * Objet `com.adobe.idp.Document` représentant le document DDX à utiliser
   * Objet `java.util.Map` contenant à la fois le document PDF d’entrée et le document XML du signet.
   * Un `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` objet qui spécifie les options d’exécution, y compris la police par défaut et le niveau de journal des tâches

   La `invokeDDX` méthode renvoie un `com.adobe.livecycle.assembler.client.AssemblerResult` objet qui contient les résultats de la tâche et les exceptions survenues.

1. Enregistrez le document PDF contenant des signets.

   Pour obtenir le document PDF nouvellement créé, effectuez les opérations suivantes :

   * Appelle la méthode `AssemblerResult` de l’ `getDocuments` objet. Cette méthode renvoie un `java.util.Map` objet.
   * Effectuez une itération sur l’ `java.util.Map` objet jusqu’à ce que vous trouviez l’ `com.adobe.idp.Document` objet obtenu. (Vous pouvez utiliser l’élément de résultat PDF spécifié dans le document DDX pour obtenir le document.)
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
   >Remplacez `localhost` par l’adresse IP du serveur hébergeant les AEM Forms.

1. Créez un client PDF Assembler.

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

1. Référencez un document PDF auquel les signets sont ajoutés.

   * Créez un objet `BLOB` en utilisant son constructeur. L’ `BLOB` objet est utilisé pour stocker le fichier PDF d’entrée.
   * Créez un `System.IO.FileStream` objet en appelant son constructeur et en transmettant une valeur de chaîne qui représente l’emplacement du fichier du document PDF d’entrée et le mode d’ouverture du fichier.
   * Créez un tableau d’octets qui stocke le contenu de l’ `System.IO.FileStream` objet. Vous pouvez déterminer la taille du tableau d’octets en obtenant la `System.IO.FileStream` `Length` propriété de l’objet.
   * Renseignez le tableau d’octets avec les données de flux en appelant la `System.IO.FileStream` `Read` méthode de l’objet et en transmettant le tableau d’octets, la position de départ et la longueur du flux à lire.
   * Renseignez l’ `BLOB` objet en affectant son `MTOM` champ au contenu du tableau d’octets.

1. Référencez le document XML du signet.

   * Créez un objet `BLOB` en utilisant son constructeur. L’ `BLOB` objet est utilisé pour stocker le document XML du signet.
   * Créez un `System.IO.FileStream` objet en appelant son constructeur et en transmettant une valeur de chaîne qui représente l’emplacement du fichier du document PDF d’entrée et le mode d’ouverture du fichier.
   * Créez un tableau d’octets qui stocke le contenu de l’ `System.IO.FileStream` objet. Vous pouvez déterminer la taille du tableau d’octets en obtenant la `System.IO.FileStream` `Length` propriété de l’objet.
   * Renseignez le tableau d’octets avec les données de flux en appelant la `System.IO.FileStream` `Read` méthode de l’objet et en transmettant le tableau d’octets, la position de départ et la longueur du flux à lire.
   * Renseignez l’ `BLOB` objet en affectant son `MTOM` champ au contenu du tableau d’octets.

1. Ajoutez le document PDF et le document XML du signet à une collection Map.

   * Create a `MyMapOf_xsd_string_To_xsd_anyType` object. Cet objet de collection est utilisé pour stocker les documents PDF d’entrée et le document XML du signet.
   * Pour chaque document PDF d’entrée et le document XML du signet, créez un `MyMapOf_xsd_string_To_xsd_anyType_Item` objet.
   * Attribuez une valeur de chaîne qui représente le nom de clé au `MyMapOf_xsd_string_To_xsd_anyType_Item` `key` champ de l’objet. Cette valeur doit correspondre à la valeur de l’élément source PDF spécifié dans le document DDX.
   * Affectez l’ `BLOB` objet qui stocke le document PDF au `MyMapOf_xsd_string_To_xsd_anyType_Item` `value` champ de l’objet.
   * Ajoutez l’ `MyMapOf_xsd_string_To_xsd_anyType_Item` objet sur l’ `MyMapOf_xsd_string_To_xsd_anyType` objet. Invoke the `MyMapOf_xsd_string_To_xsd_anyType` object&#39;s `Add` method and pass the `MyMapOf_xsd_string_To_xsd_anyType` object. (Effectuez cette tâche pour chaque document PDF d’entrée et le document XML de signet.)

1. Définissez les options d’exécution.

   * Créez un `AssemblerOptionSpec` objet qui stocke les options d’exécution à l’aide de son constructeur.
   * Définissez des options d’exécution pour répondre aux besoins de votre entreprise en attribuant une valeur à un membre de données qui appartient à l’ `AssemblerOptionSpec` objet. Par exemple, pour demander au service Assembler de poursuivre le traitement d’une tâche en cas d’erreur, affectez-lui `false` le membre `AssemblerOptionSpec` de données de l’ `failOnError` objet.

1. Assemblage du document PDF.

   Appelez la méthode `AssemblerServiceClient` de l’ `invokeDDX` objet et transmettez les valeurs suivantes :

   * Objet `BLOB` représentant le document DDX
   * Tableau `MyMapOf_xsd_string_To_xsd_anyType` contenant les documents d&#39;entrée
   * Objet `AssemblerOptionSpec` spécifiant les options d’exécution

   La `invokeDDX` méthode renvoie un `AssemblerResult` objet qui contient les résultats de la tâche et les exceptions qui ont pu se produire.

1. Enregistrez le document PDF contenant des signets.

   Pour obtenir le document PDF nouvellement créé, effectuez les opérations suivantes :

   * Accédez au `AssemblerResult` champ de l’ `documents` objet, qui est un `Map` objet contenant les documents PDF de résultat.
   * Effectuez une itération sur l’ `Map` objet jusqu’à ce que vous trouviez la clé correspondant au nom du document résultant. Ensuite, déposez les éléments `value` de ce membre de la baie sur un `BLOB`.
   * Extrayez les données binaires qui représentent le document PDF en accédant au `BLOB` champ de l’objet `MTOM` en question. Cette opération renvoie un tableau d’octets que vous pouvez écrire dans un fichier PDF.

**Voir également**

[Appel de AEM Forms à l’aide de MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
