---
title: Assembler des documents PDF avec des signets
description: Utilisez le service Assembler pour modifier un document PDF contenant des signets afin d’inclure des signets à l’aide de l’API Java et de l’API de service web.
contentOwner: admin
content-type: reference
geptopics: SG_AEMFORMS/categories/assembling_pdf_documents
products: SG_EXPERIENCEMANAGER/6.5/FORMS
topic-tags: operations
role: Developer
exl-id: 2b938410-f51b-420b-b5d4-2ed13ec29c5a
solution: Experience Manager, Experience Manager Forms
feature: Adaptive Forms,Document Services
source-git-commit: d7b9e947503df58435b3fee85a92d51fae8c1d2d
workflow-type: tm+mt
source-wordcount: '2519'
ht-degree: 100%

---

# Assembler des documents PDF avec des signets {#assembling-pdf-documents-with-bookmarks}

**Les exemples et les échantillons de ce document sont réservés à l’environnement AEM Forms sur JEE.**

Il est possible dʼassembler un document PDF qui contient des signets. Prenons lʼexemple suivant : vous disposez dʼun document PDF qui ne contient pas de signets et vous souhaitez le modifier en fournissant des signets. À l’aide du service Assembler, vous pouvez lui transmettre un document PDF qui ne contient pas de signets et récupérer un document PDF contenant des signets.

Les signets contiennent les propriétés suivantes :

* Un titre qui s’affiche sous forme de texte à l’écran.
* Une action spécifiant ce qui se produit lorsqu’un utilisateur clique sur le signet. L’action type d’un signet consiste à déplacer vers un autre emplacement du document actif ou à ouvrir un autre document PDF. D’autres actions peuvent également être spécifiées.

Dans le cadre de cette discussion, supposons que le document DDX suivant soit utilisé.

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

Dans ce document DDX, notez que la valeur `Loan.pdf` est affectée à l’attribut source. Ce document DDX indique qu’un seul document PDF est transmis au service Assembler. Lors de l’assemblage d’un document PDF avec des signets, vous devez spécifier un document XML de signet qui décrit les signets dans le document obtenu. Pour spécifier un document XML de signet, assurez-vous que l’élément `Bookmarks` est spécifié dans votre document DDX.

Dans lʼexemple suivant de document DDX, l’élément `Bookmarks` indique `doc2` comme valeur. Cette valeur indique que la carte d’entrée transmise au service Assembler contient une clé nommée `doc2`. La valeur de la clé `doc2` est une valeur `com.adobe.idp.Document` qui représente le document XML du signet. (Consultez la rubrique « Langage des signets » dans la section [Guide de référence du service Assembler et de DDX](https://www.adobe.com/go/learn_aemforms_ddx_63)).

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

Dans ce document XML de signet, notez la présence de l’élément Action, qui définit l’action effectuée lorsqu’un utilisateur clique sur le signet. Sous l’élément Action se trouve l’élément Launch qui permet de lancer des applications, comme le Bloc-notes, et dʼouvrir des fichiers, comme les fichiers PDF. Pour ouvrir un fichier PDF, vous devez utiliser l’élément File qui spécifie le fichier à ouvrir. Par exemple, dans le fichier XML du signet spécifié dans cette section, le nom du fichier ouvert est LoanDetails.pdf.

>[!NOTE]
>
>Pour plus d’informations sur les actions prises en charge, consultez la section « Élement `Action` » dans le [Guide de référence du service Assembler et de DDX](https://www.adobe.com/go/learn_aemforms_ddx_63).

Compte tenu du document DDX spécifié dans cette section et du fichier XML du signet en entrée, le service Assembler assemble un document PDF contenant les signets suivants.

![aw_aw_bmark](assets/aw_aw_bmark.png)

Lorsqu’un utilisateur clique sur le signet *Ouvrir les détails du prêt*, le fichier LoanDetails.pdf est ouvert. De même, lorsque l’utilisateur clique sur le signet *Lancer le Bloc-notes*, le Bloc-notes est démarré.

>[!NOTE]
>
>Avant dʼentamer cette section, il est recommandé de se familiariser avec l’assemblage de documents PDF à l’aide du service Assembler. Cette section nʼaborde pas les concepts tels que la création dʼun objet de collection contenant des documents dʼentrée, ou lʼapprentissage de lʼextraction des résultats de lʼobjet de collection retourné. (Consultez la section [Assembler par programmation des documents PDF](/help/forms/developing/programmatically-assembling-pdf-documents.md#programmatically-assembling-pdf-documents)).

>[!NOTE]
>
>Pour plus d’informations sur le service Assembler, consultez la section [Guide de référence des services pour AEM Forms](https://help.adobe.com/fr_FR/livecycle/11.0/Services/index.html).

>[!NOTE]
>
>Pour plus d’informations sur les documents DDX, consultez la section [Guide de référence du service Assembler et de DDX](https://www.adobe.com/go/learn_aemforms_ddx_63).

## Résumé des étapes {#summary-of-steps}

Pour assembler un document PDF contenant des signets, procédez comme suit :

1. Incluez les fichiers de projet.
1. Créez un client Assembler PDF.
1. Référencez un document DX existant.
1. Référencez un document PDF auquel des signets sont ajoutés.
1. Référencez le document XML du signet.
1. Ajoutez le document PDF et le document XML du signet à une collection Map.
1. Définissez les options d’exécution.
1. Assemblez le document PDF.
1. Enregistrez le document PDF qui contient des signets.

**Inclure des fichiers de projet**

Incluez les fichiers nécessaires dans votre projet de développement. Si vous créez une application cliente à l’aide de Java, incluez les fichiers JAR nécessaires. Si vous utilisez des services Web, veillez à inclure les fichiers proxy.

Les fichiers JAR suivants doivent être ajoutés au chemin d’accès aux classes de votre projet :

* adobe-livecycle-client.jar
* adobe-usermanager-client.jar
* adobe-assembler-client.jar
* adobe-utility.jar (obligatoire si AEM Forms est déployé sur JBoss)
* jbossall-client.jar (obligatoire si AEM Forms est déployé sur JBoss)

Si AEM Forms est déployé sur un serveur d’applications J2EE pris en charge et différent de JBoss, vous devez remplacer les fichiers adobe-utilities.jar et jbossall-client.jar par des fichiers JAR spécifiques au serveur d’applications J2EE sur lequel AEM Forms est déployé. Pour plus d’informations sur l’emplacement de ces fichiers, consultez la section [Inclure des fichiers de bibliothèque Java AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files).

**Créer un client Assembler PDF**

Avant de pouvoir effectuer une opération Assembler de manière programmée, vous devez créer un client de service Assembler.

**Référencer un document DDX existant**

Un document DDX doit être référencé pour assembler un document PDF. Ce document DDX doit contenir l’élément `Bookmarks`, qui demande au service Assembler d’assembler un PDF contenant des signets. (Pour obtenir un exemple, reportez-vous au document DDX présenté précédemment dans cette section).

**Référencer un document PDF auquel sont ajoutés des signets**

Référence un document PDF auquel des signets sont ajoutés. Peu importe que le document PDF référencé contienne déjà des signets. Si l’élément `Bookmarks` est un enfant de l’élément source du PDF, alors les signets remplaceront ceux qui existent déjà dans la source du PDF. Toutefois, si vous souhaitez conserver les signets existants, assurez-vous que `Bookmarks` est apparenté à l’élément source du PDF. Prenons l’exemple suivant :

```xml
 <PDF result="foo">
      <PDF source="inDoc"/>
      <Bookmarks source="doc2"/>
 </PDF>
```

**Référencer le document XML du signet**

Pour assembler un PDF contenant de nouveaux signets, vous devez référencer un document XML de signet. Le document XML du signet est transmis au service Assembler dans l’objet de collection Map. (Pour consulter un exemple, reportez-vous au document XML de signet illustré précédemment dans cette section).

>[!NOTE]
>
>Consultez la rubrique « Langage des signets » dans la section [Guide de référence du service Assembler et de DDX](https://www.adobe.com/go/learn_aemforms_ddx_63).

**Ajouter le document PDF et le document XML de signet à une collection Map**

Ajoutez le document PDF auquel les signets sont ajoutés et le document XML du signet à la collection Map. En toute logique, l’objet de collection Map contient deux éléments : un document PDF et le document XML de signet.

**Définir les options d’exécution**

Vous pouvez définir des options d’exécution qui contrôlent le comportement du service Assembler lors de l’exécution d’une tâche. Par exemple, vous pouvez définir une option qui indique au service Assembler de continuer à traiter une tâche même en cas d’erreur. Pour plus d’informations sur les options d’exécution que vous pouvez définir, consultez la référence de classe `AssemblerOptionSpec` dans la section [Référence de l’API AEM Forms](https://www.adobe.com/go/learn_aemforms_javadocs_63_en).

**Assembler le document PDF**

Pour assembler un document PDF contenant de nouveaux signets, utilisez l’opération `invokeDDX` du service Assembler. La raison pour laquelle vous devez utiliser l’opération `invokeDDX` plutôt que dʼautres opérations du service Assembler telles que `invokeOneDocument` est que le service Assembler requiert un document XML de signet qui est transmis dans l’objet de collection Map. Cet objet est un paramètre de l’opération `invokeDDX`.

**Enregistrer le document PDF contenant des signets**

Extrayez les résultats de l’objet map renvoyé, puis enregistrez le document PDF correspondant. (Reportez-vous à « Extraire les résultats » dans [Assembler des documents PDF par programmation](/help/forms/developing/programmatically-assembling-pdf-documents.md).)

**Voir également**

[Inclusion des fichiers de bibliothèque Java d’AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

[Assembler les documents PDF par programmation](/help/forms/developing/programmatically-assembling-pdf-documents.md)

## Assembler des documents PDF avec des signets à l’aide de l’API Java {#assemble-pdf-documents-with-bookmarks-using-the-java-api}

Pour assembler un document PDF avec des signets à l’aide de l’API du service Assembler (Java), procédez comme suit :

1. Incluez les fichiers de projet.

   Incluez les fichiers JAR clients, tels que adobe-assembler-client.jar, dans le chemin d’accès aux classes de votre projet Java.

1. Créez un client Assembler PDF.

   * Créez un objet `ServiceClientFactory` qui contient des propriétés de connexion. (Voir [Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties).)
   * Créez un objet `AssemblerServiceClient` en utilisant son constructeur et en transmettant l’objet `ServiceClientFactory`.

1. Référencez un document DX existant.

   * Créez un objet `java.io.FileInputStream` qui représente le document DDX en utilisant son constructeur et en transmettant une valeur de chaîne qui spécifie l’emplacement du fichier DDX.
   * Créez un objet `com.adobe.idp.Document` en utilisant son constructeur et en transmettant l’objet `java.io.FileInputStream`. 

1. Référencez un document PDF auquel des signets sont ajoutés.

   * Créez un objet `java.io.FileInputStream` en utilisant son constructeur et en transmettant l’emplacement du document PDF.
   * Créez un objet `com.adobe.idp.Document` en utilisant son constructeur et en transmettant l’objet `java.io.FileInputStream` contenant le document PDF.

1. Référencez le document XML du signet.

   * Créez un objet `java.io.FileInputStream` en utilisant son constructeur et en transmettant l’emplacement du fichier XML qui représente le document XML du signet.
   * Créez un objet `com.adobe.idp.Document` et transmettez l’objet `java.io.FileInputStream` contenant le document PDF.

1. Ajoutez le document PDF et le document XML du signet à une collection Map.

   * Créez un objet `java.util.Map` qui permet de stocker le document PDF d’entrée et le document XML de signet.
   * Ajoutez le document PDF d’entrée en appelant la méthode `put` de l’objet `java.util.Map` et en transmettant les arguments suivants :

      * Une valeur de chaîne qui représente le nom de la clé. Cette valeur doit correspondre à celle de l’élément source PDF spécifié dans le document DDX.
      * Un objet `com.adobe.idp.Document` contenant le document PDF d’entrée.

   * Ajoutez le document XML de signet en appelant la méthode `put` de l’objet `java.util.Map` et en transmettant les arguments suivants :

      * Une valeur de chaîne qui représente le nom de la clé. Cette valeur doit correspondre à la valeur de l’élément source Bookmarks spécifié dans le document DDX.
      * Un objet `com.adobe.idp.Document` contenant le document XML de signet.

1. Définissez les options d’exécution.

   * Créez un objet `AssemblerOptionSpec` qui stocke les options d’exécution en utilisant son constructeur.
   * Définissez les options d’exécution pour répondre à vos exigences professionnelles en appelant une méthode appartenant à l’objet `AssemblerOptionSpec`. Par exemple, pour demander au service Assembler de continuer à traiter une tâche en cas d’erreur, appelez la méthode `setFailOnError` de l’objet `AssemblerOptionSpec` et transmettez `false`.

1. Assemblez le document PDF.

   Appelez la méthode `invokeDDX` de lʼobjet `AssemblerServiceClient` et transmettez les valeurs requises suivantes :

   * Un objet `com.adobe.idp.Document` représentant le document DDX à utiliser.
   * Un objet `java.util.Map` contenant le document PDF d’entrée et le document XML de signet.
   * Un objet `com.adobe.livecycle.assembler.client.AssemblerOptionSpec` spécifiant les options d’exécution, y compris la police par défaut et le niveau du log de traitement.

   La méthode `invokeDDX` renvoie un objet `com.adobe.livecycle.assembler.client.AssemblerResult` contenant les résultats de la tâche et les exceptions survenues.

1. Enregistrez le document PDF qui contient des signets.

   Pour obtenir le document PDF nouvellement créé, procédez comme suit :

   * Appelez la méthode `getDocuments` de lʼobjet `AssemblerResult`. Celle-ci renvoie un objet `java.util.Map`.
   * Effectuez une itération au sein de l’objet `java.util.Map` jusqu’à ce que vous trouviez l’objet `com.adobe.idp.Document` résultant. (Vous pouvez utiliser l’élément de résultat PDF spécifié dans le document DDX pour obtenir le document).
   * Appelez la méthode `copyToFile` de l’objet `com.adobe.idp.Document` pour extraire le document PDF.

**Voir également**

[Démarrage rapide (mode SOAP) : assembler des documents PDF avec des signets à l’aide de l’API Java.](/help/forms/developing/assembler-service-java-api-quick.md#quick-start-soap-mode-assembling-pdf-documents-with-bookmarks-using-the-java-api)

[Inclusion des fichiers de bibliothèque Java d’AEM Forms](/help/forms/developing/invoking-aem-forms-using-java.md#including-aem-forms-java-library-files)

[Réglage des propriétés de la connexion](/help/forms/developing/invoking-aem-forms-using-java.md#setting-connection-properties)

## Assembler des documents PDF avec des signets à l’aide de l’API de service web {#assemble-pdf-documents-with-bookmarks-using-the-web-service-api}

Assemblez un document PDF avec des signets à l’aide de l’API du service Assembler (service web) :

1. Incluez les fichiers de projet.

   Créez un projet Microsoft .NET qui utilise MTOM. Veillez à utiliser la définition WSDL suivante : `http://localhost:8080/soap/services/AssemblerService?WSDL&lc_version=9.0.1`.

   >[!NOTE]
   >
   >Remplacez `localhost` par l’adresse IP du serveur hébergeant AEM Forms.

1. Créez un client Assembler PDF.

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

   * Créez un objet `BLOB` en utilisant son constructeur. L’objet `BLOB` est utilisé pour stocker le document DDX.
   * Créez un objet `System.IO.FileStream` en appelant son constructeur et en transmettant une valeur de chaîne qui représente l’emplacement du document DDX et son mode d’ouverture.
   * Créez un tableau d’octets qui stocke le contenu de l’objet `System.IO.FileStream`. Vous pouvez déterminer la taille du tableau d’octets en obtenant la propriété `Length` de l’objet `System.IO.FileStream`.
   * Renseignez le tableau d’octets avec les données de flux en appelant la méthode `Read` de l’objet `System.IO.FileStream` et en transmettant le tableau d’octets, la position de départ et la longueur du flux à lire.
   * Renseignez l’objet `BLOB` en attribuant à son champ `MTOM` le contenu du tableau d’octets.

1. Référencez un document PDF auquel des signets sont ajoutés.

   * Créez un objet `BLOB` en utilisant son constructeur. L’objet `BLOB` sert à stocker le PDF d’entrée.
   * Créez un objet `System.IO.FileStream` en appelant son constructeur et en transmettant une valeur de chaîne qui représente l’emplacement du document PDF d’entrée et son mode d’ouverture.
   * Créez un tableau d’octets qui stocke le contenu de l’objet `System.IO.FileStream`. Vous pouvez déterminer la taille du tableau d’octets en obtenant la propriété `Length` de l’objet `System.IO.FileStream`.
   * Renseignez le tableau d’octets avec les données de flux en appelant la méthode `Read` de l’objet `System.IO.FileStream` et en transmettant le tableau d’octets, la position de départ et la longueur du flux à lire.
   * Renseignez l’objet `BLOB` en attribuant à son champ `MTOM` le contenu du tableau d’octets.

1. Référencez le document XML du signet.

   * Créez un objet `BLOB` en utilisant son constructeur. L’objet `BLOB` sert à stocker le document XML du signet.
   * Créez un objet `System.IO.FileStream` en appelant son constructeur et en transmettant une valeur de chaîne qui représente l’emplacement du document PDF d’entrée et son mode d’ouverture.
   * Créez un tableau d’octets qui stocke le contenu de l’objet `System.IO.FileStream`. Vous pouvez déterminer la taille du tableau d’octets en obtenant la propriété `Length` de l’objet `System.IO.FileStream`.
   * Renseignez le tableau d’octets avec les données de flux en appelant la méthode `Read` de l’objet `System.IO.FileStream` et en transmettant le tableau d’octets, la position de départ et la longueur du flux à lire.
   * Renseignez l’objet `BLOB` en attribuant à son champ `MTOM` le contenu du tableau d’octets.

1. Ajoutez le document PDF et le document XML du signet à une collection Map.

   * Créez un objet `MyMapOf_xsd_string_To_xsd_anyType`. Cet objet de collection est utilisé pour stocker les documents PDF d’entrée et le document XML du signet.
   * Pour chaque document PDF d’entrée et le document XML de signet, créez un objet `MyMapOf_xsd_string_To_xsd_anyType_Item`.
   * Attribuez une valeur de chaîne qui représente le nom de la clé au champ `key` de l’objet `MyMapOf_xsd_string_To_xsd_anyType_Item`. Cette valeur doit correspondre à celle de l’élément source PDF spécifié dans le document DDX.
   * Affectez l’objet `BLOB` qui stocke le document PDF au champ `value` de l’objet `MyMapOf_xsd_string_To_xsd_anyType_Item`.
   * Ajoutez l’objet `MyMapOf_xsd_string_To_xsd_anyType_Item` à l’objet `MyMapOf_xsd_string_To_xsd_anyType`. Appelez la méthode `Add` de l’objet `MyMapOf_xsd_string_To_xsd_anyType` et transmettez l’objet `MyMapOf_xsd_string_To_xsd_anyType`. (Effectuez cette tâche pour chaque document PDF d’entrée et le document XML de signet).

1. Définissez les options d’exécution.

   * Créez un objet `AssemblerOptionSpec` qui stocke les options d’exécution en utilisant son constructeur.
   * Définissez les options d’exécution pour répondre à vos exigences professionnelles en attribuant une valeur à un membre de données qui appartient à l’objet `AssemblerOptionSpec`. Par exemple, pour demander au service Assembler de continuer à traiter une tâche en cas d’erreur, affectez `false` au membre de données `failOnError` de l’objet `AssemblerOptionSpec`.

1. Assemblez le document PDF.

   Appelez la méthode `invokeDDX` de l’objet `AssemblerServiceClient` et transmettez les valeurs suivantes :

   * Un objet `BLOB` qui représente le document DDX.
   * Le tableau `MyMapOf_xsd_string_To_xsd_anyType` qui contient les documents d’entrée.
   * Un objet `AssemblerOptionSpec` qui spécifie les options d’exécution.

   La méthode `invokeDDX` renvoie un objet `AssemblerResult` qui contient les résultats de la tâche et les exceptions survenues.

1. Enregistrez le document PDF qui contient des signets.

   Pour obtenir le document PDF nouvellement créé, procédez comme suit :

   * Accédez au champ `documents` de lʼobjet `AssemblerResult`, qui est un objet `Map` contenant les documents PDF obtenus.
   * Effectuez une itération au sein de l’objet `Map` jusqu’à ce que vous trouviez la clé correspondant au nom du document généré. Convertissez ensuite la `value` de ce ou cette membre de tableau en `BLOB`.
   * Procédez à lʼextraction des données binaires qui représentent le document PDF en accédant au champ `MTOM` de son objet `BLOB`. Cette opération renvoie un tableau d’octets que vous pouvez enregistrer dans un fichier PDF.

**Voir également**

[Appeler AEM Forms en utilisant MTOM](/help/forms/developing/invoking-aem-forms-using-web.md#invoking-aem-forms-using-mtom)
